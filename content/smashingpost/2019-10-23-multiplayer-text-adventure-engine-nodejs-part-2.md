---
title: 'Writing A Multiplayer Text Adventure Engine In Node.js: Game Engine Server Design (Part 2)'
slug: multiplayer-text-adventure-engine-node-js-part-2
author: fernando-doglio
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a01ceda5-bc55-4aaa-8b75-15dc1ef9d5df/multiplayer-text-adventure-engine-node-js.png
date: 2019-10-23T14:00:59+02:00
summary: >-
  Welcome to the second part of this series. The the <a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">first part</a>, we covered the architecture of a Node.js-based platform and client application that will enable people to define and play their own text adventures as a group. This time around, we’ll be covering the creation of one of the modules Fernando defined last time (the game engine) and will also be focusing on the design process in order to shed some light into what needs to happen before you start coding your own hobby projects.
description: >-
  Welcome to the second part of this series. The the <a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">first part</a>, we covered the architecture of a Node.js-based platform and client application that will enable people to define and play their own text adventures as a group.
categories:
  - Node.js
  - JavaScript
---
<p>After some careful consideration and actual implementation of the module, some of the definitions I made during the design phase had to be changed. This should be a familiar scene for anyone who has ever worked with an eager client who dreams about an ideal product but needs to be restraint by the development team.</p>

<p>Once features have been implemented and tested, your team will start noticing that some characteristics might differ from the original plan, and that’s alright. Simply notify, adjust, and go on. So, without further ado, allow me to first explain what has changed from the <a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">original plan</a>.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Other Parts Of This Series</h4>
<ul>
  <li><a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">Part 1</a>: The Introduction</li>
  <li><a href="https://www.smashingmagazine.com/2019/10/multiplayer-text-adventure-engine-node-js-part-3/">Part 3</a>: Creating The Terminal Client</li>
  <li><a href="https://www.smashingmagazine.com/2019/11/multiplayer-text-adventure-engine-node-js-part-4/">Part 4</a>: Adding Chat Into Our Game</li>
</ul>
</div>

### Battle Mechanics

<p>This is probably the biggest change from the original plan. I know I said I was going to go with a D&D-esque implementation in which each PC and NPC involved would get an initiative value and after that, we would run a turn-based combat. It was a nice idea, but implementing it on a REST-based service is a bit complicated since you can’t initiate the communication from the server side, nor maintain status between calls.</p>

<p>So instead, I will take advantage of the simplified mechanics of REST and use that to simplify our battle mechanics. The implemented version will be player-based instead of party-based, and will allow players to attack NPCs (Non-Player Characters). If their attack succeeds, the NPCs will be killed or else they will attack back by either damaging or killing the player.</p>

<p>Whether an attack succeeds or fails will be determined by the type of weapon used and the weaknesses an NPC might have. So basically, if the monster you’re trying to kill is weak against your weapon, it dies. Otherwise, it’ll be unaffected and &mdash; most likely &mdash; very angry.</p>

### Triggers

<p>If you paid close attention to the JSON game definition from my <a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">previous article</a>, you might’ve noticed the trigger’s definition found on scene items. A particular one involved updating the game status (<code>statusUpdate</code>). During implementation, I realized having it working as a toggle provided limited freedom. You see, in the way it was implemented (from an idiomatic point of view), you were able to set a status but unsetting it wasn’t an option. So instead, I’ve replaced this trigger effect with two new ones: <code>addStatus</code> and <code>removeStatus</code>. These will allow you to define <em>exactly</em> when these effects can take place &mdash; if at all. I feel this is a lot easier to understand and reason about.</p>

<p>This means that the triggers now look like this:</p>

<pre><code class="language-javascript">"triggers": [
{
    "action": "pickup",
"effect":{
    "addStatus": "has light",
"target": "game"
    }
},
{
    "action": "drop",
    "effect": {
    "removeStatus": "has light",
    "target": "game"
    }
}
]</code></pre>

<p>When picking up the item, we’re setting up a status, and when dropping it, we’re removing it. This way, having multiple game-level status indicators is completely possible and easy to manage.</p>

{{% feature-panel %}}

## The Implementation

