---
title: 'How To Create A Mobile App In Expo And Firebase (For iOS And Android)'
slug: mobile-app-expo-react-native-firebase-ios-android
author: chafik-gharbi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f02e844-43b6-4fe3-b1bc-d9053c532602/mobile-app-expo-react-native-firebase-ios-android.png
date: 2020-05-18T13:00:00.000Z
summary: >-
  In this article, based on my experience with creating a GPS and navigation application, I will show you how to create a mobile app using Expo and Firebase services such as Firestore, Firebase functions and Expo push notifications.
description: >-
  In this article, based on my experience with creating a GPS and navigation application, I will show you how to create a mobile app using Expo and Firebase services such as Firestore, Firebase functions and Expo push notifications.
categories:
  - Apps
  - React
  - Mobile
  - Firebase
---

<p>Maybe you’ve heard of or worked with React, the JavaScript framework developed by Facebook. The social media company took it even further by releasing React Native, which quickly became the most popular framework for building mobile apps with JavaScript. Many companies embraced the idea and started building their apps with it.</p>

<p>In this article, we’ll get an idea of how to develop an application for Android and iOS using Expo and Firebase, based on my own experience of creating an application with these technologies. If you haven’t worked with Firebase before, please look at its <a href="https://firebase.google.com/docs/web/setup">guide to JavaScript projects</a> before we dive in.</p>

<p>If you are new to JavaScript, make sure you’re clear on the basics of ECMAScript 6’s features, such as class importing and arrow functions. You can learn React Native from the <a href="https://reactnative.dev/docs/getting-started">official documentation</a>, which has a section on <a href="https://reactnative.dev/docs/intro-react">React fundamentals</a>, in case you haven’t worked with React. Don’t worry about how to build an app with Android Studio or Xcode, because we will be using the <a href="https://expo.io/">Expo framework</a>.</p>

### <span class="rh">Recommended reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Styling Components In React'" href="https://www.smashingmagazine.com/2020/05/styling-components-react/" rel="bookmark">Styling Components In React</a></li>
<li><a title="Read 'Best Practices With React Hooks'" href="https://www.smashingmagazine.com/2020/04/react-hooks-best-practices/" rel="bookmark">Best Practices With React Hooks</a></li>
<li><a title="Read 'Creating Sortable Tables With React'" href="https://www.smashingmagazine.com/2020/03/sortable-tables-react/" rel="bookmark">Creating Sortable Tables With React</a></li>
<li><a title="Read 'Implementing Skeleton Screens In React'" href="https://www.smashingmagazine.com/2020/04/skeleton-screens-react/" rel="bookmark">Implementing Skeleton Screens In React</a></li>
</ul>

## Brief Description of Project

<p>We can describe our project as an on-demand transporter &mdash; you could say Uber for merchandise transportation. The user will choose transportation information, such as the type of vehicle and loading and unloading locations, and then nearby transportation vehicles will appear on the map. The user confirms their request, and the drivers receive notifications one by one. Each driver’s notification is active for 25 seconds. If they ignore or decline the request, the system selects another driver, and so on. When a driver accepts the request, the user can monitor the entire transportation process on the map, including via the web application.</p>

{{% feature-panel %}}

## Expo Installation And Configuration

<p>First, we need to install the command line interface (CLI) for Expo, which will help us test to the app in a simulator or on real devices and to build our app in the cloud.</p>

<pre><code class="language-bash">npm install -g expo-cli</code></pre>

<p>Let’s create our Expo project.</p>

<pre><code class="language-bash">expo init</code></pre>

<p>The cool part is that all of your app’s configurations can be done in a single JSON file, <code>app.json</code>. Below are some tips I learned that could increase your chances of being accepted in the App Store and Google Play and to help you avoid some common problems.</p>

<ul>
<li>If you are using Google Maps in your app, be sure to provide the API in the <code>app.json</code> configuration file, in order to make it work properly. Google won’t charge you for native map rendering unless you’re rendering directions or using other paid API services.

