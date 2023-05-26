---
title: 'Supercharge Testing React Applications With Wallaby.js'
slug: supercharge-testing-react-applications-wallabyjs
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4909c34-5b96-4a0f-9d08-8f3114dbe99f/wallabyjs-001.png
date: 2020-10-16T09:30:00.000Z
summary: >-
  Ever had to switch your focus from your editor and to your terminal to see the results of your tests? This article will introduce you to Wallaby.js &mdash; a JavaScript productivity tool that supercharges your IDE by allowing you to get real-time feedback on your JavaScript tests in your code editor even before saving the file. You will also learn how to use Wallaby.js for testing React applications.<br /><br /><strong>Note</strong>: In order to be able to follow along, you’ll need to be familiar with JavaScript testing and have a working knowledge of building React applications.
description: >-
  Ever had to switch your focus from your editor and to your terminal to see the results of your tests? This article will introduce you to Wallaby.js &mdash; a JavaScript productivity tool that supercharges your IDE by allowing you to get real-time feedback on your JavaScript tests in your code editor even before saving the file. You will also learn how to use Wallaby.js for testing React applications.
categories:
  - Tools
  - JavaScript
  - React
  - Testing
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Wallaby
  link: https://wallabyjs.com/?referrer=smashing
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02973189-fbd0-4655-89e7-332f9e3e33dc/wallaby-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://wallabyjs.com/?referrer=smashing">Wallaby</a> who create awesome developer tools that push the boundaries of what is technically possible and in doing so make software developers more efficient, more effective, and happier. <em>Thank you!</em>
---

One thing you will discover very quickly when you start writing tests for an application is that you want to run your tests constantly when you are coding. Having to switch between your code editor and terminal window (or in the case of VS Code, the integrated terminal) adds an overhead and reduces your productivity as you build your application. In an ideal world, you would have instant feedback on your tests right in your editor as you are writing your code. Enter Wallaby.js.

## What Is Wallaby.js?

Wallaby.js is an intelligent test runner for JavaScript that continuously runs your tests. It reports code coverage and other results directly to your code editor immediately as you change your code (even without saving the file). The tool is available as an editor extension for VS Code, IntelliJ Editors (such as WebStorm and IntelliJ IDEA), Atom, Sublime Text, and Visual Studio.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eec07a1-a269-4177-8571-1605eae279e2/wallabyjs-000.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eec07a1-a269-4177-8571-1605eae279e2/wallabyjs-000.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eec07a1-a269-4177-8571-1605eae279e2/wallabyjs-000.png'>Large preview</a>)" alt="A screenshot of Wallaby.js, an intelligent test runner for JavaScript that continuously runs your tests" >}}

## Why Wallaby.js?

As stated earlier, Wallaby.js aims to improve your productivity in your day to day JavaScript development. Depending on your development workflow, Wallaby can save you hours of time each
week by reducing context switching. Wallaby also provides code coverage reporting, error reporting, and other time-saving features such as time-travel debugging and test stories.

## Getting Started With Wallaby.js In VS Code

Let’s see how we can get the benefits of Wallaby.js using VS Code.

