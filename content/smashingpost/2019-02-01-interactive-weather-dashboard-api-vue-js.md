---
title: 'Using Vue.js To Create An Interactive Weather Dashboard With APIs'
slug: interactive-weather-dashboard-api-vue-js
author: souvik-sarkar
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1788a5-b934-468b-9925-019445dcebfe/interactive-weather-dashboard-image3.png
date: 2019-02-01T13:00:18+01:00
summary: >-
  Creating a dashboard with API data is often a complex affair. Choosing your tech stack, integrating APIs, selecting the right charts and beautifying with CSS styles can become tricky. This tutorial is a step-by-step guide on how to help you create a weather dashboard in Vue.js using API data.
description: >-
  Creating a dashboard with API data is often a complex affair. Choosing your tech stack, integrating APIs, selecting the right charts and beautifying with CSS styles can become tricky. This tutorial is a step-by-step guide on how to help you create a weather dashboard in Vue.js using API data.
categories:
  - Interaction Design
  - JavaScript
  - API
  - Vue
disable_ads: true
disable_panels: true
---
(This is a sponsored article.) In this tutorial, you will build a simple weather dashboard from scratch. It will be a client-end application that is neither a “Hello World” example, nor too intimidating in its size and complexity.

The entire project will be developed using tools from the [Node.js](https://nodejs.org/en/) + [npm](https://www.npmjs.com/) ecosystem. In particular, we will be heavily relying on the [Dark Sky API](https://darksky.net/dev) for the data, [Vue.js](https://vuejs.org/) for all the heavy lifting, and [FusionCharts](https://www.fusioncharts.com/?utm_source=smashing_mag&utm_medium=blog&utm_campaign=weather_dashboard_vue) for data visualization.

### Prerequisites

We expect that you are familiar with the following:

- **HTML5 and CSS3** (we will also be using the basic features provided by [Bootstrap](https://getbootstrap.com/);
- **JavaScript** (especially ES6 way of using the language);
- **Node.js and npm** (the basics of the environment and package management is just fine).

Apart from the ones mentioned above, it would be great if you have familiarity with **Vue.js**, or any other similar JavaScript framework. We don’t expect you to know about **FusionCharts** &mdash; it’s so easy to use that you will learn it on the fly!

### Expected Learnings

Your key learnings from this project will be:

1. How to plan about implementing a good dashboard
2. How to develop applications with Vue.js
3. How to create data-driven applications 
4. How to visualize data using FusionCharts

In particular, each of the sections take you a step closer to the learning goals:

<ol>
	<li><a href="#weather-dashboard">An Introduction To The Weather Dashboard</a><br />This chapter gives you an overview of different aspects of the undertaking.</li>
	<li><a href="#create-project">Create The Project</a><br />In this section, you learn about creating a project from scratch using the Vue command-line tool.</li>
	<li><a href="#customize-the-default-project-structure">Customize The Default Project Structure</a><br />The default project scaffolding that you get in the previous section is not enough; here you learn the additional stuff needed for the project from a structural point of view.</li>
	<li><a href="#data-acquisition-processing">Data Acquisition And Processing</a><br />This section is the meat of the project; all the critical code for acquiring and processing data from the API is showcased here. Expect to spend maximum time on this section.</li>
	<li><a href="#data-visualization-with-fusioncharts">Data Visualization With FusionCharts</a><br />Once we have all the data and other moving parts of the project stabilized, this section is dedicated towards visualizing the data using FusionCharts and a bit of CSS. </li>
</ol>

## 1. The Dashboard Workflow

Before we dive into the implementation, it is important to be clear about our plan. We break our plan into four distinct aspects:

### Requirements

What are our requirements for this project? In other words, what are the things that we want to showcase through our Weather Dashboard? Keeping in mind that our intended audience are probably mere mortals with simple tastes, we would like to show them the following:

- Details of the location for which they want to see the weather, along with some primary information about the weather. Since there are no stringent requirements, we will figure out the boring details later. However, at this stage, it is important to note that we will have to provide the audience a search box, so that they can provide input for the location of their interest.
- Graphical information about the weather of their location of interest, such as:
	- Temperature variation for the day of query
	- Highlights of today’s weather:
		- Wind Speed and Direction
		- Visibility
		- UV Index

**Note**: *The data obtained from the API provides information regarding many other aspects of the weather. We choose not to use all of them for the sake of keeping the code to a minimum.*

### Structure

Based on the requirements, we can structure our dashboard as shown below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1788a5-b934-468b-9925-019445dcebfe/interactive-weather-dashboard-image3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1788a5-b934-468b-9925-019445dcebfe/interactive-weather-dashboard-image3.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1788a5-b934-468b-9925-019445dcebfe/interactive-weather-dashboard-image3.png'>Large preview</a>)" alt="Dashboard structure" >}}

### Data

Our dashboard is as good as the data we get, because there will be no pretty visualizations without proper data. There are plenty of public APIs that provide weather data &mdash; some of them are free, and some are not. For our project, we will collect data from the [Dark Sky API](https://darksky.net/dev). However, we will not be able to poll the API endpoint from the client end directly. Don’t worry, we have a workaround that will be revealed just at the right time! Once we get the data for the searched location, we will do some data processing and formatting &mdash; you know, the type of technicalities that helps us pay the bills.

### Visualization

Once we get clean and formatted data, we plug it in to FusionCharts. There are very few JavaScript libraries in the world as capable as FusionCharts. Out of the vast number of offerings from FusionCharts, we will use only a few &mdash; all written in JavaScript, but works seamlessly when integrated with the [Vue wrapper for FusionCharts](https://www.fusioncharts.com/vue-js-charts?utm_source=smashing_mag&utm_medium=blog&utm_campaign=weather_dashboard_vue).

Armed with the bigger picture, let’s get our hands dirty &mdash; it’s time to make things concrete! In the next section, you will create the basic Vue project, on top of which we will build further.

## 2. Creating The Project

To create the project, execute the following steps:

<ol>
	<li><strong>Install Node.js + npm</strong><br />(<em>If you have Node.js installed on your computer, skip this step.</em>)<br />Node.js comes with npm bundled with it, so you don’t need to install npm separately. Depending on the operating system, download and install Node.js according to the instructions given <a href="https://nodejs.org/en/download/">here</a>.<br /><br />Once installed, it’s probably a good idea to verify if the software is working correctly, and what are their versions. To test that, open the command-line/terminal and execute the following commands:<br />

		<pre><code class="language-bash">node --version
npm --version
</code></pre>
</li>
<li><strong>Install packages with npm</strong><br />Once you have npm up and running, execute the following command to install the basic packages necessary for our project.<br />

	<pre><code class="language-bash">npm install -g vue@2 vue-cli@2
</code></pre>
</li>
<li id="scaffolding"><strong>Initialize project scaffolding with <code>vue-cli</code></strong><br />Assuming that the previous step has gone all well, the next step is to use the <code>vue-cli</code> &mdash; a command-line tool from Vue.js, to initialize the project. To do that, execute the following:</li>
<ul>
	<li>Initialize the scaffolding with webpack-simple template.<br />

		<pre><code class="language-bash">vue init webpack-simple vue_weather_dashboard
		</code></pre>
		You will be asked a bunch of questions &mdash; accepting the defaults for all but the last question will be good enough for this project; answer <code>N</code> for the last one.
		{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371f9f63-b02f-4492-9b3d-aa1d4a8ccb7c/interactive-weather-dashboard-image2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371f9f63-b02f-4492-9b3d-aa1d4a8ccb7c/interactive-weather-dashboard-image2.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371f9f63-b02f-4492-9b3d-aa1d4a8ccb7c/interactive-weather-dashboard-image2.png'>Large preview</a>)" alt="A screenshot of the command-line/terminal" >}}
		Keep in mind that although <code>webpack-simple</code> is excellent for quick prototyping and light application like ours, it is not particularly suited for serious applications or production deployment. If you want to use any other template (although we would advise against it if you are a newbie), or would like to name your project something else, the syntax is:

		<pre><code class="language-bash">vue init [template-name] [project-name]
		</code></pre>
	</li>
	<li>Navigate to the directory created by vue-cli for the project.<br />

		<pre><code class="language-bash">cd vue_weather_dashboard
		</code></pre>
	</li>
	<li>Install all the packages mentioned in the <code>package.json</code>, which has been created by the <code>vue-cli</code> tool for the <code>webpack-simple</code> template.

		<pre><code class="language-bash">npm install
		</code></pre>
	</li>
	<li>Start the development server and see your default Vue project working in the browser!<br />

		<pre><code class="language-bash">npm run dev
		</code></pre>
</li>
</ul>
</ol>

If you are new to [Vue.js](https://vuejs.org/), take a moment to savor your latest achievement &mdash; you have created a small Vue application and its running at [localhost:8080](https://127.0.0.0:8080/)!

{{< rimg href="https://vuejs.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7800541-236a-41cb-97ac-98fd43644c7f/interactive-weather-dashboard-image4.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7800541-236a-41cb-97ac-98fd43644c7f/interactive-weather-dashboard-image4.png'>Large preview</a>)" alt="A screenshot of the Vue.js website" >}}

### Brief Explanation Of The Default Project Structure

It’s time to take a look at the structure inside the directory `vue_weather_dashboard`, so that you have an understanding of the basics before we start modifying it.

The structure looks something like this:

<pre><code class="language-bash">vue_weather_dashboard
|--- README.md
|--- node_modules/
|     |--- ...
|     |--- ...
|     |--- [many npm packages we installed]
|     |--- ...
|     |--- ...
|--- package.json
|--- package-lock.json
|--- webpack.config.js
|--- index.html
|--- src
|     |--- App.vue
|     |--- assets
|     |     |--- logo.png
|     |--- main.js 
</code></pre>

Although it might be tempting to skip getting familiar with the default files and directories, if you are new to Vue, we **strongly recommend** at least taking a look at the contents of the files. It can be a good educational session and trigger questions that you should pursue on your own, especially the following files:

- `package.json`, and just a glance at its cousin `package-lock.json`
- `webpack.config.js`
- `index.html`
- `src/main.js`
- `src/App.vue`

A brief explanation of each of the files and directories shown in the tree diagram are given below:

- **README.md**  
No prize for guessing &mdash; it is primarily for humans to read and understand the steps necessary for <a href="#scaffolding">creating the project scaffolding</a>.
- **node_modules/**  
This is the directory where npm downloads the packages necessary for kickstarting the project. The information about the packages necessary are available in the `package.json` file.
- **package.json**  
This file is created by the vue-cli tool based on the requirements of the `webpack-simple` template, and contains information about the npm packages (including with their versions and other details) that must be installed. Take a hard look at the content of this file &mdash; this is where you should visit and perhaps edit to add/delete packages necessary for the project, and then run npm install. Read more about `package.json` [here](https://docs.npmjs.com/files/package.json).
- **package-lock.json**  
This file is created by npm itself, and is primarily meant for keeping a log of things that npm downloaded and installed. 
- **webpack.config.js**  
This a JavaScript file that contains the configuration of webpack &mdash; a tool that bundles different aspects of our project together (code, static assets, configuration, environments, mode of use, etc.), and minifies before serving it to the user. The benefit is that all things are tied together automatically, and the user experience enhances greatly because of the improvement in the application’s performance (pages are served quickly and loads faster on the browser). As you might encounter later, this is the file that needs to be inspected when something in the build system does not works the way it is intended to be. Also, when you want to deploy the application, this is one of the key files that needs to be edited (read more [here](https://webpack.js.org/guides/getting-started/)). 
- **index.html**  
This HTML file serves as the matrix (or you can say, template) where data and code is to be embedded dynamically (that’s what Vue primarily does), and then served to the user.
- **src/main.js**  
This JavaScript file contains code that primarily manages top/project level dependencies, and defines the topmost level Vue component. In short, it orchestrates the JavaScript for the entire project, and serves as the entry point of the application. Edit this file when you need to declare project-wide dependencies on certain node modules, or you want something to be changed about the topmost Vue component in the project.
- **src/App.vue**  
In the previous point, when we were talking about the “topmost Vue component”, we were essentially talking about this file. Each .vue file in the project is a component, and components are hierarchically related. At the start, we have only one `.vue` file, i.e. `App.vue`, as our only component. But shortly we will add more components to our project (primarily following the structure of the dashboard), and link them in accordance to our desired hierarchy, with App.vue being the ancestor of all. These `.vue` files will contain code in a format that Vue wants us to write. Don’t worry, they are JavaScript code written maintaining a structure that can keep us sane and organized. You have been warned &mdash; by the end of this project, if you are new to Vue, you may get addicted to the `template &mdash; script &mdash; style` way of organizing code! 

Now that we have created the foundation, it’s time to:

- Modify the templates and tweak the configuration files a bit, so that the project behaves just the way we want.
- Create new `.vue` files, and implement the dashboard structure with Vue code.

We will learn them in the next section, which is going to be a bit long and demands some attention. If you need caffeine or water, or want to discharge &mdash; now is the time! 

## 3. Customizing The Default Project Structure

It’s time to tinker with the foundation that the scaffolded project has given us. Before you start, ensure that the development server provided by `webpack` is running. The advantage of running this server *continuously* is that any changes you make in the source code &mdash; one you save it and refresh the web page &mdash; it gets immediately reflected on the browser.

If you want to start the development server, just execute the following command from the terminal (assuming your current directory is the project directory):

<pre><code class="language-bash">npm run dev
</code></pre>

In the following sections, we will modify some of the existing files, and add some new files.
It will be followed by brief explanations of the content of those files, so that you have an idea of what those changes are meant to do.

### Modify Existing Files

#### index.html

Our application is literally a single page application, because there is just one webpage that gets displayed on the browser. We will talk about this later, but first let’s just make our first change &mdash; altering the text within the `<title>` tag.

With this small revision, the HTML file looks like the following:

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;!-- Modify the text of the title tag below --&gt;
    &lt;title&gt;Vue Weather Dashboard&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div id="app"&gt;&lt;/div&gt;
    &lt;script src="/dist/build.js"&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Take a moment to refresh the webpage at `localhost:8080`, and see the change reflected on the title bar of the tab on the browser &mdash; it should say “Vue Weather Dashboard”. However, this was just to demonstrate you the process of making changes and verifying if it’s working. We have more things to do!

This simple HTML page lacks many things that we want in our project, especially the following: 

- Some meta information
- CDN links to Bootstrap (CSS framework)
- link to custom stylesheet (yet to be added in the project)
- Pointers to the Google Maps Geolocation API from `<script>` tag

After adding those things, the final `index.html` has the following content:

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
 &lt;head&gt;
   &lt;meta http-equiv="Content-Type" content="text/html;charset=utf-8" /&gt;
   &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
   &lt;meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"&gt;
   &lt;link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"&gt;
   &lt;link rel="stylesheet" type="text/css" href="src/css/style.css"&gt;
   &lt;title&gt;Weather Dashboard&lt;/title&gt;
   &lt;script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC-lCjpg1xbw-nsCc11Si8Ldg2LKYizqI4&libraries=places"&gt;&lt;/script&gt;
 &lt;/head&gt;
 &lt;body&gt;
   &lt;div id="app"&gt;&lt;/div&gt;
   &lt;script src="/dist/build.js"&gt;&lt;/script&gt;
 &lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

Save the file, and refresh the webpage. You might have noticed a slight bump while the page was getting loaded &mdash; it is primarily due to the fact that the page style is now being controlled by Bootstrap, and the style elements like fonts, spacing, etc. are different from the default we had earlier (if you are not sure, roll back to the default and see the difference).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68802b5-8099-46e5-a89c-87da85634584/interactive-weather-dashboard-image5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68802b5-8099-46e5-a89c-87da85634584/interactive-weather-dashboard-image5.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68802b5-8099-46e5-a89c-87da85634584/interactive-weather-dashboard-image5.png'>Large preview</a>)" alt="A screenshot when you refresh the webpage with localhost:8080" >}}

**Note**: *One important thing before we move on &mdash; the URL for the Google Maps API contains a key which is a property of FusionCharts. For now, you can use this key to build the project, as we don’t want you to get bogged down by these type of minute details (which can be distractions while you are new). However, we strongly urge you to [generate and use your own Google Maps API key](https://developers.google.com/maps/documentation/javascript/get-api-key) once you have made some progress and feel comfortable to pay attention to these tiny details.*

#### package.json

At the time of writing this, we used certain versions of the npm packages for our project, and we know for sure that those things work together. However, by the time you are executing the project, it is very much possible that the latest stable versions of the packages that npm downloads for you are not the same as we used, and this might break the code (or do things that are beyond our control). Thus, it is very important to have the exact same `package.json` file that was used to build this project, so that our code/explanations and the results you get are consistent.

The content of the `package.json` file should be:

<div class="break-out">

 <pre><code class="language-json">{
 "name": "vue_weather_dashboard",
 "description": "A Vue.js project",
 "version": "1.0.0",
 "author": "FusionCharts",
 "license": "MIT",
 "private": true,
 "scripts": {
   "dev": "cross-env NODE_ENV=development webpack-dev-server --open --hot",
   "build": "cross-env NODE_ENV=production webpack --progress --hide-modules"
 },
 "dependencies": {
   "axios": "^0.18.0",
   "babel": "^6.23.0",
   "babel-cli": "^6.26.0",
   "babel-polyfill": "^6.26.0",
   "fusioncharts": "^3.13.3",
   "moment": "^2.22.2",
   "moment-timezone": "^0.5.21",
   "vue": "^2.5.11",
   "vue-fusioncharts": "^2.0.4"
 },
 "browserslist": [
   "> 1%",
   "last 2 versions",
   "not ie <= 8"
 ],
 "devDependencies": {
   "babel-core": "^6.26.0",
   "babel-loader": "^7.1.2",
   "babel-preset-env": "^1.6.0",
   "babel-preset-stage-3": "^6.24.1",
   "cross-env": "^5.0.5",
   "css-loader": "^0.28.7",
   "file-loader": "^1.1.4",
   "vue-loader": "^13.0.5",
   "vue-template-compiler": "^2.4.4",
   "webpack": "^3.6.0",
   "webpack-dev-server": "^2.9.1"
 }
}
</code></pre>
</div>

We encourage you to go through the new `package.json`, and figure out what are functions of different objects in the json. You may prefer changing the value of the "`author`" key to your name. Also, the packages mentioned in the dependencies will reveal themselves at the right time in the code. For the time being, it’s sufficient to know that:

- `babel`-related packages are for properly handling the ES6 style code by the browser;
- `axios` deals with [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-based HTTP requests;
- `moment` and moment-timezone are for date/time manipulation;
- `fusioncharts` and `vue-fusioncharts` are responsible for rendering charts:
- `vue`, for obvious reasons.

#### webpack.config.js

As with `package.json`, we suggest you to maintain a `webpack.config.js` file that is consistent with the one we used for building the project. However, before making any changes, we recommend you to carefully compare the default code in the `webpack.config.js`, and the code we have provided below. You will notice quite a few differences &mdash; google them and have a basic idea of what they mean. Since explaining webpack configurations in depth is out of the scope of this article, you are on your own in this regard.

The customized `webpack.config.js` file is as follows:

<div class="break-out">

 <pre><code class="language-javascript">var path = require('path')
var webpack = require('webpack')

module.exports = {
 entry: ['babel-polyfill', './src/main.js'],
 output: {
   path: path.resolve(__dirname, './dist'),
   publicPath: '/dist/',
   filename: 'build.js'
 },
 module: {
   rules: [
     {
       test: /\.css$/,
       use: [
         'vue-style-loader',
         'css-loader'
       ],
     },      {
       test: /\.vue$/,
       loader: 'vue-loader',
       options: {
         loaders: {
         }
         // other vue-loader options go here
       }
     },
     {
       test: /\.js$/,
       loader: 'babel-loader',
       exclude: /node_modules/
     },
     {
       test: /\.(png|jpg|gif|svg)$/,
       loader: 'file-loader',
       options: {
         name: '[name].[ext]?[hash]'
       }
     }
   ]
 },
 resolve: {
   alias: {
     'vue$': 'vue/dist/vue.esm.js'
   },
   extensions: ['*', '.js', '.vue', '.json']
 },
 devServer: {
   historyApiFallback: true,
   noInfo: true,
   overlay: true,
   host: '0.0.0.0',
   port: 8080
 },
 performance: {
   hints: false
 },
 devtool: '#eval-source-map'
}

if (process.env.NODE_ENV === 'production') {
 module.exports.devtool = '#source-map'
 // https://vue-loader.vuejs.org/en/workflow/production.html
 module.exports.plugins = (module.exports.plugins || []).concat([
   new webpack.DefinePlugin({
     'process.env': {
       NODE_ENV: '"production"'
     }
   }),
   new webpack.optimize.UglifyJsPlugin({
     sourceMap: true,
     compress: {
       warnings: false
     }
   }),
   new webpack.LoaderOptionsPlugin({
     minimize: true
   })
 ])
}
</code></pre>
</div>

With changes made to the project’s `webpack.config.js`, it’s imperative that you stop the development server which is running (<kbd>Ctrl</kbd> + <kbd>C</kbd>), and restart it with the following command executed from the project’s directory after installing all the packages mentioned in the `package.json` file: 

<pre><code class="language-bash">npm install

npm run dev
</code></pre>

With this, the ordeal of tweaking the configurations and ensuring that the right packages are in place ends. However, this also marks the journey of modifying and writing code, which is a bit long but also very rewarding!

#### src/main.js

This file is the key to top-level orchestration of the project &mdash; it is here that we define:

- What the top level dependencies are (where to get the most important npm packages necessary);
- How to resolve the dependencies, along with instructions to Vue on using plugins/wrappers, if any;
- A Vue instance that manages the topmost component in the project: `src/App.vue` (the nodal `.vue` file).

In line with our goals for the `src/main.js` file, the code should be:

<div class="break-out">

 <pre><code class="language-javascript">// Import the dependencies and necessary modules
import Vue from 'vue';
import App from './App.vue';
import FusionCharts from 'fusioncharts';
import Charts from 'fusioncharts/fusioncharts.charts';
import Widgets from 'fusioncharts/fusioncharts.widgets';
import PowerCharts from 'fusioncharts/fusioncharts.powercharts';
import FusionTheme from 'fusioncharts/themes/fusioncharts.theme.fusion';
import VueFusionCharts from 'vue-fusioncharts';

// Resolve the dependencies
Charts(FusionCharts);
PowerCharts(FusionCharts);
Widgets(FusionCharts);
FusionTheme(FusionCharts);

// Globally register the components for project-wide use
Vue.use(VueFusionCharts, FusionCharts);

// Instantiate the Vue instance that controls the application
new Vue({
 el: '#app',
 render: h => h(App)
})
</code></pre>
</div>

#### src/App.vue

This is one of the most important files in the entire project, and represents the topmost component in the hierarchy &mdash; the entire application itself, as a whole. For our project, this component will do all the heavy lifting, which we will explore later. For now, we want to get rid of the default boilerplate, and put something of our own.

If you are new to Vue’s way of organizing code, it would be better to get an idea of the general structure within the `.vue` files. The `.vue` files comprises of three sections:

- **Template**  
This is where the HTML template for the page is defined. Apart from the static HTML, this section also contains Vue’s way of embedding dynamic content, using the double curly braces `{{ }}`.
- **Script**  
JavaScript rules this section, and is responsible for generating dynamic content that goes and sits within the HTML template at appropriate places. This section is primarily an object that is exported, and consists of:
	- **Data**  
	This is a function itself, and usually it returns some desired data encapsulated within a nice data structure.
	- **Methods**  
	An object that consists of one or more functions/methods, each of which usually manipulates data in some way or the other, and also controls the dynamic content of the HTML template.
	- **Computed**  
	Much like the method object discussed above with one important distinction &mdash; while all the functions within the method object are executed whenever any one of them is called, the functions within the computed object behaves much more sensibly, and executes if and only if it has been called.
- **Style**  
This section is for CSS styling that applies to the HTML of the page (written within template) &mdash; put the good old CSS here to make your pages beautiful!

Keeping the above paradigm in mind, let’s minimally customize the code in `App.vue`:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;p&gt;This component’s code is in {{ filename }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  data() {
    return {
      filename: 'App.vue'
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

Remember that the above code snippet is simply for testing out that `App.vue` is working with our own code in it. It will later go on through a lot of changes, but first save the file and refresh the page on the browser.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae50e3f-da4c-40ee-b9a4-48d2ac8ebd98/interactive-weather-dashboard-image7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae50e3f-da4c-40ee-b9a4-48d2ac8ebd98/interactive-weather-dashboard-image7.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae50e3f-da4c-40ee-b9a4-48d2ac8ebd98/interactive-weather-dashboard-image7.png'>Large preview</a>)" alt="A screenshot of the browser with the message “This component’s code is in App.vue”" >}}

At this point, it’s probably a good idea to get some help in tooling. Check out the [Vue devtools for Chrome](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en), and if you don’t have much problems in using Google Chrome as your default browser for development, install the tool and play around with it a bit. It will come in extremely handy for further development and debugging, when things becomes more complicated.

### Additional Directories And Files

The next step would be to add additional files, so that the structure of our project becomes complete. We would add the following directories and files:

- `src/css/`
    &mdash; `style.css`
- `src/assets/`
    &mdash; [`calendar.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/calendar.svg)
    &mdash; [`vlocation.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/location.svg)
    &mdash; [`search.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/search.svg)
    &mdash; [`winddirection.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/winddirection.svg)
    &mdash; [`windspeed.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/windspeed.svg)
- `src/components/`
    &mdash; `Content.vue`
    &mdash; `Highlights.vue`
    &mdash; `TempVarChart.vue`
    &mdash; `UVIndex.vue`
    &mdash; `Visibility.vue`
    &mdash; `WindStatus.vue`

**Note**: *Save the hyperlinked `.svg` files in your project.*

Create the directories and files mentioned above. The final project structure should like look (remember to delete folders and files from the default structure that are now unnecessary):

<pre><code class="language-bash">vue_weather_dashboard/
|--- README.md
|--- node_modules/
|     |--- ...
|     |--- ...
|     |--- [many npm packages we installed]
|     |--- ...
|     |--- ...
|--- package.json
|--- package-lock.json
|--- webpack.config.js
|--- index.html
|--- src/
|     |--- App.vue
|     |--- css/
|     |     |--- style.css 
|     |--- assets/
|     |     |--- calendar.svg
|     |     |--- location.svg
|     |     |--- location.svg
|     |     |--- winddirection.svg
|     |     |--- windspeed.svg
|     |--- main.js
|     |--- components/
|     |     |--- Content.vue
|     |     |--- Highlights.vue
|     |     |--- TempVarChart.vue
|     |     |--- UVIndex.vue
|     |     |--- Visibility.vue
|     |     |--- WindStatus.vue
</code></pre>

*There might be some other files, like* `.babelrc`, `.gitignore`, `.editorconfig`, *etc. in the project’s root folder. You may ignore them safely for now.*

In the following section, we will add minimal content to the newly added files, and test whether they are properly working.

#### src/css/style.css

Although it will not be of much use immediately, copy the following code to the file:

<div class="break-out">

 <pre><code class="language-css">@import url("https://fonts.googleapis.com/css?family=Roboto:300,400,500");

:root {
   font-size: 62.5%;
}

body {
   font-family: Roboto;
   font-weight: 400;
   width: 100%;
   margin: 0;
   font-size: 1.6rem;
}

#sidebar {
   position: relative;
   display: flex;
   flex-direction: column;
   background-image: linear-gradient(-180deg, #80b6db 0%, #7da7e2 100%);
}

#search {
   text-align: center;
   height: 20vh;
   position: relative;
}

#location-input {
   height: 42px;
   width: 100%;
   opacity: 1;
   border: 0;
   border-radius: 2px;
   background-color: rgba(255, 255, 255, 0.2);
   margin-top: 16px;
   padding-left: 16px;
   color: #ffffff;
   font-size: 1.8rem;
   line-height: 21px;
}

#location-input:focus {
   outline: none;
}

::placeholder {
   color: #FFFFFF;
   opacity: 0.6;
}

#current-weather {
   color: #ffffff;
   font-size: 8rem;
   line-height: 106px;
   position: relative;
}

#current-weather>span {
   color: #ffffff;
   font-size: 3.6rem;
   line-height: 42px;
   vertical-align: super;
   opacity: 0.8;
   top: 15px;
   position: absolute;
}

#weather-desc {
   font-size: 2.0rem;
   color: #ffffff;
   font-weight: 500;
   line-height: 24px;
}

#possibility {
   color: #ffffff;
   font-size: 16px;
   font-weight: 500;
   line-height: 19px;
}

#max-detail,
#min-detail {
   color: #ffffff;
   font-size: 2.0rem;
   font-weight: 500;
   line-height: 24px;
}

#max-detail>i,
#min-detail>i {
   font-style: normal;
   height: 13.27px;
   width: 16.5px;
   opacity: 0.4;
}

#max-detail>span,
#min-detail>span {
   color: #ffffff;
   font-family: Roboto;
   font-size: 1.2rem;
   line-height: 10px;
   vertical-align: super;
}

#max-summary,
#min-summary {
   opacity: 0.9;
   color: #ffffff;
   font-size: 1.4rem;
   line-height: 16px;
   margin-top: 2px;
   opacity: 0.7;
}

#search-btn {
   position: absolute;
   right: 0;
   top: 16px;
   padding: 2px;
   z-index: 999;
   height: 42px;
   width: 45px;
   background-color: rgba(255, 255, 255, 0.2);
   border: none;
}

#dashboard-content {
   text-align: center;
   height: 100vh;
}

#date-desc,
#location-desc {
   color: #ffffff;
   font-size: 1.6rem;
   font-weight: 500;
   line-height: 19px;
   margin-bottom: 15px;
}

#date-desc>img {
   top: -3px;
   position: relative;
   margin-right: 10px;
}

#location-desc>img {
   top: -3px;
   position: relative;
   margin-left: 5px;
   margin-right: 15px;
}

#location-detail {
   opacity: 0.7;
   color: #ffffff;
   font-size: 1.4rem;
   line-height: 20px;
   margin-left: 35px;
}

.centered {
   position: fixed;
   top: 45%;
   left: 50%;
   transform: translate(-50%, -50%);
}

.max-desc {
   width: 80px;
   float: left;
   margin-right: 28px;
}

.temp-max-min {
   margin-top: 40px
}

#dashboard-content {
   background-color: #F7F7F7;
}

.custom-card {
   background-color: #FFFFFF !important;
   border: 0 !important;
   margin-top: 16px !important;
   margin-bottom: 20px !important;
}

.custom-content-card {
   background-color: #FFFFFF !important;
   border: 0 !important;
   margin-top: 16px !important;
   margin-bottom: 0px !important;
}

.header-card {
   height: 50vh;
}

.content-card {
   height: 43vh;
}

.card-divider {
   margin-top: 0;
}

.content-header {
   color: #8786A4;
   font-size: 1.4rem;
   line-height: 16px;
   font-weight: 500;
   padding: 15px 10px 5px 15px;
}

.highlights-item {
   min-height: 37vh;
   max-height: 38vh;
   background-color: #FFFFFF;
}

.card-heading {
   color: rgb(33, 34, 68);
   font-size: 1.8rem;
   font-weight: 500;
   line-height: 21px;
   text-align: center;
}

.card-sub-heading {
   color: #73748C;
   font-size: 1.6rem;
   line-height: 19px;
}

.card-value {
   color: #000000;
   font-size: 1.8rem;
   line-height: 21px;
}

span text {
   font-weight: 500 !important;
}

hr {
   padding-top: 1.5px;
   padding-bottom: 1px;
   margin-bottom: 0;
   margin-top: 0;
   line-height: 0.5px;
}

@media only screen and (min-width: 768px) {
   #sidebar {
       height: 100vh;
   }

   #info {
       position: fixed;
       bottom: 50px;
       width: 100%;
       padding-left: 15px;
   }

   .wrapper-right {
       margin-top: 80px;
   }
}

@media only screen and (min-width:1440px) {
   #sidebar {
       width: 350px;
       max-width: 350px;
       flex: auto;
   }

   #dashboard-content {
       width: calc(100% &mdash; 350px);
       max-width: calc(100% &mdash; 350px);
       flex: auto;
   }
}
</code></pre>
</div>

#### src/assets/

In this directory, download and save the `.svg` files mentioned below:

- [`calendar.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/calendar.svg)
- [`location.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/location.svg)
- [`search.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/search.svg)
- [`winddirection.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/winddirection.svg)
- [`windspeed.svg`](https://github.com/smashingmagazine/modified_weather_dashboard/blob/master/src/assets/windspeed.svg)

#### src/components/Content.vue

This is what we call a “dumb component” (i.e. a placeholder) that is there just to maintain the hierarchy, and essentially passes on data to its child components. 

Remember that there is no technical bar for writing all our code in the `App.vue` file, but we take the approach of splitting up the code by nesting the components for two reasons:

- To write clean code, which aids readability and maintainability;
- To replicate the same structure that we will see on screen, i.e., the hierarchy.  

Before we nest the component defined in `Content.vue` within the root component `App.vue`, let’s write some toy (but educational) code for `Content.vue`:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;This child components of Content.vue are:&lt;/p&gt;
    &lt;ul&gt;
      &lt;li v-for="child in childComponents"&gt;{{ child }}&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  data () {
    return {
      childComponents: ['TempVarChart.vue', 'Highlights.vue']
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>
</div>

In the code, carefully observe and understand the following:

- Within the `<script>` tag (where we obviously write some JavaScript code), we define an object that is exported (made available to other files) by default. This object contains a function `data()`, that returns an array object called `childComponents`, with its elements being names of the component files that should be nested further.
- Within the `<template>` tag (where we write some HTML template), the thing of interest is the `<ul>`. 
	- Within the unordered list, each list item should be names of the intended child components, as defined in the array object `childComponents`. Moreover, the list should automatically extend till the last element of the array. Seems like we should write a `for`-loop, isn’t it? We do that by using the `v-for` directive provided by Vue.js. The `v-for` directive:
		- Acts as an attribute of the `<li>` tag, iterates through the array, renders the names of the child components where the iterator is mentioned within the `{{ }}` brackets (where we write the text for the list items).

The code and the explanation above forms the basis of your subsequent understanding of how the script and the template are interrelated, and how we can use the directives provided by Vue.js. 

We have learnt quite a lot, but even after all these, we have one thing left to learn about seamlessly connecting components in hierarchy &mdash; passing data down from the parent component to its children. For now, we need to learn how to pass some data from `src/App.vue` to `src/components/Content.vue`, so that we can use the same techniques for the rest of the component nesting in this project.

Data trickling down from the parent to the child components might sound simple, but the devil is in the details! As briefly explained below, there are multiple steps involved in making it work:

- **Defining and the data**  
For now, we want some static data to play with &mdash; an object containing hard-coded values about different aspects of weather will just be fine! We create an object called `weather_data` and return it from the `data()` function of `App.vue`. The `weather_data` object is given in the snippet below:

<pre><code class="language-javascript">weather_data: {
        location: "California",
        temperature: {
          current: "35 C",
        },
        highlights: {
          uvindex: "3",
          windstatus: {
            speed: "20 km/h",
            direction: "N-E",
          },
          visibility: "12 km",
        },
      },
</code></pre>

- **Passing the data from the parent**  
To pass the data, we need a destination where we want to send the data! In this case, the destination is the `Content.vue` component, and the way to implement it is to: 
	- Assign the `weather_data` object to a *custom attribute* of the `<Content>` tag
	- Bind the attribute with the data using the `v-bind`: directive provided by Vue.js, which makes the attribute value dynamic (responsive to changes made in the original data).

	<pre><code class="language-javascript">&lt;Content v-bind:weather_data="weather_data"&gt;&lt;/Content&gt;
	</code></pre>

Defining and passing the data is handled at the source side of the handshake, which in our case is the `App.vue` file.

The code for the `App.vue` file, at its current status, is given below:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;p&gt;This component’s code is in {{ filename }}&lt;/p&gt;
    &lt;Content v-bind:weather_data="weather_data"&gt;&lt;/Content&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import Content from './components/Content.vue'

export default {
  name: 'app',
  components: {
    'Content': Content
  },
  data () {
    return {
      filename: 'App.vue',
      weather_data: {
        location: "California",
        temperature: {
          current: "35 C",
        },
        highlights: {
          uvindex: "3",
          windstatus: {
            speed: "20 km/h",
            direction: "N-E",
          },
          visibility: "12 km",
        },
      },
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c7c18e0-caba-4cb0-b3c3-79e5ee34a62f/interactive-weather-dashboard-image6.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c7c18e0-caba-4cb0-b3c3-79e5ee34a62f/interactive-weather-dashboard-image6.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c7c18e0-caba-4cb0-b3c3-79e5ee34a62f/interactive-weather-dashboard-image6.png'>Large preview</a>)" alt="A screenshot of the browser with the message “This component’s code is in App.vue. This child components of Content.vue are: TempVarChart.vue, Highlights.vue”" >}}

With the data defined and passed from the source (parent component), it is now the child’s responsibility to receive the data and render it appropriately, as explained in the next two steps.

- **Receiving the data by the child**  
The child component, in this case `Content.vue`, must receive the `weather_data` object send to it by the parent component `App.vue`. Vue.js provides a mechanism to do so &mdash; all you need is an array object called [`props`](https://vuejs.org/v2/guide/components-props.html), defined in the default object exported by `Content.vue`. Each element of the array `props` is a  name of the data objects it wants to receive from its parent. For now, the only data object that it is supposed to receive is `weather_data` from App.vue. Thus, the `props` array looks like:

<pre><code class="language-javascript">&lt;template&gt;
  // HTML template code here
&lt;/template&gt;

&lt;script&gt;
export default {
  props: ["weather_data"],
  data () {
    return {
      // data here
    }
  },
}
&lt;/script&gt;

&lt;style&gt;
  // component specific CSS here
&lt;/style&gt;
</code></pre>

- **Rendering the data in the page**  
Now that we have ensured receiving the data, the last task we need to complete is to render the data. For this example, we will directly dump the received data on the web page, just to illustrate the technique. However, in real applications (like the one we are about to build), data normally goes through lots of processing, and only the relevant parts of it are displayed in ways that suits the purpose. For example, in this project we will eventually get raw data from the weather API, clean and format it, feed the data to the data structures necessary for the charts, and then visualize it. Anyway, to display the raw data dump, we will just use the `{{ }}` brackets that Vue understands, as shown in the snippet below:

<pre><code class="language-html">&lt;template&gt;
  &lt;div id="pagecontent"&gt;
    // other template code here
    {{ weather_data }}
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>

It’s now time to assimilate all the bits and pieces. The code for `Content.vue` &mdash; at its current status &mdash; is given below:

<div class="break-out">

 <pre><code class="language-html">&lt;template&gt;
  &lt;div id="pagecontent"&gt;
    &lt;p&gt;This child components of Content.vue are:&lt;/p&gt;
    &lt;ul&gt;
      &lt;li v-for="child in childComponents"&gt;{{ child }}&lt;/li&gt;
    &lt;/ul&gt;
    {{ weather_data }}
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  props: ["weather_data"],
  data () {
    return {
      childComponents: ['TempVarChart.vue', 'Highlights.vue']
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;
#pagecontent {
  border: 1px solid black;
  padding: 2px;
}
&lt;/style&gt;
</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec620211-f991-4ce3-9731-710ba32fa3b4/interactive-weather-dashboard-image9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec620211-f991-4ce3-9731-710ba32fa3b4/interactive-weather-dashboard-image9.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec620211-f991-4ce3-9731-710ba32fa3b4/interactive-weather-dashboard-image9.png'>Large preview</a>)" alt="A screenshot of the browser with the result of the code provided" >}}

After making the changes discussed above, refresh the webpage on the browser and see how it looks. Take a moment to appreciate the complexity that Vue handles &mdash; if you modify the `weather_data` object in `App.vue`, it gets silently conveyed to `Content.vue`, and eventually to the browser displaying the webpage! Try by changing the value for the key location.

Although we have learned about props and data binding using static data, we will be using dynamic data collected using web APIs in the application, and will *change the code accordingly*.

### Summary

Before we move on to the rest of the `.vue` files, let’s summarize what we have learnt while we wrote the code for `App.vue` and `components/Content.vue`:

- The `App.vue` file is what we call the root component &mdash; the one that sits at the top of the component hierarchy. The rest of the `.vue` files represents components that are its direct child, grandchild, and so on.
- The `Content.vue` file is a dummy component &mdash; its responsibility is to pass on the data to levels below and maintain the structural hierarchy, so that our code remains consistent with the philosophy “*what we see is what we implement*”. 
- The parent-child relationship of component does not happen out of thin air &mdash; you must *register a component* (either globally or locally, depending on the intended usage of the component), and then *nest* it using custom HTML tags (whose spellings are the exact same as that of the names with which the components has been registered).
- Once registered and nested, data is passed on from parent to child components, and the flow is *never reverse* (bad things will happen if the project architecture allows backflow). The parent component is the relative source of the data, and it passes down relevant data to its children using the `v-bind` directive for the attributes of the custom HTML elements. The child receives the data intended for it using props, and then decides on its own what to do with the data.

For the rest of the components, we will not indulge in detailed explanation &mdash; we will just write the code based on the learnings from the above summary. The code will be self-evident, and if you get confused about the hierarchy, refer to the diagram below: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d907827c-a9e0-4abc-a891-274cc701965f/interactive-weather-dashboard-image8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d907827c-a9e0-4abc-a891-274cc701965f/interactive-weather-dashboard-image8.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d907827c-a9e0-4abc-a891-274cc701965f/interactive-weather-dashboard-image8.png'>Large preview</a>)" alt="A diagram explaining the hierarchy of the code" >}}

The diagram says that `TempVarChart.vue` and `Highlights.vue` are the direct child of `Content.vue`. Thus, it might be a good idea to prepare `Content.vue` for sending data to those components, which we do using the code below:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="pagecontent"&gt;
    &lt;p&gt;This child components of Content.vue are:&lt;/p&gt;
    &lt;ul&gt;
      &lt;li v-for="child in childComponents"&gt;{{ child }}&lt;/li&gt;
    &lt;/ul&gt;
    {{ weather_data }}
    &lt;temp-var-chart :tempVar="tempVar"&gt;&lt;/temp-var-chart&gt;
    &lt;today-highlights :highlights="highlights"&gt;&lt;/today-highlights&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import TempVarChart from './TempVarChart.vue'
import Highlights from './Highlights.vue'

export default {
  props: ["weather_data"],
  components: {
    'temp-var-chart': TempVarChart,
    'today-highlights': Highlights
  },
  data () {
    return {
      childComponents: ['TempVarChart.vue', 'Highlights.vue'],
      tempVar: this.weather_data.temperature,
      highlights: this.weather_data.highlights,
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>
</div>

Once you save this code, you will get errors &mdash; don’t worry, it is expected. It will be fixed once you have the rest of the component files ready. If it bothers you not to be able to see the output, comment out the lines containing the custom element tags `<temp-var-chart>` and `<today-highlights>`.

For this section, this is the final code of `Content.vue`. For the rest of this section, *we will reference to this code*, and not the previous ones that we wrote for learning.

#### src/components/TempVarChart.vue

With its parent component `Content.vue` passing on the data, `TempVarChart.vue` must be set up to receive and render the data, as shown in the code below:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="tempvarchart"&gt;
    &lt;p&gt;Temperature Information:&lt;/p&gt;
    {{ tempVar }}
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["tempVar"],
  data () {
    return {

    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

#### src/components/Highlights.vue

This component will also receive data from `App.vue` &mdash; its parent component. After that, it should be linked with its child components, and relevant data should be passed on to them.

Let’s first see the code for receiving data from the parent:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="highlights"&gt;
    &lt;p&gt;Weather Highlights:&lt;/p&gt;
    {{ highlights }}
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["highlights"],
  data () {
    return {

    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

At this point, the web page looks like the image below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8418772-369a-43ba-a5b5-c781f4fcd697/interactive-weather-dashboard-image10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8418772-369a-43ba-a5b5-c781f4fcd697/interactive-weather-dashboard-image10.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8418772-369a-43ba-a5b5-c781f4fcd697/interactive-weather-dashboard-image10.png'>Large preview</a>)" alt="Result of the code displayed in the browser" >}}

Now we need to modify the code of `Highlights.vue` to register and nest its child components, followed by passing the data to children. The code for it is as follows:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="highlights"&gt;
    &lt;p&gt;Weather Highlights:&lt;/p&gt;
    {{ highlights }}
    &lt;uv-index :highlights="highlights"&gt;&lt;/uv-index&gt;
    &lt;visibility :highlights="highlights"&gt;&lt;/visibility&gt;
    &lt;wind-status :highlights="highlights"&gt;&lt;/wind-status&gt;  
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import UVIndex from './UVIndex.vue';
import Visibility from './Visibility.vue';
import WindStatus from './WindStatus.vue';

export default {
  props: ["highlights"],
  components: {
    'uv-index': UVIndex,
    'visibility': Visibility,
    'wind-status': WindStatus,
  },  
  data () {
    return {

    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

Once you save the code and see the web page, you are *expected to see errors* in the Developer Console tool provided by the browser; they appear because although `Highlights.vue` is sending data, nobody is receiving them. We are yet to write the code for the *children* of `Highlights.vue`.

Observe that we have not done much of the data processing, i.e, we have not extracted the individual factors of weather data that goes under the Highlights section of the dashboard. We could have done that in the `data()` function, but we preferred to keep `Highlights.vue` a dumb component that just passes on the entire data dump it receives to each of the children, who then own their own extracts what is necessary for them. However, we encourage you to try out extracting data in the `Highlights.vue`, and send relevant data down to each child component &mdash; it’s a good practice exercise nonetheless!

#### src/components/UVIndex.vue

The code for this component receives the data dump of highlights from `Highlights.vue`, extracts the data for UV Index, and renders it on the page.

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="uvindex"&gt;
    &lt;p&gt;UV Index: {{ uvindex }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["highlights"],
  data () {
    return {
      uvindex: this.highlights.uvindex
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

#### src/components/Visibility.vue

The code for this component receives the data dump of highlights from `Highlights.vue`, extracts the data for Visibility, and renders it on the page.

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="visibility"&gt;
    &lt;p&gt;Visibility: {{ visibility }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["highlights"],
  data () {
    return {
      visibility: this.highlights.visibility,
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

#### src/components/WindStatus.vue

The code for this component receives the data dump of highlights from `Highlights.vue`, extracts the data for Wind Status (speed and direction), and renders it on the page.

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="windstatus"&gt;
    &lt;p&gt;Wind Status:&lt;/p&gt;
    &lt;p&gt;Speed &mdash; {{ speed }}; Direction &mdash; {{ direction }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["highlights"],
  data () {
    return {
      speed: this.highlights.windstatus.speed,
      direction: this.highlights.windstatus.direction
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>
</div>

After adding the code for all the components, take a look at the web page on the browser.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8418772-369a-43ba-a5b5-c781f4fcd697/interactive-weather-dashboard-image10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8418772-369a-43ba-a5b5-c781f4fcd697/interactive-weather-dashboard-image10.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8418772-369a-43ba-a5b5-c781f4fcd697/interactive-weather-dashboard-image10.png'>Large preview</a>)" alt="Result of the code displayed in the browser" >}}

Not to dishearten, but all these toiling was just to link the components in hierarchy, and test out whether data flow is happening between them or not! In the next section, we will *throw away most of the code we have written so far*, and add a lot more pertaining to the actual project. However, we will certainly retain the structure and nesting of the components; the learnings from this section will allow us to build a decent dashboard with Vue.js.

## 4. Data Acquisition And Processing

Remember the `weather_data` object in `App.vue`? It had some hard-coded data that we used to test whether all the components are working correctly, and also to help you learn some basic aspects of Vue application without getting bogged down in the details of real-world data. However, it’s now time that we shed our shell, and step out into the real world, where data from the API will dominate most of our code.

### Preparing Child Components To Receive And Process Real Data

In this section, you will get code dump for all the components except `App.vue`. The code will handle receiving real data from `App.vue` (unlike the code we wrote in the previous section to receive and render dummy data).

We strongly encourage to read the code of each component carefully, so that you form an idea of what data each of those components are expecting, and will eventually use in visualization.

Some of the code, and the overall structure, will be similar to the ones you have seen in the previous structure &mdash; so you will not face something drastically different. However, the devil is in the details! So examine the code carefully, and when you have understood them reasonably well, copy the code to the respective component files in your project.

**Note**: *All the components in this section are in the `src/components/` directory. So each time, the path will not be mentioned &mdash; only the `.vue` file name will be mentioned to identify the component.*

#### Content.vue

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
 &lt;div style="position: relative;"&gt;
     &lt;temp-var-chart :tempVar="tempVar"&gt;&lt;/temp-var-chart&gt;
     &lt;today-highlights :highlights="highlights"&gt;&lt;/today-highlights&gt;
 &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import TempVarChart from './TempVarChart.vue';
import Highlights from './Highlights.vue';

export default {
 props: ['highlights', 'tempVar'],
 components: {
   'temp-var-chart': TempVarChart,
   'today-highlights': Highlights
 },
}
&lt;/script&gt;
</code></pre>
</div>

The following changes have been made from the previous code:

- In the `<template>`, text and data within `{{ }}` has been removed, since we are now just receiving data and passing down to the children, with no rendering specific this component.
- In the `export default {}`:
	- The `props` have been changed to match the data objects that will be send by the parent: `App.vue`. The reason for changing the props is that `App.vue` itself will display some of the data it acquires from the weather API and other online resources, based on the search query of the user, and pass on the rest of the data. In the dummy code we wrote earlier, `App.vue` was passing on the entire dummy data dump, without any discrimination, and the props of `Content.vue` was set up accordingly.
	- The data() function now returns nothing, as we are not doing any data manipulation in this component.

#### TempVarChart.vue

This component is supposed to receive detailed temperature projections for the rest of the current day, and eventually display them using FusionCharts. But for the time being, we will display them only as text on the webpage.

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    {{ tempVar.tempToday }}    
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  props: ["tempVar"],
  components: {},
  data() {
    return {

    };
  },
  methods: {

  },

};
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

#### Highlights.vue

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;uv-index :highlights="highlights"&gt;&lt;/uv-index&gt;
    &lt;visibility :highlights="highlights"&gt;&lt;/visibility&gt;
    &lt;wind-status :highlights="highlights"&gt;&lt;/wind-status&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import UVIndex from './UVIndex.vue';
import Visibility from './Visibility.vue';
import WindStatus from './WindStatus.vue';

export default {
  props: ["highlights"],
  components: {
    'uv-index': UVIndex,
    'visibility': Visibility,
    'wind-status': WindStatus,
  },
  data () {
    return {

    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

The changes made from the previous code are:

- In the `<template>`, the text and the data within `{{ }}` has been removed, because this is a dumb component, just like `Content.vue`, whose only job is to pass on the data to children while maintaining the structural hierarchy. Remember that dumb components like `Highlights.vue` and `Content.vue` exists to maintain the parity between the visual structure of the dashboard, and the code we write.

#### UVIndex.vue

The changes made to the previous code are as follows:

- In the `<template>` and `<style>`, the `div id` has been changed to `uvIndex`, which is more readable. 
- In the `export default {}`, the `data()` function now returns a string object `uvIndex`, whose value is extracted from the highlights object received by the component using `props`. This `uvIndex` is now temporarily used to display the value as text within the `<template>`. Later on, we will plug in this value to the data structure suitable for rendering a chart.

#### Visibility.vue

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;Visibility: {{ visibility }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["highlights"],
  data () {
    return {
      visibility: this.highlights.visibility.toString()
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>

The only change made in this file (with respect to its previous code) is that the definition of the `visibility` object returned by the `data()` function now contains `toString()` at its end, since the value received from the parent will be a floating point number, which needs to be converted into string.

#### WindStatus.vue

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;Wind Speed &mdash; {{ windSpeed }}&lt;/p&gt;
    &lt;p&gt;Wind Direction &mdash; {{ derivedWindDirection }}, or {{ windDirection }} degree clockwise with respect to true N as 0 degree.&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;

export default {
  props: ["highlights"],
  data () {
    return {
      windSpeed: this.highlights.windStatus.windSpeed,
      derivedWindDirection: this.highlights.windStatus.derivedWindDirection,
      windDirection: this.highlights.windStatus.windDirection
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>
</div>

The changes made to the previous code are as follows:

- Throughout the file, `windstatus` has been renamed as `windStatus`, to promote readability and also to be in sync with the the highlights object that `App.vue` provides with actual data. 
- Similar naming changes have been made for the speed and direction &mdash; the new ones are `windSpeed` and `windDirection`.
- A new object `derivedWindDirection` has come into play (also provided by `App.vue` in the highlights bundle).

For now, the received data is rendered as text; later, it will be plugged in to the data structure necessary for visualization.

### Testing With Dummy Data 

Resorting to dummy data repeatedly might be a bit frustrating for you, but there are some good reasons behind it:

- We have made a lot of changes to the code of each component, and it’s a good idea to test whether those changes are breaking the code. In other words, we should check that whether the data flow is intact, now that we are about to move to more complex parts of the project.
- The real data from the online weather API will need lot of massaging, and it might be overwhelming for you to juggle between the code for data acquisition and processing, and the code for smooth data flow down the components. The idea is to keep the quantum of complexity under control, so that we have a better understanding of the errors we might face.

In this section, what we do is essentially hardcode some json data in the `App.vue`, which will obviously be replaced with live data in the near future. There are a lot of similarity between the dummy json structure, and the json structure we will use for the actual data. So it also provides you a rough idea of what to expect from the real data, once we encounter it.

However, we admit that this is far from the ideal approach one might adopt while building such a project from scratch. In the real world, you will often start with the real data source, play around with it a bit to understand what can and should be done to tame it, and then think about the appropriate json data structure to capture the relevant information. We intentionally shielded you from all those dirty work, since it takes you farther from the objective &mdash; learning how to use Vue.js and FusionCharts to build a dashboard.

Let’s now jump into the new code for App.vue:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;dashboard-content :highlights="highlights" :tempVar="tempVar"&gt;&lt;/dashboard-content&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import Content from './components/Content.vue'

export default {
  name: 'app',
  components: {
    'dashboard-content': Content
  },
  data () {
    return {
      tempVar: {
        tempToday: [
          {hour: '11.00 AM', temp: '35'},
          {hour: '12.00 PM', temp: '36'},
          {hour: '1.00 PM', temp: '37'},
          {hour: '2.00 PM', temp: '38'},
          {hour: '3.00 PM', temp: '36'},
          {hour: '4.00 PM', temp: '35'},
        ],
      },
      highlights: {
        uvIndex: 4,
        visibility: 10,
        windStatus: {
          windSpeed: '30 km/h',
          windDirection: '30',
          derivedWindDirection: 'NNE',
        },
      },
    }
  },
  methods: {

  },
  computed: {

  },
}
&lt;/script&gt;

&lt;style&gt;

&lt;/style&gt;
</code></pre>
</div>

The changes made to the code with respect to its previous version are as follows:

- The name of the child component has been changed to dashboard-content, and accordingly the custom HTML element in the `<template>` has been revised. Note that now we have two attributes &mdash; `highlights` and `tempVar` &mdash; instead of a single attribute that we used earlier with the custom element. Accordingly, the data associated with those attributes have also changed. What’s interesting here is that we can use the `v-bind:` directive, or its shorthand `:` (as we have done here), with multiple attributes of a custom HTML element!
- The `data()` function now returns the `filename` object (that existed earlier), along with two new objects (instead of the old `weather_data`): `tempVar` and `highlights`. The structure of the json is appropriate for the code we have written in the child components, so that they can extract the data pieces they need from the dumps. The structures are quite self-explanatory, and you can expect them to be quite similar when we deal with live data. However, the significant change that you will encounter is the absence of hardcoding (obvious, isn’t it) &mdash; we will leave the values blank as the default state, and write code to dynamically update them based on the values we will receive from the weather API.

You have written a lot of code in this section, without seeing the actual output. Before you proceed further, take a look at the browser (restart the server with `npm run dev`, if necessary), and bask in the glory of your achievement. The web page that you should see at this point looks like the image below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32be6750-69fb-4cad-8f0c-8d07ab08d107/interactive-weather-dashboard-image11.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32be6750-69fb-4cad-8f0c-8d07ab08d107/interactive-weather-dashboard-image11.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32be6750-69fb-4cad-8f0c-8d07ab08d107/interactive-weather-dashboard-image11.png'>Large preview</a>)" alt="Result of the code displayed in the browser" >}}

### Code For Data Acquisition And Processing

This section is going to be the meat of the project, with all the code to be written in `App.vue` for the following:

- Location input from the user &mdash; an input box and a call-to-action button is sufficient;
- Utility functions for various tasks; these functions will be called later in various parts of the component code;
- Getting detailed geolocation data from Google Maps API for JavaScript;
- Getting detailed weather data from the Dark Sky API;
- Formatting and processing the geolocation and weather data, which will be passed on to the child components.

The subsections that follows illustrates how we can implement the tasks laid out for us in the above points. With some exceptions, most of them will follow the sequence.

### Input From The User

It’s quite obvious that the action starts when the user provides the name of the place for which the weather data needs to be displayed. For this to happen, we need to implement the following:

- An input box for entering the location;
- A submit button that tells our application that the user has entered the location and it’s time to do the rest. We will also implement the behavior when processing starts upon hitting <kbd>Enter</kbd>.

The code we show below will be restricted to the HTML template part of `App.vue`. We will just mention the name of the method associated with the click events, and define them later in the methods object of the &lt;script&gt; in App.vue.

<div class="break-out">

 <pre><code class="language-javascript">&lt;div id="search"&gt;
           &lt;input
             id="location-input"
             type="text"
             ref="input"
             placeholder="Location?"
             @keyup.enter="organizeAllDetails"
           &gt;
           &lt;button id="search-btn" @click="organizeAllDetails"&gt;
             &lt;img src="./assets/Search.svg" width="24" height="24"&gt;
           &lt;/button&gt;
&lt;/div&gt;
</code></pre>
</div>

Placing the above snippet in the right place is trivial &mdash; we leave it to you. However, the interesting parts of the snippet are:

- `@keyup.enter="organizeAllDetails"`
- `@click="organizeAllDetails"`

As you know from the earlier sections, `@` is Vue’s shorthand for the directive `v-on`:, which is associated with some event. The new thing is "`organizeAllDetails`" &mdash; it’s nothing but the method that will fire once the events (pressing <kbd>Enter</kbd> or clicking the button) happens. We are yet to define method, and the puzzle will be complete by the end of this section.

### Text Information Display Controlled By App.vue

Once the user input triggers the action and lots of data is acquired from the APIs, we encounter the inevitable question &mdash; “What to do with all these data?”. Obviously some data massaging is required, but that does not answer our question fully! We need to decide what’s the end use of the data, or more directly, which are the entities that receives different chunks of the acquired and processed data?

The child components of `App.vue`, based on their hierarchy and purpose, are the frontline contenders for the bulk of the data. However, we will also have some data that does not belong to any of those child components, yet are quite informative and makes the dashboard complete. We can make good use of them if we display them as text information directly controlled by `App.vue`, while the rest of the data are passed on to the child for getting displayed as pretty charts ultimately.

With this context in mind, let’s focus on the code for setting the stage of using text data. It’s simple HTML template at this point, on which the data will eventually come and sit. 

<div class="break-out">

 <pre><code class="language-html">&lt;div id="info"&gt;
  &lt;div class="wrapper-left"&gt;
    &lt;div id="current-weather"&gt;
      {{ currentWeather.temp }}
      &lt;span&gt;°C&lt;/span&gt;
    &lt;/div&gt;
    &lt;div id="weather-desc"&gt;{{ currentWeather.summary }}&lt;/div&gt;
    &lt;div class="temp-max-min"&gt;
      &lt;div class="max-desc"&gt;
        &lt;div id="max-detail"&gt;
          &lt;i&gt;▲&lt;/i&gt;
          {{ currentWeather.todayHighLow.todayTempHigh }}
          &lt;span&gt;°C&lt;/span&gt;
        &lt;/div&gt;
        &lt;div id="max-summary"&gt;at {{ currentWeather.todayHighLow.todayTempHighTime }}&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="min-desc"&gt;
        &lt;div id="min-detail"&gt;
          &lt;i&gt;▼&lt;/i&gt;
          {{ currentWeather.todayHighLow.todayTempLow }}
          &lt;span&gt;°C&lt;/span&gt;
        &lt;/div&gt;
        &lt;div id="min-summary"&gt;at {{ currentWeather.todayHighLow.todayTempLowTime }}&lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="wrapper-right"&gt;
    &lt;div class="date-time-info"&gt;
      &lt;div id="date-desc"&gt;
        &lt;img src="./assets/calendar.svg" width="20" height="20"&gt;
        {{ currentWeather.time }}
      &lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="location-info"&gt;
      &lt;div id="location-desc"&gt;
        &lt;img
          src="./assets/location.svg"
          width="10.83"
          height="15.83"
          style="opacity: 0.9;"
        &gt;
        {{ currentWeather.full_location }}
        &lt;div id="location-detail" class="mt-1"&gt;
          Lat: {{ currentWeather.formatted_lat }}
          &lt;br&gt;
          Long: {{ currentWeather.formatted_long }}
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>
</div>

In the above snippet, you should understand the following:

- The stuff inside `{{ }}` &mdash; they are Vue’s way of inserting dynamic data in the HTML template, before it renders in the browser. You have encountered them before, and there is nothing new or surprising. Just keep in mind that these data objects stems from the `data()` method in the `export default()` object of `App.vue`. They have default values that we will set according to our requirements, and then write certain methods to populate the objects with real API data.

Don’t worry for not seeing the changes on the browser &mdash; the data is not defined yet, and it’s natural for Vue to not render things that it does not know. However, **once the data is set** (and for now, you can even check by hard-coding the data), the text data will be controlled by `App.vue`.	

### The `data()` Method

The `data()` method is a special construct in the `.vue` files &mdash; it contains and returns data objects that are so crucial for the application. Recollect the generic structure of the `<script>` part in any `.vue` file &mdash; it roughly contains the following:

<div class="break-out">

 <pre><code class="language-javascript">&lt;script&gt;
// import statements here

export default {
    // name, components, props, etc.

    data() {
        return {
            // the data that is so crucial for the application is defined here.
            // the data objects will have certain default values chosen by us.
            // The methods that we define below will manipulate the data.
            // Since the data is bounded to various attributes and directives, they
            // will update as and when the values of the data objects change.
        }
    },

    methods: {
        // methods (objects whose values are functions) here.
        // bulk of dynamic stuff (the black magic part) is controlled from here.
    },

    computed: {
        // computed properties here
    },

    // other objects, as necessary

}
&lt;/script&gt;
</code></pre>
</div>

So far, you have encountered the names of some of the data objects, but are a lot more. Most of them are relevant for the child components, each of which handles a different aspect of the weather information dump. Given below is the entire `data()` method that we will need for this project &mdash; you will have a fair idea about what data we are expecting from the APIs, and how we are disseminating the data, based on the nomenclature of the objects.

<div class="break-out">

 <pre><code class="language-javascript">data() {
   return {
     weatherDetails: false,
     location: '', // raw location from input
     lat: '', // raw latitude from google maps api response
     long: '', // raw longitude from google maps api response
     completeWeatherApi: '', // weather api string with lat and long
     rawWeatherData: '', // raw response from weather api
     currentWeather: {
       full_location: '', // for full address
       formatted_lat: '', // for N/S
       formatted_long: '', // for E/W
       time: '',
       temp: '',
       todayHighLow: {
         todayTempHigh: '',
         todayTempHighTime: '',
         todayTempLow: '',
         todayTempLowTime: ''
       },
       summary: '',
       possibility: ''
     },
     tempVar: {
       tempToday: [
         // gets added dynamically by this.getSetHourlyTempInfoToday()
       ],
     },
     highlights: {
       uvIndex: '',
       visibility: '',
       windStatus: {
         windSpeed: '',
         windDirection: '',
         derivedWindDirection: ''
       },
     }
   };
 },
</code></pre>
</div>

As you can see, in most cases the default value is empty, because that will suffice at this point. Methods will be written for manipulating the data and filling it up with appropriate values, before it is rendered or passed on to the child components.

#### Methods in App.vue

For `.vue` files, the methods are generally written as values of keys nested in the `methods { }` object. Their primary role is to manipulate the data objects of the component. We will write the methods in `App.vue` keeping the same philosophy in mind. However, based on their purpose, we can categorize the methods of `App.vue` into the following:

- Utility methods
- Action/Event oriented methods
- Data acquisition methods
- Data processing methods
- High level glue methods

It’s important that you understand this &mdash; we are presenting the methods to you on a platter because we have already figured out how the APIs work, what data they give, and how we should use the data in our project. It’s not that we pulled the methods out of thin air, and wrote some arcane code to deal with the data. For the purpose of learning, it’s a good exercise to diligently read and understand the code for the methods and data. However, when faced with a new project that you have to build from scratch, you must do all the dirty work yourself, and that means experimenting a lot with the APIs &mdash; their programmatic access and their data structure, before glueing them seamlessly with the data structure that your project demands. You will not have any hand holding, and there will be frustrating moments, but that’s all part of maturing as a developer.

In the following subsections, we will explain each of the method types, and also show the implementation of the methods belonging to that category. The method names are quite self-explanatory about their purpose, and so is their implementation, which we believe you will find to be easy enough to follow. However, before that, recollect the general scheme of writing methods in `.vue` files:

<div class="break-out">

 <pre><code class="language-javascript">&lt;script&gt;
// import statements here

export default {
    // name, components, props, etc.

    data() {
        return {
            // the data that is so crucial for the application is defined here.
        }
    },

    methods: {
        // methods (objects whose values are functions) here.
        // bulk of dynamic stuff (the black magic part) is controlled from here.
        method_1: function(arg_1) {

        },
        method_2: function(arg_1, arg_2) {

        },
        method_3: function(arg_1) {

        },
        …….
    },

    computed: {
        // computed properties here
    },

    // other objects, as necessary

}
&lt;/script&gt;
</code></pre>
</div>

### Utility Methods

The utility methods, as the name suggests, are methods written primarily for the purpose of modularizing repetitive code used for fringe tasks. They are called by other methods when necessary. Given below are the utility methods for `App.vue`:

<div class="break-out">

 <pre><code class="language-javascript">convertToTitleCase: function(str) {
     str = str.toLowerCase().split(' ');
     for (var i = 0; i < str.length; i++) {
       str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1);
     }
     return str.join(' ');
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">// To format the “possibility” (of weather) string obtained from the weather API
formatPossibility: function(str) {
     str = str.toLowerCase().split('-');
     for (var i = 0; i < str.length; i++) {
       str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1);
     }
     return str.join(' ');
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">// To convert Unix timestamps according to our convenience
unixToHuman: function(timezone, timestamp) {
     /* READ THIS BEFORE JUDGING & DEBUGGING
     For any location beyond the arctic circle and the
     antarctic circle, the goddamn weather api does not return certain
     keys/values in each of this.rawWeatherData.daily.data[some_array_index].
     Due to this, console throws up an error.
     The code is correct, the problem is with the API.
     May be later on I will add some padding to tackle missing values.
     */
     var moment = require('moment-timezone'); // for handling date & time
     var decipher = new Date(timestamp * 1000);
     var human = moment(decipher)
       .tz(timezone)
       .format('llll');
     var timeArray = human.split(' ');
     var timeNumeral = timeArray[4];
     var timeSuffix = timeArray[5];
     var justTime = timeNumeral + ' ' + timeSuffix;
     var monthDateArray = human.split(',');
     var monthDate = monthDateArray[1].trim();
     return {
       fullTime: human,
       onlyTime: justTime,
       onlyMonthDate: monthDate
     };
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">// To convert temperature from fahrenheit to celcius
fahToCel: function(tempInFahrenheit) {
     var tempInCelcius = Math.round((5 / 9) * (tempInFahrenheit &mdash; 32));
     return tempInCelcius;
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">// To convert the air pressure reading from millibar to kilopascal
milibarToKiloPascal: function(pressureInMilibar) {
     var pressureInKPA = pressureInMilibar * 0.1;
     return Math.round(pressureInKPA);
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">// To convert distance readings from miles to kilometers
mileToKilometer: function(miles) {
     var kilometer = miles * 1.60934;
     return Math.round(kilometer);
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">// To format the wind direction based on the angle
deriveWindDir: function(windDir) {
     var wind_directions_array = [
       { minVal: 0, maxVal: 30, direction: 'N' },
       { minVal: 31, maxVal: 45, direction: 'NNE' },
       { minVal: 46, maxVal: 75, direction: 'NE' },
       { minVal: 76, maxVal: 90, direction: 'ENE' },
       { minVal: 91, maxVal: 120, direction: 'E' },
       { minVal: 121, maxVal: 135, direction: 'ESE' },
       { minVal: 136, maxVal: 165, direction: 'SE' },
       { minVal: 166, maxVal: 180, direction: 'SSE' },
       { minVal: 181, maxVal: 210, direction: 'S' },
       { minVal: 211, maxVal: 225, direction: 'SSW' },
       { minVal: 226, maxVal: 255, direction: 'SW' },
       { minVal: 256, maxVal: 270, direction: 'WSW' },
       { minVal: 271, maxVal: 300, direction: 'W' },
       { minVal: 301, maxVal: 315, direction: 'WNW' },
       { minVal: 316, maxVal: 345, direction: 'NW' },
       { minVal: 346, maxVal: 360, direction: 'NNW' }
     ];
     var wind_direction = '';
     for (var i = 0; i < wind_directions_array.length; i++) {
       if (
         windDir >= wind_directions_array[i].minVal &&
         windDir <= wind_directions_array[i].maxVal
       ) {
         wind_direction = wind_directions_array[i].direction;
       }
     }
     return wind_direction;
   },
</code></pre>
</div>

Although we haven’t implemented it, you can take out the utility methods from the `.vue` file, and put it in a separate JavaScript file. All you need to do is import the `.js` file at the start of the script part in the `.vue` file, and you should be good to go. Such approach works really well and keeps the code clean, especially in big applications where you might use lots of methods that are better grouped together based on their purpose. You can apply this approach to all of the method groups listed in this article, and see the effect itself. However, we suggest you do that exercise once you have followed the course presented here, so that you have the big picture understanding of all the parts working in complete sync, and also have a working piece of software which you can refer to, once something breaks while experimenting. 

### Action/Event Oriented Methods

These methods are generally executed when we need to take an action corresponding to an event. Depending on the case, the event might be triggered from an user interaction, or programmatically. In the `App.vue` file, these methods sit below the utility methods.

<pre><code class="language-javascript">makeInputEmpty: function() {
     this.$refs.input.value = '';
   },
</code></pre>

<pre><code class="language-javascript">makeTempVarTodayEmpty: function() {
     this.tempVar.tempToday = [];
   },
</code></pre>

<pre><code class="language-javascript">detectEnterKeyPress: function() {
     var input = this.$refs.input;
     input.addEventListener('keyup', function(event) {
       event.preventDefault();
       var enterKeyCode = 13;
       if (event.keyCode === enterKeyCode) {
         this.setHitEnterKeyTrue();
       }
     });
   },
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">locationEntered: function() {
     var input = this.$refs.input;
     if (input.value === '') {
       this.location = "New York";
     } else {
       this.location = this.convertToTitleCase(input.value);
     }
     this.makeInputEmpty();
     this.makeTempVarTodayEmpty();
   },
</code></pre>
</div>

One interesting thing in some of the above code snippets is the use of `$ref`. In simple terms, it’s Vue’s way of associating the code statement containing it, to the HTML construct it is supposed to affect (for more information, read the [official guide](https://vuejs.org/v2/api/#vm-refs)). For example, the methods `makeInputEmpty()` and `detectEnterKeyPress()` affects the input box, because in the HTML of the input box we have mentioned the value of the attribute `ref` as `input`.

### Data Acquisition Methods

We are using the following two APIs in our project:

- [Google Maps Geocoder API](https://developers.google.com/maps/documentation/geocoding/intro)  
This API is for getting the coordinates of the location that the user searches. You will need an API key for yourself, which you can get by following the documentation in the given link. For now, you can use the API key used by FusionCharts, but we request you not to abuse it and get a key of your own. We refer to the JavaScript API from the index.html of this project, and we shall use the constructors provided by it for our code in the `App.vue` file.
- [The Dark Sky Weather API](https://darksky.net/dev)  
This API is for getting the weather data corresponding to the coordinates. However, we won’t be using it directly; we will wrap it within an URL that redirects through one of the FusionCharts’s server. The reason is that if you send a GET request to the API from an entirely client-end application such as ours, it results in the frustrating `CORS` error (more information [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) and [here](https://www.w3.org/TR/html5/infrastructure.html#cors-settings-attribute)).

<p class="c-pre-sidenote--left"><strong>Important Note</strong>: <em>Since we have used Google Maps and Dark Sky APIs, Both these APIs have their own API keys which we have shared with you in this article. This will help you focus on client-side developments rather than the headache of backend implementation. However, <strong>we recommend you to create your own keys</strong>, because our APIs keys will come with limits and if these limits exceed you won't be able to try the application by yourself.</em></p><p class="c-sidenote c-sidenote--right">For Google Maps, <a href="https://developers.google.com/maps/documentation/javascript/get-api-key">go to this article</a> to get your API key. For Dark Sky API, visit <a href="https://darksky.net/dev">https://darksky.net/dev</a> to create your API key and respective endpoints.</p>

With the context in mind, let’s see the implementation of the data acquisition methods for our project.

<div class="break-out">

 <pre><code class="language-javascript">getCoordinates: function() {
     this.locationEntered();
     var loc = this.location;
     var coords;
     var geocoder = new google.maps.Geocoder();
     return new Promise(function(resolve, reject) {
       geocoder.geocode({ address: loc }, function(results, status) {
         if (status == google.maps.GeocoderStatus.OK) {
           this.lat = results[0].geometry.location.lat();
           this.long = results[0].geometry.location.lng();
           this.full_location = results[0].formatted_address;
           coords = {
             lat: this.lat,
             long: this.long,
             full_location: this.full_location
           };
           resolve(coords);
         } else {
           alert("Oops! Couldn't get data for the location");
         }
       });
     });
   },
</code></pre> 
</div>

<div class="break-out">

 <pre><code class="language-javascript">/*
The coordinates that Google Maps Geocoder API returns are way too accurate
for our requirements. We need to bring it into shape before passing the coordinates on 
to the weather API. Although this is a data processing method in its own right, we can’t 
help mentioning it right now, because the data acquisition method for the weather API has dependency on the output of this method. 
*/
setFormatCoordinates: async function() {
     var coordinates = await this.getCoordinates();
     this.lat = coordinates.lat;
     this.long = coordinates.long;
     this.currentWeather.full_location = coordinates.full_location;
     // Remember to beautify lat for N/S
     if (coordinates.lat > 0) {
       this.currentWeather.formatted_lat =
         (Math.round(coordinates.lat * 10000) / 10000).toString() + '°N';
     } else if (coordinates.lat < 0) {
       this.currentWeather.formatted_lat =
         (-1 * (Math.round(coordinates.lat * 10000) / 10000)).toString() +
         '°S';
     } else {
       this.currentWeather.formatted_lat = (
         Math.round(coordinates.lat * 10000) / 10000
       ).toString();
     }
     // Remember to beautify long for N/S
     if (coordinates.long > 0) {
       this.currentWeather.formatted_long =
         (Math.round(coordinates.long * 10000) / 10000).toString() + '°E';
     } else if (coordinates.long < 0) {
       this.currentWeather.formatted_long =
         (-1 * (Math.round(coordinates.long * 10000) / 10000)).toString() +
         '°W';
     } else {
       this.currentWeather.formatted_long = (
         Math.round(coordinates.long * 10000) / 10000
       ).toString();
     }
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">/*
This method dynamically creates the the correct weather API query URL, based on the 
formatted latitude and longitude. The complete URL is then fed to the method querying for 
weather data.
Notice that the base URL used in this method (without the coordinates) points towards a 
FusionCharts server &mdash; we must redirect our GET request to the weather API through a server to avoid the CORS error.
*/
fixWeatherApi: async function() {
     await this.setFormatCoordinates();
     var weatherApi =
       'https://csm.fusioncharts.com/files/assets/wb/wb-data.php?src=darksky&lat=' +
       this.lat +
       '&long=' +
       this.long;
     this.completeWeatherApi = weatherApi;
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">fetchWeatherData: async function() {
     await this.fixWeatherApi();
     var axios = require('axios'); // for handling weather api promise
     var weatherApiResponse = await axios.get(this.completeWeatherApi);
     if (weatherApiResponse.status === 200) {
       this.rawWeatherData = weatherApiResponse.data;
     } else {
       alert('Hmm... Seems like our weather experts are busy!');
     }
   },
</code></pre>
</div>

Through these methods, we have introduced the concept of **async-await** in our code. If you have been a JavaScript developer for some time now, you must be familiar with the [callback hell](https://callbackhell.com/), which is a direct consequence of the asynchronous way JavaScript is written. ES6 allows us to bypass the cumbersome nested callbacks, and our code becomes much cleaner if we write JavaScript in a synchronous way, using the [async-await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) technique. However, there is a downside. It takes away the speed that asynchronous code gives us, especially for the portions of the code that deals with data being exchanged over the internet. Since this is not a mission-critical application with low latency requirements, and our primary aim is to learn stuff, the clean code is much more preferable over the slightly fast code.

### Data Processing Methods

Now that we have the methods that will bring the data to us, we need to prepare the ground for properly receiving and processing the data. Safety nets must be cast, and there should be no spills &mdash; data is the new gold (OK, that might be an exaggeration in our context)! Enough with the fuss, let’s get to the point.

Technically, the methods we implement in this section are aimed at getting the data out of the acquisition methods and the data objects in `App.vue`, and sometimes setting the data objects to certain values that suits the purpose. 

<pre><code class="language-javascript">getTimezone: function() {
     return this.rawWeatherData.timezone;
   },
</code></pre>

<pre><code class="language-javascript">getSetCurrentTime: function() {
     var currentTime = this.rawWeatherData.currently.time;
     var timezone = this.getTimezone();
     this.currentWeather.time = this.unixToHuman(
       timezone,
       currentTime
     ).fullTime;
   },
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">getSetSummary: function() {
     var currentSummary = this.convertToTitleCase(
       this.rawWeatherData.currently.summary
     );
     if (currentSummary.includes(' And')) {
       currentSummary = currentSummary.replace(' And', ',');
     }
     this.currentWeather.summary = currentSummary;
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">getSetPossibility: function() {
     var possible = this.formatPossibility(this.rawWeatherData.daily.icon);
     if (possible.includes(' And')) {
       possible = possible.replace(' And', ',');
     }
     this.currentWeather.possibility = possible;
   },
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript">getSetCurrentTemp: function() {
     var currentTemp = this.rawWeatherData.currently.temperature;
     this.currentWeather.temp = this.fahToCel(currentTemp);
   },
</code></pre>
</div>

<pre><code class="language-javascript">getTodayDetails: function() {
     return this.rawWeatherData.daily.data[0];
   },
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">getSetTodayTempHighLowWithTime: function() {
     var timezone = this.getTimezone();
     var todayDetails = this.getTodayDetails();
     this.currentWeather.todayHighLow.todayTempHigh = this.fahToCel(
       todayDetails.temperatureMax
     );
     this.currentWeather.todayHighLow.todayTempHighTime = this.unixToHuman(
       timezone,
       todayDetails.temperatureMaxTime
     ).onlyTime;
     this.currentWeather.todayHighLow.todayTempLow = this.fahToCel(
       todayDetails.temperatureMin
     );
     this.currentWeather.todayHighLow.todayTempLowTime = this.unixToHuman(
       timezone,
       todayDetails.temperatureMinTime
     ).onlyTime;
   },
</code></pre>
</div>

<pre><code class="language-javascript">getHourlyInfoToday: function() {
     return this.rawWeatherData.hourly.data;
   },
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">getSetHourlyTempInfoToday: function() {
     var unixTime = this.rawWeatherData.currently.time;
     var timezone = this.getTimezone();
     var todayMonthDate = this.unixToHuman(timezone, unixTime).onlyMonthDate;
     var hourlyData = this.getHourlyInfoToday();
     for (var i = 0; i < hourlyData.length; i++) {
       var hourlyTimeAllTypes = this.unixToHuman(timezone, hourlyData[i].time);
       var hourlyOnlyTime = hourlyTimeAllTypes.onlyTime;
       var hourlyMonthDate = hourlyTimeAllTypes.onlyMonthDate;
       if (todayMonthDate === hourlyMonthDate) {
         var hourlyObject = { hour: '', temp: '' };
         hourlyObject.hour = hourlyOnlyTime;
         hourlyObject.temp = this.fahToCel(hourlyData[i].temperature).toString();
         this.tempVar.tempToday.push(hourlyObject);
         /*
         Since we are using array.push(), we are just adding elements
         at the end of the array. Thus, the array is not getting emptied
         first when a new location is entered.
         to solve this problem, a method this.makeTempVarTodayEmpty()
         has been created, and called from this.locationEntered().
         */
       }
     }
     /*
     To cover the edge case where the local time is between 10 &mdash; 12 PM,
     and therefore there are only two elements in the array
     this.tempVar.tempToday. We need to add the points for minimum temperature
     and maximum temperature so that the chart gets generated with atleast four points.
     */
     if (this.tempVar.tempToday.length <= 2) {
       var minTempObject = {
         hour: this.currentWeather.todayHighLow.todayTempHighTime,
         temp: this.currentWeather.todayHighLow.todayTempHigh
       };
       var maxTempObject = {
         hour: this.currentWeather.todayHighLow.todayTempLowTime,
         temp: this.currentWeather.todayHighLow.todayTempLow
       };
       /*
       Typically, lowest temp are at dawn,
       highest temp is around mid day.
       Thus we can safely arrange like min, max, temp after 10 PM.
       */
       // array.unshift() adds stuff at the beginning of the array.
       // the order will be: min, max, 10 PM, 11 PM.
       this.tempVar.tempToday.unshift(maxTempObject, minTempObject);
     }
   },
</code></pre>
</div>

<pre><code class="language-javascript">getSetUVIndex: function() {
     var uvIndex = this.rawWeatherData.currently.uvIndex;
     this.highlights.uvIndex = uvIndex;
   },
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">getSetVisibility: function() {
     var visibilityInMiles = this.rawWeatherData.currently.visibility;
     this.highlights.visibility = this.mileToKilometer(visibilityInMiles);
   },
</code></pre> 
</div>

<div class="break-out">

 <pre><code class="language-javascript">getSetWindStatus: function() {
     var windSpeedInMiles = this.rawWeatherData.currently.windSpeed;
     this.highlights.windStatus.windSpeed = this.mileToKilometer(
       windSpeedInMiles
     );
     var absoluteWindDir = this.rawWeatherData.currently.windBearing;
     this.highlights.windStatus.windDirection = absoluteWindDir;
     this.highlights.windStatus.derivedWindDirection = this.deriveWindDir(
       absoluteWindDir
     );
   },
</code></pre>
</div>

### High Level Glue Methods

With the utility, acquisition, and processing methods out of our way, we are now left with the task of orchestrating the entire thing. We do that by creating high level glue methods, that essentially calls the methods written above in a particular sequence, so that the entire operation is executed seamlessly.

<pre><code class="language-javascript">// Top level for info section
// Data in this.currentWeather
organizeCurrentWeatherInfo: function() {
     // data in this.currentWeather
     /*
     Coordinates and location is covered (get & set) in:
     &mdash; this.getCoordinates()
     &mdash; this.setFormatCoordinates()
     There are lots of async-await involved there.
     So it's better to keep them there.
     */
     this.getSetCurrentTime();
     this.getSetCurrentTemp();
     this.getSetTodayTempHighLowWithTime();
     this.getSetSummary();
     this.getSetPossibility();
   },
</code></pre>

<pre><code class="language-javascript">// Top level for highlights
organizeTodayHighlights: function() {
     // top level for highlights
     this.getSetUVIndex();
     this.getSetVisibility();
     this.getSetWindStatus();
   },
</code></pre>

<pre><code class="language-javascript">// Top level organization and rendering
organizeAllDetails: async function() {
     // top level organization
     await this.fetchWeatherData();
     this.organizeCurrentWeatherInfo();
     this.organizeTodayHighlights();
     this.getSetHourlyTempInfoToday();
   },
</code></pre>

#### mounted

Vue provides instance [lifecycle hooks](https://vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks) &mdash; properties that are essentially methods, and gets triggered when the instance lifecycle reaches that stage. For example, [created](https://vuejs.org/v2/api/#created), [mounted](https://vuejs.org/v2/api/#mounted), [beforeUpdate](https://vuejs.org/v2/api/#beforeUpdate), etc., are all very useful lifecycle hooks that allows the programmer to control the instance at a much more granular level than that would have been possible otherwise.

In the code of a Vue component, these lifecycle hooks are implemented just like you would for any other `prop`. For example:

<pre><code class="language-javascript">&lt;template&gt;
&lt;/template&gt;

&lt;script&gt;
// import statements
export default {
  data() {
    return {
    // data objects here
    }
  },
  methods: {
  // methods here
  },
  mounted: function(){
  // function body here
  },
}
&lt;/script&gt;

&lt;style&gt;
&lt;/style&gt;
</code></pre>

Armed with this new understanding, take a look at the code below for the `mounted` prop of `App.vue`:

<pre><code class="language-javascript">mounted: async function() {
   this.location = "New York";
   await this.organizeAllDetails();    
 }
</code></pre>

### Complete Code For App.vue

We have covered a lot of ground in this section, and the last few sections have given you things in bits and pieces. However, it’s important that you have the complete, assembled code for `App.vue` (subject to further modifications in subsequent sections). Here it goes:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
 &lt;div id="ancestor"&gt;
   &lt;div class="container-fluid" id="app"&gt;
     &lt;div class="row"&gt;
       &lt;div id="sidebar" class="col-md-3 col-sm-4 col-xs-12 sidebar"&gt;
         &lt;div id="search"&gt;
           &lt;input
             id="location-input"
             type="text"
             ref="input"
             placeholder="Location?"
             @keyup.enter="organizeAllDetails"
           &gt;
           &lt;button id="search-btn" @click="organizeAllDetails"&gt;
             &lt;img src="./assets/Search.svg" width="24" height="24"&gt;
           &lt;/button&gt;
         &lt;/div&gt;
         &lt;div id="info"&gt;
           &lt;div class="wrapper-left"&gt;
             &lt;div id="current-weather"&gt;
               {{ currentWeather.temp }}
               &lt;span&gt;°C&lt;/span&gt;
             &lt;/div&gt;
             &lt;div id="weather-desc"&gt;{{ currentWeather.summary }}&lt;/div&gt;
             &lt;div class="temp-max-min"&gt;
               &lt;div class="max-desc"&gt;
                 &lt;div id="max-detail"&gt;
                   &lt;i&gt;▲&lt;/i&gt;
                   {{ currentWeather.todayHighLow.todayTempHigh }}
                   &lt;span&gt;°C&lt;/span&gt;
                 &lt;/div&gt;
                 &lt;div id="max-summary"&gt;at {{ currentWeather.todayHighLow.todayTempHighTime }}&lt;/div&gt;
               &lt;/div&gt;
               &lt;div class="min-desc"&gt;
                 &lt;div id="min-detail"&gt;
                   &lt;i&gt;▼&lt;/i&gt;
                   {{ currentWeather.todayHighLow.todayTempLow }}
                   &lt;span&gt;°C&lt;/span&gt;
                 &lt;/div&gt;
                 &lt;div id="min-summary"&gt;at {{ currentWeather.todayHighLow.todayTempLowTime }}&lt;/div&gt;
               &lt;/div&gt;
             &lt;/div&gt;
           &lt;/div&gt;
           &lt;div class="wrapper-right"&gt;
             &lt;div class="date-time-info"&gt;
               &lt;div id="date-desc"&gt;
                 &lt;img src="./assets/calendar.svg" width="20" height="20"&gt;
                 {{ currentWeather.time }}
               &lt;/div&gt;
             &lt;/div&gt;
             &lt;div class="location-info"&gt;
               &lt;div id="location-desc"&gt;
                 &lt;img
                   src="./assets/location.svg"
                   width="10.83"
                   height="15.83"
                   style="opacity: 0.9;"
                 &gt;
                 {{ currentWeather.full_location }}
                 &lt;div id="location-detail" class="mt-1"&gt;
                   Lat: {{ currentWeather.formatted_lat }}
                   &lt;br&gt;
                   Long: {{ currentWeather.formatted_long }}
                 &lt;/div&gt;
               &lt;/div&gt;
             &lt;/div&gt;
           &lt;/div&gt;
         &lt;/div&gt;
       &lt;/div&gt;
       &lt;dashboard-content
         class="col-md-9 col-sm-8 col-xs-12 content"
         id="dashboard-content"
         :highlights="highlights"
         :tempVar="tempVar"
       &gt;&lt;/dashboard-content&gt;
     &lt;/div&gt;
   &lt;/div&gt;
 &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import Content from './components/Content.vue';

export default {
 name: 'app',
 props: [],
 components: {
   'dashboard-content': Content
 },
 data() {
   return {
     weatherDetails: false,
     location: '', // raw location from input
     lat: '', // raw latitude from google maps api response
     long: '', // raw longitude from google maps api response
     completeWeatherApi: '', // weather api string with lat and long
     rawWeatherData: '', // raw response from weather api
     currentWeather: {
       full_location: '', // for full address
       formatted_lat: '', // for N/S
       formatted_long: '', // for E/W
       time: '',
       temp: '',
       todayHighLow: {
         todayTempHigh: '',
         todayTempHighTime: '',
         todayTempLow: '',
         todayTempLowTime: ''
       },
       summary: '',
       possibility: ''
     },
     tempVar: {
       tempToday: [
         // gets added dynamically by this.getSetHourlyTempInfoToday()
       ],
     },
     highlights: {
       uvIndex: '',
       visibility: '',
       windStatus: {
         windSpeed: '',
         windDirection: '',
         derivedWindDirection: ''
       },
     }
   };
 },
 methods: {
   // Some utility functions
   convertToTitleCase: function(str) {
     str = str.toLowerCase().split(' ');
     for (var i = 0; i &lt; str.length; i++) {
       str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1);
     }
     return str.join(' ');
   },
   formatPossibility: function(str) {
     str = str.toLowerCase().split('-');
     for (var i = 0; i &lt; str.length; i++) {
       str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1);
     }
     return str.join(' ');
   },
   unixToHuman: function(timezone, timestamp) {
     /* READ THIS BEFORE JUDGING & DEBUGGING
     For any location beyond the arctic circle and the
     antarctic circle, the goddamn weather api does not return certain
     keys/values in each of this.rawWeatherData.daily.data[some_array_index].
     Due to this, console throws up an error.
     The code is correct, the problem is with the API.
     May be later on I will add some padding to tackle missing values.
     */
     var moment = require('moment-timezone'); // for handling date & time
     var decipher = new Date(timestamp * 1000);
     var human = moment(decipher)
       .tz(timezone)
       .format('llll');
     var timeArray = human.split(' ');
     var timeNumeral = timeArray[4];
     var timeSuffix = timeArray[5];
     var justTime = timeNumeral + ' ' + timeSuffix;
     var monthDateArray = human.split(',');
     var monthDate = monthDateArray[1].trim();
     return {
       fullTime: human,
       onlyTime: justTime,
       onlyMonthDate: monthDate
     };
   },
   fahToCel: function(tempInFahrenheit) {
     var tempInCelcius = Math.round((5 / 9) * (tempInFahrenheit &mdash; 32));
     return tempInCelcius;
   },
   milibarToKiloPascal: function(pressureInMilibar) {
     var pressureInKPA = pressureInMilibar * 0.1;
     return Math.round(pressureInKPA);
   },
   mileToKilometer: function(miles) {
     var kilometer = miles * 1.60934;
     return Math.round(kilometer);
   },
   deriveWindDir: function(windDir) {
     var wind_directions_array = [
       { minVal: 0, maxVal: 30, direction: 'N' },
       { minVal: 31, maxVal: 45, direction: 'NNE' },
       { minVal: 46, maxVal: 75, direction: 'NE' },
       { minVal: 76, maxVal: 90, direction: 'ENE' },
       { minVal: 91, maxVal: 120, direction: 'E' },
       { minVal: 121, maxVal: 135, direction: 'ESE' },
       { minVal: 136, maxVal: 165, direction: 'SE' },
       { minVal: 166, maxVal: 180, direction: 'SSE' },
       { minVal: 181, maxVal: 210, direction: 'S' },
       { minVal: 211, maxVal: 225, direction: 'SSW' },
       { minVal: 226, maxVal: 255, direction: 'SW' },
       { minVal: 256, maxVal: 270, direction: 'WSW' },
       { minVal: 271, maxVal: 300, direction: 'W' },
       { minVal: 301, maxVal: 315, direction: 'WNW' },
       { minVal: 316, maxVal: 345, direction: 'NW' },
       { minVal: 346, maxVal: 360, direction: 'NNW' }
     ];
     var wind_direction = '';
     for (var i = 0; i &lt; wind_directions_array.length; i++) {
       if (
         windDir &gt;= wind_directions_array[i].minVal &&
         windDir &lt;= wind_directions_array[i].maxVal
       ) {
         wind_direction = wind_directions_array[i].direction;
       }
     }
     return wind_direction;
   },

   // Some basic action oriented functions
   makeInputEmpty: function() {
     this.$refs.input.value = '';
   },
   makeTempVarTodayEmpty: function() {
     this.tempVar.tempToday = [];
   },
   detectEnterKeyPress: function() {
     var input = this.$refs.input;
     input.addEventListener('keyup', function(event) {
       event.preventDefault();
       var enterKeyCode = 13;
       if (event.keyCode === enterKeyCode) {
         this.setHitEnterKeyTrue();
       }
     });
   },
   locationEntered: function() {
     var input = this.$refs.input;
     if (input.value === '') {
       this.location = "New York";
     } else {
       this.location = this.convertToTitleCase(input.value);
     }
     this.makeInputEmpty();
     this.makeTempVarTodayEmpty();
   },

   getCoordinates: function() {
     this.locationEntered();
     var loc = this.location;
     var coords;
     var geocoder = new google.maps.Geocoder();
     return new Promise(function(resolve, reject) {
       geocoder.geocode({ address: loc }, function(results, status) {
         if (status == google.maps.GeocoderStatus.OK) {
           this.lat = results[0].geometry.location.lat();
           this.long = results[0].geometry.location.lng();
           this.full_location = results[0].formatted_address;
           coords = {
             lat: this.lat,
             long: this.long,
             full_location: this.full_location
           };
           resolve(coords);
         } else {
           alert("Oops! Couldn't get data for the location");
         }
       });
     });
   },

   // Some basic asynchronous functions
   setFormatCoordinates: async function() {
     var coordinates = await this.getCoordinates();
     this.lat = coordinates.lat;
     this.long = coordinates.long;
     this.currentWeather.full_location = coordinates.full_location;
     // Remember to beautify lat for N/S
     if (coordinates.lat &gt; 0) {
       this.currentWeather.formatted_lat =
         (Math.round(coordinates.lat * 10000) / 10000).toString() + '°N';
     } else if (coordinates.lat &lt; 0) {
       this.currentWeather.formatted_lat =
         (-1 * (Math.round(coordinates.lat * 10000) / 10000)).toString() +
         '°S';
     } else {
       this.currentWeather.formatted_lat = (
         Math.round(coordinates.lat * 10000) / 10000
       ).toString();
     }
     // Remember to beautify long for N/S
     if (coordinates.long &gt; 0) {
       this.currentWeather.formatted_long =
         (Math.round(coordinates.long * 10000) / 10000).toString() + '°E';
     } else if (coordinates.long &lt; 0) {
       this.currentWeather.formatted_long =
         (-1 * (Math.round(coordinates.long * 10000) / 10000)).toString() +
         '°W';
     } else {
       this.currentWeather.formatted_long = (
         Math.round(coordinates.long * 10000) / 10000
       ).toString();
     }
   },
   fixWeatherApi: async function() {
     await this.setFormatCoordinates();
     var weatherApi =
       'https://csm.fusioncharts.com/files/assets/wb/wb-data.php?src=darksky&lat=' +
       this.lat +
       '&long=' +
       this.long;
     this.completeWeatherApi = weatherApi;
   },
   fetchWeatherData: async function() {
     await this.fixWeatherApi();
     var axios = require('axios'); // for handling weather api promise
     var weatherApiResponse = await axios.get(this.completeWeatherApi);
     if (weatherApiResponse.status === 200) {
       this.rawWeatherData = weatherApiResponse.data;
     } else {
       alert('Hmm... Seems like our weather experts are busy!');
     }
   },

   // Get and set functions; often combined, because they are short

   // For basic info &mdash; left panel/sidebar
   getTimezone: function() {
     return this.rawWeatherData.timezone;
   },
   getSetCurrentTime: function() {
     var currentTime = this.rawWeatherData.currently.time;
     var timezone = this.getTimezone();
     this.currentWeather.time = this.unixToHuman(
       timezone,
       currentTime
     ).fullTime;
   },
   getSetSummary: function() {
     var currentSummary = this.convertToTitleCase(
       this.rawWeatherData.currently.summary
     );
     if (currentSummary.includes(' And')) {
       currentSummary = currentSummary.replace(' And', ',');
     }
     this.currentWeather.summary = currentSummary;
   },
   getSetPossibility: function() {
     var possible = this.formatPossibility(this.rawWeatherData.daily.icon);
     if (possible.includes(' And')) {
       possible = possible.replace(' And', ',');
     }
     this.currentWeather.possibility = possible;
   },
   getSetCurrentTemp: function() {
     var currentTemp = this.rawWeatherData.currently.temperature;
     this.currentWeather.temp = this.fahToCel(currentTemp);
   },
   getTodayDetails: function() {
     return this.rawWeatherData.daily.data[0];
   },
   getSetTodayTempHighLowWithTime: function() {
     var timezone = this.getTimezone();
     var todayDetails = this.getTodayDetails();
     this.currentWeather.todayHighLow.todayTempHigh = this.fahToCel(
       todayDetails.temperatureMax
     );
     this.currentWeather.todayHighLow.todayTempHighTime = this.unixToHuman(
       timezone,
       todayDetails.temperatureMaxTime
     ).onlyTime;
     this.currentWeather.todayHighLow.todayTempLow = this.fahToCel(
       todayDetails.temperatureMin
     );
     this.currentWeather.todayHighLow.todayTempLowTime = this.unixToHuman(
       timezone,
       todayDetails.temperatureMinTime
     ).onlyTime;
   },
   getHourlyInfoToday: function() {
     return this.rawWeatherData.hourly.data;
   },
   getSetHourlyTempInfoToday: function() {
     var unixTime = this.rawWeatherData.currently.time;
     var timezone = this.getTimezone();
     var todayMonthDate = this.unixToHuman(timezone, unixTime).onlyMonthDate;
     var hourlyData = this.getHourlyInfoToday();
     for (var i = 0; i &lt; hourlyData.length; i++) {
       var hourlyTimeAllTypes = this.unixToHuman(timezone, hourlyData[i].time);
       var hourlyOnlyTime = hourlyTimeAllTypes.onlyTime;
       var hourlyMonthDate = hourlyTimeAllTypes.onlyMonthDate;
       if (todayMonthDate === hourlyMonthDate) {
         var hourlyObject = { hour: '', temp: '' };
         hourlyObject.hour = hourlyOnlyTime;
         hourlyObject.temp = this.fahToCel(hourlyData[i].temperature).toString();
         this.tempVar.tempToday.push(hourlyObject);
         /*
         Since we are using array.push(), we are just adding elements
         at the end of the array. Thus, the array is not getting emptied
         first when a new location is entered.
         to solve this problem, a method this.makeTempVarTodayEmpty()
         has been created, and called from this.locationEntered().
         */
       }
     }
     /*
     To cover the edge case where the local time is between 10 &mdash; 12 PM,
     and therefore there are only two elements in the array
     this.tempVar.tempToday. We need to add the points for minimum temperature
     and maximum temperature so that the chart gets generated with atleast four points.
     */
     if (this.tempVar.tempToday.length &lt;= 2) {
       var minTempObject = {
         hour: this.currentWeather.todayHighLow.todayTempHighTime,
         temp: this.currentWeather.todayHighLow.todayTempHigh
       };
       var maxTempObject = {
         hour: this.currentWeather.todayHighLow.todayTempLowTime,
         temp: this.currentWeather.todayHighLow.todayTempLow
       };
       /*
       Typically, lowest temp are at dawn,
       highest temp is around mid day.
       Thus we can safely arrange like min, max, temp after 10 PM.
       */
       // array.unshift() adds stuff at the beginning of the array.
       // the order will be: min, max, 10 PM, 11 PM.
       this.tempVar.tempToday.unshift(maxTempObject, minTempObject);
     }
   },

   // For Today Highlights
   getSetUVIndex: function() {
     var uvIndex = this.rawWeatherData.currently.uvIndex;
     this.highlights.uvIndex = uvIndex;
   },
   getSetVisibility: function() {
     var visibilityInMiles = this.rawWeatherData.currently.visibility;
     this.highlights.visibility = this.mileToKilometer(visibilityInMiles);
   },
   getSetWindStatus: function() {
     var windSpeedInMiles = this.rawWeatherData.currently.windSpeed;
     this.highlights.windStatus.windSpeed = this.mileToKilometer(
       windSpeedInMiles
     );
     var absoluteWindDir = this.rawWeatherData.currently.windBearing;
     this.highlights.windStatus.windDirection = absoluteWindDir;
     this.highlights.windStatus.derivedWindDirection = this.deriveWindDir(
       absoluteWindDir
     );
   },

   // top level for info section
   organizeCurrentWeatherInfo: function() {
     // data in this.currentWeather
     /*
     Coordinates and location is covered (get & set) in:
     &mdash; this.getCoordinates()
     &mdash; this.setFormatCoordinates()
     There are lots of async-await involved there.
     So it's better to keep them there.
     */
     this.getSetCurrentTime();
     this.getSetCurrentTemp();
     this.getSetTodayTempHighLowWithTime();
     this.getSetSummary();
     this.getSetPossibility();
   },
   organizeTodayHighlights: function() {
     // top level for highlights
     this.getSetUVIndex();
     this.getSetVisibility();
     this.getSetWindStatus();
   },

   // topmost level orchestration
   organizeAllDetails: async function() {
     // top level organization
     await this.fetchWeatherData();
     this.organizeCurrentWeatherInfo();
     this.organizeTodayHighlights();
     this.getSetHourlyTempInfoToday();
   },
 },
 mounted: async function() {
   this.location = "New York";
   await this.organizeAllDetails();    
 }
};
&lt;/script&gt;
</code></pre>
</div>

And finally, after so much of patience and hard work, you can see the data flow with its raw power! Visit the application on the browser, refresh the page, search for a location in the application’s search box, and hit <kbd>Enter</kbd>!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36c5478-9e55-4fc6-8725-0ab2e6af232b/interactive-weather-dashboard-image13.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36c5478-9e55-4fc6-8725-0ab2e6af232b/interactive-weather-dashboard-image13.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36c5478-9e55-4fc6-8725-0ab2e6af232b/interactive-weather-dashboard-image13.png'>Large preview</a>)" alt="The application as shown in the browser" >}}

Now that we are done with all the heavy lifting, take a break. The subsequent sections focus on using the data to create charts that are beautiful and informative, followed by giving our ugly looking application a much deserved grooming session using CSS.   

## 5. Data Visualization With FusionCharts

### Fundamental Considerations For Charts

For the end user, the essence of a dashboard is essentially this: a collection of the filtered and carefully curated information on a particular topic, conveyed through visual/graphic instruments for quick ingestion. They don’t care about the subtleties of your data pipeline engineering, or how aesthetic your code is &mdash; all they want is a high-level view in 3 seconds. Therefore, our crude application displaying text data means nothing to them, and it’s high time we implement mechanisms to wrap the data with charts.

However, before we dive deep into the implementation of charts, let’s consider some pertinent questions and the possible answers from our perspective:

- **What type of charts are appropriate for the type of data we are dealing with?**  
Well, the answer has two aspects &mdash; the context, and the purpose. By context, we mean the type of data, and it’s overall fit in the scheme of bigger things, bounded by the scope and audience of the project. And by purpose, we essentially mean “what we want to emphasize on?”. For example, we can represent today’s temperature at different times of the day by using a [Column chart](https://www.fusioncharts.com/charts/column-bar-charts/) (vertical columns of equal width, with height proportional to the value the column represents). However, we are rarely interested in the individual values, but rather the overall variation and trend throughout the data. To suit the purpose, it is in our best interest to use a [Line chart](https://www.fusioncharts.com/dev/chart-guide/standard-charts/line-area-and-column-charts#line-chart-5), and we will do that shortly.
- **What should be kept in mind before selecting a charting library?**  
Since we are doing a project predominantly using JavaScript based technologies, it’s a no-brainer that any charting library that we choose for our project should be a native of the JavaScript world. With that basic premise in mind, we should consider the following before zeroing down on any particular library:
	- **Support for the frameworks of our choice**, which in this case, is Vue.js. A project can be developed in other popular JavaScript frameworks like React, or Angular &mdash; check the support of the charting library for your favorite framework. Also, support for other popular programming languages like Python, Java, C++, .Net (AS and VB), especially when the project involves some serious backend stuff, must be considered.
	- **Availability of charts types and features**, since it is almost impossible to know beforehand what will be final shape and purpose of the data in the project (especially if the requirements are regulated by your clients in a professional setting). In this case, you should cast your net wide, and choose a charting library that has the widest collection of charts. More importantly, to differentiate your project from others, the library should have have enough features in the form of configurable chart attributes, so that you can fine-tune and customize most aspects of the charts and the right level of granularity. Also, the default chart configurations should be sensible, and the library documentation has to be top notch, for reasons that’s obvious to professional developers.
	- **Learning curve, support community, and balance** must also be taken into consideration, especially when you are new to data visualization. On one end of the spectrum, you have proprietary tools like Tableau and Qlickview that costs a bomb, has smooth learning curve, but also comes with so many limitations in terms of customizability, integration, and deployment. On the other end there is d3.js &mdash; vast, free (open source), and customizable to its core, but you have to pay the price of a very steep learning curve to be able to do anything productive with the library. 

*What you need is the sweet spot &mdash; the right balance between productivity, coverage, customizability, learning curve, and off course, cost. We nudge you to take a look at [FusionCharts](https://www.fusioncharts.com/?utm_source=smashing_mag&utm_medium=blog&utm_campaign=weather_dashboard_vue) &mdash; the world’s most comprehensive and enterprise-ready JavaScript charting library for the web and mobile, that we will be using in this project for creating charts.*

### Introduction To FusionCharts
FusionCharts is used worldwide as the go-to JavaScript charting library by millions of developers spread across hundreds of countries around the globe. Technically, it’s as loaded and configurable as it can be, with support for integrating it with almost any popular tech stack used for web based projects. Using FusionCharts commercially requires a license, and you have to pay for the license depending on your use case (please contact sales if you are curious). However, we are using FusionCharts in this projects just to try out a few things, and therefore the non-licensed version (comes with a small watermark in your charts, and a few other restrictions). Using the non-licensed version is perfectly fine when you are trying out the charts and using it in your non-commercial or personal projects. If you have plans to deploy the application commercially, please ensure that you have a license from FusionCharts.

Since this is a project involving Vue.js, we will need two modules that needs to be installed, if not done earlier:

- The `fusioncharts` module, because it contains everything you will need for creating the charts
- The `vue-fusioncharts` module, which is essentially a wrapper for fusioncharts, so that it can be used in a Vue.js project

If you have not installed them earlier (as instructed in the third section), install them by executing the following command from the project’s root directory:

<pre><code class="language-bash">npm install fusioncharts vue-fusioncharts --save
</code></pre>

Next, ensure that the `src/main.js` file of the project has the following code (also mentioned in section 3):

<div class="break-out">

 <pre><code class="language-javascript">import Vue from 'vue';
import App from './App.vue';
import FusionCharts from 'fusioncharts';
import Charts from 'fusioncharts/fusioncharts.charts';
import Widgets from 'fusioncharts/fusioncharts.widgets';
import PowerCharts from 'fusioncharts/fusioncharts.powercharts';
import FusionTheme from 'fusioncharts/themes/fusioncharts.theme.fusion';
import VueFusionCharts from 'vue-fusioncharts';

Charts(FusionCharts);
PowerCharts(FusionCharts);
Widgets(FusionCharts);
FusionTheme(FusionCharts);

Vue.use(VueFusionCharts, FusionCharts);

new Vue({
 el: '#app',
 render: h => h(App)
})
</code></pre>
</div>

Perhaps the most critical line in the above snippet is the following:

<pre><code class="language-javascript">Vue.use(VueFusionCharts, FusionCharts)
</code></pre>

It instructs Vue to use the vue-fusioncharts module for making sense of many things in the project that are apparently not explicitly defined by us, but is defined in the module itself. Also, this type of statement implies **global** declaration, by which we mean that anywhere Vue encounters anything strange in the code of our project (things that we have not explicitly defined about using FusionCharts), it will at least look once in the vue-fusioncharts and fusioncharts node modules for their definitions, before throwing up errors. If we would have used FusionCharts in an isolated part of our project (not using it in almost all of the component files), then perhaps local declaration would have made more sense. 

With that, you are all set to use FusionCharts in the project. We will be using quite a few variety of charts, the choice being dependent on the aspect of the weather data that we want to visualize. Also, we will get to see the interplay of data binding, custom components, and watchers in action. 

### General Scheme For Using Fusioncharts In `.vue` Files

In this section, we will explain the general idea of using FusionCharts for creating various charts in the `.vue` files. But first, let’s see the pseudocode that schematically illustrates the core idea.

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;fusioncharts
      :attribute_1="data_object_1"
      :attribute_2="data_object_2"
         …
         …
         ...
    &gt;
    &lt;/fusioncharts&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  props: ["data_prop_received_by_the_component"],
  components: {},
  data() {
    return {
      data_object_1: "value_1",
      data_object_2: "value_2",
          …
          …
    };
  },
  methods: {},
  computed: {},
  watch: {
    data_prop_received_by_the_component: {
      handler: function() {
        // some code/logic, mainly data manipulation based
      },
      deep: true
    }
  }
};
&lt;/script&gt;

&lt;style&gt;
  // component specific special CSS code here
&lt;/style&gt;
</code></pre>

Let’s understand different parts of the above pseudocode:

- In the `<template>`, within the top level `<div>` (that’s pretty much mandatory for the template HTML code of every component), we have the custom component `<fusioncharts>`. We have the definition of the component contained in the `vue-fusioncharts` Node module that we have installed for this project. Internally, `vue-fusioncharts` relies on the `fusioncharts` module, which have also been installed. We imported the necessary modules and resolved their dependencies, instructed Vue to use the wrapper globally (throughout the project) in the `src/main.js` file, and therefore there is no lack of definition for the custom `<fusioncharts>` component that we have used here. Also, the custom component has custom attributes, and each of the custom attribute is bound to a data object (and in turn, their values), by the `v-bind` directive, for which the shorthand is the colon (`:`) symbol. We will learn about the attributes and their associated data objects in a greater detail, when we discuss some of the specific charts used in this project.
- In the `<script>`, first you declare the props that the component is supposed to receive, and then go on defining the data objects that are bounded to the attributes of `<fusioncharts>`. The values assigned to the data objects are the values that the attributes of `<fusioncharts>` pulls in, and the charts are created on the basis of those pulled in values. Apart from these, the most interesting part of the code is the `watch { }` object. This is a very special object in Vue’s scheme of things &mdash; it essentially instructs Vue to watch over any changes happening to certain data, and then take actions based on how the `handler` function for that data has been defined. For example, we want Vue to keep a watch on the `prop` received, i.e., `data_prop_received_by_the_component` in the pseudocode. The `prop` becomes a key in the `watch { }` object, and the value of the key is another object &mdash; a handler method that describes what needs to be done whenever the `prop` changes. With such elegant mechanisms to handle the changes, the app maintains its reactivity. The `deep: true` represents a boolean flag that you can associate with watchers, so that the object being watched is watched rather deeply, i.e., even the changes made in the nested levels of the object are tracked.  
	(*For more information on watchers, consult the [official documentation](https://vuejs.org/v2/api/#vm-watch)*).

Now that you are equipped with an understanding of the general scheme of things, let’s dive into the specific implementations of the charts in the `.vue` component files. The code will be pretty self-explanatory, and you should try to understand how the specifics fit in the general scheme of things described above.     

### Implementation Of Charts In .vue Files

While the very specifics of the implementation varies from one chart to another, the following explanation is applicable for all of them:

- `<template>`  
As explained previously, the `<fusioncharts>` custom component has several attributes, each of them being bound to corresponding data object defined in the `data()` function by using the `v-bind`: directive. The attribute names are quite self-explanatory for what they mean, and figuring out the corresponding data objects is also trivial.
- `<script>`  
In the `data()` function, the data objects and their values are what makes the charts work, because of the binding done by the `v-bind` (`:`) directives used on the attributes of `<fusioncharts>`. Before we dive deep into the individual data objects, it’s worth mentioning some general characteristics:
	- The data objects whose values are either `0` or `1` are boolean in nature, where `0` represents something not available/turned off, and `1` represents availability/turned on state. However, be cautious that non-boolean data objects can also have `0` or `1` as their values, besides other possible values &mdash; it depends on the context. For example, `containerbackgroundopacity` with its default value as `0` is boolean, whereas `lowerLimit` with its default value as `0` simply means the number zero is its literal value. 
	- Some data objects deals with CSS properties like margin, padding, font-size, etc. &mdash; the value has an implied unit of “px” or pixel. Similarly, other data objects can have implicit units associated with their values. For detailed information, please refer to the respective chart attributes page of FusionCharts Dev Center.
- In the `data()` function, perhaps the most interesting and non-obvious object is the dataSource. This object has three main objects nested within it:
	- **chart**: This object encapsulates lots of chart attributes related to the configuration and cosmetics of the chart. It is almost a compulsory construct that you will find in all the charts you will create for this project.
	- **colorrange**: This object is somewhat specific to the chart under consideration, and is mainly present in charts that deals with multiple colors/shades to demarcate different sub-ranges of the scale used in chart.
	- value: This object, again, is present in charts that has a specific value that needs to be highlighted in the range of the scale.
- The `watch { }` object is perhaps the most crucial thing that makes this chart, and the other charts used in this project, spring to life. The reactivity of the charts, i.e., the charts updating themselves based on the new values resulting from a new user query is controlled by the watchers defined in this object. For example, we have defined a watcher for the prop `highlights` received by the component, and then defined a handler function to instruct Vue about the necessary actions that it should take, when anything changes about the object being watched in the entire project. This means that whenever `App.vue` yields a new value for any of the object within `highlights`, the information trickles down all the way down to this component, and the new value is updated in the data objects of this component. The chart being bound to the values, also gets updated as a result of this mechanism. 

The above explanations are quite broad strokes to help us develop an intuitive understanding of the bigger picture. Once you understand the concepts intuitively, you can always consult the documentation of Vue.js and FusionCharts, when something is not clear to you from the code itself. We leave the exercise to you, and from the next subsection onward, we will not explain stuff that we covered in this subsection. 

#### src/components/TempVarChart.vue

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18ac2859-3c79-4e90-b903-2404db7e69a0/interactive-weather-dashboard-image14.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18ac2859-3c79-4e90-b903-2404db7e69a0/interactive-weather-dashboard-image14.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18ac2859-3c79-4e90-b903-2404db7e69a0/interactive-weather-dashboard-image14.png'>Large preview</a>)" alt="A diagram showing Hourly Temperature" >}}

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
 &lt;div class="custom-card header-card card"&gt;
   &lt;div class="card-body pt-0"&gt;
     &lt;fusioncharts
       type="spline"
       width="100%"
       height="100%"
       dataformat="json"       dataEmptyMessage="i-https://i.postimg.cc/R0QCk9vV/Rolling-0-9s-99px.gif"
       dataEmptyMessageImageScale=39
       :datasource="tempChartData"
     &gt;
     &lt;/fusioncharts&gt;
   &lt;/div&gt;

 &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
 props: ["tempVar"],
 components: {},
 data() {
   return {
     tempChartData: {
       chart: {
         caption: "Hourly Temperature",
         captionFontBold: "0",
         captionFontColor: "#000000",
         captionPadding: "30",
         baseFont: "Roboto",
         chartTopMargin: "30",
         showHoverEffect: "1",
         theme: "fusion",
         showaxislines: "1",
         numberSuffix: "°C",
         anchorBgColor: "#6297d9",
         paletteColors: "#6297d9",
         drawCrossLine: "1",
         plotToolText: "$label&lt;br&gt;&lt;hr&gt;&lt;b&gt;$dataValue&lt;/b&gt;",
         showAxisLines: "0",
         showYAxisValues: "0",
         anchorRadius: "4",
         divLineAlpha: "0",
         labelFontSize: "13",
         labelAlpha: "65",
         labelFontBold: "0",
         rotateLabels: "1",
         slantLabels: "1",
         canvasPadding: "20"
       },
       data: [],
     },
   };
 },
 methods: {
   setChartData: function() {
     var data = [];
     for (var i = 0; i &lt; this.tempVar.tempToday.length; i++) {
       var dataObject = {
         label: this.tempVar.tempToday[i].hour,
         value: this.tempVar.tempToday[i].temp
       };
       data.push(dataObject);
     }
     this.tempChartData.data = data;
   },
 },
 mounted: function() {
   this.setChartData();
 },
 watch: {
   tempVar: {
     handler: function() {
       this.setChartData();                                   
     },
     deep: true
   },
 },
};
&lt;/script&gt;

&lt;style&gt;
&lt;/style&gt;
</code></pre>
</div>

#### src/components/UVIndex.vue

This component contains an extremely useful chart &mdash; the Angular Gauge. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c958d43b-e6c4-47ba-8c01-e049749f0248/interactive-weather-dashboard-image15.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c958d43b-e6c4-47ba-8c01-e049749f0248/interactive-weather-dashboard-image15.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c958d43b-e6c4-47ba-8c01-e049749f0248/interactive-weather-dashboard-image15.png'>Large preview</a>)" alt="UV Index" >}}

The code for the component is given below. For detailed information on the chart attributes of Angular Gauge, refer to [FusionCharts Dev Center page for Angular Gauge](https://www.fusioncharts.com/dev/chart-guide/gauges-and-widgets/angular-gauge?utm_source=smashing_mag&utm_medium=blog&utm_campaign=weather_dashboard_vue).

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
 &lt;div class="highlights-item col-md-4 col-sm-6 col-xs-12 border-top"&gt;
   &lt;div&gt;
     &lt;fusioncharts
       :type="type"
       :width="width"
       :height="height"
       :containerbackgroundopacity="containerbackgroundopacity"
       :dataformat="dataformat"
       :datasource="datasource"
     &gt;&lt;/fusioncharts&gt;
   &lt;/div&gt;
 &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
 props: ["highlights"],
 components: {},
 data() {
   return {
     type: "angulargauge",
     width: "100%",
     height: "100%",
     containerbackgroundopacity: 0,
     dataformat: "json",
     datasource: {
       chart: {
         caption: "UV Index",
         captionFontBold: "0",
         captionFontColor: "#000000",
         captionPadding: "30",
         lowerLimit: "0",
         upperLimit: "15",
         lowerLimitDisplay: "1",
         upperLimitDisplay: "1",
         showValue: "0",
         theme: "fusion",
         baseFont: "Roboto",
         bgAlpha: "0",
         canvasbgAlpha: "0",
         gaugeInnerRadius: "75",
         gaugeOuterRadius: "110",
         pivotRadius: "0",
         pivotFillAlpha: "0",
         valueFontSize: "20",
         valueFontColor: "#000000",
         valueFontBold: "1",
         tickValueDistance: "3",
         autoAlignTickValues: "1",
         majorTMAlpha: "20",
         chartTopMargin: "30",
         chartBottomMargin: "40"
       },
       colorrange: {
         color: [
           {
             minvalue: "0",
             maxvalue: this.highlights.uvIndex.toString(),
             code: "#7DA9E0"
           },
           {
             minvalue: this.highlights.uvIndex.toString(),
             maxvalue: "15",
             code: "#D8EDFF"
           }
         ]
       },
       annotations: {
         groups: [
           {
             items: [
               {
                 id: "val-label",
                 type: "text",
                 text: this.highlights.uvIndex.toString(),
                 fontSize: "20",
                 font: "Source Sans Pro",
                 fontBold: "1",
                 fillcolor: "#212529",
                 x: "$gaugeCenterX",
                 y: "$gaugeCenterY"
               }
             ]
           }
         ]
       },
       dials: {
         dial: [
           {
             value: this.highlights.uvIndex.toString(),
             baseWidth: "0",
             radius: "0",
             borderThickness: "0",
             baseRadius: "0"
           }
         ]
       }
     }
   };
 },
 methods: {},
 computed: {},
 watch: {
   highlights: {
     handler: function() {
       this.datasource.colorrange.color[0].maxvalue = this.highlights.uvIndex.toString();
       this.datasource.colorrange.color[1].minvalue = this.highlights.uvIndex.toString();
       this.datasource.annotations.groups[0].items[0].text = this.highlights.uvIndex.toString();
     },
     deep: true
   }
 }
};
&lt;/script&gt;
</code></pre>
</div>

#### src/components/Visibility.vue

In this component, we use a [Horizontal Linear Gauge](https://www.fusioncharts.com/dev/chart-guide/gauges-and-widgets/linear-gauge) to represent the visibility, as shown in the image below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205825ff-05a5-41d7-aa81-cd0a9eab5d21/interactive-weather-dashboard-image16.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205825ff-05a5-41d7-aa81-cd0a9eab5d21/interactive-weather-dashboard-image16.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205825ff-05a5-41d7-aa81-cd0a9eab5d21/interactive-weather-dashboard-image16.png'>Large preview</a>)" alt="A screenshot of the Horizontal Linear Gauge representing Air Visibility (16km)" >}}

The code for the component is given below. For an in depth understanding of the different attributes of this chart type, please refer to [FusionCharts Dev Center page for Horizontal Linear Gauge](https://www.fusioncharts.com/dev/chart-attributes/?chart=HLinearGauge&utm_source=smashing_mag&utm_medium=blog&utm_campaign=weather_dashboard_vue).

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
 &lt;div class="highlights-item col-md-4 col-sm-6 col-xs-12 border-left border-right border-top"&gt;
   &lt;div&gt;
     &lt;fusioncharts
       :type="type"
       :width="width"
       :height="height"
       :containerbackgroundopacity="containerbackgroundopacity"
       :dataformat="dataformat"
       :datasource="datasource"
     &gt;
     &lt;/fusioncharts&gt;
     &lt;/div&gt;
 &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
 props: ["highlights"],
 components: {},
 methods: {},
 computed: {},
 data() {
   return {
     type: "hlineargauge",
     width: "100%",
     height: "100%",
     containerbackgroundopacity: 0,
     dataformat: "json",
     creditLabel: false,
     datasource: {
       chart: {
         caption: "Air Visibility",
         captionFontBold: "0",
         captionFontColor: "#000000",
         baseFont: "Roboto",
         numberSuffix: " km",
         lowerLimit: "0",
         upperLimit: "40",
         showPointerShadow: "1",
         animation: "1",
         transposeAnimation: "1",
         theme: "fusion",
         bgAlpha: "0",
         canvasBgAlpha: "0",
         valueFontSize: "20",
         valueFontColor: "#000000",
         valueFontBold: "1",
         pointerBorderAlpha: "0",
         chartBottomMargin: "40",
         captionPadding: "30",
         chartTopMargin: "30"
       },
       colorRange: {
         color: [
           {
             minValue: "0",
             maxValue: "4",
             label: "Fog",
             code: "#6297d9"
           },
           {
             minValue: "4",
             maxValue: "10",
             label: "Haze",
             code: "#7DA9E0"
           },
           {
             minValue: "10",
             maxValue: "40",
             label: "Clear",
             code: "#D8EDFF"
           }
         ]
       },
       pointers: {
         pointer: [
           {
             value: this.highlights.visibility.toString()
           }
         ]
       }
     }
   };
 },
 watch: {
   highlights: {
     handler: function() {
       this.datasource.pointers.pointer[0].value = this.highlights.visibility.toString();
     },
     deep: true
   }
 }
};
&lt;/script&gt;
</code></pre>
</div>

#### src/components/WindStatus.vue

This component displays the wind speed and direction (wind velocity, if you are physics savvy), and it is very difficult to represent a vector using a chart. For such cases, we suggest representing them with the aid of some nice images and text values. Since the representation we have thought about is entirely dependent on CSS, we will implement it in the next section that deals with the CSS. However, take a look at what we are aiming to create:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf9ab00-3ccc-473b-82f6-ab517c7bf412/interactive-weather-dashboard-image17.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf9ab00-3ccc-473b-82f6-ab517c7bf412/interactive-weather-dashboard-image17.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf9ab00-3ccc-473b-82f6-ab517c7bf412/interactive-weather-dashboard-image17.png'>Large preview</a>)" alt="Wind Status: Wind Direction (left) and Wind Speed (right)" >}}

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
 &lt;div class="highlights-item col-md-4 col-sm-6 col-xs-12 border-top"&gt;
   &lt;div&gt;
   &lt;div class="card-heading pt-5"&gt;Wind Status&lt;/div&gt;
   &lt;div class="row pt-4 mt-4"&gt;
     &lt;div class="col-sm-6 col-md-6 mt-2 text-center align-middle"&gt;
       &lt;p class="card-sub-heading mt-3"&gt;Wind Direction&lt;/p&gt;
       &lt;p class="mt-4"&gt;&lt;img src="../assets/winddirection.svg" height="40" width="40"&gt;&lt;/p&gt;
       &lt;p class="card-value mt-4"&gt;{{ highlights.windStatus.derivedWindDirection }}&lt;/p&gt;
     &lt;/div&gt;
     &lt;div class="col-sm-6 col-md-6 mt-2"&gt;
       &lt;p class="card-sub-heading mt-3"&gt;Wind Speed&lt;/p&gt;
       &lt;p class="mt-4"&gt;&lt;img src="../assets/windspeed.svg" height="40" width="40"&gt;&lt;/p&gt;
       &lt;p class="card-value mt-4"&gt;{{ highlights.windStatus.windSpeed }} km/h&lt;/p&gt;
     &lt;/div&gt;
   &lt;/div&gt;
   &lt;/div&gt;
 &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
 props: ["highlights"],
 components: {},
 data() {
   return {};
 },
 methods: {},
 computed: {}
};
&lt;/script&gt;
</code></pre>
</div>

### Wrapping Up With Highlights.vue

Recall that we have already implemented code with CSS for all the components &mdash; except `Content.vue` and `Highlights.vue`. Since `Content.vue` is a dumb component that just relays data, the minimal styling it needs has already been covered. Also, we have already written appropriate code for styling the sidebar and the cards containing the charts. Therefore, all we are left to do is add some stylistic bits to `Highlights.vue`, which primarily involves using the CSS classes:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="custom-content-card content-card card"&gt;
    &lt;div class="card-body pb-0"&gt;
    &lt;div class="content-header h4 text-center pt-2 pb-3"&gt;Highlights&lt;/div&gt;
      &lt;div class="row"&gt;
        &lt;uv-index :highlights="highlights"&gt;&lt;/uv-index&gt;
        &lt;visibility :highlights="highlights"&gt;&lt;/visibility&gt;
        &lt;wind-status :highlights="highlights"&gt;&lt;/wind-status&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import UVIndex from "./UVIndex.vue";
import Visibility from "./Visibility.vue";
import WindStatus from "./WindStatus.vue";

export default {
  props: ["highlights"],
  components: {
    "uv-index": UVIndex,
    "visibility": Visibility,
    "wind-status": WindStatus,
  },
};
&lt;/script&gt;
</code></pre>
</div>

### Deployment And Source Code

With the charts and style in order, we are done! Take a moment to appreciate the beauty of your creation.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c538b1aa-2c4d-4dd7-8d27-6d0db227ee7c/interactive-weather-dashboard-image18.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c538b1aa-2c4d-4dd7-8d27-6d0db227ee7c/interactive-weather-dashboard-image18.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c538b1aa-2c4d-4dd7-8d27-6d0db227ee7c/interactive-weather-dashboard-image18.png'>Large preview</a>)" alt="The result" >}}

It’s now time for you to deploy your application, and share it with your peers. If you don’t have much idea about deployment and expect us to help you, look [here about our take on deployment ideas](https://www.fusioncharts.com/resources/developers/charting-react-vs-vue-npm-battle-tutorial#production-deployment). The linked article also contains suggestions on how to remove the FusionCharts watermark at the left bottom of every chart.

If you mess up somewhere and want a reference point, the [source code is available on Github](https://github.com/smashingmagazine/modified_weather_dashboard).

{{< signature "ms, ra, il" >}}