<pre><code class="language-json">...
"ios": {
    ...
    "config": {
        "googleMapsApiKey": "YOUR_API_KEY"
    }
},
"android": {
    ...
    "config": {
       "googleMaps": {
          "apiKey": "YOUR_API_KEY"
       }
    }
}</code></pre>
</li>

<li>To make location updates, or any other background tasks, work in the background in iOS, add the following keys under <code>ios.infoPlist</code>:

<pre><code class="language-json">...
"ios": {
    ...
    "infoPlist": {
        ...
        "UIBackgroundModes": [
          "location",
          "fetch"
        ]
    }
}</code></pre>
</li>

<li>If you don’t define which permissions your app will use, then Expo’s generated app will use all available authorizations by default. As a result, Google Play will reject your app. So, specify your required permissions.

<pre><code class="language-json">...
"android": {
    ...
    "permissions": [...],
 }</code></pre>
</li>

<li>Apple requires you to provide a message that tells the user why the app is requesting this access, or else you will be rejected.

<div class="break-out">

<pre><code class="language-json">...
"ios": {
    ...
    "infoPlist": {
        ...
        "NSCameraUsageDescription": "Why are you requesting access to      the device’s camera?",
        "NSLocationWhenInUseUsageDescription": "Why are you requesting access to the device’s camera?"
      }
}</code></pre>
</div>
</li>

<li>Make sure to increment the <code>android.versionCode</code> key before you publish a new version to Google Play.</li>

<li>All updates can be done with Expo over the air, without passing by Google Play or the App Store, unless you make the following changes:

<ul>
<li>upgrade the Expo SDK version;</li>
<li>change anything under the <code>ios</code>, <code>android</code>, or <code>notification</code> keys;</li>
<li>change the app’s <code>splash</code>;</li>
<li>change the app’s <code>icon</code>;</li>
<li>change the app’s <code>name</code>;</li>
<li>change the app’s <code>owner</code>;</li>
<li>change the app’s <code>scheme</code>;</li>
<li>change the <code>facebookScheme</code>;</li>
<li>change your bundled assets under <code>assetBundlePatterns</code>.</li>
</ul></li>

<li>I prefer not to interpret the user experience by setting <code>fallbackToCacheTimeout</code> to <code>0</code> under the <code>updates</code> key. This will allow your app to start immediately with a cached bundle, while downloading a newer one in the background for future use.</li>
</ul>

<p>And here is a complete example of the configuration in <code>app.json</code>:</p>

<div class="break-out">

<pre><code class="language-json">{
  "expo": {
    "name": "Transportili",
    "slug": "transportili",
    "scheme": "transportili",
    "privacy": "public",
    "sdkVersion": "36.0.0",
    "notification": {
      "icon": "./assets/notification-icon.png",
      "androidMode": "default"
    },
    "platforms": [
      "ios",
      "android",
      "web"
    ],
    "version": "0.3.2",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "updates": {
      "fallbackToCacheTimeout": 0
    },
    "assetBundlePatterns": [
      "\**/\*"
    ],
    "ios": {
      "bundleIdentifier": "com.transportili.driver",
      "supportsTablet": false,
      "infoPlist": {
        "UIBackgroundModes": [
          "location",
          "fetch"
        ],
        "LSApplicationQueriesSchemes": [
          "transportili"
        ],
        "NSCameraUsageDescription": "L’application utilise l’appareil photo pour prendre une photo ou numériser vos documents.",
        "NSLocationWhenInUseUsageDescription": "L’application utilise votre position pour aider les chauffeurs ou les transporteurs à vous trouver sur la carte."
      },
      "config": {
        "googleMapsApiKey": "AIzaSyA8Wcik6dTuxBKolLSm5ONBvXNz8Z0T-6c"
      }
    },
    "android": {
      "googleServicesFile": "./google-services.json",
      "package": "com.transportili.driver",
      "versionCode": 6,
      "permissions": [
        "ACCESS_COARSE_LOCATION",
        "ACCESS_FINE_LOCATION"
      ],
      "config": {
        "googleMaps": {
          "apiKey": "AIzaSyA8Wcik6dTuxBKolLSm5ONBvXNz8Z0T-6c"
        }
      }
    },
    "description": "",
    "githubUrl": "https://github.com/chafikgharbi/transportili-native.git"
  }
}</code></pre>
</div>

