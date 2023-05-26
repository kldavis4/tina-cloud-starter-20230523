---
title: 'Modifying Headers In HTTP(s) Requests In UI Automation Testing'
slug: headers-https-requests-ui-automation-testing
author: nafees-nehar
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8590d77e-8181-4d36-9e2e-d4e9c76a893a/headers-https-requests-ui-automation-testing.jpg
date: 2021-12-14T10:30:00.000Z
summary: >-
  To be able to modify headers in a testing environment is a great thing to have. It allows control over your application as one can bypass authentication, set cookies, and so on. In this article, Nafees Nehar explores some methods which allow modification of headers in an automation testing setup.
description: >-
  To be able to modify headers in a testing environment is a great thing to have. It allows control over your application as one can bypass authentication, set cookies, and so on. In this article, Nafees Nehar explores some methods which allow modification of headers in an automation testing setup.
categories:
  - UI
  - Testing
  - Apps
  - HTTPS
  - Techniques
---

There are various methods to modify headers. You can modify headers by using browser extensions or proxy apps (such as Charles and Proxyman) that intercept the request and let you modify the response by including the headers.

But first, let’s start at the beginning.

## What Are HTTP(s) Headers?

[HTTP(s) Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) are key-value pairs that can be used by the client or server to pass additional information along with an HTTP(s) request or response. They hold additional information about the data being sent. An HTTP(s) header consists of a case-insensitive name followed by a colon (`:`), then by its value. Field names are case insensitive but field values are case sensitive. A header can have multiple values which are separated by commas.

## Modifying Headers: How Can This Be Helpful?

I was working on an application that opened the provided webpage and then give the user an option to modify elements, add events, add analytics, and so on. without any need to code. This was being done by loading the page in `iframe` and giving various options to the user on top of it. I tried with loads of websites to see how they behave in `iframe`. I observed that most of the websites don’t work in `iframe` due to `x-frame-options` and `content-security-policy` headers.

Almost all websites have a header `X-frame-options` set to `deny` or `sameorigin` due to which the browser does not allow to load the webpage in an `iframe` or doesn’t when any cross-origin request tries to load it in an `iframe`. Also, the `content-security-policy` header has `frame-ancestors` directive which prevents this.

It was very important to load the page in `iframe`, I was wandering around the internet to find a way to load it. It was evident that I needed to override the `X-frame-options` header to `allowall` or remove it altogether. That was when I stumbled upon `Requestly` extension which gave me the feature to modify the `X-frame-options` header by matching the page URL and hence allowing me to override the `X-frame-options` header when debugging.

That was when I first got to witness the power of network headers. They carry data about the data being transferred. The ability to modify the headers of traffic that pass through your browser is a great tool to have. Besides overriding `X-frame-options`, you can delete headers to minimize online tracking, override `content-security-policy` header, test sites in production, and so on.

While testing web applications, modifying headers provides a great hack:

- to test the guest mode of an application;
- can set cookies using headers;
- to test certain parts of an application that are by default disabled and can be enabled by passing a custom request header;
- to test different test cases associated with headers;
- to bypass authentication flow in your application by passing the authorization header.

When I got to know about the automated testing of web apps, it occurred to me that modifying headers should be a feature there due to its immense applicability in web app testing. Therefore I decided to write this piece to throw some light on the ways to modify headers in automated testing.

{{% feature-panel %}}

## Selenium

Selenium is widely used as a test automation framework for end-to-end testing of web applications. It was developed in 2004. Initially, Selenium IDE was being used but it only supported firefox then Selenium RC was developed to enable cross-browser testing. Now the Selenium WebDriver is being used as it provides support for the mobile experience and dynamic websites. It mimics a real user interacting with the webpage.

### Advantages Of Using Selenium WebDriver

- Selenium WebDriver is open source;
- It offers bindings for every major programming language;
- Works across multiple OS. Test written in Windows would easily work on Mac;
- Keyboard and cursor simulation are supported;
- Add-ons can be installed.

