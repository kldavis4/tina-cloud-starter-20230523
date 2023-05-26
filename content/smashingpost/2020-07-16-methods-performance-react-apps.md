---
title: 'Methods Of Improving And Optimizing Performance In React Apps'
slug: methods-performance-react-apps
author: shedrack-akintayo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d5a37a1-ca97-41cc-bace-28bedfe061c8/methods-performance-react-apps.png
date: 2020-07-16T11:00:00.000Z
summary: >-
  Since React was introduced, it has transformed the way front-end developers build web applications, and its virtual DOM is famous for effectively rendering components. In this tutorial, we will discuss various methods of optimizing performance in React applications, and also the features of React that we can use to improve performance.
description: >-
  Since React was introduced, it has transformed the way front-end developers build web applications, and its virtual DOM is famous for effectively rendering components. In this tutorial, we will discuss various methods of optimizing performance in React applications, and also the features of React that we can use to improve performance.
categories:
  - React
  - Performance
  - Apps
---

React enables web applications to update their user interfaces (UIs) quickly, but that does not mean your medium or large React application will perform efficiently. Its performance will depend on how you use React when building it, and on your understanding of how React operates and the process through which components live through the various phases of their lifecycle. React offers a lot of performance improvements to a web app, and you can achieve these improvements through various techniques, features, and tools.

In this tutorial, we will discuss various methods of optimizing performance in React applications, and also the features of React that we can use to improve performance.

## Where To Start Optimizing Performance In A React Application?

We can’t begin to optimize an app without knowing exactly when and where to optimize. You might be asking, “Where do we start?”

During the initial rendering process, React builds a DOM tree of components. So, when data changes in the DOM tree, we want React to re-render only those components that were affected by the change, skipping the other components in the tree that were not affected.

However, React could end up re-rendering all components in the DOM tree, even though not all are affected. This will result in longer loading time, wasted time, and even wasted CPU resources. We need to prevent this from happening. So, this is where we will focus our optimization effort.

In this situation, we could configure every component to only render or diff when necessary, to avoid wasting resources and time.

{{% feature-panel %}}

## Measuring Performance

Never start the optimization process of your React application based on what you feel. Instead, use the measurement tools available to analyze the performance of your React app and get a detailed report of what might be slowing it down.

### Analyzing React Components With Chrome’s Performance Tab

