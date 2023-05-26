---
title: Building A Real-Time Retrospective Board With Video Chat
slug: building-a-real-time-retrospective-board-with-video-chat
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77d1e2c8-1fe7-4c26-ad81-459e85004d4a/01-realtime-retrospective-board-preview-opt.png
date: 2016-03-08T18:46:50.000Z
author: wolframhempel
description: >-
  If you’ve ever worked in an agile environment, chances are you’ve had your
  share of “retrospectives” — meetings where people write what made them “glad,”
  “mad” or “sad” onto different-colored notes, post them onto a board, arrange
  them in groups and — most importantly — talk about them.

  These meetings are straightforward, as long as everyone is in the same room.
  But if you’re working with a locally distributed team, things can get a bit
  tricky. Let’s address this by creating a virtual version of our board to allow
  team members in different locations to hold their retrospective just as if
  they were in the same room.
categories:
  - Coding
  - Techniques
  - jQuery
  - Node.js
---
If you’ve ever worked in an agile environment, chances are you’ve had your share of “retrospectives” — meetings where people write what made them “glad,” “mad” or “sad” onto different-colored notes, post them onto a board, arrange them in groups and — most importantly — talk about them.

These meetings are straightforward, as long as everyone is in the same room. But if you’re working with a locally distributed team, things can get a bit tricky.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Build A Real-Time Commenting System](https://www.smashingmagazine.com/2012/05/building-real-time-commenting-system/)
*   [Real-Time Data And A More Personalized Web](https://www.smashingmagazine.com/2011/04/real-time-data-and-a-more-personalized-web/)
*   [Spicing Up Your Website With jQuery Goodness](https://www.smashingmagazine.com/2010/06/spice-up-your-website-with-jquery-goodness/)
*   [Where Have All The Comments Gone?](https://www.smashingmagazine.com/2010/11/critical-thinking-vs-critical-acclaim-where-have-all-the-comments-gone/)

Let’s address this by creating a virtual version of our board to allow team members in different locations to hold their retrospective just as if they were in the same room.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af6d97de-528c-4eb9-b491-03fa58a12de5/01-realtime-retrospective-board-opt.png"><img title="Real-time retrospective board." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77d1e2c8-1fe7-4c26-ad81-459e85004d4a/01-realtime-retrospective-board-preview-opt.png" alt="The final retrospective board with video chat" /></a><figcaption>The final retrospective board with video chat. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af6d97de-528c-4eb9-b491-03fa58a12de5/01-realtime-retrospective-board-opt.png">View large version</a>)</figcaption></figure>

Our “virtual retrospective board” needs to allow team members to:

*   create, edit and move sticky notes;
*   sync the current state of the board in real time between all team members;
*   talk about the board via video chat.

It also needs to:

*   make sure users log in with the right password.

To achieve this, we’ll be using:

*   a bit of [jQuery](https://jquery.com/) (chances are you’ll pick your M*C framework of choice, but let’s keep things simple);
*   [deepstream](https://deepstream.io/) (an open-source Node.js server that comes with all sorts of real-time functionality, like pub-sub, remote procedure calls and, most importantly for our sticky-notes board, data sync and WebRTC for video communication).

One more thing:

*   You can find [all files for this tutorial on GitHub](https://github.com/hoxton-one/realtime-retrospective-board).</p>

## Let’s Fire Up The Server

Simply install deepstream via <code>npm install deepstream.io</code>, and create a file (for example, <code>start.js</code>) with the following content:

<pre><code class="language-javascript">var DeepstreamServer = require( 'deepstream.io' );
var tutorialServer = new DeepstreamServer();
tutorialServer.set( 'host', 'localhost' );
tutorialServer.set( 'port', 6020 );
tutorialServer.start();
</code></pre>

Run it with <code>node start.js</code>, and you should see this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ec424e8-549b-45a6-b461-373b6d53ec81/02-deepstream-console-output-opt.png"><img title="The output from deepstream's startup console" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/997d38d3-6489-4829-870d-a944f0eece7c/02-deepstream-console-output-preview-opt.png" alt="The output from deepstream's startup console" /></a><figcaption>The output from deepstream’s startup console. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ec424e8-549b-45a6-b461-373b6d53ec81/02-deepstream-console-output-opt.png">View large version</a>)</figcaption></figure>

Nice. Now, let’s stop it again. What, why? Well, at the moment, our server is open to the world. Anyone can connect to it and learn what happened in our retrospective. Let’s make sure that every user connecting to deepstream at least knows the password, <code>sesame</code>. To do this, we need to register a <code>permissionHandler</code> — an object that checks whether a client is allowed to log in and whether it may perform a certain action. So, let’s use the same <code>tutorialServer.set()</code> method we’ve used before.</p>

<pre><code class="language-javascript">
tutorialServer.set( 'permissionHandler', {
  isValidUser: function( connectionData, authData, callback ) {
    // We don't care what the user name is, 
    // as long as one is specified.
    if( !authData.username ) {
      callback( 'No username specified' );
    }
    // Let's keep things simple and expect the same password
    // from all users.
    else if( authData.password !== 'sesame' ) {
      callback( 'Wrong password' );
    }
    // All good. Let's log the user in.
    else {
      callback( null, authData.username );
    }
  },
  canPerformAction: function( username, message, callback ) {
     // Allow everything as long as the client is logged in.
    callback( null, true );
  }
});
</code></pre>

That’s it. If you’d like to learn more about security in deepstream, have a look at the authentication and permissioning tutorials.</p>

## Connecting And Logging In

Time to get cracking on the client. Let’s either create a basic HTML app structure or just <a href="https://github.com/hoxton-one/realtime-retrospective-board">clone the project from GitHub</a>. The first thing you’ll need is deepstream’s client script. You can get it via <code>bower install deepstream.io-client-js</code> or <a href="https://deepstream.io">from the “Downloads” page</a>.

Once you’ve got it, let’s connect to our deepstream server:

<pre><code class="language-javascript">var ds = deepstream( 'localhost:6020' );
</code></pre>

So, are we connected and ready for some real-time awesomeness? Um, not quite. At the moment, our connection is in a kind of quarantine state, waiting for the user to log in. To do this, we’ll create the world’s most basic log-in form:

<pre><code class="language-markup">&lt;form action="#"&gt;
  &lt;div class="login-error"&gt;&lt;/div&gt;
  &lt;input type="text" placeholder="username"/&gt;
  &lt;input type="password" placeholder="password"/&gt;
  &lt;input type="submit" value="login" /&gt;
&lt;/form&gt;
</code></pre>

Once the user hits the log-in button, we’ll read the values from the form, send them to deepstream using its <code>login()</code> method and wait for the response. Should the response be positive (<code>success === true</code>), we’ll hide the log-in form and start the application. Otherwise, we’ll show the error message that we set in <code>permissionHandler</code> earlier (for example, <code>callback( 'No username specified' );</code>).</p>

<pre><code class="language-javascript">$( 'form' ).on( 'submit', function( event ){
  event.preventDefault();

  var authData = {
    username: $( 'form input[type="text"]' ).val(),
    password: $( 'form input[type="password"]' ).val()
  };

  ds.login( authData, function( success, errorEvent, errorMessage ) {
    if( success ) {
      new StickyNoteBoard( ds );
      new VideoChat( ds, authData.username );
      $( 'form' ).hide();
    } else {
      $( '.login-error' ).text( errorMessage ).show();
    }   
  });
});
</code></pre>

## Building The Board

Phew! Finally, we’ve got all of the log-in bits out of the way and can start building the actual UI. But first, let’s talk about records and lists. Deepstream’s data sync is based on a concept called “records.” A record is just a bit of data — any JSON structure will do.

Each record is identified by a unique name:

<pre><code class="language-javascript">var johnDoe = ds.record.getRecord( 'johnDoe' );</code></pre>

Its data can be set like so:

<pre><code class="language-javascript">johnDoe.set({ firstname: 'John', lastname: 'Doe' });
  johnDoe.set( 'age', 28 );
</code></pre>

… and read like so:

<pre><code class="language-javascript">var firstname = johnDoe.get( 'firstname' );
</code></pre>

… and listened to like so:

<pre><code class="language-javascript">var firstname = johnDoe.subscribe( 'age', function( newAge ){ 
  alert( 'happy birthday' ); 
});
</code></pre>

Collections of records are called lists. A list is a flat array of record names. It has methods similar to a record’s but also some specific ones, like <code>hasEntry()</code> and <code>removeEntry()</code>, as well as list-specific events, such as <code>'entry-added'</code>.

For our board, we’ll use both records and lists. The board will be represented as a list, and each sticky note will be an individual record.</p>

<pre><code class="language-javascript">var stickynoteID = this.ds.getUid();
  var stickynote = this.ds.record.getRecord( stickynoteID );

  stickynote.set({
    type: 'glad',
    content: 'Great sprint!',
    position: {
      left: 500,
      top: 200,
    }
  });

  var allStickyNotes = this.ds.record.getList( 'tutorial-board' );
  allStickyNotes.addEntry( stickynoteID );
</code></pre>

## Wiring It Up To The DOM

Now that we’re armed with this knowledge, the next thing to do is set the sticky note’s text in the record whenever the user changes it — and update the DOM whenever a change comes in. If we use a <code>textarea</code> field, here’s what that would look like:

<pre><code class="language-javascript">// Subscribe to incoming changes to the sticky-note text
  this.record.subscribe( 'content', function( value ) {
    this.textArea.val( value );
  }.bind( this ), true );

  // Store and sync changes to the sticky-note text made by this user
  this.textArea.keyup( function() {
    this.record.set( 'content', this.textArea.val() );
  }.bind( this ) );
</code></pre>

## The Hard Bits

Easy enough so far. At this point, your changes will already sync across all connected clients. So, let’s add some dragging to our sticky notes.

This should be fairly straightforward. We’ll just use jQuery’s <code>draggable</code> functionality, and whenever the position changes, we’ll update both the DOM element’s position and the value of the record’s position. OK? But then we’ll also need to subscribe to the record’s <code>position</code> field to apply incoming changes — in which case, we’ll need to differentiate between local and remote changes. Surely, an <code>if</code> condition would… STOP!

Let me stop you right there. Building a collaborative real-time app can be very hard — or very easy, depending on your approach. Don’t try to orchestrate different callbacks to keep local and remote changes in sync. Make your life easier and just use the record as a single source of truth. To stick with our draggable example, here’s what I mean:

<figure><img title="Drag update flow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/673865e8-bcf5-4196-b4f0-6490a101d3aa/03-update-flow-preview-opt.png" alt="Control flow while sticky note is dragged" /><br>
<figcaption>Control flow while sticky note is dragged.</figcaption></figure>

Here it is in code:

<pre><code class="language-javascript">// Update the record's position on screen whenever it is dragged.
  this.record.subscribe( 'position', function( position ) {
    this.element.css( position );
  }.bind( this ), true );

  // Get drag events from the sticky note note using jQuery UI.
  this.element.draggable({
    handle: ".stickynote-header",
    zIndex: 999,
    // Prevent jQuery draggable from updating the DOM's position and
    // leave it to the record instead.
    helper: function(){ return $( '<i></i>' ); },
    drag: function( event, ui ) {
      this.record.set( 'position', ui.position );     
    }.bind( this )
  });
</code></pre>

Notice how the dragging and DOM updates are now decoupled. We’ll apply a similar concept to our sticky note list. Whenever the user clicks “Add note,” we’ll add an entry to the list. Whenever an entry is added to the list (whether locally or by another user), we’ll add a note to the board.</p>

<pre><code class="language-javascript">function StickyNoteBoard( ds ) {
  this.list = ds.record.getList( 'tutorial-board' );
  this.list.on( 'entry-added', this.onStickyNoteAdded.bind( this ) );
  this.list.whenReady( this.onStickyNotesLoaded.bind( this ) );
  $( '.small-stickynote' ).click( this.createStickyNote.bind( this ) );
}

StickyNoteBoard.prototype.onStickyNotesLoaded = function() {
  this.list.getEntries().forEach( this.onStickyNoteAdded.bind( this ) );
};

StickyNoteBoard.prototype.onStickyNoteAdded = function( stickynoteID ) {
  new StickyNote( /*…*/ );
};

StickyNoteBoard.prototype.createStickyNote = function( event ) {
  var stickynoteID = this.ds.getUid();
  var stickynote = this.ds.record.getRecord( stickynoteID );
  // …
  this.list.addEntry( stickynoteID );
};
</code></pre>

These should be all of the main building blocks of our board. Thanks for holding out with me for so long. I’ve skipped a few lines that wire things together; to see the full code, please have a <a href="https://github.com/hoxton-one/realtime-retrospective-board/tree/master/client">look at the GitHub repository</a>.</p>

## Adding Video Chat

Now it’s time to tackle the video-chat part of our retrospective board.</p>

<figure><img title="Video chat via WebRTC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af631f9f-5004-4f1c-99f3-4cbab8d08b94/04-video-chat-preview-opt.png" alt="Video chat via WebRTC" /><br>
<figcaption>Video chat via WebRTC.</figcaption></figure>

Retrospectives are all about people talking to each other. Without communication, even the best collection of suggestions and feedback will remain unused.</p>

## Let’s Talk About WebRTC

Chances are that if you’re working in web technology, you’ve come across WebRTC. It’s an exciting new standard that allows us to transmit audio, video and even data streams directly between browsers without having to route them through a server.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c76b6e9-5b29-489e-bab3-30b29c2b8fac/05-deepstream-webrtc-opt.png"><img title="WebRTC in deepstream" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c76b6e9-5b29-489e-bab3-30b29c2b8fac/05-deepstream-webrtc-opt.png" alt="WebRTC in deepstream" /></a><figcaption>WebRTC in deepstream. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c76b6e9-5b29-489e-bab3-30b29c2b8fac/05-deepstream-webrtc-opt.png">View large version</a>)</figcaption></figure>

However, as far as browser APIs go, WebRTC is one of the most <strong>complicated ones</strong>. And despite being a peer-to-peer protocol, it still requires a server. The reason for all of this is that in order to connect two browsers, both have to know where the other one is — and that is way more complicated than it sounds.

Imagine a friend asking for your address. You answer, “I’m in the bedroom” — leaving it to them to find out which house your bedroom is in, which street your house is on, which town that street is in and so on. And once they can reliably locate your bedroom, you still have to provide a list of windows and doors they have to try to see if one is open.</p>

<a href="https://deepstream.io/tutorials/">Deepstream</a> tries to abstract all of that away and reduce WebRTC to two concepts: a phonebook and a call. We’ll use both to create a video chat room that allows our team to talk about what’s happening on the retrospective board.</p>

## Connect The Streams

Video in a browser comes in the form of a <code>MediaStream</code>. These streams are a combination of audio and video signals that can be played in a <code>video</code> element or sent to someone else via the Internet. You can retrieve a stream from a webcam or microphone, from another user via WebRTC or, once <code>captureStream</code> is fully supported, even from a <code>canvas</code> element.</p>

## Getting Your Local Webcam Stream

Let’s start with our local webcam and microphone stream. It can be retrieved using <code>getUserMedia</code> — and immediately the trouble starts. <code>getUserMedia</code> has been around for a while now, but the API is still not fully standardized and, therefore, is still vendor-prefixed. But help is at hand. The official WebRTC initiative maintains an adapter script that normalizes browser differences and stays up to date with API changes. You can <a href="https://github.com/webrtc/adapter">find it on GitHub</a>.

Once it’s installed, retrieving your local video and audio stream and playing it in a <code>video</code> tag is as simple as this:

<pre><code class="language-javascript">navigator.mediaDevices.getUserMedia({
    video: { width: 160, height: 120 },
    audio: false
  })
  .then(function onStream( stream ) {
        // Mute the local video to eliminate microphone feedback.
        addVideo( stream, true );
    })
  .catch(function onError( error ) {
         // If the user doesn't have a webcam or doesn't allow access,
        // you'll end up here.
    });
);

function addVideo( stream, muted ) {
  var video = $( '&lt;video&gt;&lt;/video&gt;' ).attr({
    'width': '160px',
    'height': '120px',
    'autoplay': 'autoplay',
    'muted': muted,
    'data-username': username
  });
  video[0].srcObject = stream;
  this.outerElement.append( video );
}
</code></pre>

## Make Sure To Handle Errors

Whenever an application requests access to a user’s webcam or microphone, a lot of things can go wrong. A user might not have a webcam at all, might have a webcam but no microphone, might have a webcam that is not able to provide the required resolution, or might have a webcam that simply is not allowed access to their media devices. All of these cases are captured in <code>getUserMedia</code>’s error callback. Have a look at the <a href="https://www.w3.org/TR/mediacapture-streams/#mediastreamerror">official specification</a> for the full lists of errors that could occur.</p>

## Registering For Incoming Calls

Now that we’ve got our local video stream, it’s time to add ourselves to the phonebook and listen for others adding themselves. To let the others know who we are, we’ll use the user name we’ve logged in with.</p>

<pre><code class="language-javascript">// Add ourselves to the phonebook
ds.webrtc.registerCallee( this.username, this.onIncomingCall.bind( this ) );

// Listen for others adding themselves
ds.webrtc.listenForCallees( this.onCallees.bind( this ) );
</code></pre>

<code>ds.webrtc.listenForCallees</code> will invoke <code>this.onCallees</code> immediately with a list of all currently registered callees and then again whenever another users is added or removed from the phonebook.

This will help us solve an inherent problem of peer-to-peer systems: rooms.</p>

## The Problem With Rooms

Rooms are a common concept in every chat application: A number of participants all talk to each other at the same time. With a centralized server, this is easy: You log in and get every participant’s video stream. With a network of peer-to-peer connections, however, things are a bit trickier.

To create a room, every participant has to connect to every other participant exactly once.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cbadab7-3574-4f08-ad50-68402366b73a/06-peer-to-peer-rooms-opt.png"><img title="P2P video chat" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cbadab7-3574-4f08-ad50-68402366b73a/06-peer-to-peer-rooms-opt.png" alt="Many-to-many video chat: server versus peer-to-peer" /></a><figcaption>Many-to-many video chat: server versus peer-to-peer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cbadab7-3574-4f08-ad50-68402366b73a/06-peer-to-peer-rooms-opt.png">View large version</a>)</figcaption></figure>

To achieve this, we’ll assume two things:

*   that the whole phonebook (i.e. the array of callee names, provided by `listenForCallees`) constitutes one room;
*   that every new user has to call all currently present users (this way, the first user to log in won’t call anyone, the second user will call the first, the third user will call the other two and so on).

With this in mind, here’s what our <code>onCallees</code> function will look like:

<pre><code class="language-javascript">VideoChat.prototype.onCallees = function( callees ) {
var call, i, metaData = { user: this.username };

for( i = 0; i &lt; callees.length; i++ ) {
  // No point in calling ourselves.
  if( callees[ i ] === this.username ) continue;
  call = this.ds.webrtc.makeCall(callees[i], metaData, this.localStream);
  call.once( 'established', this.addVideo.bind(this, this.username) );
  call.once( 'ended', this.removeVideo.bind(this, this.username) );
}

  // And done. Let's unsubscribe from future updates.
  this.ds.webrtc.unlistenForCallees();
};
</code></pre>

## Waiting For Incoming Calls

Great! We’re now connected to everyone who’s in the room. The bit that’s left is to accept incoming calls from new participants. When we’ve registered ourselves as a callee, we’ve provided a callback function for incoming calls:

<pre><code class="language-javascript">ds.webrtc.registerCallee(this.username, this.onIncomingCall.bind(this) );</code></pre>

Now it’s time to fill it in:

<pre><code class="language-javascript">VideoChat.prototype.onIncomingCall = function( call, metaData ) {
    call.once( 'established', this.addVideo.bind( this, metaData.user ) );
    call.once( 'ended', this.removeVideo.bind( this, metaData.user ) );
    // Let's not be picky; let’s accept all calls.
    call.accept( this.localStream );
};
</code></pre>

That’s it! From now on, every time you log into the retrospective board, your webcam will spring to life, you’ll be connected to all other members of your team, and every new joiner will automatically connect to you.

Easy enough so far. At this point, your changes will already sync across all connected clients. So, let’s add some dragging to our sticky notes.

This should be fairly straightforward. We’ll just use jQuery’s <code>draggable</code> functionality, and whenever the position changes, we’ll update both the DOM element’s position and the value of the record’s position. OK? But then we’ll also need to subscribe to the record’s <code>position</code> field to apply incoming changes — in which case, we’ll need to differentiate between local and remote changes. Surely, an <code>if</code> condition would… STOP!

Let me stop you right there. Building a collaborative real-time app can be very hard — or very easy, depending on your approach. Don’t try to orchestrate different callbacks to keep local and remote changes in sync. Make your life easier and just use the record as a single source of truth. To stick with our draggable example, here’s what I mean:

<figure><img title="Drag update flow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/673865e8-bcf5-4196-b4f0-6490a101d3aa/03-update-flow-preview-opt.png" alt="Control flow while sticky note is dragged" /><br>
<figcaption>Control flow while sticky note is dragged.</figcaption></figure>

Here it is in code:

<pre><code class="language-javascript">// Update the record's position on screen whenever it is dragged.
  this.record.subscribe( 'position', function( position ) {
    this.element.css( position );
  }.bind( this ), true );

  // Get drag events from the sticky note note using jQuery UI.
  this.element.draggable({
    handle: ".stickynote-header",
    zIndex: 999,
    // Prevent jQuery draggable from updating the DOM's position and
    // leave it to the record instead.
    helper: function(){ return $( '<i></i>' ); },
    drag: function( event, ui ) {
      this.record.set( 'position', ui.position );     
    }.bind( this )
  });
</code></pre>

Notice how the dragging and DOM updates are now decoupled. We’ll apply a similar concept to our sticky note list. Whenever the user clicks “Add note,” we’ll add an entry to the list. Whenever an entry is added to the list (whether locally or by another user), we’ll add a note to the board.</p>

<pre><code class="language-javascript">function StickyNoteBoard( ds ) {
  this.list = ds.record.getList( 'tutorial-board' );
  this.list.on( 'entry-added', this.onStickyNoteAdded.bind( this ) );
  this.list.whenReady( this.onStickyNotesLoaded.bind( this ) );
  $( '.small-stickynote' ).click( this.createStickyNote.bind( this ) );
}

StickyNoteBoard.prototype.onStickyNotesLoaded = function() {
  this.list.getEntries().forEach( this.onStickyNoteAdded.bind( this ) );
};

StickyNoteBoard.prototype.onStickyNoteAdded = function( stickynoteID ) {
  new StickyNote( /*…*/ );
};

StickyNoteBoard.prototype.createStickyNote = function( event ) {
  var stickynoteID = this.ds.getUid();
  var stickynote = this.ds.record.getRecord( stickynoteID );
  // …
  this.list.addEntry( stickynoteID );
};
</code></pre>

These should be all of the main building blocks of our board. Thanks for holding out with me for so long. I’ve skipped a few lines that wire things together; to see the full code, please have a <a href="https://github.com/hoxton-one/realtime-retrospective-board/tree/master/client">look at the GitHub repository</a>.</p>

## Adding Video Chat

Now it’s time to tackle the video-chat part of our retrospective board.</p>

<figure><img title="Video chat via WebRTC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af631f9f-5004-4f1c-99f3-4cbab8d08b94/04-video-chat-preview-opt.png" alt="Video chat via WebRTC" /><br>
<figcaption>Video chat via WebRTC.</figcaption></figure>

Retrospectives are all about people talking to each other. Without communication, even the best collection of suggestions and feedback will remain unused.</p>

## Let’s Talk About WebRTC

Chances are that if you’re working in web technology, you’ve come across WebRTC. It’s an exciting new standard that allows us to transmit audio, video and even data streams directly between browsers without having to route them through a server.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c76b6e9-5b29-489e-bab3-30b29c2b8fac/05-deepstream-webrtc-opt.png"><img title="WebRTC in deepstream" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c76b6e9-5b29-489e-bab3-30b29c2b8fac/05-deepstream-webrtc-opt.png" alt="WebRTC in deepstream" /></a><figcaption>WebRTC in deepstream. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c76b6e9-5b29-489e-bab3-30b29c2b8fac/05-deepstream-webrtc-opt.png">View large version</a>)</figcaption></figure>

However, as far as browser APIs go, WebRTC is one of the most <strong>complicated ones</strong>. And despite being a peer-to-peer protocol, it still requires a server. The reason for all of this is that in order to connect two browsers, both have to know where the other one is — and that is way more complicated than it sounds.

Imagine a friend asking for your address. You answer, “I’m in the bedroom” — leaving it to them to find out which house your bedroom is in, which street your house is on, which town that street is in and so on. And once they can reliably locate your bedroom, you still have to provide a list of windows and doors they have to try to see if one is open.</p>

<a href="https://deepstream.io/tutorials/">Deepstream</a> tries to abstract all of that away and reduce WebRTC to two concepts: a phonebook and a call. We’ll use both to create a video chat room that allows our team to talk about what’s happening on the retrospective board.</p>

## Connect The Streams

Video in a browser comes in the form of a <code>MediaStream</code>. These streams are a combination of audio and video signals that can be played in a <code>video</code> element or sent to someone else via the Internet. You can retrieve a stream from a webcam or microphone, from another user via WebRTC or, once <code>captureStream</code> is fully supported, even from a <code>canvas</code> element.</p>

## Getting Your Local Webcam Stream

Let’s start with our local webcam and microphone stream. It can be retrieved using <code>getUserMedia</code> — and immediately the trouble starts. <code>getUserMedia</code> has been around for a while now, but the API is still not fully standardized and, therefore, is still vendor-prefixed. But help is at hand. The official WebRTC initiative maintains an adapter script that normalizes browser differences and stays up to date with API changes. You can <a href="https://github.com/webrtc/adapter">find it on GitHub</a>.

Once it’s installed, retrieving your local video and audio stream and playing it in a <code>video</code> tag is as simple as this:

<pre><code class="language-javascript">navigator.mediaDevices.getUserMedia({
    video: { width: 160, height: 120 },
    audio: false
  })
  .then(function onStream( stream ) {
        // Mute the local video to eliminate microphone feedback.
        addVideo( stream, true );
    })
  .catch(function onError( error ) {
         // If the user doesn't have a webcam or doesn't allow access,
        // you'll end up here.
    });
);

function addVideo( stream, muted ) {
  var video = $( '&lt;video&gt;&lt;/video&gt;' ).attr({
    'width': '160px',
    'height': '120px',
    'autoplay': 'autoplay',
    'muted': muted,
    'data-username': username
  });
  video[0].srcObject = stream;
  this.outerElement.append( video );
}
</code></pre>

## Make Sure To Handle Errors

Whenever an application requests access to a user’s webcam or microphone, a lot of things can go wrong. A user might not have a webcam at all, might have a webcam but no microphone, might have a webcam that is not able to provide the required resolution, or might have a webcam that simply is not allowed access to their media devices. All of these cases are captured in <code>getUserMedia</code>’s error callback. Have a look at the <a href="https://www.w3.org/TR/mediacapture-streams/#mediastreamerror">official specification</a> for the full lists of errors that could occur.</p>

## Registering For Incoming Calls

Now that we’ve got our local video stream, it’s time to add ourselves to the phonebook and listen for others adding themselves. To let the others know who we are, we’ll use the user name we’ve logged in with.</p>

<pre><code class="language-javascript">// Add ourselves to the phonebook
ds.webrtc.registerCallee( this.username, this.onIncomingCall.bind( this ) );

// Listen for others adding themselves
ds.webrtc.listenForCallees( this.onCallees.bind( this ) );
</code></pre>

<code>ds.webrtc.listenForCallees</code> will invoke <code>this.onCallees</code> immediately with a list of all currently registered callees and then again whenever another users is added or removed from the phonebook.

This will help us solve an inherent problem of peer-to-peer systems: rooms.</p>

## The Problem With Rooms

Rooms are a common concept in every chat application: A number of participants all talk to each other at the same time. With a centralized server, this is easy: You log in and get every participant’s video stream. With a network of peer-to-peer connections, however, things are a bit trickier.

To create a room, every participant has to connect to every other participant exactly once.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cbadab7-3574-4f08-ad50-68402366b73a/06-peer-to-peer-rooms-opt.png"><img title="P2P video chat" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cbadab7-3574-4f08-ad50-68402366b73a/06-peer-to-peer-rooms-opt.png" alt="Many-to-many video chat: server versus peer-to-peer" /></a><figcaption>Many-to-many video chat: server versus peer-to-peer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cbadab7-3574-4f08-ad50-68402366b73a/06-peer-to-peer-rooms-opt.png">View large version</a>)</figcaption></figure>

To achieve this, we’ll assume two things:

*   that the whole phonebook (i.e. the array of callee names, provided by `listenForCallees`) constitutes one room;
*   that every new user has to call all currently present users (this way, the first user to log in won’t call anyone, the second user will call the first, the third user will call the other two and so on).

With this in mind, here’s what our <code>onCallees</code> function will look like:

<pre><code class="language-javascript">VideoChat.prototype.onCallees = function( callees ) {
var call, i, metaData = { user: this.username };

for( i = 0; i &lt; callees.length; i++ ) {
  // No point in calling ourselves.
  if( callees[ i ] === this.username ) continue;
  call = this.ds.webrtc.makeCall(callees[i], metaData, this.localStream);
  call.once( 'established', this.addVideo.bind(this, this.username) );
  call.once( 'ended', this.removeVideo.bind(this, this.username) );
}

  // And done. Let's unsubscribe from future updates.
  this.ds.webrtc.unlistenForCallees();
};
</code></pre>

## Waiting For Incoming Calls

Great! We’re now connected to everyone who’s in the room. The bit that’s left is to accept incoming calls from new participants. When we’ve registered ourselves as a callee, we’ve provided a callback function for incoming calls:

<pre><code class="language-javascript">ds.webrtc.registerCallee(this.username, this.onIncomingCall.bind(this) );</code></pre>

Now it’s time to fill it in:

<pre><code class="language-javascript">VideoChat.prototype.onIncomingCall = function( call, metaData ) {
    call.once( 'established', this.addVideo.bind( this, metaData.user ) );
    call.once( 'ended', this.removeVideo.bind( this, metaData.user ) );
    // Let's not be picky; let’s accept all calls.
    call.accept( this.localStream );
};
</code></pre>

That’s it! From now on, every time you log into the retrospective board, your webcam will spring to life, you’ll be connected to all other members of your team, and every new joiner will automatically connect to you.

As with the first part of the tutorial, I’ve skipped a few lines that wire things together. To get the full script, please <a href="https://github.com/hoxton-one/realtime-retrospective-board">look at the GitHub repository</a>.</p>

## Is That All There Is To Building Production-Ready Video Chat?

Well, almost. WebRTC is used in production in large-scale apps like Google Hangouts and Skype for Web. But the developers of those apps had to take some detours to achieve their quality of service.

Hangouts relies on a number of non-standard features built specifically into Chrome (and available as plugins for other browsers), whereas Skype for Web is investigating a parallel standard, called Object Real-Time Communication (ORTC), which is currently supported only by IE Edge.

That might sound an awful lot like the standards battles of the past, but things are actually looking quite promising this time: ORTC isn’t meant to compete with WebRTC, but rather to augment and ultimately complete it. It is designed to be shimmable and, finally, merged with WebRTC in the next version after 1.0.</p>

## But Why Is It Necessary?

Production-ready RTC apps use a number of techniques to achieve a solid user experience across devices and bandwidths. Take Simulcast, which allows us to send different resolutions and frame rates of the same stream. This way, it leaves the recipient to pick a quality to display, rather than performing CPU-intensive on-the-fly compression; it is, therefore, a fundamental part of most video chats. Unfortunately, Simulcast has only just made it into the WebRTC 1.0 specification. It is, however, already available in ORTC.

The same is true for a number of other low-level APIs. WebRTC is well usable and ready to go, but not until the consolidation with ORTC and the final alignment of browser video codecs will it be fully usable in production.

Until then, great low-level libraries like <a href="https://simplewebrtc.com/">SimpleWebRTC</a> and <a href="https://github.com/webrtc/adapter">adapter.js</a> will be around to bridge the gap, and high-level technologies like <a href="https://deepstream.io/">deepstream</a> give developers a head start on building a solid RTC project without having to worry much about its internals.

{{< signature "rb, jb, ml, al" >}}

