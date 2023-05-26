---
title: 'Implementing Infinite Scroll And Image Lazy Loading In React'
slug: infinite-scroll-lazy-image-loading-react
author: chidi-orji
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86264878-3abc-4314-88b7-3a69f197b1be/infinite-scroll-lazy-image-loading-react.png
date: 2020-03-16T12:00:00.000Z
summary: >-
  In this tutorial, we’re going to learn how to use the `HTML` `Intersection Observer` API to implement infinite scrolling and image lazy loading in a React functional component. In the process, we’ll learn how to use some of React’s hooks and how to create Custom Hooks.
description: >-
  In this tutorial, we’re going to learn how to use the `HTML` `Intersection Observer` API to implement infinite scrolling and image lazy loading in a React functional component. In the process, we’ll learn how to use some of React’s hooks and how to create Custom Hooks.
categories:
  - API
  - React
  - Performance
---

If you have been looking for an alternative to pagination, [infinite scroll](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/) is a good consideration. In this article, we’re going to explore some use cases for the Intersection Observer API in the context of a React functional component. The reader should possess a working knowledge of [React functional components](https://reactjs.org/docs/components-and-props.html). Some familiarity with [React hooks](https://reactjs.org/docs/hooks-intro.html) will be beneficial but not required, as we will be taking a look at a few.

Our goal is that at the end of this article, we will have implemented infinite scroll and image lazy loading using a native HTML API. We would also have learned a few more things about React Hooks. With that you can be able to implement infinite scroll and image lazy loading in your React application where necessary.

Let’s get started.

<div class="c-felix-the-cat">
<h4 class="h3">Creating Maps With React And Leaflet</h4>
<p>Grasping information from a CSV or a JSON file isn’t only complicated, but is also tedious. Representing the same data in the form of visual aid is simpler. Shajia Abidi explains how powerful of a tool Leaflet is, and how a lot of different kinds of maps can be created. <a href="https://www.smashingmagazine.com/2020/02/javascript-maps-react-leaflet/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## The Intersection Observer API

According to the MDN docs, “the Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport”.

This API allows us to implement cool features such as infinite scroll and image lazy loading. The intersection observer is created by calling its constructor and passing it a callback and an options object. The callback is invoked whenever one element, called the `target`, intersects either the device viewport or a specified element, called the `root`. We can specify a custom root in the options argument or use the default value.

<pre><code class="language-javascript">let observer = new IntersectionObserver(callback, options);</code></pre>

The API is straightforward to use. A typical example looks like this:

<div class="break-out">

<pre><code class="language-javascript">var intObserver = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      console.log(entry)
      console.log(entry.isIntersecting) // returns true if the target intersects the root element
    })
  },
  {
    // default options
  }
);
let target = document.querySelector('#targetId');
intObserver.observe(target); // start observation</code></pre>
</div>

`entries` is a list of `IntersectionObserverEntry` objects. The `IntersectionObserverEntry` object describes an intersection change for one observed target element. Note that the callback should not handle any time-consuming task as it runs on the main thread.