<p>Let’s move on to installing Firebase, using the following command:</p>

<pre><code class="language-json">expo install firebase</code></pre>

<p>I prefer to create a <code>firebase.js</code> file in the app’s root folder that contains all Firebase configurations. In this case, I’m using only the Firestore and Storage services.</p>

<pre><code class="language-json">const firebaseConfig = {
    apiKey: "api-key",
    authDomain: "project-id.firebaseapp.com",
    databaseURL: "https://project-id.firebaseio.com",
    projectId: "project-id",
    storageBucket: "project-id.appspot.com",
    messagingSenderId: "sender-id",
    appId: "app-id",
    measurementId: "G-measurement-id"
};</code></pre>

<p>Now, whenever we want to use Firebase, we just import this file, as follows:</p>

<pre><code class="language-json">import { firebase, firestore, storage } from "./firebase";</code></pre>

<p>The documentation has a more detailed explanation of <a href="https://docs.expo.io/versions/latest/guides/using-firebase/">using Firebase with Expo</a>.</p>

{{% ad-panel-leaderboard %}}

## The Application’s Database

<p>You can store your data directly in the cloud using Firebase, which offers two types of databases. One is the real-time database, and the other is Firestore, which is considered to be the improved version of the real-time database, with more advanced functionality. Both are NoSQL databases with data sync and instant changes listeners. They have different mechanisms: The real-time database stores data as a JSON object, whereas Firestore stores data as documents in collections. They also calculate usage and cost differently: The former is based on the quantity of data exchanged, and the latter is based on the number of operations in the documents (reads, writes, and deletes).</p>

<p>In my case, I used the Firestore database to store users, requests, vehicles, and other application data. (I was trying to be smart by putting all of my data in one document to decrease operation usage, but then I discovered that each document can store only 1 MB.)</p>

<p>In addition to storing strings, numbers, objects, and so on in Firebase, you can also store a geoPoint, which is an object that contains the coordinates of geographic points (latitude and longitude). Despite this, unfortunately, you cannot make geographic queries, such as retrieving nearby users.</p>

<p>To do that, we can use GeoFirestore. But we have to take into account that this package restricts the document structure of the user to this:</p>

<pre><code class="language-json">User: {
d: {all user data here}
g: (location geohash)
l: {firstore location geopoint}
}</code></pre>

<p>So, if you’re going to implement it directly in your user collection, like I did, then you’ll need to put all of the user’s data in the <code>d</code> key.</p>

<p>Last but not least, don’t forget to optimize your code to avoid unexpected operations:</p>

<ul>
<li>Use offline persistence. On the web, offline persistence is disabled; be sure to enable it.</li>
<li>Use cursor pagination in Firestore queries. Don’t get all data at once.</li>
<li>Always unsubscribe listeners, when done, or unmounted components.</li>
</ul>

## The Application’s Back End

<p>You can manage the Firestore database, send notifications with Expo, and perform certain operations directly from the front end or the mobile application, but there are other operations that we cannot do without a back end and a server. This is why Firebase offers functions &mdash; a cloud back end that allows you to execute Node.js code on a scalable server. I’ve used the Firebase functions for the following:</p>

<ul>
<li><strong>Send notifications (see example below)</strong><br />
To send notifications, we will use push notifications, a tool that helps an app’s owner send messages to their users. It appear in the notifications section of the device, even if the application is not active. We don’t want this process to be stopped by a sudden interruption in connectivity, so we’ll have to use a server.</li>

<li><strong>Run cron jobs</strong><br />
Using cron jobs helps me to manage scheduled requests and notifications.</li>

<li><strong>Sanitize the database</strong><br />
This includes removing useless and ignored requests.</li>

