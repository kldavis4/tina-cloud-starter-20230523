---
title: So We Wanted To Build A File Uploader... A Case Study
slug: so-we-wanted-to-build-a-file-uploader-a-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab629cca-6085-4f08-9515-9f7c7ec7a9a6/fileuploader.jpg
date: 2013-10-11T18:30:49.000Z
author: konstantin-lebedev
description: >-
  One day I discovered that I needed to design an API that would upload files
  from a client to a server. I work on the Russian Web mail provider at Mail.Ru
  and deal with JavaScript in all its aspects. A basic feature of any Web mail
  service is of course attaching a file to an email.
categories:
  - Coding
  - Forms
  - File Upload
---
One day I discovered that I needed to design an API that would upload files from a client to a server. I work on the Russian Web mail provider at <a href="https://corp.mail.ru/en">Mail.Ru</a> and deal with JavaScript in all its aspects. A basic feature of any Web mail service is of course <strong>attaching a file to an email</strong>.

<a href="/2013/10/so-we-wanted-to-build-a-file-uploader-a-case-study/"><img title="So We Wanted To Build A File Uploader... (A Case Study)" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a201e4ee-0267-4016-9824-b1cf2be486c8/frontpage-image-opt.png" alt="So We Wanted To Build A File Uploader... (A Case Study)" width="500" height="228" /></a>

