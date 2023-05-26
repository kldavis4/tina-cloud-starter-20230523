---
title: 'Improving JavaScript Bundle Performance With Code-Splitting'
slug: javascript-bundle-performance-code-splitting
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f721011b-37a8-4c1d-a8b9-b249bf938678/javascript-bundle-performance-code-splitting.jpg
date: 2022-02-02T10:30:00.000Z
summary: >-
  In this article, Adrian Bece shares more about the benefits and caveats of code-splitting and how page performance and load times can be improved by dynamically loading expensive, non-critical JavaScript bundles.
description: >-
  In this article, Adrian Bece shares more about the benefits and caveats of code-splitting and how page performance and load times can be improved by dynamically loading expensive, non-critical JavaScript bundles.
categories:
  - Apps
  - Workflow
  - JavaScript
  - Performance
---

Projects built using JavaScript-based frameworks often ship large bundles of JavaScript that take time to download, parse and execute, blocking page render and user input in the process. This problem is more apparent on unreliable and slow networks and lower-end devices. In this article, we’re going to cover code-splitting best practices and showcase some examples using React, so we load the minimum JavaScript necessary to render a page and dynamically load sizeable non-critical bundles.

JavaScript-based frameworks like React made the process of developing web applications streamlined and efficient, for better or worse. This automatization often leads developers to treat a framework and build tools as a black box. It’s a common misconception that the code which is produced by the framework build tools (Webpack, for example) is fully optimized and cannot be improved upon any further.

Even though the final JavaScript bundles are tree-shaken and minified, usually the **entire web application is contained within a single or just a few JavaScript files**, depending on the project configuration and out-of-the-box framework features. What problem could there be if the file itself is minified and optimized?

## Bundling Pitfalls

Let’s take a look at a simple example. The JavaScript bundle for our web app consists of the following six pages contained in individual components. Usually, those components consist of even more sub-components and other imports, but we’ll keep this simple for clarity.

- **Four public pages**  
They can be accessed even when not logged in (homepage, login, register, and profile page).
- **A single private page**  
It can be accessed by logging in (dashboard page).
- **A restricted page**  
It’s an admin page that has an overview of all user activity, accounts, and analytics (admin page).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9938e8cb-a2b2-4bbb-b9ad-43b759d2d9e5/1-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9938e8cb-a2b2-4bbb-b9ad-43b759d2d9e5/1-improving-javascript-bundle-performance-code-splitting.png" width="800" height="291" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9938e8cb-a2b2-4bbb-b9ad-43b759d2d9e5/1-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The JavaScript bundle which consists of a homepage, a login page, a register page, a profile page, a dashboard page and an admin page." >}}

When a user lands on a homepage, for example, the entire `app.min.js` bundle with code for other pages is loaded and parsed, which means that only a part of it is used and rendered on the page. **This sounds inefficient**, doesn’t it? In addition to that, **all users are loading a restricted part of the app** which only a few users will be able to have access to &mdash; the admin page. Even though the code is partially obfuscated as part of the minification process, we risk exposing API endpoints or other data reserved for admin users. 

How can we make sure that user loads the **bare minimum JavaScript needed to render** the page they’re currently on? In addition to that, we also need to make sure that the **bundles for restricted sections** of the page are loaded by the authorized users only. The answer lies in **code-splitting**. 

Before delving into details about code-splitting, let’s quickly remind ourselves what makes JavaScript so impactful on overall performance. 

{{% feature-panel %}}

## Performance Costs

JavaScript’s effect on performance consists of **download, parsing and the execution** costs.

Like any file referenced and used on a website, it first needs to be downloaded from a server. How quickly the file is **downloaded** depends on the **connection speed** and the **size of the file** itself. Users can browse the Internet using slow and unreliable networks, so minification, optimization, and code-splitting of JavaScript files ensure that the user downloads the smallest file possible.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3287aad2-1e3b-412b-8694-67e78855f117/2-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3287aad2-1e3b-412b-8694-67e78855f117/2-improving-javascript-bundle-performance-code-splitting.png" width="800" height="579" sizes="100vw" caption="<a href='https://www.performancebudget.io/'>Estimated load times</a> for a makeshift JavaScript application. Notice the difference in loading times between mobile and cable networks. Users are having different loading experience depending on the network type. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3287aad2-1e3b-412b-8694-67e78855f117/2-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="Estimated load times for a makeshift JavaScript application. The table shows the difference in loading times between mobile (up to 3 secs) and cable (0.96 secs) networks. Users are having different loading experience depending on the network type." >}}

