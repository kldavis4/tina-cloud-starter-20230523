---
title: 'Image Manipulation With jQuery And PHP GD'
slug: image-manipulation-with-jquery-and-php-gd
date: 2011-04-05T09:05:35.000Z
author: andy-croxall
summary: >-
  Learn how to combine JavaScript/jQuery with PHP and, particularly, PHP’s GD library to create an image manipulation tool to upload an image, then crop it, and finally save the revised version to the server.
description: >-
  In this article, Andy Croxall looks at how to combine JavaScript/jQuery with PHP and, particularly, PHP’s GD library to create an image manipulation tool to upload an image, then crop it, and finally save the revised version to the server.
categories:
  - Coding
  - PHP
  - jQuery
  - Responsive Images
---

One of the numerous advantages brought about by the explosion of jQuery and other JavaScript libraries is the ease with which you can create interactive tools for your site. When combined with server-side technologies such as PHP, this puts a serious amount of power at your finger tips.

In this article, I’ll be looking at how to combine JavaScript/jQuery with PHP and, particularly, PHP’s GD library to create an image manipulation tool to upload an image, then crop it and finally save the revised version to the server. Sure, there are plugins out there that you can use to do this; but this article aims to show you what’s behind the process. You can <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a7185d-7761-4418-9e4a-c3fdb1b284c9/manipulation-img-crop.zip">download the source files</a> (*updated*) for reference.

We’ve all seen this sort of Web application before &mdash; Facebook, Flickr, t-shirt-printing sites. The advantages are obvious; by including a functionality like this, you alleviate the need to edit pictures manually from your visitors, which has obvious drawbacks. They may not have access to or have the necessary skills to use Photoshop, and in any case why would you want to make the experience of your visitors more difficult?

{{% feature-panel %}}

## Before You Start

For this article, you would ideally have had at least some experience working with PHP. Not necessarily GD &mdash; I’ll run you through that part, and GD is very friendly anyway. You should also be at least intermediate level in JavaScript, though if you’re a fast learning beginner, you should be fine as well.

A quick word about the technologies you’ll need to work through this article. You’ll need a PHP test server running the GD library, either on your hosting or, if working locally, through something like <a href="https://www.apachefriends.org">XAMPP</a>. GD has come bundled with PHP as standard for some time, but you can confirm this by running the `phpinfo()` function and verifying that it’s available on your server. Client-side-wise you’ll need a text editor, some pictures and a copy of jQuery.

## Setting Up The Files

And off we go, then. Set up a working folder and create four files in it: *index.php*, *js.js*, *image_manipulation.php* and *css.css*. *index.php* is the actual webpage, *js.js* and *css.css* should be obvious, while *image_manipulation.php* will store the code that handles the uploaded image and then, later, saves the manipulated version.

In *index.php*, first let’s add a line of PHP to start a PHP session and call in our *image_manipulation.php* file.

After that, add in the DOCTYPE and skeleton-structure of the page (header, body areas etc) and call in jQuery and the CSS sheet via script and link tags respectively.

Add a directory to your folder, called *imgs*, which will receive the uploaded files. If you’re working on a remote server, ensure you set the permissions on the directory such that the script will be able to save image files in it.

First, let’s set up and apply some basic styling to the upload facility.

## The Upload Functionality

Now to some basic HTML. Let’s add a heading and a simple form to our page that will allow the user to upload an image and assign that image a name:

<pre><code class="language-html">&lt;h1&gt;Image uploader and manipulator&lt;/h1&gt;
&lt;form id="imgForm" action="index.php" enctype="multipart/form-data" method="POST"&gt;&lt;label for="img_upload"&gt;Image on your PC to upload&lt;/label&gt; &lt;label for="img_name"&gt;Give this image a name&lt;/label&gt;&lt;/form&gt;
</code></pre>

Please note that we specify *enctype='multipart/form-data'* which is necessary whenever your form contains file upload fields.

