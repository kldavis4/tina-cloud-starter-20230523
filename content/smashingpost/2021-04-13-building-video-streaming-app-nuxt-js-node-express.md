---
title: 'Building A Video Streaming App With Nuxt.js, Node And Express'
slug: building-video-streaming-app-nuxtjs-node-express
author: deven-rathore
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50a03903-4227-4f64-b4f4-a7ec82c89a54/building-video-streaming-app-nuxtjs-node-express.jpg
date: 2021-04-13T14:00:00.000Z
summary: >-
  In this article, we’ll be building a video streaming app using Nuxt.js and Node.js. Specifically, we’ll build a server-side Node.js app that will handle fetching and streaming videos, generating thumbnails for your videos, and serving captions and subtitles.
description: >-
  In this article, we’ll be building a video streaming app using Nuxt.js and Node.js. Specifically, we’ll build a server-side Node.js app that will handle fetching and streaming videos, generating thumbnails for your videos, and serving captions and subtitles.
categories:
  - Vue
  - Nuxt.js
  - Node.js
  - Tutorials
  - JavaScript
---

Videos work with streams. This means that instead of sending the entire video at once, a video is sent as a set of smaller chunks that make up the full video. This explains why videos buffer when watching a video on slow broadband because it only plays the chunks it has received and tries to load more.

