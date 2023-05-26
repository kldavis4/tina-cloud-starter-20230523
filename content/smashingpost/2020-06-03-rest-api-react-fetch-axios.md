---
title: 'Consuming REST APIs In React With Fetch And Axios'
slug: rest-api-react-fetch-axios
author: shedrack-akintayo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7671e2-4e88-4920-a2d2-dbefbd352311/rest-api-react-fetch-axios.png
date: 2020-06-03T10:30:00.000Z
summary: >-
  If you’re a React developer who’d like to learn how you can start consuming APIs in your React applications, then this article is for you. Shedrack Akintayo explains what a REST API is and how to build a simple application that consumes a REST API by using both Fetch API and Axios.
description: >-
  If you’re a React developer who’d like to learn how you can start consuming APIs in your React applications, then this article is for you. Shedrack Akintayo explains what a REST API is and how to build a simple application that consumes a REST API by using both Fetch API and Axios.
categories:
  - API
  - React
  - REST API
  - JavaScript
---

Consuming REST APIs in a React Application can be done in various ways, but in this tutorial, we will be discussing how we can consume REST APIs using two of the most popular methods known as **Axios** (a promise-based HTTP client) and **Fetch API** (a browser in-built web API). I will discuss and implement each of these methods in detail and shed light on some of the cool features each of them have to offer. 

APIs are what we can use to supercharge our React applications with data. There are certain operations that can’t be done on the client-side, so these operations are implemented on the server-side. We can then use the APIs to consume the data on the client-side. 

APIs consist of a set of data, that is often in JSON format with specified endpoints. When we access data from an API, we want to access specific endpoints within that API framework. We can also say that an API is a contractual agreement between two services over the shape of request and response. The code is just a byproduct. It also contains the terms of this data exchange.

In React, there are various ways we can consume REST APIs in our applications, these ways include using the JavaScript inbuilt `fetch()` method and Axios which is a promise-based HTTP client for the browser and Node.js.

**Note:** *A good knowledge of ReactJS, React Hooks, JavaScript and CSS will come in handy as you work your way throughout this tutorial.*

Let’s get started with learning more about the REST API.

{{% feature-panel %}}

## What Is A REST API

