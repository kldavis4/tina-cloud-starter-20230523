---
title: 'JavaScript APIs You Don’t Know About'
slug: javascript-api-guide
author: juan-diego-rodriguez
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b583db40-b8c0-46c4-9893-5a7ae3d00453/api-page-visibility-web-sharing-broadcast-channel-internationalization.jpg
date: 2022-09-14T10:00:00.000Z
summary: >-
  In this article, Juan Diego covers the least known yet extremely useful APIs, such as the Page Visibility API, Web Sharing API, Broadcast Channel API and Internationalization API. Together we will see what they are, where we should use them, and how to use them.
description: >-
  In this article, Juan Diego covers the least known yet extremely useful APIs, such as the Page Visibility API, Web Sharing API, Broadcast Channel API and Internationalization API. Together we will see what they are, where we should use them, and how to use them.
categories:
  - API
  - Apps
  - Tools
  - Guides
  - JavaScript
---

A couple of days ago, I revisited the awesome [2021 State of JS Survey](https://2021.stateofjs.com/en-US/). The state of JS is an online survey that collects data from developers around the world to see the most recent and upcoming trends in the JavaScript community. Among the data it collects, a section is dedicated to the native features JavaScript provides, listed by their usage and awareness. As you can imagine, among the most used features are popular ones like [Optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining), [Nullish coalescing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator), [Websockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API), and so on.

However, I wasn’t interested in the most used or known APIs. Instead, I was looking for the least known ones. I wanted to know which APIs we aren’t talking about enough, and among them, I found four pretty different APIs that are extremely useful:

- [Page Visibility API](#page-visibility-api)
- [Web Share API](#web-share-api)
- [Broadcast Channel API](#broadcast-channel-api)
- [Internationalization API](#internationalization-api)

In this article, we will see what they are, where we should use them, and how to use them.

**Note**: *[These APIs are all available in this demo](https://monknow.github.io/apis-you-didnt-know-about/).*

## Page Visibility API

This is a little-known web API that rates last fourth in awareness in the [State of JS Survey](https://2021.stateofjs.com/en-US/features). It lets you know when a user has left the page. To be precise, the API triggers an event whenever the page visibility status changes, either when the user minimizes or maximizes the window or switches the tab.

In the past, you had to use gimmicks to know if a user had switched tabs or minimized the window. The most popular was using the [`blur`](https://developer.mozilla.org/en-US/docs/Web/API/Element/blur_event) and [`focus`](https://developer.mozilla.org/en-US/docs/Web/API/Element/focus_event) browser events. Using these events would result in something like the following:

<pre><code class="language-javascript">window.addEventListener("focus", function () {
	// User is back on the page
	// Do Something
});

window.addEventListener("blur", function () {
	// User left the page
	// Do Something
});
</code></pre>

The previous code works but not as intended. Since the `blur` event is triggered when the page loses focus, it can be triggered when the user clicks the search bar, an alert dialog, the console, or the window border. So, `blur` and `focus` only tell us if the page is active but not if the content of the page is hidden or visible.

### Use Cases

In general, we want to use the Page Visibility API to stop unnecessary processes when the user doesn’t see the page or, on the other hand, to perform background actions. Some specific cases can be:

-   to pause videos, image carousels, or animations when the user leaves the page;
-   if the page displays live data from an API, stop this behavior temporarily while the user is away;
-   to send user analytics.

### How To Use It?

The Page Visibility API brings two properties and an event to access the page visibility status:

-   `document.hidden`  
    It is globally available and read-only. Try to avoid it since it is now deprecated, but when accessed, it returns `true` if the page is hidden and `false` if it is visible.
-   `document.visibilityState`  
    It is the updated version of `document.hidden`, but when accessed, it returns four possible values depending on the page visibility status: - `visible`  
     The page is visible, or to be exact, it isn’t minimized nor in another tab. - `hidden`  
     The page isn’t visible; it is minimized or in another tab. - `prerender`  
     This is the initial state of a visible page when it is prerendering. A page’s visibility status may start at `prerender` and then change to another state, but it can’t change from another state to `prerender`. - `unloaded`  
     The page is being unloaded from memory.
-   `visibilitychange`  
    It’s an event provided by the `document` object that is triggered when the page `visibilityState` changes.

<pre><code class="language-javascript">document.addEventListener("visibilitychange", () =&gt; {
	if (document.visibilityState === "visible") {
		// page is visible
	} else {
		// page is hidden
	}
});
</code></pre>

To see how to use the Page Visibility API, let’s use it to pause a video and stop fetching resources from an API when the user leaves the page. To start, I will be using [vite.js](https://vitejs.dev/guide/#scaffolding-your-first-vite-project), which is an amazing tool to start a new project quickly:

<pre><code class="language-bash">npm create vite@latest unknown-web-apis</code></pre>

When asked to select a framework, select vanilla to create a vanilla javascript project. And once finished, go to the new folder, install the necessary `npm` packages and start the developer server:

<pre><code class="language-bash">  cd unknown-web-apis
  npm install
  npm run dev</code></pre>

Go to [localhost:3000/](http://localhost:3000/), and you will see your Vite project up and running!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af373d72-bc9b-49c5-994d-a92fb1e781f1/vite-new-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af373d72-bc9b-49c5-994d-a92fb1e781f1/vite-new-project.png" width="800" height="362" sizes="100vw" caption="Vite New Project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af373d72-bc9b-49c5-994d-a92fb1e781f1/vite-new-project.png'>Large preview</a>)" alt="Vite New Project" >}}

Firstly, we will direct to the `/main.js` file and delete all the boilerplate. Secondly, we will open `/index.html`, and inside the `#app` div tag, we will add a video element with any video file you want. I used a dancing Yoshi one. :)

<pre><code class="language-html">&lt;div id="app"&gt;
	&lt;video controls id="video"&gt;
		&lt;source src="./yoshi.mp4" /&gt;
	&lt;/video&gt;
&lt;/div&gt;</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/526008ab-f9d4-4deb-b384-2a5d74709b96/yoshi-screenshot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/526008ab-f9d4-4deb-b384-2a5d74709b96/yoshi-screenshot.png" width="800" height="447" sizes="100vw" caption="Video with controls showing a Yoshi image. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/526008ab-f9d4-4deb-b384-2a5d74709b96/yoshi-screenshot.png'>Large preview</a>)" alt="Video with controls showing a Yoshi image" >}}

Back to `/main.js`, we will add an event listener to the `document` object listening to the `visibilitychange` event. We then can access the `document.visibilityState` property to see when the page is visible or hidden.

<pre><code class="language-javascript">document.addEventListener("visibilitychange", () =&gt; {
	console.log(document.visibilityState);
});</code></pre>

You can go to the page’s console and see the page visibility status change when you minimize the window or switch to another tab. Now, inside the event listener, we can check the `document.visibilityState` property, pause the video when it is `hidden`, and play it when `visible`. (Of course, we first select the `video` element using [`document.querySelector()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector).)

<pre><code class="language-javascript">const video = document.querySelector("#video");

document.addEventListener("visibilitychange", () =&gt; {
	if (document.visibilityState === "visible") {
		video.play();
	} else {
		video.pause();
	}
});</code></pre>

Now the video stops whenever the user leaves the page. Another use of the Page Visibility API is to stop fetching unnecessary resources when the user doesn’t see the page. To see this, we will write a function to constantly fetch a random quote from the [quotable.io](https://github.com/lukePeavey/quotable) API and pause this behavior when the page is hidden. Firstly, we will create a new div tag to store the quote in `/index.html`.

<pre><code class="language-html">&lt;div id="app"&gt;
	&lt;video controls id="video"&gt;
		&lt;source src="./yoshi.mp4" /&gt;
	&lt;/video&gt;
	&lt;div id="quote"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

Back in `/main.js`, we will use the [**Fetch API**](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to make a call to the `quotable.io` endpoint [https://api.quotable.io/random](https://api.quotable.io/random) and then insert it into the `quote` div.

<div class="break-out">

<pre><code class="language-javascript">const quote = document.querySelector("#quote");

const getQuote = async () =&gt; {
try {
const response = await fetch("https://api.quotable.io/random");
const {content, author, dateAdded} = await response.json();
const parsedQuote = ` &lt;q&gt;${content}&lt;/q&gt; &lt;br&gt; &lt;p&gt;- ${author}&lt;/p&gt;&lt;br&gt; &lt;p&gt;Added on ${dateAdded}&lt;/p&gt;`;
quote.innerHTML = parsedQuote;
} catch (error) {
console.error(error);
}
};

getQuote();</code></pre>

</div>

Let’s shortly explain what is happening right here. We first select the `quote` element from the DOM. We then declare the `getQuote` function, which is an [`async` function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) that allows us to use the [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) keyword to wait until we fetch the data from the API. The data fetched is in JSON format, so we use the `await` keyword one more time to wait until the data is parsed into a JavaScript object. The `quotable.io` API gives us—among other things—the `content`, `author`, and `dateAdded` properties that we will inject and display into the `quote` div. This works, but the quote is only fetched once, so we can use [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/setInterval) to call the function every 10 seconds.

<div class="break-out">

<pre><code class="language-javascript">const quote = document.querySelector("#quote");

const getQuote = async () =&gt; {
try {
const response = await fetch("https://api.quotable.io/random");
const {content, author, dateAdded} = await response.json();
const parsedQuote = ` &lt;q&gt;${content}&lt;/q&gt; &lt;br&gt; &lt;p&gt;- ${author}&lt;/p&gt;&lt;br&gt; &lt;p&gt;Added on ${dateAdded}&lt;/p&gt;`;
quote.innerHTML = parsedQuote;
} catch (error) {
console.error(error);
}
};

getQuote();

setInterval(getQuote, 10000);</code></pre>

</div>

If the user minimizes the window or switches the tab, the page would still fetch the quotes, creating an unnecessary network load. To solve this, we can check if the page is visible before fetching a quote.

<div class="break-out">

<pre><code class="language-javascript">const getQuote = async () =&gt; {
	if (document.visibilityState === "visible") {
		try {
			const response = await fetch("https://api.quotable.io/random");
			const {content, author, dateAdded} = await response.json();
			const parsedQuote = `
			&lt;q&gt;${content}&lt;/q&gt; &lt;br&gt; 
			&lt;p&gt;- ${author}&lt;/p&gt;&lt;br&gt; 
			&lt;p&gt;Added on ${dateAdded}&lt;/p&gt;`;
			quote.innerHTML = parsedQuote;
		} catch (error) {
			console.error(error);
		}
	}
};

getQuote();

setInterval(getQuote, 10000);</code></pre>

</div>

Now, we will only fetch the quote if the page is visible to the user.

### Support

[Widely supported](https://caniuse.com/pagevisibility)

{{% feature-panel %}}

## Web Share API

### What Is It?

The **Web Share API** is also among the least-known APIs but is extremely useful. It lets you access the operative system’s native sharing mechanism, which is especially useful to mobile users. With this API, you can share text, links, and files without the need to create your own sharing mechanisms or use third-party ones.

### Use Cases

They are pretty self-explanatory. You can use it to share content from your page to social media or copy it to the user’s clipboard.

### How To Use It?

The Web Share API gives us two interfaces to access the user’s sharing system:

1.  `navigator.canShare()`  
    Accepts the data you want to share as an argument and returns a boolean argument depending on whether it is shareable.
2.  `navigator.share()`  
    Returns a promise that will resolve if the sharing is successful. It invokes the native sharing mechanism and accepts the data you want to share as an argument. Note that it can only be called if a user has pressed a link or button, i.e., it requires [**transient activation**](https://developer.mozilla.org/en-US/docs/Glossary/Transient_activation). The share data is an object that can have the following properties:


    -   `url`: URL to be shared,
    -   `text`: text to be shared,
    -   `title`: title to be shared,
    -   `files`: array of `File` objects representing files to be shared.

To see how to use this API, we will recycle our prior example and make an option to share our quotes using the Web Sharing API. To start, we first have to make a share button in `/index.html`:

<pre><code class="language-html">&lt;div id="app"&gt;
	&lt;video controls id="video"&gt;
		&lt;source src="./yoshi.mp4" /&gt;
	&lt;/video&gt;
	&lt;div id="quote"&gt;&lt;/div&gt;
	&lt;button type="button" id="share-button"&gt;Share Quote&lt;/button&gt;
&lt;/div&gt;</code></pre>

We direct to `/main.js` and select the share button from the DOM. Then, we create an `async` function to share the data we want.

<pre><code class="language-javascript">const shareButton = document.querySelector("#share-button");

const shareQuote = async (shareData) =&gt; {
	try {
		await navigator.share(shareData);
	} catch (error) {
		console.error(error);
	}
};</code></pre>

Now, we can add a click event listener to the `shareButton` element to callback the `shareQuote` function. Our `shareData.text` value will be the [`quote.textContent`](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) property and the `shareData.url` will be the page URL i.e the [`location.href`](https://developer.mozilla.org/en-US/docs/Web/API/Location/href) property.

<pre><code class="language-javascript">const shareButton = document.querySelector("#share-button");

const shareQuote = async (shareData) =&gt; {
	try {
		await navigator.share(shareData);
	} catch (error) {
		console.error(error);
	}
};

shareButton.addEventListener("click", () =&gt; {
	let shareData = {
		title: "A Beautiful Quote",
		text: quote.textContent,
		url: location.href,
	};

	shareQuote(shareData);
});</code></pre>

Now you can share your quotes with anyone through your native operative system. However, it is important to note that the Web Share API will only work if the context is secure, i.e., if the page is served over `https://` or `wss://` URLs.

### Support

[Poorly supported](https://caniuse.com/web-share)

{{% ad-panel-leaderboard %}}

## Broadcast Channel API

### What Is It?

Another API I want to talk about is the **Broadcast Channel API**. It allows browsing contexts to send and receive basic data from each other. Browsing contexts are elements like a tab, window, iframe, or anywhere a page can be displayed. Due to security reasons, communication between browsing contexts isn’t allowed unless they are of the same origin and use the Broadcast Channel API. For two browsing contexts to be of the same origin, they must share in their URL the same protocol (e.g. `http/https`), domain (e.g. `example.com`), and port (e.g. `:8080`).

### Use Cases

The Broadcast Channel API is generally used to keep a page’s state synced across different tabs and windows to enhance user experience or for security reasons. It can also be used to know when a service is finished in another tab or window. Some examples are:

-   Log a user in or out across all tabs.
-   Detect when an asset is uploaded and show it across all pages.
-   Instruct a service worker to do some background work.

### How To Use It?

The Broadcast Channel API involves a `BroadcastChannel` object that can be used to send messages to other contexts. Its constructor has only one argument: a string that will work as an identifier to connect to the channel from other contexts.

<pre><code class="language-javascript">const broadcast = new BroadcastChannel("new_channel");</code></pre>

Once we have created a `BroadcastChannel` object with the same identifier across two contexts, the new `BroadcastChannel` object will have two available methods to start communicating:

-   `BroadcastChannel.postMessage()` to send a message across all connected contexts. It takes any kind of object as its only argument so that you can send a wide variety of data.

<pre><code class="language-javascript">broadcast.postMessage("Example message");</code></pre>

-   `BroadcastChannel.close()` to close the channel and indicate to the browser that it won’t receive any more messages so it can collect them into the garbage.

To receive a message, the `BroadcastChannel` has a `message` event that we can listen to using an `addEventListener` or its `onmessage` property. The `message` event has a `data` property with the data sent and other properties to identify the context that sent the message, such as `origin`, `lastEventId`, `source`, and `ports`.

<pre><code class="language-javascript">broadcast.onmessage = ({data, origin}) =&gt; {
	console.log(`${origin} says ${data}`);
};</code></pre>

Let’s see how to use the Broadcast Channel API by using our prior example. Our goal would be to make another browsing context with the same origin and display the same quote in both contexts. To do this, we will create a new folder named `new-origin` with a new `/index.html` and `/main.js` files inside.

The `/new-origin/index.html` will be a new HTML boilerplate with a `#quote` div inside:

<div class="break-out">

<pre><code class="language-javascript">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
	&lt;head&gt;
		&lt;meta charset="UTF-8" /&gt;
		&lt;link rel="icon" type="image/svg+xml" href="../favicon.svg" /&gt;
		&lt;meta name="viewport" content="width=device-width, initial-scale=1.0" /&gt;
		&lt;title&gt;Vite App&lt;/title&gt;
	&lt;/head&gt;
	&lt;body&gt;
		&lt;div id="quote"&gt;&lt;/div&gt;
		&lt;script type="module" src="./main.js"&gt;&lt;/script&gt;
	&lt;/body&gt;
&lt;/html&gt;</code></pre>
</div>

In the `/new-origin/main.js` file, we will create a new broadcast channel and select the `#quote` element from the DOM:

<pre><code class="language-javascript">const broadcast = new BroadcastChannel("quote_channel");
const quote = document.querySelector("#quote");</code></pre>

And in our prior `/main.js` file, we will create a new `BroadcastChannel` object and connect it to the `"quote_channel"`. We will also modify the `getQuote` function to send the quote as a message to other contexts.

<div class="break-out">

<pre><code class="language-javascript">const broadcast = new BroadcastChannel("quote_channel");

//...

const getQuote = async () =&gt; {
try {
const response = await fetch("https://api.quotable.io/random");
const {content, author, dateAdded} = await response.json();
const parsedQuote = ` &lt;q&gt;${content}&lt;/q&gt; &lt;br&gt; &lt;p&gt;- ${author}&lt;/p&gt;&lt;br&gt; &lt;p&gt;Added on ${dateAdded}&lt;/p&gt;`;
quote.innerHTML = parsedQuote;
broadcast.postMessage(parsedQuote);
} catch (error) {
console.error(error);
}
};</code></pre>

</div>

Back in the `/new-origin/main.js` file, we will listen to the `message` event and change the `quote.innerHTML` each time a new quote is sent.

<pre><code class="language-javascript">const broadcast = new BroadcastChannel("quote_channel");
const quote = document.querySelector("#quote");

broadcast.onmessage = ({data}) =&gt; {
	quote.innerHTML = data;
};</code></pre>

Now you can see how the quote in [http://localhost:3000/new-origin/](http://localhost:3000/origin/) changes to the quote in [http://localhost:3000](http://localhost:3000). You can also notice how the quote doesn’t change when the [http://localhost:3000](http://localhost:3000) tab is hidden since it only fetches a quote when its page visibility status is visible.

### Support

[Widely supported](https://caniuse.com/mdn-api_broadcastchannel_name)

## Internationalization API

### What Is It?

When developing a web page or app, it’s extremely common to need to translate its content across other languages to reach a wider audience. However, just translating your page’s text to whichever language you need isn’t enough to make your content available to speakers of that language since things like dates, numbers, units, and so on are different across countries and may cause confusion to your users.

Let’s say you want to display the date “November 8, 2022” on your webpage like “11/8/22”. This data can be read in three distinct ways depending on the reader’s country:

-   “November 8, 2022” or MM/DD/YY by people from the US.
-   “August 11, 2022” or DD/MM/YY by people from Europe and Latam.
-   “August 22, 2011” or YY/MM/DD by people from Japan, China, and Canada.

This is where the **Internationalization API** (Or **I18n API**) comes to solve formatting issues across different languages and regions. The I18n API is an amazing tool that has several uses, but we won’t delve into them to not overcomplicate this article.

### How To Use It?

The I18n API uses locale identifiers to work. A locale identifier is a string that expresses the user’s language, country, region, dialect, and other preferences. To be precise, a locale identifier is a string that consists of subtags separated by hyphens. Subtags represent user preferences like language, country, region, or script and are formatted in the following way:

1. “zh”: Chinese (language);
2. “zh-Hant”: Chinese (language) written in traditional characters (script);
3. “zh-Hant-TW”: Chinese (language) written in traditional characters (script) as used in Taiwan (region).

There are more subtags to address more users’ preferences (if you want to learn more, you can check the [RFC definition](https://datatracker.ietf.org/doc/html/rfc5646) of language tags), but to keep it short, the I18n API uses these locale identifiers to know how to format all the language-sensitive data.

To be more precise, the I18n API provides an `Intl` object that brings a bunch of specialized constructors to work with language-sensitive data. In my opinion, some of the most useful `Intl` constructors for internationalization are:

-   `Intl.DateTimeFormat()`  
    Used to format dates and times.
-   `Intl.DisplayNames()`  
    Used to format language, region, and script display names.
-   `Intl.Locale()`  
    Used to construct and manipulate locale identifier tags.
-   `Intl.NumberFormat()`  
    Used to format numbers.
-   `Intl.RelativeTimeFormat()`  
    Used to format relative time descriptions.

For our example, we will focus on the `Intl.DateTimeFormat()` constructor to format the quote’s `dateAdded` property depending on the user locale. The `Intl.DateTimeFormat()` constructor takes two arguments: the `locale` string that defines the date formatting convention and the `options` objects to customize how to format the dates.

The `Intl.DateTimeFormat()` created object has a `format()` method that takes two arguments: the `Date` object we want to format and the `options` object to customize how to display the formatted date.

<pre><code class="language-javascript">const logDate = (locale) =&gt; {
	const newDate = new Date("2022-10-24"); // YY/MM/DD
	const dateTime = new Intl.DateTimeFormat(locale, {timeZone: "UTC"});
	const formatedDate = dateTime.format(newDate);
	console.log(formatedDate);
};

logDate("en-US"); // 10/24/2022
logDate("de-DE"); // 24.10.2022
logDate("zh-TW"); // 2022/10/24</code></pre>

**Note:** _On the `Intl.DateTimeFormat` constructor’s `options` argument, we set the `timeZone` property to `"UTC"` so the date isn’t formatted to the user’s local time. In my case, the date is parsed to “10/23/2022” without the `timeZone` option._

As you can see, the `dateTime.format()` changes the date depending on the locale’s date formatting convention. We can implement this behavior on the quotes’ date using the `navigator.language` global property, which holds the user’s preferred locale. To do this, we will create a new function that takes a date string (in YYYY-MM-DD format) and returns the date formatted depending on the user’s locale.

<div class="break-out">

<pre><code class="language-javascript">const formatDate = (dateString) =&gt; {
	const date = new Date(dateString);
	const locale = navigator.language;
	const dateTimeFormat = new Intl.DateTimeFormat(locale, {timeZone: "UTC"});

    return dateTimeFormat.format(date);

};</code></pre>

</div>

We can add this function inside the `getQuote()` function to parse the `dateAdded` date.

<div class="break-out">

<pre><code class="language-javascript">const getQuote = async () =&gt; {
	if (document.visibilityState === "visible") {
		try {
			const response = await fetch("https://api.quotable.io/random");
			const {content, author, dateAdded} = await response.json();
			const parsedQuote = `
			&lt;q&gt;${content}&lt;/q&gt; &lt;br&gt; 
			&lt;p&gt;- ${author}&lt;/p&gt;&lt;br&gt; 
			&lt;p&gt;Added on ${formatDate(dateAdded)}&lt;/p&gt;`;
			quote.innerHTML = parsedQuote;
			broadcast.postMessage(parsedQuote);
		} catch (error) {
			console.error(error);
		}
	}
};</code></pre>
</div>

With this, our quotes are localized to the user’s preferred language! In my case, my `navigator.language` value is `"en"`, so my dates are formatted to MM/DD/YY.

### Support

[Widely supported](https://caniuse.com/internationalization)

{{% ad-panel-leaderboard %}}

## Conclusion

After reading this article, you can now flex about knowing the existence of these APIs and how to use them. Even though they were ranked last in awareness in the [State of JS Survey](https://2021.stateofjs.com/en-US/features), they are extremely useful, and knowing how to use them will definitely enhance your developing experience. The fact that these powerful APIs aren’t very known means that there are still useful APIs you and I still don’t know about, so it’s the perfect time to explore and find that API that will simplify your code and save you a ton of time developing.

I hope you liked this article and until the next time!

{{< signature "vf, yk, il" >}}
