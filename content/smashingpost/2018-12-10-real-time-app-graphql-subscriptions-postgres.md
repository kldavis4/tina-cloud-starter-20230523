---
title: 'How To Build A Real-Time App With GraphQL Subscriptions On Postgres'
slug: real-time-app-graphql-subscriptions-postgres
author: sandip-devarkonda
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47d7cfa2-b5ed-4b63-bfb5-1b21adfb7b5a/poll-app-traditional-design.png
date: 2018-12-10T14:00:23+01:00
summary: >-
  Building real-time applications is hard. However, GraphQL is rapidly upending this status-quo. Let’s explore what GraphQL is, and then take it for a spin by building a poll app in which users can vote and on-screen aggregated results are updated in real time.
description: >-
  Building real-time applications is hard. However, GraphQL is rapidly upending this status-quo. Let’s explore what GraphQL is, and then take it for a spin by building a poll app.
categories:
  - Apps
  - JavaScript
  - GraphQL
---
<p>In this article, we’ll take a look at the challenges involved in building real-time applications and how emerging tooling is addressing them with elegant solutions that are easy to reason about. To do this, we’ll build a real-time polling app (like a Twitter poll with real-time overall stats) just by using Postgres, GraphQL, React and no backend code!</p>

<p>The primary focus will be on setting up the backend (deploying the ready-to-use tools, schema modeling), and aspects of frontend integration with GraphQL and less on UI/UX of the frontend (some knowledge of ReactJS will help). The tutorial section will take a paint-by-numbers approach, so we’ll just clone a GitHub repo for the schema modeling, and the UI and tweak it, instead of building the entire app from scratch.</p>

<div class="c-felix-the-cat">
<h4 class="h3">All Things GraphQL</h4>
<p>Do you know everything you need to know about GraphQL? If you have your doubts, Eric Baer has you covered with a detailed guide on its origins, its drawbacks and the basics of how to work with it. <a href="https://www.smashingmagazine.com/2018/01/graphql-primer-new-api-part-1/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

<p>Before you continue reading this article, I’d like to mention that a working knowledge of the following technologies (or substitutes) are beneficial:</p>

<ul>
<li><strong>ReactJS</strong><br />This can be replaced with any frontend framework, Android or IOS by following the client library documentation.</li>
<li><strong>Postgres</strong><br />You can work with other databases but with different tools, the principles outlined in this post will still apply.</li>
</ul>

<p>You can also adapt this tutorial context for other real-time apps very easily.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354852fd-02b3-4b9d-82ba-649853ee564e/real-time-poll-app-800w.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354852fd-02b3-4b9d-82ba-649853ee564e/real-time-poll-app-800w.gif" width="800" height="450" alt="A demonstration of the features in the polling app that is built in this tutorial" /></a><figcaption>A demonstration of the features in the polling app that we’ll be building. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354852fd-02b3-4b9d-82ba-649853ee564e/real-time-poll-app-800w.gif">Large preview</a>)</figcaption></figure>

<p>As illustrated by the accompanying GraphQL payload at the bottom, there are three major features that we need to implement:</p>

<ol>
<li>Fetch the poll question and a list of options (top left).</li>
<li>Allow a user to vote for a given poll question (the “Vote” button).</li>
<li>Fetch results of the poll in real-time and display them in a bar graph (top right; we can gloss over the feature to fetch a list of currently online users as it’s an exact replica of this use case).</li>
</ol>

{{% feature-panel %}}

## Challenges With Building Real-Time Apps

<p>Building real-time apps (especially as a frontend developer or someone who’s recently made a transition to becoming a fullstack developer), is a hard engineering problem to solve.

This is generally how contemporary real-time apps work (in the context of our example app):</p>

<ol>
<li>The frontend updates a database with some information; A user’s vote is sent to the backend, i.e. poll/option and user information (<code>user_id</code>, <code>option_id</code>).</li>
<li>The first update triggers another service that aggregates the poll data to render an output that is relayed back to the app in real-time (every time a new vote is cast by anyone; if this done efficiently, only the updated poll’s data is processed and only those clients that have subscribed to this poll are updated):