Note: If you are not using VS Code you can check out [here](https://wallabyjs.com/docs/intro/install.html?referrer=smashing) for instructions on how to set up for other editors.

### Install The Wallaby.js VS Code Extension

To get started we will install the [Wallaby.js VS Code extension](https://marketplace.visualstudio.com/items?itemName=WallabyJs.wallaby-vscode).

After the extension is installed, the Wallaby.js core runtime will be automatically downloaded and installed.

### Wallaby License

Wallaby provides an Open Source license for open source projects seeking to use Wallaby.js. Visit [here](https://wallabyjs.com/oss/?referrer=smashing) to obtain an open-source license. You may use the open-source license with the [demo repo for this article](https://github.com/DominusKelvin/wallaby-js-demo).

You can also get a fully functional 15-day trial license by visiting [here](https://wallabyjs.com/download/#try-it-free?referrer=smashing).

If you want to use Wallaby.js on a non-open-source project beyond the 15-day trial license period, you may obtain a license key from the [wallaby website](https://wallabyjs.com/purchase/?referrer=smashing).

### Add License Key To VS Code

After obtaining a license key, head over to VS Code and in the command palette search for "Wallaby.js: Manage License Key", click on the command and you will be presented with an input box to enter your license key, then hit enter and you will receive a notification that Wallaby.js has been successfully activated.

## Wallaby.js And React

Now that we have Wallaby.js set up in our VS Code editor, let’s supercharge testing a React application with Wallaby.js.

For our React app, we will add a simple upvote/downvote feature and we will write some tests for our new feature to see how Wallaby.js plays out in the mix.

### Creating The React App

**Note**: *You can [clone the demo repo](https://github.com/DominusKelvin/wallaby-js-demo) if you like, or you can follow along below.*

We will create our React app using the create-react-app CLI tool.

<pre><code class="language-bash">npx create-react-app wallaby-js-demo
</code></pre>

Then open the newly scaffolded React project in VS Code.

Open `src/App.js` and start Wallaby.js by running: "Wallaby.js: Start" in VS Code command palette (alternatively you can use the shortcut combo &mdash; <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd> <kbd>R</kbd> if you are on a Windows or Linux machine, or <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd> <kbd>R</kbd> if you are on a Mac).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4909c34-5b96-4a0f-9d08-8f3114dbe99f/wallabyjs-001.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4909c34-5b96-4a0f-9d08-8f3114dbe99f/wallabyjs-001.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4909c34-5b96-4a0f-9d08-8f3114dbe99f/wallabyjs-001.png'>Large preview</a>)" alt="A screenshot of create the React app by using the create-react-app CLI tool" >}}

When Wallaby.js starts you should see its test coverage indicators to the left of your editor similar to the screenshot below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e77624f-211a-407c-baac-32a91f8704df/wallabyjs-002.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e77624f-211a-407c-baac-32a91f8704df/wallabyjs-002.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e77624f-211a-407c-baac-32a91f8704df/wallabyjs-002.png'>Large preview</a>)" alt="A screenshot of the App.js file showing test coverage indicators when starting Wallaby.js" >}}

Wallaby.js provides *5* different colored indicators in the left margin of your code editor:

1. Gray: means that the line of code is not executed by any of your tests.
2. Yellow: means that some of the code on a given line was executed but other parts were not.
3. Green: means that all of the code on a line was executed by your tests.
4. Pink: means that the line of code is on the execution path of a failing test.
5. Red: means that the line of code is the source of an error or failed expectation, or in the stack of an error.

If you look at the status bar you will see Wallaby.js metrics for this file and it’s showing we have a 100% test coverage for `src/App.js` and a single passing test with no failing test. How does Wallaby.js know this? When we started Wallaby.js, it detected `src/App.js` has a test file `src/App.test.js`, it then runs those tests in the background for us and conveniently gives us the feedbacks using its color indicators and also giving us a summary metric on our tests in the status bar.

When you also open `src/App.test.js` you will see similar feedback from Wallaby.js

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc8cbe14-2339-4755-88e0-9fc091304870/wallabyjs-003.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc8cbe14-2339-4755-88e0-9fc091304870/wallabyjs-003.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc8cbe14-2339-4755-88e0-9fc091304870/wallabyjs-003.png'>Large preview</a>)" alt="A screenshot of the code inside the App.test.js file" >}}

Currently, all tests are passing at the moment so we get all green indicators. Let’s see how Wallaby.js handles failing tests. In `src/App.test.js` let’s make the test fail by changing the expectation of the test like so:

<pre><code class="language-javascript">// src/App.test.js
expect(linkElement).not.toBeInTheDocument();
</code></pre>

The screenshot below shows how your editor would now look with `src/App.test.js` open:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a74840-6cad-490f-ac73-1e21faaaf50a/wallabyjs-004.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a74840-6cad-490f-ac73-1e21faaaf50a/wallabyjs-004.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a74840-6cad-490f-ac73-1e21faaaf50a/wallabyjs-004.png'>Large preview</a>)" alt="A screenshot of the App.test.js file opened in a editor showing failing tests" >}}

You will see the indicators change to red and pink for the failing tests. Also notice we didn’t have to save the file for Wallaby.js to detect we made a change.

You will also notice the line in your editor in `src/App.test.js` that outputs the error of the test. This is done thanks to Wallaby.js [advanced logging](https://wallabyjs.com/docs/intro/advanced-logging.html?referrer=smashing). Using Wallaby.js advanced logging, you can also report and explore runtime values beside your code using `console.log`, a special comment format `//?` and the VS Code command, `Wallaby.js: Show Value`.

Now let’s see the Wallaby.js workflow for fixing failing tests. Click on the Wallaby.js test indicator in the status bar to open the Wallaby.js output window. ("✗ 1 ✓ 0")

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2678efa8-5330-4f5b-9e6b-cb0759a2d590/wallabyjs-005.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2678efa8-5330-4f5b-9e6b-cb0759a2d590/wallabyjs-005.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2678efa8-5330-4f5b-9e6b-cb0759a2d590/wallabyjs-005.png'>Large preview</a>)" alt="A screenshot of the App.test.js file open in an editor with the Wallaby.js Tests indicator tab open" >}}

In the Wallaby.js output window, right next to the failing test, you should see a “Debug Test” link. Pressing <kbd>Ctrl</kbd> and clicking on that link will fire up the Wallaby.js [time travel debugger](https://wallabyjs.com/docs/intro/time-travel-debugger.html?referrer=smashing). When we do that, the Wallaby.js Tools window will open to the side of your editor, and you should see the Wallaby.js debugger section as well as the Value explorer and Test file coverage sections.

If you want to see the runtime value of a variable or expression, select the value in your editor and Wallaby.js will display it for you.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e28034-145e-43c2-a238-608deff5596d/wallabyjs-006.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e28034-145e-43c2-a238-608deff5596d/wallabyjs-006.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e28034-145e-43c2-a238-608deff5596d/wallabyjs-006.png'>Large preview</a>)" alt="A screenshot of the App.test.js file opened in an editor showing the runtime value selected" >}}

Also, notice the "Open Test Story" link in the output window. Wallby.js test story allows you to see all your tests and the code they are testing in a single view in your editor.

Let’s see this in action. Press <kbd>Ctrl</kbd> and click on the link &mdash; you should be able to see the Wallaby.js test story open up in your editor. Wallaby’s Test Story Viewer provides a unique and efficient way of inspecting what code your test is executing in a single logical view.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3724c16e-93aa-4579-a1f5-b01357ec38ea/wallabyjs-007.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3724c16e-93aa-4579-a1f5-b01357ec38ea/wallabyjs-007.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3724c16e-93aa-4579-a1f5-b01357ec38ea/wallabyjs-007.png'>Large preview</a>)" alt="A screenshot of what can be seen in the Test Story tab" >}}

Another thing we will explore before fixing our failing test is the Wallaby.js app. Notice the link in the Wallaby.js output window: “Launch Coverage & Test Explorer”. Clicking on the link will launch the Wallaby.js app which will give you a compact birds-eye view of all tests in your project.

Next, click on the link and start up the Wallaby.js app in your default browser via `https://localhost:51245/`. Wallaby.js will quickly detect that we have our demo project open in our editor which will then automatically load it into the app.

Here is how the app should now look like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31506bf1-62ae-4f1b-98b1-b5912d64205c/wallabyjs-008.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31506bf1-62ae-4f1b-98b1-b5912d64205c/wallabyjs-008.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31506bf1-62ae-4f1b-98b1-b5912d64205c/wallabyjs-008.png'>Large preview</a>)" alt="A screenshot of the Wallaby.js demo app project previewed in the browser" >}}

You should be able to see the test’s metrics on the top part of the Wallaby.js app. By default, the **Tests** tab in the app is opened up. By clicking on the **Files** tab, you should be able to see the files in your project as well as their test coverage reports.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff072460-5a6c-4a3e-a4e0-29e652ad888f/wallabyjs-009.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff072460-5a6c-4a3e-a4e0-29e652ad888f/wallabyjs-009.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff072460-5a6c-4a3e-a4e0-29e652ad888f/wallabyjs-009.png'>Large preview</a>)" alt="A screenshot of a browser tab showing the demo preview of the Wallaby.js app and where the Files tab can be found" >}}

Back on to the **Tests** tab, click on the test and you should see the Wallaby.js error reporting feature to the right:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53c91ff5-9cdb-4d65-9412-2a553dc4c448/wallabyjs-010.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53c91ff5-9cdb-4d65-9412-2a553dc4c448/wallabyjs-010.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53c91ff5-9cdb-4d65-9412-2a553dc4c448/wallabyjs-010.png'>Large preview</a>)" alt="A screenshot showing how the app reports errors" >}}

Now we’ve covered all that, go back to the editor, and fix the failing test to make Wallaby.js happy by reverting the line we changed earlier to this:

<pre><code class="language-javascript">expect(linkElement).toBeInTheDocument();
</code></pre>

The Wallaby.js output window should now look like the screenshot below and your test coverage indicators should be all passing now.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cfb0528-f582-4109-8547-347c6f8da918/wallabyjs-011.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cfb0528-f582-4109-8547-347c6f8da918/wallabyjs-011.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cfb0528-f582-4109-8547-347c6f8da918/wallabyjs-011.png'>Large preview</a>)" alt="A screenshot of the App.test.js file opened in an editor showing all tests passed in the Output tab" >}}

## Implementing Our Feature

We’ve explored Wallaby.js in the default app created for us by `create-react-app`. Let’s implement our upvote/downvote feature and write tests for that. 

Our application UI should contain two buttons one for upvoting and the other for downvoting and a single counter that will be incremented or decremented depending on the button the user clicks. Let’s modify `src/App.js` to look like this.

<pre><code class="language-javascript">// src/App.js
import React, { useState } from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  const [vote, setVote] = useState(0);

  function upVote() {
    setVote(vote + 1);
  }

  function downVote() {
    // Note the error, we will fix this later...
    setVote(vote - 2);
  }
  return (
    &lt;div className='App'&gt;
      &lt;header className='App-header'&gt;
        &lt;img src={logo} className='App-logo' alt='logo' /&gt;
        &lt;p className='vote' title='vote count'&gt;
          {vote}
        &lt;/p&gt;
        &lt;section className='votes'&gt;
          &lt;button title='upVote' onClick={upVote}&gt;
            &lt;span role='img' aria-label='Up vote'&gt;
              👍🏿
            &lt;/span&gt;
          &lt;/button&gt;
          &lt;button title='downVote' onClick={downVote}&gt;
            &lt;span role='img' aria-label='Down vote'&gt;
              👎🏿
            &lt;/span&gt;
          &lt;/button&gt;
        &lt;/section&gt;
      &lt;/header&gt;
    &lt;/div&gt;
  );
}

export default App;
</code></pre>

We will also style the UI just a bit. Add the following rules to `src/index.css`

<pre><code class="language-css">.votes {
  display: flex;
  justify-content: space-between;
}
p.vote {
  font-size: 4rem;
}
button {
  padding: 2rem 2rem;
  font-size: 2rem;
  border: 1px solid #fff;
  margin-left: 1rem;
  border-radius: 100%;
  transition: all 300ms;
  cursor: pointer;
}

button:focus,
button:hover {
  outline: none;
  filter: brightness(40%);
}
</code></pre>

If you look at `src/App.js`, you will notice some gray indicators from Wallaby.js hinting us that some part of our code isn’t tested yet. Also, you will notice our initial test in `src/App.test.js` is failing and the Wallaby.js status bar indicator shows that our test coverage has dropped.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cbda23f-f1f8-40d2-870a-953270f97a10/wallabyjs-012.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cbda23f-f1f8-40d2-870a-953270f97a10/wallabyjs-012.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cbda23f-f1f8-40d2-870a-953270f97a10/wallabyjs-012.png'>Large preview</a>)" alt="A screenshot of how the initital test is shown to have failed inside the App.test.js file" >}}

These visual clues by Wallaby.js are convenient for test-driven development (TDD) since we get instant feedback on the state of our application regarding tests.

### Testing Our App Code

Let’s modify `src/App.test.js` to check that the app renders correctly.

**Note**: *We will be using React Testing Library for our test which comes out of the box when you run `create-react-app`. See the [docs](https://testing-library.com/docs/react-testing-library/intro) for usage guide.*

We are going to need a couple of extra functions from `@testing-library/react`, update your `@testing-library/react` import to:

<pre><code class="language-javascript">import { render, fireEvent, cleanup } from '@testing-library/react';
</code></pre>

Then let’s replace the single test in `src/App.js` with:

<pre><code class="language-javascript">test('App renders correctly', () =&gt; { render(&lt;App /&gt;); });
</code></pre>

Immediately you will see the indicator go green in both the `src/App.test.js` line where we test for the render of the app and also where we are calling render in our `src/App.js`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3bc0f9-b4ec-4aca-bc32-f272b055e6be/wallabyjs-013.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3bc0f9-b4ec-4aca-bc32-f272b055e6be/wallabyjs-013.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3bc0f9-b4ec-4aca-bc32-f272b055e6be/wallabyjs-013.png'>Large preview</a>)" alt="A screenshot of the App.test.js file opened in an editor showing green indicators" >}}

Next, we will test that the initial value of the `vote` state is zero(0).

<pre><code class="language-javascript">it('Vote count starts at 0', () =&gt; {
  const { getByTitle } = render(&lt;App /&gt;);
  const voteElement = getByTitle('vote count');
  expect(voteElement).toHaveTextContent(/^0$/);
});
</code></pre>

Next, we will test if clicking the upvote 👍🏿 button increments the vote:

<pre><code class="language-javascript">it('Vote increments by 1 when upVote button is pressed', () =&gt; {
  const { getByTitle } = render(&lt;App /&gt;);
  const upVoteButtonElement = getByTitle('upVote');
  const voteElement = getByTitle('vote count');
  fireEvent.click(upVoteButtonElement);
  expect(voteElement).toHaveTextContent(/^1$/);
});
</code></pre>

We will also test for the downvote 👎🏿 interaction like so:

<pre><code class="language-javascript">it('Vote decrements by 1 when downVote button is pressed', () =&gt; {
  const { getByTitle } = render(&lt;App /&gt;);
  const downVoteButtonElement = getByTitle('downVote');
  const voteElement = getByTitle('vote count');
  fireEvent.click(downVoteButtonElement);
  expect(voteElement).toHaveTextContent(/^-1$/);
});
</code></pre>

Oops, this test is failing. Let’s work out why. Above the test, click the `View story` code lens link or the `Debug Test` link in the Wallaby.js output window and use the debugger to step through to the `downVote` function. We have a bug... we should have decremented the vote count by 1 but instead, we are decrementing by 2. Let’s fix our bug and decrement by 1.

<pre><code class="language-javascript">src/App.js
function downVote() {
    setVote(vote - 1);
}
</code></pre>

Watch now how Wallaby’s indicators go green and we know that all of our tests are passing:

{{< vimeo id="468309610" caption="" breakout="true" >}}

Our `src/App.test.js` should look like this:

<pre><code class="language-javascript">import React from 'react';
import { render, fireEvent, cleanup } from '@testing-library/react';
import App from './App';

test('App renders correctly', () =&gt; {
  render(&lt;App /&gt;);
});

it('Vote count starts at 0', () =&gt; {
  const { getByTitle } = render(&lt;App /&gt;);
  const voteElement = getByTitle('vote count');
  expect(voteElement).toHaveTextContent(/^0$/);
});

it('Vote count increments by 1 when upVote button is pressed', () =&gt; {
  const { getByTitle } = render(&lt;App /&gt;);
  const upVoteButtonElement = getByTitle('upVote');
  const voteElement = getByTitle('vote count');
  fireEvent.click(upVoteButtonElement);
  expect(voteElement).toHaveTextContent(/^1$/);
});

it('Vote count decrements by 1 when downVote button is pressed', () =&gt; {
  const { getByTitle } = render(&lt;App /&gt;);
  const downVoteButtonElement = getByTitle('downVote');
  const voteElement = getByTitle('vote count');
  fireEvent.click(downVoteButtonElement);
  expect(voteElement).toHaveTextContent(/^-1$/);
});

afterEach(cleanup);
</code></pre>

After writing these tests, Wallaby.js shows us that the missing code paths that we initially identified before writing any tests have now been executed. We can also see that our coverage has increased. Again, you will notice how writing your tests with instant feedback from Wallaby.js allows you to see what’s going on with your tests right in your browser, which in turn improves your productivity.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb122b81-3f7d-4e4f-9401-60f962dc7d2d/wallabyjs-015.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb122b81-3f7d-4e4f-9401-60f962dc7d2d/wallabyjs-015.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb122b81-3f7d-4e4f-9401-60f962dc7d2d/wallabyjs-015.png'>Large preview</a>)" alt="Final outcome of the Wallaby.js demo opened in a browser tab" >}}

## Conclusion

From this article, you have seen how Wallaby.js improves your developer experience when testing JavaScript applications. We have investigated some key features of Wallaby.js, set it up in VS Code, and then tested a React application with Wallaby.js.

### Further Resources

- [VS Code Tutorial](https://wallabyjs.com/docs/intro/get-started-vscode.html?referrer=smashing), Wallaby.js
- *The demo app for this project can be found on [GitHub](https://github.com/DominusKelvin/wallaby-js-demo).*

{{< signature "ra, il" >}}
