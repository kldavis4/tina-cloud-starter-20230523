---
title: 'The Rise Of The State Machines'
slug: rise-state-machines
author: krasimirtsonev
date: 2018-01-04T14:05:57+01:00
summary: >-
  The UI development became difficult in the last couple of years. That is because we pushed the state management to the browser. And managing state is what makes our job a challenge. If we do it properly, we will see how our application scales easily with no bugs. In this article, we will see how to use the state machine concept for solving state management problems.
description: >-
  It’s 2018 already, and countless front-end developers are still leading a battle against complexity and immobility. In this article, we will see how to use the state machine concept for solving state management problems.
categories:
  - UI
  - Apps
  - JavaScript
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a80d112-9454-4608-93a4-520345cb54de/turnstile-high-res-opt.jpg
---
<p>It’s 2018 already, and countless front-end developers are still leading a battle against complexity and immobility. Month after month, they've searched for the holy grail: a bug-free application architecture that will help them deliver quickly and with high quality. I am one of those developers, and I’ve found something interesting that might help.</p>

<p>We have taken a good step forward with tools such as <a href="https://facebook.github.io/react/">React</a> and <a href="https://redux.js.org/">Redux</a>. However, they’re not enough on their own in large-scale applications. This article will introduce to you the concept of state machines in the context of front-end development. You’ve probably built several of them already without realizing it.</p>

## An Introduction To State Machines

<p>A state machine is a mathematical model of computation. It’s an abstract concept whereby the machine can have different states, but at a given time fulfills only one of them. There are different types of state machines. The most famous one, I believe, is the <a href="https://en.wikipedia.org/wiki/Turing_machine">Turing machine</a>. It is an infinite state machine, which means that it can have a countless number of states. The Turing machine does not fit well in today’s UI development because in most cases we have a finite number of states. This is why finite state machines, such as <a href="https://en.wikipedia.org/wiki/Mealy_machine">Mealy</a> and <a href="https://en.wikipedia.org/wiki/Moore_machine">Moore</a>, make more sense.</p>

<p>The difference between them is that the Moore machine changes its state based only on its previous state. Unfortunately, we have a lot of external factors, such as user interactions and network processes, which means that the Moore machine is not good enough for us either. What we are looking for is the Mealy machine. It has an initial state and then transitions to new states based on input and its current state.</p>

{{% feature-panel %}}

<p>One of the easiest ways to illustrate how a state machine works is to look at a turnstile. It has a finite number of states: locked and unlocked. Here is a simple graphic that shows us these states, with their possible inputs and transitions.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a80d112-9454-4608-93a4-520345cb54de/turnstile-high-res-opt.jpg" sizes="100vw" caption="" alt="turnstile" >}}

<p>The initial state of the turnstile is locked. No matter how many times we may push it, it stays in that locked state. However, if we pass a coin to it, then it transitions to the unlocked state. Another coin at this point would do nothing; it would still be in the unlocked state. A push from the other side would work, and we’d be able to pass. This action also transitions the machine to the initial locked state.</p>

<p>If we wanted to implement a single function that controls the turnstile, we would probably end up with two arguments: the current state and an action. And if you use Redux, this probably sounds familiar to you. It is similar to the well-known <a href="https://redux.js.org/docs/basics/Reducers.html">reducer</a> function, where we receive the current state, and based on the action’s payload, we decide what will be the next state. The reducer is the transition in the context of state machines. In fact, any application that has a state that we can somehow change may be called a state machine. It’s just that we are implementing everything manually over and over again.</p>

## How Is A State Machine Better?

<p>At work, we use Redux, and I’m quite happy with it. However, I’ve started seeing patterns that I don’t like. By “don’t like,” I don’t mean that they don’t work. It is more that they add complexity and forces me to write more code. I had to undertake a side project in which I had room to experiment, and I decided to rethink our React and Redux development practices. I started making notes about the things that concerned me, and I realized that a state machine abstraction would really solve some of these problems. Let’s jump in and see how to implement a state machine in JavaScript.</p>

<p>We will attack a simple problem. We want to fetch data from a back-end API and display it to the user. The very first step is to learn how to think in states, rather than transitions. Before we get into state machines, my workflow for building such a feature used to look something like this:</p>