<li><strong>Run sensitive, expensive, or continuous tasks</strong><br />
This includes registering, retrieving users, and scheduling orders. All of these are sensitive operations. If you make them directly from your app or front end, there is a risk of security vulnerability and broken tasks.</li>
</ul>

<p>Joaquin Cid’s article “<a href="https://www.toptal.com/firebase/role-based-firebase-authentication">How to Build a Role-based API With Firebase Authentication</a>” will give you details on how to get started with Firebase functions and how to create a back-end API using Express. It uses TypeScript, but converting TypeScript to JavaScript is not hard.</p>

## Push Notifications

<p>Expo sends a notification to the user’s device from its servers. It identifies the user’s device with a token. When someone uses the application, the app would execute code to obtain the device’s token, and then store this token on the server. I’ve used Firestore as usual to store the token and compare incoming tokens to check whether the user has logged in from another device.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e73fb4-4f0f-43c3-8d07-c13efef95101/1-mobile-app-expo-react-native-firebase-ios-android.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e73fb4-4f0f-43c3-8d07-c13efef95101/1-mobile-app-expo-react-native-firebase-ios-android.png" sizes="100vw" caption="Data to be stored for subsequent push-notification requests. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e73fb4-4f0f-43c3-8d07-c13efef95101/1-mobile-app-expo-react-native-firebase-ios-android.png'>Large preview</a>)" alt="Storing Expo push token" >}}

<p>We get our token using the following function:</p>

<pre><code class="language-json">token = await Notifications.getExpoPushTokenAsync();</code></pre>

<p>Don’t forget to request permission to push notifications. The documentation has <a href="https://docs.expo.io/versions/latest/guides/push-notifications/">example usage</a>.</p>

<p>Whenever you want to send a notification to this user, you would make a request to Expo’s server, which contains the user’s device token already stored on your server.</p>

<div class="break-out">

<pre><code class="language-json">curl -H "Content-Type: application/json" -X POST "https://exp.host/--/api/v2/push/send" -d '{ "to": "ExponentPushToken[xxxxxxxxxxxxxxxxxxxxxx]", "title":"hello", "body": "world" }'</code></pre>
</div>

<p>The following is a simple example that sends notifications to all users using Firebase functions. This example is not secure. If you want to implement authorization and authentication, please follow <a href="https://www.toptal.com/firebase/role-based-firebase-authentication">Cid’s article</a> mentioned above.</p>

<p>After initializing our project using the <a href="https://firebase.google.com/docs/cli">Firebase CLI</a>, let’s install the Express framework to handle our API.</p>

<pre><code class="language-json">npm install express</code></pre>

<p>We need to support CORS and add JSON body-parser middleware. This way, we can make requests from any URL and parse JSON-formatted requests.</p>

<pre><code class="language-json">npm install --save cors body-parser
npm install --save-dev @types/cors</code></pre>

<p>This is the main <code>index.js</code> file of our <code>functions</code> directory:</p>

<div class="break-out">

<pre><code class="language-json">const express = require("express");
const cors = require("cors");
const bodyParser = require("body-parser");
const admin = require("firebase-admin");
const functions = require("firebase-functions");

// Initialize the firebase-admin SDK module
admin.initializeApp(functions.config().firebase);

// Set the Express app
const app = express();
app.use(bodyParser.json());
app.use(cors({ origin: true }));

// Handle push notifications request
app.post("/pushNotifications", require("./controllers/pushNotifications"));

// Handle another request
// app.post("/anotherRoute", require("./controllers/anotherController"));

// Export the https endpoint API handled by the Express app
export const api = functions.https.onRequest(app);</code></pre>
</div>

<p>And this is the <code>pushNotifications.js</code> controller, located in the <code>controllers</code> folder.</p>

<div class="break-out">

<pre><code class="language-json">const admin = require("firebase-admin");
const axios = require("axios");
const chunkArray = require("./chunkArray");
const firestore = admin.firestore();

