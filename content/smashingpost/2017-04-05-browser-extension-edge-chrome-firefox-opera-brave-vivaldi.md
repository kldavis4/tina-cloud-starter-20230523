---
title: >-
  Creating One Browser Extension For All Browsers: Edge, Chrome, Firefox, Opera,
  Brave And Vivaldi
slug: browser-extension-edge-chrome-firefox-opera-brave-vivaldi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2ce6f9-dba8-4b19-b787-db1ac9da9d2c/xslide4-thumb-large-opt.png
date: 2017-04-05T19:57:19.000Z
author: davidrousset
description: >-
  In today's article, we'll create a JavaScript extension that works in all
  major modern browsers, using the very same code base. Indeed, the Chrome
  extension model based on HTML, CSS and JavaScript is now available almost
  everywhere, and there is even a _Browser Extension Community Group_ working on
  a standard.

  I'll explain how you can install this extension that supports the web
  extension model (i.e. Edge, Chrome, Firefox, Opera, Brave and Vivaldi), and
  provide some simple tips on how to get a unique code base for all of them, but
  also how to debug in each browser.
categories:
  - Coding
  - Sponsored Content
---
I'll explain how you can install this extension that supports the web extension model (i.e. Edge, Chrome, Firefox, Opera, Brave and Vivaldi), and provide some simple tips on how to get a unique code base for all of them, but also how to debug in each browser.

