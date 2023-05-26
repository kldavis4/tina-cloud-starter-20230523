---
title: 'Firebase Push Notifications In React'
slug: firebase-push-notifications-react
author: chidi-orji
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b8cd2f8-397b-4cee-a333-e9a01c6f6f2e/firebase-push-notifications-react.png
date: 2020-06-29T13:30:00.000Z
summary: >-
  In this tutorial, we’ll learn how to work with Firebase push notifications in the backend and frontend. We’ll set up the notifications system with an Express back-end server. Afterwards, we’ll listen for the notifications in a React front-end app.
description: >-
  In this tutorial, we’ll learn how to work with Firebase push notifications in the backend and frontend. We’ll set up the notifications system with an Express back-end server. Afterwards, we’ll listen for the notifications in a React front-end app.
categories:
  - Tools
  - React
  - Firebase
  - JavaScript
---

Notifications have become a stable part of the web nowadays. It’s not uncommon to come across sites asking for permission to send notifications to your browser. Most modern web browsers implement the [push API](https://www.w3.org/TR/push-api/) and are able to handle push notifications. A quick check on [caniuse](https://caniuse.com/#feat=push-api) shows that the API enjoys wide support among modern chrome-based browsers and Firefox browser.

There are various services for implementing notifications on the web. Notable ones are [Pusher](https://pusher.com/) and [Firebase](https://firebase.google.com/). In this article, we’ll implement push notifications with the Firebase Cloud Messaging (FCM) service, which is “a cross-platform messaging solution that lets you reliably send messages at no cost”.

I assume that the reader has some familiarity with writing a back-end application in Express.js and/or some familiarity with React. If you’re comfortable with either of these technologies, then, you could work with either the frontend or backend. We will implement the backend first, then move on to the frontend. In that way, you can use whichever section appeals more to you.

So let’s get started.

## Types Of Firebase Messages

The Firebase documentation specifies that an FCM implementation requires two components.

1. A trusted environment such as Cloud Functions for Firebase or an app server on which to build, target, and send messages.
2. An iOS, Android, or web (JavaScript) client app that receives messages via the corresponding platform-specific transport service.

We will take care of item 1 in our express back-end app, and item 2 in our react front-end app.

{{% feature-panel %}}

The docs also state that FCM lets us send two types of messages.

1. Notification messages (sometimes thought of as “display messages”) are handled by the FCM SDK automatically.
2. Data messages are handled by the client app.

Notification messages are automatically handled by the browser on the web. They can also take an optional `data` payload, which must be handled by the client app. In this tutorial, we’ll be sending and receiving data messages, which must be handled by the client app. This affords us more freedom in deciding how to handle the received message.

## Setting Up A Firebase Project

The very first thing we need to do is to set up a Firebase project. FCM is a service and as such, we’ll be needing some API keys. This step requires that you have a Google account. Create one if you don’t already have one. You can click [here](https://accounts.google.com/signup/v2/webcreateaccount?hl=en&flowName=GlifWebSignIn&flowEntry=SignUp) to get started.

After setting up your Google account, head on to the [Firebase console](https://console.firebase.google.com/).

Click on **add project**. Enter a *name* for your project and click on **continue**. On the next screen, you may choose to turn off analytics. You can always turn it on later from the Analytics menu of your project page. Click **continue** and wait a few minutes for the project to be created. It’s usually under a minute. Then click on **continue** to open your project page.

Once we’ve successfully set up a project, the next step is to get the necessary keys to work with our project. When working with Firebase, we need to complete a configuration step for the frontend and backend separately. Let’s see how we can obtain the credentials needed to work with both.

### Frontend

On the project page, click on the icon to add Firebase to your web app. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5e48d67-8f3c-40c7-824a-c0af3dd07dd1/01-add-project-to-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5e48d67-8f3c-40c7-824a-c0af3dd07dd1/01-add-project-to-web.png" sizes="100vw" caption="Add Firebase to a web project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5e48d67-8f3c-40c7-824a-c0af3dd07dd1/01-add-project-to-web.png'>Large preview</a>)" alt="Add Firebase to a web project" >}}

Give your app a *nickname*. No need to set up Firebase hosting. Click on **Register** app and give it a few seconds to complete the setup. On the next screen, copy out the app credentials and store them somewhere. You could just leave this window open and come back to it later.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f91f87-03b4-463f-8e5d-45399edd647d/02-firebase-credentials.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f91f87-03b4-463f-8e5d-45399edd647d/02-firebase-credentials.png" sizes="100vw" caption="Firebase web app credentials. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f91f87-03b4-463f-8e5d-45399edd647d/02-firebase-credentials.png'>Large preview</a>)" alt="Firebase web app credentials" >}}

We’ll be needing the configuration object later. Click on continue to console to return to your console.

### Backend

We need a service account credential to connect with our Firebase project from the backend. On your project page, click on the **gear** icon next to Project Overview to create a service account for use with our Express backend. Refer to the below screenshot. Follow steps 1 to 4 to download a `JSON` file with your account credentials. Be sure to keep your service account file in a safe place.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/318242f9-6697-46c6-a1b3-4774ce5403ae/03-create-service-account.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/318242f9-6697-46c6-a1b3-4774ce5403ae/03-create-service-account.png" sizes="100vw" caption="Steps for creating a service account credential. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/318242f9-6697-46c6-a1b3-4774ce5403ae/03-create-service-account.png'>Large preview</a>)" alt="Steps for creating a service account credential" >}}

I’ll advise you not to download it until you’re ready to use it. Just remember to come back to these sections if you need a refresher.

So now we’ve successfully set up a Firebase project and added a web app to it. We’ve also seen how to get the credentials we need to work with both the frontend and backend. Let’s now work on sending push notifications from our express backend.

## Getting Started

To make it easier to work through this tutorial, I’ve set up a project on [Github](https://github.com/chidimo/Fireact) with both a server and a client. Usually, you’ll have a separate repo for your backend and frontend respectively. But I’ve put them together here to make it easier to work through this tutorial.

Create a fork of the repo, clone it to your computer, and let’s get our front-end and back-end servers started.

1. Fork the repo and check out the `01-get-started` branch.
2. Open the project in your code editor of choice and observe the contents.
3. In the project root, we have two folders, `client/` and `server/`. There’s also a `.editorconfig` file, a `.gitignore`, and a `README.md`.
4. The client folder contains a React app. This is where we will listen for notifications.
5. The server folder contains an express app. This is where we’ll send notifications from. The app is from the project we built in my other article [How To Set Up An Express API Backend Project With PostgreSQL](https://www.smashingmagazine.com/2020/04/express-api-backend-project-postgresql/).
6. Open a terminal and navigate to the `client/` folder. Run the `yarn install` command to install the project dependencies. Then run `yarn start` to start the project. Visit `https://localhost:3000` to see the live app.
7. Create a `.env` file inside the `server/` folder and add the `CONNECTION_STRING` environment variable. This variable is a database connection URL pointing to a PostgreSQL database. If you need help with this, check out the **`Connecting The PostgreSQL Database And Writing A Model`** section of my linked article. You should also provide the `PORT` environment variable since React already runs on port `3000`. I set `PORT=3001`  in my `.env` file.
8. Open a separate terminal and navigate to the `server/` folder. Run the `yarn install` command to install the project dependencies. Run `yarn runQuery` to create the project database. Run `yarn startdev` to start the project. Visit https://localhost:3001/v1/messages and you should see some messages in a JSON format.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58b83a7d-b96f-4b81-8c02-da3d5d081e29/04-frontend-and-backend-running.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58b83a7d-b96f-4b81-8c02-da3d5d081e29/04-frontend-and-backend-running.png" sizes="100vw" caption="Frontend and backend servers running. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58b83a7d-b96f-4b81-8c02-da3d5d081e29/04-frontend-and-backend-running.png'>Large preview</a>)" alt="Frontend and backend servers running" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093f4592-2a65-4246-a64c-e5563b62dac3/05-react-app-running.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093f4592-2a65-4246-a64c-e5563b62dac3/05-react-app-running.png" sizes="100vw" caption="React frontend app running. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093f4592-2a65-4246-a64c-e5563b62dac3/05-react-app-running.png'>Large preview</a>)" alt="React frontend app running" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfc73121-ce16-4a72-9600-9a8a08a66a58/06-express-app-running.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfc73121-ce16-4a72-9600-9a8a08a66a58/06-express-app-running.png" sizes="100vw" caption="Express backend app running. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfc73121-ce16-4a72-9600-9a8a08a66a58/06-express-app-running.png'>Large preview</a>)" alt="Express backend app running" >}}

Now that we have our front-end and back-end apps running, let’s implement notifications in the backend.

## Setting Up Firebase Admin Messaging On The Backend

Sending out push notifications with FCM on the backend requires either the [Firebase admin SDK](https://www.npmjs.com/package/firebase-admin) or the [FCM server protocols](https://firebase.google.com/docs/cloud-messaging/server#choose). We’ll be making use of the admin SDK in this tutorial. There’s also the [notifications composer](https://console.firebase.google.com/project/_/notification), which is good for “testing and sending marketing and engagement messages with powerful built-in targeting and analytics”.

In your terminal, navigate to the `server/` folder and install the Admin SDK.

<pre><code class="language-javascript"># install firebase admin SDK
yarn add firebase-admin</code></pre>

Open your `.env` file and add the following environment variable.

<div class="break-out">

<pre><code class="language-javascript">GOOGLE_APPLICATION_CREDENTIALS="path-to-your-service-account-json-file"</code></pre>
</div>

The value of this variable is the path to your downloaded service account credentials. At this point, you probably want to go back to the section where we created the service account for our project. You should copy the admin initialization code from there and also download your service account key file. Place this file in your `server/` folder and add it to your `.gitignore`.

Remember, in an actual project, you should store this file in a very secure location on your server. Don’t let it get into the wrong hands.

Open `server/src/settings.js` and export the application credentials file path.

<div class="break-out">

<pre><code class="language-javascript"># export the service account key file path
export const googleApplicationCredentials = process.env.GOOGLE_APPLICATION_CREDENTIALS;</code></pre>
</div>

Create a file `server/src/firebaseInit.js` and add the below code.

<pre><code class="language-javascript">import admin from 'firebase-admin';

import { googleApplicationCredentials } from './settings'

const serviceAccount = require(googleApplicationCredentials);

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount),
  databaseURL: 'your-database-url-here'
});

export const messaging = admin.messaging();</code></pre>

We import the admin module from `firebase-admin`. We then initialize the admin app with our service account file. Finally, we create and export the messaging feature.

Note that I could have passed the path to my service account key file directly, but it is the less secure option. Always use environment variables when dealing with sensitive information.

To check that you completed the initialization successfully, open up server/src/app.js and include the following lines.

<pre><code class="language-javascript">import { messaging } from './firebaseInit'
console.log(messaging)</code></pre>

We import the messaging instance and log it in the console. You should see something like the picture below. You should remove these once you verify that your admin is set up correctly.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5977c1-0f78-4ee1-8a63-312b840118d4/07-messaging-logged.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5977c1-0f78-4ee1-8a63-312b840118d4/07-messaging-logged.png" sizes="100vw" caption="Console log of messaging feature. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5977c1-0f78-4ee1-8a63-312b840118d4/07-messaging-logged.png'>Large preview</a>)" alt="Console log of messaging feature" >}}

If you run into any problems, you can check out the [02-connect-firebase-admin](https://github.com/chidimo/Fireact/tree/02-connect-firebase-admin) branch of my repo for comparison.

Now that we’ve successfully setup admin messaging, let’s now write the code to send the notifications.

{{% ad-panel-leaderboard %}} 

## Sending Push Notifications From The Backend

FCM data message configuration is very simple. All you have to do is supply one or more target(s) and a `JSON` of the message you wish to send to the client(s). There are no required keys in the `JSON`. You alone decide what key-value pairs you want to include in the data. The data messages form works across all platforms, so our notification could also be processed by mobile devices.

There are additional configurations for other platforms. For example, there’s an `android` settings that only work with android devices and `apns` settings that work on only iOS devices. You can find the configuration guide [here](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification).

Create a file `server/src/notify.js` and enter the below code.

<div class="break-out">

<pre><code class="language-javascript">import { messaging } from './firebaseInit';

export const sendNotificationToClient = (tokens, data) =&gt; {
  // Send a message to the devices corresponding to the provided
  // registration tokens.
  messaging
    .sendMulticast({ tokens, data })
    .then(response => {
      // Response is an object of the form { responses: [] }
      const successes = response.responses.filter(r =&gt; r.success === true)
        .length;
      const failures = response.responses.filter(r =&gt; r.success === false)
        .length;
      console.log(
        'Notifications sent:',
        `${successes} successful, ${failures} failed`
      );
    })
    .catch(error =&gt; {
      console.log('Error sending message:', error);
    });
};</code></pre>
</div>

We created a function that accepts an array of token strings and a data object. Each token string represents a device that has accepted to receive notifications from our back-end application. The notification will be sent to each client in the tokens array. We’ll see how to generate the token in the front-end section of the tutorial.

The messaging instance’s `sendMulticast` method returns a promise. On success, we get an array from which we count the number of successes as well as failed notifications. You could certainly handle this response anyhow you want.

Let’s use this function to send out a notification each time a new message is added to the database.

Open `server/src/controllers/message.js` and update the `addMessage` function.

<div class="break-out">

<pre><code class="language-javascript">import { sendNotificationToClient } from '../notify';

export const addMessage = async (req, res) => {
  const { name, message } = req.body;
  const columns = 'name, message';
  const values = `'${name}', '${message}'`;
  try {
    const data = await messagesModel.insertWithReturn(columns, values);
    const tokens = [];
    const notificationData = {
      title: 'New message',
      body: message,
    };
    sendNotificationToClient(tokens, notificationData);
    res.status(200).json({ messages: data.rows });
  } catch (err) {
    res.status(200).json({ messages: err.stack });
  }
};</code></pre>
</div>
    
This function handles a post request to the `/messages`  endpoint. Once a message is successfully created, a notification is sent out by the `sendNotificationToClient` function followed by the response to the client. The only missing piece in this code is the `tokens` to send the notifications to.

When we connect the client app, we’ll copy the generated token and paste it in this file. In a production app, you’ll store the tokens somewhere in your database.

With this last piece of code, we’ve completed the back-end implementation. Let’s now switch over to the frontend.

The corresponding branch in my repo at this point is [03-send-notification](https://github.com/chidimo/Fireact/tree/03-send-notification).

## Setting Up Firebase Messaging Notifications On The Client

Let’s take a look at the main components of our front-end React app.

Open up `client/src/App.js` and inspect the content. I’ll leave out most of the import statements and just look at the program logic.

<div class="break-out">

<pre><code class="language-javascript"># library imports

import { Messaging } from './Messaging';

axios.defaults.baseURL = 'https://localhost:3001/v1';

const App = () =&gt; {
  return (
    &lt;Fragment&gt;
      &lt;ToastContainer autoClose={2000} position="top-center" /&gt;
      &lt;Navbar bg="primary" variant="dark"&gt;
        &lt;Navbar.Brand href="#home"&gt;Firebase notifictations with React and Express&lt;/Navbar.Brand&gt;
      &lt;/Navbar&gt;
      &lt;Container className="center-column"&gt;
        &lt;Row&gt;
          &lt;Col&gt;
            &lt;Messaging /&gt;
          &lt;/Col&gt;
        &lt;/Row&gt;
      &lt;/Container&gt;
    &lt;/Fragment&gt;
  );
};
export default App;</code></pre>
</div>

This is a regular react component styled with [react-bootstrap](https://react-bootstrap.github.io/). There’s a toast component right at the top of our app, which we shall use to display notifications. Note that we also set the `baseURL` for the `axios` library. Everything of note happens inside the `<Messaging />` component. Let’s now take a look at its content.

Open up `client/src/Messaging.js` and inspect the content.

<pre><code class="language-javascript">export const Messaging = () =&gt; {
  const [messages, setMessages] = React.useState([]);
  const [requesting, setRequesting] = React.useState(false);

  React.useEffect(() =&gt; {
    setRequesting(true);
    axios.get("/messages").then((resp) =&gt; {
      setMessages(resp.data.messages);
      setRequesting(false);
    });
  }, []);

  return (
    &lt;Container&gt;
      {/* form goes here */}
      &lt;div className="message-list"&gt;
        &lt;h3&gt;Messages&lt;/h3&gt;
        {requesting ? (
          &lt;Spinner animation="border" role="status"&gt;
            &lt;span className="sr-only"&gt;Loading...&lt;/span&gt;
          &lt;/Spinner&gt;
        ) : (
          &lt;&gt;
            {messages.map((m, index) =&gt; {
              const { name, message } = m;
              return (
                &lt;div key={index}&gt;
                  {name}: {message}
                &lt;/div&gt;
              );
            })}
          &lt;/&gt;
        )}
      &lt;/div&gt;
    &lt;/Container&gt;
  );
};</code></pre>

We have two state variables, `messages` and `requesting`. `messages` represent the list of messages from our database and `requesting` is for toggling our loader state. We have a `React.useEffect` block where we make our API call to the `/messages` endpoint and set the returned data in our `messages` state.

In the return statement, we map over the messages and display the `name` and `message` fields. On the same page, we include a form for creating new messages.

<div class="break-out">

<pre><code class="language-javascript">&lt;Formik
  initialValues={{
    name: "",
    message: "",
  }}
  onSubmit={(values, actions) =&gt; {
    setTimeout(() =&gt; {
      alert(JSON.stringify(values, null, 2));
      actions.setSubmitting(false);
      toast.success("Submitted succesfully");
    }, 1000);
  }}
&gt;
  {(prop) =&gt; {
    const { handleSubmit, handleChange, isSubmitting } = prop;
    return (
      &lt;&gt;
        &lt;InputGroup className="mb-3"&gt;
          &lt;InputGroup.Prepend&gt;
            &lt;InputGroup.Text id="basic-addon1"&gt;Name&lt;/InputGroup.Text&gt;
          &lt;/InputGroup.Prepend&gt;
          &lt;FormControl
            placeholder="Enter your name"
            onChange={handleChange("name")}
          /&gt;
        &lt;/InputGroup&gt;
        &lt;InputGroup className="mb-3"&gt;
          &lt;InputGroup.Prepend&gt;
            &lt;InputGroup.Text id="basic-addon1"&gt;Message&lt;/InputGroup.Text&gt;
          &lt;/InputGroup.Prepend&gt;
          &lt;FormControl
            onChange={handleChange("message")}
            placeholder="Enter a message"
          /&gt;
        &lt;/InputGroup&gt;
        {isSubmitting ? (
          &lt;Button variant="primary" disabled&gt;
            &lt;Spinner
              as="span"
              size="sm"
              role="status"
              animation="grow"
              aria-hidden="true"
            /&gt;
            Loading...
          &lt;/Button&gt;
        ) : (
          &lt;Button variant="primary" onClick={() =&gt; handleSubmit()}&gt;
            Submit
          &lt;/Button&gt;
        )}
      &lt;/&gt;
    );
  }}
&lt;/Formik&gt;</code></pre>
</div>
  
{{% ad-panel-leaderboard %}} 

We’re using the [`Formik`](https://jaredpalmer.com/formik/docs/overview) library to manage our form. We pass the `<Formik />` component an `initialvalues`  props, an `onSubmit` prop and the form component we want to render. In return, we get back some handy functions such as `handleChange` which we can use to manipulate our form inputs, and `handleSubmit` which we use to submit the form. `isSubmitting` is a `boolean` that we use to toggle the submit button state.

I encourage you to give formik a try. It really simplifies working with forms. We will replace the code in the `onSubmit` method later.

Let’s now implement the method that will request a browser’s permission and assign it a token.

To start using Firebase in the frontend, we have to install the [Firebase JavaScript client](https://www.npmjs.com/package/firebase) library. Note that this is a different package from the `firebase-admin SDK`.

<pre><code class="language-javascript"># install firebase client library
yarn add firebase</code></pre>

Create a file `client/src/firebaseInit.js` and add the following content.

<pre><code class="language-javascript">import firebase from 'firebase/app';
import 'firebase/messaging';

const config = {
  apiKey: "API-KEY",
  authDomain: "AUTH-DOMAIN",
  databaseURL: "DATABASE-URL",
  projectId: "PROJECT-ID",
  storageBucket: "STORAGE-BUCKET",
  messagingSenderId: "MESSAGING-SENDER-ID",
  appId: "APP-ID"
};

firebase.initializeApp(config);
const messaging = firebase.messaging();

// next block of code goes here</code></pre>

The Firebase [docs](https://www.npmjs.com/package/firebase#include-only-the-features-you-need) state that:

<blockquote>“The full Firebase JavaScript client includes support for Firebase Authentication, the Firebase Realtime Database, Firebase Storage, and Firebase Cloud Messaging.”</blockquote>

So here, we import only the messaging feature. At this point, you could refer to the section on creating a Firebase project to get the `config` object. We then initialize Firebase and export the messaging feature. Let’s add in the final block of code.

<pre><code class="language-javascript">export const requestFirebaseNotificationPermission = () =&gt;
  new Promise((resolve, reject) =&gt; {
    messaging
      .requestPermission()
      .then(() => messaging.getToken())
      .then((firebaseToken) =&gt; {
        resolve(firebaseToken);
      })
      .catch((err) =&gt; {
        reject(err);
      });
  });

export const onMessageListener = () =&gt;
  new Promise((resolve) =&gt; {
    messaging.onMessage((payload) =&gt; {
      resolve(payload);
    });
  });</code></pre>

The `requestFirebaseNotificationPermission` function requests the browser’s permission to send notifications and resolves with a token if the request is granted. This is the token that FCM uses to send a notification to the browser. It is what triggers the prompt you see on browsers asking for permission to send a notification.

The `onMessageListener` function is only invoked when the browser is in the foreground. Later, we will write a separate function to handle the notification when the browser is in the background.

Open up `client/src/App.js` and import the `requestFirebaseNotificationPermission` function.

<div class="break-out">

<pre><code class="language-javascript">import { requestFirebaseNotificationPermission } from './firebaseInit'</code></pre>
</div>

Then inside the App function, add the below code before the return statement.

<pre><code class="language-javascript">requestFirebaseNotificationPermission()
  .then((firebaseToken) => {
    // eslint-disable-next-line no-console
    console.log(firebaseToken);
  })
  .catch((err) => {
    return err;
  });</code></pre>

Once the app loads this function runs and requests the browser’s permission to show notifications. If the permission is granted, we log the token. In a production app, you should save the token somewhere that your backend can access. But for this tutorial, we’re just going to copy and paste the token into the back-end app.

Now run your app and you should see the notification request message. Click allow and wait for the token to be logged to the console. Since you’ve granted the browser permission, if we refresh the page you won’t see the banner anymore, but the token will still be logged to the console.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11cd37b3-d457-4fd6-a64a-6b107df50ce1/08-notification-request.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11cd37b3-d457-4fd6-a64a-6b107df50ce1/08-notification-request.png" sizes="100vw" caption="App request to show notifications. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11cd37b3-d457-4fd6-a64a-6b107df50ce1/08-notification-request.png'>Large preview</a>)" alt="App request to show notifications" >}}

You should know that Firefox browser (v75) doesn’t ask for notification permission by default. The permission request has to be triggered by a user-generated action like a click.

This is a good point for me to commit my changes. The corresponding branch is [04-request-permission](https://github.com/chidimo/Fireact/tree/04-request-permission).

Let’s now complete the code for saving a message to our database.

Open up `client/src/Messaging.js` and replace the `onSubmit` function of our form with the below code.

<pre><code class="language-javascript">onSubmit={(values, actions) =&gt; {
  axios
    .post("/messages", values)
    .then((resp) =&gt; {
      setMessages(resp.data.messages.concat(messages));
      actions.setSubmitting(false);
      toast.success("Submitted succesfully");
    })
    .catch((err) =&gt; {
      console.log(err);
      toast.error("There was an error saving the message");
    });
}}</code></pre>

We make a `post` request to the `/messages` endpoint to create a new message. If the request succeeds we take the returned data and put it at the top of the `messages` list. We also display a success toast.

Let’s try it out to see if it works. Start the front-end and back-end servers. Before trying out the post request, open `server/src/controllers/messages.js` and comment out the line where we’re sending the notification.

<div class="break-out">

<pre><code class="language-javascript"># this line will throw an error if tokens is an empty array comment it out temporarily
// sendNotificationToClient(tokens, notificationData);</code></pre>
</div>

Try adding some messages to the database. Works? That’s great. Now uncomment that line before continuing.

Copy the notification token from the developer console and paste it into the tokens array. The token is a very long string, as shown below.

<div class="break-out">

<pre><code class="language-javascript">
    const tokens = [
      'eEa1Yr4Hknqzjxu3P1G3Ox:APA91bF_DF5aSneGdvxXeyL6BIQy8wd1f600oKE100lzqYq2zROn50wuRe9nB-wWryyJeBmiPVutYogKDV2m36PoEbKK9MOpJPyI-UXqMdYiWLEae8MiuXB4mVz9bXD0IwP7bappnLqg',
    ];</code></pre>
</div>

Open `client/src/Messaging.js`, import the `onMessageListener` and invoke it just under the `useEffect` block. Any position within the function is fine as long it’s before the `return` statement.

<pre><code class="language-javascript">import { onMessageListener } from './firebaseInit';

  React.useEffect(() =&gt; {
    ...
  }, []);

  onMessageListener()
    .then((payload) =&gt; {
      const { title, body } = payload.data;
      toast.info(`${title}; ${body}`);
    })
    .catch((err) =&gt; {
      toast.error(JSON.stringify(err));
    });</code></pre>

The listener returns a promise which resolves to the notification payload on success. We then display the title and body in a toast. Note that we could have taken any other action once we receive this notification but I’m keeping things simple here. With both servers running, try it out and see if it’s working.

Works? That’s great.

In case you run into problems, you could always compare with my repo. The corresponding branch at this point is [05-listen-to-notification](https://github.com/chidimo/Fireact/tree/05-listen-to-notification).

There’s just one bit we need to take care of. Right now we can only see notifications when the browser is in the foreground. The point about notifications is that it should pop up whether the browser is in the foreground or not.

If we were to be sending a display message i.e. we included a `notification` object in our notification payload, the browser will take care of that on its own. But since we’re sending a data message, we have to tell the browser how to behave in response to a notification when our browser is in the background.

To handle the background notification we need to register a [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) with our front-end client.

Create a file `client/public/firebase-messaging-sw.js` and enter the following content:

<div class="break-out">

<pre><code class="language-javascript">importScripts('https://www.gstatic.com/firebasejs/7.14.2/firebase-app.js');
importScripts('https://www.gstatic.com/firebasejs/7.14.2/firebase-messaging.js');

const config = {
  apiKey: "API-KEY",
  authDomain: "AUTH-DOMAIN",
  databaseURL: "DATABASE-URL",
  projectId: "PROJECT-ID",
  storageBucket: "STORAGE-BUCKET",
  messagingSenderId: "MESSAGING-SENDER-ID",
  appId: "APP-ID"
};

firebase.initializeApp(config);
const messaging = firebase.messaging();

messaging.setBackgroundMessageHandler(function(payload) {
  console.log('[firebase-messaging-sw.js] Received background message ', payload);
  const notificationTitle = payload.data.title;
  const notificationOptions = {
    body: payload.data.body,
    icon: '/firebase-logo.png'
  };
  return self.registration.showNotification(notificationTitle,
    notificationOptions);
});

self.addEventListener('notificationclick', event =&gt; {
  console.log(event)
  return event;
});</code></pre>
</div>

At the top of the file, we’re importing the `firebase-app` and the `firebase-messaging` libraries since we only need the messaging feature. Don’t worry if the import syntax is new. It’s a syntax for importing external scripts into service worker files. Make sure that the version being imported is the same as the one in your `package.json`. I’ve run into issues that I solved by harmonizing the versions.

As usual, we initialize Firebase, then we invoke the `setBackgroundMessageHandler`, passing it a callback, which receives the notification message payload. The remaining part of the code specifies how the browser should display the notification. Notice that we can also include an icon to display as well.

We can also control what happens when we click on the notification with the `notificationclick` event handler.

Create a file `client/src/serviceWorker.js` and enter the below content.

<pre><code class="language-javascript">export const registerServiceWorker = () =&gt; {
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker
      .register('firebase-messaging-sw.js')
      .then(function (registration) {
        // eslint-disable-next-line no-console
        console.log('[SW]: SCOPE: ', registration.scope);
        return registration.scope;
      })
      .catch(function (err) {
        return err;
      });
  }
};</code></pre>

This function registers our service worker files. Note that we have replaced the more detailed version generated by React. We first check if the `serviceWorker` is present in the `navigator` object. This is simple browser support. If the browser supports service workers, we register the service worker file we created earlier.

Now open `client/src/index.js`, import this function, and invoke it.

<pre><code class="language-javascript"># other imports

import { registerServiceWorker } from './serviceWorker'

ReactDOM.render(
  ...
);

registerServiceWorker()</code></pre>

If all goes well, you should see the service worker's scope logged to your console.

Open https://localhost:3000/messaging in a second browser and create a message. You should see the notification from the other browser come into view.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d30f5f2c-d2a5-4d13-b68f-49d1c7090390/09-types-of-notification.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d30f5f2c-d2a5-4d13-b68f-49d1c7090390/09-types-of-notification.png" sizes="100vw" caption="Background and foreground notifications. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d30f5f2c-d2a5-4d13-b68f-49d1c7090390/09-types-of-notification.png'>Large preview</a>)" alt="Background and foreground notifications" >}}

With that, we’ve come to the end of this tutorial. The corresponding branch in my repo is [06-handle-background-notification](https://github.com/chidimo/Fireact/tree/06-handle-background-notification).

## Conclusion

In this article, we learned about the different types of notification messages we can send with the  Firebase Cloud Messaging (FCM). API. We then implemented the “data message” type on the backend. Finally, we generated a token on the client app which we used to receive notification messages triggered by the back-end app. Finally, we learned how to listen for and display the notification messages when the browser is in either the background or foreground.

I encourage you to take a look at the FCM docs to learn more.

### Related Resources

- [Firebase](https://console.firebase.google.com/), official website
- [Fireact](https://github.com/chidimo/Fireact), Orji Chidi Matthew, GitHub
- “[Firebase: App Success Made Simple](https://www.npmjs.com/package/firebase),” the npm blog
- [Firebase Console](https://console.firebase.google.com/project/_/notification)
- [Firebase Admin Node.js SDK](https://www.npmjs.com/package/firebase-admin), the npm blog
- [WebpushConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#webpushconfig), Firebase Docs
- [`sendMulticast`](https://firebase.google.com/docs/reference/admin/node/admin.messaging.Messaging#sendmulticast), Firebase Docs
- [Service Worker Cookbook](https://serviceworke.rs/), Mozilla
- [Notification](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification), Firebase Docs
- [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/), Firebase Documentation
- “[How To Set Up An Express API Backend Project With PostgreSQL](https://www.smashingmagazine.com/2020/04/express-api-backend-project-postgresql/),” Chidi Orji

{{< signature "ks, ra, yk, il" >}}
