---
title: 'How To Create Maps With React And Leaflet'
slug: javascript-maps-react-leaflet
author: shajia-abidi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f9c12bd-cd42-4f7a-bac9-8dc24518c84a/javascript-maps-react-leaflet.png
date: 2020-02-07T11:00:00.000Z
summary: >-
  Leaflet is a very powerful tool, and we can create a lot of different kinds of maps. This tutorial will help you understand how to create an advanced map along with the help of React and Vanilla JS.
description: >-
  Leaflet is a very powerful tool, and we can create a lot of different kinds of maps. This tutorial will help you understand how to create an advanced map along with the help of React and Vanilla JS.
categories:
  - React
  - JavaScript
  - User Interaction
---

Grasping information from a CSV or a JSON file isn’t only complicated, but is also tedious. Representing the same data in the form of visual aid is simpler. In this article, we’re going to represent the locations of the non-medical fire incidents to which the SF Fire Department responded on a map.

For this tutorial, we will be utilizing the following tools:

- [Leaflet](https://leafletjs.com/)  
*A JavaScript library for interactive maps*
- [React](https://reactjs.org/)  
*A JavaScript library for building user interfaces*
- [React-Leaflet](https://react-leaflet.js.org/)  
*React components for Leaflet maps*

## What Is Leaflet?

At about 27k stars, Leaflet.js is one of the leading open-source JavaScript libraries for mobile-friendly interactive maps. It takes advantage of HTML5 and CSS3 on modern browsers while being accessible on older ones too. All in all, it supports all the primary desktop and mobile platforms. 

Leaflet weighs about 38KB and works perfectly for basic things. For additional extensions, it can be extended with a vast amount of [plugins](https://leafletjs.com/plugins.html).

A lot of newspapers, including NPR, Washington Post, Boston Globe, among others, and other organizations use Leaflet for their in-depth data projects. 

The San Francisco Chronicle, for example, did a project called the [California Fire tracker](https://projects.sfchronicle.com/trackers/california-fire-map/) &mdash; an interactive map that provides information on wildfires burning across California, using Leaflet. Not only did they pinpoint the origin of the fire, but they also showed us the trajectory of it.

Since this is an introductory tutorial, we will only be marking the locations of the fire incidents and display some details about it.

Before jumping into React, let’s understand the basics of Leaflet. For this, we will create a simple example where we will be setting up a Leaflet map, working with markers, and popups.

{{% feature-panel %}}

First, let’s create *index.html* and *app.js* files in our `/project` folder and link the latter to our *index.html* file. 

To start using Leaflet, we need to link Leaflet CSS and Leaflet JS in our head tags. One thing to keep in mind is that Leaflet CSS comes before Leaflet JS. That’s it for Leaflet. 

There’s one more thing we need to add to our *index.html* file &mdash; a container that will hold our map. 

<pre><code class="language-css">&lt;div id="mapid"&gt;&lt;/div&gt;
</code></pre>

Before we forget, let’s give height to our div. 

<pre><code class="language-css">#mapid { height: 1000px; }
</code></pre>

Now comes the fun part. Whether you decide to create a new JavaScript file or continue in script tags, make sure `<div id="mapid">` is added to the dom before calling `L.map('mapid')`. 

You’re probably asking "But, why?" Well, it’s because it will give you an error if you bind the map to a container that doesn’t exist just yet. 

<pre><code class="language-css">Uncaught Error: Map container not found
</code></pre>

## Creating A Map

Now, onto the fun part. To initialize the map, we pass in our div to `L.map()` with some options. 

<pre><code class="language-css">const myMap = L.map('mapid', {
 center: [37.7749, -122.4194],
  zoom: 13
})
</code></pre>

Let’s go step by step to understand what just happened. We use Map class of Leaflet API to create a map on the page. We pass in two parameters to this class:

1. We passed in a string variable representing the `DOM` ID
2. An optional object literal with map options

There are many options we could pass to our class, but the main two options are the center and zoom. The center defines an initial geographic center of the map while zoom specifies an initial map zoom level. They both are undefined by default. 

For the center, we passed in San Francisco’s coordinates. There are a lot of places where we can perform forward and reverse geocoding, but for basic search such as this, we can google it. 

Usually, the value for zoom will depend on what you want to display. Do you want to show a city or a state? Country or a continent? Go ahead and play around with the zoom value to get a better idea. For this example, we chose 13 because it shows the entire city. 

Another way of initializing the map is by using setView(). It takes the in an array of coordinates and an integer for the zoom level.

<pre><code class="language-css">const myMap = L.map('map').setView([37.7749, -122.4194], 13);
</code></pre>

By default, all mouse and touch interactions on the map are enabled, and it has zoom and attribution controls.

{{% ad-panel-leaderboard %}}

## Creating A Layer

Next, we’ll add a tile layer to our map; in our case, it’s a Mapbox Streets tile layer. We can append various types of tile layers by instantiating the TileLayer class.

To create a tile layer, we need to set the URL template for the tile image, the attribution text, and the maximum zoom level of the layer. The URL template is what gives us access to the desired tile layer from the service provider. Since we are using [Mapbox’s Static Tiles API](https://docs.mapbox.com/api/maps/#static-tiles), we will need to [request an access token](https://www.mapbox.com/studio/account/tokens/).

<div class="break-out">

 <pre><code class="language-bash">L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', { 
attribution: 'Map data &copy; &lt;a href="https://www.openstreetmap.org/"&gt;OpenStreetMap&lt;/a&gt; contributors, &lt;a href="https://creativecommons.org/licenses/by-sa/2.0/"&gt;CC-BY-SA&lt;/a&gt;, Imagery (c) &lt;a href="https://www.mapbox.com/"&gt;Mapbox&lt;/a&gt;',
maxZoom: 18, 
id: 'mapbox/streets-v11', 
accessToken: 'your.mapbox.access.token' }).addTo(mymap);
</code></pre>
</div>

At this point, if we open our index.html in a browser, we should be able to see a map of San Francisco. Let’s drop a pin on the map. 

## Markers And Circles 

We’ve got the map and the layer, but it doesn’t point us to anything specific. To point to a particular location on the map, Leaflet provides us with markers.

To pin a location, we instantiate the marker using the Marker class, pass in the coordinates, and add it to the map. Here we are using the coordinates of Twin Peaks in the city. 

<pre><code class="language-css">const marker = L.marker([37.7544, -122.4477]).addTo(mymap);
</code></pre>

Similarly, we can bind a circle to the map using a `Circle` class.  We pass in a few optional options, such as radius, color, and so on. For the `circle` marker, we are passing in the coordinates of Point Bonita Lighthouse.

<pre><code class="language-css">const circle = L.circle([37.8157, -122.5295], {
 color: 'gold',
 fillColor: '#f03',
 fillOpacity: 0.5,
 radius: 200
}).addTo(mymap);
</code></pre>

## Popups

This is all great, but what if we want to pass in some more information about the location. We do this using popup. 

<pre><code class="language-css">circle.bindPopup("I am pointing to Point Bonita Lighthouse");

marker.bindPopup("I am pointing to Twin Peaks");
</code></pre>

The bindPopup method takes in a specified HTML content and appends it to the marker, so the popup appears when you click on the marker.

{{% ad-panel-leaderboard %}}

## React-Leaflet

Now we know how to create a map, and add markers using Leaflet and vanilla JavaScript. Let’s see how we can achieve the same results with React. We aren’t going to make the same application but instead make an advanced application.

The first task for us is to get an access token from the [San Francisco Open Data](https://datasf.org/opendata/) portal. It’s an online portal where we can find hundreds of datasets from the City and County of San Francisco. I decided to use this resource, but there are plenty of other resources out there that we can use instead.

### Access API Key 


1. Make an account and sign-in to the portal.
2. Click on the manage link towards the bottom-right.
3. Click on Create New API Key and give it a name.
4. Copy your Key ID and Key Secret. You’d need this to access the data.

For this, we will use React-Leaflet – react components for Leaflet maps. Let’s create a react app.

<pre><code class="language-bash">npx create-react-app react-fire-incidents
cd react-fire-incidents
</code></pre>

Then let’s install `react-leaflet`, and Leaflet by running the following command in our terminal: 

<pre><code class="language-bash">npm install react-leaflet leaflet
</code></pre>

### App.js

Let’s create a folder `/components` inside `src`. Inside components, let’s create a file named *Map.js*. This is where our Map will live. Now let’s edit *App.js* by removing unnecessary code and importing modules from `react-leaflet axios` and the newly created *Map.js*.

<pre><code class="language-javascript">import React, { Component, Fragment } from 'react';
import axios from 'axios';
import Map from './components/Map'
</code></pre>

In our App class, we are going to define an array in our state called incidents &mdash; when the page loads, we will push our data into this array. 

<pre><code class="language-javascript">class App extends Component {
 state = {
   incidents: [],
 }
 render() {
   return (
     &lt;div&gt; &lt;/div&gt;
   );
 }
}
export default App;
</code></pre>

Next, we will make a GET request when the component mounts. We have the app token, but we still need an endpoint. Where do we find the endpoint? 

Let’s head over to the portal and click on Browse Data. In the search bar, let’s search for fire incidents. The first result that shows up is what we are looking for. Once we click on the link, we can get the URL by clicking the API button on the top-right.  

We will pass in the endpoint to our GET request, and pass in a limit and our app token as parameters. The original data has thousands of records, but for the sake of keeping things simple, we have limited it to 500. We update our incidents array with our results. 

Once we get the data, we update our state. 

<div class="break-out">

 <pre><code class="language-javascript">async componentDidMount() {
   const res = await axios.get('https://data.sfgov.org/resource/wr8u-xric.json', {
     params: {
       "$limit": 500,
       "$$app_token": YOUR_APP_TOKEN
     }
   })
   const incidents = res.data;
   this.setState({incidents: incidents });
 };
</code></pre>
</div>

This is what our App.js should look like. 

<div class="break-out">

 <pre><code class="language-javascript">class App extends Component {
state = {
  incidents: [],
}

async componentDidMount() {
 const res = await axios.get('https://data.sfgov.org/resource/wr8u-xric.json', {
   params: {
     "$limit": 500,
     "$$app_token": YOUR_APP_TOKEN
   }
 })
 const incidents = res.data;
 this.setState({incidents: incidents });
};
render() {
 return (
&lt;Map incidents={this.state.incidents}/&gt;
 );
}
}
export default App;
</code></pre>
</div>

### Map.js

Since we already know how to create a Leaflet map, this part will be relatively easy. We will import `Map`, `TileLayer`, `Marker`, `Popup` components from `react-leaflet`.

<pre><code class="language-javascript">import React, { Component } from 'react'
import { Map, TileLayer, Marker, Popup } from 'react-leaflet'
</code></pre>

If we remember from the previous example, we need coordinates and a zoom level for initializing the map. In our `Map` class, we define them in our state using `lat`, `lng` and `zoom` variables.

<pre><code class="language-javascript">export default class Map extends Component {
   state = {
       lat: 37.7749,
       lng: -122.4194,
       zoom: 13,
   }
   render() {
       return (
     &lt;div&gt;&lt;/div&gt;
        )
    }
}
</code></pre>

Then we will check whether our array of incidents is empty. If it’s empty, we will return a message saying “Data is Loading”; otherwise, we will return a map. 

In our `react-leaflet`’s `Map` component, we will pass center coordinates and a zoom level along with some styling. In our `TileLayer` component, we will pass attribution and URL similar to our previous example. 

<div class="break-out">

 <pre><code class="language-javascript">render() {
       return (
          this.props.incidents ?
              &lt;Map 
                 center={[this.state.lat, this.state.lng]} 
                 zoom={this.state.zoom} 
                 style={{ width: '100%', height: '900px'}}
              &gt;
              &lt;TileLayer
                attribution='&amp;copy &lt;a href="https://osm.org/copyright"&gt;OpenStreetMap&lt;/a&gt; contributors'
                url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
               /&gt;
             &lt;/Map&gt;
               :
               'Data is loading...'
       )
   }
}
</code></pre>
</div>

Next, we loop over our `props.incident` and pass in the coordinates of every incident to the Marker component. Since React warns us to pass a key to every item in an array, we will pass in a key to Marker as well. 

Inside the `Marker` component, we pass in a `Popup` component. I’ve added some information about the incident inside the popup. 

<div class="break-out">

 <pre><code class="language-javascript">&lt;Map 
    center={[this.state.lat, this.state.lng]} 
    zoom={this.state.zoom} 
    style={{ width: '100%', height: '900px'}}&gt;
       &lt;TileLayer
          attribution='&amp;copy &lt;a href="https://osm.org/copyright"&gt;OpenStreetMap&lt;/a&gt; contributors'
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        /&gt;
        {
          this.props.incidents.map(incident =&gt; {
               const point = [incident['point']['coordinates'][1],                 incident['point']['coordinates'][0]]
         

return (
    &lt;Marker position={point} key={incident['incident_number']} &gt;
         &lt;Popup&gt;
            &lt;span&gt;ADDRESS: {incident['address']}, {incident['city']} - {incident['zip_code']}&lt;/span&gt;
          &lt;br/&gt;
            &lt;span&gt;BATTALION: {incident['battalion']}&lt;/span&gt;&lt;br/&gt;
         &lt;/Popup&gt;
     &lt;/Marker&gt;
  )
 })
}
&lt;/Map&gt;
</code></pre>
</div>

And this is it. If we run our app, and if everything went fine, we should be able to see a map of San Francisco with 500 markers pointing us to the locations of the fire-incidents. If we click on one of those markers, a popup will appear with more information about the incident. 

## Wrapping Up

Even though we covered a lot, this was just the basics. Leaflet is a very powerful tool, and we can create a lot of different kinds of maps. If you want to play around, try adding another [layer](https://leafletjs.com/examples/layers-control/) or a [custom icon](https://leafletjs.com/examples/custom-icons/). Or maybe you would like to create an interactive [Choropleth Map](https://leafletjs.com/examples/choropleth/). 

{{< signature "dm, il" >}}