As you can see, the form is pretty basic. It contains 3 fields: an upload field for the image itself, a text field, so the user can give it a name and a submit button. The submit button has a name so it can act as an identifier for our PHP handler script which will know that the form was submitted.

Let’s add a smattering of CSS to our stylesheet:

<pre><code class="language-css">/* -----------------
| UPLOAD FORM
----------------- */
#imgForm { border: solid 4px #ddd; background: #eee; padding: 10px; margin: 30px; width: 600px; overflow:hidden;}
	#imgForm label { float: left; width: 200px; font-weight: bold; color: #666; clear:both; padding-bottom:10px; }
	#imgForm input { float: left; }
	#imgForm input[type="submit"] {clear: both; }
	#img_upload { width: 400px; }
	#img_name { width: 200px; }</code></pre>

Now we have the basic page set up and styled. Next we need to nip into *image_manipulation.php* and prepare it to receive the submitted form. Which leads nicely on to validation...

## Validating The Form

Open up *image_manipulation.php*. Since we made a point above of including it into our HTML page, we can rest assured that when it’s called into action, it will be present in the environment.

Let’s set up a condition, so the PHP knows what task it is being asked to do. Remember we named our submit button *upload_form_submitted*? PHP can now check its existence, since the script knows that it should start handling the form.

This is important because, as I said above, the PHP script has two jobs to do: to handle the uploaded form and to save the manipulated image later on. It therefore needs a technique such as this to know which role it should be doing at any given time.

<pre><code class="language-php">/* -----------------
| UPLOAD FORM - validate form and handle submission
----------------- */

if (isset($_POST['upload_form_submitted'])) {
	//code to validate and handle upload form submission here
}</code></pre>

So if the form was submitted, the condition resolves to `true` and whatever code we put inside, it will execute. That code will be validation code. Knowing that the form was submitted, there are now five possible obstacles to successfully saving the file: 1) the upload field was left blank; 2) the file name field was left blank; 3) both these fields were filled in, but the file being uploaded isn’t a valid image file; 4) an image with the desired name already exists; 5) everything is fine, but for some reason, the server fails to save the image, perhaps due to file permission issues. Let’s look at the code behind picking up each of these scenarios, should any occur, then we’ll put it all together to build our validation script.

Combined into a single validation script, the whole code looks as follows.

<pre><code class="language-php">/* -----------------
| UPLOAD FORM - validate form and handle submission
----------------- */

if (isset($_POST['upload_form_submitted'])) {

	//error scenario 1
	if (!isset($_FILES['img_upload']) || empty($_FILES['img_upload']['name'])) {
		$error = "Error: You didn’t upload a file";

	//error scenario 2
	} else if (!isset($_POST['img_name']) || empty($_FILES['img_upload'])) {
		$error = "Error: You didn’t specify a file name";
	} else {

		$allowedMIMEs = array('image/jpeg', 'image/gif', 'image/png');
		foreach($allowedMIMEs as $mime) {
			if ($mime == $_FILES['img_upload']['type']) {
				$mimeSplitter = explode('/', $mime);
				$fileExt = $mimeSplitter[1];
				$newPath = 'imgs/'.$_POST['img_name'].'.'.$fileExt;
				break;
			}
		}

		//error scenario 3
		if (file_exists($newPath)) {
			$error = "Error: A file with that name already exists";

		//error scenario 4
		} else if (!isset($newPath)) {
			$error = 'Error: Invalid file format - please upload a picture file';

		//error scenario 5
		} else if (!copy($_FILES['img_upload']['tmp_name'], $newPath)) {
			$error = 'Error: Could not save file to server';

		//...all OK!
		} else {
			$_SESSION['newPath'] = $newPath;
			$_SESSION['fileExt'] = $fileExt;
		}
	}
}</code></pre>

There are a couple of things to note here.

### `$error` and `$_SESSION['newPath']`

