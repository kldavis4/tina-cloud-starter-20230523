---
title: 'Writing A Multiplayer Text Adventure Engine In Node.js: Adding Chat Into Our Game (Part 4)'
slug: multiplayer-text-adventure-engine-node-js-part-4
author: fernando-doglio
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a01ceda5-bc55-4aaa-8b75-15dc1ef9d5df/multiplayer-text-adventure-engine-node-js.png
date: 2019-11-06T11:00:00+02:00
summary: >-
  This is the final part of a series on how to create your own multiplayer text adventure engine. Today, we’ll focus on adding chat support to the text client from <a href="https://www.smashingmagazine.com/2019/10/multiplayer-text-adventure-engine-node-js-part-3/">part 3</a>. We’ll go through the basic design of a chat server using Node.js and socket.io, the basic interaction with the UI, and how we’ve integrated the chat code into the existing UI.
description: >-
  This is the final part of a series on how to create your own multiplayer text adventure engine. Today, we’ll focus on adding chat support to the text client from <a href="https://www.smashingmagazine.com/2019/10/multiplayer-text-adventure-engine-node-js-part-3/">part 3</a>. We’ll go through the basic design of a chat server using Node.js and socket.io, the basic interaction with the UI, and how we’ve integrated the chat code into the existing UI.
categories:
  - Node.js
  - JavaScript
---
<p>Any platform that allows for collaborative play between people will be required to have one very particular characteristic: the ability for players to (somehow) talk to each other. That is exactly why our text-adventure engine built in Node.js would not be complete without a way for the party members to be able to communicate with each other. And because this is indeed a <em>text</em> adventure, that form of communication will be presented in the form of a chat window.</p>

<p>So in this article, I’m going to explain how I added chat support for the text client as well as how I designed a quick chat server using Node.js.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Other Parts Of This Series</h4>
<ul>
  <li><a href="https://www.smashingmagazine.com/2018/12/multiplayer-text-adventure-engine-node-js/">Part 1</a>: The Introduction</li>
  <li><a href="https://www.smashingmagazine.com/2019/10/multiplayer-text-adventure-engine-node-js-part-2/">Part 2</a>: Game Engine Server Design</li>
  <li><a href="https://www.smashingmagazine.com/2019/10/multiplayer-text-adventure-engine-node-js-part-3/">Part 3</a>: Creating The Terminal Client</li>
</ul>
</div>

## Back To The Original Plan

<p>Lack of design skills aside, this has been the original wireframe/mock-up for the text-based client we built in the previous part of the series:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bd43e7-5f3c-48aa-b837-fad3bd2d9001/ui-wireframe.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bd43e7-5f3c-48aa-b837-fad3bd2d9001/ui-wireframe.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bd43e7-5f3c-48aa-b837-fad3bd2d9001/ui-wireframe.png'>Large preview</a>)" alt="" >}}

<p>The right side of that image is meant for inter-player communications, and it’s been planned as a chat since the beginning. Then, during the development of this particular module (the text client), I managed to simplify it into the following:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b17fad-3c2c-46e1-9a86-bf5782fcad70/client-ss2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b17fad-3c2c-46e1-9a86-bf5782fcad70/client-ss2.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b17fad-3c2c-46e1-9a86-bf5782fcad70/client-ss2.png'>Large preview</a>)" alt="" >}}

<p>Yes, we already covered this image in the previous installment but our focus was the left half. Today, however, our focus will be on the right half of what you’re seeing there. In other words:</p>

<ul>
<li>Adding the ability to reactively pull data from a third-party service and update a content window.</li>
<li>Adding support to the command interface for chat commands. Essentially changing the way commands work out of the box and adding support for things, such as “sending a message to the rest of the team”.</li>
<li>Create a basic chat server on the back-end that can facilitate team communication.</li>
</ul>

<p>Let me start with the last one before moving on to how to modify our existing code.</p>

{{% feature-panel %}}

## Creating The Chat Server

<p>Before even looking at any code, one of the first things one should do is to quickly define the scope of any new project. Particularly with this one, we need to make sure we don’t spend a  lot of time working on features we might not need for our particular use case.</p>

<p>You see, all we need is for the party members to be able to send messages with each others, but when one thinks of a “chat server”, other features often come in mind (such as chat rooms, private messages, emojis and so on).</p>

<p>So in order to keep our work manageable and get something out that works, here is what the chat server module will actually do:</p>