**Note:** We won't cover Safari in this article because it [doesn't support the same extension model](https://developer.apple.com/reference/safariextensions) as others.</p>

## Basics

I won't cover the basics of extension development because plenty of good resources are already available from each vendor:

{{% feature-panel %}}

*   [Google](https://developer.chrome.com/extensions)
*   [Microsoft](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/extensions/) (also, see the great overview video “[Building Extensions for Microsoft Edge](https://channel9.msdn.com/Events/WebPlatformSummit/edgesummit2016/ES1614?wt.mc_id=DX_879946&OC.ID=DX_879946&CR_CC=DX_879946)”)
*   [Mozilla](https://developer.mozilla.org/en-US/Add-ons/WebExtensions) (also, [see the wiki](https://wiki.mozilla.org/WebExtensions))
*   [Opera](https://dev.opera.com/extensions/getting-started/)
*   [Brave](https://github.com/brave/browser-laptop/wiki/Developer-Notes-on-Installing-or-Updating-Extensions)

So, if you've never built an extension before or don't know how it works, have a quick look at those resources. Don't worry: Building one is simple and straightforward.</p>

## Our Extension

Let's build a proof of concept — an extension that uses artificial intelligence (AI) and computer vision to help the blind analyze images on a web page.

We'll see that, with a few lines of code, we can create some powerful features in the browser. In my case, I'm concerned with **accessibility on the web** and I've already spent some time thinking about how to make a [breakout game accessible using web audio and SVG](https://www.davrous.com/2015/08/27/creating-an-accessible-breakout-game-using-web-audio-svg/), for instance.

Still, I've been looking for something that would **help blind people** in a more general way. I was recently inspired while listening to a great talk by [Chris Heilmann](https://twitter.com/codepo8) in Lisbon: “[Pixels and Hidden Meaning in Pixels](https://www.youtube.com/watch?v=TWVNTsdm27U).”

Indeed, using today's AI algorithms in the cloud, as well as text-to-speech technologies, exposed in the browser with the [Web Speech API](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html#tts-section) or using a remote cloud service, we can very easily build an extension that analyzes web page images with missing or improperly filled `alt` text properties.

My little proof of concept simply extracts images from a web page (the one in the active tab) and displays the thumbnails in a list. When you click on one of the images, the extension queries the **Computer Vision API** to get some descriptive text for the image and then uses either the **Web Speech API** or **Bing Speech API** to share it with the visitor.

The video below demonstrates it in Edge, Chrome, Firefox, Opera and Brave.</p>

<iframe loading="lazy" width="560" height="315" src="https://www.youtube.com/embed/gQ6_CZlIKyo" frameborder="0" allowfullscreen></iframe>

You'll notice that, even when the Computer Vision API is analyzing some CGI images, it's very accurate! I'm really impressed by the progress the industry has made on this in recent months.

I'm using these services:

<ul><br>
<li><a href="https://www.microsoft.com/cognitive-services/en-us/computer-vision-api">Computer Vision API</a>, Microsoft Cognitive Services<br>
This is <a href="https://www.microsoft.com/cognitive-services/en-us/subscriptions?productId=/products/54d873dd5eefd00dc474a0f4">free to use</a> (with a quota). You'll need to generate a free key; replace the <code>TODO</code> section in the code with your key to make this extension work on your machine. To get an idea of what this API can do, <a href="https://www.captionbot.ai/">play around with it</a>.</li>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb3e6c33-775d-48b6-aba0-824684bb9320/captionbot-1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb3e6c33-775d-48b6-aba0-824684bb9320/captionbot-1-preview-opt.png" width="681" height="715" alt="CaptionBot" /></a></figure>

<li><a href="https://www.microsoft.com/cognitive-services/en-us/speech-api">Bing Text to Speech API</a>, Microsoft Cognitive Services<br>
This is also <a href="https://www.microsoft.com/cognitive-services/en-us/subscriptions?productId=/products/Bing.Speech.Preview">free to use</a> (with a quota, too). You'll need to generate a free key again. We'll also use a <a href="https://github.com/davrous/BingTTSClientJSLib">small library</a> that I wrote recently to call this API from JavaScript. If you don't have a Bing key, the extension will always fall back to the Web Speech API, which is supported by all recent browsers.</li>
</ul>

But feel free to try other similar services:

*   [Visual Recognition](https://visual-recognition-demo.mybluemix.net/), IBM Watson
*   [Cloud Vision API](https://cloud.google.com/vision/), Google

You can find the code for this small browser extension on [my GitHub page](https://github.com/davrous/dareangel). Feel free to modify the code for other products you want to test.</p>

## Tip To Make Your Code Compatible With All Browsers

Most of the code and tutorials you'll find use the namespace `chrome.xxx` for the Extension API (`chrome.tabs`, for instance).

But, as I've said, the Extension API model is currently being standardized to `browser.xxx`, and some browsers are defining their own namespaces in the meantime (for example, Edge is using `msBrowser`).

Fortunately, most of the API remains the same behind the browser. So, it's very simple to create a little trick to support all browsers and namespace definitions, thanks to the beauty of JavaScript:

<pre><code class="language-javascript">
window.browser = (function () {
  return window.msBrowser ||
    window.browser ||
    window.chrome;
})();
</code></pre>

And voilà!

Of course, you'll also need to use the subset of the API supported by all browsers. For instance:

*   Microsoft Edge has a [list of support](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/extensions/api-support/).
*   Mozilla Firefox shares its [current Chrome incompatibilities](https://developer.mozilla.org/en-US/Add-ons/WebExtensions).
*   Opera maintains its own list of [extension APIs supported](https://dev.opera.com/extensions/apis/) by its browser.</p>

## Extension Architecture

Let's review together the architecture of this extension. If you're new to browser extensions, this should help you to understand the flow.

Let's start with the [manifest file](https://github.com/davrous/dareangel/blob/master/manifest.json):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f499a3a7-8cbc-44d9-83dc-247755c994d8/slide1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d21e381-d19b-4243-aa84-19105969d33d/slide1-preview-opt.png" width="780" height="439" alt="Slide1" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f499a3a7-8cbc-44d9-83dc-247755c994d8/slide1-large-opt.png">View large version</a>)</figcaption></figure>

This manifest file and its associated JSON is the minimum you'll need to load an extension in all browsers, if we're not considering the code of the extension itself, of course. Please [check the source](https://github.com/davrous/dareangel/blob/master/manifest.json) in my GitHub account, and start from here to be sure that your extension is compatible with all browsers.

For instance, you must specify an `author` property to load it in Edge; otherwise, it will throw an error. You'll also need to use the same structure for the icons. The `default_title` property is also important because it's used by screen readers in some browsers.

Here are links to the documentation to help you build a manifest file that is compatible everywhere:

*   [Chrome](https://developer.chrome.com/extensions/manifest)
*   [Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/extensions/api-support/supported-manifest-keys/)
*   [Firefox](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/manifest.json)

The sample extension used in this article is mainly based on the concept of the [content script](https://dev.opera.com/extensions/architecture-overview/#the-content-script). This is a script living in the context of the page that we'd like to inspect. Because it has access to the DOM, it will help us to retrieve the images contained in the web page. If you'd like to know more about what a content script is, [Opera](https://dev.opera.com/extensions/content-scripts/), [Mozilla](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Content_scripts) and [Google](https://developer.chrome.com/extensions/content_scripts) have documentation on it.

Our [content script](https://github.com/davrous/dareangel/blob/master/dareangel.client.ts) is simple:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22734e5a-bc5f-413e-9d09-13a79e9bc908/slide2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72de6ecb-dbe7-45d1-a9aa-494708d592f3/slide2-preview-opt.png" width="780" height="439" alt="Slide2" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22734e5a-bc5f-413e-9d09-13a79e9bc908/slide2-large-opt.png">View large version</a>)</figcaption></figure>

<pre><code class="language-javascript">
console.log("Dare Angel content script started");

browser.runtime.onMessage.addListener(function (request, sender, sendResponse) {
    if (request.command == "requestImages") {
        var images = document.getElementsByTagName('img');
        var imagesList = [];
        for (var i = 0; i < images.length; i++) {
            if ((images[i].src.toLowerCase().endsWith(".jpg") || images[i].src.toLowerCase().endsWith(".png"))
                && (images[i].width > 64 && images[i].height > 64)) {
                imagesList.push({ url: images[i].src, alt: images[i].alt });
            }
        }
        sendResponse(JSON.stringify(imagesList));
    }
});
view raw
</code></pre>

This first logs into the console to let you check that the extension has properly loaded. Check it via your browser's developer tool, accessible from `F12`, `Control + Shift + I` or `⌘ + ⌥ + I`.

It then waits for a message from the UI page with a `requestImages` command to get all of the images available in the current DOM, and then it returns a list of their URLs if they're bigger than 64 × 64 pixels (to avoid all of the pixel-tracking junk and low-resolution images).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04cbae45-6a13-40cc-8c3c-1d716161ce34/slide3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0e7aa53-4a38-47cc-a4f8-73aa2b338f75/slide3-preview-opt.png" width="780" height="439" alt="Slide3" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04cbae45-6a13-40cc-8c3c-1d716161ce34/slide3-large-opt.png">View large version</a>)</figcaption></figure>

The popup [UI page](https://github.com/davrous/dareangel/blob/master/dashboard.html) we're using is very simple and will display the list of images returned by the content script inside a [flexbox container](https://github.com/davrous/dareangel/blob/master/dashboard.css). It loads the `start.js` script, which immediately creates an instance of [`dareangel.dashboard.js`](https://github.com/davrous/dareangel/blob/master/dareangel.dashboard.js) to send a message to the content script to get the URLs of the images in the currently visible tab.

Here's the code that lives in the UI page, requesting the URLs to the content script:

<pre><code class="language-javascript">
browser.tabs.query({ active: true, currentWindow: true }, (tabs) => {
    browser.tabs.sendMessage(tabs[0].id, { command: "requestImages" }, (response) => {
        this._imagesList = JSON.parse(response);
        this._imagesList.forEach((element) => {
            var newImageHTMLElement = document.createElement("img");
            newImageHTMLElement.src = element.url;
            newImageHTMLElement.alt = element.alt;
            newImageHTMLElement.tabIndex = this._tabIndex;
            this._tabIndex++;
            newImageHTMLElement.addEventListener("focus", (event) => {
                if (COMPUTERVISIONKEY !== "") {
                    this.analyzeThisImage(event.target.src);
                }
                else {
                    var warningMsg = document.createElement("div");
                    warningMsg.innerHTML = "<h2>Please generate a Computer Vision key in the other tab.</h2>";
                    this._targetDiv.insertBefore(warningMsg, this._targetDiv.firstChild);
                    browser.tabs.create({ active: false, url: "https://www.microsoft.com/cognitive-services/en-US/sign-up?ReturnUrl=/cognitive-services/en-us/subscriptions?productId=%2fproducts%2f54d873dd5eefd00dc474a0f4" });
                }
            });
            this._targetDiv.appendChild(newImageHTMLElement);
        });
    });
});
</code></pre>

We're creating image elements. Each image will trigger an event if it has focus, querying the Computer Vision API for review.

This is done by this simple XHR call:

<pre><code class="language-css">
analyzeThisImage(url) {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = () => {
        if (xhr.readyState == 4 && xhr.status == 200) {
            var response = document.querySelector('#response');
            var reponse = JSON.parse(xhr.response);
            var resultToSpeak = `With a confidence of ${Math.round(reponse.description.captions[0].confidence * 100)}%, I think it's ${reponse.description.captions[0].text}`;
            console.log(resultToSpeak);
            if (!this._useBingTTS || BINGSPEECHKEY === "") {
                var synUtterance = new SpeechSynthesisUtterance();
                synUtterance.text = resultToSpeak;
                window.speechSynthesis.speak(synUtterance);
            }
            else {
                this._bingTTSclient.synthesize(resultToSpeak);
            }
        }
    };
    xhr.onerror = (evt) => {
        console.log(evt);
    };
    try {
        xhr.open('POST', 'https://api.projectoxford.ai/vision/v1.0/describe');
        xhr.setRequestHeader("Content-Type", "application/json");
        xhr.setRequestHeader("Ocp-Apim-Subscription-Key", COMPUTERVISIONKEY);
        var requestObject = { "url": url };
        xhr.send(JSON.stringify(requestObject));
    }
    catch (ex) {
        console.log(ex);
    }
}
view raw
</code></pre>

The following articles will you help you to understand how this Computer Vision API works:

*   “[Analyzing an Image Version 1.0](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/AnalyzeImage),” Microsoft Cognitive Services
*   “[Computer Vision API, v1.0](https://dev.projectoxford.ai/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa),” Microsoft Cognitive Services  
    This shows you via an interactive console in a web page how to call the REST API with the proper JSON properties, and the JSON object you'll get in return. It's useful to understand how it works and how you will call it.

In our case, we're using the `describe` feature of the API. You'll also notice in the callback that we will try to use either the **Web Speech API** or the **Bing Text-to-Speech** service, based on your options.

Here, then, is the global workflow of this little extension:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2ce6f9-dba8-4b19-b787-db1ac9da9d2c/xslide4-thumb-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b7e5a39-8070-4cd2-be10-da026bf79770/xslide4-thumb-preview-opt.png" width="780" height="439" alt="Slide4" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2ce6f9-dba8-4b19-b787-db1ac9da9d2c/xslide4-thumb-large-opt.png">View large version</a>)</figcaption></figure>

## Loading The Extension In Each Browser

Let's review quickly how to install the extension in each browser.</p>

### Prerequisites

Download or clone [my small extension](https://github.com/davrous/dareangel) from GitHub somewhere to your hard drive.

Also, modify `dareangel.dashboard.js` to add at least a Computer Vision API key. Otherwise, the extension will only be able to display the images extracted from the web page.</p>

### Microsoft Edge

First, you'll need at least a Windows 10 Anniversary Update (OS Build 14393+) to have support for extensions in Edge.

Then, open Edge and type `about:flags` in the address bar. Check the “Enable extension developer features.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00e0030-f948-419b-abec-70804cf29705/enableinedge001-1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00e0030-f948-419b-abec-70804cf29705/enableinedge001-1-preview-opt.png" width="695" height="768" alt="EnableInEdge001" /></a></figcaption></figure>

Click on “…” in the Edge's navigation bar and then “Extensions” and then “Load extension,” and select the folder where you've cloned my GitHub repository. You'll get this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fadbeb99-ba48-40a4-a40a-77e28c7d1c8e/edge001-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fadbeb99-ba48-40a4-a40a-77e28c7d1c8e/edge001-preview-opt.png" width="450" height="570" alt="" /></a></figure>

Click on this freshly loaded extension, and enable “Show button next to the address bar.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcedf36e-aaea-4d3e-820e-97cd2e094836/enableinedge003-1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcedf36e-aaea-4d3e-820e-97cd2e094836/enableinedge003-1-preview-opt.png" width="465" height="768" alt="EnableInEdge003" /></a></figure>

Note the “Reload extension” button, which is useful while you're developing your extension. You won't be forced to remove or reinstall it during the development process; just click the button to refresh the extension.

Navigate to [BabylonJS](https://www.babylonjs.com/), and click on the Dare Angel (DA) button to follow the same demo as shown in the video.</p>

### Google Chrome, Opera, Vivaldi

In Chrome, navigate to `chrome://extensions`. In Opera, navigate to `opera://extensions`. And in Vivaldi, navigate to `vivaldi://extensions`. Then, enable “Developer mode.”

Click on “Load unpacked extension,” and choose the folder where you've extracted my extension.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cad7f563-20e5-480a-8bd6-b08af63900f3/chrome001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e6131f-bea8-4336-a729-8fbaf49cefef/chrome001-preview-opt.png" width="780" height="508" alt="Chrome001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cad7f563-20e5-480a-8bd6-b08af63900f3/chrome001-large-opt.png">View large version</a>)</figcaption></figure>

Navigate to [BabylonJS](https://www.babylonjs.com/), and open the extension to check that it works fine.</p>

### Mozilla Firefox

You've got two options here. The first is to temporarily load your extension, which is as easy as it is in Edge and Chrome.

Open Firefox, navigate to `about:debugging` and click “Load Temporary Add-on.” Then, navigate to the folder of the extension, and select the `manifest.json` file. That's it! Now go to [BabylonJS](https://www.babylonjs.com/) to test the extension.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac784201-f63c-423c-b0e6-0ac8ca1e80f7/firefox001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd073cad-e447-47b7-b2c6-440c2aa91840/firefox001-preview-opt.png" width="780" height="374" alt="Firefox001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac784201-f63c-423c-b0e6-0ac8ca1e80f7/firefox001-large-opt.png">View large version</a>)</figcaption></figure>

The only problem with this solution is that every time you close the browser, you'll have to reload the extension. The second option would be to use the XPI packaging. You can learn more about this in “[Extension Packaging](https://developer.mozilla.org/en-US/Add-ons/Extension_Packaging)” on the Mozilla Developer Network.</p>

### Brave

The public version of Brave doesn't have a “developer mode” embedded in it to let you load an unsigned extension. You'll need to build your own version of it by following the steps in “[Loading Chrome Extensions in Brave](https://blog.brave.com/loading-chrome-extensions-in-brave/).”

As explained in that article, once you've cloned Brave, you'll need to open the `extensions.js` file in a text editor. Locate the lines below, and insert the registration code for your extension. In my case, I've just added the two last lines:

<pre><code class="language-javascript">
  // Manually install the braveExtension and torrentExtension
  extensionInfo.setState(config.braveExtensionId, extensionStates.REGISTERED)
  loadExtension(config.braveExtensionId, getExtensionsPath('brave'), generateBraveManifest(), 'component')

  extensionInfo.setState('DareAngel', extensionStates.REGISTERED)
  loadExtension('DareAngel', getExtensionsPath('DareAngel/'))
view raw
</code></pre>

Copy the extension to the `app/extensions` folder. Open two command prompts in the `browser-laptop` folder. In the first one, launch `npm run watch`, and wait for webpack to finish building Brave's Electron app. It should say, “webpack: bundle is now VALID.” Otherwise, you'll run into some issues.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfbdc9ac-2b4c-449d-93d6-e661762ae727/brave001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23c830b6-af2e-4c46-a717-f4a9e8c1baed/brave001-preview-opt.png" width="780" height="452" alt="Brave001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfbdc9ac-2b4c-449d-93d6-e661762ae727/brave001-large-opt.png">View large version</a>)</figcaption></figure>

Then, in the second command prompt, launch `npm start`, which will launch our slightly custom version of Brave.

In Brave, navigate to `about:extensions`, and you should see the extension displayed and loaded in the address bar.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9747eeff-0e85-4411-b92a-8ae18b999929/brave002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57b89e5-d7fd-4f54-9946-764183823535/brave002-preview-opt.png" width="780" height="418" alt="Brave002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9747eeff-0e85-4411-b92a-8ae18b999929/brave002-large-opt.png">View large version</a>)</figcaption></figure>

## Debugging The Extension In Each Browser

**Tip for all browsers**: Using `console.log()`, simply log some data from the flow of your extension. Most of the time, using the browser's developer tools, you'll be able to click on the JavaScript file that has logged it to open it and debug it.</p>

### Microsoft Edge

To debug the client script part, living in the context of the page, you just need to open `F12`. Then, click on the “Debugger” tab and find your extension's folder.

Open the script file that you'd like to debug — `dareangel.client.js`, in my case — and debug your code as usual, setting up breakpoints, etc.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a8ce888-2674-44f2-b403-bde359f505ac/debuginedge001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ccc2ec3-9df4-473b-bda0-18d91b0a97ce/debuginedge001-preview-opt.png" width="780" height="404" alt="DebugInEdge001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a8ce888-2674-44f2-b403-bde359f505ac/debuginedge001-large-opt.png">View large version</a>)</figcaption></figure>

If your extension creates a separate tab to do its job (like the [Page Analyzer](https://www.microsoft.com/store/p/page-analyzer/9nblggh4qws7), which our [Vorlon.js](https://www.vorlonjs.io/) team published in the store), simply press `F12` on that tab to debug it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5b84c-77ad-4a23-bbea-f135da6ae4f0/debuginedge002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6a1ab42-5ef9-413c-9716-4db7dba608f9/debuginedge002-preview-opt.png" width="780" height="505" alt="DebugInEdge002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5b84c-77ad-4a23-bbea-f135da6ae4f0/debuginedge002-large-opt.png">View large version</a>)</figcaption></figure>

If you'd like to debug the popup page, you'll first need to get the ID of your extension. To do that, simply go into the property of the extension and you'll find an ID property:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bb7215-bcbf-4ed3-92b8-8a862b522ebe/debuginedge003-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bb7215-bcbf-4ed3-92b8-8a862b522ebe/debuginedge003-preview-opt.png" width="360" height="518" alt="DebugInEdge003" /></a></figure>

Then, you'll need to type in the address bar something like `ms-browser-extension://ID_of_your_extension/yourpage.html`. In our case, it would be `ms-browser-extension://DareAngel_vdbyzyarbfgh8/dashboard.html`. Then, simply use `F12` on this page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336d9e44-00b1-4129-bf58-81ee37251bf3/debuginedge004-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1a6b5a1-9319-49be-9b54-23ac9f652d4e/debuginedge004-preview-opt.png" width="780" height="577" alt="DebugInEdge004" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336d9e44-00b1-4129-bf58-81ee37251bf3/debuginedge004-large-opt.png">View large version</a>)</figcaption></figure>

### Google Chrome, Opera, Vivaldi, Brave

Because Chrome and Opera rely on the same Blink code base, they share the same debugging process. Even though Brave and Vivaldi are forks of Chromium, they also share the same debugging process most of the time.

To debug the client script part, open the browser's developer tools on the page that you'd like to debug (pressing `F12`, `Control + Shift + I` or `⌘ + ⌥ + I`, depending on the browser or platform you're using).

Then, click on the “Content scripts” tab and find your extension's folder. Open the script file that you'd like to debug, and debug your code just as you would do with any JavaScript code.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf9a85a-0356-4535-9161-9cf0dfaf85a3/debuginchrome001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a98079d-0793-45c2-b6ff-b0306494127a/debuginchrome001-preview-opt.png" width="780" height="366" alt="DebugInChrome001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf9a85a-0356-4535-9161-9cf0dfaf85a3/debuginchrome001-large-opt.png">View large version</a>)</figcaption></figure>

The popup [UI page](https://github.com/davrous/dareangel/blob/master/dashboard.html) we're using is very simple and will display the list of images returned by the content script inside a [flexbox container](https://github.com/davrous/dareangel/blob/master/dashboard.css). It loads the `start.js` script, which immediately creates an instance of [`dareangel.dashboard.js`](https://github.com/davrous/dareangel/blob/master/dareangel.dashboard.js) to send a message to the content script to get the URLs of the images in the currently visible tab.

Here's the code that lives in the UI page, requesting the URLs to the content script:

<pre><code class="language-javascript">
browser.tabs.query({ active: true, currentWindow: true }, (tabs) => {
    browser.tabs.sendMessage(tabs[0].id, { command: "requestImages" }, (response) => {
        this._imagesList = JSON.parse(response);
        this._imagesList.forEach((element) => {
            var newImageHTMLElement = document.createElement("img");
            newImageHTMLElement.src = element.url;
            newImageHTMLElement.alt = element.alt;
            newImageHTMLElement.tabIndex = this._tabIndex;
            this._tabIndex++;
            newImageHTMLElement.addEventListener("focus", (event) => {
                if (COMPUTERVISIONKEY !== "") {
                    this.analyzeThisImage(event.target.src);
                }
                else {
                    var warningMsg = document.createElement("div");
                    warningMsg.innerHTML = "<h2>Please generate a Computer Vision key in the other tab.</h2>";
                    this._targetDiv.insertBefore(warningMsg, this._targetDiv.firstChild);
                    browser.tabs.create({ active: false, url: "https://www.microsoft.com/cognitive-services/en-US/sign-up?ReturnUrl=/cognitive-services/en-us/subscriptions?productId=%2fproducts%2f54d873dd5eefd00dc474a0f4" });
                }
            });
            this._targetDiv.appendChild(newImageHTMLElement);
        });
    });
});
</code></pre>

We're creating image elements. Each image will trigger an event if it has focus, querying the Computer Vision API for review.

This is done by this simple XHR call:

<pre><code class="language-css">
analyzeThisImage(url) {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = () => {
        if (xhr.readyState == 4 && xhr.status == 200) {
            var response = document.querySelector('#response');
            var reponse = JSON.parse(xhr.response);
            var resultToSpeak = `With a confidence of ${Math.round(reponse.description.captions[0].confidence * 100)}%, I think it's ${reponse.description.captions[0].text}`;
            console.log(resultToSpeak);
            if (!this._useBingTTS || BINGSPEECHKEY === "") {
                var synUtterance = new SpeechSynthesisUtterance();
                synUtterance.text = resultToSpeak;
                window.speechSynthesis.speak(synUtterance);
            }
            else {
                this._bingTTSclient.synthesize(resultToSpeak);
            }
        }
    };
    xhr.onerror = (evt) => {
        console.log(evt);
    };
    try {
        xhr.open('POST', 'https://api.projectoxford.ai/vision/v1.0/describe');
        xhr.setRequestHeader("Content-Type", "application/json");
        xhr.setRequestHeader("Ocp-Apim-Subscription-Key", COMPUTERVISIONKEY);
        var requestObject = { "url": url };
        xhr.send(JSON.stringify(requestObject));
    }
    catch (ex) {
        console.log(ex);
    }
}
view raw
</code></pre>

The following articles will you help you to understand how this Computer Vision API works:

*   “[Analyzing an Image Version 1.0](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/AnalyzeImage),” Microsoft Cognitive Services
*   “[Computer Vision API, v1.0](https://dev.projectoxford.ai/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa),” Microsoft Cognitive Services  
    This shows you via an interactive console in a web page how to call the REST API with the proper JSON properties, and the JSON object you'll get in return. It's useful to understand how it works and how you will call it.

In our case, we're using the `describe` feature of the API. You'll also notice in the callback that we will try to use either the **Web Speech API** or the **Bing Text-to-Speech** service, based on your options.

Here, then, is the global workflow of this little extension:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2ce6f9-dba8-4b19-b787-db1ac9da9d2c/xslide4-thumb-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b7e5a39-8070-4cd2-be10-da026bf79770/xslide4-thumb-preview-opt.png" width="780" height="439" alt="Slide4" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2ce6f9-dba8-4b19-b787-db1ac9da9d2c/xslide4-thumb-large-opt.png">View large version</a>)</figcaption></figure>

## Loading The Extension In Each Browser

Let's review quickly how to install the extension in each browser.</p>

### Prerequisites

Download or clone [my small extension](https://github.com/davrous/dareangel) from GitHub somewhere to your hard drive.

Also, modify `dareangel.dashboard.js` to add at least a Computer Vision API key. Otherwise, the extension will only be able to display the images extracted from the web page.</p>

### Microsoft Edge

First, you'll need at least a Windows 10 Anniversary Update (OS Build 14393+) to have support for extensions in Edge.

Then, open Edge and type `about:flags` in the address bar. Check the “Enable extension developer features.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00e0030-f948-419b-abec-70804cf29705/enableinedge001-1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00e0030-f948-419b-abec-70804cf29705/enableinedge001-1-preview-opt.png" width="695" height="768" alt="EnableInEdge001" /></a></figcaption></figure>

Click on “…” in the Edge's navigation bar and then “Extensions” and then “Load extension,” and select the folder where you've cloned my GitHub repository. You'll get this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fadbeb99-ba48-40a4-a40a-77e28c7d1c8e/edge001-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fadbeb99-ba48-40a4-a40a-77e28c7d1c8e/edge001-preview-opt.png" width="450" height="570" alt="" /></a></figure>

Click on this freshly loaded extension, and enable “Show button next to the address bar.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcedf36e-aaea-4d3e-820e-97cd2e094836/enableinedge003-1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcedf36e-aaea-4d3e-820e-97cd2e094836/enableinedge003-1-preview-opt.png" width="465" height="768" alt="EnableInEdge003" /></a></figure>

Note the “Reload extension” button, which is useful while you're developing your extension. You won't be forced to remove or reinstall it during the development process; just click the button to refresh the extension.

Navigate to [BabylonJS](https://www.babylonjs.com/), and click on the Dare Angel (DA) button to follow the same demo as shown in the video.</p>

### Google Chrome, Opera, Vivaldi

In Chrome, navigate to `chrome://extensions`. In Opera, navigate to `opera://extensions`. And in Vivaldi, navigate to `vivaldi://extensions`. Then, enable “Developer mode.”

Click on “Load unpacked extension,” and choose the folder where you've extracted my extension.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cad7f563-20e5-480a-8bd6-b08af63900f3/chrome001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e6131f-bea8-4336-a729-8fbaf49cefef/chrome001-preview-opt.png" width="780" height="508" alt="Chrome001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cad7f563-20e5-480a-8bd6-b08af63900f3/chrome001-large-opt.png">View large version</a>)</figcaption></figure>

Navigate to [BabylonJS](https://www.babylonjs.com/), and open the extension to check that it works fine.</p>

### Mozilla Firefox

You've got two options here. The first is to temporarily load your extension, which is as easy as it is in Edge and Chrome.

Open Firefox, navigate to `about:debugging` and click “Load Temporary Add-on.” Then, navigate to the folder of the extension, and select the `manifest.json` file. That's it! Now go to [BabylonJS](https://www.babylonjs.com/) to test the extension.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac784201-f63c-423c-b0e6-0ac8ca1e80f7/firefox001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd073cad-e447-47b7-b2c6-440c2aa91840/firefox001-preview-opt.png" width="780" height="374" alt="Firefox001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac784201-f63c-423c-b0e6-0ac8ca1e80f7/firefox001-large-opt.png">View large version</a>)</figcaption></figure>

The only problem with this solution is that every time you close the browser, you'll have to reload the extension. The second option would be to use the XPI packaging. You can learn more about this in “[Extension Packaging](https://developer.mozilla.org/en-US/Add-ons/Extension_Packaging)” on the Mozilla Developer Network.</p>

### Brave

The public version of Brave doesn't have a “developer mode” embedded in it to let you load an unsigned extension. You'll need to build your own version of it by following the steps in “[Loading Chrome Extensions in Brave](https://blog.brave.com/loading-chrome-extensions-in-brave/).”

As explained in that article, once you've cloned Brave, you'll need to open the `extensions.js` file in a text editor. Locate the lines below, and insert the registration code for your extension. In my case, I've just added the two last lines:

<pre><code class="language-javascript">
  // Manually install the braveExtension and torrentExtension
  extensionInfo.setState(config.braveExtensionId, extensionStates.REGISTERED)
  loadExtension(config.braveExtensionId, getExtensionsPath('brave'), generateBraveManifest(), 'component')

  extensionInfo.setState('DareAngel', extensionStates.REGISTERED)
  loadExtension('DareAngel', getExtensionsPath('DareAngel/'))
view raw
</code></pre>

Copy the extension to the `app/extensions` folder. Open two command prompts in the `browser-laptop` folder. In the first one, launch `npm run watch`, and wait for webpack to finish building Brave's Electron app. It should say, “webpack: bundle is now VALID.” Otherwise, you'll run into some issues.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfbdc9ac-2b4c-449d-93d6-e661762ae727/brave001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23c830b6-af2e-4c46-a717-f4a9e8c1baed/brave001-preview-opt.png" width="780" height="452" alt="Brave001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfbdc9ac-2b4c-449d-93d6-e661762ae727/brave001-large-opt.png">View large version</a>)</figcaption></figure>

Then, in the second command prompt, launch `npm start`, which will launch our slightly custom version of Brave.

In Brave, navigate to `about:extensions`, and you should see the extension displayed and loaded in the address bar.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9747eeff-0e85-4411-b92a-8ae18b999929/brave002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57b89e5-d7fd-4f54-9946-764183823535/brave002-preview-opt.png" width="780" height="418" alt="Brave002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9747eeff-0e85-4411-b92a-8ae18b999929/brave002-large-opt.png">View large version</a>)</figcaption></figure>

## Debugging The Extension In Each Browser

**Tip for all browsers**: Using `console.log()`, simply log some data from the flow of your extension. Most of the time, using the browser's developer tools, you'll be able to click on the JavaScript file that has logged it to open it and debug it.</p>

### Microsoft Edge

To debug the client script part, living in the context of the page, you just need to open `F12`. Then, click on the “Debugger” tab and find your extension's folder.

Open the script file that you'd like to debug — `dareangel.client.js`, in my case — and debug your code as usual, setting up breakpoints, etc.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a8ce888-2674-44f2-b403-bde359f505ac/debuginedge001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ccc2ec3-9df4-473b-bda0-18d91b0a97ce/debuginedge001-preview-opt.png" width="780" height="404" alt="DebugInEdge001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a8ce888-2674-44f2-b403-bde359f505ac/debuginedge001-large-opt.png">View large version</a>)</figcaption></figure>

If your extension creates a separate tab to do its job (like the [Page Analyzer](https://www.microsoft.com/store/p/page-analyzer/9nblggh4qws7), which our [Vorlon.js](https://www.vorlonjs.io/) team published in the store), simply press `F12` on that tab to debug it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5b84c-77ad-4a23-bbea-f135da6ae4f0/debuginedge002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6a1ab42-5ef9-413c-9716-4db7dba608f9/debuginedge002-preview-opt.png" width="780" height="505" alt="DebugInEdge002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5b84c-77ad-4a23-bbea-f135da6ae4f0/debuginedge002-large-opt.png">View large version</a>)</figcaption></figure>

If you'd like to debug the popup page, you'll first need to get the ID of your extension. To do that, simply go into the property of the extension and you'll find an ID property:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bb7215-bcbf-4ed3-92b8-8a862b522ebe/debuginedge003-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bb7215-bcbf-4ed3-92b8-8a862b522ebe/debuginedge003-preview-opt.png" width="360" height="518" alt="DebugInEdge003" /></a></figure>

Then, you'll need to type in the address bar something like `ms-browser-extension://ID_of_your_extension/yourpage.html`. In our case, it would be `ms-browser-extension://DareAngel_vdbyzyarbfgh8/dashboard.html`. Then, simply use `F12` on this page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336d9e44-00b1-4129-bf58-81ee37251bf3/debuginedge004-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1a6b5a1-9319-49be-9b54-23ac9f652d4e/debuginedge004-preview-opt.png" width="780" height="577" alt="DebugInEdge004" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336d9e44-00b1-4129-bf58-81ee37251bf3/debuginedge004-large-opt.png">View large version</a>)</figcaption></figure>

### Google Chrome, Opera, Vivaldi, Brave

Because Chrome and Opera rely on the same Blink code base, they share the same debugging process. Even though Brave and Vivaldi are forks of Chromium, they also share the same debugging process most of the time.

To debug the client script part, open the browser's developer tools on the page that you'd like to debug (pressing `F12`, `Control + Shift + I` or `⌘ + ⌥ + I`, depending on the browser or platform you're using).

Then, click on the “Content scripts” tab and find your extension's folder. Open the script file that you'd like to debug, and debug your code just as you would do with any JavaScript code.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf9a85a-0356-4535-9161-9cf0dfaf85a3/debuginchrome001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a98079d-0793-45c2-b6ff-b0306494127a/debuginchrome001-preview-opt.png" width="780" height="366" alt="DebugInChrome001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf9a85a-0356-4535-9161-9cf0dfaf85a3/debuginchrome001-large-opt.png">View large version</a>)</figcaption></figure>

To debug a tab that your extension would create, it's exactly the same as with Edge: Simply use the developer tools.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6958f572-1ffa-4135-a778-66da4a2d5c7b/debuginchrome002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afc658d9-75a5-45b7-bde1-0b479ddfcad8/debuginchrome002-preview-opt.png" width="780" height="532" alt="DebugInChrome002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6958f572-1ffa-4135-a778-66da4a2d5c7b/debuginchrome002-large-opt.png">View large version</a>)</figcaption></figure>

For Chrome and Opera, to debug the popup page, right-click on the button of your extension next to the address bar and choose “Inspect popup,” or open the HTML pane of the popup and right-click inside it to “Inspect.” Vivaldi only supports right-click and then “Inspect” inside the HTML pane once opened.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627f2020-8d41-4d9c-acaa-793d72520efd/debuginchrome003-1-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c00a3ef-fda8-4237-9aef-27fc3457e6e9/debuginchrome003-1-preview-opt.jpeg" width="780" height="438" alt="DebugInChrome003" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627f2020-8d41-4d9c-acaa-793d72520efd/debuginchrome003-1-large-opt.jpg">View large version</a>)</figcaption></figure>

For Brave, it's the same process as with Edge. You first need to find the GUID associated with your extension in `about:extensions`:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff612a1d-7cfc-4b7e-9869-e594670f73ec/bravedebug001-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff612a1d-7cfc-4b7e-9869-e594670f73ec/bravedebug001-preview-opt.png" width="771" height="463" alt="BraveDebug001" /></a></figure>

And then, in a separate tab, open the page you'd like to debug like — in my case, `chrome-extension://bodaahkboijjjodkbmmddgjldpifcjap/dashboard.html` — and open developer tools.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ca71f99-7c98-45e7-9c64-23629ea71e6f/bravedebug002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58608f58-a880-4fb1-987d-b2701a774908/bravedebug002-preview-opt.png" width="780" height="527" alt="BraveDebug002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ca71f99-7c98-45e7-9c64-23629ea71e6f/bravedebug002-large-opt.png">View large version</a>)</figcaption></figure>

For the layout, you have a bit of help using `Shift + F8`, which will let you inspect the complete frame of Brave. And you'll discover that Brave is an Electron app using React!

Note, for instance, the `data-reactroot` attribute.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4651970d-5b3d-412d-a999-a4d03b42799e/bravedebug003-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bedf4af-8d05-4e93-a9f9-1b9d4f517690/bravedebug003-preview-opt.jpeg" width="780" height="439" alt="BraveDebug003" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4651970d-5b3d-412d-a999-a4d03b42799e/bravedebug003-large-opt.jpg">View large version</a>)</figcaption></figure>

**Note**: I had to slightly modify the CSS of the extension for Brave because it currently displays popups with a transparent background by default, and I also had some issues with the height of my images collection. I've limited it to four elements in Brave.</p>

### Mozilla Firefox

Mozilla has really great [documentation on debugging web extensions](https://developer.mozilla.org/fr/Add-ons/WebExtensions/Debugging).

For the client script part, it's the same as in Edge, Chrome, Opera and Brave. Simply open the developer tools in the tab you'd like to debug, and you'll find a `moz-extension://guid` section with your code to debug:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39ffe362-02f7-4e37-9aa5-87c1f96b8abc/debuginfirefox001-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4553312e-e30f-4c16-a3b9-ba5eb263fb31/debuginfirefox001-preview-opt.png" width="780" height="492" alt="DebugInFirefox001" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39ffe362-02f7-4e37-9aa5-87c1f96b8abc/debuginfirefox001-large-opt.png">View large version</a>)</figcaption></figure>

If you need to debug a tab that your extension would create (like Vorlon.js' Page Analyzer extension), simply use the developer tools:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65cbf26d-7619-4142-9f4b-19f9ae49fd70/debuginfirefox002-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5310fea1-6644-4dc8-89dd-fc27149299ac/debuginfirefox002-preview-opt.png" width="780" height="675" alt="DebugInFirefox002" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65cbf26d-7619-4142-9f4b-19f9ae49fd70/debuginfirefox002-large-opt.png">View large version</a>)</figcaption></figure>

Finally, debugging a popup is a bit more complex but is well explained in the “[Debugging Popups](https://developer.mozilla.org/fr/Add-ons/WebExtensions/Debugging)” section of the documentation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0413aa48-f703-4966-b80e-17be8bf36f0c/debuginfirefox003-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f272ba0c-1427-4d32-9198-38877b42ff41/debuginfirefox003-preview-opt.jpeg" width="780" height="440" alt="DebugInFirefox003" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0413aa48-f703-4966-b80e-17be8bf36f0c/debuginfirefox003-large-opt.jpg">View large version</a>)</figcaption></figure>

## Publishing Your Extension In Each Store

Each vendor has detailed documentation on the process to follow to publish your extension in its store. They all take similar approaches. You need to package the extension in a particular file format — most of the time, a ZIP-like container. Then, you have to submit it in a dedicated portal, choose a pricing model and wait for the review process to complete. If accepted, your extension will be downloadable in the browser itself by any user who visits the extensions store.

Here are the various processes:

*   Google: “[Publish in the Chrome Web Store](https://developer.chrome.com/webstore/publish)”
*   Mozilla: “[Publishing your WebExtension](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Publishing_your_WebExtension)”
*   Opera: “[Publishing Guidelines](https://dev.opera.com/extensions/publishing-guidelines/)”
*   Microsoft: “[Packaging Microsoft Edge Extensions](https://docs.microsoft.com/en-us/microsoft-edge/extensions/guides/packaging)”

Please note that submitting a Microsoft Edge extension to the Windows Store is currently a restricted capability. [Reach out to the Microsoft Edge team](https://aka.ms/extension-request) with your request to be a part of the Windows Store, and they'll consider you for a future update.

I've tried to share as much of what I've learned from working on our [Vorlon.js Page Analyzer extension](https://www.microsoft.com/store/p/page-analyzer/9nblggh4qws7) and this little proof of concept.

Some developers remember the pain of working through various implementations to build their extension — whether it meant using different build directories, or working with slightly different extension APIs, or following totally different approaches, such as Firefox's XUL extensions or Internet Explorer's BHOs and ActiveX.

It's awesome to see that, today, using our regular JavaScript, CSS and HTML skills, we can build great extensions using the very same code base and across all browsers!

Feel free to [ping me on Twitter](https://twitter.com/davrous) for any feedback.

{{< signature "ms, vf, rb, yk, al, il" >}}

