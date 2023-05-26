---
title: Creating A “Save For Later” Chrome Extension With Modern Web Tools
slug: creating-save-later-chrome-extension-modern-web-tools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8f2f944-9417-4abb-b2df-661ab7334dd9/mark-me-illu-opt.jpg
date: 2014-11-17T23:00:20.000Z
author: daniel-sternlicht
description: >-
  Creating an extension for the Chrome browser is a great way to take a small
  and useful idea and distribute it to millions of people through the Chrome Web
  Store. This article walks you through **the development process of a Chrome
  extension** with modern web tools and libraries.

  It all begins with an idea. Mine was formed while reading an interesting (and
  long) article about new front-end technologies. I was concentrating on reading
  the article when suddenly my wife called me to kick out a poor baby pigeon
  that got stuck on our balcony. When I finally got back to the article, it was
  too late — I had to go to work.
categories:
  - Coding
  - Tools
  - CSS
  - JavaScript
---
Creating an extension for the Chrome browser is a great way to take a small and useful idea and distribute it to millions of people through the Chrome Web Store. This article walks you through the development process of a Chrome extension with modern web tools and libraries.

It all begins with an idea. Mine was formed while reading an interesting (and long) article about new front-end technologies. I was concentrating on reading the article when suddenly my wife called me to kick out a poor baby pigeon that got stuck on our balcony. When I finally got back to the article, it was too late — I had to go to work.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/06/javascript-profiling-chrome-developer-tools/#further-reading-on-smashingmag)

