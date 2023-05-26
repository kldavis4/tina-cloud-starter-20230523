---
title: 'Unit Testing In React Native Applications'
slug: unit-testing-react-native-applications
author: fortune-ikechi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d79e64d5-b6a5-493d-9156-1e8f92d02676/unit-testing-react-native-applications.png
date: 2020-09-29T12:30:00.000Z
summary: >-
  Unit testing has become an integral part of the software development process. It is the level of testing at which the components of the software are tested. In this tutorial, you’ll learn how to test units of a React Native application.
description: >-
  Unit testing has become an integral part of the software development process. It is the level of testing at which the components of the software are tested. In this tutorial, you’ll learn how to test units of a React Native application.
categories:
  - Apps
  - React
  - Testing
---

React Native is one of the most widely used frameworks for building mobile applications. This tutorial is targeted at developers who want to get started testing React Native applications that they build. We’ll make use of the Jest testing framework and Enzyme.

In this article, we’ll learn the core principles of testing, explore various libraries for testing an application, and see how to test units (or components) of a React Native application. By working with a React Native application, we’ll solidify our knowledge of testing.

**Note:** Basic knowledge of JavaScript and React Native would be of great benefit as you work through this tutorial.

## What Is Unit Testing?

Unit testing is the level of testing at which individual components of the software are tested. We do it to ensure that each component works as expected. A component is the smallest testable part of the software.

To illustrate, let’s create a `Button` component and simulate a unit test:

<pre><code class="language-javascript">import React from 'react';
import { StyleSheet, Text, TouchableOpacity } from 'react-native';
function AppButton({ onPress }) {
    return (
      &lt;TouchableOpacity
          style={[styles.button,
              { backgroundColor: colors[color] }]}
                 onPress={onPress} &gt;
          &lt;Text style={styles.text}&gt;Register&lt;/Text&gt;
      &lt;/TouchableOpacity&gt;
    );
}
const styles = StyleSheet.create({
    button: {
        backgroundColor: red;
        borderRadius: 25,
        justifyContent: 'center',
        alignItems: 'center',
    },
    text: {
        color: #fff
    }
})
export default AppButton;
</code></pre>

This `Button` component has text and an `onPress` function. Let’s test this component to see what unit testing is about.

First, let’s create a test file, named `Button.test.js`:

<pre><code class="language-javascript">it('renders correctly across screens', () =&gt; {
  const tree = renderer.create(&lt;Button /&gt;).toJSON();
  expect(tree).toMatchSnapshot();
});
</code></pre>

Here, we are testing to see whether our `Button` component renders as it should on all screens of the application. This is what unit testing is all about: testing components of an application to make sure they work as they should.

## Unit Testing In React Native Applications

A React Native application can be tested with a variety of tools, some of which are the following:

- **WebDriver**  
This open-source testing tool for Node.js apps is also used to test React Native applications.
- **Nightmare**  
This automates test operations in the browser. According to the [documentation](https://github.com/segmentio/nightmare), “the goal is to expose a few simple methods that mimic user actions (like `goto`, `type` and `click`), with an API that feels synchronous for each block of scripting, rather than deeply nested callbacks.”
- **Jest**  
This is one of the most popular testing libraries out there and the one we’ll be focusing on today. Like React, it is maintained by Facebook and was made to provide a “zero config” setup for maximum performance.
- **Mocha**  
Mocha is a popular library for testing React and React Native applications. It has become a testing tool of choice for developers because of how easy it is to set up and use and how fast it is.
- **Jasmine**  
According to its [documentation](https://jasmine.github.io/), Jasmine is a behavior-driven development framework for testing JavaScript code.

{{% feature-panel %}}

## Introduction To Jest And Enzyme

According to its [documentation](https://jestjs.io/), “Jest is a delightful JavaScript testing framework with a focus on simplicity”. It works with zero configuration. Upon installation (using a package manager such as npm or Yarn), Jest is ready to use, with no other installations needed.

[Enzyme](https://enzymejs.github.io/enzyme/) is a JavaScript testing framework for React Native applications. (If you’re working with React rather than React Native, [a guide is available](https://www.smashingmagazine.com/2020/06/practical-guide-testing-react-applications-jest/).) We’ll use Enzyme to test units of our application’s output. With it, we can simulate the application's runtime.

Let’s get started by setting up our project. We’ll be using the [Done With It](https://github.com/iamfortune/Done-With-It-App) app on GitHub. It’s a React Native application marketplace. Start by cloning it, navigate into the folder, and install the packages by running the following for npm…

<pre><code class="language-bash">npm install
</code></pre>

… or this for Yarn:

<pre><code class="language-bash">yarn install
</code></pre>

This command will install all of the packages in our application. Once that’s done, we’ll test our application’s UI consistency using snapshots, covered below.

## Snapshots And Jest Configuration

In this section, we’ll test for user touches and the UI of the app’s components by testing snapshots using Jest.

Before doing that, we need to install Jest and its dependencies. To install Jest for Expo React Native, run the following command:

<pre><code class="language-bash">yarn add jest-expo --dev
</code></pre>

This installs `jest-expo` in our application’s directory. Next, we need to update our `package.json` file to have a test script:

<pre><code class="language-json">"scripts": {
    "test" "jest"
},
"jest": {
    "preset": "jest-expo"
}
</code></pre>

By adding this command, we are telling Jest which package to register in our application and where.

Next is adding other packages to our application that will aid Jest to do a comprehensive test. For npm, run this…

<pre><code class="language-bash">npm i react-test-renderer --save-dev
</code></pre>

… and for Yarn, this:

<pre><code class="language-bash">yarn add react-test-renderer --dev
</code></pre>

We still have a little configuration to do in our `package.json` file. [According to Expo React Native’s documentation](https://jestjs.io/docs/en/configuration.html#transformignorepatterns-arraystring), we need to add a `transformIgnorePattern` configuration that prevents tests from running in Jest whenever a source file matches a test (i.e. if a test is made and a similar file is found in the `node modules` of the project).

<div class="break-out">

 <pre><code class="language-json">"jest": {
  "preset": "jest-expo",
  "transformIgnorePatterns": [
    "node_modules/(?!(jest-)?react-native|react-clone-referenced-element|@react-native-community|expo(nent)?|@expo(nent)?/.*|react-navigation|@react-navigation/.*|@unimodules/.*|unimodules|sentry-expo|native-base|@sentry/.*)"
  ]
}
</code></pre>
</div>

Now, let’s create a new file, named `App.test.js`, to write our first test. We will test whether our `App` has one child element in its tree:

<div class="break-out">

 <pre><code class="language-javascript">import React from "react";
import renderer from "react-test-renderer";
import App from "./App.js"
describe("&lt;App /&gt;", () =&gt; {
    it('has 1 child', () =&gt; {
        const tree = renderer.create(&lt;App /&gt;).toJSON();
        expect(tree.children.length).toBe(1);
    });
});
</code></pre>
</div>

Now, run `yarn test` or its npm equivalent. If `App.js` has a single child element, our test should pass, which will be confirmed in the command-line interface.

In the code above, we’ve imported `React` and `react-test-renderer`, which renders our tests for `Expo`. We’ve converted the `<App />` component tree to JSON, and then asked Jest to see whether the returned number of child components in JSON equals what we expect.

{{% ad-panel-leaderboard %}}

## More Snapshot Tests

As [David Adeneye states](https://www.smashingmagazine.com/2020/06/practical-guide-testing-react-applications-jest/):

<blockquote>“A snapshot test makes sure that the user interface (UI) of a web application does not change unexpectedly. It captures the code of a component at a moment in time, so that we can compare the component in one state with any other possible state it might take.”</blockquote>

This is done especially when a project involves global styles that are used across a lot of components. Let’s write a snapshot test for `App.js` to test its UI consistency:

<pre><code class="language-javascript">it('renders correctly across screens', () => {
  const tree = renderer.create(<App />).toJSON();
  expect(tree).toMatchSnapshot();
});
</code></pre>

Add this to the tests we’ve already written, and then run `yarn test` (or its npm equivalent). If our test passes, we should see this:

<pre><code class="language-bash">  PASS  src/App.test.js
  √ has 1 child (16ms)
  √ renders correctly (16ms)

Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
Snapshots:   1 total
Time:        24s
</code></pre>

This tells us that our tests passed and the time they took. Your result will look similar if the tests passed.

Let’s move on to mocking some functions in Jest.

## Mocking API Calls

[According to Jest’s documentation](https://jestjs.io/docs/en/mock-functions#:~:text=Mock%20functions%20allow%20you%20to,time%20configuration%20of%20return%20values.):

<blockquote>Mock functions allow you to test the links between code by erasing the actual implementation of a function, capturing calls to the function (and the parameters passed in those calls), capturing instances of constructor functions when instantiated with `new`, and allowing test-time configuration of return values.</blockquote>

Simply put, a mock is a copy of an object or function without the real workings of that function. It imitates that function.

Mocks help us test apps in so many ways, but the main benefit is that they reduce our need for dependencies.

Mocks can usually be performed in one of two ways. One is to create a mock function that is injected into the code to be tested. The other is to write a mock function that overrides the package or dependency that is attached to the component.

Most organizations and developers prefer to write manual mocks that imitate functionality and use fake data to test some components.

React Native includes `fetch` in the global object. To avoid making real API calls in our unit test, we mock them. Below is a way to mock all, if not most, of our API calls in React Native, and without the need for dependencies:

<div class="break-out">

 <pre><code class="language-javascript">global.fetch = jest.fn();

// mocking an API success response once
fetch.mockResponseIsSuccess = (body) => {
  fetch.mockImplementationForOnce (
    () => Promise.resolve({json: () => Promise.resolve(JSON.parse(body))})
  );
};

// mocking an API failure response for once
fetch.mockResponseIsFailure = (error) => {
  fetch.mockImplementationForOnce(
    () => Promise.reject(error)
  );
};
</code></pre>
</div>

Here, we’ve written a function that tries to fetch an API once. Having done this, it returns a promise, and when it is resolved, it returns the body in JSON. It’s similar to the mock response for a failed fetch transaction &mdash; it returns an error.

Below is the `product` component of our application, containing a `product` object and returning the information as `props`.

<pre><code class="language-javascript">import React from 'react';
const Product = () =&gt; {
    const product = {
        name: 'Pizza',
        quantity: 5,
        price: '$50'
    }
    return (
        &lt;&gt;
            &lt;h1&gt;Name: {product.name}&lt;/h1&gt;   
            &lt;h1&gt;Quantity: {product.quantity}&lt;/h1&gt;   
            &lt;h1&gt;Price: {product.price}&lt;/h1&gt;   
        &lt;/&gt;
    );
}
export default Product;
</code></pre>

Let’s imagine we are trying to test all of our product’s components. Directly accessing our database is not a feasible solution. This is where mocks come into play. In the code below, we are trying to mock a component of the product by using Jest to describe the objects in the component.

<pre><code class="language-javascript">describe("", () =&gt; {
  it("accepts products props", () =&gt; {
    const wrapper = mount(&lt;Customer product={product} /&gt;);
    expect(wrapper.props().product).toEqual(product);
  });
  it("contains products quantity", () =&gt; {
    expect(value).toBe(3);
  });
});
</code></pre>

We are using `describe` from Jest to dictate the tests we want to be done. In the first test, we are checking to see whether the object we are passing is equal to the props we’ve mocked.

In the second test, we are passing the `customer` props to make sure it is a product and that it matches our mocks. In doing so, we don’t have to test all of our product’s components, and we also get to prevent bugs in our code.

{{% ad-panel-leaderboard %}}

## Mocking External API Requests

Until now, we’ve been running tests for API calls with other elements in our application. Now let’s mock an external API call. We are going to be using Axios. To test an external call to an API, we have to mock our requests and also manage the responses we get. We are going to use `axios-mock-adapter` to mock Axios. First, we need to install `axios-mock-adapter` by running the command below:

<pre><code class="language-bash">yarn add axios-mock-adapter
</code></pre>

The next thing to do is create our mocks:

<div class="break-out">

 <pre><code class="language-javascript">import MockAdapter from 'axios-mock-adapter';
import Faker from 'faker'
import ApiClient from '../constants/api-client';
import userDetails from 'jest/mockResponseObjects/user-objects';

let mockApi = new MockAdapter(ApiClient.getAxiosInstance());
let validAuthentication = {
    name: Faker.internet.email(),
    password: Faker.internet.password()

mockApi.onPost('requests').reply(config) => {
  if (config.data ===  validAuthentication) {
      return [200, userDetails];
    }
  return [400, 'Incorrect username and password'];
 });
</code></pre>
</div>

Here, we are calling the `ApiClient` and passing an Axios instance to it to mock the user’s credentials. We are using a package named [faker.js](https://github.com/marak/Faker.js/) to generate fake user data, such as an email address and password.

The mock behaves as we expect the API to. If the request is successful, we’ll get a response with a status code of 200 for OK. And we’ll get a status code of 400 for a bad request to the server, which would be sent with JSON with the message “Incorrect username and password”.

Now that our mock is ready, let’s write a test for an external API request. As before, we’ll be using snapshots.

<div class="break-out">

 <pre><code class="language-javascript">it('successful sign in with correct credentials', async () =&gt; {
  await store.dispatch(authenticateUser('ikechifortune@gmail.com', 'password'));
  expect(getActions()).toMatchSnapshot();
});

it('unsuccessful sign in with wrong credentials', async () =&gt; {
  await store.dispatch(authenticateUser('ikechifortune@gmail.com', 'wrong credential'))
  .catch((error) => {
    expect(errorObject).toMatchSnapshot();
  });
</code></pre>
</div>

Here, we’re testing for a successful sign-in with the correct credentials, using the native JavaScript `async await` to hold our inputs. Meanwhile, the `authenticateUser` function from Jest authenticates the request and makes sure it matches our earlier snapshots. Next, we test for an unsuccessful sign-in in case of wrong credentials, such as email address or password, and we send an error as a response.

Now, run `yarn test` or `npm test`. I’m sure all of your tests will pass.

Let’s see how to test components in a state-management library, Redux.

## Testing Redux Actions And Reducers Using Snapshots

There’s no denying that Redux is one of the most widely used state managers for React applications. Most of the functionality in Redux involves a `dispatch`, which is a function of the Redux store that is used to trigger a change in the state of an application. Testing Redux can be tricky because Redux's `actions` grow quickly in size and complexity. With Jest snapshots, this becomes easier. Most testing with Redux comes down to two things:

- To test `actions`, we create `redux-mock-store` and dispatch the actions.
- To test reducers, we import the `reducer` and pass a state and action object to it.

Below is a Redux test with snapshots. We will be testing the actions dispatched by authenticating the user at `SIGN-IN` and seeing how the `LOGOUT` action is handled by the `user` reducer.

<div class="break-out">

 <pre><code class="language-javascript">import mockStore from 'redux-mock-store';
import { LOGOUT } from '../actions/logout';
import User from '../reducers/user';
import { testUser } from 'jest/mock-objects';

  describe('Testing the sign in authentication', () => {
    const store = mockStore();

  it('user attempts with correct password and succeeds', async () => {
  await store.dispatch(authenticateUser('example@gmail.com', 'password'));
  expect(store.getActions()).toMatchSnapshot();
  });
});
  describe('Testing reducers after user LOGS OUT', () => {
    it('user is returned back to initial app state', () => {
      expect(user(testUser, { type: LOGOUT })).toMatchSnapshot();
    });
  });
</code></pre>
</div>

In the first test, we are describing the sign-in authentication and creating a mock store. We do this by first importing a `mockStore` from Redux, and then importing a method named `testUser` from Jest to help us mock a user. Next, we test for when the user successfully signs into the application using an email address and password that matches the ones in our snapshot store. So, the snapshot ensures that the objects that the user is inputting match every time a test is run.

In the second test, we are testing for when the user logs out. Once our reducer snapshot confirms that a user has logged out, it returns to the initial state of the application.

Next, we test by running `yarn test`. If the tests have passed, we should see the following result:

<pre><code class="language-bash">  PASS  src/redux/actions.test.js
  √ user attempts with correct password and succeeds (23ms)
  √ user is returned back to initial app state (19ms)

Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
Snapshots:   2 total
Time:        31s
</code></pre>

## Conclusion

With Jest, testing React Native applications has never been easier, especially with snapshots, which ensure that the UI remains consistent regardless of the global styles. Also, Jest allows us to mock certain API calls and modules in our application. We can take this further by testing components of a React Native application.

### Further Resources

- “[A Practical Guide to Testing React Native Applications With Jest](https://www.smashingmagazine.com/2020/06/practical-guide-testing-react-applications-jest/)”, David Adeneye, Smashing Magazine
- [Jest documentation](https://jestjs.io/docs/en/getting-started)
- “[Testing With Jest](https://docs.expo.io/guides/testing-with-jest/)”, Expo React Native documentation
- “[Learning to Test React Native With Jest](https://medium.com/react-native-training/learning-to-test-react-native-with-jest-part-1-f782c4e30101)”, Jason Gaare

{{< signature "ks, ra, al, il" >}}
