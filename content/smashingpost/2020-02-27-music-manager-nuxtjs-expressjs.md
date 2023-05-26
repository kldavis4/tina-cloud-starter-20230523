---
title: 'How To Build A Music Manager With Nuxt.js And Express.js'
slug: music-manager-nuxtjs-expressjs
author: deven-rathore
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/138620e7-7da5-4729-9a4e-74f7b34e58ca/music-manager-nuxtjs-expressjs.png
date: 2020-02-27T13:00:00.000Z
summary: >-
  This article introduces how Multer streamlines the process of handling file uploads. It also introduces how to use Mongoose to interact with our database by building a music manager app using Express.js alongside Multer for the music upload and Nuxt.js (Vue framework) for our frontend.
description: >-
  This article introduces how Multer streamlines the process of handling file uploads. It also introduces how to use Mongoose to interact with our database by building a music manager app using Express.js alongside Multer for the music upload and Nuxt.js (Vue framework) for our frontend.
categories:
  - Apps
  - Vue
  - JavaScript
  - Nuxt.js
  - Frameworks
---

Handling digital media assets such as audio and video in your application can be tricky because of the considerations that have to be made server-side (e.g. networking, storage and the asynchronous nature of handling file uploads). However, we can use libraries like [Multer](https://www.npmjs.com/package/multer) and Express.js to simplify our workflow on the backend while using Nuxt.js (Vue framework) to build out the front-end interactions.

Whenever a web client uploads a file to a server, it is generally submitted through a form and encoded as `multipart/form-data`. `Multer` is a middleware for Express.js and Node.js that makes it easy to handle this so-called `multipart/form-data` whenever your users upload files. In this tutorial, I will explain how you can build a music manager app by using Express.js with Multer to upload music and Nuxt.js (Vue framework) for our frontend.

### Prerequisites

- Familiarity with HTML, CSS, and JavaScript (ES6+);
- Node.js, npm and MongoDB installed on your development machine;
- VS code or any code editor of your choice;
- Basic Knowledge of Express.js.

{{% feature-panel %}}

## Building The Back-End Service

Let’s start by creating a directory for our project by navigating into the directory, and issuing `npm init -y` on your terminal to create a *package.json* file that manages all the dependencies for our application.

<pre><code class="language-json">mkdir serverside && cd serverside
npm init -y
</code></pre>

Next, install `multer`, `express`, and the other dependencies necessary to Bootstrap an Express.js app.

<div class="break-out">

 <pre><code class="language-bash">npm install express multer nodemon mongoose cors morgan body-parser --save
</code></pre>
</div>

Next, create an *index.js* file:

<pre><code class="language-bash">touch index.js
</code></pre>

Then, in the *index.js* file, we will initialize all the modules, create an Express.js app, and create a server for connecting to browsers:

<pre><code class="language-javascript">const express = require("express");
const PORT = process.env.PORT || 4000;
const morgan = require("morgan");
const cors = require("cors");
const bodyParser = require("body-parser");
const mongoose = require("mongoose");
const config = require("./config/db");
const app = express();
//configure database and mongoose
mongoose.set("useCreateIndex", true);
mongoose
  .connect(config.database, { useNewUrlParser: true })
  .then(() => {
    console.log("Database is connected");
  })
  .catch(err => {
    console.log({ database_error: err });
  });
// db configuaration ends here
//registering cors
app.use(cors());
//configure body parser
app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());
//configure body-parser ends here
app.use(morgan("dev")); // configire morgan
// define first route
app.get("/", (req, res) => {
  res.json("Hola MEVN devs...Assemble");
});
app.listen(PORT, () => {
  console.log(`App is running on ${PORT}`);
});
</code></pre>

We, first of all, bring in Express.js into the project and then define a port that our application will be running on. Next, we bring in the `body-parser`, `morgan` ,`mongoose` and the `cors` dependencies.

We then save the express instance in a variable called `app`.  We can use the `app` instance to configure middleware in our application just as we configured the `cors` middleware. We also use the `app` instance to set up the root route that will run in the port we defined.

Let’s now create a `/config` folder for our database `config` and `multer` config:

<pre><code class="language-javascript">mkdir config and cd config
touch multer.js && touch db.js
</code></pre>

Then open *config/db.js* and add the following code to configure our database:

<pre><code class="language-javascript">module.exports = {
  database: "mongodb://localhost:27017/",
  secret: "password"
};
</code></pre>

(This is actually an object that holds the database URL and the database secret.)  

Running `nodemon`  and navigating to `localhost:4000` on your browser should give you this message:

<pre><code class="language-bash">"Hola MEVN devs...Assemble"
</code></pre>