async function pushNotifications(req, res) {
  try {
    const data = req.body;

    // Get users from Firestore, then build notifications array
    await firestore
      .collection("users").get()
      .then((querySnapshot) => {
        if (querySnapshot.size) {

          // This array will contain each user’s notification
          let notificationsArray = [];

          querySnapshot.forEach((doc) =&gt; {
            let docData = doc.data();
            if (docData && docData.d) {
              let userData = docData.d;

              // The pushNotificationsToken retrieved from the app and stored in Firestore
              if (userData.pushNotificationsToken) {
                notificationsArray.push({
                  to: userData.pushNotificationsToken,
                  ...data,
                });
              }
            }
          });

          // Send notifications to 100 users at a time (the maximum number that one Expo push request supports)
          let notificationsChunks = chunkArray(notificationsArray, 100);
          notificationsChunks.map((chunk) => {
            axios({
              method: "post",
              url: "https://exp.host/--/api/v2/push/send",
              data: chunk,
              headers: {
                "Content-Type": "application/json",
              },
            });
          });
          return res.status(200).send({ message: "Notifications sent!" });
        } else {
          return res.status(404).send({ message: "No users found" });
        }
      })
      .catch((error) =&gt; {
        return res
          .status(500)
          .send({ message: `${error.code} - ${error.message}` });
      });
  } catch (error) {
    return res
      .status(500)
      .send({ message: `${error.code} - ${error.message}` });
  }
}

module.exports = pushNotifications;</code></pre>
</div>

<p>In the controller above, we got all of the app’s users from Firestore. Each user has a push token. We divided this list into sets of 100 users, because a single request to Expo can hold only 100 notifications. Then, we sent these notifications using Axios.</p>

<p>The following is the <code>chunkArray</code> function:</p>

<pre><code class="language-json">function chunkArray(myArray, chunk_size) {
  var index = 0;
  var arrayLength = myArray.length;
  var tempArray = [];

  for (index = 0; index < arrayLength; index += chunk_size) {
    myChunk = myArray.slice(index, index + chunk_size);
    tempArray.push(myChunk);
  }

  return tempArray;
}</code></pre>

<p>This is an example of how to send notifications via our API using Axios.</p>

<pre><code class="language-json">axios({
  method: "post",
  url: "https://...cloudfunctions.net/api/pushNotifications",
  data: {
    title: "Notification title",
    body: "Notification body",
  },
});</code></pre>

{{% ad-panel-leaderboard %}}

## Maps and Geolocation

### Render Native Google Maps in React Native

<p>To render Google Maps in the mobile application, I used <code>react-native-maps</code>, and to render directions, I used the <code>react-native-maps-directions</code> package. For a web application, I would use pure JavaScript.</p>

<div class="break-out">

<pre><code class="language-bash">npm install react-native-maps react-native-maps-directions</code></pre>
</div>

<p>Then, import these packages:</p>

<div class="break-out">

<pre><code class="language-json">import MapView, { Marker, PROVIDER_GOOGLE } from "react-native-maps";
import MapViewDirections from "react-native-maps-directions";</code></pre>
</div>

<p>We’ll render the map with markers and directions:</p>

<div class="break-out">

<pre><code class="language-json">&lt;MapView
   style={mapStyle}
   // Reference is useful for controlling the map like mapView.fitToCoordinates(...)
   ref={(ref) => (mapView = ref)}
   // For better performance, avoid using default map on iOS
   provider={PROVIDER_GOOGLE}
   // Show the blue dot that represents the current location on the map
   showsUserLocation={true}
   initialRegion={{
   ...this.state.currentLocation,
   latitudeDelta: LATITUDE_DELTA,
   longitudeDelta: LONGITUDE_DELTA,
   }}
   /*
   * Watch region change when the user moves the map
   * for example, to get the address with reverse geocoding.
   \*/
   onRegionChangeComplete={(region) =&gt; {
   console.log(
       `Map center: latitude: ${region.latitude}${region.latitude}
       longitude: ${region.latitude}${region.longitude}`
   );
   }}
   // Map edge paddings
   mapPadding={{
   top: 20,
   right: 20,
   bottom: 20,
   left: 20,
   }}
