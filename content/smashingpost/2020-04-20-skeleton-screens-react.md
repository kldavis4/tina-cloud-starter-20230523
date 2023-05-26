---
title: 'Implementing Skeleton Screens In React'
slug: skeleton-screens-react
author: blessing-krofegha
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dca508c-bb0a-4824-8365-474739506785/skeleton-screens-react.png
date: 2020-04-20T10:00:00.000Z
summary: >-
  In this tutorial, you’ll learn what a skeleton screen UI is and some types of skeleton screen libraries, along with their pros and cons. We’ll build a YouTube-like skeleton screen UI using [React Loading Skeleton](https://github.com/dvtng/react-loading-skeleton). Then, you can experiment on your own with the skeleton screen React package of your choice.
description: >-
  Spinners and loaders have traditionally been the way to tell users that content is going to take a while to load. While this approach is great, it’s quickly becoming obsolete in modern development.
categories:
  - React
  - Tools
  - Techniques
---

Spinners and loaders have traditionally been the way to tell users that content is going to take a while to load. While this approach is great, it’s quickly becoming obsolete in modern development. Skeleton screens are becoming the perfect replacement for traditional loaders because they focus on progress rather than wait times, hence reducing loading-time frustration.

In this article, we won’t be going through the basics of CSS React or JavaScript syntax, so you don’t have to be an expert in either of these languages to follow along.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f973477d-7dcc-47a8-9ab9-510a97875c49/01-skeleton-screens-react.gif"><img class="breakout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f973477d-7dcc-47a8-9ab9-510a97875c49/01-skeleton-screens-react.gif" width="609" height="313" alt="The difference between a loader and a skeleton screen UI" /></a><figcaption>The difference between a loader and a skeleton screen UI (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f973477d-7dcc-47a8-9ab9-510a97875c49/01-skeleton-screens-react.gif">Large preview</a>)</figcaption></figure>

UI and UX experts teach us that, while users wait for content to load on a page, we should keep them engaged.