<ul>
<li>We display a fetch-data button.</li>
<li>The user clicks the fetch-data button.</li>
<li>Fire the request to the back end.</li>
<li>Retrieve the data and parse it.</li>
<li>Show it to the user.</li>
<li>Or, if there is an error, display the error message and show the fetch-data button so that we can trigger the process again.</li>
</ul>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7bd24b5-2d6d-47ce-8748-d28eeb2b0fcf/linear-high-res-opt.jpg" sizes="100vw" caption="" alt="linear thinking" >}}

<p>We are thinking linearly and basically trying to cover all possible directions to the final result. One step leads to another, and quickly we would start branching our code. What about problems like the user double-clicking the button, or the user clicking the button while we are waiting for back end’s response, or the request succeeding but the data being corrupted. In these cases, we would probably have various flags that show us what happened. Having flags means more <code>if</code> clauses and, in more complex apps, more conflicts.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5042df35-5be6-4d51-984e-535340891f71/linear-complex-high-res-opt.jpg" sizes="100vw" caption="" alt="linear thinking" >}}

<p>This is because we are thinking in transitions. We are focusing on how these transitions happen and in what order. Focusing instead on the application’s various states would be a lot simpler. How many states do we have, and what are their possible inputs? Using the same example:</p>

<ul>
<li><strong>idle</strong><br>
In this state, we display the fetch-data button, sit and wait. The possible action is:
<ul>
<li><strong>click</strong><br>
When the user clicks the button, we are firing the request to the back end and then transition the machine to a “fetching” state.</li>
</ul>
</li>

<li><strong>fetching</strong><br>
The request is in flight, and we sit and wait. The actions are:
<ul>
<li><strong>success</strong><br>
The data arrives successfully and is not corrupted. We use the data in some way and transition back to the “idle” state.</li>
<li><strong>failure</strong><br>
If there is an error while making the request or parsing the data, we transition to an “error” state.</li>
</ul>
</li>

<li><strong>error</strong><br>
We show an error message and display the fetch-data button. This state accepts one action:
<ul>
<li><strong>retry</strong><br>
When the user clicks the retry button, we fire the request again and transition the machine to the “fetching” state.</li>
</ul>
</li>
</ul>

<p>We’ve described roughly the same processes, but with states and inputs.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2f37efe-a89c-48fd-9176-f289aa05ccd6/sm-high-res-opt.jpg" sizes="100vw" caption="" alt="state machine" >}}

<p>This simplifies the logic and makes it more predictable. It also solves some of the problems mentioned above. Notice that, while we are in “fetching” state, we are not accepting any clicks. So, even if the user clicks the button, nothing will happen because the machine is not configured to respond to that action while in that state. This approach automatically eliminates the unpredictable branching of our code logic. This means we will have <strong>less code to cover while testing</strong>. Also, some types of testing, such as integration testing, can be automated. Think of how we would have a really clear idea of what our application does, and we could create a script that goes over the defined states and transitions and that generates assertions. These assertions could prove that we’ve reached every possible state or covered a particular journey.</p>

<p>In fact, writing down all possible states is easier than writing all possible transitions because we know which states we need or have. By the way, in most cases, the states would describe the business logic of our application, whereas transitions are very often unknown in the beginning. The bugs in our software are a result of actions dispatched in a wrong state and/or at the wrong time. They leave our app in a state that we don’t know about, and this breaks our program or makes it behave incorrectly. Of course, we don’t want to be in such a situation. <strong>State machines are good firewalls</strong>. They protect us from reaching unknown states because we set boundaries for what can happen and when, without explicitly saying how. The concept of a state machine pairs really well with a unidirectional data flow. Together, they reduce code complexity and clear the mystery of where a state has originated.</p>

## Creating A State Machine In JavaScript

<p>Enough talk &mdash; let’s see some code. We will use the same example. Based on the list above, we will start with the following:</p>

<pre><code class="language-javascript">const machine = {
  'idle': {
    click: function () { ... }
  },
  'fetching': {
    success: function () { ... },
    failure: function () { ... }
  },
  'error': {
    'retry': function () { ... }
  }
}
</code></pre>

<p>We have the states as objects and their possible inputs as functions. The initial state is missing, though. Let’s change the code above to this:</p>

<pre><code class="language-javascript">const machine = {
  state: 'idle',
  transitions: {
    'idle': {
      click: function() { ... }
    },
    'fetching': {
      success: function() { ... },
      failure: function() { ... }
    },
    'error': {
      'retry': function() { ... }
    }
  }
}
</code></pre>

