---
title: How To Build A CLI Tool With Node.js And PhantomJS
slug: build-cli-tool-nodejs-phantomjs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7523bdee-fa89-4afc-aba6-f0ba19958dd5/nodejs-new-illu-logo.jpg
date: 2014-02-12T10:04:06.000Z
author: mark-mcdonnell
description: >-
  In this article, we’ll go over the concepts and techniques required to build a command line tool using [Node.js](https://nodejs.org/) and
  [PhantomJS](https://phantomjs.org/). Building a command line tool enables you
  to automate a process that would otherwise take a lot longer.
categories:
  - Coding
  - JavaScript
  - Tutorials
  - Techniques
  - Resources
  - Node.js
---
In this article, we’ll go over the concepts and techniques required to build a command line tool using <a href="https://nodejs.org/">Node.js</a> and <a href="https://phantomjs.org/">PhantomJS</a>. Building a command line tool enables you to automate a process that would otherwise take a lot longer.

Command line tools are built in a myriad of languages, but the one we’ll focus on is Node.js.</p>

### What We’ll Cover

*   Secret sauce
*   Installing Node.js and npm
*   Process
*   Automation
*   PhantomJS
*   Squirrel
*   How it works
*   The code
*   Packaging
*   Publishing
*   Conclusion

## Secret Sauce

For those short on time, I’ve condensed the core process into three steps. This is the secret sauce to convert your Node.js script into a fully functioning command line tool. But do stick around to see what else I have to show you.

{{% feature-panel %}}

1.  In your `package.json` file, include the following settings:
    *   `"preferGlobal": "true"`
    *   `"bin": { "name-of-command": "path-to-script.js" }`
2.  Add `#!/usr/bin/env node` to `path-to-script.js`.
3.  To test your new command (`name-of-command`), use `npm link`.

The rest of the process is just deciding what functionality to implement.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful Node.js Tools, Tutorials And Resources](https://www.smashingmagazine.com/2011/09/useful-node-js-tools-tutorials-and-resources/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Sailing With Sails.js: An MVC-style Framework For Node.js](https://www.smashingmagazine.com/2015/11/sailing-sails-js-mvc-style-framework-node-js/)
*   [The Issue With Global Node Packages](https://www.smashingmagazine.com/2016/01/issue-with-global-node-npm-packages/)

## Installing Node.js And npm

To install Node.js, you have a few options:

*   [OS-specific installer](https://nodejs.org/download/) for Windows, Mac or binary;
*   [Homebrew](https://brew.sh/): `brew install node`;
*   [Nave](https://github.com/isaacs/nave#nave);
*   [NVM](https://github.com/creationix/nvm#node-version-manager).

Note that npm is installed as part of Node.js; there is no separate installation.

To test that Node.js and npm are installed correctly, run the following commands in your terminal:

*   `node --version`
*   `npm --version`

## Process

Let’s consider a sample process: generating an <a href="https://www.html5rocks.com/en/tutorials/appcache/beginner/">Application Cache</a> manifest file.

In case you are unfamiliar with AppCache, it <strong>enables you to take your application offline</strong> by specifying pages and resources to cache in the event that the user loses their Internet connection or tries to access your application later offline.

Typically, you would create an <span class="removed_link" title="https://appcachefacts.info/">appcache.manifest</span> file, where you would configure the offline settings.

We won’t go into much detail about AppCache itself because that would distract us from the purpose of this article. Nevertheless, below are the lines for a sample file:

<pre><code class="language-markup">
CACHE MANIFEST

CACHE:
foo.jpg
index.html
offline.html
styles.css
behaviours.js

NETWORK:
*

FALLBACK:
/ /offline.html
</code></pre>

As you can see, we’ve specified the following:

*   a JPG image,
*   two HTML files,
*   a CSS file,
*   a JavaScript file.

These are the resources that we want to cache in case the user goes offline.

We’ve also specified that all other items requested by the user should require a network to be accessed.

Finally, we’ve stated that any file that should be cached but isn’t yet should redirect the user to a file named <code>offline.html</code>.</p>

## Automation

Having to manually look up all of the images, style sheets, scripts and other pages linked from a Web page would be tedious. Thus, we’re trying to automate the process of generating an AppCache manifest file.

We could do this by writing some Node.js code along with some additional tools, but that wouldn’t be very easy (even for the person writing the script), because we would need to open the code and tell it which Web page to interrogate.

We also want other people to have the benefit of this tool, without their needing to download a folder full of code, change certain lines of code and run commands to run the scripts.

This is why a command line tool would help.

## PhantomJS

First, we want to figure out how to solve this problem.

We’ll use a tool named <a href="https://phantomjs.org/">PhantomJS</a>, which is a headless (i.e. chromeless) browser.

Specifically, it’s a headless <a href="https://www.webkit.org/">WebKit</a> browser, which provides a JavaScript API that we can tap into and that lets us do things such as open Web pages and analyze their network requests. (It does many other things, but those are the two fundamental aspects we’re interested in.)

We can use a Node.js module to load PhantomJS and interact with its API. We can then convert our code into a command line tool with relative ease using Node.js’s package manager, <a href="https://npmjs.org/">npm</a>, and a <code>package.json</code> file.</p>

## Squirrel

Luckily, I’ve already done the work for you. It’s an open-source project named <a href="https://github.com/Integralist/Squirrel#squirrel">Squirrel</a>.

To install it, run the command <code>npm install -g squirrel-js</code>.

Once it’s installed, you can use it by running the command <code>squirrel [url]</code>. For example, <code>squirrel bbc.co.uk/news</code>.

This would generate (in the current directory) an <code>appcache.manifest</code> file populated with all relevant page resources.</p>

## How It Works

I started Squirrel by first writing the relevant Node.js and PhantomJS code to incorporate the functionality I was after.

Then, I added a script that bootstraps that code and allows me to take arguments that configure how the code runs.

I ended up with two scripts:

*   [squirrel.js](https://github.com/Integralist/Squirrel/blob/master/lib/squirrel.js)
*   [appcache.js](https://github.com/Integralist/Squirrel/blob/master/lib/appcache.js)

The first script sets up the work:

*   We specify the environment in which we want the script to execute (in this case, Node.js).
*   Parse the arguments passed by the user.
*   Read an internal (i.e. dummy) `appcache.manifest` file.
*   Open a shell child process, call PhantomJS and pass it the script that we want it to execute (in this case, `appcache.js`) and the dummy manifest file.
*   When the second script finishes its work (collating the Web page data), return to this first script and display some statistical information to the user and generate the manifest file.

The second script processes the Web page that the user has requested:

*   We take in the dummy manifest file.
*   Create listeners for the page resources that are requested.
*   Set the viewport size.
*   Open the Web page and store the resources.
*   Get all links from the page (by executing JavaScript code directly in the Web page).
*   Convert the contents of the manifest file and inject the resources found, and then return that as a JSON file.</p>

## The Code

Now that you understand what the code does, let’s review it. I’ll show the code in its entirely, and then we’ll go through it piecemeal.</p>

### squirrel.js

<pre><code class="language-javascript">
#!/usr/bin/env node

var userArguments = process.argv.slice(2); // Copies arguments list but removes first two options (script exec type &amp; exec location)

if (userArguments.length &gt; 1) {
    throw new Error('Only one argument may be specified (the URL for which you want to generate the AppCache.)');
}

var fs               = require('fs');
var shell            = require('child_process').execFile;
var phantomjs        = require('phantomjs').path;
var scriptToExecute  = __dirname + '/appcache.js';
var manifest         = __dirname + '/../appcache.manifest';
var url              = userArguments[0];
var manifestContent;
var data;

fs.readFile(manifest, bootstrap);

function bootstrap(err, contentAsBuffer) {
    if (err) throw err;

    manifestContent = contentAsBuffer.toString('utf8');

    shell(phantomjs, [scriptToExecute, url, manifestContent], function(err, stdout, stderr) {
        if (err) throw err;

        // Sometimes an error in the loaded page's JavaScript doesn't get picked up or thrown,
        // but the error comes in via stdout and causes JSON parsing to break
        try {
            data = JSON.parse(stdout);
        } catch(err) {
            log('Whoops! It seems there was an error? You'll find the stack trace below.');
            error(err);
        }

        displayStatistics();
        createManifestFile();
    });
}

function displayStatistics() {
    log(’); // Adds extra line of spacing when displaying the results
    log('Links: '      + data.links);
    log('Images: '     + data.images);
    log('CSS: '        + data.css);
    log('JavaScript: ' + data.javascript);
}

function createManifestFile() {
    fs.writeFile(process.cwd() + '/appcache.manifest', data.manifestContent, function(err) {
        if (err) throw err;

        log('nManifest file created');
    });
}

function log(message) {
    process.stdout.write(message + 'n');
}

function error(err) {
    process.stderr.write(err);
}
</code></pre>

The first line, <code>#!/usr/bin/env node</code>, is critical to the script being used in the shell. We have to tell the shell what process should handle the script.

Next, we have to retrieve the arguments passed to the command. If we run <code>squirrel bbc.co.uk/news</code>, then <code>process.argv</code> would be an array containing the following:

*   the script execution type (`node`);
*   the script being executed (`squirrel.js`);
*   any other arguments (in this instance, only one, `bbc.co.uk/news`).

Ignore the first two arguments, and store the user-specific arguments so that we can reference them later:

<pre><code class="language-javascript">
var userArguments = process.argv.slice(2);
</code></pre>

Our script only knows how to handle a single argument (which is the page URL to load). The following line isn’t really needed because we’ll ignore any more than one argument, but it’s useful for the code to have clear intent, so we’ll throw an error if more than one argument is passed.

<pre><code class="language-javascript">
if (userArguments.length &gt; 1) {
    throw new Error('Only one argument may be specified (the URL for which you want to generate the AppCache.)');
}
</code></pre>

Because we’re using PhantomJS, we’ll need to open up a shell and call the <code>phantomjs</code> command:

<pre><code class="language-javascript">
var shell = require('child_process').execFile;
</code></pre>

We’ll also need to reference the <code>bin</code> directory, where the PhantomJS executable is stored:

<pre><code class="language-javascript">
var phantomjs = require('phantomjs').path;
</code></pre>

Next, store a reference to the script that we want PhantomJS to execute, as well as the dummy manifest file.

<pre><code class="language-javascript">
var scriptToExecute = __dirname + '/appcache.js';
var manifest        = __dirname + '/../appcache.manifest';
var url             = userArguments[0];
</code></pre>

Because the PhantomJS script that we’ll be executing needs a reference to the dummy manifest file, we’ll asynchronously read the contents of the file and then pass it on to a <code>bootstrap</code> function:

<pre><code class="language-javascript">
fs.readFile(manifest, bootstrap);
</code></pre>

Our <code>bootstrap</code> function does exactly what you would expect: start our application (in this case, by opening the shell and calling PhantomJS). You’ll also notice that Node.js passes the contents of the manifest as a buffer, which we need to convert back into a string:

<pre><code class="language-javascript">
function bootstrap(err, contentAsBuffer) {
    if (err) throw err;

    manifestContent = contentAsBuffer.toString('utf8');

    shell(phantomjs, [scriptToExecute, url, manifestContent], function(err, stdout, stderr) {
        // code...
    });
}
</code></pre>

At this point in the execution of the code, we are in the <code>appcache.js</code> file. Let’s move over there now.</p>

### appcache.js

The purpose of <code>appcache.js</code> is to get information from the user-requested page and pass it back to <code>squirrel.js</code> for processing.

Again, I’ll show the script in its entirety, and then we’ll break it down. (Don’t worry, we won’t go over each line — only the important parts.)

<pre><code class="language-javascript">
var unique     = require('lodash.uniq');
var system     = require('system');
var fs         = require('fs');
var page       = require('webpage').create();
var args       = system.args;
var manifest   = args[2];
var css        = [];
var images     = [];
var javascript = [];
var links;
var url;
var path;

bootstrap();
pageSetUp();
openPage();

function bootstrap() {
    if (urlProvided()) {
        url = cleanUrl(args[1]);
    } else {
        var error = new Error('Sorry, a valid URL could not be recognized');
            error.additional = 'Valid URL example: bbc.co.uk/news';

        throw error;

        phantom.exit();
    }

    if (bbcNews()) {
        // We want to serve the responsive code base.
        phantom.addCookie({
            'name'  : 'ckps_d',
            'value' : 'm',
            'domain': '.bbc.co.uk'
        });
    }
}

function pageSetUp() {
    page.onResourceRequested = function(request) {
        if (/.(?:png|jpeg|jpg|gif)$/i.test(request.url)) {
            images.push(request.url);
        }

        if (/.(?:js)$/i.test(request.url)) {
            javascript.push(request.url);
        }

        if (/.(?:css)$/i.test(request.url)) {
            css.push(request.url);
        }
    };

    page.onError = function(msg, trace) {
        console.log('Error :', msg);

        trace.forEach(function(item) {
            console.log('Trace:  ', item.file, ':', item.line);
        });
    }

    page.viewportSize = { width: 1920, height: 800 };
}

function openPage() {
    page.open(url, function(status) {
        links      = unique(getLinks());
        images     = unique(images);
        css        = unique(css);
        javascript = unique(javascript);

        populateManifest();

        // Anything written to stdout is actually passed back to our Node script callback
        console.log(JSON.stringify({
            links           : links.length,
            images          : images.length,
            css             : css.length,
            javascript      : javascript.length,
            manifestContent : manifest
        }));

        phantom.exit();
    });
}

function urlProvided() {
    return args.length &gt; 1 &amp;&amp; /(?:www.)?[a-z-z1-9]+./i.test(args[1]);
}

function cleanUrl(providedUrl) {
    // If no http or https found at the start of the URL...
    if (/^(?!https?://)[wd]/i.test(providedUrl)) {
        return 'https://' + providedUrl + '/';
    }
}

function bbcNews(){
    if (/bbc.co.uk/news/i.test(url)) {
        return true;
    }
}

function getLinks() {
    var results = page.evaluate(function() {
        return Array.prototype.slice.call(document.getElementsByTagName('a')).map(function(item) {
            return item.href;
        });
    });

    return results;
}

function writeVersion() {
    manifest = manifest.replace(/# Timestamp: d+/i, '# Timestamp: ' + (new Date()).getTime());
}

function writeListContentFor(str, type) {
    manifest = manifest.replace(new RegExp('(# ' + str + ')\n[\s\S]+?\n\n', 'igm'), function(match, cg) {
        return cg + 'n' + type.join('n') + 'nn';
    });
}

function populateManifest() {
    writeVersion();

    writeListContentFor('Images', images);
    writeListContentFor('Internal HTML documents', links);
    writeListContentFor('Style Sheets', css);
    writeListContentFor('JavaScript', javascript);
}
</code></pre>

We begin by using PhantomJS’ API to create a new Web page:

<pre><code class="language-javascript">
var page = require('webpage').create();
</code></pre>

Next, we’ll check that a URL was provided and, if so, clean it into the format required (for example, by giving it an <code>http</code> protocol). Otherwise, we’ll throw an error and stop PhantomJS:

<pre><code class="language-javascript">
if (urlProvided()) {
    url = cleanUrl(args[1]);
} else {
    var error = new Error('Sorry, a valid URL could not be recognized');
    error.additional = 'Valid URL example: bbc.co.uk/news';

    throw error;
    phantom.exit();
}
</code></pre>

We also put in a check to see whether the URL passed was for <code>bbc.co.uk/news</code> and, if so, use PhantomJS to set a cookie that enables the responsive version of the website to load (the purpose being merely to demonstrate some of PhantomJS’ useful APIs, such as <code>addCookie</code>):

<pre><code class="language-javascript">
if (bbcNews()) {
    phantom.addCookie({
        'name'  : 'ckps_d',
        'value' : 'm',
        'domain': '.bbc.co.uk'
    });
}
</code></pre>

For PhantomJS to be able to analyze the network data (so that we can track the style sheets, JavaScript and images being requested by the page), we need to use special PhantomJS handlers to interpret the requests:

<pre><code class="language-javascript">
page.onResourceRequested = function(request) {
    if (/.(?:png|jpeg|jpg|gif)$/i.test(request.url)) {
        images.push(request.url);
    }

    if (/.(?:js)$/i.test(request.url)) {
        javascript.push(request.url);
    }

    if (/.(?:css)$/i.test(request.url)) {
        css.push(request.url);
    }
};
</code></pre>

We’ll also use another PhantomJS API feature that enables us to determine the size of the browser window:

<pre><code class="language-javascript">
page.viewportSize = { width: 1920, height: 800 };
</code></pre>

We then tell PhantomJS to open the specified Web page. Once the page is open (i.e. the <code>load</code> event has fired), a callback is executed:

<pre><code class="language-javascript">
page.open(url, function(status) {
    // code...
});
</code></pre>

In the callback, we store the resources that were found, and we call a function that replaces the contents of our string (the dummy manifest) with a list of each set of resources:

<pre><code class="language-javascript">
page.open(url, function(status) {
    links      = unique(getLinks());
    images     = unique(images);
    css        = unique(css);
    javascript = unique(javascript);

    populateManifest();

    // Remaining code...
});
</code></pre>

Finally, we create a data object to hold statistics about the resources being requested, convert it to a JSON string, and log it using the <code>console</code> API.

Once this is done, we tell PhantomJS to <code>exit</code> (otherwise the process would stall):

<pre><code class="language-javascript">
page.open(url, function(status) {
    // Previous code...

    console.log(JSON.stringify({
        links           : links.length,
        images          : images.length,
        css             : css.length,
        javascript      : javascript.length,
        manifestContent : manifest
    }));

    phantom.exit();
});
</code></pre>

Reviewing the code above, you might wonder how we get the data back to our <code>squirrel.js</code> script? Take another look at the <code>console.log</code>. The code has an odd side effect, which is that any code logged by PhantomJS is passed back to our shell callback (originally executed in <code>squirrel.js</code>).

Let’s revisit our <code>squirrel.js</code> script now.</p>

### Back to squirrel.js

<pre><code class="language-javascript">
shell(phantomjs, [scriptToExecute, url, manifestContent], function(err, stdout, stderr) {
    if (err) throw err;

    try {
        data = JSON.parse(stdout);
    } catch(err) {
        log('Whoops! It seems there was an error? You'll find the stack trace below.');
        error(err);
    }

    displayStatistics();
    createManifestFile();
});
</code></pre>

The callback function is run when the PhantomJS script finishes executing. It is passed any errors that may have occurred and, if there are, then we throw the error:

<code>if (err) throw err;</code>

The other arguments are the standard output and error arguments provided by the shell. In this case, the standard output would be our JSON string, which we <code>console.log</code>’ed from <code>appcache.js</code>. We parse the JSON string and convert it back into an object so that we can present the data to the user who has run the <code>squirrel</code> command.

As a side note, we wrap this conversion in a <code>try/catch</code> clause to protect against Web pages that cause a JavaScript error to occur (the error is picked up by <code>stdout</code>, not <code>stderr</code>, thus causing the JSON parsing to break):

<pre><code class="language-javascript">
try {
    data = JSON.parse(stdout);
} catch(err) {
    error(err);
}
</code></pre>

Once we have our data, we call <code>displayStatistics</code>, which uses <code>stdout</code> to write a message to the user’s terminal.

Lastly, we call <code>createManifestFile</code>, which creates an <code>appcache.manifest</code> file in the user’s current directory:

<pre><code class="language-javascript">
fs.writeFile(process.cwd() + '/appcache.manifest', data.manifestContent, function(err) {
    if (err) throw err;

    log('nManifest file created');
});
</code></pre>

Now that we understand how the script works in its entirety, let’s look at how to allow others to download and install our work.</p>

## Packaging

For other users to be able to install our module, we’ll need to publish it to a public repository. The place to do this is the <a href="https://npmjs.org/">npm</a> registry.

To publish to npm, you’ll need a <code>package.json</code> file.

The purpose of <code>package.json</code> is to specify the dependencies of the project you’re working on. In this instance, it specifies the dependencies required by Squirrel to do its job.

Below is Squirrel’s <code>package.json</code> file:

<pre><code class="language-javascript">
{
  "name": "squirrel-js",
  "version": "0.1.3",
  "description": "Node.js-based CLI tool, using PhantomJS to automatically generate an Application Cache manifest file for a specified URL",
  "main": "lib/squirrel",
  "scripts": {
    "test": "echo "Error: no test specified" &amp;&amp; exit 1"
  },
  "engines": {
    "node": "&gt;=0.10"
  },
  "repository": {
    "type": "git",
    "url": "git://github.com/Integralist/Squirrel.git"
  },
  "preferGlobal": "true",
  "bin": {
    "squirrel": "lib/squirrel.js"
  },
  "dependencies": {
    "phantomjs": "~1.9.2-6",
    "lodash.uniq": "~2.4.1"
  },
  "keywords": [
    "appcache",
    "phantomjs",
    "cli"
  ],
  "author": "Mark McDonnell &lt;mark.mcdx@gmail.com&gt; (https://www.integralist.co.uk/)",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/Integralist/Squirrel/issues"
  },
  "homepage": "https://github.com/Integralist/Squirrel"
}
</code></pre>

You can read up on all of the properties of <code>package.json</code> in the npm registry.

The properties to note are these:

*   `"preferGlobal": "true"`
*   `"bin": { "squirrel": "lib/squirrel.js" }`

The first property indicates when a user has installed a module that you would prefer to be installed globally. In this case, we want it to be installed globally because then the user will be able to run the command anywhere in their system.

The second property indicates where the command will find the code required to execute the command.

To test that your command works, you’ll need to run the <code>npm link</code> command, which in this case creates a symlink from the <code>squirrel</code> command to the <code>squirrel.js</code> file.</p>

## Publishing

To publish your code, first <a href="https://npmjs.org/signup">register</a> for an npm account.

<pre><code class="language-javascript">
function bootstrap(err, contentAsBuffer) {
    if (err) throw err;

    manifestContent = contentAsBuffer.toString('utf8');

    shell(phantomjs, [scriptToExecute, url, manifestContent], function(err, stdout, stderr) {
        // code...
    });
}
</code></pre>

At this point in the execution of the code, we are in the <code>appcache.js</code> file. Let’s move over there now.</p>

### appcache.js

The purpose of <code>appcache.js</code> is to get information from the user-requested page and pass it back to <code>squirrel.js</code> for processing.

Again, I’ll show the script in its entirety, and then we’ll break it down. (Don’t worry, we won’t go over each line — only the important parts.)

<pre><code class="language-javascript">
var unique     = require('lodash.uniq');
var system     = require('system');
var fs         = require('fs');
var page       = require('webpage').create();
var args       = system.args;
var manifest   = args[2];
var css        = [];
var images     = [];
var javascript = [];
var links;
var url;
var path;

bootstrap();
pageSetUp();
openPage();

function bootstrap() {
    if (urlProvided()) {
        url = cleanUrl(args[1]);
    } else {
        var error = new Error('Sorry, a valid URL could not be recognized');
            error.additional = 'Valid URL example: bbc.co.uk/news';

        throw error;

        phantom.exit();
    }

    if (bbcNews()) {
        // We want to serve the responsive code base.
        phantom.addCookie({
            'name'  : 'ckps_d',
            'value' : 'm',
            'domain': '.bbc.co.uk'
        });
    }
}

function pageSetUp() {
    page.onResourceRequested = function(request) {
        if (/.(?:png|jpeg|jpg|gif)$/i.test(request.url)) {
            images.push(request.url);
        }

        if (/.(?:js)$/i.test(request.url)) {
            javascript.push(request.url);
        }

        if (/.(?:css)$/i.test(request.url)) {
            css.push(request.url);
        }
    };

    page.onError = function(msg, trace) {
        console.log('Error :', msg);

        trace.forEach(function(item) {
            console.log('Trace:  ', item.file, ':', item.line);
        });
    }

    page.viewportSize = { width: 1920, height: 800 };
}

function openPage() {
    page.open(url, function(status) {
        links      = unique(getLinks());
        images     = unique(images);
        css        = unique(css);
        javascript = unique(javascript);

        populateManifest();

        // Anything written to stdout is actually passed back to our Node script callback
        console.log(JSON.stringify({
            links           : links.length,
            images          : images.length,
            css             : css.length,
            javascript      : javascript.length,
            manifestContent : manifest
        }));

        phantom.exit();
    });
}

function urlProvided() {
    return args.length &gt; 1 &amp;&amp; /(?:www.)?[a-z-z1-9]+./i.test(args[1]);
}

function cleanUrl(providedUrl) {
    // If no http or https found at the start of the URL...
    if (/^(?!https?://)[wd]/i.test(providedUrl)) {
        return 'https://' + providedUrl + '/';
    }
}

function bbcNews(){
    if (/bbc.co.uk/news/i.test(url)) {
        return true;
    }
}

function getLinks() {
    var results = page.evaluate(function() {
        return Array.prototype.slice.call(document.getElementsByTagName('a')).map(function(item) {
            return item.href;
        });
    });

    return results;
}

function writeVersion() {
    manifest = manifest.replace(/# Timestamp: d+/i, '# Timestamp: ' + (new Date()).getTime());
}

function writeListContentFor(str, type) {
    manifest = manifest.replace(new RegExp('(# ' + str + ')\n[\s\S]+?\n\n', 'igm'), function(match, cg) {
        return cg + 'n' + type.join('n') + 'nn';
    });
}

function populateManifest() {
    writeVersion();

    writeListContentFor('Images', images);
    writeListContentFor('Internal HTML documents', links);
    writeListContentFor('Style Sheets', css);
    writeListContentFor('JavaScript', javascript);
}
</code></pre>

We begin by using PhantomJS’ API to create a new Web page:

<pre><code class="language-javascript">
var page = require('webpage').create();
</code></pre>

Next, we’ll check that a URL was provided and, if so, clean it into the format required (for example, by giving it an <code>http</code> protocol). Otherwise, we’ll throw an error and stop PhantomJS:

<pre><code class="language-javascript">
if (urlProvided()) {
    url = cleanUrl(args[1]);
} else {
    var error = new Error('Sorry, a valid URL could not be recognized');
    error.additional = 'Valid URL example: bbc.co.uk/news';

    throw error;
    phantom.exit();
}
</code></pre>

We also put in a check to see whether the URL passed was for <code>bbc.co.uk/news</code> and, if so, use PhantomJS to set a cookie that enables the responsive version of the website to load (the purpose being merely to demonstrate some of PhantomJS’ useful APIs, such as <code>addCookie</code>):

<pre><code class="language-javascript">
if (bbcNews()) {
    phantom.addCookie({
        'name'  : 'ckps_d',
        'value' : 'm',
        'domain': '.bbc.co.uk'
    });
}
</code></pre>

For PhantomJS to be able to analyze the network data (so that we can track the style sheets, JavaScript and images being requested by the page), we need to use special PhantomJS handlers to interpret the requests:

<pre><code class="language-javascript">
page.onResourceRequested = function(request) {
    if (/.(?:png|jpeg|jpg|gif)$/i.test(request.url)) {
        images.push(request.url);
    }

    if (/.(?:js)$/i.test(request.url)) {
        javascript.push(request.url);
    }

    if (/.(?:css)$/i.test(request.url)) {
        css.push(request.url);
    }
};
</code></pre>

We’ll also use another PhantomJS API feature that enables us to determine the size of the browser window:

<pre><code class="language-javascript">
page.viewportSize = { width: 1920, height: 800 };
</code></pre>

We then tell PhantomJS to open the specified Web page. Once the page is open (i.e. the <code>load</code> event has fired), a callback is executed:

<pre><code class="language-javascript">
page.open(url, function(status) {
    // code...
});
</code></pre>

In the callback, we store the resources that were found, and we call a function that replaces the contents of our string (the dummy manifest) with a list of each set of resources:

<pre><code class="language-javascript">
page.open(url, function(status) {
    links      = unique(getLinks());
    images     = unique(images);
    css        = unique(css);
    javascript = unique(javascript);

    populateManifest();

    // Remaining code...
});
</code></pre>

Finally, we create a data object to hold statistics about the resources being requested, convert it to a JSON string, and log it using the <code>console</code> API.

Once this is done, we tell PhantomJS to <code>exit</code> (otherwise the process would stall):

<pre><code class="language-javascript">
page.open(url, function(status) {
    // Previous code...

    console.log(JSON.stringify({
        links           : links.length,
        images          : images.length,
        css             : css.length,
        javascript      : javascript.length,
        manifestContent : manifest
    }));

    phantom.exit();
});
</code></pre>

Reviewing the code above, you might wonder how we get the data back to our <code>squirrel.js</code> script? Take another look at the <code>console.log</code>. The code has an odd side effect, which is that any code logged by PhantomJS is passed back to our shell callback (originally executed in <code>squirrel.js</code>).

Let’s revisit our <code>squirrel.js</code> script now.</p>

### Back to squirrel.js

<pre><code class="language-javascript">
shell(phantomjs, [scriptToExecute, url, manifestContent], function(err, stdout, stderr) {
    if (err) throw err;

    try {
        data = JSON.parse(stdout);
    } catch(err) {
        log('Whoops! It seems there was an error? You'll find the stack trace below.');
        error(err);
    }

    displayStatistics();
    createManifestFile();
});
</code></pre>

The callback function is run when the PhantomJS script finishes executing. It is passed any errors that may have occurred and, if there are, then we throw the error:

<code>if (err) throw err;</code>

The other arguments are the standard output and error arguments provided by the shell. In this case, the standard output would be our JSON string, which we <code>console.log</code>’ed from <code>appcache.js</code>. We parse the JSON string and convert it back into an object so that we can present the data to the user who has run the <code>squirrel</code> command.

As a side note, we wrap this conversion in a <code>try/catch</code> clause to protect against Web pages that cause a JavaScript error to occur (the error is picked up by <code>stdout</code>, not <code>stderr</code>, thus causing the JSON parsing to break):

<pre><code class="language-javascript">
try {
    data = JSON.parse(stdout);
} catch(err) {
    error(err);
}
</code></pre>

Once we have our data, we call <code>displayStatistics</code>, which uses <code>stdout</code> to write a message to the user’s terminal.

Lastly, we call <code>createManifestFile</code>, which creates an <code>appcache.manifest</code> file in the user’s current directory:

<pre><code class="language-javascript">
fs.writeFile(process.cwd() + '/appcache.manifest', data.manifestContent, function(err) {
    if (err) throw err;

    log('nManifest file created');
});
</code></pre>

Now that we understand how the script works in its entirety, let’s look at how to allow others to download and install our work.</p>

## Packaging

For other users to be able to install our module, we’ll need to publish it to a public repository. The place to do this is the <a href="https://npmjs.org/">npm</a> registry.

To publish to npm, you’ll need a <code>package.json</code> file.

The purpose of <code>package.json</code> is to specify the dependencies of the project you’re working on. In this instance, it specifies the dependencies required by Squirrel to do its job.

Below is Squirrel’s <code>package.json</code> file:

<pre><code class="language-javascript">
{
  "name": "squirrel-js",
  "version": "0.1.3",
  "description": "Node.js-based CLI tool, using PhantomJS to automatically generate an Application Cache manifest file for a specified URL",
  "main": "lib/squirrel", "echo "Error: no test specified" &amp;&amp; exit 1"
  }, "&gt;=0.10"
  }, "git",
    "url": "git://github.com/Integralist/Squirrel.git"
  },
  "preferGlobal": "true",
  "bin": {
    "squirrel": "lib/squirrel.js"
  },
  "dependencies": {
    "phantomjs": "~1.9.2-6",
    "lodash.uniq": "~2.4.1"
  },
  "keywords": [
    "appcache",
    "phantomjs",
    "cli" "Mark McDonnell &lt;mark.mcdx@gmail.com&gt; (https://www.integralist.co.uk/)",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/Integralist/Squirrel/issues"
  },
  "homepage": "https://github.com/Integralist/Squirrel"
}
</code></pre>

You can read up on all of the properties of <code>package.json</code> in the npm registry.

The properties to note are these:

*   `"preferGlobal": "true"`
*   `"bin": { "squirrel": "lib/squirrel.js" }`

The first property indicates when a user has installed a module that you would prefer to be installed globally. In this case, we want it to be installed globally because then the user will be able to run the command anywhere in their system.

The second property indicates where the command will find the code required to execute the command.

To test that your command works, you’ll need to run the <code>npm link</code> command, which in this case creates a symlink from the <code>squirrel</code> command to the <code>squirrel.js</code> file.</p>

## Publishing

To publish your code, first <a href="https://npmjs.org/signup">register</a> for an npm account.

You’ll need to verify the account via the command line. To do this, run <code>npm adduser</code>, which will ask you to specify a user name and password.

Once you’ve verified the account, you can publish your module to the npm registry using <code>npm publish</code>.

It could take a few minutes for the module to become publicly accessible.

Be aware that if you update the code and try to run <code>npm publish</code> without updating the <code>package.json</code> file’s <code>version</code> property, then npm will return an error asking you to update the version number.</p>

## Conclusion

This is just one example of the sort of command line tools you can develop with Node.js’ many features.

The next time you find yourself performing a repetitive task, consider automating the process with a CLI tool.

{{< signature "al" >}}

