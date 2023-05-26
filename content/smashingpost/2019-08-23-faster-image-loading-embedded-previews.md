---
title: 'Faster Image Loading With Embedded Image Previews'
slug: faster-image-loading-embedded-previews
author: christoph-erdmann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eece72f-e422-44a7-8e90-0ac14a46d2a2/faster-image-loading-embedded-previews.png
date: 2019-08-23T13:30:59+02:00
summary: >-
  The Embedded Image Preview (EIP) technique introduced in this article allows us to load preview images during lazy loading using progressive JPEGs, Ajax and HTTP range requests without having to transfer additional data.
description: >-
  The Embedded Image Preview (EIP) technique introduced in this article allows us to load preview images during lazy loading using progressive JPEGs, Ajax and HTTP range requests without having to transfer additional data.
categories:
  - Performance
  - Optimization
  - Media
---
<p><a href="https://www.guypo.com/introducing-lqip-low-quality-image-placeholders">Low Quality Image Preview (LQIP)</a> and the <a href="https://github.com/axe312ger/sqip">SVG-based variant SQIP</a> are the two predominant techniques for lazy image loading. What both have in common is that you first generate a low-quality preview image. This will be displayed blurred and later replaced by the original image. What if you could present a preview image to the website visitor without having to load additional data?</p>

<p>JPEG files, for which lazy loading is mostly used, have the possibility, according to the specification, to store the data contained in them in such a way that first the coarse and then the detailed image contents are displayed. Instead of having the image built up from top to bottom during loading (baseline mode), a blurred image can be displayed very quickly, which gradually becomes sharper and sharper (progressive mode).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c90dd38-e073-462e-b57e-f29029358bc9/structure-baseline.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c90dd38-e073-462e-b57e-f29029358bc9/structure-baseline.png" sizes="100vw" caption="Baseline mode (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c90dd38-e073-462e-b57e-f29029358bc9/structure-baseline.png'>Large preview</a>)" alt="Representation of the temporal structure of a JPEG in baseline mode" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93bc09a2-bf9b-445e-aa18-9f953a606e1f/structure-progressive.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93bc09a2-bf9b-445e-aa18-9f953a606e1f/structure-progressive.png" sizes="100vw" caption="Progressive mode (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93bc09a2-bf9b-445e-aa18-9f953a606e1f/structure-progressive.png'>Large preview</a>)" alt="Representation of the temporal structure of a JPEG in progressive mode" >}}

<p>In addition to the better user experience provided by the appearance that is displayed more quickly, progressive JPEGs are usually also smaller than their baseline-encoded counterparts. For files larger than 10 kB, there is a <a href="https://yuiblog.com/blog/2008/12/05/imageopt-4/">94 percent probability of a smaller image when using progressive mode</a> according to Stoyan Stefanov of the Yahoo development team.</p>

<p>If your website consists of many JPEGs, you will notice that even progressive JPEGs load one after the other. This is because modern browsers only allow six simultaneous connections to a domain. Progressive JPEGs alone are therefore not the solution to give the user the fastest possible impression of the page. In the worst case, the browser will load an image completely before it starts loading the next one.</p>

