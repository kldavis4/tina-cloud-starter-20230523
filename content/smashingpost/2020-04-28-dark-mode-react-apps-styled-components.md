---
title: 'Implementing Dark Mode In React Apps Using styled-components'
slug: dark-mode-react-apps-styled-components
author: blessing-krofegha
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cd95f4e-6e1d-4037-839c-1ba62b76f441/dark-mode-react-apps-styled-components.png
date: 2020-04-28T10:30:00.000Z
summary: >-
  Light mode is a convention in most web and mobile apps. However, in modern development, we have seen how dark mode, which displays light text and interface elements on a dark background, is quickly becoming a user preference. In this article, we’ll learn how to efficiently implement dark mode in a React app on a simple web page, using the [styled-components](https://styled-components.com/) library and leveraging some React features like hooks. We will also discuss the pros and cons of dark mode and why it should be adopted.
description: >-
  In this article, we’ll learn how to efficiently implement dark mode in a React app on a simple web page, using the [styled-components](https://styled-components.com/) library and leveraging some React features like hooks.
categories:
  - Apps
  - Dark Mode
  - React
---

One of the most commonly [requested](https://www.trustedreviews.com/news/dark-mode-apps-3810652) software features is dark mode (or night mode, as others call it). We see dark mode in the apps that we use every day. From mobile to web apps, dark mode has become vital for companies that want to take care of their users’ eyes.

Dark mode is a supplemental feature that displays mostly dark surfaces in the UI. Most major companies (such as YouTube, Twitter, and Netflix) have adopted dark mode in their mobile and web apps.

While we won’t go in depth into React and styled-components, a basic knowledge of React, CSS, and styled-components would come in handy. This tutorial will benefit those who are looking to enhance their web applications by catering to those who love dark mode.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2391029b-6a62-4adc-85b3-832e8e171384/dark-mode-resources-figure-01.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2391029b-6a62-4adc-85b3-832e8e171384/dark-mode-resources-figure-01.png" sizes="100vw" caption="StackOverflow announces dark mode on Twitter (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2391029b-6a62-4adc-85b3-832e8e171384/dark-mode-resources-figure-01.png'>Large preview</a>)" alt="StackOverflow announces dark mode on Twitter" >}}

A few days before the writing of this article, StackOverflow announced its release of dark mode, giving users the chance to toggle between the two modes.

Dark mode reduces eye strain and helps when you’re working for a long time on a computer or mobile phone.

## What Is Dark Mode?

Dark mode is the color scheme of any interface that displays light text and interface elements on a dark background, which makes the screen a little easier to look at mobile phones, tablets, and computers. Dark mode reduces the light emitted by the screen, while maintaining the minimum color-contrast ratios required for readability.

{{% feature-panel %}}

## Why Should You Care About Dark Mode?

Dark mode enhances visual ergonomics by reducing eye strain, adjusting the screen to current light conditions, and providing ease of use at night or in dark environments.

Before implementing dark mode in our app, let’s look at its benefits.

### Battery Saving

Dark mode in web and mobile apps can [prolong](https://appleinsider.com/articles/17/11/10/extreme-test-shows-oled-iphone-x-with-dark-mode-saves-nearly-60-battery-over-3-hours) the battery life of a device. Google has [confirmed](https://www.howtogeek.com/fyi/google-wants-more-battery-saving-dark-mode-options-in-its-apps/) that dark mode on OLED screens has been a huge help to battery life.

For example, at 50% brightness, dark mode in the YouTube app saves about 15% more screen energy than a flat white background. At 100% screen brightness, the dark interface saves a whopping 60% of screen energy.

### Dark Mode Is Beautiful

Dark mode is beautiful, and it can significantly enhance the appeal of the screen.

While most products are going for that similar [bland white look](https://www.businessinsider.com/f8-2019-facebook-big-redesign-stories-groups-2019-4), dark mode offers something different that feels mysterious and new.

It also provides great opportunities to present graphic content such as dashboards, pictures, and photos in a fresh way.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d042204b-1b9f-4466-85a3-b16c860e6712/dark-mode-resources-figure-02.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d042204b-1b9f-4466-85a3-b16c860e6712/dark-mode-resources-figure-02.png" sizes="100vw" caption="The beauty of Twitter’s dark mode over light mode (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d042204b-1b9f-4466-85a3-b16c860e6712/dark-mode-resources-figure-02.png'>Large preview</a>)" alt="Twitter dark versus light mode" >}}

Now that you know why you should implement dark mode in your next web app, let’s dive deep into styled-components, which is the defining resource of this tutorial.

{{% pull-quote %}}
 Dark mode is the color scheme of any interface that displays light text and interface elements on a dark background, which makes it a little easier to look at on mobile phones, tablets, and computers.
{{% /pull-quote %}}

## What Are styled-components?

Throughout this article, we will be using the [styled-components](https://styled-components.com/) library very often. There have always been many ways to style a modern web app. There’s the traditional method of styling at the document level, which includes creating an `index.css` file and linking it to the HTML or styling inside the HTML file.

A lot has changed in the ways that web apps are styled recently, since the introduction of CSS-in-JS.

CSS-in-JS refers to a pattern in which CSS is composed using JavaScript. It utilizes tagged [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) to style components in a JavaScript file.

To learn more about CSS-in-JS, check out [Anna Monus’s article](https://webdesign.tutsplus.com/articles/an-introduction-to-css-in-js-examples-pros-and-cons--cms-33574) on the subject.

[styled-components](https://styled-components.com/) is a CSS-in-JS library lets you use all of the features of CSS that you love, including media queries, pseudo-selectors, and nesting.

## Why styled-components?

styled-components was created for the following reasons:

- **No class name hell**  
Instead of you scratching your head to find a class name for an element, styled-components generates unique class names for your styles. You’ll never have to worry about misspellings or using class names that have no meaning.
- **Using props**  
styled-components allow us to extend styling properties using the `props` parameter, commonly used in React &mdash; thus, dynamically affecting the feel of a component via the application’s state.
- **Supports Sass syntax**  
Writing [Sass](https://sass-lang.com/) syntax out of the box without having to set up any preprocessors or extra build tools is possible with styled-components. In your style definitions, you can use the `&` character to target the current component, use pseudo-selectors, and experiment with nesting.
- **Theming**  
styled-components have full [theming support](https://styled-components.com/docs/advanced) by exporting a `ThemeProvider` wrapper component. This component provides a theme to all React components within itself via the Context API. In the rendering tree, all styled-components will have access to the provided theme, even when they are multiple levels deep. As we continue in this tutorial, we will look deeper into the theming features of styled-components.

To learn more advantages of styled-components, check out [Kris Guzman’s article](https://blog.cloudboost.io/getting-the-most-out-of-styled-components-7-must-know-features-acba3cc15b5).

## Implementing Dark Mode

In this article, we are going to implement dark mode on a simple YouTube-like web page.

To follow along, ensure that you clone the original repository from the [`starter` branch](https://github.com/krofax/Dark-Mode-Using-Styled-Component-In-React-Apps/tree/starter).

### Setting Up

Let’s install all of the dependencies in our `package.json` file. From the terminal, run the following command:

<pre><code class="language-bash">npm install
</code></pre>

Upon its successful installation, run `npm start`. Here is what the web page looks like without dark mode implemented on it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/920a344b-9d75-4035-9f1d-bb51dc049dc6/dark-mode-resources-figure-03.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/920a344b-9d75-4035-9f1d-bb51dc049dc6/dark-mode-resources-figure-03.gif" width="600" height="306" alt="The web page to be used, without dark mode" /></a><figcaption>The web page to be used, without dark mode. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/920a344b-9d75-4035-9f1d-bb51dc049dc6/dark-mode-resources-figure-03.gif">Large preview</a>)</figcaption></figure>

To install `styled-components`, in your terminal run `npm install styled-components`.

### Implementation

To implement dark mode, we need to create four different components.

- `Theme`  
This contains the color properties of our light and dark themes.
- `GlobalStyles`  
This contains the global styles for the entire document.
- `Toggler`  
This holds the button element that toggles the functionality.
- `useDarkMode`  
This custom hook handles the logic behind the change of theme and the persistence of our theme in localStorage.

### Theme Component

In the `src` folder, you’ll see components in the `components` folder. Create a `Themes.js` file, and add the following code to it.

<pre><code class="language-javascript">export const lightTheme = {
    body: '#FFF',
    text: '#363537',
    toggleBorder: '#FFF',
    background: '#363537',
}
export const darkTheme = {
    body: '#363537',
    text: '#FAFAFA',
    toggleBorder: '#6B8096',
    background: '#999',
}
</code></pre>

Here, we’ve defined and exported `lightTheme` and `darkTheme` objects with distinct color variables. Feel free to experiment and customize the variables to suit you.

###  globalStyles Component

Remaining in your `components` folder, create a `globalStyles.js` file, and add the following code:

<pre><code class="language-javascript">import { createGlobalStyle} from "styled-components"
export const GlobalStyles = createGlobalStyle`
  body {
    background: ${({ theme }) => theme.body};
    color: ${({ theme }) => theme.text};
    font-family: Tahoma, Helvetica, Arial, Roboto, sans-serif;
    transition: all 0.50s linear;
  }
  `
</code></pre>

We’ve imported `createGlobalStyle` from styled-components. The `createGlobalStyle` method replaces the now deprecated [injectGlobal](https://www.styled-components.com/docs/api#deprecated-injectglobal) method from styled-components version 3. This method generates a React component, which, when added to your component tree, will inject global styles into the document, in our case, `App.js`.

We defined a `GlobalStyle` component and assigned `background` and `color` properties to values from the theme object. Thus, every time we switch the toggle, the values will change depending on the dark theme or light theme objects that we are passing to `ThemeProvider` (which will be created later, as we proceed).

The transition property of `0.50s` enables this change to occur a little more smoothly, so that as we toggle back and forth, we can see the changes happen.

{{% ad-panel-leaderboard %}}

### Creating Theme-Toggling Functionality

To implement the theme-toggling functionality, we need to add only a few lines of code. In the `App.js` file, add the following code (note that the highlighted code is what you should add):

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState, useEffect } from "react";</code>
<code class="language-javascript" style="background-color: #fffbd7">import {ThemeProvider} from "styled-components";
import { GlobalStyles } from "./components/Globalstyle";
import { lightTheme, darkTheme } from "./components/Themes"</code>
<code class="language-javascript">import "./App.css";
import dummyData from "./data";
import CardList from "./components/CardList";

const App = () =&gt; {
  const [videos, setVideos] = useState([]);</code>
<code class="language-javascript" style="background-color: #fffbd7">  const [theme, setTheme] = useState('light');
  const themeToggler = () =&gt; {
    theme === 'light' ? setTheme('dark') : setTheme('light')
}</code>
<code class="language-javascript">  useEffect(() =&gt; {
    const timer = setTimeout(() =&gt; {
      setVideos(dummyData);
    }, 1000);
    return () =&gt; clearTimeout(timer);
  }, []);
  return (</code>
<code class="language-javascript" style="background-color: #fffbd7">    &lt;ThemeProvider theme={theme === 'light' ? lightTheme : darkTheme}&gt;
      &lt;&gt;
      &lt;GlobalStyles/&gt;</code>
<code class="language-javascript">        &lt;div className="App"&gt;</code>
<code class="language-javascript" style="background-color: #fffbd7">          &lt;button onClick={themeToggler}&gt;Switch Theme&lt;/button&gt;</code>
<code class="language-javascript">          {
            videos.map((list, index) =&gt; {
              return (
                &lt;section key={index}&gt;
                  &lt;h2 className="section-title"&gt;{list.section}&lt;/h2&gt;
                  &lt;CardList list={list} /&gt;
                  &lt;hr /&gt;
                &lt;/section&gt;
              );
            })}
        &lt;/div&gt;</code>
<code class="language-javascript" style="background-color: #fffbd7">      &lt;/&gt;
    &lt;/ThemeProvider&gt;</code>
<code class="language-javascript">    
  );
};
export default App;
</code></pre>
</div>

The highlighted code is the one newly added to `App.js`. We’ve imported `ThemeProvider` from `styled-components`. `ThemeProvider` is a helper component in the styled-components library that provides theming support. This helper component injects a theme into all React component below itself via the Context API.

In the rendering tree, all styled-components will have access to the provided theme, even when they are multiple levels deep. Check out the section on “[Theming](https://styled-components.com/docs/advanced#theming)”.

Next, we import the `GlobalStyle` wrapper from `./components/Globalstyle`. Lastly, from the top, we import both the `lightTheme` and `darkTheme` objects from `./components/Themes`.

In order for us to create a toggling method, we need a state that holds our theme’s initial color value. So, we create a `theme` state, and set the initial state to `light`, using the `useState` hook.

Now, for the toggling functionality.

The `themeToggler` method uses a ternary operator to check the state of the `theme`, and it toggles either dark or light based on the value of the condition.

[`ThemeProvider`](https://styled-components.com/docs/advanced#theming), a styled-components helper component, wraps everything in the `return` statement and injects any components below it. Remember that our `GlobalStyles` inject **global styles** into our components; hence, it’s called inside the `ThemeProvider` wrapper component.

Lastly, we created a button with an `onClick` event that assigns our `themeToggler` method to it.

Let’s see the outcome thus far.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28507c2f-e6ec-4ba6-96a1-63f0a228bbdf/dark-mode-resources-figure-04.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28507c2f-e6ec-4ba6-96a1-63f0a228bbdf/dark-mode-resources-figure-04.gif" width="600" height="267" alt="Dark mode implemented without persistence." /></a><figcaption>Dark mode implemented without persistence (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28507c2f-e6ec-4ba6-96a1-63f0a228bbdf/dark-mode-resources-figure-04.gif">Large preview</a>)</figcaption></figure>

Our `App.js` file needs to be refactored; a lot of its code is not [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). (DRY stands for “don’t repeat yourself”, a basic principle of software development aimed at reducing repetition.) All of the logic seems to be in `App.js`; it’s good practice to separate our logic for the sake of clarity. So, we’ll create a component that handles the toggling functionality.

### Toggle Component

Still within the `components` folder, create a `Toggler.js` file, and add the following code to it:

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react'
import { func, string } from 'prop-types';
import styled from "styled-components"
const Button = styled.button`
  background: ${({ theme }) =&gt; theme.background};
  border: 2px solid ${({ theme }) =&gt; theme.toggleBorder};
  color: ${({ theme }) =&gt; theme.text};
  border-radius: 30px;
  cursor: pointer;
  font-size:0.8rem;
  padding: 0.6rem;
  }
\`;
const Toggle = ({theme,  toggleTheme }) =&gt; {
    return (
        &lt;Button onClick={toggleTheme} &gt;
          Switch Theme
        &lt;/Button&gt;
    );
};
Toggle.propTypes = {
    theme: string.isRequired,
    toggleTheme: func.isRequired,
}
export default Toggle;
</code></pre>
</div>

To keep things neat, we’ve styled our toggle button in the `Toggle` component, using the `styled` function from styled-components.

This is purely for presentation; you can style the button as you see fit.

Inside the `Toggle` component, we pass two props:

- the `theme` provides the current theme (light or dark);
- the `toggleTheme` function will be used to switch between themes.

Next, we return the `Button` component and assign a `toggleTheme` function to the `onClick` event.

Lastly, we use `propTypes` to define our types, ensuring that our `theme` is a `string` and `isRequired`, while our `toggleTheme` is `func` and `isRequired`.

### Using Custom Hooks (`useDarkMode`)

When building an application, scalability is paramount, meaning that our business logic must be reusable, so that we can use it in many places and even in different projects.

That is why it would be great to move our toggling functionality to a separate component. For that, we would create our own custom hook.

Let’s create a new file named `useDarkMode.js` in the `components` folder, and move our logic to this file, with some tweaks. Add the following code to the file:

<div class="break-out">

 <pre><code class="language-javascript">import { useEffect, useState } from 'react';
export const useDarkMode = () => {
    const [theme, setTheme] = useState('light');

    const setMode = mode => {
        window.localStorage.setItem('theme', mode)
        setTheme(mode)
    };

    const themeToggler = () => {
        theme === 'light' ? setMode('dark') : setMode('light')
    };

    useEffect(() => {
        const localTheme = window.localStorage.getItem('theme');
        localTheme && setTheme(localTheme)
    }, []);
    return [theme, themeToggler]
};
</code></pre>
</div>

We’ve added a few things here.

- `setMode`  
We use `localStorage` to persist between sessions in the browser. So, if a user has chosen the dark or light theme, that’s what they’ll get upon their next visit to the app or if they reload the page. Hence, this function sets our state and passes `theme` to `localStorage`.
- `themeToggler`  
This function uses a ternary operator to check the state of the theme and toggles either dark or light based on the truth of the condition.
- `useEffect`  
We’ve implemented the [`useEffect`](https://css-tricks.com/intro-to-react-hooks/#article-header-id-1) hook to check on component mounting. If the user has previously selected a theme, we will pass it to our `setTheme` function. In the end, we will return our `theme`, which contains the chosen `theme` and the `themeToggler` function to switch between modes.

I think you’ll agree that our dark-mode component looks sleek.

Let’s head over to `App.js` for the final touches.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState, useEffect } from "react";
import {ThemeProvider} from "styled-components";</code>
<code class="language-javascript" style="background-color: #fffbd7">import  {useDarkMode} from "./components/useDarkMode"</code>
<code class="language-javascript">import { GlobalStyles } from "./components/Globalstyle";
import { lightTheme, darkTheme } from "./components/Themes"
import Toggle from "./components/Toggler"
import "./App.css";
import dummyData from "./data";
import CardList from "./components/CardList";
const App = () =&gt; {
  const [videos, setVideos] = useState([]);</code>
<code class="language-javascript" style="background-color: #fffbd7">  const [theme, themeToggler] = useDarkMode();

  const themeMode = theme === 'light' ? lightTheme : darkTheme;</code>
<code class="language-javascript">
  useEffect(() =&gt; {
    const timer = setTimeout(() =&gt; {
      setVideos(dummyData);
    }, 1000);
    return () =&gt; clearTimeout(timer);
  }, []);

  return (</code>
<code class="language-javascript" style="background-color: #fffbd7">    &lt;ThemeProvider theme={themeMode}&gt;</code>
<code class="language-javascript">      &lt;&gt;
      &lt;GlobalStyles/&gt;
        &lt;div className="App"&gt;</code>
<code class="language-javascript" style="background-color: #fffbd7">          &lt;Toggle theme={theme} toggleTheme={themeToggler} /&gt;</code>
<code class="language-javascript">          {
            videos.map((list, index) =&gt; {
              return (
                &lt;section key={index}&gt;
                  &lt;h2 className="section-title"&gt;{list.section}&lt;/h2&gt;
                  &lt;CardList list={list} /&gt;
                  &lt;hr /&gt;
                &lt;/section&gt;
              );
            })}
        &lt;/div&gt;
      &lt;/&gt;
    &lt;/ThemeProvider&gt;
    
  );
};
export default App;
</code></pre>
</div>

The highlighted code is newly added to `App.js`.

First, we import our custom hook, destructure the `theme` and `themeToggler` props, and set it with the `useDarkMode` function.

Note that the `useDarkMode` method **replaces** our `theme` state, which was initially in `App.js`.

We declare a `themeMode` variable, which renders either a light or dark theme based on the condition of the `theme` mode at the time.

Now, our `ThemeProvider` wrapper component is assigned our just recently created `themeMode` variable to the `theme` prop.

And lastly, in place of the regular button, we pass in the `Toggle` component.

Remember that in our `Toggle` component, we defined and styled a button and passed both `theme` and `toggleTheme` to them as props. So, all we have to do is pass these props appropriately to the `Toggle` component, which will act as our button in `App.js`.

Yes! Our dark mode is set, and it persists, not changing color when the page is refreshed or visited in a new tab.

{{% ad-panel-leaderboard %}}

Let’s see the outcome in action:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b96fefb-d7f3-422d-8e9d-9d38934a381c/dark-mode-resources-figure-05.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b96fefb-d7f3-422d-8e9d-9d38934a381c/dark-mode-resources-figure-05.gif" width="600" height="275" alt="Dark mode implemented, but with a glitch in the button color when the browser reloads." /></a><figcaption>Dark mode implemented, but with a glitch in the button color when the browser reloads. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b96fefb-d7f3-422d-8e9d-9d38934a381c/dark-mode-resources-figure-05.gif">Large preview</a>)</figcaption></figure>

Almost everything works well, but there is one small thing we can do to make our experience splendid. Switch to the dark theme and then reload the page. Do you see that the blue color in the button loads before the gray for a brief moment? That happens because our `useState` hook initiates the `light` theme initially. After that, `useEffect` runs, checks `localStorage`, and only then sets the `theme` to `dark`. Let’s jump over to our custom hook `useDarkMode.js` and add a little code:

<div class="break-out">

 <pre><code class="language-javascript">import { useEffect, useState } from 'react';
export const useDarkMode = () => {
    const [theme, setTheme] = useState('light');</code>
<code class="language-javascript" style="background-color: #fffbd7">    const [mountedComponent, setMountedComponent] = useState(false)</code>
<code class="language-javascript">    const setMode = mode => {
        window.localStorage.setItem('theme', mode)
        setTheme(mode)
    };
    const themeToggler = () => {
        theme === 'light' ? setMode('dark') : setMode('light')
    };
    useEffect(() => {
        const localTheme = window.localStorage.getItem('theme');
        localTheme ? setTheme(localTheme) : setMode('light')</code>
<code class="language-javascript" style="background-color: #fffbd7">        setMountedComponent(true)</code>
<code class="language-javascript">    }, []);
    return [theme, themeToggler,</code> <code class="language-javascript" style="background-color: #fffbd7">mountedComponent</code><code class="language-javascript">]</code>
<code class="language-javascript">};
</code></pre>
</div>

The highlighted code is the only one added to `useDarkMode.js`. We’ve created another state named `mountedComponent` and set the default value to `false` using the `useState` hook. Next, inside the `useEffect` hook, we set the `mountedComponent` state to `true` using `setMountedComponent`. Lastly, in the `return` array, we include the `mountedComponent` state.

Finally, let’s add a bit of code in `App.js` to make it all work.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState, useEffect } from "react";
import {ThemeProvider} from "styled-components";
import  {useDarkMode} from "./components/useDarkMode"
import { GlobalStyles } from "./components/Globalstyle";
import { lightTheme, darkTheme } from "./components/Themes"
import Toggle from "./components/Toggler"
import "./App.css";
import dummyData from "./data";
import CardList from "./components/CardList";
const App = () =&gt; {
  const [videos, setVideos] = useState([]);</code>
<code class="language-javascript" style="background-color: #fffbd7">  const [theme, themeToggler, mountedComponent] = useDarkMode();</code>
<code class="language-javascript">  const themeMode = theme === 'light' ? lightTheme : darkTheme;
  useEffect(() =&gt; {
    const timer = setTimeout(() =&gt; {
      setVideos(dummyData);
    }, 1000);
    return () =&gt; clearTimeout(timer);
  }, []);</code>
<code class="language-javascript" style="background-color: #fffbd7">  if(!mountedComponent) return &lt;div/&gt;</code>
<code class="language-javascript">  return (
    &lt;ThemeProvider theme={themeMode}&gt;
      &lt;&gt;
      &lt;GlobalStyles/&gt;
        &lt;div className="App"&gt;
          &lt;Toggle theme={theme} toggleTheme={themeToggler} /&gt;
          {
            videos.map((list, index) =&gt; {
              return (
                &lt;section key={index}&gt;
                  &lt;h2 className="section-title"&gt;{list.section}&lt;/h2&gt;
                  &lt;CardList list={list} /&gt;
                  &lt;hr /&gt;
                &lt;/section&gt;
              );
            })}
        &lt;/div&gt;
      &lt;/&gt;
    &lt;/ThemeProvider&gt;
    
  );
};
export default App;
</code></pre>
</div>

We’ve added our `mountedComponent` state as a prop in our `useDarkMode` hook, and we’ve checked whether our component has mounted, because this is what happens in the `useEffect` hook. If it hasn’t happened yet, then we will render an empty `div`.

Let’s see the outcome of our dark-mode web page.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/113afbae-ee37-4393-97b9-ce7263288b46/dark-mode-resources-figure-06.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/113afbae-ee37-4393-97b9-ce7263288b46/dark-mode-resources-figure-06.gif" width="599" height="276" alt="Final result of dark mode" /></a><figcaption>Final result of dark mode (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/113afbae-ee37-4393-97b9-ce7263288b46/dark-mode-resources-figure-06.gif">Large preview</a>)</figcaption></figure>

Now, you’ll notice that while in dark mode, when the page reloads, the button’s color doesn’t change.

## Conclusion

Dark mode is increasingly becoming a user preference, and implementing it in a React web app is a lot easier when using the `ThemeProvider` theming wrapper in styled-components. Go ahead and experiment with styled-components as you implement dark mode; you could add icons instead of a button.

Please do share your feedback and experience with the theming feature in styled-components in the comments section below. I’d love to see what you come up with!

*The supporting repository for this article is [available on GitHub](https://github.com/krofax/Dark-Mode-Using-Styled-Component-In-React-Apps). Also, check it out [on CodeSandbox](https://codesandbox.io/s/inspiring-khorana-f7c0v?fontsize=14&hidenavigation=1&theme=dark).*

### References

- “[Documentation](https://styled-components.com/docs)”, styled-components
- “[Create a Dark Mode of your app using Styled Components](https://medium.com/swlh/create-a-dark-mode-of-your-app-using-styled-components-a44bc5a59330)”, Tom Nolan, Medium

{{< signature "ks, ra, il, al" >}}