<ul>
<li>Allow for a single room per party. Meaning, the actual room for a party will be auto-created when the game itself is created and the first player starts playing. All subsequent party members will join the same room, automatically and without a choice.</li>
<li>There will not be support for private messages. There is no need to be secretive in your party. At least not in this first version.
Users will only be able to send messages through the chat, nothing else.</li>
<li>And to make sure everyone is aware, the only notification sent to the entire party, will be when new players join the game. That’s all.</li>
</ul>

<p>The following diagram shows the communication between servers and clients. As I mentioned, the mechanics are quite simple, so the most important bit to highlight here is the fact that we’re keeping conversations contained within the same party members:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cd1a12e-3541-48d8-ba84-b5b08169ae0d/chat-comms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cd1a12e-3541-48d8-ba84-b5b08169ae0d/chat-comms.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cd1a12e-3541-48d8-ba84-b5b08169ae0d/chat-comms.png'>Large preview</a>)" alt="" >}}

## The Tools For The Job

<p>Given the above restrictions and the fact that all we need is a direct connection between the clients and the chat server, we’ll solve this problem with an old fashion socket. Or in other words, the main tool we’ll be using is <a href="https://socket.io/">socket.io</a> (note that there are 3rd party services providing managed chat servers, for instance, but for the purposes of this, going there would the equivalent of killing a mosquito with a shotgun).</p>

<p>With <em>socket.io</em> we can establish a bidirectional, real-time,  event-based communication between the server and the clients. Unlike what we did with the game engine, where we published a REST API, the socket connection provides a faster way of communication.</p>

<p>Which is exactly what we need, a quick way to connect clients and server, exchanging messages and sending broadcasts between them.</p>

{{% ad-panel-leaderboard %}}

### Designing A Chat Server

<p>Although socket.io is quite magical when it comes to socket management, it’s not a full chat server, we still need to define some logic to use it.</p>

<p>For our particularly small list of features, the design of our server’s internal logic should look something like this:</p>

<ul>
<li>The server will need to support at least two different event types:
<ol>
<li><strong>New message</strong><br />This one is obvious, we need to know when a new message from a client is received, so we’ll need support for this type of event.</li>
<li><strong>New user joined</strong><br />We’ll need this one just to make sure we can notify the entire party when a new user joins the chat room.</li>
</ol></li>
<li>Internally, we’ll handle chat rooms, even though that concept will not be something public to clients. Instead, all they will send is the game ID (the ID players use to join the game). With this ID we’ll use socket.io’s rooms feature which handles individual rooms for us.</li>
<li>Because of how socket.io works, it keeps an in-memory session open that is automatically assigned to the socket created for each client. In other words, we have a variable automatically assigned to each individual client where we can store information, such as player names, and room assigned. We’ll be using this socket-session to handle some internal client-room associations.</li>
</ul>

#### A Note About In-Memory Sessions

