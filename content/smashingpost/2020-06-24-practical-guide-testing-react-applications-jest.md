---
title: 'A Practical Guide To Testing React Applications With Jest'
slug: practical-guide-testing-react-applications-jest
author: adeneye-david-abiodun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eb1875a-5639-4501-9745-cee3b35f343d/practical-guide-testing-react-applications-jest.png
date: 2020-06-24T12:00:00.000Z
summary: >-
  Building a well-functioning application requires good testing; otherwise, knowing whether your application works as expected would be a matter of guesswork and luck. Jest is one of the best tools available for testing React applications. In this article, you will learn everything you need to create a solid test for your React components and application.
description: >-
  Building a well-functioning application requires good testing; otherwise, knowing whether your application works as expected would be a matter of guesswork and luck. Jest is one of the best tools available for testing React applications. In this article, you will learn everything you need to create a solid test for your React components and application.
categories:
  - Apps
  - React
  - Testing
---

In this article, I’m going to introduce you to a React testing tool named [Jest](https://jestjs.io/en/), along with the popular library [Enzyme](https://enzymejs.github.io/enzyme/), which is designed to test React components. I’ll introduce you to Jest testing techniques, including: running tests, testing React components, snapshot testing, and mocking.
If you are new to testing and wondering how to get started, you will find this tutorial helpful because we will start with an introduction to testing. By the end, you’ll be up and running, testing React applications using Jest and Enzyme. You should be familiar with [React](https://reactjs.org/) in order to follow this tutorial.

## A Brief Introduction To Testing

Testing is a line-by-line review of how your code will execute. A suite of tests for an application comprises various bit of code to verify whether an application is executing successfully and without error. Testing also comes in handy when updates are made to code. After updating a piece of code, you can run a test to ensure that the update does not break functionality already in the application.

## Why Test?

It’s good to understand why we doing something before doing it. So, why test, and what is its purpose?

1. The first purpose of testing is to prevent regression. [Regression](https://en.wikipedia.org/wiki/Regression_testing) is the reappearance of a bug that had previously been fixed. It makes a feature stop functioning as intended after a certain event occurs.
2. Testing ensures the functionality of complex components and modular applications.
3. Testing is required for the effective performance of a software application or product.

Testing makes an app more robust and less prone to error. It’s a way to verify that your code does what you want it to do and that your app works as intended for your users.

{{% feature-panel %}}

Let’s go over the types of testing and what they do.

### Unit Test

In this type of test, individual units or components of the software are tested. A unit might be an individual function, method, procedure, module, or object. A unit test isolates a section of code and verifies its correctness, in order to validate that each unit of the software’s code performs as expected.

In unit testing, individual procedures or functions are tested to guarantee that they are operating properly, and all components are tested individually. For instance, testing a function or whether a statement or loop in a program is functioning properly would fall under the scope of unit testing. 

### Component Test

Component testing verifies the functionality of an individual part of an application. Tests are performed on each component in isolation from other components. Generally, React applications are made up of several components, so component testing deals with testing these components individually.

For example, consider a website that has different web pages with many components. Every component will have its own subcomponents. Testing each module without considering integration with other components is referred to as component testing.

Testing like this in React requires more sophisticated tools. So, we would need Jest and sometimes more sophisticated tools, like Enzyme, which we will discuss briefly later.

### Snapshot Test

A snapshot test makes sure that the user interface (UI) of a web application does not change unexpectedly. It captures the code of a component at a moment in time, so that we can compare the component in one state with any other possible state it might take.

We will learn about snapshot testing in a later section.

## Advantages and Disadvantages of Testing

Testing is great and should be done, but it has advantages and disadvantages.

### Advantages

1. It prevents unexpected regression.
2. It allows the developer to focus on the current task, rather than worrying about the past.
3. It allows modular construction of an application that would otherwise be too complex to build.
4. It reduces the need for manual verification.
    
### Disadvantages

1. You need to write more code, as well as debug and maintain.
2. Non-critical test failures might cause the app to be rejected in terms of continuous integration.

## Introduction to Jest

[Jest](https://jestjs.io/en/) is a delightful JavaScript testing framework with a focus on simplicity. It can be installed with npm or Yarn. Jest fits into a broader category of utilities known as [test runners](https://www.quora.com/What-is-a-test-runner). It works great for React applications, but it also works great outside of React applications.

[Enzyme](https://enzymejs.github.io/enzyme/) is a library that is used to test React applications. It’s designed to test components, and it makes it possible to write assertions that simulate actions that confirm whether the UI is working correctly.

Jest and Enzyme complement each other so well, so in this article we will be using both.
  
## Process Of Running A Test With Jest

In this section, we will be installing Jest and writing tests. If you are new to React, then I recommend using [Create React App](https://create-react-app.dev/), because it is ready for use and ships with Jest. 

<pre><code class="language-bash">npm init react-app my-app
</code></pre>

We need to install Enzyme ****and `enzyme-adapter-react-16` with `react-test-renderer` (the number should be based on the version of React you’re using).

<pre><code class="language-bash">npm install --save-dev enzyme enzyme-adapter-react-16 react-test-renderer
</code></pre>

Now that we have created our project with both Jest and Enzyme, we need to create a `setupTest.js` file in the `src` folder of the project. The file should look like this:

<pre><code class="language-javascript">import { configure } from "enzyme";
import Adapter from "enzyme-adapter-react-16";
configure({ adapter: new Adapter() });
</code></pre>

This imports Enzyme and sets up the adapter to run our tests.

Before continuing, let’s learn some basics. Some key things are used a lot in this article, and you’ll need to understand them.

- `it` or `test`
    You would pass a function to this method, and the test runner would execute that function as a block of tests.
- `describe`
    This optional method is for grouping any number of `it` or `test` statements.
- `expect`
    This is the condition that the test needs to pass. It compares the received parameter to the matcher. It also gives you access to a number of matchers that let you validate different things. You can read more about it [in the documentation](https://jestjs.io/docs/en/expect).
- `mount`
    This method renders the full DOM, including the child components of the parent component, in which we are running the tests.
- `shallow`
    This renders only the individual components that we are testing. It does not render child components. This enables us to test components in isolation.

{{% ad-panel-leaderboard %}}

## Creating A Test File

How does Jest know what’s a test file and what isn’t? The first rule is that any files found in any directory with the name `__test__` are considered a test. If you put a JavaScript file in one of these folders, Jest will try to run it when you call Jest, for better or for worse. The second rule is that Jest will recognize any file with the suffix `.spec.js` or `.test.js`. It will search the names of all folders and all files in your entire repository.

Let’s create our first test, for a React mini-application created for this tutorial. You can clone it [on Git](https://github.com/daacode/react-jest)[H](https://github.com/daacode/react-jest)[ub](https://github.com/daacode/react-jest).  Run `npm install` to install all of the packages, and then `npm start` to launch the app. Check the `README.md` file for more information.

Let’s open `App.test.js` to write our first test. First, check whether our app component renders correctly and whether we have specified an output:

<pre><code class="language-javascript">it("renders without crashing", () => {
  shallow(&lt;App /&gt;);
});

it("renders Account header", () => {
  const wrapper = shallow(&lt;App /&gt;);
  const welcome = &lt;h1&gt;Display Active Users Account Details&lt;/h1&gt;;
  expect(wrapper.contains(welcome)).toEqual(true);
});
</code></pre>

In the test above, the first test, with `shallow`, checks to see whether our app component renders correctly without crashing. Remember that the `shallow` method renders only a single component, without child components.

The second test checks whether we have specified an `h1`  tag output of “Display Active User Account” in our app component, with a [Jest matcher](https://jestjs.io/docs/en/expect.html) of `toEqual`.

Now, run the test:

<pre><code class="language-bash">npm run test 
/* OR */
npm test
</code></pre>

The output in your terminal should like this:

<pre><code class="language-bash">  PASS  src/App.test.js
  √ renders without crashing (34ms)
  √ renders Account header (13ms)

Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
Snapshots:   0 total
Time:        11.239s, estimated 16s
Ran all test suites related to changed files.

Watch Usage: Press w to show more.
</code></pre>

As you can see, our test passed. It shows we have one test suite named `App.test.js`, with two successful tests when Jest ran. We’ll talk about snapshot testing later, and you will also get to see an example of a failed test.

## Skipping Or Isolating A Test

Skipping or isolating a test means that when Jest runs, a specific marked test is not run.

<pre><code class="language-javascript">it.skip("renders without crashing", () => {
  shallow(&lt;App /&gt;);
});

it("renders Account header", () => {
  const wrapper = shallow(&lt;App /&gt;);
  const header = &lt;h1&gt;Display Active Users Account Details&lt;/h1&gt;;
  expect(wrapper.contains(header)).toEqual(true);
});
</code></pre>

Our first test will be skipped because we’ve used the `skip` method to isolate the test. So, it will not run or make any changes to our test when Jest runs. Only the second one will run. You can also use `it.only()`.

It’s a bit frustrating to make changes to a test file and then have to manually run `npm test` again. Jest has a nice feature called watch mode, which watches for file changes and runs tests accordingly. To run Jest in watch mode, you can run `npm test -- --watch` or `jest --watch`. I would also recommend leaving Jest running in the terminal window for the rest of this tutorial.

## Mocking Function

A mock is a convincing duplicate of an object or module without any real inner workings. It might have a tiny bit of functionality, but compared to the real thing, it’s a mock. It can be created automatically by Jest or manually.

Why should we mock? Mocking reduces the number of dependencies — that is, the number of related files that have to be loaded and parsed when a test is run. So, using a lot of mocks makes tests execute more quickly.

Mock functions are also known as “spies”, because they let you spy on the behavior of a function that is called directly by some other code, rather than only testing the output.

There are two ways to mock a function: either by creating a mock function to use it in test code, or by writing a manual mock to override a module dependency.

Manual mocks ****are used to stub out functionality with mock data. For example, instead of accessing a remote resource, like a website or a database, you might want to create a manual mock that allows you to use fake data.

We will use a mock function in the next section.

{{% ad-panel-leaderboard %}}

## Testing React Components

The section will combine all of the knowledge we have gained so far in understanding how to test React components. Testing involves making sure the output of a component hasn’t unexpectedly changed to something else. Constructing components in the right way is by far the most effective way to ensure successful testing.

One thing we can do is to test components props — specifically, testing whether props from one component are being passed to another. Jest and the Enzyme API allow us to create a mock function to simulate whether props are being passed between components.

We have to pass the user-account props from the main `App` component to the `Account` component. We need to give user-account details to `Account` in order to render the active account of users. This is where mocking comes in handy, enabling us to test our components with fake data.

Let’s create a mock for the `user` props:

<pre><code class="language-javascript">const user = {
  name: "Adeneye David",
  email: "david@gmail.com",
  username: "Dave",
};
</code></pre>

We have created a manual mock function in our test file and wrapped it around the components. Let’s say we are testing a large database of users. Accessing the database directly from our test file is not advisable. Instead, we create a mock function, which enables us to use fake data to test our component.

<pre><code class="language-javascript">describe("<Account />", () => {
  it("accepts user account props", () => {
    const wrapper = mount(&lt;Account user={user} /&gt;);
    expect(wrapper.props().user).toEqual(user);
  });
  it("contains users account email", () => {
    const wrapper = mount(&lt;Account user={user} /&gt;);
    const value = wrapper.find("p").text();
    expect(value).toEqual("david@gmail.com");
  });
});
</code></pre>

We have two tests above, and we use a `describe` layer, which takes the component being tested. By specifying the props and values that we expect to be passed by the test, we are able to proceed.

In the first test, we check whether the props that we passed to the mounted component equal the mock props that we created above.

For the second test, we pass the user props to the mounted `Account` component. Then, we check whether we can find the `<p>` element that corresponds to what we have in the `Account` component. When we run the test suite, you’ll see that the test runs successfully.

We can also test the state of our component. Let’s check whether the state of the error message is equal to null:

<pre><code class="language-javascript">it("renders correctly with no error message", () => {
  const wrapper = mount(<App />);
  expect(wrapper.state("error")).toEqual(null);
});
</code></pre>

In this test, we check whether the state of our component error is equal to null, using a `toEqual()` matcher. If there is an error message in our app, the test will fail when run.

In the next section, we will go through how to test React components with snapshot testing, another amazing technique.

## Snapshot Testing

Snapshot testing captures the code of a component at a moment in time, in order to compare it to a reference snapshot file stored alongside the test. It is used to keep track of changes in an app’s UI.

The actual code representation of a snapshot is a JSON file, and this JSON contains a record of what the component looked like when the snapshot was made. During a test, Jest compares the contents of this JSON file to the output of the component during the test. If they match, the test passes; if they don't, the test fails.

To convert an Enzyme wrapper to a format that is compatible with Jest snapshot testing, we have to install `enzyme-to-json`:

<pre><code class="language-bash">npm install --save-dev enzyme-to-json
</code></pre>

Let’s create our snapshot test. When we run it the first time, the snapshot of that component’s code will be composed and saved in a new `__snapshots__` folder in the `src` directory.

<pre><code class="language-javascript">it("renders correctly", () => {
  const tree = shallow(&lt;App /&gt;);
  expect(toJson(tree)).toMatchSnapshot();
});
</code></pre>
 
When the test above runs successfully, the current UI component will be compared to the existing one.

Now, let’s run the test:
 

<pre><code class="language-bash">npm run test
</code></pre>

When the test suite runs, a new snapshot will be generated and saved to the `__snapshots__` folder. When we run a test subsequently, Jest will check whether the components match the snapshot.

As explained in the previous section, that `shallow` method from the Enzyme package is used to render a single component and nothing else. It doesn’t render child components. Rather, it gives us a nice way to isolate code and get better information when debugging. Another method, named `mount`, is used to render the full DOM, including the child components of the parent component, in which we are running the tests.

We can also update our snapshot, Let’s make some changes to our component in order to make our test fail, which will happen because the component no longer corresponds to what we have in the snapshot file. To do this, let’s change the `<h3>` tag in our component from `<h3> Loading...</h3>` to `<h3>Fetching Users...</h3>`. When the test runs, this what we will get in the terminal:

<div class="break-out">

 <pre><code class="language-javascript"> FAIL  src/App.test.js (30.696s)
  × renders correctly (44ms)

  ● renders correctly

    expect(received).toMatchSnapshot()
    Snapshot name: `renders correctly
1

    - Snapshot
    + Received

      <Fragment>
        <h1>
          Display Active Users Account Details
        </h1>
        <h3>
    -     Loading...
    +     Fetching Users...
        </h3>
      </Fragment>

       7 | it("renders correctly", ()
=> {
       8 |   const wrapper = shallow(<App />);
    >  9 |   expect(toJson(wrapper)).toMatchSnapshot();
         |                           ^      10 | });
      11 |
      12 | /* it("renders without crashing", () => {

      at Object.<anonymous> (src/App.test.js:9:27)

 › 1 snapshot failed.
Snapshot Summary
 › 1 snapshot failed from 1 test suite. Inspect your code changes or press `u` to update them.

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   1 failed, 1 total
Time:        92.274s
Ran all test suites related to changed files.

Watch Usage: Press w to show more.
</code></pre>
</div>

If we want our test to pass, we would either change the test to its previous state or update the snapshot file. In the command line, Jest provides instruction on how to update the snapshot. First, press `w` in the command line to show more, and then press `u` to update the snapshot.


    › Press u to update failing snapshots.

When we press `u` to update the snapshot, the test will pass.


## Conclusion

I hope you’ve enjoyed working through this tutorial. We’ve learned some Jest testing techniques using the Enzyme testing library. I’ve also introduced you to the process of running a test, testing React components, mocking, and snapshot testing. If you have any questions, you can leave them in the comments section below, and I’ll be happy to answer every one and work through any issues with you.

### Resources And Further Reading

- [Jest documentation](https://jestjs.io/docs/en/getting-started)
- [Enzyme documentation](https://enzymejs.github.io/enzyme/docs/api/)
- “[How to Test React Components: The Complete Guide](https://www.freecodecamp.org/news/testing-react-hooks/)”, Mohammad Iqbal, freeCodeCamp
- “[Testing React With Jest and Enzyme](https://medium.com/codeclan/testing-react-with-jest-and-enzyme-20505fec4675)”, Dominic Fraser, CodeClan

{{< signature "ks, ra, il, al" >}}
