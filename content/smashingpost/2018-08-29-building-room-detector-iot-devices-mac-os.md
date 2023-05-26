---
title: 'Building A Room Detector For IoT Devices On Mac OS'
slug: building-room-detector-iot-devices-mac-os
author: alvin-wan
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b15151-2a24-4464-8540-64143f60d355/5-building-room-detector-iot-devices.png
date: 2018-08-29T14:20:53+02:00
summary: >-
  In this tutorial, you build a desktop app that predicts which room you’re in using a simple machine learning algorithm: least squares. The code applies to any platform, but we only provide dependency installation instructions for Mac OSX.
description: >-
  In this tutorial, you build a desktop app that predicts which room you’re in using a simple machine learning algorithm: least squares. The code applies to any platform, but we only provide dependency installation instructions for Mac OSX.
categories:
  - Node.js
  - JavaScript
  - Apps
  - Machine Learning
---
Knowing which room you’re in enables various IoT applications &mdash; from turning on the light to changing TV channels. So, how can we detect the moment you and your phone are in the kitchen, or bedroom, or living room? With today’s commodity hardware, there are a myriad of possibilities:

One solution is to **equip each room with a bluetooth device**. Once your phone is within range of a bluetooth device, your phone will know which room it is, based on the bluetooth device. However, maintaining an array of Bluetooth devices is significant overhead &mdash; from replacing batteries to replacing dysfunctional devices. Additionally, proximity to the Bluetooth device is not always the answer: if you’re in the living room, by the wall shared with the kitchen, your kitchen appliances should not start churning out food.

Another, albeit impractical, solution is to **use GPS**. However, keep in mind hat GPS works poorly indoors in which the multitude of walls, other signals, and other obstacles wreak havoc on GPS’s precision.

Our approach instead is to **leverage all in-range WiFi networks** &mdash; even the ones your phone is not connected to. Here is how: consider the strength of WiFi A in the kitchen; say it is 5. Since there is a wall between the kitchen and the bedroom, we can reasonably expect the strength of WiFi A in the bedroom to differ; say it is 2. We can exploit this difference to predict which room we’re in. What’s more: WiFi network B from our neighbor can only be detected from the living room but is effectively invisible from the kitchen. That makes prediction even easier. In sum, the list of all in-range WiFi gives us plentiful information.

This method has the distinct advantages of:

1. not requiring more hardware;
2. relying on more stable signals like WiFi;
3. working well where other techniques such as GPS are weak.

The more walls the better, as the more disparate the WiFi network strengths, the easier the rooms are to classify. You will build a simple desktop app that collects data, learns from the data, and predicts which room you’re in at any given time.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'The Rise Of Intelligent Conversational UI'" href="https://www.smashingmagazine.com/2018/04/rise-intelligent-conversational-ui/" rel="bookmark">The Rise Of Intelligent Conversational UI</a></li>
<li><a title="Read 'Applications Of Machine Learning For Designers'" href="https://www.smashingmagazine.com/2017/04/applications-machine-learning-designers/" rel="bookmark">Applications Of Machine Learning For Designers</a></li>
<li><a title="Read 'How To Prototype IoT Experiences: Building The Hardware'" href="https://www.smashingmagazine.com/2017/04/prototype-iot-experiences-building-hardware-part-1/" rel="bookmark">How To Prototype IoT Experiences: Building The Hardware</a></li>
<li><a title="Read 'Designing For The Internet Of Emotional Things'" href="https://www.smashingmagazine.com/2016/04/designing-for-the-internet-of-emotional-things/" rel="bookmark">Designing For The Internet Of Emotional Things</a></li>
</ul>

## Prerequisites

For this tutorial, you will need a Mac OSX. Whereas the code can apply to any platform, we will only provide dependency installation instructions for Mac.

