---
title: 'Gatsby Serverless Functions And The International Space Station'
slug: gatsby-serverless-functions-international-space-station
author: paul-scanlon
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07c5052-399e-4aee-aa83-706eb1f0c1b6/gatsby-serverless-functions-international-space-station.jpg
date: 2021-07-26T10:30:00.000Z
summary: >-
  Gatsby recently announced the launch of “functions”. In this article, Paul Scanlon explains how to get the current location of the International Space Station (ISS) as it orbits the Earth in realtime using [Gatsby Functions](https://www.gatsbyjs.com/docs/reference/functions/) and then display it on a 3D interactive globe using [React Three Fibre](https://github.com/pmndrs/react-three-fiber). 
description: >-
  Gatsby recently announced the launch of “functions”. In this article, Paul Scanlon explains how to get the current location of the International Space Station (ISS) as it orbits the Earth in real-time using [Gatsby Functions](https://www.gatsbyjs.com/docs/reference/functions/) and then display it on a 3D interactive globe using [React Three Fibre](https://github.com/pmndrs/react-three-fiber).
categories:
  - React
  - Gatsby
  - Serverless
  - JavaScript
---

[Gatsby](https://www.gatsbyjs.com/) recently announced the launch of Functions which opens up a new dimension of possibilities &mdash; and I for one couldn’t be more excited! With Gatsby now providing Serverless Functions on [Gatsby Cloud](https://www.gatsbyjs.com/products/cloud/) (and Netlify also providing support via [@netlify/plugin-gatsby](https://www.npmjs.com/package/@netlify/plugin-gatsby)), the framework that was once misunderstood to be “just for blogs” is now more than ever, (in my opinion) the most exciting technology provider in the [Jamstack](https://jamstack.org/) space.

The demo in this article is the result of a recent project I worked on where I needed to plot geographical locations around a 3D globe and I thought it might be fun to see if it were possible to use the same technique using off-planet locations. Spoiler alert: It’s possible! Here’s a [sneak peek of what I’ll be talking about in this post](https://smashingmagazinewhereisiss.gatsbyjs.io), or if you prefer to jump ahead, the finished code can be found [here](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss).

## Getting Started

With Gatsby Functions, you can create more dynamic applications using techniques typically associated with client-side applications by adding an `api` directory to your project and exporting a function, e.g.

<pre><code class="language-bash">&#124;-- src
  &#124;-- api
     -- some-function.js
  &#124;-- pages
</code></pre>

<pre><code class="language-javascript">// src/api/some-function.js
export default function handler(req, res) {
  res.status(200).json({ hello: `world` })
}
</code></pre>

If you already have a Gatsby project setup, great! but do make sure you’ve upgraded Gatsby to at least version `v3.7`

<pre><code class="language-bash">npm install gatsby@latest --save
</code></pre>

If not, then feel free to clone my absolute bare-bones Gatsby starter repo: [mr-minimum](https://github.com/PaulieScanlon/mr-minimum).

Before I can start using Gatsby Functions to track the International Space Station, I first need to create a globe for it to orbit. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a040d24b-f65e-4eef-9e7e-7c914e22bb1d/featured-image.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a040d24b-f65e-4eef-9e7e-7c914e22bb1d/featured-image.jpg" width="800" height="500" sizes="100vw" caption="Let’s make something like this! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a040d24b-f65e-4eef-9e7e-7c914e22bb1d/featured-image.jpg'>Large preview</a>)" alt="Featured Image showing International Space Station orbiting Earth" >}}

### Step 1: Building The 3D Interactive Globe

I start by setting up a 3D interactive globe which can be used later to plot the current ISS location. 

#### Install Dependencies

<pre><code class="language-bash">npm install @react-three/fiber @react-three/drei three three-geojson-geometry axios --save
</code></pre>

#### Create The Scene

Create a new file in `src/components` called [three-scene.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/components/three-scene.js)

<pre><code class="language-javascript">// src/components/three-scene.js
import React from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls } from '@react-three/drei';

const ThreeScene = () =&gt; {
  return (
    &lt;Canvas
      gl={{ antialias: false, alpha: false }}
      camera={{
        fov: 45,
        position: [0, 0, 300]
      }}
      onCreated={({ gl }) =&gt; {
        gl.setClearColor('#ffffff');
      }}
      style={{
        width: '100vw',
        height: '100vh',
        cursor: 'move'
      }}
    &gt;
      &lt;OrbitControls enableRotate={true} enableZoom={false} enablePan={false} /&gt;
    &lt;/Canvas&gt;
  );
};

export default ThreeScene;
</code></pre>

The above sets up a new `<Canvas />` element and can be configured using props exposed by React Three Fibre.

Elements that are returned as children of the canvas component will be displayed as part of the 3D scene. You’ll see above that I’ve included `<OrbitControls />` which adds touch/mouse interactivity allowing users to rotate the scene in 3D space

Ensure `ThreeScene` is imported and rendered on a page somewhere in your site. In my example repo I’ve added `ThreeScene` to [index.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/pages/index.js):

<pre><code class="language-javascript">// src/pages/index.js
import React from 'react';

import ThreeScene from '../components/three-scene';

const IndexPage = () =&gt; {
  return (
    &lt;main&gt;
      &lt;ThreeScene /&gt;
    &lt;/main&gt;
  );
};

export default IndexPage;
</code></pre>

{{% feature-panel %}}

This won’t do much at the moment because there’s nothing to display in the scene. Let’s correct that!

#### Create The Sphere

Create a file in `src/components` called [three-sphere.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/components/three-sphere.js):

<pre><code class="language-javascript">// src/components/three-sphere.js
import React from 'react';

const ThreeSphere = () =&gt; {
  return (
    &lt;mesh&gt;
      &lt;sphereGeometry args={[100, 32, 32]} /&gt;
      &lt;meshBasicMaterial color="#f7f7f7" transparent={true} opacity={0.6} /&gt;
    &lt;/mesh&gt;
  );
};

export default ThreeSphere;
</code></pre>

If the syntax above looks a little different to that of the [Three.js docs](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene) it’s because React Three Fibre uses a declarative approach to using Three.js in React. 

A good explanation of how constructor arguments work in React Three Fibre can be seen in the docs here: [Constructor arguments](https://docs.pmnd.rs/react-three-fiber/getting-started/your-first-scene#constructor-arguments)

Now add `ThreeSphere` to `ThreeScene`:

<pre><code class="language-diff">// src/components/three-scene.js
import React from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls } from '@react-three/drei';

+ import ThreeSphere from './three-sphere';

const ThreeScene = () =&gt; {
  return (
    &lt;Canvas
      gl={{ antialias: false, alpha: false }}
      camera={{
        fov: 45,
        position: [0, 0, 300]
      }}
      onCreated={({ gl }) =&gt; {
        gl.setClearColor('#ffffff');
      }}
      style={{
        width: '100vw',
        height: '100vh',
        cursor: 'move'
      }}
    &gt;
      &lt;OrbitControls enableRotate={true} enableZoom={false} enablePan={false} /&gt;
+      &lt;ThreeSphere /&gt;
    &lt;/Canvas&gt;
  );
};

export default ThreeScene;
</code></pre>

You should now be looking at something similar to the image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09955dc1-9129-4269-ad1e-0de354c7ee24/three-sphere.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09955dc1-9129-4269-ad1e-0de354c7ee24/three-sphere.jpg" width="800" height="500" sizes="100vw" caption="A blank Three.js sphere rendered in a 3D scene (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09955dc1-9129-4269-ad1e-0de354c7ee24/three-sphere.jpg'>Large preview</a>)" alt="image of ThreeSphere rendered in ThreeScene" >}}

Not very exciting, ay? Let’s do something about that!

#### Create The Geometry (To Visualize The Countries Of Planet Earth)

This next step requires the use of [three-geojson-geometry](https://github.com/vasturiano/three-geojson-geometry) and a CDN resource that contains Natural Earth Data. You can take your pick from [a full list of suitable geometries here](https://geojson.xyz).

I’ll be using [admin 0 countries](https://geojson.io/#map=1/-7/0). I chose this option because it provides enough geometry detail to see each country, but not so much that it will add unnecessary strain on your computer’s GPU.

Now, create a file in `src/components` called [three-geo.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/components/three-geo.js): 

<pre><code class="language-javascript">// src/components/three-geo.js
import React, { Fragment, useState, useEffect } from 'react';
import { GeoJsonGeometry } from 'three-geojson-geometry';
import axios from 'axios';

const ThreeGeo = () =&gt; {
const [isLoading, setIsLoading] = useState(true);
  const [geoJson, setGeoJson] = useState(null);
 
  useEffect(() =&gt; {
    axios
      .get(
   'https://d2ad6b4ur7yvpq.cloudfront.net/naturalearth-3.3.0/ne_110m_admin_0_countries.geojson'
      )
      .then((response) =&gt; {
        setIsLoading(false);
        setGeoJson(response.data);
      })
      .catch((error) =&gt; {
        console.log(error);
        throw new Error();
      });
  }, []);

  return (
    &lt;Fragment&gt;
      {!isLoading ? (
        &lt;Fragment&gt;
          {geoJson.features.map(({ geometry }, index) =&gt; {
            return (
              &lt;lineSegments
                key={index}
                geometry={new GeoJsonGeometry(geometry, 100)}
              &gt;
                &lt;lineBasicMaterial color="#e753e7" /&gt;
              &lt;/lineSegments&gt;
            );
          })}
        &lt;/Fragment&gt;
      ) : null}
    &lt;/Fragment&gt;
  );
};

export default ThreeGeo;
</code></pre>

There’s quite a lot going on in this file so I’ll walk you through it.

1. Create an `isLoading` state instance using React hooks and set it to `true`. This prevents React from attempting to return data I don’t yet have. 
2. Using a `useEffect` I request the geojson from the CloudFront CDN.
3. Upon successful retrieval I set the response in React state using `setGeoJson(...)` and set `isLoading` to `false`
4. Using an [Array.prototype.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) I iterate over the “features” contained within the geojson response and return `lineSegments` with `lineBasicMaterial` for each `geometry`
5. I set the `lineSegments` `geometry` to the return value provided by `GeoJsonGeomtry` which is passed the “features” `geometry` along with a radius of `100`.

(You may have noticed I’ve used the same radius of `100` here as I’ve used in the `sphereGeometry` `args` in [three-sphere.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/components/three-sphere.js). You don’t have to set the radius to the same value but it makes sense to use the same radii for `ThreeSphere` and `ThreeGeo`.

If you’re interested to know more about how GeoJsonGeometry works, here’s the open-source repository for reference: [https://github.com/vasturiano/three-geojson-geometry](https://github.com/vasturiano/three-geojson-geometry). The repository has an [example](https://github.com/vasturiano/three-geojson-geometry/tree/master/example) directory however, the syntax is slightly different from what you see here because the examples are written in vanilla JavaScript not React.

#### Combine The Sphere And Geometry

Now it’s time to overlay the geometry on top of the blank sphere: Add `ThreeGeo` to `ThreeScene`

<pre><code class="language-diff">// src/components/three-scene.js
import React from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls } from '@react-three/drei';

import ThreeSphere from './three-sphere';
+ import ThreeGeo from './three-geo';


const ThreeScene = () =&gt; {
  return (
    &lt;Canvas
      gl={{ antialias: false, alpha: false }}
      camera={{
        fov: 45,
        position: [0, 0, 300]
      }}
      onCreated={({ gl }) =&gt; {
        gl.setClearColor('#ffffff');
      }}
      style={{
        width: '100vw',
        height: '100vh',
        cursor: 'move'
      }}
    &gt;
      &lt;OrbitControls enableRotate={true} enableZoom={false} enablePan={false} /&gt;
      &lt;ThreeSphere /&gt;
+      &lt;ThreeGeo /&gt;
    &lt;/Canvas&gt;
  );
};
</code></pre>

You should now be looking at something similar to the image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a47128cb-92f7-4563-bfe8-0a73d06f4d43/three-geo.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a47128cb-92f7-4563-bfe8-0a73d06f4d43/three-geo.jpg" width="800" height="500" sizes="100vw" caption="Exciting Three.js sphere displaying the countries of the world (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a47128cb-92f7-4563-bfe8-0a73d06f4d43/three-geo.jpg'>Large preview</a>)" alt="image of ThreeGeo rendered in ThreeScene" >}}

Now that’s slightly more exciting! 

{{% ad-panel-leaderboard %}}

### Step 2: Building A Serverless Function

#### Create A Function

This next step is where I use a Gatsby Function to request data from [Where is ISS at](https://wheretheiss.at/), which returns the current location of the International Space Station.

Create a file in `src/api` called [get-iss-location.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/api/get-iss-location.js):

<pre><code class="language-javascript">// src/api/get-iss-location.js
const axios = require('axios');

export default async function handler(req, res) {
  try {
    const { data } = await axios.get(
      'https://api.wheretheiss.at/v1/satellites/25544'
    );

    res.status(200).json({ iss_now: data });
  } catch (error) {
    res.status(500).json({ error });
  }
}
</code></pre>

This function is responsible for fetching data from `api.whereistheiss.at` and upon success will return the `data` and a `200` status code back to the browser.

The Gatsby engineers have done **such** an amazing job at simplifying serverless functions that the above is all you really need to get going, but here’s a little more detail about what’s going on. 

* The function is a **default** export from a file named `get-iss-location.js`;
* With Gatsby Functions the filename becomes the file path used in a client-side `get` request prefixed with _api_, e.g. `/api/get-iss-location`;
* If the request to “Where is ISS at” is successful I return an `iss_now` object containing `data` from the Where is ISS at API and a status code of `200` back to the client;
* If the request errors I send the `error` back to the client.

### Step 3: Build The International Space Station

#### Creating The ISS Sphere

In this next step, I use Gatsby Functions to position a sphere that represents the International Space Station as it orbits the globe. I do this by repeatedly calling an `axios.get` request from a `poll` function and setting the response in React state.

Create a file in `src/components` called [three-iss.js](https://github.com/PaulieScanlon/smashing-magazine-where-is-iss/blob/main/src/components/three-iss.js)

<pre><code class="language-javascript">// src/components/three-iss.js
import React, { Fragment, useEffect, useState } from 'react';
import * as THREE from 'three';
import axios from 'axios';

export const getVertex = (latitude, longitude, radius) =&gt; {
  const vector = new THREE.Vector3().setFromSpherical(
    new THREE.Spherical(
      radius,
      THREE.MathUtils.degToRad(90 - latitude),
      THREE.MathUtils.degToRad(longitude)
    )
  );
  return vector;
};

const ThreeIss = () =&gt; {
  const [issNow, setIssNow] = useState(null);

  const poll = () =&gt; {
    axios
      .get('/api/get-iss-location')
      .then((response) =&gt; {
        setIssNow(response.data.iss_now);
      })
      .catch((error) =&gt; {
        console.log(error);
        throw new Error();
      });
  };

  useEffect(() =&gt; {
    const pollInterval = setInterval(() =&gt; {
      poll();
    }, 5000);

    poll();
    return () =&gt; clearInterval(pollInterval);
  }, []);

  return (
    &lt;Fragment&gt;
      {issNow ? (
        &lt;mesh
          position={getVertex(
            issNow.latitude,
            issNow.longitude,
            120
          )}
        &gt;
          &lt;sphereGeometry args={[2]} /&gt;
          &lt;meshBasicMaterial color="#000000" /&gt;
        &lt;/mesh&gt;
      ) : null}
    &lt;/Fragment&gt;
  );
};

export default ThreeIss;
</code></pre>

There’s quite a lot going on in this file so I’ll walk you through it.

1. Create an `issNow` state instance using React hooks and set it to null. This prevents React from attempting to return data I don’t yet have;
2. Using a `useEffect` I create a JavaScript interval that calls the `poll` function every 5 seconds;
3. The `poll` function is where I request the ISS location from the Gatsby Function endpoint (`/api/get-iss-location`);
4. Upon successful retrieval, I set the response in React state using `setIssNow(...)`;
5. I pass the `latitude` and `longitude` onto a custom function called `getVertex`, along with a `radius`.

You may have noticed that here I’m using a radius of `120`. This does differ from the `100` radius value used in `ThreeSphere` and `ThreeGeo`. The effect of the larger radius is to position the ISS higher up in the 3D scene, rather than at ground level &mdash; because that’s logically where the ISS would be, right?  
`100` has the effect of the sphere and geometry overlapping to represent Earth, and `120` for the ISS has the effect of the space station “orbiting” the globe I’ve created. 

One thing that took a bit of figuring out, at least for me, was how to use spherical two dimensional coordinates (latitude and longitude) in three dimensions, e.g. x,y,z. The concept has been explained rather well in [this post by Mike Bostock](https://observablehq.com/@mbostock/geojson-in-three-js). 

The key to plotting lat / lng in 3D space lies within this formula… which makes absolutely no sense to me!

<pre><code class="language-bash">x=rcos(ϕ)cos(λ)
y=rsin(ϕ)
z=−rcos(ϕ)sin(λ)
</code></pre>

Luckily, [Three.js](https://threejs.org/) has a set of [MathUtils](https://threejs.org/docs/?q=Math#api/en/math/MathUtils) which I’ve used like this:

* Pass the `latitude`, `longitude` and `radius` into the `getVertex(...)` function
* Create a new `THREE.Spherical` object from the above named parameters 
* Set the `THREE.Vector3` object using the Spherical values returned by the `setFromSpherical` helper function.

These numbers can now be used to position elements in 3D space on their respective x, y, z axis &mdash; phew! Thanks, Three.js!

Now add `ThreeIss` to `ThreeScene`:

<pre><code class="language-diff">import React from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls } from '@react-three/drei';

import ThreeSphere from './three-sphere';
import ThreeGeo from './three-geo';
+ import ThreeIss from './three-iss';

const ThreeScene = () =&gt; {
  return (
    &lt;Canvas
      gl={{ antialias: false, alpha: false }}
      camera={{
        fov: 45,
        position: [0, 0, 300]
      }}
      onCreated={({ gl }) =&gt; {
        gl.setClearColor('#ffffff');
      }}
      style={{
        width: '100vw',
        height: '100vh',
        cursor: 'move'
      }}
    &gt;
      &lt;OrbitControls enableRotate={true} enableZoom={false} enablePan={false} /&gt;
      &lt;ThreeSphere /&gt;
      &lt;ThreeGeo /&gt;
+     &lt;ThreeIss /&gt;
    &lt;/Canvas&gt;
  );
};

export default ThreeScene;
</code></pre>

*Et voilà!* You should now be looking at something similar to the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b5e051-b2cc-4037-817b-d87d8da08314/three-iss.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b5e051-b2cc-4037-817b-d87d8da08314/three-iss.jpg" width="800" height="500" sizes="100vw" caption="Looook, it’s the ISS (the black dot)! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b5e051-b2cc-4037-817b-d87d8da08314/three-iss.jpg'>Large preview</a>)" alt="image of ThreeIss rendered in ThreeScene" >}}

The `poll` function will repeatedly call the Gatsby Function, which in turn requests the current location of the ISS and re-renders the React component each time a response is successful. You’ll have to watch carefully but the ISS will change position ever so slightly every 5 seconds.

The ISS is traveling at roughly 28,000 km/h and polling the Gatsby Function less often would reveal larger jumps in position. I’ve used 5 seconds here because that’s the most frequent request time as allowed by the Where is ISS at API

You might have also noticed that there’s no authentication required to request data from the Where is ISS at API. Meaning that yes, technically, I could have called the API straight from the browser, however, I’ve decided to make this API call server side using Gatsby Functions for two reasons:

1. It wouldn’t have made a very good blog post about Gatsby Functions if i didn’t use them.
2. Who knows what the future holds for Where is ISS at, it might at some point require authentication and adding API keys to server side API requests is pretty straightforward, moreover this change wouldn’t require any updates to the client side code.

{{% ad-panel-leaderboard %}}

### Step 4: Make It Fancier! (Optional)

I’ve used the above approach to create this slightly more snazzy implementation: [https://whereisiss.gatsbyjs.io](https://whereisiss.gatsbyjs.io),  

In this site I’ve visualized the time delay from the `poll` function by implementing an Svg `<circle />` countdown animation and added an extra `<circle />` with a `stroke-dashoffset` to create the dashed lines surrounding it. 

{{< rimg href="https://whereisiss.gatsbyjs.io" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aab8652-11a0-4c0b-9d44-bd9239674696/where-is-iss.jpg" width="800" height="500" sizes="100vw" caption="Here’s one I made earlier. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aab8652-11a0-4c0b-9d44-bd9239674696/where-is-iss.jpg'>Large preview</a>)" alt="Screen shot of whereisiss.gatsbyjs.io" >}}

### Step 5: Apply Your New Geo Rendering Skills In Other Fun Ways!

I recently used this approach for plotting geographical locations for the competition winners of 500 Bottles: [https://500bottles.gatsbyjs.io](https://500bottles.gatsbyjs.io).  A limited edition **FREE** swag giveaway I worked on with Gatsby’s marketing team. 

{{< rimg breakout="true" href="https://500bottles.gatsbyjs.io" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f42ad133-2741-4263-b292-8bd555336044/500-bottles.jpg" width="800" height="500" sizes="100vw" caption="Three.js can do many things! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f42ad133-2741-4263-b292-8bd555336044/500-bottles.jpg'>Large preview</a>)" alt="Screenshot of 500bottles.gatsbyjs.io" >}}

You can read all about how this site was made on the Gatsby blog: [How We Made the Gatsby 500 Bottles Giveaway](https://www.gatsbyjs.com/blog/how-we-made-the-gatsby-500-bottles-giveaway/?utm_campaign=500-bottles)

In the 500 Bottles site I plot the geographical locations of each of the competition winners using the same method as described in `ThreeIss,` which allows anyone visiting the site to see where in the world the winners are.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b51e5320-34b0-492b-b762-b7cd532e9f8b/where-are-the-winners.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b51e5320-34b0-492b-b762-b7cd532e9f8b/where-are-the-winners.jpg" width="800" height="500" sizes="100vw" caption="The snazziest of them all. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b51e5320-34b0-492b-b762-b7cd532e9f8b/where-are-the-winners.jpg'>Large preview</a>)" alt="image of 500 Bottles winners geographical locations rendered on a 3D globe." >}}

## Closing Thoughts

Gatsby Functions really open up a lot of possibilities for [Jamstack](https://jamstack.org/) developers and never having to worry about spinning up or scaling a server removes so many problems leaving us free to think about new ways they can be used.

I have a number of ideas I’d like to explore using the [V4 Space X API’s](https://github.com/r-spacex/SpaceX-API) so give me a follow if that’s your cup of tea: [@PaulieScanlon](https://twitter.com/PaulieScanlon)

### Further Reading

- If you’re interested in learning more about Gatsby Functions, I highly recommend [Summer Functions](https://queen.raae.codes/), a five week course run by my good chum [Benedicte Raae](https://twitter.com/raae). 
- In a recent **FREE** Friday night Summer Functions webinar we created an emoji slot machine which was super fun:
- [Build an emoji slot machine with a #GatsbyJS Serverless Function · #GatsbySummerFunctions](https://youtu.be/Md07LbVlxGI)
- You might also be interested in the following episode from our pokey internet show [Gatsby Deep Dives](https://www.youtube.com/playlist?list=PL9W-8hhRoLoN7axEFJQ17rJvk2KTiM2GP) where [Kyle Mathews](https://twitter.com/kylemathews) (creator of Gatsby) talks us through how Gatsby Functions work:  
- [Gatsby Serverless Functions 💝 &mdash; Are we live? with Kyle Mathews](https://youtu.be/gG9E7ZYbhGo)
- If you’re interested in learning more about Gatsby I have a number of articles and tutorials on my blog: [https://paulie.dev](https://paulie.dev/), and please do come find me on Twitter if you fancy a chat: [@PaulieScanlon](https://twitter.com/PaulieScanlon)

I hope you enjoyed this post. Ttfn 🕺!

{{< signature "vf, il" >}}
