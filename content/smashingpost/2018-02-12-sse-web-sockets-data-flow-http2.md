---
title: 'Using SSE Instead Of WebSockets For Unidirectional Data Flow Over HTTP/2'
slug: sse-websockets-data-flow-http2
author: martin-chaov
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d83590d0-3f1b-463f-8dac-d0d0c53fd6ef/headers-long-polling-800w.png
date: 2018-02-12T11:30:04+01:00
summary: >
  Whenever we design a web application utilizing real-time data, we need to consider how we are going to deliver our data from the server to the client. The default answer usually is "WebSockets." But is there a better way? Let's compare three different methods: Long polling, WebSockets, and Server-Sent Events; to understand their real-world limitations. The answer might surprise you.
description: >-
  What is the best way to deliver real-time updates to your web application in an easy and structured way? Is WebSockets still relevant in the world of HTTP/2? Let's compare the architectural impact of three different mechanisms.
categories:
  - Performance
  - Backend
---
When building a web application, one must consider what kind of delivery mechanism they are going to use. Let's say we have a cross-platform application that works with real-time data; a stock market application providing ability to buy or sell stock in real time. This application is composed of widgets that bring different value to the different users.

When it comes to data delivery from the server to the client, we are limited to two general approaches: *client pull* or *server push*. As a simple example with any web application, the client is the web browser. When the website in your browser is asking the server for data, this is called *client pull*. The reverse, when the server is proactively pushing updates to your website, it is called *server push*.

Nowadays, there are a few ways to implement these:

- Long/short polling (client pull)
- WebSockets (server push)
- Server-Sent events (server push).

We are going to take an in-depth look at the three alternatives after we have set the requirements for our business case.

## The Business Case

In order to be able to deliver new widgets for our stock market application fast and plug'n'play them without redeployment of the entire platform, we need these to be self-contained and manage their own data I/O. The widgets are not coupled with each other in any way. In the ideal case, all of them are going to subscribe to some API endpoint and start getting data from it. Beside faster time to market of new features, this approach gives us the ability to export content onto third-party websites whereas our widgets bring everything they need on their own.

{{% feature-panel %}}

The main pitfall here is that the number of connections is going to grow linearly with the number of widgets we have and we are going to hit the browsers' limit for the number of HTTP requests handled at once.

The data our widgets are going to receive is mainly comprised of numbers and updates to their numbers: The initial response contains ten stocks with some market values for them. This includes updates of adding/removing stocks and updates of the market values of the currently presented ones. We transfer small amounts of JSON strings for every update as fast as possible.

HTTP/2 provides multiplexing of the requests that are coming from the same domain, meaning we can get only one connection for multiple responses. This sounds like it could solve our problem. We start by exploring the different options to get the data and see what we can get out of them.

- We are going to be using NGINX for load balancing and proxy to hide all our endpoints behind the same domain. This will enable us to use HTTP/2 multiplexing out of the box.
- We want to use the mobile devices' network and battery efficiently.

## The Alternatives

### Long Polling

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/debac4c6-a38a-45f7-b16e-e06ad45aab64/headers-long-polling.png" sizes="100vw" caption="" alt="Long polling" >}}

Client pull is the software implementation equivalent of the annoying child sitting in the back seat of your car constantly asking, "Are we there yet?" In short, the client asks the server for data. The server has no data and waits for some amount of time before sending the response:

- If something pops up during the wait, the server sends it and closes request;
- If there is nothing to send and the maximum wait time is achieved, the server sends a response that there is no data;
- In both cases, the client opens the next request for data;
- Lather, rinse, repeat.

AJAX calls work on the HTTP protocol meaning requests to the same domain should get multiplexed by default. However, we hit multiple issues with trying to get that to work as required. Some of the pitfalls we identified with our widgets approach:

- **Headers Overhead**  
Every poll request and response is a complete HTTP message and contains a full set of HTTP headers in the message framing. In our case where we have small frequent messages, the headers actually represent the bigger percentage of the data transmitted. The actual useful payload is much less than the total transmitted bytes (e.g., 15 KB of headers for 5 KB of data).

- **Maximal Latency**  
After the server responds, it can no longer send data to the client until the client sends the next request. While the average latency for long polling is close to one network transit, the maximum latency is over three network transits: response, request, response. However, due to packet loss and retransmission, maximum latency for any TCP/IP protocol will be more than three network transits (avoidable with HTTP pipelining). While in direct LAN connection this is not a big issue, it becomes one while one is on the move and switching network cells. To a certain degree, this is observed with SSE and WebSockets, but the effect is greatest with polling.