According to [React’s documentation,](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab), while you’re still in development mode, you can use the “Performance” tab in the Chrome browser to visualize how React components mount, update, and unmount.
For example, the image below shows Chrome’s “Performance” tab profiling and analyzing my blog in development mode.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff54a3cd-9f50-4d35-b3d9-b85d83344540/1-performance-profiler-summary-methods-performance-react-apps.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff54a3cd-9f50-4d35-b3d9-b85d83344540/1-performance-profiler-summary-methods-performance-react-apps.png" sizes="100vw" caption="Performance profiler summary (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff54a3cd-9f50-4d35-b3d9-b85d83344540/1-performance-profiler-summary-methods-performance-react-apps.png'>Large preview</a>)" alt="Performance profiler summary" >}}

To do this, follow these steps:

1. Disable all extensions temporarily, especially React Developer Tools, because they can mess with the result of the analysis. You can easily disable extensions by running your browser in incognito mode.
2. Make sure the application is running in development mode. That is, the application should be running on your localhost.
3. Open Chrome’s Developer Tools, click on the “Performance” tab, and then click the “Record” button.
4. Perform the actions you want to profile. Don’t record more than 20 seconds, or else Chrome might hang.
5. Stop the recording.
6. React events will be grouped under the “User Timing” label.

The numbers from the profiler are relative. Most times and components will render more quickly in production. Nevertheless, this should help you to figure out when the UI is updated by mistake, as well as how deep and how often the UI updates occur.

## React Developer Tools Profiler

According to [React’s documentation](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-devtools-profiler), in `react-dom` 16.5+ and `react-native` 0.57+, enhanced profiling capabilities are available in developer mode using React Developer Tools Profiler. The profiler uses React’s experimental [Profiler API](https://reactjs.org/docs/profiler.html) to collate timing information about each component that’s rendered, in order to identify performance bottlenecks in a React application.

Just download React Developer Tools for your browser, and then you can use the profiler tool that ships with it. The profiler can only be used either in development mode or in the production-profiling build of React v16.5+. The image below is the profiler summary of my blog in development mode using React Developer Tools Profiler:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efcaa472-277a-4a7f-9d26-5da385e0d158/2-react-devtools-profiler-methods-performance-react-apps.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efcaa472-277a-4a7f-9d26-5da385e0d158/2-react-devtools-profiler-methods-performance-react-apps.png" sizes="100vw" caption="React Developer Tools Profiler flamegraph (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efcaa472-277a-4a7f-9d26-5da385e0d158/2-react-devtools-profiler-methods-performance-react-apps.png'>Large preview</a>)" alt="React Developer Tools Profiler flamegraph" >}}

To achieve this, follow these steps:

1. Download React Developer Tools.
2. Make sure your React application is either in development mode or in the production-profiling build of React v16.5+.
3. Open Chrome’s “Developer Tools” tab. A new tab named “Profiler” will be available, provided by React Developer Tools.
4. Click the “Record” button, and perform the actions you want to profile. Ideally, stop recording after you have performed the actions you want to profile.
5. A graph (known as a flamegraph) will appear with all of the event handlers and components of your React app.

**Note**: *[See the documentation](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) for more information.*

{{% ad-panel-leaderboard %}}

## Memoization With `React.memo()`

React v16 was released with an additional API, a higher-order component called `React.memo()`. According to the [documentation](https://reactjs.org/docs/react-api.html#reactmemo), this exists only as a **performance optimization**.

Its name, “**memo**” comes from memoization, which is basically a form of optimization used mainly to speed up code by storing the results of expensive function calls and returning the stored result whenever the **same expensive function** is called again.

Memoization is a technique for executing a function once, usually a pure function, and then saving the result in memory. If we try to execute that function again, with the **same arguments as before**, it will just return the previously saved result from the first function’s execution, without executing the function again.

Mapping the description above to the React ecosystem, the functions mentioned are React components and the arguments are props.

The default behavior of a component declared using `React.memo()` is that it renders only if the props in the component have changed. It does a shallow comparison of the props to check this, but an option is available to override this.

`React.memo()` boosts the performance of a React app by avoiding re-rendering components whose props haven’t changed or when re-rendering is not needed.

The code below is the basic syntax of `React.memo()`:

<pre><code class="language-javascript">const MemoizedComponent = React.memo((props) => {
// Component code goes in here
})
</code></pre>

### When To Use `React.memo()`

- **Pure functional component**  
You can use `React.memo()` if your component is functional, is given the same props, and always renders the same output. You can also use `React.memo()` on non-pure-functional components with React hooks.
- **The component renders often**  
You can use `React.memo()` to wrap a component that renders often.
- **The component re-renders with same props**  
Use `React.memo()` to wrap a component that is usually provided with the same props during re-rendering.
- **Medium to high elements**  
Use it for a component that contains a medium to high number of UI elements to check props for equality.

**Note**: *Be careful when memoizing components that make use of props as callbacks. Be sure to use the same callback function instance between renderings. This is because the parent component could provide different instances of the callback function on every render, which will cause the memoization process to break. To fix this, make sure that the memoized component always receives the same callback instance.*

Let’s see how we can use memoization in a real-world situation. The functional component below, called “Photo”, uses `React.memo()` to prevent re-rendering.

<pre><code class="language-javascript">export function Photo({ title, views }) {
  return (
    &lt;div&gt;
      &lt;div&gt;Photo title: {title}&lt;/div&gt;
      &lt;div&gt;Location: {location}&lt;/div&gt;
    &lt;/div&gt;
  );
}
// memoize the component
export const MemoizedPhoto = React.memo(Photo);
</code></pre>

The code above consists of a functional component that displays a div containing a photo title and the location of the subject in the photo. We are also memoizing the component by creating a new function and calling it `MemoizedPhoto`. Memoizing the photo component will prevent the component from re-rendering as long as the props, `title`, and `location` are the same on subsequent renderings.

<div class="break-out">

 <pre><code class="language-javascript">// On first render, React calls MemoizedPhoto function.
&lt;MemoizedPhoto
  title="Effiel Tower"
  location="Paris"
/&gt;

// On next render, React does not call MemoizedPhoto function,
// preventing rendering
&lt;MemoizedPhoto
  title="Effiel Tower"
  location="Paris"
/&gt;
</code></pre>
</div>

Here, React calls the memoized function only once. It won’t render the component in the next call as long as the props remain the same.

## Bundling And Minification

In React single-page applications, we can bundle and minify all our JavaScript code into a single file. This is OK, as long as our application is relatively small.

As our React application grows, bundling and minifying all of our JavaScript code into a single file becomes problematic, difficult to understand, and tedious. It will also affect the performance and loading time of our React app because we are sending a large JavaScript file to the browser. So, we need some process to help us split the code base into various files and deliver them to the browser in intervals as needed.

In a situation like this, we can use some form of asset bundler like [Webpack](https://webpack.js.org/), and then leverage its code-splitting functionality to split our application into multiple files.

Code-splitting is suggested in [Webpack’s documentation](https://webpack.js.org/guides/code-splitting/#root) as a means to improve the loading time of an application. It is also suggested in [React’s documentation](https://reactjs.org/docs/code-splitting.html#code-splitting) for lazy-loading (serving only the things currently needed by the user), which can dramatically improve performance.

[Webpack suggests](https://webpack.js.org/guides/code-splitting/#root) three general approaches to code-splitting:

- **Entry points**  
Manually split code using entry configuration.
- **Duplication prevention**  
Use `SplitChunksPlugin` to de-duplicate and split chunks.
- **Dynamic imports**  
Split code via inline function calls within modules.

### Benefits Of Code Splitting

- Splitting code assists with the browser’s cache resources and with code that doesn’t change often.
- It also helps the browser to download resources in parallel, which reduces the overall loading time of the application.
- It enables us to split code into chunks that will be loaded on demand or as needed by the application.
- It keeps the initial downloading of resources on first render relatively small, thereby reducing the loading time of the app.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c88b4f-4875-4520-8f2b-03c7ce779212/3-bundling-and-minification-methods-performance-react-apps.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c88b4f-4875-4520-8f2b-03c7ce779212/3-bundling-and-minification-methods-performance-react-apps.png" sizes="100vw" caption="Bundling and minification process (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c88b4f-4875-4520-8f2b-03c7ce779212/3-bundling-and-minification-methods-performance-react-apps.png'>Large preview</a>)" alt="Bundling and minification process" >}}

## Immutable Data Structures

[React’s documentation](https://reactjs.org/docs/optimizing-performance.html#the-power-of-not-mutating-data) talks of the power of not mutating data. Any data that cannot be changed is immutable. Immutability is a concept that React programmers should understand.

An immutable value or object cannot be changed. So, when there is an update, a new value is created in memory, leaving the old one untouched.

We can use immutable data structures and `React.PureComponent` to automatically check for a complex state change. For example, if the state in your application is immutable, you can actually save all state objects in a single store with a state-management library like [Redux](https://redux.js.org/), enabling you to easily implement undo and redo functionality.

Don’t forget that we cannot change immutable data once it’s created.

### Benefits Of Immutable Data Structures

- They have no side effects.
- Immutable data objects are easy to create, test, and use.
- They help us to write logic that can be used to quickly check for updates in state, without having to check the data over and over again.
- They help to prevent temporal coupling (a type of coupling in which code depends on the order of execution).

The following libraries help to provide a set of immutable data structures:

- [immutability-helper](https://github.com/kolodny/immutability-helper)  
Mutate a copy of data without changing the source.
- [Immutable.js](https://immutable-js.github.io/immutable-js/)  
Immutable persistent data collections for JavaScript increase efficiency and simplicity.
- [seamless-immutable](https://github.com/rtfeldman/seamless-immutable)  
Immutable data structures for JavaScript become backwards-compatible with normal JavaScript arrays and objects.
- [React-copy-write](https://github.com/aweary/react-copy-write)  
This gives immutable state with a mutable API.

{{% ad-panel-leaderboard %}}

## Other Methods Of Improving Performance

### Use A Production Build Before Deployment

[React’s documentation](https://reactjs.org/docs/optimizing-performance.html#use-the-production-build) suggests using the minified production build when deploying your app.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8d553eb-b942-4f2d-ba09-573c4b780bb7/4-react-devtools-warning-methods-performance-react-apps.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8d553eb-b942-4f2d-ba09-573c4b780bb7/4-react-devtools-warning-methods-performance-react-apps.png" sizes="100vw" caption="React Developer Tools’ “production build” warning (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8d553eb-b942-4f2d-ba09-573c4b780bb7/4-react-devtools-warning-methods-performance-react-apps.png'>Large preview</a>)" alt="React Developer Tools’ “production build” warning" >}}

### Avoid Anonymous Functions

Because anonymous functions aren’t assigned an identifier (via `const/let/var`), they aren’t persistent whenever a component inevitably gets rendered again. This causes JavaScript to allocate new memory each time this component is re-rendered, instead of allocating a single piece of memory only once, like when named functions are being used.

<pre><code class="language-javascript">import React from 'react';

// Don’t do this.
class Dont extends Component {
  render() {
    return (
      &lt;button onClick={() =&gt; console.log('Do not do this')}&gt;
        Don’t
      &lt;/button&gt;
    );
  }
}

// The better way
class Do extends Component {
  handleClick = () =&gt; {
    console.log('This is OK');
  }
  render() {
    return (
      &lt;button onClick={this.handleClick}&gt;
        Do
      &lt;/button&gt;
    );
  }
}
</code></pre>

The code above shows two different ways to make a button perform an action on click. The first code block uses an anonymous function in the `onClick()` prop, and this would affect performance. The second code block uses a named function in the `onClick()` function, which is the correct way in this scenario.

### Mounting And Unmounting Components Often Is Expensive

Using conditionals or tenaries to make a component disappear (i.e. to unmount it) is not advisable, because the component made to disappear will cause the browser to [repaint and reflow](https://developers.google.com/speed/docs/insights/browser-reflow). This is an expensive process because the positions and geometries of HTML elements in the document will have to be recalculated. Instead, we can use CSS’ `opacity` and `visibility` properties to hide the component. This way, the component will still be in the DOM but invisible, without any performance cost.

### Virtualize Long Lists

The [documentation suggests](https://reactjs.org/docs/optimizing-performance.html#virtualize-long-lists) that if you are rendering a list with a large amount of data, you should render a small portion of the data in the list at a time within the visible viewport. Then, you can render more data as the list is being scrolled; hence, the data is displayed only when it is in the viewport. This process is called “windowing”. In windowing, a small subset of rows are rendered at any given time. There are popular libraries for doing this, two of which are maintained by Brian Vaughn:

- [react-window](https://react-window.now.sh)
- [react-virtualized](https://bvaughn.github.io/react-virtualized/)

## Conclusion

There are several other methods of improving the performance of your React application. This article has discussed the most important and effective methods of performance optimization.

I hope you’ve enjoyed reading through this tutorial. You can learn more via the resources listed below. If you have any questions, leave them in the comments section below. I’ll be happy to answer every one of them.

### References And Related Resources

- “[Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab)”, React Docs
- “[Use React.memo Wisely](https://dmitripavlutin.com/use-react-memo-wisely/#:~:text=When%20to%20use%20React.&text=The%20best%20case%20of%20wrapping,render%20by%20a%20parent%20component.)”, Dmitri Pavlutin
- “[Performance Optimization Techniques in React](https://levelup.gitconnected.com/performance-optimization-techniques-in-react-31dee64c3b5)”, Niteesh Yadav
- “[Immutability in React: There’s Nothing Wrong With Mutating Objects](https://blog.logrocket.com/immutability-in-react-ebe55253a1cc/)”, Esteban Herrera
- “[10 Ways to Optimize Your React App’s Performance](https://blog.bitsrc.io/10-ways-to-optimize-your-react-apps-performance-e5e437c9abce)”, Chidume Nnamdi
- “[5 Tips to Improve the Performance of Your React Apps](https://www.digitalocean.com/community/tutorials/react-keep-react-fast)”, William Le

{{< signature "ks, ra, al, il" >}}
