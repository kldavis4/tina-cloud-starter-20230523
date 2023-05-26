---
title: 'Get Started With React By Building A Whac-A-Mole Game'
slug: get-started-whac-a-mole-react-game
author: jhey-tompkins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a9db037-1a8d-42ad-b0c3-1c885e456693/get-started-whac-a-mole-react-game.jpg
date: 2021-05-10T11:00:00.000Z
summary: >-
  Want to get started with React but struggling to find a good place to start? This article should have you covered. We’ll focus on some of the main concepts of React and then we’ll be building a game from scratch! We assume that you have a working knowledge of JavaScript. Ah, and if you’re here for the game, you can <a href="#whac-a-mole-game">get started right away</a>.
description: >-
  Want to get started with React but struggling to find a good place to start? This article should have you covered. We’ll focus on some of the main concepts of React and then we’ll be building a game from scratch!
categories:
  - React
  - Tutorials
---

I’ve been working with React since &#126;v0.12 was released. (2014! Wow, where did the time go?) It’s changed a lot. I recall certain “Aha” moments along the way. One thing that’s remained is the mindset for using it. We think about things in a different way as opposed to working with the DOM direct.

For me, my learning style is to get something up and running as fast as I can. Then I explore deeper areas of the docs and everything included whenever necessary. **Learn by doing, having fun, and pushing things!**

## Aim