Firstly, note that I’m using a variable, $error, to log whether we hit any of the hurdles. If no error occurs and the image is saved, we set a session variable,<code>$\_SESSION['new_path']</code>, to store the path to the saved image. This will be helpful in the next step where we need to display the image and, therefore, need to know its <code>SRC</code>.

I’m using a session variable rather than a simple variable, so when the time comes for our PHP script to crop the image, we don’t have to pass it a variable informing the script which image to use &mdash; the script will already know the context, because it will remember this session variable. Whilst this article doesn’t concern itself deeply with security, this is a simple precaution. Doing this means that the user can affect only the image he uploaded, rather than, potentially, someone else’s previously-saved image &mdash; the user is locked into manipulating only the image referenced in `$error` and has no ability to enforce the PHP script to affect another image.

### The `$_FILES` Superglobal

Note that even though the form was sent via POST, we access the file upload not via the `$_POST` superglobal (i.e. variables in PHP which are available in all scopes throughout a script), but via the special `$_FILES` superglobal. PHP automatically assigns file fields to that, provided the form was sent with the required `enctype='multipart/form-data'` attribute. Unlike the `$_POST` and `$_GET` superglobals, the `$_FILES` superglobal goes a little "deeper" and is actually a multi-dimensional array. Through this, you can access not only the file itself but also a variety of meta data related to it. You’ll see how we can use this information shortly. We use this meta data in the third stage of validation above, namely checking that the file was a valid image file. Let’s look at this code in a little more detail.

### Confirming The Upload Is An Image

Any time you’re allowing users to upload files to your server, you obviously want to assume full control of precisely what sort of files you allow to be uploaded. It should be blindingly obvious, but you don’t want people able to upload just any file to you server - this needs to be something you control, and tightly.

We could check by file extension - only this would be insecure. Just because something has a .jpg extension, doesn’t mean its inner code is that of a picture. Instead, we check by MIME-type, which is more secure (though still not totally perfect).

To this end we check the uploaded file’s MIME-type - which lives in the ‘type’ property of its array - against a white list of allowed MIME-types.

<pre><code class="language-php">$allowedMIMEs = array('image/jpeg', 'image/gif', 'image/png');
foreach($allowedMIMEs as $mime) {
	if ($mime == $_FILES['img_upload']['type']) {
		$mimeSplitter = explode('/', $mime);
		$fileExt = $mimeSplitter[1];
		$newPath = 'imgs/'.$_POST['img_name'].'.'.$fileExt;
		break;
	}
}</code></pre>

If a match is found, we extract its extension and use that to build the name we’ll use to save the file.

To extract the extension we exploit the fact that MIME-types are always in the format something/something - i.e. we can rely on the forward slash. We therefore ‘explode’ the string based on that delimited. Explode returns an array of parts - in our case, two parts, the part of the MIME-type either side of the slash. We know, therefore, that the second part of the array ([1]) is the extension associated with the MIME-type.

Note that, if a matching MIME-type is found, we set two variables: $newPath and $fileExt. Both of these will be important later to the PHP that actually saves the file, but the former is also used, as you can see, by error scenario 4 as a means of detecting whether MIME look-up was successful.

### Saving The File

All uploaded files are assigned a temporary home by the server until such time as the session expires or they are moved. So saving the file means moving the file from its temporary location to a permanent home. This is done via the `copy()` function, which needs to know two rather obvious things: what’s the path to the temporary file, and what’s the path to where we want to put it.

The answer to the first question is read from the `tmp_name` part of the `$_FILES` superglobal. The answer to the second is the full path, including new filename, to where you want it to live. So it is formed of the name of the directory we set up to store images (*/imgs*), plus the new file name (i.e. the value entered into the `img_name` field) and the extension. Let’s assign it to its own variable, `$newPath` and then save the file:

<pre><code class="language-php">$newPath = 'imgs/'.$_POST['img_name'].'.'.$fileExt;
...
copy($_FILES['img_upload']['tmp_name'],$newPath);</code></pre>

