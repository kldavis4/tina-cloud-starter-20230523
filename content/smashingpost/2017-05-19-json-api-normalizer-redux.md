---
title: 'json-api-normalizer: An Easy Way To Integrate The JSON API And Redux'
slug: json-api-normalizer-redux
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b7b031e-5006-42e8-b811-a36806746c27/data-model-diagram-500w-opt.png
date: 2017-05-19T15:55:42.000Z
author: yurydymov
description: >-
  As a front-end developer, for each and every application I work on, I need to
  decide **how to manage the data**. The problem can be broken down into the
  following three subproblems: Fetch data from the back end, store it somewhere
  locally in the front-end application, retrieve the data from the local store
  and format it as required by the particular view or screen.
categories:
  - JavaScript
  - React
  - Redux
  - API
  - JSON
---
1.  fetch data from the back end,
2.  store it somewhere locally in the front-end application,
3.  retrieve the data from the local store and format it as required by the particular view or screen.

This article sums up my experience with consuming data from JSON, the JSON API and GraphQL back ends, and it gives practical recommendations on how to manage front-end application data.

<div class="c-felix-the-cat">
<h4 class="h3">Creating Secure Password Resets With JSON Web Tokens</h4>
<p>Does your site still send password reminders via email? This should be a red flag to you, both as a user and a developer. Let’s look into how to create secure password resets with JSON web tokens. <a href="https://www.smashingmagazine.com/2017/11/creating-secure-password-resets-with-json-web-tokens/" class="btn btn--medium btn--blue">Read a related article →</a></p>
</div>

To illustrate my ideas and make the article closer to real-world use cases, **I’ll develop a very simple front-end application** by the end of the article. Imagine we’ve implemented a survey that asks the same pile of questions of many users. After each user has provided their answers, other users may comment on them if desired. Our web app will perform a request to the back end, store the fetched data in the local store and render the content on the page. To keep things simple, we will omit the answer-creation flow.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d323eb-d9bf-48df-bd53-ea6b7ee37e0c/sm-result-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae9d39df-91a9-4c5c-8ec1-77f06c816417/sm-result-800w-opt.png" width="800" height="710" alt="Simple Demo React Application we will build by the end of the article" /></a><figcaption>The simple React demo application that we will build by the end of this article (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d323eb-d9bf-48df-bd53-ea6b7ee37e0c/sm-result-large-opt.png">View large version</a>)</figcaption></figure>

<p>A live demo is also <a href="https://yury-dymov.github.io/json-api-react-redux-example/">available on GitHub</a></p>

{{% feature-panel %}}

## Back Story