<p>With those updates out of the way, we can start covering the actual implementation. From an architectural point of view, nothing changed; we’re still building a REST API that will contain the main game engine’s logic.</p>

### The Tech Stack

<p>For this particular project, the modules I’m going to be using are the following:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Module</th>
			<th>Description</th>
		</tr>
	</thead>
<tbody>
<tr>
<td><a href="https://expressjs.com">Express.js</a></td>
<td>Obviously, I’ll be using Express to be the base for the entire engine.</td>
</tr>
<tr>
<td><a href="https://www.npmjs.com/package/winston">Winston</a></td>
<td>Everything in regards to logging will be handled by Winston.</td>
</tr>
<tr>
<td><a href="https://www.npmjs.com/package/config">Config</a></td>
<td>Every constant and environment-dependant variable will be handled by the config.js module, which greatly simplifies the task of accessing them.</td>
</tr>
<tr>
<td><a href="https://www.npmjs.com/package/mongoose">Mongoose</a></td>
<td>This will be our ORM. I will model all resources using Mongoose Models and use that to interact directly with the database.</td>
</tr>
<tr>
<td><a href="https://www.npmjs.com/package/uuid">uuid</a></td>
<td>We’ll need to generate some unique IDs &mdash; this module will help us with that task.</td>
</tr>
</tbody>
</table>

<p>As for other technologies used aside from Node.js, we have <strong>MongoDB</strong> and <strong>Redis</strong>. I like to use Mongo due to the lack of schema required. That simple fact allows me to think about my code and the data formats, without having to worry about updating the structure of my tables, schema migrations or conflicting data types.</p>

<p>Regarding Redis, I tend to use it as a support system as much as I can in my projects and this case is no different. I will be using Redis for everything that can be considered volatile information, such as party member numbers, command requests, and other types of data that are small enough and volatile enough to not merit permanent storage.</p>

<p>I’m also going to be using Redis’ key expiration feature to auto manage some aspects of the flow (more on this shortly).</p>

## API Definition

<p>Before moving into client-server interaction and data-flow definitions I want to go over the endpoints defined for this API. They aren’t that many, mostly we need to comply with the main features described in <a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">Part 1</a>:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Feature</th>
			<th>Description</th>
		</tr>
	</thead>
<tbody>
<tr>
<td>Join a game</td>
<td>A player will be able to join a game by specifying the game’s ID.</td>
</tr>
<tr>
<td>Create a new game</td>
<td>A player can also create a new game instance. The engine should return an ID, so that others can use it to join.</td>
</tr>
<tr>
<td>Return scene</td>
<td>This feature should return the current scene where the party is located. Basically, it’ll return the description, with all of the associated information (possible actions, objects in it, etc.).</td>
</tr>
<tr>
<td>Interact with scene</td>
<td>This is going to be one of the most complex ones, because it will take a command from the client and perform that action &mdash; things like move, push, take, look, read, to name just a few.</td>
</tr>
<tr>
<td>Check inventory</td>
<td>Although this is a way to interact with the game, it does not directly relate to the scene. So, checking the inventory for each player will be considered a different action.</td>
</tr>
<tr>
<td>Register client application</td>
<td>The above actions require a valid client to execute them. This endpoint will verify the client application and return a Client ID that will be used for authentication purposes on subsequent requests.</td>
</tr>
</tbody>
</table>

<p>The above list translates into the following list of endpoints:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Verb</th>
			<th>Endpoint</th>
			<th>Description</th>
		</tr>
	</thead>
<tbody>
<tr>
<td>POST</td>
<td><code>/clients</code></td>
<td>Client applications will require to get a Client ID key using this endpoint.</td>
</tr>
<tr>
<td>POST</td>
<td><code>/games</code></td>
<td>New game instances are created using this endpoint by the client applications.</td>
</tr>
<tr>
<td>POST</td>
<td><code>/games/:id</code></td>
<td>Once the game is created, this endpoint will enable party members to join it and start playing.</td>
</tr>
<tr>
<td>GET</td>
<td><code>/games/:id/:playername</code></td>
<td>This endpoint will return the current game state for a particular player.</td>
</tr>
<tr>
<td>POST</td>
<td><code>/games/:id/:playername/commands</code></td>
<td>Finally, with this endpoint, the client application will be able to submit commands (in other words, this endpoint will be used to play).</td>
</tr>
</tbody>
</table>

