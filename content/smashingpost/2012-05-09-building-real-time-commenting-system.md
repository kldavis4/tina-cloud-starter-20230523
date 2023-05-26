---
title: How To Build A Real-Time Commenting System
slug: building-real-time-commenting-system
image: null
date: 2012-05-09T10:56:12.000Z
author: phil-leggetter
description: >-
  The Web has become increasingly interactive over the years. This trend is set to continue with the next generation of applications driven by the **real-time
  Web**.
categories:
  - Coding
  - CSS
  - JavaScript
  - HTML5
  - HTML
---
Adding real-time functionality to an application can result in a more interactive and engaging user experience. However, setting up and maintaining the server-side real-time components can be an unwanted distraction. But don't worry, there is a solution.

Cloud hosted Web services and APIs have come to the rescue of many a developer over the past few years, and real-time functionality is no different. The focus at <a href="https://pusher.com">Pusher</a>, for example, is to let you concentrate on building your real-time Web applications by offering a hosted API which makes it quick and easy to add scalable real-time functionality to Web and mobile apps.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Improve User Experience With Real-Time Features](https://www.smashingmagazine.com/2016/04/improve-user-experience-real-time-features/)
*   [Real-Time Data And A More Personalized Web](https://www.smashingmagazine.com/2011/04/real-time-data-and-a-more-personalized-web/)
*   [Building A Real-Time Retrospective Board With Video Chat](https://www.smashingmagazine.com/2016/03/building-a-real-time-retrospective-board-with-video-chat/)
*   [Where Have All The Comments Gone?](https://www.smashingmagazine.com/2010/11/critical-thinking-vs-critical-acclaim-where-have-all-the-comments-gone/)

In this tutorial, I'll show how to convert a basic blog commenting system into a real-time engaging experience where you'll see a comment made in one browser window "magically" appear in a second window.

{{% feature-panel %}}

## Why Should We Care About The Real-Time Web?

Although <a href="https://en.wikipedia.org/wiki/Real-time_web">the Real-Time Web</a> is a relatively recent mainstream phrase, real-time Web technologies have been around for over 10 years. They were mainly used by companies building software targeted at the financial services sector or in Web chat applications. These initial solutions were classed as "hacks". In 2006 these solutions were given an umbrella term called <a href="https://en.wikipedia.org/wiki/Comet_(programming)">Comet</a>, but even with a defined name the solutions were still considered hacks. <strong>So, what's changed?</strong>

In my opinion there are a number of factors that have moved real-time Web technologies to the forefront of Web application development.</p>

### Social Media Data

Social media, and specifically Twitter, has meant that more and more data is becoming instantly available. Gone are the days where we have to wait an eternity for Google to find our data (blog posts, status updates, images). There are now platforms that not only make our data instantly discoverable but also instantly deliver it to those who have declared an interest. This idea of <a href="https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern">Publish/Subscribe</a> is core to the real-time Web, especially when building Web applications.</p>

### Increased User Expectations

As more users moved to using applications such as Twitter and Facebook, and the user experiences that they deliver, their perception of what can be expected from a Web application changed. Although applications had become more dynamic through the use of JavaScript, the experiences were seldom truly interactive. Facebook, with it's real-time wall (and later other realtime features) and Twitter with it's activity stream centric user interface, and focus on conversation, demonstrated how Web applications could be highly engaging.</p>

### WebSockets

<img class="119588" title="HTML5 Logo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd210513-101a-445f-99f3-1fad7e5cdca0/html5-logo-256.png" alt="HTML5 and WebSockets Rock!" width="256" height="256" />

Earlier on I stated that previous solutions to let servers instantly push data to Web browsers were considered "hacks". But this didn't remove the fact that there was a requirement to be able to do this in a cross-browser and standardised way. Our prayers have finally been answered with <strong>HTML5</strong> WebSockets. WebSockets represent a <a href="https://www.w3.org/TR/websockets/">stardardized API</a> and <a href="https://tools.ietf.org/html/rfc6455">protocol</a> that allows realtime server and client (web browser) two way communication over a single connection. Older solutions could only achieve two-way communication using two connections so the fact the WebSockets use a single connection is actually a big deal. It can be a massive resource saving to the server and client, with the latter being particularly important for mobile devices where battery power is extremely valuable.</p>

### How are Real-Time Technologies being used?

Real-time Web technologies are making it possible to build all sorts of engaging functionality, leading to improved user experiences. Here are a handful of common use cases:

*   **Realtime Stats** - The technology was first used in finance to show stock exchange information so it's no surprise that the technology is now used more than ever. It's also highly beneficial to sports, betting and analytics.
*   **Notifications** - when something a user is interested in becomes available or changes.
*   **Activity Streams** - streams of friend or project activity. This is commonly seen in apps like Twitter, Facebook, Trello, Quora and many more.
*   **Chat** - the 101 or real-time Web technology but still a very valuable function. It helps delivery instant interaction between friends, work colleagues, customers and customer service etc.
*   **Collaboration** - Google docs offers this kind of functionality within its docs, spreadsheets and drawing applications and we're going to see similar use cases in many more applications.
*   **Multiplayer Games** - The ability to instantly deliver player moves, game state changes and score updates is clearly important to multiplayer gaming.

In the rest of this tutorial I'll cover building a basic blog commenting system, how to progressively enhance it using jQuery and finally I'll also progressively enhance it using the real-time Web service I work for, Pusher, which will demonstrate not just how easy it can be to use real-time Web technology, but also the value and increased engagement that a real-time factor can introduce.</p>

## Creating Generic Blog Commenting System

### Start from a Template

I want to focus on adding real-time commenting to a blog post so <strong>let's start from a <a href="https://github.com/pusher/realtime-commenting/zipball/start">template</a></strong>.

This template re-uses the HTML5 layout defined in the post on <a href="https://www.smashingmagazine.com/2009/08/04/designing-a-html-5-layout-from-scratch/">Coding An HTML 5 Layout From Scratch</a> and the file structure we'll start with is as follows (with some additions that we don't need to worry about at the moment):

*   css (dir)
    *   global-forms.css
    *   main.css
    *   reset.css
*   images (dir)
*   index.php

### HTML

The template HTML, found in <em>index.php</em>, has been changed from the HTML5 Layout article to focus on the content being a blog post with comments. You can view the HTML source <a href="https://github.com/pusher/realtime-commenting/blob/start/index.php">here</a>.

The main elements to be aware of are:

*   `<section id="content">` - the blog post content
*   `<section id="comments">` - where the comments are to appear. This is where the majority of our work will be done

### Comments

Now that we've got the HTML in place for our blog post and for displaying the comments we also need a way for our readers to submit comments, so let's add a <code>&lt;form&gt;</code> element to collect and submit the comment details to <em>post_comment.php</em>. We'll add this at the end of the <code>&lt;section id="comments"&gt;</code> section wrapped in a <code>&lt;div id="respond"&gt;</code>.

<pre><code class="language-markup tmp-html">&lt;div id="respond"&gt;

  &lt;h3&gt;Leave a Comment&lt;/h3&gt;

  &lt;form action="post_comment.php" method="post" id="commentform"&gt;

    &lt;label for="comment_author" class="required"&gt;Your name&lt;/label&gt;
    &lt;input type="text" name="comment_author" id="comment_author" value="" tabindex="1" required="required"&gt;

    &lt;label for="email" class="required"&gt;Your email;&lt;/label&gt;
    &lt;input type="email" name="email" id="email" value="" tabindex="2" required="required"&gt;

    &lt;label for="comment" class="required"&gt;Your message&lt;/label&gt;
    &lt;textarea name="comment" id="comment" rows="10" tabindex="4"  required="required"&gt;&lt;/textarea&gt;

    &lt;-- comment_post_ID value hard-coded as 1 --&gt;
    &lt;input type="hidden" name="comment_post_ID" value="1" id="comment_post_ID" /&gt;
    &lt;input name="submit" type="submit" value="Submit comment" /&gt;

  &lt;/form&gt;

&lt;/div&gt;</code></pre>

### Comment Form CSS

Let's apply some CSS to make things look a bit nicer by adding the following to <em>main.css</em>:

<pre><code class="language-css">#respond {
  margin-top: 40px;
}

#respond input[type='text'],
#respond input[type='email'],
#respond textarea {
  margin-bottom: 10px;
  display: block;
  width: 100%;

  border: 1px solid rgba(0, 0, 0, 0.1);
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -o-border-radius: 5px;
  -ms-border-radius: 5px;
  -khtml-border-radius: 5px;
  border-radius: 5px;

  line-height: 1.4em;
}</code></pre>

Once the HTML structure, the comment form and the CSS are in place our blogging system has started to look a bit more presentable.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2323eb83-f51f-435d-ad4b-5750d5c8dcb6/blog-and-comments.png" alt="Screenshot of blog post and commenting system" width="500" />

### Handling Comment Submission

The next step is to write the PHP form submission handler which accepts the request and stores the comment, <em>post_comment.php</em>. You should create this file in the root of your application.

As I said earlier I'm keen to focus on the real-time functionality so a class exists within the template that you've downloaded which encapsulate some of the standard data checking and persistence functionality. This class is defined in <em>Persistence.php</em> (you can view the source <a href="https://github.com/pusher/realtime-commenting/blob/start/Persistence.php">here</a>), is in no way production quality, and handles:

*   Basic validation
*   Basic data sanitization
*   Very simple persistence using a user `$_SESSION`. This means that a comment saved by one user will not be available to another user.

This also means that we don't need to spend time setting up a database and all that goes with it and makes <em>post_comment.php</em> very simple an clean. If you wanted to use this functionality in a production environment you would need to re-write the contents of <em>Persistence.php</em>. Here's the code for <em>post_comment.php</em>.

<pre><code class="language-php">&lt;?php
require('Persistence.php');

$db = new Persistence();
if( $db-&gt;add_comment($_POST) ) {
  header( 'Location: index.php' );
}
else {
  header( 'Location: index.php?error=Your comment was not posted due to errors in your form submission' );
}
?&gt;</code></pre>

The above code does the following:

1.  Includes the _Persistence.php_ class which handles saving and fetching comments.
2.  Creates a new instances of the `Persistence` object and assigns it to the variable `$db`.
3.  Tries to add the comment to the `$db`. If the comment is successfully added it redirects back to the blog post. If it fails the redirection also occurs but some error text is appended to an _error_ query parameter.</p>

### Displaying the Comments with the Blog Post

The final thing we need to do to have our Generic Blog Commenting System up and running is to update the blog page, <em>index.php</em>, to fetch and display the comments from the <code>Persistence</code> object.

*   Since this isn't a real blogging system we'll hard code the `$comment_post_ID` value to be `1`.
*   Include the _Persistence.php_ class and fetch the comments from it. Comments are associated with a blog post using a unique `$comment_post_ID`.

<pre><code class="language-php">&lt;?php
require('Persistence.php');
$comment_post_ID = 1;
$db = new Persistence();
$comments = $db-&gt;get_comments($comment_post_ID);
$has_comments = (count($comments) &gt; 0);
?&gt;</code></pre>

Since we now have the <code>$comment_post_ID</code> accessible via PHP we should update the HTML for the comment form to use this value.

<pre><code class="language-php">&lt;input type="hidden" name="comment_post_ID" value="&lt;?php echo($comment_post_ID); ?&gt;" id="comment_post_ID" /&gt;</code></pre>

We now have all the comments related to the blog post referenced by the <code>$comments</code> variable we need to display them on the page. To do this we need to update the PHP in <em>index.php</em> to iterate through them and create the required HTML.

<pre><code class="language-php">&lt;ol id="posts-list" class="hfeed&lt;?php echo($has_comments?' has-comments':’); ?&gt;"&gt;
  &lt;li class="no-comments"&gt;Be the first to add a comment.&lt;/li&gt;
  &lt;?php
    foreach ($comments as $comment) {
      ?&gt;
      &lt;li&gt;&lt;article id="comment_&lt;?php echo($comment['id']); ?&gt;" class="hentry"&gt;
        &lt;footer class="post-info"&gt;
          &lt;abbr class="published" title="&lt;?php echo($comment['date']); ?&gt;"&gt;
            &lt;?php echo( date('d F Y', strtotime($comment['date']) ) ); ?&gt;
          &lt;/abbr&gt;

          &lt;address class="vcard author"&gt;
            By &lt;a class="url fn" href="#"&gt;&lt;?php echo($comment['comment_author']); ?&gt;&lt;/a&gt;
          &lt;/address&gt;
        &lt;/footer&gt;

        &lt;div class="entry-content"&gt;
          &lt;p&gt;&lt;?php echo($comment['comment']); ?&gt;&lt;/p&gt;
        &lt;/div&gt;
      &lt;/article&gt;&lt;/li&gt;
      &lt;?php
    }
  ?&gt;
&lt;/ol&gt;</code></pre>

You'll notice that if the value of <code>$has_comments</code> is true an additional CSS class is applied to the ordered list called <em>has-comments</em>. This is so we can hide the list item with the "Be the first to add a comment" message when comments are being displayed using CSS:

<pre><code class="language-css">#posts-list.has-comments li.no-comments {
  display: none;
}</code></pre>