<ul>
<li>Vote data is first processed by an <code>register_vote</code> service (assume that some validation happens here) that triggers a <code>poll_results</code> service.</li>
<li>Real-time aggregated poll data is relayed by the <code>poll_results</code> service to the frontend for displaying overall statistics.</li>
</ul>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47d7cfa2-b5ed-4b63-bfb5-1b21adfb7b5a/poll-app-traditional-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47d7cfa2-b5ed-4b63-bfb5-1b21adfb7b5a/poll-app-traditional-design.png" sizes="100vw" caption="A poll app designed traditionally" alt="Traditional design for a real-time poll app" >}}

<p>This model is derived from a traditional API-building approach, and consequently has similar problems:</p>

<ol>
<li>Any of the sequential steps could go wrong, leaving the UX hanging and affecting other independent operations.</li>
<li>Requires a lot of effort on the API layer as it’s a single point of contact for the frontend app, that interacts with multiple services. It also needs to implement a websockets-based real-time API &mdash; there is no universal standard for this and therefore sees limited support for automation in tools.</li>
<li>The frontend app is required to add the necessary plumbing to consume the real-time API and may also have to solve the data consistency problem typically seen in real-time apps (less important in our chosen example, but critical in ordering messages in a real-time chat app).</li>
<li>Many implementations resort to using additional non-relational databases on the server-side (Firebase, etc.) for easy real-time API support.</li>
</ol>

<p>Let’s take a look at how GraphQL and associated tooling address these challenges.</p>

{{% ad-panel-leaderboard %}}

## What Is GraphQL?

<p>GraphQL is a specification for a query language for APIs, and a server-side runtime for executing queries. This specification was developed by Facebook to accelerate app development and provide a standardized, database-agnostic data access format. Any specification-compliant GraphQL server must support the following:</p>

<ol>
<li><strong>Queries for reads</strong><br /> A request type for requesting nested data from a data source (which can be either one or a combination of a database, a REST API or another GraphQL schema/server).</li>
<li><strong>Mutations for writes</strong><br />A request type for writing/relaying data into the aforementioned data sources.</li>
<li><strong>Subscriptions for live-queries</strong><br />A request type for clients to subscribe to real-time updates.</li>
</ol>

<p>GraphQL also uses a typed schema. The ecosystem has plenty of tools that help you identify errors at dev/compile time which results in fewer runtime bugs.</p>

<p>Here’s why GraphQL is great for real-time apps:</p>

<ul>
<li>Live-queries (subscriptions) are an implicit part of the GraphQL specification. Any GraphQL system has to have native real-time API capabilities.</li>
<li>A standard spec for real-time queries has consolidated community efforts around client-side tooling, resulting in a very intuitive way of integrating with GraphQL APIs.</li>
</ul>

<p>GraphQL and a combination of open-source tooling for database events and serverless/cloud functions offer a great substrate for building cloud-native applications with asynchronous business logic and real-time features that are easy to build and manage. This new paradigm also results in great user and developer experience.</p>

<p>In the rest of this article, I will use open-source tools to build an app based on this architecture diagram:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/605a4010-002d-49c5-8219-1147f275b4a3/poll-app-graphql-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/605a4010-002d-49c5-8219-1147f275b4a3/poll-app-graphql-design.png" sizes="100vw" caption="A poll app designed with GraphQL" alt="GraphQL-based design for a real-time poll app" >}}

## Building A Real-Time Poll/Voting App

<p>With that introduction to GraphQL, let’s get back to building the polling app as described in the first section.</p>

<p>The three features (or stories highlighted) have been chosen to demonstrate the different GraphQL requests types that our app will make:</p>

