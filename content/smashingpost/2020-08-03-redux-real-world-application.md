---
title: 'Setting Up Redux For Use In A Real-World Application'
slug: redux-real-world-application
author: jerry-navi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb418b05-a190-4e3e-85f1-7ece1fa1039b/redux-real-world-application.png
date: 2020-08-03T11:00:00.000Z
summary: >-
  Redux is a robust state-management library for single-page JavaScript apps. It is described on the official documentation as a predictable state container for Javascript applications and it’s fairly simple to learn the concepts and implement Redux in a simple app. Going from a simple counter app to a real-world app, however, can be quite the jump.
description: >-
  Redux is a robust state-management library for single-page JavaScript apps. It is described on the official documentation as a predictable state container for Javascript applications and it’s fairly simple to learn the concepts and implement Redux in a simple app. Going from a simple counter app to a real-world app, however, can be quite the jump.
categories:
  - Apps
  - React
  - Redux
  - JavaScript
---

Redux is an important library in the React ecosystem, and almost the default to use when working on React applications that involve state management. As such, the importance of knowing how it works cannot be overestimated.

This guide will walk the reader through setting up Redux in a fairly complex React application and introduce the reader to “best practices” configuration along the way. It will be beneficial to beginners especially, and anyone who wants to fill in the gaps in their knowledge of Redux.

## Introducing Redux

Redux is a library that aims to solve the problem of state management in JavaScript apps by imposing restrictions on how and when state updates can happen. These restrictions are formed from Redux’s “three principles” which are:

- **Single source of truth**  
All of your application’s `state` is held in a Redux `store`. This state can be represented visually as a tree with a single ancestor, and the store provides methods for reading the current state and subscribing to changes from anywhere within your app.

- **State is read-only**  
The only way to change the state is to send the data as a plain object, called an action. You can think about actions as a way of saying to the state, "I have some data I would like to insert/update/delete".