Also, this is what your terminal should now look like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d60d74-5ebd-440e-b9a5-f40d9754b0b0/1-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d60d74-5ebd-440e-b9a5-f40d9754b0b0/1-nuxtjs-expressjs.png" sizes="100vw" caption="Terminal preview (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d60d74-5ebd-440e-b9a5-f40d9754b0b0/1-nuxtjs-expressjs.png'>Large preview</a>)" alt="Running Nodemon using Terminal" >}}

## Setting Up Model, Routes, And Controllers

Let’s set up a file structure by typing in the following:

<pre><code class="language-javascript">mkdir api && cd api
mkdir model && cd model && touch Music.js
cd ..
mkdir controller && cd controller && touch musicController.js
cd ..
mkdir routes && cd routes && touch music.js
</code></pre>

In our terminal, we use `mkdir` to create a new directory, and then `cd` to move into a directory. So we start by creating a directory called `api` and then move into the `api` directory. 

The `touch` command is used to create a new file inside a directory using the terminal, while the `cd` command is used to move out of a directory.

Now let’s head on over to our *api/model/Music.js* file to create a music schema. A model is a class with which we construct documents. In this case, each document will be a piece of music with properties and behaviors as declared in our schema:

<pre><code class="language-javascript">let mongoose = require("mongoose");
let musicSchema = mongoose.Schema({
  title: {
    type: String,
    required: true
  },
  music: {
    type: Object,
    required: true
  },
  artist: {
    type: String,
    required: true
  },
  created: {
    type: Date,
    default: Date.now()
  }
});
let Music = mongoose.model("Music", musicSchema);
module.exports = Music;
</code></pre>

Let’s head over to `config/multer` to configure Multer:

<pre><code class="language-javascript">let multer = require("multer");
const path = require("path");
const storage = multer.diskStorage({
  destination: (req, res, cb) => {
    cb(null, "./uploads");
  },
  filename: (req, file, cb) => {
    cb(null, new Date().toISOString() + file.originalname);
  }
});
const fileFilter = (req, file, cb) => {
  if (
     file.mimetype === "audio/mpeg" ||
     file.mimetype === "audio/wave" ||
     file.mimetype === "audio/wav" ||
     file.mimetype === "audio/mp3"
  ) {
    cb(null, true);
  } else {
    cb(null, false);
  }
};
exports.upload = multer({
  storage: storage,
  limits: {
    fileSize: 1024 * 1024 * 5
  },
  fileFilter: fileFilter
});
</code></pre>

In the *multer.js* file, we start by setting up a folder where all the uploaded music files will be uploaded. We need to make this file static by defining that in the *index.js* file:

<pre><code class="language-javascript">app.use('/uploads', express.static('uploads'));
</code></pre>

After that, we write a simple validator that will check the file *mimetype* before uploading. We then define the `multer` instance by adding the storage location, the limits of each file, and the validator that we created.

### Create The Necessary Routes

Now let’s create our routes. Below is the list of endpoints we will be creating.

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>HTTP POST /music</code></td>
      <td>Add new music</td>
    </tr>
    <tr>
      <td><code>HTTP GET /music</code></td>
      <td>Get all music</td>
    </tr>
    <tr>
      <td><code>HTTP DELETE /music/:blogId</code></td>
      <td>Delete a music</td>
    </tr>
  </tbody>
</table>

Let’s start by creating the blog route. Head over to *api/routes/music.js* and write the following code:

<div class="break-out">

 <pre><code class="language-javascript">const express = require("express");
const router = express.Router();
const musicController = require("../controller/musicController");
const upload = require("../../config/multer");
router.get("/",  musicController.getAllMusics);
router.post("/", upload.upload.single("music"), musicController.addNewMusic);
router.delete("/:musicId", musicController.deleteMusic);
module.exports = router;
</code></pre>
</div>

**Note**: *Now whenever we make a* `get` *request to* `/music`*. the route calls the* `getAllMusic` *function that is located in the ‘controllers’ file.*

Let’s move on over to `api/controllers/musicController` to define the controllers. We start by writing a function to get all the music in our database using the mongoose `db.collection.find` method which will return all the items in that collection.

After doing that, we write another function that will create a piece of new music in the database. We need to create a new music instance using the `new` keyword and then define the music object. After doing this, we will use the mongoose `save` method to add new music to the database.

In order to delete a piece of music, we need to use the mongoose `remove` method by simply passing the music ID as a parameter in the `remove` instance. This results to mongoose looking into the music collection that has that particular ID and then removing it from that collection.

<div class="break-out">

 <pre><code class="language-javascript">let mongoose = require("mongoose");
const Music = require("../model/Music");
exports.getAllMusics = async (req, res) => {
  try {
    let music = await Music.find();
    res.status(200).json(music);
  } catch (err) {
    res.status(500).json(err);
  }
};
exports.addNewMusic = async (req, res) => {
  try {
    const music = new Music({
      title:req.body.title,
      artist:req.body.artist,
      music:req.file
    });
    
    let newMusic = await music.save();
    res.status(200).json({ data: newMusic });
  } catch (err) {
    res.status(500).json({ error: err });
  }
};
exports.deleteMusic = async (req, res) => {
  try {
    const id = req.params.musicId;
    let result = await Music.remove({ &#95;id: id });
    res.status(200).json(result);
  } catch (err) {
    res.status(500).json(err);
  }
};
</code></pre>
</div>

Last but not least, in order to test the routes, we need to register the music routes in our *index.js* file:

<pre><code class="language-javascript">const userRoutes = require("./api/user/route/user"); //bring in our user routes
app.use("/user", userRoutes);
</code></pre>

{{% ad-panel-leaderboard %}}

## Testing The End Points

To test our endpoints, we will be using POSTMAN.

### Adding New Music

To test the `Add Music` functionality, set the method of the request by clicking on the methods drop-down. After doing this, type the URL of the endpoint and then click on the body tab to select how you want to send your data. (In our case, we will be using the form-data method.)

So click on the form-data and set up your model key. As you set it up, give the keys some value as shown in the image below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c923c966-759b-46c1-bcee-d3b2253efa0f/2-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c923c966-759b-46c1-bcee-d3b2253efa0f/2-nuxtjs-expressjs.png" sizes="100vw" caption="Testing Adding new music API in Postman dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c923c966-759b-46c1-bcee-d3b2253efa0f/2-nuxtjs-expressjs.png'>Large preview</a>)" alt="Testing Adding new music API using Postman" >}}

After doing this, click on ‘Send’ to make the request.

### Listing All Music

To list all of the music in our database, we have to type the endpoint URL in the URL section provided. After doing this, click on the ‘Send’ button to make the request.
    
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b65765e-43b4-40a4-a94c-faa7c881372b/3-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b65765e-43b4-40a4-a94c-faa7c881372b/3-nuxtjs-expressjs.png" sizes="100vw" caption="Testing Listing API in Postman dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b65765e-43b4-40a4-a94c-faa7c881372b/3-nuxtjs-expressjs.png'>Large preview</a>)" alt="Testing Listing API using Postman" >}}

### Deleting Music

To delete a piece of music, we need to pass the `music id` as a parameter.
    
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55cd6a0-2484-4614-99ea-6f2cfc4860ed/4-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55cd6a0-2484-4614-99ea-6f2cfc4860ed/4-nuxtjs-expressjs.png" sizes="100vw" caption="Testing Delete API Postman dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55cd6a0-2484-4614-99ea-6f2cfc4860ed/4-nuxtjs-expressjs.png'>Large preview</a>)" alt="Testing Delete API using Postman" >}}

That’s it!

## Building The Frontend

For our frontend, we will be using a Vue framework: Nuxt.js. 

<blockquote>“Nuxt is a progressive framework based on Vue.js to create modern web applications. It is based on Vue.js official libraries (vue, vue-router and vuex) and powerful development tools (webpack, Babel and PostCSS).”<br /><br />&mdash; <a href="https://nuxtjs.org/guide/">NuxtJS Guide</a></blockquote>

To create a new Nuxt.js application, open up your terminal and type in the following (with `musicapp` as the name of the app we will be building):

<pre><code class="language-bash">$ npx create-nuxt-app musicapp
</code></pre>

During the installation process, we will be asked some questions regarding the project setup:

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>Project name</code></td>
      <td>musicapp</td>
    </tr>
    <tr>
      <td><code>project description</code></td>
      <td>A Simple music manager app</td>
    </tr>
    <tr>
      <td><code>Author name</code></td>
      <td>&lt;your name&gt;</td>
    </tr>
    <tr>
      <td><code>Package manager</code></td>
      <td>npm</td>
    </tr>
    <tr>
      <td><code>UI framework</code></td>
      <td>Bootstrap vue</td>
    </tr>
    <tr>
      <td><code>custom ui framework</code></td>
      <td>none</td>
    </tr>
    <tr>
      <td><code>Nuxt modules</code></td>
      <td>Axios,pwa (use the spacebar on your keyboard to select items)</td>
    </tr>
    <tr>
      <td><code>Linting tool</code></td>
      <td>Prettier</td>
    </tr>
    <tr>
      <td><code>test framework</code></td>
      <td>None</td>
    </tr>
    <tr>
      <td><code>Rendering Mode</code></td>
      <td>Universal (SSR)</td>
    </tr>
    <tr>
      <td><code>development tool</code></td>
      <td>Jsonconfig.json</td>
    </tr>
  </tbody>
</table>

After selecting all of this, we have to wait a little while for the project to be set up. Once it’s ready, move into the `/project` folder and serve the project as follows:

<pre><code class="language-bash">cd musicapp && npm run dev
</code></pre>

Open up the project in any code editor of your choice and then open the project in the browser by accessing `localhost:3000`.
 
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a5b642-9308-4c62-89b1-2e6d2bb18354/5-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a5b642-9308-4c62-89b1-2e6d2bb18354/5-nuxtjs-expressjs.png" sizes="100vw" caption="Nuxt.js Project Preview (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a5b642-9308-4c62-89b1-2e6d2bb18354/5-nuxtjs-expressjs.png'>Large preview</a>)" alt="Preview Of Nuxt.js project" >}}

## Configuring Axios

We will be using `axios` to make an HTTP request to our back-end server. Axios is already installed in our project, so we just have to configure the `baseURL`- to our backend server.

To do this, open the *nuxt.config.js* file in the `root` directory and add the `baseURL` in the `axios` object.

<pre><code class="language-javascript">axios: {
  baseURL:'https://localhost:4000'
},
</code></pre>

## Building The Music Manager

### Setting Up The UI

Let’s start by cleaning up the UI. Open up the *pages/index.vue* file and remove all of the code in there with the following:

<pre><code class="language-javascript">&lt;template&gt;
&lt;div&gt;Hello&lt;/div&gt;
&lt;/template&gt;
</code></pre>

After doing this, you should only be able to see a “Hello” in the browser.

In the `root` directory, create a `/partials` folder. Inside the `/partials` folder, create a *navbar.vue* file and add the following code:

<div class="break-out">

 <pre><code class="language-javascript">
&lt;template&gt;
  &lt;header&gt;
    &lt;nav class="navbar navbar-expand-lg navbar-light bg-info"&gt;
      &lt;div class="container"&gt;
        &lt;a class="navbar-brand" href="#"&gt;Music App&lt;/a&gt;
        &lt;button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        &gt;
          &lt;span class="navbar-toggler-icon"&gt;&lt;/span&gt;
        &lt;/button&gt;
        &lt;div class="collapse navbar-collapse justify-content-end" id="navbarNav"&gt;
          &lt;ul class="navbar-nav"&gt;
            &lt;li class="nav-item active"&gt;
              &lt;a class="nav-link" href="#"&gt;Player&lt;/a&gt;
            &lt;/li&gt;
            &lt;li class="nav-item"&gt;
              &lt;a class="nav-link" href="#"&gt;Manager&lt;/a&gt;
            &lt;/li&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/nav&gt;
  &lt;/header&gt;
&lt;/template&gt;
&lt;style scoped&gt;
.nav-link,
.navbar-brand {
  color: #ffff !important;
}
&lt;/style&gt;
</code></pre>
</div>

**Note**: *We will be using the component to navigate through pages in our application. This is just going to be a simple component made up of Bootstrap* `navbar`. *Check out the official Bootstrap [documentation](https://getbootstrap.com/docs/4.1/getting-started/introduction/) for more reference.*

Next, let’s define a custom layout for the application. Open the `/layouts` folder, replace the code in the *default.vue* file with the code below.

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;navbar /&gt;
    &lt;nuxt /&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import navbar from '@/partial/navbar'
export default {
  components: {
    navbar
  }
}
&lt;/script&gt;
</code></pre>

We import the `navbar` into this layout, meaning that all the pages in our application will have that `navbar` component in it. (This is going to be the component that all other component in our application will be mounted.)

After this, you should be able to see this in your browser:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/363a52e3-4e15-421e-9492-4a9d9fc71108/6-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/363a52e3-4e15-421e-9492-4a9d9fc71108/6-nuxtjs-expressjs.png" sizes="100vw" caption="Nuxt.js Navbar component (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/363a52e3-4e15-421e-9492-4a9d9fc71108/6-nuxtjs-expressjs.png'>Large preview</a>)" alt="Nuxt.js Navbar component after modification" >}}

Now let’s setup the UI for our manager. To do this, we need to create a `/manager` folder within the components folder and then add a file into the folder named *manager.vue*. 

In this file, add the following code:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;section class="mt-5"&gt;
    &lt;div class="container mb-4"&gt;
      &lt;div class="row"&gt;
        &lt;div class="col-md-12"&gt;
          &lt;div class="card"&gt;
            &lt;div class="card-body"&gt;
              &lt;div class="card-title mb-4"&gt;
                &lt;h4&gt;Add Music&lt;/h4&gt;
              &lt;/div&gt;
              &lt;form&gt;
                &lt;div class="form-group"&gt;
                  &lt;label for="title"&gt;Title&lt;/label&gt;
                  &lt;input type="text" class="form-control" /&gt;
                &lt;/div&gt;
                &lt;div class="form-group"&gt;
                  &lt;label for="artist"&gt;Artist&lt;/label&gt;
                  &lt;input type="text" class="form-control" /&gt;
                &lt;/div&gt;
                &lt;div class="form-group"&gt;
                  &lt;label for="artist"&gt;Music&lt;/label&gt;
                  &lt;div class="custom-file"&gt;
                    &lt;input type="file" class="custom-file-input" id="customFile" /&gt;
                    &lt;label class="custom-file-label" for="customFile"&gt;Choose file&lt;/label&gt;
                  &lt;/div&gt;
                &lt;/div&gt;
                &lt;div class="form-group"&gt;
                  &lt;button class="btn btn-primary"&gt;Submit&lt;/button&gt;
                &lt;/div&gt;
              &lt;/form&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="container"&gt;
      &lt;div class="row"&gt;
        &lt;div class="col-md-12"&gt;
          &lt;div class="card bg-light p-1 showdow-sm"&gt;
            &lt;div class="card-title"&gt;
              &lt;button class="btn btn-info m-3"&gt;Add Music&lt;/button&gt;
            &lt;/div&gt;
            &lt;div class="card-body"&gt;
              &lt;table class="table"&gt;
                &lt;thead&gt;
                  &lt;tr&gt;
                    &lt;th scope="col"&gt;#&lt;/th&gt;
                    &lt;th scope="col"&gt;Title&lt;/th&gt;
                    &lt;th scope="col"&gt;Artist&lt;/th&gt;
                    &lt;th scope="col"&gt;Date created&lt;/th&gt;
                    &lt;th scope="col"&gt;Action&lt;/th&gt;
                  &lt;/tr&gt;
                &lt;/thead&gt;
                &lt;tbody&gt;
                  &lt;tr&gt;
                    &lt;td&gt;1&lt;/td&gt;
                    &lt;td&gt;Demo Title&lt;/td&gt;
                    &lt;td&gt;Wisdom.vue&lt;/td&gt;
                    &lt;td&gt;12/23/13&lt;/td&gt;
                    &lt;td&gt;
                      &lt;button class="btn btn-info"&gt;Delete&lt;/button&gt;
                    &lt;/td&gt;
                  &lt;/tr&gt;
                &lt;/tbody&gt;
              &lt;/table&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/section&gt;
&lt;/template&gt;
</code></pre>
</div>

**Note**: *This is just a simple Bootstrap template for adding music into our application. The form will define a table template that will list all os the music that can be found in our database.*


<p class="c-pre-sidenote--left">After defining this component, we need to register it in the <code>/pages</code> folder to initailize routing.</p><p class="c-sidenote c-sidenote--right">Nuxt.js doesn’t have a ‘router.js’ file like Vue.js. It uses the pages folder for routing. For more details, visit the <a href="https://nuxtjs.org/guide/routing/">Nuxt.js</a> website.</p>

To register the component, create a `/manager` folder within the `/pages` folder and create an *index.vue* file. Then, place the following code inside the file:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;manager /&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import manager from '@/components/manager/manager'
export default {
  components: {
    manager
  }
}
&lt;/script&gt;
</code></pre>

This is the component that will render in our `pages` route.

After doing this, head over to your browser and navigate to `/manager` &mdash; you should be seeing this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7925d2c0-65ab-4693-851e-70946ae72fbe/7-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7925d2c0-65ab-4693-851e-70946ae72fbe/7-nuxtjs-expressjs.png" sizes="100vw" caption="Music manager UI (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7925d2c0-65ab-4693-851e-70946ae72fbe/7-nuxtjs-expressjs.png'>Large preview</a>)" alt="UI of music Manager" >}}

## Listing All Music

Let’s continue by creating a function that will fetch all of the music. This function will be registered in the created life cycle hook, so that whenever the component is created, the function will be called.

Let’s start by creating a variable in the `vue` instance that will hold all of the music:

<pre><code class="language-bash">allmusic = [];
musicLoading: false,
</code></pre>

Then, define a `getAllMusics` function and add the following code:

<pre><code class="language-javascript">async getAllMusics() {
    this.musicLoading = true
    try {
      let data = await this.$axios.$get('/music')
      this.allmusic = data
      this.musicLoading = false
    } catch (err) {
      this.musicLoading = false
      swal('Error', 'Error Fetting Musics', 'error')
    }
  }
</code></pre>

Next, register within the created life cycle hook:

<pre><code class="language-javascript">created() {
    this.getAllMusics()
  }
</code></pre>

{{% ad-panel-leaderboard %}}

## Outputting The Data

Now it’s time to output all of the songs on the table which we’ve created earlier:

<div class="break-out">

 <pre><code class="language-javascript">&lt;table class="table"&gt;
              &lt;thead&gt;
                &lt;tr&gt;
                  &lt;th scope="col"&gt;#&lt;/th&gt;
                  &lt;th scope="col"&gt;Title&lt;/th&gt;
                  &lt;th scope="col"&gt;Artist&lt;/th&gt;
                  &lt;th scope="col"&gt;Date created&lt;/th&gt;
                  &lt;th scope="col"&gt;Action&lt;/th&gt;
                &lt;/tr&gt;
              &lt;/thead&gt;
              &lt;div
                v-if="musicLoading"
                class="spinner-border"
                style="width: 3rem; height: 3rem;"
                role="status"
              &gt;
                &lt;span class="sr-only"&gt;Loading...&lt;/span&gt;
              &lt;/div&gt;
              &lt;tbody v-else&gt;
                &lt;tr v-for="(music, index) in allmusic" :key="index"&gt;
                  &lt;td&gt;{{ index + 1 }}&lt;/td&gt;
                  &lt;td&gt;{{ music.title }}&lt;/td&gt;
                  &lt;td&gt;{{ music.artist }}&lt;/td&gt;
                  &lt;td&gt;{{ music.created }}&lt;/td&gt;
                  &lt;td&gt;
                    &lt;button class="btn btn-info" @click="deleteMusic(music._id)"&gt;Delete&lt;/button&gt;
                  &lt;/td&gt;
                &lt;/tr&gt;
              &lt;/tbody&gt;
            &lt;/table&gt;
</code></pre>
</div>

Remember that table we created earlier? Well, we will need to loop through the response we get back from our backend to list all of the music received back from the database.

## Adding Music

To add a new piece of music we need to make an HTTP request to the back-end server with the music details. To do this, let’s start by modifying the form and handling of the file uploads.

On the form, we need to add an `event` listener that will listen to the form when it is submitted. On the `input` field, we add a `v-` model to bind the value to the input field.

<div class="break-out">

 <pre><code class="language-javascript">&lt;form @submit.prevent="addNewMusic"&gt;
            &lt;div class="form-group"&gt;
              &lt;label for="title"&gt;Title&lt;/label&gt;
              &lt;input type="text" v-model="musicDetails.title" class="form-control" /&gt;
            &lt;/div&gt;
            &lt;div class="form-group"&gt;
              &lt;label for="artist"&gt;Artist&lt;/label&gt;
              &lt;input type="text" v-model="musicDetails.artist" class="form-control" /&gt;
            &lt;/div&gt;
            &lt;div class="form-group"&gt;
              &lt;label for="artist"&gt;Music&lt;/label&gt;
              &lt;div class="custom-file"&gt;
                &lt;input
                  type="file"
                  id="customFile"
                  ref="file"
                  v-on:change="handleFileUpload()"
                  class="custom-file-input"
                /&gt;
                &lt;label class="custom-file-label" for="customFile"&gt;Choose file&lt;/label&gt;
              &lt;/div&gt;
            &lt;/div&gt;
            &lt;div class="form-group"&gt;
               &lt;button class="btn btn-primary" :disabled="isDisabled"&gt;
                &lt;span
                  class="spinner-border spinner-border-sm"
                  v-if="addLoading"
                  role="status"
                  aria-hidden="true"
                &gt;&lt;/span&gt;Submit
              &lt;/button&gt;
            &lt;/div&gt;
          &lt;/form&gt;
</code></pre>
</div>

And the script section should look like this:

<pre><code class="language-javascript">&lt;script&gt;
export default {
  data() {
    return {
      musicDetails: {
        title: '',
        artist: '',
        music: ''
      },
      allmusic = [],
        musicLoading: false,
      isValid: false;
      addLoading: false,
    }
  },
  computed: {
    isDisabled: function() {
      if (
        this.musicDetails.title === '' ||
        this.musicDetails.artist === '' ||
        this.musicDetails.music === ''
      ) {
        return !this.isValid
      }
    }
  },
  methods: {
    handleFileUpload() {
      this.musicDetails.music = this.$refs.file.files[0]
      console.log(this.musicDetails.music.type)
    },
    addNewMusic() {
      let types = /(\.|\/)(mp3|mp4)$/i
      if (
        types.test(this.musicDetails.music.type) ||
        types.test(this.musicDetails.music.name)
      ) {
        console.log('erjkb')
      } else {
        alert('Invalid file type')
        return !this.isValid
      }
    }
  }
}
&lt;/script&gt;
</code></pre>

We will define a function that will send a request to our back-end service to create any new music that has been added to the list. Also. we need to write a simple validation function that will check for the file type so that the users can only upload files with an extention of *.mp3* and *.mp4*.

It’s important to define a computed property to make sure that our input field isn’t empty. We also need to add a simple validator that will make sure the the file we are trying to upload is actually a music file.

Let’s continue by editing the `addMusic` function to make a request to our back-end service. But before we do this, let’s first install `sweetalert` which will provide us with a nice modal window. To do this this, open up your terminal and type in the following:

<pre><code class="language-bash">npm i sweetalert
</code></pre>

After installing the package, create a *sweetalert.js* file in the `/plugins` folder and add this:

<pre><code class="language-bash">import Vue from 'vue';
import swal from 'sweetalert';

Vue.prototype.$swal = swal;
</code></pre>

Then, register the plugin in the *nuxt.config.js* file inside the plugin instace like this:

<pre><code class="language-javascript">plugins: [
    {
      src: '~/plugins/sweetalert'
    }
  ],
</code></pre>

We have now successfully configured `sweetalert` in our application, so we can move on and edit the `addmusic` function to this:

<pre><code class="language-javascript">addNewMusic() {
    let types = /(\.|\/)(mp3|mp4)$/i
    if (
      types.test(this.musicDetails.music.type) ||
      types.test(this.musicDetails.music.name)
    ) {
      let formData = new FormData()
      formData.append('title', this.musicDetails.title)
      formData.append('artist', this.musicDetails.artist)
      formData.append('music', this.musicDetails.music)
      this.addLoading = true
      this.$axios
        .$post('/music', formData)
        .then(response => {
          console.log(response)
          this.addLoading = false
          this.musicDetails = {}
          this.getAllMusics() // we will create this function later
          swal('Success', 'New Music Added', 'success')
        })
        .catch(err => {
          this.addLoading = false
          swal('Error', 'Something Went wrong', 'error')
          console.log(err)
        })
    } else {
      swal('Error', 'Invalid file type', 'error')
      return !this.isValid
    }
  },
</code></pre>

Let’s write a simple script that will toggle the form, i.e it should only display when we want to add new music.

We can do this by editing the ‘Add Music’ button in the table that displays all of the music that can be found:

<pre><code class="language-javascript">&lt;button
    class="btn btn-info m-3"
    @click="initForm"&gt;
    {{addState?"Cancel":"Add New Music"}}
&lt;/button&gt;
</code></pre>

Then, add a state that will hold the state of the form in the `data` property:

<pre><code class="language-javascript">addState: false
</code></pre>

After doing this, let’s define the `initForm` function:

<pre><code class="language-javascript">initForm() {
    this.addState = !this.addState
  },
</code></pre>

And then add `v-if="addState"` to the `div` that holds the form:

<pre><code class="language-javascript">&lt;div class="card" v-if="addState"&gt;
</code></pre>

## Deleting Music

To delete music, we need to call the `delete` endpoint and pass the `music id` as a param. Let’s add a `click` event to the ‘Delete’ button that will trigger the function to delete a function:

<div class="break-out">

 <pre><code class="language-javascript">&lt;button class="btn btn-info" @click="deleteMusic(music._id)"&gt;Delete&lt;/button&gt;
</code></pre> 
</div>

The `delete` function will be making an HTTP request to our back-end service. After getting the music ID from the `deleteMusic` function parameter, we will add the ID in the URL that we are using to send the request. This specifies the exact piece of music that ought to be removed from the database.

<div class="break-out">

 <pre><code class="language-javascript">deleteMusic(id) {
    swal({
      title: 'Are you sure?',
      text: 'Once deleted, you will not be able to recover this Music!',
      icon: 'warning',
      buttons: true,
      dangerMode: true
    }).then(willDelete => {
      if (willDelete) {
        this.$axios
          .$delete('/music/' + id)
          .then(response => {
            this.getAllMusics()
            swal('Poof! Your Music file has been deleted!', {
              icon: 'success'
            })
          })
          .catch(err => {
            swal('Error', 'Somethimg went wrong', 'error')
          })
      } else {
        swal('Your Music file is safe!')
      }
    })
  }
</code></pre>
</div>

With all of this, we have just built our music manager. Now it’s time to build the music player.

Let’s start by creating a new folder in the components folder named `/player`. Then, create a *player.vue* file within this folder and add this:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;section&gt;
    &lt;div class="container"&gt;
      &lt;div class="row"&gt;
        &lt;div class="col-md-12"&gt;
          &lt;h3 class="text-center"&gt;Player&lt;/h3&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/section&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  data() {
    return {}
  }
}
&lt;/script&gt;
&lt;style  scoped&gt;
&lt;/style&gt;
</code></pre>

Next, let’s import this component into the *index.vue* file in the `/pages` folder. Replace the code in *index.vue* file to this:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;player /&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import player from '@/components/player/player'
export default {
  components: {
    player
  }
}
&lt;/script&gt;
</code></pre>

Let’s configure routing in our `navbar` component to enable routing between our pages.

To route in a Nuxt.js application, the `nuxt-link` is used after which you have specified the page for that route to a particular instance. So let’s edit the code in the `partials/navbar` component to this:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;header&gt;
    &lt;nav class="navbar navbar-expand-lg navbar-light bg-info"&gt;
      &lt;div class="container"&gt;
        &lt;nuxt-link to="/" class="navbar-brand"&gt;Music App&lt;/nuxt-link&gt;
        &lt;button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        &gt;
          &lt;span class="navbar-toggler-icon"&gt;&lt;/span&gt;
        &lt;/button&gt;
        &lt;div class="collapse navbar-collapse justify-content-end" id="navbarNav"&gt;
          &lt;ul class="navbar-nav"&gt;
            &lt;li class="nav-item active"&gt;
              &lt;nuxt-link to="/" class="nav-link"&gt;Player&lt;/nuxt-link&gt;
            &lt;/li&gt;
            &lt;li class="nav-item"&gt;
              &lt;nuxt-link to="/manager" class="nav-link"&gt;Manager&lt;/nuxt-link&gt;
            &lt;/li&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/nav&gt;
  &lt;/header&gt;
&lt;/template&gt;
&lt;style scoped&gt;
.nav-link,
.navbar-brand {
  color: #ffff !important;
}
&lt;/style&gt;
</code></pre>
</div>

With this, we can navigate through our pages by using the navbar.

## Building The Player

Before we begin, we need to extend Webpack to load audio files. Audio files should be processed by `file-loader`. This loader is already included in the default Webpack configuration, but it is not set up to handle audio files. 

To do this, go to the *nuxt.config.js* file and modify the `build` object to this:

<pre><code class="language-javascript">build: {
    extend(config, ctx) {
      config.module.rules.push({
        test: /\.(ogg|mp3|mp4|wav|mpe?g)$/i,
        loader: 'file-loader',
        options: {
          name: '\[path\][name].[ext]'
        }
      })
    }
  }
</code></pre>

Next, let’s write a function that will get all songs and then use the [`Audio`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement/Audio) constructor to play the first song in the `allMusic` array.

For starters, let’s modify our *player.vue* file to this:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;section v-if="allMusic"&gt;
    &lt;div class="container"&gt;
      &lt;div class="row"&gt;
        &lt;div class="col-md-12"&gt;
          &lt;h3 class="text-center"&gt;Player&lt;/h3&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="row"&gt;
        &lt;div class="col-md-6"&gt;
          &lt;span&gt;{{this.current.title}} - {{this.current.artist}}&lt;/span&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/section&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  data() {
    return {
      current: {
        title: '',
        artist: ''
      },
      song: true,
      isplaying: false,
      allMusic: null,
      index: 0,
      player: ''
    }
  },
  methods: {
     async initPlayer() {
      if (this.allMusic !== []) {
        this.current = await this.allMusic[this.index]
        this.player.src = `https://localhost:4000/${this.current.music.path}`
      } else {
        this.song = true
      }
    },
      async getAllSongs() {
        try {
        let response = await this.$axios.$get('/music')
        console.log(response)
        if (response === []) {
          this.song = true
          this.current = null
        } else {
          this.song = false
          this.allMusic = response
        }
        await this.initPlayer()
      } catch (err) {
        this.current = null
        console.log(err)
      }
    }
  },
  created() {
 if (process.client) {
      this.player = new Audio()
    }
    this.getAllSongs()
  }
}
&lt;/script&gt;
&lt;style  scoped&gt;
&lt;/style&gt;
</code></pre>
</div>

Once the file is served, the music will play in the background and then you should be able to see this in your browser:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27eb3de4-0ab7-42b1-8bb2-6f88f78692b1/8-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27eb3de4-0ab7-42b1-8bb2-6f88f78692b1/8-nuxtjs-expressjs.png" sizes="100vw" caption="Music player UI (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27eb3de4-0ab7-42b1-8bb2-6f88f78692b1/8-nuxtjs-expressjs.png'>Large preview</a>)" alt="UI of Music player" >}}

To stop the music, all you need to do is comment out the `await player.play()` in the `initPlayer` function.

## Creating The Player UI

Let’s now define our music player UI by replacing the template in our *player.vue* file with the following:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;section v-if="allMusic"&gt;
    &lt;div class="container"&gt;
      &lt;div class="row mb-5"&gt;
        &lt;div class="col-md-12"&gt;
          &lt;h3 class="text-center"&gt;Player&lt;/h3&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="row mt-5"&gt;
        &lt;div class="col-md-6"&gt;
          &lt;img
            src="https://images.pexels.com/photos/3624281/pexels-photo-3624281.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
            class="image"
          /&gt;
          &lt;div class="card player_card"&gt;
            &lt;div class="card-body"&gt;
              &lt;h6 class="card-title"&gt;
                &lt;b&gt;{{this.current.title}} - {{this.current.artist}}&lt;/b&gt;
              &lt;/h6&gt;
              &lt;div&gt;
                &lt;i class="fas fa-backward control mr-4"&gt;&lt;/i&gt;
                &lt;i class="fas fa-play play"&gt;&lt;/i&gt;
                &lt;i class="fas fa-pause play"&gt;&lt;/i&gt;
                &lt;i class="fas fa-forward control ml-4"&gt;&lt;/i&gt;
              &lt;/div&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
        &lt;div class="col-md-6"&gt;
          &lt;div class="card shadow"&gt;
            &lt;table class="table"&gt;
              &lt;thead&gt;
                &lt;tr&gt;
                  &lt;th scope="col"&gt;#&lt;/th&gt;
                  &lt;th scope="col"&gt;Title&lt;/th&gt;
                  &lt;th scope="col"&gt;Artist&lt;/th&gt;
                  &lt;th scope="col"&gt;Action&lt;/th&gt;
                &lt;/tr&gt;
              &lt;/thead&gt;
              &lt;tbody&gt;
                &lt;tr&gt;
                  &lt;th scope="row"&gt;1&lt;/th&gt;
                  &lt;td&gt;Mark&lt;/td&gt;
                  &lt;td&gt;Otto&lt;/td&gt;
                  &lt;td&gt;
                    &lt;button class="btn btn-primary"&gt;Play&lt;/button&gt;
                  &lt;/td&gt;
                &lt;/tr&gt;
              &lt;/tbody&gt;
            &lt;/table&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/section&gt;
&lt;/template&gt;
</code></pre>
</div>

Then, add the following style into the `style` section:

<pre><code class="language-css">&lt;style  scoped&gt;
.image {
  border-radius: 5px !important;
  position: relative;
  height: 300px;
  width: 100%;
}
.player_card {
  text-align: center;
  bottom: 20px;
  margin: 0px 40px;
}
.text-muted {
  font-size: 15px;
}
.play {
  font-size: 40px;
}
.control {
  font-size: 25px;
}
&lt;/style&gt;
</code></pre>

After modifying this, the player should look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2242e7d7-25ea-464c-a1d3-6950bc32d4e0/9-nuxtjs-expressjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2242e7d7-25ea-464c-a1d3-6950bc32d4e0/9-nuxtjs-expressjs.png" sizes="100vw" caption="Final UI of music player (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2242e7d7-25ea-464c-a1d3-6950bc32d4e0/9-nuxtjs-expressjs.png'>Large preview</a>)" alt="Music player final UI" >}}

## Adding The Play Function

We’ll continue by displaying the music description on the table. In order to do this, replace the table with the code below:

<div class="break-out">

 <pre><code class="language-javascript">&lt;table class="table"&gt;
              &lt;thead&gt;
                &lt;tr&gt;
                  &lt;th scope="col"&gt;#&lt;/th&gt;
                  &lt;th scope="col"&gt;Title&lt;/th&gt;
                  &lt;th scope="col"&gt;Artist&lt;/th&gt;
                  &lt;th scope="col"&gt;Action&lt;/th&gt;
                &lt;/tr&gt;
              &lt;/thead&gt;
              &lt;tbody&gt;
                &lt;tr v-for="(music,index) in allMusic" :key="index"&gt;
                  &lt;th scope="row"&gt;{{index+1}}&lt;/th&gt;
                  &lt;td&gt;{{music.title}}&lt;/td&gt;
                  &lt;td&gt;{{music.artist}}&lt;/td&gt;
                  &lt;td&gt;
                    &lt;button class="btn btn-primary"&gt;Play&lt;/button&gt;
                  &lt;/td&gt;
                &lt;/tr&gt;
              &lt;/tbody&gt;
            &lt;/table&gt;
</code></pre>
</div>

We don’t want to display the ‘Play’ and ‘Pause’ icons at the same time. Instead, we want a situation that when the song is playing, the ‘Pause’ icon is displayed. Also, when the song is paused, the play icon should be displayed.

To achieve this, we need to set a `isPlaying` state to the `false` instance and then use this instance to toggle the icons. After that, we will add a function to our ‘Play’ icon.

<pre><code class="language-javascript">isplaying:false
</code></pre>

After doing this, modify your ‘Play’ and ‘Pause’ icon to this:

<pre><code class="language-javascript">&lt;i class="fas fa-play play" v-if="!isplaying" @click="play"&gt;&lt;/i&gt;
&lt;i class="fas fa-pause play" v-else&gt;&lt;/i&gt;
</code></pre>

With all this let’s define the `play` method:

<div class="break-out">

 <pre><code class="language-javascript">play(song) {
      console.log(song)
      if (song) {
        this.current = song
        this.player.src = `https://localhost:4000/${this.current.music.path}`
      }
      this.player.play()
      this.isplaying = true
    },
</code></pre>
</div>

We, first of all, get the current song and pass it into the `function` parameter. We then define the JavaScript `Audio()` instance. Next, we check if the song is null: If it isn’t, we set `this.current` to the song we passed in the parameter, and then we call the `Audio` player instance.  (Also, don’t forget that we have to set the `isPlaying` state to `true` when the music is playing.)

## Adding The Pause Function

To pause a song, we will use the `Audio` pause method. We need to add a `click` event to the pause icon:

<pre><code class="language-javascript">&lt;i class="fas fa-pause play" @click="pause" v-else&gt;&lt;/i&gt;
</code></pre>

And then define the function in the `methods` instance:

<pre><code class="language-javascript">pause() {
      this.player.pause()
      this.isplaying = false
    },
</code></pre>

## Playing A Song From The Music List

This is quite simple to implement. All we have to do is add a `click` event that will change the `song` parameter in the `play` method to the song we just created.

Simply modify the `play` button on the music list table to this:

<div class="break-out">

 <pre><code class="language-javascript">&lt;button class="btn btn-primary" @click="play(music)"&gt;Play&lt;/button&gt;
</code></pre>
</div>

And there you have it!

## Adding The Next Function

To add the next function, we need to increment the index by one. To do this, add a `click` event to the next icon:

<pre><code class="language-bash">@click="next"
</code></pre>

And then define the `prev` function in the `methods` instance:

<pre><code class="language-javascript">next() {
      this.index++
      if (this.index > this.allMusic.length - 1) {
        this.index = 0
      }
       this.current = this.allMusic[this.index]
      this.play(this.current)
    },
</code></pre>

This conditional is responsible for replaying all of the songs whenever the last song in the list has been played.

## Adding The `previous` Function

This is actually the opposite of the next function, so let’s add a `click` event to the previous function:

<pre><code class="language-bash">@click="prev"
</code></pre>

Next, we define the previous function:

<pre><code class="language-javascript">prev() {
      this.index--
      if (this.index < 0) {
        this.index = this.allMusic.length - 1
      }
      this.current = this.allMusic[this.index]
      this.play(this.current)
    },
</code></pre>

Our music player app is now complete!

## Conclusion

In this article, we looked at how we can build a music manager with Nuxt.js and Express.js. Along the way, we saw how Multer streamlines the process of handling file uploads and how to use Mongoose to interact without a database. Finally, we used Nuxt.js to build the client app which gives it a fast and snappy feel.

Unlike other frameworks, building an application with Nuxt.js and Express.js is quite easy and fast. The cool part about Nuxt.js is the way it manages your routes and makes you structure your apps better.

- You can access more information about Nuxt.js [here](https://nuxtjs.org/guide).
- You can access the source code on Github [here](https://github.com/Dunebook/Music-app-nuxtjs)

{{< signature "dm, il" >}}
