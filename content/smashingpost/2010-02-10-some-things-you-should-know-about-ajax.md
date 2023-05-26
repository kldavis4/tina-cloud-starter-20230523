---
title: 'Developing Sites With AJAX: Design Challenges and Common Issues'
slug: some-things-you-should-know-about-ajax
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be7e8d8-0f43-4d7c-8b34-c66f039e4bf4/ajax.png
date: 2010-02-10T14:59:14.000Z
author: christian-heilmann
description: >-
  Almost every movie has a scene in which a character pull the protagonist aside and says, "There's something you should know about [insert another character's name here]." Most of the time, we find out some dark secret about a supposed friend of the protagonist or that the main ally is actually an evil overlord.
categories:
  - Coding
  - AJAX
  - Techniques
---
This is that moment, and I am here to tell you a few things about our friend in the Web 2.0 world: AJAX.

<strong>We seem to have AJAX licked</strong>. The Web technology is ubiquitous, and libraries and frameworks make it dead easy for us to create highly interactive Web applications and to spice up our static pages and blogs.

For example, we could take the following HTML...

{{% feature-panel %}}

<pre><code class="language-markup tmp-html">&lt;div id="target"&gt;&lt;/div&gt;
&lt;p&gt;&lt;a href="#" class="ajaxtrigger"&gt;Let there be AJAX magic&lt;/a&gt;&lt;/p&gt;</code></pre>

... and add this jQuery code:

<pre><code class="language-javascript">$('.ajaxtrigger').click(function(){
  $('#target').load('ajaxcontent.html');
});</code></pre>

In a browser, if we clicked on the link labelled "Let there be AJAX magic," the content of the HTML document <code>ajaxcontent.html</code> would be loaded and written into the element with the ID <code>target</code>. You can try this <span class="removed_link" title="https://icant.co.uk/articles/things-to-know-about-ajax/very-simple-ajax.html">very simple AJAX example here</span>. It's simple and easy to use, but what's really happening there? What is AJAX?

## What Is AJAX?

After the main HTML document has loaded, AJAX loads content from the server and replaces parts of the document with that content rather than reload the main document. It's as simple as that. AJAX stands for "Asynchronous JavaScript and XML" and was meant to load only XML documents, but we soon used it to load everything under the sun, and so the XML part was quickly forgotten. The asynchronous part is the killer feature; but what is it?

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84b0cc76-57df-4b67-be38-86d81c28e0d9/ajax.gif" alt="AJAX Model" width="591" height="566" /><br>
<em>The traditional model for web applications (left) compared to the Ajax model (right).</em>

Let's start by analysing how a normal Web interaction works:

1.  The user enters a URI (like [https://wait-till-i.com/index.php](https://wait-till-i.com/index.php)) into a user agent (usually a browser).
2.  The browser turns this URI into an IP and requests the file located at the URI specified endpoint.
3.  The browser loads the file and, if it recognizes the document type, tries to display it.
4.  If the document is in HTML, we get an interface that we can interact with; for example, by clicking a link or entering data into a form and submitting it.
5.  In both cases, the whole document is replaced and the sequence restarts.

This has worked since the beginning of the Web and has become expected behaviour for Web surfers. With AJAX, we disrupt this sequence of events. Instead of reloading the document or loading a new one, we replace only a part of the interface, either when the user requests it or automatically every few seconds to display new information.

The benefits of AJAX are pretty clear:

*   We maintain a consistent interface, rather than discard it only to bring it up again with a few slight changes after a long and annoying loading process.
*   We request only the data that we need, when we need it, saving us a lot of server traffic.
*   We are able to offer data without wrapping HTML around it to make it an interface.
*   We allow for simultaneous interaction; a user would be able, for example, to fill out a form while an attachment uploads in the background.

However, with great power comes great responsibility, and with AJAX we have taken it upon ourselves to simulate browser behavior for end users.</p>

## AJAX Should Not Break The Web

The first thing to make sure of is that you do not break the Web with your AJAX solutions. The above example would, though:

<pre><code class="language-markup tmp-html">&lt;div id="target"&gt;&lt;/div&gt;
&lt;p&gt;&lt;a href="#" class="ajaxtrigger"&gt;Let there be AJAX magic&lt;/a&gt;&lt;/p&gt;</code></pre>

This is not useful HTML. If JavaScript is not available or anything else goes wrong, you would be offering the end user a link that goes nowhere. This is annoying; I've come to your website, took the step of clicking a link, got excited by the prospect of awesome content but don't get anything. Not good. So, rather than keep the URI in the JavaScript part of the AJAX solution, leave it in the HTML:

<pre><code class="language-markup tmp-html">&lt;div id="target"&gt;&lt;/div&gt;
&lt;p&gt;&lt;a href="ajaxtest-fullpage.html" class="ajaxtrigger"&gt;
  Let there be AJAX magic
&lt;/a&gt;&lt;/p&gt;</code></pre>

This would ensure that the link works; if there is a JavaScript error, the browser would simply move on to load and display <em>ajaxcontent.html</em>. The jQuery code would change accordingly:

<pre><code class="language-javascript">$('.ajaxtrigger').click(function(){
  var url = $(this).attr('href');
  $('#target').load(url);
  return false;
});</code></pre>

Instead of hard-wiring a URI to load, we just read the <code>href</code> attribute of the link. The <code>return false</code> is needed to stop the browser from following the link after jQuery has initiated the AJAX request. This also means that any link with the class <code>ajaxtrigger</code> will load content via AJAX and display it in the element with the ID <code>target</code>. You can try this reusable AJAX example here.

There is a problem, of course, because the document we load might be a full HTML document, with a head and a body and so on. This works well in the browser, but the AJAX request would load and inject this document it into another document, which is invalid HTML and would cause display issues. Try this out by clicking the "Load a full document" link on the page referred to above.

Let's say that <em>ajaxtest-fullpage.html</em> is the following:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
 "https://www.w3.org/TR/html4/strict.dtd"&gt;
&lt;html&gt;
&lt;head&gt;
  [... some links and title and so on ...]
&lt;/head&gt;
&lt;body&gt;
&lt;div id="doc" class="yui-t7"&gt;
  &lt;div id="hd" role="banner"&gt;&lt;h1&gt;Excerpt from Alice's Adventure Underground&lt;/h1&gt;&lt;/div&gt;
  &lt;div id="bd" role="main"&gt;
    &lt;blockquote
     cite="https://ia341030.us.archive[...]-h.htm"&gt;
      &lt;p&gt;Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had  peeped into the book her sister was reading, but it had no pictures or conversations in it, and where is the use of a book, thought Alice, without pictures or conversations? So she was considering in her own mind, (as well as she could, for the hot day made her feel very sleepy and stupid,) whether the pleasure of making a daisy-chain was worth the trouble of getting up and picking the daisies, when a white rabbit with pink eyes ran close by her.&lt;/p&gt;
    &lt;/blockquote&gt;
    &lt;p&gt;Excerpt taken from 
      &lt;a href="https://ia341030.us.archive[...]-h.htm"&gt;archive.org&lt;/a&gt;.
    &lt;/p&gt;
  &lt;/div&gt;
  &lt;div id="ft" role="contentinfo"&gt;
    &lt;p&gt;Demo by &lt;a href="https://wait-till-i.com"&gt;Chris Heilmann&lt;/a&gt;&lt;/p&gt;
  &lt;/div&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

jQuery is all about selectors, which is why the <code>load()</code> function allows you to cut down on the returned HTML by defining a selector. This means that you can change the script to the following (you can try the selector filtering example for yourself):

<pre><code class="language-javascript">$('.ajaxtrigger').click(function(){
  var url = $(this).attr('href');
  $('#target').load(url+' #bd blockquote');
  return false;
});</code></pre>

This loads only the <code>blockquote</code> into the other document, so you wouldn't be creating invalid HTML with the AJAX call. However, we lose the other benefit of AJAX, which is to load less content. If the page is 100 KB and you want to show only the main text, which is 2 KB, why should your users have to wait for 98 KB to load?

To work around this, you need to go server-side. In PHP, you can get information about the request that was sent to load the page. One bit of information is the request method; JavaScript libraries such as jQuery send a specific header across when they load a document with AJAX. You can use this in PHP to set up conditional content:

<pre><code class="language-php">&lt;?php if($_SERVER['HTTP_X_REQUESTED_WITH']=='XMLHttpRequest'){?&gt;
This is content requested by AJAX.
&lt;?php }?&gt;

&lt;?php if($_SERVER['HTTP_X_REQUESTED_WITH']==’){?&gt;
This is the normal content requested in a browser
&lt;?php }?&gt;</code></pre>

Try this header, switching out example for yourself: click the "Load a document with AJAX" link, and then right-click (or Command-click) the same link to open it in a new tab (or hit the "Load the same document without AJAX" link). The results should be "This is content requested by AJAX" and "This is the normal content requested in a browser" respectively.

This way, you can keep all of the header and footer information in includes and load them only when the request could not be done with AJAX. Try the header includes example to see it in action:

<pre><code class="language-php">&lt;?php if($_SERVER['HTTP_X_REQUESTED_WITH']==’){?&gt;
  include('header.php');
&lt;?php }?&gt;

&lt;blockquote
 cite="https://ia341030.us.archive[...]-h.htm"&gt;
  &lt;p&gt;Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, and where is the use of a book, thought Alice, without pictures or conversations? So she was considering in her own mind, (as well as she could, for the hot day made her feel very sleepy and stupid,) whether the pleasure of making a daisy-chain was worth the trouble of getting up and picking the daisies, when a white rabbit with pink eyes ran close by her.&lt;/p&gt;
&lt;/blockquote&gt;
&lt;p&gt;Excerpt taken from 
  &lt;a href="https://ia341030.us.archive[...]-h.htm"&gt;archive.org&lt;/a&gt;.
&lt;/p&gt;

&lt;?php if($_SERVER['HTTP_X_REQUESTED_WITH']==’){?&gt;
  include('footer.php');
&lt;?php }?&gt;</code></pre>

Using this "unobtrusive AJAX" approach does a few things:

*   You don't create broken links, ever.
*   You make it easier to maintain functionality; no need to hunt for URIs in the JavaScript—everything is in the HTML.
*   You allow users to open links in another window or tab.
*   You maintain the AJAX-enabled and AJAX-disabled content in the same document without duplicating content.

"Unobtrusive JavaScript" is the term for this method of developing highly interactive websites. It was coined by <a href="https://www.kryogenix.org/code/browser/aqlists">Stuart Langridge in 2002</a>, and I wrote a <a href="https://onlinetools.org/articles/unobtrusivejavascript/">self-training course</a> for it in 2004. Incidentally, Stuart was also the first author to cover AJAX in a JavaScript book, the unfortunately named <a href="https://www.sitepoint.com/books/dhtml1/">DHTML Utopia</a>. My own not-quite-so-succinctly-titled book <a href="https://beginningjavascript.com">Beginning JavaScript with DOM Scripting and AJAX</a> was, I think, the second. Both books follow the approach shown here and create AJAX solutions that fall back to non-JavaScript versions.

Jeremy Keith tried to further popularize this idea of "safer AJAX" in 2006 <a href="https://domscripting.com/blog/display/41">by calling it "Hijax"</a>, and he wrote a book titled <a href="https://bulletproofajax.com/">Bulletproof AJAX</a> in 2007. Sadly, though, I have encountered people who use this as an excuse, saying, "We're building an AJAX solution now, and we'll move it to Hijax later." This will not work! Do it right the first time and you'll have a stable solution. There is no "We'll fix it in the next iteration" when it comes to essential functionality in Web development: 12 years of professional development have taught me that much.

## AJAX Design Challenges

In dealing with AJAX as designers, we have to reconsider the ways in which we define interfaces. Rather than concentrate on the look and feel of the page and subsequent pages, we need to drill down to an atomic level. Each part of an AJAX interaction needs to be defined. Also, think about non-JavaScript versions of widgets.

With AJAX interfaces, we move into a world of applications that have states and views and out of a world in which our document or page model was based on ideas carried over from print. This for me is a good thing. The Web is a rich medium, not a sequence of linked designs.</p>

## AJAX And Usability

As mentioned, we use AJAX to disrupt the normal browsing behaviour of our users. This can be a good thing: no one claims that browsers do everything right, but understanding just how many things we should take care of when taking over the browser is important.</p>

### What Browsers Do That You Need to Simulate

We sometimes forget just how many things the browser does for us:

*   When we click a link, an indicator alerts us to a loading process (whether an animated icon, progress bar, etc.).
*   For large files, the progress bar gives us an idea of how far we've reached in the loading process.
*   If we get tired of waiting, we can hit the "Stop" button or try again by reloading the page.
*   If a page cannot be found, we are shown an error page.
*   If a page takes too long to load, we are shown an error page.
*   Other errors we encounter (for example, a page that needs authentication, or a document that has been moved) are also displayed on a special page.
*   We can right-click a link to open it in a new tab or window, instead of replacing the current document.
*   We can bookmark a page and come back to it at any time in the future.
*   When we need to undo something that's gone wrong, a "Back" button takes us back one step in our journey.

All of this needs to be accounted for in a full-fledged AJAX application, because AJAX should improve the end user's experience rather than make it harder. Let's now enhance our AJAX script until we can say that we've covered the basics.</p>

### Bookmarking and the Back Button

One thing I won't go into in detail is the "Back" button and bookmarking functionality. To make this work, you need to update the URI of the current page with a fragment and reload a hidden frame in the page. There are all kinds of annoying differences between browsers, too, and you can use something like <a href="https://plugins.jquery.com/project/history">the history plug-in</a> for jQuery to get this to work.</p>

### Alerting the User That Something Is Loading

Probably the first thing to fix is to tell the user that something is loading when they click a link or push a button. If the page shows no apparent change, the user will think something is wrong and keep clicking. This is an unfortunate human reflex, because the more you tell a computer to do something, the slower and more confused it gets.

A simple way to provide the user with feedback is to show a loading message. To do this in jQuery, we need to get away from the <code>load()</code> method and instead use <code>ajax()</code>, which gives us information about what happens to the request, such as:

*   The `beforeSend` event that is fired before the AJAX request is initiated, and
*   The `success` event that is fired when the AJAX request is successful.

Putting them together, we can add a loading message to the target element when the AJAX request starts, which is replaced when the data has successfully loaded:

<pre><code class="language-javascript">$(document).ready(function(){
  var container = $('#target');
  $('.ajaxtrigger').click(function(){
    doAjax($(this).attr('href'));
    return false;
  });
  function doAjax(url){
    $.ajax({
      url: url,
      success: function(data){
        container.html(data);
      },
      beforeSend: function(data){
        container.html('&lt;p&gt;Loading...&lt;/p&gt;');
      }
    });
  }
});</code></pre>

### Error Handling

As you may have guessed, the next logical step is to handle error cases. This is something far too many AJAX solutions haven't gotten right, and seeing a great application become useless just because one call has timed out is very frustrating.

We have to prepare for three different errors:

*   The user tries to load an external file that is not available because of AJAX security settings;
*   There is some server error (for example, "Page not found");
*   The resource takes too long to load.

The following script takes care of all this, and you can see it in action on the error handling demo page.

<pre><code class="language-javascript">$(document).ready(function(){
  var container = $('#target');
  $('.ajaxtrigger').click(function(){
    doAjax($(this).attr('href'));
    return false;
  });
  function doAjax(url){
    if(url.match('^http')){
      var errormsg = 'AJAX cannot load external content';
      container.html(errormsg);
    } else {
      $.ajax({
        url: url,
        timeout:5000,
        success: function(data){
          container.html(data);
        },
        error: function(req,error){
          if(error === 'error'){error = req.statusText;}
          var errormsg = 'There was a communication error: '+error;
          container.html(errormsg);
        },
        beforeSend: function(data){
          container.html('&lt;p&gt;Loading...&lt;/p&gt;');
        }
      });
    }
  }
});</code></pre>

The changes are:

*   We test whether the link URI starts with `http` and then report an error that loading it with AJAX is not possible.
*   If the link doesn't begin with `http`, we start a new AJAX request. This one has a few new features:
    *   We define a `timeout` of 5 seconds (i.e. 5000 milliseconds);
    *   We add an error handler.
*   The error handler either sends us what happened on the server as `req.statustext` or gives us the error message `timeout` when the 5 seconds are up. So, we need to check what we got before we write out the error message.</p>

### Highlighting Changes

We're almost done enhancing the usability of our AJAX solution. One last touch is to make it very obvious that something on the page has changed. The standard way of doing this is called the <a href="https://37signals.com/svn/archives/000558.php">yellow fade</a> and was introduced in 2004 by 37signals in its Basecamp application.

With this technique, you change the background colour of the element to yellow and then fade it smoothly back to white. This grabs the user's attention without overloading them (unlike zooming in on the content in or popping it up, PowerPoint style, which would overwhelm), and it is pretty easy to implement.

jQuery has a plug-in in the effects package called <a href="https://docs.jquery.com/UI/Effects/Highlight">Highlight</a> that does exactly that. Using it, we can highlight the AJAX returns, making it very obvious that something has changed:

<pre><code class="language-javascript">$(document).ready(function(){
  var container = $('#target');
  $('.ajaxtrigger').click(function(){
    doAjax($(this).attr('href'));
    return false;
  });
  function doAjax(url){
    if(url.match('^http')){
      var errormsg = 'AJAX cannot load external content';
      container.html(errormsg).
        effect('highlight',{color:'#c00'},1000);
    } else {
      $.ajax({
        url: url,
        timeout:5000,
        success: function(data){
          container.html(data).
            effect("highlight",{},1000);
        },
        error: function(req,error){
          if(error === 'error'){error = req.statusText;}
          var errormsg = 'There was a communication error: '+error;
          container.html(errormsg).
            effect('highlight',{color:'#c00'},1000);
        },
        beforeSend: function(data){
          container.html('&lt;p&gt;Loading...&lt;/p&gt;');
        }
      });
    }
  }
});</code></pre>

Notice the different colors for the error case and success case.

This is about all we need to do to make AJAX more usable. But to make it accessible to everyone out there, we have to do a bit more.</p>

## AJAX And Accessibility

Accessibility does not mean much more than hard-core usability. If the "average" user is confused by an interface that doesn't work as they expect, imagine the predicament of users who cannot see the interface at all. Or think someone who has trouble noticing changes from one page to the next and all of a sudden has to deal with small changes on individual pages—changes they are not notified about. Imagine a keyboard user tabbing through a document to activate a link and out of the blue being confronted by 10 more links. There are a lot more cases such as these, and your interface should be able to handle them at least at a very basic level.</p>

### Much Ado About Screen Readers

If you research the topic of AJAX and accessibility, you will come across a lot of tutorials that deal with the problem of screen readers. I won't go into details—this could be its own article—but here are the main points:

*   Screen readers are tools that read out to visually impaired users what is on the screen (or in the HTML and hidden by CSS).
*   Screen readers work on top of the normal browser and enhance its functionality. Specifically, they allow for quicker keyboard navigation (for example, jumping from headline to headline with a shortcut).
*   They take a copy of a document after it has loaded and apply changes to it.
*   This means that screen readers understand JavaScript, but they only execute a request when the page has loaded. If you change a document with JavaScript and AJAX after it has loaded, you need to notify the screen reader somehow that something has changed and refresh the copy of the page. This can be done by [refreshing a form field](https://juicystudio.com/article/improving-ajax-applications-for-jaws-users.php) as a hack.

The real problem with screen readers, and any assistive technology, is that they add yet another level of complexity to our Web interaction.

We have HTML interfaces such as links and forms that need to work with all kinds of input devices: keyboard, mouse, voice recognition software, to name a few. Then the browser needs to somehow tell the assistive software (whether a screen reader or software that zooms the screen or a voice recognition tool) that something has changed, and that other tool has to translate it into an understandable format. All of this can, and frequently does, fail.

Much like how HTML 5 is being pushed to replace HTML 4 because the latter is not rich enough to support the interfaces we want to build, <a href="https://www.w3.org/WAI/intro/aria">WAI-ARIA</a> is a standard that works around the problem of assistive technology and browsers not talking to each other.

With WAI-ARIA, you can tell a screen reader, for example, that a particular element on the page changes frequently and will be refreshed with AJAX. Again, this topic is too big to cover here, but <a href="https://www.alistapart.com/articles/waiaria">some good articles are out there</a> in case you are interested.</p>

### Important Feature #1: Keyboard Access

One very important requirement of accessibility and AJAX is providing keyboard access, and doing this in a very basic way is not hard. The element that triggers the AJAX call has to be something that users can access with the keyboard (i.e. either a link or a button). You can test this yourself: simply use the Tab key to jump from one keyboard-accessible element to the next in your document. Can you access all of the functionality, and is it obvious where you are at any given moment?

This is where you as a designer can do a lot to make your AJAX interface more accessible. Patrick Lauke has <a href="https://24ways.org/2009/dont-lose-your-focus">written a wonderful article on keyboard-access styling</a> to get you on your way.</p>

### Important Feature #2: Notify at the Source

The second, very important, part is to notify users in the element that they activated that something is happening. You'll often see interfaces where the activation button or link is in one spot but the content gets loaded somewhere else on the screen. One example of this is the contact form on Get Satisfaction:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2cd9f1a-3f9e-40c6-bd4b-925dfd1570fe/get-satisfaction-small.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0077280-16c6-41f7-aa4e-64b7795c985c/get-satisfaction-small2.jpg" alt="Modal Pop-Up form by get satisfaction" width="550" height="390" /></a><br>
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2cd9f1a-3f9e-40c6-bd4b-925dfd1570fe/get-satisfaction-small.jpg">Large view</a>

When we can see the screen in full, everything is pretty obvious. But consider an end user who has to magnify the screen to 1600% to be able to read it. Or someone who gets easily confused and uses a tool to focus on the part of the screen they are interacting with and blur out the rest. Their experience is different:

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6834ccd-bccf-44bf-ab22-ca1d420e739d/zoomed.jpg" alt="zoomed button" width="300" height="313" />

By clicking this, the user expects to be able to submit feedback. Instead, all they get is a darker screen, which could be a hardware problem (running out of battery?) or something else entirely. They have no information on which to base their next move.

You don't even have to go as far as considering people with disabilities: just use a netbook whose viewport is a mere 300-pixels high (like my first-generation Eee PC) or a mobile interface that zooms into a certain part of the page (like my Blackberry with Opera Mini).

In any of these cases, your AJAX solution will be neither usable nor accessible if the section that is replaced is far removed from the button that fires the AJAX request.

You have two workarounds. The most obvious one is to keep the elements close together. If that is not possible, the other workaround is to change the content of the element that fires the AJAX request once the user clicks on it. This indicates to the end user what is going on.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9e295e7-0468-4752-a91a-a50bd6a3dae9/notifications.png" alt="notifications at the source and the target make it obvious to any user what happened." />

As an added assistance, you can shift the keyboard focus to the target element when the AJAX request has been processed. Be aware, though, that this could confuse some users; being jumped around the screen without meaning to can be scary. Pretty, smooth-transitioning solutions look good to the rest of us, but they can be a total nightmare for users with learning disabilities.

Putting all of this together, take a look at this more accessible example. It adds a <code>span</code> to the link to show the state of the AJAX request, it highlights the content when it has finished loading, and then it shifts the focus to the new element. Here is the final code. Check the comments (// example) to see what is going on.

<pre><code class="language-javascript">$(document).ready(function(){

  // this is the container we'll load content into var container = $('#target');

  // adding a tabIndex of -1 makes it keyboard accessible,
  // and we can set the focus to it container.attr('tabIndex','-1');

  // if a user clicks on an element with the class ajaxtrigger...
  $('.ajaxtrigger').click(function(){

    // define trigger as the link
    var trigger = $(this);

    // read its href attribute (which is the URI we'll load with AJAX)
    var url = trigger.attr('href');

    // if the element does not have a class called "loaded" 
    if(!trigger.hasClass('loaded')){

      // add a new span to the element.
      trigger.append('&lt;span&gt;&lt;/span&gt;');

      // add a class called 'loaded' to the element
      trigger.addClass('loaded');

      // and define msg as the last span in the element
      var msg = trigger.find('span::last');

    // otherwise, simply define msg as the last span in the element
    } else {
      var msg = trigger.find('span::last');
    }
    // ^ this condition means we only add the span once and not
    //   every time users click the element.

    // call the doAjax function with the URI to load, 
    // the span inside the link to change and the 
    // target element to replace.    
    doAjax(url,msg,container);

    // tell the browser to not follow the link 
    return false;
  });

  // here's where the AJAX magic happens function doAjax(url,msg,container){

    // if the URI starts with http...
    if(url.match('^http')){
      // show an error and set the class of the span to 'error'
      msg.html(' (error!)').addClass('error');

      // tell the end user in the target element what the error is
      var errormsg = 'AJAX cannot load external content';

      // update the container with the error
      updateContainer(errormsg,'#c00');

    // if the URI does not start with http          
    } else {

      // start an AJAX request using the url
      $.ajax({
        url: url,

        // give the request five seconds time, otherwise call it 
        // a timeout error
        timeout:5000,

        // if all went well
        success: function(data){

          // set the span content to ready
          msg.html(' (ready.)');

          // update the container with the right data
          updateContainer(data,'#ff9');
        },

        // if there was an error
        error: function(req,error){

          // say in the link that there was an error and set the 
          // class of the span to 'error'
          msg.html(' (error!)').addClass('error');

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6834ccd-bccf-44bf-ab22-ca1d420e739d/zoomed.jpg" alt="zoomed button" width="300" height="313" />

By clicking this, the user expects to be able to submit feedback. Instead, all they get is a darker screen, which could be a hardware problem (running out of battery?) or something else entirely. They have no information on which to base their next move.

You don't even have to go as far as considering people with disabilities: just use a netbook whose viewport is a mere 300-pixels high (like my first-generation Eee PC) or a mobile interface that zooms into a certain part of the page (like my Blackberry with Opera Mini).

In any of these cases, your AJAX solution will be neither usable nor accessible if the section that is replaced is far removed from the button that fires the AJAX request.

You have two workarounds. The most obvious one is to keep the elements close together. If that is not possible, the other workaround is to change the content of the element that fires the AJAX request once the user clicks on it. This indicates to the end user what is going on.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9e295e7-0468-4752-a91a-a50bd6a3dae9/notifications.png" alt="notifications at the source and the target make it obvious to any user what happened." />

As an added assistance, you can shift the keyboard focus to the target element when the AJAX request has been processed. Be aware, though, that this could confuse some users; being jumped around the screen without meaning to can be scary. Pretty, smooth-transitioning solutions look good to the rest of us, but they can be a total nightmare for users with learning disabilities.

Putting all of this together, take a look at this more accessible example. It adds a <code>span</code> to the link to show the state of the AJAX request, it highlights the content when it has finished loading, and then it shifts the focus to the new element. Here is the final code. Check the comments (// example) to see what is going on.

<pre><code class="language-javascript">$(document).ready(function(){

  // this is the container we'll load content into var container = $('#target');

  // adding a tabIndex of -1 makes it keyboard accessible,
  // and we can set the focus to it container.attr('tabIndex','-1');

  // if a user clicks on an element with the class ajaxtrigger...
  $('.ajaxtrigger').click(function(){

    // define trigger as the link
    var trigger = $(this);

    // read its href attribute (which is the URI we'll load with AJAX)
    var url = trigger.attr('href');

    // if the element does not have a class called "loaded" 
    if(!trigger.hasClass('loaded')){

      // add a new span to the element.
      trigger.append('&lt;span&gt;&lt;/span&gt;');

      // add a class called 'loaded' to the element
      trigger.addClass('loaded');

      // and define msg as the last span in the element
      var msg = trigger.find('span::last');

    // otherwise, simply define msg as the last span in the element
    } else {
      var msg = trigger.find('span::last');
    }
    // ^ this condition means we only add the span once and not
    //   every time users click the element.

    // call the doAjax function with the URI to load, 
    // the span inside the link to change and the 
    // target element to replace.    
    doAjax(url,msg,container);

    // tell the browser to not follow the link 
    return false;
  });

  // here's where the AJAX magic happens function doAjax(url,msg,container){

    // if the URI starts with http...
    if(url.match('^http')){
      // show an error and set the class of the span to 'error'
      msg.html(' (error!)').addClass('error');

      // tell the end user in the target element what the error is
      var errormsg = 'AJAX cannot load external content';

      // update the container with the error
      updateContainer(errormsg,'#c00');

    // if the URI does not start with http          
    } else {

      // start an AJAX request using the url
      $.ajax({
        url: url,

        // give the request five seconds time, otherwise call it 
        // a timeout error
        timeout:5000,

        // if all went well
        success: function(data){

          // set the span content to ready
          msg.html(' (ready.)');

          // update the container with the right data
          updateContainer(data,'#ff9');
        },

        // if there was an error
        error: function(req,error){

          // say in the link that there was an error and set the 
          // class of the span to 'error'
          msg.html(' (error!)').addClass('error');

          // if the error just says error, get the real status 
          // text from the browser (jQuery doesn't do this right)
          if(error === 'error'){error = req.statusText;}

          // tell the user that there is a communication error
          var errormsg = 'There was a communication error: '+error;

          // update the container with the error
          updateContainer(errormsg,'#c00');
        },

        // if the link was clicked but the AJAX request was not fired...
        beforeSend: function(data){

          // remove any "error" classes and set the span message to loading
          msg.removeClass('error').html(' (loading...)');
        }
      });
    }
  };

  // update the container 
  function updateContainer(content,colour){
    container.
      // set the content
      html(content).
        // shift the browser focus
        focus().
          // flash the container for a second in the 
          // specified colour
          effect('highlight',{color:colour},1000);
  }

});</code></pre>

The code is a bit longer than in that our other examples, but the payoff makes it very much worthwhile.</p>

### Important Feature #3: De-Clutter Your Interface

With a library such as jQuery, you can make anything on the page interactive and make it initiate AJAX requests. You could use roll-overs or drag-and-drop interfaces, and these are great to look at, but ask yourself: are they really intuitive? Browsers do not yet have any drag-and-drop functionality or even roll-overs. Roll over your menu bar; you have to click to initiate any action.

But by using JavaScript tricks, you can <a href="https://www.yuiblog.com/blog/2009/02/23/managing-focus/">make any element keyboard accessible</a>. And if you build widgets, go even further by following <a href="https://www.w3.org/TR/wai-aria-practices/#kbd_generalnav">the rules of keyboard navigation</a>. You could even create a <a href="https://dev.opera.com/articles/view/accessible-drag-and-drop/">screen reader-compatible drag-and-drop interface</a>. But again, ask yourself a few questions:

*   Is it worth the hassle?
*   Does it really make the interface easier to understand?
*   Does it make it more natural to use?
*   Does it help all users reach their goal faster, or have you implemented the feature just because it looks cool?

Making the interface as simple as possible does not mean neutering your creativity. On the contrary, the easiest and simplest interfaces are the ones that have gone through a lot of research and design iterations. Great usability means not recognizing that something has been done to make the interface easy.</p>

## What Not To Use AJAX For

Never rely on AJAX to handle sensitive information, because modern debugging tools allow anyone to see what is happening on the page. Using the Firebug extension, I can get all of the information about the HTTP traffic of a certain document, including the AJAX requests:

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5d95017-d3af-499e-8658-829d278f7ce6/firebug.png" alt="AJAX requests as shown in Firebug" width="690" height="326" />

By analyzing these requests, I could glean information that you wouldn't want to show the world; for example, the endpoints of the services on your system (such as mail scripts), which I could exploit for my own purposes.

Nothing in your JavaScript or HTML is secure. I can change it on the fly and work around your protection mechanisms.

If you are not building a Web application but are merely offering articles for people to read or a catalogue to flip through, you probably shouldn't go the AJAX route anyway.

The other thing to consider is search engines. If you load all of your content with AJAX, you aren't offering much in your documents for search engines to index. Static HTML content is still best for search engine indexing—as well as performance, because pages can be packed and cached nicely on your server, if you do it right. Loading via AJAX brings up the content much faster for users and saves on bandwidth, but you will see less traffic from search engines. Something to consider.</p>

### The External Content Problem

One built-in security setting of AJAX is that you cannot load content on another server. This is critical, otherwise people would be able to call and inject whatever script they please from the Web. Definitely a bad idea.

You may sometimes need, though, to retrieve third-party content; i.e. load external content in your document as data (because you can always use iFrames to embed other documents). This is where we have to get clever with the technologies at our disposal.

The most common workaround for AJAX not being able to load something like <code>https://icant.co.uk/index.php</code> is to write a server-side script that loads the page and then prints it out. This is called a proxy, and you can see an example of the solution here.

Of <strong>utmost importance</strong> when using a proxy is to whitelist the URIs that you want to load. Do not simply load any URI off the Web, or else attackers would be able to read files from your server and use your server to send out spam and attack other servers, making it look as though you were the perpetrator.

Other ways to retrieve external content is by getting data in a special format called JSON-P or by using a hosted proxy service such as YQL. I'll keep this brief because there are several solutions to this problem. If you are interested in learning more, <a href="https://www.wait-till-i.com/2010/01/10/loading-external-content-with-ajax-using-jquery-and-yql/">check out this blog post on the subject</a>.</p>

## What To Use AJAX For

When used wisely, AJAX makes our life on the Web easier. If you're wondering when and how to use it, check out the examples in the <a href="https://developer.yahoo.com/ypatterns/">Design Pattern Gallery</a>, which are based on real user research. For starters, think about these use cases:

*   **Adding a large attachment to a message.**.  Nothing is more annoying than waiting for your browser to upload something without having a clue how fast and how far along it is. Browser progress bars give us a hint but no real numbers. The [Yahoo User Interface uploader](https://developer.yahoo.com/yui/examples/uploader/uploader-advanced-queue.html), as well as jQuery implementations such as [Uploadify](https://www.uploadify.com/demo/), show how that would look like in the browser.
*   **Handling a lot of small data sets.**.  A great example of this is the comments section in WordPress. Rather than having to click a lot of checkboxes or reload the page every time I want to delete or approve comments, all I do is click a few links.
*   **Rating content.**.  No need to reload the entire page if you just want a simple Yay or Nay from the user in response to a question.
*   **Displaying constantly changing content.**.  For example, financial tickers or instant updates from Twitter and Facebook.
*   Add your own use here.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [24 Excellent AJAX Tutorials](https://www.smashingmagazine.com/2008/10/50-excellent-ajax-tutorials/)
*   [Why AJAX Isn’t Enough](https://www.smashingmagazine.com/2015/01/why-ajax-isnt-enough/)
*   [How To Use AJAX In WordPress](https://www.smashingmagazine.com/2011/10/how-to-use-ajax-in-wordpress/)

I hope you've gained a few more insights into what AJAX is and how you can use it to improve the user experience in a way that is safe and doesn't leave certain segments of users out in the cold. AJAX makes stuff smoother, but nothing is more annoying than a supposed enhancement spoiling the whole experience.

{{< signature "al" >}}

