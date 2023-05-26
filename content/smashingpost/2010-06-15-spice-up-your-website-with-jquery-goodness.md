---
title: Spicing Up Your Website With jQuery Goodness
slug: spice-up-your-website-with-jquery-goodness
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51b5fcd3-fee7-4cee-b362-0b3b22987527/css-55.jpg
date: 2010-06-15T11:53:01.000Z
author: dmitry-dragilev
description: >-
  There comes a point in every website design when you simply want to give the
  website a little spice to impress the visitor and make it memorable. You want
  that sexy interaction to capture the user's attention. In our previous
  articles, we showed you how to spice up your website with [sexy
  buttons](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/),
  [practical
  elements](https://www.smashingmagazine.com/2009/12/16/stronger-better-faster-design-with-css3/)
  and [attractive visual
  effects](https://www.smashingmagazine.com/2010/01/25/the-new-hotness-using-css3-visual-effects/).

  In this article, we’ll discuss how to seduce your visitors with a little
  JavaScript action. In our examples, we'll be using jQuery, a fast and concise
  JavaScript library that simplifies HTML document traversing, event handling,
  animation and Ajax interactions for rapid Web development. Ready? Let's get
  things rolling!
categories:
  - Coding
  - jQuery
---
There comes a point in every website design when you simply want to give the website a little spice to impress the visitor and make it memorable. You want that sexy interaction to capture the user's attention. In our previous articles, we showed you how to spice up your website with [sexy buttons](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/), [practical elements](https://www.smashingmagazine.com/2009/12/16/stronger-better-faster-design-with-css3/) and [attractive visual effects](https://www.smashingmagazine.com/2010/01/25/the-new-hotness-using-css3-visual-effects/).

In this article, we’ll discuss how to seduce your visitors with a little JavaScript action. In our examples, we'll be using jQuery, a fast and concise JavaScript library that simplifies HTML document traversing, event handling, animation and Ajax interactions for rapid Web development. Ready? Let's get things rolling!

## Ajax Image Uploader

Image uploads will be much better after your read this. Guaranteed. By using a bit of jQuery, we can upload images with previews.

How do you upload images now? You select a file and click upload. Simple, right? Except that once you select your image, you can no longer see what was selected. The name of the file is at the end of the input field, and if the input field is short or the file path is deep, you won't see anything useful. You'll forget what you selected and have no idea what you're about to upload.

{{% feature-panel %}}

Now try this variation on uploading an image. We ditch the "Upload" button in favor of a "Save" button and fire the Ajax upload event as soon as a file is selected. The image is processed server-side, and a thumbnail is loaded onto the existing page. Doesn't that feel so much better? We now have a visual representation (imagine that!) of the image we selected.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48ce78b5-944d-478e-9aca-296f5d7474f4/ajax-upload-lead.jpg)](https://www.zurb.com/playground/ajax_upload)

This is particularly useful in larger forms where many fields will be submitted in a single action. It allows the user to review the form before pressing "Save" and see what image (or images) they selected.

**How does it work?** Here's the code. You'l need jQuery and the Ajax Upload jQuery plug-in. Link them up, and make sure jQuery is loaded first.

<pre><code class="language-markup tmp-xml">&lt;script src="/js/jquery.min.js" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="/js/ajaxupload.js" type="text/javascript"&gt;&lt;/script&gt;</code></pre>

Here is the JavaScript we will use in its entirety.

<pre><code class="language-javascript">$(document).ready(function(){

	var thumb = $('img#thumb');	

	new AjaxUpload('imageUpload', {
		action: $('form#newHotnessForm').attr('action'),
		name: 'image',
		onSubmit: function(file, extension) {
			$('div.preview').addClass('loading');
		},
		onComplete: function(file, response) {
			thumb.load(function(){
				$('div.preview').removeClass('loading');
				thumb.unbind();
			});
			thumb.attr('src', response);
		}
	});
});</code></pre>

Let's break the code down now and look at what's really going on. First, we attach the AjaxUpload behavior to our `file` form element.

<pre><code class="language-javascript">new AjaxUpload('imageUpload', {</code></pre>

Next, we specify where to post the Ajax upload. We want to keep all of our URLs in our HTML document, so we pass this URL using the `action` attribute of our `form` element.

<pre><code class="language-javascript">action: $('form#newHotnessForm').attr('action'),</code></pre>

Set the name of the `file` form element that will be posted to your server.

<pre><code class="language-javascript">name: 'image',</code></pre>

Add a `class` to your preview `div` to indicate that the image is uploading. In our case, we are applying a background image to the preview `div`. We also need to set the image tag to `display: none;` in the preview `div`, so that the loading background image is visible, as well as for a more subtle reason explained below.

<pre><code class="language-javascript">onSubmit: function(file, extension) {
     $('div.preview').addClass('loading');
},</code></pre>

When the image has been uploaded, we have to do two things:

*   First, we have to set the `src` attribute of our preview `img` tag to the new thumb.
*   Secondly, we have to remove the loading class. If we simply execute these things in that order, then we would see an annoying flicker of the old image when the loading class has been removed but the new image has not yet loaded.

We avoid the annoying flicker of the old image by waiting to remove the loading class until after the preview image's `load` event fires. We also `unbind` our listener after it has fired because we want to capture this event only once.

<pre><code class="language-javascript">onComplete: function(file, response) {
	thumb.load(function(){
		$('div.preview').removeClass('loading');
		thumb.unbind();
	});</code></pre>

Lastly, we set the source of the preview image to the thumbnail that our server has just created. In this example, the response from the Ajax call is just the thumbnail's URL as text. You could return it in whatever fancy format you like.

<pre><code class="language-javascript">thumb.attr('src', response);
}</code></pre>

If JavaScript-support is disabled in user's browsers, they will get the good old submit form without the interactive preview. Clean and functional solution, with rich interactions for users with more capable browsers.

<div style="background: #f4f4f4; padding: 20px; margin: 30px 0px;">
	<a href="https://www.zurb.com/playground/ajax_upload" style="border: solid 1px #ddd; float: left; margin-right: 20px"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70836b3e-c5e2-4996-823c-ba4c2a7df5a3/ajax-upload-box.png" /></a>
	<h4 style="margin-top: 0px"><a href="https://www.zurb.com/playground/ajax_upload">Better Image Uploads</a></h4>
	<p>Want to try out and implement the image uploader yourself? Check out a live demo, the example code and more for this improved way to support image uploads on your website.</p>
	<p><a href="https://www.zurb.com/playground/ajax_upload">Check out the live demo &raquo;</a></p>
</div>

## Validation With jQuery Text-Change Event

Here's a pretty **common problem**: you have a text form to validate client-side. Doing this is easy enough when the form is submitted, but in some cases doing it as the user is typing is best. For example, imagine how annoying [Twitter](https://twitter.com) would be if you had to submit your tweet before you were told how many characters it was.

Keep in mind, though, that this kind of immediate validation can be overused or abused. Don't insult the user by congratulating them for every piece of text they enter in a field.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5de2f8c-1188-4892-955f-7c96a3895c9b/image22.jpg)](https://www.zurb.com/playground/jquery-text-change-custom-event)

Implementing this requires that you bind events to the `keyup` event — and a couple other events if you want to detect text changes on cut-and-paste events. Even if you're a JavaScript god, having to keep writing this logic over and over again is tedious. We created a text-change event plug-in to help you handle all text-change events.</p>

### Detecting the Text (Better Than Twitter)

We begin by detecting text in the standard `textarea`. Look at the shot below: looks like a standard `textarea` with a disabled "Save" button.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff333d99-5aeb-4453-b0fd-70c6910ea703/detecttextone.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

If you add text to the field, then the "Save" button enables and then disables when no text is in the field. Moderately impressive, right?

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/616b2289-002a-4c11-827a-2f8c9bbb996e/detectext.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

Now, what if you try copying, pasting or cutting text with the shortcut keys? That works as well. What about right-clicking or using the "Edit" menu? Works, too. (By the way, Twitter doesn't support the click or menu interactions.)

The code behind this is pretty simple. You'll need to download and link up the textchange plug-in.

<pre><code class="language-markup tmp-xml">&lt;script src="/javascripts/plugins/jquery.textchange.js"&gt;&lt;/script&gt;</code></pre>

The plug-in adds the `hastext` and `notext` events, to which you can bind `input` and `textarea` elements.

<pre><code class="language-markup tmp-xml">$('#exhibita').bind('hastext', function () {
  $('#exhibitaButton').removeClass('disabled').attr('disabled', false);
});

$('#exhibita').bind('notext', function () {
  $('#exhibitaButton').addClass('disabled').attr('disabled', true);
});</code></pre>

The `hastext` event fires when the element goes from having no text to having text, and the `notext` event fires when the element goes from having text to being blank. Looking for more advanced validation? Keep reading.</p>

### Detecting Text Change

What about detecting text change in the field?

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76630c71-404e-4918-a4c7-4fe78f4011fe/change.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

This is very easy, too. A third `textchange` event fires whenever the text changes, and it provides you with the previous value.

<pre><code class="language-javascript">$('#exhibitb').bind('textchange', function (event, previousText) {
  $('#output').append('<p>Text changed from &lt;strong&gt;' + 
    previousText + '&lt;/strong&gt; to &lt;strong&gt;' + $(this).val() + 
    '&lt;/strong&gt; &lt;/p&gt;');
});</code></pre>

### Twitter-Style Validation

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ad6466c-bf30-4e4a-8c1a-a3d5c3ee0e71/twit.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

We can implement some simple Twitter-like validation with just a single line and our `textchange` event.

<pre><code class="language-javascript">$('#twitter').bind('textchange', function (event, previousText) {
  $('#charactersLeft').html( 140 - parseInt($(this).val().length) );
});</code></pre>

### Ajax Save

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb80b5a-8efa-48d1-a15f-7c4e01ba7e67/ajax.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

With a little more code and `setTimeout`, we can hook up an Ajax call to save a few seconds once the user stops editing. The Ajax call is just stubbed out here, but you get the idea.

<pre><code class="language-javascript">var timeout;
$('#ajaxSave').bind('textchange', function () {
  clearTimeout(timeout);
  $('#ajaxFired').html('<strong>Typing...</strong>');
    var self = this;
    timeout = setTimeout(function () {
    $('#ajaxFired').html('<strong>Saved</strong>: ' + $(self).val());
  }, 1000);
});</code></pre>

### Validate Text

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5ba1066-035e-412e-84dd-85c4bcde7ffa/comp.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

This may sound contrived, but say you would like to ensure that the two words "[companion cube](https://en.wikipedia.org/wiki/Portal_(video_game))" are in the emergency intelligence incinerator (i.e. the text field) before allowing the user to continue. No problem:

<pre><code class="language-javascript">$('#emergencyIntelligenceIncinerator').bind('textchange', function () {
  if ($(this).val().indexOf('companion cube') !== -1) {
    $('#continue').removeClass('disabled').attr('disabled', false);
  }
});</code></pre>

jQuery Text-Change event can be very useful for web applications that are aiming for a high level of interactivity and visual feedback. You may even want to analyze some of the input and provide helpful clues. For instance, if the user is opening a new ticket in your support area, you may want to present links to possibly related answers in the support forum. Be sure not to analyze every keystroke, though, as it could result in a significant overhead for the back-end. And it is also important to keep in mind that the immediacy of the application should be subtle and should not interrupt user's interaction.

<div style="background: #f4f4f4; padding: 20px; margin: 30px 0px;">
	<a href="https://www.zurb.com/playground/jquery-text-change-custom-event" style="border: solid 1px #ddd; float: left; margin-right: 20px"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b516c93d-e3f7-488c-9e15-94fc20e26783/text-change-box.png" /></a>
	<h4 style="margin-top: 0px"><a href="https://www.zurb.com/playground/jquery-text-change-custom-event">Text Change Events</a></h4>
	<p>Don't fret about complicated validation, text events and edge cases. Check out the live demo and download the plug-in, which makes it a snap to perform a number of functions on text boxes to look for values, changes and more.</p>
	<p><a href="https://www.zurb.com/playground/jquery-text-change-custom-event">Check out the live demo &raquo;</a></p>
</div>

## JavaScript Annotation Plug-In

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81479b4f-9fab-44ad-9049-342287e80853/image12.jpg)](https://www.zurb.com/playground/javascript-annotation-plugin)

An application that we recently developed ([Notable](https://www.notableapp.com)) allows users to collect user feedback through interactive tools. Most of these tools require the user to annotate an image. We figured that many folks are trying to solve the same problem, so why not create a plug-in that they can use? This is the result. Our plug-in uses jQuery and makes it very simple to add and save image annotations.

To start off, download the JS Annotation Plug-In. To use the plug-in, just link up jQuery (1.2.3 or higher) and our plug-in.

<pre><code class="language-markup tmp-xml">&lt;script src="/javascripts/plugins/jquery.js"&gt;&lt;/script&gt;
&lt;script src="/javascripts/plugins/jquery.annotate.js"&gt;&lt;/script&gt;</code></pre>

Meet Nutmeg the Dog. After clicking on a random spot on Nutmeg, you'll see the black circle appear.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbc42903-547e-4735-ab27-79e5d57a4cd6/first.jpg)](https://www.zurb.com/playground/javascript-annotation-plugin)

<pre><code class="language-javascript">function blackNote() {
  return $(document.createElement('span')).addClass('black circle note')
}

$('#nutmeg').annotatableImage(blackNote);</code></pre>

Here's how it works: The first parameter to `annotatableImage` is a function that is implemented by you and that defines the element to be added when you click. In the example above, that function is called `blackNote`. Simple, right?

### How to Save the Annotations?

Glad you asked. Use the jQuery selector to grab all the elements that you want to serialize, and call the `serializeAnnotations` function.

<pre><code class="language-javascript">$('#nutmeg span.note').serializeAnnotations();</code></pre>

<p>These values are returned in an array of objects, so you can easily save them with an Ajax call. The <code>response_time</code> variable is the time in milliseconds that the user took to add the annotation after you made the call to <code>annotatableImage</code>.

<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/508978ff-ddbf-41e7-9838-befbf44ae351/savea.png" /></a></p>

### Let's Get Relative

<p>In our website feedback tool we needed to show our annotations in different-sized versions of our original image. The full size is just won't always cut it in the world of good design. To make this easier, we store the x and y positions of our annotations relative to the width and height of the image.</p>

<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8523275f-52de-4ef6-8a8a-54c3e46ca18f/small.jpg" /></a></p>

<p>If you didn't pass fifth-grade math, don't worry: our plug-in does all the basic arithmetic for you. Warning: if you change the aspect ratio or crop the image, this will not work properly. Also, be sure to always store x and y as floating-point data types.</p>

<pre><code class="language-javascript">$('#smallNutmeg').addAnnotations(blackNote, annotations);</code></pre>

<p>The annotations variable is an array of objects with x and y attributes. It looks exactly like the array returned by the <code>serializeAnnotations</code> function without the <code>response_time</code> attribute. What other attributes might you put in the annotation object? Read on…</p>

### Passing Attributes

<p>We may want to pass some data to each of our annotations when adding existing annotations. Maybe we have numbered our annotations, or have added special classes or behaviors, whatever.</p>

<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63f586fc-26a4-4063-981b-9aa80aee3402/numdata.jpg" /></a></p>

<p>The function we pass to <code>annotatableImage</code> accepts a single parameter, which is the annotation object from the array that you passed to <code>addAnnotations</code>. In this example, we added a position attribute, which we will display.</p>

<pre><code class="language-javascript">$('#numberedNutmeg').addAnnotations(function(annotation){
  return $(document.createElement('span')).
    addClass('black circle note').html(annotation.position);
},[
    {x: 0.3875, y: 0.3246, position: 4}, 
    {x: 0.57, y: 0.329, position: 2}
  ]
);</code></pre>

### Hitting All the Positions

<p>When we were annotating Nutmeg, you may have noticed that the annotation was centered at your click position. This may be great for circles and sparkly unicorns, but sometimes we may want to position our annotations differently.</p>

<p>The <code>xPosition</code> and <code>yPosition</code> options allow you to indicate where the annotation is positioned relative to the click. Options are middle (default), left, right and middle (default), top, bottom, respectively.</p>

<pre><code class="language-javascript">$('#labeledNutmeg').annotatableImage(function(annotation){
  return $(document.createElement('span')).addClass('set-label');
}, {xPosition: 'left'});</code></pre>

<p>Give Nutmeg some clicks on our demo page to see what we're talking about. In this example, we are positioning the click on the <strong>left</strong> side of the annotation.</p>

<p>Warning: make sure to pass the <code>xPosition</code> and <code>yPosition</code> to the <code>serializeAnnotations</code> function if you set these options in <code>annotatableImage</code>. The default behavior is to calculate the x and y values from the middle of the annotation.</p>

<div style="background: #f4f4f4; padding: 20px; margin: 30px 0px;">
	<a href="https://www.zurb.com/playground/javascript-annotation-plugin" style="border: solid 1px #ddd; float: left; margin-right: 20px"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e30fd2f-7009-43a2-8032-4e51f0c87997/javascript-annotations-box.png" /></a>
	<h4 style="margin-top: 0px"><a href="https://www.zurb.com/playground/javascript-annotation-plugin">JavaScript Annotations Plug-In</a></h4>
	<p>Start supporting powerful, easily implemented annotations on your website or app with this plug-in. Adding notes, descriptions and more to these annotations is simple.</p>
	<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin">Check out the live demo &raquo;</a></p>
</div>

## Bonus: CSS Grid Builder

<p><a href="https://www.zurb.com/playground/css-grid-builder"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2e3f9d8-e608-4e1f-822b-821257d576e4/grid-builder-lead.png" /></a></p>

<p>In our design process, we have been using a flexible grid framework that lets us rapidly prototype and implement websites. Recently, we've created some variant grids for different widths and gutter sizes, so we thought, why not just create grids on the fly with a simple tool?</p>

<pre><code class="language-markup tmp-xml">$('#exhibita').bind('hastext', function () {
  $('#exhibitaButton').removeClass('disabled').attr('disabled', false);
});

$('#exhibita').bind('notext', function () {
  $('#exhibitaButton').addClass('disabled').attr('disabled', true);
});</code></pre>

The `hastext` event fires when the element goes from having no text to having text, and the `notext` event fires when the element goes from having text to being blank. Looking for more advanced validation? Keep reading.</p>

### Detecting Text Change

What about detecting text change in the field?

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76630c71-404e-4918-a4c7-4fe78f4011fe/change.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

This is very easy, too. A third `textchange` event fires whenever the text changes, and it provides you with the previous value.

<pre><code class="language-javascript">$('#exhibitb').bind('textchange', function (event, previousText) {
  $('#output').append('<p>Text changed from &lt;strong&gt;' + 
    previousText + '&lt;/strong&gt; to &lt;strong&gt;' + $(this).val() + 
    '&lt;/strong&gt; &lt;/p&gt;');
});</code></pre>

### Twitter-Style Validation

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ad6466c-bf30-4e4a-8c1a-a3d5c3ee0e71/twit.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

We can implement some simple Twitter-like validation with just a single line and our `textchange` event.

<pre><code class="language-javascript">$('#twitter').bind('textchange', function (event, previousText) {
  $('#charactersLeft').html( 140 - parseInt($(this).val().length) );
});</code></pre>

### Ajax Save

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb80b5a-8efa-48d1-a15f-7c4e01ba7e67/ajax.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

With a little more code and `setTimeout`, we can hook up an Ajax call to save a few seconds once the user stops editing. The Ajax call is just stubbed out here, but you get the idea.

<pre><code class="language-javascript">var timeout;
$('#ajaxSave').bind('textchange', function () {
  clearTimeout(timeout);
  $('#ajaxFired').html('<strong>Typing...</strong>');
    var self = this;
    timeout = setTimeout(function () {
    $('#ajaxFired').html('<strong>Saved</strong>: ' + $(self).val());
  }, 1000);
});</code></pre>

### Validate Text

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5ba1066-035e-412e-84dd-85c4bcde7ffa/comp.png)](https://www.zurb.com/playground/jquery-text-change-custom-event)

This may sound contrived, but say you would like to ensure that the two words "[companion cube](https://en.wikipedia.org/wiki/Portal_(video_game))" are in the emergency intelligence incinerator (i.e. the text field) before allowing the user to continue. No problem:

<pre><code class="language-javascript">$('#emergencyIntelligenceIncinerator').bind('textchange', function () {
  if ($(this).val().indexOf('companion cube') !== -1) {
    $('#continue').removeClass('disabled').attr('disabled', false);
  }
});</code></pre>

jQuery Text-Change event can be very useful for web applications that are aiming for a high level of interactivity and visual feedback. You may even want to analyze some of the input and provide helpful clues. For instance, if the user is opening a new ticket in your support area, you may want to present links to possibly related answers in the support forum. Be sure not to analyze every keystroke, though, as it could result in a significant overhead for the back-end. And it is also important to keep in mind that the immediacy of the application should be subtle and should not interrupt user's interaction.

<div style="background: #f4f4f4; padding: 20px; margin: 30px 0px;">
	<a href="https://www.zurb.com/playground/jquery-text-change-custom-event" style="border: solid 1px #ddd; float: left; margin-right: 20px"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b516c93d-e3f7-488c-9e15-94fc20e26783/text-change-box.png" /></a>
	<h4 style="margin-top: 0px"><a href="https://www.zurb.com/playground/jquery-text-change-custom-event">Text Change Events</a></h4>
	<p>Don't fret about complicated validation, text events and edge cases. Check out the live demo and download the plug-in, which makes it a snap to perform a number of functions on text boxes to look for values, changes and more.</p>
	<p><a href="https://www.zurb.com/playground/jquery-text-change-custom-event">Check out the live demo &raquo;</a></p>
</div>

## JavaScript Annotation Plug-In

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81479b4f-9fab-44ad-9049-342287e80853/image12.jpg)](https://www.zurb.com/playground/javascript-annotation-plugin)

An application that we recently developed ([Notable](https://www.notableapp.com)) allows users to collect user feedback through interactive tools. Most of these tools require the user to annotate an image. We figured that many folks are trying to solve the same problem, so why not create a plug-in that they can use? This is the result. Our plug-in uses jQuery and makes it very simple to add and save image annotations.

To start off, download the JS Annotation Plug-In. To use the plug-in, just link up jQuery (1.2.3 or higher) and our plug-in.

<pre><code class="language-markup tmp-xml">&lt;script src="/javascripts/plugins/jquery.js"&gt;&lt;/script&gt;
&lt;script src="/javascripts/plugins/jquery.annotate.js"&gt;&lt;/script&gt;</code></pre>

Meet Nutmeg the Dog. After clicking on a random spot on Nutmeg, you'll see the black circle appear.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbc42903-547e-4735-ab27-79e5d57a4cd6/first.jpg)](https://www.zurb.com/playground/javascript-annotation-plugin)

<pre><code class="language-javascript">function blackNote() {
  return $(document.createElement('span')).addClass('black circle note')
}

$('#nutmeg').annotatableImage(blackNote);</code></pre>

Here's how it works: The first parameter to `annotatableImage` is a function that is implemented by you and that defines the element to be added when you click. In the example above, that function is called `blackNote`. Simple, right?

### How to Save the Annotations?

Glad you asked. Use the jQuery selector to grab all the elements that you want to serialize, and call the `serializeAnnotations` function.

<pre><code class="language-javascript">$('#nutmeg span.note').serializeAnnotations();</code></pre>

<p>These values are returned in an array of objects, so you can easily save them with an Ajax call. The <code>response_time</code> variable is the time in milliseconds that the user took to add the annotation after you made the call to <code>annotatableImage</code>.

<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/508978ff-ddbf-41e7-9838-befbf44ae351/savea.png" /></a></p>

### Let's Get Relative

<p>In our website feedback tool we needed to show our annotations in different-sized versions of our original image. The full size is just won't always cut it in the world of good design. To make this easier, we store the x and y positions of our annotations relative to the width and height of the image.</p>

<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8523275f-52de-4ef6-8a8a-54c3e46ca18f/small.jpg" /></a></p>

<p>If you didn't pass fifth-grade math, don't worry: our plug-in does all the basic arithmetic for you. Warning: if you change the aspect ratio or crop the image, this will not work properly. Also, be sure to always store x and y as floating-point data types.</p>

<pre><code class="language-javascript">$('#smallNutmeg').addAnnotations(blackNote, annotations);</code></pre>

<p>The annotations variable is an array of objects with x and y attributes. It looks exactly like the array returned by the <code>serializeAnnotations</code> function without the <code>response_time</code> attribute. What other attributes might you put in the annotation object? Read on…</p>

### Passing Attributes

<p>We may want to pass some data to each of our annotations when adding existing annotations. Maybe we have numbered our annotations, or have added special classes or behaviors, whatever.</p>

<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63f586fc-26a4-4063-981b-9aa80aee3402/numdata.jpg" /></a></p>

<p>The function we pass to <code>annotatableImage</code> accepts a single parameter, which is the annotation object from the array that you passed to <code>addAnnotations</code>. In this example, we added a position attribute, which we will display.</p>

<pre><code class="language-javascript">$('#numberedNutmeg').addAnnotations(function(annotation){
  return $(document.createElement('span')).
    addClass('black circle note').html(annotation.position);
},[
    {x: 0.3875, y: 0.3246, position: 4}, 
    {x: 0.57, y: 0.329, position: 2}
  ]
);</code></pre>

### Hitting All the Positions

<p>When we were annotating Nutmeg, you may have noticed that the annotation was centered at your click position. This may be great for circles and sparkly unicorns, but sometimes we may want to position our annotations differently.</p>

<p>The <code>xPosition</code> and <code>yPosition</code> options allow you to indicate where the annotation is positioned relative to the click. Options are middle (default), left, right and middle (default), top, bottom, respectively.</p>

<pre><code class="language-javascript">$('#labeledNutmeg').annotatableImage(function(annotation){
  return $(document.createElement('span')).addClass('set-label');
}, {xPosition: 'left'});</code></pre>

<p>Give Nutmeg some clicks on our demo page to see what we're talking about. In this example, we are positioning the click on the <strong>left</strong> side of the annotation.</p>

<p>Warning: make sure to pass the <code>xPosition</code> and <code>yPosition</code> to the <code>serializeAnnotations</code> function if you set these options in <code>annotatableImage</code>. The default behavior is to calculate the x and y values from the middle of the annotation.</p>

<div style="background: #f4f4f4; padding: 20px; margin: 30px 0px;">
	<a href="https://www.zurb.com/playground/javascript-annotation-plugin" style="border: solid 1px #ddd; float: left; margin-right: 20px"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e30fd2f-7009-43a2-8032-4e51f0c87997/javascript-annotations-box.png" /></a>
	<h4 style="margin-top: 0px"><a href="https://www.zurb.com/playground/javascript-annotation-plugin">JavaScript Annotations Plug-In</a></h4>
	<p>Start supporting powerful, easily implemented annotations on your website or app with this plug-in. Adding notes, descriptions and more to these annotations is simple.</p>
	<p><a href="https://www.zurb.com/playground/javascript-annotation-plugin">Check out the live demo &raquo;</a></p>
</div>

## Bonus: CSS Grid Builder

<p><a href="https://www.zurb.com/playground/css-grid-builder"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2e3f9d8-e608-4e1f-822b-821257d576e4/grid-builder-lead.png" /></a></p>

<p>In our design process, we have been using a flexible grid framework that lets us rapidly prototype and implement websites. Recently, we've created some variant grids for different widths and gutter sizes, so we thought, why not just create grids on the fly with a simple tool?</p>

<p>Please feel free to use the <a href="https://www.zurb.com/playground/css-grid-builder">ZURB CSS Grid Builder</a> to build and generate source code for a simple, flexible grid framework for variable grid sizes and column numbers. Play around with it &mdash; we prefer it to a more full-featured solution such as YUI because it's lighter and a little more flexible.</p>

<div style="background: #f4f4f4; padding: 20px; margin: 30px 0px;">
	<a href="https://www.zurb.com/playground/css-grid-builder" style="border: solid 1px #ddd; float: left; margin-right: 20px"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14199cb5-2680-461b-8cd8-d512d22de872/grid-builder-box.png" /></a>
	<h4 style="margin-top: 0px"><a href="https://www.zurb.com/playground/css-grid-builder">CSS Grid Builder</a></h4>
	<p>Check out the CSS Grid Builder in the playground. You can preview the grid in different-sized browser windows and output a complete CSS framework.</p>
	<p><a href="https://www.zurb.com/playground/css-grid-builder">Check out the grid builder &raquo;</a></p>
</div>

{{< signature "al" >}}