<p>Once we define all of the states that make sense to us, we are ready to send the input and change state. We will do that by using the two helper methods below:</p>

<pre><code class="language-javascript">const machine = {
  dispatch(actionName, ...payload) {
    const actions = this.transitions[this.state];
    const action = this.transitions[this.state][actionName];

    if (action) {
      action.apply(machine, ...payload);
    }
  },
  changeStateTo(newState) {
    this.state = newState;
  },
  ...
}
</code></pre>

<p>The <code>dispatch</code> function checks whether there is an action with the given name in the current state’s transitions. If so, it fires it with the given payload. We are also calling the <code>action</code> handler with the <code>machine</code> as a context, so that we can dispatch other actions with <code>this.dispatch(&lt;action&gt;)</code> or change the state with <code>this.changeStateTo(&lt;new state&gt;)</code>.</p>

<p>Following the user journey of our example, the first action we have to dispatch is <code>click</code>. Here is what the handler of that action looks like:</p>

<pre><code class="language-javascript">transitions: {
  'idle': {
    click: function () {
      this.changeStateTo('fetching');
      service.getData().then(
        data =&gt; {
          try {
            this.dispatch('success', JSON.parse(data));
          } catch (error) {
            this.dispatch('failure', error)
          }
        },
        error =&gt; this.dispatch('failure', error)
      );
    }
  },
  ...
}

machine.dispatch('click');
</code></pre>

<p>We first change the state of the machine to <code>fetching</code>. Then, we trigger the request to the back end. Let’s assume we have a service with a method <code>getData</code> that returns a promise. Once it is resolved and the data parsing is OK, we dispatch <code>success</code>, if not <code>failure</code>.</p>

<p>So far, so good. Next, we have to implement <code>success</code> and <code>failure</code> actions and inputs under the <code>fetching</code> state:</p>

<pre><code class="language-javascript">transitions: {
  'idle': { ... },
  'fetching': {
    success: function (data) {
      // render the data
      this.changeStateTo('idle');
    },
    failure: function (error) {
      this.changeStateTo('error');
    }
  },
  ...
}
</code></pre>

<p>Notice how we’ve freed our brain from having to think about the previous process. We don’t care about user clicks or what is happening with the HTTP request. We know that the application is in a <code>fetching</code> state, and we are expecting just these two actions. It is a little bit like writing new logic in isolation.</p>

<p>The last bit is the <code>error</code> state. It would be nice if we provided that retry logic so that the application can recover from failure.</p>

<pre><code class="language-javascript">transitions: {
  'error': {
    retry: function () {
      this.changeStateTo('idle');
      this.dispatch('click');
    }
  }
}
</code></pre>

<p>Here we have to duplicate the logic that we wrote in the <code>click</code> handler. To avoid that, we should either define the handler as a function accessible to both actions, or we first transition to the <code>idle</code> state and then dispatch the <code>click</code> action manually.</p>

<p>A full example of the working state machine can be found in <a href="https://codepen.io/krasimir/pen/boGvKj?editors=0010">my Codepen</a>.</p>

## Managing State Machines With A Library

<p>The finite state machine pattern works regardless of whether we use React, Vue or Angular. As we saw in the previous section, we can easily implement a state machine without much trouble. However, sometimes a library provides more flexibility. Some of the good ones are <a href="https://machina-js.org/">Machina.js</a> and <a href="https://github.com/davidkpiano/xstate">XState</a>. In this article, however, we will talk about <a href="https://github.com/krasimir/stent">Stent</a>, my Redux-like library that bakes in the concept of finite state machines.</p>

<p>Stent is an implementation of a state machines container. It follows some of the ideas in the <a href="https://redux.js.org/">Redux</a> and <a href="https://redux-saga.js.org/">Redux-Saga</a> projects, but provides, in my opinion, simpler and boilerplate-free processes. It is developed using <a href="https://krasimirtsonev.com/blog/article/readme-driven-development">readme-driven development</a>, and I literally spent weeks only on the API design. Because I was writing the library, I had the chance to fix the problems that I encountered while using the Redux and Flux architectures.</p>

## Creating Machines

<p>In most cases, our applications cover multiple domains. We can’t go with just one machine. So, Stent allows for the creation of many machines:</p>

