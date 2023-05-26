---
title: 'How To Build A Skin For Your Web App With React And WordPress'
slug: react-wordpress-web-app
author: muhammad-muhsin
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b9dab3-8e73-4858-b878-d42d0db66dcf/react-wp-app14.png
date: 2018-03-07T13:00:58+01:00
summary: >-
  If you've been looking for a content-driven solution, this article will explain how you can build a SPA WordPress theme with React. Continue reading to find out why this is a good choice for your web app's back-end technology.
description: >-
  If you've been looking for a content-driven solution, this article will explain how you can build a SPA WordPress theme with React. Continue reading to find out why this is a good choice for your web app's back-end technology.
categories:
  - WordPress
  - React
  - Node.js
---
So you’ve trained yourself as a web engineer, and now want to build a blazing fast online shop for your customers. The product list should appear in an instant, and searching should waste no more than a split second either. Is that the stuff of daydreams?

Not anymore. Well, at least it's nothing that can't be achieved with the combination of WordPress’ REST API and React, a modern JavaScript library.

## Wait, What? WordPress REST API?

Yes, the [WordPress REST API](https://v2.wp-api.org/) will help you build the back-end foundation for your web application. This is a good choice for your web application’s back-end technology if you are building a content-driven solution. WordPress will interoperate smoothly with other technologies as well; you could **use Node.js as the focus of your application** to connect to other RESTful services.

The WordPress REST API is a game-changer for WordPress, which can now safely be called a web application framework &mdash; not just a CMS. Now that the front- and back-end are completely decoupled, WordPress can be used as a mobile app back-end or as a back-end for any system focusing on content.

But why WordPress? The reason: You will be amazed at the functionalities that emerge out of the box with WordPress. You will get extensive user management, media management, and an incredibly developer-friendly set of APIs to extend your work.

In this article, I will walk you through building an SPA (Single Page Application) WordPress theme using the JavaScript library called React, connecting to the WP REST API.

{{% feature-panel %}}

## Let’s Jump Into Building The Theme

This article assumes you are already familiar with the various existing WordPress APIs, particularly the ones that drive the development of themes for your site’s aesthetics, and functionalities for your site’s plugins. I also assume you have set up your development platform for WordPress, such as the LAMP stack in a Linux or MacOS environment.

For simplicity, though, I will refer only to absolute paths as visible with the XAMPP platform that is used with Windows.

Now, let's create an instance of WordPress in our localhost, naming it 'Celestial.’ That is the name of the WordPress theme we are going to use to help us set the direction for building future themes ready for use with web applications powered by the WordPress REST API. You may already be familiar with WordPress’ much-loved template hierarchy, but with the REST API, you have an opportunity to discover something different!

We then need to create a folder for the theme within the `wp-content\themes` folder. Navigate to `C:\xampp\htdocs\celestial\wp-content\themes\` (or equivalent) and create a folder `celestial`. Add these files inside the `celestial` theme folder:

1. `index.php`  
The catch-all file for the theme.
2. `style.css`  
This contains information about the theme (and not actual CSS).
3. `functions.php`  
To write the functionality and the importing of CSS and JS files.

Add an image file named `screenshot.jpg` if you want a picture for your theme showing inside the dashboard.

**Note**: *The code for each file is a few lines long and can be found on [GitHub](https://github.com/m-muhsin/celestial)*.

Next, log in to your WordPress Dashboard, head over to **Appearance** → **Themes** and select 'Celestial' as the theme. Now that the foundation is in place, let's get onto creating the theme.

{{< rimg href="https://codex.wordpress.org/Using_Themes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b9dab3-8e73-4858-b878-d42d0db66dcf/react-wp-app14.png" sizes="100vw" caption="You can select the 'Celestial' theme you created from the Themes panel in the dashboard." alt="WordPress theme selector" >}}

## Getting Started With React And Webpack For The Theme

React is a very popular UI library supported and maintained by Facebook. According to [Stack Overflow's Developer Survey 2017](https://insights.stackoverflow.com/survey/2017) results, “React is the most loved among developers.”

<figure><a href="https://reactjs.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/064fc70f-5df3-4333-b9d4-f6abe2f946de/react-wp-app8.png" width="" height="" alt="ReactJS" /></a><figcaption>React: A JavaScript library for building user interfaces.</figcaption></figure>

For starting the project, you need to initialize the project as an NPM (Node Package Manager) project. This is done with the command `npm init` in the terminal (after having [installed Node.js and NPM on your computer](https://blog.teamtreehouse.com/install-node-js-npm-windows)). Initializing the project will prompt you for certain configuration information. After successful initialization, NPM will create a package.json file in the theme’s root directory. This file will include the project details and all dependencies of the project.  

[React](https://reactjs.org/) is now under MIT license, so we will be using version 16 of React as the JavaScript library for this project. React has some cool features under the hood, such as the Virtual DOM (a representation of the document within memory) and has a host of tools surrounding it such as the React Router. React is also used in the [WordPress’ Project Calypso](https://developer.wordpress.com/calypso/) &mdash; the dashboard for WordPress.com.

We will now install the required NPM packages to the project:

<ol>
<li>Type <code>npm install --save react react-dom</code> in the terminal and press enter to install the packages.  

{{< rimg href="https://reactjs.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f970843a-470d-4ad9-96ab-367615902678/react-wp-app11.png" sizes="100vw" caption="Using npm to install react and react-dom." alt="Installing React via CLI" >}}

Since we are building the theme as a Single Page Application (SPA), we need the help of a tool such as Webpack. We will be writing code as different components, and Webpack will help us package them all together and output them as a single .js or .css file. In short, it’s a module bundler.<br /><br />Webpack has first to be installed globally on your computer. To do that, we again can utilize NPM.</li>

<li>Type in the command <code>npm install -g webpack</code> to get the latest stable version of Webpack installed globally in your system.<br /><br />Next, we will install NPM packages supporting Webpack in our app.</li>

<li>Go to the <em>package.json</em> file in my git repo and copy the rest of the dependencies from there into your <em>package.json</em>’s dependencies section. Then run <code>npm install</code> again to install all the packages within <em>package.json</em>.

<div class="break-out">

<pre><code class="language-javascript">{
 "name": "celestial",
 "version": "1.0.0",
 "description": "A basic theme using the WordPress REST API and React",
 "main": "index.js",
 "dependencies": {
   "babel-core": "&#94;6.26.0",
   "babel-loader": "&#94;7.1.2",
   "babel-preset-es2015": "&#94;6.24.1",
   "babel-preset-react": "&#94;6.24.1",
   "css-loader": "&#94;0.28.7",
   "extract-text-webpack-plugin": "&#94;3.0.1",
   "file-loader": "&#94;1.1.5",
   "image-webpack-loader": "&#94;3.4.2",
   "node-sass": "&#94;4.5.3",
   "path": "&#94;0.12.7",
   "react": "&#94;16.0.0",
   "react-dom": "&#94;16.0.0",
   "react-router-dom": "&#94;4.2.2",
   "sass-loader": "&#94;6.0.6",
   "style-loader": "&#94;0.19.0",
   "url-loader": "&#94;0.6.2",
   "webpack": "&#94;3.6.0"
 },
 "devDependencies": {},
 "scripts": {
   "build": "webpack",   
   "watch": "webpack --watch"
 },
 "keywords": [
   "blog",
   "decoupled",
   "react",
   "rest-api"
 ],
 "author": "Muhammad Muhsin",
 "license": "GPL-3.0"
}
</code></pre></div>
<br /><em>The above is a list of all required packages in the package.json file for this project.</em></li>
<li>Copy the configurations from <a href="https://github.com/m-muhsin/celestial/blob/master/webpack.config.js">GitHub</a> and paste it into your theme folder’s <em>webpack.config.js</em> file.

<div class="break-out">

<pre><code class="language-javascript">var ExtractTextPlugin = require("extract-text-webpack-plugin");
var path = require('path');

module.exports = {
   entry: {
       app: './src/index.jsx'
   },
   output: {
       path: path.resolve(__dirname, 'dist'),
       filename: '[name].js'
   },
   module: {
       rules: [
           {
               test: /\.scss$/,
               use: ExtractTextPlugin.extract({
                   fallback: 'style-loader',
                   use: ['css-loader','sass-loader'],
                   publicPath: 'dist'
               })
           },
           {
               test: /\.jsx?$/,
               exclude: /node_modules/,
               use: 'babel-loader'
           },
           {
               test: /\.(jpe?g|png|gif|svg)$/i,
               use: [
                   'file-loader?name=[name].[ext]&amp;outputPath=images/&amp;publicPath=https://localhost/celestial/wp-content/themes/celestial/dist/images',
                   'image-webpack-loader'
               ]
           },
           { test:
               /\.(woff2?|svg)$/,
               loader: 'url-loader?limit=10000&amp;name=fonts/[name].[ext]'
           },
           {
               test: /\.(ttf|eot)$/,
               loader: 'file-loader?name=fonts/[name].[ext]'
           }
       ]
   },
   resolve: {
       extensions: ['.js', '.jsx']
   },
   plugins: [
       new ExtractTextPlugin({
           filename: "style.css",
           allChunks: true
       })
   ]
}
</code></pre></div>
<br /><strong>Important</strong>: Please note that <code>module.exports</code> → <code>module</code> → <code>rules[3]</code> → <code>use</code> → <code>publicPath</code> can change according to where your project’s dist images are situated in localhost. If this is wrong, images may not display correctly in the web app.</li>
<li>Afterwards, these commands can be used to compile the project:
  <ul>
    <li><code>webpack</code> or <code>npm run build</code> to compile the project, or</li>
    <li><code>webpack --watch</code> or <code>npm run watch</code> to compile the project and watch for changes.</li>
  </ul>
</li>
</li>
</ol>

**Note**: *To get a better understanding of Webpack, read this [article by Joseph Zimmerman](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/) on Smashing Magazine*.

## Extending The WordPress REST API

The WordPress REST API comes with many different endpoints for fetching posts, pages, media and so on. However, they may not always have all the details in their response. For instance, the posts method does not give the URL of the featured image or the author’s name. Therefore, we have to make separate calls to each of these elements.

{{< rimg href="https://v2.wp-api.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59bb4534-9079-4ee0-9cd1-ccc15a0eb1e7/react-wp-app17.png" sizes="100vw" caption="Access your WordPress site's data through an easy-to-use HTTP REST API." alt="Wordpress REST API" >}}

But what if you wanted to have your own data appear *within* the posts response? That’s where the magic of extending the REST API comes in. The following code will add two additional variables in the response to the *posts* request, namely `author_name` and `featured_image_src`. The code is within the *functions.php* file:

<p><div class="break-out">

<pre><code class="language-javascript">// Add various fields to the JSON output
function celestial_register_fields() {
    // Add Author Name
    register_rest_field( 'post',
        'author_name',
        array(
            'get_callback'      => 'celestial_get_author_name',
            'update_callback'   => null,
            'schema'            => null
        )
    );
    // Add Featured Image
    register_rest_field( 'post',
        'featured_image_src',
        array(
            'get_callback'      => 'celestial_get_image_src',
            'update_callback'   => null,
            'schema'            => null
        )
   );
   // Add Published Date
    register_rest_field( 'post',
       'published_date',
       array(
           'get_callback'      => 'celestial_published_date',
           'update_callback'   => null,
           'schema'            => null
       )
    );
}
add_action( 'rest_api_init', 'celestial_register_fields' );

function celestial_get_author_name( $object, $field_name, $request ) {
    return get_the_author_meta( 'display_name' );
}
function celestial_get_image_src( $object, $field_name, $request ) {
   if($object[ 'featured_media' ] == 0) {
       return $object[ 'featured_media' ];
   }
    $feat_img_array = wp_get_attachment_image_src( $object[ 'featured_media' ], 'thumbnail', true );
   return $feat_img_array[0];
}
function celestial_published_date( $object, $field_name, $request ) {
    return get_the_time('F j, Y');
}
</code></pre></div>  
<br /><em>Extending the REST API with additional variables in the functions.php file.</em></p>

## A Global JavaScript Variable

There are certain WordPress constants (or known as 'variables') that we will be using throughout the React app. This will be information about the various routes of the application (and later on be WooCommerce specific ones).

This variable is defined within the *functions.php* file. It will be called 'CelestialSettings' and be appended to `celestial-scripts`, the handle for the enqueued *app.js* file:

<p><div class="break-out">

<pre><code class="language-javascript">wp_enqueue_script( 'celestial-script', get_stylesheet_directory_uri() . '/dist/app.js' , array(), '1.0', true );

    $url = trailingslashit( home_url() );
    $path = trailingslashit( parse_url( $url, PHP_URL_PATH ) );

    wp_scripts()->add_data( 'celestial-script', 'data', sprintf( 'var CelestialSettings = %s;', wp_json_encode( array(
        'title' => get_bloginfo( 'name', 'display' ),
        'path' => $path,
        'URL' => array(
            'api' => esc_url_raw( get_rest_url( null, '/wp/v2' ) ),
            'root' => esc_url_raw( $url ),
        ),
        'woo' => array(
            'url' => esc_url_raw( 'https://localhost/celestial/wp-json/wc/v2/' ),
            'consumer_key' => 'ck_803bcdcaa73d3a406a0f107041b07ef6217e05b9',
            'consumer_secret' => 'cs_c50ba3a77cc88c3bf46ebac49bbc96de3a543f03'
        ),
    ) ) ) );
</code></pre></div>
<br /><em>Passing WordPress (PHP) variables to the front-end.</em></p>

The above code shows an example of getting WordPress (PHP) variables to the front-end, an important and very useful technique when building a decoupled theme. This object variable holds the site title, path, the URL for the API and root and three variables relating to WooCommerce (explained later).

## React And JSX

React is different from the rest of the major JavaScript libraries. What I mean by that is, we generally write JavaScript within our HTML. However, when it comes to React, we write HTML inside our JavaScript code. To be more accurate, we write JSX inside JS. JSX is very similar to HTML but has a few differences. The `class` attribute is written as `className` for instance. This is then converted to plain JavaScript through Webpack and Babel and saved within *app.js*.

There are, however, a few restrictions with writing JSX. For instance, we can have only one child within our `render()` method, which will serve as the root element for a Component. However, the advantage is that it is easier to debug. We can know exactly where we have made a mistake, whereas in normal HTML our error will generally not be shown explicitly. We will be writing JSX for this project, and therefore, the JavaScript files will have an extension of `.jsx`. However, it could also be `.js` if you prefer so.

Create the following files within the `src` folder:

1. `index.jsx` (the main file and the one which contains the React Router configurations)
2. `header.jsx` (the header component)
3. `footer.jsx` (the footer component)
4. `posts.jsx` (for the archive of posts)
5. `post-list.jsx` (component for an individual post within `posts.jsx`)
6. `post.jsx` (for a single post)
7. `products.jsx` (contains all the products from WooCommerce)
8. `product.jsx` (displays a single product from WooCommerce)
9. `style.scss` (to contain all CSS code in SASS format)

<figure><a href="https://github.com/m-muhsin/celestial/tree/master/src"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1a08949-3305-4013-a8d8-db32676be359/react-wp-app16.png" width="" height="" alt="Folder structure of src folder" /></a><figcaption>Folder structure of the src folder in the Celestial project.</figcaption></figure>

## ReactDOM.render()

The *index.jsx* file is the root of the project. What I mean by that is, the *index.jsx* contains the component App which is rendered to the DOM.

<div class="break-out">

<pre><code class="language-javascript">import { render } from 'react-dom'; // importing render from ReactDOM

const App = () =&gt; ( // defining the routes

   &lt;div id="page-inner"&gt;

       &lt;Header /&gt;

       &lt;div id="content"&gt;

           &lt;Switch&gt;

               &lt;Route exact path={CelestialSettings.path} component={Posts} /&gt; // the root path

           &lt;/Switch&gt;

       &lt;/div&gt;

       &lt;Footer /&gt;

   &lt;/div&gt;

);

// React Router

const routes = (

   &lt;Router&gt;

       &lt;Route path="/" component={App} /&gt;

   &lt;/Router&gt;

);

render( // rendering to the DOM by replacing #page with the root React component

   (routes), document.getElementById('page') // rendering the route

);
</code></pre></div>

The other components are specified within React Router and will be loaded upon visiting the different routes.

This is how we write modular components where all the different components ultimately end at *index.jsx*.

## Stateful vs. Stateless Components

You would have noticed components being written in either of the following two ways:

1. `const App = () => (`
2. `class Post extends React.Component {`

The first way is how we write Stateless Components and the second is an example of Stateful Components. Stateless means that component does not have ‘state’ in it. ‘state’ is essentially a variable that has information within the component, and every time the variable changes, the component is re-rendered. Stateful Components are also known as ‘Smart Components.’ The state variables are thus used for inner communication within that component.

The second type, Stateless Components do not have the state variable in them and sometimes called ‘Dumb Components.’ However, like Stateful Components, they have ‘props,’ which are properties passed down to them from their parent components.

Stateful components have the React lifecycle methods whereas the Stateless one has only the `render()` method which is the default method for it.

## React Lifecycle Methods

These are methods called at different stages in the component’s lifecycle, which we can override to run our own code at those instances. We are utilizing the following methods in our application:

- `constructor()`  
Called before a component is mounted.
- `componentDidMount()`  
Invoked immediately after a component is mounted.
- `render()`  
The method which is called to render the JSX (HTML) content.
- `componentDidUpdate()`  
Called when the component is updated.
- `componentWillUnmount()`  
Invoked when a component is to be removed.

**Note**: *To learn more about Components and their lifecycle, [read the documentation here](https://reactjs.org/docs/react-component.html)*.

## JavaScript Promises

We are going to use [JavaScript Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) to get data from our WordPress REST API. First, we have the URL to the REST API in our *functions.php*, where we have appended it as a JavaScript variable which we can access from the front-end.

We will use JavaScript’s [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) method to get data from the different endpoints. We are adding a loader to show the user while the content is being fetched:

<p><div class="break-out">

<pre><code class="language-javascript">getMorePosts() {
       var that = this;
       var totalPages;

       // adding a loader
       jQuery("#loader").addClass("active");

       this.setState({ page: this.state.page + 1 });

       fetch(CelestialSettings.URL.api + "/posts/?page=" + this.state.page)
           .then(function (response) {
               for (var pair of response.headers.entries()) {

                   // getting the total number of pages
                   if (pair[0] == 'x-wp-totalpages') {
                       totalPages = pair[1];
                   }

                   if (that.state.page >= totalPages) {
                       that.setState({ getPosts: false })
                   }
               }
               if (!response.ok) {
                   throw Error(response.statusText);
               }
               return response.json();
           })
           .then(function (results) {
               var allPosts = that.state.posts.slice();
               results.forEach(function (single) {
                   allPosts.push(single);
               })
               that.setState({ posts: allPosts });

               // removing the loader
               jQuery("#loader").removeClass("active");

           }).catch(function (error) {
               console.log('There has been a problem with your fetch operation: ' + error.message);
               jQuery("#loader").remove();
           });
   }
</code></pre></div><br /><em>Fetching data from various endpoints, with loader to indicate process is running.</em></p>

## Using The React Router

React Router is the library that will handle client-side routing for our application. Server-side routing is possible with WordPress, but to achieve a truly SPA experience we need the help of [React Router](https://reacttraining.com/react-router/web/guides/philosophy).

Since version 4, React Router has been broken into three packages: `react-router`, `react-router-dom`, and `react-router-native`. We will be using `react-router-dom` for this project since that is the one used in web applications.

Since `react-router-dom` is installed already, we can write the router configuration inside the *index.jsx* file. The code will be as follows:

<p><div class="break-out">

<pre><code class="language-javascript">const App = () =&gt; (
   &lt;div id="page-inner"&gt;
       &lt;Header /&gt;
       &lt;div id="content"&gt;
           &lt;Switch&gt;
               &lt;Route exact path={CelestialSettings.path} component={Posts} /&gt;
               &lt;Route exact path={CelestialSettings.path + 'posts/:slug'} component={Post} /&gt;
               &lt;Route exact path={CelestialSettings.path + 'products'} component={Products} /&gt;
               &lt;Route exact path={CelestialSettings.path + 'products/:product'} component={Product} /&gt;
               &lt;Route path="&#42;" component={NotFound} /&gt;
           &lt;/Switch&gt;
       &lt;/div&gt;
       &lt;Footer /&gt;
   &lt;/div&gt;
);

// Routes
const routes = (
   &lt;Router&gt;
       &lt;Route path="/" component={App} /&gt;
   &lt;/Router&gt;
);

render(
   (routes), document.getElementById('page')
);
</code></pre></div><br /><em>Router configuration in the index.jsx file.</em></p>

The above code will take care of all routing, handled in the client side. The `*` in the last line says that any other route not mentioned above will take the user to the '404 Not Found' page.

The `<Link to="">` tag is used instead of the `<a href=””>` tag for linking between different pages using React Router:

<p><div class="break-out">

<pre><code class="language-javascript">&lt;div className="navbar-nav"&gt;
                       &lt;Link className="nav-item nav-link active" to={CelestialSettings.path} &gt;Home &lt;span className="sr-only"&gt;(current)&lt;/span&gt;&lt;/Link&gt;
                       &lt;Link className="nav-item nav-link" to={CelestialSettings.path + "products/"} &gt;Products&lt;/Link&gt;
&lt;/div&gt;
</code></pre></div><br /><em>Using the <code>&lt;Link to=""&gt;</code> tag for linking between different pages.</em></p>

## Getting Test Data

Now that you have created the theme, it is time to add some data. One way of adding data is to create our own content. However, there is an easier (and better) way to add data to our WordPress site. This method imports placeholder data from an external source:

- Head to [https://codex.wordpress.org/Theme_Unit_Test](https://codex.wordpress.org/Theme_Unit_Test) and download the [theme unit test data](https://raw.githubusercontent.com/WPTRT/theme-unit-test/master/themeunittestdata.wordpress.xml)
- Head over to **Tools > Import > WordPress** to install the WordPress importer.
- After the WordPress importer is installed, click on Run Importer.
- Click ‘Choose file’ in the importer
- Select the downloaded file and import the WordPress Theme Unit Test Data

Now you have to select the *theme-unit-test-data.xml* file and all the placeholder content is now on your site.

{{< rimg href="https://codex.wordpress.org/Theme_Unit_Test" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc28288b-6d0a-47ae-b36c-ede1b06fd20a/react-wp-app10.png" sizes="100vw" caption="When all the data is imported correctly." alt="Placeholder content imported successfully" >}}

## WooCommerce Integration

Now, we are ready to power our store using React. We will use the *products.jsx* and *product.jsx* files for this purpose, whose code is similar to *posts.jsx* and p*ost.jsx* respectively.

We will add three more variables to CelestialSettings under ‘woo’ (see A Global JavaScript Variable):

1. URL
2. `consumer_key`
3. `consumer_secret`

The Consumer key and Consumer secret have to be [generated](https://docs.woocommerce.com/document/woocommerce-rest-api/) from **Dashboard** → **WooCommerce** → **Settings** → **API** → **Keys/Apps**.

For the woo URL, you have to manually add it (since WooCommerce allows transfer only over SSL, add the URL with https, i.e. `https://localhost/celestial/wp-json/wc/v2/`).

Copy the Consumer key and Consumer secret and paste them in the appropriate places within *functions.php*. This will serve as the authentication for accessing WooCommerce via an API call.

Visit the [WooCommerce REST API documentation](https://woocommerce.github.io/woocommerce-rest-api-docs/#introduction) for more information about its API. The *products.jsx* file has the code for populating the store with products. The products can be added by an admin from the dashboard. Just go to **Dashboard** → **Products** → **Add New** and enter product details.

<figure><a href="https://docs.woocommerce.com/document/managing-products/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ca1381-26ba-47e8-b43b-e059ba054da4/react-wp-app12.png" width="" height="" alt="Add new product" /></a><figcaption>Add new product via the dashboard.</figcaption></figure>

When you click on a certain product, you will be taken to the *product.jsx* page:

<figure><a href="https://github.com/m-muhsin/celestial/blob/master/src/product.jsx"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbdf8f94-5900-4207-8324-6e7b16c7c113/react-wp-app9.png" width="" height="" alt="Individual product page" /></a><figcaption>Individual product page rendered based on the product.jsx file</figcaption></figure>

The code for the above page is similar to *post.jsx*:

<p><div class="break-out">

<pre><code class="language-javascript">renderProduct() {
       return (
           &lt;div className="card"&gt;
               &lt;div className="card-body"&gt;
                   &lt;div className="col-sm-4"&gt;&lt;img className="product-image" src={this.state.product.images ? this.state.product.images[0].src : null} alt={this.state.product.images ? this.state.product.images[0].alt : null } /&gt;&lt;/div&gt;
                   &lt;div className="col-sm-8"&gt;
                       &lt;h4 className="card-title"&gt;{this.state.product.name}&lt;/h4&gt;
                       &lt;p className="card-text"&gt;&lt;strike&gt;${this.state.product.regular_price}&lt;/strike&gt; &lt;u&gt;${this.state.product.sale_price}&lt;/u&gt;&lt;/p&gt;
                       &lt;p className="card-text"&gt;&lt;small className="text-muted"&gt;{this.state.product.stock_quantity} in stock&lt;/small&gt;&lt;/p&gt;
                       &lt;p className="card-text"&gt;{jQuery(this.state.product.description).text()}&lt;/p&gt;
                   &lt;/div&gt;
               &lt;/div&gt;
           &lt;/div&gt;
       );
   }
</code></pre></div><br /><em>Code for product.jsx file" alt="Code for product.jsx file</em></p>

## Permalinks

For the theme to work correctly, we have to set the following permalinks within **Dashboard** → **Settings** → **Permalinks**:

1. Under **Common Settings** → **Custom Structure**:
    `https://localhost/celestial/posts/%postname%/`

2. Under **Product permalinks** → **Custom base**:
    `/products/`

If you don’t set the permalinks as above, the theme may not function as desired.

## A WooCommerce Fix

When you navigate to *localhost/celestial/products*, chances are you will get a blank space where the products are supposed to be loaded. This happens because WooCommerce needs authenticated requests whereas our localhost is not https. To fix the issue:

1. Visit [https://localhost/celestial/wp-json/wc/v2/products](https://localhost/celestial/wp-json/wc/v2/products). This will give us a warning:

<figure><a href="https://github.com/m-muhsin/celestial/blob/master/src/product.jsx"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da1ad12b-3cd3-4bf7-8561-4da82de2facf/react-wp-app6.png" width="" height="" alt="Warning when localhost is not https" /></a><figcaption>WooCommerce requires authenticated requests and will show a warning if localhost is not https</figcaption></figure>

2. Click on **ADVANCED > Proceed to localhost (unsafe)**.
3. Now, if you go back to the products page, the items will be displayed correctly.

**Note**: *If you are on Valet on a Mac, you have to run Valet Secure on your site to secure the local site with a TLS certificate. This is another way of fixing the problem.*

## What Is ScrollMagic?

[ScrollMagic](https://scrollmagic.io/) is a library that allows us to perform certain actions when scrolling through the page. To use ScrollMagic we will enqueue the ScrollMagic JavaScript library in *functions.php*.  We are using ScrollMagic for two instances in this project:

<ol>
  <li>To lazy-load posts within the <em>posts.jsx</em> component:
<div class="break-out">

<pre><code class="language-javascript">componentDidMount() {
       var that = this;
       window.onbeforeunload = function () { window.scrollTo(0, 0); }

       // init ScrollMagic Controller
       that.state.controller = new ScrollMagic.Controller();

       // build scene
       var scene = new ScrollMagic.Scene({ triggerElement: "#colophon", triggerHook: "onEnter" })
           .addTo(that.state.controller)
           .on("enter", function (e) {
               if (that.state.getPosts &amp;&amp; that.getMorePosts !== null) {
                   that.getMorePosts();
               }
           });
   }
</code></pre></div><br /><em>Lazy-loading posts within the posts.jsx component</em></li>
<li>To show a fade-in animation for posts appearing by scrolling through posts and products in the <em>posts.jsx</em> and <em>products.jsx</em> components respectively:

<div class="break-out">

<pre><code class="language-javascript">componentDidUpdate() {
       var FadeInController = new ScrollMagic.Controller();
       jQuery('.posts-container .col-md-4.card-outer').each(function () {

           // build a scene
           var FadeInScene = new ScrollMagic.Scene({
               triggerElement: this.children[0],
               reverse: false,
               triggerHook: 1
           })
               .setClassToggle(this, 'fade-in')
               .addTo(FadeInController);
       });
   }
</code></pre></div><br /><em>Applying a fade-in animation for posts which appear as scrolling occurs</em></li>
</ol>

We are now ready to view our theme from the front-end. Navigate to *localhost/celestial* on your web browser and see your theme in action.

And pat yourself on the back, because you have now successfully created the theme!

### Other WordPress Themes With JavaScript Libraries

If you found this helpful, you can take a look at other awesome decoupled WordPress themes built using modern JavaScript libraries/frameworks:

- [Foxhound](https://github.com/ryelle/Foxhound): The first decoupled theme to make it to the WordPress themes repository. Written by [Kelly Dwan](https://ryelle.codes/), this theme uses React, Redux and React Router.
- [Anadama React](https://github.com/ryelle/anadama-react): Another theme by the same author, but using Flux instead of Redux, and Page instead of React Router.
- [Wallace](https://wallacetheme.com/): Written by [Kirby](https://github.com/bkirby989), this theme uses Angular with the WordPress REST API.
- [Picard](https://github.com/Automattic/Picard): Written by Automattic themselves to showcase the capability of the WordPress REST API.
- [React Verse](https://github.com/m-muhsin/react-verse): A React and Redux theme I wrote based on Foxhound.

## Next Steps

The main sections I wanted to show you are now done. You can continue with building the project for further knowledge. These are some recommendations that you could pursue:

1. A full-fledged store with the WooCommerce plugin, including checkout and shopping cart;
2. A page each for archive, tag, taxonomy, and so on;
3. State management with Redux or Flux.        

Good luck, and happy coding!

{{< signature "mc, ra, al, il" >}}

