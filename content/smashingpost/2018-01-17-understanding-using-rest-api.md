---
title: 'Understanding And Using REST APIs'
slug: understanding-using-rest-api
author: zellliew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7681a34-e325-454a-b492-2759b93f7f99/understanding-api-github-root-opt.png
date: 2018-01-17T10:01:38+01:00
summary: >-
  If you want to be able to read API documentations and use them effectively, you’ll first need to understand everything about REST APIs. Let’s get started.
description: >-
  Everything you need to know about REST APIs, from start to finish. How and why to use REST APIs, how to deal with headers, error messages and API versions. Let’s get started.
categories:
  - API
  - REST API
  - JavaScript
last_updated: 2021-05-20T11:30:00.000Z
---
There’s a high chance you came across the term "REST API" if you’ve thought about getting data from another source on the internet, such as Twitter or Github. But what is a REST API? What can it do for you? How do you use it?

In this article, you’ll learn everything you need to know about REST APIs to be able to read API documentations and use them effectively.

{{< refs >}}
    <h4 style="margin-top: 1.25em">Part Of: Rest API &amp; GraphQL</h4>
    <ul>
    <li><strong>Understanding And Using REST APIs</strong></li>
    <li><a href="https://www.smashingmagazine.com/2020/06/rest-api-react-fetch-axios/">Consuming REST APIs In React With Fetch And Axios</a></li>
    <li><a href="https://www.smashingmagazine.com/2018/01/graphql-primer-new-api-part-1/">A GraphQL Primer: Why We Need A New Kind Of API (Part 1)</a></li>
    <li><a href="https://www.smashingmagazine.com/2018/01/graphql-primer-new-api-part-2/">A GraphQL Primer: The Evolution Of API Design (Part 2)</a></li>
    <li><a href="https://www.smashingmagazine.com/2019/01/introducing-component-based-api/">Introducing The Component-Based API</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>
{{< /refs >}}

## What Is A REST API

Let’s say you’re trying to find videos about Batman on Youtube. You open up Youtube, type "Batman" into a search field, hit enter, and you see a list of videos about Batman. A REST API works in a similar way. You search for something, and you get a list of results back from the service you’re requesting from.

An **API** is an application programming interface. It is a set of rules that allow programs to talk to each other. The developer creates the API on the server and allows the client to talk to it.

**REST** determines how the API looks like. It stands for "Representational State Transfer". It is a set of rules that developers follow when they create their API. One of these rules states that you should be able to get a piece of data (called a resource) when you link to a specific URL.

Each URL is called a **request** while the data sent back to you is called a **response**.

## The Anatomy Of A Request

It’s important to know that a request is made up of four things:

1. The endpoint
2. The method
3. The headers
4. The data (or body)

**The endpoint** (or route) is the url you request for. It follows this structure:

<pre><code class="language-bash">root-endpoint/<path>?<query-params>
</code></pre>

