---
title: 'React State Management Using Easy Peasy'
slug: react-state-management-easy-peasy
author: topple
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24aacd02-eab4-420c-89c9-560c182570c4/react-state-management-easy-peasy.jpg
date: 2022-02-01T12:00:00.000Z
summary: >-
  According to the <a href="https://easy-peasy.now.sh/docs/introduction/">documentation</a>, Easy Peasy is an abstraction of Redux, providing a reimagined API that focuses on <strong>developer experience</strong>. It allows you to <strong>quickly</strong> and <strong>easily</strong> manage your state, whilst leveraging the strong <strong>architectural guarantees</strong>. We’ll use Easy Peasy as a state manager of choice to build a note application which would help us learn how it works. 
description: >-
  According to the <a href="https://easy-peasy.now.sh/docs/introduction/">documentation</a>, Easy Peasy is an abstraction of Redux, providing a reimagined API that focuses on <strong>developer experience</strong>. It allows you to <strong>quickly</strong> and <strong>easily</strong> manage your state, whilst leveraging the strong <strong>architectural guarantees</strong>. We’ll use Easy Peasy as a state manager of choice to build a note application which would help us learn how it works.
categories:
  - React
  - Tools
  - Apps
---

In building React applications, one of the most important questions for developers include managing state effectively. In this tutorial, we are going to learn how to use [Easy Peasy](https://easy-peasy.now.sh/) for managing state in React applications. We’d understand the core concepts of Easy Peasy, some use cases for it, why it should be used for your next application and build a simple example. Easy Peasy is open source with more than 4.1k stars on [GitHub](https://github.com/ctrlplusb/easy-peasy).

This tutorial will be beneficial to readers who are interested in learning how to manage state with Easy Peasy in their React applications, or looking for alternatives in regards to state management in a React application. This article requires a basic understanding of React and JavaScript. 

### What Is Easy Peasy?

Easy Peasy is a state manager that works similar to Redux but with less code and complexity than Redux. Easy Peasy was built in mind to provide the same performance as Redux and other state managers.

Core concepts of Easy Peasy include the following hooks and methods.

- **Store**  
Similar to Redux, Easy Peasy requires a store powered by React Context, which will disclose the application state to certains parts of your application.
- **State**   
This is an essential part of Easy Peasy because it uses the state or model to define your application store.
- **Thunk Action**  
This is used in Easy Peasy to perform operations that are termed side effects, such as making an API call.
- **Actions**   
Actions are used to update the application store. 
- **useStoreState**  
This is a custom hook from Easy Peasy that gives our components access to the application’s store state. 
- **useStoreActions**  
Like the name implies, this hook gives our components access to the store’s actions. 
- **Provider**  
Similar to Redux, Easy Peasy comes with a Provider method that exposes the store to our React app, this is done so our components will be able to consume the store with React hooks.

Easy Peasy can be installed using any package manager by using the command below:

<pre><code class="language-bash">npm install easy-peasy</code></pre>

 Or this command for yarn package manager :
 

<pre><code class="language-bash">yarn add easy-peasy</code></pre>

{{% feature-panel %}}

### Why Easy Peasy?

Easy Peasy’s  main objective is to improve state management for React developers and make for an easier way of managing application state with less code and boilerplate. Easy Peasy removes the abstractions of Redux and simplifies state management with a simpler process, making it easier for anyone to use in React applications.

Easy Peasy also provides support for React Hooks based API and Redux middlewares such as Redux thunk out of the box. With this, Easy Peasy can be setup to perform API requests as side effect using thunk actions. Let’s see the API call below for an example of a request that deletes a user and gets a user by their `id`. 

<div class="break-out">

<pre><code class="language-javascript">import { action, computed, createContextStore, thunk } from 'easy-peasy';
import { deleteUser, getUserById } from './user';

const UserStore = createContextStore({
  getUsers: thunk(async actions =&gt; {
    actions.setIsLoading();
    try {
      const { data } = await getUsers();
      actions.setUsers(data);
    } catch (e) {
      actions.setError(e);
    }
    actions.setIsLoading();
  }),
  getUserById: thunk(async (actions, id) =&gt; {
    actions.setIsLoading();
    try {
      const { data } = await getUserById(id);
      actions.setUser(data);
    } catch (e) {
      actions.setError(e);
    }
    actions.setIsLoading();
  })
});</code></pre>
</div>

In the code block, we are getting users from the API using the `getUser` thunk and setting the user as our current state, we also did the same thing to the `deleteUser` method. 

### Easy Peasy vs Redux/MobX/HookState

Similar to other state managers like Redux and MobX, Easy Peasy makes use of a single store to handle the application state, and it also appreciates the use of actions as a source of data for our application store. It’s important to note that Easy Peasy uses Redux internally to manage state.

Unlike Redux and MobX, Easy Peasy requires little to no boilerplate code to work with, Easy Peasy uses [Immer](https://immerjs.github.io/immer/docs/introduction) under the hood, which gives developers the power to interact with data while keeping the benefits of the immutable data.

Easy Peasy allows developers to extend the application store by using Redux middlewares and other custom hooks to enhance performance.

Compared to React HookState, Easy Peasy offers more ease of managing and updating state with a single store and sharing information with component using custom hooks such as `useStoreState` and `useStoreAction` which comes out of the box with Easy Peasy.

With its ease and zero boilerplate code, Easy Peasy can be used to manage state from simple React to-do applications to larger applications. Easy Peasy also provides a support for TypeScript out of the box.

### Building Notes Application With Easy Peasy 

Now that we know the core concepts of Easy Peasy, we’ll be building a notes application and managing the state with Easy Peasy. The application will allow users to add, delete and temporary cancel a note using a toggle.

Without further ado, let’s start!

### Setting Up Your Environment

First, let’s create a bare React application, write the code block below on your terminal:

<pre><code class="language-bash">create-react-app easy-peasy-notes-app</code></pre>

The above code will create a bare React application using the [create-react-app](https://github.com/facebook/create-react-app) package. Move into the project directory and add the dependencies we’d need for our application.

<pre><code class="language-bash">cd easy-peasy-notes-app</code></pre>

<pre><code class="language-bash">yarn add easy-peasy uuid

In the above code block, we installed</code></pre>

- **easy-peasy**  
Our state manager for our application.
- **uuid**  
This is for creating unique string of notes for our application.

If you’ve done this, then start the project server using the command below:

<pre><code class="language-bash">yarn start</code></pre>

Next, let’s create a `components` folder in our `src` directory, we’d be creating three components and an app store for our application. 

### Creating The App Store

As mentioned above, Easy Peasy works with a `store` to hold the application state. With this we can access the application store and update the state. In the store, we’d need to set up a function to add, toggle and delete notes in our application. 

To create our app store, first create a `Store.js` file in our project’s `src` directory, next let’s add logic to our store.

<div class="break-out">

<pre><code class="language-javascript">import { action } from "easy-peasy";
import uuid from "uuid";

export default {
  notes: [],
  setNote: action((state, notes) =&gt; {
    state.notes = notes;
  }),
  addNote: action((state, note) =&gt; {
    note.id = uuid.v4();
    state.notes.push(note);
  }),
  toggleNote: action((state, id) =&gt; {
    state.notes.map((note) =&gt; {
      return note.id === id ? (note.completed = !note.completed) : note;
    });
  }),
  removeNote: action((state, id) =&gt; {
    state.notes = state.notes.filter((note) =&gt; note.id !== id);
  })
};
</code></pre>
</div>

In the code above, we imported `actions` from `easy-peasy`, the actions will be used to update our application store, we imported `uuid` to give unique `ids` to our notes when they are created. We initialized notes as an empty array object and created a function `setNote` that takes in the state and note parameters and sets the current note as the value for `state.notes`.

The `addNote` function takes in two parameters, an initial `state` and a `note`, next we assigned the note `id` to one automatically provided by `uuid.v4()` and pushes the new note into the `state.notes` array. 

The `toggleNote` takes in the state and `id` parameters and using the native JavaScript [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) object to cross off completed notes by toggling the value of `note.completed`, the `removeNote` object deletes a note using the [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) object. 

We will use the logic above to create our application’s component in the next section. 

{{% ad-panel-leaderboard %}}

### Building The Note Component

Here, we will build our note component which will be the basic component for how each list will look on our application, to do this, let’s create a components folder in the `src` directory of our project and create a new file `Note.jsx` and inside it, write the code block below.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import { useStoreActions } from "easy-peasy";

const Note = ({ note }) =&gt; {
  const { completed } = note;
  const removeNote = useStoreActions(actions =&gt; actions.removeNote);
  const toggleNote = useStoreActions(actions =&gt; actions.toggleNote);
  return (
    &lt;li className="d-flex justify-content-between align-items-center mb-2"&gt;
      &lt;span
        className="h2 mr-2"
        style={{
          textDecoration: completed ? "line-through" : "",
          cursor: "pointer"
        }}
        onClick={() =&gt; toggleNote(note.id)}
      &gt;
        {note.title}
      &lt;/span&gt;
      &lt;button
        onClick={() =&gt; removeNote(note.id)}
        className="btn btn-danger btn-lg"
      &gt;
        &times;
      &lt;/button&gt;
    &lt;/li&gt;
  );
};

export default Note;</code></pre>
</div>

Here, the `useStoreActions` hook from easy-peasy give our `Note` component access to the actions in the store, in this case the `toggleNote` for crossing off a note as completed and `addNote` for adding a new note. We returned the `li` tag which contains the new note. 

Next, we added a delete button for our application, similar to the toggling a note, we added an `onClick` event that takes in the `removeNote` action, if we did this correctly our app should look like the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfb85b87-61d2-4238-8350-782b45ea523c/2-react-state-management-easy-peasy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfb85b87-61d2-4238-8350-782b45ea523c/2-react-state-management-easy-peasy.png" width="768" height="328" sizes="100vw" caption="Notes component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfb85b87-61d2-4238-8350-782b45ea523c/2-react-state-management-easy-peasy.png'>Large preview</a>)" alt="Notes component." >}}

### Building Notes Component

This component will act as a render for our notes, here we will add a header component for our application name and render all our notes in this component, let’s do that below.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import { useStoreState } from "easy-peasy";
import Note from "./Note";
const Notes = () =&gt; {
  const notes = useStoreState((state) =&gt; state.notes);
  return (
    &lt;&gt;
      &lt;h1 className="display-4"&gt;Notes&lt;/h1&gt;
      {notes.length === 0 ? (
        &lt;h2 className="display-3 text-capitalize"&gt;Please add note&lt;/h2&gt;
      ) : (
        notes.map((note) =&gt; &lt;Note key={note.id} note={note} /&gt;)
      )}
    &lt;/&gt;
  );
};
export default Notes;</code></pre>
</div>  

Here, we imported the [`useStoreState`](https://easy-peasy.now.sh/docs/api/use-store-state.html) hook from easy-peasy, the `useStoreState` grants our component access to the store’s state, next we created a functional component notes and using the `useStorestate` we assigned `notes` to the state of the application found on the store. 

As an [edge case](https://www.quora.com/What-is-an-edge-case-when-programming) using a tenary operaor, we will drop a text for the user to add a note if they haven’t and to render a note if they did. You can learn more about tenary operators [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator).

### Building NotesForm Component

This component will be the bulk of our application, here will will handle submitting our notes and setting it as the updated value of our application state. Let’s build the component below.

<div class="break-out">

<pre><code class="language-javascript">import React, { useState } from "react";
import { useStoreActions } from "easy-peasy";

const NotesForm = () =&gt; {
  const [title, setTitle] = useState("");
  const [err, setErr] = useState(false);
  const addNote = useStoreActions(actions =&gt; actions.addNote);
  const handleSubmit = e =&gt; {
    e.preventDefault();
    if (title.trim() === "") {
      setErr(true);
    } else {
      setErr(false);
      addNote({
        title,
        completed: false
      });
    }
    setTitle("");
  };
  return (
    &lt;&gt;
      &lt;form onSubmit={handleSubmit} className="d-flex py-5 form-inline"&gt;
        &lt;input
          type="text"
          placeholder="Add Todo Title"
          value={title}
          className="form-control mr-sm-2 form-control-lg"
          onChange={e =&gt; setTitle(e.target.value)}
        /&gt;
        &lt;button type="submit" className="btn btn-success btn-lg rounded"&gt;
          Add Note
        &lt;/button&gt;
      &lt;/form&gt;
      {err && (
        &lt;div className="alert alert-dismissible alert-danger"&gt;
          &lt;button
            type="button"
            className="close"
            data-dismiss="alert"
            onClick={() =&gt; setErr(false)}
          &gt;
            &times;
          &lt;/button&gt;
          &lt;strong&gt;Oh oh!&lt;/strong&gt;{" "}
          &lt;span className="alert-link"&gt;please add a valid text&lt;/span&gt;&lt;/div&gt;
      )}
    &lt;/&gt;
  );
};
export default NotesForm;
</code></pre>
</div>  

In this component, first in order to access our project’s action objects in the store, we imported the `useStoreActions` and initialized the `addNote` action for adding a note in our component, next we created an input form that includes input for adding notes, submitting a note to be added and a button for alert for when a user tries to add an empty note using the input. 

A final act will be to setup our `App.js` file and wrap our application using a `Provider` and restart our server to see our final application, let’s do tht in the code block below. 

<pre><code class="language-javascript">import React from "react";
import "./styles.css";
import Notes from './components/Notes';
import NotesForm from './components/NotesForm'

import { StoreProvider, createStore } from "easy-peasy";
import store from "./Store";

const Store = createStore(store);
function App() {
  return (
    &lt;StoreProvider store={Store}&gt;
      &lt;div className="container"&gt;
        &lt;NotesForm /&gt;
        &lt;Notes /&gt;
      &lt;/div&gt;
    &lt;/StoreProvider&gt;
  );
}</code></pre>

Here, we are imported the `StoreProvider` and `createStore,` the `StoreProvider` exposes the `store` to our application so that our components will be able to able to consume the store using hooks while the `createStore` similar to Redux creates a global `store` based on the models we’ve provided, next we wrapped our App component using the store as a parameter of the `StoreProvider`. 

Once done correctly, our app should look like the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/016f49e9-ea70-4770-9d13-8c09dd6de2cf/3-react-state-management-easy-peasy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/016f49e9-ea70-4770-9d13-8c09dd6de2cf/3-react-state-management-easy-peasy.png" width="765" height="435" sizes="100vw" caption="Easy peasy note application. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/016f49e9-ea70-4770-9d13-8c09dd6de2cf/3-react-state-management-easy-peasy.png'>Large preview</a>)" alt="Easy peasy note application" >}}

### API Request With Easy Peasy

In this section, we are going to look at handling API requests with Easy peasy, to better understand this, we will be building a currency converter using React, TypeScript and Easy peasy to manage the state of the application. In our application, users should be able to convert dollars to any currency, users can input the amount they’d like to convert and the currency they’re converting to. 

First, we will create a react app using the command below.

<pre><code class="language-bash">create-react-app currency-converter</code></pre>

We will add typescript support and reactstrap for styling using the Yarn package manager. 

<div class="break-out">

<pre><code class="language-bash">yarn add @testing-library/jest-dom @testing-library/react @testing-library/user-event @types/jest @types/node @types/react @types/react-dom axios bootstrap easy-peasy reactstrap typescript</code></pre>
</div>

For TypeScript support, create a `tsconfig.json` file in the root directory of our project and copy the code block below into it.

<pre><code class="language-javascript">{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": [
    "src"
  ]
}</code></pre>

After we’ve added the code above, to finish TypeScript configuration for our project, create a new file in the root directory of our project named `react-app-env.d.ts`, this file will reference the type of react-scripts we’d have in our project, you can learn more about it [here](https://www.sitepoint.com/react-with-typescript-best-practices/#:~:text=json%20is%20the%20TypeScript%20configuration,like%20allowing%20for%20SVG%20imports.).

<pre><code class="language-javascript">/// &lt;reference types="react-scripts" /&gt;</code></pre>

### Building Our App’s Store

To get started on our project proper, in the `src` directory of your project, create a `store` folder for our app’s store and inside it, create two files, `index.ts` and `typehook.ts.` Our `index.ts` file will contain our TypeScript interfaces for our API functions and our application store actions while our `typehook.ts` will contain Typed hooks from Easy peasy. In the code block below, we will create interfaces for our API requests.

<div class="break-out">

<pre><code class="language-javascript">import { createStore, Action, action, Thunk, thunk } from "easy-peasy";
import axios from "../axios";

export interface ICurrency {
  currency_name: string;
  currency_code: string;
  decimal_units: string;
  countries: string[];
}
interface IAllCurrencies {
  data: ICurrency[];
  updateResult: Action&lt;IAllCurrencies, ICurrency[]&gt;;
  getAllCurrencies: Thunk&lt;IAllCurrencies&gt;;
}
interface ICurrencyRates {
  rates: { [key: string]: string };
  updateRates: Action&lt;ICurrencyRates, any&gt;;
  getCurrencyRates: Thunk&lt;ICurrencyRates&gt;;
}
interface IConversion {
  data: {
    to: string;
    amount: string;
  };
  updateTo: Action&lt;IConversion, string&gt;;
  updateAmount: Action&lt;IConversion, string&gt;;
}
export interface IStore {
  allCurrencies: IAllCurrencies;
  currencyRates: ICurrencyRates;
  conversion: IConversion;
}

const store = createStore&lt;IStore&gt;({
  allCurrencies: {
    data: [],
    updateResult: action((state, payload) =&gt; {
      state.data = Object.values(payload);
    }),
    getAllCurrencies: thunk(async (actions) =&gt; {
      try {
        const res = await axios.get(`/currencies`);
        actions.updateResult(res?.data?.response?.fiats);
      } catch (error) {
        console.log(error);
      }
    }),
  },
  currencyRates: {
    rates: {},
    updateRates: action((state, payload) =&gt; {
      state.rates = payload;
    }),
    getCurrencyRates: thunk(async (actions) =&gt; {
      try {
        const res = await axios.get(`/latest`);
        actions.updateRates(res?.data?.response?.rates);
      } catch (error) {
        console.log(error);
      }
    }),
  },
  conversion: {
    data: {
      to: "",
      amount: "",
    },
    updateTo: action((state, payload) =&gt; {
      state.data.to = payload;
    }),
    updateAmount: action((state, payload) =&gt; {
      state.data.amount = payload;
    }),
  },
});
export default store;</code></pre>
</div>

Here, we created interfaces, which defines the contract on the properties we have, for example in `ICurrency` we enforced the name, code, decimal units and countries to be of type `string`. 

In `IAllCurrencies` we defined the data we’ll get from the API as an array containing the object we’ve defined in `ICurrency`, we also enforced our `updateResult` works based on the interface of `IAllCurrencies` and accepts a payload of `ICurrency` in an array while the `getAllCurrencies` method uses a [Thunk](https://easy-peasy.now.sh/docs/api/thunk.html) to perform asynchronous functions. 

We added an interface for `ICurrencyRates`, we defined rates to take in objects with keys which must be strings and also accept a string payload and `updateRates` will work with the data and any data type, `getCurrencyRates` uses Thunk to perform asynchronous functions with the data returned. 

To create store, we first called the easy-peasy store, in our case we structured the store to use the `IStore` interface, next we called the `allCurrencies` object from the `IStore`, inside it we will receive the data as an array. 

Similar to Redux, to update a state in easy peasy, you’d use an action. To update our state, we defined the action `updateResult` which acts as a [reducer](https://easy-peasy.now.sh/docs/api/reducer.html) and takes in our current state and the user’s payload and sets the current state using the values we get from the user’s payload. You can learn more about updating the [store](https://redux.js.org/api/createstore) and [createStore](https://easy-peasy.now.sh/docs/api/create-store.html).

To `getAllCurrencies` we performed an async operation using `axios` to get all currencies and use actions from set the data as the response, in the case of errors we wrapped the full application with a `try…catch` method. We performed similar functions in our `currencyRate` object, updating the state with an action and performing an async operation to get the latest rates from the API and setting the state using the data we receive.

The Conversion object converts the amount inputted by the user from dollars to any currency the user chooses, to display the amount we defined an action that updates and renders the amount converted to the user. 

{{% ad-panel-leaderboard %}}

### Building Our Store Type Hooks 

When using Easy Peasy with TypeScript, hooks are often recommended to have types, often this is done with interfaces defined in the project store. In this section, we will add types to the hooks we will be using in our application.

To do this, inside of our store directory, create a new file called `typehook.ts` and inside it, write the code block below.

<div class="break-out">

<pre><code class="language-javascript">import { createTypedHooks } from "easy-peasy";
import { IStore } from "./index";

const typedHooks = createTypedHooks&lt;IStore&gt;();

export const useStoreActions = typedHooks.useStoreActions;
export const useStoreDispatch = typedHooks.useStoreDispatch;
export const useStoreState = typedHooks.useStoreState;</code></pre>
</div>

In the code block above, we are adding types to our `useStoreActions`, `useStoreDispatch` and our `useStoreState` hooks, with this we are configuring it to the interfaces we’ve defined in our `IStore`. By doing this, whatever actions we are dispatching here will come from actions from the store.

### Building Header Component

In this section, we will add a `Header` to our application, the application header will contain our header, input fields for the user to add the amount and the currency they wish to convert. First, inside of our `src` directory, create a `components` folder and inside that folder, we’ll create a `header` folder, which will contain a `header.tsx` file.  Let’s add the logic for this.

<div class="break-out">

<pre><code class="language-javascript">import { useState } from "react";
import { Button, Form, FormGroup, Input, Jumbotron } from "reactstrap";
import { ICurrency } from "../../store";
import { useStoreState, useStoreActions } from "../../store/typehook";

const Header = () =&gt; {
  const allCurrencies = useStoreState((state) =&gt; state.allCurrencies.data);
  const setAmountToConvert = useStoreActions((actions) =&gt; actions.conversion.updateAmount);
  const setCurrencyToConvertTo = useStoreActions((actions) =&gt; actions.conversion.updateTo);
  const [to, setTo] = useState&lt;string&gt;("");
  const [amount, setAmount] = useState&lt;string&gt;("");

  const onSubmitHandler = (e: { preventDefault: () =&gt; void }) =&gt; {
    e.preventDefault();
    (to && amount) && setAmountToConvert(amount);
    (to && amount) && setCurrencyToConvertTo(to);
  };</code></pre>
</div>

In the code block above, we imported the `ICurrency` object from our store, we also imported `useStoreState` and `useStoreActions` from our custom typed hooks. 

We initialized our Header as a functional component, next we create a constant `allCurrencies` to get the state of `allCurrencies` in our store. With `setAmountToConvertTo`, there we called an action, the action we called is the `updateAmount` action from the store. 

Using React `useState`, we defined the state we want to update, we added a `<string>` to let our app know that state we are updating and defining is of string type. 

To handle submit, we created a function `onSubmitHandler` which converts an amount and currency the user inputted on submit. 

To finish our Header component, let’s render the input fields using react strap for our components and bootstrap for styling, to do that we’d append the code block below to the functions we’ve defined at the beginning of this section.

<div class="break-out">

<pre><code class="language-javascript">return (
    &lt;div className="text-center"&gt;
      &lt;Jumbotron fluid&gt;
        &lt;h1 className="display-4"&gt;Currency Converter&lt;/h1&gt;
        &lt;div className="w-50 mx-auto"&gt;
          &lt;Form id='my-form' onSubmit={onSubmitHandler}&gt;
            &lt;FormGroup className="d-flex flex-row mt-5 mb-5"&gt;
              &lt;Input
                type="number"
                value={amount}
                onChange={(e) =&gt; setAmount(e.target.value)}
                placeholder="Amount in Number"
              /&gt;
              &lt;Input
                type="text"
                value="from USD ($)"
                className='text-center w-50 mx-4'
                disabled
              /&gt;
              &lt;Input
                type="select"
                value={to}
                onChange={(e) =&gt; setTo(e.target.value)}
              &gt;
                &lt;option&gt;Converting to?&lt;/option&gt;
                {allCurrencies.map((currency: ICurrency) =&gt; (
                  &lt;option
                    key={currency?.currency_code}
                    value={currency?.currency_code}
                  &gt;
                    {currency?.currency_name}
                  &lt;/option&gt;
                ))}
              &lt;/Input&gt;
            &lt;/FormGroup&gt;
          &lt;/Form&gt;
          &lt;Button
            color="primary"
            size="lg"
            block
            className="px-4"
            type="submit"
            form='my-form'
          &gt;
            Convert
          &lt;/Button&gt;
        &lt;/div&gt;
      &lt;/Jumbotron&gt;
    &lt;/div&gt;
  );
};
export default Header;</code></pre>
</div>

Here, we built the input fields for our application, one for the amount to be converted and the currency, if done correctly our app should look similar to the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad30175-aee6-4075-ae8d-988dda842e75/1-react-state-management-easy-peasy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad30175-aee6-4075-ae8d-988dda842e75/1-react-state-management-easy-peasy.png" width="759" height="375" sizes="100vw" caption="Header component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad30175-aee6-4075-ae8d-988dda842e75/1-react-state-management-easy-peasy.png'>Large preview</a>)" alt="Header component" >}}

### Adding Currency API

To get the latest conversion rates and countries, we’d be using the rapid API currency API. To get started, first create a new folder `axios` in our `src` directory, inside this folder create a new file `index.tsx`. 

Next is to visit [Rapid API](https://rapidapi.com/citeamaccount/api/currencyscoop) and sign up to get an apiKey, when we do this, paste your API base URL and API keys inside our `index.tsx` in the format below.

<pre><code class="language-javascript">import axios from "axios";
export default axios.create({
  baseURL: "https://currencyscoop.p.rapidapi.com",
  headers: {
    "your api key goes here",
    "x-rapidapi-host": "currencyscoop.p.rapidapi.com",
  },
});
</code></pre>

To complete our application, let’s configure our `App.tsx` in the next section 

### Configuring `App.tsx`

First, we’d import all our actions and state from our `typedhooks`, initialize them in our `App.tsx`. Let’s do that below.

<div class="break-out">

<pre><code class="language-javascript">import { useEffect } from "react";
import { useStoreActions, useStoreState } from "./store/typehook";
import Header from "./components/header/Header";

const App = () =&gt; {
  const getAllCurrencies = useStoreActions(
    (actions) =&gt; actions.allCurrencies.getAllCurrencies
  );
  const getCurrencyRates = useStoreActions(
    (actions) =&gt; actions.currencyRates.getCurrencyRates
  );
  const currencyRates = useStoreState((state) =&gt; state.currencyRates.rates);
  const amountToConvert = useStoreState(
    (state) =&gt; state.conversion.data.amount
  );
  const currencyConvertingTo = useStoreState(
    (state) =&gt; state.conversion.data.to
  );

  useEffect(() =&gt; {
    getAllCurrencies();
    getCurrencyRates();
  }, [getAllCurrencies, getCurrencyRates]);

  const equivalence = () =&gt; {
    const val = Number(currencyRates[currencyConvertingTo]);
    return val * parseInt(amountToConvert);
  };

  return (
    &lt;div
      style={{ background: "#E9ECEF", height: "100vh" }}
      className="container-fluid"
    &gt;
      &lt;Header /&gt;
      &lt;div className="w-50 mx-auto"&gt;
        {amountToConvert && currencyConvertingTo ? &lt;h2&gt;Result:&lt;/h2&gt; : null}
        {amountToConvert ? (
          &lt;h3&gt;
            ${amountToConvert} = {equivalence()}
          &lt;/h3&gt;
        ) : null}
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default App;</code></pre>
</div>

Similar to what we did in our `typedhooks` file, in the code block above, we initialized all our store functions such as the `getAllCurrencies` and `getCurrencyRates` in this component. We used React `useEffect` hook to call the actions `getAllCurrencies` and `getCurrencyRates` from our store. 

Next, we initialized a function `equivalence` that converts the currency rates from an object and returning the value we get from the API and multiplies it by the amount inputted by the user as an integer. 

To conclude we used bootstrap and react strap to build components for our input. If done correctly, our app should look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c326f61-0cec-40b0-bbfc-048064529620/4-react-state-management-easy-peasy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c326f61-0cec-40b0-bbfc-048064529620/4-react-state-management-easy-peasy.png" width="800" height="426" sizes="100vw" caption="Easy peasy currency converter. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c326f61-0cec-40b0-bbfc-048064529620/4-react-state-management-easy-peasy.png'>Large preview</a>)" alt="easy peasy currency converter" >}}

### Conclusion

In this article, we learnt about Easy-Peasy, a state manager for React applications that focuses on providing better experience for developers. We also went through the process of creating a notes application using Easy-Peasy, to manage the state and also detailed the pros of using easy-peasy to manage state for your next application. Have fun using easy-peasy for your next React application. A working version of the notes  app can be found on [Codesandbox](https://codesandbox.io/s/awesome-meninsky-kjco6?file=/src/components/NotesForm.jsx), a working version of the currency converter can be found [here](https://codesandbox.io/s/dry-hooks-9qio1?file=/src/App.tsx). 

#### Resources

- [Easy Peasy docs](https://easy-peasy.now.sh/docs/introduction/)
- [Easy Peasy GitHub page](https://github.com/ctrlplusb/easy-peasy)
- [Easy Peasy The React Redux Wrapper](https://itnext.io/easy-peasy-the-react-redux-wrapper-b31a5911c5e3)
- [Easy Peasy global state with React Hooks](https://medium.com/@ctrlplusb/easy-peasy-global-state-in-react-w-hooks-421f5bf827cf)
- [Easy Peasy TypeScript](https://easy-peasy.now.sh/docs/tutorials/typescript.html)

{{< signature "ks, yk, il" >}}