- Mac OSX
- Homebrew, a package manager for Mac OSX. To install, copy-and-paste the command at [brew.sh](https://brew.sh)
- Installation of NodeJS 10.8.0+ and npm
- Installation of Python 3.6+ and pip. See the first 3 sections of ["How To Install virtualenv, Installing With pip, and Managing Packages"](https://www.digitalocean.com/community/tutorials/common-python-tools-using-virtualenv-installing-with-pip-and-managing-packages#python-and-packages)

{{% feature-panel %}}

## Step 0: Setup Work Environment

Your desktop app will be written in NodeJS. However, to leverage more efficient computational libraries like `numpy`, the training and prediction code will be written in Python. To start, we will setup your environments and install dependencies. Create a new directory to house your project.

<pre><code class="language-bash">mkdir ~/riot
</code></pre>

Navigate into the directory.

<pre><code class="language-bash">cd ~/riot
</code></pre>

Use pip to install Python’s default virtual environment manager.

<pre><code class="language-bash">sudo pip install virtualenv
</code></pre>

Create a Python3.6 virtual environment named `riot`.

<pre><code class="language-bash">virtualenv riot --python=python3.6
</code></pre>

Activate the virtual environment.

<pre><code class="language-bash">source riot/bin/activate
</code></pre>

Your prompt is now preceded by `(riot)`. This indicates we have successfully entered the virtual environment. Install the following packages using `pip`:

- `numpy`: An efficient, linear algebra library
- `scipy`: A scientific computing library that implements popular machine learning models

<pre><code class="language-bash">pip install numpy==1.14.3 scipy
==1.1.0
</code></pre>

With the working directory setup, we will start with a desktop app that records all WiFi networks in-range. These recordings will constitute training data for your machine learning model. Once we have data on hand, you will write a least squares classifier, trained on the WiFi signals collected earlier. Finally, we will use the least squares model to predict the room you’re in, based on the WiFi networks in range.

## Step 1: Initial Desktop Application

In this step, we will create a new desktop application using Electron JS. To begin, we will instead the Node package manager `npm` and a download utility `wget`.

<pre><code class="language-bash">brew install npm wget
</code></pre>

To begin, we will create a new Node project.

<pre><code class="language-bash">npm init
</code></pre>

This prompts you for the package name and then the version number. Hit `ENTER` to accept the default name of `riot` and default version of `1.0.0`.

<pre><code class="language-bash">package name: (riot)
version: (1.0.0)
</code></pre>

This prompts you for a project description. Add any non-empty description you would like. Below, the description is `room detector`

<pre><code class="language-bash">description: room detector
</code></pre>

This prompts you for the entry point, or the main file to run the project from. Enter `app.js`.

<pre><code class="language-bash">entry point: (index.js) app.js
</code></pre>

This prompts you for the `test command` and `git repository`. Hit `ENTER` to skip these fields for now.

<pre><code class="language-bash">test command:
git repository:
</code></pre>

This prompts you for `keywords` and `author`. Fill in any values you would like. Below, we use `iot`, `wifi` for keywords and use `John Doe` for the author.

<pre><code class="language-bash">keywords: iot,wifi
author: John Doe
</code></pre>

This prompts you for the license. Hit `ENTER` to accept the default value of `ISC`.

<pre><code class="language-bash">license: (ISC)
</code></pre>

At this point, `npm` will prompt you with a summary of information so far. Your output should be similar to the following.

<pre><code class="language-json">{
  "name": "riot",
  "version": "1.0.0",
  "description": "room detector",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "iot",
    "wifi"
  ],
  "author": "John Doe",
  "license": "ISC"
}
</code></pre>

Hit `ENTER` to accept. `npm` then produces a `package.json`. List all files to double-check.

<pre><code class="language-bash">ls
</code></pre>

This will output the only file in this directory, along with the virtual environment folder.

<pre><code class="language-bash">package.json
riot
</code></pre>

Install NodeJS dependencies for our project.

<div class="break-out">

<pre><code class="language-bash">npm install electron --global  # makes electron binary accessible globally
npm install node-wifi --save
</code></pre></div>

Start with [`main.js` from Electron Quick Start](https://github.com/electron/electron-quick-start/blob/master/main.js), by downloading the file, using the below. The following `-O` argument renames `main.js` to `app.js`.

<div class="break-out">

<pre><code class="language-bash">wget https://raw.githubusercontent.com/electron/electron-quick-start/master/main.js -O app.js
</code></pre></div>

Open `app.js` in `nano` or your favorite text editor.

<pre><code class="language-bash">nano app.js
</code></pre>

On line 12, change *index.html* to *static/index.html*, as we will create a directory `static` to contain all HTML templates.

<pre><code class="language-bash">function createWindow () {
  // Create the browser window.
  win = new BrowserWindow({width: 1200, height: 800})

  // and load the index.html of the app.
  win.loadFile('static/index.html')

  // Open the DevTools.
</code></pre>

Save your changes and exit the editor. Your file should match the [source code](https://github.com/alvinwan/riot/blob/master/app.js) of the `app.js` file. Now create a new directory to house our HTML templates.

<pre><code class="language-bash">mkdir static
</code></pre>

Download a stylesheet created for this project.

<div class="break-out">

<pre><code class="language-bash">wget https://raw.githubusercontent.com/alvinwan/riot/master/static/style.css?token=AB-ObfDtD46ANlqrObDanckTQJ2Q1Pyuks5bf79PwA%3D%3D -O static/style.css
</code></pre></div>

Open `static/index.html` in `nano` or your favorite text editor. Start with the standard HTML structure.

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
  &lt;html&gt;
    &lt;head&gt;
      &lt;meta charset="UTF-8"&gt;
      &lt;title&gt;Riot | Room Detector&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
      &lt;main&gt;
      &lt;/main&gt;
    &lt;/body&gt;
  &lt;/html&gt;
</code></pre>

Right after the title, link the Montserrat font linked by Google Fonts and stylesheet.

<div class="break-out">

<pre><code class="language-html">&lt;title&gt;Riot &#124; Room Detector&lt;/title&gt;
  &lt;!-- start new code --&gt;
  &lt;link href="https://fonts.googleapis.com/css?family=Montserrat:400,700" rel="stylesheet"&gt;
  &lt;link href="style.css" rel="stylesheet"&gt;
  &lt;!-- end new code --&gt;
&lt;/head&gt;
</code></pre></div>

Between the `main` tags, add a slot for the predicted room name.

<pre><code class="language-html">&lt;main&gt;
  &lt;!-- start new code --&gt;
  &lt;p class="text"&gt;I believe you’re in the&lt;/p&gt;
  &lt;h1 class="title" id="predicted-room-name"&gt;(I dunno)&lt;/h1&gt;
  &lt;!-- end new code --&gt;
&lt;/main&gt;
</code></pre>

Your script should now match the following exactly. Exit the editor.

<div class="break-out">

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
  &lt;html&gt;
    &lt;head&gt;
      &lt;meta charset="UTF-8"&gt;
      &lt;title&gt;Riot | Room Detector&lt;/title&gt;
      &lt;link href="https://fonts.googleapis.com/css?family=Montserrat:400,700" rel="stylesheet"&gt;
      &lt;link href="style.css" rel="stylesheet"&gt;
    &lt;/head&gt;
    &lt;body&gt;
      &lt;main&gt;
        &lt;p class="text"&gt;I believe you’re in the&lt;/p&gt;
        &lt;h1 class="title" id="predicted-room-name"&gt;(I dunno)&lt;/h1&gt;
      &lt;/main&gt;
    &lt;/body&gt;
  &lt;/html&gt;
</code></pre></div>

Now, amend the package file to contain a start command.

<pre><code class="language-bash">nano package.json
</code></pre>

Right after line 7, add a `start` command that’s aliased to `electron .`. Make sure to add a comma to the end of the previous line.

<pre><code class="language-bash">"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "start": "electron ."
},
</code></pre>

Save and exit. You are now ready to launch your desktop app in Electron JS. Use `npm` to launch your application.

<pre><code class="language-bash">npm start
</code></pre>

Your desktop application should match the following.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a91cdb8b-81d9-4e49-9abb-f05c8a9112bf/1-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a91cdb8b-81d9-4e49-9abb-f05c8a9112bf/1-building-room-detector-iot-devices.png" sizes="100vw" caption="Home page with “Add New Room” button available (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a91cdb8b-81d9-4e49-9abb-f05c8a9112bf/1-building-room-detector-iot-devices.png'>Large preview</a>)" alt="home page with button" >}}

This completes your starting desktop app. To exit, navigate back to your terminal and CTRL+C. In the next step, we will record wifi networks, and make the recording utility accessible through the desktop application UI.

## Step 2: Record WiFi Networks

In this step, you will write a NodeJS script that records the strength and frequency of all in-range wifi networks. Create a directory for your scripts.

<pre><code class="language-javascript">mkdir scripts
</code></pre>

Open `scripts/observe.js` in `nano` or your favorite text editor.

<pre><code class="language-javascript">nano scripts/observe.js
</code></pre>

Import a NodeJS wifi utility and the filesystem object.

<pre><code class="language-javascript">var wifi = require('node-wifi');
var fs = require('fs');
</code></pre>

Define a `record` function that accepts a completion handler.

<pre><code class="language-javascript">/**
 * Uses a recursive function for repeated scans, since scans are asynchronous.
 */
function record(n, completion, hook) {
}
</code></pre>

Inside the new function, initialize the wifi utility. Set `iface` to null to initialize to a random wifi interface, as this value is currently irrelevant.

<pre><code class="language-javascript">function record(n, completion, hook) {
    wifi.init({
        iface : null
    });
}
</code></pre>

Define an array to contain your samples. *Samples* are training data we will use for our model. The samples in this particular tutorial are lists of in-range wifi networks and their associated strengths, frequencies, names etc.

<pre><code class="language-javascript">function record(n, completion, hook) {
    ...
    samples = []
}
</code></pre>

Define a recursive function `startScan`, which will asynchronously initiate wifi scans. Upon completion, the asynchronous wifi scan will then recursively invoke `startScan`.

<pre><code class="language-javascript">function record(n, completion, hook) {
  ...
  function startScan(i) {
    wifi.scan(function(err, networks) {
    });
  }
  startScan(n);
}
</code></pre>

In the `wifi.scan` callback, check for errors or empty lists of networks and restart the scan if so.

<pre><code class="language-javascript">wifi.scan(function(err, networks) {
  if (err || networks.length == 0) {
    startScan(i);
    return
  }
});
</code></pre>

Add the recursive function’s base case, which invokes the completion handler.

<div class="break-out">

<pre><code class="language-javascript">wifi.scan(function(err, networks) {
  ...
  if (i <= 0) {
    return completion({samples: samples});
  }
});
</code></pre></div>

Output a progress update, append to the list of samples, and make the recursive call.

<pre><code class="language-javascript">wifi.scan(function(err, networks) {
  ...
  hook(n-i+1, networks);
  samples.push(networks);
  startScan(i-1);
});
</code></pre>

At the end of your file, invoke the `record` function with a callback that saves samples to a file on disk.

<div class="break-out">

<pre><code class="language-javascript">function record(completion) {
  ...
}

function cli() {
  record(1, function(data) {
    fs.writeFile('samples.json', JSON.stringify(data), 'utf8', function() {});
  }, function(i, networks) {
    console.log(" * [INFO] Collected sample " + (21-i) + " with " + networks.length + " networks");
  })
}

cli();
</code></pre></div>

Double check that your file matches the following:

<div class="break-out">

<pre><code class="language-javascript">var wifi = require('node-wifi');
var fs = require('fs');

/**
 * Uses a recursive function for repeated scans, since scans are asynchronous.
 */
function record(n, completion, hook) {
  wifi.init({
      iface : null // network interface, choose a random wifi interface if set to null
  });

  samples = []
  function startScan(i) {
    wifi.scan(function(err, networks) {
        if (err || networks.length == 0) {
          startScan(i);
          return
        }
        if (i <= 0) {
          return completion({samples: samples});
        }
        hook(n-i+1, networks);
        samples.push(networks);
        startScan(i-1);
    });
  }

  startScan(n);
}

function cli() {
    record(1, function(data) {
        fs.writeFile('samples.json', JSON.stringify(data), 'utf8', function() {});
    }, function(i, networks) {
        console.log(" * [INFO] Collected sample " + i + " with " + networks.length + " networks");
    })
}

cli();
</code></pre></div>

Save and exit. Run the script.

<pre><code class="language-javascript">node scripts/observe.js
</code></pre>

Your output will match the following, with variable numbers of networks.

<pre><code class="language-javascript"> * [INFO] Collected sample 1 with 39 networks
</code></pre>

Examine the samples that were just collected. Pipe to `json_pp` to pretty print the JSON and pipe to head to view the first 16 lines.

<pre><code class="language-javascript">cat samples.json &#124; json_pp &#124; head -16
</code></pre>

The below is example output for a 2.4 GHz network.

<pre><code class="language-javascript">{
  "samples": [
    [
      {
        "mac": "64:0f:28:79:9a:29",
        "bssid": "64:0f:28:79:9a:29",
        "ssid": "SMASHINGMAGAZINEROCKS",
         "channel": 4,
         "frequency": 2427,
          "signal_level": "-91",
          "security": "WPA WPA2",
          "security_flags": [
           "(PSK/AES,TKIP/TKIP)",
          "(PSK/AES,TKIP/TKIP)"
        ]
      },
</code></pre>

This concludes your NodeJS wifi-scanning script. This allows us to view all in-range WiFi networks. In the next step, you will make this script accessible from the desktop app.

{{% ad-panel-leaderboard %}}

## Step 3: Connect Scan Script To Desktop App

In this step, you will first add a button to the desktop app to trigger the script with. Then, you will update the desktop app UI with the script’s progress.

Open `static/index.html`.

<pre><code class="language-html">nano static/index.html
</code></pre>

Insert the "Add" button, as shown below.

<div class="break-out">

<pre><code class="language-html">&lt;h1 class="title" id="predicted-room-name"&gt;(I dunno)&lt;/h1&gt;
        &lt;!-- start new code --&gt;
        &lt;div class="buttons"&gt;
            &lt;a href="add.html" class="button"&gt;Add new room&lt;/a&gt;
        &lt;/div&gt;
        &lt;!-- end new code --&gt;
    &lt;/main&gt;
</code></pre></div>

Save and exit. Open `static/add.html`.

<pre><code class="language-html">nano static/add.html
</code></pre>

Paste the following content.

<div class="break-out">

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
  &lt;html&gt;
    &lt;head&gt;
      &lt;meta charset="UTF-8"&gt;
      &lt;title&gt;Riot | Add New Room&lt;/title&gt;
      &lt;link href="https://fonts.googleapis.com/css?family=Montserrat:400,700" rel="stylesheet"&gt;
      &lt;link href="style.css" rel="stylesheet"&gt;
    &lt;/head&gt;
    &lt;body&gt;
      &lt;main&gt;
        &lt;h1 class="title" id="add-title"&gt;0&lt;/h1&gt;
        &lt;p class="subtitle"&gt;of &lt;span&gt;20&lt;/span&gt; samples needed. Feel free to move around the room.&lt;/p&gt;
        &lt;input type="text" id="add-room-name" class="text-field" placeholder="(room name)"&gt;
        &lt;div class="buttons"&gt;
          &lt;a href="#" id="start-recording" class="button"&gt;Start recording&lt;/a&gt;
          &lt;a href="index.html" class="button light"&gt;Cancel&lt;/a&gt;
        &lt;/div&gt;
        &lt;p class="text" id="add-status" style="display:none"&gt;&lt;/p&gt;
      &lt;/main&gt;
      &lt;script&gt;
        require('../scripts/observe.js')
      &lt;/script&gt;
    &lt;/body&gt;
  &lt;/html&gt;
</code></pre></div>

Save and exit. Reopen `scripts/observe.js`.

<pre><code class="language-javascript">nano scripts/observe.js
</code></pre>

Beneath the `cli` function, define a new `ui` function.

<pre><code class="language-javascript">function cli() {
    ...
}

// start new code
function ui() {
}
// end new code

cli();
</code></pre>

Update the desktop app status to indicate the function has started running.

<div class="break-out">

<pre><code class="language-javascript">function ui() {
  var room_name = document.querySelector('#add-room-name').value;
  var status = document.querySelector('#add-status');
  var number = document.querySelector('#add-title');
  status.style.display = "block"
  status.innerHTML = "Listening for wifi..."
}
</code></pre></div>

Partition the data into training and validation data sets.

<pre><code class="language-javascript">function ui() {
  ...
  function completion(data) {
    train_data = {samples: data['samples'].slice(0, 15)}
    test_data = {samples: data['samples'].slice(15)}
    var train_json = JSON.stringify(train_data);
    var test_json = JSON.stringify(test_data);
  }
}
</code></pre>

Still within the `completion` callback, write both datasets to disk.

<div class="break-out">

<pre><code class="language-javascript">function ui() {
  ...
  function completion(data) {
    ...
    fs.writeFile('data/' + room_name + '_train.json', train_json, 'utf8', function() {});
    fs.writeFile('data/' + room_name + '_test.json', test_json, 'utf8', function() {});
    console.log(" * [INFO] Done")
    status.innerHTML = "Done."
  }
}
</code></pre></div>

Invoke `record` with the appropriate callbacks to record 20 samples and save the samples to disk.

<div class="break-out">

<pre><code class="language-javascript">function ui() {
  ...
  function completion(data) {
    ...
  }
  record(20, completion, function(i, networks) {
    number.innerHTML = i
    console.log(" * [INFO] Collected sample " + i + " with " + networks.length + " networks")
  })
}
</code></pre></div>

Finally, invoke the `cli` and `ui` functions where appropriate. Start by deleting the `cli();` call at the bottom of the file.

<pre><code class="language-javascript">function ui() {
    ...
}

cli();  // remove me
</code></pre>

Check if the document object is globally accessible. If not, the script is being run from the command line. In this case, invoke the `cli` function. If it is, the script is loaded from within the desktop app. In this case, bind the click listener to the `ui` function.

<pre><code class="language-javascript">if (typeof document == 'undefined') {
    cli();
} else {
    document.querySelector('#start-recording').addEventListener('click', ui)
}
</code></pre>

Save and exit. Create a directory to hold our data.

<pre><code class="language-bash">mkdir data
</code></pre>

Launch the desktop app.

<pre><code class="language-bash">npm start
</code></pre>

You will see the following homepage. Click on "Add room".

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png'>Large preview</a>)" alt="" >}}

You will see the following form. Type in a name for the room. Remember this name, as we will use this later on. Our example will be `bedroom`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7dfbf49-0b2b-4203-9524-c9b84d64cc5d/3-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7dfbf49-0b2b-4203-9524-c9b84d64cc5d/3-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” page on load (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7dfbf49-0b2b-4203-9524-c9b84d64cc5d/3-building-room-detector-iot-devices.png'>Large preview</a>)" alt="Add New Room page" >}}

Click "Start recording," and you will see the following status "Listening for wifi...".

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaf322d0-60e8-4b2a-9751-62be0c5cc7b6/4-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaf322d0-60e8-4b2a-9751-62be0c5cc7b6/4-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” starting recording (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaf322d0-60e8-4b2a-9751-62be0c5cc7b6/4-building-room-detector-iot-devices.png'>Large Preview</a>)" alt="starting recording" >}}

Once all 20 samples are recorded, your app will match the following. The status will read “Done.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b15151-2a24-4464-8540-64143f60d355/5-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b15151-2a24-4464-8540-64143f60d355/5-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” page after recording is complete (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7b15151-2a24-4464-8540-64143f60d355/5-building-room-detector-iot-devices.png'>Large preview</a>)" alt="" >}}

Click on the misnamed “Cancel” to return to the homepage, which matches the following.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” page after recording is complete (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png'>Large preview</a>)" alt="finished recording" >}}

We can now scan wifi networks from the desktop UI, which will save all recorded samples to files on disk. Next, we will train an out-of-box machine learning algorithm-least squares on the data you have collected.

## Step 4: Write Python Training Script

In this step, we will write a training script in Python. Create a directory for your training utilities.

<pre><code class="language-bash">mkdir model
</code></pre>

Open `model/train.py`

<pre><code class="language-bash">nano model/train.py
</code></pre>

At the top of your file, import the `numpy` computational library and `scipy` for its least squares model.

<pre><code class="language-bash">import numpy as np
from scipy.linalg import lstsq
import json
import sys
</code></pre>

The next three utilities will handle loading and setting up data from the files on disk. Start by adding a utility function that flattens nested lists. You will use this to flatten a list of list of samples.

<pre><code class="language-bash">import sys

def flatten(list_of_lists):
    """Flatten a list of lists to make a list.
    >>> flatten([[1], [2], [3, 4]])
    [1, 2, 3, 4]
    """
    return sum(list_of_lists, [])
</code></pre>

Add a second utility that loads samples from the specified files. This method abstracts away the fact that samples are spread out across multiple files, returning just a single generator for all samples. For each of the samples, the label is the index of the file. e.g., If you call `get_all_samples('a.json', 'b.json')`, all samples in `a.json` will have label 0 and all samples in `b.json` will have label 1.

<div class="break-out">

<pre><code class="language-bash">def get_all_samples(paths):
  """Load all samples from JSON files."""
  for label, path in enumerate(paths):
  with open(path) as f:
    for sample in json.load(f)['samples']:
      signal_levels = [
        network['signal_level'].replace('RSSI', '') or 0
        for network in sample]
      yield [network['mac'] for network in sample], signal_levels, label
</code></pre></div>

Next, add a utility that encodes the samples using a bag-of-words-esque model. Here is an example: Assume we collect two samples.

1. wifi network A at strength 10 and wifi network B at strength 15
2. wifi network B at strength 20 and wifi network C at strength 25.

This function will produce a list of three numbers for each of the samples: the first value is the strength of wifi network A, the second for network B, and the third for C. In effect, the format is [A, B, C].

1. [10, 15, 0]
2. [0, 20, 25]

<div class="break-out">

<pre><code class="language-bash">def bag_of_words(all_networks, all_strengths, ordering):
  """Apply bag-of-words encoding to categorical variables.

  >>> samples = bag_of_words(
  ...     [['a', 'b'], ['b', 'c'], ['a', 'c']],
  ...     [[1, 2], [2, 3], [1, 3]],
  ...     ['a', 'b', 'c'])
  >>> next(samples)
  [1, 2, 0]
  >>> next(samples)
  [0, 2, 3]
  """
  for networks, strengths in zip(all_networks, all_strengths):
    yield [strengths[networks.index(network)]
      if network in networks else 0
      for network in ordering]
</code></pre></div>

Using all three utilities above, we synthesize a collection of samples and their labels. Gather all samples and labels using `get_all_samples`. Define a consistent format `ordering` to one-hot encode all samples, then apply `one_hot` encoding to samples. Finally, construct the data and label matrices `X` and `Y` respectively.

<div class="break-out">

<pre><code class="language-bash">def create_dataset(classpaths, ordering=None):
  """Create dataset from a list of paths to JSON files."""
  networks, strengths, labels = zip(*get_all_samples(classpaths))
  if ordering is None:
    ordering = list(sorted(set(flatten(networks))))
  X = np.array(list(bag_of_words(networks, strengths, ordering))).astype(np.float64)
  Y = np.array(list(labels)).astype(np.int)
  return X, Y, ordering
</code></pre></div>

These functions complete the data pipeline. Next, we abstract away model prediction and evaluation. Start by defining the prediction method. The first function normalizes our model outputs, so that the sum of all values totals to 1 and that all values are non-negative; this ensures that the output is a valid probability distribution. The second evaluates the model.

<div class="break-out">

<pre><code class="language-bash">def softmax(x):
  """Convert one-hotted outputs into probability distribution"""
  x = np.exp(x)
  return x / np.sum(x)

def predict(X, w):
  """Predict using model parameters"""
  return np.argmax(softmax(X.dot(w)), axis=1)
</code></pre></div>

Next, evaluate the model’s accuracy. The first line runs prediction using the model. The second counts the numbers of times both predicted and true values agree, then normalizes by the total number of samples.

<pre><code class="language-bash">def evaluate(X, Y, w):
  """Evaluate model w on samples X and labels Y."""
  Y_pred = predict(X, w)
  accuracy = (Y == Y_pred).sum() / X.shape[0]
  return accuracy
</code></pre>

This concludes our prediction and evaluation utilities. After these utilities, define a `main` function that will collect the dataset, train, and evaluate. Start by reading the list of arguments from the command line `sys.argv`; these are the rooms to include in training. Then create a large dataset from all of the specified rooms.

<div class="break-out">

<pre><code class="language-bash">def main():
  classes = sys.argv[1:]

  train_paths = sorted(['data/{}_train.json'.format(name) for name in classes])
  test_paths = sorted(['data/{}_test.json'.format(name) for name in classes])
  X_train, Y_train, ordering = create_dataset(train_paths)
  X_test, Y_test, _ = create_dataset(test_paths, ordering=ordering)
</code></pre></div>

Apply one-hot encoding to the labels. A *one-hot encoding* is similar to the bag-of-words model above; we use this encoding to handle categorical variables. Say we have 3 possible labels. Instead of labelling 1, 2, or 3, we label the data with [1, 0, 0], [0, 1, 0], or [0, 0, 1]. For this tutorial, we will spare the explanation for why one-hot encoding is important. Train the model, and evaluate on both the train and validation sets.

<div class="break-out">

<pre><code class="language-bash">def main():
  ...
  X_test, Y_test, _ = create_dataset(test_paths, ordering=ordering)

  Y_train_oh = np.eye(len(classes))[Y_train]
  w, _, _, _ = lstsq(X_train, Y_train_oh)
  train_accuracy = evaluate(X_train, Y_train, w)
  test_accuracy = evaluate(X_test, Y_test, w)
</code></pre></div>

Print both accuracies, and save the model to disk.

<pre><code class="language-bash">def main():
  ...
  print('Train accuracy ({}%), Validation accuracy ({}%)'.format(train_accuracy*100, test_accuracy*100))
  np.save('w.npy', w)
  np.save('ordering.npy', np.array(ordering))
  sys.stdout.flush()
</code></pre>

At the end of the file, run the `main` function.

<pre><code class="language-javascript">if __name__ == '__main__':
  main()
</code></pre>

Save and exit. Double check that your file matches the following:

<div class="break-out">

<pre><code class="language-bash">import numpy as np
from scipy.linalg import lstsq
import json
import sys

def flatten(list_of_lists):
    """Flatten a list of lists to make a list.
    >>> flatten([[1], [2], [3, 4]])
    [1, 2, 3, 4]
    """
    return sum(list_of_lists, [])

def get_all_samples(paths):
    """Load all samples from JSON files."""
    for label, path in enumerate(paths):
        with open(path) as f:
            for sample in json.load(f)['samples']:
                signal_levels = [
                    network['signal_level'].replace('RSSI', '') or 0
                    for network in sample]
                yield [network['mac'] for network in sample], signal_levels, label

def bag_of_words(all_networks, all_strengths, ordering):
    """Apply bag-of-words encoding to categorical variables.
    >>> samples = bag_of_words(
    ...     [['a', 'b'], ['b', 'c'], ['a', 'c']],
    ...     [[1, 2], [2, 3], [1, 3]],
    ...     ['a', 'b', 'c'])
    >>> next(samples)
    [1, 2, 0]
    >>> next(samples)
    [0, 2, 3]
    """
    for networks, strengths in zip(all_networks, all_strengths):
        yield [int(strengths[networks.index(network)])
            if network in networks else 0
            for network in ordering]

def create_dataset(classpaths, ordering=None):
    """Create dataset from a list of paths to JSON files."""
    networks, strengths, labels = zip(*get_all_samples(classpaths))
    if ordering is None:
        ordering = list(sorted(set(flatten(networks))))
    X = np.array(list(bag_of_words(networks, strengths, ordering))).astype(np.float64)
    Y = np.array(list(labels)).astype(np.int)
    return X, Y, ordering

def softmax(x):
    """Convert one-hotted outputs into probability distribution"""
    x = np.exp(x)
    return x / np.sum(x)

def predict(X, w):
    """Predict using model parameters"""
    return np.argmax(softmax(X.dot(w)), axis=1)

def evaluate(X, Y, w):
    """Evaluate model w on samples X and labels Y."""
    Y_pred = predict(X, w)
    accuracy = (Y == Y_pred).sum() / X.shape[0]
    return accuracy

def main():
    classes = sys.argv[1:]

    train_paths = sorted(['data/{}_train.json'.format(name) for name in classes])
    test_paths = sorted(['data/{}_test.json'.format(name) for name in classes])
    X_train, Y_train, ordering = create_dataset(train_paths)
    X_test, Y_test, _ = create_dataset(test_paths, ordering=ordering)

    Y_train_oh = np.eye(len(classes))[Y_train]
    w, _, _, _ = lstsq(X_train, Y_train_oh)
    train_accuracy = evaluate(X_train, Y_train, w)
    validation_accuracy = evaluate(X_test, Y_test, w)

    print('Train accuracy ({}%), Validation accuracy ({}%)'.format(train_accuracy*100, validation_accuracy*100))
    np.save('w.npy', w)
    np.save('ordering.npy', np.array(ordering))
    sys.stdout.flush()

if __name__ == '__main__':
    main()
</code></pre></div>

Save and exit. Recall the room name used above when recording the 20 samples. Use that name instead of `bedroom` below. Our example is `bedroom`. We use `-W ignore` to ignore warnings from a LAPACK bug.

<pre><code class="language-bash">python -W ignore model/train.py bedroom
</code></pre>

Since we've only collected training samples for one room, you should see 100% training and validation accuracies.

<pre><code class="language-bash">Train accuracy (100.0%), Validation accuracy (100.0%)
</code></pre>

Next, we will link this training script to the desktop app.

{{% ad-panel-leaderboard %}}

## Step 5: Link Train Script

In this step, we will automatically retrain the model whenever the user collects a new batch of samples. Open `scripts/observe.js`.

<pre><code class="language-bash">nano scripts/observe.js
</code></pre>

Right after the `fs` import, import the child process spawner and utilities.

<pre><code class="language-javascript">var fs = require('fs');
// start new code
const spawn = require("child_process").spawn;
var utils = require('./utils.js');
</code></pre>

In the `ui` function, add the following call to `retrain` at the end of the completion handler.

<div class="break-out">

<pre><code class="language-javascript">function ui() {
  ...
  function completion() {
    ...
    retrain((data) => {
      var status = document.querySelector('#add-status');
      accuracies = data.toString().split('\n')[0];
      status.innerHTML = "Retraining succeeded: " + accuracies
    });
  }
    ...
}
</code></pre></div>

After the `ui` function, add the following `retrain` function. This spawns a child process that will run the python script. Upon completion, the process calls a completion handler. Upon failure, it will log the error message.

<div class="break-out">

<pre><code class="language-javascript">function ui() {
  ..
}

function retrain(completion) {
  var filenames = utils.get_filenames()
  const pythonProcess = spawn('python', ["./model/train.py"].concat(filenames));
  pythonProcess.stdout.on('data', completion);
  pythonProcess.stderr.on('data', (data) => {
    console.log(" * [ERROR] " + data.toString())
  })
}
</code></pre></div>

Save and exit. Open `scripts/utils.js`.

<pre><code class="language-javascript">nano scripts/utils.js
</code></pre>

Add the following utility for fetching all datasets in `data/`.

<div class="break-out">

<pre><code class="language-javascript">var fs = require('fs');

module.exports = {
  get_filenames: get_filenames
}

function get_filenames() {
  filenames = new Set([]);
  fs.readdirSync("data/").forEach(function(filename) {
      filenames.add(filename.replace('_train', '').replace('_test', '').replace('.json', '' ))
  });
  filenames = Array.from(filenames.values())
  filenames.sort();
  filenames.splice(filenames.indexOf('.DS_Store'), 1)
  return filenames
}
</code></pre></div>

Save and exit. For the conclusion of this step, physically move to a new location. There ideally should be a wall between your original location and your new location. The more barriers, the better your desktop app will work.

Once again, run your desktop app.

<pre><code class="language-bash">npm start
</code></pre>

Just as before, run the training script. Click on "Add room".

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png" sizes="100vw" caption="Home page with “Add New Room” button available (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b7d71e-21c0-452e-9122-8ef76427c053/2-building-room-detector-iot-devices.png'>Large preview</a>)" alt="home page with button" >}}

Type in a room name that is different from your first room's. We will use `living room`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7dfbf49-0b2b-4203-9524-c9b84d64cc5d/3-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7dfbf49-0b2b-4203-9524-c9b84d64cc5d/3-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” page on load (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7dfbf49-0b2b-4203-9524-c9b84d64cc5d/3-building-room-detector-iot-devices.png'>Large preview</a>)" alt="Add New Room page" >}}

Click "Start recording," and you will see the following status "Listening for wifi...".

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcc6909-e63b-461c-a01d-7a5b1f42b3de/6-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcc6909-e63b-461c-a01d-7a5b1f42b3de/6-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” starting recording for second room (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcc6909-e63b-461c-a01d-7a5b1f42b3de/6-building-room-detector-iot-devices.png'>Large preview</a>)" alt="" >}}

Once all 20 samples are recorded, your app will match the following. The status will read "Done. Retraining model..."

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4f30314-0743-4ed4-a7d9-e008e6cea4db/7-building-room-detector-iot-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4f30314-0743-4ed4-a7d9-e008e6cea4db/7-building-room-detector-iot-devices.png" sizes="100vw" caption="“Add New Room” page after recording for second room complete (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4f30314-0743-4ed4-a7d9-e008e6cea4db/7-building-room-detector-iot-devices.png'>Large preview</a>)" alt="finished recording 2" >}}

In the next step, we will use this retrained model to predict the room you’re in, on the fly.

## Step 6: Write Python Evaluation Script

In this step, we will load the pretrained model parameters, scan for wifi networks, and predict the room based on the scan.

Open `model/eval.py`.

<pre><code class="language-bash">nano model/eval.py
</code></pre>

Import libraries used and defined in our last script.

<pre><code class="language-bash">import numpy as np
import sys
import json
import os
import json

from train import predict
from train import softmax
from train import create_dataset
from train import evaluate
</code></pre>

Define a utility to extract the names of all datasets. This function assumes that all datasets are stored in `data/` as `<dataset>_train.json` and `<dataset>_test.json`.

<div class="break-out">

<pre><code class="language-javascript">from train import evaluate

def get_datasets():
  """Extract dataset names."""
  return sorted(list({path.split('_')[0] for path in os.listdir('./data')
    if '.DS' not in path}))
</code></pre></div>

Define the `main` function, and start by loading parameters saved from the training script.

<pre><code class="language-javascript">def get_datasets():
  ...

def main():
  w = np.load('w.npy')
  ordering = np.load('ordering.npy')
</code></pre>

Create the dataset and predict.

<pre><code class="language-javascript">def main():
  ...
  classpaths = [sys.argv[1]]
  X, _, _ = create_dataset(classpaths, ordering)
  y = np.asscalar(predict(X, w))
</code></pre>

Compute a confidence score based on the difference between the top two probabilities.

<pre><code class="language-javascript">def main():
  ...
  sorted_y = sorted(softmax(X.dot(w)).flatten())
  confidence = 1
  if len(sorted_y) > 1:
    confidence = round(sorted_y[-1] - sorted_y[-2], 2)
</code></pre>

Finally, extract the category and print the result. To conclude the script, invoke the `main` function.

<div class="break-out">

<pre><code class="language-javascript">def main()
  ...
  category = get_datasets()[y]
  print(json.dumps({"category": category, "confidence": confidence}))

if __name__ == '__main__':
  main()
</code></pre></div>

Save and exit. Double check your code matches the following ([source code](https://github.com/alvinwan/riot/blob/master/model/eval.py)):

<div class="break-out">

<pre><code class="language-python">import numpy as np
import sys
import json
import os
import json

from train import predict
from train import softmax
from train import create_dataset
from train import evaluate

def get_datasets():
    """Extract dataset names."""
    return sorted(list({path.split('_')[0] for path in os.listdir('./data')
        if '.DS' not in path}))

def main():
    w = np.load('w.npy')
    ordering = np.load('ordering.npy')

    classpaths = [sys.argv[1]]
    X, _, _ = create_dataset(classpaths, ordering)
    y = np.asscalar(predict(X, w))

    sorted_y = sorted(softmax(X.dot(w)).flatten())
    confidence = 1
    if len(sorted_y) > 1:
        confidence = round(sorted_y[-1] - sorted_y[-2], 2)

    category = get_datasets()[y]
    print(json.dumps({"category": category, "confidence": confidence}))

if __name__ == '__main__':
    main()
</code></pre></div>

Next, we will connect this evaluation script to the desktop app. The desktop app will continuously run wifi scans and update the UI with the predicted room.

## Step 7: Connect Evaluation To Desktop App

In this step, we will update the UI with a "confidence" display. Then, the associated NodeJS script will continuously run scans and predictions, updating the UI accordingly.

Open `static/index.html`.

<pre><code class="language-bash">nano static/index.html
</code></pre>

Add a line for confidence right after the title and before the buttons.

<div class="break-out">

<pre><code class="language-html">&lt;h1 class="title" id="predicted-room-name"&gt;(I dunno)&lt;/h1&gt;
&lt;!-- start new code --&gt;
&lt;p class="subtitle"&gt;with &lt;span id="predicted-confidence"&gt;0%&lt;/span&gt; confidence&lt;/p&gt;
&lt;!-- end new code --&gt;
&lt;div class="buttons"&gt;
</code></pre></div>

Right after `main` but before the end of the `body`, add a new script `predict.js`.

<pre><code class="language-javascript">&lt;/main&gt;
  &lt;!-- start new code --&gt;
  &lt;script&gt;
  require('../scripts/predict.js')
  &lt;/script&gt;
  &lt;!-- end new code --&gt;
&lt;/body&gt;
</code></pre>

Save and exit. Open `scripts/predict.js`.

<pre><code class="language-javascript">nano scripts/predict.js
</code></pre>

Import the needed NodeJS utilities for the filesystem, utilities, and child process spawner.

<pre><code class="language-javascript">var fs = require('fs');
var utils = require('./utils');
const spawn = require("child_process").spawn;
</code></pre>

Define a `predict` function which invokes a separate node process to detect wifi networks and a separate Python process to predict the room.

<div class="break-out">

<pre><code class="language-javascript">function predict(completion) {
  const nodeProcess = spawn('node', ["scripts/observe.js"]);
  const pythonProcess = spawn('python', ["-W", "ignore", "./model/eval.py", "samples.json"]);
}
</code></pre></div>

After both processes have spawned, add callbacks to the Python process for both successes and errors. The success callback logs information, invokes the completion callback, and updates the UI with the prediction and confidence. The error callback logs the error.

<div class="break-out">

<pre><code class="language-javascript">function predict(completion) {
  ...
  pythonProcess.stdout.on('data', (data) => {
    information = JSON.parse(data.toString());
    console.log(" * [INFO] Room '" + information.category + "' with confidence '" + information.confidence + "'")
    completion()

    if (typeof document != "undefined") {
      document.querySelector('#predicted-room-name').innerHTML = information.category
      document.querySelector('#predicted-confidence').innerHTML = information.confidence
    }
  });
  pythonProcess.stderr.on('data', (data) => {
    console.log(data.toString());
  })
}
</code></pre></div>

Define a main function to invoke the `predict` function recursively, forever.

<pre><code class="language-javascript">function main() {
  f = function() { predict(f) }
  predict(f)
}

main();
</code></pre>

One last time, open the desktop app to see the live prediction.

<pre><code class="language-bash">npm start
</code></pre>

Approximately every second, a scan will be completed and the interface will be updated with the latest confidence and predicted room. Congratulations; you have completed a simple room detector based on all in-range WiFi networks.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8aa10fb-c91b-4dd5-833d-4179b57aed86/8-building-room-detector-iot-devices.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8aa10fb-c91b-4dd5-833d-4179b57aed86/8-building-room-detector-iot-devices.gif" width="500" alt="demo" /></a><figcaption>Recording 20 samples inside the room and another 20 out in the hallway. Upon walking back inside, the script correctly predicts “hallway” then “bedroom.” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8aa10fb-c91b-4dd5-833d-4179b57aed86/8-building-room-detector-iot-devices.gif">Large preview</a>)</figcaption></figure>

## Conclusion

In this tutorial, we created a solution using only your desktop to detect your location within a building. We built a simple desktop app using Electron JS and applied a simple machine learning method on all in-range WiFi networks. This paves the way for Internet-of-things applications without the need for arrays of devices that are costly to maintain (cost not in terms of money but in terms of time and development).

**Note**: *You can see the source code in its entirety on [Github](https://github.com/alvinwan/riot).*

With time, you may find that this least squares does not perform spectacularly in fact. Try finding two locations within a single room, or stand in doorways. Least squares will be large unable to distinguish between edge cases. Can we do better? It turns out that we can, and in future lessons, we will leverage other techniques and the fundamentals of machine learning to better performance. This tutorial serves as a quick test bed for experiments to come.

{{< signature "ra, il" >}}