{{% ad-panel-leaderboard %}}

## Reporting Back and Moving On

What happens next depends entirely on whether an error occurred, and we can find it out by looking up whether `$error` is set. If it is, we need to communicate this error back to the user. If it’s not set, it’s time to move on and show the image and let the user manipulate it. Add the following above your form:

<pre><code class="language-php">&lt;?php if (isset($error)) echo '&lt;p id="error"&gt;'.$error.'&lt;/p&gt;'; ?&gt;</code></pre>

If there’s an error, we’d want to show the form again. But the form is currently set to show regardless of the situation. This needs to change, so that it shows only if no image has been uploaded yet, i.e. if the form hasn’t been submitted yet, or if it has but there was an error. We can check whether an uploaded image has been saved by interrogating the `$_SESSION['newPath']` variable. Wrap your form HTML in the following two lines of code:

<pre><code class="language-php">&lt;?php if (!isset($_SESSION['newPath']) || isset($_GET['true'])) { ?&gt;

&lt;?php } else echo '&lt;img src="'.$_SESSION['newPath'].'" /&gt;'; ?&gt;</code></pre>

Now the form appears only if an uploaded image isn’t registered &mdash; i.e. `$_SESSION['newPath']` isn’t set &mdash; or if `new=true` is found in the URL. (This latter part provides us with a means of letting the user start over with a new image upload should they wish so; we’ll add a link for this in a moment). Otherwise, the uploaded image displays (we know where it lives because we saved its path in `$_SESSION['newPath']`).

This is a good time to take stock of where we are, so try it out. Upload an image, and verify that that it displays. Assuming it does, it’s time for our JavaScript to provide some interactivity for image manipulation.

## Adding Interactivity

First, let’s extend the line we just added so that we a) give the image an ID to reference it later on; b) call the JavaScript itself (along with jQuery); and c) we provide a "start again" link, so the user can start over with a new upload (if necessary). Here is the code snippet:

