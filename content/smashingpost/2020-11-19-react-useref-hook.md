---
title: 'A Thoughtful Way To Use React’s <code>useRef()</code> Hook'
slug: react-useref-hook
author: aleem-isiaka
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cf66d77-d466-449f-90ad-da8545f5db99/react-useref-hook.png
date: 2020-11-19T10:30:00.000Z
summary: >-
  In a React component, `useState` and `useReducer` can cause your component to re-render each time there is a call to the update functions. In this article, you will find out how to use the `useRef()` hook to keep track of variables without causing re-renders, and how to enforce the re-rendering of React Components.
description: >-
  In a React component, `useState` and `useReducer` can cause your component to re-render each time there is a call to the update functions. In this article, you will find out how to use the `useRef()` hook to keep track of variables without causing re-renders, and how to enforce the re-rendering of React Components.
categories:
  - Apps
  - React
  - Coding
  - React Hooks
---

In React components, there are times when frequent changes have to be tracked without enforcing the re-rendering of the component. It can also be that there is a need to re-render the component efficiently. While `useState` and `useReducer` hooks are the React API to manage local state in a React component, they can also come at a cost of being called too often making the component to re-render for each call made to the update functions.

In this article, I’ll explain why `useState` is not efficient for tracking some states, illustrate how `useState` creates too much re-render of a component, how values that are stored in a variable are not persisted in a component, and last but not least, how `useRef` can be used keep track of variables without causing re-render of the component. And give a solution on how to enforce re-render without affecting the performance of a component.

After the evolution of functional components, functional components got the ability to have a local state that causes re-rendering of the component once there is an update to any of their local state.

<pre><code class="language-javascript">function Card (props) {
  const [toggled, setToggled] = useState(false);
  
  const handleToggleBody  = () =&gt; {
    setToggled(!toggled)
  }
  
  return (&lt;section className="card"&gt;
    &lt;h3 className="card__title" onMouseMove={handleToggleBody}&gt;
       {props.title}
    &lt;/h3&gt;
    
    {toggled && &lt;article className="card__body"&gt;
      {props.body}
    &lt;/article>}
  &lt;/section&gt;)
}

// Consumed as:
&lt;Card name="something" body="very very interesting" /&gt;</code></pre>

In the component above, a card is rendered using a `section` element having a child `h3` with a `card__title` class which holds the title of the card, the body of the card is rendered in an article tag with the body of `card__body`. We rely on the `title` and `body` from the props to set the content of the title and body of the card, while the body is only toggled when the header is hovered over.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8cf523a-bf3c-4981-bbcc-c1259124b54a/3-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8cf523a-bf3c-4981-bbcc-c1259124b54a/3-react-useref-hook.gif" width="892" height="531" alt="Scenario – mouseover event" /></a><figcaption>Scenario – mouseover event (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8cf523a-bf3c-4981-bbcc-c1259124b54a/3-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

{{% feature-panel %}}

### Re-rendering A Component With `useState`

Initial rendering of a component is done when a component has its pristine, undiluted state values, just like the Card component, its initial render is when the mouseover event is yet to be triggered. Re-rendering of a component is done in a component when one of its local states or props have been updated, this causes the component to call its render method to display the latest elements based on the state update.

In the `Card` component, the `mousemove` event handler calls the `handleToggleBody` function to update the state negating the previous value of the toggled state.

We can see this scenario in the `handleToggleBody` function calling the `setToggled` state update function. This causes the function to be called every time the event is triggered.

### Storing State Values In A Variable

A workaround for the repeated re-rendering is using a *local variable* within the component to hold the toggled state which can also be updated to prevent the frequent re-rendering &mdash; which is carried out only when there is an update to local states or props of a component.