In-memory storage is not always the best solution. For this particular example, I’m going with it because it simplifies the job. That being said, a good and easy improvement you could implement if you wanted to take this into a production-ready product would be to substitute it with a [Redis](https://www.redis.io) instance. That way you keep the in-memory performance but add an extra layer of reliability in case something goes wrong and your process dies.

<p>With all of that being said, let me show you the actual implementation.</p>

### The Implementation

<p>Although the full project can be seen on <a href="https://github.com/deleteman/tardis-project-chatserver">GitHub</a>, the most relevant code lies in the main file (<em>index.js</em>):</p>

<div class="break-out">

<pre><code class="language-javascript">// Setup basic express server
let express = require('express');
let config = require("config")
let app = express();
let server = require('http').createServer(app);
let io = require('socket.io')(server);
let port = process.env.PORT || config.get('app.port');

server.listen(port, () => {
  console.log('Server listening at port %d', port);
});

let numUsers = 0;


io.on('connection', (socket) => {
  let addedUser = false;

  // when the client emits 'new message', this listens and executes
  socket.on(config.get('chat.events.NEWMSG'), (data, done) => {
    let room = socket.roomname
    if(!socket.roomname) {
        socket.emit(config.get('chat.events.NEWMSG'), "You're not part of a room yet")
        return done()
    }

    // we tell the client to execute 'new message'
    socket.to(socket.roomname).emit(config.get('chat.events.NEWMSG'), {
      room: room,
      username: socket.username,
      message: data
    });
    done()
  });

  socket.on(config.get('chat.events.JOINROOM'), (data, done) => {
      console.log("Requesting to join a room: ", data)

      socket.roomname = data.roomname
      socket.username = data.username
      socket.join(data.roomname, _ => {
          socket.to(data.roomname).emit(config.get('chat.events.NEWMSG'), {
            username: 'Game server',
            message: socket.username + ' has joined the party!'
          })
          done(null, {joined: true})
      })
  })

  // when the user disconnects.. perform this
  socket.on('disconnect', () => {
    if (addedUser) {
      --numUsers;

      // echo globally that this client has left
      socket.to(socket.roomname).emit('user left', {
        username: socket.username,
        numUsers: numUsers
      });
    }
  });
});</code></pre>
</div>

<p>That is all there is for this particular server. Simple right? A couple of notes:</p>

<ol>
<li>I’m using the <a href="https://www.npmjs.com/package/config">config module</a> to handle all my constants. I personally love this module, it simplifies my life every time I need to keep “magic numbers” out of my code. So everything from the list of accepted messages to the port the server will listen to are stored and accessed through it.</li>
<li>There are two main events to pay attention to, just like I said before. 
<ul>
<li>When a new message is received, which can be seen when we listen for <code>config.get('chat.events.NEWMSG')</code>. This code also makes sure you don’t accidentally try to send a message before joining a room. This shouldn’t happen if you implement the chat client correctly, but just in case these type of checks are always helpful when others are writing the clients for your services.</li>
<li>When a new user joins a room. You can see that event on the <code>config.get('chat.events.JOINROOM')</code> listener. In that case, all we do is add the user to the room (again, this is handled by socket.io, so all it takes is a single line of code) and then we broadcast to the room a message notifying who just joined. The key here is that by using the socket instance of the player joining, the broadcast will be sent to everyone in the room <em>except</em> the player. Again, behavior provided by <em>socket.io</em>, so  we don’t have to add this in.</li>
</ul></li>
</ol>

<p>That is all there is to the server code, let’s now review how I integrated the client-side code into the text-client project.</p>

{{% ad-panel-leaderboard %}}

## Updating The Client Code

<p>In order to integrate both, chat commands and game commands, the input box at the bottom of the screen will have to parse the player’s input and decide on what they’re trying to do.</p>

<p>The rule is simple: If the player is trying to send a message to the party, they’ll start the command with the word “chat”, otherwise, they won’t.</p>

### What Happens When Sending A Chat Message?

<p>The following list of actions takes place when the user hits the ENTER key:</p>

<ol>
<li>Once a chat command is found, the code will trigger a new branch, where a chat client library will be used and a new message will be sent (emitted through the active socket connection) to the server.</li>
<li>The server will emit the same message to all other players in the room.</li>
<li>A callback (setup during boot-time) listening for new events from the server will be triggered. Depending on the event type (either a player sent a message, or a player just joined), we’ll display a message on the chat box (i.e the text box on the right).</li>
</ol>

<p>The following diagram presents a graphic representation of the above steps; ideally, it should help visualize which components are involved in this process:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c9b316-d791-4a1d-bfd6-c018e58658bf/client-chat.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c9b316-d791-4a1d-bfd6-c018e58658bf/client-chat.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c9b316-d791-4a1d-bfd6-c018e58658bf/client-chat.png'>Large preview</a>)" alt="" >}}

### Reviewing The Code Changes

<p>For a full list of changes and the entire code working, you should check the full <a href="https://github.com/deleteman/tardis-project-client">repository on Github</a>. Here, I’m quickly going to glance over some of the most relevant bits of code.</p>

<p>For example, setting up the main screen is where we now trigger the connection with the chat server and where we configure the callback for updating the chat box (red box on the top from the diagram above).</p>

<div class="break-out">

<pre><code class="language-javascript">setUpChatBox: function() {
        let handler = require(this.elements["chatbox"].meta.handlerPath)
        handler.handle(this.UI.gamestate, (err, evt) => {
            if(err) {
                this.UI.setUpAlert(err)    
                return this.UI.renderScreen()
            }

            if(evt.event == config.get('chatserver.commands.JOINROOM')) {
                this.elements["chatbox"].obj.insertBottom(["::You've joined the party chat room::"])
                this.elements["chatbox"].obj.scroll((config.get("screens.main-ui.elements.gamebox.autoscrollspeed") ) + 1)
            }
            if(evt.event == config.get('chatserver.commands.SENDMSG')) {
                this.elements["chatbox"].obj.insertBottom([evt.msg.username + ' said :> ' + evt.msg.message])
                this.elements["chatbox"].obj.scroll((config.get("screens.main-ui.elements.gamebox.autoscrollspeed") ) + 1)
            }
            this.UI.renderScreen()
        })

    },</code></pre>
</div>

<p>This method gets called from the init method, just like everything else. The main function for this code is to use the assigned handler (the chatbox handler) and call it’s <em>handle</em> method, which will connect to the chat server, and afterwards, setup the callback (which is also defined here) to be triggered when something happens (one of the two events we support).</p>

<p>The interesting logic from the above snippet is inside the callback, because it’s the logic used to update the chat box.</p>



<p>For completeness sake, the code that connects to the server and configures the callback shown above is the following:</p>

<div class="break-out">

<pre><code class="language-javascript">const io = require('socket.io-client'),
    config = require("config"),
    logger = require("../utils/logger")


// Use https or wss in production.
let url = config.get("chatserver.url") 
let socket = io(url)


module.exports = {

    connect2Room: function(gamestate, done) {
        socket.on(config.get('chatserver.commands.SENDMSG'), msg => {
            done(null, {
                event: config.get('chatserver.commands.SENDMSG'),
                msg: msg
            })     
        })
        socket.emit(config.get("chatserver.commands.JOINROOM") , {
            roomname: gamestate.gameID,
            username: gamestate.playername
        }, _ => {
            logger.info("Room joined!")
            gamestate.inroom = true
            done(null, {
                event: config.get('chatserver.commands.JOINROOM')
            })
        })
        
    },

   handleCommand: function(command, gamestate, done) {
        logger.info("Sending command to chatserver!")
        
        let message = command.split(" ").splice(1).join(" ")

        logger.info("Message to send: ", message)

        if(!gamestate.inroom) { //first time sending the message, so join the room first
            logger.info("Joining a room")
            let gameId = gamestate.game
            
    socket.emit(config.get("chatserver.commands.JOINROOM") , {
                roomname: gamestate.gameID,
                username: gamestate.playername
            }, _ => {
                logger.info("Room joined!")
                gamestate.inroom = true
                updateGameState = true

                logger.info("Updating game state ...")
                socket.emit(config.get("chatserver.commands.SENDMSG"), message, done)
            })
        } else {
            logger.info("Sending message to chat server: ", message  )
            socket.emit(config.get("chatserver.commands.SENDMSG"), message, done)
        }
            
    }
}</code></pre>
</div>

<p>The <code>connect2room</code> method is the one called during setup of the main screen as I mentioned, you can see how we set up the handler for new messages and emit the event related to joining a room (which then triggers the same event being broadcasted to other players on the server-side).</p>

<p>The other method, <code>handleCommand</code> is the one that takes care of sending the chat message to the server (and it does so with a simple <code>socket.emit</code>). This one is executed when the <code>commandHandler</code> realizes a chat message is being sent. Here is the code for that logic:</p>

<div class="break-out">

<pre><code class="language-javascript">module.exports = {
    handle: function(gamestate, text, done) {
        let command = text.trim()
        if(command.indexOf("chat") === 0) { //chat command
            chatServerClient.handleCommand(command, gamestate, done)
        } else {
            sendGameCommand(gamestate, text, done)
        }     
    }
}</code></pre>
</div>

<p>That is the new code for the commandHandler, the sendGameCommand function is where the old code now is encapsulated (nothing changed there).</p>

<p>And that is it for the integration, again, fully working code can be downloaded and tested from the <a href="https://github.com/deleteman/tardis-project-client">full repository</a>.</p>

## Final Thoughts

<p>This marks the end of the road for this project. If you stuck to it until the end, thanks for reading! The code is ready to be tested and played with, and if you happen to do so, please reach out and let me know what you thought about it.</p>

<p>Hopefully with this project, many old-time fans of the genre can get back to it and experience it in a way they never did.</p>

<p>Have fun playing (and coding)!</p>

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Building A Pub/Sub Service In-House Using Node.js And Redis'" href="https://www.smashingmagazine.com/2018/06/pub-sub-service-in-house-node-js-redis/" rel="bookmark">Building A Pub/Sub Service In-House Using Node.js And Redis</a></li>
<li><a title="Read 'Building A Node.js Express API To Convert Markdown To HTML'" href="https://www.smashingmagazine.com/2019/04/nodejs-express-api-markdown-html/" rel="bookmark">Building A Node.js Express API To Convert Markdown To HTML</a></li>
<li><a title="Read 'Get Started With Node: An Introduction To APIs, HTTP And ES6+ JavaScript'" href="https://www.smashingmagazine.com/2019/02/node-api-http-es6-javascript/" rel="bookmark">Get Started With Node: An Introduction To APIs, HTTP And ES6+ JavaScript</a></li>
<li><a title="Read 'Keeping Node.js Fast: Tools, Techniques, And Tips For Making High-Performance Node.js Servers'" href="https://www.smashingmagazine.com/2018/06/nodejs-tools-techniques-performance-servers/" rel="bookmark">Keeping Node.js Fast: Tools, Techniques, And Tips For Making High-Performance Node.js Servers</a></li>
</ul>

{{< signature "dm, yk, il" >}}
