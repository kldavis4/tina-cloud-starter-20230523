---
title: 'Automated Browser Testing With The WebDriver API'
slug: automated-testing
author: jason-mcconnell
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cc5f152-3760-419c-a09b-91e8592a8997/automated-testing-cover-opt.png
date: 2018-01-30T16:30:57+01:00
summary: >-
  This article provides an overview of the concepts, technologies and coding techniques involved with running test scripts against browsers automatically using WebDriverJS on Windows 10 and Microsoft Edge.
description: >-
  This article provides an overview of the concepts, technologies and coding techniques involved with running test scripts against browsers automatically using WebDriverJS on Windows 10 and Microsoft Edge.
categories:
  - JavaScript
  - API
  - Testing
  - Techniques
---
<p>Manually clicking through different browsers as they run your development code, either locally or remotely, is a quick way to validate that code. It allows you to visually inspect that things are as you intended them to be from a layout and functionality point of view. However, it’s not a solution for testing the full breadth of your site’s code base on the assortment of browsers and device types available to your customers. That’s where automated testing really comes into its own.</p>

<p>Spearheaded by the <a href="https://docs.seleniumhq.org/">Selenium</a> project, automated web testing is a suite of tools to author, manage and
run test against browsers across platforms.</p>

## WebDriverJS API

<p>The <a href="https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/dev-guide/tools/webdriver/">WebDriver</a> API is a standard that abstracts out the device/browser specific bindings from the developer so that test scripts written in your language of choice can be written once and run on many different browsers via WebDriver. Some browsers have built-in WebDriver capabilities, others require you to download a binary for your browser/OS combination.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3607ef2-6487-4afc-aa90-ebbe9a518d8d/webdriveroverview.png" sizes="100vw" caption="" alt="webdriverjs api" >}}

### Driving The Browser Through WebDriver APIs

<p>The <a href="https://w3c.github.io/webdriver/webdriver-spec.html">WebDriver spec</a> at the W3C documents the APIs available to developers to programmatically control the browser.  This diagram shows a sample page with some of the general WebDriver collections and APIs that can be used to get and set browser properties.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19faeb66-131b-4878-b3ce-554db6a17482/webdriverobjects.png" sizes="100vw" caption="" alt="webdriverjs api" >}}

## Authoring Tests

<p>You have a choice of languages based on the supported language bindings for WebDriver. The core languages supported by the main Selenium/WebDriverJS project include:</p>

<ul>
<li>C#</li>
<li>Java</li>
<li>JavaScript (via Node)</li>
<li>Python</li>
<li>Ruby</li>
</ul>

{{% feature-panel %}}

<p>Tests can vary from checking layout of the page, values returned from server-side calls, expected behavior of user interaction to workflow verification like ensuring a shopping cart workflow works as expected.</p>

<p>For illustrative purposes, let’s assume we’re testing the TODOMVC <a href="https://todomvc.com/">application</a>, a demo application that's implemented in several different model-view-control JavaScript frameworks. This simple application provides UI to enter To-Do items, edit, delete and mark items as complete. We’ll use the React based example at <a href="https://todomvc.com/examples/react/">https://todomvc.com/examples/react/</a>.</p>

<p>We will then be able to demonstrate running the tests for the React example against the Backbone.js and Vue.js examples by simply changing the URL.</p>