Now that all this is in place we have a functional blog commenting system. If you would like to start writing your code from this basic functioning blog commenting system you can also <a href="https://github.com/pusher/realtime-commenting/zipball/basic">download the code completed up to here</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15351086-1023-4f7d-8c34-ac4a56b782ed/functioning-comments.png" alt="Screenshot of the functioning blog commenting system" width="500" />

## Progressive Enhancement With jQuery

The first step in making our blog commenting system feel less like a Web page and more like an application is to stop page reloads when a user submits a comment. We can do this by submitting the comments to the server using an AJAX request. Since jQuery is probably the defacto standard for cross browser JavaScript functionality we'll use it here. Although I'm using jQuery here, I'd also like to highlight that it's a good idea to <a href="https://www.leggetter.co.uk/2012/02/19/jquery-uk-2012-event-dont-always-use-jquery.html">not always use jQuery</a>. Instead, analyze your scenario and make a considered decision because there are <a href="https://www.leggetter.co.uk/2012/02/12/considerations-when-updating-the-dom-to-display-realtime-data.html">some cases</a> where you are best not to.

In an attempt to try and keep as much scripting (PHP and JavaScript) from the <em>index.php</em> file we'll create a new folder for our JavaScript and in there a file for our application JavaScript. The path to this fill should be <em>js/app.js</em>. This file should be included after the jQuery include.