### Limitations Of Selenium WebDriver

- No support to modify headers;
- No support to add request parameters;
- Cannot block a request.

As discussed, the ability to modify headers helps tremendously in testing applications but the Selenium WebDriver doesn’t support it, and [they don’t plan to include it lately](https://github.com/seleniumhq/selenium-google-code-issue-archive/issues/141#issuecomment-191404986).

This article focuses on various approaches to modify headers in a Selenium automation setup.

## Approach 1: Selenium Wire (Python)

[Selenium Wire](https://github.com/wkeeling/selenium-wire) extends Selenium Python bindings to give you access to the underlying requests made by the browser. You author your code in the same way as you do with Selenium, but you get extra APIs for inspecting requests and responses and making changes to them on the fly.

It allows modifying requests and responses on the go using interceptors. It can also block requests, mock responses, add request parameters in the URL.

### Usage

#### Adding Request Headers

<pre><code class="language-javascript"># interceptor function intercepts the network request
# If one arg is provided, requests are intercepted
# and can be modified
def interceptor(request):
    request.headers['New-Header'] = 'Some Value'
# setting the driver's request_interceptor to equal
# the customised interceptor
driver.request_interceptor = interceptor
driver.get(&lt;URL_where_to_modify_the_header&gt;)

# All requests will now contain New-Header</code></pre>

Duplicate header names are permitted in an HTTP request, so before setting the replacement header you must first delete the existing header using `del` otherwise two headers of the same name will exist.

#### Adding Response Headers

<pre><code class="language-javascript"># A response interceptor takes two args which
# then allows to tinker with the response
def interceptor(request, response):  
    if request.url == 'https://server.com/some/path':
        response.headers['New-Header'] = 'Some Value'
driver.response_interceptor = interceptor
driver.get(&lt;URL_where_to_modify_the_header)

# Responses from https://server.com/some/path will now contain 
# the New-Header</code></pre>

A response interceptor should accept two arguments, [one for the originating request and one for the response](https://pypi.org/project/selenium-wire/#intercepting-requests-and-responses).

### Limitations

- This is only available as a Python module.
- It does not support other languages.

{{% ad-panel-leaderboard %}}

## Approach 2: Loading Browser Extension In Selenium Which Can Modify Headers

There are tools like [Requestly](https://requestly.io/) which is a one-stop tool to debug & modify network requests. Requestly allows users to Modify Headers, Redirect URLs, Switch hosts, Mock API response, Delay network requests, Insert custom scripts, etc. It provides ready to go npm package which is a wrapper around the extension enabling the use of extension in Selenium. It supports Chrome, Firefox and Edge.

### Using Requestly In Selenium

Requestly allows you to do a lot more things other than just modifying headers. All these things can be set up within a web interface and the shared list can be loaded into the application which allows the user’s flexibility to edit the rules easily in a web application.

**To Install: `npm i @requestly/selenium`**

### Usage

A Modify Headers Rule can be created at [app.requestly.io/rules](https://app.requestly.io/rules) after installing the extension.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d7717e3-3b0e-4104-b8c8-4675e91267a4/1-headers-https-requests-ui-automation-testing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d7717e3-3b0e-4104-b8c8-4675e91267a4/1-headers-https-requests-ui-automation-testing.png" width="800" height="165" sizes="100vw" caption="Adding a Header to all requests. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d7717e3-3b0e-4104-b8c8-4675e91267a4/1-headers-https-requests-ui-automation-testing.png'>Large preview</a>)" alt="Adding a Header to all requests" >}}

After creating the URL, click on the `Share` button to generate a link for the URL.

The URL for the above created `sharedList` is [here](https://app.requestly.io/rules/#sharedList/1626984924247-Adding-Headers-Example).

This URL is a Requestly rule which adds `Access-Control-Allow-Origin` header to all requests. 

This rule can be used in the Selenium WebDriver using the `sharedList` URL which is described below:

<div class="break-out">

<pre><code class="language-javascript">require("chromedriver");
const { Builder } = require("selenium-webdriver");
const chrome = require("selenium-webdriver/chrome");
const { getRequestlyExtension, importRequestlySharedList } = require("@requestly/selenium");

const options = new chrome.Options().addExtensions(getRequestlyExtension("chrome"));
const driver = new Builder()
    .forBrowser("chrome")
    .setChromeOptions(options)
    .build();

// Imports Rules in Selenium using Requestly sharedList feature
// importRequestlySharedList(driver, &lt;sharedList_URL&gt;);

importRequestlySharedList(driver, 'https://app.requestly.io/rules/#sharedList/1626984924247-Adding-Headers-Example');</code></pre>
</div>

More information can be found [here](https://www.npmjs.com/package/@requestly/selenium).

### Limitations

- It offers an npm package limiting the module to JavaScript only.
- Shared Lists have to be created manually to use the rules in Selenium, hence the rules cannot be controlled through the code written for the Selenium automation test.

## Approach 3: Using Puppeteer

[Puppeteer](https://www.npmjs.com/package/puppeteer) is a Node library developed by Google which provides a high-level API to control headless Chrome or Chromium over the DevTools Protocol. It can also be configured to use full (non-headless) Chrome or Chromium.

When talking about browser automation setup, Selenium automatically comes to the mind but since the advent of Puppeteer it is widely being used for web scraping. It offers more control over chrome than Selenium probably due to google’s support to it. Also due to the same reason, it rules out the need for an external driver to run the browser.

### Usage

<pre><code class="language-javascript">const puppeteer = require('puppeteer');

(async () =&gt; {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();
    await page.goto('&lt;https://example.com&gt;');
    await page.screenshot({ path: 'example.png' });
    await browser.close();
})();</code></pre>

### Modifying Headers

The `page.setExtraHTTPHeaders(headers)` method can be used to set headers.

It can also modify and remove existing headers. Once requests are intercepted using a combination of `page.setRequestInterception(true)` and `page.on()`.

<pre><code class="language-javascript">await page.setRequestInterception(true);
page.on('request', request => {
// Override headers
    const headers = Object.assign({}, request.headers(), {
    foo: 'bar', // set "foo" header
    origin: undefined, // remove "origin" header
});

request.continue({headers});

});</code></pre>

[*Code source*](https://github.com/puppeteer/puppeteer/blob/main/docs/api.md)

### Limitations

- Puppeteer is limited to chrome for now. It cannot be used for cross-browser testing.
- It has a smaller community compared to Selenium. There seems to be more support for Selenium in the community.
- It only supports JavaScript.

{{% ad-panel-leaderboard %}}

## Conclusion

Modifying network headers happens to be a very powerful tool in a testing environment. There’s a lot more to it than what can be covered in this article. I have tried to cover some of the simplest methods to modify headers in UI Automation Testing.

Every method has some advantages based on the use case and language you use. Here are some of the preferences:

- If you want to use Selenium in Python, prefer Selenium-Wire as it provided a lot of features on top of Selenium-Webdriver.
- If you want to test on only chrome, prefer puppeteer due to its google support and out-of-the-box support for all features including modifying headers.
- If you work with Selenium and want to do cross-browser testing, prefer adding extensions to emulate the testing in Selenium-Webdriver. If your use-case requires you to inject scripts or redirect network resources in runtime (in addition to modifying headers), then Requestly is an ideal choice.

Hope this article gives you insight on modifying headers in an automated web application testing setup.

### Further Resources

- [MDN Http Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [Selenium-Wire](https://pypi.org/project/selenium-wire/1.0.3)
- [Puppeteer](https://developers.google.com/web/tools/puppeteer)
- [Requestly-Selenium](https://github.com/requestly/requestly-selenium)
- [Requestly](https://docs.requestly.io/)

{{< signature "vf, yk, il" >}}