<pre><code class="language-javascript">import { Machine } from 'stent';

const machineA = Machine.create('A', {
  state: ...,
  transitions: ...
});
const machineB = Machine.create('B', {
  state: ...,
  transitions: ...
});
</code></pre>

<p>Later, we can get access to these machines using the <code>Machine.get</code> method:</p>

<pre><code class="language-javascript">const machineA = Machine.get('A');
const machineB = Machine.get('B');
</code></pre>

## Connecting The Machines To The Rendering Logic

<p>Rendering in my case is done via React, but we can use any other library. It boils down to firing a callback in which we trigger the rendering. One of the first features I worked on was the <code>connect</code> function:</p>

<pre><code class="language-javascript">import { connect } from 'stent/lib/helpers';

Machine.create('MachineA', ...);
Machine.create('MachineB', ...);

connect()
  .with('MachineA', 'MachineB')
  .map((MachineA, MachineB) =&gt; {
    ... rendering here
  });
</code></pre>

<p>We say which machines are important to us and give their names. The callback that we pass to <code>map</code> is fired once initially and then later every time the state of some of the machines changes. This is where we trigger the rendering. At this point, we have direct access to the connected machines, so we can retrieve the current state and methods. There are also <code>mapOnce</code>, for getting the callback fired only once, and <code>mapSilent</code>, to skip that initial execution.</p>

<p>For convenience, a helper is exported specifically for React integration. It is really similar to <a href="https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options">Redux’s <code>connect(mapStateToProps)</code></a>.</p>

<pre><code class="language-javascript">import React from 'react';
import { connect } from 'stent/lib/react';

class TodoList extends React.Component {
  render() {
    const { isIdle, todos } = this.props;
    ...
  }
}

// MachineA and MachineB are machines defined
// using Machine.create function
export default connect(TodoList)
  .with('MachineA', 'MachineB')
  .map((MachineA, MachineB) =&gt; {
    isIdle: MachineA.isIdle,
    todos: MachineB.state.todos
  });
</code></pre>

<p>Stent runs our mapping callback and expects to receive an object &mdash; an object that is sent as <code>props</code> to our React component.</p>

## What Is State In The Context Of Stent?

<p>Until now, our state has been simple strings. Unfortunately, in the real world, we have to keep more than a string in state. This is why Stent’s state is actually an object with properties inside. The only one reserved property is <code>name</code>. Everything else is app-specific data. For example:</p>

<pre><code class="language-javascript">{ name: 'idle' }
{ name: 'fetching', todos: [] }
{ name: 'forward', speed: 120, gear: 4 }
</code></pre>

<p>My experience with Stent so far shows me that if the state object becomes larger, we’d probably need another machine that handles those additional properties. Identifying the various states takes some time, but I believe this is a big step forward in writing more manageable applications. It is a little bit like predicting the future and drawing frames of the possible actions.</p>

## Working With The State Machine

<p>Similar to the example in the beginning, we have to define the possible (finite) states of our machine and describe the possible inputs:</p>

<pre><code class="language-javascript">import { Machine } from 'stent';

const machine = Machine.create('sprinter', {
  state: { name: 'idle' }, // initial state
  transitions: {
    'idle': {
      'run please': function () {
        return { name: 'running' };
      }
    },
    'running': {
      'stop now': function () {
        return { name: 'idle' };
      }
    }
  }
});
</code></pre>

<p>We have our initial state, <code>idle</code>, which accepts an action of <code>run</code>. Once the machine is in a <code>running</code> state, we are able to fire the <code>stop</code> action, which brings us back to the <code>idle</code> state.</p>

<p>You’ll probably remember the <code>dispatch</code> and <code>changeStateTo</code> helpers from our implementation earlier. This library provides the same logic, but it is hidden internally, and we don’t have to think about it. For convenience, based on the <code>transitions</code> property, Stent generates the following:</p>

<ul>
<li>helper methods for checking whether the machine is in a particular state &mdash; the <code>idle</code> state produces the <code>isIdle()</code> method, whereas for <code>running</code> we have <code>isRunning()</code>;</li>

<li>helper methods for dispatching actions: <code>runPlease()</code> and <code>stopNow()</code>.</li>
</ul>

<p>So, in the example above, we can use this:</p>

<pre><code class="language-javascript">machine.isIdle(); // boolean
machine.isRunning(); // boolean
machine.runPlease(); // fires action
machine.stopNow(); // fires action
</code></pre>