<pre><code class="language-markup tmp-html">&lt;script src="https://code.jquery.com/jquery-1.7.1.min.js"&gt;&lt;/script&gt;
&lt;script src="js/app.js"&gt;&lt;/script&gt;</code></pre>

### Capture the Comment Form Submission

When the page is ready bind to the <code>submit</code> event of the form.

<pre><code class="language-javascript">$(function() {
  $('#commentform').submit(handleSubmit);
});</code></pre>

When the form is submitted and the <code>handleSubmit</code> function is called the comment data we want to send to the server is extracted from the form. There are more elegant ways of fetching the data from the form but this approach clearly shows where we're getting the values from and the <code>data</code> object we are creating.

<pre><code class="language-javascript">function handleSubmit() {
  var form = $(this);
  var data = {
    "comment_author": form.find('#comment_author').val(),
    "email": form.find('#email').val(),
    "comment": form.find('#comment').val(),
    "comment_post_ID": form.find('#comment_post_ID').val()
  };

  postComment(data);

  return false;
}

function postComment(data) {
  // send the data to the server
}</code></pre>

### POST the Comment with AJAX

Within the <code>postComment</code> function make a <em>POST</em> request to the server passing the data that we've retrieved from the form. When the request is made an additional HTTP header will be sent to identify the request as being an AJAX request. We want to do this so that we can return a JSON response if it is an AJAX request and maintain our basic functionality if it isn't (for more information on this see <a href="https://www.learningjquery.com/2010/03/detecting-ajax-events-on-the-server">Detected AJAX events on the Server</a>). We also define two handlers; <code>postSuccess</code> for handling the comment being successfully stored and <code>postError</code> to handle any failures.