<p>The idea presented here is now to load only so many bytes of a progressive JPEG from the server that you can quickly get an impression of the image content. Later, at a time defined by us (e.g. when all preview images in the current viewport have been loaded), the rest of the image should be loaded without requesting the part already requested for the preview again.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6f3a6c6-c7da-4050-a620-7be6ce5592ec/progressive-jpeg-with-two-requests.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6f3a6c6-c7da-4050-a620-7be6ce5592ec/progressive-jpeg-with-two-requests.png" sizes="100vw" caption="Loading a progressive JPEG with two requests (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6f3a6c6-c7da-4050-a620-7be6ce5592ec/progressive-jpeg-with-two-requests.png'>Large preview</a>)" alt="Shows the way the EIP (Embedded image preview) technique loads the image data in two requests." >}}

<p>Unfortunately, you can’t tell an <code>img</code> tag in an attribute how much of the image should be loaded at what time. With Ajax, however, this is possible, provided that the server delivering the image supports <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests">HTTP Range Requests</a>.</p>

<p>Using HTTP range requests, a client can inform the server in an HTTP request header which bytes of the requested file are to be contained in the HTTP response. This feature, supported by each of the larger servers (Apache, IIS, nginx), is mainly used for video playback. If a user jumps to the end of a video, it would not be very efficient to load the complete video before the user can finally see the desired part. Therefore, only the video data around the time requested by the user is requested by the server, so that the user can watch the video as fast as possible.</p>

<p>We now face the following three challenges:</p>

<ol>
<li><a href="#creating-progressive-jpeg">Creating The Progressive JPEG</a></li>
<li><a href="#determine-byte-offset">Determine Byte Offset Up To Which The First HTTP Range Request Must Load The Preview Image</a></li>
<li><a href="#creating-frontend-javascript-code">Creating the Frontend JavaScript Code</a></li>
</ol>

{{% feature-panel %}}

## 1. Creating The Progressive JPEG

<p>A progressive JPEG consists of several so-called scan segments, each of which contains a part of the final image. The first scan shows the image only very roughly, while the ones that follow later in the file add more and more detailed information to the already loaded data and finally form the final appearance.</p>

<p>How exactly the individual scans look is determined by the program that generates the JPEGs. In command-line programs like <em>cjpeg</em> from the <a href="https://github.com/mozilla/mozjpeg">mozjpeg project</a>, you can even define which data these scans contain. However, this requires more in-depth knowledge, which would go beyond the scope of this article. For this, I would like to refer to my article "<a href="https://compress-or-die.com/Understanding-JPG">Finally Understanding JPG</a>", which teaches the basics of JPEG compression. The exact parameters that have to be passed to the program in a scan script are explained in the <a href="https://github.com/mozilla/mozjpeg/blob/master/wizard.txt">wizard.txt</a> of the mozjpeg project. In my opinion, the parameters of the scan script (seven scans) used by mozjpeg by default are a good compromise between fast progressive structure and file size and can, therefore, be adopted.</p>

<p>To transform our initial JPEG into a progressive JPEG, we use <code>jpegtran</code> from the mozjpeg project. This is a tool to make lossless changes to an existing JPEG. Pre-compiled builds for Windows and Linux are available here: <a href="https://mozjpeg.codelove.de/binaries.html">https://mozjpeg.codelove.de/binaries.html</a>. If you prefer to play it safe for security reasons, it’s better to build them yourself.</p>

<p>From the command line we now create our progressive JPEG:</p>

<pre><code class="language-bash">$ jpegtran input.jpg > progressive.jpg</code></pre>

<p>The fact that we want to build a progressive JPEG is assumed by jpegtran and does not need to be explicitly specified. The image data will not be changed in any way. Only the arrangement of the image data within the file is changed.</p>

<p>Metadata irrelevant to the appearance of the image (such as Exif, IPTC or XMP data), should ideally be removed from the JPEG since the corresponding segments can only be read by metadata decoders if they precede the image content. Since we cannot move them behind the image data in the file for this reason, they would already be delivered with the preview image and enlarge the first request accordingly. With the command-line program <a href="https://www.sno.phy.queensu.ca/~phil/exiftool/"><code>exiftool</code></a> you can easily remove these metadata:</p>

<pre><code class="language-bash">$ exiftool -all= progressive.jpg
</code></pre>

<p>If you don’t want to use a command-line tool, you can also use the online compression service <a href="https://compress-or-die.com/jpg">compress-or-die.com</a> to generate a progressive JPEG without metadata.</p>

## 2. Determine Byte Offset Up To Which The First HTTP Range Request Must Load The Preview Image

<p>A JPEG file is divided into different segments, each containing different components (image data, metadata such as IPTC, Exif and XMP, embedded color profiles, quantization tables, etc.). Each of these segments begins with a marker introduced by a hexadecimal <code>FF</code> byte. This is followed by a byte indicating the type of segment. For example, <code>D8</code> completes the marker to the SOI marker <code>FF D8</code> (Start Of Image), with which each JPEG file begins.</p>

<p>Each start of a scan is marked by the SOS marker (Start Of Scan, hexadecimal <code>FF DA</code>). Since the data behind the SOS marker is entropy coded (JPEGs use the <a href="https://en.wikipedia.org/wiki/Huffman_coding">Huffman coding</a>), there is another segment with the Huffman tables (DHT, hexadecimal <code>FF C4</code>) required for decoding before the SOS segment. The area of interest for us within a progressive JPEG file, therefore, consists of alternating Huffman tables/scan data segments. Thus, if we want to display the first very rough scan of an image, we have to request all bytes up to the second occurrence of a DHT segment (hexadecimal <code>FF C4</code>) from the server.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70e9e9a-6d5e-425d-b16f-6ff97fe4e6a3/jpeg-sos.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70e9e9a-6d5e-425d-b16f-6ff97fe4e6a3/jpeg-sos.png" sizes="100vw" caption="Structure of a JPEG file (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70e9e9a-6d5e-425d-b16f-6ff97fe4e6a3/jpeg-sos.png'>Large preview</a>)" alt="Shows the SOS markers in a JPEG file" >}}

<p>In PHP, we can use the following code to read the number of bytes required for all scans into an array:</p>

<pre><code class="language-javascript">&lt;?php
$img = "progressive.jpg";
$jpgdata = file_get_contents($img);
$positions = [];
$offset = 0;
while ($pos = strpos($jpgdata, "\xFF\xC4", $offset)) {
    $positions[] = $pos+2;
    $offset = $pos+2;
}</code></pre>

<p>We have to add the value of two to the found position because the browser only renders the last row of the preview image when it encounters a new marker (which consists of two bytes as just mentioned).</p>

<p>Since we are interested in the first preview image in this example, we find the correct position in <code>$positions[1]</code> up to which we have to request the file via HTTP Range Request. To request an image with a better resolution, we could use a later position in the array, e.g. <code>$positions[3]</code>.</p>

{{% ad-panel-leaderboard %}}

## 3. Creating The Frontend JavaScript Code

<p>First of all, we define an <code>img</code> tag, to which we give the just evaluated byte position:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;img data-src="progressive.jpg" data-bytes="&lt;?= $positions[1] ?&gt;"&gt;</code></pre>
</div>

As is often the case with lazy load libraries, we do not define the <code>src</code> attribute directly so that the browser does not immediately start requesting the image from the server when parsing the HTML code. 


With the following JavaScript code we now load the preview image:

<div class="break-out">

<pre><code class="language-javascript">var $img = document.querySelector("img[data-src]");
var URL = window.URL || window.webkitURL;

var xhr = new XMLHttpRequest();
xhr.onload = function(){
    if (this.status === 206){
        $img.src_part = this.response;
        $img.src = URL.createObjectURL(this.response);
    }
}

xhr.open('GET', $img.getAttribute('data-src'));
xhr.setRequestHeader("Range", "bytes=0-" + $img.getAttribute('data-bytes'));
xhr.responseType = 'blob';
xhr.send();</code></pre>
</div>

<p>This code creates an Ajax request that tells the server in an HTTP range header to return the file from the beginning to the position specified in <code>data-bytes</code>... and no more. If the server understands HTTP Range Requests, it returns the binary image data in an HTTP-206 response (HTTP 206 = Partial Content) in the form of a blob, from which we can generate a browser-internal URL using <code>createObjectURL</code>. We use this URL as <code>src</code> for our <code>img</code> tag. Thus we have loaded our preview image.</p>

<p>We store the blob additionally at the DOM object in the property <code>src_part</code>, because we will need this data immediately.</p>

<p>In the network tab of the developer console you can check that we have not loaded the complete image, but only a small part. In addition, the loading of the blob URL should be displayed with a size of 0 bytes.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc1f5b2e-6447-48fe-a6ef-04df8dce290b/network-console.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc1f5b2e-6447-48fe-a6ef-04df8dce290b/network-console.png" sizes="100vw" caption="Network console when loading the preview image (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc1f5b2e-6447-48fe-a6ef-04df8dce290b/network-console.png'>Large preview</a>)" alt="Shows the network console and the sizes of the HTTP requests" >}}

<p>Since we already load the JPEG header of the original file, the preview image has the correct size. Thus, depending on the application, we can omit the height and width of the <code>img</code> tag.</p>

### Alternative: Loading the preview image inline

<p>For performance reasons, it is also possible to transfer the data of the preview image as data URI directly in the HTML source code. This saves us the overhead of transferring the HTTP headers, but the base64 encoding makes the image data one third larger. This is relativized if you deliver the HTML code with a content encoding like <em>gzip</em> or <em>brotli</em>, but you should still use data URIs for small preview images.</p>

<p>Much more important is the fact that the preview images are available immediately and there is no noticeable delay for the user when building the page.</p>

<p>First of all, we have to create the data URI, which we then use in the <code>img</code> tag as <code>src</code>. For this, we create the data URI via PHP, whereby this code is based on the code just created, which determines the byte offsets of the SOS markers:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php
…

$fp = fopen($img, 'r');
$data_uri = 'data:image/jpeg;base64,'. base64_encode(fread($fp, $positions[1]));
fclose($fp);</code></pre>
</div>

<p>The created data URI is now directly inserted into the `img` tag as <code>src</code>:</p>

<pre><code class="language-javascript">&lt;img src="&lt;?= $data_uri ?&gt;" data-src="progressive.jpg" alt=""&gt;</code></pre>

<p>Of course, the JavaScript code must also be adapted:</p>

<pre><code class="language-javascript">&lt;script&gt;
var $img = document.querySelector("img[data-src]");

var binary = atob($img.src.slice(23));
var n = binary.length;
var view = new Uint8Array(n);
while(n--) { view[n] = binary.charCodeAt(n); }

$img.src_part = new Blob([view], { type: 'image/jpeg' });
$img.setAttribute('data-bytes', $img.src_part.size - 1);
&lt;/script&gt;</code></pre>

<p>Instead of requesting the data via Ajax request, where we would immediately receive a blob, in this case we have to create the blob ourselves from the data URI. To do this, we free the data-URI from the part that does not contain image data: <code>data:image/jpeg;base64</code>. We decode the remaining base64 coded data with the <code>atob</code> command. In order to create a blob from the now binary string data, we have to transfer the data into a Uint8 array, which ensures that the data is not treated as a UTF-8 encoded text. From this array, we can now create a binary blob with the image data of the preview image.</p>

<p>So that we don’t have to adapt the following code for this inline version, we add the attribute <code>data-bytes</code> on the <code>img</code> tag, which in the previous example contains the byte offset from which the second part of the image has to be loaded.</p>

<p>In the network tab of the developer console, you can also check here that loading the preview image does not generate an additional request, while the file size of the HTML page has increased.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4209e75d-e1ad-480a-8081-0be0146dfb1a/network-console-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4209e75d-e1ad-480a-8081-0be0146dfb1a/network-console-1.png" sizes="100vw" caption=" Network console when loading the preview image as data URI (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4209e75d-e1ad-480a-8081-0be0146dfb1a/network-console-1.png'>Large preview</a>)" alt="Shows the network console and the sizes of the HTTP requests" >}}


### Loading the final image

<p>In a second step we load the rest of the image file after two seconds as an example:</p>

<div class="break-out">

<pre><code class="language-javascript">setTimeout(function(){
    var xhr = new XMLHttpRequest();
    xhr.onload = function(){
        if (this.status === 206){
            var blob = new Blob([$img.src_part, this.response], { type: 'image/jpeg'} );
            $img.src = URL.createObjectURL(blob);
        }
    }
    xhr.open('GET', $img.getAttribute('data-src'));
    xhr.setRequestHeader("Range", "bytes="+ (parseInt($img.getAttribute('data-bytes'), 10)+1) +'-');
    xhr.responseType = 'blob';
    xhr.send();
}, 2000);</code></pre>
</div>

<p>In the Range header this time we specify that we want to request the image from the end position of the preview image to the end of the file. The answer to the first request is stored in the property <code>src_part</code> of the DOM object. We use the responses from both requests to create a new blob per <code>new Blob()</code>, which contains the data of the whole image. The blob URL generated from this is used again as <code>src</code> of the DOM object. Now the image is completely loaded.</p>

<p>Also now we can check the loaded sizes in the network tab of the developer console again..</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b8723c-1c47-4177-9864-7b4cb41e7394/network-console-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b8723c-1c47-4177-9864-7b4cb41e7394/network-console-2.png" sizes="100vw" caption="Network console when loading the entire image (31.7 kB) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b8723c-1c47-4177-9864-7b4cb41e7394/network-console-2.png'>Large preview</a>)" alt="Shows the network console and the sizes of the HTTP requests" >}}

## Prototype

<p>At the following URL I have provided a prototype where you can experiment with different parameters: <a href="https://embedded-image-preview.cerdmann.com/prototype/">https://embedded-image-preview.cerdmann.com/prototype/</a></p>

<p>The GitHub repository for the prototype can be found here: <a href="https://github.com/McSodbrenner/embedded-image-preview">https://github.com/McSodbrenner/embedded-image-preview</a></p>

{{% ad-panel-leaderboard %}}

## Considerations At The End

<p>Using the Embedded Image Preview (EIP) technology presented here, we can load qualitatively different preview images from progressive JPEGs with the help of Ajax and HTTP Range Requests. The data from these preview images is not discarded but instead reused to display the entire image.</p>

<p>Furthermore, no preview images need to be created. On the server-side, only the byte offset at which the preview image ends has to be determined and saved. In a CMS system, it should be possible to save this number as an attribute on an image and take it into account when outputting it in the <code>img</code> tag. Even a workflow would be conceivable, which supplements the file name of the picture by the offset, e.g. <em>progressive-8343.jpg</em>, in order not to have to save the offset apart from the picture file. This offset could be extracted by the JavaScript code.</p>

<p>Since the preview image data is reused, this technique could be a better alternative to the usual approach of loading a preview image and then a WebP (and providing a JPEG fallback for non-WebP-supporting browsers). The preview image often destroys the storage advantages of the WebP, which does not support progressive mode.</p>

<p>Currently, preview images in normal LQIP are of inferior quality, since it is assumed that loading the preview data requires additional bandwidth. As Robin Osborne already made clear in a <a href="https://www.robinosborne.co.uk/2018/01/05/image-placeholders-do-it-right-or-dont-do-it-at-all-please/">blog post in 2018</a>, it doesn’t make much sense to show placeholders that don’t give you an idea of the final image. By using the technique suggested here, we can show some more of the final image as a preview image without hesitation by presenting the user a later scan of the progressive JPEG.</p>

<p>In case of a weak network connection of the user, it might make sense, depending on the application, not to load the whole JPEG, but e.g. to omit the last two scans. This produces a much smaller JPEG with an only slightly reduced quality. The user will thank us for it, and we don’t have to store an additional file on the server.</p>

<p>Now I wish you a lot of fun trying out the prototype and look forward to your comments.</p>

{{< signature "dm, yk, il" >}}