*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [<span class="headline">Creating One Browser Extension For All Browsers</span>](https://www.smashingmagazine.com/2017/04/browser-extension-edge-chrome-firefox-opera-brave-vivaldi/)
*   [<span class="headline">How To Write Fast, Memory-Efficient JavaScript</span>](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
*   [Revisiting Firefox’s DevTools](https://www.smashingmagazine.com/2015/12/revisiting-firefox-devtools/)

To make a long story short, I thought it would be nice to create a Chrome extension that enables you to mark your reading progress in articles so that you can continue reading them later — anywhere.

{{% feature-panel %}}

"<a href="https://markticle.com/">Markticle</a>" is the name I chose for this extension. I’ll share here the technologies that I used to develop it. After reading this article, you’ll have a ready-to-use “Save for Later”-like Chrome extension.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3678671d-1dab-4388-8589-f5e4caba701b/image01-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e783d7-eaac-4ba8-b685-0052691e47b2/image01-preview-opt.jpg" alt="image01-preview-opt" width="500" height="313" /></a></figure>

### Prior Knowledge

We’re going to use a few front-end technologies. While you can learn some of them on the fly, knowledge of others is required (marked in bold):

*   **jQuery**
*   **AngularJS**
*   Node.js
*   Grunt
*   Bower
*   Yeoman

## Scaffolding

Let’s start with some infrastructure work.

Assuming you’re familiar with <a href="https://nodejs.org/">npm</a> (Node.js’ package manager), we’re going to use the Yeoman generator to create a basic extension for Chrome.

<strong>Note</strong>: If you still don’t have Yeoman installed on your machine, start by following the “<a href="https://yeoman.io/learning/index.html">Getting Started</a>” tutorial.

Open a new command line or terminal window, and write the following command:

<pre><code class="language-markup">
npm install -g generator-chrome-extension
</code></pre>

This will install Yeoman’s generator for Chrome extensions on your machine.

Create a new folder in your file system:

<pre><code class="language-markup">
mkdir my-extension
</code></pre>

And then run the following command to generate all of the files that you’ll need to start developing your extension:

<pre><code class="language-markup">
yo chrome-extension
</code></pre>

After running this command, the generator will ask you which features to include in the extension.

In our case, Markticle should do a few things:

1.  Add an icon next to the address bar.
2.  Run on each page that the user opens.
3.  Run some code in the background to connect the current page to the extension in order to save data.

For the first feature, we’ll choose “browser” as a UI action. To enable the extension to run on each web page, we’ll check the “Content scripts” box. Finally, to enable background processes to run, we’ll use a <code>background.js</code> file.

<strong>Note</strong>: Another way to create a Chrome extension is to use the online generator <a href="https://extensionizr.com/">Extensionizr</a>. Extensionizr is a great tool that helps you create basic Chrome extensions. It has multiple configuration options, all of which can be enabled with checkboxes. In the end, you’ll get a ZIP file that includes all of the files you’ll need to start working on the extension. The downside is that you’ll need to configure Grunt and Bower manually.</p>

## Folder Tree

Let’s look at the generated files and folders we’ve got now.

*   `app`
*   `test`
*   `bower.json`
*   `package.json`
*   `Gruntfile.js`

<code>Gruntfile.js</code> is where we’ll configure Grunt tasks for serving, building, testing and packaging our extension.

The <code>package.json</code> and <code>bower.json</code> files are Node.js and Bower JSON files that define our extension’s dependencies on third-party plugins and libraries.

The <code>test</code> folder will include all of the unit and end-to-end tests for the extension. Finally, the <code>app</code> folder is the most interesting because it is where the core of our extension will reside.

After reordering some of the folders and files, here’s what our <code>app</code> folder will look like:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d47858d-c28f-45b4-bb34-89ea1ed8f2dc/image06-preview-opt.jpg" alt="image06-preview-opt" width="424" height="280" /></figure>

*   `icons`
    *   `icon-16.png`
    *   `icon-19.png`
    *   `icon-38.png`
    *   `icon-128.png`
*   `images`
*   `views`
*   `scripts`
    *   `inject.js`
    *   `background.js`
*   `styles`
*   `main.css`
*   `_locales`
    *   `en`
    *   `messages.json`
*   `index.html`
*   `manifest.json`

The most important file here is <code>manifest.json</code>. It is actually the heart of the extension, and it specifies several things, including the following:

*   the location of every file used by the extension,
*   which icon to present as the “action” button,
*   the permissions that your extension needs,
*   the name of the extension.

Here’s an example of what the <code>manifest.json</code> file should look like:

<pre><code class="language-javascript">
{
  "name": "Markticle",
  "version": "1.0.0",
  "manifest_version": 2,
  "icons": {
    "16": "icons/icon-16.png",
    "38": "icons/icon-38.png",
    "128": "icons/icon-128.png"
  },

  "default_locale": "en",
  "background": {
    "scripts": [
      "scripts/helpers/storage.helper.js",
      "scripts/background.js"
    ]
  },

  "browser_action": {
    "default_icon": "icons/icon-19.png",
    "default_popup": "index.html"
  }
}
</code></pre>

## First Flight

We now have a basic extension that does nothing. Still, just to make sure everything is in place and working properly, let’s test the extension in runtime.

Open Chrome and write this in the address bar:

<pre><code class="language-markup">
chrome://extensions
</code></pre>

This page displays information about all of the extensions currently installed in your browser.

In the top-right corner, you’ll see an option to enable “Developer mode.” Click it.

Now, click the “Load unpacked extension” button, browse to the location of the extension you created, select the <code>app</code> folder, and click “Select.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad231f2c-05a3-4bb3-91d7-d02bb3246ad4/image04-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5885185-ea99-4617-9195-c082cca0520f/image04-preview-opt.jpg" alt="image04-preview-opt" width="500" height="181" /></a></figure>

You should now see the extension’s icon next to the address bar.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54e58d53-e7d2-4b07-892e-982a13a146c7/image05-preview-opt.jpg" alt="image05-preview-opt" width="119" height="115" /></figure>

## Installing Dependencies

Before running the app, we need to install some Node.js plugin dependencies. We’ll do so by running the following command:

<pre><code class="language-bash">
npm install
</code></pre>

The last thing we need to do before diving into the code is set up the dependencies of the third-party libraries we’re going to use. We do this in the <code>bower.json</code> file:

<pre><code class="language-javascript">
{
  "name": "Markticle",
  "version": "1.0.0",
    "dependencies": {
      "angular": "1.2.6",
      "jquery": "2.0.3",
      "normalize.scss": "3.0.0"
    },

  "devDependencies": {}
}
</code></pre>

I chose three libraries for this project: AngularJS, jQuery and Normalize.css. To install these, run this command:

<pre><code class="language-bash">
bower install
</code></pre>

## Development

Now that we are ready to start development, let’s split our work into two parts.

The first part will be the popup window that opens when the user clicks the extension’s icon. Markticle’s popup will present the list of bookmarks (i.e. websites) that the user has saved.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc22192-2f7c-41d6-a366-de6178dd39f2/image07-preview-opt.jpg" alt="image07-preview-opt" width="469" height="440" /></figure>

The second part connects the user’s actions to the extension itself. Each time the user takes a particular action on a page, the extension should save the URL and title of the current tab (so that we know what to display in the popup).

The first part is pretty straightforward. We’ll use classic AngularJS code to develop it.

Let’s start by adding the following file structure to the <code>app/scripts</code> folder.

*   `scripts`
    *   `controllers`
        *   `main.controller.js`
    *   `directives`
        *   `main.directive.js`
    *   `helpers`
    *   `storage.helper.js`
    *   `services`
        *   `storage.service.js`
    *   `app.js`
    *   `inject.js`
    *   `background.js`

In the <code>app.js</code> file, we’ll add the following code, which will define our app’s main module:

<pre><code class="language-javascript">
angular.module('markticle', []);
</code></pre>

Now, let’s add some basic code to the <code>index.html</code> file:

<pre><code class="language-markup">
&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;link href="styles/main.css" rel="stylesheet"&gt;
  &lt;/head&gt;
  &lt;body ng-app="markticle"&gt;
    &lt;div id="main_wrapper"&gt;Sample&lt;/div&gt;

    &lt;script src="bower_components/jquery/jquery.min.js"&gt;
    &lt;script src="bower_components/angular/angular.min.js"&gt;

    &lt;script src="scripts/app.js"&gt;
    &lt;script src="scripts/controllers/main.controller.js"&gt;
    &lt;script src="scripts/directives/main.directive.js"&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

What we’ve done here is very simple:

*   define a global AngularJS module named `markticle`,
*   add a single div element with sample text,
*   include the list of script files that we’re going to use.

Now, let’s extend the div element that we created.

<pre><code class="language-markup">
&lt;div id="main_wrapper" ng-controller="MainController"&gt;
  &lt;header&gt;
  &lt;h1&gt;My Marks&lt;/h1&gt;
&lt;/header&gt;
&lt;section id="my_marks"&gt;&lt;/section&gt;
&lt;/div&gt;
</code></pre>

Again, nothing special here — we’ve just set up an AngularJS controller named <code>MainController</code> and added some <code>header</code> and <code>section</code> tags for the upcoming content.

In the <code>app/scripts/controllers/main.controller.js</code> file, let’s create a new AngularJS controller:

<pre><code class="language-javascript">
angular.module('markticle').controller('MainController', function($scope) {
  $scope.marks = [];
});
</code></pre>

This controller currently doesn’t do much except define an array, named <code>marks</code>, that is attached to the controller’s scope. This array will include the user’s saved items.

Just for fun, let’s add two items to this array:

<pre><code class="language-javascript">
$scope.marks = [
{
  title: 'Smashing magazine',
  url: 'https://www.smashingmagazine.com/'
},
{
  title: 'Markticle',
  url: 'https://markticle.com'
}
];
</code></pre>

Now, in the <code>index.html</code> file, let’s loop through them with the <code>ng-repeat</code> directive:

<pre><code class="language-markup">
&lt;section id="my_marks"&gt;
  &lt;ul&gt;
    &lt;li ng-repeat="mark in marks"&gt;
      &lt;a target="_blank" ng-href="{{mark.url}}"&gt;{{mark.title}}
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/section&gt;
</code></pre>

Click the extension’s icon to open the popup and see the result!

After adding some basic CSS to the <code>main.css</code> file, here’s what we’ve come up with:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ef140c-706d-439b-8361-24be2c08b1af/image00-preview-opt.jpg" alt="image00-preview-opt" width="419" height="178" /></figure>

Now for the second part.

In the second part, we’ll connect user interactions to our extension.

Let’s start by adding a new property to our <code>manifest.js</code> file:

<pre><code class="language-javascript">
{
  …
  "background": {…},
  "content_scripts": [
{
  "matches": ["https://*/*", "https://*/*"],
  "js": ["bower_components/jquery/jquery.min.js", "scripts/inject.js"]
}
],
…
}
</code></pre>

Here, we’ve added a property named <code>content_scripts</code>, which has its own two properties:

*   `matches` This is an array that defines in which websites to inject the script — in our case, all websites.
*   `js` This is an array of scripts that will be injected into each web page by the extension.

Let’s open the <code>inject.js</code> script and add some basic code to it:

<pre><code class="language-javascript">
$(document).ready(function() {
  var createMarkticleButton = function() {
  var styles = 'position: fixed; z-index: 9999; bottom: 20px; left: 20px;';
$('body').append('<button id="markticle_button">Mark me!</button>');
};
$(document).on('click', '#markticle_button', function() {
    var title = document.title;
    var url = window.location.href;
console.log(title + ': ' + url);
});
createMarkticleButton();
});
</code></pre>

This script does two things once the page is ready. First, it adds a basic button using the <code>createMarkticleButton()</code> method. Then, it adds an event listener that writes the URL and title of the current page to Chrome’s console every time the user clicks the button.

To test this, go to <code>chrome://extensions</code>, find your extension, and click the “Reload” button. Then, open any website, click the Markticle button, and look at the console in Chrome Developer Tools.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd25e302-985e-4507-971f-36b904bcb5f3/image03-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb810a89-743f-4d82-bdb7-e301254b5690/image03-preview-opt.jpg" alt="image03-preview-opt" width="500" height="263" /></a></figure>

## Storing Data

To store data in the extension (without having to use a server-side solution), we have several options. My favorite is <a href="https://www.w3schools.com/html/html5_webstorage.asp">HTML5 localStorage</a>.

Let’s go back to our <code>scripts</code> folder and create a localStorage service. First, edit <code>app/scripts/helpers/storage.helper.js</code>:

<pre><code class="language-markup">
var markticleStorageService = function() {
  var lsName = 'marks';
  var data = localStorage.getItem(lsName) ? JSON.parse(localStorage.getItem(lsName)) : [];

  return {

    get: function() {
      return data;
    },
    add: function(item) {
      this.remove(item.url);
      data.push(item);
      this.save();
    },
    remove: function(url) {
      var idx = null;
      for(var i = 0; i &lt; data.length; i++) {
        if(data[i].url === url) {
          idx = i;
          break;
        }
        }
      if(idx !== null) {
      data.splice(idx, 1);
      this.save();
      }
    },
    save: function() {
      localStorage.setItem(lsName, JSON.stringify(data));
    }
  };
};
</code></pre>

With this, we’re first holding a <code>data</code> array with the current data that we’re pulling from localStorage. Then, we’re revealing a few methods to manipulate the data, such as <code>get()</code>, <code>add()</code> and <code>remove()</code>.

After creating this class, let’s also add it as an AngularJS service in <code>app/scripts/services/storage.service.js</code>:

<pre><code class="language-markup">
angular.module('markticle').service('StorageService', markticleStorageService);
</code></pre>

<strong>Note</strong>: Don’t forget to refer to both scripts in <code>index.html</code>.

The reason we’ve split it into two scripts is because we’re going to reuse the <code>markticleStorageService</code> class in <code>background.js</code>, where we won’t access AngularJS.

Returning to our <code>MainController</code>, let’s make sure we’re injecting the storage service in the app:

<pre><code class="language-markup">
angular.module('markticle').controller('MainController', function($scope, StorageService) {
  $scope.marks = […];
});
</code></pre>

Finally, let’s connect the <code>StorageService</code> data to our app and introduce a method that will be used in the UI.

<pre><code class="language-markup">
angular.module('markticle').controller('MainController', function($scope, StorageService) {
  $scope.marks = StorageService.get();
  $scope.removeMark = function(url) {
    StorageService.remove(url);
    $scope.marks = StorageService.get();
    if(!$scope.$$phase) {
      $scope.$apply();
    }
  };
});
</code></pre>

Back to the <code>index.html</code> file. Let’s add an option to remove items by connecting the view to the controller’s <code>remove()</code> method:

<pre><code class="language-markup">
&lt;li ng-repeat="mark in marks"&gt;
  &lt;a ng-href="{{mark.url}}"&gt;{{mark.title}}&lt;/a&gt;
  &lt;span class="remove" ng-click="removeMark(mark.url)"&gt;remove&lt;/span&gt;
&lt;/li&gt;
</code></pre>

So, each time the user clicks the “Remove” button, it will call the <code>remove()</code> method from the controller, with the page’s URL as a parameter. Then, the controller will go to <code>StorageService</code> and remove the item from the data array and save the new data array to the localStrorage property.</p>

## Background Process

Our extension now knows how to get and remove data from the localStorage service. It’s time to enable the user to add and save items.

Open <code>app/scripts/background.js</code>, and add the following code:

<pre><code class="language-markup">
chrome.extension.onMessage.addListener(function(request, sender, sendResponse) {
  if(request) {
    var storageService = new markticleStorageService();
    if(request.action === 'add') {
      storageService.add(request.data);
    }
  }
});
</code>
</pre>

Here, we’re adding a listener for the <code>onMessage</code> event. In the callback function, we’re creating a new instance for <code>markticleStorageService</code> and getting a <code>request</code> object. This object is what we’re going to send with the <code>chrome.extension.sendMessage</code> event that is triggered from the <code>inject.js</code> script. It contains two properties:

*   `action` This is the type of action that we want the background process to perform.
*   `data` This is the object of the data that we want to add.

In our case, the type of action is <code>add</code>, and the object is a model of a single item. For example:

<pre><code class="language-markup">
{
title: 'Markticle',
url: 'https://markticle.com'
}
</code></pre>

Let’s go back to the <code>inject.js</code> script and connect it to the <code>background.js</code> script:

<pre><code class="language-markup">
$(document).on('click', '#markticle_button', function() {
  var title = document.title;
  var url = window.location.href;
chrome.extension.sendMessage({
    action : 'add',
    data: {
  title: title,
  url: url
}
});
alert('Marked!');
});
</code></pre>

Now, go to any website and click the “Mark me!” button. Open the popup again and see the new item you’ve just added. Pretty cool, right?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7771cd5c-188d-4162-8344-032ab9e608a5/image02-preview-opt.jpg" alt="image02-preview-opt" width="414" height="210" /></figure>

## Build

<pre><code class="language-javascript">
angular.module('markticle').controller('MainController', function($scope) {
  $scope.marks = [];
});
</code></pre>

This controller currently doesn’t do much except define an array, named <code>marks</code>, that is attached to the controller’s scope. This array will include the user’s saved items.

Just for fun, let’s add two items to this array:

<pre><code class="language-javascript">
$scope.marks = [
{
  title: 'Smashing magazine',
  url: 'https://www.smashingmagazine.com/'
},
{
  title: 'Markticle',
  url: 'https://markticle.com'
}
];
</code></pre>

Now, in the <code>index.html</code> file, let’s loop through them with the <code>ng-repeat</code> directive:

<pre><code class="language-markup">
&lt;section id="my_marks"&gt;
  &lt;ul&gt;
    &lt;li ng-repeat="mark in marks"&gt;
      &lt;a target="_blank" ng-href="{{mark.url}}"&gt;{{mark.title}}
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/section&gt;
</code></pre>

Click the extension’s icon to open the popup and see the result!

After adding some basic CSS to the <code>main.css</code> file, here’s what we’ve come up with:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ef140c-706d-439b-8361-24be2c08b1af/image00-preview-opt.jpg" alt="image00-preview-opt" width="419" height="178" /></figure>

Now for the second part.

In the second part, we’ll connect user interactions to our extension.

Let’s start by adding a new property to our <code>manifest.js</code> file:

<pre><code class="language-javascript">
{
  …
  "background": {…},
  "content_scripts": [
{
  "matches": ["https://*/*", "https://*/*"],
  "js": ["bower_components/jquery/jquery.min.js", "scripts/inject.js"]
}
],
…
}
</code></pre>

Here, we’ve added a property named <code>content_scripts</code>, which has its own two properties:

*   `matches` This is an array that defines in which websites to inject the script — in our case, all websites.
*   `js` This is an array of scripts that will be injected into each web page by the extension.

Let’s open the <code>inject.js</code> script and add some basic code to it:

<pre><code class="language-javascript">
$(document).ready(function() {
  var createMarkticleButton = function() {
  var styles = 'position: fixed; z-index: 9999; bottom: 20px; left: 20px;';
$('body').append('<button id="markticle_button">Mark me!</button>');
};
$(document).on('click', '#markticle_button', function() {
    var title = document.title;
    var url = window.location.href;
console.log(title + ': ' + url);
});
createMarkticleButton();
});
</code></pre>

This script does two things once the page is ready. First, it adds a basic button using the <code>createMarkticleButton()</code> method. Then, it adds an event listener that writes the URL and title of the current page to Chrome’s console every time the user clicks the button.

To test this, go to <code>chrome://extensions</code>, find your extension, and click the “Reload” button. Then, open any website, click the Markticle button, and look at the console in Chrome Developer Tools.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd25e302-985e-4507-971f-36b904bcb5f3/image03-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb810a89-743f-4d82-bdb7-e301254b5690/image03-preview-opt.jpg" alt="image03-preview-opt" width="500" height="263" /></a></figure>

## Storing Data

To store data in the extension (without having to use a server-side solution), we have several options. My favorite is <a href="https://www.w3schools.com/html/html5_webstorage.asp">HTML5 localStorage</a>.

Let’s go back to our <code>scripts</code> folder and create a localStorage service. First, edit <code>app/scripts/helpers/storage.helper.js</code>:

<pre><code class="language-markup">
var markticleStorageService = function() {
  var lsName = 'marks';
  var data = localStorage.getItem(lsName) ? JSON.parse(localStorage.getItem(lsName)) : [];

  return {

    get: function() {
      return data;
    },
    add: function(item) {
      this.remove(item.url);
      data.push(item);
      this.save();
    },
    remove: function(url) {
      var idx = null;
      for(var i = 0; i &lt; data.length; i++) {
        if(data[i].url === url) {
          idx = i;
          break;
        }
        }
      if(idx !== null) {
      data.splice(idx, 1);
      this.save();
      }
    },
    save: function() {
      localStorage.setItem(lsName, JSON.stringify(data));
    }
  };
};
</code></pre>

With this, we’re first holding a <code>data</code> array with the current data that we’re pulling from localStorage. Then, we’re revealing a few methods to manipulate the data, such as <code>get()</code>, <code>add()</code> and <code>remove()</code>.

After creating this class, let’s also add it as an AngularJS service in <code>app/scripts/services/storage.service.js</code>:

<pre><code class="language-markup">
angular.module('markticle').service('StorageService', markticleStorageService);
</code></pre>

<strong>Note</strong>: Don’t forget to refer to both scripts in <code>index.html</code>.

The reason we’ve split it into two scripts is because we’re going to reuse the <code>markticleStorageService</code> class in <code>background.js</code>, where we won’t access AngularJS.

Returning to our <code>MainController</code>, let’s make sure we’re injecting the storage service in the app:

<pre><code class="language-markup">
angular.module('markticle').controller('MainController', function($scope, StorageService) {
  $scope.marks = […];
});
</code></pre>

Finally, let’s connect the <code>StorageService</code> data to our app and introduce a method that will be used in the UI.

<pre><code class="language-markup">
angular.module('markticle').controller('MainController', function($scope, StorageService) {
  $scope.marks = StorageService.get();
  $scope.removeMark = function(url) {
    StorageService.remove(url);
    $scope.marks = StorageService.get();
    if(!$scope.$$phase) {
      $scope.$apply();
    }
  };
});
</code></pre>

Back to the <code>index.html</code> file. Let’s add an option to remove items by connecting the view to the controller’s <code>remove()</code> method:

<pre><code class="language-markup">
&lt;li ng-repeat="mark in marks"&gt;
  &lt;a ng-href="{{mark.url}}"&gt;{{mark.title}}&lt;/a&gt;
  &lt;span class="remove" ng-click="removeMark(mark.url)"&gt;remove&lt;/span&gt;
&lt;/li&gt;
</code></pre>

So, each time the user clicks the “Remove” button, it will call the <code>remove()</code> method from the controller, with the page’s URL as a parameter. Then, the controller will go to <code>StorageService</code> and remove the item from the data array and save the new data array to the localStrorage property.</p>

## Background Process

Our extension now knows how to get and remove data from the localStorage service. It’s time to enable the user to add and save items.

Open <code>app/scripts/background.js</code>, and add the following code:

<pre><code class="language-markup">
chrome.extension.onMessage.addListener(function(request, sender, sendResponse) {
  if(request) {
    var storageService = new markticleStorageService();
    if(request.action === 'add') {
      storageService.add(request.data);
    }
  }
});
</code>
</pre>

Here, we’re adding a listener for the <code>onMessage</code> event. In the callback function, we’re creating a new instance for <code>markticleStorageService</code> and getting a <code>request</code> object. This object is what we’re going to send with the <code>chrome.extension.sendMessage</code> event that is triggered from the <code>inject.js</code> script. It contains two properties:

*   `action` This is the type of action that we want the background process to perform.
*   `data` This is the object of the data that we want to add.

In our case, the type of action is <code>add</code>, and the object is a model of a single item. For example:

<pre><code class="language-markup">
{
title: 'Markticle',
url: 'https://markticle.com'
}
</code></pre>

Let’s go back to the <code>inject.js</code> script and connect it to the <code>background.js</code> script:

<pre><code class="language-markup">
$(document).on('click', '#markticle_button', function() {
  var title = document.title;
  var url = window.location.href;
chrome.extension.sendMessage({
    action : 'add',
    data: {
  title: title,
  url: url
}
});
alert('Marked!');
});
</code></pre>

Now, go to any website and click the “Mark me!” button. Open the popup again and see the new item you’ve just added. Pretty cool, right?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7771cd5c-188d-4162-8344-032ab9e608a5/image02-preview-opt.jpg" alt="image02-preview-opt" width="414" height="210" /></figure>

## Build

We’ve created a cool “Save for Later” Chrome extension of sorts. Before releasing it to the Chrome store, let’s talk about the build process for a Chrome extension.

A build process for this kind of app could have a few goals (or “tasks,” to use Grunt’s naming convention):

*   test (if you’re writing unit tests for the extension),
*   minify,
*   concatenate,
*   increment the version number in the manifest file,
*   compress into a ZIP file.

If you’re using Yeoman’s generator, you can perform all of these tasks automatically by running this command:

<pre><code class="language-markup">
grunt build
</code></pre>

This will create a new <code>dist</code> folder, where you will find the minified and concatenated files, and another folder named <code>package</code>, where you’ll find a ZIP file named with the current version of your extension, ready to be deployed.</p>

## Deploy

All that’s left to do is deploy the extension.

Go to your “<a href="https://chrome.google.com/webstore/developer/dashboard">Developer Dashboard</a>” in the Chrome Web Store, and click the “Add new item” button.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c607a3f-063c-4575-a3c6-c8e13adf132a/image08-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37bb287c-e6d2-4804-b792-41755a54b3dc/image08-preview-opt.jpg" alt="image08-preview-opt" width="500" height="212" /></a></figure>

Browse to the ZIP file we created and upload it. Fill in all of the required information, and then click the “Publish changes” button.

<strong>Note</strong>: If you want to update the extension, instead of creating a new item, click the “Edit” button next to the extension. Then, click the “Upload updated package” button and repeat the remaining steps.</p>

## Conclusion

As you can see, developing a Chrome extension has never been easier!

If you use Node.js and Grunt for their time-saving features, AngularJS as a development framework and the Chrome Web Store for distribution, all you need is a good idea.

I hope you’ve enjoyed reading this article. If it was too long to read in one sitting, consider using <a href="https://markticle.com/">Markticle</a>.

{{< signature "il, al" >}}