The Intersection Observer API currently enjoys broad browser support, as shown on [caniuse](https://caniuse.com/#feat=intersectionobserver).

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd0c890-49b7-4589-8c91-22c778eecd37/fig-01-int-obs-browser-support.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd0c890-49b7-4589-8c91-22c778eecd37/fig-01-int-obs-browser-support.png" sizes="100vw" caption="Intersection Observer browser support. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd0c890-49b7-4589-8c91-22c778eecd37/fig-01-int-obs-browser-support.png'>Large preview</a>)" alt="" >}}

You can read more about the API in the links provided in the resources section.

Let us now look at how to make use of this API in a real React app. The final version of our app will be a page of pictures that scrolls infinitely and will have each image loaded lazily.

## Making API Calls With The `useEffect` Hook

To get started, clone the starter project from [this URL](https://github.com/chidimo/React-Infinite-Scroll-and-Lazy-Loading). It has minimal setup and a few styles defined. I've also added a link to `Bootstrap`'s CSS in the `public/index.html` file as I'll be using its classes for styling.

Feel free to create a new project if you like. Make sure you have `yarn` package manager installed if you want to follow with the repo. You can find the installation instructions for your specific operating system [here](https://classic.yarnpkg.com/en/docs/install).

For this tutorial, we're going to be grabbing pictures from a public API and displaying them on the page. We will be using the [Lorem Picsum](https://picsum.photos/) APIs.

For this tutorial, we'll be using the endpoint, [`https://picsum.photos/v2/list?page=0&limit=10`](https://picsum.photos/v2/list?page=0&limit=10), which returns an array of picture objects. To get the next ten pictures, we change the value of page to 1, then 2, and so on.

We will now build the App component piece by piece. 

Open up `src/App.js` and enter the following code.

<div class="break-out">

<pre><code class="language-javascript">import React, { useEffect, useReducer } from 'react';

import './index.css';

function App() {
  const imgReducer = (state, action) => {
    switch (action.type) {
      case 'STACK_IMAGES':
        return { ...state, images: state.images.concat(action.images) }
      case 'FETCHING_IMAGES':
        return { ...state, fetching: action.fetching }
      default:
        return state;
    }
  }
  const [imgData, imgDispatch] = useReducer(imgReducer,{ images:[], fetching: true})
  // next code block goes here
}</code></pre>
</div>

Firstly, we define a reducer function, `imgReducer`. This reducer handles two actions. 

1. The `STACK_IMAGES` action concatenates the `images` array.
2. `FETCHING_IMAGES` action toggles the value of the `fetching` variable between `true` and `false`.

The next step is to wire up this reducer to a `useReducer` hook. Once that is done, we get back two things:

1. `imgData`, which contains two variables: `images` is the array of picture objects. `fetching` is a boolean which tells us if the API call is in progress or not.
2. `imgDispatch`, which is a function for updating the reducer object.

You can learn more about the `useReducer` hook in the [React documentation](https://reactjs.org/docs/hooks-reference.html#usereducer).

The next part of the code is where we make the API call. Paste the following code below the previous code block in `App.js`.

<div class="break-out">

<pre><code class="language-javascript">// make API calls
useEffect(() => {
  imgDispatch({ type: 'FETCHING_IMAGES', fetching: true })
  fetch('https://picsum.photos/v2/list?page=0&limit=10')
    .then(data => data.json())
    .then(images => {
      imgDispatch({ type: 'STACK_IMAGES', images })
      imgDispatch({ type: 'FETCHING_IMAGES', fetching: false })
    })
    .catch(e => {
      // handle error
      imgDispatch({ type: 'FETCHING_IMAGES', fetching: false })
      return e
    })
}, [ imgDispatch ])

// next code block goes here</code></pre>
</div>

Inside the `useEffect` hook, we make a call to the API endpoint with `fetch` API. We then update the images array with the result of the API call by dispatching the `STACK_IMAGES` action.  We also dispatch the `FETCHING_IMAGES` action once the API call completes.

The next block of code defines the return value of the function. Enter the following code after the `useEffect` hook.

<div class="break-out">

<pre><code class="language-javascript">return (
  &lt;div className=""&gt;
    &lt;nav className="navbar bg-light"&gt;
      &lt;div className="container"&gt;
        &lt;a className="navbar-brand" href="/#"&gt;
          &lt;h2&gt;Infinite scroll + image lazy loading&lt;/h2&gt;
        &lt;/a&gt;
      &lt;/div&gt;
    &lt;/navv
    &lt;div id='images' className="container"&gt;
      &lt;div className="row"&gt;
        {imgData.images.map((image, index) =&gt; {
          const { author, download_url } = image
          return (
            &lt;div key={index} className="card"&gt;
              &lt;div className="card-body "&gt;
                &lt;img
                  alt={author}
                  className="card-img-top"
                  src={download_url}
                /&gt;
              &lt;/div&gt;
              &lt;div className="card-footer"&gt;
                &lt;p className="card-text text-center text-capitalize text-primary"&gt;Shot by: {author}&lt;/p&gt;
              &lt;/div&gt;
            &lt;/div&gt;
          )
        })}
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
);</code></pre>
</div>

To display the images, we map over the images array in the `imgData` object.

Now start the app and view the page in the browser. You should see the images nicely displayed in a responsive grid.

The last bit is to export the App component.

<pre><code class="language-javascript">export default App;</code></pre>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ebe219c-3815-407e-86f3-ef387a1a2996/fig-02-images-displayed.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ebe219c-3815-407e-86f3-ef387a1a2996/fig-02-images-displayed.png" sizes="100vw" caption="Pictures in responsive grid. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ebe219c-3815-407e-86f3-ef387a1a2996/fig-02-images-displayed.png'>Large preview</a>)" alt="" >}}

The corresponding branch at this point is [01-make-api-calls](https://github.com/chidimo/React-Infinite-Scroll-and-Lazy-Loading/tree/01-make-api-calls).

Let’s now extend this by displaying more pictures as the page scrolls.

{{% ad-panel-leaderboard %}}

## Implementing Infinite Scroll

We aim to present more pictures as the page scrolls. From the URL of the API endpoint, `https://picsum.photos/v2/list?page=0&limit=10`, we know that to get a new set of photos, we only need to increment the value of `page`. We also need to do this when we have run out of pictures to show. For our purpose here, we’ll know we have run out of images when we hit the bottom of the page. It’s time to see how the Intersection Observer API helps us achieve that.

Open up `src/App.js` and create a new reducer, `pageReducer`, below `imgReducer`.

<div class="break-out">

<pre><code class="language-javascript">// App.js
const imgReducer = (state, action) => {
  ...
}
const pageReducer = (state, action) => {
  switch (action.type) {
    case 'ADVANCE_PAGE':
      return { ...state, page: state.page + 1 }
    default:
      return state;
  }
}
const [ pager, pagerDispatch ] = useReducer(pageReducer, { page: 0 })</code></pre>
</div>

We define only one action type. Each time the `ADVANCE_PAGE` action is triggered, the value of `page` is incremented by 1.

Update the URL in the `fetch` function to accept page numbers dynamically as shown below.

<pre><code class="language-javascript">fetch(`https://picsum.photos/v2/list?page=${pager.page}&limit=10`)</code></pre>

Add `pager.page` to the dependency array alongside `imgData`. Doing this ensures that the API call will run whenever `pager.page` changes.

<pre><code class="language-javascript">useEffect(() => {
...
}, [ imgDispatch, pager.page ])</code></pre>

After the `useEffect` hook for the API call, enter the below code. Update your import line as well.

<div class="break-out">

<pre><code class="language-javascript">// App.js
import React, { useEffect, useReducer, useCallback, useRef } from 'react';
useEffect(() => {
  ...
}, [ imgDispatch, pager.page ])

// implement infinite scrolling with intersection observer
let bottomBoundaryRef = useRef(null);
const scrollObserver = useCallback(
  node => {
    new IntersectionObserver(entries => {
      entries.forEach(en => {
        if (en.intersectionRatio > 0) {
          pagerDispatch({ type: 'ADVANCE_PAGE' });
        }
      });
    }).observe(node);
  },
  [pagerDispatch]
);
useEffect(() => {
  if (bottomBoundaryRef.current) {
    scrollObserver(bottomBoundaryRef.current);
  }
}, [scrollObserver, bottomBoundaryRef]);</code></pre>
</div>

We define a variable `bottomBoundaryRef` and set its value to `useRef(null)`. `useRef` lets variables preserve their values across component renders, i.e. the *current* value of the variable persists when the containing component re-renders. The only way to change its value is by re-assigning the `.current` property on that variable.

In our case, `bottomBoundaryRef.current` starts with a value of `null`. As the page rendering cycle proceeds, we set its current property to be the node `<div id='page-bottom-boundary'>`. 

We use the assignment statement `ref={bottomBoundaryRef}` to tell React to set `bottomBoundaryRef.current` to be the div where this assignment is declared.

Thus,

<pre><code class="language-javascript">bottomBoundaryRef.current = null</code></pre>

at the end of the rendering cycle, becomes:

<div class="break-out">

<pre><code class="language-javascript">bottomBoundaryRef.current = &lt;div id="page-bottom-boundary" style="border: 1px solid red;"&gt;&lt;/div&gt;</code></pre>
</div>

We shall see where this assignment is done in a minute.

Next, we define a `scrollObserver` function, in which to set the observer. This function accepts a `DOM` node to observe. The main point to note here is that whenever we hit the intersection under observation, we dispatch the `ADVANCE_PAGE` action. The effect is to increment the value of `pager.page` by 1. Once this happens, the `useEffect` hook that has it as a dependency is re-run. This re-run, in turn, invokes the fetch call with the new page number.

The event procession looks like this.

<blockquote>Hit intersection under observation&nbsp;&rarr; call <code>ADVANCE_PAGE</code> action&nbsp;&rarr; increment value of <code>pager.page</code> by 1&nbsp;&rarr; <code>useEffect</code> hook for fetch call runs&nbsp;&rarr; <code>fetch</code> call is run&nbsp;&rarr; returned images are concatenated to the <code>images</code> array.</blockquote>

We invoke `scrollObserver` in a `useEffect` hook so that the function will run only when any of the hook's dependencies change. If we didn't call the function inside a `useEffect` hook, the function would run on every page render.

Recall that `bottomBoundaryRef.current` refers to `<div id="page-bottom-boundary" style="border: 1px solid red;"></div>`. We check that its value is not null before passing it to `scrollObserver`. Otherwise, the `IntersectionObserver` constructor would return an error. 

Because we used `scrollObserver` in a `useEffect` hook, we have to wrap it in a `useCallback` hook to prevent un-ending component re-renders. You can learn more about useCallback in the React docs.

Enter the below code after the `<div id='images'>` div.

<div class="break-out">

<pre><code class="language-javascript">// App.js
&lt;div id='image'&gt;
...
&lt;/div&gt;
{imgData.fetching && (
  &lt;div className="text-center bg-secondary m-auto p-3"&gt;
    &lt;p className="m-0 text-white"&gt;Getting images&lt;/p&gt;
  &lt;/div&gt;
)}
&lt;div id='page-bottom-boundary' style={{ border: '1px solid red' }} ref={bottomBoundaryRef}&gt;&lt;/div&gt;</code></pre>
</div>

When the API call starts, we set `fetching` to `true`, and the text *Getting images* becomes visible. As soon as it finishes, we set `fetching` to `false`, and the text gets hidden. We could also trigger the API call before hitting the boundary exactly by setting a different `threshold` in the constructor options object. The red line at the end lets us see exactly when we hit the page boundary.

The corresponding branch at this point is [02-infinite-scroll](https://github.com/chidimo/React-Infinite-Scroll-and-Lazy-Loading/tree/02-infinite-scroll).

We will now implement image lazy loading.

{{% ad-panel-leaderboard %}}

## Implementing Image Lazy Loading

If you inspect the network tab as you scroll down, you’ll see that as soon as you hit the red line (the bottom boundary), the API call happens, and all the images start loading even when you haven’t gotten to viewing them. There are a variety of reasons why this might not be desirable behavior. We may want to save network calls until the user wants to see an image. In such a case, we could opt for loading the images *lazily,* i.e., we won’t load an image until it scrolls into view.

Open up `src/App.js`. Just below the infinite scrolling functions, enter the following code.

<div class="break-out">

<pre><code class="language-javascript">// App.js

// lazy loads images with intersection observer
// only swap out the image source if the new url exists
const imagesRef = useRef(null);
const imgObserver = useCallback(node => {
  const intObs = new IntersectionObserver(entries => {
    entries.forEach(en => {
      if (en.intersectionRatio > 0) {
        const currentImg = en.target;
        const newImgSrc = currentImg.dataset.src;
        // only swap out the image source if the new url exists
        if (!newImgSrc) {
          console.error('Image source is invalid');
        } else {
          currentImg.src = newImgSrc;
        }
        intObs.unobserve(node); // detach the observer when done
      }
    });
  })
  intObs.observe(node);
}, []);
useEffect(() => {
  imagesRef.current = document.querySelectorAll('.card-img-top');
  if (imagesRef.current) {
    imagesRef.current.forEach(img => imgObserver(img));
  }
}, [imgObserver, imagesRef, imgData.images]);
</code></pre>
</div>

As with `scrollObserver`, we define a function, `imgObserver`, which accepts a node to observe. When the page hits an intersection, as determined by `en.intersectionRatio > 0`, we swap the image source on the element. Notice that we first check if the new image source exists before doing the swap. As with the `scrollObserver` function, we wrap imgObserver in a `useCallback` hook to prevent un-ending component re-render.

Also note that we stop observing an `img` element once we’re done with the substitution. We do this with the `unobserve` method.

In the following `useEffect` hook, we grab all the images with a class of `.card-img-top` on the page with `document.querySelectorAll`. Then we iterate over each image and set an observer on it.

Note that we added `imgData.images` as a dependency of the `useEffect` hook. When this changes it triggers the `useEffect` hook and in turn `imgObserver` get called with each `<img className='card-img-top'>` element.

Update the `<img className='card-img-top'/>` element as shown below.

<div class="break-out">

<pre><code class="language-javascript">&lt;img
  alt={author}
  data-src={download_url}
  className="card-img-top"
  src={'https://picsum.photos/id/870/300/300?grayscale&blur=2'}
/&gt;</code></pre>
</div>

We set a default source for every `<img className='card-img-top'/>` element and store the image we want to show on the `data-src` property. The default image usually has a small size so that we're downloading as little as possible.  When the `<img/>`  element comes into view, the value on the `data-src` property replaces the default image.

In the picture below, we see the default lighthouse image still showing in some of the spaces.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ff0bc9-62c7-4c39-ad43-3acd9643d586/fig-03-showing-default-image.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ff0bc9-62c7-4c39-ad43-3acd9643d586/fig-03-showing-default-image.png" sizes="100vw" caption="Images being lazily loaded. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ff0bc9-62c7-4c39-ad43-3acd9643d586/fig-03-showing-default-image.png'>Large preview</a>)" alt="" >}}

The corresponding branch at this point is [03-lazy-loading](https://github.com/chidimo/React-Infinite-Scroll-and-Lazy-Loading/tree/03-lazy-loading).

Let's now see how we can abstract all these functions so that they're re-usable.

## Abstracting Fetch, Infinite Scroll And Lazy Loading Into Custom Hooks

We have successfully implemented fetch, infinite scroll, and image lazy loading. We might have another component in our application that needs similar functionality. In that case, we could abstract and reuse these functions. All we have to do is move them inside a separate file and import them where we need them. We want to turn them into Custom Hooks.

The React documentation defines a Custom Hook as a JavaScript function whose name starts with `"use"` and that may call other hooks. In our case, we want to create three hooks, `useFetch`, `useInfiniteScroll`, `useLazyLoading`.

Create a file inside the `src/` folder. Name it `customHooks.js` and paste the code below inside.

<div class="break-out">

<pre><code class="language-javascript">// customHooks.js

import { useEffect, useCallback, useRef } from 'react';
// make API calls and pass the returned data via dispatch
export const useFetch = (data, dispatch) => {
  useEffect(() => {
    dispatch({ type: 'FETCHING_IMAGES', fetching: true });
    fetch(`https://picsum.photos/v2/list?page=${data.page}&limit=10`)
      .then(data => data.json())
      .then(images => {
        dispatch({ type: 'STACK_IMAGES', images });
        dispatch({ type: 'FETCHING_IMAGES', fetching: false });
      })
      .catch(e => {
        dispatch({ type: 'FETCHING_IMAGES', fetching: false });
        return e;
      })
  }, [dispatch, data.page])
}

// next code block here</code></pre>
</div>

The `useFetch` hook accepts a dispatch function and a data object. The dispatch function passes the data from the API call to the `App` component, while the data object lets us update the API endpoint URL.

<div class="break-out">

<pre><code class="language-javascript">// infinite scrolling with intersection observer
export const useInfiniteScroll = (scrollRef, dispatch) => {
  const scrollObserver = useCallback(
    node => {
      new IntersectionObserver(entries => {
        entries.forEach(en => {
          if (en.intersectionRatio > 0) {
            dispatch({ type: 'ADVANCE_PAGE' });
          }
        });
      }).observe(node);
    },
    [dispatch]
  );
  useEffect(() => {
    if (scrollRef.current) {
      scrollObserver(scrollRef.current);
    }
  }, [scrollObserver, scrollRef]);
}

// next code block here</code></pre>
</div>

The `useInfiniteScroll` hook accepts a `scrollRef` and a `dispatch` function. The `scrollRef` helps us set up the observer, as already discussed in the section where we implemented it. The dispatch function gives a way to trigger an action that updates the page number in the API endpoint URL.

<div class="break-out">

<pre><code class="language-javascript">// lazy load images with intersection observer
export const useLazyLoading = (imgSelector, items) => {
  const imgObserver = useCallback(node => {
  const intObs = new IntersectionObserver(entries => {
    entries.forEach(en => {
      if (en.intersectionRatio > 0) {
        const currentImg = en.target;
        const newImgSrc = currentImg.dataset.src;
        // only swap out the image source if the new url exists
        if (!newImgSrc) {
          console.error('Image source is invalid');
        } else {
          currentImg.src = newImgSrc;
        }
        intObs.unobserve(node); // detach the observer when done
      }
    });
  })
  intObs.observe(node);
  }, []);
  const imagesRef = useRef(null);
  useEffect(() => {
    imagesRef.current = document.querySelectorAll(imgSelector);
    if (imagesRef.current) {
      imagesRef.current.forEach(img => imgObserver(img));
    }
  }, [imgObserver, imagesRef, imgSelector, items])
}
</code></pre>
</div>

The `useLazyLoading` hook receives a selector and an array. The selector is used to find the images. Any change in the array triggers the `useEffect` hook that sets up the observer on each image.

We can see that it is the same functions we have in `src/App.js` that we have extracted to a new file. The good thing now is that we can pass arguments dynamically. Let’s now use these custom hooks in the App component.

Open `src/App.js`. Import the custom hooks and delete the functions we defined for fetching data, infinite scroll, and image lazy loading. Leave the reducers and the sections where we make use of `useReducer`. Paste in the below code.

<div class="break-out">

<pre><code class="language-javascript">// App.js

// import custom hooks
import { useFetch, useInfiniteScroll, useLazyLoading } from './customHooks'

  const imgReducer = (state, action) => { ... } // retain this
  const pageReducer = (state, action) => { ... } // retain this
  const [pager, pagerDispatch] = useReducer(pageReducer, { page: 0 }) // retain this
  const [imgData, imgDispatch] = useReducer(imgReducer,{ images:[], fetching: true }) // retain this

let bottomBoundaryRef = useRef(null);
useFetch(pager, imgDispatch);
useLazyLoading('.card-img-top', imgData.images)
useInfiniteScroll(bottomBoundaryRef, pagerDispatch);

// retain the return block
return (
  ...
)</code></pre>
</div>

We have already talked about `bottomBoundaryRef` in the section on infinite scroll. We pass the `pager` object and the `imgDispatch` function to `useFetch`. `useLazyLoading` accepts the class name `.card-img-top`. Note the `.` included in the class name. By doing this, we don’t need to specify it `document.querySelectorAll`. `useInfiniteScroll` accepts both a ref and the dispatch function for incrementing the value of `page`.

The corresponding branch at this point is [04-custom-hooks](https://github.com/chidimo/React-Infinite-Scroll-and-Lazy-Loading/tree/04-custom-hooks).

## Conclusion

HTML is getting better at providing nice APIs for implementing cool features. In this post, we’ve seen how easy it is to use the intersection observer in a React functional component. In the process, we learned how to use some of React’s hooks and how to write our own hooks.

### Resources

- “[Infinite Scroll + Image Lazy Loading](https://github.com/chidimo/React-Infinite-Scroll-and-Lazy-Loading),” Orji Chidi Matthew, GitHub
- “[Infinite Scrolling, Pagination Or “Load More” Buttons? Usability Findings In eCommerce](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/),” Christian Holst, Smashing Magazine
- “[Lorem Picsum](https://picsum.photos/),” David Marby & Nijiko Yonskai
- “[IntersectionObserver’s Coming Into View](https://developers.google.com/web/updates/2016/04/intersectionobserver),” Surma, Web Fundamentals
- [Can I Use...`IntersectionObserver`](https://caniuse.com/#feat=intersectionobserver)
- “[Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API),” MDN web docs
- “[Components And Props](https://reactjs.org/docs/components-and-props.html),” React
- “[`useCallback`](https://reactjs.org/docs/hooks-reference.html#usecallback),” React
- “[`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer),” React

{{< signature "ks, ra, yk, il" >}}