<pre><code class="language-javascript">function Card (props) {
  let toggled = false;
  
  const handleToggleBody  = () =&gt; {
    toggled = !toggled;
    console.log(toggled);
  }
  
  return (&lt;section className="card"&gt;
    &lt;section className="cardTitle" onMouseMove={handleToggleBody}&gt;
       {title}
    &lt;/section&gt;
    
    {toggled && &lt;article className="cardBody"&gt;
      {body}
    &lt;/article&gt;}
  &lt;/section&gt;)
}

&lt;Card name="something" body="very very interesting" /&gt;</code></pre>

This comes with an unexpected behavior where the value is updated but the component is not re-rendered because no internal state or props has changed to trigger a re-render of the component.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3026ffbd-22bd-4862-8a4f-20c78c7ab973/7-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4e79b2c-8ac7-4623-b6d3-aad9197290fe/7-react-useref-hook-800w.gif" width="800" height="103" alt="Using variable in place of state" /></a><figcaption>Using variable in place of state (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3026ffbd-22bd-4862-8a4f-20c78c7ab973/7-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

### Local Variables Are Not Persisted Across Rerender

Let's consider the steps from initial rendering to a re-rendering of a React component. 

- Initially, the component initializes all variables to the default values, also stores all the state and refs to a unique store as defined by the React algorithm.
- When a new update is available for the component through an update to its props or state, React pulls the old value for states and refs from its store and re-initializes the state to the old value also applying an update to the states and refs that have an update.
- It then runs the function for the component to render the component with the updated states and refs. This re-rendering will also re-initialize variables to hold their initial values as defined in the component since they are not tracked.
- The component is then re-rendered.

Below is an example that can illustrate this:

<div class="break-out">

<pre><code class="language-javascript">function Card (props) {
  let toggled = false;
  
  const handleToggleBody = () =&gt; {
    toggled = true;
    console.log(toggled);
  };

  useEffect(() =&gt; {
    console.log(“Component rendered, the value of toggled is:“, toggled);
  }, [props.title]);

  return (
    &lt;section className=“card”&gt;
      &lt;h3 className=“card__title” onMouseMove={handleToggleBody}&gt;
        {props.title}
      &lt;/h3&gt;

      {toggled && &lt;article className=“card__body”&gt;{props.body}&lt;/article&gt;}
    &lt;/section&gt;
  );
}

// Renders the application
function App () {
  
  const [cardDetails, setCardDetails] = useState({
    title: “Something”,
    body: “uniquely done”,
  });

  useEffect(() =&gt; {
    setTimeout(() =&gt; {
      setCardDetails({
        title: “We”,
        body: “have updated something nice”,
      });
    }, 5000); // Force an update after 5s
  }, []);

  return (
    &lt;div&gt;
      &lt;Card title={cardDetails.title} body={cardDetails.body} /&gt;
    &lt;/div&gt;
  );
}
</code></pre>
</div>

In the above code, the `Card` component is being rendered as a child in the `App` component. The `App` component is relying on an internal state object named `cardDetails` to store the details of the card. Also, the component makes an update to the `cardDetails` state after 5seconds of initial rendering to force a re-rendering of the `Card` component list.

The `Card` has a slight behavior; instead of switching the toggled state, it is set to `true` when a mouse cursor is placed on the title of the card. Also, a `useEffect` hook is used to track the value of the `toggled` variable after re-rendering.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/847df04c-f117-4f42-9559-94ef3b2817c6/6-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a64fb419-f106-4cff-9d6e-44dbe2b189a0/6-react-useref-hook-800w.gif" width="800" height="159" alt="Using variable in place of state – second test" /></a><figcaption>Using variable in place of state (second test) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/847df04c-f117-4f42-9559-94ef3b2817c6/6-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

The result after running this code and placing a mouse on the title updates the variable internally but does not cause a re-render, meanwhile, a re-render is triggered by the parent component which re-initializes the variable to the initial state of `false` as defined in the component. Interesting!

{{% ad-panel-leaderboard %}}

## About `useRef()` Hook

Accessing DOM elements is core JavaScript in the browser, using vanilla JavaScript a `div` element with class  `"title"` can be accessed using:

<pre><code class="language-html">&lt;div class="title"&gt;
  This is a title of a div
&lt;/div&gt;
&lt;script&gt;
  const titleDiv = document.querySelector("div.title")
&lt;/script&gt;</code></pre>

The reference to the element can be used to do interesting things such as changing the text content `titleDiv.textContent = "this is a newer title"` or changing the class name `titleDiv.classList = "This is the class"` and much more operations.

Overtime, DOM manipulation libraries like jQuery made this process seamless with a single function call using the `$` sign. Getting the same element using jQuery is possible through  `const el = ("div.title")`, also the text content can be updated through the jQuery's API: `el.text("New text for the title div")`.

### Refs In React Through The `useRef` Hook

ReactJS being a modern frontend library took it further by providing a Ref API to access its element, and even a step further through the `useRef` hook for a functional component.

<pre><code class="language-javascript">import React, {useRef, useEffect} from "react";

export default function (props) {
  // Initialized a hook to hold the reference to the title div.
  const titleRef = useRef();
  
  useEffect(function () {
    setTimeout(() =&gt; {
      titleRef.current.textContent = "Updated Text"
    }, 2000); // Update the content of the element after 2seconds 
  }, []);
  
  return &lt;div className="container"&gt;
    {/** The reference to the element happens here **/ }
    &lt;div className="title" ref={titleRef}&gt;Original title&lt;/div&gt;
  &lt;/div&gt;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bdcfd8f-4a40-40a5-bd32-17d6295fa41c/4-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c7f5c27-b232-43b2-8b06-5c528c3933ed/4-react-useref-hook-800w.gif" width="800" height="175" alt="Using Ref to store state" /></a><figcaption>Using Ref to store state (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bdcfd8f-4a40-40a5-bd32-17d6295fa41c/4-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

As seen above, after the 2 seconds of the component initial rendering, the text content for the `div` element with the className of title changes to "Updated text".

### How Values Are Stored In `useRef`

A Ref variable in React is a mutable object, but the value is persisted by React across re-renders. A ref object has a single property named `current` making refs have a structure similar to `{ current: ReactElementReference }`.

The decision by the React Team to make refs persistent and mutable should be seen as a wise one. For example, during the re-rendering of a component, the DOM element may get updated during the process, then it is necessary for the ref to the DOM element to be updated too, and if not updated, the reference should be maintained. This helps to avoid inconsistencies in the final rendering.

### Explicitly Updating The Value Of A `useRef` Variable

The update to a `useRef` variable, the new value can be assigned to the `.current` of a ref variable. This should be done with caution when a ref variable is referencing a DOM element which can cause some unexpected behavior, aside from this, updating a ref variable is *safe*.

<pre><code class="language-javascript">function User() {
  const name = useRef("Aleem");

  useEffect(() =&gt; {
    setTimeout(() =&gt; {
      name.current = "Isiaka";
      console.log(name);
    }, 5000);
  });

  return &lt;div&gt;{name.current}&lt;/div&gt;;
}</code></pre>

## Storing Values In `useRef`

A unique way to implement a `useRef` hook is to use it to store values instead of DOM references. These values can either be a state that does not need to change too often or a state that should change as frequently as possible but should not trigger full re-rendering of the component.

Bringing back the card example, instead of storing values as a state, or a variable, a ref is used instead.

<div class="break-out">

<pre><code class="language-javascript">function Card (props) {
  
  let toggled = useRef(false);
  
  const handleToggleBody  = () =&gt; {
    toggled.current = !toggled.current;
  }
  
  return (
    &lt;section className=“card”&gt;
      &lt;h3 className=“card__title” onMouseMove={handleToggleBody}&gt;
        {props.title}
      &lt;/h3&gt;

      {toggled && &lt;article className=“card__body”&gt;{props.body}&lt;/article&gt;}
    &lt;/section&gt;
  );
  &lt;/section&gt;)
}</code></pre>
</div>

