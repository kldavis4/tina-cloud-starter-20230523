---
title: 'How To Use The HTML Drag-And-Drop API In React'
slug: html-drag-drop-api-react
author: chidi-orji
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/307d09ce-87e3-456a-bebd-ed0ce1cf9884/html-drag-drop-api-react.png
date: 2020-02-19T11:00:00.000Z
summary: >-
  In this tutorial, we’ll build a React drag-and-drop component for file and image uploads. In the process, we’ll learn about the HTML drag-and-drop API. We will also learn how to use the [useReducer](https://reactjs.org/docs/hooks-reference.html#usereducer) hook for managing state in a React functional component.
description: >-
  In this tutorial, we’ll learn about the HTML drag-and-drop API and how to use the `useReducer` hook for managing state in a React functional component.
categories:
  - API
  - React
  - JavaScript
---

The drag-and-drop API is one of the coolest features of HTML. It helps us implement drag-and-drop features in web browsers.

In the current context, we will be dragging files from outside the browser. On dropping the file(s), we put them on a list and display their names. With the files in hand, we could then perform some other operation on the file(s), e.g. upload them to a cloud server.

In this tutorial, we’ll be focusing on how to implement the action of dragging and dropping in a React application. If what you need is a plain `JavaScript` implementation, perhaps you’d first like to read “[How To Make A Drag-And-Drop File Uploader With Vanilla JavaScript](https://www.smashingmagazine.com/2018/01/drag-drop-file-uploader-vanilla-js/),” an excellent tutorial written by Joseph Zimmerman not too long ago.

## The  `dragenter`, `dragleave`, `dragover`, And `drop` Events

There are eight different drag-and-drop events. Each one fires at a different stage of the drag-and-drop operation. In this tutorial, we’ll focus on the four that are fired when an item is dropped into a drop zone: `dragenter`, `dragleave`, `dragover` and `drop`.

1. The `dragenter` event fires when a dragged item enters a valid drop target.
2. The `dragleave` event fires when a dragged item leaves a valid drop target.
3. The `dragover` event fires when a dragged item is being dragged over a valid drop target. (It fires every few hundred milliseconds.)
4. The `drop` event fires when an item drops on a valid drop target, i.e dragged over and released.

We can turn any HTML element into a valid drop target by defining the `ondragover` and `ondrop` event handler attributes.

*You can learn all about the eight events from the [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API).*

{{% feature-panel %}}

## Drag-And-Drop Events In React

To get started, clone the tutorial repo from this URL:

<pre><code class="language-bash">https://github.com/chidimo/react-dnd.git
</code></pre>

Check out the `01-start` branch. Make sure you have `yarn` installed as well. You can get it from [yarnpkg.com](https://yarnpkg.com/).

But if you prefer, create a new React project and replace the content of *App.js* with the code below:
   

<pre><code class="language-javascript">import React from 'react';
import './App.css';

function App() {
  return (
    &lt;div className="App"&gt;
      &lt;h1&gt;React drag-and-drop component&lt;/h1&gt;
    &lt;/div&gt;
  );
}
export default App;
</code></pre>

Also, replace the content of *App.css* with the below CSS style:
  

<pre><code class="language-css">.App {
  margin: 2rem;
  text-align: center;
}
h1 {
  color: #07F;
}
.drag-drop-zone {
  padding: 2rem;
  text-align: center;
  background: #07F;
  border-radius: 0.5rem;
  box-shadow: 5px 5px 10px #C0C0C0;
}
.drag-drop-zone p {
  color: #FFF;
}
.drag-drop-zone.inside-drag-area {
  opacity: 0.7;
}
.dropped-files li {
  color: #07F;
  padding: 3px;
  text-align: left;
  font-weight: bold;
}
</code></pre>

If you cloned the repo, issue the following commands (in order) to start the app:

<pre><code class="language-bash">yarn # install dependencies
yarn start # start the app
</code></pre>

The next step is to create a drag-and-drop component. Create a file *DragAndDrop.js* inside the `src/` folder. Enter the following function inside the file:

<pre><code class="language-javascript">import React from 'react';

const DragAndDrop = props => {
  const handleDragEnter = e => {
    e.preventDefault();
    e.stopPropagation();
  };
  const handleDragLeave = e => {
    e.preventDefault();
    e.stopPropagation();
  };
  const handleDragOver = e => {
    e.preventDefault();
    e.stopPropagation();
  };
  const handleDrop = e => {
    e.preventDefault();
    e.stopPropagation();
  };
  return (
    &lt;div className={'drag-drop-zone'}
      onDrop={e => handleDrop(e)}
      onDragOver={e => handleDragOver(e)}
      onDragEnter={e => handleDragEnter(e)}
      onDragLeave={e => handleDragLeave(e)}
    &gt;
      &lt;p&gt;Drag files here to upload&lt;/p&gt;
    &lt;/div&gt;
  );
};
export default DragAndDrop;
</code></pre>

In the return `div`, we have defined our focus `HTML` event handler attributes. You can see that the only difference from pure `HTML` is the camel-casing.

The `div` is now a valid drop target since we have defined the `onDragOver` and `onDrop` event handler attributes.

We also defined functions to handle those events. Each of these handler function receives the event object as its argument.

For each of the event handlers, we call `preventDefault()` to stop the browser from executing its default behavior. The default browser behavior is to open the dropped file. We also call `stopPropagation()` to make sure that the event is not propagated from child to parent elements.

Import the `DragAndDrop` component into the `App` component and render it below the heading.

<pre><code class="language-javascript">&lt;div className="App"&gt;
  &lt;h1&gt;React drag-and-drop component&lt;/h1&gt;
  &lt;DragAndDrop /&gt;
&lt;/div&gt;
</code></pre>

Now view the component in the browser and you should see something like the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd7973bb-d198-4d10-9f3e-caf187968d06/01-react-drag-and-drop.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd7973bb-d198-4d10-9f3e-caf187968d06/01-react-drag-and-drop.png" sizes="100vw" caption="<code>div</code> to be converted into a drop zone (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd7973bb-d198-4d10-9f3e-caf187968d06/01-react-drag-and-drop.png'>Large preview</a>)" alt="Drop zone" >}}

If you’re following with the repo, the corresponding branch is `02-start-dragndrop`

{{% ad-panel-leaderboard %}}

## Managing State With The `useReducer` Hook

Our next step will be to write the logic for each of our event handlers. Before we do that, we have to consider how we intend to keep track of dropped files. This is where we begin to think about state management.

We will be keeping track of the following states during the drag-and-drop operation:

1. `dropDepth`  
This will be an integer. We’ll use it to keep track of how many levels deep we are in the drop zone. Later on, I will explain this with an illustration. (*Credits to [Egor Egorov](https://medium.com/@650egor) for shining a light on this one for me!*)
2. `inDropZone`  
This will be a boolean. We will use this to keep track of whether we’re inside the drop zone or not.
3. `FileList`  
This will be a list. We’ll use it to keep track of files that have been dropped into the drop zone.

To handle states, React provides the `useState` and `useReducer` hooks. We’ll opt for the `useReducer` hook given that we will be dealing with situations where a state depends on the previous state.

The `useReducer` hook accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a `dispatch` method.

*You can read more about* `useReducer` *in the [React](https://reactjs.org/docs/hooks-reference.html#usereducer) [docs](https://reactjs.org/docs/hooks-reference.html#usereducer).*

Inside the `App` component (before the `return` statement), add the following code:

<div class="break-out">

 <pre><code class="language-javascript">...
const reducer = (state, action) => {
  switch (action.type) {
    case 'SET_DROP_DEPTH':
      return { ...state, dropDepth: action.dropDepth }
    case 'SET_IN_DROP_ZONE':
      return { ...state, inDropZone: action.inDropZone };
    case 'ADD_FILE_TO_LIST':
      return { ...state, fileList: state.fileList.concat(action.files) };
    default:
      return state;
  }
};
const [data, dispatch] = React.useReducer(
  reducer, { dropDepth: 0, inDropZone: false, fileList: [] }
)
...
</code></pre>
</div>

The `useReducer` hook accepts two arguments: a reducer and an initial state. It returns the current state and a `dispatch` function with which to update the state. The state is updated by dispatching an action that contains a `type`  and an optional payload. The update made to the component’s state is dependent on what is returned from the case statement as a result of the action type. (Note here that our initial state is an `object`.)

For each of the state variables, we defined a corresponding case statement to update it. The update is performed by invoking the `dispatch` function returned by `useReducer`.

Now pass `data` and `dispatch` as `props` to the `DragAndDrop` component you have in your *App.js* file:

<pre><code class="language-javascript">&lt;DragAndDrop data={data} dispatch={dispatch} /&gt;
</code></pre>

 At the top of the `DragAndDrop` component, we can access both values from `props`.
 

<pre><code class="language-javascript">const { data, dispatch } = props;
</code></pre>

If you’re following with the repo, the corresponding branch is `03-define-reducers`.

Let’s finish up the logic of our event handlers. Note that the ellipsis represents the two lines:

<div class="break-out">

 <pre><code class="language-javascript">e.preventDefault()
e.stopPropagation()


const handleDragEnter = e => {
  ...
  dispatch({ type: 'SET_DROP_DEPTH', dropDepth: data.dropDepth + 1 });
};

const handleDragLeave = e => {
  ...
  dispatch({ type: 'SET_DROP_DEPTH', dropDepth: data.dropDepth - 1 });
  if (data.dropDepth > 0) return
  dispatch({ type: 'SET_IN_DROP_ZONE', inDropZone: false })
};
</code></pre>
</div>

In the illustration that follows, we have nested drop zones A and B. A is our zone of interest. This is where we want to listen for drag-and-drop events.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7855a68-1719-4f02-a328-75e6c467aae8/02-react-drag-and-drop.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7855a68-1719-4f02-a328-75e6c467aae8/02-react-drag-and-drop.png" sizes="100vw" caption="An illustration of the <code>ondragenter</code> and <code>ondragleave</code> events (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7855a68-1719-4f02-a328-75e6c467aae8/02-react-drag-and-drop.png'>Large preview</a>)" alt="An illustration of the ondragenter and ondragleave events" >}}

When dragging into a drop zone, each time we hit a boundary, the `ondragenter` event is fired. This happens at boundaries `A-in` and `B-in`. Since we’re entering the zone, we increment `dropDepth`.

{{% ad-panel-leaderboard %}}

Likewise, when dragging out of a drop zone, each time we hit a boundary, the `ondragleave` event is fired. This happens at boundaries `A-out` and `B-out`. Since we’re leaving the zone, we decrement the value of `dropDepth`. Notice that we don’t set `inDropZone` to `false` at boundary `B-out`. That is why we have this line to check the dropDepth and return from the function `dropDepth` greater than `0`.

<pre><code class="language-javascript">if (data.dropDepth > 0) return</code></pre>

This is because even though the `ondragleave` event is fired, we’re still within zone A. It is only after we have hit `A-out`, and `dropDepth` is now `0` that we set `inDropZone` to `false`. At this point, we have left all drop zones.

<pre><code class="language-javascript">const handleDragOver = e => {
  ...
  e.dataTransfer.dropEffect = 'copy';
  dispatch({ type: 'SET_IN_DROP_ZONE', inDropZone: true });
};
</code></pre>

Each time this event fires, we set `inDropZone` to `true`. This tells us that we’re inside the drop zone. We also set the `dropEffect` on the `dataTransfer` object to `copy`. On a Mac, this has the effect of showing a green plus sign as you drag an item around in the drop zone.

<div class="break-out">

 <pre><code class="language-javascript">const handleDrop = e => {
  ...
  let files = [...e.dataTransfer.files];
  
  if (files && files.length > 0) {
    const existingFiles = data.fileList.map(f => f.name)
    files = files.filter(f => !existingFiles.includes(f.name))
    
    dispatch({ type: 'ADD_FILE_TO_LIST', files });
    e.dataTransfer.clearData();
    dispatch({ type: 'SET_DROP_DEPTH', dropDepth: 0 });
    dispatch({ type: 'SET_IN_DROP_ZONE', inDropZone: false });
  }
};
</code></pre>
</div>

We can access the dropped files with `e.dataTransfer.files`. The value is an array-like object so we use the array spread syntax to convert it to a `JavaScript` array.

We now need to check if there is at least one file before attempting to add it to our array of files. We also make sure to not include files that are already on our `fileList`.
The `dataTransfer` object is cleared in preparation for the next drag-and-drop operation. We also reset the values of `dropDepth` and `inDropZone`.

Update the `className` of the `div` in the `DragAndDrop` component. This will conditionally change the `className` of the `div` depending on the value of `data.inDropZone`.

<div class="break-out">

 <pre><code class="language-javascript">&lt;div className={data.inDropZone ? 'drag-drop-zone inside-drag-area' : 'drag-drop-zone'}
      ...
    &gt;
  &lt;p&gt;Drag files here to upload&lt;/p&gt;
&lt;/div&gt;
</code></pre>
</div>

Render the list of files in *App.js* by mapping through `data.fileList`.

<pre><code class="language-javascript">&lt;div className="App"&gt;
  &lt;h1&gt;React drag-and-drop component&lt;/h1&gt;
  &lt;DragAndDrop data={data} dispatch={dispatch} /&gt;
  &lt;ol className="dropped-files"&gt;
    {data.fileList.map(f =&gt; {
      return (
        &lt;li key={f.name}&gt;{f.name}&lt;/li&gt;
      )
    })}
  &lt;/ol&gt;
&lt;/div&gt;
</code></pre>

Now try dragging and dropping some files onto the drop zone. You’ll see that as we enter the drop zone, the background becomes less opaque because the `inside-drag-area` class is activated.

When you release the files inside the drop zone, you’ll see the file names listed under the drop zone:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40aade50-a9c8-4ab2-ab5e-22c9a10cd3ac/03-react-drag-and-drop.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40aade50-a9c8-4ab2-ab5e-22c9a10cd3ac/03-react-drag-and-drop.png" sizes="100vw" caption="Drop zone showing low opacity during dragover (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40aade50-a9c8-4ab2-ab5e-22c9a10cd3ac/03-react-drag-and-drop.png'>Large preview</a>)" alt="Drop zone showing low opacity during dragover" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab70fff-d821-4638-9440-8a53954d2519/04-react-drag-and-drop.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab70fff-d821-4638-9440-8a53954d2519/04-react-drag-and-drop.png" sizes="100vw" caption="A list of files dropped into the drop zone (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab70fff-d821-4638-9440-8a53954d2519/04-react-drag-and-drop.png'>Large preview</a>)" alt="A list of files dropped into the drop zone" >}}

The complete version of this tutorial is on the `04-finish-handlers` branch.

## Conclusion

We’ve seen how to handle file uploads in React using the `HTML` drag-and-drop API. We’ve also learned how to manage state with the `useReducer` hook. We could extend the file `handleDrop`  function. For example, we could add another check to limit file sizes if we wanted. This can come before or after the check for existing files. We could also make the drop zone clickable without affecting the drag-and-drop functionality.

### Resources

- “[Hooks API Reference: `useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer),” React Docs
- “[HTML Drag-and-Drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API),” MDN web docs
- “[Examples Of Web And XML Development Using The DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Examples#Example_5:_Event_Propagation),” MDN web docs
- “[How To Make A Drag-and-Drop File Uploader With Vanilla JavaScript](https://www.smashingmagazine.com/2018/01/drag-drop-file-uploader-vanilla-js/),” Joseph Zimmerman, Smashing Magazine
- “[Simple Drag-And-Drop File Upload In React](https://medium.com/@650egor/simple-drag-and-drop-file-upload-in-react-2cb409d88929),” Egor Egorov, Medium

{{< signature "ra, ks, il" >}}