In the last couple of years, I’ve participated in many front-end projects based on the React stack. We use [Redux](https://www.smashingmagazine.com/2016/06/an-introduction-to-redux/) to manage state not only because it is the most widely used solution in its category, according to the recent [State of JavaScript in 2016](https://stateofjs.com/2016/statemanagement/) survey, but it is also very lightweight, straightforward and predictable. Yes, sometimes it requires a lot more boilerplate code to be written than other state-management solutions; nevertheless, you can fully understand and control how your application works, which gives you a lot of freedom to implement any business logic and scenarios.

To give you some context, some time ago we tried [GraphQL](https://graphql.org/) and [Relay](https://facebook.github.io/relay/) in one of our proofs of concept. Don't get me wrong: It worked great. However, every time we wanted to implement a flow that was slightly different from the standard one, we ended up fighting with our stack, instead of delivering new features. I know that many things have changed since then, and Relay is a decent solution now, but we learned the hard way that **using simple and predictable tools works better for us** because we can plan our development process more precisely and better meet our [deadlines](https://www.smashingmagazine.com/2010/07/passing-the-holy-milestone-how-to-meet-deadlines/).

**Note:** _Before moving forward, I assume that you have some basic knowledge of state management and either Flux or Redux._

## Redux Best Practices

The best thing about Redux is that it is unopinionated about what kind of API you consume. You can even change your API from JSON to JSON API or GraphQL and back during development, and as long as you preserve your data model, it will not affect the implementation of your state management at all. This is possible because, before you send the API response to the store, you would process it in a certain way. Redux itself doesn't force you to do that; however, the community has identified and developed several **best practices based on real-world experience**. Following these practices will save you a lot of time by reducing the complexity of your applications and decreasing the number of bugs and edge cases.</p>

## Best Practice 1: Keep Data Flat In The Redux Store

Let's go back to the demo application and discuss the data model:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f53e9e0b-7bdb-4937-a445-5a11bfffdaa1/sm-diagram-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce86a88f-fb3b-483d-9614-9ce3b5151617/sm-diagram-800w-opt.png" width="800" height="677" alt="Data Model Diagram" /></a><figcaption>Data model diagram (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce86a88f-fb3b-483d-9614-9ce3b5151617/sm-diagram-800w-opt.png">View large version</a>)</figcaption>
</figure>

Here we have a `question` data object, which might have many `post` objects. Each `post` might have many `comment` objects. Each `post` and `comment` has one `author`, respectively.

Let's assume we have a back end that returns a typical JSON response. Very likely it would have a deeply nested structure. If you prefer to store your data in a similar manner in the store, you will sooner or later face many issues. For example, you might store the same object several times. You might have `post` and `comment` objects that share the same `author`. Your store would look like this:

<pre><code class="language-javascript">
{
  "text": "My Post",
  "author": {
    "name": "Yury",
    "avatar": "avatar1.png"
  },
  "comments": [
    {
      "text": "Awesome Comment",
      "author": {
            "name": "Yury",
        "avatar": "avatar1.png"
      }
    }
  ]
}
</code></pre>

As you can see, we store the same Author</code>object in several places, which not only requires more memory but also has negative side effects. Imagine if in the back end somebody changed the user's avatar. Instead of updating one object in the Redux store, you would now need to traverse the whole state and update all instances of the same object. Not only might it be very slow, but it would also require you to learn precisely the data object’s structure. 

Refactoring would be a nightmare as well. Another issue is that if you decided to reuse certain data objects for new views and they were nested in some other objects, then traversal implementation would be complex, slow and dirty.

Instead, we can store the data in a flattened structure. This way, each object would be stored only once, and we would have very easy access to any data.

<pre><code class="language-javascript">
{
  "post": [{
    "id": 1,
    "text": "My Post",
    "author": { "id": 1 },
    "comments": [ { "id": 1 } ]
  }],
  "comment": [{
    "id": 1,
    "text": "Awesome Comment"
  }],
  "author": [{
    "name": "Yury",
    "avatar": "avatar1.png",
    "id": 1
  }]
 }
</code></pre>

The same principles have been widely used in [relational database management systems](https://en.wikipedia.org/wiki/Relational_database_management_system) for many years.

### 2. Store Collections As Maps Whenever Possible

OK, so we’ve got the data in a nice flat structure. It is a very common practice to incrementally accumulate received data, so that we can reuse it later as a cache, to improve [performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/) or for [offline use](https://www.smashingmagazine.com/2016/02/making-a-service-worker/).

However, after merging new data in the existing storage, we need to select only relevant data objects for the particular view, not everything we’ve received so far. To achieve this, we can store the structure of each JSON document separately, so that we can quickly **figure out which data objects were provided in a particular request**. This structure would contain a list of the data object IDs, which we could use to fetch the data from the storage.

Let me illustrate this point. We will perform two requests to fetch a list of friends of two different users, Alice and Bob, and review the contents of our storage accordingly. To make things easier, let's assume that, in the beginning, the storage is empty.</p>

### /alice/friends Response

So, here we are getting the `User` data object with an ID of `1` and a name of `Mike`, which might be stored like this:

<pre><code class="language-javascript">
{
  "data": [{
    "type": "User",
    "id": "1",
    "attributes": {
      "name": "Mike"
    }
  }]
}
</code></pre>

### /bob/friends Response

Another request would return a `User` with the ID of `2` and the name of `Kevin`:

<pre><code class="language-javascript">
{
  "data": [{
    "type": "User",
    "id": "2",
    "attributes": {
      "name": "Kevin"
    }
  }]
}
</code></pre>

### Storage State

After merging, our storage would look like this:

<pre><code class="language-javascript">
{
  "users": [
    {
      "id": "1",
      "name": "Mike"
    },
    {
        "id": "2",
        "name": "Kevin"
    }
  ]
}
</code></pre>

The big question is, how can we distinguish from this point on which users are Alice’s friends and which are Bob’s?

### Storage State With Meta Data

We could preserve the structure of the JSON API document, so that we might quickly figure out which data objects in storage are relevant. Keeping this in mind, we could change the implementation of the storage so that it looks like this:

<pre><code class="language-javascript">
{
  "users": [
    {
      "id": "1",
      "name": "Mike"
    },
    {
        "id": "2",
        "name": "Kevin"
    }
  ],
  "meta": {
      "/alice/friends": [
        {
          "type": "User",
          "id": "1"
        }
      ],
      "/bob/friends": [
        {
          "type": "User",
          "id": "2"
        }
      ]
  }
}
</code></pre>

Now, we can read the meta data and fetch all mentioned data objects. Problem solved! Can we do better? Note that we are constantly doing three operations: insert, read and merge. Which data structure will perform best for us?

Let's briefly recap the operation’s complexities.

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
		<tr>
			<th>Type</th>
			<th>Add</th>
			<th>Delete</th>
			<th>Search</th>
			<th>Preserves Order</th>
		</tr>
</thead>
<tbody>
		<tr>
			<td>Map</td>
			<td>O(1)</td>
			<td>O(1)</td>
			<td>O(1)</td>
			<td>No</td>
		</tr>
		<tr>
			<td>Array</td>
			<td>O(1)</td>
			<td>O(n)</td>
			<td>O(n)</td>
			<td>Yes</td>
		</tr>
	</tbody>
</table>

**Note:** _If you are not familiar with [Big O notation](https://en.wikipedia.org/wiki/Big_O_notation), `n` here means the number of data objects, `O(1)` means that the operation will take relatively the same amount of time regardless of the data set size, and `O(n)` means that the operation’s execution time is linearly dependent on the data set’s size._

As we can see, maps will work a lot better than arrays because all operations have a complexity of `O(1)`, instead of `O(n)`. If the order of data objects is important, we still can use maps for data handling and save the ordering information in the meta data. Maps can also be easily transformed into arrays and sorted, if required.

Let’s reimplement the storage mentioned above and use a map instead of an array for the `User` data object.</p>

### Storage State Revised

<pre><code class="language-javascript">
{
  "users": {
      "1": {
        "name": "Mike"
      },
      "2": {
        "name": "Kevin"
      }
  },
  "meta": {
      "/alice/friends": [
        {
          "type": "User",
          "id": "1"
        }
      ],
      "/bob/friends": [
        {
          "type": "User",
           "id": "2"
        }
      ]
  }
}
</code></pre>

Now, instead of iterating over the whole array to find a particular user, we can get it by ID almost instantly.</p>

## Processing The Data And JSON API

As you can imagine, there should be a widely used solution to convert JSON documents to a Redux-friendly form. The [Normalizr](https://github.com/paularmstrong/normalizr) library was initially developed by Dan Abramov, the author of Redux, for this purpose. You have to provide a JSON document and the scheme to “normalize” the function, and it will return the data in a nice flat structure, which we can save in the Redux store.

We’ve used this approach in many projects, and while it works great if your data model is known in advance and won’t change much within the application’s lifecycle, it dramatically fails if things are too dynamic. For example, when you are prototyping, developing a proof of concept or creating a new product, the data model will change very frequently to fit new requirements and change requests. Each back-end change should be reflected in an update to the Normalizr scheme. Because of this, several times I ended up fighting with my front-end app to fix things, rather than working on new features.

Are there any alternatives? We tried out GraphQL and the JSON API.

While GraphQL seems very promising and might be an interesting choice, we were not able to adopt it at the time because our APIs were being consumed by many third parties, and we couldn’t just drop the REST approach.

Let's briefly discuss the [JSON API](https://jsonapi.org/) standard.</p>

## JSON API Vs. Typical Web Services

Here are the JSON API’s main features:

*   Data is represented in a flat structure, with relationships no more than one level deep.
*   Data objects are typified.
*   The specification defines pagination, sorting and data-filtering features out of the box.</p>

### A Typical JSON Document

<pre><code class="language-javascript">
{
  "id": "123",
  "author": {
    "id": "1",
    "name": "Paul"
  },
  "title": "My awesome blog post",
  "comments": [
    {
      "id": "324",
      "text": "Great job, bro!",
      "commenter": {
        "id": "2",
        "name": "Nicole"
      }
    }
  ]
}
</code></pre>

### JSON API Document

<pre><code class="language-javascript">
{
  "data": [{
     "type": "post",
     "id": "123",
     "attributes": {
         "id": 123,
         "title": "My awesome blog post"
     },
     "relationships": {
         "author": {
           "type": "user",
           "id": "1"
         },
         "comments": {
           "type":  "comment",
           "id": "324"
         }
     }
  }],
  "included": [{
      "type": "user",
      "id": "1",
      "attributes": {
        "id": 1,
        "name": "Paul"
      }
  }, {
    "type": "user",
    "id": "2",
    "attributes": {
      "id": 2,
      "name": "Nicole"
    }
  }, {
    "type": "comment",
    "id": "324",
    "attributes": {
      "id": 324,
      "text": "Great job!"
    },
    "relationships": {
      "commenter": {
        "type": "user",
        "id": "2"
      }
    }
  }]
}
</code></pre>

The JSON API might seem too verbose compared to traditional JSON, right?

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
		<tr>
			<th>Type</th>
			<th>Raw (bytes)</th>
			<th>Gzipped (bytes)</th>
		</tr>
</thead>
<tbody>
		<tr>
			<td>Typical JSON</td>
			<td>264</td>
			<td>170</td>
		</tr>
		<tr>
			<td>JSON API</td>
			<td>771</td>
			<td>293</td>
		</tr>
	</tbody>
</table>

While the raw size difference might be remarkable, the Gzipped sizes are much closer to each other.

Keep in mind that it is also possible to develop a contrived example whose size in a typical JSON format is greater than that of the JSON API. Imagine dozens of blog posts that share the same author. In a typical JSON document, you would have to store the `author` object for each `post` object, whereas in the JSON API format, the `author` object would be stored only once.

The bottom line is, yes, the size of JSON API document on average is bigger, but it shouldn't be considered an issue. Typically, you will be dealing with structured data, which compresses to one fifth in size or more and which is also relatively small thanks to pagination.

Let's discuss the advantages:

*   First of all, the JSON API returns data in a flat form, with no more than one level of relationships. This helps to avoid redundancy and guarantees that each unique object will be stored in a document only once. This approach is a perfect match for Redux best practices, and we will use this feature soon.
*   Secondly, data is provided in the form of typified objects, which means that on the client side you don't need to implement parsers or define schemes like you do with [Normalizr](https://github.com/paularmstrong/normalizr). This will make your front-end apps more flexible to changes in data structure and will require less effort on your side to adapt the application to new requirements.
*   Thirdly, the JSON API specification defines a `links` object, which helps with moving pagination and with filtering and sorting features from your application to JSON API clients. An optional `meta` object is also available, where you can define your app-specific payload.</p>

## JSON API And Redux

Redux and the JSON API work great when used together; they complement each other well.

The JSON API provides data in a flat structure by definition, which conforms nicely with Redux best practices. Data comes typified, so that it can be naturally saved in Redux’s storage in a map with the format `type` → map of objects.

So, are we missing anything?

Despite the fact that dividing data objects into two types, “data” and “included,” might make some sense for the application, we can't afford to store them as two separate entities in the Redux store, because then the same data objects would be stored more than once, which violates Redux best practiсes.

As we discussed, the JSON API also returns a collection of objects in the form of an array, but for the Redux store, using a map is a lot more suitable.

To resolve these issues, consider using my [json-api-normalizer](https://github.com/yury-dymov/json-api-normalizer) library.

Here are the main features of json-api-normalizer:

*   Merge data and included fields, normalizing the data.
*   Collections are converted into maps in a form a `id` => `object`.
*   The response’s original structure is stored in a special `meta` object

First of all, a distinction between data and included data objects was introduced in the JSON API specification, to resolve issues with recursive structures and circular dependencies. Secondly, most of the time, **data in Redux is incrementally updated**, which helps to improve performance, and it has offline support. However, as we work with the same data objects in our application, sometimes it is not possible to distinguish which data objects we should use for a particular view. json-api-normalizer can store a web service response’s structure in a special `meta` field, so that you can unambiguously determine which data objects were fetched for a particular API request.</p>

## Implementing The Demo App

**Note:** _I assume that you have some practical experience with React and Redux._

Once again, we will build a very simple web app that will render the survey data provided by the back end in JSON API format.

We will start with the boilerplate, which has everything we need for the basic React app; we will implement Redux middleware to process the JSON API documents; we’ll provide the reducers data in an appropriate format; and we’ll build a simple UI on top of that.

First of all, we need a back end with JSON API support. Because this article is fully dedicated to front-end development, I’ve prebuilt a publicly available data source, so that we can focus on our web app. If you are interested, you can check the [source code](https://github.com/yury-dymov/phoenix-json-api-example). Note that many [JSON API implementation libraries](https://jsonapi.org/implementations/) are available for all kinds of technology stacks, so choose the one that works best for you.

My demo web service gives us two questions. The first one has two answers, and the second has three. The second answer to the first question has three comments.

The web service’s output will be converted to something similar to [Heroku’s example](https://phoenix-json-api-example.herokuapp.com/api/test) after the user presses the button and the data is successfully fetched.</p>

## 1\. Download The Boilerplate

To reduce time in configuring the web app, I’ve developed a [small React boilerplate](https://github.com/yury-dymov/json-api-react-redux-example/tree/initial) that can be used as a starting point.

Let's clone the repository.

<pre><code class="language-bash">
git clone https://github.com/yury-dymov/json-api-react-redux-example.git --branch initial
</code></pre>

Now we have the following:

*   React and ReactDOM;
*   Redux and Redux DevTools;
*   Webpack;
*   ESLint;
*   Babel;
*   an entry point to the application, two simple components, ESLint configuration, Webpack configuration and Redux store initialization;
*   definition CSS for all components, which we are going to develop;

Everything should work out of the box, with no action needed on your part.

To start the application, type this in the console:

<pre><code class="language-bash">
npm run webpack-dev-server
</code></pre>

Then, open [https://localhost:8050](https://localhost:8050) in a browser.</p>

## 2\. API Integration

Let's start with developing Redux middleware that will interact with API. We will use json-api-normalizer here to adhere to the don't-repeat-yourself (DRY) principle; otherwise, we would have to use it over and over again in many Redux actions.</p>

### src/redux/middleware/api.js

<pre><code class="language-javascript">
import fetch from 'isomorphic-fetch';
import normalize from 'json-api-normalizer';

const API_ROOT = 'https://phoenix-json-api-example.herokuapp.com/api';

export const API_DATA_REQUEST = 'API_DATA_REQUEST';
export const API_DATA_SUCCESS = 'API_DATA_SUCCESS';
export const API_DATA_FAILURE = 'API_DATA_FAILURE';

function callApi(endpoint, options = {}) {
  const fullUrl = (endpoint.indexOf(API_ROOT) === -1) ? API_ROOT + endpoint : endpoint;

  return fetch(fullUrl, options)
    .then(response => response.json()
      .then((json) => {
        if (!response.ok) {
          return Promise.reject(json);
        }

        return Object.assign({}, normalize(json, { endpoint }));
      }),
    );
}

export const CALL_API = Symbol('Call API');

export default function (store) {
  return function nxt(next) {
    return function call(action) {
      const callAPI = action[CALL_API];

      if (typeof callAPI === 'undefined') {
        return next(action);
      }

      let { endpoint } = callAPI;
      const { options } = callAPI;

      if (typeof endpoint === 'function') {
        endpoint = endpoint(store.getState());
      }

      if (typeof endpoint !== 'string') {
        throw new Error('Specify a string endpoint URL.');
      }

      const actionWith = (data) => {
        const finalAction = Object.assign({}, action, data);
        delete finalAction[CALL_API];
        return finalAction;
      };

      next(actionWith({ type: API_DATA_REQUEST, endpoint }));

      return callApi(endpoint, options || {})
        .then(
          response => next(actionWith({ response, type: API_DATA_SUCCESS, endpoint })),
          error => next(actionWith({ type: API_DATA_FAILURE, error: error.message || 'Something bad happened' })),
        );
    };
  };
}
</code></pre>

Once the data is returned from the API and parsed, we can convert it to a Redux-friendly format with json-api-normalizer and forward it to the Redux actions.

**Note:** _This code was copied and pasted from a [real-world Redux instance](https://github.com/reactjs/redux/blob/master/examples/real-world/src/middleware/api.js), with small adjustments to add json-api-normalizer. Now you can see that integration with json-api-normalizer is simple and straightforward._

### src/redux/configureStore.js

Let's adjust the Redux store’s configuration:

<pre><code class="language-javascript">
+++ import api from './middleware/api';

export default function (initialState = {}) {
  const store = createStore(rootReducer, initialState, compose(
--- applyMiddleware(thunk),
+++ applyMiddleware(thunk, api),
    DevTools.instrument(),
</code></pre>

### src/redux/actions/post.js

Now we can implement our first action, which will request data from the back end:

<pre><code class="language-javascript">
import { CALL_API } from '../middleware/api';

export function test() {
  return {
    [CALL_API]: {
      endpoint: '/test',
    },
  };
}
</code></pre>

### src/redux/reducers/data.js

Let's implement the reducer, which will merge the data provided from the back end into the Redux store:

<pre><code class="language-javascript">
import merge from 'lodash/merge';
import { API_DATA_REQUEST, API_DATA_SUCCESS } from '../middleware/api';

const initialState = {
  meta: {},
};

export default function (state = initialState, action) {
  switch (action.type) {
    case API_DATA_SUCCESS:
      return merge(
        {},
        state,
        merge({}, action.response, { meta: { [action.endpoint]: { loading: false } } }),
      );
    case API_DATA_REQUEST:
      return merge({}, state, { meta: { [action.endpoint]: { loading: true } } });
    default:
      return state;
  }
}
</code></pre>

### src/redux/reducers/data.js

Now we need to add our reducer to the root reducer:

<pre><code class="language-javascript">
import { combineReducers } from 'redux';
import data from './data';

export default combineReducers({
  data,
});
</code></pre>

### src/components/Content.jsx

The model layer is done! Let's add the button that will trigger the `fetchData` action and download some data for our app.

<pre><code class="language-javascript">
import React, { PropTypes } from 'react';
import { connect } from 'react-redux';
import Button from 'react-bootstrap-button-loader';
import { test } from '../../redux/actions/test';

const propTypes = {
  dispatch: PropTypes.func.isRequired,
  loading: PropTypes.bool,
};

function Content({ loading = false, dispatch }) {
  function fetchData() {
    dispatch(test());
  }

  return (
    &lt;div&gt;
      &lt;Button loading={loading} onClick={() =&gt; { fetchData(); }}&gt;Fetch Data from API&lt;/Button&gt;
    &lt;/div&gt;
  );
}

Content.propTypes = propTypes;

function mapStateToProps() {
  return {};
}

export default connect(mapStateToProps)(Content);
</code></pre>

Let's open our page in a browser. With the help of our browser’s developer tools and Redux DevTools, we can see that the application is fetching the data from the back end in JSON API document format, converts it to a more suitable representation and stores it in the Redux store. Great! Everything works as expected. So, let's add some UI components to visualize the data.</p>

## 3\. Fetching The Data From The Store

The [redux-object](https://github.com/yury-dymov/redux-object) package converts the data from the Redux store into a JSON object. We need to pass part of the store, the object type and the ID, and it will take care of the rest.

<pre><code class="language-javascript">
import build, { fetchFromMeta } from 'redux-object';

console.log(build(state.data, 'post', '1')); // ---> Post Object: { text: "I am fine", id: 1, author: @AuthorObject }
console.log(fetchFromMeta(state.data, '/posts')); // ---> array of posts
</code></pre>

All relationships are represented as JavaScript object properties, with lazy-loading support. So, all child objects will be loaded only when required.

<pre><code class="language-javascript">
const post = build(state.data, 'post', '1'); // ---> post object; `author` and `comments` properties are not loaded yet

post.author; // ---> User Object: { name: "Alice", id: 1 }
</code></pre>

Let's add several UI components to visualize the data.

Typically, React’s component structure follows the data model, and our app is no exception.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcf857f6-ae91-4df4-ad12-859cf01d480f/sm-react-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ec08798-3cbb-4531-860b-9bfd7ebd9d79/sm-react-800w-opt.png" width="800" height="345" alt="React Components Hierarchy" /></a><figcaption>React components hierarchy (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcf857f6-ae91-4df4-ad12-859cf01d480f/sm-react-large-opt.png">View large version</a>)</figcaption></figure>

### src/components/Content.jsx

<p>First, we need to fetch the data from the store and propogate it to the component via the <code>connect</code> function from <code>react-redux</code>:<p>

<pre><code class="language-javascript">
import React, { PropTypes } from 'react';
import { connect } from 'react-redux';
import Button from 'react-bootstrap-button-loader';
import build from 'redux-object';
import { test } from '../../redux/actions/test';
import Question from '../Question';

const propTypes = {
  dispatch: PropTypes.func.isRequired,
  questions: PropTypes.array.isRequired,
  loading: PropTypes.bool,
};

function Content({ loading = false, dispatch, questions }) {
  function fetchData() {
    dispatch(test());
  }

  const qWidgets = questions.map(q =&gt; &lt;Question key={q.id} question={q} /&gt;);

  return (
    &lt;div&gt;
      &lt;Button loading={loading} onClick={() =&gt; { fetchData(); }}&gt;Fetch Data from API&lt;/Button&gt;
      {qWidgets}
    &lt;/div&gt;
  );
}

Content.propTypes = propTypes;

function mapStateToProps(state) {
  if (state.data.meta['/test']) {
    const questions = (state.data.meta['/test'].data || []).map(object =&gt; build(state.data, 'question', object.id));
    const loading = state.data.meta['/test'].loading;

    return { questions, loading };
  }

  return { questions: [] };
}

export default connect(mapStateToProps)(Content);
</code></pre>

<p>We are fetching object IDs from the meta data of the API request with the <code>/test</code> endpoint, building JavaScript objects with the redux-object library and providing them to our component in the <code>questions</code> prop.</p>

<p>Now we need to implement a bunch of “dumb” components for rendering questions, posts, comments and users. They are very straightforward.</p>

### src/components/Question/package.json

<p>Here is the <code>package.json</code> of the <code>Question</code> visualization component:</p>

<pre><code class="language-javascript">
{
  "name": "question",
  "version": "0.0.0",
  "private": true,
  "main": "./Question"
}
</code></pre>

### src/components/Question/Question.jsx

<p>The <code>Question</code> component renders the question text and the list of answers.</p>

<pre><code class="language-javascript">
import React, { PropTypes } from 'react';
import Post from '../Post';

const propTypes = {
  question: PropTypes.object.isRequired,
};

function Question({ question }) {
  const postWidgets = question.posts.map(post =&gt; &lt;Post key={post.id} post={post} /&gt;);

  return (
    &lt;div className="question"&gt;
      {question.text}
      {postWidgets}
    &lt;/div&gt;
  );
}

Question.propTypes = propTypes;

export default Question;
</code></pre>

### src/components/Post/package.json

<p>Here is the <code>package.json</code> of the <code>Post</code> component:</p>

<pre><code class="language-javascript">
{
  "name": "post",
  "version": "0.0.0",
  "private": true,
  "main": "./Post"
}
</code></pre>

### src/components/Post/Post.jsx

<p>The <code>Post</code> component renders some information about the author, the answer text and also the list of comments.</p>

<pre><code class="language-javascript">
import React, { PropTypes } from 'react';
import Comment from '../Comment';
import User from '../User';

const propTypes = {
  post: PropTypes.object.isRequired,
};

function Post({ post }) {
  const commentWidgets = post.comments.map(c =&gt; &lt;Comment key={c.id} comment={c} /&gt;);

  return (
    &lt;div className="post"&gt;
      &lt;User user={post.author} /&gt;
      {post.text}
      {commentWidgets}
    &lt;/div&gt;
  );
}

Post.propTypes = propTypes;

export default Post;
</code></pre>

### src/components/User/package.json

<p>Here is the <code>package.json</code> of the <code>User</code> component:</p>

<pre><code class="language-javascript">
{
  "name": "user",
  "version": "0.0.0",
  "private": true,
  "main": "./User"
}
</code></pre>

### src/components/User/User.jsx

<p>The <code>User</code> component renders some meaningful information about either the answer or the comment’s author. In this app, we will output just the user’s name, but in a real application, we could add an avatar and other nice things for a better user experience.</p>

<pre><code class="language-javascript">
import React, { PropTypes } from 'react';

const propTypes = {
  user: PropTypes.object.isRequired,
};

function User({ user }) {
  return &lt;span className="user"&gt;{user.name}: &lt;/span&gt;;
}

User.propTypes = propTypes;

export default User;
</code></pre>

### src/components/Comment/package.json

<p>Here is the <code>package.json</code> of the <code>Comment</code> component:</p>

<pre><code class="language-javascript">
{
  "name": "comment",
  "version": "0.0.0",
  "private": true,
  "main": "./Comment"
}
</code></pre>

### src/components/Comment/Comment.jsx

<p>The <code>Comment</code> component is very similar to the <code>Post</code> component. It renders some information about the author and the comment’s text.</p>

<pre><code class="language-javascript">
import React, { PropTypes } from 'react';
import User from '../User';

const propTypes = {
  comment: PropTypes.object.isRequired,
};

function Comment({ comment }) {
  return (
    &lt;div className="comment"&gt;
      &lt;User user={comment.author} /&gt;
      {comment.text}
    &lt;/div&gt;
  );
}

Comment.propTypes = propTypes;

export default Comment;
</code></pre>

<p>And we are done! Open the browser, press the button, and enjoy the result.</p>

<p>If something doesn't work for you, feel free to compare your code with <a href="https://github.com/yury-dymov/json-api-react-redux-example">my project’s master branch</a></p>

<p>A live demo is also <a href="https://yury-dymov.github.io/json-api-react-redux-example">available on GitHub</a>.

## Conclusion

<p>This ends the story I would like to tell. This approach helps us to prototype a lot faster and to be very flexible with changes to the data model. Because data comes out typified and in a flat structure from the back end, we don't need to know in advance the relationships between data objects and particular fields. Data will be saved in the Redux store in a format that conforms to the Redux best practices anyway. This frees us to <strong>dedicate most of our time to developing features and experimenting</strong>, rather than adopting normalizr schemes, rethinking selectors and debugging over and over again.</p>

<p>I encourage you to try the JSON API in your next pet project. You’ll spend more time on experiments, without fear of breaking things.</p>

### Related Links

<ul>
<li><a href="https://jsonapi.org/">JSON API</a> specification</li>

<li>“<a href="https://jsonapi.org/implementations/">Implementations</a>,” JSON API</li>

<li><a href="https://github.com/yury-dymov/json-api-normalizer">json-api-normalizer</a>, Yury Dymov, GitHub</li>

<li><a href="https://github.com/yury-dymov/redux-object">redux-object</a>, Yury Dymov, GitHub</li>

<li><a href="https://phoenix-json-api-example.herokuapp.com/api/test">Phoenix JSON API example</a>, Heroku<br>
JSON API Data Source example developed with Phoenix framework</li>

<li><a href="https://github.com/yury-dymov/phoenix-json-api-example">Phoenix JSON API Example</a>, Yury Dymov, GitHub<br>
JSON API data source example source code</li>

<li><a href="https://yury-dymov.github.io/json-api-react-redux-example">json-api-normalizer Demo</a>, Yury Dymov, GitHub<br>
A React application consuming a JSON API live demo</li>

<li><a href="https://github.com/yury-dymov/json-api-react-redux-example/tree/initial">JSON API React Redux Example</a>, Yury Dymov, GitHub<br>
React application source code, <strong>initial</strong> version</li>

<li><a href="https://github.com/yury-dymov/json-api-react-redux-example">JSON API React Redux Example</a>, Yury Dymov, GitHub<br>
React application source code, <strong>final</strong> version</li>
</ul>

{{< signature "al" >}}