This code gives the desired result internally but not visually. The value of the toggled state is persisted but no re-rendering is done when the update is done, this is because refs are expected to hold the same values throughout the lifecycle of a component, React does not expect them to change.

{{% ad-panel-leaderboard %}}

### Shallow And Deep Rerender

In React, there are two rendering mechanisms, *shallow* and *deep* rendering. Shallow rendering affects just the component and not the children, while deep rendering affects the component itself and all of its children.

When an update is made to a ref, the shallow rendering mechanism is used to re-render the component.

<div class="break-out">

<pre><code class="language-javascript">function UserAvatar (props) {
  return &lt;img src={props.src} /&gt;
}

function Username (props) {
  return &lt;span&gt;{props.name}&lt;/span&gt;
}

function User () {
  const user = useRef({
    name: "Aleem Isiaka",
    avatarURL: "https://icotar.com/avatar/jake.png?bg=e91e63",
  })

  console.log("Original Name", user.current.name);
  console.log("Original Avatar URL", user.current.avatarURL);
  
  useEffect(() =&gt; {
    setTimeout(() =&gt; {
      user.current = {
        name: "Isiaka Aleem",
        avatarURL: "https://icotar.com/avatar/craig.png?s=50", // a new image
      };
    },5000)
  })
  
  // Both children won't be re-rendered due to shallow rendering mechanism
  // implemented for useRef
  return (&lt;div&gt;
    &lt;Username name={user.name} /&gt;
      &lt;UserAvatar src={user.avatarURL} /&gt;
  &lt;/div&gt;);
}</code></pre>
</div>

In the above example, the user's details are stored in a ref which is updated after 5 seconds, the User component has two children, Username to display the user's name and `UserAvatar` to display the user's avatar image.

After the update has been made, the value of the `useRef` is updated but the children are not updating their UI since they are not re-rendered. This is shallow re-rendering, and it is what is implemented for useRef hook.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aac040c-c818-411f-a437-4c3e3306e0c2/5-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23f8af37-7977-426b-904f-f0e4b23edfbd/5-react-useref-hook-800w.gif" width="800" height="175" alt="Shallow-rerender" /></a><figcaption>Shallow-rerender (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aac040c-c818-411f-a437-4c3e3306e0c2/5-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

Deep re-rendering is used when an update is carried out on a state using the `useState` hook or an update to the component's props.

<div class="break-out">

<pre><code class="language-javascript">function UserAvatar (props) {
  return &lt;img src={props.src} /&gt;
}

function Username (props) {
  return &lt;span&gt;{props.name}&lt;/span&gt;
}

function User () {
  const [user, setUser] = useState({
    name: "Aleem Isiaka",
    avatarURL: "https://icotar.com/avatar/jake.png?bg=e91e63",
  });

  useEffect(() =&gt; {
    setTimeout(() =&gt; {
      setUser({
        name: "Isiaka Aleem",
        avatarURL: "https://icotar.com/avatar/craig.png?s=50", // a new image
      });
    },5000);
  })
  
  // Both children are re-rendered due to deep rendering mechanism
  // implemented for useState hook
  return (&lt;div&gt;
    &lt;Username name={user.name} /&gt;
      &lt;UserAvatar src={user.avatarURL} /&gt;
  &lt;/div&gt;);
}</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be901fbd-9ee1-4630-9dd5-b5b86bf13b14/2-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/289ad835-8e30-4c01-b7e5-eb3e014e2693/2-react-useref-hook-800w.gif" width="800" height="175" alt="Deep rerender" /></a><figcaption>Deep rerender (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be901fbd-9ee1-4630-9dd5-b5b86bf13b14/2-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

Contrary to the result experienced when `useRef` is used, the children, in this case, get the latest value and are re-rendered making their UIs have the desired effects. 

### Forcing A Deep Re-render For `useRef` Update

To achieve a deep re-render when an update is made to refs, the deep re-rendering mechanism of the `useState` hook can be *partially* implemented.