- **Connection Establishment**  
Although it can be avoided by using with persistent HTTP connection reusable for many poll requests, it is tricky to accordingly time all of your components to poll in short-timed durations to keep the connection alive. Eventually, depending on the server responses, your polls will get desynchronized.

- **Performance Degradation**  
A long polling client (or server) that is under load has a natural tendency to degrade in performance at the cost of message latency. When that happens, events that are pushed to the client will queue. This really depends on the implementation; in our case, we need to aggregate all the data as we are sending add/remove/update events to our widgets.

- **Timeouts**  
Long poll requests need to remain pending until the server has something to send to the client. This can lead to the connection getting closed by the proxy server if it remains idle for too long.

- **Multiplexing**  
This can happen if the responses happen at the same time over a persistent HTTP/2 connection. This can be tricky to do as polling responses can't really be in sync.

*More about real-world issues one could experience with long polling can be found [here](https://tools.ietf.org/html/rfc6202#section-2.2)*.

### WebSockets

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/985c8400-ef48-437a-83a7-43aa75db8a63/headers-web-sockets.png" sizes="100vw" caption="" alt="WebSockets" >}}

As a first example of the *server push* method, we are going to look at WebSockets.

*Via MDN:*

<blockquote>WebSockets is an advanced technology that makes it possible to open an interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.</blockquote>

This is a communications protocol providing full-duplex communication channels over a single TCP connection.

Both HTTP and WebSockets are located at the application layer from the OSI model and as such depend on TCP at layer 4.

7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data link
1. Physical

<p class="c-pre-sidenote--left">RFC 6455 states that WebSocket "is designed to work over HTTP ports 80 and 443 as well as to support HTTP proxies and intermediaries" thus making it compatible with the HTTP protocol. To achieve compatibility, the WebSocket handshake uses the HTTP Upgrade header to change from the HTTP protocol to the WebSocket protocol.</p><p class="c-sidenote c-sidenote--right">There is also a very good article that explains everything you need to know about WebSockets on <a href="https://en.wikipedia.org/wiki/WebSocket">Wikipedia</a>. I encourage you to read it.</p>

After establishing that sockets could actually work for us, we started exploring their capabilities in our business case, and hit wall after wall after wall.

- **Proxy servers**:
In general, there are a few different issues with WebSockets and proxies:
  - The first one is related to Internet service providers and the way they handle their networks. Issues with radius proxies blocked ports, and so on.
  - The second type of issues is related to the way the proxy is configured to handle the unsecured HTTP traffic and long-lived connections (impact is lessened with HTTPS).
  - The third issue "with WebSockets, you are forced to run TCP proxies as opposed to HTTP proxies. TCP proxies can not inject headers, rewrite URLs or perform many of the roles we traditionally let our HTTP proxies take care of."

- **A number of connections**:
The famous connection limit for HTTP requests that revolves around the number 6, doesn't apply to WebSockets. 50 sockets = 50 connections. Ten browser tabs by 50 sockets = 500 connections and so on. Since WebSocket is a different protocol for delivering data, it's not automatically multiplexed over HTTP/2 connections (it doesn't really run on top of HTTP at all). Implementing custom multiplexing both on the server and the client is too complicated to make sockets useful in the specified business case. Furthermore, this couples our widgets to our platform as they will need some kind of API on the client to subscribe to and we are not able to distribute them without it.

- **Load balancing (without multiplexing)**:
If every single user opens `n` number of sockets, proper load balancing is very complicated. When your servers get overloaded, and you need to create new instances and terminate old ones depending on the implementation of your software the actions that are taken on "reconnect" can trigger a massive chain of refreshes and new requests for data that will overload your system. WebSockets need to be maintained both on the server and on the client. It's not possible to move socket connections to a different server if the current one experiences high load. They must be closed and reopened.

- **DoS**:
This is usually handled by front-end HTTP proxies that cannot be handled by TCP proxies which are needed for the WebSockets. One can connect to the socket and starts flooding your servers with data. WebSockets leave you vulnerable to these kind of attacks.

- **Reinventing the wheel**:
With WebSockets, one must handle lots of problems that are taken care of in HTTP on their own.

*More about real-world issues with WebSockets can be read [here](https://samsaffron.com/archive/2015/12/29/websockets-caution-required).*

Some good use cases for WebSockets are chats and multi-player games in which the benefits outweigh the implementation issues. With their main benefit being duplex communication, and us not really needing it, we need to move on.

### Impact

We get increased operational overhead in terms of developing, testing, and scaling; the software and it's IT infrastructure with both: polling and WebSockets.

We get the same issue over mobile devices and networks with both. The hardware design of these devices maintains an open connection by keeping the antenna and connection to the cellular network alive. This leads to reduced battery life, heat, and in some cases, extra charges for data.

#### But Why Do We Still Have Issues With Mobile Devices?

Let's consider how the default mobile device connects to the Internet:

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/253960836" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<figcaption>Mobile devices need to go through few hoops before they are able to connect to the Internet.</figcaption></figure>

A straightforward explanation of how mobile network works: Typically mobile devices have a low power antenna that may receive data from a cell. This way, once the device receives data from an incoming call, it boots up the full-duplex antenna in order to establish the call. The same antenna is used whenever *you* want to make a call or access the Internet (if no WiFi is available). The full-duplex antenna needs to establish a connection to the cellular network and do some authentication. Once the connection is established, there is some communication between your device and the cell in order to do our network request. We get redirected to the internal proxy of the mobile service provider which handles Internet requests. From then on, the procedure is already known: it asks a DNS where `www.domainname.ext` actually is, receiving the URI to the resource, and eventually getting redirected to it.

This process, as you could imagine, draws quite a lot of battery power. This is the reason why the mobile phone vendors give a standby time of few days and talk time in just a couple of hours.

Without WiFi, both WebSockets and polling require the full-duplex antenna to work almost constantly. Thus, we face increased data consumption and increased power draw &mdash; and depending on the device &mdash; heat, too.

By the time things seem bleak, it looks like we are going to have to reconsider the business requirements for our application. Are we missing something?

## SSE

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e330934-fccf-48be-aa6d-fc3e2cdd41f8/headers-sse.png" sizes="100vw" caption="" alt="Server-Sent Events" >}}

*Via MDN:*

>"The EventSource interface is used to receive Server-Sent Events. It connects to a server over HTTP and receives events in text/event-stream format without closing the connection."

The main difference to polling is that we get only one connection and keep an event stream going through it. Long polling creates a new connection for every pull &mdash; ergo the headers overhead and other issues we faced there.

*Via html5doctor.com:*

<blockquote>Server-Sent Events are real-time events emitted by the server and received by the browser. They’re similar to WebSockets in that they happen in real time, but they’re very much a one-way communication method from the server.</blockquote>

It looks kind of strange, but after consideration &mdash; our main flow of data is from the server to the client and in much fewer occasions from the client to the server.

It looks like we can use this for our main business case of delivering data. We can resolve customer purchases by sending a new request as the protocol is unidirectional and the client can't send messages to the server through it. This eventually is going to have the time delay of the full-duplex antenna to boot up on mobile devices. However, we can live with it happening from time to time &mdash; this delay is measured in milliseconds after all.

### Unique Features

- The connection stream is coming from the server and is read-only.
- They use regular HTTP requests for the persistent connection, not a special protocol. Getting multiplexing over HTTP/2 out of the box.
- If the connection drops, the EventSource fires an error event and automatically tries to reconnect. The server can also control the timeout before the client tries to reconnect (explained in more details later).
- Clients can send a unique ID with messages. When a client tries to reconnect after a dropped connection, it will send the last known ID. Then the server can see that the client missed `n` number of messages and send the backlog of missed messages on reconnect.

### Sample Client Implementation

These events are similar to ordinary JavaScript events that occur in the browser &mdash; like click events &mdash; except we can control the name of the event and the data associated with it.

Let's see the simple code preview for the client side:

<pre><code class="language-javascript">// subscribe for messages
    var source = new EventSource('URL');

    // handle messages
    source.onmessage = function(event) {
        // Do something with the data:
        event.data;
    };
</code></pre>

What we see from the example is that the client side is fairly simple. It connects to our source and waits to receive messages.

<p class="c-pre-sidenote--left">To enable servers to push data to web pages over HTTP or using dedicated server-push protocols, the specification introduces the `EventSource` interface on the client. Using this API consists of creating an `EventSource` object and registering an event listener.</p><p class="c-sidenote c-sidenote--right">Client implementation for WebSockets looks very similar to this. Complexity with sockets lies in the IT infrastructure and server implementation.</p>

#### EventSource

Each `EventSource` object has the following members:

- URL: set during construction.
- Request: initially is null.
- Reconnection time: value in ms (user-agent-defined value).
- Last event ID: initially an empty string.
- Ready state: state of the connection.
  - CONNECTING    (0)
  - OPEN          (1)
  - CLOSED        (2)

Apart from the URL, all are treated like private and cannot be accessed from outside.

Build-in events:

1. Open
1. Message
1. Error

#### Handling Connection Drops

The connection is automatically re-established by the browser if it drops. The server may send timeout to retry or close the connection permanently. In such a case, the browser will comply with either trying to reconnect after the timeout or not trying at all if connection got terminate message. Seems fairly simple &mdash; and it actually is.

### Sample Server Implementation

Well if the client is that simple, maybe the server implementation is complex?

Well, the server handler for SSE may look like this:

<div class="break-out">

<pre><code class="language-javascript">function handler(response)
    {
        // setup headers for the response in order to get the persistent HTTP connection
        response.writeHead(200, {
            'Content-Type': 'text/event-stream',
            'Cache-Control': 'no-cache',
            'Connection': 'keep-alive'
        });

        // compose the message
        response.write('id: UniqueID\n');
        response.write("data: " + data + '\n\n'); // whenever you send two new line characters the message is sent automatically
    }
</code></pre></div>

We define a function that is going to handle the response:

1. Setup headers
1. Create message
1. Send

Note that you don't see a `send()` or `push()` method call. This is because the standard defines that the message is going to be sent as soon as it receives two `\n\n` characters as in the example: `response.write("data: " + data + '\n\n');`. This will immediately push the message to the client. Please note that the `data` must be an escaped string and doesn't have new line characters at the end of it.

#### Message Construction

As mentioned earlier, the message can contain a few properties:

1. **ID**  
If the field value does not contain U+0000 NULL, then set the last event ID buffer to the field value. Otherwise, ignore the field.
1. **Data**  
Append the field value to the data buffer, then append a single U+000A LINE FEED (LF) character to the data buffer.
1. **Event**  
Set the event type buffer to the field value. This leads to `event.type` getting your custom event name.
1. **Retry**  
If the field value consists of only ASCII digits, then interpret the field value as an integer in base ten, and set the event stream's reconnection time to that integer. Otherwise, ignore the field.

Anything else will be ignored. We can't introduce our own fields.

Example with added `event`:

<pre><code class="language-javascript">response.write('id: UniqueID\n');
    response.write('event: add\n');
    response.write('retry: 10000\n');
    response.write("data: " + data + '\n\n');
</code></pre>

Then on the client, this is handled with `addEventListener` as such:

<pre><code class="language-javascript">source.addEventListener("add", function(event) {
        // do stuff with data
        event.data;
    });
</code></pre>

You can send multiple messages separated by a new line as long as you provide different IDs.

<pre><code class="language-javascript">...
    id: 54
    event: add
    data: "[{SOME JSON DATA}]"

    id: 55
    event: remove
    data: JSON.stringify(some_data)

    id: 56
    event: remove
    data: {
    data: "msg" : "JSON data"\n
    data: "field": "value"\n
    data: "field2": "value2"\n
    data: }\n\n
    ...
</code></pre>

This vastly simplifies what we can do with our data.

#### Specific Server Requirements

During our POC for the back-end, we identified it has some specifics that need to be addressed to have a working implementation of SSE. The best case scenario you will be using event loop based server like NodeJS, Kestrel, or Twisted. The idea being that with the thread-based solution you will have a thread per connection &rarr; 1000 connections = 1000 threads. With the event loop solution, you will have one thread for 1000 connections.

1. You can only accept EventSource requests if the HTTP request says it can accept the event-stream MIME type;
2. You need to maintain a list of all the connected users in order to emit new events;
3. You should listen for dropped connections and remove them from the list of connected users;
4. You should optionally maintain a history of messages so that reconnecting clients can catch up on missed messages.

It works as expected and looks like magic at first. We get everything we want for our application to work in an efficient way. As with all things that look too good to be true, we sometimes face some issues that need to be addressed. However, they are not complicated to implement or go around:

- Legacy proxy servers are known to, in certain cases, drop HTTP connections after a short timeout. To protect against such proxy servers, authors can include a comment line (one starting with a ':' character) every 15 seconds or so.

- Authors wishing to relate event source connections to each other or to specific documents previously served might find that relying on IP addresses doesn't work, as individual clients can have multiple IP addresses (due to having multiple proxy servers) and individual IP addresses can have multiple clients (due to sharing a proxy server). It is better to include a unique identifier in the document when it is served and then passes that identifier as part of the URL when the connection is established.

- Authors are also cautioned that HTTP chunking can have unexpected negative effects on the reliability of this protocol, in particular, if the chunking is done by a different layer unaware of the timing requirements. If this is a problem, chunking can be disabled for serving event streams.

- Clients that support HTTP's per-server connection limitation might run into trouble when opening multiple pages from a site if each page has an EventSource to the same domain. Authors can avoid this using the relatively complex mechanism of using unique domain names per connection, or by allowing the user to enable or disable the EventSource functionality on a per-page basis, or by sharing a single EventSource object using a shared worker.

- Browser support and Polyfills: Edge is lagging behind this implementation, but a polyfill is available that can save you. However, the most important case for SSE is made for mobile devices where IE/Edge have no viable market share.

Some of the available polyfills:

- [Yaffle](https://github.com/Yaffle/EventSource)
- [amvtek](https://github.com/amvtek/EventSource)
- [remy](https://github.com/remy/polyfills/blob/master/EventSource.js)

### Connectionless Push And Other Features

User agents running in controlled environments, e.g., browsers on mobile handsets tied to specific carriers, may offload the management of the connection to a proxy on the network. In such a situation, the user agent for the purposes of conformance is considered to include both the handset software and the network proxy.

For example, a browser on a mobile device, after having established a connection, might detect that it is on a supporting network and request that a proxy server on the network takes over the management of the connection. The timeline for such a situation might be as follows:

1. The browser connects to a remote HTTP server and requests the resource specified by the author in the EventSource constructor.
2. The server sends occasional messages.
3. In between two messages, the browser detects that it is idle except for the network activity involved in keeping the TCP connection alive, and decides to switch to sleep mode to save power.
4. The browser disconnects from the server.
5. The browser contacts a service on the network and requests that the service, a "push proxy," maintain the connection instead.
6. The "push proxy" service contacts the remote HTTP server and requests the resource specified by the author in the EventSource constructor (possibly including a `Last-Event-ID` HTTP header, etc.).
7. The browser allows the mobile device to go to sleep.
8. The server sends another message.
9. The "push proxy" service uses a technology such as OMA push to convey the event to the mobile device, which wakes only enough to process the event and then returns to sleep.

This can reduce the total data usage, and can, therefore, result in considerable power savings.

As well as implementing the existing API and text/event-stream wire format as defined by the specification and in more distributed ways (as described above), formats of event framing defined by other applicable specifications may be supported.

## Summary

After long and exhaustive POCs including server and client implementations, it looks like SSE is the answer to our problems with data delivery. There are some pitfalls with it as well, but they proved to be trivial to fix.

This is how our production setup looks like in the end:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccaa6566-01c9-4a65-8f41-a7f0a002a0d8/nginx-sse-polling.png" sizes="100vw" caption="Final architecture overview. All API endpoints are behind nginx so clients get multiplexed reponse." alt="Architecture overview" >}}

We get the following from NGINX:

- Proxy to API endpoints in different places;
- HTTP/2 and all of its benefits like multiplexing for the connections;
- Load balancing;
- SSL.

This way we manage our data delivery and certificates in one place instead of doing it on every endpoint separately.

The main benefits we get from this approach are:

- Data efficient;
- Simpler implementation;
- It is automatically multiplexed over HTTP/2;
- Limits the number of connections for data on the client to one;
- Provides a mechanism to save the battery by offloading the connection to a proxy.

SSE is not just a viable alternative to the other methods for delivering fast updates; it looks like it is in a league of its own when it comes to optimizations for mobile devices. There is no overhead in its implementation compared with the alternatives. In terms of server-side implementation, it is not much different than polling. On the client, it is much simpler than polling as it requires an initial subscription and assigning event handlers &mdash; much similar to how WebSockets are managed.

*Check the code [demo](https://github.com/mchaov/simple-sse-nodejs-setup) if you'd like to get a simple client-server implementation.*

## Resources
- "[Known Issues and Best Practices for the Use of Long Polling and Streaming in Bidirectional HTTP](https://www.rfc-editor.org/rfc/pdfrfc/rfc6202.txt.pdf)," IETF (PDF)
- [W3C Recommendation](https://www.w3.org/TR/eventsource/), W3C
- "[Will WebSocket survive HTTP/2?](https://www.infoq.com/articles/websocket-and-http2-coexist),"  Allan Denis, InfoQ
- "[Stream Updates with Server-Sent Events](https://www.html5rocks.com/en/tutorials/eventsource/basics/)," Eric Bidelman, HTML5 Rocks
- "[Data Push Apps with HTML5 SSE](https://shop.oreilly.com/product/0636920030928.do)," Darren Cook, O'Reilly Media

{{< signature "rb, ra, yk, il" >}}

