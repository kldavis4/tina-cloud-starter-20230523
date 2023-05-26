---
title: 'Building Real-Time Charts With GraphQL And Postgres'
slug: realtime-charts-graphql-postgres
author: rishichandra-wawhal
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f1db83-c44a-4857-8029-a2819ee51663/realtime-charts-graphql-postgres-create-react-app-start.png
date: 2019-03-27T13:00:08+01:00
summary: >-
  There is no better way to understand data than by visualizing it with charts and diagrams. The JS community has some great open-source projects that make data visualization easier, however, there has not been a go-to solution for building real-time backends that can back these charts and make them real-time. With [GraphQL](https://graphql.org) (which has a well-defined spec for real-time subscriptions), we can get a real-time backend running within seconds and use it to power real-time charts.
description: >-
  There is no better way to understand data than by visualizing it with charts and diagrams. Luckily for us, the JS community has some great open-source projects that make data visualization easier.
categories:
  - JavaScript
  - GraphQL
  - Visualizations
---
Charts form an integral part of any industry that deals with data. Charts are useful in the voting and polling industry, and they’re also great at helping us better understand the different behaviors and characteristics of the users and clients we work with.

Why are real-time charts so important? Well, they’re useful in cases when new data is produced continuously; for example, when using live-time series for visualizing stock prices is a great use for real-time charts. In this tutorial, I’ll explain how to build real-time charts with open-source technologies apt for exactly this particular task.

**Note**: *This tutorial requires basic knowledge of React and GraphQL.*

### Stack

1. [PostgreSQL](https://www.postgresql.org/)  
The very point behind using Charts is to visualize "huge" volumes data. We, therefore, need a database that efficiently handles large data and provides an intuitive API to restructure it. SQL databases allow us to make views that abstract and aggregate data for us. We will be using Postgres which is a [time-tested](https://www.postgresql.org/docs/9.2/history.html) and highly efficient database. It also has fancy open-source extensions like [Timescale](https://www.timescale.com) and [PostGIS](https://postgis.net/) which allow us to build geolocation-based and time-series-based charts respectively. We will be using Timescale for building our time series chart.
2. [GraphQL Engine](https://hasura.io)  
This post is about building real-time charts, and GraphQL comes with a well-defined spec for real-time subscriptions. Hasura GraphQL Engine is an [open-source](https://github.com/hasura/graphql-engine) GraphQL server that takes a Postgres connection and allows you to query the Postgres data over realtime GraphQL. It also comes with an access control layer that helps you restrict your data based on custom access control rules.
3. [ChartJS](https://www.chartjs.org)  
ChartJS is a popular and well maintained open source library for building charts with JavaScript. We will use `chart.js` along with its ReactJS abstraction `react-chartjs-2`. About why React, it is because React empowers developers with an intuitive event-driven API. Also, React’s unidirectional data flow is ideal for building charts that are data-driven.

{{% feature-panel %}}

### Requirements

For this tutorial, you will need the following on your system:

1. [Docker CE](www.docker.com)  
Docker is a software that lets you containerize your applications. A docker image is an independent packet that contains software along with its dependencies and a minimalistic operating system. Such docker images can be technically run in any machine that has docker installed. You will need docker for this tutorial.
    - [Read more about Docker](https://www.docker.com/get-started)
    - [Install Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
2. [npm](www.npmjs.com): npm is the package manage for JavaScript.

### Demo

We will build the following live time series chart that shows the maximum temperature of a location in intervals of 5 seconds over the past 20 minutes from the present moment.

<figure><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8d4cdf3-0456-4b1d-a4df-bd933304a375/realtime-charts-graphql-postgres-demo.gif" alt="GIF Demo of the realtime chart" /><figcaption>GIF Demo of the realtime chart</figcaption></figure>

## Setting Up The Backend

### Running The Services

The backend comprises of a Postgres database, its timescale extension, and Hasura GraphQL Engine. Let us get the database and our GraphQL server running by running the respective docker images. Create a file called `docker-compose.yaml` and paste this content into it.

**Note**: `docker-compose` *is a utility to run multiple docker images declaratively.*

<div class="break-out">

 <pre><code class="language-yaml">version: '2'
services:
  timescale:
    image: timescale/timescaledb:latest-pg10
    restart: always
    environment:
      POSTGRES_PASSWORD: postgrespassword
    volumes:
    - db_data:/var/lib/postgresql/data
  graphql-engine:
    image: hasura/graphql-engine:v1.0.0-alpha38
    ports:
    - "8080:8080"
    depends_on:
    - "timescale"
    restart: always
    environment:
      HASURA_GRAPHQL_DATABASE_URL: postgres://postgres:postgrespassword@timescale:5432/postgres
      HASURA_GRAPHQL_ACCESS_KEY: mylongsecretkey
    command:
      - graphql-engine
      - serve
      - --enable-console
volumes:
  db_data:
</code></pre>
</div>

This `docker-compose.yaml` contains the spec for two services:

1. `timescale`  
This is our Postgres database with Timescale extension installed. It is configured to run at port 5432.
2. `graphql-engine`  
This is our Hasura GraphQL Engine instance, i.e. the GraphQL server that points to the database and gives GraphQL APIs over it. It is configured to run at the port 8080, and the port 8080 is mapped to the port 8080 of the machine that this docker container runs on. This means that you can access this GraphQL server through at `localhost:8080` of the machine.

Let’s run these docker containers by running the following command wherever you have placed your `docker-compose.yaml`.

<pre><code class="language-bash">docker-compose up -d
</code></pre>

This command pulls the docker images from the cloud and runs them in the given order. It might take a few seconds based on your internet speed. Once it is complete, you can access your GraphQL Engine console at `https://localhost:8080/console`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1baeaf-4b1b-40e2-932b-5efe334e9eda/realtime-charts-graphql-postgres-console-landing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1baeaf-4b1b-40e2-932b-5efe334e9eda/realtime-charts-graphql-postgres-console-landing.png" sizes="100vw" caption="Hasura GraphQL Engine console (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1baeaf-4b1b-40e2-932b-5efe334e9eda/realtime-charts-graphql-postgres-console-landing.png'>Large preview</a>)" alt="Hasura GraphQL Engine Console" >}}

### Setting Up The Database

Next, let us create a table called temperature that stores the values of temperatures at different times. Go to the Data tab in the console and go to the `SQL` section. Create our `temperature` table by running this SQL block:

<pre><code class="language-sql">CREATE TABLE temperature (
  temperature numeric not null,
  location text not null,
  recorded_at timestamptz not null default now()
);
</code></pre>

This creates a simple Postgres table in the database. But we wish to leverage the time interval partitioning of the Timescale extension. To do this, we must convert this table into timescale’s hypertable by running the SQL command:

<pre><code class="language-sql">SELECT create_hypertable('temperature', 'recorded_at');
</code></pre>

This command creates a hypertable that is partitioned by time in the field `recorded_at`.

Now, since this table is created, we can directly start making GraphQL queries over it. You can try them out by clicking on the `GraphiQL` tab on top. Try making a mutation first:

<pre><code class="language-graphql">mutation {
  insert_temperature (
    objects: [{
      temperature: 13.4
      location: "London"
    }]
  ) {
    returning {
      recorded_at
      temperature
    }
  }
}
</code></pre>

The GraphQL mutation above inserts a row in the `temperature` table. Now try to make a GraphQL query to check if the data was inserted.

Then try making a query:

<pre><code class="language-graphql">query {
  temperature {
    recorded_at
    temperature
    location
  }
}
</code></pre>

Hope it worked :)

Now, the task at our hand is to create a live time-series chart that shows the maximum temperature of a location in intervals of 5 seconds over the past 20 minutes from the present moment. Let’s create a view that gives us exactly this data.

<pre><code class="language-sql">CREATE VIEW last_20_min_temp AS (
  SELECT time_bucket('5 seconds', recorded_at) AS five_sec_interval,
  location,     
    MAX(temperature) AS max_temp
  FROM temperature
  WHERE recorded_at > NOW() - interval '20 minutes'    
  GROUP BY five_sec_interval, location    
  ORDER BY five_sec_interval ASC
);
</code></pre>

This view groups the data from the `temperature` table in 5-second windows with their max temperature (`max_temp)`. The secondary grouping is done using the `location` field. All this data is only from the past twenty minutes from the present moment.

That’s it. Our backend is set up. Let us now build a nice real-time chart.

{{% ad-panel-leaderboard %}}

## Frontend

### Hello GraphQL Subscriptions

GraphQL subscriptions are essentially "live" GraphQL queries. They operate over WebSockets and have exactly the same response structure like GraphQL queries. Go back to `https://localhost:8080/console` and try to make a GraphQL subscription to the view we created.

<pre><code class="language-graphql">subscription {
  last_20_min_temp(
    order_by: {
      five_sec_interval: asc
    }
    where: {
      location: {
        _eq: "London"
      }
    }
  ) {
    five_sec_interval
    location
    max_temp
  }
}
</code></pre>

This subscription subscribes to the data in the view where the location is `London` and it is ordered in ascending order of the `five_second_intervals`.

Naturally, the response from the view would be an empty array because we have not inserted anything in the database in the past twenty minutes. (You might see the entry that we inserted sometime back if you reached this section within twenty minutes.)

<pre><code class="language-json">{
  "data": {
    "last_20_min_temp": []
  }
}
</code></pre>

Keeping this subscription on, open another tab and try inserting another value in the `temperatures` table using the same mutation that we performed earlier. After inserting, if you go back to the tab where the subscription was on, you would see the response having updated automatically. That’s the realtime magic that GraphQL Engine provides. Let’s use this subscription to power our real-time chart.

### Getting Started With Create-React-App

Let us quickly get started with a React app starter using [create react app](https://github.com/facebook/create-react-app). Run the command:

<pre><code class="language-bash">npx create-react-app time-series-chart
</code></pre>

This will create an empty starter project. `cd` into it and install the GraphQL and chart libraries. Also, install [moment](https://momentjs.com/) for converting timestamps to a human-readable format.

<div class="break-out">

 <pre><code class="language-bash">cd time-series-chart
npm install --save apollo-boost apollo-link-ws subscriptions-transport-ws graphql react-apollo chart.js react-chartjs-2 moment
</code></pre>
</div>

Finally, run the app with `npm start` and a basic React app would open up at `https://localhost:3000`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f1db83-c44a-4857-8029-a2819ee51663/realtime-charts-graphql-postgres-create-react-app-start.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f1db83-c44a-4857-8029-a2819ee51663/realtime-charts-graphql-postgres-create-react-app-start.png" sizes="100vw" caption="Raw creat-react-app (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f1db83-c44a-4857-8029-a2819ee51663/realtime-charts-graphql-postgres-create-react-app-start.png'>Large preview</a>)" alt="Raw create-react-app" >}}

### Setting Up Apollo Client For Client-Side GraphQL

[Apollo client](https://www.apollographql.com/docs/react/) is currently the best GraphQL client that works with any GraphQL compliant server. Relay modern is good too but the server must support the relay spec to leverage all the benefits of Relay modern. We’ll use Apollo client for client-side GraphQL for this tutorial. Let us perform the setup to provide Apollo client to the app.

I am not getting into the subtleties of this setup because the following code snippets are [taken directly from the docs](https://www.apollographql.com/docs/react/advanced/subscriptions.html#subscriptions-client). Head to `src/index.js` in the React app directory and instantiate Apollo client and add this code snippet above `ReactDOM.render`.

<pre><code class="language-javascript">import { WebSocketLink } from 'apollo-link-ws';
import { ApolloClient } from 'apollo-client';
import { ApolloProvider } from 'react-apollo';
import { InMemoryCache } from 'apollo-cache-inmemory';

// Create a WebSocket link:
const link = new WebSocketLink({
  uri: `ws://localhost:8080/v1alpha1/graphql`,
  options: {
    reconnect: true,
    connectionParams: {
      headers: {
        "x-hasura-admin-secret: "mylongsecretkey"
      }
    }
  }
})
const cache = new InMemoryCache();
const client = new ApolloClient({
  link,
  cache
});
</code></pre>

Finally, wrap the `App` inside `ApolloProvider` so that we can use Apollo client in the children components. Your `App.js` should finally look like:

<pre><code class="language-javascript">import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { WebSocketLink } from 'apollo-link-ws';
import { ApolloClient } from 'apollo-client';
import { ApolloProvider } from 'react-apollo';
import { InMemoryCache } from 'apollo-cache-inmemory';

// Create a WebSocket link:
const link = new WebSocketLink({
  uri: `ws://localhost:8080/v1alpha1/graphql`,
  options: {
    reconnect: true,
    connectionParams: {
      headers: {
        "x-hasura-admin-secret: "mylongsecretkey"
      }
    }
  }
})
const cache = new InMemoryCache();
const client = new ApolloClient({
  link,
  cache
});

ReactDOM.render(
  (
    &lt;ApolloProvider client={client}&gt; 
      &lt;App /&gt;
    &lt;/ApolloProvider&gt;
  ),
  document.getElementById('root')
);
</code></pre>

Apollo client has been set up. We can now easily use real-time GraphQL from our App. Head to `src/App.js`.

{{% ad-panel-leaderboard %}}

### Building The Chart

ChartJS provides a pretty neat API for building charts. We will be building a line chart; so a line chart expects data of the form:

<pre><code class="language-json">{
  "labels": ["label1", "label2", "label3", "label4"],
  "datasets": [{
    "label": "Sample dataset",
    "data": [45, 23, 56, 55],
    "pointBackgroundColor": ["red", "brown", "green", "yellow"],
    "borderColor": "brown",
    "fill": false
  }],
}
</code></pre>

If the above dataset is used for rendering a line chart, it would look something like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3e7b9bf-129d-44c7-9f32-dd1b2af0129f/realtime-charts-graphql-postgres-line-chart-sample.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3e7b9bf-129d-44c7-9f32-dd1b2af0129f/realtime-charts-graphql-postgres-line-chart-sample.png" sizes="100vw" caption="Sample line chart (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3e7b9bf-129d-44c7-9f32-dd1b2af0129f/realtime-charts-graphql-postgres-line-chart-sample.png'>Large preview</a>)" alt="Sample line chart" >}}

Let us try to build this sample chart first. Import `Line` from `react-chartjs-2` and render it passing the above object as a data prop. The render method would look something like:

<div class="break-out">

 <pre><code class="language-javascript">render() {
  const data = {
    "labels": ["label1", "label2", "label3", "label4"],
    "datasets": [{
      "label": "Sample dataset",
      "data": [45, 23, 56, 55],
      "pointBackgroundColor": ["red", "brown", "green", "yellow"],
      "borderColor": "brown",
      "fill": false
    }],
  }
  return (
    &lt;div
      style={{display: 'flex', alignItems: 'center', justifyContent: 'center', margin: '20px'}}
    &gt;
      &lt;Line
        data={data}
      /&gt;
    &lt;/div&gt;
  );
}
</code></pre>
</div>

Next, we will subscribe to the data in our view and feed it to the Line chart. But how do we perform subscriptions on the client?

[Apollo’s `<Subscription>` components](https://www.apollographql.com/docs/react/advanced/subscriptions.html#subscription-component) work using the [render prop](https://reactjs.org/docs/render-props.html) pattern where the children of a component are rendered with the context of the subscription data.

<pre><code class="language-html">&lt;Subscription
  subscription={gql`subscription { parent { child } }`}
/&gt;
  {
    ({data, error, loading}) =&gt; {
      if (error) return &lt;Error error={error} /&gt;;
      if (loading) return &lt;Loading /&gt;;
      return &lt;RenderData data={data} /&gt;;
    }
  }
&lt;/Subscription&gt;
</code></pre>

Let us use one such `Subscription` component to subscribe to our view and then transform the subscription data to the structure that ChartJS expects. The transforming logic looks like this:

<div class="break-out">

 <pre><code class="language-javascript">let chartJSData = {
  labels: [],
  datasets: [{
    label: "Max temperature every five seconds",
    data: [],
    pointBackgroundColor: [],
    borderColor: 'brown',
    fill: false
  }]
};
data.last_20_min_temp.forEach((item) => {
  const humanReadableTime = moment(item.five_sec_interval).format('LTS');
  chartJSData.labels.push(humanReadableTime);
  chartJSData.datasets[0].data.push(item.max_temp);
  chartJSData.datasets[0].pointBackgroundColor.push('brown');
})
</code></pre>
</div>

**Note**: *You can also use the open-source library [graphq2chartjs](https://github.com/hasura/graphql-engine/tree/master/community/tools/graphql2chartjs) for transforming the data from GraphQL response to a form that ChartJS expects.*

After using this inside the Subscription component, our `App.js` looks like:

<div class="break-out">

 <pre><code class="language-javascript">import React, { Component } from 'react';
import { Line } from 'react-chartjs-2';
import { Subscription } from 'react-apollo';
import gql from 'graphql-tag';
import moment from 'moment';

const TWENTY_MIN_TEMP_SUBSCRIPTION= gql'
  subscription {
    last_20_min_temp(
      order_by: {
        five_sec_interval: asc
      }
      where: {
        location: {
          &#95;eq: "London"
        }
      }
    ) {
      five_sec_interval
      location
      max_temp
    }
  }
'

class App extends Component {
  render() {
    return (
      &lt;div
        style={{display: 'flex', alignItems: 'center', justifyContent: 'center', margin: '20px'}}
      &gt;
        &lt;Subscription subscription={TWENTY_MIN_TEMP_SUBSCRIPTION}&gt;
          {
            ({data, error, loading}) => {
              if (error) {
                console.error(error);
                return "Error";
              }
              if (loading) {
                return "Loading";
              }
              let chartJSData = {
                labels: [],
                datasets: [{
                  label: "Max temperature every five seconds",
                  data: [],
                  pointBackgroundColor: [],
                  borderColor: 'brown',
                  fill: false
                }]
              };
              data.last_20_min_temp.forEach((item) => {
                const humanReadableTime = moment(item.five_sec_interval).format('LTS');
                chartJSData.labels.push(humanReadableTime);
                chartJSData.datasets[0].data.push(item.max_temp);
                chartJSData.datasets[0].pointBackgroundColor.push('brown');
              })
              return (
                &lt;Line
                  data={chartJSData}
                  options={{
                    animation: {duration: 0},
                    scales: { yAxes: [{ticks: { min: 5, max: 20 }}]}
                  }}
                /&gt;
              );
            }
          }
        &lt;/Subscription&gt;
      &lt;/div&gt;
    );
  }
}

export default App;
</code></pre>
</div>

You will have a fully working real-time chart ready at `https://localhost:3000` . However, it would be empty, so let’s populate some sample data so we can actually see some magic happen.

**Note**: *I have added some more options to the Line chart because I don’t like those fancy animations in ChartJS. A time series looks sweet when it’s simple, however, you can remove the options prop if you like.*

### Inserting Sample Data

Lets write a script that populates our database with dummy data. Create a separate directory (outside this app) and create a file called `script.js` with the following content, 

<div class="break-out">

 <pre><code class="language-javascript">const fetch = require('node-fetch');
setInterval(
  () => {
    const randomTemp = (Math.random() * 5) + 10;
    fetch(
      `https://localhost:8080/v1alpha1/graphql`,
      {
        method: 'POST',
        body: JSON.stringify({
          query: `
            mutation ($temp: numeric) {
              insert_temperature (
                objects: [{
                  temperature: $temp
                  location: "London"
                }]
              ) {
                returning {
                  recorded_at
                  temperature
                }
              }
            }
          `,
          variables: {
            temp: randomTemp
          }
        })
      }
    ).then((resp) => resp.json().then((respObj) => console.log(JSON.stringify(respObj, null, 2))));
  },
  2000
);
</code></pre>
</div>

Now run these two commands:

<pre><code class="language-bash">npm install --save node-fetch
node script.js
</code></pre>

You can go back to `https://localhost:3000` and see the chart updating.

## Finishing Up

You can build most of the real-time charts using the ideas that we discussed above. The algorithm is:

1. Deploy GraphQL Engine with Postgres;
2. Create tables where you wish to store data;
3. Subscribe to those tables from your React app;
4. Render the chart.

You can find the source code [here](https://github.com/wawhal/graphql-live-time-series).

{{< signature "dm, ra, il" >}}