This article is for developers who are willing to learn a new technology by building an actual project: a video streaming app with [Node.js](https://nodejs.org/en/) as the backend and [Nuxt.js](https://nuxtjs.org/) as the client. 

- **Node.js** is a runtime used for building fast and scalable applications. We will use it to handle fetching and streaming videos, generating thumbnails for videos, and serving captions and subtitles for videos.
- **Nuxt.js** is a Vue.js framework that helps us build server-rendered Vue.js applications easily. We will consume our API for the videos and this application will have two views: a listing of available videos and a player view for each video.

## Prerequisities

- An understanding of HTML, CSS, JavaScript, Node/Express, and Vue.
- A text editor (e.g. VS Code).
- A web browser (e.g. Chrome, Firefox).
- [FFmpeg](https://www.ffmpeg.org/download.html) installed on your workstation.
- [Node.js](https://nodejs.org/en/download/). [nvm](https://github.com/nvm-sh/nvm).
- You can [get the source code on GitHub](https://github.com/smashingmagazine/Nuxt-Node-video-streaming).

## Setting Up Our Application

In this application, we will build the routes to make requests from the frontend:

- `videos` route to get a list of videos and their data.
- a route to fetch only one video from our list of videos.
- `streaming` route to stream the videos.
- `captions` route to add captions to the videos we are streaming.

After our routes have been created, we’ll scaffold our `Nuxt` frontend, where we’ll create the `Home` and dynamic `player` page. Then we request our `videos` route to fill the home page with the video data, another request to stream the videos on our `player` page, and finally a request to serve the caption files to be used by the videos.

To set up our application, we create our project directory,

<pre><code class="language-bash">mkdir streaming-app</code></pre>

{{% feature-panel %}}

## Setting Up Our Server 

In our `streaming-app` directory, we create a folder named `backend`.

<pre><code class="language-bash">cd streaming-app
mkdir backend</code></pre>

In our backend folder, we initialize a `package.json` file to store information about our server project.

<pre><code class="language-bash">cd backend
npm init -y</code></pre>

we need to install the following packages to build our app.

- `nodemon` automatically restarts our server when we make changes.
- `express` gives us a nice interface to handle routes.
- `cors` will allow us to make cross-origin requests since our client and server will be running on different ports.

In our backend directory, we create a folder `assets` to hold our videos for streaming.

<pre><code class="language-bash"> mkdir assets</code></pre>

Copy a `.mp4` file into the assets folder, and name it `video1`. You can use  `.mp4` short sample videos that can be found on [Github Repo](https://github.com/Dunebook/Nuxt-Node-video-streaming/tree/main/backend/assets).

Create an `app.js` file and add the necessary packages for our app.

<pre><code class="language-javascript">const express = require('express');
const fs = require('fs');
const cors = require('cors');
const path = require('path');
const app = express();
app.use(cors())</code></pre>

The `fs` module is used to read and write into files easily on our server, while the `path` module provides a way of working with directories and file paths.

Now we create a `./video` route. When requested, it will send a video file back to the client.

<pre><code class="language-javascript">// add after 'const app = express();'

app.get('/video', (req, res) =&gt; {
    res.sendFile('assets/video1.mp4', { root: __dirname });
});</code></pre>

This route serves the `video1.mp4` video file when requested. We then listen to our server at port `3000`.

<pre><code class="language-javascript">// add to end of app.js file

app.listen(5000, () =&gt; {
    console.log('Listening on port 5000!')
});</code></pre>

A script is added in the `package.json` file to start our server using nodemon.
 

<pre><code class="language-javascript">
"scripts": {
    "start": "nodemon app.js"
  },</code></pre>

Then on your terminal run:

<pre><code class="language-bash">npm run start</code></pre>

If you see the message `Listening on port 3000!` in the terminal, then the server is working correctly. Navigate to [https://localhost:5000/video](https://localhost:5000/video) in your browser and you should see the video playing.

## Requests To Be Handled By The Frontend

Below are the requests that we will make to the backend from our frontend that we need the server to handle.

- `/videos`  
Returns an array of video mockup data that will be used to populate the list of videos on the `Home` page in our frontend.
- `/video/:id/data`  
Returns metadata for a single video. Used by the `Player` page in our frontend.
- `/video/:id`  
Streams a video with a given ID. Used by the `Player` page.

Let’s create the routes.

{{% ad-panel-leaderboard %}}

## Return Mockup Data For List Of Videos

For this demo application, we’ll create an **array of objects** that will hold the metadata and send that to the frontend when requested. In a real application, you would probably be reading the data from a database, which would then be used to generate an array like this. For simplicity's sake, we won’t be doing that in this tutorial.

In our backend folder create a file `mockdata.js` and populate it with metadata for our list of videos.

<div class="break-out">

<pre><code class="language-javascript">const allVideos = [
    {
        id: "tom and jerry",
        poster: 'https://image.tmdb.org/t/p/w500/fev8UFNFFYsD5q7AcYS8LyTzqwl.jpg',
        duration: '3 mins',
        name: 'Tom & Jerry'
    },
    {
        id: "soul",
        poster: 'https://image.tmdb.org/t/p/w500/kf456ZqeC45XTvo6W9pW5clYKfQ.jpg',
        duration: '4 mins',
        name: 'Soul'
    },
    {
        id: "outside the wire",
        poster: 'https://image.tmdb.org/t/p/w500/lOSdUkGQmbAl5JQ3QoHqBZUbZhC.jpg',
        duration: '2 mins',
        name: 'Outside the wire'
    },
];
module.exports = allVideos</code></pre>
</div>

We can see from above, each object contains information about the video. Notice the `poster` attribute which contains the link to a poster image of the video. 

Let’s create a `videos` route since all our request to be made by the frontend is prepended with `/videos`.

To do this, let’s create a `routes` folder and add a `Video.js` file for our `/videos` route. In this file, we’ll require `express` and use the express router to create our route.

<pre><code class="language-javascript">const express = require('express')
const router = express.Router()</code></pre>

When we go to the `/videos` route, we want to get our list of videos, so let’s require the `mockData.js` file into our `Video.js` file and make our request.

<pre><code class="language-javascript">const express = require('express')
const router = express.Router()
const videos = require('../mockData')
// get list of videos
router.get('/', (req,res)=>{
    res.json(videos)
})
module.exports = router;</code></pre>

The `/videos` route is now declared, save the file and it should automatically restart the server. Once it’s started, navigate to https://localhost:3000/videos and our array is returned in JSON format.

## Return Data For A Single Video

We want to be able to make a request for a particular video in our list of videos. We can fetch a particular video data in our array by using the `id` we gave it. Let’s make a request, still in our `Video.js` file.

<pre><code class="language-javascript">
// make request for a particular video
router.get('/:id/data', (req,res)=> {
    const id = parseInt(req.params.id, 10)
    res.json(videos[id])
})</code></pre>

The code above gets the `id` from the route parameters and converts it to an integer. Then we send the object that matches the `id` from the `videos` array back to the client.

## Streaming The Videos

In our `app.js` file, we created a `/video` route that serves a video to the client. We want this endpoint to send smaller chunks of the video, instead of serving an entire video file on request.

We want to be able to *dynamically* serve one of the three videos that are in the `allVideos` array, and stream the videos in chunks, so:

Delete the `/video` route from `app.js`.

We need three videos, so copy the example videos from the tutorial’s [source code](https://github.com/smashingmagazine/Nuxt-Node-video-streaming/tree/main/backend/assets) into the `assets/` directory of your `server` project. Make sure the filenames for the videos are corresponding to the `id` in the `videos` array:

Back in our `Video.js` file, create the route for streaming videos.

<div class="break-out">

<pre><code class="language-javascript">router.get('/video/:id', (req, res) =&gt; {
    const videoPath = `assets/${req.params.id}.mp4`;
    const videoStat = fs.statSync(videoPath);
    const fileSize = videoStat.size;
    const videoRange = req.headers.range;
    if (videoRange) {
        const parts = videoRange.replace(/bytes=/, "").split("-");
        const start = parseInt(parts[0], 10);
        const end = parts[1]
            ? parseInt(parts[1], 10)
            : fileSize-1;
        const chunksize = (end-start) + 1;
        const file = fs.createReadStream(videoPath, {start, end});
        const head = {
            'Content-Range': `bytes ${start}-${end}/${fileSize}`,
            'Accept-Ranges': 'bytes',
            'Content-Length': chunksize,
            'Content-Type': 'video/mp4',
        };
        res.writeHead(206, head);
        file.pipe(res);
    } else {
        const head = {
            'Content-Length': fileSize,
            'Content-Type': 'video/mp4',
        };
        res.writeHead(200, head);
        fs.createReadStream(videoPath).pipe(res);
    }
});</code></pre>
</div>

If we navigate to https://localhost:5000/videos/video/outside-the-wire in our browser, we can see the video streaming.

## How The Streaming Video Route Works

There is a fair bit of code written in our stream video route, so let’s look at it line by line.

<pre><code class="language-javascript"> const videoPath = `assets/${req.params.id}.mp4`;
 const videoStat = fs.statSync(videoPath);
 const fileSize = videoStat.size;
 const videoRange = req.headers.range;</code></pre>

First, from our request, we get the `id` from the route using `req.params.id` and use it to generate the `videoPath` to the video. We then read the `fileSize` using the file system `fs` we imported. For videos, a user’s browser will send a `range` parameter in the request. This lets the server know which chunk of the video to send back to the client.

Some browsers send a *range* in the initial request, but others don’t. For those that don’t, or if for any other reason the browser doesn’t send a range, we handle that in the `else` block. This code gets the file size and send the first few chunks of the video:

<pre><code class="language-javascript">else {
    const head = {
        'Content-Length': fileSize,
        'Content-Type': 'video/mp4',
    };
    res.writeHead(200, head);
    fs.createReadStream(path).pipe(res);
}</code></pre>

We will handle subsequent requests including the range in an `if` block.

<div class="break-out">

<pre><code class="language-javascript">if (videoRange) {
        const parts = videoRange.replace(/bytes=/, "").split("-");
        const start = parseInt(parts[0], 10);
        const end = parts[1]
            ? parseInt(parts[1], 10)
            : fileSize-1;
        const chunksize = (end-start) + 1;
        const file = fs.createReadStream(videoPath, {start, end});
        const head = {
            'Content-Range': `bytes ${start}-${end}/${fileSize}`,
            'Accept-Ranges': 'bytes',
            'Content-Length': chunksize,
            'Content-Type': 'video/mp4',
        };
        res.writeHead(206, head);
        file.pipe(res);
    }</code></pre>
</div>

This code above creates a read stream using the `start` and `end` values of the range. Set the `Content-Length` of the response headers to the chunk size that is calculated from the `start` and `end` values. We also use [HTTP code 206](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/206), signifying that the response contains partial content. This means the browser will keep making requests until it has fetched all chunks of the video.

## What Happens On Unstable Connections

If the user is on a slow connection, the network stream will signal it by requesting that the I/O source pauses until the client is ready for more data. This is known as *back-pressure*. We can take this example one step further and see how easy it is to extend the stream. We can easily add compression, too!

<div class="break-out">

<pre><code class="language-javascript">const start = parseInt(parts[0], 10);
        const end = parts[1]
            ? parseInt(parts[1], 10)
            : fileSize-1;
        const chunksize = (end-start) + 1;
        const file = fs.createReadStream(videoPath, {start, end});</code></pre>
</div>

We can see above that a `ReadStream` is created and serves the video chunk by chunk.

<div class="break-out">

<pre><code class="language-javascript">const head = {
            'Content-Range': `bytes ${start}-${end}/${fileSize}`,
            'Accept-Ranges': 'bytes',
            'Content-Length': chunksize,
            'Content-Type': 'video/mp4',
        };
res.writeHead(206, head);
        file.pipe(res);</code></pre>
</div>

The request header contains the `Content-Range`, which is the start and end changing to get the next chunk of video to stream to the frontend, the `content-length` is the chunk of video sent. We also specify the type of content we are streaming which is `mp4`. The writehead of 206 is set to respond with only newly made streams.

## Creating A Caption File For Our Videos

This is what a `.vtt` caption file looks like.

<pre><code class="language-javascript">WEBVTT

00:00:00.200 --> 00:00:01.000
Creating a tutorial can be very

00:00:01.500 --> 00:00:04.300
fun to do.</code></pre>

Captions files contain text for what is said in a video. It also contains time codes for when each line of text should be displayed. We want our videos to have captions, and we won’t be creating our own caption file for this tutorial, so you can head over to the captions folder in the `assets` directory in [the repo](https://github.com/Dunebook/Nuxt-Node-video-streaming/tree/main/backend/assets/captions) and download the captions.

Let’s create a new route that will handle the caption request:

<div class="break-out">

<pre><code class="language-javascript">router.get('/video/:id/caption', (req, res) => res.sendFile(`assets/captions/${req.params.id}.vtt`, { root: __dirname }));</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Building Our Frontend

To get started on the visual part of our system, we would have to build out our frontend scaffold.

**Note**: *You need vue-cli to create our app. If you don’t have it installed on your computer, you can run `npm install -g @vue/cli` to install it.*

## Installation

At the root of our project, let's create our front-end folder:

<pre><code class="language-bash">mkdir frontend
cd frontend</code></pre>

and in it, we initialize our `package.json` file, copy and paste the following in it:

<pre><code class="language-javascript">{
  "name": "my-app",
  "scripts": {
    "dev": "nuxt",
    "build": "nuxt build",
    "generate": "nuxt generate",
    "start": "nuxt start"
  }
}</code></pre>

then install `nuxt`:

<pre><code class="language-bash">npm add nuxt</code></pre>

and execute the following command to run Nuxt.js app:

<pre><code class="language-bash">npm run dev</code></pre>

## Our Nuxt File Structure

Now that we have Nuxt installed, we can begin laying out our frontend.

First, we need to create a `layouts` folder at the root of our app. This folder defines the layout of the app, no matter the page we navigate to. Things like our navigation bar and footer are found here. In the frontend folder, we create `default.vue` for our default layout when we start our frontend app.

<pre><code class="language-javascript">mkdir layouts
cd layouts
touch default.vue</code></pre>

Then a `components` folder to create all our components. We will be needing only two components, `NavBar` and `video` component. So in our root folder of frontend we:

<pre><code class="language-javascript">mkdir components
cd components
touch NavBar.vue
touch Video.vue</code></pre>

Finally, a pages folder where all our pages like `home` and `about` can be created. The two pages we need in this app, are the `home` page displaying all our videos and video information and a dynamic player page that routes to the video we click on.

<pre><code class="language-javascript">mkdir pages
cd pages
touch index.vue
mkdir player
cd player
touch _name.vue</code></pre>

Our frontend directory now looks like this:

<pre><code class="language-javascript">|-frontend
  |-components
    |-NavBar.vue
    |-Video.vue
  |-layouts
    |-default.vue
  |-pages
    |-index.vue
    |-player
      |-_name.vue
  |-package.json
  |-yarn.lock</code></pre> 

## Navbar Component

Our `NavBar.vue` looks like this:

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="navbar"&gt;
        &lt;h1&gt;Streaming App&lt;/h1&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;style scoped&gt;
.navbar {
    display: flex;
    background-color: #161616;
    justify-content: center;
    align-items: center;
}
h1{
    color:#a33327;
}
&lt;/style&gt;</code></pre>

The `NavBar` has a `h1` tag that displays **Streaming App**, with some little styling.

Let’s import the `NavBar` into our `default.vue` layout. 

<pre><code class="language-javascript">// default.vue
&lt;template&gt;
 &lt;div&gt;
   &lt;NavBar /&gt;
   &lt;nuxt /&gt;
 &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import NavBar from "@/components/NavBar.vue"
export default {
    components: {
        NavBar,
    }
}
&lt;/script&gt;</code></pre>

The `default.vue` layout now contains our `NavBar` component and the `<nuxt />` tag after it signifies where any page we create will be displayed.

In our `index.vue` (which is our homepage), let’s make a request to `https://localhost:5000/videos` to get all the videos from our server. Passing the data as a prop to our `video.vue` component we will create later. But for now, we have already imported it.

<pre><code class="language-javascript">&lt;template&gt;
&lt;div&gt;
  &lt;Video :videoList="videos"/&gt;
&lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import Video from "@/components/Video.vue"
export default {
  components: {
    Video
  },
head: {
    title: "Home"
  },
    data() {
      return {
        videos: []
      }
    },
    async fetch() {
      this.videos = await fetch(
        'https://localhost:5000/videos'
      ).then(res =&gt; res.json())
    }
}
&lt;/script&gt;</code></pre>

## Video Component

Below, we first declare our prop. Since the video data is now available in the component, using Vue’s `v-for` we iterate on all the data received and for each one, we display the information. We can use the `v-for` directive to loop through the data and display it as a list. Some basic styling has also been added.

<pre><code class="language-javascript">&lt;template&gt;
&lt;div&gt;
  &lt;div class="container"&gt;
    &lt;div
    v-for="(video, id) in videoList"
    :key="id"
    class="vid-con"
  &gt;
    &lt;NuxtLink :to="`/player/${video.id}`"&gt;
    &lt;div
      :style="{
        backgroundImage: `url(${video.poster})`
      }"
      class="vid"
    &gt;&lt;/div&gt;
    &lt;div class="movie-info"&gt;
      &lt;div class="details"&gt;
      &lt;h2&gt;{{video.name}}&lt;/h2&gt;
      &lt;p&gt;{{video.duration}}&lt;/p&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/NuxtLink&gt;
  &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
    props:['videoList'],
}
&lt;/script&gt;
&lt;style scoped&gt;
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 2rem;
}
.vid-con {
  display: flex;
  flex-direction: column;
  flex-shrink: 0;
  justify-content: center;
  width: 50%;
  max-width: 16rem;
  margin: auto 2em;
  
}
.vid {
  height: 15rem;
  width: 100%;
  background-position: center;
  background-size: cover;
}
.movie-info {
  background: black;
  color: white;
  width: 100%;
}
.details {
  padding: 16px 20px;
}
&lt;/style&gt;</code></pre>

We also notice that the `NuxtLink` has a dynamic route, that is routing to the `/player/video.id`. 

The functionality we want is when a user clicks on any of the videos, it starts streaming. To achieve this, we make use of the dynamic nature of the `_name.vue` route.

In it, we create a video player and set the source to our endpoint for streaming the video, but we dynamically append which video to play to our endpoint with the help of  `this.$route.params.name` that captures which parameter the link received.

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="player"&gt;
        &lt;video controls muted autoPlay&gt;
            &lt;source :src="`https://localhost:5000/videos/video/${vidName}`" type="video/mp4"&gt;
        &lt;/video&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
 data() {
      return {
        vidName: ''
      }
    },
mounted(){
    this.vidName = this.$route.params.name
}
}
&lt;/script&gt;
&lt;style scoped&gt;
.player {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 2em;
}
&lt;/style&gt;</code></pre>
</div>

When we click on any of the video we get:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b6e82b-9aa5-4c25-8f03-56c8bac69b74/01-nuxtjs-video-preview.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b6e82b-9aa5-4c25-8f03-56c8bac69b74/01-nuxtjs-video-preview.jpg" width="800" height="397" sizes="100vw" caption="Video streaming gets started when user clicks the thumbnail. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/234cb7d7-81ac-469a-ba08-a792edbfe159/1-building-video-streaming-app-nuxt-js-node-express.png'>Large preview</a>)" alt="Nuxt video streaming app final result" >}}

## Adding Our Caption File

To add our track file, we make sure all the `.vtt` files in the *captions* folder have the same name as our `id`. Update our video element with the track, making a request for the captions.

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="player"&gt;
        &lt;video controls muted autoPlay crossOrigin="anonymous"&gt;
            &lt;source :src="`https://localhost:5000/videos/video/${vidName}`" type="video/mp4"&gt;
            &lt;track label="English" kind="captions" srcLang="en" :src="`https://localhost:5000/videos/video/${vidName}/caption`" default&gt;
        &lt;/video&gt;
    &lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

We’ve added `crossOrigin="anonymous"` to the video element; otherwise, the request for captions will fail. Now refresh and you’ll see captions have been added successfully.

## What To Keep In Mind When Building Resilient Video Streaming.

When building streaming applications like Twitch, Hulu or Netflix, there are a number of things that are put into consideration:

- **Video data processing pipeline**  
This can be a technical challenge as high-performing servers are needed to serve millions of videos to users. High latency or downtime should be avoided at all costs.
- **Caching**  
Caching mechanisms should be used when building this type of application example Cassandra, Amazon S3, AWS SimpleDB.
- **Users’ geography**  
Considering the geography of your users should be thought about for distribution.

## Conclusion

In this tutorial, we have seen how to create a server in Node.js that streams videos, generates captions for those videos, and serves metadata of the videos. We’ve also seen how to use Nuxt.js on the frontend to consume the endpoints and the data generated by the server.

Unlike other frameworks, building an application with Nuxt.js and Express.js is quite easy and fast. The cool part about Nuxt.js is the way it manages your routes and makes you structure your apps better.

- You can get more information about Nuxt.js [here](https://nuxtjs.org/guide).
- You can get the [source code on Github](https://github.com/smashingmagazine/Nuxt-Node-video-streaming/).

### Resources

- “[Adding Captions And Subtitles To HTML5 Video](https://developer.mozilla.org/en-US/docs/Web/Guide/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video),” MDN Web Docs
- “[Understanding Captions And Subtitles](https://web.archive.org/web/20160117160743/https://screenfont.ca/learn/),” Screenfont.ca

{{< signature "ks, vf, yk, il" >}}