The **root-endpoint** is the starting point of the API you’re requesting from. The root-endpoint of [Github’s API](https://developer.github.com/v3/) is `https://api.github.com` while the root-endpoint [Twitter’s API](https://dev.twitter.com/rest/reference) is `https://api.twitter.com`.

The **path** determines the resource you’re requesting for. Think of it like an automatic answering machine that asks you to press 1 for a service, press 2 for another service, 3 for yet another service and so on.

{{% feature-panel %}}

You can access paths just like you can link to parts of a website. For example, to get a list of all posts tagged under "JavaScript" on Smashing Magazine, you navigate to `https://www.smashingmagazine.com/tag/javascript/`. `https://www.smashingmagazine.com/` is the root-endpoint and `/tag/javascript` is the path.

To understand what paths are available to you, you need to look through the API documentation.
For example, let’s say you want to get a list of repositories by a certain user through Github’s API. The [docs](https://developer.github.com/v3/repos/#list-user-repositories) tells you to use the the following path to do so:

<pre><code class="language-bash">/users/:username/repos
</code></pre>

Any colons (`:`) on a path denotes a variable. You should replace these values with actual values of when you send your request. In this case, you should replace `:username` with the actual username of the user you’re searching for. If I’m searching for my Github account, I’ll replace `:username` with `zellwk`.

The endpoint to get a list of my repos on Github is this:

<pre><code class="language-bash">https://api.github.com/users/zellwk/repos</code></pre>

The final part of an endpoint is **query parameters**. Technically, query parameters are not part of the REST architecture, but you’ll see lots of APIs use them. So, to help you completely understand how to read and use API’s we’re also going to talk about them.
Query parameters give you the option to modify your request with key-value pairs. They always begin with a question mark (`?`). Each parameter pair is then separated with an ampersand (`&`), like this:

<div class="break-out">

<pre><code class="language-bash">?query1=value1&query2=value2
</code></pre></div>

When you try to get a list of a user’s repositories on Github, you add three possible parameters to your request to modify the results given to you:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c119c0b2-4ded-42d0-90f0-496b14bf5e1f/understanding-api-doc-github-repo-opt.png" sizes="100vw" caption="Github let’s you add three parameters to your request" alt="An image that shows Github’s API for a user’s repositories" >}}

If you'd like to get a list the repositories that I pushed to recently, you can set `sort` to `push`.

<pre><code class="language-markup">https://api.github.com/users/zellwk/repos?sort=pushed
</code></pre>

How do you know if this endpoint works? Well, it’s time to give it a try!

## Testing Endpoints With curl

You can send a request with any programming language. JavaScript users can use methods like the [Fetch API](https://css-tricks.com/using-fetch/) and [jQuery’s Ajax method](https://api.jquery.com/jquery.ajax/); Ruby users can use [Ruby’s Net::HTTP class](https://ruby-doc.org/stdlib-2.4.2/libdoc/net/http/rdoc/index.html), Python users can use [Python Requests](https://docs.python-requests.org/en/master/); and so on.

For this article, we’ll use the command line utility called [cURL](https://curl.haxx.se). We use cURL because API documentations are normally written with reference to cURL. If you understand how to use cURL, you’ll have no problems understanding API documentations. Then, you can easily perform requests with your preferred language.

Before you continue, you’ll want to make sure you have cURL installed on your machine. Open up your Terminal and type `curl -version`. This command checks the version of cURL you have installed on your system.

<pre><code class="language-markup">curl --version
</code></pre>

If you don’t have cURL installed, you’ll get a "command not found" error. If you get this error, you will need to [install curl](https://curl.haxx.se/download.html) before moving on.

To use cURL, you type `curl`, followed by the endpoint you’re requesting for. For example, to get Github’s root endpoint, you type the following:

<div class="break-out">

<pre><code class="language-markup">curl https://api.github.com
</code></pre></div>

Once you hit enter, you should get a response from Github that looks like this:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7681a34-e325-454a-b492-2759b93f7f99/understanding-api-github-root-opt.png" sizes="100vw" caption="Response from Github’s root-endpoint" alt="An image that shows a response from Github’s root-endpoint" >}}

To get a list of a user’s repositories, you modify the endpoint to the correct path, like what we discussed above. To get a list of my repositories, you can use this command:

<div class="break-out">

<pre><code class="language-markup">curl https://api.github.com/users/zellwk/repos</code></pre></div>

If you wish to include query parameters with cURL, make sure you prepend a backslash (`\`) before the `?` and `=` characters. This is because `?` and `=` are special characters in the command line. You need to use `\` before them for the command line to interpret them as normal characters:

<div class="break-out">

<pre><code class="language-markup">curl https://api.github.com/users/zellwk/repos\?sort\=pushed
</code></pre></div>

Try using either commands and perform a request! You’ll get a similar response to what you’ve seen with Github’s root-endpont (but with a lot more data).

## JSON

JSON (JavaScript Object Notation) a common format for sending and requesting data through a REST API. The response that Github sends back to you is also formatted as JSON.

A JSON object looks like a JavaScript Object. In JSON, each property and value must be wrapped with double quotation marks, like this:

<pre><code class="language-json">{
  "property1": "value1",
  "property2": "value2",
  "property3": "value3"
}
</code></pre>

## Back To The Anatomy Of A Request

You’ve learned that a request consists of four parts.

1. The endpoint
2. The method
3. The headers
4. The data (or body)

Let’s go through the rest of what makes up a request.

**The Method**

The method is the type of request you send to the server. You can choose from these five types below:

- `GET`
- `POST`
- `PUT`
- `PATCH`
- `DELETE`

These methods provide meaning for the request you’re making. They are used to perform four possible actions: `Create`, `Read`, `Update` and `Delete` (CRUD).

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
  <tr>
    <th data-tablesaw-priority="persist">Method Name</th>
    <th>Request Meaning</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>`GET`</td>
    <td>This request is used to get a resource from a server. If you perform a `GET` request, the server looks for the data you requested and sends it back to you. In other words, a `GET` request performs a `READ` operation. This is the default request method.</td>
  </tr>
  <tr>
    <td>`POST`</td>
    <td>This request is used to create a new resource on a server. If you perform a `POST` request, the server creates a new entry in the database and tells you whether the creation is successful. In other words, a `POST` request performs an `CREATE` operation.</td>
  </tr>
  <tr>
    <td>`PUT` and `PATCH`</td>
    <td>These two requests are used to update a resource on a server. If you perform a `PUT` or `PATCH` request, the server updates an entry in the database and tells you whether the update is successful. In other words, a `PUT` or `PATCH` request performs an `UPDATE` operation.</td>
  </tr>
  <tr>
    <td>`DELETE`</td>
    <td>This request is used to delete a resource from a server. If you perform a `DELETE` request, the server deletes an entry in the database and tells you whether the deletion is successful. In other words, a `DELETE` request performs a `DELETE` operation.</td>
  </tr>
</tbody>
</table>

The API lets you know what request method to use each request. For example, to get a list of a user’s repositories, you need a `GET` request:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d1a8b7-51ef-45d2-a416-b34d7c76abda/understanding-api-doc-github-repo-get-opt.png" sizes="100vw" caption="A GET request is required to get a list of repositories from a user" alt="An example GET request on Github" >}}

A GET request is required to get a list of repositories from a user. To [create a new Github repository](https://developer.github.com/v3/repos/#create), you need a `POST` request:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f809fa89-47a5-439d-9360-2a9981264c3c/understanding-api-doc-github-repo-create-opt.png" sizes="100vw" caption="A POST request is required to create a new repository" alt="A POST request is required to create a new repository" >}}

You can set the request method in cURL by writing `-X` or `--request`, followed by the request method. This command below tries to create a repository via cURL:

<div class="break-out">

<pre><code class="language-bash">curl -X POST https://api.github.com/user/repos
</code></pre></div>

Try running this request. You’ll get a response that tells you that authentication is required. (More on authentication later).

<div class="break-out">

<pre><code class="language-bash">{
  "message": "Requires authentication",
  "documentation_url": "https://developer.github.com/v3"
}
</code></pre></div>

**The Headers**

Headers are used to provide information to both the client and server. It can be used for many purposes, such as authentication and providing information about the body content. You can find a list of valid headers on MDN’s [HTTP Headers Reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).

**HTTP Headers are property-value pairs** that are separated by a colon. The example below shows a header that tells the server to expect JSON content.

<div class="break-out">

<pre><code class="language-bash">"Content-Type: application/json". Missing the opening ".
</code></pre></div>

You can send HTTP headers with curl through the `-H` or `--header` option. To send the above header to Github’s API, you use this command:

<div class="break-out">

<pre><code class="language-bash">curl -H "Content-Type: application/json" https://api.github.com</code></pre></div>

(Note: the Content-Type header is not a requirement for Github’s API to work. This is only an example to illustrate how to use a header with cURL).

To view headers you’ve sent, you can use the `-v` or `--verbose` option as you send the request, like this:

<div class="break-out">

<pre><code class="language-bash">curl -H "Content-Type: application/json" https://api.github.com -v
</code></pre></div>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32443654-68fc-4b26-9d03-9eef0c202f57/understanding-api-github-root-v-opt.png" sizes="100vw" caption="cURL tells you additional information, which includes headers when you use the verbose option" alt="An image that shows the response from Github’s root endpoint with the verbose option" >}}

Here, `*` refers to additional information provided by cURL. `>` refers to request headers, and `<` refers to the response headers.

**The Data (Or "Body")**

The data (sometimes called "body" or "message") contains information you want to be sent to the server. This option is only used with `POST`, `PUT`, `PATCH` or `DELETE` requests.

To send data through cURL, you can use the `-d` or `--data` option:

<div class="break-out">

<pre><code class="language-bash">curl -X POST &lt;URL&gt; -d property1=value1
</code></pre></div>

To send multiple data fields, you can create multiple `-d` options:

<div class="break-out">

<pre><code class="language-bash">curl -X POST &lt;URL&gt; -d property1=value1 -d property2=value2
</code></pre></div>

If it makes sense, you can break your request into multiple lines `\` to make it easier to read:

<div class="break-out">

<pre><code class="language-bash">curl -X POST &lt;URL&gt; \
  -d property1=value1 \
  -d property2=value2
</code></pre></div>

If you know how to spin up a server, you can make an API and test your own data. If you don’t know, but feel courageous enough to try, you can follow [this article](https://zellwk.com/blog/crud-express-mongodb/) to learn to create a server with Node, Express, and MongoDB

If you don’t want to spin up your server, you can go to [Requestbin.com](https://requestbin.com/) (*it’s free!*) and click on the “create endpoint”. You’ll be given a URL that you can use to test requests, like `https://requestb.in/1ix963n1` shown in the picture below.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d313545-fd55-4a81-bcde-48cef1a5b74f/understanding-api-request-bin-url-opt.png" sizes="100vw" caption="Request bin gives you a unique URL you can use for 48 hours" alt="Example of a Request Bin URL" >}}

Make sure you create your own request bin if you want to test your request. Request bins only remains open for 48 hours after its creation. By the time you read this article, the bin I created above will be long gone.

Now, try sending some data to your request bin, then refresh your bin’s webpage. You’ll see some data, like this:

<div class="break-out">

<pre><code class="language-bash">curl -X POST https://requestb.in/1ix963n1 \
  -d property1=value1 \
  -d property2=value2
</code></pre></div>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f709c301-9b18-422f-aef2-9be74daca789/understanding-api-request-bin-form-opt.png" sizes="100vw" caption="Requests you sent to your bin will appear like this" alt="Results of a request sent to the Request Bin URL" >}}

By default, cURL sends data as if they’re sent through "form fields" on a page. If you wish to send JSON data, you’ll need to set the `Content-Type` to `application/json`, and you’ll need to format your data as a JSON object, like this:

<div class="break-out">

<pre><code class="language-bash">curl -X POST https://requestb.in/1ix963n1 \
  -H "Content-Type: application/json" \
  -d '{
  "property1":"value1",
  "property2":"value2"
}'
</code></pre></div>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7660eb4f-8b85-40e9-9285-27ad46d492c3/understanding-api-request-bin-json-opt.png" sizes="100vw" caption="Sending data as JSON" alt="Example of a JSON Response on Request Bin" >}}

And that is (almost!) everything you need to know about the structure of a request.

Now, remember when you tried to send a `POST` request through Github’s API, you got a message that says "Requires authentication"? Well, that’s because you’re not authorized to perform the `POST` request!

## Authentication

You wouldn’t allow anyone to access your bank account without your permission, would you? On the same line of thought, developers put measures in place to ensure you perform actions only when you’re authorized to do. This prevents others from impersonating you.

Since `POST`, `PUT`, `PATCH` and `DELETE` requests alter the database, developers almost always put them behind an authentication wall. In some cases, a `GET` request also requires authentication (like when you access your bank account to check your current balance, for example).

On the web, there are two main ways to authenticate yourself:

1. With a username and password (also called basic authentication)
2. With a secret token

The secret token method includes [oAuth](https://oauth.net), which lets you to authenticate yourself with social media networks like Github, Google, Twitter, Facebook, etc.

For this article, you’ll only learn to use basic authentication with a username and a password. If you’re interested in authenticating with oAuth, I suggest reading "[What You Need To Know About OAuth2 And Logging In With Facebook](https://www.smashingmagazine.com/2017/05/oauth2-logging-in-facebook/)" by [Zack Grossbart](https://www.smashingmagazine.com/author/zack-grossbart/).

To perform a basic authentication with cURL, you can use the `-u` option, followed by your username and password, like this:

<div class="break-out">

<pre><code class="language-bash">curl -x POST -u "username:password" https://api.github.com/user/repos
</code></pre></div>

Try authenticating yourself with your username and password in the above request. Once you succeed in authentication, you’ll see the response change from "Requires authentication" to "Problems parsing JSON."

This is because you’ve yet to provide any data (which is required by all `POST`, `PUT`, `PATCH` and `DELETE` requests) to the server.

With the knowledge you’ve learned so far, you should be able to edit the code above to create a Github repository via your cURL. I'd leave you to try it yourself!

Now, let’s talk about HTTP Status codes and error messages.

## HTTP Status Codes And Error Messages

Some of the messages you’ve received earlier, like "Requires authentication" and "Problems parsing JSON" are error messages. They only appear when something is wrong with your request.
HTTP status codes let you tell the status of the response quickly. The range from 100+ to 500+. In general, the numbers follow the following rules:

1. **200+** means the request has **succeeded**.
2. **300+** means the request is **redirected** to another URL
3. **400+** means an **error that originates from the client** has occurred
4. **500+** means an **error that originates from the server** has occurred

You can debug the status of a response with the verbose option (`-v` or `--verbose`) or the head option (`-I` or `--head`).

For example, if you tried adding `-I` to a `POST` request without providing your username and password, you’ll get a 401 status code (Unauthorized):

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6719e654-f45a-4629-a143-1b403cc76063/understanding-api-http-401-opt.png" sizes="100vw" caption="Example of an unauthorized request" alt="Example of an unauthorized request" >}}

If your request is invalid because your data is wrong or missing, you usually get a 400 status code (Bad Request).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/560b86fa-2db7-48f8-b918-3a16a521c357/understanding-api-http-400-opt.png" sizes="100vw" caption="Example of a bad request" alt="Example of a bad request" >}}

To get more information about specific HTTP status codes, you may want to consult MDN’s [HTTP Status Reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

## API Versions

Developers update their APIs from time to time. Sometimes, the API can change so much that the developer decides to upgrade their API to another version. If this happens, and your application breaks, it’s usually because you’ve written code for an older API, but your request points to the newer API.

You can request for a specific API version in two ways. Which way you choose depends on how the API is written.

These two ways are:

1. Directly in the endpoint
2. In a request header

Twitter, for example, uses the first method. At the time of writing, Twitter’s API is at version 1.1, which is evident through its endpoint:

<div class="break-out">

<pre><code class="language-bash">https://api.twitter.com/1.1/account/settings.json
</code></pre></div>

Github, on the other hand, uses the second method. At the time of writing, Github’s API is at version 3, and you can specify the version with an `Accept` header:

<div class="break-out">

<pre><code class="language-bash">curl https://api.github.com -H Accept:application/vnd.github.v3+json
</code></pre></div>

## Wrapping Up

In this article, you learned what a REST API is and how to use cURL to perform a request with `GET`, `POST`, `PUT`, `PATCH` and `DELETE` methods. In addition, you also learned how to authenticate your requests with the `-u` option, and what HTTP statuses mean.

I hope this article has helped you learn enough about REST APIs, and you can use them fluently as you create your applications. Feel free to pop over to my [blog](https://zellwk.com/newsletter/smashing-magazine) or leave your comments below if you have any questions.

{{< signature "rb, ra, il" >}}

