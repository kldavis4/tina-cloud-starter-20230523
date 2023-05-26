---
title: 'Building Mobile Apps With Ionic And React'
slug: building-mobile-apps-ionic-react
author: ahmed-bouchefra
image: >-
 https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0ad88ac-ba4e-49da-9c5b-3ebec31de23c/bouchfra-ionic-react.png
date: 2019-08-07T12:30:00+02:00
summary: >-
  React developers can get the advantages of Ionic to build hybrid mobile apps and progressive web apps. In this tutorial, we’ll be using Ionic and React to build a mobile app from scratch.
description: >-
  React developers can get the advantages of Ionic to build hybrid mobile apps and progressive web apps. In this tutorial, we’ll be using Ionic and React to build a mobile app from scratch.
categories:
  - Apps
  - React
  - Mobile
---
Ionic has recently added support for React; so now, React developers can get the advantages of Ionic to build hybrid mobile apps and progressive web apps (PWAs). In this post, we’ll show you how to get started using Ionic with React by building a simple demo app from scratch.

## Prerequisites

In order to properly follow this tutorial, you'll need the following prerequisites:

- recent versions of Node.js and npm installed on your system,
- working knowledge of TypeScript and React.

You can check that you have the [latest Node](https://nodejs.org/en/).js version (v10) installed by running the following command:

<pre><code class="language-javascript">$ node -v</code></pre>

## Introducing React And Ionic

Let's start with brief introductions to both React and Ionic.

According to the [official website](https://reactjs.org/tutorial/tutorial.html):

<blockquote>“React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called ‘components’.”</blockquote>

React focuses on building UIs and doesn't provide any built-in tools for the common tasks required in web development, such as fetching remote data and routing, so you'll need to use some existing third-party libraries for these tasks.

According to the [Ionic website](https://ionicframework.com/):

<blockquote>“Ionic Framework is the free, open-source mobile UI toolkit for developing high-quality cross-platform apps for native iOS, Android, and the web &mdash; all from a single codebase.”</blockquote>

Basically, it’s a set of UI components that you can use with plain JavaScript or any popular front-end framework or library, such as Angular, React or Vue, to build a hybrid mobile app and PWA.

In this tutorial, we'll see and use some Ionic UI components such as the following:

- [IonMenu](https://ionicframework.com/docs/api/menu): With this, a navigation drawer will slide in from the side of the current view.
- [IonToolbar](https://ionicframework.com/docs/api/toolbar): These top bars are positioned above or below the content.
- [IonHeader](https://ionicframework.com/docs/api/header): This parent component holds the toolbar component.
- [IonContent](https://ionicframework.com/docs/api/content): This component provides a content area, with methods to control the scrollable area and other things. You need only one content component inside a single view.
- [IonList](https://ionicframework.com/docs/api/list): This component contains items with similar data content, such as images and text. It's made up of IonItem objects.
- [IonItem](https://ionicframework.com/docs/api/item): This component may contain text, icons, avatars, images, inputs and any other native or custom element.
- [IonButton](https://ionicframework.com/docs/api/button): This component provides a clickable element, which can be used in a form or anywhere that needs simple, standard button functionality.

{{% feature-panel %}}

## Installing Ionic CLI v5

Ionic’s command line interface (CLI), version 5, has support for creating Ionic projects based on React. So, let's get started by installing the tool from npm.

Open a CLI, and run the following command:

<pre><code class="language-javascript">$ npm install -g ionic</code></pre>

At the time of writing, Ionic’s CLI v5.2.3 is the latest.

**Note**: *According to how you installed Node.js in your system, you may need to add **sudo** before your command in macOS or Linux or run the command prompt as administrator in Windows if you get any permission errors. You can also simply fix your [npm permissions](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) or use a tool such as [nvm](https://github.com/nvm-sh/nvm).*

Next, install `Cordova Resources` (which is used to generate Cordova resources locally) and `Native Run` (used to deploy app binaries to devices):

<pre><code class="language-javascript">$ npm install -g cordova-res native-run</code></pre>

These are required only if you want to test your application on a real mobile device or emulator.

## Creating An Ionic And React Project

Now, let's create a project based on React. Go back to your terminal, make sure you are in your working directory, and run the following command:

<pre><code class="language-javascript">$ ionic start myApp --type=react</code></pre>

We use `--type=react` to generate a project based on React. You'll next need to choose a starter template from the available ones. Let's pick `sidemenu` for a starter template with a side menu and navigation.

After generating the project and installing the dependencies, you can serve your app locally using the following commands:

<pre><code class="language-javascript">$ cd ./myApp
$ ionic serve</code></pre>

Your app will be available from the [https://localhost:8100](https://localhost:8100) address, and you can actually use your web browser to start playing with it.

Ionic is called a hybrid mobile framework because it makes use of web technologies that were originally designed to create web apps, along with a native container ([Cordova](https://cordova.apache.org/) or [Capacitor](https://capacitor.ionicframework.com/)), to build mobile apps without using native technologies for the target platforms, such as Java or Kotlin for Android or Swift for iOS.

Because your mobile app is actually a web application, you can do most development by testing in a web browser without using an emulator or a real mobile device, except for testing native device features such as the camera or the SQLite storage, in case you’ve used them in your app. In fact, it's even possible to use certain techniques to [mimic the plugins](https://www.techiediaries.com/mocking-native-sqlite-plugin/) that provide the native features and do the entire testing during development in your web browser.

{{% ad-panel-leaderboard %}}

## Cleaning Our Project

We have the app’s basic structure, with two pages (home and list) and a menu. Let's remove the list page since it's just boilerplate code.

First, remove the `src/pages/List.tsx` file, then open the `src/App.tsx` file, and remove the entry for the list page from the `appPages` array:

<pre><code class="language-javascript">const appPages: AppPage[] = [
  {
    title: 'Home',
    url: '/home',
    icon: home
  }
];</code></pre>

Also, remove the import of the list page from the file:

<pre><code class="language-javascript">import  List  from  './pages/List';</code></pre>

Next, remove `<Route path="/:tab(home)/list" component={List} exact={true} />` from the `App` component:

<div class="break-out">

<pre><code class="language-javascript">const App: React.FunctionComponent = () => (
  &lt;IonApp&gt;
    &lt;IonReactRouter&gt;
      &lt;IonSplitPane contentId="main"&gt;
        &lt;Menu appPages={appPages} /&gt;
        &lt;IonPage id="main"&gt;
          &lt;IonRouterOutlet&gt;
            &lt;Route path="/:tab(home)" component={Home} exact={true} /&gt;
            &lt;Route exact path="/" render={() => &lt;Redirect to="/home" /&gt;} /&gt;
          &lt;/IonRouterOutlet&gt;
        &lt;/IonPage&gt;
      &lt;/IonSplitPane&gt;
    &lt;/IonReactRouter&gt;
  &lt;/IonApp&gt;
);

export default App;</code></pre>
</div>

The `App` component is the root component that gets rendered by our application. If you open the `src/index.tsx` file, you'll find the following code:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(&lt;App /&gt;, document.getElementById('root'));</code></pre>
</div>

[The render() method](https://reactjs.org/docs/react-dom.html#reference) is used to render a React element into the DOM in the supplied `root` element.

## Theming The App

Having created, served and cleaned our Ionic project, let's now see how we can change the colors of the UI so that it looks more professional.

Let's get started with the side menu. Open the `src/components/Menu.tsx` file, and add a `color` attribute with a `primary` value to the `IonToolbar`, `IonContent`, `IonList` and `IonItem` UI components:

<div class="break-out">

<pre><code class="language-javascript">const Menu: React.FunctionComponent<MenuProps> = ({ appPages }) => (
  &lt;IonMenu contentId="main"&gt;
    &lt;IonHeader&gt;
      &lt;IonToolbar color="primary"&gt;
        &lt;IonTitle&gt;Menu&lt;/IonTitle&gt;
      &lt;/IonToolbar&gt;
    &lt;/IonHeader&gt;
    &lt;IonContent color="primary"&gt;
      &lt;IonList style= {{ background : '#3880ff'}} color="primary"&gt;
        {appPages.map((appPage, index) => {
          return (
            &lt;IonMenuToggle key={index} auto-hide="false"&gt;
              &lt;IonItem color="primary" href={appPage.url}&gt;
                &lt;IonIcon slot="start" icon={appPage.icon} /&gt;
                &lt;IonLabel&gt;{appPage.title}&lt;/IonLabel&gt;
              &lt;/IonItem&gt;
            &lt;/IonMenuToggle&gt;
          );
        })}
      &lt;/IonList&gt;
    &lt;/IonContent&gt;
  &lt;/IonMenu&gt;
);</code></pre>
</div>

Ionic provides some default colors (primary, secondary, tertiary, success, warning, danger, light, medium and dark) that can be used to change the color of UI components. A color can be applied to an Ionic component in order to change the default colors using the `color` attribute. See “[Colors](https://ionicframework.com/docs/theming/colors)” for more information.

These colors have default values, but you can customize them via some predefined CSS variables. See “[Modifying Colors](https://ionicframework.com/docs/theming/colors#modifying-colors)“.

This is a screenshot of our menu:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a0fad5b-bad4-4e89-adae-6321a7951d6f/ionic-menu.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a0fad5b-bad4-4e89-adae-6321a7951d6f/ionic-menu.png" alt="Ionic menu" /></a><figcaption>Ionic menu. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a0fad5b-bad4-4e89-adae-6321a7951d6f/ionic-menu.png'>Large preview</a>)</figcaption></figure>

Next, let's change the color of the Home page. Open the `src/pages/Home.tsx` file, and set the `color` attribute of the `IonToolbar` and `IonContent` components to `primary`:

<pre><code class="language-javascript">const HomePage: React.FunctionComponent = () => {
  return (
    &lt;&gt;
      &lt;IonHeader&gt;
        &lt;IonToolbar color="primary"&gt;
          &lt;IonButtons slot="start"&gt;
            &lt;IonMenuButton /&gt;
          &lt;/IonButtons&gt;
          &lt;IonTitle&gt;Home&lt;/IonTitle&gt;
        &lt;/IonToolbar&gt;
      &lt;/IonHeader&gt;
      &lt;IonContent color="primary" &gt;

      &lt;/IonContent&gt;
    &lt;/&gt;
  );
};</code></pre>

This is a screenshot of the page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a19d53-77ef-49a4-a491-59ebd38e7436/ionic-home.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a19d53-77ef-49a4-a491-59ebd38e7436/ionic-home.png" alt="Ionic home" /></a><figcaption>Ionic home. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a19d53-77ef-49a4-a491-59ebd38e7436/ionic-home.png'>Large preview</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

## Installing Axios And Consuming A REST API

We'll see how to install Axios and consume a third-party RESTful API in our application, and we'll also see how to display the fetched data using Ionic card and list components.

Having themed our application, let's now see how to fetch data using Axios. We'll use the third-party API available from [NewsAPI.org](https://newsapi.org/).

First, we need to grab an API key, so that we can communicate with the API. Go to the [registration](https://newsapi.org/register) page, enter your information, and register an account. You'll be given an API key; note it, and let's continue.

Head back to your terminal, and run the following command to install Axios:

<pre><code class="language-javascript">$ npm install axios --save</code></pre>

Next, open the `src/pages/Home.tsx` file, and start by importing Axios and `IonButton`:

<pre><code class="language-javascript">import {
  IonButton
} from '@ionic/react';

import axios from 'axios';</code></pre>

Next, define the `API_KEY` and `URL` constant variables:

<div class="break-out">

<pre><code class="language-javascript">const  API_KEY  =  "&lt;YOUR_API_KEY_HERE&gt;";
const  URL  =  `https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=${API_KEY}`;</code></pre>
</div>

In the URL variable, we’ll add an endpoint to get the top headlines from our source, TechCrunch. You can use any source you want from the available [sources](https://newsapi.org/sources).

**Note**: *Make sure to put your own API key in the `API_KEY` variable.*

Next, define the `fetchArticles()` method as follows:

<pre><code class="language-javascript">const fetchArticles = () => {

  return axios({
    url: URL,
    method: 'get'
  }).then(response => {

    console.log(response);
    return response.data;
  })
};</code></pre>

We simply call the `axios()` method to send a GET request to the news endpoint, and the result from the method is a promise that needs to be resolved in order to get the news data.

Next, update the `HomePage` component as follows to call the `fetchArticles()` method and resolve the returned promise:

<div class="break-out">

<pre><code class="language-javascript">const HomePage: React.FunctionComponent = () => {

  const [articles, setArticles] = React.useState([]);
  const items: any[] = [];

  React.useEffect(() => {

    fetchArticles().then(data => setArticles(data.articles));

  }, []);

  return (
    &lt;&gt;
      &lt;IonHeader&gt;
        &lt;IonToolbar color="primary"&gt;
          &lt;IonButtons slot="start"&gt;
            &lt;IonMenuButton /&gt;
          &lt;/IonButtons&gt;
          &lt;IonTitle&gt;Home&lt;/IonTitle&gt;
        &lt;/IonToolbar&gt;
      &lt;/IonHeader&gt;
      &lt;IonContent color="primary" &gt;
        &lt;IonList color="primary"&gt;

          {
            articles.map(a => {

              return (
                &lt;IonItem&gt;
                  {a['title']}
                  &lt;IonButton href={a['url']} color="primary" slot="end"&gt;Read&lt;/IonButton&gt;
                &lt;/IonItem&gt;
              );
            })
          }

        &lt;/IonList&gt;
      &lt;/IonContent&gt;
    &lt;/&gt;
  );
};</code></pre>
</div>

In our function component, we first call the `useState()` hook of React to create the `articles` state variable, which will hold the news articles after we fetch them from the API.

`useState()` returns the state variable, which has the empty array as its initial value and a function that we can use to change the value of the variable. We use [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to unpack the values from the returned pair into distinct variables (i.e. `articles` and `setArticles()`).

<p class="c-pre-sidenote--left">Next, we call the <code>useEffect()</code> hook to perform a side effect in our component. In our case, the side effect is to fetch data from the news API using the <code>fetchArticles()</code> method, which returns a promise. Once the promise is resolved, we call the <code>setArticles()</code> method to assign the news data to the <code>articles</code> variable.</p><p class="c-sidenote c-sidenote--right">Both <code>useState()</code> and <code>useEffect()</code> are built-in React hooks that were introduced in React 16.8; they simply let you use state and other React features without having to write a class. The <code>useEffect()</code> hook is equivalent to calling the <code>componentDidMount</code>, <code>componentDidUpdate</code> and <code>componentWillUnmount</code> lifecycle methods combined in class-based components.</p>

Finally, in the view template, we iterate over the `articles` array using the `map()` method, and we display the title of each news article inside an `IonItem` element of the `IonList` component, and also a button that takes us to the page of the full article.

This is a screenshot of the page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636438f9-83e5-400c-b1dc-18c12caed2bd/ionic-news.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636438f9-83e5-400c-b1dc-18c12caed2bd/ionic-news.png" alt="Ionic news app" /></a><figcaption>Ionic news app (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636438f9-83e5-400c-b1dc-18c12caed2bd/ionic-news.png'>Large preview</a>)</figcaption></figure>

You can find the source code in this [GitHub repository](https://github.com/techiediaries/ionic-react-news-app).

## Conclusion

In this tutorial, we have started using both Ionic and React and used them to build a simple mobile application that fetches and displays news data from a third-party API using the Axios client. We have also seen how to use hooks in React &mdash; namely, the `useState()` and `useEffect()` hooks &mdash; to create state and perform side effects inside React function components. With Ionic, we've seen how easy it is to generate a project based on React and how we can theme the application using the color attributes of components.

{{< signature "dm, al, yk, ra, il" >}}
