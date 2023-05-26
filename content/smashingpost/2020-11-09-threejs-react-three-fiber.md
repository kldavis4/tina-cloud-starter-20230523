---
title: 'A Dive Into React And Three.js Using <code>react-three-fiber</code>'
slug: threejs-react-three-fiber
author: fortune-ikechi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2a8bc95-738b-4138-86da-248072d54684/threejs-react-three-fiber.png
date: 2020-11-09T12:00:00.000Z
summary: >-
  `react-three-fiber` is a powerful Three.js renderer that helps render 3D models and animations for React and its native applications. In this tutorial, you will learn how to configure and build 3D models in a React application. 
description: >-
  `react-three-fiber` is a powerful Three.js renderer that helps render 3D models and animations for React and its native applications. In this tutorial, you will learn how to configure and build 3D models in a React application. 
categories:
  - Apps
  - React
  - JavaScript
---

Today, we’re going to learn how to configure and use `react-three-fiber` for building and displaying 3D models and animations in React and React Native applications.

This tutorial is for developers who want to learn more about 3D model animations in the web using React and for anyone who’s had limitations with Three.js like inability to create canvas, bind user events like `click`  events and start a render loop, `react-three-fiber` comes with these methods. We’ll be building a 3D model to better understand how to build Three.js 3D models using `react-three-fiber`. 

## Getting Started With `react-three-fiber`