<p>Combining the automatically generated methods with the <code>connect</code> utility function, we are able to close the circle. A user interaction triggers the machine input and action, which updates the state. Because of that update, the mapping function passed to <code>connect</code> gets fired, and we are informed about the state change. Then, we rerender.</p>

## Input And Action Handlers

<p>Probably the most important bit is the action handlers. This is the place where we write most of the application logic because we are responding to input and changed states. Something I really like in Redux is also integrated here: the immutability and simplicity of the <a href="https://redux.js.org/docs/basics/Reducers.html">reducer function</a>. The essence of Stent’s action handler is the same. It receives the current state and action payload, and it must return the new state. If the handler returns nothing (<code>undefined</code>), then the state of the machine stays the same.</p>

<pre><code class="language-javascript">transitions: {
  'fetching': {
    'success': function (state, payload) {
      const todos = [ ...state.todos, payload ];

      return { name: 'idle', todos };
    }
  }
}
</code></pre>

<p>Let’s assume we need to fetch data from a remote server. We fire the request and transition the machine to a <code>fetching</code> state. Once the data comes from the back end, we fire a <code>success</code> action, like so:</p>

<pre><code class="language-javascript">machine.success({ label: '...' });
</code></pre>

<p>Then, we go back to an <code>idle</code> state and keep some data in the form of the <code>todos</code> array. There are a couple of other possible values to set as action handlers. The first and the simplest case is when we pass just a string that becomes the new state.</p>

<pre><code class="language-javascript">transitions: {
  'idle': {
    'run': 'running'
  }
}
</code></pre>

<p>This is a transition from <code>{ name: 'idle' }</code> to <code>{ name: 'running' }</code> using the <code>run()</code> action. This approach is useful when we have synchronous state transitions and don’t have any meta data. So, if we keep something else in state, that type of transition will flush it out. Similarly, we can pass a state object directly:</p>

<pre><code class="language-javascript">transitions: {
  'editing': {
    'delete all todos': { name: 'idle', todos: [] }
  }
}
</code></pre>

<p>We are transitioning from <code>editing</code> to <code>idle</code> using the <code>deleteAllTodos</code> action.</p>

<p>We already saw the function handler, and the last variant of the action handler is a generator function. It is inspired by the <a href="https://redux-saga.js.org/">Redux-Saga</a> project, and it looks like this:</p>

<pre><code class="language-javascript">import { call } from 'stent/lib/helpers';

Machine.create('app', {
  'idle': {
    'fetch data': function * (state, payload) {
      yield { name: 'fetching' }

      try {
        const data = yield call(requestToBackend, '/api/todos/', 'POST');

        return { name: 'idle', data };
      } catch (error) {
        return { name: 'error', error };
      }
    }
  }
});
</code></pre>

<p>If you don’t have experience with generators, this might look a bit cryptic. But the generators in JavaScript are a powerful tool. We are allowed to pause our action handler, change state multiple times and handle async logic.</p>

## Fun With Generators

<p>When I was first introduced to <a href="https://redux-saga.js.org/">Redux-Saga</a>, I thought it was an over-complicated way to handle async operations. In fact, it is a pretty smart implementation of the <a href="https://addyosmani.com/resources/essentialjsdesignpatterns/book/#commandpatternjavascript">command design pattern</a>. The main benefit of this pattern is that it separates the invocation of logic and its actual implementation.</p>

<p>In other words, we say what we want but not how it should happen. <a href="https://formidable.com/blog/category/redux-saga/">Matt Hink’s blog series</a> helped me understand how sagas are implemented, and I strongly recommend reading it. I brought the same ideas into Stent, and for the purpose of this article, we will say that by yielding stuff, we are giving instructions about what we want without actually doing it. Once the action is performed, we receive the control back.</p>

<p>At the moment, a couple of things may be sent out (yielded):</p>

<ul>
<li>a state object (or a string) for changing the state of the machine;</li>
<li>a call of the <code>call</code> helper (it accepts a synchronous function, which is a function that returns a promise or another generator function) &mdash; we are basically saying, “Run this for me, and if it is asynchronous, wait. Once you are done, give me the result.”;</li>
<li>a call of the <code>wait</code> helper (it accepts a string representing another action); if we use this utility function, we pause the handler and wait for another action to be dispatched.</li>
</ul>

