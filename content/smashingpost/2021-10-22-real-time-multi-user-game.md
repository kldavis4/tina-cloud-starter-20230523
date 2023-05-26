---
title: 'How To Build A Real-Time Multi-User Game From Scratch'
slug: real-time-multi-user-game
author: martin-grubinger
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f27da7cf-e0e3-4ed4-a845-6fd61fdb0e70/real-time-multi-user-game.jpg
date: 2021-10-22T09:30:00.000Z
summary: >-
  This article highlights the process, technical decisions and lessons learned behind building the real-time game Autowuzzler. Learn how to share game state across multiple clients in real-time with Colyseus, do physics calculations with Matter.js, store data in Supabase.io and build the front-end with SvelteKit.
description: >-
  This article highlights the process, technical decisions and lessons learned behind building the real-time game Autowuzzler. Learn how to share game state across multiple clients in real-time with Colyseus, do physics calculations with Matter.js, store data in Supabase.io and build the front-end with SvelteKit.
categories:
  - Apps
  - Games
  - Coding
  - JavaScript
---

As the pandemic lingered, the suddenly-remote team I work with became increasingly [foosball](https://en.wikipedia.org/wiki/Table_football)-deprived. I thought about how to play foosball in a remote setting, but it was clear that simply reconstructing the rules of foosball on a screen would not be a lot of fun.

What _is_ fun is to kick a ball using toy cars &mdash; a realization made as I was playing with my 2-year old kid. The same night I set out to build the first prototype for a game that would become _Autowuzzler_.

**The idea is simple**: players steer virtual toy cars in a top-down arena that resembles a foosball table. The first team to score 10 goals wins. 

Of course, the idea of using cars to play soccer is not unique, but two main ideas should set *Autowuzzler* apart: I wanted to reconstruct some of the look and feel of playing on a physical foosball table, and I wanted to make sure it is as easy as possible to invite friends or teammates to a quick casual game.

In this article, I’ll describe **the process behind the creation of [Autowuzzler](https://www.autowuzzler.com/)**, which tools and frameworks I chose, and share a few implementation details and lessons I learned. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6252ae01-40e7-48c9-88af-15add0425258/2-real-time-multi-user-game.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6252ae01-40e7-48c9-88af-15add0425258/2-real-time-multi-user-game.png" width="800" height="" sizes="100vw" caption="Autowuzzler (beta) with six concurrent players in two teams. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6252ae01-40e7-48c9-88af-15add0425258/2-real-time-multi-user-game.png'>Large preview</a>)" alt="Game user interface showing a foosball table background, six cars in two teams and one ball." >}}

## First Working (Terrible) Prototype

The first prototype was built using the open-source game engine [Phaser.js](https://phaser.io/), mostly for the included physics engine and because I already had some experience with it. The game stage was embedded in a [Next.js](https://nextjs.org/) application, again because I already had a solid understanding of Next.js and wanted to focus mainly on the game. 

As the game needs to **support multiple players in real-time**, I utilized Express as a WebSockets broker. Here is where it becomes tricky, though. 

Since the physics calculations were done on the client in the Phaser game, I chose a simple, but obviously flawed logic: The _first_ connected client had the doubtful privilege of doing the physics calculations for all game objects, sending the results to the express server, which in turn broadcasted the updated positions, angles and forces back to the other player’s clients. The other clients would then apply the changes to the game objects. 

This led to the situation where the _first_ player got to **see the physics happening in real-time** (it is happening locally in their browser, after all), while all the other players were lagging behind at least 30 milliseconds (the broadcast rate I chose), or &mdash; if the _first_ player’s network connection was slow &mdash; considerably worse. 

If this sounds like poor architecture to you &mdash; you’re absolutely right. However, I accepted this fact in favor of quickly getting something playable to figure out if the game is actually _fun_ to play. 

### Validate The Idea, Dump The Prototype

As flawed as the implementation was, it was sufficiently playable to invite friends for a first test drive. **Feedback was very positive**, with the major concern being &mdash; not surprisingly &mdash; the real-time performance. Other inherent problems included the situation when the _first_ player (remember, the one in charge of _everything_) left the game &mdash; who should take over? At this point there was only one game room, so anyone would join the same game. I was also a bit concerned by the bundle size the Phaser.js library introduced.

It was time to dump the prototype and start with a fresh setup and a clear goal.

## Project Setup

Clearly, the "first client rules all" approach needed to be replaced with a solution in which **the game state lives on the server**. In my research, I came across [Colyseus](https://www.colyseus.io/), which sounded like the perfect tool for the job.

For the other main building blocks of the game I chose:

* [Matter.js](https://brm.io/matter-js/) as a physics engine instead of Phaser.js because it runs in Node and Autowuzzler does not require a full game framework.
* [SvelteKit](https://kit.svelte.dev/) as an application framework instead of Next.js, because it *just* went into public beta at that time. (Besides: I love working with [Svelte](https://svelte.dev/).)
* [Supabase.io](https://supabase.io/) for storing user-created game PINs.

Let’s look at those building blocks in more detail.

{{% feature-panel %}}

### Synchronized, Centralized Game State With Colyseus

Colyseus is a multiplayer game framework based on Node.js and Express. At its core, it provides:

* Synchronizing state across clients in an authoritative fashion;
* Efficient real-time communication using WebSockets by sending changed data only;
* Multi-room setups;
* Client libraries for JavaScript, Unity, Defold Engine, Haxe, Cocos Creator, Construct3;
* Lifecycle hooks, e.g. room is created, user joins, user leaves, and more;
* Sending messages, either as broadcast messages to all users in the room, or to a single user;
* A built-in monitoring panel and load test tool.

**Note**: *The [Colyseus docs](https://docs.colyseus.io/) make it easy to get started with a barebones Colyseus server by providing an `npm init` script and [an examples repository](https://github.com/colyseus/colyseus-examples).*

### Creating A Schema

The main entity of a Colyseus app is the game room, which holds the state for a single room instance and all its game objects. In the case of *Autowuzzler*, it’s a game session with:

* two teams,
* a finite amount of players,
* one ball.

A schema needs to be defined for all properties of the game objects that **should be synchronized across clients**. For example, we want the ball to synchronize, and so we need to create a schema for the ball:

<pre><code class="language-javascript">class Ball extends Schema {
  constructor() {
   super();
   this.x = 0;
   this.y = 0;
   this.angle = 0;
   this.velocityX = 0;
   this.velocityY = 0;
  }
}
defineTypes(Ball, {
  x: "number",
  y: "number",
  angle: "number",
  velocityX: "number",
  velocityY: "number"
});
</code></pre>

In the example above, a new class that extends the schema class provided by Colyseus is created; in the constructor, all properties receive an initial value. The position and movement of the ball is described using the five properties: `x`, `y`, `angle`, `velocityX,` `velocityY`. Additionally, we need to **specify the types of each property**. This example uses JavaScript syntax, but you can also use the slightly [more compact TypeScript syntax](https://docs.colyseus.io/state/schema/). 

Property types can either be primitive types:

* `string`
* `boolean`
* `number` (as well as more efficient integer and float types)

or complex types:

* `ArraySchema` (similar to Array in JavaScript)
* `MapSchema` (similar to Map in JavaScript)
* `SetSchema`  (similar to Set in JavaScript)
* `CollectionSchema` (similar to ArraySchema, but without control over indexes)

The `Ball` class above has five properties of type `number`: its coordinates (`x`, `y`), its current `angle` and the velocity vector (`velocityX`, `velocityY`). 

The schema for players is similar, but includes a few more properties to store the player's name and team’s number, which need to be supplied when creating a Player instance:

<pre><code class="language-javascript">class Player extends Schema {
  constructor(teamNumber) {
    super();
    this.name = "";
    this.x = 0;
    this.y = 0;
    this.angle = 0;
    this.velocityX = 0;
    this.velocityY = 0;
    this.teamNumber = teamNumber;
  }
}
defineTypes(Player, {
  name: "string",
  x: "number",
  y: "number",
  angle: "number",
  velocityX: "number",
  velocityY: "number",
  angularVelocity: "number",
  teamNumber: "number",
});
</code></pre>

Finally, the schema for the *Autowuzzler* `Room` connects the previously defined classes: One room instance has multiple teams (stored in an ArraySchema). It also contains a single ball, therefore we create a new Ball instance in the RoomSchema’s constructor. Players are stored in a MapSchema for quick retrieval using their IDs.

{{< figure caption="**Note**: *Definition of the `Team` class is omitted.*" >}}

<pre><code class="language-javascript">class RoomSchema extends Schema {
 constructor() {
   super();
   this.teams = new ArraySchema();
   this.ball = new Ball();
   this.players = new MapSchema();
 }
}
defineTypes(RoomSchema, {
 teams: [Team], // an Array of Team
 ball: Ball,    // a single Ball instance
 players: { map: Player } // a Map of Players
});
</code></pre>
{{< /figure >}}

### Multi-Room Setup (“Match-Making”)

Anyone can join an *Autowuzzler* game if they have a valid game PIN. Our Colyseus server creates a new Room instance for every game session as soon as the first player joins and discards the room when the last player leaves it.

The process of **assigning players to their desired game room** is called “match-making”. Colyseus makes it very easy to set up by using the [`filterBy`](https://docs.colyseus.io/server/api/#filterbyoptions) method when defining a new room:

<pre><code class="language-javascript">gameServer.define("autowuzzler", AutowuzzlerRoom).filterBy(['gamePIN']);
</code></pre>

Now, any players joining the game with the same `gamePIN` (we’ll see how to “join” later on) will end up in the same game room! Any state updates and other broadcast messages are limited to players in the same room.

### Physics In A Colyseus App

Colyseus provides a lot out-of-the-box to get up and running quickly with an authoritative game server, but leaves it up to the developer to create the actual game mechanics &mdash; including physics. Phaser.js, which I used in the prototype, cannot be executed in a non-browser environment, but Phaser.js’ integrated physics engine Matter.js can run on Node.js.

With Matter.js, you define a physics world with certain physical properties like its size and gravity. It provides several methods to create primitive physics objects which interact with each other by adhering to (simulated) laws of physics, including mass, collisions, movement with friction, and so on. You can **move objects around by applying force** &mdash; just like you would in the real world.

A Matter.js “world” sits at the heart of the *Autowuzzler* game; it defines how fast the cars move, how bouncy the ball should be, where the goals are located, and what happens if someone shoots a goal. 

<pre><code class="language-javascript">let ball = Bodies.circle(
 ballInitialXPosition,
 ballInitialYPosition,
 radius,
 {
   render: {
     sprite: {
       texture: '/assets/ball.png',
     }
   },
   friction: 0.002,
   restitution: 0.8
 }
);
World.add(this.engine.world, [ball]);
</code></pre>

*Simplified code for adding a “ball” game object to the stage in Matter.js.*

Once the rules are defined, Matter.js can run _with_ or _without_ actually rendering something to a screen. For *Autowuzzler*, I’m utilizing this feature to reuse the physics world code for both the server _and_ the client &mdash; with several key differences:

Physics world **on the server**:

* receives user input (keyboard events for steering a car) via Colyseus and applies the appropriate force on the game object (the user’s car);
* does all the physics calculations for all objects (players and the ball), including detecting collisions;
* communicates the updated state for each game object back to Colyseus, which in turn broadcasts it to the clients;
* is updated every 16.6 milliseconds (= 60 frames per second), triggered by our Colyseus server.

Physics world **on the client**:

* does not manipulate game objects directly;
* receives updated state for each game object from Colyseus;
* applies changes in position, velocity and angle after receiving updated state;
* sends user input (keyboard events for steering a car) to Colyseus;
* loads game sprites and uses a renderer to draw the physics world onto a canvas element;
* skips collision detection (using [`isSensor`](https://brm.io/matter-js/docs/classes/Body.html#property_isSensor) option for objects);
* updates using requestAnimationFrame, ideally at 60 fps.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/511ac6c5-568b-45a4-95c8-8339c57d0e3e/5-real-time-multi-user-game.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/511ac6c5-568b-45a4-95c8-8339c57d0e3e/5-real-time-multi-user-game.png" width="800" height="" sizes="100vw" caption="Main logical units of the Autowuzzler architecture: the Physics World is shared between the Colyseus server and the SvelteKit client app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/511ac6c5-568b-45a4-95c8-8339c57d0e3e/5-real-time-multi-user-game.png'>Large preview</a>)" alt="Diagram showing two main blocks: Colyseus Server App and SvelteKit App. Colyseus Server App contains Autowuzzler Room block, SvelteKit App contains Colyseus Client block. Both main blocks share a block named Physics World (Matter.js)" >}}

Now, with all the magic happening on the server, the client only handles the input and draws the state it receives from the server to the screen. With one exception:

#### Interpolation On The Client

Since we are re-using the same Matter.js physics world on the client, we can improve the experienced performance with a simple trick. Rather than only updating the position of a game object, we also **synchronize the velocity of the object**. This way, the object keeps on moving on its trajectory even if the next update from the server takes longer than usual. So rather than moving objects in discrete steps from position A to position B, we change their position and make them move in a certain direction.

### Lifecycle

The *Autowuzzler* `Room` class is where the logic concerned with the different phases of a Colyseus room is handled. Colyseus provides several lifecycle methods: 

* `onCreate`: when a new room is created (usually when the first client connects);
* `onAuth`: as an authorization hook to permit or deny entry to the room;
* `onJoin`: when a client connects to the room;
* `onLeave`: when a client disconnects from the room;
* `onDispose`: when the room is discarded.

The *Autowuzzler* room creates a new instance of the physics world (see section “[Physics In A Colyseus App](#physics-in-a-colyseus-app)”) as soon as it is created (`onCreate`) and adds a player to the world when a client connects (`onJoin`). It then updates the physics world 60 times a second (every 16.6 milliseconds) using the `setSimulationInterval` method (our main game loop):

<pre><code class="language-javascript">// deltaTime is roughly 16.6 milliseconds
this.setSimulationInterval((deltaTime) => this.world.updateWorld(deltaTime));
</code></pre>

The physics objects are independent of the Colyseus objects, which leaves us with **two permutations of the same game object** (like the ball), i.e. an object in the physics world and a Colyseus object that can be synced.

As soon as the physical object changes, its updated properties need to be applied back to the Colyseus object. We can achieve that by listening to Matter.js’ `afterUpdate` event and setting the values from there:

<pre><code class="language-javascript">Events.on(this.engine, "afterUpdate", () => {
 // apply the x position of the physics ball object back to the colyseus ball object
 this.state.ball.x = this.physicsWorld.ball.position.x;
 // ... all other ball properties
 // loop over all physics players and apply their properties back to colyseus players objects
})
</code></pre>

There’s one more copy of the objects we need to take care of: **the game objects in the user-facing game**.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6549e7bb-4207-4060-a46c-861671798c03/4-real-time-multi-user-game.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6549e7bb-4207-4060-a46c-861671798c03/4-real-time-multi-user-game.png" width="800" height="" sizes="100vw" caption="Autowuzzler maintains three copies of each physics object, one authoritative version (Colyseus object), a version in the Matter.js physics world and a version on the client. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6549e7bb-4207-4060-a46c-861671798c03/4-real-time-multi-user-game.png'>Large preview</a>)" alt="Diagram showing the three versions of a game object: Colyseus Schema Objects, Matter.js Physics Objects, Client Matter.js Physics Objects. Matter.js updates the Colyseus version of the object, Colyseus synchronizes to the Client Matter.js Physics Object." >}}

{{% ad-panel-leaderboard %}}

## Client-Side Application

Now that we have an application on the server that handles the synchronization of the game state for multiple rooms as well as physics calculations, let’s focus on **building the website and the actual game interface**. The *Autowuzzler* frontend has the following responsibilities:

* enables users to create and share game PINs to access individual rooms;
* sends the created game PINs to a Supabase database for persistence;
* provides an optional “Join a game” page for players to enter the game PIN;
* validates game PINs when a player joins a game;
* hosts and renders the actual game on a shareable (i.e. unique) URL;
* connects to the Colyseus server and handle state updates;
* provides a landing (“marketing”) page.

For the implementation of those tasks, I chose SvelteKit over Next.js for the following reasons:

### Why SvelteKit?

I have been wanting to develop another app using Svelte ever since I built [neolightsout](https://neolightsout.grooovinger.com/). When SvelteKit (the official application framework for Svelte) went into public beta, I decided to build *Autowuzzler* with it and accept any headaches that come with using a fresh beta &mdash; the joy of using Svelte clearly makes up for it.

These **key features** made me choose SvelteKit over Next.js for the actual implementation of the game frontend:

* Svelte is a UI framework _and_ a compiler and therefore ships minimal code without a client runtime;
* Svelte has an expressive templating language and component system (personal preference);
* Svelte includes global stores, transitions and animations out of the box, which means: no decision fatigue choosing a global state management toolkit and an animation library;
* Svelte supports scoped CSS in single-file-components;
* SvelteKit supports SSR, simple but flexible file-based routing and server-side routes for building an API;
* SvelteKit allows for each page to run code on the server, e.g. to fetch data that is used to render the page;
* Layouts shared across routes;
* SvelteKit can be run in a serverless environment.

### Creating And Storing Game PINs

Before a user can start playing the game, they first need to create a game PIN. By sharing the PIN with others, they can all access the same game room.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55799f4-a6c6-4795-8261-0848a07645df/3-real-time-multi-user-game.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55799f4-a6c6-4795-8261-0848a07645df/3-real-time-multi-user-game.png" width="800" height="" sizes="100vw" caption="Start a new game by copying the generated game PIN or share the direct link to the game room. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55799f4-a6c6-4795-8261-0848a07645df/3-real-time-multi-user-game.png'>Large preview</a>)" alt="Screenshot of the start a new game section of the Autowuzzler website showing the game PIN 751428 and options to copy and share the game PIN and URL." >}}

This is a great use case for SvelteKits server-side [endpoints](https://kit.svelte.dev/docs#routing-endpoints) in conjunction with Sveltes [onMount](https://svelte.dev/docs#onMount) function: The endpoint `/api/createcode` generates a game PIN, stores it in a Supabase.io database and **outputs the game PIN as a response**. This is response is fetched as soon as the page component of the “create” page is mounted:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da77cb83-8b8a-434c-b6a7-245dfbf91228/1-real-time-multi-user-game.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da77cb83-8b8a-434c-b6a7-245dfbf91228/1-real-time-multi-user-game.png" width="800" height="" sizes="100vw" caption="Game PINs are created in the endpoint, stored in a Supabase.io database and displayed on the “Create” page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da77cb83-8b8a-434c-b6a7-245dfbf91228/1-real-time-multi-user-game.png'>Large preview</a>)" alt="Diagram showing three sections: Create page, createcode endpoint and Supabase.io. Create page fetches the endpoint in its onMount function, the endpoint generates a game PIN, stores it in Supabase.io and responds with the game PIN. The Create page then displays the game PIN." >}}

#### Storing Game PINs With Supabase.io

Supabase.io is an open-source alternative to Firebase. Supabase makes it very easy to create a PostgreSQL database and access it either via one of its client libraries or via REST.

For the JavaScript client, we import the `createClient` function and execute it using the parameters `supabase_url` and `supabase_key` we received when creating the database. To **store the game PIN** that is created on each call to the `createcode` endpoint, all we need to do is to run this simple `insert` query:

<pre><code class="language-javascript">import { createClient } from '@supabase/supabase-js'

const database = createClient(
 import.meta.env.VITE_SUPABASE_URL,
 import.meta.env.VITE_SUPABASE_KEY
);

const { data, error } = await database
 .from("games")
 .insert([{ code: 123456 }]);
</code></pre>

**Note**: *The `supabase_url` and `supabase_key` are stored in a .env file. Due to Vite &mdash; the build tool at the heart of SvelteKit &mdash; it is required to prefix the environment variables with VITE_ to make them accessible in SvelteKit.*

### Accessing The Game

I wanted to make joining an *Autowuzzler* game as easy as following a link. Therefore, every game room needed to have its **own URL based on the previously created game PIN**, e.g. [https://autowuzzler.com/play/12345](https://autowuzzler.com/play/12345).

In SvelteKit, pages with dynamic route parameters are created by putting the dynamic parts of the route in square brackets when naming the page file: `client/src/routes/play/[gamePIN].svelte`. The value of the `gamePIN` parameter will then become available in the page component (see the [SvelteKit docs](https://kit.svelte.dev/docs#routing-pages) for details). In the `play` route, we need to connect to the Colyseus server, instantiate the physics world to render to the screen, handle updates to game objects, listen to keyboard input and display other UI like the score, and so on.

### Connecting To Colyseus And Updating State

The Colyseus client library enables us to connect a client to a Colyseus server. First, let’s create a new `Colyseus.Client` by pointing it to the Colyseus server (`ws://localhost:2567 `in development). Then join the room with the name we chose earlier (`autowuzzler`) and the `gamePIN` from the route parameter. The `gamePIN` parameter makes sure the user joins the correct room instance (see “[match-making](#multi-room-setup-match-making)” above).

<pre><code class="language-javascript">let client = new Colyseus.Client("ws://localhost:2567");
this.room = await client.joinOrCreate("autowuzzler", { gamePIN });
</code></pre>

Since SvelteKit renders pages on the server initially, we need to make sure that this **code only runs on the client** after the page is done loading. Again, we use the `onMount` lifecycle function for that use case. (If you’re familiar with React, `onMount` is similar to the `useEffect` hook with an empty dependency array.)

<pre><code class="language-javascript">onMount(async () => {
  let client = new Colyseus.Client("ws://localhost:2567");
  this.room = await client.joinOrCreate("autowuzzler", { gamePIN });
})
</code></pre>

Now that we are connected to the Colyseus game server, we can start to listen to any changes to our game objects.

Here’s an example of **how to listen to a player joining the room** (`onAdd`) and receiving consecutive state updates to this player:

<pre><code class="language-javascript">this.room.state.players.onAdd = (player, key) => {
  console.log(`Player has been added with sessionId: ${key}`);

  // add player entity to the game world
  this.world.createPlayer(key, player.teamNumber);

  // listen for changes to this player
  player.onChange = (changes) => {
   changes.forEach(({ field, value }) => {
     this.world.updatePlayer(key, field, value); // see below
   });
 };
};
</code></pre>

In the `updatePlayer` method of the physics world, we update the properties one by one because Colyseus’ `onChange` delivers a set of all changed properties.

**Note**: *This function only runs on the client version of the physics world, as game objects are only manipulated indirectly via the Colyseus server.*

<pre><code class="language-javascript">updatePlayer(sessionId, field, value) {
 // get the player physics object by its sessionId
 let player = this.world.players.get(sessionId);
 // exit if not found
 if (!player) return;
 // apply changes to the properties
 switch (field) {
   case "angle":
     Body.setAngle(player, value);
     break;
   case "x":
     Body.setPosition(player, { x: value, y: player.position.y });
     break;
   case "y":
     Body.setPosition(player, { x: player.position.x, y: value });
     break;
   // set velocityX, velocityY, angularVelocity ...
 }
}
</code></pre>

The same procedure applies to the other game objects (ball and teams): listen to their changes and apply the changed values to the client's physics world.

So far, no objects are moving because we still need to **listen to keyboard input and send it to the server**. Instead of directly sending events on every `keydown` event, we maintain a map of currently pressed keys and send events to the Colyseus server in a 50ms loop. This way, we can support pressing multiple keys at the same time and mitigate the pause that happens after the first and consecutive `keydown` events when the key stays pressed:

<pre><code class="language-javascript">let keys = {};
const keyDown = e => {
 keys[e.key] = true;
};
const keyUp = e => {
 keys[e.key] = false;
};
document.addEventListener('keydown', keyDown);
document.addEventListener('keyup', keyUp);

let loop = () => {
 if (keys["ArrowLeft"]) {
   this.room.send("move", { direction: "left" });
 }
 else if (keys["ArrowRight"]) {
   this.room.send("move", { direction: "right" });
 }
 if (keys["ArrowUp"]) {
   this.room.send("move", { direction: "up" });
 }
 else if (keys["ArrowDown"]) {
   this.room.send("move", { direction: "down" });
 }
 // next iteration
 requestAnimationFrame(() => {
  setTimeout(loop, 50);
 });
}
// start loop
setTimeout(loop, 50);
</code></pre>

Now the cycle is complete: listen for keystrokes, send the corresponding commands to the Colyseus server to manipulate the physics world on the server. The Colyseus server then applies the new physical properties to all the game objects and propagates the data back to the client to update the user-facing instance of the game. 

{{% ad-panel-leaderboard %}}

## Minor Nuisances

In retrospect, two things of the category _nobody-told-me-but-someone-should-have_ come to mind:

* A **good understanding of how physics engines work** is beneficial. I spent a considerable amount of time fine-tuning physics properties and constraints. Even though I built a small game with Phaser.js and Matter.js before, there was a lot of trial-and-error to get objects to move in the way I imagined them to.
* **Real-time is hard** &mdash; especially in physics-based games. Minor delays considerably worsen the experience, and while synchronizing state across clients with Colyseus works great, it can’t remove computation and transmission delays.

### Gotchas And Caveats With SvelteKit

Since I used SvelteKit when it was fresh out of the beta-oven, there were a few gotchas and caveats I would like to point out:

* It took a while to figure out that environment variables need to be prefixed with VITE_ in order to use them in SvelteKit. This is now properly documented in the [FAQ](https://kit.svelte.dev/faq).
* To use Supabase, I had to add Supabase to _both_ the `dependencies` and `devDependencies` lists of package.json. I believe this is no longer the case.
* SvelteKits `load` function runs both on the server _and_ the client!
* To enable full hot module replacement (including preserving state), you have to manually add a comment line `<!-- @hmr:keep-all -->` in your page components. See [FAQ](https://kit.svelte.dev/faq) for more details.

Many other frameworks would have been great fits as well, but I have no regrets about choosing SvelteKit for this project. It enabled me to work on the client application in a very efficient way &mdash; mostly because Svelte itself is very expressive and skips a lot of the boilerplate code, but also because Svelte has things like animations, transitions, scoped CSS and global stores baked in. SvelteKit **provided all the building blocks I needed** (SSR, routing, server routes) and although still in beta, it felt very stable and fast.

### Deployment And Hosting

Initially, I hosted the Colyseus (Node) server on a [Heroku](https://www.heroku.com/) instance and wasted a lot of time getting WebSockets and CORS working. As it turns out, the performance of a tiny (free) Heroku dyno is not sufficient for a real-time use case. I later migrated the Colyseus app to a small server at [Linode](http://linode.com/). The client-side application is deployed by and hosted on Netlify via SvelteKits[ adapter-netlify](https://github.com/sveltejs/kit/tree/master/packages/adapter-netlify). No surprises here: Netlify just worked great!

## Conclusion

Starting out with a really simple prototype to validate the idea helped me a lot in figuring out if the project is worth following and where the technical challenges of the game lay. In the final implementation, Colyseus took care of all the heavy lifting of synchronizing state in real-time across multiple clients, distributed in multiple rooms. **It’s impressive how quickly a real-time multi-user application can be built** with Colyseus &mdash; once you figure out how to properly describe the schema. Colyseus’ built-in monitoring panel helps in troubleshooting any synchronizing issues.

What complicated this setup was the physics layer of the game because it introduced an additional copy of each physics-related game object that needed to be maintained. Storing game PINs in Supabase.io from the SvelteKit app was very straightforward. In hindsight, I could have just used an SQLite database to store the game PINs, but **trying out new things** is half of the fun when building side projects.

Finally, using SvelteKit for building out the frontend of the game allowed me to move quickly &mdash; and with the occasional grin of joy on my face.

Now, go ahead and invite your friends to a round of [Autowuzzler](https://www.autowuzzler.com/)!

### Further Reading on Smashing Magazine

- “[Get Started With React By Building A Whac-A-Mole Game](https://www.smashingmagazine.com/2021/05/get-started-whac-a-mole-react-game/),” Jhey Tompkins
- “[How To Build A Real-Time Multiplayer Virtual Reality Game](https://www.smashingmagazine.com/2019/08/real-time-multiplayer-virtual-reality-game-part-1/),” Alvin Wan
- “[Writing A Multiplayer Text Adventure Engine In Node.js](https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/),” Fernando Doglio
- “[The Future Of Mobile Web Design: Video Game Design And Storytelling](https://www.smashingmagazine.com/2018/03/future-mobile-web-design-video-game-design-storytelling/),” Suzanne Scacca
- “[How To Build An Endless Runner Game In Virtual Reality](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-1/),” Alvin Wan

{{< signature "vf, il" >}}