<pre><code class="language-php">&lt;?php } else { ?&gt;
	&lt;img id="uploaded_image" src="" /&gt;
	&lt;p&gt;<a href="index.php?new=true">start over with new image</a>
  &lt;script src="https://www.google.com/jsapi"&gt;&lt;/script&gt; 
  &lt;script&gt;google.load("jquery", "1.5");&lt;/script&gt; 
  &lt;script src="js.js"&gt;&lt;/script&gt;
</code></pre>

Note that I defined an ID for the image, not a class, because it’s a unique element, and not one of the many (this sounds obvious, but many people fail to observe this distinction when assigning IDs and classes). Note also, in the image’s `SRC`, I’m appending a random string. This is done to force the browser not to cache the image once we’ve cropped it (since the `SRC` doesn’t change).

Open *js.js* and let’s add the obligatory document ready handler (DRH), required any time you’re using freestanding jQuery (i.e. not inside a custom function) to reference or manipulate the DOM. Put the following JavaScript inside this DRH:

<pre><code class="language-javascript">$(function() {
	// all our JS code will go here
});</code></pre>

We’re providing the functionality to a user to crop the image, and it of course means allowing him to drag a box area on the image, denoting the part he wishes to keep. Therefore, the first step is to listen for a `mousedown` event on the image, the first of three events involved in a drag action (mouse down, mouse move and then, when the box is drawn, mouse up).

<pre><code class="language-javascript">var dragInProgress = false;

$("#uploaded_image").mousedown(function(evt) {
	dragInProgress = true;
});</code></pre>

And in similar fashion, let’s listen to the final mouseup event.

<pre><code class="language-javascript">$(window).mouseup(function() {
	dragInProgress = false;
});</code></pre>

Note that our `mouseup` event runs on `window`, not the image itself, since it’s possible that the user could release the mouse button anywhere on the page, not necessarily on the image.

Note also that the `mousedown` event handler is prepped to receive the event object. This object holds data about the event, and jQuery always passes it to your event handler, whether or not it’s set up to receive it. That object will be crucial later on in ascertaining where the mouse was when the event fired. The `mouseup` event doesn’t need this, because all we care about if is that the drag action is over and it doesn’t really matter where the mouse is.

We’re tracking whether or not the mouse button is currently depressed in a variable, &lt;cpde?dragInProgress. Why? Because, in a drag action, the middle event of the three (see above) only applies if the first happened. That is, in a drag action, you move the mouse *whilst* the mouse is down. If it’s not, our `mousemove` event handler should exit. And here it is:

<pre><code class="language-javascript">$("#uploaded_image").mousemove(function(evt) {
	if (!dragInProgress) return;
});</code></pre>

So now our three event handlers are set up. As you can see, the `mousemove` event handler exits if it discovers that the mouse button is not currently down, as we decided above it should be.

Now let’s extend these event handlers.

This is a good time to explain how our JavaScript will be simulating the drag action being done by the user. The trick is to create a `DIV` on `mousedown`, and position it at the mouse cursor. Then, as the mouse moves, i.e. the user is drawing his box, that element should resize consistently to mimic that.

Let’s add, position and style our `DIV`. Before we add it, though, let’s remove any previous such `DIV`, i.e. from a previous drag attempt. This ensures there’s only ever one drag box, not several. Also, we want to log the mouse coordinates at the time of mouse down, as we’ll need to reference these later when it comes to drawing and resizing our `DIV`. Extend the `mousedown` event handler to become:

<pre><code class="language-javascript">$("#uploaded_image").mousedown(function(evt) {
	dragInProgress = true;
	$("#drag_box").remove();
	$("&lt;div&gt;").appendTo("body").attr("id", "drag_box").css({left: evt.clientX, top: evt.clientY});
	mouseDown_left = evt.clientX;
	mouseDown_top = evt.clientY;
});</code></pre>

Notice that we don’t prefix the three variables there with the `'var'` keyword. That would make them accessible only within the `mousedown` handler, but we need to reference them later in our `mousemove` handler. Ideally, we’d avoid global variables (using a namespace would be better) but for the purpose of keeping the code in this tutorial concise, they’ll do for now.

Notice that we obtain the coordinates of where the event took place &mdash; i.e. where the mouse was when the mouse button was depressed &mdash; by reading the `clientX` and `clientY` properties of the event object, and it’s those we use to position our `DIV`.

Let’s style the `DIV` by adding the following CSS to your stylesheet.

<pre><code class="language-css">#drag_box { position: absolute; border: solid 1px #333; background: #fff; opacity: .5; filter: alpha(opacity=50); z-index: 10; }</code></pre>

Now, if you upload an image and then click it, the DIV will be inserted at your mouse position. You won’t see it yet, as it’s got width and height zero; only when we start dragging should it become visible, but if you use Firebug or Dragonfly to inspect it, you will see it in the DOM.

So far, so good. Our drag box functionality is almost complete. Now we just need to make it respond to the user’s mouse movement. What’s involved here is very much what we did in the `mousedown` event handler when we referenced the mouse coordinates.

The key to this part is working out what properties should be updated, and with what values. We’ll need to change the box’s `left`, `top`, `width` and `height`.

Sounds pretty obvious. However, it’s not as simple as it sounds. Imagine that the box was created at coordinates 40x40 and then the user drags the mouse to coordinates 30x30. By updating the box’s left and top properties to 30 and 30, the position of the top left corner of the box would be correct, but the position of its bottom right corner would not be where the `mousedown` event happened. The bottom corner would be 10 pixels north west of where it should be!

To get around this, we need to compare the `mousedown` coordinates with the current mouse coordinates. That’s why in our `mousedown` handler, we logged the mouse coordinates at the time of mouse down. The box’s new CSS values will be as follows:

*   `left`: the lower of the two `clientX` coordinates
*   `width`: the difference between the two `clientX` coordinates
*   `top`: the lower of the two `clientY` coordinates
*   `height`: the difference between the two `clientY` coordinates

So let’s extend the `mousemove` event handler to become:

<pre><code class="language-javascript">$("#uploaded_image").mousemove(function(evt) {
	if (!dragInProgress) return;
	var newLeft = mouseDown_left &lt; evt.clientX ? mouseDown_left : evt.clientX;
	var newWidth = Math.abs(mouseDown_left - evt.clientX);
	var newTop = mouseDown_top &lt; evt.clientY ? mouseDown_top : evt.clientY;
	var newHeight = Math.abs(mouseDown_top - evt.clientY);
	$('#drag_box').css({left: newLeft, top: newTop, width: newWidth, height: newHeight});
});</code></pre>

Notice also that, to establish the new width and height, we didn’t have to do any comparison. Although we don’t know, for example, which is lower out of the mousedown left and the current mouse left, we can subtract either from the other and counter any negative result by forcing the resultant number to be positive via `Math.abs()`, i.e.

<pre><code class="language-javascript">result = 50 – 20; //30
result = Math.abs(20 – 50); //30 (-30 made positive)</code></pre>

One final, small but important thing. When Firefox and Internet Explorer detect drag attempts on images they assume the user is trying to drag out the image onto their desktop, or into Photoshop, or wherever. This has the potential to interfere with our creation. The solution is to stop the event from doing its default action. The easiest way is to return false. What’s interesting, though, is that Firefox interprets drag attempts as beginning on mouse down, whilst IE interprets them as beginning on mouse move. So we need to append the following, simple line to the ends of both of these functions:

<pre><code class="language-javascript">return false;</code></pre>

Try your application out now. You should have full drag box functionality.

{{% ad-panel-leaderboard %}}

## Saving The Cropped Image

And so to the last part, saving the modified image. The plan here is simple: we need to grab the coordinates and dimensions of the drag box, and pass them to our PHP script which will use them to crop the image and save a new version.

### Grabbing The Drag Box Data

It makes sense to grab the drag box’s coordinates and dimensions in our `mouseup` handler, since it denotes the end of the drag action. We *could* do that with the following:

<pre><code class="language-javascript">var db = $("#drag_box");
var db_data = {left: db.offset().left, top: db.offset().top, width: db.width(), height: db.height()};</code></pre>

There’s a problem, though, and it has to do with the drag box’s coordinates. The coordinates we grab above are relative to the body, not the uploaded image. So to correct this, we need to subtract the position, relative to the body, of the image itself, from them. So let’s add this instead:

<pre><code class="language-javascript">var db = $("#drag_box");
if (db.width() == 0 || db.height() == 0 || db.length == 0) return;
var img_pos = $('#uploaded_image').offset();
var db_data = {
	left: db.offset().left – img_pos.left,
	top: db.offset().top - img_pos.top,
	width: db.width(),
	height: db.height()
};</code></pre>

What’s happening there? We’re first referencing the drag box in a local shortcut variable, `db`, and then store the four pieces of data we need to know about it, its `left`, `top`, `width` and `height`, in an object `db_data`. The object isn’t essential: we could use separate variables, but this approach groups the data together under one roof and might be considered tidier.

Note the condition on the second line, which guards against simple, dragless clicks to the image being interpreted as crop attempts. In these cases, we return, i.e. do nothing.

Note also that we get the left and top coordinates via jQuery’s `offset()` method. This returns the dimensions of an object relative to the document, rather than relative to any parent or ancestor with relative positioning, which is what `position()` or `css('top/right/bottom/left')` would return. However, since we appended our drag box directly to the body, all of these three techniques would work the same in our case. Equally, we get the width and height via the `width()` and `height()` methods, rather than via `css('width/height')`, as the former omits ‘px’ from the returned values. Since our PHP script will be using these coordinates in a mathematical fashion, this is the more suitable option.

For more information on the distinction between all these methods, see my previous article on SmashingMag, <a href="https://www.smashingmagazine.com/2010/08/04/commonly-confused-bits-of-jquery/">Commonly Confused Bits of jQuery</a>.

Let’s now throw out a confirm dialogue box to check that the user wishes to proceed in cropping the image using the drag box they’ve drawn. If so, time to pass the data to our PHP script. Add a bit more to your `mouseup` handler:

<pre><code class="language-javascript">if (confirm("Crop the image using this drag box?")) {
	location.href = "index.php?crop_attempt=true&amp;crop_l="+db_data.left+"&amp;crop_t="+
db_data.top+"&amp;crop_w="+db_data.width+"&amp;crop_h="+db_data.height;
} else {
	db.remove();
}</code></pre>

So if the user clicks ‘OK’ on the dialogue box that pops up, we redirect to the same page we’re on, but passing on the four pieces of data we need to give to our PHP script. We also pass it a flag `crop_attempt`, which our PHP script can detect, so it knows what action we’d like it to do. If the user clicks ‘Cancel’, we remove the drag box (since it’s clearly unsuitable). Onto the PHP...

### PHP: Saving The Modified File

Remember we said that our *image_manipulation.php* had two tasks &mdash; one to first save the uploaded image and another to save the cropped version of the image? It’s time to extend the script to handle the latter request. Append the following to *image_manipulation.php*:

<pre><code class="language-php">/* -----------------
| CROP saved image
----------------- */

if (isset($_GET["crop_attempt"])) {
	//cropping code here
}</code></pre>

So just like before, we condition-off the code area and make sure a flag is present before executing the code. As for the code itself, we need to go back into the land of GD. We need to create two image handles. Into one, we import the uploaded image; the second one will be where we paste the cropped portion of the uploaded image into, so we can essentially think of these two as source and destination. We copy from the source onto the destination canvas via the GD function `imagecopy()`. This needs to know 8 pieces of information:

*   `destination`, the destination image handle
*   `source`, the source image handle
*   `destination X`, the left position to paste TO on the destination image handle
*   `destination Y`, the top position “ “ “ “
*   `source X`, the left position to grab FROM on the source image handle
*   `source Y`, the top position “ “ “ “
*   `source W`, the width (counting from source X) of the portion to be copied over from the source image handle
*   `source H`, the height (counting from source Y) “ “ “ “

**Fortunately, we already have the data necessary to pass to the final 6 arguments** in the form of the JavaScript data we collected and passed back to the page in our `mouseup` event handler a few moments ago.

Let’s create our first handle. As I said, we’ll import the uploaded image into it. That means we need to know its file extension, and that’s why we saved it as a session variable earlier.

<pre><code class="language-php">switch($_SESSION["fileExt"][1]) {
	case "jpg": case "jpeg":
		var source_img = imagecreatefromjpeg($_SESSION["newPath"]);
		break;
	case "gif":
		var source_img = imagecreatefromgif($_SESSION["newPath"]); 
		break;
	case "png":
		var source_img = imagecreatefrompng($_SESSION["newPath"]); 
		break;
}</code></pre>

As you can see, the file type of the image determines which function we use to open it into an image handle. Now let’s extend this switch statement to create the second image handle, the destination canvas. Just as the function for opening an existing image depends on image type, so too does the function used to create a blank image. Hence, let’s extend our switch statement:

<pre><code class="language-php">switch($_SESSION["fileExt"][1]) {
	case "jpg": case "jpeg":
		$source_img = imagecreatefromjpeg($_SESSION["newPath"]);
		$dest_ing = imagecreatetruecolor($_GET["crop_w"], $_GET["crop_h"]);
		break;
	case "gif":
		$source_img = imagecreatefromgif($_SESSION["newPath"]);
		$dest_ing = imagecreate($_GET["crop_w"], $_GET["crop_h"]);
		break;
	case "png":
		$source_img = imagecreatefrompng($_SESSION["newPath"]);
		$dest_ing = imagecreate($_GET["crop_w"], $_GET["crop_h"]);
		break;
}</code></pre>

You’ll notice that the difference between opening a blank image and opening one from an existing or uploaded file is that, for the former, you must specify the dimensions. In our case, that’s the width and height of the drag box, which we passed into the page via the `$_GET['crop_w']` and `$_GET['crop_h']` vars respectively.

So now we have our two canvases, it’s time to do the copying. The following is one function call, but since it takes 8 arguments, I’m breaking it onto several lines to make it readable. Add it after your switch statement:

<pre><code class="language-php">imagecopy(
	$dest_img,
	$source_img,
	0,
	0,
	$_GET["crop_l"],
	$_GET["crop_t"],
	$_GET["crop_w"],
	$_GET["crop_h"]
);</code></pre>

The final part is to save the cropped image. For this tutorial, we’ll overwrite the original file, but you might like to extend this application, so the user has the option of saving the cropped image as a separate file, rather than losing the original.

Saving the image is easy. We just call a particular function based on (yes, you guessed it) the image’s type. We pass in two arguments: the image handle we’re saving, and the file name we want to save it as. So let’s do that:

<pre><code class="language-php">switch($_SESSION["fileExt"][1]) {
	case "jpg": case "jpeg":
		imagejpeg($dest_img, $_SESSION["newPath"]); break;
	case "gif":
		imagegif($dest_img, $_SESSION["newPath"]); break;
	case "png":
		imagepng($dest_img, $_SESSION["newPath"]); break;
}</code></pre>

It’s always good to clean up after ourselves - in PHP terms that means freeing up memory, so let’s destroy our image handlers now that we don’t need them anymore.

<pre><code class="language-php">imagedestroy($dest_img);
imagedestroy($source_img);</code></pre>

Lastly, we want to redirect to the index page. You might wonder why we’d do this, since we’re on it already (and have been the whole time). The trick is that by redirecting, we can lose the arguments we passed in the URL. We don’t want these hanging around because, if the user refreshes the page, he’ll invoke the PHP crop script again (since it will detect the arguments). The arguments have done their job, so now they have to go, so we redirect to the index page without these arguments. Add the following line to force the redirect:

<pre><code class="language-php">header("Location: index.php"); //bye bye arguments</code></pre>

## Final Touches

So that’s it. We now have a fully-working facility to first upload then crop an image, and save it to the server. Don’t forget you can <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a7185d-7761-4418-9e4a-c3fdb1b284c9/manipulation-img-crop.zip">download the source files</a> (*updated*) for your reference.

There’s plenty of ways you could extend this simple application. Explore GD (and perhaps other image libraries for PHP); you can do wonders with images, resizing them, distorting them, changing them to greyscale and much more. Another thing to think about would be security; this tutorial does not aim to cover that here, but if you were working in a user control panel environment, you’d want to make sure the facility was secure and that the user could not edit other user’s files.

With this in mind, you might make the saved file’s path more complex, e.g. if the user named it `pic.jpg`, you might actually name it on the server `34iweshfjdshkj4r_pic.jpg`. You could then hide this image path, e.g. by specifying the `SRC` attribute as '`getPic.php`' instead of referencing the image directly inside an image’s `SRC` attribute. That PHP script would then open and display the saved file (by reading its path in the session variable), and the user would never be aware of its path.

The possibilities are endless, but hopefully this tutorial has given you a starting point.

### Further Reading

*   [Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)
*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)
*   [A Guide To PHP Error Messages For Designers](https://www.smashingmagazine.com/2011/11/a-guide-to-php-error-messages-for-designers/)
*   [Choosing A Responsive Image Solution](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/)

{{< signature "vf, il, mrn" >}}