A [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/) is an API that follows what is structured in accordance with the [REST Structure](https://gtjourney.gatech.edu/gt-devhub/documentation/restful-api-structure) for APIs. REST stands for “Representational State Transfer”. It consists of various rules that developers follow when creating APIs.

### The Benefits Of REST APIs

1. Very easy to learn and understand;
2. It provides developers with the ability to organize complicated applications into simple resources;
3. It easy for external clients to build on your REST API without any complications;
4. It is very easy to scale;
5. A REST API is not language or platform-specific, but can be consumed with any language or run on any platform.

### An Example Of A REST API Response

The way a REST API is structured depends on the product it’s been made for &mdash; but the rules of REST must be followed.

The sample response below is from the [Github Open API](https://developer.github.com/v3). We’ll be using this API to build a React app later on in this tutorial.

<div class="break-out">

 <pre><code class="language-javascript">{
"login": "hacktivist123",
"id": 26572907,
"node_id": "MDQ6VXNlcjI2NTcyOTA3",
"avatar_url": "https://avatars3.githubusercontent.com/u/26572907?v=4",
"gravatar_id": "",
"url": "https://api.github.com/users/hacktivist123",
"html_url": "https://github.com/hacktivist123",
"followers_url": "https://api.github.com/users/hacktivist123/followers",
"following_url": "https://api.github.com/users/hacktivist123/following{/other_user}",
"gists_url": "https://api.github.com/users/hacktivist123/gists{/gist_id}",
"starred_url": "https://api.github.com/users/hacktivist123/starred{/owner}{/repo}",
"subscriptions_url": "https://api.github.com/users/hacktivist123/subscriptions",
"organizations_url": "https://api.github.com/users/hacktivist123/orgs",
"repos_url": "https://api.github.com/users/hacktivist123/repos",
"events_url": "https://api.github.com/users/hacktivist123/events{/privacy}",
"received_events_url": "https://api.github.com/users/hacktivist123/received_events",
"type": "User",
"site_admin": false,
"name": "Shedrack akintayo",
"company": null,
"blog": "https://sheddy.xyz",
"location": "Lagos, Nigeria ",
"email": null,
"hireable": true,
"bio": "☕ Software Engineer | | Developer Advocate🥑|| ❤ Everything JavaScript",
"public_repos": 68,
"public_gists": 1,
"followers": 130,
"following": 246,
"created_at": "2017-03-21T12:55:48Z",
"updated_at": "2020-05-11T13:02:57Z"
} 
</code></pre>
</div>

The response above is from the Github REST API when I make a `GET` request to the following endpoint  `https://api.github.com/users/hacktivist123`. It returns all the stored data about a user called **hacktivist123**. With this response, we can decide to render it whichever way we like in our React app. 

## Consuming APIs Using The Fetch API

The `fetch()` API is an inbuilt JavaScript method for getting resources from a server or an API endpoint. It’s similar to [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), but the [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) provides a more powerful and flexible feature set.

It defines concepts such as [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) and the [HTTP Origin header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) semantics, supplanting their separate definitions elsewhere.

The `fetch()` API method always takes in a compulsory argument, which is the path or URL to the resource you want to fetch. It returns a promise that points to the response from the request, whether the request is successful or not. You can also optionally pass in an init options object as the second argument.

Once a response has been fetched, there are several inbuilt methods available to define what the body content is and how it should be handled.

### The Difference Between The Fetch API And jQuery Ajax

The Fetch API is different from [jQuery Ajax](https://api.jquery.com/jquery.ajax/) in three main ways, which are: 

1. The promise returned from a `fetch()` request will not reject when there’s an HTTP error, no matter the nature of the response status. Instead, it will resolve the request normally, if the response status code is a 400 or 500 type code, it’ll set the ok status. A request will only be rejected either because of network failure or if something is preventing the request from completing
2. `fetch()` will not allow the use of cross-site cookies i.e you cannot carry out a cross-site session using `fetch()`
3. `fetch()` will also not send cookies by default unless you set the `credentials` in the init option.
    
### Parameters For The Fetch API

- `resource`  
This is the path to the resource you want to fetch, this can either be a direct link to the resource path or a request object
- `init`  
This is an object containing any custom setting or credentials you’ll like to provide for your `fetch()` request. The following are a few of the possible options that can be contained in the `init` object:
    - `method`  
    This is for specifying the HTTP request method e.g GET, POST, etc.
    - `headers`  
    This is for specifying any headers you would like to add to your request, usually contained in an object or an object literal.
    - `body`  
    This is for specifying a body that you want to add to your request: this can be a `Blob`, `BufferSource`, `FormData`, `URLSearchParams`, `USVString`, or `ReadableStream` object
    - `mode`  
    This is for specifying the mode you want to use for the request, e.g., `cors`, `no-cors`, or `same-origin`.
    - `credentials`  
    This for specifying the request credentials you want to use for the request, this option must be provided if you consider sending cookies automatically for the current domain.

### Basic Syntax for Using the Fetch() API

A basic fetch request is really simple to write, take a look at the following code:

<pre><code class="language-javascript">fetch('https://api.github.com/users/hacktivist123/repos')
  .then(response => response.json())
  .then(data => console.log(data));
</code></pre>

In the code above, we are fetching data from a URL that returns data as JSON and then printing it to the console. The simplest form of using fetch() often takes just one argument which is the path to the resource you want to fetch and then return a promise containing the response from the fetch request. This response is an object.

The response is just a regular HTTP response and not the actual JSON. In order to get the JSON body content from the response, we’d have to change the response to actual JSON using the json() method on the response.

### Using Fetch API In React Apps

Using the Fetch API in React Apps is the normal way we’d use the Fetch API in javascript, there is no change in syntax, the only issue is deciding where to make the fetch request in our React app. Most fetch requests or any HTTP request of any sort is usually done in a React Component. 

This request can either be made inside a [Lifecycle Method](https://reactjs.org/docs/react-component.html#the-component-lifecycle) if your component is a Class Component or inside a [`useEffect()`](https://www.smashingmagazine.com/2020/04/react-hooks-api-guide/) [React Hook](https://www.smashingmagazine.com/2020/04/react-hooks-api-guide/) if your component is a Functional Component.

For example, In the code below, we will make a fetch request inside a class component, which means we’ll have to do it inside a lifecycle method. In this particular case, our fetch request will be made inside a `componentDidMount` lifecycle method because we want to make the request just after our React Component has mounted.

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';

class myComponent extends React.Component {
  componentDidMount() {
    const apiUrl = 'https://api.github.com/users/hacktivist123/repos';
    fetch(apiUrl)
      .then((response) => response.json())
      .then((data) => console.log('This is your data', data));
  }
  render() {
    return &lt;h1&gt;my Component has Mounted, Check the browser 'console' &lt;/h1&gt;;
  }
}
export default myComponent;
</code></pre>
</div>

In the code above, we are creating a very simple class component that makes a fetch request that logs the final data from the fetch request we have made to the API URL into the browser console after the React component has finished mounting. 

The `fetch()` method takes in the path to the resource we want to fetch, which is assigned to a variable called `apiUrl`. After the fetch request has been completed it returns a promise that contains a response object. Then, we are extracting the JSON body content from the response using the `json()` method, finally we log the final data from the promise into the console.

{{% ad-panel-leaderboard %}}

## Let’s Consume A REST API With Fetch Method

In this section, we will be building a simple react application that consumes an external API, we will be using the Fetch method to consume the API.

The simple application will display all the repositories and their description that belongs to a particular user. For this tutorial, I’ll be using my GitHub username, you can also use yours if you wish.

The first thing we need to do is to generate our React app by using `create-react-app`:

<pre><code class="language-bash">npx create-react-app myRepos
</code></pre>

The command above will bootstrap a new React app for us. As soon as our new app has been created, all that’s left to do is to run the following command and begin coding:

<pre><code class="language-bash">npm start
</code></pre>

If our React is created properly we should see this in our browser window when we navigate to `localhost:3000` after running the above command.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbf2489-eb0b-42ff-8fe7-7fa5387031cd/rest-api-react-fetch-axios-initial-app-screen.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbf2489-eb0b-42ff-8fe7-7fa5387031cd/rest-api-react-fetch-axios-initial-app-screen.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbf2489-eb0b-42ff-8fe7-7fa5387031cd/rest-api-react-fetch-axios-initial-app-screen.png'>Large preview</a>)" alt="Initial App Screen" >}}

In your `src` folder, create a new folder called `component`. This folder will hold all of our React components. In the new folder, create two files titled *List.js* and *withListLoading.js*. These two files will hold the components that will be needed in our app.

The *List.js* file will handle the display of our Repositories in the form of a list, and the *withListLoading.js* file will hold a higher-order component that will be displayed when the Fetch request we will be making is still ongoing. 

In the *List.js* file we created inside the `components` folder, let’s paste in the following code:

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';
const List = (props) =&gt; {
  const { repos } = props;
  if (!repos || repos.length === 0) return &lt;p&gt;No repos, sorry&lt;/p&gt;;
  return (
    &lt;ul&gt;
      &lt;h2 className='list-head'&gt;Available Public Repositories&lt;/h2&gt;
      {repos.map((repo) =&gt; {
        return (
          &lt;li key={repo.id} className='list'&gt;
            &lt;span className='repo-text'&gt;{repo.name} &lt;/span&gt;
            &lt;span className='repo-description'&gt;{repo.description}&lt;/span&gt;
          &lt;/li&gt;
        );
      })}
    &lt;/ul&gt;
  );
};
export default List;
</code></pre>
</div>

The code above is a basic React list component that would display the data, in this case, the repositories name and their descriptions in a list.

Now, Let me explain the code bit by bit.

<pre><code class="language-javascript">const { repos } = props;
</code></pre>

We are initializing a prop for the component called repos.

<pre><code class="language-javascript">if (repos.length === 0 || !repos) return &lt;p&gt;No repos, sorry&lt;/p&gt;;
</code></pre>

Here, all we are doing is making a conditional statement that will render a message when the length of the repos we get from the request we make is equal to zero.

<div class="break-out">

 <pre><code class="language-javascript">return (
    &lt;ul&gt;
      &lt;h2 className='list-head'&gt;Available Public Repositories&lt;/h2&gt;
      {repos.map((repo) =&gt; {
        return (
          &lt;li key={repo.id} className='list'&gt;
            &lt;span className='repo-text'&gt;{repo.name} &lt;/span&gt;
            &lt;span className='repo-description'&gt;{repo.description}&lt;/span&gt;
          &lt;/li&gt;
        );
      })}
    &lt;/ul&gt;
  );
</code></pre>
</div>
 
Here, we are mapping through each of the repositories that will be provided by the API request we make and extracting each of the repositories names and their descriptions then we are displaying each of them in a list. 
 

<pre><code class="language-javascript">export default List;
</code></pre>

 Here we are exporting our `List` component so that we can use it somewhere else.
 
In the *withListLoading.js* file we created inside the components folder, let’s paste in the following code: 

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';

function WithListLoading(Component) {
  return function WihLoadingComponent({ isLoading, ...props }) {
    if (!isLoading) return &lt;Component {...props} /&gt;;
    return (
      &lt;p style={{ textAlign: 'center', fontSize: '30px' }}&gt;
        Hold on, fetching data may take some time :)
      &lt;/p&gt;
    );
  };
}
export default WithListLoading;
</code></pre>
</div>

The code above is a higher-order React component that takes in another component and then returns some logic. In our case, our higher component will wait to check if the current `isLoading` state of the component it takes is `true` or `false`. If the current `isLoading` state is true, it will display a message *Hold on, fetching data may take some time :)*. Immediately the `isLoading` state changes to `false` it’ll render the component it took in. In our case, it’ll render the **List** component.

In your **App.js* file inside the **src** folder, let’s paste in the following code:

<div class="break-out">

 <pre><code class="language-javascript">import React, { useEffect, useState } from 'react';
import './App.css';
import List from './components/List';
import withListLoading from './components/withListLoading';
function App() {
  const ListLoading = withListLoading(List);
  const [appState, setAppState] = useState({
    loading: false,
    repos: null,
  });

  useEffect(() =&gt; {
    setAppState({ loading: true });
    const apiUrl = `https://api.github.com/users/hacktivist123/repos`;
    fetch(apiUrl)
      .then((res) =&gt; res.json())
      .then((repos) =&gt; {
        setAppState({ loading: false, repos: repos });
      });
  }, [setAppState]);
  return (
    &lt;div className='App'&gt;
      &lt;div className='container'&gt;
        &lt;h1&gt;My Repositories&lt;/h1&gt;
      &lt;/div&gt;
      &lt;div className='repo-container'&gt;
        &lt;ListLoading isLoading={appState.loading} repos={appState.repos} /&gt;
      &lt;/div&gt;
      &lt;footer&gt;
        &lt;div className='footer'&gt;
          Built{' '}
          &lt;span role='img' aria-label='love'&gt;
            💚
          &lt;/span&gt;{' '}
          with by Shedrack Akintayo
        &lt;/div&gt;
      &lt;/footer&gt;
    &lt;/div&gt;
  );
}
export default App;
</code></pre>
</div>

Our App.js is a functional component that makes use of React Hooks for handling state and also side effects. If you’re not familiar with React Hooks, read my [Getting Started with React Hooks Guide.](https://www.smashingmagazine.com/2020/04/react-hooks-api-guide/)

Let me explain the code above bit by bit.

<pre><code class="language-javascript">import React, { useEffect, useState } from 'react';
import './App.css';
import List from './components/List';
import withListLoading from './components/withListLoading';
</code></pre>

Here, we are importing all the external files we need and also the components we created in our components folder. We are also importing the React Hooks we need from React.

<pre><code class="language-javascript">const ListLoading = withListLoading(List);
  const [appState, setAppState] = useState({
    loading: false,
    repos: null,
  });
</code></pre>

Here, we are creating a new component called `ListLoading` and assigning our `withListLoading` higher-order component wrapped around our list component. We are then creating our state values `loading` and `repos` using the `useState()` React Hook. 

<div class="break-out">

 <pre><code class="language-javascript">useEffect(() => {
    setAppState({ loading: true });
    const user = `https://api.github.com/users/hacktivist123/repos`;
    fetch(user)
      .then((res) => res.json())
      .then((repos) => {
        setAppState({ loading: false, repos: repos });
      });
  }, [setAppState]);
</code></pre>
</div>

Here, we are initializing a `useEffect()` React Hook. In the `useEffect()` hook, we are setting our initial loading state to true, while this is true, our higher-order component will display a message.
We are then creating a constant variable called `user` and assigning the API URL we’ll be getting the repositories data from.

We are then making a basic `fetch()` request like we discussed above and then after the request is done we are setting the app loading state to false and populating the repos state with the data we got from the request.

<div class="break-out">

 <pre><code class="language-javascript">return (
    &lt;div className='App'&gt;
      &lt;div className='container'&gt;
        &lt;h1&gt;My Repositories&lt;/h1&gt;
      &lt;/div&gt;
      &lt;div className='repo-container'&gt;
        &lt;ListLoading isLoading={AppState.loading} repos={AppState.repos} /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}
export default App;
</code></pre>
</div>

Here we are basically just rendering the Component we assigned our higher-order component to and also filling the `isLoading` prop and `repos` prop with their state value.

Now, we should see this in our browser, when the fetch request is still being made, courtesy of our `withListLoading` higher-order component:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287290a1-eb17-486e-9630-a5a13b2b3697/rest-api-react-fetch-axios-app-loading-state.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287290a1-eb17-486e-9630-a5a13b2b3697/rest-api-react-fetch-axios-app-loading-state.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287290a1-eb17-486e-9630-a5a13b2b3697/rest-api-react-fetch-axios-app-loading-state.png'>Large preview</a>)" alt="App Loading State" >}}

Now, when the fetch request has completed successfully, we should see the repositories displayed in a list format as below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b693782-ce77-4cb4-b4e9-2ef560b076d8/rest-api-react-fetch-axios-finished-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b693782-ce77-4cb4-b4e9-2ef560b076d8/rest-api-react-fetch-axios-finished-app.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b693782-ce77-4cb4-b4e9-2ef560b076d8/rest-api-react-fetch-axios-finished-app.png'>Large preview</a>)" alt="Finished App" >}}

Now, let’s style our project a little bit, in your *App.css* file, copy and paste this code.

<div class="break-out">

 <pre><code class="language-css">@import url('https://fonts.googleapis.com/css2?family=Amiri&display=swap');
:root {
  --basic-color: #23cc71;
}
.App {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: 'Amiri', serif;
  overflow: hidden;
}
.container {
  display: flex;
  flex-direction: row;
}
.container h1 {
  font-size: 60px;
  text-align: center;
  color: var(--basic-color);
}
.repo-container {
  width: 50%;
  height: 700px;
  margin: 50px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  overflow: scroll;
}
@media screen and (max-width: 600px) {
  .repo-container {
    width: 100%;
    margin: 0;
    box-shadow: none;
  }
}
.repo-text {
  font-weight: 600;
}
.repo-description {
  font-weight: 600;
  font-style: bold;
  color: var(--basic-color);
}
.list-head {
  text-align: center;
  font-weight: 800;
  text-transform: uppercase;
}
.footer {
  font-size: 15px;
  font-weight: 600;
}
.list {
  list-style: circle;
}
</code></pre>
</div>

So in the code above, we are styling our app to look more pleasing to the eyes, we have assigned various class names to each element in our *App.js* file and thus we are using these class names to style our app.

Once we’ve applied our styling, our app should look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54fe00da-f1a4-4610-bead-b4904a4b4788/rest-api-react-fetch-axios-app-with-axios.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54fe00da-f1a4-4610-bead-b4904a4b4788/rest-api-react-fetch-axios-app-with-axios.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54fe00da-f1a4-4610-bead-b4904a4b4788/rest-api-react-fetch-axios-app-with-axios.png'>Large preview</a>)" alt="Styled App" >}}

Now our app looks much better. 😊 

So that’s how we can use the Fetch API to consume a REST API. In the next section, we’ll be discussing Axios and how we can use it to consume the same API in the same App.

{{% ad-panel-leaderboard %}}

## Consuming APIs With Axios

Axios is an easy to use promise-based HTTP client for the browser and node.js. Since Axios is promise-based, we can take advantage of async and await for more readable and asynchronous code. With Axios, we get the ability to intercept and cancel request, it also has a built-in feature that provides client-side protection against cross-site request forgery.

### Features Of Axios

- Request and response interception
- Streamlined error handling
- Protection against **XSRF**
- Support for upload progress
- Response timeout
- The ability to cancel requests
- Support for older browsers
- Automatic JSON data transformation

### Making Requests With Axios

Making HTTP Requests with Axios is quite easy. The code below is basically how to make an HTTP request.

<pre><code class="language-javascript">// Make a GET request
axios({
  method: 'get',
  url: 'https://api.github.com/users/hacktivist123',
});

// Make a Post Request
axios({
  method: 'post',
  url: '/login',
  data: {
    firstName: 'shedrack',
    lastName: 'akintayo'
  }
});
</code></pre>

The code above shows the basic ways we can make a GET and POST HTTP request with Axios.

Axios also provides a set of shorthand method for performing different HTTP requests. The Methods are as follows:

- `axios.request(config)`
- `axios.get(url[, config])`
- `axios.delete(url[, config])`
- `axios.head(url[, config])`
- `axios.options(url[, config])`
- `axios.post(url[, data[, config]])`
- `axios.put(url[, data[, config]])`
- `axios.patch(url[, data[, config]])`

For example, if we want to make a similar request like the example code above but with the shorthand methods we can do it like so:

<pre><code class="language-javascript">// Make a GET request with a shorthand method
axios.get('https://api.github.com/users/hacktivist123');

// Make a Post Request with a shorthand method
axios.post('/signup', {
    firstName: 'shedrack',
    lastName: 'akintayo'
});
</code></pre>

In the code above, we are making the same request as what we did above but this time with the shorthand method. Axios provides flexibility and makes your HTTP requests even more readable.

### Making Multiple Requests With Axios

Axios provides developers the ability to make and handle simultaneous HTTP requests using the `axios.all()` method. This method takes in an array of arguments and it returns a single promise object that resolves only when all arguments passed in the array have resolved.

For example, we can make multiple requests to the GitHub api using the `axios.all()` method like so:

<pre><code class="language-javascript">axios.all([
  axios.get('https://api.github.com/users/hacktivist123'),
  axios.get('https://api.github.com/users/adenekan41')
])
.then(response => {
  console.log('Date created: ', response[0].data.created_at);
  console.log('Date created: ', response[1].data.created_at);
});
</code></pre>

The code above makes simultaneous requests to an array of arguments in parallel and returns the response data, in our case, it will log to the console the `created_at` object from each of the API responses.

## Let’s Consume A REST API With Axios Client

In this section, all we’ll be doing is replacing `fetch()` method with Axios in our existing React Application. All we need to do is to install Axios and then use it in our App.js file for making the HTTP request to the GitHub API.

Now let’s install Axios in our React app by running either of the following: 

With NPM:

<pre><code class="language-bash">npm install axios
</code></pre>

With Yarn:

<pre><code class="language-bash">yarn add axios
</code></pre>

After installation is complete, we have to import axios into our App.js. In our App.js we’ll add the following line to the top of our App.js file:

<pre><code class="language-javascript">import axios from 'axios'
</code></pre>

After adding the line of code our *App.js* all we have to do inside our `useEffect()` is to write the following code:

<div class="break-out">

 <pre><code class="language-javascript">useEffect(() => {
    setAppState({ loading: true });
    const apiUrl = 'https://api.github.com/users/hacktivist123/repos';
    axios.get(apiUrl).then((repos) => {
      const allRepos = repos.data;
      setAppState({ loading: false, repos: allRepos });
    });
  }, [setAppState]);
</code></pre>
</div>

You may have noticed that we have now replaced the fetch API with the Axios shorthand method `axios.get` to make a `get` request to the API.

<pre><code class="language-javascript">axios.get(apiUrl).then((repos) => {
      const allRepos = repos.data;
      setAppState({ loading: false, repos: allRepos });
    });
</code></pre>

In this block of code, we are making a GET request then we are returning a promise that contains the repos data and assigning the data to a constant variable called `allRepos`.  We are then setting the current loading state to false and also passing the data from the request to the repos state variable.

If we did everything correctly, we should see our app still render the same way without any change.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54fe00da-f1a4-4610-bead-b4904a4b4788/rest-api-react-fetch-axios-app-with-axios.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54fe00da-f1a4-4610-bead-b4904a4b4788/rest-api-react-fetch-axios-app-with-axios.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54fe00da-f1a4-4610-bead-b4904a4b4788/rest-api-react-fetch-axios-app-with-axios.png'>Large preview</a>)" alt="App with Axios" >}}

So this is how we can use Axios client to consume a REST API.

## Fetch vs Axios

In this section, I will be listing our certain features and then I’ll talk about how well Fetch and Axios support these features.

1. **Basic Syntax**  
Both Fetch and Axios have very simple syntaxes for making requests. But Axios has an upper hand because Axios automatically converts a response to JSON, so when using Axios we skip the step of converting the response to JSON, unlike Fetch() where we’d still have to convert the response to JSON. Lastly, Axios shorthand methods allow us to make specific HTTP Requests easier.

2. **Browser Compatibility**  
One of the many reasons why developers would prefer Axios over Fetch is because Axios is supported across major browsers and versions unlike Fetch that is only supported in Chrome 42+, Firefox 39+, Edge 14+, and Safari 10.1+.

3. **Handling Response Timeout**  
Setting a timeout for responses is very easy to do in Axios by making use of the `timeout` option inside the request object. But in Fetch, it is not that easy to do this. Fetch provides a similar feature by using the `AbortController()` interface but it takes more time to implement and can get confusing. 

4. **Intercepting HTTP Requests**  
Axios allows developers to intercept HTTP requests. HTTP interceptors are needed when we need to change HTTP requests from our application to the server. Interceptors give us the ability to do that without having to write extra code.

5. **Making Multiple Requests Simultaneously**  
Axios allows us to make multiple HTTP requests with the use of the `axios.all()` method ( I talked about this above). `fetch()` provides the same feature with the use of the `promise.all()` method, we can make multiple `fetch()` requests inside it.

## Conclusion

Axios and `fetch()` are all great ways of consuming APIs but I advise you to use `fetch()` when building relatively small applications and make use of Axios when building large applications for scalability reasons.
I hope you enjoyed working through this tutorial, you could always read more on Consuming REST APIs with either Fetch or Axios from the references below. If you have any questions, you can leave it in the comments section below and I’ll be happy to answer every single one.

- *The supporting repo for this article is [available on Github](https://github.com/hacktivist123/consuming-rest-apis).*

### Related Resources

- “[REST API Structure](https://gtjourney.gatech.edu/gt-devhub/documentation/restful-api-structure),” 
- “[Understanding And Using REST APIs](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/),” Zell Liew
- “[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS),” 
- “[HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers),” 
- “[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API),” Mozilla Developer Network
- “[Using Axios And React](https://alligator.io/react/axios-react/),” Paul Halliday
- “[How To Make HTTP Requests Like A Pro With Axios](https://blog.logrocket.com/how-to-make-http-requests-like-a-pro-with-axios/),” Faraz Kelhini

{{< signature "ks, ra, il" >}}