The aim here is to show you enough React to cover some of those "Aha" moments. Leaving you curious enough to dig into things yourself and create your own apps.
I recommend [checking out the docs](https://reactjs.org/docs/hello-world.html) for anything you want to dig into. I won’t be duplicating them.

*Please note that you can find all examples in [CodePen](https://codepen.io), but you can also jump to [my Github repo](https://github.com/jh3y/whac-a-mole-react) for a fully working game.*

## First App

You can bootstrap a React app in various ways. Below is an example:

<pre><code class="language-javascript">import React from 'https://cdn.skypack.dev/react'
import { render } from 'https://cdn.skypack.dev/react-dom'

const App = () =&gt; &lt;h1&gt;{`Time: ${Date.now()}`}&lt;/h1&gt;

render(&lt;App/&gt;, document.getElementById('app')
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="xxqGYWg" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Your First React App](https://codepen.io/smashingmag/pen/xxqGYWg) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

This is pretty much all you need to create your first React app (besides the HTML) to get started. But, we could make this smaller, like so:

<pre><code class="language-javascript">render(&lt;h1&gt;{`Time: ${Date.now()}`}&lt;/h1&gt;, document.getElementById('app'))
</code></pre>

In the first version, `App` is a component, but this example tells React DOM to **render an element instead of a component**. Elements are the HTML elements we see in both examples. What makes a component, is a function returning those elements

 Before we get started with components, what’s the deal with this "HTML in JS"?

{{% feature-panel %}}

## JSX

That "HTML in JS" is JSX. You can read all about [JSX in the React documentation](https://reactjs.org/docs/introducing-jsx.html). The gist? A syntax extension to JavaScript that allows us to write HTML in JavaScript. It’s like a templating language with full access to JavaScript powers. It’s actually an abstraction on an underlying API. Why do we use it? For most, it’s easier to follow and comprehend than the equal.

<pre><code class="language-javascript">React.createElement('h1', null, `Time: ${Date.now()}`)</code></pre>

The thing to take on board with JSX is that this is how you put things in the DOM 99% of the time with React. And it’s also how we bind event handling a lot of the time. That other 1% is a little out of scope for this article. But, sometimes we want to render elements outside the realms of our React application. We can do this using React DOM’s Portal. We can also get direct access to the DOM within the component lifecycle (coming up).

Attributes in JSX are camelCase. For example, `onclick` becomes `onClick`. There are [some special cases](https://reactjs.org/docs/dom-elements.html#differences-in-attributes) such as `class` which becomes `className`. Also, attributes such as `style` now accept an `Object` instead of a `string`.

<pre><code class="language-javascript">&lt;div className="awesome-class" style={{ color: 'red' }}&gt;Cool&lt;/div&gt;
</code></pre>

**Note**: *You can check out all the differences in attributes [here](https://reactjs.org/docs/dom-elements.html#differences-in-attributes).*

## Rendering

How do we get our JSX into the DOM? We need to inject it. In most cases, our apps have a single point of entry. And if we are using React, we use React DOM to insert an element/component at that point. You could use JSX without React though. As we mentioned, it’s a **syntax extension**. You could change how JSX gets interpreted by Babel and [have it pump out something different](https://blog.r0b.io/post/using-jsx-without-react/).

Everything within becomes managed by React. This can yield certain performance benefits when we are modifying the DOM a lot. This is because React makes use of a Virtual DOM. Making DOM updates isn’t slow by any means. But, it’s the impact it has within the browser that can impact performance. Each time we update the DOM, browsers need to calculate the **rendering changes** that need to take place. That can be expensive. Using the Virtual DOM, these DOM updates get kept in memory and synced with the browser DOM in batches when required.

There’s nothing to stop us from having many apps on a page or having only part of a page managed by React.

{{< codepen height="480" theme_id="light" slug_hash="QWpbmWw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Two Apps](https://codepen.io/smashingmag/pen/QWpbmWw) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

Take this example. The same app is rendered twice between some regular HTML. Our React app renders the current time using `Date.now`.

<pre><code class="language-javascript">const App = () =&gt; &lt;h1&gt;{`Time: ${Date.now()}`}&lt;/h1&gt;
</code></pre>

For this example, we’re rendering the app twice between some regular HTML. We should see the title "Many React Apps" followed by some text, then the first rendering of our app appears followed by some text, and then the second rendering of our app.

*For a deeper dive into rendering, check out [the docs](https://reactjs.org/docs/rendering-elements.html).*

## Components && Props

This is one of the biggest parts of React to grok. Components are reusable blocks of UI. But underneath, it’s all functions. Components are functions whose arguments we refer to as `props`. And we can use those "props" to determine what a component should render. Props are "read-only" and you can pass anything in a prop. Even other components. Anything within the tags of a component we access via a special prop, `children`.

Components are functions that return elements. If we don’t want to show anything, return `null`.

We can write components in a variety of ways. But, it’s all the same result.

Use a function:

<pre><code class="language-javascript">function App() {
  return &lt;h1&gt;{`Time: ${Date.now()}`}&lt;/h1&gt;
}
</code></pre>

Use a class:

<pre><code class="language-javascript">class App extends React.Component {
  render() {
    return &lt;h1&gt;{`Time: ${Date.now()}`}&lt;/h1&gt;
  }
}
</code></pre>

Before the release of hooks(coming up), we used class-based components a lot. We needed them for state and accessing the component API. But, with hooks, the use of class-based components has petered out a bit. In general, we always opt for **function-based components** now. This has various benefits. For one, it requires less code to achieve the same result. Hooks also make it easier to share and reuse logic between components. Also, classes can be confusing. They need the developer to have an understanding of bindings and context.

We’ll be using function-based and you’ll notice we used a different style for our `App` component.

<pre><code class="language-javascript">const App = () =&gt; &lt;h1&gt;{`Time: ${Date.now()}`}&lt;/h1&gt;
</code></pre>

That’s valid. The main thing is that our component returns what we want to render. In this case, a single element that is a `h1` displaying the current time. If we don’t need to write `return`, etc. then don’t. But, it’s all preference. And different projects may adopt different styles.

What if we updated our multi-app example to accept `props` and we extract the `h1` as a component?

<div class="break-out">

 <pre><code class="language-javascript">const Message = ({ message }) =&gt; &lt;h1&gt;{message}&lt;/h1&gt;
const App = ({ message }) =&gt; &lt;Message message={message} /&gt;
render(&lt;App message={`Time: ${Date.now()}`}/&gt;, document.getElementById('app'))
</code></pre>
</div>

{{< codepen height="480" theme_id="light" slug_hash="rNyVJKe" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Our First Component Extraction](https://codepen.io/smashingmag/pen/rNyVJKe) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

That works and now we can change the `message` prop on `App` and we’d get different messages rendered. We could’ve made the component `Time`. But, creating a `Message` component implies many opportunities to reuse our component. This is the biggest thing about React. It’s about making decisions around architecture/design.

What if we forget to pass the prop to our component? We could provide a default value. Some ways we could do that.

<div class="break-out">

 <pre><code class="language-javascript">const Message = ({message = "You forgot me!"}) =&gt; &lt;h1&gt;{message}&lt;/h1&gt;
</code></pre>
</div>

Or by specifying `defaultProps` on our component. We can also provide [propTypes](https://reactjs.org/docs/typechecking-with-proptypes.html) which is something I’d recommend having a look at. It provides a way to type check props on our components.

<pre><code class="language-javascript">Message.defaultProps = {
  message: "You forgot me!"
}
</code></pre>

We can access props in different ways. We’ve used ES6 conveniences to destructure props. But, our `Message` component could also look like this and work the same.

<pre><code class="language-javascript">const Message = (props) =&gt; &lt;h1&gt;{props.message}&lt;/h1&gt;
</code></pre>

Props are an object passed to the component. We can read them any way we like.

Our `App` component could even be this:

<pre><code class="language-javascript">const App = (props) =&gt; &lt;Message {...props}/&gt;
</code></pre>

It would yield the same result. We refer to this as "Prop spreading". It’s better to be explicit with what we pass through though.

We could also pass the `message` as a child.

<pre><code class="language-javascript">const Message = ({ children }) =&gt; &lt;h1&gt;{children}&lt;/h1&gt;
const App = ({ message }) =&gt; &lt;Message&gt;{message}&lt;/Message&gt;
</code></pre>

Then we refer to the message via the special `children` prop.

How about taking it further and doing something like have our `App` pass a `message` to a component that is also a prop.

<pre><code class="language-javascript">const Time = ({ children }) =&gt; &lt;h1&gt;{`Time: ${children}`}&lt;/h1&gt;

const App = ({ message, messageRenderer: Renderer }) =&gt; &lt;Renderer&gt;{message}&lt;/Renderer&gt;

render(&lt;App message={`${Date.now()}`} messageRenderer={Time} /&gt;, document.getElementById('app'))
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="xxqGYJq" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Passing Components as Props](https://codepen.io/smashingmag/pen/xxqGYJq) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

In this example, we create two apps and one renders the time and another a message. Note how we rename the `messageRenderer` prop to `Renderer` in the destructure? React won’t see anything starting with a lowercase letter as a component. That’s because anything starting in lowercase is seen as an element. It would render it as `<messageRenderer>`. We’ll rarely use this pattern but it’s a way to show how anything can be a prop and you can do what you want with it.

One thing to make clear is that anything passed as a prop needs processing by the component. For example, want to pass styles to a component, you need to read them and apply them to whatever is being rendered.

Don’t be afraid to experiment with different things. Try different patterns and practice. The skill of determining what should be a component comes through practice. In some cases, it’s obvious, and in others, you might realize it later and refactor.

A common example would be the layout for an application. Think at a high level what that might look like. A layout with children that comprises of a header, footer, some main content. How might that look? It could look like this.

<pre><code class="language-javascript">const Layout = ({ children }) =&gt; (
  &lt;div className="layout"&gt;
    &lt;Header/&gt;
    &lt;main&gt;{children}&lt;/main&gt;
    &lt;Footer/&gt;
  &lt;/div&gt;
)
</code></pre>

It’s all about building blocks. Think of it like LEGO for apps.

In fact, one thing I’d advocate is getting familiar with [Storybook](https://storybook.js.org) as soon as possible (I’ll create content on this if people would like to see it). Component-driven development isn’t unique to React, we see it in other frameworks too. Shifting your mindset to think this way will help a lot.

{{% ad-panel-leaderboard %}}

## Making Changes

Up until now, we’ve only dealt with static rendering. Nothing changes. The biggest thing to take on board for learning React is how React works. We need to understand that components can have state. And we must understand and respect that state drives everything. Our elements react to state changes. And React will only re-render where necessary.

Data flow is unidirectional too. Like a waterfall, state changes flow down the UI hierarchy. Components don’t care about where the data comes from. For example, a component may want to pass state to a child through props. And that change may trigger an update to the child component. Or, components may choose to manage their own internal state which isn’t shared. 

These are all design decisions that get easier the more you work with React. The main thing to remember is how unidirectional this flow is. To trigger changes higher up, it either needs to happen via events or some other means passed by props.

Let’s create an example.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useEffect, useRef, useState } from 'https://cdn.skypack.dev/react'
import { render } from 'https://cdn.skypack.dev/react-dom'

const Time = () =&gt; {
  const [time, setTime] = useState(Date.now())
  const timer = useRef(null)
  useEffect(() =&gt; {
    timer.current = setInterval(() =&gt; setTime(Date.now()), 1000)
    return () =&gt; clearInterval(timer.current)
  }, [])
  return &lt;h1&gt;{`Time: ${time}`}&lt;/h1&gt;
}

const App = () =&gt; &lt;Time/&gt;

render(&lt;App/&gt;, document.getElementById('app'))
</code></pre>
</div>

{{< codepen height="480" theme_id="light" slug_hash="MWpwQqa" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [An Updating Timer](https://codepen.io/smashingmag/pen/MWpwQqa) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

There is a fair bit to digest there. But, here we introduce the use of "Hooks". We are using "useEffect", "useRef", and "useState". These are utility functions that give us access to the component API.

If you check the example, the time is updating every second or `1000ms`. And that’s driven by the fact we update the `time` which is a piece of state. We are doing this within a `setInterval`. Note how we don’t change `time` directly. State variables are treated as immutable. We do it through the `setTime` method we receive from invoking `useState`. Every time the state updates, our component re-renders if that state is part of the render. `useState` always returns a state variable and a way to update that piece of state. The argument passed is the initial value for that piece of state.

We use `useEffect` to hook into the component lifecycle for events such as state changes. Components mount when they’re inserted into the DOM. And they get unmounted when they’re removed from the DOM. To hook into these lifecycle stages, we use effects. And we can return a function within that effect that will fire when the component gets unmounted. The second parameter of `useEffect` determines when the effect should run. We refer to it as the dependency array. Any listed items that change will trigger the effect to run. No second parameter means the effect will run on every render. And an empty array means the effect will only run on the first render. This array will usually contain state variables or props.

We are using an effect to both set up and tear down our timer when the component mounts and unmounts.

We use a `ref` to reference that timer. A `ref`  provides a way to keep a reference to things that don’t trigger rendering. We don’t need to use state for the timer. It doesn’t affect rendering. But, we need to keep a reference to it so we can clear it on unmount.

Want to dig into hooks a bit before moving on? I wrote an article before about them – "[React Hooks in 5 Minutes](https://dev.to/jh3y/react-hooks-in-5-minutes-55ic)". And there’s also great info in [the React docs](https://reactjs.org/docs/hooks-intro.html).

Our `Time` component has its own internal state that triggers renders. But, what if we wanted to change the interval length? We could manage that from above in our `App` component.

<div class="break-out">

 <pre><code class="language-javascript">const App = () =&gt; {
  const [interval, updateInterval] = useState(1000)
  return (
    &lt;Fragment&gt;
      &lt;Time interval={interval} /&gt;
      &lt;h2&gt;{`Interval: ${interval}`}&lt;/h2&gt;
      &lt;input type="range" min="1" value={interval} max="10000" onChange={e =&gt; updateInterval(e.target.value)}/&gt;
    &lt;/Fragment&gt;
  )
}
</code></pre>
</div>

Our new `interval` value is being stored in the state of `App`. And it dictates the rate at which the `Time` component updates.

The `Fragment` component is a special component we have access to through `React`. In `React`, a component must return a single child or `null`. We can’t return adjacent elements. But, sometimes we don’t want to wrap our content in a `div`. `Fragment`s allow us to avoid wrapper elements whilst keeping React happy.

You’ll also notice our first event bind happening there. We use `onChange` as an attribute of the `input` to update the `interval`.

The updated `interval` is then passed to `Time` and the change of `interval` triggers our effect to run. This is because the second parameter of our `useEffect` hook now contains `interval`.

<pre><code class="language-javascript">const Time = ({ interval }) =&gt; {
  const [time, setTime] = useState(Date.now())
  const timer = useRef(null)
  useEffect(() =&gt; {
    timer.current = setInterval(() =&gt; setTime(Date.now()), interval)
    return () =&gt; clearInterval(timer.current)
  }, [interval])
  return &lt;h1&gt;{`Time: ${time}`}&lt;/h1&gt;
}
</code></pre>

Have a play with the demo and see the changes!

{{< codepen height="480" theme_id="light" slug_hash="KKWpQGK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Managed Interval](https://codepen.io/smashingmag/pen/KKWpQGK) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

I recommend visiting the [React documentation](https://reactjs.org/docs/hello-world.html) if you want to dig into some of these concepts more. But, we’ve seen enough React to get started making something fun! Let’s do it!

## Whac-A-Mole React Game

Are you ready? We’ll be creating our very own “Whac-A-Mole” with React! This [well-known game](https://en.wikipedia.org/wiki/Whac-A-Mole) is basic in theory but throws up some interesting challenges to build. The important part here is how we’re using React. I’ll gloss over applying styles and making it pretty &mdash; that’s your job! Although, I’m happy to take any questions on that. 

Also, this game will not be "polished". But, it works. You can go and make it your own! Add your own features, and so on.

## Design

Let’s start by thinking about what we’ve got to make, i.e. what components we may need, and so on:

- Start/Stop Game
- Timer
- Keeping Score
- Layout
- Mole Component

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae30bae4-cada-4a88-b7fa-361dee61e533/whac-a-mole-sketch.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae30bae4-cada-4a88-b7fa-361dee61e533/whac-a-mole-sketch.png" width="800" height="" sizes="100vw" caption="Whac-A-Mole Sketch (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae30bae4-cada-4a88-b7fa-361dee61e533/whac-a-mole-sketch.png'>Large preview</a>)" alt="Whac-A-Mole Sketch" >}}

## Starting Point

We’ve learned how to make a component and we can roughly gauge what we need.

<div class="break-out">

 <pre><code class="language-javascript">import React, { Fragment } from 'https://cdn.skypack.dev/react'
import { render } from 'https://cdn.skypack.dev/react-dom'

const Moles = ({ children }) =&gt; &lt;div&gt;{children}&lt;/div&gt;
const Mole = () =&gt; &lt;button&gt;Mole&lt;/button&gt;
const Timer = () =&gt; &lt;div&gt;Time: 00:00&lt;/div&gt;
const Score = () =&gt; &lt;div&gt;Score: 0&lt;/div&gt;

const Game = () =&gt; (
  &lt;Fragment&gt;
    &lt;h1&gt;Whac-A-Mole&lt;/h1&gt;
    &lt;button&gt;Start/Stop&lt;/button&gt;
    &lt;Score/&gt;
    &lt;Timer/&gt;
    &lt;Moles&gt;
      &lt;Mole/&gt;
      &lt;Mole/&gt;
      &lt;Mole/&gt;
      &lt;Mole/&gt;
      &lt;Mole/&gt;
    &lt;/Moles&gt;
  &lt;/Fragment&gt;
)

render(&lt;Game/&gt;, document.getElementById('app'))
</code></pre>
</div>

## Starting/Stopping

Before we do anything, we need to be able to start and stop the game. Starting the game will trigger elements like the timer and moles to come to life. This is where we can introduce **conditional rendering**.

<pre><code class="language-javascript">const Game = () =&gt; {
  const [playing, setPlaying] = useState(false)
  return (
    &lt;Fragment&gt;
      {!playing && &lt;h1&gt;Whac-A-Mole&lt;/h1&gt;}
      &lt;button onClick={() =&gt; setPlaying(!playing)}&gt;
        {playing ? 'Stop' : 'Start'}
      &lt;/button&gt;
      {playing && (
        &lt;Fragment&gt;
          &lt;Score /&gt;
          &lt;Timer /&gt;
          &lt;Moles&gt;
            &lt;Mole /&gt;
            &lt;Mole /&gt;
            &lt;Mole /&gt;
            &lt;Mole /&gt;
            &lt;Mole /&gt;
          &lt;/Moles&gt;
        &lt;/Fragment&gt;
      )}
    &lt;/Fragment&gt;
  )
}
</code></pre>

We have a state variable of `playing` and we use that to render elements that we need. In JSX, we can use a condition with `&&` to render something if the condition is `true`. Here we say to render the board and its content if we are playing. This also affects the button text where we can use a [ternary](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator).

{{< codepen height="480" theme_id="light" slug_hash="gOmpvBB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [1. Toggle Play State](https://codepen.io/smashingmag/pen/gOmpvBB) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

## Timer

Let’s **get the timer running**. By default, we’re going to set a time limit of `30000ms`, And we can declare this as a constant outside of our React components.

<pre><code class="language-javascript">const TIME_LIMIT = 30000
</code></pre>

Declaring constants in one place is a good habit to pick up. Anything that can be used to configure your app can be co-located in one place.

Our `Timer` component only cares about three things:

1. The time it’s counting down;
2. At what interval it’s going to update;
3. What it does when it ends.

A first attempt might look like this:

<pre><code class="language-javascript">const Timer = ({ time, interval = 1000, onEnd }) =&gt; {
  const [internalTime, setInternalTime] = useState(time)
  const timerRef = useRef(time)
  useEffect(() =&gt; {
    if (internalTime === 0 && onEnd) onEnd()
  }, [internalTime, onEnd])
  useEffect(() =&gt; {
    timerRef.current = setInterval(
      () =&gt; setInternalTime(internalTime - interval),
      interval
    )
    return () =&gt; {
      clearInterval(timerRef.current)
    }
  }, [])
  return &lt;span&gt;{`Time: ${internalTime}`}&lt;/span&gt;
}
</code></pre>

But, it only updates once?

{{< codepen height="480" theme_id="light" slug_hash="yLMNvQN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [2. Attempted Timer](https://codepen.io/smashingmag/pen/yLMNvQN) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

We’re using the same interval technique we did before. But, the issue is we’re using `state` in our **interval callback**. And this is our first "gotcha". Because we have an empty dependency array for our effect, it only runs once. The closure for `setInterval` uses the value of `internalTime` from the first render. This is an interesting problem and makes us think about how we approach things.

**Note**: *I highly recommend [reading this article by Dan Abramov](https://overreacted.io/making-setinterval-declarative-with-react-hooks/) that digs into timers and how to get around this problem. It’s a worthwhile read and provides a deeper understanding. One issue is that empty dependency arrays can often introduce bugs in our React code. There’s also an [eslint plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks) I’d recommend using to help point these out. The React docs also [highlight the potential risks](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects) of using the empty dependency array.*

One way to fix our `Timer` would be to **update the dependency array** for the effect. This would mean that our `timerRef` would get updated every interval. However, it introduces the issue of drifting accuracy.

<pre><code class="language-javascript">useEffect(() =&gt; {
  timerRef.current = setInterval(
 () =&gt; setInternalTime(internalTime - interval),
    interval
 )
  return () =&gt; {
 clearInterval(timerRef.current)
  }
}, [internalTime, interval])
</code></pre>

If you check this demo, it has the same Timer twice with different intervals and logs the drift to the developer console. A smaller interval or longer time equals a bigger drift.

{{< codepen height="480" theme_id="light" slug_hash="zYZGRbN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [3. Checking Timer Drift](https://codepen.io/smashingmag/pen/zYZGRbN) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

We can use a `ref` to solve our problem. We can use it to track the `internalTime` and avoid running the effect every interval.

<pre><code class="language-javascript">const timeRef = useRef(time)
useEffect(() =&gt; {
  timerRef.current = setInterval(
    () =&gt; setInternalTime((timeRef.current -= interval)),
    interval
  )
  return () =&gt; {
    clearInterval(timerRef.current)
  }
}, [interval])
</code></pre>

And this reduces the drift significantly with smaller intervals too. Timers are sort of an edge case. But, it’s a great example to think about **how we use hooks in React**. It’s an example that’s stuck with me and helped me understand the “Why?”.

Update the render to divide the time by `1000` and append an `s` and we have a seconds timer.

{{< codepen height="480" theme_id="light" slug_hash="oNZXEVp" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [4. Rudimentary Timer](https://codepen.io/smashingmag/pen/oNZXEVp) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

This timer is still rudimentary. It will drift over time. For our game, it’ll be fine. If you want to dig into **accurate counters**, this is a [great video on creating accurate timers](https://youtu.be/MCi6AZMkxcU) with JavaScript.

## Scoring

Let’s make it possible to update the score. How do we score? By whacking a mole! In our case, that means clicking a `button`. For now, let’s give each mole a score of `100`, and we can pass an `onWhack` callback to our `Mole`s.

<div class="break-out">

 <pre><code class="language-javascript">const MOLE_SCORE = 100

const Mole = ({ onWhack }) =&gt; (
  &lt;button onClick={() =&gt; onWhack(MOLE_SCORE)}&gt;Mole&lt;/button&gt;
)

const Score = ({ value }) =&gt; &lt;div&gt;{`Score: ${value}`}&lt;/div&gt;

const Game = () =&gt; {
  const [playing, setPlaying] = useState(false)
  const [score, setScore] = useState(0)
  
  const onWhack = points =&gt; setScore(score + points)
  
  return (
    &lt;Fragment&gt;
      {!playing && &lt;h1&gt;Whac-A-Mole&lt;/h1&gt;}
      &lt;button onClick={() =&gt; setPlaying(!playing)}&gt;{playing ? 'Stop' : 'Start'}&lt;/button&gt;
      {playing &&
        &lt;Fragment&gt;
          &lt;Score value={score} /&gt;
          &lt;Timer
            time={TIME_LIMIT}
            onEnd={() =&gt; setPlaying(false)}
          /&gt;
          &lt;Moles&gt;
            &lt;Mole onWhack={onWhack} /&gt;
            &lt;Mole onWhack={onWhack} /&gt;
            &lt;Mole onWhack={onWhack} /&gt;
            &lt;Mole onWhack={onWhack} /&gt;
            &lt;Mole onWhack={onWhack} /&gt;
          &lt;/Moles&gt;
        &lt;/Fragment&gt;
      }
    &lt;/Fragment&gt;
  )
}
</code></pre>
</div>

Note how the `onWhack` callback gets passed to each `Mole`, and that the callback updates our `score` state. These updates will trigger a render.

This is a good time to install the [React Developer Tools extension](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab) in your browser. There is a neat feature that will highlight component renders in the DOM. Open the "Components" tab in Dev Tools and hit the Settings cog. Select "Highlight updates when components render":

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc29ad67-6029-43f3-9469-b406741aa211/react-devtools.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc29ad67-6029-43f3-9469-b406741aa211/react-devtools.png" width="800" height="" sizes="100vw" caption="Setting up React DevTools (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc29ad67-6029-43f3-9469-b406741aa211/react-devtools.png'>Large preview</a>)" alt="Setting up React DevTools" >}}

Open the demo at [this link](https://cdpn.io/jh3y/debug/abpQvPg) and set the extension to highlight renders. Next, you’ll see that **the timer renders as time changes**, but when we whack a mole, all components re-render.

## Loops in JSX

You might be thinking that the way we’re rendering our `Mole`s is inefficient. And you’d be right to think that! There’s an opportunity for us here to **render these in a loop**.

With JSX, we tend to use `Array.map` 99% of the time to render a collection of things. [For example](https://codepen.io/smashingmag/pen/VwpLRLd):

<div class="break-out">

 <pre><code class="language-javascript">const USERS = [
  { id: 1, name: 'Sally' },
  { id: 2, name: 'Jack' },
]
const App = () =&gt; (
  &lt;ul&gt;
    {USERS.map(({ id, name }) =&gt; &lt;li key={id}&gt;{name}&lt;/li&gt;)}
  &lt;/ul&gt;
)
</code></pre>
</div>

The alternative would be to generate the content in a for loop and then render the return from a function.

<pre><code class="language-javascript">return (
  &lt;ul&gt;{getLoopContent(DATA)}&lt;/ul&gt;
)
</code></pre>

What’s that `key` attribute for? That helps React **determine what changes need to render**. If you can use a unique identifier, then do so! As a last resort, use the index of the item in a collection. (Read [the docs on lists](https://reactjs.org/docs/lists-and-keys.html) for more.)

For our example, we don’t have any data to work with. If you need to generate a collection of things, then here’s a trick you can use:

<pre><code class="language-javascript">new Array(NUMBER_OF_THINGS).fill().map()
</code></pre>

This could work for you in some scenarios.

<div class="break-out">

 <pre><code class="language-javascript">return (
  &lt;Fragment&gt;
    &lt;h1&gt;Whac-A-Mole&lt;/h1&gt;
    &lt;button onClick={() =&gt; setPlaying(!playing)}&gt;{playing ? 'Stop' : 'Start'}&lt;/button&gt;
    {playing &&
      &lt;Board&gt;
        &lt;Score value={score} /&gt;
        &lt;Timer time={TIME_LIMIT} onEnd={() =&gt; console.info('Ended')}/&gt;
        {new Array(5).fill().map((&#95;, id) =&gt; 
          &lt;Mole key={id} onWhack={onWhack} /&gt;
        )}
      &lt;/Board&gt;
    }
  &lt;/Fragment&gt;
)
</code></pre>
</div>

Or, if you want a persistent collection, you could use something like `uuid`:

<div class="break-out">

 <pre><code class="language-javascript">import { v4 as uuid } from 'https://cdn.skypack.dev/uuid'
const MOLE_COLLECTION = new Array(5).fill().map(() =&gt; uuid())

// In our JSX
{MOLE_COLLECTION.map((id) =&gt; 
  <Mole key={id} onWhack={onWhack} />
)}
</code></pre>
</div>

## Ending Game

We can only end our game with the Start button. When we do end it, the score remains when we start again. The `onEnd` for our `Timer` also does nothing yet.

{{< codepen height="480" theme_id="light" slug_hash="BaWNYEE" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [6. Looping Moles](https://codepen.io/smashingmag/pen/BaWNYEE) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

What we need is a third state where we aren’t `playing` but we have finished. In more complex applications, I’d recommend reaching for [XState](https://xstate.js.org/docs/) or [using reducers](https://reactjs.org/docs/hooks-reference.html#usereducer). But, for our app, we can introduce a new state variable: `finished`. When the state is `!playing` and `finished`, we can display the score, reset the timer, and give the option to restart.

We need to put our logic caps on now. If we end the game, then instead of toggling `playing`, we need to also toggle `finished`. We could create an `endGame` and `startGame` function.

<pre><code class="language-javascript">const endGame = () =&gt; {
  setPlaying(false)
  setFinished(true)
}

const startGame = () =&gt; {
  setScore(0)
  setPlaying(true)
  setFinished(false)
}
</code></pre>

When we start a game, we reset the `score` and put the game into the `playing` state. This triggers the playing UI to render. When we end the game, we set `finished` to `true`. (The reason we don’t reset the `score` is so we can show it as a result.)

And, when our `Timer` ends, it should invoke that same function.

<pre><code class="language-javascript">&lt;Timer time={TIME_LIMIT} onEnd={endGame} /&gt;
</code></pre>

It can do that within an effect. If the `internalTime` hits `0`, then unmount and invoke `onEnd`.

<pre><code class="language-javascript">useEffect(() =&gt; {
  if (internalTime === 0 && onEnd) {
    onEnd()
  }
}, [internalTime, onEnd])
</code></pre>

We can shuffle our UI rendering to render three states:

- Fresh
- Playing
- Finished

<pre><code class="language-javascript">&lt;Fragment&gt;
  {!playing && !finished &&
    &lt;Fragment&gt;
      &lt;h1&gt;Whac-A-Mole&lt;/h1&gt;
      &lt;button onClick={startGame}&gt;Start Game&lt;/button&gt;
    &lt;/Fragment&gt;
  }
  {playing &&
    &lt;Fragment&gt;
      &lt;button
        className="end-game"
        onClick={endGame}
       &gt;
        End Game
      &lt;/button&gt;
      &lt;Score value={score} /&gt;
      &lt;Timer
        time={TIME&#95;LIMIT}
        onEnd={endGame}
      /&gt;
      &lt;Moles&gt;
        {new Array(NUMBER&#95;OF&#95;MOLES).fill().map((&#95;, index) =&gt; (
          &lt;Mole key={index} onWhack={onWhack} /&gt;
        ))}
      &lt;/Moles&gt;
    &lt;/Fragment&gt;
  }
  {finished && 
    &lt;Fragment&gt;
      &lt;Score value={score} /&gt;
      &lt;button onClick={startGame}&gt;Play Again&lt;/button&gt;
    &lt;/Fragment&gt;
  }
&lt;/Fragment&gt;
</code></pre>

And now we have a functioning game minus moving moles:

{{< codepen height="480" theme_id="light" slug_hash="abJOqrw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [7. Ending a Game](https://codepen.io/smashingmag/pen/abJOqrw) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

Note how we’ve reused the `Score` component.
Was there an opportunity there to not repeat `Score`? Could you put it in its own conditional? Or does it need to appear there in the DOM. This will come down to your design.

Might you end up with a more generic component to cover it? These are the questions to keep asking. The goal is to **keep a separation of concerns with your components**. But, you also want to keep portability in mind.

## Moles

Moles are the centerpiece of our game. They don’t care about the rest of the app. But, they’ll give you their score `onWhack`. This emphasizes **portability**.

We aren’t digging into styling in this "Guide", but for our moles, we can create a container with `overflow: hidden` that our `Mole` (button) moves in and out of. The default position of our `Mole` will be out of view:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f075c25f-811f-4d14-844d-117076251094/mole-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f075c25f-811f-4d14-844d-117076251094/mole-design.png" width="800" height="" sizes="100vw" caption="Mole design (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f075c25f-811f-4d14-844d-117076251094/mole-design.png'>Large preview</a>)" alt="Mole Design" >}}

We’re going to bring in a third-party solution to make our moles bob up and down. This is an example of how to bring in **third-party solutions that work with the DOM**. In most cases, we use refs to grab DOM elements, and then we use our solution within an effect.

We’re going to use [GreenSock(GSAP)](https://greensock.com) to make our moles bob. We won’t dig into the GSAP APIs today, but if you have any questions about what they’re doing, please ask me!

Here’s an updated `Mole` with `GSAP`:

<pre><code class="language-javascript">import gsap from 'https://cdn.skypack.dev/gsap'

const Mole = ({ onWhack }) =&gt; {
  const buttonRef = useRef(null)
  useEffect(() =&gt; {
    gsap.set(buttonRef.current, { yPercent: 100 })
    gsap.to(buttonRef.current, {
      yPercent: 0,
      yoyo: true,
      repeat: -1,
    })
  }, [])
  return (
    &lt;div className="mole-hole"&gt;
      &lt;button
        className="mole"
        ref={buttonRef}
        onClick={() =&gt; onWhack(MOLE_SCORE)}&gt;
        Mole
      &lt;/button&gt;
    &lt;/div&gt;
  )
}
</code></pre>

We’ve added a wrapper to the `button` which allows us to show/hide the `Mole`, and we’ve also given our `button` a `ref`. Using an effect, we can create a tween (GSAP animation) that moves the button up and down.

You’ll also notice that we’re using `className` which is the attribute equal to `class` in JSX to apply class names. Why don’t we use the `className` with GSAP? Because if we have many elements with that `className`, our effect will try to use them all. This is why `useRef` is a great choice to stick with.

{{< codepen height="480" theme_id="light" slug_hash="QWpbQXW" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [8. Moving Moles](https://codepen.io/smashingmag/pen/QWpbQXW) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

Awesome, now we have bobbing `Mole`s, and our game is complete from a functional sense. They all move exactly the same which isn’t ideal. They should **operate at different speeds**. The points scored should also reduce the longer it takes for a `Mole` to get whacked.

Our Mole’s internal logic can deal with how scoring and speeds get updated. Passing the initial `speed`, `delay`, and `points` in as props will make for a more flexible component.

<div class="break-out">

 <pre><code class="language-javascript">&lt;Mole key={index} onWhack={onWhack} points={MOLE_SCORE} delay={0} speed={2} /&gt;
</code></pre>
</div>

Now, for a breakdown of our `Mole` logic.

Let’s start with how our points will reduce over time. This could be a good candidate for a `ref`. We have something that doesn’t affect render whose value could get lost in a closure. We create our animation in an effect and it’s never recreated. On each repeat of our animation, we want to decrease the `points` value by a multiplier. The points value can have a minimum value defined by a `pointsMin` prop.

<pre><code class="language-javascript">const bobRef = useRef(null)
const pointsRef = useRef(points)

useEffect(() =&gt; {
  bobRef.current = gsap.to(buttonRef.current, {
    yPercent: -100,
    duration: speed,
    yoyo: true,
    repeat: -1,
    delay: delay,
    repeatDelay: delay,
    onRepeat: () =&gt; {
      pointsRef.current = Math.floor(
        Math.max(pointsRef.current * POINTS_MULTIPLIER, pointsMin)
      )
    },
  })
  return () =&gt; {
    bobRef.current.kill()
  }
}, [delay, pointsMin, speed])
</code></pre>

We’re also creating a `ref` to keep a reference for our GSAP animation. We will use this when the `Mole` gets whacked. Note how we also return a function that kills the animation on unmount. If we don’t kill the animation on unmount, the repeat code will keep firing.

{{< codepen height="480" theme_id="light" slug_hash="JjWdpQr" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [9. Score Reduction](https://codepen.io/smashingmag/pen/JjWdpQr) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

What will happen when a mole gets whacked? We need a new state for that.

<pre><code class="language-javascript">const [whacked, setWhacked] = useState(false)
</code></pre>

And instead of using the `onWhack` prop in the `onClick` of our `button`, we can create a new function `whack`. This will set `whacked` to `true` and call `onWhack` with the current `pointsRef` value.

<pre><code class="language-javascript">const whack = () =&gt; {
 setWhacked(true)
 onWhack(pointsRef.current)
}

return (
 &lt;div className="mole-hole"&gt;
    &lt;button className="mole" ref={buttonRef} onClick={whack}&gt;
      Mole
    &lt;/button&gt;
  &lt;/div&gt;
)
</code></pre>

The last thing to do is respond to the `whacked` state in an effect with `useEffect`. Using the **dependency array**, we can make sure we only run the effect when `whacked` changes. If `whacked` is `true`, we reset the points, pause the animation, and animate the `Mole` underground. Once underground, we wait for a random delay before restarting the animation. The animation will start speedier using `timescale` and we set `whacked` back to `false`.

<pre><code class="language-javascript">useEffect(() =&gt; {
  if (whacked) {
    pointsRef.current = points
    bobRef.current.pause()
    gsap.to(buttonRef.current, {
      yPercent: 100,
      duration: 0.1,
      onComplete: () =&gt; {
        gsap.delayedCall(gsap.utils.random(1, 3), () =&gt; {
          setWhacked(false)
          bobRef.current
            .restart()
            .timeScale(bobRef.current.timeScale() * TIME_MULTIPLIER)
        })
      },
    })
  }
}, [whacked])
</code></pre>

That gives us:

{{< codepen height="480" theme_id="light" slug_hash="MWpwQNy" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [10. React to Whacks](https://codepen.io/smashingmag/pen/MWpwQNy) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

The last thing to do is pass props to our `Mole` instances that will make them behave differently. But, how we generate these props could cause an issue.

<pre><code class="language-javascript">&lt;div className="moles"&gt;
  {new Array(MOLES).fill().map((&#95;, id) =&gt; (
    &lt;Mole
      key={id}
      onWhack={onWhack}
      speed={gsap.utils.random(0.5, 1)}
      delay={gsap.utils.random(0.5, 4)}
      points={MOLE_SCORE}
    /&gt;
  ))}
&lt;/div&gt;
</code></pre>

This would cause an issue because the props would change on every render as we generate the moles. A better solution could be to generate a new `Mole` array each time we start the game and iterate over that. This way, we can keep the game random without causing issues.

<pre><code class="language-javascript">const generateMoles = () =&gt; new Array(MOLES).fill().map(() =&gt; ({
  speed: gsap.utils.random(0.5, 1),
  delay: gsap.utils.random(0.5, 4),
  points: MOLE_SCORE
}))
// Create state for moles
const [moles, setMoles] = useState(generateMoles())
// Update moles on game start
const startGame = () =&gt; {
  setScore(0)
  setMoles(generateMoles())
  setPlaying(true)
  setFinished(false)
}
// Destructure mole objects as props
&lt;div className="moles"&gt;
  {moles.map(({speed, delay, points}, id) =&gt; (
    &lt;Mole
      key={id}
      onWhack={onWhack}
      speed={speed}
      delay={delay}
      points={points}
    /&gt;
  ))}
&lt;/div&gt;
</code></pre>

And here’s the result! I’ve gone ahead and added some styling along with a few varieties of moles for our buttons.

{{< codepen height="480" theme_id="light" slug_hash="VwpLQod" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [11. Functioning Whac-a-Mole](https://codepen.io/smashingmag/pen/VwpLQod) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

We now have a fully working “Whac-a-Mole” game built in React. It took us **less than 200 lines of code**. At this stage, you can take it away and make it your own. Style it how you like, add new features, and so on. Or you can stick around and we can put together some extras!

## Tracking The Highest Score

We have a working "Whac-A-Mole", but how can we keep track of our highest achieved score? We could use an effect to write our score to `localStorage` every time the game ends. But, what if persisting things was a common need. We could create a custom hook called `usePersistentState`. This could be a wrapper around `useState` that reads/writes to `localStorage`.

<pre><code class="language-javascript">  const usePersistentState = (key, initialValue) =&gt; {
  const [state, setState] = useState(
    window.localStorage.getItem(key)
      ? JSON.parse(window.localStorage.getItem(key))
      : initialValue
  )
  useEffect(() =&gt; {
    window.localStorage.setItem(key, state)
  }, [key, state])
  return [state, setState]
}
</code></pre>

And then we can use that in our game:

<div class="break-out">

 <pre><code class="language-javascript">const [highScore, setHighScore] = usePersistentState('whac-high-score', 0)
</code></pre>
</div>

We use it exactly the same as `useState`. And we can hook into `onWhack` to set a new high score during the game when appropriate:

<pre><code class="language-javascript">const endGame = points =&gt; {
  if (score > highScore) setHighScore(score) // play fanfare!
}
</code></pre>

How might we be able to tell if our game result is a new high score? Another piece of state? Most likely.

{{< codepen height="480" theme_id="light" slug_hash="NWpqYKK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [12. Tracking High Score](https://codepen.io/smashingmag/pen/NWpqYKK) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

## Whimsical Touches

At this stage, we’ve covered everything we need to. Even how to make your own custom hook. Feel free to go off and make this your own.

Sticking around? Let’s **create another custom hook** for adding audio to our game:

<pre><code class="language-javascript">const useAudio = (src, volume = 1) =&gt; {
  const [audio, setAudio] = useState(null)
  useEffect(() =&gt; {
    const AUDIO = new Audio(src)
    AUDIO.volume = volume
    setAudio(AUDIO)
  }, [src])
  return {
    play: () =&gt; audio.play(),
    pause: () =&gt; audio.pause(),
    stop: () =&gt; {
      audio.pause()
      audio.currentTime = 0
    },
  }
}
</code></pre>

This is a rudimentary hook **implementation for playing audio**. We provide an audio `src` and then we get back the API to play it. We can add noise when we “whac” a mole. Then the decision will be, is this part of `Mole`? Is it something we pass to `Mole`? Is it something we invoke in `onWhack` ?

These are the types of decisions that come up in component-driven development. We need to keep portability in mind. Also, what would happen if we wanted to **mute the audio?** How could we globally do that? It might make more sense as a first approach to control the audio within the `Game` component:

<pre><code class="language-javascript">// Inside Game
const { play: playAudio } = useAudio('/audio/some-audio.mp3')
const onWhack = () =&gt; {
  playAudio()
  setScore(score + points)
}
</code></pre>

It’s all about design and decisions. If we bring in lots of audio, renaming the `play` variable could get tedious. Returning an Array from our hook-like `useState` would allow us to name the variable whatever we want. But, it also might be hard to remember which index of the Array accounts for which API method.

{{< codepen height="480" theme_id="light" slug_hash="eYvNMOB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [13. Squeaky Moles](https://codepen.io/smashingmag/pen/eYvNMOB) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

## That’s It!

More than enough to get you started on your React journey, and we got to make something interesting. We sure did cover a lot:

- Creating an app,
- JSX,
- Components and props,
- Creating timers,
- Using refs,
- Creating custom hooks.

We made a game! And now you can use your new skills to add new features or make it your own.

Where did I take it? At the time of writing, it’s at this stage so far:

{{< codepen height="480" theme_id="light" slug_hash="JjWdLPO" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Whac-a-Mole w/ React &amp;&amp; GSAP](https://codepen.io/smashingmag/pen/JjWdLPO) by <a href="https://codepen.io/jh3y">@jh3y</a>.{{< /codepen >}}

## Where To Go Next!

I hope building “Whac-a-Mole” has motivated you to start your React journey. Where next? Well, here are some links to resources to check out if you’re looking to dig in more &mdash; some of which are ones I found useful along the way.

- [React Documentation](https://reactjs.org/docs/)
- “[Making `setInterval` Declarative With React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/),” Dan Abramov
- “[How To Fetch Data With React Hooks](https://www.robinwieruch.de/react-hooks-fetch-data),” Robin Wieruch
- “[When To `useMemo` And `useCallback`](https://kentcdodds.com/blog/usememo-and-usecallback),” Kent C Dodds
- [Read more React articles](https://www.smashingmagazine.com/search/?q=react) right here on Smashing Magazine

{{< signature "vf, il" >}}