<div class="break-out">

<pre><code class="language-javascript">function UserAvatar (props) {
  return &lt;img src={props.src} /&gt;
}

function Username (props) {
  return &lt;span&gt;{props.name}&lt;/span&gt;
}

function User () {
  const user = useRef({
    name: "Aleem Isiaka",
    avatarURL: "https://icotar.com/avatar/jake.png?bg=e91e63",
  })

  const [, setForceUpdate] = useState(Date.now());
  
  useEffect(() =&gt; {
    setTimeout(() =&gt; {
      user.current = {
        name: "Isiaka Aleem",
        avatarURL: "https://icotar.com/avatar/craig.png?s=50", // a new image
      };
      
      setForceUpdate();
    },5000)
  })
  return (&lt;div&gt;
    &lt;Username name={user.name} /&gt;
      &lt;UserAvatar src={user.avatarURL} /&gt;
  &lt;/div&gt;);
}</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04438ef5-5552-4ce1-8c79-b6d17c75fae3/1-react-useref-hook.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f4dc4aa-e071-46cf-bbde-b292c2579b4b/1-react-useref-hook-800w.gif" width="800" height="175" alt="Deep + Shallow rerender" /></a><figcaption>Deep + Shallow rerender (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04438ef5-5552-4ce1-8c79-b6d17c75fae3/1-react-useref-hook.gif">Large preview</a>)</figcaption></figure>

In the above improvement to the `User` component, a state is introduced but its value is ignored since it is not required, while the update function to enforce a rerender of the component is named ``setForceUpdate`` to maintain the naming convention for `useState` hook. The component behaves as expected and re-renders the children after the ref has been updated.

This can raise questions such as:

<blockquote>“Is this not an anti-pattern?”<br /><br />or<br /><br />“Is this not doing the same thing as the initial problem but differently?”</blockquote>

Sure, this is an anti-pattern, because we are taking advantage of the flexibility of `useRef` hook to store local states, and still calling `useState` hook to ensure the children get the latest value of the `useRef` variable current value both of which can be achieved with `useState`.

Yes, this is doing *almost* the same thing as the initial case but differently. The `setForceUpdate` function does a deep re-rendering but does not update any state that is acting on the component’s element, which keeps it consistent across re-render.

## Conclusion

Frequently updating state in a React component using `useState` hook can cause undesired effects. We have also seen while variables can be a go-to option; they are not persisted across the re-render of a component like a state is persisted.

Refs in React are used to store a reference to a React element and their values are persisted across re-render. Refs are mutable objects, hence they can be updated explicitly and can hold values other than a reference to a React element.

Storing values in refs solve the problem of frequent re-rendering but brought a new challenge of the component not being updated after a ref’s value has changed which can be solved by introducing a `setForceUpdate` state update function. 

Overall, the takeaways here are:

- We can store values in refs and have them updated, which is more efficient than `useState` which can be expensive when the values are to be updated multiple times within a second.
- We can force React to re-render a component, even when there is no need for the update by using a non-reference `useState` update function.
- We can combine 1 and 2 to have a high-performance ever-changing component.

### References

- “[Hooks API Reference](https://reactjs.org/docs/hooks-reference.html),” React Docs
- “[Understanding <code>useRef</code>: An Intro To Refs And React Hooks](https://levelup.gitconnected.com/understanding-useref-513b1bbe00dc),” Kris Mason, Medium
- “[Managing Component State With The `useRef` Hook](https://livebook.manning.com/book/react-hooks-in-action/chapter-6/v-3/69),” React Hooks in Action (Chapter 6), Manning Publications Co.
- “[Use <code>useRef</code> Hook To Store Values You Want To Keep An Eye On](https://mariosfakiolas.com/blog/use-useref-hook-to-store-values-you-want-to-keep-an-eye-on/),” Marios Fakiolas

{{< signature "ra, yk, il" >}}