- **Changes are made with pure functions**  
To change your app’s state, you write a function that takes the previous state and an action and returns a new state object as the next state. This function is called a [`reducer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce), and it is a pure function because it returns the same output for a given set of inputs.

The last principle is the most important in Redux, and this is where the magic of Redux happens. Reducer functions must not contain unpredictable code, or perform side-effects such as network requests, and should not directly mutate the state object.

Redux is a great tool, as we’ll learn later in this guide, but it doesn’t come without its challenges or tradeoffs. To help make the process of writing Redux efficient and more enjoyable, the Redux team offers a toolkit that abstracts over the process of setting up a Redux store and provides helpful Redux add-ons and utilities that help to simplify application code. For example, the library uses [Immer.js](https://immerjs.github.io/immer/), a library that makes it possible for you to write “mutative” immutable update logic, under the hood.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2020/06/better-reducers-with-immer/">Better Reducers With Immer</a></em></p>

In this guide, we will explore Redux by building an application that lets authenticated users create and manage digital diaries.

{{% feature-panel %}}

## Building Diaries.app

As stated in the previous section, we will be taking a closer look at Redux by building an app that lets users create and manage diaries. We will be building our application using React, and we’ll set up Mirage as our API mocking server since we won’t have access to a real server in this guide.

- [See source code](https://github.com/jerrynavi/diaries-app) (GitHub repo)

### Starting a Project and Installing Dependencies

Let’s get started on our project. First, bootstrap a new React application using `create-react-app`:

Using npx:

<pre><code class="language-bash">npx create-react-app diaries-app --template typescript
</code></pre>

We are starting with the TypeScript template, as we can improve our development experience by writing type-safe code.

Now, let’s install the dependencies we’ll be needing. Navigate into your newly created project directory

<pre><code class="language-bash">cd diaries-app
</code></pre>

And run the following commands:

<pre><code class="language-bash">npm install --save redux react-redux @reduxjs/toolkit
</code></pre>

<div class="break-out">

<pre><code class="language-bash">npm install --save axios react-router-dom react-hook-form yup dayjs markdown-to-jsx sweetalert2
</code></pre>
</div>

<div class="break-out">

<pre><code class="language-bash">npm install --save-dev miragejs @types/react-redux @types/react-router-dom @types/yup @types/markdown-to-jsx
</code></pre>
</div>
    
The first command will install Redux, React-Redux (official React bindings for Redux), and the Redux toolkit.

The second command installs some extra packages which will be useful for the app we’ll be building but are not required to work with Redux.

The last command installs Mirage and type declarations for the packages we installed as devDependencies.

### Describing the Application’s Initial State

Let’s go over our application’s requirements in detail. The application will allow authenticated users to create or modify existing diaries. Diaries are private by default, but they can be made public. Finally, diary entries will be sorted by their last modified date.

This relationship should look something like this:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f2121c-7b89-4f45-a808-5359671e44b7/fig-01-application-data-model.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f2121c-7b89-4f45-a808-5359671e44b7/fig-01-application-data-model.png" sizes="100vw" caption="An Overview of the Application’s Data Model. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f2121c-7b89-4f45-a808-5359671e44b7/fig-01-application-data-model.png'>Large preview</a>)" alt="" >}}

Armed with this information, we can now model our application’s state. First, we will create an interface for each of the following resources: `User`, `Diary` and `DiaryEntry`. Interfaces in Typescript describe the *shape* of an object.

Go ahead and create a new directory named `interfaces` in your app’s `src` sub-directory:

<pre><code class="language-bash">cd src && mkdir interfaces
</code></pre>

Next, run the following commands in the directory you just created:

<pre><code class="language-bash">touch entry.interface.ts
touch diary.interface.ts
touch user.interface.ts
</code></pre>
    
This will create three files named **entry.interface.ts**, **diary.interface.ts** and **user.interface.ts** respectively. I prefer to keep interfaces that would be used in multiple places across my app in a single location.

Open **entry.interface.ts** and add the following code to set up the `Entry` interface:

<pre><code class="language-ts">export interface Entry {
  id?: string;
  title: string;
  content: string;
  createdAt?: string;
  updatedAt?: string;
  diaryId?: string;
}
</code></pre>
    
A typical diary entry will have a title and some content, as well as information about when it was created or last updated. We’ll get back to the `diaryId` property later.

Next, add the following to **diary.interface.ts**:

<pre><code class="language-ts">export interface Diary {
  id?: string;
  title: string;
  type: 'private' | 'public';
  createdAt?: string;
  updatedAt?: string;
  userId?: string;
  entryIds: string[] | null;
}
</code></pre>

Here, we have a `type` property which expects an exact value of either ‘private’ or ‘public’, as diaries must be either private or public. Any other value will throw an error in the TypeScript compiler.

We can now describe our `User` object in the **user.interface.ts** file as follows:

<pre><code class="language-ts">export interface User {
  id?: string;
  username: string;
  email: string;
  password?: string;
  diaryIds: string[] | null;
}
</code></pre>
   
With our type definitions finished and ready to be used across our app, let’s setup our mock API server using Mirage.

### Setting up API Mocking with MirageJS

Since this tutorial is focused on Redux, we will not go into the details of setting up and using Mirage in this section. Please check out [this excellent series](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/) if you would like to learn more about Mirage.

To get started, navigate to your `src` directory and create a file named `server.ts` by running the following commands:

<pre><code class="language-ts">mkdir -p services/mirage
cd services/mirage

# ~/diaries-app/src/services/mirage
touch server.ts
</code></pre>
    
Next, open the `server.ts` file and add the following code:

<div class="break-out">

<pre><code class="language-ts">import { Server, Model, Factory, belongsTo, hasMany, Response } from 'miragejs';

export const handleErrors = (error: any, message = 'An error ocurred') =&gt; {
  return new Response(400, undefined, {
    data: {
      message,
      isError: true,
    },
  });
};

export const setupServer = (env?: string): Server =&gt; {
  return new Server({
    environment: env ?? 'development',

    models: {
      entry: Model.extend({
        diary: belongsTo(),
      }),
      diary: Model.extend({
        entry: hasMany(),
        user: belongsTo(),
      }),
      user: Model.extend({
        diary: hasMany(),
      }),
    },

    factories: {
      user: Factory.extend({
        username: 'test',
        password: 'password',
        email: 'test@email.com',
      }),
    },

    seeds: (server): any => {
      server.create('user');
    },

    routes(): void {
      this.urlPrefix = 'https://diaries.app';
    },
  });
};
</code></pre>
</div>

In this file, we are exporting two functions. A utility function for handling errors, and `setupServer()`, which returns a new server instance. The `setupServer()` function takes an optional argument which can be used to change the server’s environment. You can use this to set up Mirage for testing later.

We have also defined three models in the server’s `models` property: `User`, `Diary` and `Entry`. Remember that earlier we set up the `Entry` interface with a property named `diaryId`. This value will be automatically set to the `id` the entry is being saved to. Mirage uses this property to establish a relationship between an `Entry` and a `Diary`. The same thing also happens when a user creates a new diary: `userId` is automatically set to that user’s id.

We seeded the database with a default user and configured Mirage to intercept all requests from our app starting with `https://diaries.app`. Notice that we haven’t configured any [route handlers](https://miragejs.com/docs/main-concepts/route-handlers/) yet. Let’s go ahead and create a few.

Ensure that you are in the **src/services/mirage** directory, then create a new directory named **routes** using the following command:

<pre><code class="language-ts"># ~/diaries-app/src/services/mirage
mkdir routes
</code></pre>

`cd` to the newly created directory and create a file named **user.ts**:

<pre><code class="language-ts">cd routes
touch user.ts
</code></pre>
 
Next, paste the following code in the `user.ts` file:

<div class="break-out">

<pre><code class="language-ts">import { Response, Request } from 'miragejs';
import { handleErrors } from '../server';
import { User } from '../../../interfaces/user.interface';
import { randomBytes } from 'crypto';

const generateToken = () =&gt; randomBytes(8).toString('hex');

export interface AuthResponse {
  token: string;
  user: User;
}

const login = (schema: any, req: Request): AuthResponse | Response =&gt; {
  const { username, password } = JSON.parse(req.requestBody);
  const user = schema.users.findBy({ username });
  if (!user) {
    return handleErrors(null, 'No user with that username exists');
  }
  if (password !== user.password) {
    return handleErrors(null, 'Password is incorrect');
  }
  const token = generateToken();
  return {
    user: user.attrs as User,
    token,
  };
};

const signup = (schema: any, req: Request): AuthResponse | Response =&gt; {
  const data = JSON.parse(req.requestBody);
  const exUser = schema.users.findBy({ username: data.username });
  if (exUser) {
    return handleErrors(null, 'A user with that username already exists.');
  }
  const user = schema.users.create(data);
  const token = generateToken();
  return {
    user: user.attrs as User,
    token,
  };
};

export default {
  login,
  signup,
};
</code></pre>
</div>

The `login` and `signup` methods here receive a `Schema` class and a fake `Request` object and, upon validating the password or checking that the login does not already exist, return the existing user or a new user respectively. We use the `Schema` object to interact with Mirage’s ORM, while the `Request` object contains information about the intercepted request including the request body and headers.

Next, let’s add methods for working with diaries and diary entries. Create a file named **diary.ts** in your **routes** directory:

<pre><code class="language-ts">touch diary.ts
</code></pre>    

Update the file with the following methods for working with `Diary` resources:

<div class="break-out">

<pre><code class="language-ts">export const create = (
  schema: any,
  req: Request
): { user: User; diary: Diary } | Response =&gt; {
  try {
    const { title, type, userId } = JSON.parse(req.requestBody) as Partial&lt;
      Diary
    &gt;;
    const exUser = schema.users.findBy({ id: userId });
    if (!exUser) {
      return handleErrors(null, 'No such user exists.');
    }
    const now = dayjs().format();
    const diary = exUser.createDiary({
      title,
      type,
      createdAt: now,
      updatedAt: now,
    });
    return {
      user: {
        ...exUser.attrs,
      },
      diary: diary.attrs,
    };
  } catch (error) {
    return handleErrors(error, 'Failed to create Diary.');
  }
};

export const updateDiary = (schema: any, req: Request): Diary | Response =&gt; {
  try {
    const diary = schema.diaries.find(req.params.id);
    const data = JSON.parse(req.requestBody) as Partial&lt;Diary&gt;;
    const now = dayjs().format();
    diary.update({
      ...data,
      updatedAt: now,
    });
    return diary.attrs as Diary;
  } catch (error) {
    return handleErrors(error, 'Failed to update Diary.');
  }
};

export const getDiaries = (schema: any, req: Request): Diary[] | Response =&gt; {
  try {
    const user = schema.users.find(req.params.id);
    return user.diary as Diary[];
  } catch (error) {
    return handleErrors(error, 'Could not get user diaries.');
  }
};
</code></pre>
</div>
   
Next, let’s add some methods for working with diary entries:

<div class="break-out">

<pre><code class="language-ts">export const addEntry = (
  schema: any,
  req: Request
): { diary: Diary; entry: Entry } | Response =&gt; {
  try {
    const diary = schema.diaries.find(req.params.id);
    const { title, content } = JSON.parse(req.requestBody) as Partial&lt;Entry&gt;;
    const now = dayjs().format();
    const entry = diary.createEntry({
      title,
      content,
      createdAt: now,
      updatedAt: now,
    });
    diary.update({
      ...diary.attrs,
      updatedAt: now,
    });
    return {
      diary: diary.attrs,
      entry: entry.attrs,
    };
  } catch (error) {
    return handleErrors(error, 'Failed to save entry.');
  }
};

export const getEntries = (
  schema: any,
  req: Request
): { entries: Entry[] } | Response =&gt; {
  try {
    const diary = schema.diaries.find(req.params.id);
    return diary.entry;
  } catch (error) {
    return handleErrors(error, 'Failed to get Diary entries.');
  }
};

export const updateEntry = (schema: any, req: Request): Entry | Response =&gt; {
  try {
    const entry = schema.entries.find(req.params.id);
    const data = JSON.parse(req.requestBody) as Partial&lt;Entry&gt;;
    const now = dayjs().format();
    entry.update({
      ...data,
      updatedAt: now,
    });
    return entry.attrs as Entry;
  } catch (error) {
    return handleErrors(error, 'Failed to update entry.');
  }
};
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

Finally, let’s add the necessary imports at the top of the file:

<pre><code class="language-ts">import { Response, Request } from 'miragejs';
import { handleErrors } from '../server';
import { Diary } from '../../../interfaces/diary.interface';
import { Entry } from '../../../interfaces/entry.interface';
import dayjs from 'dayjs';
import { User } from '../../../interfaces/user.interface';
</code></pre>
   
In this file, we have exported methods for working with the `Diary` and `Entry` models. In the `create` method, we call a method named `user.createDiary()` to save a new diary and associate it to a user account.

The `addEntry` and `updateEntry` methods create and correctly associate a new entry to a diary or update an existing entry’s data respectively. The latter also updates the entry’s `updatedAt` property with the current timestamp. The `updateDiary` method also updates a diary with the timestamp the change was made. Later, we’ll be sorting the records we receive from our network request with this property.

We also have a `getDiaries` method which retrieves a user’s diaries and a `getEntries` methods which retrieves a selected diary’s entries.

We can now update our server to use the methods we just created. Open **server.ts** to include the files:

<div class="break-out">

<pre><code class="language-ts">import { Server, Model, Factory, belongsTo, hasMany, Response } from 'miragejs';

import user from './routes/user';
import * as diary from './routes/diary';
</code></pre>
</div>
   
Then, update the server’s `route` property with the routes we want to handle:

<pre><code class="language-ts">export const setupServer = (env?: string): Server =&gt; {
  return new Server({
    // ...
    routes(): void {
      this.urlPrefix = 'https://diaries.app';

      this.get('/diaries/entries/:id', diary.getEntries);
      this.get('/diaries/:id', diary.getDiaries);

      this.post('/auth/login', user.login);
      this.post('/auth/signup', user.signup);

      this.post('/diaries/', diary.create);
      this.post('/diaries/entry/:id', diary.addEntry);

      this.put('/diaries/entry/:id', diary.updateEntry);
      this.put('/diaries/:id', diary.updateDiary);
    },
  });
};
</code></pre>
    
With this change, when a network request from our app matches one of the route handlers, Mirage intercepts the request and invokes the respective route handler functions.

Next, we’ll proceed to make our application aware of the server. Open **src/index.tsx** and import the `setupServer()` method:

<pre><code class="language-ts">import { setupServer } from './services/mirage/server';
</code></pre>

And add the following code before `ReactDOM.render()`:

<pre><code class="language-ts">if (process.env.NODE_ENV === 'development') {
  setupServer();
}
</code></pre>
   
The check in the code block above ensures that our Mirage server will run only while we are in development mode.

One last thing we need to do before moving on to the Redux bits is configure a custom [Axios instance](https://www.npmjs.com/package/axios#creating-an-instance) for use in our app. This will help to reduce the amount of code we’ll have to write later on.

Create a file named **api.ts** under src/services and add the following code to it:

<div class="break-out">

<pre><code class="language-ts">import axios, { AxiosInstance, AxiosResponse, AxiosError } from 'axios';
import { showAlert } from '../util';

const http: AxiosInstance = axios.create({
  baseURL: 'https://diaries.app',
});

http.defaults.headers.post['Content-Type'] = 'application/json';

http.interceptors.response.use(
  async (response: AxiosResponse): Promise<any> =&gt; {
    if (response.status &gt;= 200 && response.status &lt; 300) {
      return response.data;
    }
  },
  (error: AxiosError) =&gt; {
    const { response, request }: {
      response?: AxiosResponse;
      request?: XMLHttpRequest;
    } = error;
    if (response) {
      if (response.status &gt;= 400 && response.status &lt; 500) {
        showAlert(response.data?.data?.message, 'error');
        return null;
      }
    } else if (request) {
      showAlert('Request failed. Please try again.', 'error');
      return null;
    }
    return Promise.reject(error);
  }
);

export default http;
</code></pre>
</div>

In this file, we are exporting an Axios instance modified to include our app’s API url, https://diaries.app. We have configured an interceptor to handle success and error responses, and we display error messages using a `sweetalert` toast which we will configure in the next step.

Create a file named `util.ts` in your src directory and paste the following code in it:

<div class="break-out">

<pre><code class="language-ts">import Swal, { SweetAlertIcon } from 'sweetalert2';

export const showAlert = (titleText = 'Something happened.', alertType?: SweetAlertIcon): void =&gt; {
  Swal.fire({
    titleText,
    position: 'top-end',
    timer: 3000,
    timerProgressBar: true,
    toast: true,
    showConfirmButton: false,
    showCancelButton: true,
    cancelButtonText: 'Dismiss',
    icon: alertType,
    showClass: {
      popup: 'swal2-noanimation',
      backdrop: 'swal2-noanimation',
    },
    hideClass: {
      popup: '',
      backdrop: '',
    },
  });
};
</code></pre>
</div>

This file exports a function that displays a toast whenever it is invoked. The function accepts parameters to allow you set the toast message and type. For example, we are showing an error toast in the Axios response error interceptor like this:

<pre><code class="language-ts">showAlert(response.data?.data?.message, 'error');
</code></pre>

Now when we make requests from our app while in development mode, they will be intercepted and handled by Mirage instead. In the next section, we will set up our Redux store using Redux toolkit.

### Setting up a Redux Store

In this section, we are going to set up our store using the following exports from Redux toolkit: `configureStore()`, `getDefaultMiddleware()` and `createSlice()`. Before we start, we should take a detailed look at what these exports do.

`configureStore()` is an abstraction over the Redux `createStore()` function that helps simplify your code. It uses `createStore()` internally to set up your store with some useful development tools:

<div class="break-out">

<pre><code class="language-ts">export const store = configureStore({
  reducer: rootReducer, // a single reducer function or an object of slice reducers
});
</code></pre>
</div>

The `createSlice()` function helps simplify the process of creating action creators and slice reducers. It accepts an initial state, an object full of reducer functions, and a "slice name", and automatically generates action creators and action types corresponding to the reducers and your state. It also returns a single reducer function, which can be passed to Redux’s `combineReducers()` function as a “slice reducer”.

Remember that the state is a single tree, and a single root reducer manages changes to that tree. For maintainability, it is recommended to split your root reducer into “slices,” and have a "slice reducer" provide an initial value and calculate the updates to a corresponding slice of the state. These slices can be joined into a single reducer function by using `combineReducers()`.

There are additional options for [configuring the store](https://redux-toolkit.js.org/api/configureStore#parameters). For example, you can pass an array of your own middleware to `configureStore()` or start up your app from a saved state using the `preloadedState` option. When you supply the `middleware` option, you have to define *all* the middleware you want added to the store. If you would like to retain the defaults when setting up your store, you can use `getDefaultMiddleware()` to get the default list of middleware:

<pre><code class="language-ts">export const store = configureStore({
  // ...
  middleware: [...getDefaultMiddleware(), customMiddleware],
});
</code></pre>

Let’s now proceed to set up our store. We will adopt a [“ducks-style”](https://github.com/erikras/ducks-modular-redux) approach to structuring our files, specifically following the guidelines in practice from the [Github Issues](https://github.com/reduxjs/rtk-github-issues-example) sample app. We will be organizing our code such that related components, as well as actions and reducers, live in the same directory. The final state object will look like this:

<pre><code class="language-ts">type RootState = {
  auth: {
    token: string | null;
    isAuthenticated: boolean;
  };
  diaries: Diary[];
  entries: Entry[];
  user: User | null;
  editor: {
    canEdit: boolean;
    currentlyEditing: Entry | null;
    activeDiaryId: string | null;
  };
}
</code></pre>

To get started, create a new directory named **features** under your **src** directory:

<pre><code class="language-ts"># ~/diaries-app/src
mkdir features
</code></pre>

Then, `cd` into features and create directories named **auth**, **diary** and **entry**:

<pre><code class="language-ts">cd features
mkdir auth diary entry
</code></pre>
   
`cd` into the auth directory and create a file named **authSlice.ts**:

<pre><code class="language-ts">cd auth
# ~/diaries-app/src/features/auth
touch authSlice.ts
</code></pre>

Open the file and paste the following in it:

<div class="break-out">

<pre><code class="language-ts">import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface AuthState {
  token: string | null;
  isAuthenticated: boolean;
}

const initialState: AuthState = {
  token: null,
  isAuthenticated: false,
};

const auth = createSlice({
  name: 'auth',
  initialState,
  reducers: {
    saveToken(state, { payload }: PayloadAction<string>) {
      if (payload) {
        state.token = payload;
      }
    },
    clearToken(state) {
      state.token = null;
    },
    setAuthState(state, { payload }: PayloadAction<boolean>) {
      state.isAuthenticated = payload;
    },
  },
});

export const { saveToken, clearToken, setAuthState } = auth.actions;
export default auth.reducer;
</code></pre>
</div>

In this file, we’re creating a slice for the `auth` property of our app’s state using the `createSlice()` function introduced earlier. The `reducers` property holds a map of reducer functions for updating values in the auth slice. The returned object contains automatically generated action creators and a single slice reducer. We would need to use these in other files so, following the “ducks pattern”, we do named exports of the action creators, and a default export of the reducer function.

Let’s set up the remaining reducer slices according to the app state we saw earlier. First, create a file named **userSlice.ts** in the auth directory and add the following code to it:

<pre><code class="language-ts">import { createSlice, PayloadAction } from '@reduxjs/toolkit';
import { User } from '../../interfaces/user.interface';

const user = createSlice({
  name: 'user',
  initialState: null as User | null,
  reducers: {
    setUser(state, { payload }: PayloadAction&lt;User | null&gt;) {
      return state = (payload != null) ? payload : null;
    },
  },
});

export const { setUser } = user.actions;
export default user.reducer;
</code></pre>

This creates a slice reducer for the `user` property in our the application’s store. The `setUser` reducer function accepts a payload containing user data and updates the state with it. When no data is passed, we set the state’s user property to `null`.
 
Next, create a file named **diariesSlice.ts** under **src/features/diary**:

<pre><code class="language-ts"># ~/diaries-app/src/features
cd diary
touch diariesSlice.ts
</code></pre>

Add the following code to the file:

<div class="break-out">

<pre><code class="language-ts">import { createSlice, PayloadAction } from '@reduxjs/toolkit';
import { Diary } from '../../interfaces/diary.interface';

const diaries = createSlice({
  name: 'diaries',
  initialState: [] as Diary[],
  reducers: {
    addDiary(state, { payload }: PayloadAction&lt;Diary[]&gt;) {
      const diariesToSave = payload.filter((diary) =&gt; {
        return state.findIndex((item) =&gt; item.id === diary.id) === -1;
      });
      state.push(...diariesToSave);
    },
    updateDiary(state, { payload }: PayloadAction&lt;Diary&gt;) {
      const { id } = payload;
      const diaryIndex = state.findIndex((diary) =&gt; diary.id === id);
      if (diaryIndex !== -1) {
        state.splice(diaryIndex, 1, payload);
      }
    },
  },
});

export const { addDiary, updateDiary } = diaries.actions;
export default diaries.reducer;
</code></pre>
</div>

The “diaries” property of our state is an array containing the user’s diaries, so our reducer functions here all work on the state object they receive using array methods. Notice here that we are writing normal “mutative” code when working on the state. This is possible because the reducer functions we create using the `createSlice()` method are wrapped with Immer’s `produce()` method. This results in Immer returning a correct immutably updated result for our state regardless of us writing mutative code.

Next, create a file named **entriesSlice.ts** under **src/features/entry**:

<pre><code class="language-ts"># ~/diaries-app/src/features
mkdir entry
cd entry
touch entriesSlice.ts
</code></pre>

Open the file and add the following code:

<pre><code class="language-ts">import { createSlice, PayloadAction } from '@reduxjs/toolkit';
import { Entry } from '../../interfaces/entry.interface';

const entries = createSlice({
  name: 'entries',
  initialState: [] as Entry[],
  reducers: {
    setEntries(state, { payload }: PayloadAction&lt;Entry[] | null&gt;) {
      return (state = payload != null ? payload : []);
    },
    updateEntry(state, { payload }: PayloadAction&lt;Entry&gt;) {
      const { id } = payload;
      const index = state.findIndex((e) =&gt; e.id === id);
      if (index !== -1) {
        state.splice(index, 1, payload);
      }
    },
  },
});

export const { setEntries, updateEntry } = entries.actions;
export default entries.reducer;
</code></pre>

The reducer functions here have logic similar to the previous slice’s reducer functions. The `entries` property is also an array, but it only holds entries for a single diary. In our app, this will be the diary currently in the user’s focus.

Finally, create a file named editorSlice.ts in src/features/entry and add the following to it:

<div class="break-out">

<pre><code class="language-ts">import { createSlice, PayloadAction } from '@reduxjs/toolkit';
import { Entry } from '../../interfaces/entry.interface';

interface EditorState {
  canEdit: boolean;
  currentlyEditing: Entry | null;
  activeDiaryId: string | null;
}

const initialState: EditorState = {
  canEdit: false,
  currentlyEditing: null,
  activeDiaryId: null,
};

const editor = createSlice({
  name: 'editor',
  initialState,
  reducers: {
    setCanEdit(state, { payload }: PayloadAction&lt;boolean&gt;) {
      state.canEdit = payload != null ? payload : !state.canEdit;
    },
    setCurrentlyEditing(state, { payload }: PayloadAction&lt;Entry | null&gt;) {
      state.currentlyEditing = payload;
    },
    setActiveDiaryId(state, { payload }: PayloadAction&lt;string&gt;) {
      state.activeDiaryId = payload;
    },
  },
});

export const { setCanEdit, setCurrentlyEditing, setActiveDiaryId } = editor.actions;
export default editor.reducer;
</code></pre>
</div>

Here, we have a slice for the `editor` property in state. We’ll be using the properties in this object to check if the user wants to switch to editing mode, which diary the edited entry belongs to, and what entry is going to be edited.

To put it all together, create a file named **rootReducer.ts** in the src directory with the following content:

<pre><code class="language-ts">import { combineReducers } from '@reduxjs/toolkit';
import authReducer from './features/auth/authSlice';
import userReducer from './features/auth/userSlice';
import diariesReducer from './features/diary/diariesSlice';
import entriesReducer from './features/entry/entriesSlice';
import editorReducer from './features/entry/editorSlice';

const rootReducer = combineReducers({
  auth: authReducer,
  diaries: diariesReducer,
  entries: entriesReducer,
  user: userReducer,
  editor: editorReducer,
});

export type RootState = ReturnType&lt;typeof rootReducer&gt;;
export default rootReducer;
</code></pre>

In this file, we’ve combined our slice reducers into a single root reducer with the `combineReducers()` function. We’ve also exported the `RootState` type, which will be useful later when we’re selecting values from the store. We can now use the root reducer (the default export of this file) to set up our store.

Create a file named store.ts with the following contents:

<pre><code class="language-ts">import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './rootReducer';
import { useDispatch } from 'react-redux';

const store = configureStore({
  reducer: rootReducer,
});

type AppDispatch = typeof store.dispatch;
export const useAppDispatch = () =&gt; useDispatch&lt;AppDispatch&gt;();
export default store;
</code></pre>

With this, we’ve created a store using the `configureStore()` export from Redux toolkit. We’ve also exported an hook called `useAppDispatch()` which merely returns a typed [`useDispatch()`](https://react-redux.js.org/api/hooks#usedispatch) hook.

Next, update the imports in index.tsx to look like the following:

<pre><code class="language-ts">import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './app/App';
import * as serviceWorker from './serviceWorker';
import { setupServer } from './services/mirage/server';
import { Provider } from 'react-redux';
import store from './store';
// ...
</code></pre>
 
Finally, make the `store` available to the app’s components by wrapping `<App />` (the top-level component) with `<Provider />`:

<pre><code class="language-ts">ReactDOM.render(
  &lt;React.StrictMode&gt;
    &lt;Provider store={store}&gt;
      &lt;App /&gt;
    &lt;/Provider&gt;
  &lt;/React.StrictMode&gt;,
  document.getElementById('root')
);
</code></pre>

Now, if you start your app and you navigate to https://localhost:3000 with the [Redux Dev Tools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd) extension enabled, you should see the following in your app’s state:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147528a7-3b45-4f54-836a-a134da707b54/fig-02-application-initial-state-in-redux-dev-tools-extension.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147528a7-3b45-4f54-836a-a134da707b54/fig-02-application-initial-state-in-redux-dev-tools-extension.png" sizes="100vw" caption="Initial State in Redux Dev Tools Extension. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147528a7-3b45-4f54-836a-a134da707b54/fig-02-application-initial-state-in-redux-dev-tools-extension.png'>Large preview</a>)" alt="" >}}

Great work so far, but we’re not quite finished yet. In the next section, we will design the app’s User Interface and add functionality using the store we’ve just created.

{{% ad-panel-leaderboard %}}

## Designing The Application User Interface

To see Redux in action, we are going to build a demo app. In this section, we will connect our components to the store we’ve created and learn to dispatch actions and modify the state using reducer functions. We will also learn how to read values from the store. Here’s what our Redux-powered application will look like.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea2add0-730a-475e-9f47-bc0a8ff54e6b/fig-03-final-app-home-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea2add0-730a-475e-9f47-bc0a8ff54e6b/fig-03-final-app-home-page.png" sizes="100vw" caption="Home page showing an authenticated user’s diaries. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea2add0-730a-475e-9f47-bc0a8ff54e6b/fig-03-final-app-home-page.png'>Large preview</a>)" alt="" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1abbde2-fd45-4a3d-91c4-25e4a9de28ac/fig-04-final-app-diary-entries-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1abbde2-fd45-4a3d-91c4-25e4a9de28ac/fig-04-final-app-diary-entries-page.png" sizes="100vw" caption="Screenshots of final app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1abbde2-fd45-4a3d-91c4-25e4a9de28ac/fig-04-final-app-diary-entries-page.png'>Large preview</a>)" alt="" >}}

### Setting up the Authentication Feature

To get started, move **App.tsx** and its related files from the **src** directory to its own directory like this:

<pre><code class="language-ts"># ~/diaries-app/src
mkdir app
mv App.tsx App.test.tsx app
</code></pre>

You can delete the App.css and logo.svg files as we won’t be needing them.

Next, open the App.tsx file and replace its contents with the following:

<div class="break-out">

<pre><code class="language-ts">import React, { FC, lazy, Suspense } from 'react';
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom';
import { useSelector } from 'react-redux';
import { RootState } from '../rootReducer';

const Auth = lazy(() =&gt; import('../features/auth/Auth'));
const Home = lazy(() =&gt; import('../features/home/Home'));

const App: FC = () =&gt; {
  const isLoggedIn = useSelector(
    (state: RootState) =&gt; state.auth.isAuthenticated
  );
  return (
    &lt;Router&gt;
      &lt;Switch&gt;
        &lt;Route path="/"&gt;
          &lt;Suspense fallback={&lt;p&gt;Loading...&lt;/p&gt;}&gt;
            {isLoggedIn ? &lt;Home /&gt; : &lt;Auth /&gt;}
          &lt;/Suspense&gt;
        &lt;/Route&gt;
      &lt;/Switch&gt;
    &lt;/Router&gt;
  );
};

export default App;
</code></pre>
</div>

Here we have set up our app to render an `<Auth />` component if the user is unauthenticated, or otherwise render a `<Home />` component. We haven’t created either of these components yet, so let’s fix that. Create a file named **Auth.tsx** under src/features/auth and add the following contents to the file:

<div class="break-out">

<pre><code class="language-ts">import React, { FC, useState } from 'react';
import { useForm } from 'react-hook-form';
import { User } from '../../interfaces/user.interface';
import * as Yup from 'yup';
import http from '../../services/api';
import { saveToken, setAuthState } from './authSlice';
import { setUser } from './userSlice';
import { AuthResponse } from '../../services/mirage/routes/user';
import { useAppDispatch } from '../../store';

const schema = Yup.object().shape({
  username: Yup.string()
    .required('What? No username?')
    .max(16, 'Username cannot be longer than 16 characters'),
  password: Yup.string().required('Without a password, "None shall pass!"'),
  email: Yup.string().email('Please provide a valid email address (abc@xy.z)'),
});

const Auth: FC = () =&gt; {
  const { handleSubmit, register, errors } = useForm&lt;User&gt;({
    validationSchema: schema,
  });
  const [isLogin, setIsLogin] = useState(true);
  const [loading, setLoading] = useState(false);
  const dispatch = useAppDispatch();

  const submitForm = (data: User) =&gt; {
    const path = isLogin ? '/auth/login' : '/auth/signup';
    http
      .post&lt;User, AuthResponse&gt;(path, data)
      .then((res) =&gt; {
        if (res) {
          const { user, token } = res;
          dispatch(saveToken(token));
          dispatch(setUser(user));
          dispatch(setAuthState(true));
        }
      })
      .catch((error) =&gt; {
        console.log(error);
      })
      .finally(() =&gt; {
        setLoading(false);
      });
  };

  return (
    &lt;div className="auth"&gt;
      &lt;div className="card"&gt;
        &lt;form onSubmit={handleSubmit(submitForm)}&gt;
          &lt;div className="inputWrapper"&gt;
            &lt;input ref={register} name="username" placeholder="Username" /&gt;
            {errors && errors.username && (
              &lt;p className="error"&gt;{errors.username.message}&lt;/p&gt;
            )}
          &lt;/div&gt;
          &lt;div className="inputWrapper"&gt;
            &lt;input
              ref={register}
              name="password"
              type="password"
              placeholder="Password"
            /&gt;
            {errors && errors.password && (
              &lt;p className="error"&gt;{errors.password.message}&lt;/p&gt;
            )}
          &lt;/div&gt;
          {!isLogin && (
            &lt;div className="inputWrapper"&gt;
              &lt;input
                ref={register}
                name="email"
                placeholder="Email (optional)"
              /&gt;
              {errors && errors.email && (
                &lt;p className="error"&gt;{errors.email.message}&lt;/p&gt;
              )}
            &lt;/div&gt;
          )}
          &lt;div className="inputWrapper"&gt;
            &lt;button type="submit" disabled={loading}&gt;
              {isLogin ? 'Login' : 'Create account'}
            &lt;/button&gt;
          &lt;/div&gt;
          &lt;p
            onClick={() =&gt; setIsLogin(!isLogin)}
            style={{ cursor: 'pointer', opacity: 0.7 }}
          &gt;
            {isLogin ? 'No account? Create one' : 'Already have an account?'}
          &lt;/p&gt;
        &lt;/form&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default Auth;
</code></pre>
</div>

In this component, we have set up a form for users to log in, or to create an account. Our form fields are validated using [Yup](https://github.com/jquense/yup) and, on successfully authenticating a user, we use our `useAppDispatch` hook to dispatch the relevant actions. You can see the dispatched actions and the changes made to your state in the Redux DevTools Extension:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b68c944c-717f-40f9-ae77-ec83a0219dc4/06-dispatched-actions-changes-tracked-in-redux-dev-tools-extensions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b68c944c-717f-40f9-ae77-ec83a0219dc4/06-dispatched-actions-changes-tracked-in-redux-dev-tools-extensions.png" sizes="100vw" caption="Dispatched Actions with Changes Tracked in Redux Dev Tools Extensions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b68c944c-717f-40f9-ae77-ec83a0219dc4/06-dispatched-actions-changes-tracked-in-redux-dev-tools-extensions.png'>Large preview</a>)" alt="" >}}

Finally, create a file named **Home.tsx** under **src/features/home** and add the following code to the file:

<pre><code class="language-ts">import React, { FC } from 'react';

const Home: FC = () =&gt; {
  return (
    &lt;div&gt;
      &lt;p&gt;Welcome user!&lt;/p&gt;
    &lt;/div&gt;
  );
};

export default Home;
</code></pre>

For now, we are just displaying some text to the authenticated user. As we build the rest of our application, we will be updating this file.

### Setting up the Editor

The next component we are going to build is the editor. Though basic, we will enable support for rendering markdown content using the `markdown-to-jsx` library we installed earlier.

First, create a file named **Editor.tsx** in the src/features/entry directory. Then, add the following code to the file:

<div class="break-out">

<pre><code class="language-ts">import React, { FC, useState, useEffect } from 'react';
import { useSelector } from 'react-redux';
import { RootState } from '../../rootReducer';
import Markdown from 'markdown-to-jsx';
import http from '../../services/api';
import { Entry } from '../../interfaces/entry.interface';
import { Diary } from '../../interfaces/diary.interface';
import { setCurrentlyEditing, setCanEdit } from './editorSlice';
import { updateDiary } from '../diary/diariesSlice';
import { updateEntry } from './entriesSlice';
import { showAlert } from '../../util';
import { useAppDispatch } from '../../store';

const Editor: FC = () =&gt; {
  const { currentlyEditing: entry, canEdit, activeDiaryId } = useSelector(
    (state: RootState) =&gt; state.editor
  );
  const [editedEntry, updateEditedEntry] = useState(entry);
  const dispatch = useAppDispatch();

  const saveEntry = async () =&gt; {
    if (activeDiaryId == null) {
      return showAlert('Please select a diary.', 'warning');
    }
    if (entry == null) {
      http
        .post&lt;Entry, { diary: Diary; entry: Entry }&gt;(
          `/diaries/entry/${activeDiaryId}`,
          editedEntry
        )
        .then((data) =&gt; {
          if (data != null) {
            const { diary, entry: _entry } = data;
            dispatch(setCurrentlyEditing(_entry));
            dispatch(updateDiary(diary));
          }
        });
    } else {
      http
        .put&lt;Entry, Entry&gt;(`diaries/entry/${entry.id}`, editedEntry)
        .then((_entry) =&gt; {
          if (_entry != null) {
            dispatch(setCurrentlyEditing(_entry));
            dispatch(updateEntry(_entry));
          }
        });
    }
    dispatch(setCanEdit(false));
  };

  useEffect(() =&gt; {
    updateEditedEntry(entry);
  }, [entry]);

  return (
    &lt;div className="editor"&gt;
      &lt;header
        style={{
          display: 'flex',
          flexWrap: 'wrap',
          alignItems: 'center',
          marginBottom: '0.2em',
          paddingBottom: '0.2em',
          borderBottom: '1px solid rgba(0,0,0,0.1)',
        }}
      &gt;
        {entry && !canEdit ? (
          &lt;h4&gt;
            {entry.title}
            &lt;a
              href="#edit"
              onClick={(e) =&gt; {
                e.preventDefault();
                if (entry != null) {
                  dispatch(setCanEdit(true));
                }
              }}
              style={{ marginLeft: '0.4em' }}
            &gt;
              (Edit)
            &lt;/a&gt;
          &lt;/h4&gt;
        ) : (
          &lt;input
            value={editedEntry?.title ?? ''}
            disabled={!canEdit}
            onChange={(e) =&gt; {
              if (editedEntry) {
                updateEditedEntry({
                  ...editedEntry,
                  title: e.target.value,
                });
              } else {
                updateEditedEntry({
                  title: e.target.value,
                  content: '',
                });
              }
            }}
          /&gt;
        )}
      &lt;/header&gt;
      {entry && !canEdit ? (
        &lt;Markdown&gt;{entry.content}&lt;/Markdown&gt;
      ) : (
        &lt;&gt;
          &lt;textarea
            disabled={!canEdit}
            placeholder="Supports markdown!"
            value={editedEntry?.content ?? ''}
            onChange={(e) =&gt; {
              if (editedEntry) {
                updateEditedEntry({
                  ...editedEntry,
                  content: e.target.value,
                });
              } else {
                updateEditedEntry({
                  title: '',
                  content: e.target.value,
                });
              }
            }}
          /&gt;
          &lt;button onClick={saveEntry} disabled={!canEdit}&gt;
            Save
          &lt;/button&gt;
        &lt;/&gt;
      )}
    &lt;/div&gt;
  );
};

export default Editor;
</code></pre>
</div>

Let’s break down what’s happening in the `Editor` component.

First, we are picking some values (with correctly inferred types) from the app’s state using the `useSelector()` hook from `react-redux`. In the next line, we have a stateful value called `editedEntry` whose initial value is set to the `editor.currentlyEditing` property we’ve selected from the store.

Next, we have the `saveEntry` function which updates or creates a new entry in the API, and dispatches the respective Redux action.

Finally, we have a `useEffect` that is fired when the `editor.currentlyEditing` property changes. Our editor’s UI (in the component’s return function) has been set up to respond to changes in the state. For example, rendering the entry’s content as JSX elements when the user isn’t editing.

With that, the app’s `Entry` feature should be completely set up. In the next section, we will finish building the `Diary` feature and then import the main components in the `Home` component we created earlier.

### Final Steps

To finish up our app, we will first create components for the `Diary` feature. Then, we will update the `Home` component with the primary exports from the `Diary` and `Entry` features. Finally, we will add some styling to give our app the required pizzazz!

Let’s start by creating a file in src/features/diary named **DiaryTile.tsx**. This component will present information about a diary and its entries, and allow the user to edit the diary’s title. Add the following code to the file:

<div class="break-out">

<pre><code class="language-ts">import React, { FC, useState } from 'react';
import { Diary } from '../../interfaces/diary.interface';
import http from '../../services/api';
import { updateDiary } from './diariesSlice';
import { setCanEdit, setActiveDiaryId, setCurrentlyEditing } from '../entry/editorSlice';
import { showAlert } from '../../util';
import { Link } from 'react-router-dom';
import { useAppDispatch } from '../../store';

interface Props {
  diary: Diary;
}

const buttonStyle: React.CSSProperties = {
  fontSize: '0.7em',
  margin: '0 0.5em',
};

const DiaryTile: FC&lt;Props> = (props) =&gt; {
  const [diary, setDiary] = useState(props.diary);
  const [isEditing, setIsEditing] = useState(false);
  const dispatch = useAppDispatch();
  const totalEntries = props.diary?.entryIds?.length;

  const saveChanges = () =&gt; {
    http
      .put&lt;Diary, Diary&gt;(`/diaries/${diary.id}`, diary)
      .then((diary) =&gt; {
        if (diary) {
          dispatch(updateDiary(diary));
          showAlert('Saved!', 'success');
        }
      })
      .finally(() =&gt; {
        setIsEditing(false);
      });
  };

  return (
    &lt;div className="diary-tile"&gt;
      &lt;h2
        className="title"
        title="Click to edit"
        onClick={() =&gt; setIsEditing(true)}
        style={{
          cursor: 'pointer',
        }}
      &gt;
        {isEditing ? (
          &lt;input
            value={diary.title}
            onChange={(e) =&gt; {
              setDiary({
                ...diary,
                title: e.target.value,
              });
            }}
            onKeyUp={(e) =&gt; {
              if (e.key === 'Enter') {
                saveChanges();
              }
            }}
          /&gt;
        ) : (
          &lt;span&gt;{diary.title}&lt;/span&gt;
        )}
      &lt;/h2&gt;
      &lt;p className="subtitle"&gt;{totalEntries ?? '0'} saved entries&lt;/p&gt;
      &lt;div style={{ display: 'flex' }}&gt;
        &lt;button
          style={buttonStyle}
          onClick={() =&gt; {
            dispatch(setCanEdit(true));
            dispatch(setActiveDiaryId(diary.id as string));
            dispatch(setCurrentlyEditing(null));
          }}
        &gt;
          Add New Entry
        &lt;/button&gt;
        &lt;Link to={`diary/${diary.id}`} style={{ width: '100%' }}&gt;
          &lt;button className="secondary" style={buttonStyle}&gt;
            View all &rarr;
          &lt;/button&gt;
        &lt;/Link&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default DiaryTile;
</code></pre>
</div>

In this file, we receive a diary object as a prop and display the data in our component. Notice that we use local state and component props for our data display here. That’s because you don’t have to manage all your app’s state using Redux. Sharing data using props, and maintaining local state in your components is acceptable and encouraged [in some cases](https://redux.js.org/faq/organizing-state).

Next, let’s create a component that will display a list of a diary’s entries, with the last updated entries at the top of the list. Ensure you are in the src/features/diary directory, then create a file named **DiaryEntriesList.tsx** and add the following code to the file:

<div class="break-out">

<pre><code class="language-ts">import React, { FC, useEffect } from 'react';
import { useParams, Link } from 'react-router-dom';
import { useSelector } from 'react-redux';
import { RootState } from '../../rootReducer';
import http from '../../services/api';
import { Entry } from '../../interfaces/entry.interface';
import { setEntries } from '../entry/entriesSlice';
import { setCurrentlyEditing, setCanEdit } from '../entry/editorSlice';
import dayjs from 'dayjs';
import { useAppDispatch } from '../../store';

const DiaryEntriesList: FC = () =&gt; {
  const { entries } = useSelector((state: RootState) =&gt; state);
  const dispatch = useAppDispatch();
  const { id } = useParams();

  useEffect(() =&gt; {
    if (id != null) {
      http
        .get&lt;null, { entries: Entry[] }&gt;(`/diaries/entries/${id}`)
        .then(({ entries: _entries }) =&gt; {
          if (_entries) {
            const sortByLastUpdated = _entries.sort((a, b) =&gt; {
              return dayjs(b.updatedAt).unix() - dayjs(a.updatedAt).unix();
            });
            dispatch(setEntries(sortByLastUpdated));
          }
        });
    }
  }, [id, dispatch]);

  return (
    &lt;div className="entries"&gt;
      &lt;header&gt;
        &lt;Link to="/"&gt;
          &lt;h3&gt;&larr; Go Back&lt;/h3&gt;
        &lt;/Link&gt;
      &lt;/header&gt;
      &lt;ul&gt;
        {entries.map((entry) =&gt; (
          &lt;li
            key={entry.id}
            onClick={() =&gt; {
              dispatch(setCurrentlyEditing(entry));
              dispatch(setCanEdit(true));
            }}
          &gt;
            {entry.title}
          &lt;/li&gt;
        ))}
      &lt;/ul&gt;
    &lt;/div&gt;
  );
};

export default DiaryEntriesList;
</code></pre>
</div>

Here, we subscribe to the entries property of our app’s state, and have our effect fetch a diary’s entry only run when a property, `id`, changes. This property’s value is gotten from our URL as a path parameter using the `useParams()` hook from `react-router`. In the next step, we will create a component that will enable users to create and view diaries, as well as render a diary’s entries when it is in focus.

Create a file named **Diaries.tsx** while still in the same directory, and add the following code to the file:

<div class="break-out">

<pre><code class="language-ts">import React, { FC, useEffect } from 'react';
import { useSelector } from 'react-redux';
import { RootState } from '../../rootReducer';
import http from '../../services/api';
import { Diary } from '../../interfaces/diary.interface';
import { addDiary } from './diariesSlice';
import Swal from 'sweetalert2';
import { setUser } from '../auth/userSlice';
import DiaryTile from './DiaryTile';
import { User } from '../../interfaces/user.interface';
import { Route, Switch } from 'react-router-dom';
import DiaryEntriesList from './DiaryEntriesList';
import { useAppDispatch } from '../../store';
import dayjs from 'dayjs';

const Diaries: FC = () =&gt; {
  const dispatch = useAppDispatch();
  const diaries = useSelector((state: RootState) =&gt; state.diaries);
  const user = useSelector((state: RootState) =&gt; state.user);

  useEffect(() =&gt; {
    const fetchDiaries = async () =&gt; {
      if (user) {
        http.get&lt;null, Diary[]&gt;(`diaries/${user.id}`).then((data) =&gt; {
          if (data && data.length &gt; 0) {
            const sortedByUpdatedAt = data.sort((a, b) =&gt; {
              return dayjs(b.updatedAt).unix() - dayjs(a.updatedAt).unix();
            });
            dispatch(addDiary(sortedByUpdatedAt));
          }
        });
      }
    };
    fetchDiaries();
  }, [dispatch, user]);

  const createDiary = async () =&gt; {
    const result = await Swal.mixin({
      input: 'text',
      confirmButtonText: 'Next &rarr;',
      showCancelButton: true,
      progressSteps: ['1', '2'],
    }).queue([
      {
        titleText: 'Diary title',
        input: 'text',
      },
      {
        titleText: 'Private or public diary?',
        input: 'radio',
        inputOptions: {
          private: 'Private',
          public: 'Public',
        },
        inputValue: 'private',
      },
    ]);
    if (result.value) {
      const { value } = result;
      const {
        diary,
        user: _user,
      } = await http.post&lt;Partial&lt;Diary&gt;, { diary: Diary; user: User }&gt;('/diaries/', {
        title: value[0],
        type: value[1],
        userId: user?.id,
      });
      if (diary && user) {
        dispatch(addDiary([diary] as Diary[]));
        dispatch(addDiary([diary] as Diary[]));
        dispatch(setUser(_user));
        return Swal.fire({
          titleText: 'All done!',
          confirmButtonText: 'OK!',
        });
      }
    }
    Swal.fire({
      titleText: 'Cancelled',
    });
  };

  return (
    &lt;div style={{ padding: '1em 0.4em' }}&gt;
      &lt;Switch&gt;
        &lt;Route path="/diary/:id"&gt;
          &lt;DiaryEntriesList /&gt;
        &lt;/Route&gt;
        &lt;Route path="/"&gt;
          &lt;button onClick={createDiary}&gt;Create New&lt;/button&gt;
          {diaries.map((diary, idx) =&gt; (
            &lt;DiaryTile key={idx} diary={diary} /&gt;
          ))}
        &lt;/Route&gt;
      &lt;/Switch&gt;
    &lt;/div&gt;
  );
};

export default Diaries;
</code></pre>
</div>

In this component, we have a function to fetch the user’s diaries inside a `useEffect` hook, and a function to create a new diary. We also render our components in `react-router`’s `<Route />` component, rendering a diary’s entries if its `id` matches the path param in the route `/diary/:id`, or otherwise rendering a list of the user’s diaries.

To wrap things up, let’s update the `Home.tsx` component. First, update the imports to look like the following:

<pre><code class="language-ts">import React, { FC } from 'react';
import Diaries from '../diary/Diaries';
import Editor from '../entry/Editor';
</code></pre>

Then, change the component’s return statement to the following:

<pre><code class="language-ts">return (
  &lt;div className="two-cols"&gt;
    &lt;div className="left"&gt;
      &lt;Diaries /&gt;
    &lt;/div&gt;
    &lt;div className="right"&gt;
      &lt;Editor /&gt;
    &lt;/div&gt;
  &lt;/div&gt;
</code></pre>

Finally, replace the contents of the index.css file in your app’s src directory with the following code:

<div class="break-out">

<pre><code class="language-ts">:root {
  --primary-color: #778899;
  --error-color: #f85032;
  --text-color: #0d0d0d;
  --transition: all ease-in-out 0.3s;
}
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
html, body, #root {
  height: 100%;
}
*, *:before, *:after {
  box-sizing: border-box;
}
.auth {
  display: flex;
  align-items: center;
  height: 100%;
}
.card {
  background: #fff;
  padding: 3rem;
  text-align: center;
  box-shadow: 2px 8px 12px rgba(0, 0, 0, 0.1);
  max-width: 450px;
  width: 90%;
  margin: 0 auto;
}
.inputWrapper {
  margin: 1rem auto;
  width: 100%;
}
input:not([type='checkbox']), button {
  border-radius: 0.5rem;
  width: 100%;
}
input:not([type='checkbox']), textarea {
  border: 2px solid rgba(0, 0, 0, 0.1);
  padding: 1em;
  color: var(--text-color);
  transition: var(--transition);
}
input:not([type='checkbox']):focus, textarea:focus {
  outline: none;
  border-color: var(--primary-color);
}
button {
  appearance: none;
  border: 1px solid var(--primary-color);
  color: #fff;
  background-color: var(--primary-color);
  text-transform: uppercase;
  font-weight: bold;
  outline: none;
  cursor: pointer;
  padding: 1em;
  box-shadow: 1px 4px 6px rgba(0, 0, 0, 0.1);
  transition: var(--transition);
}
button.secondary {
  color: var(--primary-color);
  background-color: #fff;
  border-color: #fff;
}
button:hover, button:focus {
  box-shadow: 1px 6px 8px rgba(0, 0, 0, 0.1);
}
.error {
  margin: 0;
  margin-top: 0.2em;
  font-size: 0.8em;
  color: var(--error-color);
  animation: 0.3s ease-in-out forwards fadeIn;
}
.two-cols {
  display: flex;
  flex-wrap: wrap;
  height: 100vh;
}
.two-cols .left {
  border-right: 1px solid rgba(0, 0, 0, 0.1);
  height: 100%;
  overflow-y: scroll;
}
.two-cols .right {
  overflow-y: auto;
}
.title {
  font-size: 1.3rem;
}
.subtitle {
  font-size: 0.9rem;
  opacity: 0.85;
}
.title, .subtitle {
  margin: 0;
}
.diary-tile {
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  padding: 1em;
}
.editor {
  height: 100%;
  padding: 1em;
}
.editor input {
  width: 100%;
}
.editor textarea {
  width: 100%;
  height: calc(100vh - 160px);
}
.entries ul {
  list-style: none;
  padding: 0;
}
.entries li {
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  padding: 0.5em;
  cursor: pointer;
}
.entries li:nth-child(even) {
  background: rgba(0, 0, 0, 0.1);
}

@media (min-width: 768px) {
  .two-cols .left {
    width: 25%;
  }
  .two-cols .right {
    width: 75%;
  }
}
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 0.8;
  }
}
</code></pre>
</div>

That’s it! You can now run `npm start` or `yarn start` and check out the final app at [https://localhost:3000](https://localhost:3000).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b104ce-358e-414c-81a7-22cc28c51fb2/fig-05-final-app-home-screen-unauthenticated-user.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b104ce-358e-414c-81a7-22cc28c51fb2/fig-05-final-app-home-screen-unauthenticated-user.png" sizes="100vw" caption="Final App Home Screen (Unauthenticated User). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b104ce-358e-414c-81a7-22cc28c51fb2/fig-05-final-app-home-screen-unauthenticated-user.png'>Large preview</a>)" alt="" >}}

## Conclusion

In this guide, you have learned how to rapidly develop applications using Redux. You also learned about good practices to follow when working with Redux and React, in order to make debugging and extending your applications easier. This guide is by no means extensive as there are still [ongoing discussions surrounding Redux](https://redux.js.org/faq) and some of its concepts. Please check out the [Redux](https://redux.js.org) and [React-Redux](https://react-redux.js.org/) docs if you’d like to learn more about using Redux in your React projects.

- [See source code](https://github.com/jerrynavi/diaries-app) (GitHub repo)

## References

- [Redux FAQs](https://redux.js.org/faq)
- [`Array.prototype.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) on [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
- [Immer.js Docs](https://immerjs.github.io/immer/docs/introduction)
- [Mirage.js Deep Dive Series](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/)
- [Axios on npm](https://www.npmjs.com/package/axios#creating-an-instance)
- [The “Ducks” Proposal](https://github.com/erikras/ducks-modular-redux)

{{< signature "yk" >}}