&gt;
{/* Render marker with custom icon \*/}
   {this.state.marker && (
   &lt;Marker
       title={this.state.marker.title}
       coordinate={{
       latitude: this.state.marker.latitude,
       longitude: this.state.marker.longitude,
       }}
   &gt;
       &lt;MaterialIcons name="place" size={40} color="green" /&gt;
   &lt;/Marker&gt;
   )}

 {/* Render multiple markers \*/}
   {this.state.markers.map((marker, index) =&gt; {
   return (
       &lt;Marker
       key={index}
       title={marker.address}
       coordinate={{
           latitude: marker.latitude,
           longitude: marker.longitude,
       }}
       &gt;
       &lt;MaterialIcons name="place" size={40} color="green" /&gt;
       &lt;/Marker&gt;
   );
   })}

 {/* Render directions from array of points \*/}
   {this.state.directions.length &gt;= 2 && (
   &lt;MapViewDirections
       origin={this.state.directions[0]}
       destination={
       this.state.directions[this.state.directions.length - 1]
       }
       waypoints={
       this.state.directions.length > 2
           ? this.state.directions.slice(1, -1)
           : null
       }
       optimizeWaypoints={true}
       apikey={GOOGLE_MAPS_APIKEY}
       strokeWidth={5}
       strokeColor="green"
       onReady={(result) =&gt; {
       console.log(
           `Distance "${result.distance} km", "${result.duration} min"`
       );
       }}
       onError={(errorMessage) =&gt; {
       console.log(errorMessage);
       }}
   /&gt;
   )}
&lt;/MapView&gt;</code></pre>
</div>

## Watch User’s Location in Foreground and Background

<p>The Expo framework supports background location updates, I want to use this feature to get the user’s position. Even if the app is not in the foreground or the phone is locked, the application should always send the location to the server.</p>

<pre><code class="language-json">import * as Location from "expo-location";
import * as TaskManager from "expo-task-manager";
import geohash from "ngeohash";
import { firebase, firestore } from "../firebase";


let USER_ID = null;
let LOCATION_TASK = "background-location";

let updateLocation = (location) =&gt; {
  if (USER_ID) {
    firestore
      .collection("users")
      .doc(USER_ID)
      .update({
        "d.location": new firebase.firestore.GeoPoint(
          location.latitude,
          location.longitude
        ),
        g: geohash.encode(location.latitude, location.longitude, 10),
        l: new firebase.firestore.GeoPoint(
          location.latitude,
          location.longitude
        ),
      });
  }
};

TaskManager.defineTask(LOCATION_TASK, ({ data, error }) =&gt; {
  if (error) {
    // Error occurred - check `error.message` for more details.
    return;
  }
  if (data) {
    const { locations } = data;

    // Current position with latitude and longitude
    currentLocation = {
      latitude: locations[0].coords.latitude,
      longitude: locations[0].coords.longitude,
    };
    updateLocation(currentLocation);
  }
});

export default async function watchPosition(userid) {
  // Set user ID
  USER_ID = userid;

  // Ask permissions for using GPS
  const { status } = await Location.requestPermissionsAsync();
  if (status === "granted") {
    // watch position in background
    await Location.startLocationUpdatesAsync(LOCATION_TASK, {
      accuracy: Location.Accuracy.BestForNavigation,
      distanceInterval: 10,
      showsBackgroundLocationIndicator: true,
      foregroundService: {
        notificationTitle: "Title",
        notificationBody: "Explanation",
        notificationColor: "#FF650D",
      },
    });
    // Watch position in foreground
    await Location.watchPositionAsync(
      {
        accuracy: Location.Accuracy.BestForNavigation,
        distanceInterval: 10,
      },
      (location) => {
        let currentLocation = {
          latitude: location.coords.latitude,
          longitude: location.coords.longitude,
        };
        updateLocation(currentLocation);
      }
    );
  } else {
    // Location permission denied
  }
}</code></pre>

<p>If you’ll notice, I’ve used different structures when updating the location to Firestore. That’s because I’m using the GeoFirestore package to query nearby users.</p>

