---
title: 'GraphQL On The Front-End (React And Apollo)'
slug: graphql-frontend-react-apollo
author: david-atanda
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb584488-c16f-4409-a992-993ce92d4b51/graphql-frontend-react-apollo.jpg
date: 2021-11-04T11:30:00.000Z
summary: >-
  Within the last decade, technologies like GraphQL have changed how we build web apps and how they communicate with each other. GraphQL provides certain benefits over REST APIs &mdash; let’s find out what they are.
description: >-
  Within the last decade, technologies like GraphQL have changed how we build web apps and how they communicate with each other. GraphQL provides certain benefits over REST APIs &mdash; let’s find out what they are.
categories:
  - React
  - GraphQL
  - Coding
  - API
---

One of the main benefits of GraphQL is the client’s ability to request what they need from the server and receive that data exactly and predictably. Without much effort, one can easily pull nested data by just adding more properties to our queries instead of adding multiple endpoints. This prevents issues like over-fetching that can impact performance.

Usually, to handle GraphQL on the client-side, we make use of the Apollo Client. It allows developers to define, handle, and make queries/mutations available within our application. It can also act as a state management tool with your client-side application.

In this article, we’re going to learn how to handle real-time updates on the client-side using GraphQL. We’ll be learning how to do this with GraphQL Features like Cache Update, Subscriptions, and Optimistic UI. We’ll also be touching on how to use Apollo as a state-management tool, possibly replacing redux. Plus, we’ll look at how to create usuable GraphQL queries with Fragments, and how to use Apollo directives to write more complex queries.

## Installation

Before we begin, let’s just go through installation and setting up our project. Let’s get right into the code. To create a React app, make sure you have Node.js installed on your computer. If you haven’t built a React app before, you can check to see if you have Node.js installed by typing the following into your terminal:

<pre><code class="language-bash">node -v</code></pre>

