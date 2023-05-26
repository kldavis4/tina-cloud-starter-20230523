---
title: 'How To Test Your React Apps With The React Testing Library'
slug: react-apps-testing-library
author: chidi-orji
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71a39af1-d08b-46cc-b068-88a94f890774/react-apps-testing-library.png
date: 2020-07-03T12:30:00.000Z
summary: >-
  Testing gives confidence in written code. In the context of this article, ‘testing’ means ‘automated testing’. Without automated testing, it is significantly harder to ensure the quality of a web application of significant complexity. Fails caused by automated testing may lead to more bugs in production. In this article, we’re going to show how React developers can quickly start testing their app with the [React Testing Library](https://testing-library.com/docs/react-testing-library/intro) (RTL).
description: >-
  Testing gives confidence in written code. In the context of this article, ‘testing’ means ‘automated testing’. Without automated testing, it is significantly harder to ensure the quality of a web application of significant complexity. Fails caused by automated testing may lead to more bugs in production. In this article, we’re going to show how React developers can quickly start testing their app with the [React Testing Library](https://testing-library.com/docs/react-testing-library/intro) (RTL).
categories:
  - Tools
  - React
  - Testing
  - JavaScript
---

Today, we’ll briefly discuss why it’s important to write automated tests for any software project, and shed light on some of the common types of automated testing. We’ll build a to-do list app by following the Test-Driven Development (TDD) approach. I’ll show you how to write both unit and functional tests, and in the process, explain what code mocks are by mocking a few libraries. I’ll be using a combination of RTL and Jest &mdash; both of which come pre-installed in any new project created with Create-React-App (CRA).

To follow along, you need to know how to set up and navigate a new React project and how to work with the yarn package manager (or npm). Familiarities with [Axios](https://github.com/axios/axios) and [React-Router](https://reacttraining.com/react-router/web) are also required.

<div class="c-felix-the-cat">
<h4 class="h3">Best React Practices</h4>
<p>React is a fantastic JavaScript library for building rich user interfaces. It provides a great component abstraction for organizing your interfaces into well-functioning code, and there’s just about anything you can use it for. <a href="https://www.smashingmagazine.com/category/react" class="btn btn--medium btn--blue">Read a related article on React&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## Why You Should Test Your Code

Before shipping your software to end-users, you first have to confirm that it is working as expected. In other words, the app should satisfy its project specifications.

Just as it is important to test our project as a whole before shipping it to end-users, it's also essential to keep testing our code during the lifetime of a project. This is necessary for a number of reasons. We may make updates to our application or refactor some parts of our code. A third-party library may undergo a breaking change. Even the browser that is running our web application may undergo breaking changes. In some cases, something stops working for no apparent reason &mdash; things could go wrong unexpectedly. Thus, it is necessary to test our code regularly for the lifetime of a project.

Broadly speaking, there are manual and automated software tests. In a manual test, a real user performs some action on our application to verify that they work correctly. This kind of test is less reliable when repeated several times because it’s easy for the tester to miss some details between test runs.

In an automated test, however, a test script is executed by a machine. With a test script, we can be sure that whatever details we set in the script will remain unchanged on every test run.

This kind of test gives us the benefits of being predictable and fast, such that we can quickly find and fix bugs in our code.

Having seen the necessity of testing our code, the next logical question is, what sort of automated tests should we write for our code? Let’s quickly go over a few of them.

## Types Of Automated Testing

There are many different types of automated software testing. Some of the most common ones are unit tests, integration tests, functional tests, end-to-end tests, acceptance tests, performance tests, and smoke tests.

1. **Unit test**  
In this kind of test, the goal is to verify that each unit of our application, considered in isolation, is working correctly. An example would be testing that a particular function returns an expected value, give some known inputs. We’ll see several examples in this article.
2. **Smoke test**  
This kind of test is done to check that the system is up and running. For example, in a React app, we could just render our main app component and call it a day. If it renders correctly we can be fairly certain that our app would render on the browser.
3. **Integration test**  
This sort of test is carried out to verify that two or more modules can work well together. For example, you might run a test to verify that your server and database are actually communicating correctly.
4. **Functional test**  
A functional test exists to verify that the system meets its functional specification. We’ll see an example later.
5. **End-to-end test**  
This kind of test involves testing the application the same way it would be used in the real world. You can use a tool like [cypress](https://www.cypress.io) for E2E tests.
6. **Acceptance test**  
This is usually done by the business owner to verify that the system meets specifications.
7. **Performance test**  
This sort of testing is carried out to see how the system performs under significant load. In frontend development, this is usually about how fast the app loads on the browser.

There’s more [here](https://www.softwaretestinghelp.com/types-of-software-testing/) if you’re interested.

{{% ad-panel-leaderboard %}}

## Why Use React Testing Library?

When it comes to testing React applications, there are a few testing options available, of which the most common ones I know of are [Enzyme](https://github.com/enzymejs/enzyme) and [React Testing Library](https://testing-library.com/docs/react-testing-library/intro) (RTL).

RTL is a subset of the [@testing-library](https://testing-library.com/) family of packages. Its philosophy is very simple. Your users don't care whether you use redux or context for state management. They care less about the simplicity of hooks nor the distinction between class and functional components. They just want your app to work in a certain way. It is, therefore, no surprise that the testing library’s primary [guiding principle](https://testing-library.com/docs/guiding-principles) is

<blockquote>“The more your tests resemble the way your software is used, the more confidence they can give you.”</blockquote>

So, whatever you do, have the end-user in mind and test your app just as they would use it.

Choosing RTL gives you a number of advantages. First, it’s much easier to get started with it. Every new React project bootstrapped with CRA comes with RTL and [Jest](https://jestjs.io/en) configured. The React [docs](https://reactjs.org/docs/testing.html#tools) also recommend it as the testing library of choice. Lastly, the guiding principle makes a lot of sense &mdash; functionality over implementation details.

With that out of the way, let’s get started with building a to-do list app, following the TDD approach.

## Project Setup

Open a terminal and copy and run the below command.

<pre><code class="language-bash"># start new react project and start the server
npx create-react-app start-rtl && cd start-rtl && yarn start</code></pre>

This should create a new React project and start the server on https://localhost:3000. With the project running, open a separate terminal, run `yarn test` and then press `a`. This runs all tests in the project in `watch` mode. Running the test in watch mode means that the test will automatically re-run when it detects a change in either the test file or the file that is being tested. On the test terminal, you should see something like the picture below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e9199eb-010d-41b6-86de-06b11a8d2570/01-initial-test-passing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e9199eb-010d-41b6-86de-06b11a8d2570/01-initial-test-passing.png" sizes="100vw" caption="Initial test passing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e9199eb-010d-41b6-86de-06b11a8d2570/01-initial-test-passing.png'>Large preview</a>)" alt="Initial test passing" >}}

You should see a lot of greens, which indicates that the test we’re running passed in flying colors.

As I mentioned earlier, CRA sets up RTL and Jest for every new React project. It also includes a sample test. This sample test is what we just executed.

When you run the `yarn test` command, react-scripts calls upon Jest to execute the test. Jest is a JavaScript testing framework that’s used in running tests. You won’t find it listed in `package.json` but you can do a search inside `yarn.lock` to find it. You can also see it in `node_modules/`.

Jest is incredible in the range of functionality that it provides. It provides tools for assertions, mocking, spying, etc. I strongly encourage you to take at least a quick tour of the documentation. There’s a lot to learn there that I cannot scratch in this short piece. We’ll be using Jest a lot in the coming sections.

Open `package.json` let’s see what we have there. The section of interest is `dependencies`. 

<pre><code class="language-javascript">  "dependencies": {
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    ...
  },</code></pre>     

We have the following packages installed specifically for testing purpose:

1. [@testing-library/jest-dom](https://github.com/testing-library/jest-dom): provides custom DOM element matchers for Jest.
2. [@testing-library/react](https://github.com/testing-library/react-testing-library): provides the APIs for testing React apps.
3. [@testing-library/user-event](https://github.com/testing-library/user-event): provides advanced simulation of browser interactions.

Open up `App.test.js` let’s take a look at its content.

<pre><code class="language-javascript">import React from 'react';
import { render } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  const { getByText } = render(<App />);
  const linkElement = getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});</code></pre>

The `render` method of RTL renders the `<App />` component and returns an object which is de-structured for the `getByText` query. This query finds elements in the DOM by their display text. Queries are the tools for finding elements in the DOM. The complete list of queries can be found [here](https://testing-library.com/docs/dom-testing-library/api-queries). All of the queries from the testing library are exported by RTL, in addition to the render, cleanup, and act methods. You can read more about these in the [API](https://testing-library.com/docs/react-testing-library/api) section.

The text is matched with the regular expression `/learn react/i`. The `i` flag makes the regular expression case-insensitive. We `expect` to find the text `Learn React` in the document.

All of this mimics the behavior a user would experience in the browser when interacting with our app.

Let’s start making the changes required by our app. Open `App.js` and replace the content with the below code.

<pre><code class="language-javascript">import React from "react";
import "./App.css";
function App() {
  return (
    &lt;div className="App"&gt;
      &lt;header className="App-header"&gt;
        &lt;h2&gt;Getting started with React testing library&lt;/h2&gt;
      &lt;/header&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>
    
If you still have the test running, you should see the test fail. Perhaps you can guess why that is the case, but we’ll return to it a bit later. Right now I want to refactor the test block.

Replace the test block in `src/App.test.js` with the code below:

<div class="break-out">

<pre><code class="language-javascript"># use describe, it pattern
describe("&lt;App /&gt;", () =&gt; {
  it("Renders &lt;App /&gt; component correctly", () =&gt; {
    const { getByText } = render(&lt;App /&gt;);
    expect(getByText(/Getting started with React testing library/i)).toBeInTheDocument();
  });
});</code></pre>
</div>

This refactor makes no material difference to how our test will run. I prefer the `describe` and `it` pattern as it allows me structure my test file into logical blocks of related tests. The test should re-run and this time it will pass. In case you haven’t guessed it, the fix for the failing test was to replace the `learn react` text with `Getting started with React testing library`.

In case you don’t have time to write your own styles you can just copy the one below into `App.css`.

<pre><code class="language-css">.App {
  min-height: 100vh;
  text-align: center;
}
.App-header {
  height: 10vh;
  display: flex;
  background-color: #282c34;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
.App-body {
  width: 60%;
  margin: 20px auto;
}
ul {
  padding: 0;
  display: flex;
  list-style-type: decimal;
  flex-direction: column;
}
li {
  font-size: large;
  text-align: left;
  padding: 0.5rem 0;
}
li a {
  text-transform: capitalize;
  text-decoration: none;
}
.todo-title {
  text-transform: capitalize;
}
.completed {
  color: green;
}
.not-completed {
  color: red;
}</code></pre>

You should already see the page title move up after adding this CSS.

I consider this a good point for me to commit my changes and push to Github. The corresponding branch is [01-setup](https://github.com/chidimo/Getting-started-with-react-testing-library/tree/01-setup).

Let’s continue with our project setup. We know we’re going to need some navigation in our app so we need React-Router. We’ll also be making API calls with Axios. Let’s install both.

<pre><code class="language-bash"># install react-router-dom and axios
yarn add react-router-dom axios</code></pre>

Most React apps you’ll build will have to maintain state. There’s a lot of libraries available for managing state. But for this tutorial, I’ll be using React’s context API and the `useContext` hook. So let’s set up our app’s context.

Create a new file `src/AppContext.js` and enter the below content.

<pre><code class="language-javascript">import React from "react";
export const AppContext = React.createContext({});

export const AppProvider = ({ children }) =&gt; {
  const reducer = (state, action) =&gt; {
    switch (action.type) {
      case "LOAD_TODOLIST":
        return { ...state, todoList: action.todoList };
      case "LOAD_SINGLE_TODO":
        return { ...state, activeToDoItem: action.todo };
      default:
        return state;
    }
  };
  const [appData, appDispatch] = React.useReducer(reducer, {
    todoList: [],
    activeToDoItem: { id: 0 },
  });
  return (
    &lt;AppContext.Provider value={{ appData, appDispatch }}&gt;
      {children}
    &lt;/AppContext.Provider&gt;
  );
};</code></pre>

Here we create a new context with `React.createContext({})`, for which the initial value is an empty object. We then define an `AppProvider` component that accepts `children` component. It then wraps those children in `AppContext.Provider`, thus making the `{ appData, appDispatch }` object available to all children anywhere in the render tree.

Our `reducer` function defines two action types.

1. `LOAD_TODOLIST` which is used to update the `todoList` array.
2. `LOAD_SINGLE_TODO` which is used to update `activeToDoItem`.

`appData` and `appDispatch` are both returned from the `useReducer` hook. `appData` gives us access to the values in the state while `appDispatch` gives us a function which we can use to update the app’s state.

Now open `index.js`, import the `AppProvider` component and wrap the `<App />` component with `<AppProvider />`. Your final code should look like what I have below.

<pre><code class="language-javascript">import { AppProvider } from "./AppContext";

ReactDOM.render(
  &lt;React.StrictMode&gt;
    &lt;AppProvider&gt;
      &lt;App /&gt;
    &lt;/AppProvider&gt;
  &lt;/React.StrictMode&gt;,
  document.getElementById("root")
);</code></pre>

Wrapping `<App />` inside `<AppProvider />` makes `AppContext` available to every child component in our app.

Remember that with RTL, the aim is to test our app the same way a real user would interact with it. This implies that we also want our tests to interact with our app state. For that reason, we also need to make our `<AppProvider />` available to our components during tests. Let’s see how to make that happen.

The render method provided by RTL is sufficient for simple components that don’t need to maintain state or use navigation. But most apps require at least one of both. For this reason, it provides a `wrapper` option. With this wrapper, we can wrap the UI rendered by the test renderer with any component we like, thus creating a [custom render](https://testing-library.com/docs/react-testing-library/setup#custom-render). Let’s create one for our tests.

Create a new file `src/custom-render.js` and paste the following code.

<pre><code class="language-javascript">import React from "react";
import { render } from "@testing-library/react";
import { MemoryRouter } from "react-router-dom";

import { AppProvider } from "./AppContext";

const Wrapper = ({ children }) =&gt; {
  return (
    &lt;AppProvider&gt;
      &lt;MemoryRouter&gt;{children}&lt;/MemoryRouter&gt;
    &lt;/AppProvider&gt;
  );
};

const customRender = (ui, options) =&gt;
  render(ui, { wrapper: Wrapper, ...options });

// re-export everything
export * from "@testing-library/react";

// override render method
export { customRender as render };</code></pre>

Here we define a `<Wrapper />` component that accepts some children component. It then wraps those children inside `<AppProvider />` and `<MemoryRouter />`. [MemoryRouter](https://reacttraining.com/react-router/web/api/MemoryRouter) is 

> A [`<Router>`](https://reacttraining.com/react-router/Router.md) that keeps the history of your “URL” in memory (does not read or write to the address bar). Useful in tests and non-browser environments like [React Native](https://facebook.github.io/react-native/).

We then create our render function, providing it the Wrapper we just defined through its wrapper option. The effect of this is that any component we pass to the render function is rendered inside `<Wrapper />`, thus having access to navigation and our app’s state.

The next step is to export everything from `@testing-library/react`. Lastly, we export our custom render function as `render`, thus overriding the default render.

Note that even if you were using Redux for state management the same pattern still applies.

Let’s now make sure our new render function works. Import it into `src/App.test.js` and use it to render the `<App />` component.

Open `App.test.js` and replace the import line. This

<pre><code class="language-javascript">import { render } from '@testing-library/react';</code></pre>

should become 

<pre><code class="language-javascript">import { render } from './custom-render';</code></pre>

Does the test still pass? Good job.

There’s one small change I want to make before wrapping up this section. It gets tiring very quickly to have to write `const { getByText }` and other queries every time. So, I’m going to be using the [`screen`](https://testing-library.com/docs/dom-testing-library/api-queries#screen) object from the DOM testing library henceforth.

Import the screen object from our custom render file and replace the `describe` block with the code below.

<div class="break-out">

<pre><code class="language-javascript">import { render, screen } from "./custom-render";

describe("&lt;App /&gt;", () =&gt; {
  it("Renders &lt;App /&gt; component correctly", () =&gt; {
    render(&lt;App /&gt;);
    expect(
      screen.getByText(/Getting started with React testing library/i)
    ).toBeInTheDocument();
  });
});</code></pre>
</div>

We’re now accessing the `getByText` query from the screen object. Does your test still pass? I’m sure it does. Let’s continue.

If your tests don’t pass you may want to compare your code with mine. The corresponding branch at this point is [02-setup-store-and-render](https://github.com/chidimo/Getting-started-with-react-testing-library/tree/02-setup-store-and-render).

{{% ad-panel-leaderboard %}}

## Testing And Building The To-Do List Index Page

In this section, we’ll pull to-do items from [https://jsonplaceholder.typicode.com/](https://jsonplaceholder.typicode.com/). Our component specification is very simple. When a user visits our app homepage,

1. show a loading indicator that says `Fetching todos` while waiting for the response from the API;
2. display the title of 15 to-do items on the screen once the API call returns (the API call returns 200). Also, each item title should be a link that will lead to the to-do details page.

Following a test-driven approach, we’ll write our test before implementing the component logic. Before doing that we’ll need to have the component in question. So go ahead and create a file `src/TodoList.js` and enter the following content:

<pre><code class="language-javascript">import React from "react";
import "./App.css";
export const TodoList = () =&gt; {
  return (
    &lt;div&gt;
    &lt;/div&gt;
  );
};</code></pre>

Since we know the component specification we can test it in isolation before incorporating it into our main app. I believe it’s up to the developer at this point to decide how they want to handle this. One reason you might want to test a component in isolation is so that you don’t accidentally break any existing test and then having to fight fires in two locations. With that out of the way let’s now write the test.

Create a new file `src/TodoList.test.js` and enter the below code:

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import axios from "axios";
import { render, screen, waitForElementToBeRemoved } from "./custom-render";
import { TodoList } from "./TodoList";
import { todos } from "./makeTodos";

describe("&lt;App /&gt;", () =&gt; {
  it("Renders &lt;TodoList /&gt; component", async () =&gt; {
    render(&lt;TodoList /&gt;);
    await waitForElementToBeRemoved(() =&gt; screen.getByText(/Fetching todos/i));

    expect(axios.get).toHaveBeenCalledTimes(1);
    todos.slice(0, 15).forEach((td) =&gt; {
      expect(screen.getByText(td.title)).toBeInTheDocument();
    });
  });
});</code></pre>
</div>

Inside our test block, we render the `<TodoList />` component and use the `waitForElementToBeRemoved` function to wait for the `Fetching todos` text to disappear from the screen. Once this happens we know that our API call has returned. We also check that an Axios `get` call was fired once. Finally, we check that each to-do title is displayed on the screen. Note that the `it` block receives an `async` function. This is necessary for us to be able to use `await` inside the function.

Each to-do item returned by the API has the following structure.

<pre><code class="language-css">{
  id: 0,
  userId: 0,
  title: 'Some title',
  completed: true,
}</code></pre>

We want to return an array of these when we

<pre><code class="language-javascript">import { todos } from "./makeTodos"</code></pre>

The only condition is that each `id` should be unique.

Create a new file `src/makeTodos.js` and enter the below content. This is the source of todos we’ll use in our tests.

<pre><code class="language-javascript">const makeTodos = (n) =&gt; {
  // returns n number of todo items
  // default is 15
  const num = n || 15;
  const todos = [];
  for (let i = 0; i &lt; num; i++) {
    todos.push({
      id: i,
      userId: i,
      title: `Todo item ${i}`,
      completed: [true, false][Math.floor(Math.random() * 2)],
    });
  }
  return todos;
};

export const todos = makeTodos(200);</code></pre>

This function simply generates a list of `n` to-do items. The `completed` line is set by randomly choosing between `true` and `false`.

Unit tests are supposed to be fast. They should run within a few seconds. Fail fast! This is one of the reasons why letting our tests make actual API calls is impractical. To avoid this we **mock** such unpredictable API calls. Mocking simply means replacing a function with a fake version, thus allowing us to customize the behavior. In our case, we want to mock the get method of Axios to return whatever we want it to. Jest already provides mocking functionality out of the box.

Let’s now mock Axios so it returns this list of to-dos when we make the API call in our test. Create a file `src/__mocks__/axios.js` and enter the below content:

<pre><code class="language-javascript">import { todos } from "../makeTodos";

export default {
  get: jest.fn().mockImplementation((url) =&gt; {
    switch (url) {
      case "https://jsonplaceholder.typicode.com/todos":
        return Promise.resolve({ data: todos });
      default:
        throw new Error(`UNMATCHED URL: ${url}`);
    }
  }),
};</code></pre>

When the test starts, Jest automatically finds this **mocks** folder and instead of using the actual Axios from `node_modules/` in our tests, it uses this one. At this point, we’re only mocking the `get` method using Jest’s [mockImplementation](https://jestjs.io/docs/en/mock-function-api#mockfnmockimplementationfn) method. Similarly, we can mock other Axios methods like `post`, `patch`, `interceptors`, `defaults` etc. Right now they’re all undefined and any attempt to access, `axios.post` for example, would result in an error.

Note that we can customize what to return based on the URL the Axios call receives. Also, Axios calls return a promise which resolves to the actual data we want, so we return a promise with the data we want.

At this point, we have one passing test and one failing test. Let’s implement the component logic.

Open `src/TodoList.js` let’s build out the implementation piece by piece. Start by replacing the code inside with this one below.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import axios from "axios";
import { Link } from "react-router-dom";
import "./App.css";
import { AppContext } from "./AppContext";

export const TodoList = () =&gt; {
  const [loading, setLoading] = React.useState(true);
  const { appData, appDispatch } = React.useContext(AppContext);

  React.useEffect(() =&gt; {
    axios.get("https://jsonplaceholder.typicode.com/todos").then((resp) =&gt; {
      const { data } = resp;
      appDispatch({ type: "LOAD_TODOLIST", todoList: data });
      setLoading(false);
    });
  }, [appDispatch, setLoading]);

  return (
    &lt;div&gt;
      // next code block goes here
    &lt;/div&gt;
  );
};</code></pre>
</div>

We import `AppContext` and de-structure `appData` and `appDispatch` from the return value of `React.useContext`. We then make the API call inside a `useEffect` block. Once the API call returns, we set the to-do list in state by firing the `LOAD_TODOLIST` action. Finally, we set the loading state to false to reveal our to-dos.

Now enter the final piece of code.

<pre><code class="language-javascript">{loading ? (
  &lt;p&gt;Fetching todos&lt;/p&gt;
) : (
  &lt;ul&gt;
    {appData.todoList.slice(0, 15).map((item) =&gt; {
      const { id, title } = item;
      return (
        &lt;li key={id}&gt;
          &lt;Link to={`/item/${id}`} data-testid={id}&gt;
            {title}
          &lt;/Link&gt;
        &lt;/li&gt;
      );
    })}
  &lt;/ul&gt;
)}
</code></pre>

We slice `appData.todoList` to get the first 15 items. We then map over those and render each one in a `<Link />` tag so we can click on it and see the details. Note the `data-testid` attribute on each Link. This should be a unique ID that will aid us in finding individual DOM elements. In a case where we have similar text on the screen, we should never have the same ID for any two elements. We’ll see how to use this a bit later.

My tests now pass. Does yours pass? Great.

Let’s now incorporate this component into our render tree. Open up `App.js` let’s do that. 

First things. Add some imports.

<pre><code class="language-javascript">import { BrowserRouter, Route } from "react-router-dom";
import { TodoList } from "./TodoList";</code></pre>

We need `BrowserRouter` for navigation and `Route` for rendering each component in each navigation location.

Now add the below code after the `<header />` element.

<pre><code class="language-html">&lt;div className="App-body"&gt;
  &lt;BrowserRouter&gt;
    &lt;Route exact path="/" component={TodoList} /&gt;
  &lt;/BrowserRouter&gt;
&lt;/div&gt;</code></pre>
          
This is simply telling the browser to render the `<TodoList />` component when we’re on the root location, `/`. Once this is done, our tests still pass but you should see some error messages on your console telling you about some `act` something. You should also see that the `<TodoList />` component seems to be the culprit here.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c59fe17-cd7a-4ac9-ba1f-c6487de7c1d3/02-act-warning.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c59fe17-cd7a-4ac9-ba1f-c6487de7c1d3/02-act-warning.png" sizes="100vw" caption="Terminal showing act warnings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c59fe17-cd7a-4ac9-ba1f-c6487de7c1d3/02-act-warning.png'>Large preview</a>)" alt="Terminal showing act warnings" >}}

Since we’re sure that our TodoList component by itself is okay, we have to look at the App component, inside of which is rendered the `<TodoList />` component.

This warning may seem complex at first but it is telling us that something is happening in our component that we’re not accounting for in our test. The fix is to wait for the loading indicator to be removed from the screen before we proceed.

Open up `App.test.js` and update the code to look like so:

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import { render, screen, waitForElementToBeRemoved } from "./custom-render";
import App from "./App";
describe("&lt;App /&gt;", () =&gt; {
  it("Renders &lt;App /&gt; component correctly", async () =&gt; {
    render(&lt;App /&gt;);
    expect(
      screen.getByText(/Getting started with React testing library/i)
    ).toBeInTheDocument();
    await waitForElementToBeRemoved(() =&gt; screen.getByText(/Fetching todos/i));
  });
});</code></pre>
</div>

We’ve made two changes. First, we changed the function in the `it` block to an `async` function. This is a necessary step to allow us to use `await` in the function body. Secondly, we wait for the `Fetching todos` text to be removed from the screen. And voila!. The warning is gone. Phew! I strongly advise that you bookmark this [post](https://kentcdodds.com/blog/fix-the-not-wrapped-in-act-warning) by Kent Dodds for more on this `act` warning. You’re gonna need it.

Now open the page in your browser and you should see the list of to-dos. You can click on an item if you like, but it won’t show you anything because our router doesn’t yet recognize that URL.

For comparison, the branch of my repo at this point is [03-todolist](https://github.com/chidimo/Getting-started-with-react-testing-library/tree/03-todolist).

Let’s now add the to-do details page.

## Testing And Building The Single To-Do Page

To display a single to-do item we’ll follow a similar approach. The component specification is simple. When a user navigates to a to-do page:

1. display a loading indicator that says `Fetching todo item id` where id represents the to-do’s id, while the API call to https://jsonplaceholder.typicode.com/todos/item_id runs.
2. When the API call returns, show the following information:
    - **Todo item title**
    - **Added by: userId**
    - **This item has been completed** if the to-do has been completed or
    - **This item is yet to be completed** if the to-do has not been completed.

Let’s start with the component. Create a file `src/TodoItem.js` and add the following content.

<pre><code class="language-javascript">import React from "react";
import { useParams } from "react-router-dom";

import "./App.css";

export const TodoItem = () =&gt; {
  const { id } = useParams()
  return (
    &lt;div className="single-todo-item"&gt;
    &lt;/div&gt;
  );
};</code></pre>

The only thing new to us in this file is the `const { id } = useParams()` line. This is a hook from `react-router-dom` that lets us read URL parameters. This id is going to be used in fetching a to-do item from the API.

This situation is a bit different because we’re going to be reading the id from the location URL. We know that when a user clicks a to-do link, the id will show up in the URL which we can then grab using the `useParams()` hook. But here we’re testing the component in isolation which means that there’s nothing to click, even if we wanted to. To get around this we’ll have to mock `react-router-dom`, but only some parts of it. Yes. It’s possible to mock only what we need to. Let’s see how it’s done.

Create a new mock file `src/__mocks__ /react-router-dom.js`. Now paste in the following code:

<pre><code class="language-javascript">module.exports = {
  ...jest.requireActual("react-router-dom"),
  useParams: jest.fn(),
};</code></pre>

By now you should have noticed that when mocking a module we have to use the exact module name as the mock file name.

Here, we use the `module.exports` syntax because `react-router-dom` has mostly named exports. (I haven’t come across any default export since I’ve been working with it. If there are any, kindly share with me in the comments). This is unlike Axios where everything is bundled as methods in one default export.

We first spread the actual `react-router-dom`, then replace the `useParams` hook with a Jest function. Since this function is a Jest function, we can modify it anytime we want. Keep in mind that we’re only mocking the part we need to because if we mock everything, we’ll lose the implementation of `MemoryHistory` which is used in our render function. 

Let’s start testing!

Now create `src/TodoItem.test.js` and enter the below content:

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import axios from "axios";
import { render, screen, waitForElementToBeRemoved } from "./custom-render";
import { useParams, MemoryRouter } from "react-router-dom";
import { TodoItem } from "./TodoItem";

describe("&lt;TodoItem /&gt;", () =&gt; {
  it("can tell mocked from unmocked functions", () =&gt; {
    expect(jest.isMockFunction(useParams)).toBe(true);
    expect(jest.isMockFunction(MemoryRouter)).toBe(false);
  });
});</code></pre>
</div>

Just like before, we have all our imports. The describe block then follows. Our first case is only there as a demonstration that we’re only mocking what we need to. Jest’s [isMockFunction](https://jestjs.io/docs/en/jest-object#jestismockfunctionfn) can tell whether a function is mocked or not. Both expectations pass, confirming the fact that we have a mock where we want it.

Add the below test case for when a to-do item has been completed.

<div class="break-out">

<pre><code class="language-javascript">  it("Renders &lt;TodoItem /&gt; correctly for a completed item", async () =&gt; {
    useParams.mockReturnValue({ id: 1 });
    render(&lt;TodoItem /&gt;);

    await waitForElementToBeRemoved(() =&gt;
      screen.getByText(/Fetching todo item 1/i)
    );

    expect(axios.get).toHaveBeenCalledTimes(1);
    expect(screen.getByText(/todo item 1/)).toBeInTheDocument();
    expect(screen.getByText(/Added by: 1/)).toBeInTheDocument();
    expect(
      screen.getByText(/This item has been completed/)
    ).toBeInTheDocument();
  });</code></pre>
</div>

The very first thing we do is to mock the return value of `useParams`. We want it to return an object with an id property, having a value of 1. When this is parsed in the component, we end up with the following URL https://jsonplaceholder.typicode.com/todos/1. Keep in mind that we have to add a case for this URL in our Axios mock or it will throw an error. We will do that in just a moment.

We now know for sure that calling `useParams()` will return the object `{ id: 1 }` which makes this test case predictable.

As with previous tests, we wait for the loading indicator, `Fetching todo item 1` to be removed from the screen before making our expectations. We expect to see the to-do title, the id of the user who added it, and a message indicating the status.

Open `src/__mocks__/axios.js` and add the following case to the `switch` block.

<div class="break-out">

<pre><code class="language-javascript">      case "https://jsonplaceholder.typicode.com/todos/1":
        return Promise.resolve({
          data: { id: 1, title: "todo item 1", userId: 1, completed: true },
        });</code></pre>
</div>

When this URL is matched, a promise with a completed to-do is returned. Of course, this test case fails since we’re yet to implement the component logic. Go ahead and add a test case for when the to-do item has not been completed.

<div class="break-out">

<pre><code class="language-javascript">  it("Renders &lt;TodoItem /&gt; correctly for an uncompleted item", async () =&gt; {
    useParams.mockReturnValue({ id: 2 });
    render(&lt;TodoItem /&gt;);
    await waitForElementToBeRemoved(() =&gt;
      screen.getByText(/Fetching todo item 2/i)
    );
    expect(axios.get).toHaveBeenCalledTimes(2);
    expect(screen.getByText(/todo item 2/)).toBeInTheDocument();
    expect(screen.getByText(/Added by: 2/)).toBeInTheDocument();
    expect(
      screen.getByText(/This item is yet to be completed/)
    ).toBeInTheDocument();
  });</code></pre>
</div>
 
This is the same as the previous case. The only difference is the ID of the to-do, the `userId`, and the completion status. When we enter the component, we’ll need to make an API call to the URL [https://jsonplaceholder.typicode.com/todos/2](https://jsonplaceholder.typicode.com/todos/2). Go ahead and add a matching case statement to the switch block of our Axios mock.
 
<div class="break-out">

<pre><code class="language-javascript">case "https://jsonplaceholder.typicode.com/todos/2":
  return Promise.resolve({
    data: { id: 2, title: "todo item 2", userId: 2, completed: false },
  });
</code></pre>
</div>
        
When the URL is matched, a promise with an uncompleted to-do is returned.

Both test cases are failing. Now let’s add the component implementation to make them pass.

Open `src/TodoItem.js` and update the code to the following:

<pre><code class="language-javascript">import React from "react";
import axios from "axios";
import { useParams } from "react-router-dom";
import "./App.css";
import { AppContext } from "./AppContext";

export const TodoItem = () =&gt; {
  const { id } = useParams();
  const [loading, setLoading] = React.useState(true);
  const {
    appData: { activeToDoItem },
    appDispatch,
  } = React.useContext(AppContext);

  const { title, completed, userId } = activeToDoItem;
  React.useEffect(() =&gt; {
    axios
      .get(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then((resp) =&gt; {
        const { data } = resp;
        appDispatch({ type: "LOAD_SINGLE_TODO", todo: data });
        setLoading(false);
      });
  }, [id, appDispatch]);
  return (
    &lt;div className="single-todo-item"&gt;
      // next code block goes here.
    &lt;/div&gt;
  );
};
</code></pre>

As with the `<TodoList />` component, we import `AppContext`. We read `activeTodoItem` from it, then we read the to-do title, userId, and completion status. After that we make the API call inside a `useEffect` block. When the API call returns we set the to-do in state by firing the `LOAD_SINGLE_TODO` action. Finally, we set our loading state to false to reveal the to-do details.

Let’s add the final piece of code inside the return div:

<div class="break-out">

<pre><code class="language-javascript">{loading ? (
  &lt;p&gt;Fetching todo item {id}&lt;/p&gt;
) : (
  &lt;div&gt;
    &lt;h2 className="todo-title"&gt;{title}&lt;/h2&gt;
    &lt;h4&gt;Added by: {userId}&lt;/h4&gt;
    {completed ? (
      &lt;p className="completed"&gt;This item has been completed&lt;/p&gt;
    ) : (
      &lt;p className="not-completed"&gt;This item is yet to be completed&lt;/p&gt;
    )}
  &lt;/div&gt;
)}</code></pre>
</div>

Once this is done all tests should now pass. Yay! We have another winner.

Our component tests now pass. But we still haven’t added it to our main app. Let’s do that.

Open `src/App.js` and add the import line:

<pre><code class="language-javascript">import { TodoItem } from './TodoItem'</code></pre>

Add the TodoItem route above the TodoList route. Be sure to preserve the order shown below.

<pre><code class="language-javascript"># preserve this order
&lt;Route path="/item/:id" component={TodoItem} /&gt;
&lt;Route exact path="/" component={TodoList} /&gt;</code></pre>

Open your project in your browser and click on a to-do. Does it take you to the to-do page? Of course, it does. Good job.

In case you’re having any problem, you can check out my code at this point from the [04-test-todo](https://github.com/chidimo/Getting-started-with-react-testing-library/tree/04-test-todo) branch.

Phew! This has been a marathon. But bear with me. There’s one last point I’d like us to touch. Let’s quickly have a test case for when a user visits our app, and then proceed to click on a to-do link. This is a functional test to mimic how our app should work. In practice, this is all the testing we need to be done for this app. It ticks every box in our app specification.

Open `App.test.js` and add a new test case. The code is a bit long so we’ll add it in two steps.

<div class="break-out">

<pre><code class="language-javascript">import userEvent from "@testing-library/user-event";
import { todos } from "./makeTodos";

jest.mock("react-router-dom", () =&gt; ({
  ...jest.requireActual("react-router-dom"),
}));

describe("&lt;App /&gt;"
  ...
  // previous test case
  ...

  it("Renders todos, and I can click to view a todo item", async () =&gt; {
    render(&lt;App /&gt;);
    await waitForElementToBeRemoved(() =&gt; screen.getByText(/Fetching todos/i));
    todos.slice(0, 15).forEach((td) =&gt; {
      expect(screen.getByText(td.title)).toBeInTheDocument();
    });
    // click on a todo item and test the result
    const { id, title, completed, userId } = todos[0];
    axios.get.mockImplementationOnce(() =&gt;
      Promise.resolve({
        data: { id, title, userId, completed },
      })
    );
    userEvent.click(screen.getByTestId(String(id)));
    await waitForElementToBeRemoved(() =&gt;
      screen.getByText(`Fetching todo item ${String(id)}`)
    );

    // next code block goes here
  });
});</code></pre>
</div>

We have two imports of which [userEvent](https://testing-library.com/docs/ecosystem-user-event#docsNav) is new. According to the docs, 

<blockquote>“<a href="https://github.com/testing-library/user-event"><code>user-event</code></a> is a companion library for the <code>React Testing Library</code> that provides a more advanced simulation of browser interactions than the built-in <code>fireEvent</code> method.”</blockquote>

Yes. There is a `fireEvent` method for simulating user events. But userEvent is what you want to be using henceforth.

Before we start the testing process, we need to restore the original `useParams` hooks. This is necessary since we want to test actual behavior, so we should mock as little as possible. Jest provides us with [requireActual](https://jestjs.io/docs/en/jest-object#jestrequireactualmodulename) method which returns the original `react-router-dom` module. 

Note that we must do this before we enter the describe block, otherwise, Jest would ignore it. It states in the documentation that `requireActual`:

<blockquote>“...returns the actual module instead of a mock, bypassing all checks on whether the module should receive a mock implementation or not.”</blockquote>

Once this is done, Jest bypasses every other check and ignores the mocked version of the `react-router-dom`.

As usual, we render the `<App />` component and wait for the `Fetching todos` loading indicator to disappear from the screen. We then check for the presence of the first 15 to-do items on the page.

Once we’re satisfied with that, we grab the first item in our to-do list. To prevent any chance of a URL collision with our global Axios mock, we override the global mock with Jest’s [mockImplementationOnce](https://jestjs.io/docs/en/mock-function-api#mockfnmockimplementationoncefn). This mocked value is valid for one call to the Axios get method. We then grab a link by its `data-testid` attribute and fire a user click event on that link. Then we wait for the loading indicator for the single to-do page to disappear from the screen.

Now finish the test by adding the below expectations in the position indicated.

<div class="break-out">

<pre><code class="language-javascript">expect(screen.getByText(title)).toBeInTheDocument();
expect(screen.getByText(`Added by: ${userId}`)).toBeInTheDocument();
switch (completed) {
  case true:
    expect(
      screen.getByText(/This item has been completed/)
    ).toBeInTheDocument();
    break;
  case false:
    expect(
      screen.getByText(/This item is yet to be completed/)
    ).toBeInTheDocument();
    break;
  default:
    throw new Error("No match");
    }
  </code></pre>
</div>

We expect to see the to-do title and the user who added it. Finally, since we can’t be sure about the to-do status, we create a switch block to handle both cases. If a match is not found we throw an error.

You should have 6 passing tests and a functional app at this point. In case you’re having trouble, the corresponding branch in my repo is [05-test-user-action](https://github.com/chidimo/Getting-started-with-react-testing-library/tree/05-test-user-action).

## Conclusion

Phew! That was some marathon. If you made it to this point, congratulations. You now have almost all you need to write tests for your React apps. I strongly advise that you read CRA’s [testing docs](https://create-react-app.dev/docs/running-tests/) and RTL’s documentation. Overall both are relatively short and direct.

I strongly encourage you to start writing tests for your React apps, no matter how small. Even if it’s just smoke tests to make sure your components render. You can incrementally add more test cases over time.

### Related Resources

- “[Testing Overview](https://reactjs.org/docs/testing.html),” React official website
- “[`Expect`](https://jestjs.io/docs/en/expect.html),” Jest API Reference
- “[Custom Render](https://testing-library.com/docs/react-testing-library/setup#custom-render),” React Testing Library
- “[`jest-dom`](https://github.com/testing-library/jest-dom),” Testing Library, GitHub
- “[Guiding Principles](https://testing-library.com/docs/guiding-principles),” Getting Started, Testing Library
- “[React Testing Library](https://testing-library.com/docs/react-testing-library/intro),” Testing Library
- “[Recommended Tools](https://reactjs.org/docs/testing.html#tools),” Testing Overview, React official website
- “[Fix the "not wrapped in act(...)" warning](https://kentcdodds.com/blog/fix-the-not-wrapped-in-act-warning),” Kent C. Dodds
- “[`<MemoryRouter>`](https://reacttraining.com/react-router/web/api/MemoryRouter),” React Training
- “[`screen`](https://testing-library.com/docs/dom-testing-library/api-queries#screen),” DOM Testing Library
- “[`user-event`](https://testing-library.com/docs/ecosystem-user-event#docsNav),” Ecosystem, Testing Library Docs
- “[The Different Types Of Software Testing](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing),” Sten Pittet, Atlassian

{{< signature "ks, ra, yk, il" >}}