<pre><code class="language-javascript">function postComment(data) {
  $.ajax({
    type: 'POST',
    url: 'post_comment.php',
    data: data,
    headers: {
      'X-Requested-With': 'XMLHttpRequest'
    },
    success: postSuccess,
    error: postError
  });
}

function postSuccess(data, textStatus, jqXHR) {
  // add comment to UI
}

function postError(jqXHR, textStatus, errorThrown) {
  // display error
}</code></pre>

### Dynamically Updating the User Interface with the Comment

At this point the comment data is being sent to the server and saved, but the AJAX response isn't providing any meaningful response. Also, the comments section isn't being updated to show the newly submitted comment so the user would have to refresh the page to see it. Let's start by writing the code to update the UI and test that functionality.

If you are thinking "Hang on a minute! We don't have all the data we need from the Web server to display the comment" then you are correct. However, this doesn't stop us writing the code to update the UI and also testing that it works. Here's how:

<pre><code class="language-javascript">function postSuccess(data, textStatus, jqXHR) {
  $('#commentform').get(0).reset();
  displayComment(data);
}

function displayComment(data) {
  var commentHtml = createComment(data);
  var commentEl = $(commentHtml);
  commentEl.hide();
  var postsList = $('#posts-list');
  postsList.addClass('has-comments');
  postsList.prepend(commentEl);
  commentEl.slideDown();
}

function createComment(data) {
  var html = ’ +
  '&lt;li&gt;&lt;article id="' + data.id + '" class="hentry"&gt;' +
    '&lt;footer class="post-info"&gt;' +
      '&lt;abbr class="published" title="' + data.date + '"&gt;' +
        parseDisplayDate(data.date) +
      '&lt;/abbr&gt;' +
      '&lt;address class="vcard author"&gt;' +
        'By &lt;a class="url fn" href="#"&gt;' + data.comment_author + '&lt;/a&gt;' +
      '&lt;/address&gt;' +
    '&lt;/footer&gt;' +
    '&lt;div class="entry-content"&gt;' +
      '&lt;p&gt;' + data.comment + '&lt;/p&gt;' +
    '&lt;/div&gt;' +
  '&lt;/article&gt;&lt;/li&gt;';

  return html;
}

function parseDisplayDate(date) {
  date = (date instanceof Date? date : new Date( Date.parse(date) ) );
  var display = date.getDate() + ' ' +
                ['January', 'February', 'March',
                 'April', 'May', 'June', 'July',
                 'August', 'September', 'October',
                 'November', 'December'][date.getMonth()] + ' ' +
                date.getFullYear();
  return display;
}</code></pre>

