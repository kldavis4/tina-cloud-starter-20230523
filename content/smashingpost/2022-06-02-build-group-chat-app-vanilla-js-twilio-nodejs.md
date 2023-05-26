---
title: 'How To Build A Group Chat App With Vanilla JS, Twilio And Node.js'
slug: build-group-chat-app-vanillajs-twilio-nodejs
author: zara-cooper
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd5325c3-f376-4565-9ce4-a3798d7d33b3/build-group-chat-app-vanillajs-twilio-nodejs.jpg
date: 2022-06-02T09:30:00.000Z
summary: >-
  In this tutorial, you will learn how to create a group chat app. You will build a backend app using Node.js that will make group chats, authorize chat participants, and maintain sessions for them. The front-end will be built using Vanilla JS, HTML and CSS. It will allow users to log in, make new groups, invite friends, and trade messages. By the end, you should have a working app where multiple participants can send messages in one group.
description: >-
  In this tutorial, you will learn how to create a group chat app. You will build a backend app using Node.js that will make group chats, authorize chat participants, and maintain sessions for them.
categories:
  - API
  - Node.js
  - Apps
  - JavaScript
---

Chat is becoming an increasingly popular communication medium in both business and social contexts. Businesses use chat for customer and employee intra-company communication like with [Slack](https://slack.com/), [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software), [Chanty](https://www.chanty.com/), [HubSpot Live Chat](https://www.hubspot.com/products/crm/live-chat), [Help Scout](https://www.helpscout.com/), etc. Most social networks and communication apps also offer chat as an option by default, like on Instagram, Facebook, Reddit, and Twitter. Other apps like Discord, Whatsapp, and Telegram are mostly chat-based, with group chats being one of their main functionalities. 

While there exist numerous products to facilitate chat, you may need a custom-tailored solution for your site that fits your particular communication needs. For example, many of these products are stand-alone apps and may not be able to integrate within your own site. Having your users leave your website to chat may not be the greatest option as it can affect user experience and conversion. On the flip side, building a chat app from scratch can be a daunting and sometimes overwhelming task. However, by using APIs like [Twilio Conversations](https://www.twilio.com/conversations-api) you can simplify the process of creating them. These communication APIs handle group creation, adding participants, sending messages, notifications, among other important chat functions. Backend apps that use these APIs only have to handle authentication and make calls to these APIs. Front-end apps then display conversations, groups, and messages from the backend. 

In this tutorial, you will learn how to create a group chat app using the [Twilio Conversations API](https://www.twilio.com/conversations-api). The front end for this app will be built using HTML, CSS, and Vanilla JavaScript. It will allow users to create group chats, send invites, login, as well as send and receive messages. The backend will be a Node.js app. It will provide authentication tokens for chat invitees and manage chat creation. 

## Prerequisites

Before you can start this tutorial, you need to have the following:

- [Node.js](https://nodejs.org/en/) installed. You’ll use it primarily for the backend app and to install dependencies in the front-end app.  
*You can get it using a pre-built installer available on the [Node.js downloads page](https://nodejs.org/en/download/).*
- A [Twilio](https://www.twilio.com/) account.  
*You can create one [on the Twilio website at this link](https://www.twilio.com/try-twilio).*
- [`http-server`](https://www.npmjs.com/package/http-server) to serve the front-end app.  
*You can install it by running `npm i -g http-server`. You can also run it with `npx http-server` for one-off runs.*
- [MongoDB](https://www.mongodb.com/) for session storage in the backend app.  
*Its [installation page](https://docs.mongodb.com/manual/installation/) has a detailed guide on how to get it running.*

{{% feature-panel %}}

## The Backend App

To send chat messages using Twilio API, you need a **conversation**. Chat messages are sent and received within a conversation. The people sending the messages are called **participants**. A participant can only send a message within a conversation if they are added to it. Both conversations and participants are created using the Twilio API. The backend app will perform this function.

A participant needs an **[access token](https://www.twilio.com/docs/iam/access-tokens#token-anatomy)** to send a message and get their subscribed conversations. The front-end portion of this project will use this access token. The backend app creates the token and sends it to the frontend. There it will be used to load conversations and messages. 

### Project Starter

You’ll call the backend app `twilio-chat-server`. [A scaffolded project starter for it is available on Github](https://github.com/zaracooper/twilio-chat-server). To clone the project and get the starter, run:

<pre><code class="language-bash">git clone https://github.com/zaracooper/twilio-chat-server.git
cd twilio-chat-server
git checkout starter</code></pre>

The backend app takes this structure:

<pre><code class="language-bash">.
├── app.js
├── config/
├── controllers/
├── package.json
├── routes/
└── utils/</code></pre>

To run the app, you’ll use the `node index.js` command. 

### Dependencies

The backend app needs 8 dependencies. You can install them by running:

<pre><code class="language-bash">npm i </code></pre>

Here’s a list of each of the dependencies:

- `connect-mongo` connects to MongoDB, which you’ll use as a session store;
- `cors` handles [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS);
- `dotenv` loads environment variables from the `.env` file that you will create in a later step;
- `express` is the web framework you’ll use for the backend;
- `express-session` provides middleware to handle session data;
- `http-errors` helps create server errors;
- `morgan` handles logging;
- `twilio` creates the Twilio client, generates tokens, creates conversations, and adds participants.

### Configuration

The `config` folder is responsible for loading configuration from environment variables. The configuration is grouped into three categories: configuration for CORS, Twilio, and the MongoDB session DB. When the environment is `development`, you will load `config` from the `.env` file using `dotenv`.

Start by creating the `.env` file on the terminal. This file is already added to the `.gitignore` file to prevent the sensitive values it contains from being checked into the repository.

<pre><code class="language-bash">touch .env</code></pre>

Here’s what your `.env` should look like:

<pre><code class="language-bash"># Session DB Config
SESSION&#95;DB&#95;HOST=XXXX
SESSION&#95;DB&#95;USER=XXXX
SESSION&#95;DB&#95;PASS=XXXX
SESSION&#95;DB&#95;PORT=XXXX
SESSION&#95;DB&#95;NAME=XXXX
SESSION&#95;DB&#95;SECRET=XXXX

# Twilio Config
TWILIO&#95;ACCOUNT&#95;SID=XXXX
TWILIO&#95;AUTH&#95;TOKEN=XXXX
TWILIO&#95;API&#95;KEY=XXXX
TWILIO&#95;API&#95;SECRET=XXXX

# CORS Client Config
CORS&#95;CLIENT&#95;DOMAIN=XXXX</code></pre>

You can [learn how to create a user for your session DB from this MongoDB manual entry](https://docs.mongodb.com/manual/tutorial/create-users/). Once you create a session database and a user who can write to it, you can fill the `SESSION_DB_USER`, `SESSION_DB_PASS`, and `SESSION_DB_NAME` values. If you’re running a local instance of MongoDB, the `SESSION_DB_HOST` would be `localhost`, and the `SESSION_DB_PORT` usually is `27017`. The `SESSION_DB_SECRET` is [used by express-session to sign the session ID cookie](https://github.com/expressjs/session#secret), and it can be any secret string you set. 

In the next step, you will get credentials from the [Twilio Console](https://console.twilio.com). The credentials should be assigned to the variables with the `TWILIO_` prefix. During local development, the front-end client will run on [http://localhost:3000](http://localhost:3000). So, you can use this value for the `CORS_CLIENT_DOMAIN` environment variable.   

Add the following code to [`config/index.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/config/index.js) to load environment variables. 

<pre><code class="language-javascript">import dotenv from 'dotenv';

if (process.env.NODE&#95;ENV == 'development') {
    dotenv.config();
}

const corsClient = {
    domain: process.env.CORS&#95;CLIENT&#95;DOMAIN
};

const sessionDB = {
    host: process.env.SESSION&#95;DB&#95;HOST,
    user: process.env.SESSION&#95;DB&#95;USER,
    pass: process.env.SESSION&#95;DB&#95;PASS,
    port: process.env.SESSION&#95;DB&#95;PORT,
    name: process.env.SESSION&#95;DB&#95;NAME,
    secret: process.env.SESSION&#95;DB&#95;SECRET
};

const twilioConfig = {
    accountSid: process.env.TWILIO&#95;ACCOUNT&#95;SID,
    authToken: process.env.TWILIO&#95;AUTH&#95;TOKEN,
    apiKey: process.env.TWILIO&#95;API&#95;KEY,
    apiSecret: process.env.TWILIO&#95;API&#95;SECRET
};

const port = process.env.PORT || '8000';

export { corsClient, port, sessionDB, twilioConfig };</code></pre>

The environment variables are grouped into categories based on what they do. Each of the configuration categories has its own object variable, and they are all exported for use in other parts of the app.

### Getting Twilio Credentials From the Console

To build this project, you’ll need four different Twilio credentials: an **Account SID**, an **Auth Token**, an **API key**, and an **API secret**. In the console, on the *[General Settings page](https://console.twilio.com/us1/account/manage-account/general-settings)*, scroll down to the **API Credentials** section. This is where you will find your **Account SID** and **Auth Token**. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd939f57-e82b-4fb8-bf3f-fb886754803d/3-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd939f57-e82b-4fb8-bf3f-fb886754803d/3-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="443" sizes="100vw" caption="<strong>API Credentials</strong> section on the <strong>General Settings</strong> page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd939f57-e82b-4fb8-bf3f-fb886754803d/3-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="API Credentials section on the General Settings page" >}}

To get an **API Key** and **Secret**, go to the [**API Keys page**](https://console.twilio.com/us1/account/keys-credentials/api-keys). You can see it in the screenshot below. Click the <kbd>+</kbd> button to go to the **New API Key page**. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a13145-8b87-4f8d-8aa7-77c70ec69634/10-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a13145-8b87-4f8d-8aa7-77c70ec69634/10-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="" sizes="100vw" caption="Create <code>API Key</code> button on API Key list page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a13145-8b87-4f8d-8aa7-77c70ec69634/10-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot where it's shown how to create API key button on API Key list page" >}}

On this page, add a key name and leave the `KEY TYPE` as `Standard`, then click <kbd>Create API Key</kbd>. Copy the API key and secret. You will add all these credentials in a `.env` file as you shall see in subsequent steps.  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca88a2e6-d649-4599-9858-12c7a4f2d749/8-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca88a2e6-d649-4599-9858-12c7a4f2d749/8-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="313" sizes="100vw" caption="<strong>New API Key</strong> page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca88a2e6-d649-4599-9858-12c7a4f2d749/8-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot with the properties on a New API Key page" >}}

### Utils

The backend app needs two utility functions. One will create a token, and the other will wrap async controllers and handle errors for them.

In [`utils/token.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/utils/token.js), add the following code to create a function called `createToken` that will generate Twilio access tokens:

<pre><code class="language-javascript">import { twilioConfig } from '../config/index.js';
import twilio from 'twilio';

function createToken(username, serviceSid) {
    const AccessToken = twilio.jwt.AccessToken;
    const ChatGrant = AccessToken.ChatGrant;

    const token = new AccessToken(
        twilioConfig.accountSid,
        twilioConfig.apiKey,
        twilioConfig.apiSecret,
        { identity: username }
    );

    const chatGrant = new ChatGrant({
        serviceSid: serviceSid,
    });

    token.addGrant(chatGrant);

    return token.toJwt();
}</code></pre>

In this function, you generate [access tokens](https://www.twilio.com/docs/libraries/reference/twilio-node/3.67.0/AccessToken.html) using your **Account SID**, **API key**, and **API secret**. You can optionally supply a unique identity which could be a username, email, etc. After creating a token, you have to add a [chat grant](https://www.twilio.com/docs/libraries/reference/twilio-node/3.67.0/ChatGrant.html) to it. The chat grant can take a conversation service ID among other optional values. Lastly, you’ll convert the token to a [JWT](https://jwt.io/) and return it. 

The [`utils/controller.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/utils/controller.js) file contains an `asyncWrapper` function that wraps async controller functions and catches any errors they throw. Paste the following code into this file:

<div class="break-out">

<pre><code class="language-javascript">function asyncWrapper(controller) {
    return (req, res, next) =&gt; Promise.resolve(controller(req, res, next)).catch(next);
}

export { asyncWrapper, createToken };</code></pre>
</div>

### Controllers

The backend app has four controllers: two for authentication and two for handling conversations. The first auth controller creates a token, and the second deletes it. One of the conversations controllers creates new [conversations](https://www.twilio.com/docs/libraries/reference/twilio-node/3.67.0/Twilio.Conversations.V1.ConversationInstance.html), while the other adds [participants](https://www.twilio.com/docs/libraries/reference/twilio-node/3.67.0/Twilio.Api.V2010.AccountContext.ConferenceContext.ParticipantInstance.html) to existing conversations. 

#### Conversation Controllers

In the [`controllers/conversations.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/controllers/conversations.js) file, add these imports and code for the `StartConversation` controller:

<div class="break-out">

<pre><code class="language-javascript">import { twilioConfig } from '../config/index.js';
import { createToken } from '../utils/token.js';
import twilio from 'twilio';

async function StartConversation(req, res, next) {
    const client = twilio(twilioConfig.accountSid, twilioConfig.authToken);

    const { conversationTitle, username } = req.body;

    try {
        if (conversationTitle && username) {
            const conversation = await client.conversations.conversations
                .create({ friendlyName: conversationTitle });

            req.session.token = createToken(username, conversation.chatServiceSid);
            req.session.username = username;

            const participant = await client.conversations.conversations(conversation.sid)
                .participants.create({ identity: username })

            res.send({ conversation, participant });
        } else {
            next({ message: 'Missing conversation title or username' });
        }
    }
    catch (error) {
        next({ error, message: 'There was a problem creating your conversation' });
    }
}</code></pre>
</div>

The `StartConversation` controller first creates a Twilio `client` using your `twilioConfig.accountSid` and `twilioConfig.authToken` which you get from `config/index.js`. 

Next, it creates a conversation. It needs a conversation title for this, which it gets from the request body. A user has to be added to a conversation before they can participate in it. A participant cannot send a message without an access token. So, it generates an access token using the username provided in the request body and the `conversation.chatServiceSid`. Then the user identified by the username is added to the conversation. The controller completes by responding with the newly created conversation and participant. 

Next, you need to create the `AddParticipant` controller. To do this, add the following code below what you just added in the `controllers/conversations.js` file above:

<div class="break-out">

<pre><code class="language-javascript">async function AddParticipant(req, res, next) {
    const client = twilio(twilioConfig.accountSid, twilioConfig.authToken);

    const { username } = req.body;
    const conversationSid = req.params.id;

    try {
        const conversation = await client.conversations.conversations
            .get(conversationSid).fetch();

        if (username && conversationSid) {
            req.session.token = createToken(username, conversation.chatServiceSid);
            req.session.username = username;

            const participant = await client.conversations.conversations(conversationSid)
                .participants.create({ identity: username })

            res.send({ conversation, participant });
        } else {
            next({ message: 'Missing username or conversation Sid' });
        }
    } catch (error) {
        next({ error, message: 'There was a problem adding a participant' });
    }
}

export { AddParticipant, StartConversation };</code></pre>
</div>

The `AddParticipant` controller adds new participants to already existing conversations. Using the `conversationSid` provided as a route parameter, it fetches the conversation. It then creates a token for the user and adds them to the conversation using their username from the request body. Lastly, it sends the conversation and participant as a response. 

#### Auth Controllers

The two controllers in [`controllers/auth.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/controllers/auth.js) are called `GetToken` and `DeleteToken`. Add them to the file by copying and pasting this code:

<div class="break-out">

<pre><code class="language-javascript">function GetToken(req, res, next) {
    if (req.session.token) {
        res.send({ token: req.session.token, username: req.session.username });
    } else {
        next({ status: 404, message: 'Token not set' });
    }
}

function DeleteToken(req, res, &#95;next) {
    delete req.session.token;
    delete req.session.username;

    res.send({ message: 'Session destroyed' });
}

export { DeleteToken, GetToken };</code></pre>
</div>

The `GetToken` controller retrieves the token and username from the session if they exist and returns them as a response. `DeleteToken` deletes the session.

### Routes

The `routes` folder has three files: `index.js`, `conversations.js`, and `auth.js`.  

Add these auth routes to the [`routes/auth.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/routes/auth.js) file by adding this code:

<div class="break-out">

<pre><code class="language-javascript">import { Router } from 'express';

import { DeleteToken, GetToken } from '../controllers/auth.js';

var router = Router();

router.get('/', GetToken);
router.delete('/', DeleteToken);

export default router;</code></pre>
</div>

The `GET` route at the `/` path returns a token while the `DELETE` route deletes a token.

Next, copy and paste the following code to the [`routes/conversations.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/routes/conversations.js) file:

<div class="break-out">

<pre><code class="language-javascript">import { Router } from 'express';
import { AddParticipant, StartConversation } from '../controllers/conversations.js';
import { asyncWrapper } from '../utils/controller.js';

var router = Router();

router.post('/', asyncWrapper(StartConversation));
router.post('/:id/participants', asyncWrapper(AddParticipant));

export default router;</code></pre>
</div>

In this file, the conversations router is created. A `POST` route for creating conversations with the path `/` and another `POST` route for adding participants with the path `/:id/participants` are added to the router. 

Lastly, add the following code to your new [`routes/index.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/routes/index.js) file. 

<pre><code class="language-javascript">import { Router } from 'express';

import authRouter from './auth.js';
import conversationRouter from './conversations.js';

var router = Router();

router.use('/auth/token', authRouter);
router.use('/api/conversations', conversationRouter);

export default router;</code></pre>

By adding the `conversation` and `auth` routers here, you are making them available at `/api/conversations` and `/auth/token` to the main router respectively. The router is then exported. 

### The Backend App

Now it’s time to put the backend pieces together. Open the [`index.js`](https://github.com/zaracooper/twilio-chat-server/blob/main/index.js) file in your text editor and paste in the following code:

<div class="break-out">

<pre><code class="language-javascript">import cors from 'cors';
import createError from 'http-errors';
import express, { json, urlencoded } from 'express';
import logger from 'morgan';
import session from 'express-session';
import store from 'connect-mongo';

import { corsClient, port, sessionDB } from './config/index.js';

import router from './routes/index.js';

var app = express();

app.use(logger('dev'));
app.use(json());
app.use(urlencoded({ extended: false }));

app.use(cors({
    origin: corsClient.domain,
    credentials: true,
    methods: ['GET', 'POST', 'DELETE'],
    maxAge: 3600 &#42; 1000,
    allowedHeaders: ['Content-Type', 'Range'],
    exposedHeaders: ['Accept-Ranges', 'Content-Encoding', 'Content-Length', 'Content-Range']
}));
app.options('&#42;', cors());

app.use(session({
    store: store.create({
        mongoUrl: `mongodb://${sessionDB.user}:${sessionDB.pass}@${sessionDB.host}:${sessionDB.port}/${sessionDB.name}`,
        mongoOptions: { useUnifiedTopology: true },
        collectionName: 'sessions'
    }),
    secret: sessionDB.secret,
    cookie: {
        maxAge: 3600 &#42; 1000,
        sameSite: 'strict'
    },
    name: 'twilio.sid',
    resave: false,
    saveUninitialized: true
}));

app.use('/', router);

app.use(function (&#95;req, &#95;res, next) {
    next(createError(404, 'Route does not exist.'));
});

app.use(function (err, &#95;req, res, &#95;next) {
    res.status(err.status || 500).send(err);
});

app.listen(port);</code></pre>
</div>

This file starts off by creating the express app. It then sets up JSON and URL-encoded payload parsing and adds the logging middleware. Next, it sets up CORS and the session handling. As mentioned earlier, MongoDB is used as the session store.

After all that is set up, it then adds the router created in the earlier step before configuring error handling. Lastly, it makes the app listen to and accept connections at the port specified in the `.env` file. If you haven’t set the port, the app will listen on port `8000`.

Once you’re finished creating the backend app, make sure MongoDB is running and start it by running this command on the terminal:

<pre><code class="language-bash">NODE&#95;ENV=development npm start</code></pre>

You pass the `NODE_ENV=development` variable, so that configuration is loaded from the local `.env` file. 

{{% ad-panel-leaderboard %}}

## The Front-end

The front-end portion of this project serves a couple of functions. It allows users to create conversations, see the list of conversations they are a part of, invite others to conversations they created, and send messages within conversations. These roles are achieved by four pages: 

- a **conversations** page,
- a **chat** page,
- an **error** page,
- a **login** page.

You’ll call the front-end app `twilio-chat-app`. [A scaffolded starter exists for it on Github](https://github.com/zaracooper/twilio-vanilla-js-chat-app). To clone the project and get the starter, run:

<div class="break-out">

<pre><code class="language-bash">git clone https://github.com/zaracooper/twilio-vanilla-js-chat-app.git
cd twilio-vanilla-js-chat-app
git checkout starter</code></pre>
</div>

The app takes this structure:

<pre><code class="language-bash">.
├── index.html
├── pages
│   ├── chat.html
│   ├── conversation.html
│   ├── error.html
│   └── login.html
├── scripts
│   ├── chat.js
│   ├── conversation.js
│   └── login.js
└── styles
    ├── chat.css
    ├── main.css
    └── simple-page.css
</code></pre>

The styling and HTML markup have already been added for each of the pages in the starter. This section will only cover the scripts you have to add. 

### Dependencies

The app has two dependencies: [`axios`](https://www.npmjs.com/package/axios) and [`@twilio/conversations`](http://media.twiliocdn.com/sdk/js/conversations/releases/1.2.3/docs/index.html). You’ll use `axios` to make requests to the backend app and `@twilio/conversations` to send and fetch messages and conversations in scripts. You can install them on the terminal by running: 

<pre><code class="language-bash">npm i</code></pre>

### The Index Page

This page serves as a landing page for the app. You can [find the markup for this page (`index.html`) here](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/index.html). It uses two CSS stylesheets: [`styles/main.css`](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/styles/main.css) which all pages use and [`styles/simple-page.css`](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/styles/simple-page.css) which smaller, less complicated pages use.

You can find the contents of these stylesheets linked in the earlier paragraph. Here is a screenshot of what this page will look like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a602139c-a8fa-411b-a9bb-2e5cb3c8b09a/4-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a602139c-a8fa-411b-a9bb-2e5cb3c8b09a/4-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="437" sizes="100vw" caption="Twilio Vanilla JS Chat App's Landing Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a602139c-a8fa-411b-a9bb-2e5cb3c8b09a/4-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="Twilio Vanilla JS Chat App Landing Page" >}}

### The Error Page

This page is shown when an error occurs. [The contents of `pages/error.html` can be found here.](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/pages/error.html) If an error occurs, a user can click the button to go to the home page. There, they can try what they were attempting again. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2598a3-bfaa-4e29-8477-0aa7c472e935/5-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2598a3-bfaa-4e29-8477-0aa7c472e935/5-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="435" sizes="100vw" caption="Twilio Vanilla JS Chat App's Error Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2598a3-bfaa-4e29-8477-0aa7c472e935/5-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="Twilio Vanilla JS Chat App Error Page" >}}

### The Conversations Page

On this page, a user provides the title of a conversation to be created and their username to a form. 

[The contents of `pages/conversation.html` can be found here.](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/pages/conversation.html) Add the following code to the `scripts/conversation.js` file:

<pre><code class="language-javascript">window.twilioChat = window.twilioChat || {};

function createConversation() {
    let convoForm = document.getElementById('convoForm');
    let formData = new FormData(convoForm);

    let body = Object.fromEntries(formData.entries()) || {};

    let submitBtn = document.getElementById('submitConvo');
    submitBtn.innerText = "Creating..."
    submitBtn.disabled = true;
    submitBtn.style.cursor = 'wait';

    axios.request({
        url: '/api/conversations',
        baseURL: 'http://localhost:8000',
        method: 'post',
        withCredentials: true,
        data: body
    })
        .then(() =&gt; {
            window.twilioChat.username = body.username;
            location.href = '/pages/chat.html';
        })
        .catch(() =&gt; {
            location.href = '/pages/error.html';
        });
}</code></pre>

When a user clicks the <kbd>Submit</kbd> button, the `createConversation` function is called. In it, the contents of the form are collected and used in the body of a `POST` request made to `http://localhost:8000/api/conversations/` in the backend. 

You will use `axios` to make the request. If the request is successful, a conversation is created and the user is added to it. The user will then be redirected to the chat page where they can send messages in the conversation. 

Below is a screenshot of the conversations page:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28017a81-6a1c-4a01-a673-87ce848045e1/7-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28017a81-6a1c-4a01-a673-87ce848045e1/7-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="436" sizes="100vw" caption="Twilio Vanilla JS Chat App's Conversation Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28017a81-6a1c-4a01-a673-87ce848045e1/7-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="Twilio Vanilla JS Chat App Conversation Page" >}}

### The Chat Page

On this page, a user will view a list of conversations they are part of and send messages to them. You can find [the markup for `pages/chat.html` here](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/pages/chat.html) and [the styling for `styles/chat.css` here](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/styles/chat.css). 

The `scripts/chat.js` file starts out by defining a namespace `twilioDemo`. 

<pre><code class="language-javascript">window.twilioChat = window.twilioChat || {};</code></pre>

Add the `initClient` function below. It is responsible for initializing the Twilio client and loading conversations.

<div class="break-out">

<pre><code class="language-javascript">async function initClient() {
    try {
        const response = await axios.request({
            url: '/auth/token',
            baseURL: 'http://localhost:8000',
            method: 'GETget',
            withCredentials: true
        });

        window.twilioChat.username = response.data.username;
        window.twilioChat.client = await Twilio.Conversations.Client.create(response.data.token);

        let conversations = await window.twilioChat.client.getSubscribedConversations();

        let conversationCont, conversationName;

        const sideNav = document.getElementById('side-nav');
        sideNav.removeChild(document.getElementById('loading-msg'));

        for (let conv of conversations.items) {
            conversationCont = document.createElement('button');
            conversationCont.classList.add('conversation');
            conversationCont.id = conv.sid;
            conversationCont.value = conv.sid;
            conversationCont.onclick = async () =&gt; {
                await setConversation(conv.sid, conv.channelState.friendlyName);
            };

            conversationName = document.createElement('h3');
            conversationName.innerText = `💬 ${conv.channelState.friendlyName}`;

            conversationCont.appendChild(conversationName);
            sideNav.appendChild(conversationCont);
        }
    }
    catch {
        location.href = '/pages/error.html';
    }
};</code></pre>
</div>

When the page loads, `initClient` fetches the user’s access token from the backend, then uses it to initialise the client. Once the client is initialised, it’s used to fetch all the conversations the user is subscribed to. After that, the conversations are loaded onto the `side-nav`. In case any error occurs, the user is sent to the error page.

The `setConversion` function loads a single conversation. Copy and paste the code below in the file to add it:

<div class="break-out">

<pre><code class="language-javascript">async function setConversation(sid, name) {
    try {
        window.twilioChat.selectedConvSid = sid;

        document.getElementById('chat-title').innerText = '+ ' + name;

        document.getElementById('loading-chat').style.display = 'flex';
        document.getElementById('messages').style.display = 'none';

        let submitButton = document.getElementById('submitMessage')
        submitButton.disabled = true;

        let inviteButton = document.getElementById('invite-button')
        inviteButton.disabled = true;

        window.twilioChat.selectedConversation = await window.twilioChat.client.getConversationBySid(window.twilioChat.selectedConvSid);

        const messages = await window.twilioChat.selectedConversation.getMessages();

        addMessagesToChatArea(messages.items, true);

        window.twilioChat.selectedConversation.on('messageAdded', msg =&gt; addMessagesToChatArea([msg], false));

        submitButton.disabled = false;
        inviteButton.disabled = false;
    } catch {
        showError('loading the conversation you selected');
    }
};</code></pre>
</div>

When a user clicks on a particular conversation, `setConversation` is called. This function receives the **conversation SID** and **name** and uses the **SID** to fetch the conversation and its messages. The messages are then added to the chat area. Lastly, a listener is added to watch for new messages added to the conversation. These new messages are appended to the chat area when they are received. In case any errors occur, an error message is displayed.

This is a screenshot of the chat page:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74fcb0d9-ee52-484d-9e2d-3d585cb2cd8f/6-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74fcb0d9-ee52-484d-9e2d-3d585cb2cd8f/6-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="470" sizes="100vw" caption="Twilio Vanilla JS Chat App's Chat Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74fcb0d9-ee52-484d-9e2d-3d585cb2cd8f/6-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot of the chat page" >}}

Next, you’ll add the `addMessagedToChatArea` function which loads conversation messages.

<pre><code class="language-javascript">function addMessagesToChatArea(messages, clearMessages) {
    let cont, msgCont, msgAuthor, timestamp;

    const chatArea = document.getElementById('messages');

    if (clearMessages) {
        document.getElementById('loading-chat').style.display = 'none';
        chatArea.style.display = 'flex';
        chatArea.replaceChildren();
    }

    for (const msg of messages) {
        cont = document.createElement('div');
        if (msg.state.author == window.twilioChat.username) {
            cont.classList.add('right-message');
        } else {
            cont.classList.add('left-message');
        }

        msgCont = document.createElement('div');
        msgCont.classList.add('message');

        msgAuthor = document.createElement('p');
        msgAuthor.classList.add('username');
        msgAuthor.innerText = msg.state.author;

        timestamp = document.createElement('p');
        timestamp.classList.add('timestamp');
        timestamp.innerText = msg.state.timestamp;

        msgCont.appendChild(msgAuthor);
        msgCont.innerText += msg.state.body;

        cont.appendChild(msgCont);
        cont.appendChild(timestamp);

        chatArea.appendChild(cont);
    }

    chatArea.scrollTop = chatArea.scrollHeight;
}</code></pre>

The function `addMessagesToChatArea` adds messages of the current conversation to the chat area when it is selected from the side nav. It is also called when new messages are added to the current conversation. A loading message is usually displayed as the messages are being fetched. Before the conversation messages are added, this loading message is removed. Messages from the current user are aligned to the right, while all other messages from group participants are aligned to the left.

This is what the loading message looks like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9e6b5d4-bb08-4568-b233-73bbd5cc589c/9-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9e6b5d4-bb08-4568-b233-73bbd5cc589c/9-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="470" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9e6b5d4-bb08-4568-b233-73bbd5cc589c/9-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot with the 'loading messages' displayed in the middle" >}}

Add the `sendMessage` function to send messages:

<div class="break-out">

<pre><code class="language-javascript">function sendMessage() {
    let submitBtn = document.getElementById('submitMessage');
    submitBtn.disabled = true;

    let messageForm = document.getElementById('message-input');
    let messageData = new FormData(messageForm);

    const msg = messageData.get('chat-message');

    window.twilioChat.selectedConversation.sendMessage(msg)
        .then(() =&gt; {
            document.getElementById('chat-message').value = '';
            submitBtn.disabled = false;
        })
        .catch(() =&gt; {
            showError('sending your message');
            submitBtn.disabled = false;
        });
};</code></pre>
</div>

When the user sends a message, the `sendMessage` function is called. It gets the message text from the text area and disables the <kbd>submit</kbd> button. Then using the currently selected conversation, the message is sent using its `sendMessage` method. If successful, the text area is cleared and the <kbd>submit</kbd> button is re-enabled. If unsuccessful, an error message is displayed instead. 

The `showError` method displays an error message when it is called; `hideError` hides it.

<div class="break-out">

<pre><code class="language-javascript">function showError(msg) {
    document.getElementById('error-message').style.display = 'flex';
    document.getElementById('error-text').innerText = `There was a problem ${msg ? msg : 'fulfilling your request'}.`;
}

function hideError() {
    document.getElementById('error-message').style.display = 'none';
}</code></pre>
</div>

This is what this error message will look like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be1c9ad3-22cc-49a9-a710-b8e87ad624cc/1-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be1c9ad3-22cc-49a9-a710-b8e87ad624cc/1-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="471" sizes="100vw" caption="Twilio Vanilla JS Chat App's Error Message. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be1c9ad3-22cc-49a9-a710-b8e87ad624cc/1-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot with the error message banner on top" >}}

The `logout` function logouts out the current user. It does this by making a request to the backend which clears their session. The user is then redirected to the conversation page, so they can create a new conversation if they’d like.

<pre><code class="language-javascript">function logout(logoutButton) {
    logoutButton.disabled = true;
    logoutButton.style.cursor = 'wait';

    axios.request({
        url: '/auth/token',
        baseURL: 'http://localhost:8000',
        method: 'DELETEdelete',
        withCredentials: true
    })
        .then(() =&gt; {
            location.href = '/pages/conversation.html';
        })
        .catch(() =&gt; {
            location.href = '/pages/error.html';
        });
}</code></pre>

Add the `inviteFriend` function to send conversation invites:

<div class="break-out">

<pre><code class="language-javascript">async function inviteFriend() {
    try {
        const link = `http://localhost:3000/pages/login.html?sid=${window.twilioChat.selectedConvSid}`;

        await navigator.clipboard.writeText(link);

        alert(`The link below has been copied to your clipboard.\n\n${link}\n\nYou can invite a friend to chat by sending it to them.`);
    } catch {
        showError('preparing your chat invite');
    }
}</code></pre>
</div>

To invite other people to participate in the conversation, the current user can send another person a link. This link is to the login page and contains the current **conversation SID** as a query parameter. When they click the <kbd>invite</kbd> button, the link is added to their clipboard. An alert is then displayed giving invite instructions. 

Here is a screenshot of the invite alert:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/715f67fa-ee72-4110-b712-9882693e27a6/11-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/715f67fa-ee72-4110-b712-9882693e27a6/11-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="470" sizes="100vw" caption="Twilio Vanilla JS Chat App's Invite Alert. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/715f67fa-ee72-4110-b712-9882693e27a6/11-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot of the invite alert" >}}

### The Login Page

On this page, a user logs in when they are invited to a conversation. You can [find the markup for `pages/login.html` at this link](https://github.com/zaracooper/twilio-vanilla-js-chat-app/blob/main/pages/login.html). 

In `scripts/login.js`, the `login` function is responsible for logging in conversation invitees. Copy its code below and add it to the aforementioned file:

<div class="break-out">

<pre><code class="language-javascript">function login() {
    const convParams = new URLSearchParams(window.location.search);
    const conv = Object.fromEntries(convParams.entries());

    if (conv.sid) {
        let submitBtn = document.getElementById('login-button');
        submitBtn.innerText = 'Logging in...';
        submitBtn.disabled = true;
        submitBtn.style.cursor = 'wait';

        let loginForm = document.getElementById('loginForm');
        let formData = new FormData(loginForm);
        let body = Object.fromEntries(formData.entries());
        
        axios.request({
            url: `/api/conversations/${conv.sid}/participants`,
            baseURL: 'http://localhost:8000',
            method: 'POSTpost',
            withCredentials: true,
            data: body
        })
            .then(() =&gt; {
                location.href = '/pages/chat.html';
            })
            .catch(() =&gt; {
                location.href = '/pages/error.html';
            });
    } else {
        location.href = '/pages/conversation.html';
    }
}</code></pre>
</div>

The `login` function takes the conversation `sid` query parameter from the URL and the username from the form. It then makes a `POST` request to `api/conversations/{sid}/participants/` on the backend app. The backend app adds the user to the conversation and generates an access token for messaging. If successful, a session is started in the backend for the user. 

The user is then redirected to the *chat page*, but if the request returns an error, they are redirected to the *error page*. If there is no conversation `sid` query parameter in the URL, the user is redirected to the *conversation page*. 

Below is a screenshot of the login page:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a6d21-3f40-4e3d-a4b2-0f2485d194fb/2-build-group-chat-app-vanilla-js-twilio-nodejs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a6d21-3f40-4e3d-a4b2-0f2485d194fb/2-build-group-chat-app-vanilla-js-twilio-nodejs.png" width="800" height="437" sizes="100vw" caption="Twilio Vanilla JS Chat App's Login Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a6d21-3f40-4e3d-a4b2-0f2485d194fb/2-build-group-chat-app-vanilla-js-twilio-nodejs.png'>Large preview</a>)" alt="A screenshot of the login page" >}}

### Running the App

Before you can start the front-end app, make sure that the backend app is running. As mentioned earlier, you can start the backend app using this command on the terminal:

<pre><code class="language-bash">NODE&#95;ENV=development npm start</code></pre>

To serve the front-end app, run this command in a different terminal window:

<pre><code class="language-bash">http-server -p 3000</code></pre>

This serves the app at [http://localhost:3000](http://localhost:3000). Once it’s running, head on over to [http://localhost:3000/pages/conversation.html](http://localhost:3000/pages/conversation.html); set a name for your conversation and add your username, then create it. When you get to the *chat page*, click on the `conversation`, then click the <kbd>Invite</kbd> button. 

In a separate incognito window, paste the invite link and put a different username. Once you’re on the chat page in the incognito window, you can begin chatting with yourself. You can send messages back and forth between the user in the first window and the second user in the incognito window in the same conversation. 

{{< youtube id="bnnNBrGaSYs" breakout="true" caption="A video demonstration of the app." >}}

{{% ad-panel-leaderboard %}}

## Conclusion

In this tutorial, you learned how to create a chat app using Twilio Conversations and Vanilla JS. You created a Node.js app that generates user access tokens, maintains a session for them, creates conversations, and adds users to them as participants. You also created a front-end app using HTML, CSS, and Vanilla JS. This app should allow users to create conversations, send messages, and invite other people to chat. It should get access tokens from the backend app and use them to perform these functions. I hope this tutorial gave you a better understanding of how Twilio Conversations works and how to use it for chat messaging.

*To find out more about Twilio Conversations and what else you could do with it, [check out its documentation linked here](https://www.twilio.com/conversations-api). You can also find the [source code for the backend app on Github here](https://github.com/zaracooper/twilio-chat-server), and the [code for the front-end app here](https://github.com/zaracooper/twilio-vanilla-js-chat-app).*

{{< signature "yk, il">}}