## Using WebView in React Native

<p>The application is not only for mobile users, but also for desktop users. So, let’s not spend time developing another application that shares much of the same functionality, such as login and registration, profiles and settings, and orders history.</p>

<p>On the app website, we check whether the user came from a desktop browser or the mobile application. We then redirect them to the corresponding application.</p>

<p>For a mobile application, we have to implement some sort of communication between the native app and WebView app, thanks to the JavaScript injection of <code>postMessage</code> and <code>onMessage</code> in WebView. But be careful when and how you use it:</p>

<blockquote>Security Warning: Currently, <code>onMessage</code> and <code>postMessage</code> do not allow specifying an origin. This can lead to cross-site scripting attacks if an unexpected document is loaded within a <code>WebView</code> instance. Please refer to the MDN documentation for <code>Window.postMessage()</code> for more details on the security implications of this.<br /><br />&mdash; <a href="https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage">React Native documentation</a></blockquote>

<p>We’ll send data from web JavaScript to React Native. Here is an example of sending a user ID:</p>

<pre><code class="language-json">window.ReactNativeWebView.postMessage(
    JSON.stringify({
        action: "setUserID",
        data: user.uid
    })
);</code></pre>

<p>We’ll listen to data coming from the web in WebView.</p>

<pre><code class="language-json">&lt;WebView
  ref={(reference) =&gt; (webview = reference)}
  onMessage={(event) =&gt; {
    let message = JSON.parse(event.nativeEvent.data);
    switch (message.action) {
      case "setUserID":
        let id = message.data;
        break;
      case "anotherAction":
        //
        break;
    }
  }}
/&gt;;</code></pre>

<p>Let’s send data from React Native to the web. The following example sends a location retrieved from React Native.</p>

<div class="break-out">

<pre><code class="language-json">let location = JSON.stringify({ latitude: 36.742022, longitude: 3.103771 });
webview.injectJavaScript(`
  window.injectData({
    action: "setLocation",
    data: JSON.stringify(${location})
  })
\`);</code></pre>
</div>

<p>We’ll read the location on the web:</p>

<pre><code class="language-json">window.injectData = (message) => {
  switch (message.action) {
    case "setLocation":
      let location = JSON.parse(message.data);
      break;
    case "anotherAction":
      //
      break;
  }
};</code></pre>

## The Web Application and Website

<p>All web-related parts, from the website to the web application, were made with Next.js and hosted on Netlify for three main raisons:</p>

<ul>
<li><strong>cost-effectiveness</strong><br />
There is no server to maintain, and Netlify’s free plan is more than enough for my needs. Unlimited private repositories are now free on GitHub, so nothing to worry about there.</li>

<li><strong>effortless development</strong><br />
Commit, push, and let Netlify do the rest. Is anything simpler than that?</li>

<li><strong>speed</strong><br />
The websites are static and all hosted on a content delivery network (CDN). When a user requests these websites, the CDN directs them to the nearest copy in order to minimize latency. So, the websites are extremely fast.</li>
</ul>

## Limitations of Expo

<p>There are two approaches to building an app with Expo: the managed workflow, where you write only JavaScript, and Expo tools and services do the rest for you, and the bare workflow, where you have full control over all aspects of the native project, and where Expo tools can’t help as much. If you plan to follow the first approach, then consider <a href="https://docs.expo.io/introduction/why-not-expo/">Expo’s limitations</a>, because some functionality that exists in major apps, such as Spotify (for example, music playing in the background) and Messenger (call notifications), cannot be done yet.</p>

## Conclusion

<p>Expo is an excellent choice if you are not familiar with native development and you want to avoid all of the headaches associated with creating and regularly deploying an application. Firebase can save you a lot of time and work, because of its scalability and variety of services. However, both are third-party services, over which you have no control, and Firestore is not designed for complex queries and data relationships.</p>

<p>Thanks for your attention. I hope you’ve enjoyed this article and learned something new.</p>

{{< signature "ra, yk, il, al" >}}