<p>Here is a function that illustrates the variants:</p>

<div class="break-out">

<pre><code class="language-javascript">const fireHTTPRequest = function () {
  return new Promise((resolve, reject) =&gt; {
    // ...
  });
}

...
transitions: {
  'idle': {
    'fetch data': function * () {
      yield 'fetching'; // sets the state to { name: 'fetching' }
      yield { name: 'fetching' }; // same as above

      // wait for getTheData and checkForErrors actions
      // to be dispatched
      const [ data, isError ] = yield wait('get the data', 'check for errors');

      // wait for the promise returned by fireHTTPRequest
      // to be resolved
      const result = yield call(fireHTTPRequest, '/api/data/users');

      return { name: 'finish', users: result };
    }
  }
}
</code></pre></div>

<p>As we can see, the code looks synchronous, but in fact it is not. It is just Stent doing the boring part of waiting for the resolved promise or iterating over another generator.</p>

## How Stent Is Solving My Redux Concerns

### Too Much Boilerplate Code

<p>The Redux (and Flux) architecture relies on actions that circulate in our system. When the application grows, we usually end up having a lot of constants and action creators. These two things are very often in different folders, and tracking the code’s execution sometimes takes time. Also, when adding a new feature, we always have to deal with a whole set of actions, which means defining more action names and action creators.</p>

<p>In Stent, we don’t have action names, and the library creates the action creators automatically for us:</p>

<pre><code class="language-javascript">const machine = Machine.create('todo-app', {
  state: { name: 'idle', todos: [] },
  transitions: {
    'idle': {
      'add todo': function (state, todo) {
        ...
      }
    }
  }
});

machine.addTodo({ title: 'Fix that bug' });
</code></pre>

<p>We have the <code>machine.addTodo</code> action creator defined directly as a method of the machine. This approach also solved another problem that I faced: finding the reducer that responds to a particular action. Usually, in React components, we see action creator names such as <code>addTodo</code>; however, in the reducers, we work with a type of action that is constant. Sometimes I have to jump to the action creator code just so that I can see the exact type. Here, we have no types at all.</p>

### Unpredictable State Changes

<p>In general, Redux does a good job of managing state in an immutable fashion. The problem is not in Redux itself, but in that the developer is allowed to dispatched any action at any time. If we say that we have an action that turns the lights on, is it OK to fire that action twice in a row? If not, then how we are supposed to solve this issue with Redux? Well, we would probably put some code in the reducer that protects the logic and that check whether the lights are already turned on &mdash; maybe an <code>if</code> clause that checks the current state. Now the question is, isn’t this beyond the scope of the reducer? Should the reducer know about such edge cases?</p>

<p>What I’m missing in Redux is a way to stop the dispatching of an action based on the application’s current state without polluting the reducer with conditional logic. And I don’t want to take this decision to the view layer either, where the action creator is fired. With Stent, this happens automatically because the machine does not respond to actions that are not declared in the current state. For example:</p>

<pre><code class="language-javascript">const machine = Machine.create('app', {
  state: { name: 'idle' },
  transitions: {
    'idle': {
      'run': 'running',
      'jump': 'jumping'
    },
    'running': {
      'stop': 'idle'
    }
  }
});

// this is fine
machine.run();

// This will do nothing because at this point
// the machine is in a 'running' state and there is
// only 'stop' action there.
machine.jump();
</code></pre>

<p>The fact that the machine accepts only specific inputs at a given time protects us from weird bugs and makes our applications more predictable.</p>

### States, Not Transitions

<p>Redux, like Flux, makes us think in terms of transitions. The mental model of developing with Redux is pretty much driven by actions and how these actions transform the state in our reducers. That is not bad, but I’ve found it makes more sense to think in terms of states instead &mdash; what states the app might be in and how these states represent the business requirements.</p>

## Conclusion

<p>The concept of state machines in programming, especially in UI development, was eye-opening for me. I started seeing state machines everywhere, and I have some desire to always shift to that paradigm. I definitely see the <strong>benefits of having more strictly defined states</strong> and transitions between them. I’m always searching for ways to make my apps simple and readable. I believe that state machines are a step in this direction. The concept is simple and at the same time powerful. It has the potential to eliminate a lot of bugs.</p>

{{< signature "rb, ra, al, il" >}}

