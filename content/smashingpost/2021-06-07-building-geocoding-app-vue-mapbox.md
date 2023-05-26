---
title: 'How To Build A Geocoding App In Vue.js Using Mapbox'
slug: building-geocoding-app-vue-mapbox
author: prince-chukwudire
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20dc2361-e5a5-4a78-b380-2f5942ecfba8/building-geocoding-app-vue-mapbox.jpg
date: 2021-06-07T11:00:00.000Z
summary: >-
  In this guide, we’ll take a general look at the concepts of forward geocoding and reverse geocoding. We will build a mini-app that applies these concepts to display specific locations, using <a href="https://docs.mapbox.com/mapbox-gl-js/api/">Mapbox</a> and Vue.js 2.6.11 to achieve this.
description: >-
  In this guide, we’ll be taking a general look at the concepts of forward geocoding and reverse geocoding, and will build a mini-app that applies these concepts to display specific locations, using Mapbox and Vue.js 2.6.11 to achieve this.
categories:
  - API
  - Vue
  - Apps
  - JavaScript
---

Pinpoint accuracy and modularity are among the perks that make geocodes the perfect means of finding a particular location.

In this guide, we’ll build a [simple geocoding app](https://github.com/smashingmagazine/Tutorials/tree/Geocoding-app-vue) from scratch, using Vue.js and Mapbox. We’ll cover the process from building the front-end scaffolding up to building a geocoder to handle forward geocoding and reverse geocoding. To get the most out of this guide, you’ll need a basic understanding of JavaScript and Vue.js and how to make API calls.

## What Is Geocoding?

Geocoding is the transformation of text-based locations to geographic coordinates (typically, longitude and latitude) that indicate a location in the world.

Geocoding is of two types: **forward and reverse**. Forward geocoding converts location texts to geographic coordinates, whereas reverse geocoding converts coordinates to location texts.

In other words, reverse geocoding turns 40.714224, -73.961452 into “277 Bedford Ave, Brooklyn”, and forward geocoding does the opposite, turning “277 Bedford Ave, Brooklyn” into 40.714224, -73.961452.

To give more insight, we will build a mini web app that uses an interactive web map with custom markers to display location coordinates, which we will subsequently decode to location texts.

Our app will have the following basic functions:

- give the user access to an interactive map display with a marker;
- allow the user to move the marker at will, while displaying coordinates;
- return a text-based location or location coordinates upon request by the user.

{{% feature-panel %}}

## Set Up Project Using Vue CLI

We’ll make use of the [boilerplate found in this repository](https://github.com/smashingmagazine/Tutorials/tree/geocoder/boilerplate). It contains a new project with the Vue CLI and `yarn` as a package manager. You’ll need to clone the repository. Ensure that you’re working from the `geocoder/boilerplate` branch.

## Set Up File Structure of Application

Next, we will need to set up our project’s file structure. Rename the `Helloworld.vue` file in the component’s folder to `Index.vue`, and leave it blank for now. Go ahead and copy the following into the `App.vue` file:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;!--Navbar Here --&gt;
    &lt;div&gt;
      &lt;nav&gt;
        &lt;div class="header"&gt;
          &lt;h3&gt;Geocoder&lt;/h3&gt;
        &lt;/div&gt;
      &lt;/nav&gt;
    &lt;/div&gt;
    &lt;!--Index Page Here --&gt;
    &lt;index /&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import index from "./components/index.vue";
export default {
  name: "App",
  components: {
    index,
  },
};
&lt;/script&gt;</code></pre>

Here, we’ve imported and then registered the recently renamed component locally. We’ve also added a navigation bar to lift our app’s aesthetics.

We need an `.env` file to load the environment variables. Go ahead and add one in the root of your project folder.

## Install Required Packages and Libraries

To kickstart the development process, we will need to install the required libraries. Here’s a list of the ones we’ll be using for this project:

1. **Mapbox GL JS**  
This JavaScript library uses WebGL to render interactive maps from [vector tiles](https://docs.mapbox.com/help/glossary/vector-tiles/) and [Mapbox](https://docs.mapbox.com/mapbox-gl-js/style-spec/).
2. **Mapbox-gl-geocoder**  
This geocoder control for Mapbox GL will help with our forward geocoding.
3. **Dotenv**    
We won’t have to install this because it comes preinstalled with the Vue CLI. It helps us to load environment variables from an `.env` file into [`process.env`](https://nodejs.org/docs/latest/api/process.html#process_process_env). This way, we can keep our configurations separate from our code.
4. **Axios**  
This library will help us make HTTP requests.

Install the packages in your CLI according to your preferred package manager. If you’re using Yarn, run the command below:

<pre><code class="language-bash">cd geocoder && yarn add mapbox-gl @mapbox/mapbox-gl-geocoder axios</code></pre>

If you’re using npm, run this:

<pre><code class="language-bash">cd geocoder && npm i mapbox-gl @mapbox/mapbox-gl-geocoder axios --save</code></pre>

We first had to enter the `geocoder` folder before running the installation command.

## Scaffolding the Front End With Vue.js

Let’s go ahead and create a layout for our app. We will need an element to house our map, a region to display the coordinates while listening to the marker’s movement on the map, and something to display the location when we call the reverse geocoding API. We can house all of this within a card component.

Copy the following into your `Index.vue` file:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="main"&gt;
    &lt;div class="flex"&gt;
      &lt;!-- Map Display here --&gt;
      &lt;div class="map-holder"&gt;
        &lt;div id="map"&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;!-- Coordinates Display here --&gt;
      &lt;div class="dislpay-arena"&gt;
        &lt;div class="coordinates-header"&gt;
          &lt;h3&gt;Current Coordinates&lt;/h3&gt;
          &lt;p&gt;Latitude:&lt;/p&gt;
          &lt;p&gt;Longitude:&lt;/p&gt;
        &lt;/div&gt;
        &lt;div class="coordinates-header"&gt;
          &lt;h3&gt;Current Location&lt;/h3&gt;
          &lt;div class="form-group"&gt;
            &lt;input
              type="text"
              class="location-control"
              :value="location"
              readonly
            /&gt;
            &lt;button type="button" class="copy-btn"&gt;Copy&lt;/button&gt;
          &lt;/div&gt;
          &lt;button type="button" class="location-btn"&gt;Get Location&lt;/button&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;</code></pre>

To see what we currently have, start your development server. For Yarn:

<pre><code class="language-bash">yarn serve</code></pre>

Or for npm:

<pre><code class="language-bash">npm run serve</code></pre>

Our app should look like this now:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2db65f59-f1f9-4373-b2b1-8514d763b09d/1-building-geocoding-app-vue-mapbox.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2db65f59-f1f9-4373-b2b1-8514d763b09d/1-building-geocoding-app-vue-mapbox.png" width="800" height="387" sizes="100vw" caption="Geocoding app scaffold preview. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2db65f59-f1f9-4373-b2b1-8514d763b09d/1-building-geocoding-app-vue-mapbox.png'>Large preview</a>)" alt="Scaffold preview" >}}

The blank spot to the left looks off. It should house our map display. Let’s add that.


## Interactive Map Display With Mapbox

The first thing we need to do is gain access to the Mapbox GL and Geocoder libraries. We’ll start by importing the Mapbox GL and Geocoder libraries in the `Index.vue` file.

<pre><code class="language-javascript">import axios from "axios";
import mapboxgl from "mapbox-gl";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";
import "@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";</code></pre>

Mapbox requires a unique [access token](https://docs.mapbox.com/help/glossary/access-token/) to compute map vector tiles. [Get yours](https://docs.mapbox.com/help/glossary/access-token/), and add it as an environmental variable in your `.env` file.

<pre><code class="language-javascript">.env</code></pre>

<pre><code class="language-javascript">VUE_APP_MAP_ACCESS_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</code></pre>

We also need to define properties that will help with putting our map tiles together in our data instance. Add the following below the spot where we imported the libraries:

<pre><code class="language-javascript">export default {
  data() {
    return {
      loading: false,
      location: "",
      access_token: process.env.VUE_APP_MAP_ACCESS_TOKEN,
      center: [0, 0],
      map: {},
    };
  },
}</code></pre>

- The `location` property will be modeled to the input that we have in our scaffolding. We will use this to handle reverse geocoding (i.e. display a location from the coordinates).
- The `center` property houses our coordinates (longitude and latitude). This is critical to putting our map tiles together, as we will see shortly.
- The `access_token` property refers to our environmental variable, which we added earlier.
- The `map` property serves as a constructor for our map component.

Let’s proceed to create a method that plots our interactive map with our forward geocoder embedded in it. This method is our base function, serving as an intermediary between our component and Mapbox GL; we will call this method `createMap`. Add this below the data object:

<pre><code class="language-javascript">mounted() {
  this.createMap()
},

methods: {
  async createMap() {
    try {
      mapboxgl.accessToken = this.access_token;
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11",
        center: this.center,
        zoom: 11,
      });

    } catch (err) {
      console.log("map error", err);
    }
  },
},
</code></pre>

To create our map, we’ve specified a `container` that houses the map, a `style` property for our map’s display format, and a `center` property to house our coordinates. The `center` property is an array type and holds the longitude and latitude.

Mapbox GL JS initializes our map based on these parameters on the page and returns a `Map` object to us. The `Map` object refers to the map on our page, while exposing methods and properties that enable us to interact with the map. We’ve stored this returned object in our data instance, `this.map`.

{{% ad-panel-leaderboard %}}

## Forward Geocoding With Mapbox Geocoder

Now, we will add the geocoder and custom marker. The geocoder handles forward geocoding by transforming text-based locations to coordinates. This will appear in the form of a search input box appended to our map.

Add the following below the `this.map` initialization that we have above:

<pre><code class="language-javascript">let geocoder =  new MapboxGeocoder({
    accessToken: this.access_token,
    mapboxgl: mapboxgl,
    marker: false,
  });

this.map.addControl(geocoder);

geocoder.on("result", (e) => {
  const marker = new mapboxgl.Marker({
    draggable: true,
    color: "#D80739",
  })
    .setLngLat(e.result.center)
    .addTo(this.map);
  this.center = e.result.center;
  marker.on("dragend", (e) => {
    this.center = Object.values(e.target.getLngLat());
  });
});</code></pre>

Here, we’ve first created a new instance of a geocoder using the `MapboxGeocoder` constructor. This initializes a geocoder based on the parameters provided and returns an object, exposed to methods and events. The `accessToken` property refers to our Mapbox access token, and `mapboxgl` refers to the [map library](https://docs.mapbox.com/#maps) currently used.

Core to our app is the custom marker; the geocoder comes with one by default. This, however, wouldn’t give us all of the customization we need; hence, we’ve disabled it.

Moving along, we’ve passed our newly created geocoder as a parameter to the `addControl` method, exposed to us by our map object. `addControl` accepts a `control` as a parameter.

To create our custom marker, we’ve made use of an event exposed to us by our geocoder object. The `on` event listener enables us to subscribe to events that happen within the geocoder. It accepts various [events](https://github.com/mapbox/mapbox-gl-geocoder/blob/master/API.md#on) as parameters. We’re listening to the `result` event, which is fired when an input is set.

In a nutshell, on `result`, our marker constructor creates a marker, based on the parameters we have provided (a draggable attribute and color, in this case). It returns an object, with which we use the `setLngLat` method to get our coordinates. We append the custom marker to our existing map using the `addTo` method. Finally, we update the `center` property in our instance with the new coordinates.

We also have to track the movement of our custom marker. We’ve achieved this by using the `dragend` event listener, and we updated our `center` property with the current coordinates.

Let’s update the template to display our interactive map and forward geocoder. Update the coordinates display section in our template with the following:

<pre><code class="language-html">&lt;div class="coordinates-header"&gt;
  &lt;h3&gt;Current Coordinates&lt;/h3&gt;
  &lt;p&gt;Latitude: {{ center[0] }}&lt;/p&gt;
  &lt;p&gt;Longitude: {{ center[1] }}&lt;/p&gt;
&lt;/div&gt;
</code></pre>

Remember how we always updated our `center` property following an event? We are displaying the coordinates here based on the current value.

To lift our app’s aesthetics, add the following CSS file in the `head` section of the `index.html` file. Put this file in the public folder.

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://api.tiles.mapbox.com/mapbox-gl-js/v0.53.0/mapbox-gl.css" rel="stylesheet" /&gt;</code></pre>
</div>

Our app should look like this now:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ec158a-9a69-4349-8676-38307bfda229/2-building-geocoding-app-vue-mapbox.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ec158a-9a69-4349-8676-38307bfda229/2-building-geocoding-app-vue-mapbox.png" width="800" height="389" sizes="100vw" caption="Forward geocoding preview. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ec158a-9a69-4349-8676-38307bfda229/2-building-geocoding-app-vue-mapbox.png'>Large preview</a>)" alt="Forward geocoding preview" >}}

{{% ad-panel-leaderboard %}}

## Reverse Geocode Location With Mapbox API

Now, we will handle reverse geocoding our coordinates to text-based locations. Let’s write a method that handles that and trigger it with the `Get Location` button in our template.

Reverse geocoding in Mapbox is handled by the reverse geocoding API. This accepts `longitude`, `latitude`, and `access token` as request parameters. This call returns a response payload &mdash; typically, with various details. Our concern is the first object in the `features` array, where the reverse geocoded location is.

We’ll need to create a function that sends the `longitude`, `latitude` and `access_token` of the location we want to get to the Mapbox API. We need to send them in order to get the details of that location.

Finally, we need to update the `location` property in our instance with the value of the `place_name` key in the object.

Below the `createMap()` function, let’s add a new function that handles what we want. This is how it should look:

<div class="break-out">

<pre><code class="language-javascript">async getLocation() {
  try {
    this.loading = true;
    const response = await axios.get(
      `https://api.mapbox.com/geocoding/v5/mapbox.places/${this.center[0]},${this.center[1]}.json?access_token=${this.access_token}`
    );
    this.loading = false;
    this.location = response.data.features[0].place_name;
  } catch (err) {
    this.loading = false;
    console.log(err);
  }
},
</code></pre>
</div>

This function makes a `GET` request to the Mapbox API. The response contains `place_name` &mdash; the name of the selected location. We get this from the response and then set it as the value of `this.location`.

With that done, we need to edit and set up the button that will call this function we have created. We’ll make use of a `click` event listener &mdash; which will call the `getLocation` method when a user clicks on it. Go ahead and edit the button component to this.

<pre><code class="language-javascript">&lt;button
  type="button"
  :disabled="loading"
  :class="{ disabled: loading }"
  class="location-btn"
  @click="getLocation"
&gt;
  Get Location
&lt;/button&gt;
</code></pre>

As icing on the cake, let’s attach a function to copy the displayed location to the clipboard. Add this just below the `getLocation` function:

<pre><code class="language-javascript">copyLocation() {
  if (this.location) {
    navigator.clipboard.writeText(this.location);
    alert("Location Copied")
  }
  return;
},
</code></pre>

Update the `Copy` button component to trigger this:

<pre><code class="language-html">&lt;button type="button" class="copy-btn" @click="copyLocation"&gt;</code></pre>

## Conclusion

In this guide, we’ve looked at geocoding using Mapbox. We built a geocoding app that transforms text-based locations to coordinates, displaying the location on an interactive map, and that converts coordinates to text-based locations, according to the user’s request. This guide is just the beginning. A lot more could be achieved with the geocoding APIs, such as changing the presentation of the map using the various [map styles](https://docs.mapbox.com/api/maps/styles/) provided by Mapbox.

- *The source code is [available on GitHub](https://github.com/smashingmagazine/Tutorials/tree/Geocoding-app-vue).*

### Resources

- “[Geocoding](https://docs.mapbox.com/api/search/geocoding/)”, Mapbox documentation
- “[Styles](https://docs.mapbox.com/api/maps/styles/)”, Mapbox documentation
- “[Using Env Variables in Client-Side Code](https://cli.vuejs.org/guide/mode-and-env.html#using-env-variables-in-client-side-code)”, in “Modes and Environment Variables”, Vue CLI

{{< signature "ks, vf, yk, il, al" >}}