<p>Let me go into a bit more detail about some of the concepts I described in the previous list.</p>

### Client Apps

The client applications will need to register into the system to start using it. All endpoints (except for the first one on the list) are secured and will require a valid application key to be sent with the request. In order to obtain that key, client apps need to simply request one. Once provided, they will last for as long as they are used, or will expire after a month of not being used. This behavior is controlled by storing the key in Redis and setting a one-month long TTL to it.

### Game Instance

Creating a new game basically means creating a new instance of a particular game. This new instance will contain a copy of all of the scenes and their content. Any modifications done to the game will only affect the party. This way, many groups can play the same game on their own individual way.

### Player’s Game State

This is similar to the previous one, but unique to each player. While the game instance holds the game state for the entire party, the player’s game state holds the current status for one particular player. Mainly, this holds inventory, position, current scene and HP (health points).

### Player Commands

Once everything is set up and the client application has registered and joined a game, it can start sending commands. The implemented commands in this version of the engine include: <code>move</code>, <code>look</code>, <code>pickup</code> and <code>attack</code>.

<ul>
<li>The <code>move</code> command will allow you to traverse the map. You’ll be able to specify the direction you want to move towards and the engine will let you know the result. If you take a quick glimpse at <a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">Part 1</a>, you can see the approach I took to handle maps. (In short, the map is represented as a graph, where each node represents a room or scene and is only connected to other nodes that represent adjacent rooms.)<br /><br />The distance between nodes is also present in the representation and coupled with the standard speed a player has; going from room to room might not be as simple as stating your command, but you’ll also have to traverse the distance. In practice, this means that going from one room to the other might require several move commands). The other interesting aspect of this command comes from the fact that this engine is meant to support multiplayer parties, and the party can’t be split (at least not at this time).<br /><br />Therefore, the solution for this is similar to a voting system: every party member will send a move command request whenever they want. Once more than half of them have done so, the most requested direction will be used.</li>
<li><code>look</code> is quite different from move. It allows the player to specify a direction, an  item or NPC they want to inspect. The key logic behind this command, comes into consideration when you think about status-dependant descriptions.<br /><br />For example, let’s say that you enter a new room, but it’s completely dark (you don’t see anything), and you move forward while ignoring it. A few rooms later, you pick up a lit torch from a wall. So now you can go back and re-inspect that dark room. Since you’ve picked up the torch, you now can see inside of it, and be able to interact with any of the items and NPCs you find in there.<br /><br />This is achieved by maintaining a game wide and player specific set of status attributes and allowing the game creator to specify several descriptions for our status-dependant elements in the JSON file. Every description is then equipped with a default text and a set of conditional ones, depending on the current status. The latter are optional; the only one that is mandatory is the default value.<br /><br />Additionally, this command has a short-hand version for <code>look at room: look around</code>; that is because players will be trying to inspect a room very often, so providing a short-hand (or alias) command that is easier to type makes a lot of sense.</li>
<li>The <code>pickup</code> command plays a very important role for the gameplay. This command takes care of adding items into the players inventory or their hands (if they’re free). In order to understand where each item is meant to be stored, their definition has a “destination” property that specifies if it is meant for the inventory or the player’s hands. Anything that is successfully picked up from the scene is then removed from it, updating the game instance’s version of the game.</li>
<li>The <code>use</code> command will allow you to affect the environment using items in your inventory. For instance, picking up a key in a room will allow you to use it to open a locked door in another room.</li>
<li>There is a special command, one that is not gameplay-related, but instead a helper command meant to obtain particular information, such as the current game ID or the player’s name. This command is called <strong>get</strong>, and the players can use it to query the game engine. For example: <em>get gameid</em>.</li>
<li>Finally, the last command implemented for this version of the engine is the <code>attack</code> command. I already covered this one; basically, you’ll have to specify your target and the weapon you’re attacking it with. That way the system will be able to check the target’s weaknesses and determine the output of your attack.</li>
</ul>