The code above does the following:

*   Within the `postSuccess` function we clear the form values and call `displayComment`.
*   `displayComment` first calls the `createComment` function to create the list item (`<li>`) HTML as a `String`.
*   We then convert the HTML to a jQuery object using `$(commentHtml)` and hide the element.
*   The comment list item is then prepended to the comments ordered list (`<ol>`). The list also has a class called _has-comments_ added to it so we can hide the first list item which contains the "Be the first to comment" statement.
*   Finally, we call `commentEl.slideDown()` so that the comment is shown in what is becoming the standard "here's a new item" way.

The functionality is now implemented but we want to test it out. This can be achieved in two ways:

*   The `displayComment` is a global function so we can call it directly using the JavaScript console of the browser.
*   We can bind to an event on the page that triggers a fake update which calls the `displayComment` function

Let's go with the latter and bind to the <em>"u"</em> key being released by binding to the <code>keyup</code> event. When it is, we'll create a fake <code>data</code> object containing all the information required to create a new comment and pass it to the <code>displayComment</code> function. That comment will then be displayed in the UI.

Hit the <em>"u"</em> key a few times and see the comments appear.

<pre><code class="language-javascript">$(function() {

  $(document).keyup(function(e) {
    e = e || window.event;
    if(e.keyCode === 85){
      displayComment({
        "id": "comment_1",
        "comment_post_ID": 1,
        "date":"Tue, 21 Feb 2012 18:33:03 +0000",
        "comment": "The realtime Web rocks!",
        "comment_author": "Phil Leggetter"
      });
    }
  });

});</code></pre>

Great! We now know that our <code>displayComment</code> function works exactly as we expect it to. <strong>Remember to remove the test function</strong> before you go live or you'll really confuse your user every time they press <em>"u"</em>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f858016-b271-4c84-90bd-27edbe232fc7/fake-comments1.png" alt="Screenshot of a bunch of fake comments" width="500" />

### Detect and Responding to the AJAX request

All that's left to do is update the <em>post_comment.php</em> file to detect the AJAX call and return information about the newly created comment.

Detecting the AJAX request is done by checking for the <code>X-Requested-With</code> header:

<pre><code class="language-php">$ajax = ($_SERVER[ 'HTTP_X_REQUESTED_WITH' ] === 'XMLHttpRequest');</code></pre>

Once we know the request is an AJAX request we can update the code to respond with an appropriate status code and the data representing the comment. We also need to ensure that the original functionality is maintained. The <em>post_comment.php</em> code now looks as follows:

<pre><code class="language-php">&lt;?php
require('Persistence.php');

$ajax = ($_SERVER[ 'HTTP_X_REQUESTED_WITH' ] === 'XMLHttpRequest');

$db = new Persistence();
$added = $db-&gt;add_comment($_POST);

if($ajax) {
  sendAjaxResponse($added);
}
else {
  sendStandardResponse($added);
}

function sendAjaxResponse($added) {
  header("Content-Type: application/x-javascript");
  if($added) {
    header( 'Status: 201' );
    echo( json_encode($added) );
  }
  else {
    header( 'Status: 400' );
  }
}

function sendStandardResponse($added) {
  if($added) {
    header( 'Location: index.php' );
  }
  else {
    header( 'Location: index.php?error=Your comment was not posted due to errors in your form submission' );
  }
}
?&gt;</code></pre>

Key points from the above code are:

*   The `$db->add_comment($_POST)` call returns the data from the added comment which is assigned to the `$added` variable.
*   By setting the response _Content-Type_ to "application/json" we tell jQuery to convert the returned string into a JavaScript object. For more information on calling JSON Web services see [A Beginner’s Guide To jQuery-Based JSON API Clients](https://www.smashingmagazine.com/2012/02/09/beginners-guide-jquery-based-json-api-clients/).
*   The _201_ status code indicates a successful call and also that a resource (the comment) was created by the call.

The blog commenting system now works in a much more dynamic way, instantly showing the user that their comment has been posted without refreshing the page. In addition, the way the we've added the JavaScript based functionality to the page means that if JavaScript is disabled or a JavaScript file fails to load that the system will fallback to the standard functionality we first implemented.</p>

## Getting Real-Time—Finally!

As with any "from scratch" tutorial it can take a bit of time to get to the <strong>really</strong> interesting part, but we're finally here. However, <strong>all the work we've up in has been worth it</strong>. Because we've built our commenting system up in a progressively enhanced way, plugging Pusher into it is going to be really easy

### What is Pusher?

At the start of the tutorial we said that we would use Pusher to add the realtime functionality to the application. But what is Pusher?

Pusher is a hosted service for quickly and easily adding realtime features into Web and mobile applications. It offers a RESTful API that makes it really easy to publish events from any application that can make a HTTP request and a WebSocket API for realtime bi-directional communication. You don't even need to use the APIs directly as there are <a href="https://pusher.com/docs/rest_libraries">server</a> (PHP, Ruby, node.js, ASP.NET, Python and more) and <a href="https://pusher.com/docs/client_libraries">client</a> (JavaScript, iOS, Android, .NET, ActionScript, Arduino and more) libraries available in a host of technologies which means you can add realtime functionality to an app within minutes ‐ I'm confident you'll be surprised just how easy!

### Sign up for Pusher and get your API Credentials

In order to add Pusher-powered real-time functionality to a Web application you first need to <a href="https://pusher.com/signup">sign up for a free Sandbox account</a>. After you have signed up you'll be taken to the Pusher dashboard where you'll see that a "Main" application has been created for you. You'll also see you are in the "API Access" section for that application where you can grab your API credentials.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b1a193-f5ee-47d6-b0f0-8a3bd8162d49/pusher-main-api-access.png" alt="Screenshot of API Access section in Pusher Dashboard" width="500" />

For ease of access create a <em>pusher_config.php</em> file and <code>define</code> the credentials in there so we can refer to them later:

<pre><code class="language-php">&lt;?php
define('APP_ID', 'YOUR_APP_ID');
define('APP_KEY', 'YOUR_APP_KEY');
define('APP_SECRET', 'YOUR_APP_SECRET');
?&gt;</code></pre>

In your version of <em>pusher_config.php</em> be sure to replace the values which being <em>'YOUR_</em> with your actual credentials.

You should also <code>require</code> this in your <em>index.php</em> file. We should also make the <code>APP_KEY</code> available to the JavaScript runtime as we are going to need it to connect to Pusher.

<pre><code class="language-php">&lt;?php
require('pusher_config.php);
?&gt;

&lt;script&gt;
var APP_KEY = '&lt;?php echo(APP_KEY); ?&gt;';
&lt;/script&gt;</code></pre>

### Real-time JavaScript

The first thing you need to do when adding Pusher to a Web application is include the Pusher JavaScript library and connect to Pusher. To connect you'll need to use the <em>key</em> which you grabbed from the Pusher dashboard. Below you can see all that is required to hook up the front-end application to Pusher.

Include the Pusher JavaScript library after the <em>app.js</em> include:

<pre><code class="language-markup tmp-html">&lt;script src="https://code.jquery.com/jquery-1.7.1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://js.pusher.com/1.11/pusher.min.js"&gt;&lt;/script&gt;
&lt;script src="js/app.js"&gt;&lt;/script&gt;</code></pre>

Add the Pusher functionality to <em>app.js</em>:

<pre><code class="language-javascript">var pusher = new Pusher(APP_KEY);
var channel = pusher.subscribe('comments-' + $('#comment_post_ID').val());
channel.bind('new_comment', displayComment);</code></pre>

This probably looks too easy to be true, so here are the details about what the above code does:

*   `var pusher = new Pusher(APP_KEY);` Creates a new instance of a `Pusher` object and in doing so connects you to Pusher. The application to use is defined by the `APP_KEY` value that you pass in and that we set up earlier.
*   `var channel = pusher.subscribe('comments-' + $('#comment_post_ID').val());` [Channels](https://pusher.com/docs/channels) provide a great way of organizing streams of real-time data. Here we are subscribing to comments for the current blog post, uniquely identified by the value of the `comment_post_ID` hidden form input element.
*   `channel.bind('new_comment', displayComment);` [Events](https://pusher.com/docs/client_api_guide/client_events) are used to further filter data and are ideal for linking updates to changes in the UI. In this case we want to bind to an event which is triggered whenever a new comment is added and display it. Because we've already created the `displayComment` function we can just pass in a reference to the call to `bind`.</p>

### Sending Real-Time Events using the Event Creator

We can also test out this functionality without writing any server-side code by using the <strong>Event Creator</strong> for your app which can also be found in the Pusher dashboard. The Event Creator lets you publish events on a channel through a simple user interface. From the code above we can see that we want to publish an event named <em>"new_comment"</em> on the <em>"comments-1"</em> channel. From the earlier test function we also have an example of the test data we can publish.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c98864d6-d32f-48e2-a511-79bc4e0a36e3/event-creator.png" alt="Screenshot of the Event Creator in Pusher Dashboard" width="500" />

### Real-time PHP

Again, we've proven that our client-side functionality works without having to write any server-side code. Now lets add the PHP code we need to trigger the new comment event as soon as a comment is posted in our comment system.

Pusher offers a number of <a href="https://pusher.com/docs/rest_libraries">server-side libraries</a> which make it easy to publish events in addition to helping with functionality such as <a href="https://pusher.com/docs/private_channels">private channel</a> authentication and providing user information for <a href="https://pusher.com/docs/presence">presence channels</a>. We just want to use the basic event triggering functionality in the <em>post_comment.php</em> file so we need to download the Pusher PHP library.

Once you've downloaded this zip file, unzip it into the directory along with your other files. Your file structure will now look something like this:

*   index.php
*   css (dir)
*   images (dir)
*   post_comment.php
*   pusher_config.php
*   Persistence.php
*   squeeks-Pusher-PHP (dir)
    *   lib (dir)
        *   Pusher.php

An event can be triggering in just a few lines of code:

<pre><code class="language-php">&lt;?php
require('squeeks-Pusher-PHP/lib/Pusher.php');
require('pusher_config.php');

$pusher = new Pusher(APP_KEY, APP_SECRET, APP_ID);
$pusher-&gt;trigger('comments-1', 'new_comment', array(
  "comment_post_ID" =&gt; 1,
  "date" =&gt; "Tue, 21 Feb 2012 18:33:03 +0000",
  "comment" =&gt; "The realtime Web rocks!",
  "comment_author" =&gt; "Phil Leggetter"
));
?&gt;</code></pre>

However, we need to apply a some additional logic before we trigger the event:

*   Check that the comment was added.
*   Extract the unique comment identifier from the `$added` array.
*   Build the text to identify a channel name for the submitted comment.
*   Trigger a _new_comment_ event on the channel with the `$added` data. _Note: The library automatically converts the `$added` array variable to JSON to be sent through Pusher._

Therefore the full <em>post_comment.php</em> file ends up looking as follows:

<pre><code class="language-php">&lt;?php
require('Persistence.php');
require('squeeks-Pusher-PHP/lib/Pusher.php');
require('pusher_config.php');

$ajax = ($_SERVER[ 'HTTP_X_REQUESTED_WITH' ] === 'XMLHttpRequest');

$db = new Persistence();
$added = $db-&gt;add_comment($_POST);

if($added) {
  $channel_name = 'comments-' . $added['comment_post_ID'];
  $event_name = 'new_comment';

  $pusher = new Pusher(APP_KEY, APP_SECRET, APP_ID);
  $pusher-&gt;trigger($channel_name, $event_name, $added);
}

if($ajax) {
  sendAjaxResponse($added);
}
else {
  sendStandardResponse($added);
}

function sendAjaxResponse($added) {
  header("Content-Type: application/json");
  if($added) {
    header( 'Status: 201' );
    echo( json_encode($added) );
  }
  else {
    header( 'Status: 400' );
  }
}

function sendStandardResponse($added) {
  if($added) {
    header( 'Location: index.php' );
  }
  else {
    header( 'Location: index.php?error=Your comment was not posted due to errors in your form submission' );
  }
}
?&gt;</code></pre>

If you run the app now in two different browser windows you'll see that as soon as you submit a comment in one window that comment will instantly ("magically") appear in the second window. <strong>We now have a real-time commenting system!</strong>

<strong>But...</strong>, we're not done quite yet. You'll also see that the comment is shown twice in the window of the user who submitted it. This is because the comment has been added by the AJAX callback, and by the Pusher event. Because this is a very common scenario, especially if you've built an application in a progressively enhanced way as we have, the Pusher server libraries expose a way of <a href="https://pusher.com/docs/publisher_api_guide/publisher_excluding_recipients">excluding a connection/user</a> from receiving the event via Pusher.

In order to do this you need to send a unique connection identifier called a <code>socket_id</code> from the client to the server. This identifier can then be used to define who will be excluded.

<pre><code class="language-javascript">function handleSubmit() {
  var form = $(this);
  var data = {
    "comment_author": form.find('#comment_author').val(),
    "email": form.find('#email').val(),
    "comment": form.find('#comment').val(),
    "comment_post_ID": form.find('#comment_post_ID').val()
  };

  var socketId = getSocketId();
  if(socketId !== null) {
    data.socket_id = socketId;
  }

  postComment(data);

  return false;
}

function getSocketId() {
  if(pusher &amp;&amp; pusher.connection.state === 'connected') {
    return pusher.connection.socket_id;
  }
  return null;
}</code></pre>

The changes we've made are:

*   A new function called `getSocketId` has been added to get the `socket_id`. It wraps a check to ensure that the `pusher` variable has been set and also that the client is connected to Pusher.
*   The `handleSubmit` has been updated to check to see if a `socket_id` is available. If it is, this information is posted to the server along with the comment data.

On the server we need to use the <code>socket_id</code> parameter if it is present and therefore exclude the connection and user who submitted the comment, or pass in <code>null</code> if it's not:

<pre><code class="language-php">$channel_name = 'comments-' . $added['comment_post_ID'];
$event_name = 'new_comment';
$socket_id = (isset($_POST['socket_id'])?$_POST['socket_id']:null);

$pusher = new Pusher(APP_KEY, APP_SECRET, APP_ID);
$pusher-&gt;trigger($channel_name, $event_name, $added, $socket_id);</code></pre>

And as simple as that we have <strong>a fully realtime enabled blog commenting system</strong> and we only send messages to users who really need to see them. As with the AJAX functionality the realtime functionality has been added in a progressively enhancing way, to ensure it doesn't impact on any other functionality. You can find the a demo running <a href="https://www.leggetter.co.uk/pusher/realtime-commenting/">here</a> and the completed solution in the <a href="https://github.com/pusher/realtime-commenting">realtime commenting repository</a> in github.</p>

## Good Real-Time App Development Practices

Real-time application development shares common good development practices with general Web development. However, I thought I would share a couple of tips that can come in particularly handy.</p>

### Use Browser Developer Tools

When you start doing a lot of JavaScript development the browser developer tools becomes your best friend. It's the same when adding realtime functionality to your Web app, not only because you are using JavaScript, but also because the JavaScript library you are using is likely to be doing some reasonably complex things internally. So, the best way of understanding what is going on and if your code is using it as expect is to enable logging which usually goes to the developer console. All major browser vendors now offer good developer tools which include a console:

*   [Firebug addon](https://getfirebug.com/) for Firefox
*   Internet Explorer [F12 developer tools](https://msdn.microsoft.com/en-us/library/gg589507(v=VS.85).aspx)
*   [Opera Dragonfly](https://www.opera.com/dragonfly/documentation/)
*   [Safari Developer Tools](https://developer.apple.com/library/safari/#documentation/appleapplications/Conceptual/Safari_Developer_Guide/2SafariDeveloperTools/SafariDeveloperTools.html)

The Pusher JavaScript library provides a way to hook into the logging functionality. All you need to do is assign a function to the <a href="https://pusher.com/docs/client_api_guide/client_global_configuration#pusher_log"><code>Pusher.log</code></a> static property. This function will then receive all log messages. You can do what you like within the function but best practice is to log the messages to the developer console. You can do this as follow, ensuring the code it executed after the Pusher JavaScript library include:

<pre><code class="language-javascript">Pusher.log = function(msg) {
  if(window.console &amp;&amp; window.console.log) {
    window.console.log(new Date().getTime() + ': ' + msg);
  }
};</code></pre>

The code above checks to make sure the <code>console</code> and <code>log</code> function is available - it's not in older browsers - and then logs the messages along with a timestamp to the JavaScript console. This can be incredibly handy in tracking down problems.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2c01f6c-6878-46d2-a5e2-4a381b4845b3/javascript-console.png" alt="Screenshot of Pusher logging in the Chrome Developer Tools Console" width="500" />

### Check Connectivity

Any good real-time technology will maintain a persistent connection between the client (web browser) and the Web server or service. Sometimes the client will lose connectivity and when the client isn't connected to the Internet the real-time functionality won't work. This can happen a lot with applications running on mobile devices which rely on mobile networks. So, if your application relies on that connectivity and functionality then it's important to deal with scenarios where the client isn't connected. This might be by displaying a message to tell the user they are offline or you might want to implement some alternative functionality.

The Pusher JavaScript library exposes connectivity state via the <code>pusher.connection</code> object, which we briefly saw earlier when fetching the <code>socket_id</code>. Binding to state changes and implementing your required functionality is quite simple as it follows the same mechanism as binding to events on channels:

<pre><code class="language-javascript">var pusher = new Pusher(APP_KEY);

pusher.connection.bind('state_change', function(states) {
  Pusher.log('Connection state changed from: ' + states.previous + ' to ' + states.current);
});</code></pre>

## Conclusion

We're seeing real-time functionality appearing in a large number of high profile applications: some have it at the core of what they offer whilst others use it sparingly. No matter how it is used the end goal is generally the same; to enhance the user experience and keep users engaged with an application. By converting a basic blog commenting system into a more engaging communication platform I hope I've demonstrated that the functionality and experience can easily be layered on existing application.

The ease of access to this technology is a relatively new thing and we've only just touched the potential uses for the technology. Real-time stats, instant news updates, activity streams, social interaction, collaboration and gaming are just a few common uses but as more developers become aware of, and comfortable with, the technology I'm confident that we're going to see some truly amazing innovation. An "Internet of Real-Time Things?"?

