---
title: 'How To Create A Custom React Hook To Fetch And Cache Data'
slug: custom-react-hook-fetch-cache-data
author: ademola-adegbuyi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c5dfa02-5d43-4b36-940d-2bdff23e139e/custom-react-hook-fetch-cache-data.png
date: 2020-07-13T09:00:00.000Z
summary: >-
  There is a high possibility that a lot of components in your React application will have to make calls to an API to retrieve data that will be displayed to your users. It’s already possible to do that using the `componentDidMount()` lifecycle method, but with the introduction of Hooks, you can build a custom hook that will fetch and cache the data for you. That’s what this tutorial will cover.
description: >-
  There is a high possibility that a lot of components in your React application will have to make calls to an API to retrieve data that will be displayed to your users. It’s already possible to do that using the `componentDidMount()` lifecycle method, but with the introduction of Hooks, you can build a custom hook which will fetch and cache the data for you. That’s what this tutorial will cover.
categories:
  - React
  - React Hooks
  - Tools
---

If you are a newbie to React Hooks, you can start by checking the [official documentation](https://reactjs.org/docs/hooks-intro.html) to get a grasp of it. After that, I’d recommend reading Shedrack Akintayo’s “[Getting Started With React Hooks API](https://www.smashingmagazine.com/2020/04/react-hooks-api-guide/)”. To ensure you’re following along, there is also an article written by Adeneye David Abiodun that covers [best practices with React Hooks](https://www.smashingmagazine.com/2020/04/react-hooks-best-practices/) which I’m sure will prove to be useful to you.

Throughout this article, we’ll be making use of [Hacker News Search API](https://hn.algolia.com/api) to build a custom hook which we can use to fetch data. While this tutorial will cover the Hacker News Search API, we’ll have the hook work in a way that it will return response from any *valid* API link we pass to it.

<div class="c-felix-the-cat">
<h4 class="h3">Best React Practices</h4>
<p>React is a fantastic JavaScript library for building rich user interfaces. It provides a great component abstraction for organizing your interfaces into well-functioning code, and there’s just about anything you can use it for. <a href="https://www.smashingmagazine.com/category/react" class="btn btn--medium btn--blue">Read a related article on React&nbsp;&rarr;</a></p>
</div>

## Fetching Data In A React Component

Before React hooks, it was conventional to fetch initial data in the `componentDidMount()` lifecycle method, and data based on prop or state changes in `componentDidUpdate()` lifecycle method. 

Here’s how it works:

<div class="break-out">

<pre><code class="language-javascript">componentDidMount() {
  const fetchData = async () =&gt; {
    const response = await fetch(
      `https://hn.algolia.com/api/v1/search?query=JavaScript`
    );
    const data = await response.json();
    this.setState({ data });
  };
  
  fetchData();
}


componentDidUpdate(previousProps, previousState) {
    if (previousState.query !== this.state.query) {
      const fetchData = async () =&gt; {
        const response = await fetch(
          `https://hn.algolia.com/api/v1/search?query=${this.state.query}`
        );
        const data = await response.json();
        this.setState({ data });
      };

      fetchData();
    }
  }
</code></pre>
</div>

The `componentDidMount` lifecycle method gets invoked as soon as the component gets mounted, and when that is done, what we did was to make a request to search for “JavaScript” via the Hacker News API and update the state based on the response.

The `componentDidUpdate` lifecycle method, on the other hand, gets invoked when there’s a change in the component. We compared the previous query in the state with the current query to prevent the method from getting invoked every time we set “data” in state. One thing we get from using hooks is to combine both lifecycle methods in a cleaner way &mdash; meaning that we won’t need to have two lifecycle methods for when the component mounts and when it updates.

{{% feature-panel %}} 

## Fetching Data With `useEffect` Hook

The `useEffect` hook gets invoked as soon as the component is mounted. If we need the hook to rerun based on some prop or state changes, we’ll need to pass them to the dependency array (which is the second argument of the `useEffect` hook).

Let’s explore how to fetch data with hooks:

<pre><code class="language-javascript">import { useState, useEffect } from 'react';

const [status, setStatus] = useState('idle');
const [query, setQuery] = useState('');
const [data, setData] = useState([]);

useEffect(() =&gt; {
    if (!query) return;

    const fetchData = async () =&gt; {
        setStatus('fetching');
        const response = await fetch(
            `https://hn.algolia.com/api/v1/search?query=${query}`
        );
        const data = await response.json();
        setData(data.hits);
        setStatus('fetched');
    };

    fetchData();
}, [query]);
</code></pre>

In the example above, we passed `query` as a dependency to our `useEffect` hook. By doing that, we’re telling `useEffect` to track query changes. If the previous `query` value isn’t the same as the current value, the `useEffect` get invoked again.

With that said, we’re also setting several `status` on the component as needed, as this will better convey some message to the screen based on some finite states `status`. In the **idle** state, we could let users know that they could make use of the search box to get started. In the **fetching** state, we could show a **spinner**. And, in the **fetched** state, we’ll render the data. 

It’s important to set the data before you attempt to set status to `fetched` so that you can prevent a flicker which occurs as a result of the data being empty while you’re setting the `fetched` status.

## Creating A Custom Hook

<blockquote>“A custom hook is a JavaScript function whose name starts with ‘use’ and that may call other Hooks.”<br /><br />&mdash; <a href="https://reactjs.org/docs/hooks-custom.html#extracting-a-custom-hook">React Docs</a></blockquote>

That’s really what it is, and along with a JavaScript function, it allows you to reuse some piece of code in several parts of your app. 

The definition from the React Docs has given it away but let’s see how it works in practice with a counter custom hook:

<pre><code class="language-javascript">const useCounter = (initialState = 0) =&gt; {
      const [count, setCount] = useState(initialState);
      const add = () =&gt; setCount(count + 1);
      const subtract = () =&gt; setCount(count - 1);
      return { count, add, subtract };
};
</code></pre>

Here, we have a regular function where we take in an optional argument, set the value to our state, as well as add the `add` and the `subtract` methods that could be used to update it.

Everywhere in our app where we need a counter, we can call `useCounter` like a regular function and pass an `initialState` so we know where to start counting from. When we don’t have an initial state, we default to 0.

Here’s how it works in practice:

<pre><code class="language-javascript">import { useCounter } from './customHookPath';

const { count, add, subtract } = useCounter(100);

eventHandler(() =&gt; {
  add(); // or subtract();
});
</code></pre>

What we did here was to import our custom hook from the file we declared it in, so we could make use of it in our app. We set its initial state to 100, so whenever we call `add()`, it increases `count` by 1, and whenever we call `subtract()`, it decreases `count` by 1.

## Creating `useFetch` Hook

Now that we’ve learned how to create a simple custom hook, let’s extract our logic to fetch data into a custom hook.

<div class="break-out">

<pre><code class="language-javascript">const useFetch = (query) =&gt; {
    const [status, setStatus] = useState('idle');
    const [data, setData] = useState([]);

    useEffect(() =&gt; {
        if (!query) return;

        const fetchData = async () =&gt; {
            setStatus('fetching');
            const response = await fetch(
                `https://hn.algolia.com/api/v1/search?query=${query}`
            );
            const data = await response.json();
            setData(data.hits);
            setStatus('fetched');
        };

        fetchData();
    }, [query]);

    return { status, data };
};
</code></pre>
</div>

It’s pretty much the same thing we did above with the exception of it being a function that takes in `query` and returns `status` and `data`. And, that’s a `useFetch` hook that we could use in several components in our React application.

This works, but the problem with this implementation now is, it’s specific to Hacker News so we might just call it `useHackerNews`. What we intend to do is, to create a `useFetch` hook that can be used to call any URL. Let’s revamp it to take in a URL instead!

<pre><code class="language-javascript">const useFetch = (url) =&gt; {
    const [status, setStatus] = useState('idle');
    const [data, setData] = useState([]);

    useEffect(() =&gt; {
        if (!url) return;
        const fetchData = async () =&gt; {
            setStatus('fetching');
            const response = await fetch(url);
            const data = await response.json();
            setData(data);
            setStatus('fetched');
        };

        fetchData();
    }, [url]);

    return { status, data };
};
</code></pre>

Now, our useFetch hook is generic and we can use it as we want in our various components.

Here’s one way of consuming it:

<div class="break-out">

<pre><code class="language-javascript">const [query, setQuery] = useState('');

const url = query && `https://hn.algolia.com/api/v1/search?query=${query}`;
const { status, data } = useFetch(url);
</code></pre>
</div>
 
In this case, if the value of `query` is `truthy`, we go ahead to set the URL and if it’s not, we’re fine with passing undefined as it’d get handled in our hook. The effect will attempt to run once, regardless.

{{% ad-panel-leaderboard %}}

## Memoizing Fetched Data

Memoization is a technique we would use to make sure that we don’t hit the `hackernews` endpoint if we have made some kind of request to fetch it at some initial phase. Storing the result of expensive fetch calls will save the users some load time, therefore, increasing overall performance.

**Note**: *For more context, you could check out [Wikipedia’s explanation on Memoization](https://en.wikipedia.org/wiki/Memoization).*

Let’s explore how we could do that!

<pre><code class="language-javascript">const cache = {};

const useFetch = (url) =&gt; {
    const [status, setStatus] = useState('idle');
    const [data, setData] = useState([]);

    useEffect(() =&gt; {
        if (!url) return;

        const fetchData = async () =&gt; {
            setStatus('fetching');
            if (cache[url]) {
                const data = cache[url];
                setData(data);
                setStatus('fetched');
            } else {
                const response = await fetch(url);
                const data = await response.json();
                cache[url] = data; // set response in cache;
                setData(data);
                setStatus('fetched');
            }
        };

        fetchData();
    }, [url]);

    return { status, data };
};
</code></pre>

Here, we’re mapping URLs to their data. So, if we make a request to fetch some existing data, we set the data from our local cache, else, we go ahead to make the request and set the result in the cache. This ensures we do not make an API call when we have the data available to us locally. We’ll also notice that we’re killing off the effect if the URL is `falsy`, so it makes sure we don’t proceed to fetch data that doesn’t exist. We can’t do it before the `useEffect` hook as that will go against one of the rules of hooks, which is to always call hooks at the top level.

Declaring `cache` in a different scope works but it makes our hook go against the principle of a [pure function](https://www.sitepoint.com/functional-programming-pure-functions/). Besides, we also want to make sure that React helps in cleaning up our mess when we no longer want to make use of the component. We’ll explore `useRef` to help us in achieving that.

## Memoizing Data With `useRef`

<blockquote> “<code>useRef</code> is like a box that can hold a mutable value in its <code>.current property</code>.”<br /><br />&mdash; <a href="https://reactjs.org/docs/hooks-reference.html#useref">React Docs</a></blockquote>

With `useRef`, we can set and retrieve mutable values at ease and its value persists throughout the component’s lifecycle.

Let’s replace our cache implementation with some `useRef` magic!

<div class="break-out">

<pre><code class="language-javascript">const useFetch = (url) =&gt; {
    const cache = useRef({});
    const [status, setStatus] = useState('idle');
    const [data, setData] = useState([]);

    useEffect(() =&gt; {
        if (!url) return;
        const fetchData = async () =&gt; {
            setStatus('fetching');
            if (cache.current[url]) {
                const data = cache.current[url];
                setData(data);
                setStatus('fetched');
            } else {
                const response = await fetch(url);
                const data = await response.json();
                cache.current[url] = data; // set response in cache;
                setData(data);
                setStatus('fetched');
            }
        };

        fetchData();
    }, [url]);

    return { status, data };
};
</code></pre>
</div>

Here, our cache is now in our `useFetch` hook with an empty object as an initial value.

### Wrapping Up

Well, I did state that setting the data before setting the fetched status was a good idea, but there are two potential problems we could have with that, too:

1. Our unit test could fail as a result of the data array not being empty while we’re in the fetching state. React could actually batch state changes but it can’t do that if it’s triggered asynchronously;
2. Our app re-renders more than it should.

Let’s do a final clean-up to our `useFetch` hook.,We’re going to start by switching our `useState`s to a `useReducer`. Let’s see how that works!

<div class="break-out">

<pre><code class="language-javascript">const initialState = {
    status: 'idle',
    error: null,
    data: [],
};

const [state, dispatch] = useReducer((state, action) =&gt; {
    switch (action.type) {
        case 'FETCHING':
            return { ...initialState, status: 'fetching' };
        case 'FETCHED':
            return { ...initialState, status: 'fetched', data: action.payload };
        case 'FETCH_ERROR':
            return { ...initialState, status: 'error', error: action.payload };
        default:
            return state;
    }
}, initialState);
</code></pre>
</div>

Here, we added an initial state which is the initial value we passed to each of our individual `useState`s. In our `useReducer`, we check what type of action we want to perform, and set the appropriate values to state based on that.

This resolves the two problems we discussed earlier, as we now get to set the status and data at the same time in order to help prevent impossible states and unnecessary re-renders.

There’s just one more thing left: cleaning up our side effect. Fetch implements the Promise API, in the sense that it could be resolved or rejected. If our hook tries to make an update while the component has unmounted because of some `Promise` just got resolved, React would return `Can't perform a React state update on an unmounted component.` 

Let’s see how we can fix that with `useEffect` clean-up!

<div class="break-out">

<pre><code class="language-javascript">useEffect(() =&gt; {
    let cancelRequest = false;
    if (!url) return;

    const fetchData = async () =&gt; {
        dispatch({ type: 'FETCHING' });
        if (cache.current[url]) {
            const data = cache.current[url];
            dispatch({ type: 'FETCHED', payload: data });
        } else {
            try {
                const response = await fetch(url);
                const data = await response.json();
                cache.current[url] = data;
                if (cancelRequest) return;
                dispatch({ type: 'FETCHED', payload: data });
            } catch (error) {
                if (cancelRequest) return;
                dispatch({ type: 'FETCH_ERROR', payload: error.message });
            }
        }
    };

    fetchData();

    return function cleanup() {
        cancelRequest = true;
    };
}, [url]);
</code></pre>
</div>

Here, we set `cancelRequest` to `true` after having defined it inside the effect. So, before we attempt to make state changes, we first confirm if the component has been unmounted. If it has been unmounted, we skip updating the state and if it hasn’t been unmounted, we update the state. This will resolve the *React state update* error, and also prevent race conditions in our components. 

{{% ad-panel-leaderboard %}}

## Conclusion

We’ve explored several hooks concepts to help fetch and cache data in our components. We also went through cleaning up our `useEffect` hook which helps prevent a good number of problems in our app.

If you have any questions, please feel free to drop them in the comments section below!

- [*See the repo for this article&nbsp;&rarr;*](https://github.com/ooade/use-fetch-hook)

### References

- “[Introducing Hooks](https://reactjs.org/docs/hooks-intro.html),” React Docs
- “[Getting Started With The React Hooks API](https://www.smashingmagazine.com/2020/04/react-hooks-api-guide/),” Shedrack Akintayo
- “[Best Practices With React Hooks](https://www.smashingmagazine.com/2020/04/react-hooks-best-practices/),” Adeneye David Abiodun
- “[Functional Programming: Pure Functions](https://www.sitepoint.com/functional-programming-pure-functions/),” Arne Brasseur

{{< signature "ks, ra, yk, il" >}}