{{% ad-panel-leaderboard %}}

### Client-Engine Interaction

<p>In order to understand how to use the above-listed endpoints, let me show you how any would-be-client can interact with our new API.</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Step</th>
			<th>Description</th>
		</tr>
	</thead>
<tbody>
<tr>
<td>Register client</td>
<td>First things first, the client application needs to request an API key to be able to access all other endpoints. In order to get that key, it needs to register on our platform. The only parameter to provide is the name of the app, that’s all.</td>
</tr>
<tr>
<td>Create a game</td>
<td>After the API key is obtained, the first thing to do (assuming this is a brand new interaction) is to create a brand new game instance. Think about it this way: the JSON file I created in my last post contains the game’s definition, but we need to create an instance of it just for you and your party (think classes and objects, same deal). You can do with that instance whatever you want, and it will not affect other parties.</td>
</tr>
<tr>
<td>Join the game</td>
<td>After creating the game, you’ll get a game ID back from  the engine. You can then use that game ID to join the instance using your unique username. Unless you join the game, you can’t play, because joining the game will also create a game state instance for you alone. This will be where your inventory, your position and your basic stats are saved in relation to the game you’re playing. You could potentially be playing several games at the same time, and in each one have independent states.</td>
</tr>
<tr>
<td>Send commands</td>
<td>In other words: play the game. The final step is to start sending commands. The amount of commands available was already covered, and it can be easily extended (more on this in a bit). Everytime you send a command, the game will return the new game state for your client to update your view accordingly.</td>
</tr>
</tbody>
</table>

{{% ad-panel-leaderboard %}}

## Let’s Get Our Hands Dirty

<p>I’ve gone over as much design as I can, in the hopes that that information will help you understand the following part, so let’s get into the nuts and bolts of the game engine.</p>

<p><strong>Note</strong>: <em>I will not be showing you the full code in this article since it’s quite big and not all of it is interesting. Instead, I’ll show the more relevant parts and <a href="https://github.com/deleteman/tardis-project-engine">link to the full repository</a> in case you want more details.</em></p>

### The Main File

<p>First things first: this is an Express project and it’s based boilerplate code was generated using Express’ own generator, so the <em>app.js</em> file should be familiar to you. I just want to go over two tweaks I like to do on that code to simplify my work.</p>

<p>First, I add the following snippet to automate the inclusion of new route files:</p>

<pre><code class="language-javascript">const requireDir = require("require-dir")
const routes = requireDir("./routes")

//...

Object.keys(routes).forEach( (file) => {
    let cnt = routes[file]
    app.use('/' + file, cnt)
})</code></pre>

<p>It’s quite simple really, but it removes the need to manually require each route files you create in the future. By the way, <code>require-dir</code> is a simple module that takes care of auto-requiring every file inside a folder. That’s it.</p>

<p>The other change I like to do is to tweak my error handler just a little bit. I should really start using something more robust, but for the needs at hand, I feel like this gets the work done:</p>

<pre><code class="language-javascript">// error handler
app.use(function(err, req, res, next) {
  // render the error page
  if(typeof err === "string") {
    err = {
      status: 500,
      message: err
    }
  }
  res.status(err.status || 500);
  let errorObj = {
    error: true,
    msg: err.message,
    errCode: err.status || 500
  }
  if(err.trace) {
    errorObj.trace = err.trace
  }

  res.json(errorObj);
});</code></pre>

<p>The above code takes care of the different types of error messages we might have to deal with &mdash; either full objects, actual error objects thrown by Javascript or simple error messages without any other context. This code will take it all and format it into a standard format.</p>

### Handling Commands

<p class="c-pre-sidenote--left">This is another one of those aspects of the engine that had to be easy to extend. In a project like this one, it makes total sense to assume new commands will pop up in the future. If there is something you want to avoid, then that would probably be avoid making changes on the base code when trying to add something new three or four months in the future.</p><p class="c-sidenote c-sidenote--right">No amount of code comments will make the task of modifying code you haven’t touched (or even thought about) in several months easy, so the priority is to avoid as many changes as possible. Lucky for us, there are a few patterns we can implement to solve this. In particular, I used a mixture of the Command and the Factory patterns.</p>