Three.js is a library that makes it easier to create 3D graphics in the browser, it uses a [canvas](https://glossarytech.com/terms/go_to_term/606) + WebGL to display the 3D models and animations, you can learn more [here](https://threejs.org/).

[react-three-fiber](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API) is a React [renderer](https://reactjs.org/docs/codebase-overview.html#renderers) for Three.js on the web and react-native, it is a boost to the speed at which you create 3D models and animations with Three.js, some examples of sites with 3D models and animations can be found [here.](https://www.awwwards.com/websites/three-js/) `react-three-fiber` reduces the time spent on animations because of its reusable components, binding events and render loop, first let’s take a look at what is Three.js.

`react-three-fiber` allows us to build components of `threeJS` code using React state, hooks and props, it also comes with the following elements:

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
	<tr>
	<th>Element</th>
	<th>Description</th>
	</tr>
	</thead>
  <tbody>
    <tr>
      <td><code>mesh</code></td>
      <td>A property that helps define the shape of our models </td>
    </tr>
    <tr>
      <td><code>hooks</code></td>
      <td><code>react-three-fiber</code> defines hooks that help us write functions that help define user events such as <code>onClick</code> and <code>onPointOver</code></td>
    </tr>
    <tr>
      <td>Component-based and render loop</td>
      <td><code>react-three-fiber</code> is component-based and renders according to a change in state or the store</td>
    </tr>
  </tbody>
</table>


{{% feature-panel %}}

## How To Use `react-three-fiber`

To use `react-three-fiber`, you start by using the commands below: 

### NPM

<pre><code class="language-bash">npm i three react-three-fiber
</code></pre>

### YARN

<pre><code class="language-bash">yarn add three react-three-fiber 
</code></pre>

**Note**: *For `react-three-fiber` to work, you’ll need to install `three` (Three.js) as we did above.*

## Building A React 3D Ludo Dice Model And Animation Project

Here we are going to build a 3D ludo dice model using `react-three-fiber` like we have in the video below.

{{< vimeo id="475406801" breakout="true" >}}

We will be using `create-react-app` to initialize our project, to do that let’s execute the command below on our terminal.

<pre><code class="language-bash">create-react-app react-three-fiber-ludo-model
</code></pre>

The command above initializes a React project within our local machine, next let’s `cd` into the directory and install our packages `react-three-fiber` and `three`. 

<pre><code class="language-bash">cd react-three-fiber-ludo-model

npm i three react-three-fiber
</code></pre>

Once, the packages are installed, let’s start our development server using the command 

<pre><code class="language-bash">npm start
</code></pre>

The above command should start our project development server in our browser. Next let’s open our project in our text editor of choice, inside our project `src` folder, delete the following files: `App.css`, `App.test.js`, `serviceWorker.js` and `setupTests.js`. Next, let’s delete all code that references the deleted files on our `App.js`. 

For this project, we will need a `Box` component for our ludo dices and our `App` component that’s given by React. 

{{% ad-panel-leaderboard %}}

## Building The `Box` Component

The `Box` component will contain the shape for our ludo dices, an image of a ludo dice and a state to always keep it in rotation. First, let’s import all the packages we need for our `Box` component below. 

<pre><code class="language-javascript">import React, { useRef, useState, useMemo } from "react";
import { Canvas, useFrame } from "react-three-fiber";
import * as THREE from "three";
import five from "./assets/five.png";
</code></pre>

In the above code, we are importing `useRef`, `useState` and `useMemo`. We’ll be using the `useRef` hook to access the mesh of the dice and the `useState` hook to check for the active state of the ludo dice. `useMemo` hook will be used to return the number on the dice. Next, we are importing `Canvas` and `useFrame` from `react-three-fiber`, the `canvas` is used to draw the graphics on the browser, while the `useFrame` allows components to hook into the render-loop, this makes it possible for one component to render over the content of another. Next, we imported the `three`  package and then we imported a static image of a ludo dice. 

Next for us is to write logic for our `Box` component. First, we’ll start with building a functional component and add state to our component, let’s do that below.

<div class="break-out">

 <pre><code class="language-javascript">const Box = (props) =&gt; {
  const mesh = useRef();

  const [active, setActive] = useState(false);

  useFrame(() =&gt; {
    mesh.current.rotation.x = mesh.current.rotation.y += 0.01;
  });

  const texture = useMemo(() =&gt; new THREE.TextureLoader().load(five), []);
  
  return (
    &lt;Box /&gt;
  );
}
</code></pre>
</div>

In the code above, we are creating a `Box` component with props, next we create a ref called `mesh` using the `useRef` hook, we did this so that we can always return the same mesh each time. 

A mesh is a visual element in a scene, its a 3D object that make up a triangular polygon, it’s usually built using a **Geometry,** which is used to define the shape of the model and **Material** which defines the appearance of the model, you can learn about a Mesh [here](https://threejs.org/docs/#api/en/objects/Mesh), You can also learn more about the `useRef` hook [here](https://reactjs.org/docs/hooks-reference.html#useref). 

After initializing a `mesh`, we need to initialize a state for our application using the `useState` hook, here we set up the hovered and active state of the application to false. 

Next, we use the `useFrame` hook from `react-three-fiber` to rotate the mesh (ludo dice), using the code below 

<pre><code class="language-javascript">mesh.current.rotation.x = mesh.current.rotation.y += 0.01;
</code></pre>

Here, we are rotating the current position of the mesh every 0.01 seconds, this is done to give the rotation a good animation. 

<div class="break-out">

 <pre><code class="language-javascript">const texture = useMemo(() => new THREE.TextureLoader().load(five), []);
</code></pre>
</div>

In the code above, we are creating a constant called `texture` and passing in a react `useMemo` hook as a function to load a new dice roll, here the `useMemo` to memorize the dice image and its number. You can learn about the `useMemo` hook [here.](https://reactjs.org/docs/hooks-reference.html?#usememo) 

Next, we want to render the `Box` component on the browser and add our events, we do that below 

<div class="break-out">

 <pre><code class="language-javascript">const Box = (props) =&gt; {
return (
    &lt;mesh
    {...props}
    ref={mesh}
    scale={active ? [2, 2, 2] : [1.5, 1.5, 1.5]}
    onClick={(e) =&gt; setActive(!active)}
      &gt;
      &lt;boxBufferGeometry args={[1, 1, 1]} /&gt;
      &lt;meshBasicMaterial attach="material" transparent side={THREE.DoubleSide}&gt;
        &lt;primitive attach="map" object={texture} /&gt;
      &lt;/meshBasicMaterial&gt;
    &lt;/mesh&gt;
  );
}
</code></pre>
</div>

In the code above, we are returning our `Box` component and wrapping it in the `mesh` we passed all the properties of the `Box` component using the spread operator, and then we referenced the mesh using the `useRef` hook. Next, we use the `scale` property from Three.js to set the size of the dice box when it's active to 2 and 1.5 when it’s not. Last but not least, we added an `onClick` event to set `state` to `active` if it's not set on default. 

<pre><code class="language-javascript">&lt;boxBufferGeometry args={[1, 1, 1]} /&gt;
</code></pre>

In order to render the dice box, we rendered the `boxBufferGeometry` component from Three.js, `boxBufferGeometry`  helps us draw lines and point such as boxes, we used the `args` argument to pass constructors such as the size of box geometry. 

<div class="break-out">

 <pre><code class="language-javascript">&lt;meshBasicMaterial attach="material" transparent side={THREE.DoubleSide}&gt;
</code></pre>
</div>

The `meshBasicMaterial` from Three.js, is used to draw geometries in a simple form. Here we passed the `attach` attribute and passing a `THREE.DoubleSide`props to the `side` attribute. The `THREE.DoubleSide` defines the sides or spaces that should be rendered by `react-three-fiber`. 

<pre><code class="language-javascript">&lt;primitive attach="map" object={texture} /&gt;
</code></pre>

The [`primitive`](https://threejsfundamentals.org/threejs/lessons/threejs-primitives.html) component from Three.js is used to draw 3D graphs. We attached the map property in order to maintain the original shape of the ludo dice. Next, we are going to render our `Box` component in the `App.js` file and complete our 3d ludo dice box. Your component should look similar to the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e8eba2a-d9a6-49af-b06d-b0950da9430d/ludo-3d-box-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e8eba2a-d9a6-49af-b06d-b0950da9430d/ludo-3d-box-example.png" sizes="100vw" caption="" alt="Box component for ludo 3D box" >}}

## Rendering 3D Ludo Dice Box

In this section, we are going to render our `Box` component in our `App.js` and complete our 3d ludo box, to do that first, let’s create an `App` component and wrap it with a `Canvas` tag, this is to render our 3D models, let’s do that below.

<pre><code class="language-javascript">const App = () =&gt; {
  return (
    &lt;Canvas&gt;
    &lt;/Canvas&gt;
  );
}
export default App;
</code></pre>

Next, let’s add a light to the boxes, `react-three-fiber` provides us with three components to light our models, they are as follows 

- `ambientLight`  
This is used to light all objects in a scene or model equally, it accepts props such as the intensity of the light, this will light the body of the ludo dice.
- `spotLight`  
This light is emitted from a single direction, and it increases as the size of the object increases, this will light the points of the ludo dice.
- `pointLight`  
This works similar to the light of a light bulb, light is emitted from a single point to all directions, this will be necessary for the active state of our application. 

Let’s implement the above on our application below.

<div class="break-out">

 <pre><code class="language-javascript">const App = () =&gt; {
  return (
    &lt;Canvas&gt;
      &lt;ambientLight intensity={0.5} /&gt;
      &lt;spotLight position={[10, 10, 10]} angle={0.15} penumbra={1} /&gt;
      &lt;pointLight position={[-10, -10, -10]} /&gt;
    &lt;/Canvas&gt;
  );
}
export default App;
</code></pre>
</div>

In the above code, we imported the `ambientLight` component from `react-three-fiber` and added an intensity of 0.5 to it, next we added a position and angle to our `spotLight` and `pointLight` component. The final step to our application is to render our box component and add a position to the ludo dice boxes, we’d do that in the code below 

<pre><code class="language-javascript">&lt;Box position={[-1.2, 0, 0]} /&gt;
&lt;Box position={[2.5, 0, 0]} /&gt;
</code></pre>

When done, your ludo 3D dice should look similar to the image below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf7865bd-97d9-4ce8-b0b0-7d7a738afe69/ludo-3d-dice-preview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf7865bd-97d9-4ce8-b0b0-7d7a738afe69/ludo-3d-dice-preview.png" sizes="100vw" caption="" alt="3D ludo dice box" >}}

A working demo is available on CodeSandbox.

<iframe loading="lazy" src="https://codesandbox.io/embed/friendly-cookies-v9mmc?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="friendly-cookies-v9mmc"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## Conclusion

`react-three-fiber` has made rendering 3D models and animations easier to create for React and React Native applications. By building our 3D ludo dice box, we’ve learned about the basics of Three.js alongside its components and benefits of `react-three-fiber` as well as how to use it.

You can take this further by building 3D models and animations in your React and Native applications by using `react-three-fiber` on your own. I’d love to see what new things you come up with!

*You can read more on Three.js and `react-three-fiber` in the references below.*

### Related Resources

- [Three.js documentation](https://threejs.org/)
- [Three.js fundamentals](https://threejsfundamentals.org/threejs/lessons/threejs-fundamentals.html)
- [React-Three-fiber](https://github.com/pmndrs/react-three-fiber) GitHub repo by Poimandres
- [react-three-fiber](https://inspiring-wiles-b4ffe0.netlify.app/) documentation
- [React Hooks (useState, useMemo, etc.) official documentation](https://reactjs.org/docs/hooks-intro.html)

{{< signature "ks, ra, il" >}}