- [Gist of the full JS example file](https://gist.github.com/Maggers/63fbbc7af1d9a1883d545ed08febefd6#file-automatedtests-js)

<p>For this demonstration, we’re going to write tests in JavaScript running in node to:</p>

<ol>
<li>Add three to-do items and verifying what we typed in was created into a to-do item.</li>
<li>Modify that item by double clicking, sending backspace keyboard commands and adding more text.</li>
<li>Delete that item using by using the mouse APIs.</li>
<li>Check an item off the list as completed.</li>
</ol>

### Setup Your Basic Automation Test Environment

<p>Let's begin by getting our Windows 10 machine setup to run WebDriver using JavaScript. Calls to WebDriver from node are going to be almost always asynchronous. To make the code easier to read we have used ES2016's async/await over Promises or callbacks.</p>

<p>You’ll need <a href="https://nodejs.org/en/">install node.js</a> newer than v7.6 or use Babel to cross compile to have support for the async/await feature. Also, we use <a href="https://code.visualstudio.com/">Visual Studio Code</a> for editing and debugging node.</p>

<p><strong>WebDriverJS For Microsoft Edge</strong></p>

<p>Each browser will have a binary file that you will need locally to interact with the browser itself. That binary is called by your code through the Selenium WebDriver APIs. You can find the latest downloads and documentation for the Microsoft Edge <a href="https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/">WebDriver here</a>.</p>

<p>Note that the version of Edge you want to run the tests against must be tested with the matching version of <code>MicrosoftWebDriver.exe</code>. We’re going to be using the stable version of Edge (16.16299) with the corresponding MicrosoftWebDriver.exe version 5.16299.</p>

<p>Place the <code>MicrosoftWebDriver.exe</code> in your path or in the same folder that your test script will run. Running this executable will start a console window showing you the URL and port number that WebDriverJS will be expecting to handle requests to be sent.</p>

<p><strong>WebDriverJS For Other Browsers</strong></p>

<p>You can easily tell WebDriverJS to run tests in a different browser by setting a configuration variable and having the appropriate binary driver for the respective browser installed. You can find them here:</p>

<ul>
<li>Apple Safari: <a href="https://webkit.org/blog/6900/webdriver-support-in-safari-10/">Bundled with</a> Safari 10+</li>
<li>Google Chrome: <a href="https://sites.google.com/a/chromium.org/chromedriver/">ChromeDriver
</a></li>
<li>Microsoft Internet Explorer: IEDriver from the <a href="https://docs.seleniumhq.org/download/">Selenium project
</a></li>
<li>Mozilla Firefox: <a href="https://github.com/mozilla/geckodriver/releases">Geckodriver</a></li>
<li>Opera: <a href="https://github.com/operasoftware/operachromiumdriver/">OperaChromiumDriver
</a></li>
</ul>

<p><strong>Selenium WebDriverJS For JavaScript</strong></p>

<p>To interact with the binary driver you just downloaded via JavaScript, you’ll need to install the Selenium WebDriver <a href="https://www.npmjs.com/package/selenium-webdriver">automation library</a> for JavaScript. This can be easily installed as a node package using:</p>

<p><code>npm install selenium-webdriver</code></p>

## Writing Automation Code

<p>Once your browser specific driver binary is in your system’s path or local folder, and you’ve installed Selenium WebDriver via npm, you can start automating the browser through code.</p>

<p>Let’s break down our example code into the various steps you’ll need.</p>

<ol>
<li>Create a local variable to load and interact with the library.

<pre><code class="language-javascript">var webdriver = require('selenium-webdriver');</code></pre>
</li>
<li>By default, WebDriverJS will assume you’re running locally and that the driver file exists. Later we’ll show how you can pass configuration information into the library when instantiating the browser the first time. WebDriverJS gets instantiated with a configuration variable called “capabilities” to define which browser driver you want to use.

<pre><code class="language-javascript">var capabilities = {
    'browserName': 'MicrosoftEdge'
  };
  var entrytoEdit = "Browser Stack";
</code></pre>
</li>
<li>Then you create a variable and call build() with the capabilities config variable to have WebDriverJS instantiate the browser:

<pre><code class="language-javascript">var browser = new webdriver.Builder().withCapabilities(capabilities).build();</code></pre>
</li>
<li>Now that we can interact with the browser, we tell it to navigate to a URL using the `get` method. This method is asynchronous so we use `await` to wait until it finishes.

<pre><code class="language-javascript">// Have the browser navigate to the TODO MVC example for React
    await browser.get('https://todomvc.com/examples/react/#');
</code></pre>
</li>
<li>For some browsers and systems, it’s best to give the WebDriverJS binary some time to navigate to the URL and load the page. For our example, we wait for 1 second (1000ms) using the manage function of WebDriverJS:

<pre><code class="language-javascript">//Send a wait to the browser to account for script execution running
    await browser.manage().timeouts().implicitlyWait(1000);
</code></pre>
</li>
<li>You now have a programmatic hook into a running browser through the browser variable.  Note the collection diagram earlier in this document that shows the WebDriver API collections. We use the Elements collection to get specific elements from the page. In this case, we’re looking for the entry box within the TODOMVC example so we can enter some TODO items. 

We ask WebDriverJS to look for elements that match the class rule <code>.new-todo</code> as we know that’s the class assigned to this field. We declare a constant as we cannot change the data that comes back &mdash; just query it. Note this will find the first element in the DOM that matches the CSS pattern which is fine in our case as we know there’s only one.

<pre><code class="language-javascript">const todoEntry = await browser.findElement(webdriver.By.css('.new-todo'));</code></pre>
</li>
<li>Next, we send keystrokes to the field we just got a handle to using the sendKeys function. We put the escaped enter key on its own await line to avoid race conditions. We use the <code>for (x of y)</code> iteration pattern as we’re dealing with promises. <code>toDoTestItems</code> is simply an array of 3 strings, one string variable (which we’ll test against later) and 2 literals. Under the covers, WebDriverJS will send individual characters of the string one at a time, but we just pass the whole string variable to <code>sendKeys</code>:</p>

<pre><code class="language-javascript">var toDoTestItems = [entrytoEdit, "Test Value1", "Test Value2"];
    //Send keystrokes to the field we just found with the test strings and then send the Enter special character
    for (const item of toDoTestItems) {
      await todoEntry.sendKeys(item);
      await todoEntry.sendKeys("\n");
    }
</code></pre>
</li>
</ol>

<p>At this point, let’s run the script with node and see if we see a browser that navigates to the page and enters those three test TODO items. Wrap the code after the first variable declaration in an <code>async</code> function like this:</p>

<pre><code class="language-javascript">async function run() {</code></pre>

<p>Close off the function <code>}</code> at the end of the code, then call that async function with:</p>

<pre><code class="language-javascript">run();</code></pre>

<p>Save your JS file. Go to the node command window, navigate to the folder you saved the JS file in and run <code>node yourfile.js</code></pre>

<p>You should see a browser window appear and the text sent to the TODOMVC file be entered as new TODO entries in the application. Congratulations &mdash; you’re up and running with WebDriverJS.</p>

<p>Try changing the URL that WebDriverJS loads in this example to one of the other TODOMVC samples and observe that the same test code can run against different frameworks.</p>

<pre><code class="language-javascript">await browser.get('https://todomvc.com/examples/vue/');</code></pre>

## Running Tests On BrowserStack

<p>We’ve shown how this test runs locally on your machine. The same test can run just as easily using online test services like BrowserStack. Sign up for free access to the BrowserStack service to get access to Microsoft Edge browsers for free live and automated testing. Once signed in, go to the "Automate" section and look up your automated test account settings. You’ll need to pass these to the WebDriverJS function to sign in via code, name your test session and pass in your access token.</p>

<p>Then simply add those values into the <code>capabilities </code>variable and call the WebDriver builder again.</p>

<pre><code class="language-javascript">var capabilities = {
    'browserName': MicrosoftEdge,
    'browserstack.user': 'yourusername’,
    'browserstack.key': 'yqniJ4quDL6s2Ak2EZpe',
    'browserstack.debug': 'true',
    'build': 'Name your test'
  }
</code></pre>

<p>You can learn more about the <code>capabilities</code> variable and <a href="https://www.browserstack.com/automate/capabilities">values BrowserStack can accept here</a>.</p>

<p>Then call the <code>builder</code> function and pass in the BrowserStack server URL:</p>

<pre><code class="language-javascript">var browser = new webdriver.Builder().
    usingServer('https://hub-cloud.browserstack.com/wd/hub').
    withCapabilities(capabilities).
    build();
</code></pre>

<p>Finally, you should instruct WebDriverJS to quit the browser or else it will stay running and eventually time out. Place a call to the quit function at the end of your test file.</p>

<pre><code class="language-javascript">browser.quit();</code></pre>

<p>Now when you run your JS test file using NodeJS, you’ll be sending the test instructions to a browser hosted on BrowserStack’s cloud service. You can go to the "Automate" section of BrowserStack and observe the test jobs starting and stopping. Once complete, you can browse through the WebDriver commands that were sent, see images of the browser screen at intervals during the test run and even see a video of the browser session.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91f81b9d-c852-4ef0-8c58-e6eddce39952/pic3.png" sizes="100vw" caption="A screenshot of the visual log feature of a test run on BrowserStack’s Automate service" alt="A screenshot of the visual log feature of a test run on BrowserStack’s Automate service" >}}

## Testing Values With Assertions

<p>When testing your site, you are comparing actual results with expected results. The best way to do that is through assertions where an exception will be thrown if an assert condition is not met. In our example, we use an assertion library to express those assertions and help make the code more readable. We chose <a href="https://chaijs.com/">ChaiJS</a> as its flexible enough to be used with any JavaScript library and is quite popular as of the time of writing.</p>

<p>You download and install Chai as a node package using npm. In code, you need to require <code>chai</code>:</p>

<pre><code class="language-javascript">var expect = require('chai').expect;</code></pre>

<p>We decided to use the <a href="https://chaijs.com/guide/styles/#expect">Expect interface</a> to use natural language to chain together our assertions.</p>

<p>You can test for length, existence, contains a value, and many more.</p>

<pre><code class="language-javascript">expect(testElements).to.not.have.lengthOf(0);
  //make sure that we're comparing the right number of items in each array/collection
  expect(testElements.length).to.equal(toDoTestItems.length);
</code></pre>

<p>Should one of these assertions not be true, an assertion exception is thrown.  Our sample code will stop executing when the exception is thrown as we’re not handling the exception. In practice, you’ll use a test runner with node that will handle the exceptions and report out test errors and passes.</p>

## Automating Test Passes With A Test Runner

<p>To better handle the assertion exceptions, a test runner is paired with node to wrap code blocks containing test assertions in try/catch-style functions that map the exceptions to failed test cases.</p>

<p>In this example, we chose the <a href="https://mochajs.org/">MochaJS</a> test framework as it pairs well with Chai and is something we use to test our production code.</p>

<p>To integrate the runner, there is both code added to the test script and a change in the way you run the code with node.</p>

### Adding Test Runner Code

<p>You wrap test code into async functions with the top level function using the keyword “describe” and the subtest function using keyword “it.” The functions are marked up with a description of what the tests are looking for. This description is what will be mapped to test results.</p>

<p>MochaJS is installed as a node package via npm.</p>

<p>Here’s the top-level function in our sample using <code>describe</code>:</p>

<pre><code class="language-javascript">describe('Run four tests against TODOMVC sample', async () => {</code></pre>

<p>Subsequently, wrap your logical tests into groups with the <code>it</code> keyword:</p>

<pre><code class="language-javascript">it('TEST 3: Delete a TODO item from the list by clicking the X button', async () => {</code></pre>

<p>Assertions wrapped within these functions that cause an exception will be mapped back to these descriptions.</p>

### Executing The Code With NodeJS And MochaJS

<p>Finally, you need to run your test code with node calling the MochaJS binary to handle the exceptions correctly. Mocha can be passed arguments to configure timeout values, the folder to look for that holds your test files and more. Here’s the configuration we used for Visual Studio Code to attach the debugger and use Code’s inspection and step through features:</p>

<pre><code class="language-javascript">{
            "type": "node",
            "request": "launch",
            "name": "Mocha Tests",
            "program": "${workspaceRoot}/node_modules/mocha/bin/_mocha",
            "args": [
                "-u",
                "tdd",
                "--timeout",
                "999999",
                "--colors",
                "${workspaceRoot}/test/**/*.js"
            ],
            "internalConsoleOptions": "openOnSessionStart"
        }
</code></pre>

<p>Automated testing is a great way to ensure your site works across a variety of browsers consistently without the hassle or cost of testing manually. The tools we’ve used here are just a few of the many choices available but illustrate the common steps involved in setting up and executing automated tests for your projects.</p>

{{< signature "rb, ra, yk, il" >}}