<em>Mail.ru</em> is no exception: We used to have a Flash uploader, which was rather good, but still had some problems. HTML markup, graphics, business logic and even localization were all built into it, and it made the uploader pretty bloated. Furthermore, only a Flash developer could make any changes to it. We realized that we needed to build something new and different. This article covers all of our steps in creating what we consider to be a better tool for the job.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">How Mail.Ru Reduced Email Storage From 50 To 32 PB</span>](https://www.smashingmagazine.com/2017/01/reducing-email-storage-mailru/)
*   [Product Design Unification Case Study: Mobile Web Framework](https://www.smashingmagazine.com/2015/02/product-design-unification-case-study-mobile-web-framework/)
*   [How To Improve Your Email Workflow With Modular Design](https://www.smashingmagazine.com/2014/08/improve-your-email-workflow-with-modular-design/)
*   [Making Responsive HTML Email Coding Easy With MJML](https://www.smashingmagazine.com/2017/01/making-responsive-html-email-coding-easy-with-mjml/)

Anyone who has ever written a Flash uploader knows what problems it always brings:

{{% feature-panel %}}

*   Cookies for authentication are [difficult to manage](https://forums.adobe.com/thread/221811) because depending on browser and operating system they have erratic behaviour in Flash (i.e. cookies are not shared between HTTP requests and FileReference upload/download). Officially Flash supports cookies only in IE and they will not be shared among other browsers, or they will be retrieved from IE;
*   There are assumptions that with Flash, cookies are read from Internet Explorer although it's not officially confirmed;
*   [Proxy settings are quite inconvenient to update](https://www.ehow.com/how_7571780_update-proxy-flash-player.html); with Flash, they are always retrieved from IE, independent of the browser used;
*   Errors #[2038](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#2038) and #[2048](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#2048), elusive errors that appear in some combinations of network settings, browser and Flash player version;
*   AdBlock and the like (no comment).

So, we decided that <strong>it was the right time for a change</strong>. Here’s a list of features that we wanted to have with a new approach to this problem:

*   Select multiple files;
*   Get file information (name, type and mini-type);
*   Preview images before uploading;
*   Resize, crop and rotate images client-side;
*   Upload results to the server, plus [CORS](https://enable-cors.org/);
*   Make it independent of external libraries;
*   Make it extensible.

Over the last four years, we’ve all read heated debates about various features and options of HTML5, including the <a href="https://caniuse.com/#search=fileapi">File API</a>. Many publications touch on this API, and we have a few functioning examples of it. One would think, “Here’s a tool that solves the problem.” But is it as easy as it looks?

Well, let’s look at the <a href="https://top.mail.ru/browsers?id=250&amp;ago=1#sids=chrome,firefox,opera,msie,safari,others&amp;percent=0">browser statistics for Mail.Ru</a>. We have selected only browser versions that support the File API, although in some cases these browsers do not provide full support for the API.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ed7461b-f525-4ebb-9533-2cefde26927f/no-full-support-api-opt.png"><img loading="lazy" decoding="async" class="129292" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ed7461b-f525-4ebb-9533-2cefde26927f/no-full-support-api-opt.png" alt="The browsers used support File API" width="300" height="219" /></a>

The diagram shows that a bit more than a whopping 87% of browsers indeed support the File API:

*   Chrome 10+
*   Firefox 3.6+
*   Opera 11.10+
*   Safari 5.4+
*   IE 10+

Also, we shouldn't forget about mobile browsers, which are becoming more popular by the day. Take iOS 6+, for example, which already supports the File API. However, 87% is not 100% and in our case it wasn't feasible to entirely abandon Flash at this point.

So, our task evolved to <strong>building a tool that combines two techniques (File API and Flash)</strong> and that lets the developer kind of... <em>ignore</em> the way files are actually uploaded. During the development process we decided to combine all preliminary development into a separate library (a unified API) that would work independent of the environment and could be used wherever you like, not only in our service.

So let’s go into detail on a few specifics of the development process and see what we've built, how we built it and what we've learned along the way.</p>

## Retrieve File List

Basics first. Here is how files are received in HTML5. Very simple.

<pre><code class="language-markup">&lt;input id="file" type="file" multiple="multiple" /&gt;
&lt;script&gt;
      var input = document.getElementById("file");
      input.addEventListener("change", function (){
           var files = input.files;
      }, false);
&lt;/script&gt;
</code></pre>

But what do you do if you have only Flash support and no File API? The basic idea that we had for users with Flash support was to make <em>all</em> interactions go through Flash. You couldn’t simply call up a file-selection dialog. Due to the security policy, the dialog would open only after the Flash object has been clicked.

This is why the Flash object would be positioned above your target input. Then, you would attach a <code>mouseover</code> event handler to the document, and put the Flash object into the input’s parent element when the user hovers over it.

The user would click the Flash object, open the file-selection dialog and select a file. Data would be transferred from Flash to JavaScript using <code>ExternalInterface</code>. The JavaScript would bind the data received with the input element and emulate the <code>change</code> event.

<pre><code class="language-javascript">
[[Flash]] --&gt; jsFunc([{
     id: "346515436346", // unique identifier
     name: "hello-world.png", // file name
     type: "image/png", // mime-type
     size: 43325 // file size
   }, {
     // etc.
 }])
</code></pre>

All further interactions between JavaScript and Flash are performed through the only available method in Flash. The first argument is a command name. The second parameter is an object with two mandatory fields: the file <code>id</code> and the <code>callback</code> function. The <code>callback</code> is called from Flash once the command is executed.

<pre><code class="language-javascript">
flash.cmd("imageTransform", {
    id: "346515436346",    // file identification
    matrix: { },    // transformation matrix
    callback: "__UNIQ_NAME__"
});
</code></pre>

The combination of the two methods results in the API, which is very similar to native JavaScript. The only difference is in the way files are received. Now we use the API method because the input has the <code>files</code> property only when the browser supports HTML5 and the File API. In the case of Flash, the list is taken from the data associated with it.

<pre><code class="language-markup">&lt;span class="js-fileapi-wrapper" style="position: relative"&gt;
    &lt;input id="file" type="file" multiple /&gt;
&lt;/span&gt;
&lt;script&gt;
    var input = document.getElementById("file");
    FileAPI.event.on(input, "change", function (){
        var files = FileAPI.getFiles(input);
    });
&lt;/script&gt;
</code></pre>

## Filter

Usually, file uploading comes with a set of restrictions. The most common restrictions are on file size, image type and dimensions (width and height). If you look around solutions for this issue, you'll notice that validation is usually done on the server, and the user would receive an error message if the file doesn’t match any restrictions. <strong>I tried to solve this problem in another way, by validating files on the client side</strong> — before the file has started uploading.

What’s the catch? The catch is that when we initially get the list of files, we have only the bare minimum of information about the files: name, size and type. To get more detailed information, we need to actually <em>read</em> the files. To do that, we can use <a href="https://developer.mozilla.org/en-US/docs/DOM/FileReader">FileReader</a>.

So if we play around with FileReader, we'll probably come up with the following filtering technique:

<pre><code class="language-javascript">
FileAPI.filterFiles(files, function (file, info){
    if( /^image/.test(file.type) ){
        return info.width &gt; 320 &amp;&amp; info.height &gt; 240;
    } else if( file.size ){
        return file.size &lt; 10 * FileAPI.MB;
     } else {
         // Unfortunately, there is no support for File API or Flash. We have to validate on the server.
         // This case is rather rare, but we must consider it as part of the project.
         return true;
     }
 }, function (files, ignore){
     if( files.length &gt; 0 ){
        // ...
    }
});
</code></pre>

You can get the file’s dimensions “out of the box,” as well as a way to collect all of the data you’ll need:

<pre><code class="language-javascript">
FileAPI.addInfoReader(/^audio/, function (file, callback){
    // collect required information
    // and call it back
    callback(
        false,    // or error message
        { artist: "...", album: "...", title: "...", ... }
    );
});
</code></pre>

## Process Images

In developing the API, we also wanted a convenient and powerful tool that would allow us to work with images — to create previews, crop, rotate and resize, for example — and whose functionality would be supported in both HTML5 and Flash.</p>

### Flash

First, we needed to understand how to do this via Flash — that is, what to send to JavaScript to build the image. As we of course know, this is usually done using the data URI. Flash reads the file as Base64 and transfers it to JavaScript. So we add <code>data:image/png;base64</code> to it, and use this string as the <code>src</code>.

A happy ending? Unfortunately, IE 6 and 7 do not support the data URI, and IE 8+, which supports the data URI, cannot process more than 32 KB. In this case, JavaScript would create a second Flash object and transfer the Base64-encoded content into it. This Flash object would restore the image.</p>

### HTML5

In the case of HTML5, we would get the original image first, and then perform all required transformations using the canvas. Getting the original image can be done in one of two ways. The first is to read the file as a dataURI using <code>FileReader</code>. The second is to use <a href="https://developer.mozilla.org/en-US/docs/DOM/window.URL.createObjectURL">URL.createObjectURL</a> to create a link to the file, which is bound to the current tab. Of course, the second option is good and is enough to generate a preview, but not all browsers support it. Opera 12, for example, does not support the accompanying <code>URL.revokeObjectURL</code>, which informs the browser that there is no need to keep a link to the file anymore.

When we combine all of these methods, we get a class of <code>FileAPI.Image</code>:

*   `crop(x, y, width, height)`
*   `resize(width,[height])`
*   `rotate(deg)`
*   `preview(width, height)` — crop and resize
*   `get(callback)` — get final image

All of these techniques fill the transformation matrix, which is applied only when the <code>get()</code> method is called. Transformations are performed using the HTML5 <code>canvas</code> or in Flash (when the file is uploaded through the Flash interface).

Here is our description of the matrix:

<pre><code class="language-javascript">
{   // parameters fragment of original
   sx: Number,
   sy: Number,
   sw: Number,
   sh: Number,

   // destination size
   dw: Number,
   dh: Number,
   deg: Number
}
</code></pre>

And here is a short example:

<pre><code class="language-javascript">
FileAPI.Image(imageFle) // returns FileAPI.Image instance
   .crop(300, 300)      // crop the image width and height
   .resize(100, 100)    // resize to 100x100px
   .get(function (err, img){
      if( !err ){
        // Append the result in the DOM-node (&lt;div id="images"&gt;).
         images.appendChild(img);
      }
   });
</code></pre>

### Resize

Digital cameras emerged long ago and are still very popular. Some cost about $20 to $30 and can take photos with a resolution of 10 MP and up. We tried to downsize photos taken with such cameras, and this is what we ended up with:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5da773-5f21-4eaa-a0f5-40101ae1ac19/downsize-image-opt.png"><img loading="lazy" decoding="async" class="129293" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5da773-5f21-4eaa-a0f5-40101ae1ac19/downsize-image-opt.png" alt="Downsizing the image one time." width="500" height="228" /></a>

As you can see, the quality is rather poor. However, if we first resize it in half and then do it again several times until we get the desired dimensions, then the quality is much better. This method is actually quite old, and in fact a consequence of the <a href="https://en.wikipedia.org/wiki/Nearest-neighbor_interpolation">"nearest neighbor" interpolation</a>; when compressing images at once, we are losing the quality of the image really "quickly".

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6711c71d-3c86-469c-a946-cd8d0cb621b7/resize-image-in-half-opt.png"><img loading="lazy" decoding="async" class="129294" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6711c71d-3c86-469c-a946-cd8d0cb621b7/resize-image-in-half-opt.png" alt="Resize image in half several times." width="500" height="166" /></a>

The <strong>difference is evident:</strong>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d931b8-211c-40c0-8ba2-25e128a4333f/quality-difference-images-opt.png"><img loading="lazy" decoding="async" class="129295" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d931b8-211c-40c0-8ba2-25e128a4333f/quality-difference-images-opt.png" alt="Quality difference of images." width="429" height="172" /></a>

Apply a slight sharpening effect, and the image will be ideal.

We also tried other variations, such as bicubic interpolation and the Lanczos algorithm. The result was a bit better, but the process took more time: 1.5 seconds versus 200 to 300 milliseconds. This method also yielded the same results in canvas and Flash.</p>

## Uploading Files

Now let’s sum up our various options for uploading a file to the server.</p>

### iframe

Yes, we still use this many years later:

<pre><code class="language-markup">&lt;form
   target="__UNIQ__"
   action="/upload"
   method="post"
   enctype="multipart/form-data"&gt;&lt;!-- This bit is often forgotten --&gt;
        &lt;iframe name="__UNIQ__" height="240" width="320"&gt;&lt;/iframe&gt;
        &lt;input type="file" name="files" /&gt;
        &lt;input type="hidden" name="foo" value="bar" /&gt;
&lt;/form&gt;
</code></pre>

At first, we create а <code>form</code> element with a nested <code>iframe</code> inside. (The <code>form</code>’s target attribute and the name of the <code>iframe</code> should be the same.) After that, we move the <code>input[type="file"]</code> into it because if you put a clone there, it will turn up empty.

To illustrate this issue, imagine that you load a file via <code>iframe</code>. We could use something like this:

<pre><code class="language-javascript">
    var inp = document.getElementById('photo');
    var form = getIFrameFormTransport();
    form.appendChild(inp.cloneNode(true)); // send a "clone"
    form.submit();
</code></pre>

However, such input <a href="https://webstorehouse.blogspot.ru/2009/02/clone-node-issue-in-ie.html">would be "empty" in IE</a>, i.e. it wouldn't contain the selected file, which is why we need to "send" the original file and replace it with a clone.

That is why we subscribe to events via API methods, to save them during cloning. Then, we call <code>form.submit()</code>, and put the contents of the form through the <code>iframe</code>. We’ll get the results using JSONP.

<pre><code class="language-javascript">
    var inp = document.getElementById('photo');
    var cloneInp = inp.cloneNode(true);
    var form = getIFrameFormTransport();

    // Insert the "clone" after the "original"
    inp.parentNode.insertBefore(cloneInp, inp);

    form.appendChild(inp); // Send the "original
    form.submit();
</code></pre>

Yes, erratic indeed.</p>

### Flash

In principle, everything is quite simple: JavaScript calls the method from the Flash object and passes the ID of the file to be uploaded. Flash, in turn, duplicates all states and events in JavaScript.</p>

### XMLHttpRequest and FormData

Now we can send binary data, not just text data. This is easy:

<pre><code class="language-javascript">
// collect data to be sent
var form = new FormData
form.append("foo", "bar"); // the first parameter is the name of POST-parameter,
form.append("attach", file); // the second parameter is the string, file or Blob

// send to server
var  xhr = new XMLHttpRequest;
xhr.open("POST", "/upload", true);
xhr.send(form);
</code></pre>

What if, for example, we want to send not a file, but <code>canvas</code> data? There are two options. The first, which is easiest and correct, is to convert <code>canvas</code> to <a href="https://developer.mozilla.org/en-US/docs/Web/API/Blob"><code>Blob</code></a>:

<pre><code class="language-javascript">
canvasToBlob(canvas, function (blob){
    var form = new FormData
    form.append("foo", "bar");
    form.append("attach", blob, "filename.png"); //not all support the third parameter

    // ...
});
</code></pre>

As you can see, this trick is not universal. In case canvas doesn’t have <code>Canvas.toBlob()</code> (or it cannot be implemented), we will choose another option. This option is also good for browsers that do not support <code>FormData</code>. The point is to create the multipart request manually and then send it to the server. The code for the canvas would look like this:

<pre><code class="language-javascript">
var dataURL = canvas.toDataURL("image/png"); // or result from FileReader
var base64 = dataURL.replace(/^data:[^,]+,/, ""); // cut the beginning
var binaryString = window.atob(base64); // decode Base64

// now get together multipart, nothing complicated
var uniq = '1234567890';
var data = [
      '--_'+ uniq
    , 'Content-Disposition: form-data; name="my-file"; filename="hello-world.png"'
    , 'Content-Type: image/png'
    , ’
    , binaryString
    , '--_'+ uniq +'--'
].join('rn');

var xhr = new XMLHttpRequest;
xhr.open('POST', '/upload', true);
xhr.setRequestHeader('Content-Type', 'multipart/form-data; boundary=_'+uniq);

if( xhr.sendAsBinary ){
  xhr.sendAsBinary(data);
} else {
  var bytes = Array.prototype.map.call(data, function(c){
     return c.charCodeAt(0) &amp; 0xff;
  });
  xhr.send(new Uint8Array(bytes).buffer);
}
</code></pre>

Finally, our efforts result in the following method:

<pre><code class="language-javascript">
var xhr = FileAPI.upload({
   url:  '/upload',
   data:  { foo: 'bar' },
   headers:  { 'Session-Id': '...' },
   files:   { images: imageFiles, others: otherFiles },
   imageTransform:  { maxWidth: 1024, maxHeight: 768 },
   upload: function (xhr){},
   progress: function (event, file){},
   complete: function (err, xhr, file){},
   fileupload: function (file, xhr){},
   fileprogress: function (event, file){},
   filecomplete: function (err, xhr, file){}
});
</code></pre>

This has a lot of parameters, but the most important one is <code>imageTransform</code>. It transforms images on the client, and it operates via both Flash and HTML5.

And that’s not even half of the story. We can have multiple <code>imageTransforms</code>:

<pre><code class="language-javascript">
{
     huge:   { maxWidth: 800, maxHeight: 600, rotate: 90 },
     medium: { width: 320, height: 240, preview: true },
     small:  { width: 100, height: 120, preview: true }
}
</code></pre>

This means that three copies (besides the original) will be sent to the server. What for? If you can <strong>transfer the load from the server to the client</strong>, it's a good idea to do it. The server should probably only minimally validate input files. First of all, you are not only removing the load, but also avoid logic on the server, completely moving it to the client.

Second, if the file doesn't have to get uploaded to the server, we save bandwidth. In addition, there are often problems when it isn't possible to make further processing on the server, such as integration with third-party services (Amazon S3, for example). In our experience, it's OK to move the additional logic that previously was managed server-side to the client.

The upload function also calls back an <code>XMLHttpRequest</code>-like object; that is, it assumes some properties and methods of <code>XMLHttpRequest</code>, such as:

*   `status` HTTP status code
*   `statusText` HTTP status text
*   `responseText` server’s reply
*   `getResponseHeader(name)` get header of the server’s reply
*   `getAllResponseHeaders()` get all headers
*   `abort()` abort upload

Although HTML5 allows you to upload several files in one request, standard Flash allows only file-by-file uploading. Moreover, in our opinion, uploading files in a batch proved not to be a good idea. For one, Flash doesn't support this, and we wanted to have an identical behavior for both Flash and HTML5. Second, the user might simply run out of memory and the browser will fail.

<code>XMLHttpRequest</code>, which has called back the upload, is a proxy <code>XMLHttpRequest</code>, in fact. Its methods and properties reflect states in the file currently being uploaded.</p>

## Final Word

I’ll end with a small example of how we let users upload files using drag'n'drop:

<pre><code class="language-markup">&lt;div id="el" class="dropzone"&gt;&lt;/div&gt;
&lt;script&gt;
    if( FileAPI.support.dnd ){
        // element where you can drop the files
        var el = document.getElementById("el");

        // subscribe to events associated with Drag'n'Drop
        FileAPI.event.dnd(el, function (over){
            // method will be activated when you enter/leave the element
            if( over ){
                el.classList.add("dropzone_hover");
            } else {
                el.classList.remove("dropzone_hover");
            }
        }, function (dropFiles){
            // the user has dropped the files
            FileAPI.upload({
                url: "/upload",
                files: { attaches: dropFiles },
                complete: function (err, xhr){
                    if( !err ){
                        // files are uploaded
                    }
                }
            });
        });
    }
&lt;/script&gt;

</code></pre>

It took us quite some time to develop the library. We worked on it for about 5 months since it was a little side thing that we had to finish aside from the regular work. The main headache was caused by the little details that different browsers had. Chrome, Firefox and IE10+ were just fine, but Safari and Opera had very different behaviors from version to version, including inconsistencies on Win/Mac platforms. Still, <strong>the main problem was to actually combine all three technologies</strong> — iframe, Flash, HTML5 — to create a bulletproof file uploader.

The library is <a href="https://github.com/mailru/FileAPI/">available on GitHub</a> and we've published a <a href="https://mailru.github.io/FileAPI/">documentation</a> as well. Bug reports and pull requests are more than welcome!

### Useful Links

*   [FileAPI](https://github.com/mailru/FileAPI) (and [demo](https://mailru.github.io/FileAPI/examples/demo.html)), Mail.ru, GitHub
*   [Mail.ru](https://github.com/mailru/), GitHub Find Tarantool, fest and much else.
*   “[HTML5 Form Features](https://caniuse.com/#feat=forms),” Can I Use…? See the support for `input[type="file" multiple]`.
*   “[File API](https://caniuse.com/#feat=fileapi),” Can I Use…?
*   “[FileReader](https://developer.mozilla.org/en-US/docs/DOM/FileReader),” Mozilla Developer Network
*   “[URL.createObjectURL](https://developer.mozilla.org/en-US/docs/DOM/window.URL.createObjectURL)” and “[URL.revokeObjectURL](https://developer.mozilla.org/en-US/docs/DOM/window.URL.revokeObjectURL),” Mozilla Developer Network
*   “[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/DOM/XMLHttpRequest),” Mozilla Developer Network
*   “[FormData](https://developer.mozilla.org/en-US/docs/DOM/XMLHttpRequest/FormData),” Mozilla Developer Network

This article has been reviewed and edited by <a href="https://twitter.com/AndrewSumin">Andrew Sumin</a>, a front-end engineer working on <a href="https://corp.mail.ru/en">Mail.ru</a> front-end team.

<em>(al ea il)</em>