If not, just go to the Node.js website to [download the latest version](https://nodejs.org/en/download/).

Once that’s done, we can get started with our React app by running this command:

<pre><code class="language-bash">npx create-react-app react-graphql</code></pre>                

Next, let’s navigate into our project folder on the terminal:

<pre><code class="language-bash">cd react-graphql</code></pre>

Once that’s done, we’ll install Apollo using this line:

<pre><code class="language-bash">npm i @apollo/client</code></pre>

Or better still, you could just go on and clone the repo. The repo contains both the client-side and server, so we have some other dependencies that’s needed. We’ll install those dependencies by running:

<pre><code class="language-bash">npm install</code></pre>

Just before we start, this is the [repo](https://github.com/Atanda1/react-graphql) containing the code demonstrating everything under Real-time update on GraphQL, using Apollo as a state management tool, Fragments, and Apollo directives. Also, here’s the [repo](https://github.com/Atanda1/subscrpition) containing the code demonstrating subscription on the the client-side.  

{{% feature-panel %}}

## Real-time Update On GraphQL 

The ability to create a real-time update on the client-side helps improve the user experience of the site, making everything seem smoother. Just imagine a situation where a user adds a new item by filling a form, and that item updates instantly by been added to the list of items on the same page. Although, this real-time update could sync with a server directly through subscriptions, or it might be manipulated on the frontend through things like Optimistic UI, or using the `update` function on the `useMutation`. So let’s get to the technical implementation. Here’s the [repo](https://github.com/Atanda1/react-graphql) containing the code demonstrating everything under Real-time update On Graphql, using Apollo as a state management tool, Fragments, and Apollo directives.

### Updating the cache directly using `update` function on the `useMutation`

`useMutations` are imported directly from the `@apollo/client` library, and it helps us make mutations to the data on our server.

Usually, we can create mutations with Apollo using `useMutations`, but beyond that, what we’ll be doing is using the `update` function to update our apollo-client cache directly through `useMutation`.

In this sample below, we send queries to the server to get a list of pets using `useQuery` and make a mutation by having a form to add more pets to our server using `useMutation`. The problem we’ll have is that when a new pet is added to the server, it doesn’t get added to the list of pets(on the browser) immediately, unless the page is refreshed. This makes the user experience of this section of the app feel broken, especially since the list of pets and the form are on the same page.

{{< vimeo id="610757694" breakout="true" >}}

<pre><code class="language-javascript">import React, { useState } from "react";
import gql from "graphql-tag";
import { useQuery, useMutation } from "@apollo/client";
import Loader from "../components/Loader";
import PetSection from "../components/PetSection";

//ALL_PETS uses gql from @apollo/client to allow us send nested queries 
const ALL_PETS = gql`
  query AllPets {
    pets {
      id
      name
      type
      img
    }
  }
`;

// NEW_PET uses gql from @apollo/client to create mutations
const NEW_PET = gql`
  mutation CreateAPet($newPet: NewPetInput!) {
    addedPet(input: $newPet) {
      id
      name
      type
      img
    }
  }
`;
function Pets() {
  const initialCount = 0;
  const [count, setCount] = useState(initialCount);
  const pets = useQuery(ALL_PETS);
  const [createPet, newPet] = useMutation(NEW_PET);
  const [name, setName] = useState("");
  const type = `DOG`;
 
  const onSubmit = (input) =&gt; {
    createPet({
      variables: { newPet: input },
    });
  };

  // this function triggers the submit action by calling the onSubmit function above it
  const submit = (e) =&gt; {
    e.preventDefault();
    onSubmit({ name, type });
  };

//If the data is loading we display the &lt;Loader/&gt; component instead
  if (pets.loading || newPet.loading) {
    return &lt;Loader /&gt;;
  }

//loops through the pets data in order to get each pet and display them with props using the &lt;PetSection&gt; component
  const petsList = pets.data.pets.map((pet) =&gt; (
    &lt;div className="col-xs-12 col-md-4 col" key={pet.id}&gt;
      &lt;div className="box"&gt;
        &lt;PetSection pet={pet} /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  ));

  return (
    &lt;div&gt;
      &lt;form onSubmit={submit}&gt;
        &lt;input
          className="input"
          type="text"
          placeholder="pet name"
          value={name}
          onChange={(e) =&gt; setName(e.target.value)}
          required
        /&gt;
        &lt;button type="submit" name="submit"&gt;
          add pet
        &lt;/button&gt;
      &lt;/form&gt;
      &lt;div&gt;
        {petsList}
      &lt;/div&gt;
      
    &lt;/div&gt;
  );
}
export default Pets;
</code></pre>

Using `update` function in the `useMutation` hook allows us to directly update our cache by reading and writing our `ALL_PETS`. Immediately we hit the submit button, the data is added to the list of pets in the cache by altering `ALL_PETS`. This lets us update our client-side cache immediately with consistent data.

<pre><code class="language-javascript">import React, { useState } from "react";
import gql from "graphql-tag";
import { useQuery, useMutation } from "@apollo/client";
import Loader from "../components/Loader";
import PetSection from "../components/PetSection";

//ALL_PETS uses gql from @apollo/client to allow us send nested queries 
const ALL_PETS = gql`
  query AllPets {
    pets {
      id
      name
      type
      img
    }
  }
`;

// NEW_PET uses gql from @apollo/client to create mutations
const NEW_PET = gql`
  mutation CreateAPet($newPet: NewPetInput!) {
    addedPet(input: $newPet) {
      id
      name
      type
      img
    }
  }
`;

function ThePets() {
  const initialCount = 0;
  const [count, setCount] = useState(initialCount);
  const pets = useQuery(ALL_PETS);

  //We then make use of useMutation and update() to update our ALL_PET

  const [createPet, newPet] = useMutation(NEW_PET, {
    update(cache, {data: {addedPet}}) {
      const allPets = cache.readQuery({query: ALL_PETS})
      cache.writeQuery({
        query: ALL_PETS,
        data: {pets: [addedPet, ...allPets.pets]}
      })
    }
  });
  const [name, setName] = useState("");
  const type = `DOG`;
 
  const onSubmit = (input) =&gt; {
    createPet({
      variables: { newPet: input },
    });
  };

  //Handles the submission of Pets that eventually triggers createPet through onSumit

  const submit = (e) =&gt; {
    e.preventDefault();
    onSubmit({ name, type });
  };

  //If the data is loading we display the &lt;Loader/&gt; component instead

  if (pets.loading || newPet.loading) {
    return &lt;Loader /&gt;;
  }

//loops through the pets data in order to get each pet and display them with props using the &lt;PetSection&gt; component

  const petsList = pets.data.pets.map((pet) =&gt; (
    &lt;div className="col-xs-12 col-md-4 col" key={pet.id}&gt;
      &lt;div className="box"&gt;
        &lt;PetSection pet={pet} /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  ));
  return (
    &lt;div&gt;
      &lt;form onSubmit={submit}&gt;
        &lt;input
          className="input"
          type="text"
          placeholder="pet name"
          value={name}
          onChange={(e) =&gt; setName(e.target.value)}
          required
        /&gt;
        &lt;button type="submit" name="submit"&gt;
          add pet
        &lt;/button&gt;
      &lt;/form&gt;
      &lt;div&gt;
        {petsList}
      &lt;/div&gt;
      
    &lt;/div&gt;
  );
}
export default ThePets;
</code></pre>

{{< vimeo id="610770120" breakout="true" >}}

{{% ad-panel-leaderboard %}}

## Subscriptions In GraphQL

Based on functionalities, subscription in GraphQL is similar to queries. The major difference is that while Queries is done just once, subscriptions are connected to the server, and automatically updates when there’s any change to that particular subscription. Here’s the [repo](https://github.com/Atanda1/subscrpition) containing the code demonstrating subscription on the the client-side.

First, we have to install:

<pre><code class="language-bash">npm install subscriptions-transport-ws</code></pre>

Then we go to our `index.js` to import and use it.

<pre><code class="language-javascript"> import { WebSocketLink } from "@apollo/client/link/ws";

//setting up our web sockets using WebSocketLink
const link = new WebSocketLink({
  uri: `ws://localhost:4000/`,
  options: {
    reconnect: true,
  },
});
const client = new ApolloClient({
  link,
  uri: "http://localhost:4000",
  cache: new InMemoryCache(),
});</code></pre>

**Note:** *`uri` in the code block directly above is for our endpoint.*

Then we go into our component and instead of query like we have above, we’ll use this subscription instead:

<pre><code class="language-javascript">import {  useMutation, useSubscription } from "@apollo/client";
//initiate our subscription on the client-side
const ALL_PETS = gql`
  subscription AllPets {
    pets {
      id
      name
      type
      img
    }
  }
`;</code></pre>
 
And instead of using `useQuery`, we would access our data using `useSubscription`.

<pre><code class="language-javascript"> const getMessages = useSubscription(ALL_PETS);</code></pre>

## Optimistic UI

Optimistic UI is a little different in the sense that it’s not syncing with the server, like a subscription. When we make a mutation, instead of waiting for another server request, it automatically uses the already inputted data to update the list of pets immediately. Then, once the original data from the server arrives, it will replace the optimistic response. This is also different from “Updating the cache directly using `update` function on the `useMutation`”, even though we are still going to update the cache in this process.

<pre><code class="language-javascript">import React, { useState } from "react";
import gql from "graphql-tag";
import { useQuery, useMutation } from "@apollo/client";
import Loader from "./Loader";
import PetSection from "./PetSection";

//We use ALL_PET to send our nested queries to the server
const ALL_PETS = gql`
  query AllPets {
    pets {
      id
      name
      type
      img
    }
  }
`;

//We use NEW_PET to handle our mutations
const NEW_PET = gql`
  mutation CreateAPet($newPet: NewPetInput!) {
    addPet(input: $newPet) {
      id
      name
      type
      img
    }
  }
`;

function OptimisticPets() {
//We use useQuery to handle the ALL_PETS response and assign it to pets
  const pets = useQuery(ALL_PETS);
//We use useMutation to handle mutations and updating ALL_PETS.
  const [createPet, newPet] = useMutation(NEW_PET
    , {
    update(cache, {data: {addPet}}) {
      const allPets = cache.readQuery({query: ALL_PETS})
      cache.writeQuery({
        query: ALL_PETS,
        data: {pets: [addPet, ...allPets.pets]}
      })
    }
  });;
  const [name, setName] = useState("");
  const type = `DOG`;
 //Handles mutation and creates the optimistic response
  const onSubmit = (input) =&gt; {
    createPet({
      variables: { newPet: input },
      optimisticResponse: {
        __typename: 'Mutation',
        addPet: {
          __typename: 'Pet',
          id: Math.floor(Math.random() * 1000000) + '',
          type: "CAT",
          name: input.name,
          img: 'https://via.placeholder.com/300',
        }
      }
    });
  };

//Here's our submit triggers the onSubmit function
  const submit = (e) =&gt; {
    e.preventDefault();
    onSubmit({ name, type });
  };
//returns the loading the component when the data is still loading
  if (pets.loading ) {
    return &lt;Loader /&gt;;
  }
//loops through the pets and displays them in the PetSection component 
  const petsList = pets.data.pets.map((pet) =&gt; (
    &lt;div className="col-xs-12 col-md-4 col" key={pet.id}&gt;
      &lt;div className="box"&gt;
        &lt;PetSection pet={pet} /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  ));
  return (
    &lt;div&gt;
      &lt;form onSubmit={submit}&gt;
        &lt;input
          className="input"
          type="text"
          placeholder="pet name"
          value={name}
          onChange={(e) =&gt; setName(e.target.value)}
          required
        /&gt;
        &lt;button type="submit" name="submit"&gt;
          add pet
        &lt;/button&gt;
      &lt;/form&gt;
      &lt;div&gt;
        {petsList}
      &lt;/div&gt;
      
    &lt;/div&gt;
  );
}
export default OptimisticPets;</code></pre>

When the code above calls *`onSubmit`*, the Apollo Client cache stores an `addPet` object with the field values specified in `optimisticResponse`. However, it does not overwrite the main cached `pets(ALL_PETS)` with the same cache identifier. Instead, it stores a separate, optimistic version of the object. This ensures that our cached data **remains accurate** if our `optimisticResponse` is wrong.

Apollo Client notifies all active queries that include the modified `pets(ALL_PETS)`. Those queries automatically update, and their associated components re-render to show our optimistic data. This doesn’t require any network requests, so it displays instantly to the user.

Eventually, our server responds to the mutation’s actual to get the correct `addPet` object. Then, Apollo Client cache discards our optimistic version of the `addPet` object. It also overwrites the cached version with values returned from the server.

Apollo Client immediately notifies all affected queries **again**. The concerned components re-render, but if the server’s response matches our `optimisticResponse`, this is entire process is invisible to the user.

{{% ad-panel-leaderboard %}}

## Using Apollo As A State Management Tool On The Client-side

When we think of state management tools or libraries concerning react, redux comes to mind. Interestingly, Apollo can also act as a management tool for our local state. Similar to what we’ve been doing with our API.

### Client-side Schemas And Resolvers

To achieve this, we’ll have to write schemas on the client-side to define the type of data we want and how we want it to be structured. To do this, we’ll create `Client.js` where we’ll define the schemas and resolvers, after which, we’ll make it globally accessible in our project with the Apollo client. 

For this example, I’ll be extending the `User` type that exists already to add `height` as an integer. The resolvers is also added to populate the `height` field in our schema.

<pre><code class="language-javascript">import { ApolloClient } from 'apollo-client'
import { InMemoryCache } from 'apollo-cache-inmemory'
import { ApolloLink } from 'apollo-link'
import { HttpLink } from 'apollo-link-http'
import { setContext } from 'apollo-link-context'
import gql from 'graphql-tag'

//Extending the User type
const typeDefs = gql`
  extend type User {
    height: Int
  }
`

//Declaring our height inside our resolvers within the client-side
const resolvers = {
  User : {
    height() {
      return 35
    }
  }
}
const cache = new InMemoryCache()
const http = new HttpLink({
  uri: 'http://localhost:4000/'
})
const link = ApolloLink.from([
  http
])

const client = new ApolloClient({
  link,
  cache,
  typeDefs,
  resolvers
})
export default client

client.js</code></pre>

We can then import the `client` into our `index.js`:

<pre><code class="language-javascript">import client from "./client"
import {
  ApolloProvider,
} from "@apollo/client";

//importing our client.js file into ApolloProvider
ReactDOM.render(
  &lt;ApolloProvider client={client}&gt;
    &lt;Routing /&gt;
  &lt;/ApolloProvider&gt;,
  document.getElementById("root")
);

index.js</code></pre>

Within the component, it will use it just like this. We add `@client` to indicate that the query is from the client-side, and it should not try to pull it from the server.

<pre><code class="language-javascript">const ALL_PETS = gql`
  query AllPets {
    pets {
      id
      name
      type
      img
      owner {
        id
        height @client
      }
    }
  }
`;</code></pre>

So we’re pulling data from both the server and the client within the same query, and it’ll be accessible through the `useQuery` hook.

## Fragments-Creating Reusable Queries

Sometimes we might need to pull the same query in different components. So instead of hardcoding it multiple times, we assign that query to some sort of variable, and use that variable instead.

In our component we just define the fragment as `PetFields` on `Pet`(which is the Type). That way we can just use it in both our `query` and `mutation`.

<pre><code class="language-javascript">const DUPLICATE_FIELD = gql`
  fragment PetFields on Pet {
      id
      name
      type
      img
  }
`
const ALL_PETS = gql`
  query AllPets {
    pets {
      ...PetFields
    }
  }
  ${DUPLICATE_FIELD}
`;
const NEW_PET = gql`
  mutation CreateAPet($newPet: NewPetInput!) {
    addPet(input: $newPet) {
        ...PetFields
    }
  }
  ${DUPLICATE_FIELD}
`;</code></pre>

## Apollo Directives

When making queries, we might want to have some conditionals that remove or include a field or fragment if a particular condition is fulfilled or not. The default directives include:

`@skip`: Indicates that a field/fragment should be skipped if a condition is fulfilled.

<pre><code class="language-javascript">const ALL_PETS = gql`
  query AllPets($name: Boolean!){
    pets {
      id
      name @skip: (if: $name)
      type
      img
    }
  }
`;</code></pre>

Here `$name` is a boolean that’s added as a variable when we are calling this query. Which is then used with `@skip` to determine when to display the field `name`. If true, it skips, and if falses it resolves that field.

`@includes` also work in a similar manner. If the condition is `true`, that field is resolved and added, and if it’s `false`, it’s not resolved.

We also have `@deprecated` that can be used in `schemas` to retire fields, where you can even add reasons.

We also have [libraries](https://github.com/Saeris/graphql-directives) that allow us to add even more directives, they could prove useful when building somewhat complicated stuff with GraphQL.

## Tips And Tricks With Using GraphQL Lodash Inside Your Queries

[GraphQL Lodash](https://github.com/APIs-guru/graphql-lodash) is a library that can help us a query in a more efficient way, more like an advanced form of the Apollo directives.

It can help you query your server in a way that returns data more neatly and compactly. For instance, you’re querying the `title` of `films` like this:

<pre><code class="language-javascript">films {
  title
}</code></pre>

And it returns the `title` of movies as objects in an array.

<pre><code class="language-javascript">"films": [
    {
      "title" : "Prremier English"
    },
    {
      "title" : "There was a country"
    },
    {
      "title" : "Fast and Furious"
    }
    {
      "title" : "Beauty and the beast"
    }
]</code></pre>

But, when we use lodash’s `map` directive, when can sort of loop through the films array to have a single array with all the titles as direct children. We would send a query our server that looks like this:

<pre><code class="language-javascript">films @_(map: "title") {
  title
}</code></pre>

You’ll get this response which one might consider relatively neater than the previous one.

<pre><code class="language-javascript">"films": [  
  "Premier English",
  "There was a country",
  "Fast and Furious",
  "Beauty and the beast"
]</code></pre>

Another one that proves useful is the is `keyby` directive. You can send a simple query like this:

<pre><code class="language-javascript">people {
  name
  age
  gender
}</code></pre>

Response:

<pre><code class="language-javascript">"people" : [
  {
    "name":  "James Walker",
    "age": "19",
    "gender": "male"
  },
  {
    "name":  "Alexa Walker",
    "age": "19",
    "gender": "female"
  }, 
]</code></pre>

Let’s use `@_keyup` directive in our query:

<pre><code class="language-javascript">people @_(keyBy: "name") {
  name
  age
  gender
}</code></pre>

The response will look just like this:

<pre><code class="language-javascript">"people" : [
  "James Walker" : {
     "name":  "James Walker",
     "age": "19",
     "gender": "male"    
  }
  "Alexa Walker" : {
     "name":  "Alexa Walker",
     "age": "19",
     "gender": "female"
  }
]</code></pre>

So in this case each response has a key, that’s the `name` of the person.

## Conclusion

In this article, we covered advanced topics to achieve real-time update of data using the `update()` function, subscription, and Optimistic UI. All in a bit to improve user experience. 

We also touched upon using GraphQL to manage state on the client-side, and creating resuable queries with GrahQL fragments. The latter allows us to use the same queries in different components where it’s needed without having to repeat the entire thing every time. 

In the end, we went through Apollo directives and Grahql Lodash to help us query our servers in a faster and better way. You can also check out [Scott Moss’s tutorial](https://frontendmasters.com/courses/client-graphql-react/) if you’re looking to cover Graphql and react from scratch.

{{< signature "vf, yk, il" >}}
