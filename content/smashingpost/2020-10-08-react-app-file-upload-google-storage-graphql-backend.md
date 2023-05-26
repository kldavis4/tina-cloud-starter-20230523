---
title: 'How To Manage File Uploads In React With Google Storage And GraphQL'
slug: file-uploads-react-apollo-google-storage-graphql
author: nwani-victory
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcb82c7-1908-45af-888d-0613e4baef09/file-uploads-react-apollo-google-storage-graphql.png
date: 2020-10-08T10:00:00.000Z
summary: >-
  From a user’s profile picture to other media assets, data collection and storage to cloud services through file uploads have become an essential feature for most modern applications. In this article, you will learn how file uploads can be implemented in a GraphQL application.
description: >-
  From a user’s profile picture to other media assets, data collection and storage to cloud services through file uploads have become an essential feature for most modern applications. In this article, you will learn how file uploads can be implemented in a GraphQL application.
categories:
  - React
  - GraphQL
  - Forms
  - Tools
---

By leveraging [React-Apollo](https://www.apollographql.com/docs/react/), this article focuses on how a file upload functionality  can be added to a new or existing front-end application being powered by a GraphQL API. To achieve this, we would build [this demo application](https://graphql-upload.netlify.app/) which allows users to upload a profile image when creating an account alongside their preferred username. While we do this, we would gradually work through the process of : 

- Creating a Node GraphQL backend application capable of accepting and sending the uploaded file to a Storage Bucket within the Google Cloud. 
- Setting up a connection to the Google Cloud Storage.
- Collecting files inputs in a React Application and sending them to a GraphQL backend application using React Apollo.

**Note**: *Although all code snippets are explained, to fully understand them you should have an understanding of [JavaScript's es6 syntax,](https://es6-features.org/) [GraphQL](https://graphql.org/learn/) and [React.js](https://reactjs.org/).*

This article will be beneficial to developers who are interested in or considering using Google Cloud Storage for file uploads in their React and Nodejs GraphQL application. While this article is not an [introduction to GraphQL](https://www.smashingmagazine.com/2020/07/client-side-graphql-apollo-client-react-apps/), each GraphQL concept used within this article is explained and referenced for better understanding.

## Setting Up A Node GraphQL API

We will be building a GraphQL API to be consumed by our React application. This backend application will receive the image uploaded by a user and send the uploaded file to Google Cloud Storage. 

To begin, we use the [Apollo-Server-express](https://www.npmjs.com/package/apollo-server-express) and [Express.js](https://www.npmjs.com/package/express) library to quickly bootstrap a GraphQL API. We can do this by running the following commands :
     

<pre><code class="language-bash"># Create a new Project folder and( && ) move into it
mkdir Node-GraphQL-API && cd Node-GraphQL-API

# Create a new Node project
yarn init -y

# Install the two needed dependencies 
yarn add apollo-server-express express
</code></pre>

Next, we proceed to build a single GraphQL endpoint, which is accessible via port `4000`.

<div class="break-out">

 <pre><code class="language-javascript">const express = require('express')
const { ApolloServer } = require('apollo-server-express')

const { Queries , Mutations , TypeDefs } = require('./resolvers') 

const resolvers = {
  Query : Queries , 
  Mutation : Mutations 
} 

const server = new ApolloServer({ TypeDefs, resolvers });
 
const app = express();
server.applyMiddleware({ app });
 
app.listen({ port: 4000 }, () =>
  console.log(`Graphiql running at https://localhost:4000/${server.graphqlPath}`));
</code></pre>
</div>

We started by importing our queries, mutations and type definitions from the resolvers file,  then we created a `resolvers` object containing the imported queries and mutations then passed it into the `ApolloServer` constructor alongside the imported type definition. 

Next, we created an instance of express.js in the app variable and integrated it into apollo server by calling the `applyMiddleware` method. According to [react-apollo’s documentation](https://www.apollographql.com/docs/apollo-server/integrations/middleware/#applying-middleware) on the applyMiddleware method, this integration enables the addition of various small internal middlewares. Lastly, we called the `listen` method on the express instance, telling it to listen and serve HTTP connections on port 4000. We also added a callback to log out a message telling users the server has been started. 

The Graph Query Language is strongly typed and this is where most of it’s auto-documenting feature comes from. This strong typing is achieved using the [GraphQL Schema definition language](https://graphql.org/learn/schema/). It is also what is used to specify the data resolved by the Query, Mutation and Subscription operations.

A practical example of this is our schema definition for our upload application below.

<pre><code class="language-javascript">const { gql }  =  require('apollo-server-express')

const typeDefinitions  = gql&#96; 
  type File {
    filename: String!
    mimetype: String!
    encoding: String!
  }

  type User {
     username: String
     imageurl: String
  }

  type Query { 
    getUser  : User
  }

  type Mutation {
    createUser ( 
      username : String!
      image : Upload!
     ) : User

    deleteUser () : Boolean!
   }
&#96;
export default typeDefinitions
</code></pre>

Above, we created a schema using [gql](https://www.apollographql.com/docs/apollo-server/api/apollo-server/#gql), consisting of three types; the File and User types which are [object types](https://www.apollographql.com/docs/apollo-server/schema/schema/#object-types) in the GraphQL Schema Definition Language and the [Query](https://www.apollographql.com/docs/apollo-server/schema/schema/#the-query-type) and [Mutation](https://www.apollographql.com/docs/apollo-server/schema/schema/#the-mutation-type) types respectively

{{% feature-panel %}}

The created File object type contains three string fields; `filename, mimetype and  encoding` which are all typically contained in any uploaded file. Next, we created an [object type](https://www.apollographql.com/docs/apollo-server/schema/schema/#object-types) for Users with two string fields; `username` and `imageurl`. The `username` field is the username typed in by a user when creating an account, while the `imageu`rl is the url of the image uploaded to the Google Cloud Storage. It would be used passed into the image `src` attribute to render the stored image to the user.

Next, we create the Query type which defines the query resolver function we have in the application. In our case, it is a single query used to get the user’s data. The `getUser` query here returns all data in the  User object type. 

We also created the Mutation type, which defines the two following mutations resolver functions below;

-  The first one `createUser`  takes in a username which is a [string scalar type](https://www.apollographql.com/docs/apollo-server/schema/schema/#scalar-types) and an Upload input type which comes from React-Apollo. It returns all data contained in the User object type after a successful account creation
- The second one `deleteUser` takes in no argument but returns a boolean value to indicate if the deletion was successful or not.  

**Note**: *The exclamation mark (`!`)  attached to these values make them mandatory, meaning that data must be present in that operation.*

### Implementing Resolver Functions

Having written a schema which defines the resolver function in our application, we can now go ahead in implementing the functions for the resolvers which we previously defined in the schema. 
         
We start with the `getUser` resolver function which returns the user’s data.

<pre><code class="language-javascript">// stores our user data
let Data  = []

export const Queries = {
   getUser: () => {
      return Data
  }
}
</code></pre>

We created a data array which stores the user’ data. This data array is to be used by both the mutation and query function and so it is declared globally. 
Next, we  implemented  the `getUser` function which  returns the array containing the user’s data when queried. 

### Mutating Data

In Graphql applications, CREATE, UPDATE and DELETE operations are performed through the use of the Mutation resolver functions, they are what **mutate** the data.

An example of these mutation resolvers are the two resolvers in our application which creates a user and deletes a user.  

<pre><code class="language-javascript">export const Mutations = {
    createUser: (_, { username, image }) => {
      # boilerplate resolver function
   },

 # resets the user's data 
  deleteUser: (_ ) =>  {
    Data = []

    if (Data.length < 1) {
        return true
    } else {
        return false
    }
 },
}
</code></pre>

Here is an explanation of the two resolvers above:

- **`createUser`**  
This creates a user using the passed in arguments. First, we specify the [parent argument](https://www.apollographql.com/docs/apollo-server/data/resolvers/#resolver-arguments) (`_`) and next we destructure the username and image which would be passed in when making the mutation in our frontend application.  
This is where the uploading of files will take place. We will come back to the actual implementation of this mutation resolver after setting up a connection to the Google Cloud Storage.
- **`deleteUser`**  
As we defined it in our schema, this resolver function takes no [argument](https://www.apollographql.com/docs/apollo-server/data/resolvers/#resolver-arguments). The purpose is to empty the data array and by checking the length, it returns a boolean value; - `true` if the items are less than 1, meaning the array is empty and `false` if not.  
**Note**: *If we had a real database connection, this resolver function would take in an ID argument which would be used in selecting the user whose record is to be deleted.*

Having created our schema and resolver functions, we can now start our node server and test it by making HTTP requests using [curl](https://curl.haxx.se/) at  `https://localhost:4000/graphql`  or more conveniently, using the offline GraphiQL web console on  `https://localhost:4000/graphql`  just as shown below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55367957-ec22-4c00-89cc-beb18370ff24/react-app-graphiql.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55367957-ec22-4c00-89cc-beb18370ff24/react-app-graphiql.png" sizes="100vw" caption="Offline GraphiQL GUI editor for making GraphQL operations (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55367957-ec22-4c00-89cc-beb18370ff24/react-app-graphiql.png'>Large preview</a>)" alt="The graphiql console with a getUser request being made an empty reponse" >}}

{{% ad-panel-leaderboard %}}

## Setting Up The Google Cloud Storage

The [Google Cloud Storage,](https://cloud.google.com/storage/docs)  an online file storage service is used to store object data. It is flexible enough to serve the needs of either enterprise grade applications or personal projects such as this. Being one of the offerings of the [Google Cloud Platform,](https://cloud.google.com/)  it can be found within the **Storage** section of the Google Cloud Console. 
 
To get started, follow the following steps : 

1. Visit the [Google Cloud Platform](https://console.cloud.google.com) to create an account and a [project](https://console.cloud.google.com/projectcreate).  
(*First time users are given $300 worth of GCP credits so which is more than enough for this demo project.)*
2. Visit the [Storage Browser](https://console.cloud.google.com/storage/browser) section, within the Google Cloud Console and click on the [Create Bucket](https://console.cloud.google.com/storage/create-bucket?) button within the top navigation pane.
3. Enter a preferred bucket name, leave other settings as default and click the create button at the bottom of the list.

After being created, we would be redirected to the empty bucket similar to the one below;

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b25c5b3c-ebca-4a3a-80f9-8d64e2121df3/react-app-empty-bucket.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b25c5b3c-ebca-4a3a-80f9-8d64e2121df3/react-app-empty-bucket.png" sizes="100vw" caption="Webpage for our cloud bucket within the Google Storage Browser (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b25c5b3c-ebca-4a3a-80f9-8d64e2121df3/react-app-empty-bucket.png'>Large preview</a>)" alt="The default page for new buckets created on the Google Cloud" >}}

At this point we have created a bucket where the uploaded files would be stored. Next we need a [Service Account](https://cloud.google.com/iam/docs/understanding-service-accounts) in order to enable a communication between our Node server and the Google Cloud.

### What are Service Accounts?

[Service accounts](https://cloud.google.com/iam/docs/understanding-service-accounts) are a special type of account on the Google Cloud, created for non-human interaction, meaning communication through APIs. In our application, it would be used with a service account key by our API  to authenticate with the Google Cloud when uploading  stored user's images.  

We follow the following steps in order to create a service account.


1. Open the [Identity Access Management](https://console.cloud.google.com/iam-admin/iam?) ( IAM ) section of the Google Cloud Console
2. From the left side navigation bar, click on Service Accounts and when there click on the Create Service Account button. 
3. Enter a preferred name and a description and click the **Create** button.
    We would see a service account ID being auto generated using characters from our typed in name.
4. Next, click the **Select Role** dropdown menu to select a role for this service account.
5. Type “Storage Admin” and click the [Storage Admin](https://cloud.google.com/iam/docs/understanding-roles#cloud-storage-roles) role.
    This role gives our Node server a full control over stored resources in our storage buckets.
6. Leave the remaining fields blank and click on the Done button.


    After being created, we would be redirected to a list of all Service Accounts within our project, including the default created ones and the newly created service account. 

           
Next, we need to create a secret [Service Account Key](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) in JSON format. The following steps below outline how to do that;
 
 1. Click on the newly created Service Account to get to the page for this Service Account.
 2. Scroll to the Keys section and click the **Add Key** dropdown and click on the **Create new key** option which opens a modal.
 3. Select a [JSON](https://json.org/) file format and click the Create button at the bottom right of the modal.

After creating that, the key would be downloaded locally to our device and we would see an alert telling the user to keep the key private. This is because it contains sensitive fields about our project on the Google Cloud Platform. 
Below is an example of the contained fields :

<div class="break-out">

 <pre><code class="language-json"> {
  "type": "service_account",
  "project_id": "PROJECT_NAME-PROJECT_ID",
  "private_key_id": "XXX-XXX-XXX-XXX-XXXX-XXX",
  "private_key": AN R.S.A KEY,
  "client_email": "SERVICE_ACCOUNT_NAME-PROJECT-NAME.iam.gserviceaccount.com",
  "client_id": PROJECT-CLIENT-ID,
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/SERVICE-ACCOUNT-NAME%PROJECT-NAME-PROJECT-ID.iam.gserviceaccount.com"
}
</code></pre>
</div>
              
We now left with the following additional steps below in order to complete setting up our project on the Google Cloud Platform.

1. Move the renamed file into our project directory 
2. Add the name of this file into our `.gitignore` file inorder to prevent it getting pushed to Github or any preferred Version Control Service. 

## Implementing Create User Mutation

At this point, we can begin our implementation of the  `createUser`  resolver by connecting the Google Cloud Storage  using  [@google-cloud/storage](https://www.npmjs.com/package/@google-cloud/storage) package. Aside using this library, we have the option of interacting with the Google Cloud Storage by make direct [HTTP requests](https://cloud.google.com/storage/docs/request-endpoints) to the available [API Endpoints](https://cloud.google.com/storage/docs/request-endpoints#typical), however the [Google Storage Package](https://www.npmjs.com/package/@google-cloud/storage) does that internally and more for us.

First we initiate a connection process with the Google Cloud Storage in the `createUser` resolver
       
<div class="break-out">

 <pre><code class="language-javascript">import  { Storage } from '@google-cloud/storage';
 

export const Mutations = {

createUser : (&#95;, { username, image }) => {
const bucketName = "node-graphql-application"; // our bucket name

// We pass-in the downloaded SECRET KEY from our Service Account, 
 const storage = new Storage({ keyFilename: path.join(&#95;&#95;dirname, "../upload.json") });
  }
}
</code></pre>
</div> 
    
After initializing the Storage constructor import from the [@google-cloud/storage](https://www.npmjs.com/package/@google-cloud/storage) package, using  [path](https://www.npmjs.com/package/path) we construct the file path to where the secret-key json file was stored. The is secret-key file has all the necessary data needed to authenticate with the Google Cloud.
    
Next, we expand our `createUser`  resolver function to process and upload the passed in images to our Bucket on the Google Cloud Storage.

<div class="break-out">

 <pre><code class="language-javascript">const removeWhiteSpaces = (name) => {
  return name.replace(/\s+/g, "");
};

export const Mutations = {
  createUser : async (_ , {filename , image}) => {
   const { filename, createReadStream } = await image;

    let sanitizedName = removeWhiteSpaces(filename);
    await new Promise((resolve, reject) => {
      createReadStream().pipe(
        storage
          .bucket(bucketName)
          .file(sanitizedName)
          .createWriteStream()
          .on("finish", () => {
            storage
              .bucket(bucketName)
              .file(sanitizedName)

           // make the file public
              .makePublic() 
              .then(() => {
                Data = [];

            // save user's data into the Data array
                Data.push({
                  username: username,
                  imageurl: `https://storage.googleapis.com/${bucketName}/${sanitizedName}`,
                });
                resolve();
              })
              .catch((e) => {
                reject((e) => console.log(`exec error : ${e}`));
              });
          })
      );
    });
  }
}
</code></pre>
</div>      

Above we are a performing a file upload of the file passed in to the resolver function. Here is a gradual breakdown of everything being done within the resolver;

- First, we asynchronously destructured `filename` and `createReadStream` from the uploaded file.  We then rid the destructured filename of whitespaces. The Storage library will try to do this by replacing the whitespace with the percentage character ( `%` )and this leads to a distorted file URL which can also choose to ignore.
- Next, we create a new promise and using [Node Streams,](https://nodejs.org/api/stream.html#stream_api_for_stream_consumers) we pipe the  `createReadStream`  to the Google Storage constructor. We resolve this promise after a successful file upload or reject it in the error promise state from the `makePublic` method.
- We call the the bucket method on the storage class and pass in the name of our storage bucket and we further call the file method and pass in the name of the file and then we call the `createWriteStream` method to upload the file.  
- We make the file public, by calling the `makePublic` method after passing the bucket name and filename of the recently uploaded file. 
- We create an object of the user’s data containing the username, and a constructed url of the file uploaded to our storage bucket. The URL structure for public files on the Google Cloud Storage is `https://storage.googleapis.com/{BUCKET_NAME}/{FILENAME}`, using JavaScript’s template literals, we can insert our bucket name into the `BUCKET_NAME` placeholder and also the name of the uploaded file into the `FILENAME` placeholder and this would give a valid URL of the file which we can access it through.

**Note**: *Files are private by default on the Google Cloud Storage and cannot be accessed via URL, hence the need to make the file public after uploading into our cloud bucket.*

We can test the `createUser` endpoint using [curl](https://curl.haxx.se/) to perform a demo account creation. 
 
<div class="break-out">

 <pre><code class="language-bash">curl localhost:4000/graphql  -F operations='{ "query": "mutation createUser($image: Upload! $username : String!) { createUser(image: $image  username : $username) { username imageuri } }", "variables": { "image": null, "username" : "Test user" } }' -F map='{ "0": ["variables.image"] }'  -F 0=test.png
</code></pre>
</div>

In the HTTP request above, we specified the HTTP verb as a POST request and our endpoint and other request headers. After that, we specified the GraphQL operation for the `createUser` resolver, inferring the username and image types. Then we specified the path to the test file. 

If the request above is successful, we would see the uploaded file listed in our bucket like this: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c455c8-4e5d-422e-b4bf-a5be33388ff8/react-app-curl-test-request.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c455c8-4e5d-422e-b4bf-a5be33388ff8/react-app-curl-test-request.png" sizes="100vw" caption="Http request being made using curl to upload an image and the uploaded image listed in the Google Cloud Bucket (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c455c8-4e5d-422e-b4bf-a5be33388ff8/react-app-curl-test-request.png'>Large preview</a>)" alt="Http request to test the `createUser` mutation resolver function" >}}

## Consuming Our GraphQL API

Now we are left with building the front-end part of our application which consumes our GraphQL API. We would be bootstrapping our React application using the [create-react-app cli](https://github.com/facebook/create-react-app).

To get started, run the following commands from your terminal : 

<div class="break-out">

 <pre><code class="language-bash"># Create A New Application using Create-React-App CLI
npx create-react-app Graphql-upload-frontend

# Move into newly created project directory
cd Graphql-upload-frontend

# Dependencies needed for our application
yarn add react-dropzone @apollo/react-hooks graphql apollo-cache-inmemory
</code></pre>
</div>
    
Next, we create a link to our GraphQL endpoint and initiate the Apollo Client in a separate configuration file.

<div class="break-out">

 <pre><code class="language-javascript">// config.js

import { ApolloClient } from "apollo-client";
import { InMemoryCache } from "apollo-cache-inmemory";
import { createUploadLink } from "apollo-upload-client";

const GRAPHQL_ENDPOINT = "https://localhost:3000/graphql"; 
const cache = new InMemoryCache()

const Link = createUploadLink({
  url: GRAPHQL_ENDPOINT,
});

export const Config = new ApolloClient({
  link: uploadLink,
  cache
})
</code></pre>
</div>  
  
If you have gone through the [Getting Started](https://www.apollographql.com/docs/react/get-started/#create-a-client) section of the [React-Apollo documentation,](https://www.apollographql.com/docs/react/) you would notice a slight difference in the packages used. Here is a breakdown of what we accomplished above: 

- By initializing the `InMemoryCache` constructor from the `[apollo-cache-inmemor](https://www.npmjs.com/package/apollo-cache-inmemory)``y` package, we created a data store which stores the cache from all requests made in our application
- We created a connection link using the `apollo-upload-client` package which has our single GraphQL endpoint as a value. This link handles the multi-part upload requests which is done when a file is being uploaded through a GraphQL endpoint and also handles the Query and Mutation operation.  
- We initialized the Apollo Client constructor in a variable, passed in the upload link and the cache and  then exported the variable to be used by the ApolloClient provider.  

We then wrap our entire application tree with the `ApolloProvider`, so we can make a query, mutation or subscription from any component.

<pre><code class="language-javascript">import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import * as serviceWorker from "./serviceWorker";
import { Config } from "./config";
import { ApolloProvider } from "@apollo/react-hooks";

ReactDOM.render(
    &lt;ApolloProvider client={Config}&gt;
      &lt;App /&gt;
    &lt;/ApolloProvider&gt;,
  document.getElementById("root")
);

serviceWorker.unregister();
</code></pre>

We can above see the `ApolloProvider` wrap the root component and we passed in the Apollo Client which was exported from the configuration file as `Config` into the ApolloProvider’s client prop.

{{% ad-panel-leaderboard %}}

## Working With GraphQL Data

At this stage, our application is almost ready to begin working with data from the GraphQL application but before that, we need to define our GraphQL operations. Remember the strong typing feature of GraphQL we previously talked about? It also applies on the Client Side.

We define our GraphQL operations using `gql`  from the `@apollo/react-hooks` package. We use [gql](https://www.apollographql.com/docs/apollo-server/api/apollo-server/#gql) with grave accents (backticks) to parse a GraphQL string. First we define the operation type (either a mutation, subscription or query) then we give it a name. If the operation takes any arguments, we infer the types of the individual arguments in a parenthesis to a prefix identifier using a [sigil operator](https://en.wikipedia.org/wiki/Sigil_(computer_programming)) ($) and we can then use this typed argument  through it’s prefix.

We can see a practical example of this in the three GraphQL operations we have defined below for our application.
        

<pre><code class="language-javascript"># data.js
import { gql } from "@apollo/react-hooks";

export const CREATE_USER = gql`
  mutation createUser($username: String!, $image: Upload!) {
    createUser(username: $username, image: $image) {
      username
    }
  }
`;

export const DELETE_ACCOUNT = gql`
  mutation deleteAccount {
    deleteUser
  }
`;

export const GET_USER = gql`
  query getUser {
    getUser {
      username
      imageurl
    }
  }
`;
</code></pre>   

Above, we are defining our GraphQL operations to be used in variables and we are exporting these variables so they can be used by the application components. Here is a quick rundown of each variable:    

- `CREATE_USER`  
It defines the `createUser` mutation which receives a username of a string type  and also an image which has the Upload object type from React-Apollo. The image is represents the file which is uploaded by the user with all necessary fields within.
- `DELETE_ACCOUNT`  
This is also defined as a mutation, but it receives nothing hence it has no parenthesis containing any defined scalar. It only defines and name the `deleteUser` mutation.
- `GET_USER`  
This is defined as a Query operation. We can see the two values which are returned from this query being stated in the within the curly braces. Although this query receives no argument, GraphQL queries sometime also receive arguments when fetching a specific data and the arguments are also defined in the parenthesis just like a mutation.

Now that we have  a GraphQL connection in our application, we can now build out Application Layout where we make use of the previously defined GraphQL operations in two components.

## Application Layout

Our application would have the following states in order to welcome a new user, create an account and lastly keep that user logged in.
  
- **Guest State**  
This is the initial state of the application where users are shown a default username and image. A user can switch this state by creating an account.  
- **Create Account State**  
Users at this point can type in a username and  drag ‘n’ drop or click to add an image. This is the point where the createUser mutation is fired when the submit button is clicked. 
- **Signed In State**  
At this point an account has been created, the image displayed is that which was uploaded by the user and is accessed using the image url from the Google Cloud Bucket.

All the states would be implemented in two components: **App Component** and **Create Account Component**. These states would be managed using React Hooks.

We begin with implementing the Guest state in the **App Component**, which shows a welcome text and a default stored image.
     
<div class="break-out">

 <pre><code class="language-javascript">import React, { useState } from "react";

const App  = () =&gt; { 
 const [ isCreatingAccount , setCreatingAccount ] = useState(false)

 return (
  &lt;div className="App" style={{ height: window.innerHeight - 35 }}&gt;
      &lt;div onClick={() =&gt; {isCreatingAccount(true)}}  className="auth" &gt;
        &lt;p className="auth-text"&gt;
          Sign In
        &lt;/p&gt;
      &lt;/div&gt;
        &lt;div className="content"
            &lt;img
              className="user-img"
              src={ require("./assets/groot.jpg")}
              alt="default user and user"
            /&gt;
              &lt;h1&gt;  Hi There, i am   Groot &lt;/h1&gt;
              &lt;p&gt; You can sign-in to become you!  &lt;/p&gt;
          &lt;/div&gt;
    &lt;/div&gt;
   )
}

export default App
</code></pre>
</div>

Above we have a React component which renders; a button, an image and a default welcome text. A user can switch the application state to create an account by the click of the Sign In button. 

When placed in the `app.js` file in our project, our application becomes similar to the application below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bc8cdfe-1d23-49de-8ef3-a2b494f2eec2/react-app-application-default-state.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bc8cdfe-1d23-49de-8ef3-a2b494f2eec2/react-app-application-default-state.png" sizes="100vw" caption="The default application state when opened (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bc8cdfe-1d23-49de-8ef3-a2b494f2eec2/react-app-application-default-state.png'>Large preview</a>)" alt="Default application state" >}}

We expand the App Component to switch from the default view to the input fields at the click of the **Create Account** button.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState, useEffect } from "react";
import { useMutation, useLazyQuery } from "@apollo/react-hooks";
import CreateUser from "./create-user";
import "../App.css";
import { DELETE_ACCOUNT, GET_USER } from "../data";

function App() {
  const [deleteUser] = useMutation(DELETE_ACCOUNT);
  const [getUser, { data, error }] = useLazyQuery(GET_USER);

  // state used to switch between a Guest and a user
  const [isLoggedIn, setLoggedIn] = useState(false);
  const [isCreatingAccount, beginCreatingAccount] = useState(false);

  // user data stored in state and passed to GraphQL
  const [userName, setuserName] = useState("");
  const [imgUrl, setImgUrl] = useState(null);

  // deleteAccount function which deletes the user's account
  const deleteAnAccount = () =&gt; {
    deleteUser()
      .then(() =&gt; {
        // resets all stored state
        setLoggedIn(false);
        setImgUrl(null);
        setuserName("");
      })
      .catch((e) =&gt; console.log(e));
  };

  useEffect(() =&gt; {
    if (isLoggedIn && data !== undefined) {
      setImgUrl(data.getUser[0].imageurl);
    }
  }, [data]);

  return (
    &lt;div className="App" style={{ height: window.innerHeight - 35 }}&gt;
      &lt;div
        onClick={() =&gt; {
          if (!isLoggedIn) {
            beginCreatingAccount(!isCreatingAccount);
          } else if (isLoggedIn) {
            deleteAnAccount();
          }
        }}
        className="auth"
      &gt;
        &lt;p className="auth-text"&gt;
          {!isLoggedIn ? (!isCreatingAccount ? "Sign In" : "Cancel") : "Logout"}
        &lt;/p&gt;
      &lt;/div&gt;
      &lt;div className="content"&gt;
        {!isCreatingAccount ? (
          &lt;div&gt;
            &lt;img
              className="user-img"
              src={imgUrl ? imgUrl : require("../assets/groot.jpg")}
              alt="default user and user"
            /&gt;
            &lt;h1&gt;
              Hi There, i am
              {userName.length &gt; 3 ? ` ${userName}` : ` Groot`}.
            &lt;/h1&gt;
            &lt;p&gt;
              {!isLoggedIn
                ? "You can sign-in to become you!"
                : "You sign-out to become Groot!"}
            &lt;/p&gt;
          &lt;/div&gt;
        ) : (
          &lt;CreateUser
            updateProfile={() =&gt; {
              getUser();
              setLoggedIn(true);
              beginCreatingAccount(false);
            }}
          /&gt;
        )}
      &lt;/div&gt;
    &lt;/div&gt;
  );
}

export default App;
</code></pre>
</div>

In the code above, we have made the following additions to our application; 

- We created two new states to track when the user is logged in and when the user is creating an account. These two states are updated by the Sign In button which can now start an account creation process or cancel it and return back to the default state. 
- Our application now uses the `useLazyQuery` hook which comes from `apollo/react-hooks` package to make a GraphQL query to fetch the user’s data using our previously created `GET_USER` definition.

    - Our query here is said to be lazy because it is not executed immediately the application is loaded. It is executed after the `createUser`  mutation in the Create Account component has been executed successfully. According to the [React - Apollo documentation](https://www.apollographql.com/docs/react/data/queries/#executing-queries-manually), `useLazyQuery` does not execute it’s associated query immediately, but rather in response to events.
    
- We watch the destructured data value which is undefined by default until the query is made, in a `useEffect` and then we switch the image src attribute to the imageurl returned from the query after querying the user’s data.
- At the click of the Sign In button the `isCreatingAccount` state is updated to true and the Create Account component is shown for a user to input a username and add an image file.
- After creating an account, a user can click the Sign Out button to invoke the `deleteAUser` function which executes the `deleteUser` mutation and when successful, it  resets all state in the App Component.

Now, we can implement a drag ‘n’ drop functionality within the create-user component where an image can be dragged or clicked to open the device media explorer and after this we upload the added file to our Node server.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState, useCallback } from "react";
import { useMutation } from "@apollo/react-hooks";
import { useDropzone } from "react-dropzone";
import "../App.css";
import { CREATE_USER, GET_USER } from "../data";

const CreateUser = (props) =&gt; {
  const { updateProfile } = props;
  const [createAccount, { loading }] = useMutation(CREATE_USER);
  // user data stored in state and passed to GraphQL
  const [userName, setuserName] = useState("");
  // user's uploaded image store in useState and passed to the GraphQL mutation
  const [userImage, setUserImage] = useState(null);

  // create user mutation function fired at the click of `createAccount` button
  const createAUser = () =&gt; {
    createAccount({
      variables: {
        username: userName,
        image: userImage,
      },
    })
      .then(() =&gt; {
        updateProfile();
      })
      .catch((e) =&gt; console.log(e));
  };

  const onDrop = useCallback(([file]) =&gt; {
    setUserImage(file);
  }, []);

  const {
    getRootProps,
    isDragActive,
    isDragAccept,
    getInputProps,
    isDragReject,
  } = useDropzone({
    onDrop,
    accept: "image/jpeg , image/jpg, image/png",
  });

  return (
    &lt;div className="CreateUser" style={{ height: window.innerHeight - 35 }}&gt;
      &lt;div className="content"&gt;
        &lt;div&gt;
          &lt;h1&gt; {!loading ? "Create An Account" : "Creating Account ..."}&lt;/h1&gt;
          &lt;hr /&gt;
          &lt;br /&gt;
          &lt;form className="form"&gt;
            &lt;div className="input-body"&gt;
              &lt;label style={{ color: loading && "grey" }}&gt; Username &lt;/label&gt;
              &lt;input
                disabled={loading}
                style={{ color: loading && "grey" }}
                onChange={(e) =&gt; setuserName(e.target.value)}
                placeholder="some nifty name"
                required={true}
                type="text"
              /&gt;
              &lt;br /&gt;
              &lt;br /&gt;
              {!userImage ? (
                &lt;div
                  className="circle-ctn"
                  {...getRootProps({
                    isDragActive,
                    isDragAccept,
                    isDragReject,
                  })}
                &gt;
                  &lt;input {...getInputProps()} /&gt;
                  &lt;div
                    className="box"
                    style={{
                      background: isDragActive && "#1b2733",
                    }}
                  &gt;
                    &lt;p
                      style={{ color: isDragReject && "red" }}
                      className="circle-text"
                    &gt;
                      {!isDragActive
                        ? `Tap or Drag 'n' Drop Image  to Add Profile Picture`
                        : isDragReject
                        ? "Ooops upload images only"
                        : "Drop your image here to upload"}
                    &lt;/p&gt;
                  &lt;/div&gt;
                &lt;/div&gt;
              ) : (
                &lt;div className="img-illustration"&gt;
                  &lt;img
                    style={{ filter: loading && "grayscale(80%)" }}
                    className="img-icon"
                    src={require("../assets/image-icon.png")}
                    alt="image illustration"
                  /&gt;
                  &lt;p style={{ color: loading && "grey" }} className="file-name"&gt;
                    {userImage.path}
                  &lt;/p&gt;
                &lt;/div&gt;
              )}
              &lt;br /&gt;
              &lt;br /&gt;
              &lt;button
                style={{
                  background: userName.length &lt; 3 && "transparent",
                  color: userName.length &lt; 3 && "silver",
                }}
                className="create-acct-btn"
                onClick={(e) =&gt; {
                  e.preventDefault();
                  createAUser();
                }}
                disabled={userName.length &lt; 3 || loading}
              &gt;
                {!loading ? "Create Account" : "Creating Account"}
              &lt;/button&gt;
            &lt;/div&gt;
          &lt;/form&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default CreateUser;
</code></pre>
</div>

Here is a gradual breakdown of all that’s happening above:

- We destructured `createAccount` resolver function from the `useMutation` hook after passing in our previously defined `CREATE_USER` operation.
- We created a function;- `createAUser` which is invoked at the click of the **Create Account** button after typing in a username and adding an image. 
- We created an `onDrop` function which is wrapped in the [useCallback](https://reactjs.org/docs/hooks-reference.html#usecallback) to avoid a recompution of this function.  After the file is dropped,  we keep it temporarily in the `userImage` state to be used when submitting the data.
- We destructured the four root properties from the useDropZone hook and then specified the acceptable file types alongside our custom onDrop function.
- Next, those root properties destructured are used in building a reactive dropzone, that reacts when an acceptable file or non - acceptable file is being dragged over our dropzone. This done by applying the root properties to our selected dropzone , which here happens to be a div element wrapping other smaller div elements. Also, by spreading the `…getInputProps()` in the `input` element, it makes the input element hidden with a file type so when the dropzone is clicked, it opens the device media explorer. 
- Lastly, we used the ternary operator in the inline styles to make the div have a border when a file is being dragged over it and also make this border red when a file type not specified is being dragged.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f2ad873-9625-444f-83b4-a043e1e86155/react-app-test-file-upload.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f2ad873-9625-444f-83b4-a043e1e86155/react-app-test-file-upload.png" sizes="100vw" caption="Testing the reactiveness of the dropzone using the isDragAccept and isDragReject props from react-dropzone (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f2ad873-9625-444f-83b4-a043e1e86155/react-app-test-file-upload.png'>Large preview</a>)" alt="Testing the isDragAccept and isDragReject applied props" >}}

Now at the click of the Create Account button, using a ternary operator and the loading boolean value destructured from the `useMutation` hook, we switch the  “Create Account “ text  to “Creating Account …” to indicate that the data is being submitted and a network request is in flight.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfd294ac-e35a-4d54-bcc2-7592f76d9df0/react-app-mutation-loading.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfd294ac-e35a-4d54-bcc2-7592f76d9df0/react-app-mutation-loading.png" sizes="100vw" caption="An upload to test the entire application built (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfd294ac-e35a-4d54-bcc2-7592f76d9df0/react-app-mutation-loading.png'>Large preview</a>)" alt="A test of the entire upload application built" >}}

Once the mutation has been executed successfully, we execute the lazy `getUser` query and we switch back to the Home Component but this time with data from the `getUser` query. Using the imageurl value returned in the `getUser` query result, we can access the uploaded image over the internet and also display it in the page. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4edf156f-28eb-42fa-bb81-74f3f9240525/react-app-user-created-state.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4edf156f-28eb-42fa-bb81-74f3f9240525/react-app-user-created-state.png" sizes="100vw" caption="Application view changed to reflect a loading mutation state (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4edf156f-28eb-42fa-bb81-74f3f9240525/react-app-user-created-state.png'>Large preview</a>)" alt="CreateUser mutation being executed" >}}

## Conclusion 

In this article, we have walked through three aspects of creating a file upload pipeline. First we built a frontend application where users can drag and upload a file to upload it. Then we built a GraphQL API that connects the frontend application and a mutation to handle the incoming file. Lastly we connected our server to the Google Cloud Storage to store the file from the node server.

It is also recommended to read [Apollo Server File Upload Best Practices](https://www.apollographql.com/blog/apollo-server-file-upload-best-practices-1e7f24cdc050/) on two more ways of performing file in a GraphQL application.

All files and code snippets referenced and used within this article is available [Github](https://github.com/smashingmagazine/Node-graphql-upload-article). 

### References

- [Google Cloud](https://cloud.google.com/), official website
- “[Introduction to Apollo Client](https://www.apollographql.com/docs/react/),” Apollo Docs
- “[API for stream consumers](https://nodejs.org/api/stream.html#stream_api_for_stream_consumers),” Node.js official website
- [`react-dropzone`](https://www.npmjs.com/package/react-dropzone), npm
- [`useCallback`](https://reactjs.org/docs/hooks-reference.html#usecallback), React.js Docs
- “[Apollo Server File Upload Best Practices](https://www.apollographql.com/blog/apollo-server-file-upload-best-practices-1e7f24cdc050/),” Apollo Blog
- “[Understanding Client-Side GraphQl With Apollo-Client In React Apps](https://www.smashingmagazine.com/2020/07/client-side-graphql-apollo-client-react-apps/),” Blessing Krofegha, Smashing Magazine

{{< signature "ks, ra, il" >}}
