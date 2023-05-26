---
title: 'Integrating A Dialogflow Agent Into A React Application'
slug: dialogflow-agent-react-application
author: nwani-victory
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08526bfc-64de-4913-9333-7da6c7230606/dialogflow-agent-react-application.png
date: 2021-01-14T14:30:13.000Z
summary: >-
  When it comes to building a conversational chat assistant that could be used at a small or enterprise level, Dialogflow would most likely be one of the first options that would show up in your search list &mdash; and why wouldn’t it? It offers several features such as the ability to process audio and text inputs, provide dynamic responses using custom webhooks, connect to millions of Google-enabled devices by using the Google assistant, and so much more. But apart from its [console](https://cloud.google.com/dialogflow/es/docs/console) that is provided to design and manage an Agent, how can we create a chat assistant that can be used within our built web applications, too?
description: >-
  When it comes to building a conversational chat assistant that could be used at a small or enterprise level, Dialogflow would most likely be one of the first options that would show up in your search list. But apart from its console that is provided to design and manage an Agent, how can we create a chat assistant that can be used within our built web applications, too?
categories:
  - Apps
  - React
  - JavaScript
  - Chatbots
---

Dialogflow is a platform that simplifies the process of creating and designing a natural language processing conversational chat assistant which can process voice or text input when being used either from the Dialogflow console or from an integrated web application.

Although the integrated Dialogflow Agent is briefly explained in this article, it is expected that you have an understanding of [Node.js](https://nodejs.org/) and Dialogflow. If you are learning about Dialogflow for the first time, [this article](https://www.smashingmagazine.com/2020/12/conversational-nlp-enabled-chatbot-google-dialogflow/) gives a clear explanation of what [Dialogflow](https://cloud.google.com/dialogflow/docs) is and its concepts.

This article is a guide on how a built a Dialogflow agent with voice and chat support that can be integrated into a web application with the help of an [Express.js](https://expressjs.com/) back-end application as a link between a [React.js](https://reactjs.org/) Web application and the Agent on Dialogflow itself. By the end of the article, you should able to connect your own Dialogflow agent to your preferred web application. 

To make this guide easy to follow through, you can skip to whichever part of the tutorial interests you most or follow them in the following order as they appear:

<ul>
	<li><a href="#setting-up-dialogflow-agent">Setting Up A Dialogflow Agent</a></li>
	<li><a href="#integrating-dialogflow">Integrating A Dialogflow Agent</a></li>
	<li><a href="#setting-up-node-express-app">Setting Up A Node Express Application</a></li>
	<ul>
		<li><a href="#authenticating-dialogflow">Authenticating With Dialogflow</a></li>
		<li><a href="#service-accounts">What Are Service Accounts?</a></li>
		<li><a href="#handling-voice-inputs">Handling Voice Inputs</a></li>
	</ul>
	<li><a href="#integrating-web-app">Integrating Into A Web Application</a></li>
	<ul>
		<li><a href="#creating-chat-interface">Creating A Chat Interface</a></li>
		<li><a href="#recording-user-voice-input">Recording User Voice Input</a></li>
	</ul>
	<li><a href="#conclusion">Conclusion</a></li>
	<li><a href="#references">References</a></li>
</ul>

## 1. Setting Up A Dialogflow Agent

As explained in [this](https://www.smashingmagazine.com/2020/12/conversational-nlp-enabled-chatbot-google-dialogflow/) article, a chat assistant on [Dialogflow](https://cloud.google.com/dialogflow/docs) is called an [Agent](https://cloud.google.com/dialogflow/es/docs/agents-overview) and it comprises of smaller components such as [intents](https://cloud.google.com/dialogflow/es/docs/intents-overview), [fulfillment](https://cloud.google.com/dialogflow/es/docs/fulfillment-overview), [knowledge base](https://cloud.google.com/dialogflow/es/docs/how/knowledge-bases) and much more. Dialogflow provides a [console](https://cloud.google.com/dialogflow/es/docs/console) for users to create, train, and design the conversation flow of an Agent. In our use case, we will restore an agent that was exported into a ZIP folder after being trained, using the agent [Export and Import](https://cloud.google.com/dialogflow/es/docs/agents-settings#export) feature.

Before we perform the import, we need to create a new agent that will be merged with the agent about to be restored. To create a new Agent from the console, a unique name is needed and also, a project on the [Google Cloud](https://cloud.google.com/docs) to link the agent with. If there is no existing project on the Google Cloud to link with, a new one can be created [here](https://console.cloud.google.com/).

An agent has been previously created and trained to recommend wine products to a user based on their budget. This agent has been exported into a ZIP; you can [download the folder here](https://res.cloudinary.com/dkfptto8m/raw/upload/v1608642166/blog/dialogflow-recommender-agent.zip) and restore it into our newly created agent from the [Export and Import](https://cloud.google.com/dialogflow/es/docs/agents-settings#export) tab found in the agent Settings page.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe4910cb-40a7-4232-9b8a-fac7052f728f/dialogflow-agent-restore.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe4910cb-40a7-4232-9b8a-fac7052f728f/dialogflow-agent-restore.png" sizes="100vw" caption="Restoring a previously exported agent from a ZIP folder. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe4910cb-40a7-4232-9b8a-fac7052f728f/dialogflow-agent-restore.png'>Large preview</a>)" alt="Restoring a previously exported agent from a ZIP folder" >}}

The imported agent has been previously trained to recommend a wine product to the user based on the user’s budget for purchasing a bottle of wine. 

Going through the imported agent, we will see it has three created intents from the intents page. One being a fallback intent, used when the Agent does not recognize input from a user, the other is a Welcome intent used when a conversation with the Agent is started, and the last intent is used to recommend a wine to the user based on the amount parameter within the sentence. Of concern to us is the `get-wine-recommendation` intent

This intent has a single input [context](https://cloud.google.com/dialogflow/es/docs/contexts-overview) of `wine-recommendation` coming from the Default Welcome intent to link the conversation to this intent.

<blockquote>“A <a href="https://cloud.google.com/dialogflow/es/docs/contexts-overview">Context</a> is a system within an Agent used to control the flow of a conversation from one intent to the other.”</blockquote>

Below the [contexts](https://cloud.google.com/dialogflow/es/docs/contexts-overview) are the [Training phrases](https://cloud.google.com/dialogflow/es/docs/intents-training-phrases), which are sentences used to train an agent on what type of statements to expect from a user. Through a large variety of training phrases within an intent, an agent is able to recognize a user’s sentence and the intent it falls into.

The training phrases within our agents `get-wine-recommendation` intent (as shown below) indicates the wine choice and the price category:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51a434d-ddad-4d99-9da9-4c6f9eb5223b/training-phrases.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51a434d-ddad-4d99-9da9-4c6f9eb5223b/training-phrases.png" sizes="100vw" caption="Get-wine-recommendation intent page showing the available training phrases. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51a434d-ddad-4d99-9da9-4c6f9eb5223b/training-phrases.png'>Large preview</a>)" alt="List of available training phrases with get-wine-recommendation intent." >}}

Looking at the image above, we can see the available training phrases listed out, and the currency figure is highlighted in yellow color for each of them. This highlighting is known as an annotation on Dialogflow and it is automatically done to extract the recognized data types known as an entity from a user’s sentence. 
 
After this intent has been matched in a conversation with the agent, an HTTP request will be made to an external service to get the recommended wine based on the price extracted as a parameter from a user’s sentence, through the use of the enabled webhook found within the Fulfillment section at the bottom of this intent page. 
 
We can test the agent using the Dialogflow emulator located in the right section of the Dialogflow console. To test, we start the conversation with a “**Hi**” message and follow up with the desired amount of wine. The webhook will immediately be called and a rich response similar to the one below will be shown by the agent.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3baee8fd-6532-4e96-8622-9ed959fe325f/console-emulator-test.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3baee8fd-6532-4e96-8622-9ed959fe325f/console-emulator-test.png" sizes="100vw" caption="Testing the imported agent’s fulfillment webhook using the Agent emulator in the console. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3baee8fd-6532-4e96-8622-9ed959fe325f/console-emulator-test.png'>Large preview</a>)" alt="Testing the imported agent agent webhook." >}}

From the image above we can see the webhook URL generated using [Ngrok](https://ngrok.com/) and the agent’s response on the right-hand side showing a wine within the $20 price range typed in by the user.
 
At this point, the Dialogflow agent has been fully setup. We can now get started with integrating this agent into a web application to enable other users to access and interact with the agent without access to our [Dialogflow console](https://cloud.google.com/dialogflow/es/docs/console).

{{% feature-panel %}}

## Integrating A Dialogflow Agent

While there are other means of connecting to a Dialogflow Agent such as making HTTP requests to its [REST endpoints](https://cloud.google.com/dialogflow/es/docs/reference/rest/v2-overview), the recommended way to connect to Dialogflow is through the use of its official client library available in several programming languages. For JavaScript, the [@google-cloud/dialogflow](https://www.npmjs.com/package/@google-cloud/dialogflow) package is available for installation from [NPM](https://www.npmjs.com/).

Internally the [@google-cloud/dialogflow](https://www.npmjs.com/package/@google-cloud/dialogflow) package uses [gRPC](https://grpc.io/) for its network connections and this makes the package unsupported within a browser environment except when patched using [webpack](https://webpack.js.org/), the recommended way to use this package is from a Node environment. We can do this by setting up an Express.js back-end application to use this package then serve data to the web application through its API endpoints and this is what we will do next. 

## Setting Up A Node Express Application

To set up an express application we create a new project directory then grab the needed dependencies using `yarn` from an opened command line terminal.

<pre><code class="language-bash"># create a new directory and ( && ) move into directory
mkdir dialogflow-server && cd dialogflow-server

# create a new Node project
yarn init -y

# Install needed packages
yarn add express cors dotenv uuid
</code></pre>

With the needed dependencies installed, we can proceed to set up a very lean Express.js server that handles connections on a specified port with CORS support enabled for the web app.

<div class="break-out">

<pre><code class="language-javascript">// index.js
const express =  require("express")
const dotenv =  require("dotenv")
const cors =  require("cors")

dotenv.config();

const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());

app.listen(PORT, () => console.log(`🔥  server running on port ${PORT}`));</code></pre>
</div>

When executed, the code in the snippet above starts an HTTP server that listens for connections on a specified PORT Express.js. It also has [Cross-origin resource sharing](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) (CORS) enabled on all requests using the [cors](https://www.npmjs.com/package/cors) package as an [Express middleware](https://expressjs.com/en/guide/using-middleware.html). For now, this server only listens for connections, it cannot respond to a request because it has no created [route](https://expressjs.com/en/guide/routing.html), so let’s create this.

We now need to add two new routes: one for sending text data while the other for sending a recorded voice input. They will both accept a `POST` request and send the data contained in the request body to the Dialogflow agent later on.

<div class="break-out">

<pre><code class="language-javascript">const express = require("express") 

const app = express()

app.post("/text-input", (req, res) =&gt; {
  res.status(200).send({ data : "TEXT ENDPOINT CONNECTION SUCCESSFUL" })
});

app.post("/voice-input", (req, res) =&gt; {
  res.status(200).send({ data : "VOICE ENDPOINT CONNECTION SUCCESSFUL" })
});

module.exports = app</code></pre>
</div>

Above we created a separate router instance for the two created `POST` routes which for now,  only respond with a `200` status code and a hardcoded dummy response. When we are done authenticating with Dialogflow, we can come back to implement an actual connection to Dialogflow within these endpoints.

For the last step in our backend application setup, we mount the previously created router instance created into the Express application using [app.use](https://expressjs.com/en/api.html#app.use) and a base path for the route.

<div class="break-out">

<pre><code class="language-javascript">// agentRoutes.js

const express =  require("express")
const dotenv =  require("dotenv")
const cors =  require("cors")

const Routes =  require("./routes")

dotenv.config();
const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());

app.use("/api/agent", Routes);

app.listen(PORT, () => console.log(`🔥  server running on port ${PORT}`));
</code></pre>
</div>    

Above, we have added a base path to the two routes two we can test any of them via a `POST` request using [cURL](https://curl.se/) from a command line as it’s done below with an empty request body;

<pre><code class="language-javascript">curl -X https://localhost:5000/api/agent/text-response</code></pre>

After successful completion of the request above, we can expect to see a response containing object data being printed out to the console.

Now we are left with making an actual connection with Dialogflow which includes handling authentication, sending, and receiving data from the Agent on Dialogflow using the [@google-cloud/dialogflow](https://www.npmjs.com/package/@google-cloud/dialogflow) package.  

### Authenticating With Dialogflow

Every Dialogflow agent created is linked to a project on the [Google Cloud](https://cloud.google.com/). To connect externally to the Dialogflow agent, we authenticate with the project on the Google cloud and use Dialogflow as one of the project’s resources. Out of the six [available](https://cloud.google.com/endpoints/docs/openapi/authentication-method) ways to connect to a project on the google-cloud, using the [Service accounts](https://cloud.google.com/endpoints/docs/openapi/authentication-method#service_accounts) option is the most convenient when connecting to a particular service on the google cloud through its client library. 

**Note**: *For production-ready applications, the use of short-lived API keys are recommended over Service Account keys in order to reduce the risk of a service account key getting into the wrong hands.*

### What Are Service Accounts?

[Service accounts](https://cloud.google.com/iam/docs/understanding-service-accounts) are a special type of account on the [Google Cloud](https://cloud.google.com/), created for non-human interaction, mostly through external APIs. In our application, the service account will be accessed through a generated key by the Dialogflow [client library](https://www.npmjs.com/package/@google-cloud/dialogflow) to authenticate with the Google Cloud.

The cloud documentation on creating and managing service accounts provides an excellent [guide](https://cloud.google.com/iam/docs/creating-managing-service-accounts) to create a service account. When creating the service account, the [Dialogflow API Admin](https://cloud.google.com/dialogflow/es/docs/access-control) role should be assigned to the created service account as shown in the last step. This role gives the service account administrative control over the linked Dialogflow agent.

To use the service account, we need to create a [Service Account Key](https://cloud.google.com/iam/docs/creating-managing-service-account-keys). The following steps below outline how to create one in JSON format:

1. Click on the newly created Service Account to navigate to the Service account page.
2. Scroll to the Keys section and click the **Add Key** dropdown and click on the **Create new key** option which opens a modal.
3. Select a [JSON](https://json.org/) file format and click the Create button at the bottom right of the modal.

**Note:** *It is recommended to keep a service account key private and not commit it to any* [*version control system*](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) *as it contains highly sensitive data about a project on the Google Cloud. This can be done by adding the file to the `.gitignore` file.*

With a service account created and a service account key available within our project’s directory, we can use the Dialogflow client library to send and receive data from the Dialogflow agent.

<pre><code class="language-javascript">// agentRoute.js
require("dotenv").config();

const express = require("express")
const Dialogflow = require("@google-cloud/dialogflow")
const { v4 as uuid } = require("uuid")
const Path = require("path")
 
const app = express();

app.post("/text-input", async (req, res) =&gt; {
  const { message } = req.body;

  // Create a new session
   const sessionClient = new Dialogflow.SessionsClient({
    keyFilename: Path.join(__dirname, "./key.json"),
  });

  const sessionPath = sessionClient.projectAgentSessionPath(
    process.env.PROJECT_ID,
    uuid()
  );

  // The dialogflow request object
  const request = {
    session: sessionPath,
    queryInput: {
      text: {
        // The query to send to the dialogflow agent
        text: message,
      },
    },
  };

  // Sends data from the agent as a response
  try {
    const responses = await sessionClient.detectIntent(request);
    res.status(200).send({ data: responses });
  } catch (e) {
    console.log(e);
    res.status(422).send({ e });
  }
});

module.exports = app;
</code></pre>

The entire route above sends data to the Dialogflow agent and receives a response through the following steps.

- **First**  
It authenticates with the Google cloud then it creates a session with Dialogflow using the projectID of Google cloud project linked to the Dialogflow agent and also a random ID to identify the session created. In our application, we are creating a [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) identifier on each session created using the JavaScript [UUID](https://www.npmjs.com/package/uuid) package. This is very useful when logging or tracing all conversations handled by a Dialogflow agent.
- **Second**  
We create a request object data following the specified format in the Dialogflow documentation. This request object contains the created session and the message data gotten from the request body which is to be passed to the Dialogflow agent.
- **Third**  
Using the `detectIntent` method from the Dialogflow session, we send the request object asynchronously and await the Agent’s response using ES6 [async / await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) syntax in a try-catch block should the `detectIntent` method return an exception, we can catch the error and return it, rather than crashing the entire application. A sample of the response object returned from the Agent is provided in the Dialogflow documentation and can be inspected to know how to extract the data from the object. 

We can make use of [Postman](https://web.postman.com/) to test the Dialogflow connection implemented above in the `dialogflow-response` route. [Postman](https://web.postman.com/) is a collaboration platform for API development with features to test APIs built in either development or production stages.

**Note:** *If not already installed, the Postman desktop application is not needed to test an API. Starting from September 2020, Postman’s web client moved into a Generally Available (GA) state and can be used directly from a browser.*  

Using the Postman Web Client, we can either create a new workspace or use an existing one to create a `POST` request to our API endpoint at `https://localhost:5000/api/agent/text-input`  and add data with a key of `message` and value of “**Hi There**” into the query parameters. 

At the click of the **Send** button, a `POST` request will be made to the running Express server &mdash; with a response similar to the one shown in the image below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a04edd9f-11a2-47db-971c-6cda20fa2eb6/postman-test.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a04edd9f-11a2-47db-971c-6cda20fa2eb6/postman-test.png" sizes="100vw" caption="Testing the text-input API endpoint using Postman. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a04edd9f-11a2-47db-971c-6cda20fa2eb6/postman-test.png'>Large preview</a>)" alt="Testing the text-input API endpoint using Postman." >}}

Within the image above, we can see the prettified response data from the Dialogflow agent through the Express server. The data returned is formatted according to the [sample response](https://developers.google.com/assistant/conversational/df-asdk/reference/dialogflow-webhook-json#simple-response-example-df) definition given in the Dialogflow [Webhook documentation](https://developers.google.com/assistant/conversational/df-asdk/reference/dialogflow-webhook-json#simple-response-example-df).

### Handling Voice Inputs

By default, all Dialogflow agents are enabled to process both text and audio data and also return a response in either text or audio format. However, working with audio input or output data can be a bit more complex than text data. 

To handle and process voice inputs, we will begin the implementation for the `/voice-input` endpoint that we have previously created in order to receive audio files and send them to Dialogflow in exchange for a response from the Agent:

<pre><code class="language-javascript">// agentRoutes.js
import { pipeline, Transform } from "stream";
import busboy from "connect-busboy";
import util from "promisfy"
import Dialogflow from "@google-cloud/dialogflow"

const app = express();

app.use(
  busboy({
    immediate: true,
  })
);

app.post("/voice-input", (req, res) =&gt; {
  const sessionClient = new Dialogflow.SessionsClient({
    keyFilename: Path.join(__dirname, "./recommender-key.json"),
  });
  const sessionPath = sessionClient.projectAgentSessionPath(
    process.env.PROJECT_ID,
    uuid()
  );

  // transform into a promise
  const pump = util.promisify(pipeline);

  const audioRequest = {
    session: sessionPath,
    queryInput: {
      audioConfig: {
        audioEncoding: "AUDIO_ENCODING_OGG_OPUS",
        sampleRateHertz: "16000",
        languageCode: "en-US",
      },
      singleUtterance: true,
    },
  };
  
  const streamData = null;
  const detectStream = sessionClient
    .streamingDetectIntent()
    .on("error", (error) =&gt; console.log(error))
    .on("data", (data) =&gt; {
      streamData = data.queryResult    
    })
    .on("end", (data) =&gt; {
      res.status(200).send({ data : streamData.fulfillmentText }}
    }) 
  
  detectStream.write(audioRequest);

  try {
    req.busboy.on("file", (_, file, filename) =&gt; {
      pump(
        file,
        new Transform({
          objectMode: true,
          transform: (obj, _, next) =&gt; {
            next(null, { inputAudio: obj });
          },
        }),
        detectStream
      );
    });
  } catch (e) {
    console.log(`error  : ${e}`);
  }
});
</code></pre>

At a high overview, the `/voice-input` route above receives a user’s voice input as a file containing the message being spoken to the chat assistant and sends it to the Dialogflow agent. To understand this process better, we can break it down into the following smaller steps:

- First, we add and use [connect-busboy](https://www.npmjs.com/package/connect-busboy) as an [Express middleware](https://expressjs.com/en/guide/using-middleware.html) for parsing form data being sent in the request from the web application. After which we authenticate with Dialogflow using the Service Key and create a session, the same way we did in the previous route.  
Then using the [promisify](https://nodejs.org/dist/latest-v8.x/docs/api/util.html) method from the built-in [Node.js](https://nodejs.org/) [util](https://nodejs.org/api/util.html) module, we get and save a promise equivalent of the Stream pipeline method to be used later to pipe multiple streams and also perform a clean up after the streams are completed.
- Next, We create a request object containing the Dialogflow authentication session and a configuration for the audio file about to be sent to Dialogflow. The nested audio configuration object enables the Dialogflow agent to perform a [Speech-To-Text](https://cloud.google.com/speech-to-text) conversion on the sent audio file. 
- Next, using the created session and the request object, we detect a user’s intent from the audio file using `detectStreamingIntent` method which opens up a new data stream from the Dialogflow agent to the backend application. Data will send back in small bits through this stream and using the data “**event**” from the readable stream we store the data in  `streamData` variable for later use. After the stream is closed the “**end**” event is fired and we send the response from the Dialogflow agent stored in the `streamData`  variable to the Web Application.
- Lastly using the file stream event from [connect-busboy](https://www.npmjs.com/package/connect-busboy), we receive the stream of the audio file sent in the request body and we further pass it into the promise equivalent of Pipeline which we created previously. The function of this is to pipe the audio file stream coming in from request to the Dialogflow stream, we pipe the audio file stream to the stream opened by the `detectStreamingIntent` method above.

To test and confirm that the steps above are working as laid out, we can make a test request containing an audio file in the request body to the `/voice-input` endpoint using Postman. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236d6e74-9023-4e43-b379-e1a61f824bc9/testing-voice-input-route.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236d6e74-9023-4e43-b379-e1a61f824bc9/testing-voice-input-route.png" sizes="100vw" caption="Testing the voice-input API endpoint using postman with a recorded voice file. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236d6e74-9023-4e43-b379-e1a61f824bc9/testing-voice-input-route.png'>Large preview</a>)" alt="Testing the voice-input API endpoint using Postman." >}}

The Postman result above shows the response gotten after making a POST request with the form-data of a recorded voice note message saying “**Hi**” included in the request’s body. 

At this point, we now have a functional Express.js application that sends and receives data from Dialogflow, the two parts of this article are done. Where are now left with integrating this Agent into a web application by consuming the APIs created here from a [Reactjs](https://reactjs.org/) application.

{{% ad-panel-leaderboard %}}

## Integrating Into A Web Application

To consume our built REST API we will expand [this](https://wines-list.netlify.app/) existing React.js application which already has a home page showing a list of wines fetched from an API and support for decorators using the [babel proposal decorators plugin](https://babeljs.io/docs/en/babel-plugin-proposal-decorators). We will refactor it a little by introducing [Mobx](https://mobx.js.org/README.html) for state management and also a new feature to recommend a wine from a chat component using the added REST API endpoints from the Express.js application.

To get started, we begin to manage the application’s state using [MobX](https://mobx.js.org/README.html) as we create a Mobx store with a few [observable](https://mobx.js.org/api.html#observablearray) values and some methods as [actions](https://mobx.js.org/api.html#action).

<div class="break-out">

<pre><code class="language-javascript">// store.js

import Axios from "axios";
import { action, observable, makeObservable, configure } from "mobx";

const ENDPOINT = process.env.REACT_APP_DATA_API_URL;

class ApplicationStore {
  constructor() {
    makeObservable(this);
  }

  @observable
  isChatWindowOpen = false;

  @observable
  isLoadingChatMessages = false;

  @observable
  agentMessages = [];

  @action
  setChatWindow = (state) =&gt; {
    this.isChatWindowOpen = state;
  };

  @action
  handleConversation = (message) =&gt; {
     this.isLoadingChatMessages = true;
     this.agentMessages.push({ userMessage: message });

     Axios.post(`${ENDPOINT}/dialogflow-response`, {
      message: message || "Hi",
     })
      .then((res) =&gt; {
        this.agentMessages.push(res.data.data[0].queryResult);
        this.isLoadingChatMessages = false;
      })
      .catch((e) =&gt; {
        this.isLoadingChatMessages = false;
        console.log(e);
      });
  };
}

export const store = new ApplicationStore();</code></pre>
</div>

Above we created a store for the chat component feature within the application having the following values: 

- `isChatWindowOpen`   
The value stored here controls the visibility of the chat component where the messages of Dialogflow are shown.
- `isLoadingChatMessages`  
This is used to show a loading indicator when a request to fetch a response from the Dialogflow agent is made.
- `agentMessages`    
This array stores all responses coming from the requests made to get a response from the Dialogflow agent. The data in the array is later displayed in the component.
- `handleConversation`    
This method decorated as an action adds data into the `agentMessages` array. First, it adds the user’s message passed in as an argument then makes a request using [Axios](https://github.com/axios/axios) to the backend application to get a response from Dialogflow. After the request is resolved, it adds the response from the request into the `agentMessages` array. 

**Note:** *In the absence of the* [*decorators*](https://github.com/tc39/proposal-decorators) *support in an Application, MobX provides* [*makeObservable*](https://mobx.js.org/api.html#makeobservable) *which can be used in the constructor of the target store class. See an example* [*here*](https://mobx.js.org/observable-state.html#makeobservable). 

With the store setup, we need to wrap the entire application tree with the MobX Provider higher-order component starting from the root component in the `index.js` file.

<pre><code class="language-javascript">import React from "react";
import { Provider } from "mobx-react";

import { store } from "./state/";
import Home from "./pages/home";

function App() {
  return (
    &lt;Provider ApplicationStore={store}&gt;
      &lt;div className="App"&gt;
        &lt;Home /&gt;
      &lt;/div&gt;
    &lt;/Provider&gt;
  );
}

export default App;
</code></pre>

Above we wrap the root App component with MobX Provider and we pass in the previously created store as one of the Provider’s values. Now we can proceed to read from the store within components connected to the store.

### Creating A Chat Interface

To display the messages sent or received from the API requests, we need a new component with some chat interface showing the messages listed out. To do this, we create a new component to display some hard-coded messages first then later we display messages in an ordered list.

<pre><code class="language-javascript">// ./chatComponent.js

import React, { useState } from "react";
import { FiSend, FiX } from "react-icons/fi";
import "../styles/chat-window.css";

const center = {
  display: "flex",
  jusitfyContent: "center",
  alignItems: "center",
};

const ChatComponent = (props) =&gt; {
  const { closeChatwindow, isOpen } = props;
  const [Message, setMessage] = useState("");

  return (
   &lt;div className="chat-container"&gt;
      &lt;div className="chat-head"&gt;
        &lt;div style={{ ...center }}&gt;
          &lt;h5&gt; Zara &lt;/h5&gt;
        &lt;/div&gt;
        &lt;div style={{ ...center }} className="hover"&gt;
          &lt;FiX onClick={() =&gt; closeChatwindow()} /&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div className="chat-body"&gt;
        &lt;ul className="chat-window"&gt;
          &lt;li&gt;
            &lt;div className="chat-card"&gt;
              &lt;p&gt;Hi there, welcome to our Agent&lt;/p&gt;
            &lt;/div&gt;
          &lt;/li&gt;
        &lt;/ul&gt;
        &lt;hr style={{ background: "#fff" }} /&gt;
        &lt;form onSubmit={(e) =&gt; {}} className="input-container"&gt;
          &lt;input
            className="input"
            type="text"
            onChange={(e) =&gt; setMessage(e.target.value)}
            value={Message}
            placeholder="Begin a conversation with our agent"
          /&gt;
          &lt;div className="send-btn-ctn"&gt;
            &lt;div className="hover" onClick={() =&gt; {}}&gt;
              &lt;FiSend style={{ transform: "rotate(50deg)" }} /&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/form&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default ChatComponent</code></pre>

The component above has the basic HTML markup needed for a chat application. It has a header showing the Agent’s name and an icon for closing the chat window, a message bubble containing a hardcoded text in a list tag, and lastly an input field having an `onChange` event handler attached to the input field to store the text typed into the component’s local state using React’s [useState](https://reactjs.org/docs/hooks-reference.html#usestate). 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cebbe94-2dea-4de2-8da5-ecc07d8391b0/chat-component-preview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cebbe94-2dea-4de2-8da5-ecc07d8391b0/chat-component-preview.png" sizes="100vw" caption="A preview of the Chat Component with a hard coded message from the chat Agent. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cebbe94-2dea-4de2-8da5-ecc07d8391b0/chat-component-preview.png'>Large preview</a>)" alt="A preview of the Chat Component with a hard coded message from the chat Agent" >}}

From the image above, the chat component works as it should, showing a styled chat window having a single chat message and the input field at the bottom. We however want the message shown to be actual responses gotten from the API request and not hardcoded text.  

We move forward to refactor the Chat component, this time connecting and making use of values in the MobX store within the component.

<div class="break-out">

<pre><code class="language-javascript">// ./components/chatComponent.js

import React, { useState, useEffect } from "react";
import { FiSend, FiX } from "react-icons/fi";
import { observer, inject } from "mobx-react";
import { toJS } from "mobx";
import "../styles/chat-window.css";

const center = {
  display: "flex",
  jusitfyContent: "center",
  alignItems: "center",
};

const ChatComponent = (props) =&gt; {
  const { closeChatwindow, isOpen } = props;
  const [Message, setMessage] = useState("");

  const {
    handleConversation,
    agentMessages,
    isLoadingChatMessages,
  } = props.ApplicationStore;

  useEffect(() =&gt; {
    handleConversation();
    return () =&gt; handleConversation()
  }, []);

  const data = toJS(agentMessages);
 
  return (
        &lt;div className="chat-container"&gt;
          &lt;div className="chat-head"&gt;
            &lt;div style={{ ...center }}&gt;
              &lt;h5&gt; Zara {isLoadingChatMessages && "is typing ..."} &lt;/h5&gt;
            &lt;/div&gt;
            &lt;div style={{ ...center }} className="hover"&gt;
              &lt;FiX onClick={(_) =&gt; closeChatwindow()} /&gt;
            &lt;/div&gt;
          &lt;/div&gt;
          &lt;div className="chat-body"&gt;
            &lt;ul className="chat-window"&gt;
              {data.map(({ fulfillmentText, userMessage }) =&gt; (
                &lt;li&gt;
                  {userMessage && (
                    &lt;div
                      style={{
                        display: "flex",
                        justifyContent: "space-between",
                      }}
                    &gt;
                      &lt;p style={{ opacity: 0 }}&gt; . &lt;/p&gt;
                      &lt;div
                        key={userMessage}
                        style={{
                          background: "red",
                          color: "white",
                        }}
                        className="chat-card"
                      &gt;
                        &lt;p&gt;{userMessage}&lt;/p&gt;
                      &lt;/div&gt;
                    &lt;/div&gt;
                  )}
                  {fulfillmentText && (
                    &lt;div
                      style={{
                        display: "flex",
                        justifyContent: "space-between",
                      }}
                    &gt;
                      &lt;div key={fulfillmentText} className="chat-card"&gt;
                        &lt;p&gt;{fulfillmentText}&lt;/p&gt;
                      &lt;/div&gt;
                      &lt;p style={{ opacity: 0 }}&gt; . &lt;/p&gt;
                    &lt;/div&gt;
                  )}
                &lt;/li&gt;
              ))}
            &lt;/ul&gt;
            &lt;hr style={{ background: "#fff" }} /&gt;
            &lt;form
              onSubmit={(e) =&gt; {
                e.preventDefault();
                handleConversation(Message);
              }}
              className="input-container"
            &gt;
              &lt;input
                className="input"
                type="text"
                onChange={(e) =&gt; setMessage(e.target.value)}
                value={Message}
                placeholder="Begin a conversation with our agent"
              /&gt;
              &lt;div className="send-btn-ctn"&gt;
                &lt;div
                  className="hover"
                  onClick={() =&gt; handleConversation(Message)}
                &gt;
                  &lt;FiSend style={{ transform: "rotate(50deg)" }} /&gt;
                &lt;/div&gt;
              &lt;/div&gt;
            &lt;/form&gt;
          &lt;/div&gt;
        &lt;/div&gt;
     );
};

export default inject("ApplicationStore")(observer(ChatComponent));
</code></pre>
</div>

From the highlighted parts of the code above, we can see that the entire chat component has now been modified to perform the following new operations;

- It has access to the MobX store values after injecting the `ApplicationStore` value. The component has also been made an observer of these store values so it re-renders when one of the values changes.
- We start the conversation with the Agent immediately after the chat component is opened by invoking the `handleConversation` method within a `useEffect` hook to make a request immediately the component is rendered.
- We are now making use of the `isLoadingMessages` value within the Chat component header. When a request to get a response from the Agent is in flight, we set the `isLoadingMessages` value to `true` and update the header to **Zara is typing...**
- The `agentMessages` array within the store gets updated to a proxy by MobX after its values are set. From this component, we convert that proxy back to an array using the `toJS` utility from MobX and store the values in a variable within the component. That array is further iterated upon to populate the chat bubbles with the values within the array using a map function.

Now using the chat component we can type in a sentence and wait for a response to be displayed in the agent.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e3f8f6-e88d-408c-84db-714fddc0dbfb/chat-component-messages.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e3f8f6-e88d-408c-84db-714fddc0dbfb/chat-component-messages.png" sizes="100vw" caption="Chat component showing a list data returned from the HTTP request to the express application. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e3f8f6-e88d-408c-84db-714fddc0dbfb/chat-component-messages.png'>Large preview</a>)" alt="Chat component showing a list data returned from the HTTP request to the express application." >}}

{{% ad-panel-leaderboard %}}

### Recording User Voice Input

By default, all Dialogflow agents can accept either voice or text-based input in any specified language from a user. However, it requires a few adjustments from a web application to gain access to a user’s microphone and record a voice input. 

To achieve this, we modify the MobX store to use the HTML [MediaStream Recording API](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API) to record a user’s voice within two new methods in the MobX store.   

<pre><code class="language-javascript">// store.js

import Axios from "axios";
import { action, observable, makeObservable } from "mobx";

class ApplicationStore {
  constructor() {
    makeObservable(this);
  }

  @observable
  isRecording = false;

  recorder = null;
  recordedBits = [];

  @action
  startAudioConversation = () =&gt; {
    navigator.mediaDevices
      .getUserMedia({
        audio: true,
      })
      .then((stream) =&gt; {
        this.isRecording = true;
        this.recorder = new MediaRecorder(stream);
        this.recorder.start(50);

        this.recorder.ondataavailable = (e) =&gt; {
           this.recordedBits.push(e.data);
        };
      })
      .catch((e) =&gt; console.log(`error recording : ${e}`));
  };
};
</code></pre>

At the click of the record icon from the chat component, the `startAudioConversation` method in the MobX store above is invoked to set the method the observable `isRecording` property is to true , for the chat component to provide visual feedback to show a recording is in progress.

Using the browser’s [navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) interface, the [Media Device](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/mediaDevices) object is accessed to request the user’s device microphone. After permission is granted to the `getUserMedia` request, it resolves its promise with a [MediaStream](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream) data which we further pass to the [MediaRecorder](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder) constructor to create a recorder using the media tracks in the stream returned from the user’s device microphone. We then store the Media recorder instance in the store’s `recorder` property as we will access it from another method later on.

Next, we call the start method on the recorder instance, and after the recording session is ended, the `ondataavailable` function is fired with an event argument containing the recorded stream in a Blob which we store in the `recordedBits` array property.

Logging out the data in the event argument passed into the fired `ondataavailable` event, we can see the Blob and its properties in the browser console.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee10f274-b1cf-4a93-8d71-9a16e949f29a/media-recorder-blob.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee10f274-b1cf-4a93-8d71-9a16e949f29a/media-recorder-blob.png" sizes="100vw" caption="Browser Devtools console showing logged out Blob created by the Media Recorder after a recording is ended. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee10f274-b1cf-4a93-8d71-9a16e949f29a/media-recorder-blob.png'>Large preview</a>)" alt="Browser Devtools console showing logged out Blob created by the Media Recorder after a recording is ended.Pull Quotes" >}}

Now that we can start a MediaRecorder stream, we need to be able to stop the MediaRecorder stream when a user is done recording their voice input and send the generated audio file to the Express.js application.

The new method added to the store below stops the stream and makes a `POST` request containing the recorded voice input.

<div class="break-out">

<pre><code class="language-javascript">//store.js

import Axios from "axios";
import { action, observable, makeObservable, configure } from "mobx";

const ENDPOINT = process.env.REACT_APP_DATA_API_URL;

class ApplicationStore {
  constructor() {
    makeObservable(this);
  }

  @observable
  isRecording = false;

  recorder = null;
  recordedBits = []; 

  @action
  closeStream = () =&gt; {
    this.isRecording = false;
    this.recorder.stop();
    
    this.recorder.onstop = () =&gt; {
      if (this.recorder.state === "inactive") {
        const recordBlob = new Blob(this.recordedBits, {
          type: "audio/mp3",
        });

        const inputFile = new File([recordBlob], "input.mp3", {
          type: "audio/mp3",
        });
        const formData = new FormData();
        formData.append("voiceInput", inputFile);

        Axios.post(`${ENDPOINT}/api/agent/voice-input`, formData, {
          headers: {
            "Content-Type": "multipart/formdata",
          },
        })
          .then((data) =&gt; {})
          .catch((e) =&gt; console.log(`error uploading audio file : ${e}`));
      }
    };
  };
}

export const store = new ApplicationStore();</code></pre>
</div>

The method above executes the MediaRecorder’s stop method to stop an active stream. Within the `onstop` event fired after the MediaRecorder is stopped, we create a new [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) with a music type and append it into a created [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData). 

As the last step., we make `POST` request with the created Blob added to the request body and a `Content-Type: multipart/formdata` added to the request’s headers so the file can be parsed by the connect-busboy middleware from the backend-service application.

With the recording being performed from the MobX store, all we need to add to the chat-component is a button to execute the MobX actions to start and stop the recording of the user’s voice and also a text to show when a recording session is active.

<pre><code class="language-javascript">import React from 'react'

const ChatComponent = ({ ApplicationStore }) =&gt; {
  const {
     startAudiConversation,
     isRecording,
     handleConversation,
     endAudioConversation,
     isLoadingChatMessages
    } = ApplicationStore

  const [ Message, setMessage ] = useState("") 

    return (
        &lt;div&gt;
           &lt;div className="chat-head"&gt;
            &lt;div style={{ ...center }}&gt;
              &lt;h5&gt; Zara {} {isRecording && "is listening ..."} &lt;/h5&gt;
            &lt;/div&gt;
            &lt;div style={{ ...center }} className="hover"&gt;
              &lt;FiX onClick={(_) =&gt; closeChatwindow()} /&gt;
            &lt;/div&gt;
          &lt;/div&gt;          
   
          &lt;form
              onSubmit={(e) =&gt; {
                  e.preventDefault();
                  handleConversation(Message);
                }}
                className="input-container"
              &gt;
                &lt;input
                  className="input"
                  type="text"
                  onChange={(e) =&gt; setMessage(e.target.value)}
                  value={Message}
                  placeholder="Begin a conversation with our agent"
                /&gt;
                &lt;div className="send-btn-ctn"&gt;
                  {Message.length &gt; 0 ? (
                    &lt;div
                      className="hover"
                      onClick={() =&gt; handleConversation(Message)}
                    &gt;
                      &lt;FiSend style={{ transform: "rotate(50deg)" }} /&gt;
                    &lt;/div&gt;
                  ) : (
                    &lt;div
                      className="hover"
                      onClick={() =&gt;  handleAudioInput()}
                    &gt;
                      &lt;FiMic /&gt;
                    &lt;/div&gt;
                  )}
                &lt;/div&gt;
              &lt;/form&gt;
        &lt;/div&gt;     
    )
}

export default ChatComponent</code></pre>

From the highlighted part in the chat component header above, we use the [ES6 ternary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) to switch the text to “**Zara is listening ….**” whenever a voice input is being recorded and sent to the backend application. This gives the user feedback on what is being done.

Also, besides the text input, we added a microphone icon to inform the user of the text and voice input options available when using the chat assistant. If a user decides to use the text input, we switch the microphone button to a Send button by counting the length of the text stored and using a ternary operator to make the switch. 

We can test the newly connected chat assistant a couple of times by using both voice and text inputs and watch it respond exactly like it would when using the Dialogflow console! 

## Conclusion

In the coming years, the use of language processing chat assistants in public services will have become mainstream. This article has provided a basic guide on how one of these chat assistants built with Dialogflow can be integrated into your own web application through the use of a backend application.

The built application has been deployed using [Netlify](https://www.netlify.com/) and can be found [here](https://wine-recommender.netlify.app/). Feel free to explore the Github repository of the backend express application [here](https://github.com/vickywane/dialogflow-article-server) and the React.js web application [here](https://github.com/vickywane/dialogflow-article). They both contain a detailed README to guide you on the files within the two projects.  

### References

- [Dialogflow Documentation](https://cloud.google.com/dialogflow/docs)
- [Building A Conversational N.L.P Enabled Chatbot Using Google’s Dialogflow](https://www.smashingmagazine.com/2020/12/conversational-nlp-enabled-chatbot-google-dialogflow/) by Nwani Victory
- [MobX](https://mobx.js.org/)
- [https://web.postman.com](https://web.postman.com/)
- [Dialogflow API: Node.js Client](https://www.npmjs.com/package/@google-cloud/dialogflow)
- [Using the MediaStream Recording API](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API/Using_the_MediaStream_Recording_API)

{{< signature "ks, vf, yk, il" >}}
