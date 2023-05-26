---
title: 'Handling Mounting And Unmounting Of Navigation Routes In React Native'
slug: mounting-unmounting-navigation-routes-react-native
author: daniel-don
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03d97d60-d23b-419c-acb3-23e467d4cc16/mounting-unmounting-navigation-routes-react-native.jpg
date: 2021-08-11T11:40:00.000Z
summary: >-
  Often you need two different sets of navigation stacks for pre and post user authentication. Usually, to see more content, you have to be authenticated in some way. Let’s look at how to mount and unmount navigation stack based on a met condition in React Native.
description: >-
  Often you need two different sets of navigation stacks for pre and post user authentication. Usually, to see more content, you have to be authenticated in some way. Let’s look at how to mount and unmount navigation stack based on a met condition in React Native.
categories:
  - JavaScript
  - React
  - Tools
---

In this article, we are going to walk through **mounting and unmounting of navigation routes** in React Native. An expected behavior of your app is that once the authentication condition is met, a new set of navigation routes are available only to logged-in users, while the other screens which were displayed before authentication is removed and can’t be returned to unless the user signs out of the application.

For security in your app, protected routes provide you with a way to only display certain information/content on your app to specific users, while restricting access from unauthorized persons.

We will be working with [Expo](https://expo.io/) for this project because it’ll help us focus on the problem at hand instead of worrying about a lot of setups. The exact same steps in this article could be followed for a bare React Native application.

You need some familiarity with **JavaScript and React Native** to follow through with this tutorial. Here are a few important things you should already be familiar with:

- Custom components in React Native (how to create components, receive, pass, and use props in a component). [Read more](https://www.fastfwd.com/custom-component-in-react-native/).
- React Navigation. [Read more](https://reactjs.org/docs/context.html).
- Stack Navigator in React Native. [Read more](https://reactnavigation.org/docs/stack-navigator/).
- Basic Knowledge of React Native Core components (`<View/>`, `<Text/>`, etc.). [Read more](https://reactnative.dev/docs/components-and-apis).
- React Native `AsyncStorage`. [Read more](https://reactnative.dev/docs/asyncstorage).
- Context API. [Read more](https://reactjs.org/docs/context.html).

## Project Setup And Base Authentication

If you're new to using expo and don’t know how to install expo, [visit the official documentation](https://docs.expo.io/get-started/installation/). Once the installation is complete, go ahead to initialize a new React Native project with expo from our command prompt:

<pre><code class="language-javascript">expo init navigation-project</code></pre>

You will be presented with some options to choose how you want the base setup to be:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf792489-413d-48a1-9f0d-2343e662ab7d/1-mounting-unmounting-navigation-routes-authentication-react-native.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf792489-413d-48a1-9f0d-2343e662ab7d/1-mounting-unmounting-navigation-routes-authentication-react-native.PNG" width="800" height="135" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf792489-413d-48a1-9f0d-2343e662ab7d/1-mounting-unmounting-navigation-routes-authentication-react-native.PNG'>Large preview</a>)" alt="React Native project's base setup" >}}

In our case, let’s select the first option to set up our project as a blank document. Now, wait until the installation of the JavaScript dependencies is complete.

Once our app is set up, we can change our directory to our new project directory and open it in your favorite code editor. We need to install the library we will be using for `AsyncStorage` and our navigation libraries. Inside your folder directory in your terminal, paste the command above and choose a template (`blank` would work) to install our project dependencies.

Let's look at what each of these dependencies is for:

- **@react-native-community/async-storage**  
Like localStorage on the web, it is a React Native API for persisting data on a device in key-value pairs. 
- **@react-native-community/masked-view, react-native-screens, react-native-gesture-handle**  
These dependencies are core utilities that are used by most navigators to create the navigation structure in the app. (Read more in [Getting started with React Native navigation](https://reactnavigation.org/docs/getting-started/).)
- **@react-navigation/native**  
This is the dependency for React Native navigation.
- **@react-navigation/stack**  
This is the dependency for stack navigation in React Native.

<div class="break-out">

<pre><code class="language-bash">npm install @react-native-community/async-storage @react-native-community/masked-view @react-navigation/native @react-navigation/stack react-native-screens react-native-gesture-handle</code></pre>
</div>

To start the application use `expo start` from the app directory in your terminal. Once the app is started, you can use the expo app from your mobile phone to scan the bar code and view the application, or if you have an android emulator/IOS simulator, you can open the app through them from the expo developer tool that opens up in your browser when you start an expo application. For the images examples in this article, we will be using [Genymotions](https://www.genymotion.com/) to see our result. Here’s what our final result will look like in Genymotions:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a271a5a6-2d28-4334-a57e-8aff24818578/2-mounting-unmounting-navigation-routes-authentication-react-native.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a271a5a6-2d28-4334-a57e-8aff24818578/2-mounting-unmounting-navigation-routes-authentication-react-native.PNG" width="800" height="449" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a271a5a6-2d28-4334-a57e-8aff24818578/2-mounting-unmounting-navigation-routes-authentication-react-native.PNG'>Large preview</a>)" alt="final result in Genymotions" >}}

### Folder Structures

Let us create our folder structure from the start so that it's easier for us to work with it as we proceed:

We need two folders first:

- **context**  
This folder will hold the context for our entire application as we will be working with Context API for global state management.
- **views**  
This folder will hold both the navigation folder and the views for different screens.

Go ahead and create the two folders in your project directory.

Inside the context folder, create a folder called **authContext** and create two file inside of the **authContext** folder:

- **AuthContext.js**,
- **AuthState.js**.

We will need these files when we start working with Context API.

Now go to the **views** folder we created and create two more folders inside of it, namely:

- **navigation**,
- **screens**.

Now, we are not yet finished, inside the **screens** folder, create these two more folders:

- **postAuthScreens**,
- **preAuthScreens**.

If you followed the folder setup correctly, this is how your folder structure should look like at the moment:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ffaf659-afec-4555-9224-de273d1d10c2/3-mounting-unmounting-navigation-routes-authentication-react-native.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ffaf659-afec-4555-9224-de273d1d10c2/3-mounting-unmounting-navigation-routes-authentication-react-native.PNG" width="800" height="351" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ffaf659-afec-4555-9224-de273d1d10c2/3-mounting-unmounting-navigation-routes-authentication-react-native.PNG'>Large preview</a>)" alt="folder structure" >}}

{{% feature-panel %}}

### Creating Our First Screen

Now let's create our first screen and call it the **welcomeScreen.js** inside the **preAuthScreens** folder.

**preAuthScreens   >   welcomeScreen.js**

Here’s the content of our **welcomeScreen.js** file:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';
import { View, Text, Button, StyleSheet, TextInput } from 'react-native';

const WelcomeScreen = () =&gt; {

  const onUserAuthentication = () =&gt; {
    console.log("User authentication button clicked")
  }

  return (
    &lt;View style={styles.container}&gt;
      &lt;Text style={styles.header}&gt;Welcome to our App!&lt;/Text&gt;
      &lt;View&gt;
        &lt;TextInput style={styles.inputs} placeholder="Enter your email here.." /&gt;
        &lt;TextInput style={styles.inputs} secureTextEntry={true} placeholder="Enter your password here.." /&gt;
&lt;Button  title="AUTHENTICATE" onPress={onUserAuthentication} /&gt;
      &lt;/View&gt;
    &lt;/View&gt;
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  header: {
    fontSize: 25,
    fontWeight: 'bold',
    marginBottom: 30
  },
  inputs: {
    width: 300,
    height: 40,
    marginBottom: 10,
    borderWidth: 1,
  }
})

export default WelcomeScreen
</code></pre>
</div>

Here's what we did in the code block above:

First, we imported the things we need from the React Native library, namely, `View`, `Text`, `Button`, `TextInput`. Next, we created our functional component `WelcomeScreen`. 

You’ll notice that we imported the `StyleSheet` from React Native and used it to define styles for our header and also our `<TextInput />`.

Lastly, we export the `WelcomeScreen` component at the bottom of the code.

Now that we are done with this, let's get this component to function as expected by using the `useState` hook to store the values of the inputs and update their states anytime a change happens in the input fields. We will also bring import the `useCallback` hook from React as we will be needing it later to hold a function.

First, while we are still in the `WelcomeScreen` component, we need to import the `useState` and `useCallback` from React.

<pre><code class="language-javascript">import React, { useState, useCallback } from 'react';</code></pre>

Now inside the `WelcomeScreen` functional component, let's create the two states for the email and password respectively:

<pre><code class="language-javascript">...
const WelcomeScreen = () =&gt; {
  const [email, setEmail] = useState('')
  const [password, setPassword] = useState('')
  return (
    ...
  )
}
...</code></pre>

Next, we need to modify our `<TextInput />` fields so that the get their value from their respective states and update their state when the value of the input is updated:

<div class="break-out">

<pre><code class="language-javascript">import React, { useState, useCallback } from 'react';
import { View, Text, Button, StyleSheet, TextInput } from 'react-native';

const WelcomeScreen = () =&gt; {
  const [email, setEmail] = useState('')
  const [password, setPassword] = useState('')

  const onInputChange = (value, setState) =&gt; {
    setState(value);
  }
  return (
    &lt;View&gt;
      ...      
      &lt;View&gt;
        &lt;TextInput
          style={styles.inputs}
          placeholder="Enter your email here.."
          value={email}
          onChangeText={(value) =&gt; onInputChange(value, setEmail)}
        /&gt;
        &lt;TextInput
          style={styles.inputs}
          secureTextEntry={true}
          placeholder="Enter your password here.."
          value={password}
          onChangeText={(value) =&gt; onInputChange(value, setPassword)}
        /&gt;
        ...
      &lt;/View&gt;
    &lt;/View&gt;
  )
}
...
</code></pre>
</div>

In the code above, here is what we did:

- We made the `value` of each of the text inputs to point to their respective states.
- We added the `onChangeText` handler to our text inputs. This fires up anytime a new value is entered or deleted from the input fields.
- We called our `onInputChange` function which accepts two arguments:
    - The current `value` is supplied by the `onChangeText` handler.
    - The setter of the state that should be updated (for the first input field we pass `setEmail` and the second we pass `setPassword`.
    - Finally, we write our `onInputChange` function, and our function does only one thing: It updates the respective states with the new value.

The next thing we need to work on is the `onUserAuthentication()` function with is called whenever the button for the form submission is clicked.

Ideally, the user must have already created an account and login will involve some backend logic of some sort to check that the user exists and then assign a token to the user. In our case, since we are not using any backend, we will create an object holding the correct user login detail, and then only authenticate a user when the values they enter matches our fixed values from the login object of `email` and `password` that we will create.

Here’s the code we need to do this:

<div class="break-out">

<pre><code class="language-javascript">...

const correctAuthenticationDetails = {
  email: 'demouser@gmail.com',
  password: 'password'
}
const WelcomeScreen = () =&gt; {
  ...

  // This function gets called when the `AUTHENTICATE` button is clicked
  const onUserAuthentication = () =&gt; {
    if (
      email !== correctAuthenticationDetails.email ||
      password !== correctAuthenticationDetails.password
    ) {
      alert('The email or password is incorrect')
      return
    }
      // In here, we will handle what happens if the login details are       // correct
  }

  ...
  return (
    ...
  )
}
...
</code></pre>
</div>

One of the first things you’ll notice in the code above is that we defined a `correctAuthenticationDetails` (which is an object that holds the correct login details we expect a user to supply)  outside of the `WelcomeScreen()` functional component.

Next, we wrote the content of the `onUserAuthentication()` function and used a conditional statement to check if the `email` or `password` held in the respective states does not match the one we supplied in our object.

If you would like to see what we have done so far, import the **WelcomeScreen** component into your **App.js** like this:

Open the **App.js** file and put this replace the entire code with this:

<div class="break-out">

<pre><code class="language-javascript">import { StatusBar } from 'expo-status-bar';
import React from 'react';
import { View } from 'react-native';
import WelcomeScreen from './views/screens/preAuthScreens/welcomeScreen';
export default function App() {
  return (
    &lt;View&gt;
      &lt;StatusBar style="auto" /&gt;
      &lt;WelcomeScreen /&gt;
    &lt;/View&gt;
  );
}
</code></pre>
</div> 

Looking closely at the code above, you’ll see that what we did was import the **WelcomeScreen** component and then used it in the `App()` function.

Here’s what the result looks like of our `WelcomeScreen` looks like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ecde0ee-f05f-4a93-91e1-371f5d3fa834/4-mounting-unmounting-navigation-routes-authentication-react-native.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ecde0ee-f05f-4a93-91e1-371f5d3fa834/4-mounting-unmounting-navigation-routes-authentication-react-native.PNG" width="800" height="477" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ecde0ee-f05f-4a93-91e1-371f5d3fa834/4-mounting-unmounting-navigation-routes-authentication-react-native.PNG'>Large preview</a>)" alt="the result of WelcomeScreen" >}}

Now that we are done building the **WelcomeScreen** component, let’s move ahead and start working with Context API for managing our global state.

{{% ad-panel-leaderboard %}}

### Why Context API?

Using Context API, we do not need to install any additional library into ReactJS, it is less stressful to set up, and is one of the most popular ways of handling global state in ReactJS. For lightweight state management, it is a good choice.

### Creating Our Context

If you recall, we created a **context** folder earlier and created a subfolder inside of it called the **authContext**.

Now let’s navigate to the **AuthContext.js** file in the **authContext** folder and create our context:

*context > authContext > AuthContext.js*

<pre><code class="language-javascript">
import React, { createContext } from 'react';
const AuthContext = createContext();
export default AuthContext;
</code></pre>

The `AuthContext` we just created holds the `loading` state value and the `userToken` state values. Currently, in the `createContext` we declared in the code-block above, we didn’t initialize any default values here so our context is currently `undefined`.  An example value of the auth context could be `{loading: false, userToken: 'abcd}`

The **AuthState.js** file holds our Context API logic and their state values. Functions written here can be called from anywhere in our app and when they update values in state, it is updated globally also.

First, let’s bring in all the imports we will need in this file:

*context > AuthContext > AuthState.js*

<div class="break-out">

<pre><code class="language-javascript">import React, { useState } from 'react';
import AuthContext from './AuthContext';
import AsyncStorage from '@react-native-community/async-storage';</code></pre>
</div>

We imported the `useState()` hook from ReactJS to hold our states, we imported the **AuthContext** file we created above because this is where our empty context for authentication is initialized and we will need to use it as you’ll see later on while we progress, finally we import the `AsyncStorage` package (similar to localStorage for the web). 

`AsyncStorage` is a React Native API that allows you to persist data offline over the device in a React Native application.

<pre><code class="language-javascript">...

const AuthState = (props) =&gt; {
    const [userToken, setUserToken] = useState(null);
    const [isLoading, setIsLoading] = useState(true);

    const onAuthentication = async() =&gt; {
        const USER_TOKEN = "drix1123q2"
        await AsyncStorage.setItem('user-token', USER_TOKEN);
        setUserToken(USER_TOKEN);
        console.warn("user has been authenticated!")
    }

    return (
        &lt;AuthContext.Provider
            value={{
                onAuthentication,
            }}
        &gt;
            {props.children}
        &lt;/AuthContext.Provider&gt;
    )
}
export default AuthState;
</code></pre>  

In the code block above here's what we did:

- We declared two states for the `userToken` and `isLoading`. The `userToken` state will be used to store the token saved to `AsyncStorage`, while the `isLoading` state will be used to track the loading status (initially it is set to `true`). We will find out more about the use of these two states as we proceed.

- Next, we wrote our `onAuthentication()` function. This function is an `async` function that gets called when the login button is clicked from the `welcomeScreen.jsx` file. This function will only get called if the email and password the user has supplied matches the correct user detail object we provided. Usually what happens during authentication is that a token is generated for the user after the user is authenticated on the backend using a package like [JWT](https://jwt.io/introduction), and this token is sent to the frontend. Since we are not going into all of that for this tutorial, we created a static token and kept it in a variable called `USER_TOKEN`.

- Next, we use the `await` keyword to set our user token to AsyncStorage with the name `user-token`. The `console.warn()` statement is just used to check that everything went right, you can take it off whenever you like.

- Finally, we pass our `onAuthenticated` function as a value inside our `<AuthContext.Provider>` so that we can access and call the function from anywhere in our app.

*screens > preAuth > welcomeScreen.js*

First, import `useContext` from ReactJS and import the `AuthContext` from the `AuthContext.js` file.

<div class="break-out">

<pre><code class="language-javascript">import React, { useState, useContext } from 'react';
import AuthContext from '../../../context/authContext/AuthContext'
...</code></pre>
</div>

Now, inside the `welcomeScreen()` functional component, let’s use the context which we have created:

<pre><code class="language-javascript">...
const WelcomeScreen = () =&gt; {
  const { onAuthentication } = useContext(AuthContext)
  const onUserAuthentication = () =&gt; {
    if (
      email !== correctAuthenticationDetails.email ||
      password !== correctAuthenticationDetails.password
    ) {
      alert('The email or password is incorrect')
      return
    }
    onAuthentication()
  }
  return (
    ...
  )
}
...
</code></pre>

In the above code block, we destructured the `onAuthentication` function from our `AuthContext` and then we called it inside our `onUserAuthentication()` function and removed the `console.log()` statement which was there before now.

Right now, this will throw an error because we don’t yet have access to the `AuthContext`. To use the `AuthContext` anywhere in your application, we need to wrap the top-level file in our app with the `AuthState` (in our case, it is the **App.js** file).

Go to the **App.js** file and replace the code there with this:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';
import WelcomeScreen from './views/screens/preAuthScreens/welcomeScreen';
import AuthState from './context/authContext/AuthState'

export default function App() {
  return (
    &lt;AuthState&gt;
      &lt;WelcomeScreen /&gt;
    &lt;/AuthState&gt;
  );
}
</code></pre>
</div>

We've come so far and we're done with this section. Before we move into the next section where we set up our routing, let's create a new screen. The screen we are about to create will be the **HomeScreen.js** file which is supposed to show up only after successful authentication.

Go to: *screens > postAuth*.

Create a new file called **HomeScreen.js**. Here's the code for the **HomeScreen.js** file:

*screens > postAuth >* ***HomeScreen.js***

<pre><code class="language-javascript">import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

const HomeScreen = () =&gt; {

  const onLogout = () =&gt; {
    console.warn("Logout button cliked")
  }

  return (
    &lt;View style={styles.container}&gt;
      &lt;Text&gt;Now you're authenticated! Welcome!&lt;/Text&gt;
      &lt;Button title="LOG OUT" onPress={onLogout} /&gt;
    &lt;/View&gt;
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
})

export default HomeScreen
</code></pre>

For now, the logout button has a dummy `console.log()` statement. Later on, we will create the logout functionality and pass it to the screen from our context.

{{% ad-panel-leaderboard %}}

## Setting Up Our Routes

We need to create three (3) files inside our navigation folder:

- **postAuthNavigator.js**,
- **preAuthNavigator.js**,
- **AppNavigator.js**.

Once you’ve created these three files, navigate to the **preAuthNaviagtor.js** file you just created and write this:

*navigation > preAuthNavigator.js*

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import { createStackNavigator } from "@react-navigation/stack";
import WelcomeScreen from "../screens/preAuthScreens/welcomeScreen";

const PreAuthNavigator = () =&gt; {
    const { Navigator, Screen } = createStackNavigator();

    return (
        &lt;Navigator initialRouteName="Welcome"&gt;
            &lt;Screen
                name="Welcome"
                component={WelcomeScreen}
            /&gt;
        &lt;/Navigator&gt;
    )
}
export default PreAuthNavigator;
</code></pre>
</div>

In the file above, here's what we did:

- We imported the `createStackNavigator` from the `@react-navigation/stack` which we are using for our stack navigation. The `createStackNavigator`Provides a way for your app to transition between screens where each new screen is placed on top of a stack. By default the stack navigator is configured to have the familiar iOS and Android look & feel: new screens slide in from the right on iOS, fade in from the bottom on Android. Click [here](https://reactnavigation.org/docs/stack-navigator/) if you want to learn more about the [stack navigator in React Native](https://reactnavigation.org/docs/stack-navigator/).
- We destructured `Navigator` and `Screen` from the `createStackNavigator()`.
- In our return statement, we created our navigation with the `<Navigator/>` and created our screen with the `<Screen/>`. this means that if we had multiple screens that can be accessed before authentication, we will have multiple `<Screen/>` tags here representing them.
- Finally, we export our `PreAuthNavigator` component.

Let us do a similar thing for the `postAuthNavigator.js` file.

*navigation > postAuthNavigator.js*

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import { createStackNavigator } from "@react-navigation/stack";
import HomeScreen from "../screens/postAuthScreens/HomeScreen";
const PostAuthNavigator = () =&gt; {
  const { Navigator, Screen} = createStackNavigator();
  return (
    &lt;Navigator initialRouteName="Home"&gt;
      &lt;Screen
        name="Home"
        component={HomeScreen}
      /&gt;
    &lt;/Navigator&gt; 
  )
}
export default PostAuthNavigator;
</code></pre>
</div>

As we see in the code above, the only difference between the **preAuthNavigator.js** and the **postAuthNavigator.js** is the screen being rendered. While the first one takes the `WelcomeScreen`, the **postAuthNavigator.js** takes the `HomeScreen`.

To create our **AppNavigator.js** we need to create a few things.

Since the **AppNavigator.js** is where we will be switching and checking which route will be available for access by the user, we need several screens in place for this to work properly, let’s outline the things we need to create first:

1. **TransitionScreen.js**  
While the app decides which navigation it is going to mount, we want a transition screen to show up. Typically, the transition screen will be a loading spinner or any other custom animation chosen for the app, but in our case, we will use a basic `<Text/>` tag to display *`loading…`*.
3. `checkAuthenticationStatus()`  
This function is what we will be calling to check the authentication status which will determine which navigation stack is going to be mounted. We will create this function in our context and use it in the **Appnavigator.js**.

Now, let's go ahead and create our **TransitionScreen.js** file.

*screens >* ***TransitionScreen.js***

<pre><code class="language-javascript">import React from 'react';
import { Text, View } from 'react-native';

const TransitionScreen = () =&gt; {
  return (
    &lt;View&gt;
      &lt;Text&gt;Loading...&lt;/Text&gt;
    &lt;/View&gt;
  )
}

export default TransitionScreen
</code></pre>

Our transition screen is just a simple screen that shows loading text. We will see where to use this as we proceed in this article.

Next, let us go to our **AuthState.js** and write our `checkAuthenticationStatus()`:

*context > authContext >* ***AuthState.js***

<div class="break-out">

<pre><code class="language-javascript">import React, { useState, useEffect } from 'react';
import AuthContext from './AuthContext';
import AsyncStorage from '@react-native-community/async-storage';

const AuthState = (props) =&gt; {
    const [userToken, setUserToken] = useState(null);
    const [isLoading, setIsLoading] = useState(true);

    ...
    useEffect(() =&gt; {
        checkAuthenticationStatus()
    }, [])
    
    const checkAuthenticationStatus = async () =&gt; {
        try {
            const returnedToken = await AsyncStorage.getItem('user-toke             n');
            setUserToken(returnedToken);
            console.warn('User token set to the state value)
        } catch(err){
            console.warn(`Here's the error that occured while retrievin             g token: ${err}`) 
        }
        setIsLoading(false)
    }


    const onAuthentication = async() =&gt; {
        ...
    }

    return (
        &lt;AuthContext.Provider
            value={{
                onAuthentication,
                userToken,
                isLoading,
            }}
        &gt;
            {props.children}
        &lt;/AuthContext.Provider&gt;
    )
}
export default AuthState;
</code></pre>
</div>

In the code block above, we wrote the function `checkAuthenticationStatus()`. In our function, here's what we are doing:

- We used the `await` keyword to get our token from `AsyncStorage`. With `AsyncStorage`, if there’s no token supplied, it returns `null`. Our initial `userToken` state is set to `null` also.
- We use the `setUserToken` to set our returned value from `AsyncStorage` as our new `userToken`. If the returned value is `null`, it means our `userToken` remains `null`.
- After the `try{}…catch(){}` block, we set `isLoading` to false because the function to check authentication status is complete. We’ll need the value of `isLoading` to know if we should still be displaying the `TransitionScreen` or not. It’s worth considering setting an error if there is an error retrieving the token so that we can show the user a “Retry” or “Try Again” button when the error is encountered.
- Whenever `AuthState` mounts we want to check the authentication status, so we use the `useEffect()` ReactJS hook to do this. We call our `checkAuthenticationStatus()` function inside the `useEffect()` hook and set the value of `isLoading` to `false` when it is done.
- Finally, we add our states to our `<AuthContext.Provider/>` values so that we can access them from anywhere in our app covered by the Context API.

Now that we have our function, it is time to go back to our **AppNavigator.js** and write the code for mounting a particular stack navigator based on the authentication status:

*navigation > AppNavigator.js*

First, we will import all we need for our **AppNavigator.js**.

<div class="break-out">

<pre><code class="language-javascript">import React, { useEffect, useContext } from "react";
import PreAuthNavigator from "./preAuthNavigator";
import PostAuthNavigator from "./postAuthNavigator";
import { NavigationContainer } from "@react-navigation/native"
import { createStackNavigator } from "@react-navigation/stack";
import AuthContext from "../../context/authContext/AuthContext";
import TransitionScreen from "../screens/TransitionScreen";
</code></pre>
</div>

Now that we have all our imports, let’s create the `AppNavigator()` function.

<pre><code class="language-javascript">...
const AppNavigator = () =&gt; {

}

export default AppNavigator
</code></pre>

Next, we will now go ahead to write the content of our `AppNavigator()` function:

<div class="break-out">

<pre><code class="language-javascript">import React, { useState, useEffect, useContext } from "react";
import PreAuthNavigator from "./preAuthNavigator";
import PostAuthNavigator from "./postAuthNavigator";
import { NavigationContainer } from "@react-navigation/native"
import { createStackNavigator } from "@react-navigation/stack";
import AuthContext from "../../context/authContext/AuthContext";
import TransitionScreen from "../screens/transition";

const AppNavigator = () =&gt; {
    const { Navigator, Screen } = createStackNavigator();
    const authContext = useContext(AuthContext);
    const { userToken, isLoading } = authContext;
    if(isLoading) {
      return &lt;TransitionScreen /&gt;
    }
    return (
    &lt;NavigationContainer&gt;
      &lt;Navigator&gt;
        { 
          userToken == null ? (
            &lt;Screen
              name="PreAuth"
              component={PreAuthNavigator}
              options={{ header: () =&gt; null }}
            /&gt;
          ) : (
            &lt;Screen 
              name="PostAuth"
              component={PostAuthNavigator}
              options={{ header: () =&gt; null }}
            /&gt;
          )
        }
      &lt;/Navigator&gt;
    &lt;/NavigationContainer&gt;
  )
}

export default AppNavigator
</code></pre>
</div>

In the above block of code, here's an outline of what we did:

- We created a stack navigator and destructured the `Navigator` and `Screen` from it.
- We imported the `userToken` and the `isLoading` from our `AuthContext`
- When the `AuthState` mounts, the `checkAuthenticationStatus()` is called in the `useEffecct` hook there. We use the `if` statement to check if  `isLoading` is `true`, if it is `true` the screen we return is our `<TransitionScreen />` which we created earlier because the `checkAuthenticationStatus()` function is not yet complete.
- Once our `checkAuthenticationStatus()` is complete, `isLoading` is set to `false` and we return our main Navigation components.
- The `NavigationContainer` was imported from the `@react-navigation/native`. It is only used once in the main top-level navigator. Notice that we are not using this in the **preAuthNavigator.js** or the **postAuthNavigator.js.**
- In our `AppNavigator()`, we still create a stack navigator. If the `userToken` gotten from our Context API is `null`, we mount the `PreAuthNavigator`, if its value is something else (meaning that the `AsyncStorage.getItem()` in the `checkAuthenticationStatus()` returned an actual value), then we mount the `PostAuthNavigator`. Our conditional rendering is done using the [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator).

Now we’ve set up our **AppNavigator.js**. Next, we need to pass our `AppNavigator` into our **App.js** file.

Let’s pass our `AppNavigator` into the **App.js** file:

*App.js*

<pre><code class="language-javascript"> ...
import AppNavigator from './views/navigation/AppNavigator';

...
return (
    &lt;AuthState&gt;
      &lt;AppNavigator /&gt;
    &lt;/AuthState&gt;
  );
</code></pre>

Let's now see what our app looks like at the moment:

{{< vimeo 567131718 >}}

Here’s what happens when you supply an incorrect credential while trying to log in:

{{< vimeo 567132688 >}}

### Adding The Logout Functionality

At this point, our authentication and route selection process is complete. The only thing left for our app is to add the logout functionality.

The logout button is in the **HomeScreen.js** file. We passed an `onLogout()` function to the `onPress` attribute of the button. For now, we have a simple `console.log()` statement in our function, but in a little while that will change.

Now, let’s go to our **AuthState.js** and write the function for logout. This function simply clears the `AsyncStorage` where the user token is saved.

*context > authContext > AuthState.js*

<pre><code class="language-javascript">...
const AuthState = (props) =&gt; {
    ...

    const userSignout = async() =&gt; {
        await AsyncStorage.removeItem('user-token');
        setUserToken(null);
    }


    return (
      ...
    )
}

export default AuthState;
</code></pre>

The `userSignout()` is an asynchronous function that removes the `user-token` from our `AsyncStorage`.

Now we need to call the `userSignout()` function in our **HomeScreen.js** any time the logout button is clicked on.

Let’s go to our **HomeScreen.js** and use ther `userSignout()` from our `AuthContext`.

*screens > postAuthScreens >* ***HomeScreen.js***

<div class="break-out">

<pre><code class="language-javascript">import React, { useContext } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import AuthContext from '../../../context/authContext/AuthContext'

const HomeScreen = () =&gt; {
  const { userSignout } = useContext(AuthContext)
  
  const onLogout = () =&gt; {
    userSignout()
  }
  return (
    &lt;View style={styles.container}&gt;
      &lt;Text&gt;Now you're authenticated! Welcome!&lt;/Text&gt;
 &lt;Button title="LOG OUT" onPress={onLogout} /&gt;
    &lt;/View&gt;
  )
}
...
</code></pre>
</div>

In the above code block we imported thee `useContext` hook from ReactJS, then we imported our AuthContext. Next, we destructured the `userSignout` function from our `AuthContext` and this `userSignout()` function is called in our `onLogout()` function.

Now whenever our logout button is clicked, the user token in our `AsyncStorage` is cleared.

Voila! our entire process is finished.

{{< vimeo 567135661 >}}

Here’s what happens when you press the back button after you’re logged in:

{{< vimeo id="567136502" caption="Pressing the back button after logging into the app." >}}

Here’s what happens when you press the back button after logging out:

{{< vimeo id="567136982" caption="Pressing the back button after logging out of the app." >}}

Here are some  different behaviors we notice when using this pattern in our navigation stack switching:

1. You’ll notice that there was nowhere we needed to make use of `navigation.navigate()` or `navigation.push()` to go to another route after login. Once our state is updated with the user token, the navigation stack rendered is automatically changed.
2. Pressing the back button on your device after login is successful cannot take you back to the login page, instead, it closes the app entirely. This behavior is important because you don’t want the user to be able to return back to the login page except they log out of the app. The same thing applies to logging out &mdash; once the user logs out, they cannot use the back button to return to the `HomeScreen` screen, but instead, the app closes.

## Conclusion

In many Apps, authentication is one of the most important parts because it confirms that the person trying to gain access to protected content has the right to access the information. Learning how to do it right is an important step in building a great, intuitive, and easy to use/navigate the application.

Building on top of this code, here are a few things you might consider adding:

- Form validation for validating input fields. Check out [React Native form validation with Formik and Yup](https://blog.logrocket.com/react-native-form-validations-with-formik-and-yup/).
- Firebase authentication for integrating authentication with Gmail, Github, Facebook, Twitter, or your custom interface. Check out [React Native Firebase](https://rnfirebase.io/auth/usage).
- [Code concepts for designers: Authentication and Authorization.](https://uxdesign.cc/code-concepts-for-designers-authentication-authorization-24b72ab33a62)

Here are also some important resources I found that will enlighten you more about authentication, security and how to do it right:

### Resources
  
- [React Native: User Authentication Flow Explained](https://rossbulat.medium.com/react-native-user-authentication-flow-explained-d988905ba106)
- [10 React Security Best Practices](https://snyk.io/blog/10-react-security-best-practices/)
- [Authentication Methods That Can Prevent The Next Breach](https://www.idrnd.ai/5-authentication-methods-that-can-prevent-the-next-breach/)
- View a live build/preview of our application [here](https://snack.expo.io/@danieldon/github.com-chiagozielam-reactnative_authentication_navigation_pattern);
- View the project on [GitHub](https://github.com/Chiagozielam/ReactNative_authentication_navigation_pattern).

{{< signature "ks, vf, yk, il" >}}
