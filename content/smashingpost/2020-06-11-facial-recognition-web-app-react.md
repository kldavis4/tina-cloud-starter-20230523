---
title: 'Building A Facial Recognition Web Application With React'
slug: facial-recognition-web-application-react
author: adeneye-david-abiodun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4966fe4-3ccb-4416-9358-63df87b00a3b/facial-recognition-web-application-react.png
date: 2020-06-11T10:00:00.000Z
summary: >-
  In this article, Adeneye David Abiodun explains how to build a facial recognition web app with React by using the Face Recognition API, as well as the Face Detection model and Predict API. The app built in this article is similar to the face detection box on a pop-up camera in a mobile phone &mdash; it’s able to detect a human face in any image fetched from the Internet. Please note that  you will need to know the [fundamentals of React](https://reactjs.org/).
description: >-
  In this article, we will build a facial recognition web app with the help of React and the Face Recognition API, and cover the Face Detection model and Predict API.
categories:
  - API
  - Apps
  - React
  - Tools
---

If you are going to build a facial recognition web app, this article will introduce you to an easy way of integrating such. In this article, we will take a look at the Face Detection model and Predict API for our face recognition web app with React. 

## What Is Facial Recognition And Why Is It Important?

Facial recognition is a technology that involves classifying and recognizing human faces, mostly by mapping individual facial features and recording the unique ratio mathematically and storing the data as a face print. The face detection in your mobile camera makes use of this technology.

## How Facial Recognition Technology Works

Facial recognition is an enhanced application [bio-metric software](https://en.wikipedia.org/wiki/Biometrics) that uses a deep learning algorithm to compare a live capture or digital image to the stored face print to verify individual identity. However, **deep learning** is a class of machine learning algorithms that uses multiple layers to progressively extract higher-level features from the raw input. For example, in image processing, lower layers may identify edges, while higher layers may identify the concepts relevant to a human such as digits or letters or faces.

Facial detection is the process of identifying a human face within a scanned image; the process of extraction involves obtaining a facial region such as the eye spacing, variation, angle and ratio to determine if the object is human. 

**Note**: *The scope of this tutorial is far beyond this; you can read more on this topic in “[Mobile App With Facial Recognition Feature: How To Make It Real](https://www.smashingmagazine.com/2018/02/mobile-app-facial-recognition-feature/)”. In today’s article, we’ll only be building a web app that detects a human face in an image.*

{{% feature-panel %}} 

## A Brief Introduction To Clarifai

In this tutorial, we will be using [Clarifai](https://www.clarifai.com/), a platform for visual recognition that offers a free tier for developers. They offer a comprehensive set of tools that enable you to manage your input data, annotate inputs for training, create new models, predict and search over your data. However, there are other face recognition API that you can use, check [here](https://analyticsindiamag.com/top-5-face-recognition-and-detection-api-services/) to see a list of them. Their documentation will help you to integrate them into your app, as they all almost use the same model and process for detecting a face.

## Getting Started With Clarifai API

In this article, we are just focusing on one of the Clarifai model called [Face Detection](https://www.clarifai.com/models/face-detection-image-recognition-model-a403429f2ddf4b49b307e318f00e528b-detection). This particular model returns probability scores on the likelihood that the image contains human faces and coordinates locations of where those faces appear with a bounding box. This model is great for anyone building an app that monitors or detects human activity. The [Predict API](https://docs.clarifai.com/api-guide/predict) analyzes your images or videos and tells you what’s inside of them. The API will return a list of concepts with corresponding probabilities of how likely it is that these concepts are contained within the image.

You will get to integrate all these with React as we continue with the tutorial, but now that you have briefly learned more about the Clarifai API, you can deep dive more about it [here](https://docs.clarifai.com/).

What we are building in this article is similar to the face detection box on a pop-up camera in a mobile phone. The image presented below will give more clarification:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cce9387-a4d1-406d-b44c-3e31cf4bc37e/01-sample-app-facial-recognition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cce9387-a4d1-406d-b44c-3e31cf4bc37e/01-sample-app-facial-recognition.png" sizes="100vw" caption="Sample-App (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cce9387-a4d1-406d-b44c-3e31cf4bc37e/01-sample-app-facial-recognition.png'>Large preview</a>)" alt="Sample-App" >}}

You can see a rectangular box detecting a human face. This is the kind of simple app we will be building with React.

## Setting Development Environment

The first step is to create a new directory for your project and start a new react project, you can give it any name of your choice. I will be using the [npm](https://www.npmjs.com/) package manager for this project, but you can use yarn depending on your choice.

**Note**: *Node.js is required for this tutorial. If you don’t have it, go to the [Node.js official website](https://nodejs.org/en/) to download and install before continuing.*

Open your terminal and create a new React project.

We are using [`create-react-app`](https://reactjs.org/docs/create-a-new-react-app.html) which is a comfortable environment for **learning React** and is the best way to start building a new [single-page](https://reactjs.org/docs/glossary.html#single-page-application)application to React. It is a global package that we would install from npm. it creates a starter project that contains webpack, babel and a lot of nice features.

<pre><code class="language-javascript">/* install react app globally */
npm install -g create-react-app

/* create the app in your new directory */
create-react-app face-detect

/* move into your new react directory */
cd face-detect

/* start development sever */
npm start</code></pre>

Let me first explain the code above. We are using `npm install -g create-react-app` to install the [`create-react-app`](https://reactjs.org/docs/create-a-new-react-app.html) package globally so you can use it in any of your projects. `create-react-app face-detect` will create the project environment for you since it’s available globally. After that, `cd face-detect` will move you into our project directory. `npm start` will start our development server. Now we are ready to start building our app.

You can open the project folder with any editor of your choice. I use visual studio code. It’s a free IDE with tons of plugins to make your life easier, and it is available for all major platforms. You can download it from the official [website.](https://code.visualstudio.com/) 

At this point, you should have the following folder structure.

<pre><code class="language-javascript">FACE-DETECT TEMPLATE
├── node_modules
├── public 
├── src
├── .gitignore
├── package-lock.json
├── package.json
├── README.md</code></pre>

**Note:** React provide us with a single page React app template, let us get rid of what we won’t be needing. First, delete the **logo.svg** file in **src** folder and replace the code you have in **src/app.js** to look like this.

<pre><code class="language-javascript">import React, { Component } from "react";
import "./App.css";
class App extends Component {
  render() {
    return (
      <div className="App">
      </div>
    );
  }
}
export default App;</code></pre>

<figcaption>src/<em>App.js</em></figcaption>

What we did was to clear the component by removing the logo and other unnecessary code that we will not be making use of. Now replace your **src/App.css**  with the minimal CSS below:

<pre><code class="language-css">.App {
  text-align: center;
}
.center {
  display: flex;
  justify-content: center;
}</code></pre>            

We’ll be using [Tachyons](https://tachyons.io/) for this project, It is a tool that allows you to create fast-loading, highly readable, and 100% responsive interfaces with as little CSS as possible.

You can install tachyons to this project through npm:

<pre><code class="language-javascript"># install tachyons into your project
npm install tachyons</code></pre>         

After the installation has completely let us add the Tachyons into our project below at **src/index.js** file.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import * as serviceWorker from "./serviceWorker";
// add tachyons below into your project, note that its only the line of code you adding here
import "tachyons";

ReactDOM.render(&lt;App /&gt;, document.getElementById("root"));
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.register();</code></pre>
</div>

The code above isn’t different from what you had before, all we did was to add the import statement for **tachyons**.

So let us give our interface some styling at **src/index.css** file.

<div class="break-out">

<pre><code class="language-css">
body {
  margin: 0;
  font-family: "Courier New", Courier, monospace;
  -webkit-font-smoothing: antialiased;
  -Moz-osx-font-smoothing: grayscale;
  background: #485563; /* fallback for old browsers */
  background: linear-gradient(
    to right,
    #29323c,
    #485563
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
button {
  cursor: pointer;
}
code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
    monospace;
}</code></pre>
</div>

<figcaption><em>src/index.css</em></figcaption>
                                   
In the code block above, I added a background color and a cursor pointer to our page, at this point we have our interface setup, let get to start creating our components in the next session.

{{% ad-panel-leaderboard %}}

## Building Our React Components

In this project, we’ll have two components, we have a URL input box to fetch images for us from the internet &mdash; `ImageSearchForm`, we’ll also have an image component to display our image with a face detection box &mdash; `FaceDetect`. Let us start building our components below:

Create a new folder called **Components** inside the **src** directory. Create another two folders called **ImageSearchForm** and **FaceDetect**  inside the **src/Components**  after that open **ImageSearchForm** folder and create two files as follow **ImageSearchForm.js** and **ImageSearchForm.css**.

Then open **FaceDetect** directory and create two files as follow **FaceDetect.js** and **FaceDetect.css**.

When you are done with all these steps your folder structure should look like this below in **src/Components** directory:

<pre><code class="language-javascript">src/Components TEMPLATE

├── src
  ├── Components 
    ├── FaceDetect
      ├── FaceDetect.css 
      ├── FaceDetect.js 
    ├── ImageSearchForm
      ├── ImageSearchForm.css 
      ├── ImageSearchForm.js</code></pre>

At this point, we have our Components folder structure, now let us import them into our `App` component. Open your **src/App.js** folder and make it look like what I have below.

<div class="break-out">

<pre><code class="language-javascript">import React, { Component } from "react";
import "./App.css";
import ImageSearchForm from "./components/ImageSearchForm/ImageSearchForm";
// import FaceDetect from "./components/FaceDetect/FaceDetect";

class App extends Component {
  render() {
    return (
      &lt;div className="App"&gt;
        &lt;ImageSearchForm /&gt;
        {/&#42; &lt;FaceDetect /&gt; &#42;/}
      &lt;/div&gt;
    );
  }
}
export default App;
</code></pre>
</div>

<figcaption>src/<em>App.js</em></figcaption>
                                                                
In the code above, we mounted our components at lines 10 and 11, but if you notice  `FaceDetect` is commented out because we are not working on it yet till our next section and to avoid error in the code we need to add a comment to it. We have also imported our components into our app.

To start working on our **ImageSearchForm** file, open the `ImageSearchForm.js` file and let us create our component below.
This example below is our ImageSearchForm component which will contain an input form and the button.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import "./ImageSearchForm.css";

// imagesearch form component

const ImageSearchForm = () =&gt; {
  return (
    &lt;div className="ma5 to"&gt;
      &lt;div className="center"&gt;
        &lt;div className="form center pa4 br3 shadow-5"&gt;
          &lt;input className="f4 pa2 w-70 center" type="text" /&gt;
          &lt;button className="w-30 grow f4 link ph3 pv2 dib white bg-blue"&gt;
            Detect
          &lt;/button&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default ImageSearchForm;</code></pre>
</div>

<figcaption><em>ImageSearchForm.js</em></figcaption>

In the above line component, we have our input form to fetch the image from the web and a **Detect** button to perform face detection action. I’m using *Tachyons* CSS here that works like bootstrap; all you just have to call is `className`. You can find more details on their [website](https://tachyons.io/).

To style our component, open the **ImageSearchForm.css** file. Now let’s style the components below:

<div class="break-out">

<pre><code class="language-css">.form {
  width: 700px;
  background: radial-gradient(
      circle,
      transparent 20%,
      slategray 20%,
      slategray 80%,
      transparent 80%,
      transparent
    ),
    radial-gradient(
        circle,
        transparent 20%,
        slategray 20%,
        slategray 80%,
        transparent 80%,
        transparent
      )
      50px 50px,
    linear-gradient(#a8b1bb 8px, transparent 8px) 0 -4px,
    linear-gradient(90deg, #a8b1bb 8px, transparent 8px) -4px 0;
  background-color: slategray;
  background-size: 100px 100px, 100px 100px, 50px 50px, 50px 50px;
}</code></pre>
</div>

The CSS style property is a CSS pattern for our form background just to give it a beautiful design. You can generate the CSS pattern of your choice [here](https://lea.verou.me/css3patterns) and use it to replace it with.

Open your terminal again to run your application.

<pre><code class="language-javascript">/* To start development server again */
npm start</code></pre>

We have our `ImageSearchForm` component display in the image below.
      
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b85d077-f7e1-4080-99c9-5824feb28c2c/02-image-search-page-facial-recognition.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b85d077-f7e1-4080-99c9-5824feb28c2c/02-image-search-page-facial-recognition.JPG" sizes="100vw" caption="Image-Search-Page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b85d077-f7e1-4080-99c9-5824feb28c2c/02-image-search-page-facial-recognition.JPG'>Large preview</a>)" alt="Image-Search-Page" >}}

Now we have our application running with our first components.

{{% ad-panel-leaderboard %}}

## Image Recognition API

It’s time to create some functionalities where we enter an image URL, press Detect and an image appear with a **face detection box** if a face exists in the image. Before that let setup our Clarifai account to be able to integrate the API into our app.

### How to Setup Clarifai Account

This API makes it possible to utilize its machine learning app or services. For this tutorial, we will be making use of the tier that’s available for **free** to developers with 5,000 operations per month. You can read more [here](https://www.clarifai.com/pricing) and **sign up**, after **sign in** it will take you to your account **dashboard** click on my first application or create an application to get your API-key that we will be using in this app as we progress.

**Note:** You cannot use mine, you have to get yours.
  
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1e3f14-8bba-4bc4-b39a-57e730639380/03-clarifai-dashboard-facial-recognition.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1e3f14-8bba-4bc4-b39a-57e730639380/03-clarifai-dashboard-facial-recognition.JPG" sizes="100vw" caption="Clarifai-Dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1e3f14-8bba-4bc4-b39a-57e730639380/03-clarifai-dashboard-facial-recognition.JPG'>Large preview</a>)" alt="Clarifai-Dashboard" >}}

This is how your dashboard above should look. Your API key there provides you with access to Clarifai services. The arrow below the image points to a copy icon to copy your API key.

If you go to [Clarifai model](https://www.clarifai.com/models) you will see that they use machine learning to train what is called models, they train a computer by giving it many pictures, you can also create your own model and teach it with your own images and concepts. But here we would be making use of their [Face Detection model](https://www.clarifai.com/models/face-detection-image-recognition-model-a403429f2ddf4b49b307e318f00e528b-detection).

The Face detection model has a predict API we can make a call to (read more in the documentation [here](https://www.clarifai.com/models/face-detection-image-recognition-model-a403429f2ddf4b49b307e318f00e528b-detection)).

So let’s install the `clarifai` package below.

Open your terminal and run this code:

<pre><code class="language-javascript">/* Install the client from npm */
npm install clarifai</code></pre>
  
When you are done installing `clarifai`, we need to import the package into our app with the above installation we learned earlier. 

However, we need to create functionality in our input search-box to detect what the user enters. We need a state value so that our app knows what the user entered, remembers it, and updates it anytime it gets changes.

You need to have your API key from **Clarifai** and must have also installed `clarifai` through npm.

The example below shows how we import `clarifai` into the app and also implement our API key.

Note that (as a user) you have to fetch any clear image URL from the web and paste it in the input field; that URL will the state value of `imageUrl` below.

<div class="break-out">

<pre><code class="language-javascript">import React, { Component } from "react";
// Import Clarifai into our App
import Clarifai from "clarifai";
import ImageSearchForm from "./components/ImageSearchForm/ImageSearchForm";
// Uncomment FaceDetect Component
import FaceDetect from "./components/FaceDetect/FaceDetect";
import "./App.css";

// You need to add your own API key here from Clarifai.
const app = new Clarifai.App({
  apiKey: "ADD YOUR API KEY HERE",
});

class App extends Component {
  // Create the State for input and the fectch image
  constructor() {
    super();
    this.state = {
      input: "",
      imageUrl: "",
    };
  }

// setState for our input with onInputChange function
  onInputChange = (event) =&gt; {
    this.setState({ input: event.target.value });
  };

// Perform a function when submitting with onSubmit
  onSubmit = () =&gt; {
        // set imageUrl state
    this.setState({ imageUrl: this.state.input });
    app.models.predict(Clarifai.FACE_DETECT_MODEL, this.state.input).then(
      function (response) {
        // response data fetch from FACE_DETECT_MODEL 
        console.log(response);
        /&#42; data needed from the response data from clarifai API, 
           note we are just comparing the two for better understanding 
           would to delete the above console&#42;/ 
        console.log(
          response.outputs[0].data.regions[0].region_info.bounding_box
        );
      },
      function (err) {
        // there was an error
      }
    );
  };
  render() {
    return (
      &lt;div className="App"&gt;
        // update your component with their state
        &lt;ImageSearchForm
          onInputChange={this.onInputChange}
          onSubmit={this.onSubmit}
        /&gt;
        // uncomment your face detect app and update with imageUrl state
        &lt;FaceDetect imageUrl={this.state.imageUrl} /&gt;
      &lt;/div&gt;
    );
  }
}
export default App;</code></pre>
</div>

In the above code block, we imported `clarifai` so that we can have access to [Clarifai](https://www.clarifai.com/) services and also add our API key. We use `state` to manage the value of `input` and the `imageUrl`. We have an `onSubmit` function that gets called when the **Detect** button is clicked, and we set the state of `imageUrl` and also fetch image with Clarifai **FACE DETECT MODEL** which returns a response data or an error.

For now, we’re logging the data we get from the API to the console; we’ll use that in the future when determining the face detect model.

For now, there will be an error in your terminal because we need to update the `ImageSearchForm` and `FaceDetect` Components files.

Update the **ImageSearchForm.js** file with the code below:

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import "./ImageSearchForm.css";
// update the component with their parameter
const ImageSearchForm = ({ onInputChange, onSubmit }) =&gt; {
  return (
    &lt;div className="ma5 mto"&gt;
      &lt;div className="center"&gt;
        &lt;div className="form center pa4 br3 shadow-5"&gt;
          &lt;input
            className="f4 pa2 w-70 center"
            type="text"
            onChange={onInputChange}    // add an onChange to monitor input state
          /&gt;
          &lt;button
            className="w-30 grow f4 link ph3 pv2 dib white bg-blue"
            onClick={onSubmit}  // add onClick function to perform task
          &gt;
            Detect
          &lt;/button&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default ImageSearchForm;</code></pre>
</div>

In the above code block, we passed `onInputChange` from props as a function to be called when an `onChange` event happens on the input field, we’re doing the same with `onSubmit` function we tie to the `onClick` event.

Now let us create our `FaceDetect` component that we uncommented in **src/App.js** above. Open **FaceDetect.js** file and input the code below:

In the example below, we created the `FaceDetect` component to pass the props `imageUrl`.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
// Pass imageUrl to FaceDetect component
const FaceDetect = ({ imageUrl }) =&gt; {
  return (
  # This div is the container that is holding our fetch image and the face detect box
    &lt;div className="center ma"&gt;
      &lt;div className="absolute mt2"&gt;
                        # we set our image SRC to the url of the fetch image 
        &lt;img alt="" src={imageUrl} width="500px" heigh="auto" /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default FaceDetect;</code></pre>
</div>
    
This component will display the image we have been able to determine as a result of the response we’ll get from the API. This is why we are passing the `imageUrl` down to the component as props, which we then set as the `src` of the `img` tag.

Now we both have our `ImageSearchForm` component and `FaceDetect` components are working. The Clarifai **FACE_DETECT_MODEL** has detected the position of the face in the image with their **model** and provided us with data but not a box that you can check in the console.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6575d0-b406-4bd8-bd30-4d2e9f358b08/04-image-link-form-facial-recognition.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6575d0-b406-4bd8-bd30-4d2e9f358b08/04-image-link-form-facial-recognition.JPG" sizes="100vw" caption="Image-Link-Form (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6575d0-b406-4bd8-bd30-4d2e9f358b08/04-image-link-form-facial-recognition.JPG'>Large preview</a>)" alt="Image-Link-Form" >}}

Now our `FaceDetect` component is working and Clarifai Model is working while fetching an image from the URL we input in the `ImageSearchForm` component. However, to see the data response Clarifai provided for us to annotate our result and the section of data we would be needing from the response if you remember we made two `console.log` in **App.js** file.

So let’s open the console to see the response like mine below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92d944e8-1867-4f0e-bdbf-d2c556c0f218/05-image-link-form-console-facial-recognition.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92d944e8-1867-4f0e-bdbf-d2c556c0f218/05-image-link-form-console-facial-recognition.JPG" sizes="100vw" caption="Image-Link-Form (Console) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92d944e8-1867-4f0e-bdbf-d2c556c0f218/05-image-link-form-console-facial-recognition.JPG'>Large preview</a>)" alt="Image-Link-Form (Console)" >}}

The first `console.log` statement which you can see above is the response data from Clarifai **FACE_DETECT_MODEL** made available for us if successful, while the second `console.log` is the data we are making use of in order to detect the face using the `data.region.region_info.bounding_box`. At the second console.log, `bounding_box` data are:

<pre><code class="language-css">bottom_row: 0.52811456
left_col: 0.29458505
right_col: 0.6106333
top_row: 0.10079138</code></pre>
      
This might look twisted to us but let me break it down briefly. At this point the Clarifai **FACE_DETECT_MODEL** has detected the position of face in the image with their **model** and provided us with a data but not a box, it ours to do a little bit of math and calculation to display the box or anything we want to do with the data in our application. So let me explain the data above,

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>bottom_row: 0.<span class="rh">52</span>811456</code></td>
      <td>This indicates our face detection box start at <strong>52%</strong> of the image height from the bottom.</td>
    </tr>
    <tr>
      <td><code>left_col: 0.<span class="rh">29</span>458505</code></td>
      <td>This indicates our face detection box start at <strong>29%</strong> of the image width from the left.</td>
    </tr>
    <tr>
      <td><code>right_col: 0.<span class="rh">61</span>06333</code></td>
      <td>This indicates our face detection box start at <strong>61%</strong> of the image width from the right.</td>
    </tr>
    <tr>
      <td><code>top_row: 0.<span class="rh">10</span>079138</code></td>
      <td>This indicates our face detection box start at <strong>10%</strong> of the image height from the top.</td>
    </tr>
  </tbody>
</table>

If you take a look at our app inter-phase above, you will see that the model is accurate to detect the **bounding_box** from the face in the image. However, it left us to write a function to create the box including styling that will display a box from earlier information on what we are building based on their response data provided for us from the API. So let’s implement that in the next section.

## Creating A Face Detection Box

This is the final section of our web app where we get our facial recognition to work fully by calculating the face location of any image fetch from the web with Clarifai **FACE_DETECT_MODEL** and then display a facial box. Let open our **src/App.js**  file and include the code below:

In the example below, we created a `calculateFaceLocation` function with a little bit of math with the response data from Clarifai and then calculate the coordinate of the face to the image width and height so that we can give it a style to display a face box.

<div class="break-out">

<pre><code class="language-javascript">import React, { Component } from "react";
import Clarifai from "clarifai";
import ImageSearchForm from "./components/ImageSearchForm/ImageSearchForm";
import FaceDetect from "./components/FaceDetect/FaceDetect";
import "./App.css";

// You need to add your own API key here from Clarifai.
const app = new Clarifai.App({
  apiKey: "ADD YOUR API KEY HERE",
});

class App extends Component {
  constructor() {
    super();
    this.state = {
      input: "",
      imageUrl: "",
      box: {},  # a new object state that hold the bounding_box value
    };
  }

  // this function calculate the facedetect location in the image
  calculateFaceLocation = (data) =&gt; {
    const clarifaiFace =
      data.outputs[0].data.regions[0].region_info.bounding_box;
    const image = document.getElementById("inputimage");
    const width = Number(image.width);
    const height = Number(image.height);
    return {
      leftCol: clarifaiFace.left_col * width,
      topRow: clarifaiFace.top_row * height,
      rightCol: width - clarifaiFace.right_col * width,
      bottomRow: height - clarifaiFace.bottom_row * height,
    };
  };

  /* this function display the face-detect box base on the state values */
  displayFaceBox = (box) =&gt; {
    this.setState({ box: box });
  };

  onInputChange = (event) =&gt; {
    this.setState({ input: event.target.value });
  };

  onSubmit = () =&gt; {
    this.setState({ imageUrl: this.state.input });
    app.models
      .predict(Clarifai.FACE_DETECT_MODEL, this.state.input)
      .then((response) =&gt;
        # calculateFaceLocation function pass to displaybox as is parameter
        this.displayFaceBox(this.calculateFaceLocation(response))
      )
      // if error exist console.log error
      .catch((err) =&gt; console.log(err));
  };

  render() {
    return (
      &lt;div className="App"&gt;
        &lt;ImageSearchForm
          onInputChange={this.onInputChange}
          onSubmit={this.onSubmit}
        /&gt;
        // box state pass to facedetect component
        &lt;FaceDetect box={this.state.box} imageUrl={this.state.imageUrl} /&gt;
      &lt;/div&gt;
    );
  }
}
export default App;
</code></pre>
</div>

The first thing we did here was to create another state value called `box` which is an empty object that contains the response values that we received.  The next thing we did was to create a function called `calculateFaceLocation` which will receive the response we get from the API when we call it in the `onSubmit` method. Inside the `calculateFaceLocation`  method, we assign `image` to the element object we get from calling `document.getElementById("inputimage")` which we use to perform some calculation.

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>leftCol</code></td>
      <td><code>clarifaiFace.left_col</code> is the % of the width multiply with the width of the image then we would get the actual width of the image and where the <code>left_col</code> should be.</td>
    </tr>
    <tr>
      <td><code>topRow</code></td>
      <td><code>clarifaiFace.top_row</code> is the % of the height multiply with the height of the image then we would get the actual height of the image and where the <code>top_row</code> should be.</td>
    </tr>
    <tr>
      <td><code>rightCol</code></td>
      <td>This subtracts the width from (<code>clarifaiFace.right_col</code> width) to know where the <code>right_Col</code> should be.</td>
    </tr>
    <tr>
      <td><code>bottomRow</code></td>
      <td>This subtract the height from (<code>clarifaiFace.right_col</code> height) to know where the <code>bottom_Row</code> should be.</td>
    </tr>
  </tbody>
</table>

In the `displayFaceBox` method, we update the state of `box` value to the data we get from calling `calculateFaceLocation`.

We need to update our `FaceDetect` component, to do that open **FaceDetect.js** file and add the following update to it.

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
// add css to style the facebox
import "./FaceDetect.css";
// pass the box state to the component

const FaceDetect = ({ imageUrl, box }) =&gt; {
  return (
    &lt;div className="center ma"&gt;
      &lt;div className="absolute mt2"&gt;
            /&#42; insert an id to be able to manipulate the image in the DOM &#42;/
        &lt;img id="inputimage" alt="" src={imageUrl} width="500px" heigh="auto" /&gt;
       //this is the div displaying the faceDetect box base on the bounding box value 
      &lt;div
          className="bounding-box"
          // styling that makes the box visible base on the return value
          style={{
            top: box.topRow,
            right: box.rightCol,
            bottom: box.bottomRow,
            left: box.leftCol,
          }}
        &gt;&lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default FaceDetect;</code></pre>
</div>

In order to show the box around the face, we pass down `box` object from the parent component into the `FaceDetect` component which we can then use to style the `img` tag.

We imported a CSS we have not yet created, open **FaceDetect.css** and add the following style:

<pre><code class="language-css">.bounding-box {
  position: absolute;
  box-shadow: 0 0 0 3px #fff inset;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  cursor: pointer;
}</code></pre>

Note the style and our final output below, you could see we set our box-shadow color to be white and display flex.

At this point, your final output should look like this below. In the output below, we now have our face detection working with a face box to display and a border style color of white.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3467fc-910b-4705-a3f2-143609ab0bda/06-final-app-facial-recognition.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3467fc-910b-4705-a3f2-143609ab0bda/06-final-app-facial-recognition.JPG" sizes="100vw" caption="Final App (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3467fc-910b-4705-a3f2-143609ab0bda/06-final-app-facial-recognition.JPG'>Large preview</a>)" alt="Final-App1" >}}

Let try another image below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32ebb6ba-616c-48dc-bae2-adc03391f4cb/07-final-app-facial-recognition.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32ebb6ba-616c-48dc-bae2-adc03391f4cb/07-final-app-facial-recognition.JPG" sizes="100vw" caption="Final App (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32ebb6ba-616c-48dc-bae2-adc03391f4cb/07-final-app-facial-recognition.JPG'>Large preview</a>)" alt="Final-App2" >}}

## Conclusion

I hope you enjoyed working through this tutorial. We’ve learned how to build a face recognition app that can be integrated into our future project with more functionality, you also learn how to use an amazing machine learning API with react. You can always read more on **Clarifai** API from the references below. If you have any questions, you can leave them in the comments section and I’ll be happy to answer every single one and work you through any issues.

The supporting repo for this article is [available on Github.](https://github.com/daacode/face-detect)

### Resources And Further Reading

- [React Doc](https://reactjs.org/docs/getting-started.html)
- [Getting Started with Clarifai](https://www.clarifai.com/)
- [Clarifai Developer Documentation](https://docs.clarifai.com/)
- [Clarifai Face Detection Model](https://www.clarifai.com/models/face-detection-image-recognition-model-a403429f2ddf4b49b307e318f00e528b-detection)
- “[The Complete Web Developer in 2020: Zero to Mastery](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/),” Andrei Neagoie, Udemy

{{< signature "ks, ra, yk, il" >}}