Unlike the image file, for example, which only needs to be rendered once the file has been downloaded, JavaScript files need to be **parsed, compiled, and executed**. This is a CPU-intensive operation that **blocks the main thread** making the page **unresponsive** for that time. A user **cannot interact** with the page during that phase even though the content might be displayed and has seemingly finished loading. If the script takes too long to parse and execute, the user will get the impression that the site is broken and leave. This is why Lighthouse and Core Web Vitals specify [First Input Delay (FID)](https://web.dev/fid/) and [Total Blocking Time (TBT)](https://web.dev/lighthouse-total-blocking-time/) metrics to measure site interactivity and input responsiveness.

JavaScript is also a [render-blocking resource](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript#parser_blocking_versus_asynchronous_javascript), meaning that if the browser encounters a script within the HTML document which isn’t deferred, it doesn’t render the page until it loads and executes the script. HTML attributes `async` and `defer` signal to the browser not to block page processing, however, **the CPU thread still gets blocked** and the script needs to be executed before the page becomes responsive to user input.

Website [performance is not consistent](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/javascript-startup-optimization#parsecompile) across devices. There is a wide range of devices available on the market with different CPU and memory specs, so it’s no surprise that **the difference in JavaScript execution time between the high-end devices and average devices is huge.**

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b88d7cd-8f54-4814-9eb5-4955b9bbe06c/3-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b88d7cd-8f54-4814-9eb5-4955b9bbe06c/3-improving-javascript-bundle-performance-code-splitting.png" width="800" height="484" sizes="100vw" caption="JavaScript processing times are vastly different between high-end, average and low-end devices (Image source: '<a href='https://v8.dev/blog/cost-of-javascript-2019'>The cost of JavaScript in 2019</a>' by Addy Osmani) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b88d7cd-8f54-4814-9eb5-4955b9bbe06c/3-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The table shows the difference in JavaScript processing times between high-end, average and low-end devices." >}}

To cater to a wide range of device specs and network types, we should **ship only critical code**. For JavaScript-based web apps, it means that only the code which is used on that particular page should be loaded, as loading the complete app bundle at once can result in longer execution times and, for users, longer waiting time until the page becomes usable and responsive to input.

{{% ad-panel-leaderboard %}}

## Code-splitting

With code-splitting, our goal is to defer the loading, parsing, and execution of JavaScript code which is not needed for the current page or state. For our example, that would mean that individual pages should be split into their respective bundles &mdash; `homepage.min.js`, `login.min.js`, `dashboard.min.js`, and so on.

When the user initially lands on the homepage, the main vendor bundle containing the framework and other shared dependencies should be loaded in alongside the bundle for the homepage. The user clicks on a button that toggles an account creation modal. As the user is interacting with the inputs, the expensive password strength check library is dynamically loaded. When a user creates an account and logs in successfully, they are redirected to the dashboard, and only then is the dashboard bundle loaded. It’s also important to note that this particular user doesn’t have an admin role on the web app, so the admin bundle is not loaded.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8690142a-80e7-4705-9467-a6b037566ac2/4-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8690142a-80e7-4705-9467-a6b037566ac2/4-improving-javascript-bundle-performance-code-splitting.png" width="800" height="435" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8690142a-80e7-4705-9467-a6b037566ac2/4-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="Code-splitting between the bundles. The homepage refers to the initial app load, the account creation modul refers to interaction and the dashboard to navigation." >}}
  
### Dynamic Imports & Code-splitting In React

Code splitting is available out-of-the-box for Create React App and other frameworks that use Webpack like Gatsby and Next.js. If you have set up the React project manually or if you are using a framework that doesn’t have code-splitting configured out-of-the-box, you’ll have to consult the [Webpack documentation](https://webpack.js.org/guides/code-splitting/) or the documentation for the build tool that you’re using.

#### Functions

Before diving into code-splitting React components, we also need to mention that we can also code split functions in React by [dynamically importing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#dynamic_imports) them. Dynamic importing is vanilla JavaScript, so this approach should work for all frameworks. However, keep in mind that this syntax is [not supported by legacy browsers](https://caniuse.com/es6-module-dynamic-import) like Internet Explorer and Opera Mini.

<pre><code class="language-javascript">import("path/to/myFunction.js").then((myFunction) =&gt; {
   /&#42; ... &#42;/
});</code></pre>

In the following example, we have a blog post with a comment section. We’d like to encourage our readers to create an account and leave comments, so we are offering a quick way to create an account and start commenting by displaying the form next to the comment section if they’re not logged in.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0265152d-9a52-4816-b090-b9f7f767c654/5-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0265152d-9a52-4816-b090-b9f7f767c654/5-improving-javascript-bundle-performance-code-splitting.png" width="800" height="520" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0265152d-9a52-4816-b090-b9f7f767c654/5-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="A blog post with a comment section" >}}

The form is using a sizeable 800kB [`zxcvbn`](https://www.npmjs.com/package/zxcvbn) library to check password strength which could prove problematic for performance, so it’s the right candidate for code splitting. This is the exact scenario I was dealing with last year and we managed to achieve a noticeable performance boost by code-splitting this library to a separate bundle and loading it dynamically.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5e871e-c891-4c77-bcfb-914b58d6affe/6-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5e871e-c891-4c77-bcfb-914b58d6affe/6-improving-javascript-bundle-performance-code-splitting.png" width="800" height="490" sizes="100vw" caption="Bundle size and estimated download times for <code>zxcvbn</code> package. This estimation doesn’t include parsing and execution times which also affects website performance. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5e871e-c891-4c77-bcfb-914b58d6affe/6-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="Bundle size and estimated download times for zxcvbn package." >}}

Let’s see what the `Comments.jsx` component looks like.

<pre><code class="language-javascript">import React, { useState } from "react";
import zxcvbn from "zxcvbn"; /&#42; We're importing the lib directly &#42;/

export const Comments = () =&gt; {
  const [password, setPassword] = useState("");
  const [passwordStrength, setPasswordStrength] = useState(0);

  const onPasswordChange = (event) =&gt; {
    const { value } = event.target;
    const { score } = zxcvbn(value)
    setPassword(value);
    setPasswordStrength(score);
  };

  return (
    &lt;form&gt;
      {/&#42; ... &#42;/}
      &lt;input onChange={onPasswordChange} type="password"&gt;&lt;/input&gt;
      &lt;small&gt;Password strength: {passwordStrength}&lt;/small&gt;
      {/&#42; ... &#42;/}
    &lt;/form&gt;
  );
};</code></pre>

We’re importing the `zxcvbn` library directly and it gets included in the main bundle as a result. The resulting minified bundle for our tiny blog post component is a whopping **442kB** gzipped! React library and this blog post page barely reach **45kB** gzipped, so we have slowed down the initial loading of this page considerably by instantly loading this password checking library.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ba9cf4f-9a78-4961-923d-f4e71d1c9447/7-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ba9cf4f-9a78-4961-923d-f4e71d1c9447/7-improving-javascript-bundle-performance-code-splitting.png" width="800" height="516" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ba9cf4f-9a78-4961-923d-f4e71d1c9447/7-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="A blog post with a comment section on the left, and the main bundle with the imported zxcvbn library which is 442kB on the right." >}}

We can reach the same conclusion by looking at the [Webpack Bundle Analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer) output for the app. That narrow rectangle on the far right is our blog post component.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f43e5e3f-adb4-469a-87a0-ebb7c9097a30/8-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f43e5e3f-adb4-469a-87a0-ebb7c9097a30/8-improving-javascript-bundle-performance-code-splitting.png" width="800" height="346" sizes="100vw" caption="The entire app is contained in a single bundle, and <code>zxcvbn</code> library is the largest part of the bundle. It’s even larger than the react-dom dependency. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f43e5e3f-adb4-469a-87a0-ebb7c9097a30/8-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The entire app is contained in a single bundle, and zxcvbn library is the largest part of the bundle. It’s even larger than the react-dom dependency." >}}

Password checking is not critical for page render. Its functionality is required only when the user interacts with the password input. So, let’s code-split `zxcvbn` into a separate bundle, dynamically import it and load it only when the password input value changes, i.e. when the user starts typing their password. We need to remove the `import` statement and add the dynamic import statement to the password `onChange` event handler function.

<pre><code class="language-javascript">import React, { useState } from "react";

export const Comments = () =&gt; {
  /&#42; ... &#42;/
  const onPasswordChange = (event) =&gt; {
    const { value } = event.target;
    setPassword(value);

    /&#42; Dynamic import - rename default import to lib name for clarity &#42;/
    import("zxcvbn").then(({default: zxcvbn}) =&gt; {
      const { score } = zxcvbn(value);
      setPasswordStrength(score);
    });
  };

  /&#42; ... &#42;/
}</code></pre>

Let’s see how our app behaves now after we’ve moved the library to a dynamic import.

{{< vimeo id="669945248" breakout="true" >}}

As we can see from the video, the initial page load is around **45kB** which covers only framework dependencies and the blog post page components. This is the ideal case since users will be able to get the content much faster, especially the ones using slower network connections. 

Once the user starts typing in the password input, we can see the bundle for the `zxcvbn` library appears in the network tab and the result of the function running is displayed below the input. Even though this process repeats on every keypress, the file is only requested once and it runs instantly once it becomes available. 

We can also confirm that the library has been code-split into a separate bundle by checking [Webpack Bundle Analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer) output.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c4dd02-3ff4-4ef4-b393-855654cc9ebe/9-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c4dd02-3ff4-4ef4-b393-855654cc9ebe/9-improving-javascript-bundle-performance-code-splitting.png" width="800" height="310" sizes="100vw" caption="This looks much better. The smaller blue colored bundle on the right is the 'critical' bundle that loads instantly, while the large bundle on the left is dynamically-loaded bundle. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c4dd02-3ff4-4ef4-b393-855654cc9ebe/9-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The smaller blue colored bundle on the right, and the large bundle on the left." >}}

#### Third-party React components

Code-splitting React components are simple for most cases and it consists of the following four steps:

1. **use a default export** for a component that we want to code-split;
2. **import** the component with `React.lazy`;
3. **render** the component as a child of `React.Suspense`;
4. **provide a fallback** component to `React.Suspense`.

Let’s take a look at another example. This time we’re building a date-picking component that has requirements that default HTML date input cannot meet. We have chosen `react-calendar` as the library that we’re going to use.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e295d42c-8f82-4780-99b2-572d6acbbb07/10-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e295d42c-8f82-4780-99b2-572d6acbbb07/10-improving-javascript-bundle-performance-code-splitting.png" width="800" height="315" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e295d42c-8f82-4780-99b2-572d6acbbb07/10-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="A date-picking component" >}}

Let’s take a look at the `DatePicker` component. We can see that the `Calendar` component from the `react-calendar` package is being displayed conditionally when the user focuses on the date input element.

<pre><code class="language-javascript">import React, { useState } from "react";
import Calendar from "react-calendar";

export const DatePicker = () =&gt; {
  const [showModal, setShowModal] = useState(false);

  const handleDateChange = (date) =&gt; {
    setShowModal(false);
  };

  const handleFocus = () =&gt; setShowModal(true);

  return (
    &lt;div&gt;
      &lt;label htmlFor="dob"&gt;Date of birth&lt;/label&gt;
      &lt;input id="dob"
        onFocus={handleFocus}
        type="date"
        onChange={handleDateChange}
      /&gt;
      {showModal && &lt;Calendar value={startDate} onChange={handleDateChange} /&gt;}
    &lt;/div&gt;
  );
};</code></pre>

This is pretty much a standard way almost anyone would have created this app. Let’s run the Webpack Bundle Analyzer and see what the bundles look like.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f7fc31-b5a5-4293-bcce-70850bcb3b04/11-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f7fc31-b5a5-4293-bcce-70850bcb3b04/11-improving-javascript-bundle-performance-code-splitting.png" width="800" height="355" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f7fc31-b5a5-4293-bcce-70850bcb3b04/11-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The bundles analysed by the Webpack Bundle Analyzer with the entire app loaded in a single JavaScript bundle where react-calendar takes a considerable portion of it." >}}

Just like in the previous example, the entire app is loaded in a single JavaScript bundle and `react-calendar` takes a considerable portion of it. Let's see if we can code split it.

The first thing we need to notice is that the `Calendar` popup is loaded conditionally, only when the `showModal` state is set. This makes the `Calendar` component a prime candidate for code-splitting.

Next, we need to check if `Calendar` is a default export. In our case, it is.

<pre><code class="language-javascript">import Calendar from "react-calendar"; /&#42; Standard import &#42;/</code></pre>

Let’s change the `DatePicker` component to lazy load the `Calendar` component.

<pre><code class="language-javascript">import React, { useState, lazy, Suspense } from "react";

const Calendar = lazy(() =&gt; import("react-calendar")); /&#42; Dynamic import &#42;/

export const DateOfBirth = () =&gt; {
  const [showModal, setShowModal] = useState(false);

  const handleDateChange = (date) =&gt; {
    setShowModal(false);
  };

  const handleFocus = () =&gt; setShowModal(true);

  return (
    &lt;div&gt;
      &lt;input
        id="dob"
        onFocus={handleFocus}
        type="date"
        onChange={handleDateChange}
      /&gt;
      {showModal && (
        &lt;Suspense fallback={null}&gt;
          &lt;Calendar value={startDate} onChange={handleDateChange} /&gt;
        &lt;/Suspense&gt;
      )}
    &lt;/div&gt;
  );
};</code></pre>

First, we need to remove the `import` statement and replace it with `lazy` import statement. Next, we need to wrap the lazy-loaded component in a `Suspense` component and provide a `fallback` which is rendered until the lazy-loaded component becomes available.

It’s important to note that `fallback` is a required prop of the `Suspense` component. We can provide any valid React node as a fallback:

- `null`  
If we do not want anything to render during the loading process.
- `string`  
If we want to just display a text.
- React component  
[Skeleton loading elements](https://css-tricks.com/a-bare-bones-approach-to-versatile-and-reusable-skeleton-loaders/), for example.

Let’s run Webpack Bundle Analyzer and confirm that the `react-calendar` has been successfully code-split from the main bundle.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/903c8c05-8d21-47cd-825d-450bef79fb08/12-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/903c8c05-8d21-47cd-825d-450bef79fb08/12-improving-javascript-bundle-performance-code-splitting.png" width="800" height="347" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/903c8c05-8d21-47cd-825d-450bef79fb08/12-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The bundles analysed by the Webpack Bundle Analyzer where react-calendar has been code-split from the main bundle." >}}

#### Project components

We are not limited to third-party components or NPM packages. We can code-split virtually any component in our project. Let’s take the website routes, for example, and code-split individual page components into separate bundles. That way, we’ll always load only the main (shared) bundle and a component bundle needed for the page we’re currently on.

Our main `App.jsx` consists of a React router and three components that are loaded depending on the current location (URL).

<pre><code class="language-javascript">import { Navigation } from "./Navigation";
import { Routes, Route } from "react-router-dom";
import React from "react";

import Dashboard from "./pages/Dashboard";
import Home from "./pages/Home";
import About from "./pages/About";

function App() {
  return (
    &lt;Routes&gt;
      &lt;Route path="/" element={&lt;Home /&gt;} /&gt;
      &lt;Route path="/dashboard" element={&lt;Dashboard /&gt;} /&gt;
      &lt;Route path="/about" element={&lt;About /&gt;} /&gt;
    &lt;/Routes&gt;
  );
}

export default App;</code></pre>

Each of those page components has a default export and is currently imported in a default non-lazy way for this example.

<pre><code class="language-javascript">import React from "react";

const Home = () =&gt; {
  return (/&#42; Component &#42;/);
};
export default Home;</code></pre>

As we’ve already concluded, these components get included in the main bundle by default (depending on the framework and build tools) meaning that everything gets loaded regardless of the route which user lands on. Both Dashboard and About components are loaded on the homepage route and so on.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b5a73ed-9d9b-4241-aef1-4a313dc10ffd/13-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b5a73ed-9d9b-4241-aef1-4a313dc10ffd/13-improving-javascript-bundle-performance-code-splitting.png" width="800" height="434" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b5a73ed-9d9b-4241-aef1-4a313dc10ffd/13-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="The main bundle with different page components in it" >}}

Let’s refactor our `import` statements like in the previous example and use `lazy` import to code-split page components. We also need to nest these components under a single `Suspense` component. If we had to provide a different fallback element for these components, we’d nest each component under a separate `Suspense` component. Components have a default export, so we don’t need to change them.

<pre><code class="language-javascript">import { Routes, Route } from "react-router-dom";
import React, { lazy, Suspense } from "react";

const Dashboard = lazy(() =&gt; import("./pages/Dashboard"));
const Home = lazy(() =&gt; import("./pages/Home"));
const About = lazy(() =&gt; import("./pages/About"));

function App() {
  return (
    &lt;Suspense fallback={null}&gt;
      &lt;Routes&gt;
        &lt;Route path="/" element={&lt;Home /&gt;} /&gt;
        &lt;Route path="/dashboard" element={&lt;Dashboard /&gt;} /&gt;
        &lt;Route path="/about" element={&lt;About /&gt;} /&gt;
      &lt;/Routes&gt;
    &lt;/Suspense&gt;
  );
}

export default App;</code></pre>

And that’s it! Page components are neatly split into separate packages and are loaded on-demand as the user navigates between the pages. Keep in mind, that you can provide a fallback component like a spinner or a skeleton loader to provide a better loading experience on slower networks and average to low-end devices.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72345bcc-f555-4693-b41f-46a5e02ec342/14-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72345bcc-f555-4693-b41f-46a5e02ec342/14-improving-javascript-bundle-performance-code-splitting.png" width="800" height="345" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72345bcc-f555-4693-b41f-46a5e02ec342/14-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="Page components are split into separate packages." >}}

{{< vimeo id="669967735" breakout="true" >}}

### What Should We Code-split?

It’s crucial to understand, which functions and components should be code-split into separate bundles from the get-go. That way, we can code-split proactively and early on in development and avoid the aforementioned bundling pitfalls and having to untangle everything.

You might already have some idea on how to choose the right components for code-splitting from the examples that we’ve covered. Here is a good baseline criterion to follow when choosing potential candidates for code-splitting:

- page components for routes (individual pages),
- expensive or sizeable conditionally-loaded components (modals, dropdowns, menus, etc.),
- expensive or sizeable third-party functions and components.

**We shouldn’t get overzealous with code-splitting.** Although we identified potential candidates for code-splitting, we want to **dynamically load bundles that significantly impact performance** **or load times**. We want to avoid creating bundles with the size of a few hundred bytes or a few kilobytes. These micro-bundles can actually harm the UX and performance in some cases, as we’ll see later on in the article.

{{% ad-panel-leaderboard %}}

## Auditing And Refactoring JavaScript Bundles

Some projects will require optimization later in the development cycle or even sometime after the project goes live. The main downside of code-splitting later in the development cycle is that you’ll have to deal with components and changes on a wider scale. If some widely-used component turns out a good candidate for code-splitting and it is used across 50 other components, the scope of the pull request and changes would be large and difficult to test if no automated test exists.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/882584c9-2805-4b04-852f-85494d13fe1c/15-improving-javascript-bundle-performance-code-splitting.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/882584c9-2805-4b04-852f-85494d13fe1c/15-improving-javascript-bundle-performance-code-splitting.jpg" width="800" height="417" sizes="100vw" caption="If not addressed on time, bundle size issues get increasingly difficult and risky to fix and refactor on larger projects like this one (filenames and components omitted on purpose). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/882584c9-2805-4b04-852f-85494d13fe1c/15-improving-javascript-bundle-performance-code-splitting.jpg'>Large preview</a>)" alt="An example of bundle size issues on big projects" >}}

Being tasked with optimizing the performance of the entire web app may be a bit overwhelming at first. A good place to start is to audit the app using [Webpack Bundle Analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer) or [Source Map Explorer](https://github.com/danvk/source-map-explorer) and identify bundles that should be code-split and fit the aforementioned criteria. An additional way of identifying those bundles is to run a [performance test in a browser](https://developer.chrome.com/docs/devtools/evaluate-performance/) or use [WebPageTest](https://www.webpagetest.org/), and check which bundles [block the CPU](https://nooshu.com/blog/2019/10/02/how-to-read-a-wpt-waterfall-chart/) main thread the longest.

After identifying code-splitting candidates, we need to check the scope of changes that are required to code-split this component from the main bundle. At this point, we need to evaluate if the benefit of code-splitting outweighs the scope of changes required and the development and testing time investment. This risk is minimal to none early in the development cycle.

Finally, we need to verify that the component has been code-split correctly and that the main bundle size has decreased. We also need to build and test the component to avoid introducing potential issues.

There are a lot of steps for code-splitting a single existing component, so let’s summarize the steps in a quick checklist:

1. Audit the site using bundle analyzer and browser performance profiler, and identify larger components and bundles that take the most time to execute.
2. Check if the benefit of code-splitting outweighs the development and testing time required.
3. If the component has a named export, convert it to the default export.
4. If the component is a part of [barrel export](https://hackernoon.com/react-project-architecture-using-barrels-d086146eb0f6), remove it from the barrel file.
5. Refactor `import` statements to use `lazy` statements.
6. Wrap code-split components in the `Suspense` component and provide a fallback.
7. Evaluate the resulting bundle (file size and performance gains). If the bundle doesn’t significantly decrease the bundle file size or improve performance, undo code-splitting.
8. Check if the project builds successfully and if it performs without any issues.

### Performance Budgets

We can configure our build tools and continuous integration (CI) tools to catch bundle sizing issues early in development by setting **performance budgets** that can serve as a performance baseline or a general asset size limit. Build tools like Webpack, CI tools, and performance audit tools like Lighthouse can [use the defined performance budgets](https://web.dev/incorporate-performance-budgets-into-your-build-tools/) and throw a warning if some bundle or resource goes over the budget limit. We can then run code-splitting for bundles that get caught by the performance budget monitor. This is especially useful information for pull request reviews, as we check how the added features affect the overall bundle size.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bccfb425-03e0-4b61-92a2-92ea78bd4df2/16-improving-javascript-bundle-performance-code-splitting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bccfb425-03e0-4b61-92a2-92ea78bd4df2/16-improving-javascript-bundle-performance-code-splitting.png" width="800" height="326" sizes="100vw" caption="Tools like bundlesizes can be easily integrated with any build or CI tool to keep track of bundle size stats on pull request basis. (Image from bundlesizes documentation) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bccfb425-03e0-4b61-92a2-92ea78bd4df2/16-improving-javascript-bundle-performance-code-splitting.png'>Large preview</a>)" alt="An example of bundlesizes integrated into github to keep track of bundle size stats on pull request basis." >}}

We can fine-tune performance budgets to tailor for worse possible user scenarios, and use that as a baseline for performance optimization. For example, if we use the scenario of a user browsing the site on an unreliable and slow connection on an average phone with a slower CPU as a baseline, we can provide optimal user experience for a much wider range of user devices and network types.

Alex Russell has covered this topic in great detail in his article on the topic of [real-world web performance budgets](https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/) and found out that the optimal budget size for those worst-case scenarios lies somewhere between 130kB and 170kB.

<blockquote>“Performance budgets are an essential but under-appreciated part of product success and team health. Most partners we work with are not aware of the real-world operating environment and make inappropriate technology choices as a result. We set a budget in <strong>time</strong> of &lt;= 5 seconds first-load <a href="https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive">Time-to-Interactive</a> and &lt;= 2s for subsequent loads. We constrain ourselves to a real-world baseline device + network configuration to measure progress. The default global baseline is a ~$200 Android device on a 400Kbps link with a 400ms round-trip-time (“RTT”). This translates into a budget of ~130-170KB of critical-path resources, depending on composition &mdash; the more JS you include, the smaller the bundle must be.”<br /><br />&mdash; Alex Russell</blockquote>

## React Suspense And Server-Side Rendering (SSR)

An important caveat that we have to be aware of is that React `Suspense` component is only for client-side use, meaning that **server-side rendering (SSR) will throw an error** if it tries to render the `Suspense` component regardless of the fallback component. This issue will be addressed in the upcoming [React version 18](https://reactjs.org/blog/2021/06/08/the-plan-for-react-18.html). However, if you are working on a project running on an older version of React, you will need to address this issue.

One way to address it is to check if the code is running on the browser which is a simple solution, if not a bit hacky.

<pre><code class="language-javascript">const isBrowser = typeof window !== "undefined"

return (
  &lt;&gt;
    {isBrowser && componentLoadCondition && (
      &lt;Suspense fallback={&lt;Loading /&gt;}&gt;
        &lt;SomeComponent /&gt;
      &lt;Suspense&gt;
    )}
  &lt;/&gt;
)</code></pre>

However, this solution is far from perfect. The content won’t be rendered server-side which is perfectly fine for modals and other non-essential content. Usually, when we use SSR, it is for improved **performance and SEO**, so we want content-rich components to render into HTML, thus crawlers can parse them to improve search result rankings.

Until React version 18 is released, React team recommends using [the Loadable Components](https://loadable-components.com/) library for this exact case. This plugin extends React’s `lazy` import and `Suspense` components, and adds [Server-side rendering support](https://loadable-components.com/docs/server-side-rendering/), [dynamic imports](https://loadable-components.com/docs/dynamic-import/) with dynamic properties, [custom timeouts](https://loadable-components.com/docs/timeout/), and more. Loadable Components library is a great solution for larger and more complex React apps, and the basic React code-splitting is perfect for smaller and some medium apps.

## Benefits And Caveats Of Code-Splitting

We’ve seen how page performance and load times can be improved by dynamically loading expensive, non-critical JavaScript bundles. As an added benefit of code-splitting, **each JavaScript bundle gets its unique hash** which means that when the app gets updated, the user’s browser will download only the updated bundles that have different hashes.

However, **code-splitting can be easily abused** and developers can get overzealous and create too many micro bundles which harm usability and performance. Dynamically loading too many smaller and irrelevant components can make the UI feel unresponsive and delayed, harming the overall user experience. Overzealous code-splitting can even harm performance in cases where the bundles are served via HTTP 1.1 which lacks [multiplexing](https://developers.google.com/web/fundamentals/performance/http2#request_and_response_multiplexing).

<blockquote>Use performance budgets, bundle analyzers, performance monitoring tools to identify and evaluate each potential candidate for code splitting. Use code-splitting in a sensible and temperate way, only if it results in a significant bundle size reduction or noticeable performance improvement.</blockquote>

### References

- [Code-Splitting](https://reactjs.org/docs/code-splitting.html), React documentation
- “[JavaScript Start-up Optimization](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/javascript-startup-optimization)”, Addy Osmani
- “[Can You Afford It?: Real-world Web Performance Budgets](https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/)”, Alex Russell
- “[Incorporate Performance Budgets Into Your Build Process](https://web.dev/incorporate-performance-budgets-into-your-build-tools/)”, Milica Mihajlija
- “[When JavaScript Bytes](https://vimeo.com/396638607)”, Tim Kadlec 

{{< signature "vf, yk, il" >}}