<p>I basically encapsulated the behavior of each command inside a single class which inherits from a <code>BaseCommand</code> class that contains the generic code to all commands. At the same time, I added a <code>CommandParser</code> module that grabs the string sent by the client and returns the actual command to execute.</p>

<p>The parser is very simple since all implemented commands now have the actual command as to their first word (i.e. “move north”, “pick up knife”, and so on) it’s a simple matter of splitting the string and getting the first part:</p>

<pre><code class="language-javascript">const requireDir = require("require-dir")
const validCommands = requireDir('./commands')

class CommandParser {


    constructor(command) {
        this.command = command
    }


    normalizeAction(strAct) {
        strAct = strAct.toLowerCase().split(" ")[0]
        return strAct
    }


    verifyCommand() {
        if(!this.command) return false
        if(!this.command.action) return false
        if(!this.command.context) return false

        let action = this.normalizeAction(this.command.action)

        if(validCommands[action]) {
            return validCommands[action]
        }
        return false
    }

    parse() {
        let validCommand = this.verifyCommand()
        if(validCommand) {
            let cmdObj = new validCommand(this.command)
            return cmdObj
        } else {
            return false
        }
    }
}</code></pre>

<p><strong>Note</strong>: <em>I’m using the <code>require-dir</code> module once again to simplify the inclusion of any existing and new command classes. I simply add it to the folder and the entire system is able to pick it up and use it.</em></p>

<p>With that being said, there are many ways this can be improved; for instance, by being able to add synonym support for our commands would be a great feature (so saying “move north”, “go north” or even “walk north” would mean the same). That is something that we could centralize in this class and affect all commands at the same time.</p>

<p>I won’t go into details on any of the commands because, again, that’s too much code to show here, but you can see in the following route code how I managed to generalize that handling of the existing (and any future) commands:</p>

<pre><code class="language-javascript">/**  
Interaction with a particular scene
*/
router.post('/:id/:playername/:scene', function(req, res, next) {

    let command = req.body
    command.context = {
        gameId: req.params.id,
        playername: req.params.playername,
    }

    let parser = new CommandParser(command)

    let commandObj = parser.parse() //return the command instance
    if(!commandObj) return next({ //error handling
        status: 400,
          errorCode: config.get("errorCodes.invalidCommand"),
        message: "Unknown command"
    })

    commandObj.run((err, result) => { //execute the command
        if(err) return next(err)

        res.json(result)
    })

})</code></pre>

<p>All commands only require the <code>run</code> method &mdash; anything else is extra and meant for internal use.</p>

<p>I encourage you to go and review the <a href="https://github.com/deleteman/tardis-project-engine">entire source code</a> (even download it and play with it if you like!). In the next part of this series, I’ll show you the actual client implemention and interaction of this API.</p>

## Closing Thoughts

<p>I may not have covered a lot of my code here, but I still hope that the article was helpful to show you how I tackle projects &mdash; even after the initial design phase. I feel like a lot of people try to start coding as their first response to a new idea and that sometimes can end up discouraging to a developer since there is no real plan set nor any goals to achieve &mdash; other than having the final product ready (and that is too big of a milestone to tackle from day 1). So again, my hope with these articles is to share a different way to go about working solo (or as part of a small group) on big projects.</p>

<p>I hope you’ve enjoyed the read! Please feel free to leave a comment below with any type of suggestions or recommendations, I’d love to read what you think and if you’re eager to start testing the API with your own client-side code.</p>

<p><em>See you on the next one!</em></p>

<div class="c-felix-the-cat">
<h4 class="h3">Other Parts Of This Series</h4>
<ul>
  <li><a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">Part 1</a>: The Introduction</li>
  <li><a href="https://www.smashingmagazine.com/2019/10/multiplayer-text-adventure-engine-node-js-part-3/">Part 3</a>: Creating The Terminal Client</li>
  <li><a href="https://www.smashingmagazine.com/2019/11/multiplayer-text-adventure-engine-node-js-part-4/">Part 4</a>: Adding Chat Into Our Game</li>
</ul>
</div>

{{< signature "dm, yk, il" >}}