<ol>
	<li><strong>Query</strong><br />Fetch the poll question and its options.</li>
	<li><strong>Mutation</strong><br />Let a user cast a vote.</li>
	<li><strong>Subscription</strong><br />Display a real-time dashboard for poll results.</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72306f74-09c6-4f52-bfd0-2c9fec9da118/poll-app-graphql-elements.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72306f74-09c6-4f52-bfd0-2c9fec9da118/poll-app-graphql-elements.png" sizes="100vw" caption="GraphQL request types in the poll app (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72306f74-09c6-4f52-bfd0-2c9fec9da118/poll-app-graphql-elements.png'>Large preview</a>)" alt="GraphQL elements in the poll app" >}}

### Prerequisites

<ul>
	<li><strong>A Heroku account</strong> (use the free tier, no credit card required)<br />To deploy a GraphQL backend (see next point below) and a Postgres instance.</li>
	<li><strong>Hasura GraphQL Engine</strong> (free, open-source)</br />A ready-to-use GraphQL server on Postgres.</li>
	<li><strong>Apollo Client</strong> (free, open-source SDK)<br />For easily integrating clients apps with a GraphQL server.</li>
	<li><strong>npm</strong> (free, open-source package manager)<br />To run our React app.</li>
</ul>

{{% ad-panel-leaderboard %}}

### Deploying The Database And A GraphQL Backend

<p>We will deploy an instance each of Postgres and GraphQL Engine on Heroku’s free tier. We can use a nifty Heroku button to do this with a single click.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74adceef-4c53-4de5-94b3-346fcf56d7ef/how-to-build-a-real-time-app.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74adceef-4c53-4de5-94b3-346fcf56d7ef/how-to-build-a-real-time-app.png" width="147" height="32" alt="Heroku button" /></a><figcaption>Heroku button</figcaption></figure>

<p><strong>Note:</strong> <em>You can also follow this <a href="https://heroku.com/deploy?template=https://github.com/hasura/graphql-engine-heroku">link</a> or search for documentation Hasura GraphQL deployment for Heroku (or other platforms).</em></p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/226dddbc-ebfb-4ccf-84c3-fb3dc1e487db/deploy-hge-realtime-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/226dddbc-ebfb-4ccf-84c3-fb3dc1e487db/deploy-hge-realtime-app.png" sizes="100vw" caption="Deploying Postgres and GraphQL Engine to Heroku’s free tier (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/226dddbc-ebfb-4ccf-84c3-fb3dc1e487db/deploy-hge-realtime-app.png'>Large preview</a>)" alt="Deploying app backend to Heroku’s free tier" >}}

<p>You will not need any additional configuration, and you can just click on the “Deploy app” button. Once the deployment is complete, make a note of the app URL:</p>

<pre><code class="language-bash">&lt;app-name&gt;.herokuapp.com
</code></pre>

<p>For example, in the screenshot above, it would be:</p>

<pre><code class="language-bash">hge-realtime-app-tutorial.herokuapp.com
</code></pre>

<p>What we’ve done so far is deploy an instance of Postgres (as an add-on in Heroku parlance) and an instance of GraphQL Engine that is configured to use this Postgres instance. As a result of doing so, we now have a ready-to-use GraphQL API but, since we don’t have any tables or data in our database, this is not useful yet. So, let’s address this immediately.</p>

### Modeling the database schema

<p>The following schema diagram captures a simple relational database schema for our poll app:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6796af2f-9933-45bd-b91a-df57adf5b8a9/schema-design-realtime-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6796af2f-9933-45bd-b91a-df57adf5b8a9/schema-design-realtime-app.png" sizes="100vw" caption="Schema design for the poll app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6796af2f-9933-45bd-b91a-df57adf5b8a9/schema-design-realtime-app.png'>Large preview</a>)" alt="Schema design for the poll app" >}}

<p>As you can see, the schema is a simple, normalized one that leverages foreign-key constraints. It is these constraints that are interpreted by the GraphQL Engine as 1:1 or 1:many relationships (e.g. <code>poll:options</code> is a 1: many relationship since each poll will have more than 1 option that are linked by the foreign key constraint between the <code>id</code> column of the <code>poll</code> table and the <code>poll_id</code> column in the <code>option</code> table). Related data can be modelled as a graph and can thus power a GraphQL API. This is precisely what the GraphQL Engine does.</p>

<p>Based on the above, we’ll have to create the following tables and constraints to model our schema:</p>

<ol>
<li><code>Poll</code><br />A table to capture the poll question.</li>
<li><code>Option</code><br />Options for each poll.</li>
<li><code>Vote</code><br />To record a user’s vote.</li>
<li>Foreign-key constraint between the following fields (<code>table : column</code>):
<ul>
<li><code>option : poll_id → poll : id</code></li>
<li><code>vote : poll_id  → poll : id</code></li>
<li><code>vote : created_by_user_id → user : id</code></li>
</ul>

</li>
</ol>

<p>Now that we have our schema design, let’s implement it in our Postgres database. To instantly bring this schema up, here’s what we’ll do:</p>

<ol>
<li><a href="https://docs.hasura.io/1.0/graphql/manual/hasura-cli/install-hasura-cli.html">Download</a> the GraphQL Engine CLI.</li>
<li>Clone this repo:<br />
<div class="break-out">

<pre><code class="language-bash">$ git clone clone https://github.com/hasura/graphql-engine

$ cd graphql-engine/community/examples/realtime-poll</code></pre></div>
</li>
<li>Go to <code>hasura/</code> and edit <code>config.yaml</code>:<br />

<pre><code class="language-bash">endpoint: https://&lt;app-name&gt;.herokuapp.com</code></pre>
</li>
<li>Apply the migrations using the CLI, from inside the project directory (that you just downloaded by cloning):<br />

<pre><code class="language-bash">$ hasura migrate apply</code></pre>
</li>
</ol>

<p>That’s it for the backend. You can now open the GraphQL Engine console and check that all the tables are present (the console is available at <code>https://&lt;app-name&gt;.herokuapp.com/console</code>).</p>

<p><strong>Note:</strong> <em>You could also have used the console to implement the schema by creating individual tables and then adding constraints using a UI. Using the built-in support for migrations in GraphQL Engine is just a convenient option that was available because our sample repo has migrations for bringing up the required tables and configuring relationships/constraints (this is also highly recommended regardless of whether you are building a hobby project or a production-ready app).</em></p>

### Integrating The Frontend React App With The GraphQL Backend

<p>The frontend in this tutorial is a simple app that shows poll question, the option to vote and the aggregated poll results in one place. As I mentioned earlier, we’ll first focus on running this app so you get the instant gratification of using our recently deployed GraphQL API , see how the GraphQL concepts we looked at earlier in this article power the different use-cases of such an app, and then explore how the GraphQL integration works under the hood.</p>

<p><strong>NOTE:</strong> <em>If you are new to ReactJS, you may want to check out some of <a href="https://www.smashingmagazine.com/category/react/">these articles</a>. We won’t be getting into the details of the React part of the app, and instead, will focus more on the GraphQL aspects of the app. You can refer to the source code in the repo for any details of how the React app has been built</em>.</p>

#### Configuring The Frontend App

<ol>
<li>In the repo cloned in the previous section, edit <code>HASURA_GRAPHQL_ENGINE_HOSTNAME</code> in the <em>src/apollo.js</em> file (inside the <code>/community/examples/realtime-poll</code> folder) and set it to the Heroku app URL from above:<br />
<div class="break-out">

<pre><code class="language-javascript">export const HASURA_GRAPHQL_ENGINE_HOSTNAME = 'random-string-123.herokuapp.com';</code></pre></div>
</li>
<li>Go to the root of the repository/app-folder (<code>/realtime-poll/</code>) and use npm to install the prequisite modules and then run the app:<br />

<pre><code class="language-bash">$ npm install

$ npm start
</code></pre>
</code></pre>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/399070ab-e84f-4854-9e99-bb108b7b9b03/screenshot-realtime-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/399070ab-e84f-4854-9e99-bb108b7b9b03/screenshot-realtime-app.png" sizes="100vw" caption="Screenshot of the live poll app (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/399070ab-e84f-4854-9e99-bb108b7b9b03/screenshot-realtime-app.png'>Large preview</a>)" alt="Screenshot of the live poll app" >}}

<p>You should be able to play around with the app now. Go ahead and vote as many times as you want, you’ll notice the results changing in real time. In fact, if you set up another instance of this UI and point it to the same backend, you’ll be able to see results aggregated across all the instances.</p>

<p>So, how does this app use GraphQL? Read on.</p>

## Behind The Scenes: GraphQL

<p>In this section, we’ll explore the GraphQL features powering the app, followed by a demonstration of the ease of integration in the next one.</p>

### The Poll Component And The Aggregated Results Graph

<p>The poll component on the top left that fetches a poll with all of its options and captures a user’s vote in the database. Both of these operations are done using the GraphQL API. For fetching a poll’s details, we make a query (remember this from the GraphQL introduction?):</p>

<pre><code class="language-bash">query {
  poll {
    id
    question
    options {
      id
      text
    }
  }
}
</code></pre>

<p>Using the Mutation component from <code>react-apollo</code>, we can wire up the mutation to a HTML form such that the mutation is executed using variables <code>optionId</code> and <code>userId</code> when the form is submitted:</p>

<div class="break-out">

<pre><code class="language-javascript">mutation vote($optionId: uuid!, $userId: uuid!) {
  insert_vote(objects: [{option_id: $optionId, created_by_user_id: $userId}]) {
    returning {
      id
    }
  }
}
</code></pre></div>

<p>To show the poll results, we need to derive the count of votes per option from the data in vote table. We can create a Postgres View and track it using GraphQL Engine to make this derived data available over GraphQL.</p>

<div class="break-out">

<pre><code class="language-javascript">CREATE VIEW poll_results AS
 SELECT poll.id AS poll_id, o.option_id, count(*) AS votes
 FROM (( SELECT vote.option_id, option.poll_id, option.text
   FROM ( vote
          LEFT JOIN 
      public.option ON ((option.id = vote.option_id)))) o

           LEFT JOIN poll ON ((poll.id = o.poll_id)))
 GROUP BY poll.question, o.option_id, poll.id;
</code></pre></div>

<p>The <code>poll_results</code> view joins data from <code>vote</code> and <code>poll</code> tables to provide an aggregate count of number of votes per each option.</p>

<p>Using GraphQL Subscriptions over this view, <a href="https://www.npmjs.com/package/react-google-charts">react-google-charts</a> and the subscription component from <code>react-apollo</code>, we can wire up a reactive chart which updates in realtime when a new vote happens from any client.</p>

<pre><code class="language-javascript">subscription getResult($pollId: uuid!) {
  poll_results(where: {poll_id: {_eq: $pollId}}) {
    option {
      id
      text
    }
    votes
  }
}
</code></pre>

### GraphQL API Integration

<p>As I mentioned earlier, I used Apollo Client, an open-source SDK to integrate a ReactJS app with the GraphQL backend. Apollo Client is analogous to any HTTP client library like <a href="https://docs.python-requests.org/en/master/">requests for python</a>, the standard <a href="https://nodejs.org/api/http.html">http module for JavaScript</a>, and so on. It encapsulates the details of making an HTTP request (in this case POST requests). It uses the configuration (specified in <code>src/apollo.js</code>) to make query/mutation/subscription requests (specified in <em>src/GraphQL.jsx</em> with the option to use variables that can be dynamically substituted in the JavaScript code of your REACT app) to a GraphQL endpoint. It also leverages the typed schema behind the GraphQL endpoint to provide compile/dev time validation for the aforementioned requests. Let’s see just how easy it is for a client app to make a live-query (subscription) request to the GraphQL API.</p>

#### Configuring The SDK

<p>The Apollo Client SDK needs to be pointed at a GraphQL server, so it can automatically handle the boilerplate code typically needed for such an integration. So, this is exactly what we did when we modified <em>src/apollo.js</em> when setting up the frontend app.</p>

#### Making A GraphQL Subscription Request (Live-Query)

<p>Define the subscription we looked at in the previous section in the <em>src/GraphQL.jsx</em> file:</p>

<pre><code class="language-javascript">const SUBSCRIPTION_RESULT = `
subscription getResult($pollId: uuid!) {
  poll_results (
    order_by: option_id_desc,
    where: { poll_id: {_eq: $pollId} }
  ) {
    option_id
    option { id text }
    votes
  }
}`;
</code></pre>

<p>We’ll use this definition to wire up our React component:</p>

<div class="break-out">

<pre><code class="language-javascript">export const Result = (pollId) => (
  &lt;Subscription subscription={gql`${SUBSCRIPTION_RESULT}`} variables={pollId}>
    {({ loading, error, data }) => {
       if (loading) return <p>Loading...&lt;/p>;
       if (error) return <p>Error :&lt;/p>;
       return (
         &lt;div>
           &lt;div>
             {renderChart(data)}
           &lt;/div>
         &lt;/div>
       );
    }}
  &lt;/Subscription>
)
</code></pre></div>

<p>One thing to note here is that the above subscription could also have been a query.  Merely replacing one keyword for another gives us a “live-query”, and that’s all it takes for the Apollo Client SDK to hook this real-time API with your app. Every time there’s a new dataset from our live-query, the SDK triggers a re-render of our chart with this updated data (using the <code>renderChart(data)</code> call). That’s it. It really is that simple!</p>

## Final Thoughts

<p>In three simple steps (creating a GraphQL backend, modeling the app schema, and integrating the frontend with the GraphQL API), you can quickly wire-up a fully-functional real-time app, without getting mired in unnecessary details such as setting up a websocket connection. That right there is the power of community tooling backing an abstraction like GraphQL.</p>

<p>If you’ve found this interesting and want to explore GraphQL further for your next side project or production app, here are some factors you may want to use for building your GraphQL toolchain:</p>

<ul>
<li><strong>Performance & Scalability</strong><br />GraphQL is meant to be consumed directly by frontend apps (it’s no better than an ORM in the backend; real productivity benefits come from doing this). So your tooling needs to be smart about efficiently using database connections and should be able scale effortlessly.</li>
<li><strong>Security</strong><br />It follows from above that a mature role-based access-control system is needed to authorize access to data.</li>
<li><strong>Automation</strong><br />If you are new to the GraphQL ecosystem, handwriting a GraphQL schema and implementing a GraphQL server may seem like daunting tasks. Maximize the automation from your tooling so you can focus on the important stuff like building user-centric frontend features.</li>
<li><strong>Architecture</strong></br />As trivial as the above efforts seem like, a production-grade app’s backend architecture may involve advanced GraphQL concepts like schema-stitching, etc. Moreover, the ability to easily generate/consume real-time APIs opens up the possibility of building asynchronous, reactive apps that are resilient and inherently scalable. Therefore, it’s critical to evaluate how GraphQL tooling can streamline your architecture.</li>
</ul>

### Related Resources

<ul>
<li>You can check out a live version of the app over <a href="https://shahidh.in/hasura-realtime-poll/">here</a>.</li>
<li>The complete source code is available on <a href="https://github.com/hasura/graphql-engine/tree/master/community/examples/realtime-poll">GitHub</a>.</li>
<li>If you’d like to explore the database schema and run test GraphQL queries, you can do so over <a href="https://hasura-realtime-dashboard.herokuapp.com/console/data/schema/public">here</a>.</li>
</ul>

{{< signature "rb, ra, yk, il" >}}