The idea behind using spinners to engage users before content loads is great; however, the result can be less than ideal because most users will get bored staring at a dummy animated spinner like it’s a clock. [Luke Wroblewski elaborates](https://www.lukew.com/ff/entry.asp?1797) on this.

Skeleton screens offer a better user experience by reducing loading-time frustration. By focusing on progress instead of wait times, it create the illusion for users that information will be incrementally displayed on the screen. Bill Chung in his [research confirms](https://uxdesign.cc/what-you-should-know-about-skeleton-screens-a820c45a571a) this.

## What Is a Skeleton Screen?

A skeleton screen is a version of the UI that doesn’t contain actual content; instead, it mimics the page’s layout by showing its elements in a shape similar to the actual content as it is loading and becoming available (i.e. when network latency allows).

A skeleton screen is essentially a wireframe of the page, with placeholder boxes for text and images.

{{% feature-panel %}}

## What’s Unique About a Skeleton Screen?

A skeleton UI resembles the page’s actual UI, so users will understand how quickly the web or mobile app will load even before the content has shown up. Here are a couple of reasons why you might want to consider using skeleton screens in your next project:

- mimicking a page’s layout is easier with a skeleton screen,
- contents loads progressively (not all at once).

Skeleton screens are also referred to as:

- ghost elements,
- content placeholders,
- content loaders.

Blockchain.com, YouTube, Facebook, Medium, and other big tech companies display skeleton screens while their content loads to boost the UX.

### Blockchain.com

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca566f0d-f177-46ea-a3dd-345ade848c8b/02-skeleton-screens-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca566f0d-f177-46ea-a3dd-345ade848c8b/02-skeleton-screens-react.png" sizes="100vw" caption="Blockchain.com’s partially loaded state (notice how a skeleton is used in the graph analytics) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca566f0d-f177-46ea-a3dd-345ade848c8b/02-skeleton-screens-react.png'>Large preview</a>)" alt="Blockchain.com skeleton screen UI" >}}

### Medium

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bf4ac8-84b6-4851-893c-ba2cbdd02eaa/03-skeleton-screens-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bf4ac8-84b6-4851-893c-ba2cbdd02eaa/03-skeleton-screens-react.png" sizes="100vw" caption="Medium’s skeleton UI (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bf4ac8-84b6-4851-893c-ba2cbdd02eaa/03-skeleton-screens-react.png'>Large preview</a>)" alt="Medium skeleton screen UI" >}}

### LinkedIn

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15a70140-841d-4290-a06d-909d5fc35aa0/04-skeleton-screens-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15a70140-841d-4290-a06d-909d5fc35aa0/04-skeleton-screens-react.png" sizes="100vw" caption="LinkedIn’s home feed loading state in 2018 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15a70140-841d-4290-a06d-909d5fc35aa0/04-skeleton-screens-react.png'>Large preview</a>)" alt="LinkedIn skeleton screen UI" >}}

## Types of Skeleton Screens

There are [different kinds of skeleton screens](https://alligator.io/react/skeleton-screens-react-and-react-native/). The major ones are text placeholders and image (or color) placeholders.

Most developers prefer to use text placeholders as the skeleton UI on their pages because they’re easy to build, and the developer doesn’t require any details about the substance of the actual content; instead the skeleton mimics the UI.

Color placeholders are harder to build because they require details about the content.

Some popular packages make implementing skeleton screens in web apps easier. Let’s take a closer look at both of them:

- [React Placeholder](https://github.com/buildo/react-placeholder)
- [React Loading Skeleton](https://github.com/dvtng/react-loading-skeleton)

We’ll look at the pros and cons of each package, before considering which to use for our application.

## React Placeholder

### Pros

- Placeholder components are used to create a custom skeleton UI.
- Pulse animation (i.e. motion effect on an element) is supported.
- It comes with a component-based API.

### Cons

- Skeleton components are maintained separately, so updating styles of a component possibly requires updating the skeleton component as well.
- The learning curve is not linear because there are multiple components for different needs.

The following is an example of a skeleton component using the `react-placeholder` package:

<div class="break-out">

 <pre><code class="language-javascript">import { TextBlock, RectShape } from 'react-placeholder/lib/placeholders';
import ReactPlaceholder from 'react-placeholder';

const GhostPlaceholder = () =&gt; (
  &lt;div className='my-placeholder'&gt;
    &lt;RectShape color='gray' style={{width: 25, height: 70}} /&gt;
    &lt;TextBlock rows={6} color='blue'/&gt;
  &lt;/div&gt;
);
&lt;ReactPlaceholder ready={ready} customPlaceholder={&lt;GhostPlaceholder /&gt;}&gt;
  &lt;MyComponent /&gt;
&lt;/ReactPlaceholder&gt;
</code></pre>
</div>

Importing `TextBlock` and `RectShape` from `react-placeholder/lib/placeholder` and `ReactPlaceholder` from `react-placeholder`, we’ve created a functional component named `GhostPlaceholder`. `GhostPlaceholder` has a div, and inside the div we’ve used the RectShape component, which describes the dimensions of a rectangle, passes the value of any color, and defines the rectangle’s styles.

Next, we used the `TextBlock` component to set the values for the rows and color. The `TextBlock` component defines the number of rows and color of text.

We pass `MyComponent` as a child of the `ReactPlaceholder` component, which receives `ready` and the `GhostPlaceholder` component as values for its `ready` and `customPlaceholder` props.

The `MyComponent` will load when the skeleton screen UI is shown.

To learn more, [check the documentation](https://github.com/buildo/react-placeholder).

{{% ad-panel-leaderboard %}}

## React Loading Skeleton

### Pros

- It is API-based, and it has one component with props for all customization.
- It can be used as a separate skeleton component and also inside any component directly, so it’s flexible.
- It supports theming and Pulse animation.

### Cons

- It’s easy to implement for a simple skeleton UI, but complicated for more complex skeletons.
- Having a separate skeleton component will make it harder to maintain when the UI and styles change.

The following is an example of React Loading Skeleton:

<div class="break-out">

 <pre><code class="language-javascript">import Skeleton, { SkeletonTheme } from "react-loading-skeleton";

const SkeletonComponent = () =&gt; (
  &lt;SkeletonTheme color="#202020" highlightColor="#444"&gt;
    &lt;section&gt;
      &lt;Skeleton height={50} width={50} /&gt;
    &lt;/section&gt;
  &lt;/SkeletonTheme&gt;
);
</code></pre>
</div>

We’ve imported `Skeleton` and `SkeletonTheme` from the `react-loading-skeleton` library, then created a functional component that renders the `SkeletonTheme` component, with `color` and `hightlightColor` as properties.

The `SkeletonTheme` component is used for theming (for example, adding color effects to the skeleton UI).

Finally, inside the section, we define the `Skeleton` component, with height and width properties and their appropriate values passed in.

## Building a YouTube-Like Skeleton Screen UI

Let’s create a YouTube-like skeleton screen, using React Loading Skeleton, to show how a skeleton UI works.

### Set Up React

The easiest way to set up React is to use [Create React App](https://create-react-app.dev/docs/getting-started/), which is “an officially supported way to create single-page React applications. It offers a modern build setup with no configuration.”

We’ll use it to bootstrap the application that we’ll be building. From your terminal, run the command below:

<div class="break-out">

 <pre><code class="language-bash">npx create-react-app skeleton-screens && cd skeleton-screens
</code></pre>
</div>

Once the installation has completed, start the React server by running `npm start`:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2920640-c8cc-4cd3-8fb4-d7660a3c0085/05-skeleton-screens-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2920640-c8cc-4cd3-8fb4-d7660a3c0085/05-skeleton-screens-react.png" sizes="100vw" caption="React welcome page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2920640-c8cc-4cd3-8fb4-d7660a3c0085/05-skeleton-screens-react.png'>Large preview</a>)" alt="React app - Scaffold React app" >}}

### Create the YouTube UI Without a Skeleton Screen

First, let’s input YouTube dummy data. Real endpoints would normally be used instead of dummy data, but in this tutorial we will use dummy data.

Create a file in your `src/` folder, and name it `data.js`, add the following code to it.

<div class="break-out">

 <pre><code class="language-javascript">const dummyData= [
  {
    section: "Recommended",
    channel: "CNN",
    items: [
      {
        id: "fDObf2AeAP4",
        image: "https://img.youtube.com/vi/fDObf2AeAP4/maxresdefault.jpg",
        title: "75 million Americans ordered to stay home",
        views: "1.9M views",
        published: "3 days agos"
      },
      {
        id: "3AzIgAa0Cm8",
        image: "https://img.youtube.com/vi/3AzIgAa0Cm8/maxresdefault.jpg",
        title: "Gupta: The truth about using chloroquine to fight coronavirus pandemic",
        views: "128K views",
        published: "4 hours ago"
      },
      {
        id: "92B37aXykYw",
        image: "https://img.youtube.com/vi/92B37aXykYw/maxresdefault.jpg",
        title: "Willie Jones STUNS Simon Cowell In Pitch Perfect Performance of 'Your Man'!",
        views: "2.47 million views",
        published: "1 month ago"
      },
      {
        id: "J6rVaFzOEP8",
        image: "https://img.youtube.com/vi/J6rVaFzOEP8/maxresdefault.jpg",
        title: "Guide To Becoming A Self-Taught Software Developer",
        views: "104K views",
        published: "17 days ago"
      },
      {
        id: "Wbk8ZrfU3EM",
        image: "https://img.youtube.com/vi/Wbk8ZrfU3EM/maxresdefault.jpg",
        title: "Tom Hanks and Rita Wilson test positive for coronavirus",
        views: "600k views",
        published: "1 week ago"
      },
      {
        id: "ikHpFgKJax8",
        image: "https://img.youtube.com/vi/ikHpFgKJax8/maxresdefault.jpg",
        title: "Faces Of Africa- The Jerry Rawlings story",
        views: "2.3 million views",
        published: "2014"
      }
    ]
  },
  {
    section: "Breaking News",
    channel: "CGTN America",
    items: [
      {
        id: "tRLDPy1A8pI",
        image: "https://img.youtube.com/vi/tRLDPy1A8pI/maxresdefault.jpg",
        title: "Is Trump blaming China for COVID-19? You decide.",
        views: "876k views",
        published: "9 days ago"
      },
      {
        id: "2ulH1R9hlG8",
        image: "https://img.youtube.com/vi/2ulH1R9hlG8/maxresdefault.jpg",
        title: "Journalist still goes to office during pandemic, see her daily routine",
        views: "873 views",
        published: "3 hours ago"
      },
      {
        id: "TkfQ9MaIgU",
        image: "https://img.youtube.com/vi/_TkfQ9MaIgU/maxresdefault.jpg",
        title: "How are small businesses going to survive the economic downturn of the COVID-19 era?",
        views: "283 views",
        published: "4 day ago"
      }
    ]
  }
];
export default dummyData;
</code></pre>
</div>

To replicate YouTube’s format, we’ve created dummy data that has an array of objects, with properties such as ID, image, title, number of views, and publication date.

Next, let’s create our YouTube UI. We will have three components:

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>Card</code></td>
      <td>Holds the details of the video’s thumbnail, title, number of views, publication date, and channel.</td>
    </tr>
    <tr>
      <td><code>CardList</code></td>
      <td>Returns all cards in a row.</td>
    </tr>
    <tr>
      <td><code>App</code></td>
      <td>Mounts our <code>dummyData</code> object, loads the skeleton UI for two seconds, and returns the <code>CardList</code> component.</td>
    </tr>
  </tbody>
</table>

Inside your `src` folder, create a folder and name it `components`. Inside the `components` folder, create a `Card.js` file, add the following code to it:

<div class="break-out">

 <pre><code class="language-javascript">import React from "react";
const Card = ({ item, channel }) =&gt; {
    return (
      &lt;li className="card"&gt;
        &lt;a
          href={`https://www.youtube.com/watch?v=${item.id}`}
          target="_blank"
          rel="noopener noreferrer"
          className="card-link"
        &gt;
          &lt;img src={item.image} alt={item.title} className="card-image" /&gt;
          &lt;img src={item.image} alt={item.title} className="channel-image" /&gt;
          &lt;h4 className="card-title"&gt;{item.title}&lt;/h4&gt;
          &lt;p className="card-channel"&gt;
            &lt;i&gt;{channel}&lt;/i&gt;
          &lt;/p&gt;
          &lt;div className="card-metrics"&gt;
            {item.views} &bull; {item.published}
          &lt;/div&gt;
        &lt;/a&gt;
      &lt;/li&gt;
    );
  };
  export default Card;
</code></pre>
</div>

We created a `Card` component. Inside it, we imported `React` from `react`, and we deconstructed the `item` and `channel` props so that they can be used across the `Card` component. Each `Card` item component that displays one video will show the thumbnail, number of views, publication date, and title.

### CardList Component

Inside the `components` folder, create a *CardList.js* file and add the following code to it:

<div class="break-out">

 <pre><code class="language-javascript">import React from "react";
import Card from "./Card";
const CardList = ({ list }) =&gt; {
    return (
      &lt;ul className="list"&gt;
        {list.items.map((item, index) =&gt; {
          return &lt;Card key={index} item={item} channel={list.channel} /&gt;;
        })}
      &lt;/ul&gt;
    );
  };
  export default CardList;
</code></pre>
</div>

In this component, we’ve imported the `Card` component that we created. The card accepts the `item` and `channel` props, which we get by mapping through the `list.items`. We then export this component as `CardList`, because we’ll be making use of it in our `App` component.

**Note**: *The items array that is mapped in this component is the array of objects in our `dummyData`.*

### App Component

Inside the *app.js* file in the `src/` directory, delete the code that is there and add the following to it.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState, useEffect } from "react";
import "./App.css";
import dummyData from "./data";
import CardList from "./components/CardList";

const App = () =&gt; {
  const [videos, setVideos] = useState([]);
  const [loading, setLoading] = useState(false);

  useEffect(() =&gt; {
    setLoading(true);
    const timer = setTimeout(() =&gt; {
      setVideos(dummyData);
      setLoading(false);
    }, 5000);
    return () =&gt; clearTimeout(timer);
  }, []);
  return (
    &lt;div className="App"&gt;
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
  );
};
export default App;
</code></pre>
</div>

In this component, we’ve imported the `useState` and `useEffect` hooks alongside `React` and the other files that we’ve created and that will be needed in the `App` component.

Because our data is dummy data, we need to mock it up like the API data by loading the content after a two-second timeout, using the [JavaScript `setTimeout` method](https://electrictoolbox.com/using-settimeout-javascript/).

Next, in the `App` component, we create a video state, and set the state to an empty array using `useState`.

To load our dummy data, we’ll use the `useEffect` hook. In our hook, we create a variable timer that holds the `setTimeout``()` function. Inside the function, we set our video state to our `dummyData` object, and we ensure that the data loads after two seconds, and, lastly, we cancel the timer while unmounting.

Finally, we map through our video state and return the section element that contains the `list-section` and the `CardList` component with its list props.

{{% ad-panel-leaderboard %}}

## Adding CSS

Until now, we’ve used a lot of classes without actual CSS. Inside the `src` folder, delete everything in `App.css` and replace it with the following code;

<pre><code class="language-css">.App {
  max-width: 960px;
  margin: 0 auto;
  font-size: 16px;
}
.list {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
}
.section-title {
  margin-top: 30px;
}
.card {
  width: calc(33% - 10px);
  margin: 20px 0;
}
.card-link {
  color: inherit;
  text-decoration: none;
}
.card-image {
  width: 100%;
}
.channel-image {
  border-radius: 100%;
  padding: 0, 10px, 0, 0;
  width: 40px;
  height: 40px;  
}
.card-title {
  margin-top: 10px;
  margin-bottom: 0;
}
.card-channel {
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 14px;
}
/* Tablets */
@media (max-width: 1000px) {
  .App {
    max-width: 600px;
  }
  .card {
    width: calc(50% - 22px);
  }
}
/* Mobiles \*/
@media (max-width: 640px) {
  .App {
    max-width: 100%;
    padding: 0 15px;
  }
  .card {
    width: 100%;
  }
}
</code></pre>

Let’s see what our YouTube UI looks like without the skeleton screen. You can see that when the page loads, a white screen appears for two seconds, and then the data loads promptly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f62be7-6150-4166-9067-29a1d1536d77/07-skeleton-screens-react.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f62be7-6150-4166-9067-29a1d1536d77/07-skeleton-screens-react.gif" width="600" height="306" alt="YouTube-like UI without skeleton screen" /></a><figcaption>YouTube-Like UI without skeleton screen (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f62be7-6150-4166-9067-29a1d1536d77/07-skeleton-screens-react.gif">Large preview</a>)</figcaption></figure>

## Using React Loading Skeleton

Unlike other libraries in which you would meticulously craft a skeleton screen to match the font sizes, line heights and margins of your content, the `Skeleton` component is designed to be used directly in your components, in place of the content that is loading.

Let’s go over a few reasons why we’ve chosen React Loading Skeleton over others.

### Theming

React Loading Skeleton supports theming. Thus, you can easily change the colors of all skeleton components by using `SkeletonTheme` and pass values to the color `props`.

Below is an example showing how it works:

<div class="break-out">

 <pre><code class="language-javascript">import Skeleton, { SkeletonTheme } from "react-loading-skeleton";

&lt;SkeletonTheme color="grey" highlightColor="#444"&gt;
  &lt;p&gt;
    &lt;Skeleton height={250} width={300} count={1} /&gt;
  &lt;/p&gt;

&lt;/SkeletonTheme&gt;
&lt;SkeletonTheme color="#990" highlightColor="#550"&gt;
  &lt;p&gt;
    &lt;Skeleton height={250} width={300} count={1} /&gt;
  &lt;/p&gt;

&lt;/SkeletonTheme&gt;
</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abb735b0-25f9-4966-9e6c-4a6a2a33d220/06-skeleton-screens-react.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abb735b0-25f9-4966-9e6c-4a6a2a33d220/06-skeleton-screens-react.gif" width="473" height="256" alt="Theming effect in action" /></a><figcaption>Theming effect in action (<a href="">Large preview</a>)</figcaption></figure>

### Duration

In addition to the `height`, `width`, and `color` props, we can also specify a `duration` prop.

<pre><code class="language-javascript">&lt;Skeleton duration={2} /&gt;
</code></pre>

The duration defaults to `1.2`. This determines how long it takes to do one cycle of the skeleton animation.

To learn more, check out [the documentation](https://github.com/dvtng/react-loading-skeleton).

## Implementing Skeleton Screen UI

Now, we’ll install `react-loading-skeleton`. Run the following command in your terminal to install the package:

<pre><code class="language-bash">npm install react-loading-skeleton
</code></pre>

### Skeleton Component

Let’s create a skeleton component for our video data. Inside our `components` folder, create a  `SkeletonCard.js` file, and add the following code:

<div class="break-out">

 <pre><code class="language-javascript">import React from "react";
import Skeleton from "react-loading-skeleton";
const SkeletonCard = () =&gt; {
    return (
      &lt;section&gt;
        &lt;h2 className="section-title"&gt;
          &lt;Skeleton height={30} width={300} /&gt;
        &lt;/h2&gt;

        &lt;ul className="list"&gt;
          {Array(9)
            .fill()
            .map((item, index) =&gt; (
              &lt;li className="card" key={index}&gt;
                &lt;Skeleton height={180} /&gt;
                &lt;h4 className="card-title"&gt;
                &lt;Skeleton circle={true} height={50} width={50} /&gt; &nbsp;
                  &lt;Skeleton height={36} width={`80%`} /&gt;
                &lt;/h4&gt;
                &lt;p className="card-channel"&gt;
                  &lt;Skeleton width={`60%`} /&gt;
                &lt;/p&gt;
                &lt;div className="card-metrics"&gt;
                  &lt;Skeleton width={`90%`} /&gt;
                &lt;/div&gt;
              &lt;/li&gt;
            ))}
        &lt;/ul&gt;
      &lt;/section&gt;
    );
  };
  export default SkeletonCard;
</code></pre>
</div>

We’ve created an unordered list. Inside it, we’ve used the `Array.fill()` method. Because we have nine items of dummy data, we’ve used the `Array.fill()` method to loop through the length of our `items` object and filled it with no index value, hence making our array **empty**. See the [Array.fill documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill) to learn how it works.

Next, we mapped through our empty array to return a list containing the skeleton properties, and we specified the value of each of the skeleton properties.

Here, `height` connotes the length of a skeleton rectangle, and `width` refers to the breadth, while `circle` creates the rounded part of the skeleton UI.

React Loading Skeleton comes with default Pulse animation, which makes it handy. You could create Pulse animation to suit your project, but if you ask me, I would stick with the default.

Finally, the complete [source code is available](https://github.com/krofax/React-Skeleton-Screen-UI).

We now have a fully functional skeleton screen UI. Our example shows the skeleton for five seconds before showing the content.

Let’s see our result thus far:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326ff1db-d7a5-4495-951d-07181c96f22d/08-skeleton-screens-react.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326ff1db-d7a5-4495-951d-07181c96f22d/08-skeleton-screens-react.gif" width="600" height="305" alt="YouTube-like UI plus skeleton screen UI" /></a><figcaption>Our YouTube-like skeleton UI (<a href="">Large preview</a>)</figcaption></figure>

## Conclusion

Skeleton screens tremendously improve the user experience by avoiding the frustration of facing an entirely blank screen and giving the user an impression of what content will look like before it loads.

If you aren’t comfortable with any of the packages we’ve looked at, you can create your own skeleton UI by making rectangles and circles that mimic the page’s layout.

Please do share your feedback and experience with in the comments section below. I’d love to see what you come up with!

The supporting repo for this article is [available on Github](https://github.com/krofax/React-Skeleton-Screen-UI).

### References

- “[Everything You Need to Know About Skeleton Screens](https://uxdesign.cc/what-you-should-know-about-skeleton-screens-a820c45a571a)”, Bill Chung, UX Collective
- “[Skeleton Loading Pages With React](https://medium.com/octopus-wealth/skeleton-loading-pages-with-react-5a931f12677b)”, Anthony Panagi, Octopus Wealth
- “[Skeleton Screens With React And React Native](https://alligator.io/react/skeleton-screens-react-and-react-native/)”, Chris Dolphin, Alligator.io
- “[Implementing Skeleton Loading In React ](https://dev.to/prototyp/implementing-skeleton-loading-in-react-kia)”, Adrian Bece, DEV

{{< signature "ks, il, al" >}}
