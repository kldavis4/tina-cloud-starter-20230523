---
title: 'Write Your Next Web App With Ember CLI'
slug: write-next-web-app-ember-cli
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a70d01-893a-4706-81b4-894ed9954b3e/05-no-ember-app-opt.png
date: 2016-01-07T19:26:37.000Z
author: mitchlloyd
summary: >-
  Ember is a JavaScript web framework focused on building ambitious, rich client web applications. If you’ve been waiting to give Ember a try, why not start today with Ember CLI? It provides a productive and feature&ndash;rich development experience. All you need to get started and create an Ember App using Ember CLI is right here below.
description: >-
  Ember CLI is the Ember community’s shared solution for front&ndash;end tooling. Using Ember Addons, create an Ember App from scratch, through Testing to Production.
categories:
  - Coding
  - JavaScript
  - Frameworks
---
When you start a fresh web project or start digging into an existing code base, chances are you’re trying to create or enhance a feature for your users. The **last thing you want to do is spend time customizing build tools** and creating infrastructure to develop your application. If you land a new client, you want to show them features today, not in a week after you’ve cobbled together a build pipeline.

As you might already know, [Ember](https://www.smashingmagazine.com/2013/11/an-in-depth-introduction-to-ember-js/) is an “opinionated” JavaScript web framework focused on building ambitious, rich client web applications. Technologically, Ember has positioned itself as the [antidote to hype fatigue](https://brewhouse.io/blog/2015/05/13/emberjs-an-antidote-to-your-hype-fatigue.html). It’s a framework that [just won’t die](https://twitter.com/wycats/status/597772107510976512), but keeps pressing on with [each innovation](https://github.com/emberjs/ember.js/pull/10501) and with a commitment to backwards&ndash;compatibility.

[Ember CLI](https://www.ember-cli.com/) is the Ember community’s shared solution for front&ndash;end tooling. It provides a productive and feature&ndash;rich development experience out of the box.

## The Challenge Of Trivial Choices

On the face of it, front&ndash;end build tools appear too diverse for a shared solution. There are too many factors to account for, and every project has its own specials needs. As stated on React’s documentation page for “[Tooling Integration]("https://facebook.github.io/react/docs/tooling-integration.html)”, “Every project uses a different system for building and deploying JavaScript”.

Are you using Rails or .NET? What CSS preprocessor are you using? Does your application consist of a single page or “islands of richness”? Are you using JavaScript globals, asynchronous module definition (AMD), universal module definition (UMD), CommonJS or ECMAScript 6 modules? What testing framework do you prefer?

Because developers’ needs vary so much, low&ndash;level build tools such as Gulp, Grunt and Broccoli are often the starting point for front&ndash;end development. Yeoman, Lineman and Brunch take us further by generating the boilerplate needed for various use cases.

So, how is Ember CLI different? By making Ember CLI the official build tool for Ember, the community gets a default suite of tools that are integrated by 225 Ember CLI contributors and battle&ndash;tested around the clock by the Ember user community. These tools provide useful conventions, clear paths to best practices, and escape from the [burden of trivial choices](https://youtu.be/9naDS3r4MbY?t=1m47s). As [Chris Eppstein tweeted](https://twitter.com/chriseppstein/status/590211838782013440), referring to the Sass language, “It’s our belief that this consistency promotes a vibrant ecosystem and that it’s a bigger benefit than the ‘just right for me’ approach”.

Some developers might find it difficult to give up choice in favor of productivity. I argue that we must become experts in the domain in which we work and, for most developers, that domain is the intersection of the client’s business and maintainable application development. Frankly, I’ve never heard of a development team that created build tools they were happy with. However, I have seen custom build tools be disastrous for projects. You should try Ember CLI before attempting to build your own.

## New Opportunities

Ember CLI isn’t just about building assets better than before. When a community coalesces around a technology, new opportunities for productivity emerge. Here are a few innovations that have become possible with Ember CLI.

*   [Ember Addons](https://www.emberaddons.com/) These are libraries that can be installed in an Ember CLI application and that “just work” with zero configuration.
*   [Ember CLI Deploy](https://github.com/ember-cli/ember-cli-deploy) This is for conventional front-end deployment.
*   [Ember FastBoot](https://github.com/tildeio/ember-cli-fastboot) Render Ember applications on the server for faster initial page load.

Another side effect of Ember CLI is that developers receive the latest and greatest technology, without even needing to know it exists. Out of the box, Ember CLI applications have ECMAScript transpilation with Babel, live reloading during development, and a simple way to proxy AJAX requests to a local or remote server.

{{% feature-panel %}}

## Let’s Create An Ember App

Before creating an Ember CLI app, you’ll need to install Node.js. You can find out how to install it on the [Node.js website](https://nodejs.org/), or you can use the popular [Homebrew](https://brew.sh/) project if your computer runs Mac OS X:

<div class="break-out">

<pre><code class="language-bash">brew install node</code></pre>
</div>

Next, install Ember CLI itself:

<div class="break-out">

<pre><code class="language-bash">npm install -g ember-cli</code></pre>
</div>

With the prerequisites out of the way, you’re ready to create your first Ember application:

<div class="break-out">

<pre><code class="language-bash">ember new my-app</code></pre>
</div>

Once that’s finished, move to your app’s directory (`cd my-app`), run your app with `ember serve`, and visit `localhost:4200` to see your application in action.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2128bc08-a38c-445f-9233-962d4dc79ebd/01-default-app-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0269cffb-b8a3-45ee-9c33-66c39f62be3e/01-default-app-opt-small.png" width="800" height="331" alt="A freshly minted Ember CLI app showing on the Browser" /></a><figcaption>A freshly minted Ember CLI app. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2128bc08-a38c-445f-9233-962d4dc79ebd/01-default-app-opt.png">Large preview</a>)</figcaption></figure>

## Using Ember CLI

Using the blueprints feature of Ember CLI, let’s add some meat to our app and show a list of posts when a user visits the `/posts` URL. You can also follow along in the [accompanying GitHub repository](https://github.com/mitchlloyd/smashing-ember-cli-my-app/commits/master).

<div class="break-out">

<pre><code class="language-bash">ember g resource posts title:string body:string</code></pre>
</div>

This tells Ember CLI to generate a `posts` resource — it creates a `route` entry in your router, a route, a posts template and a post model. The post model will have title and body attributes that are cast to strings.

We’ll need to loop through our posts and render them in our `posts` template. The `each` helper makes this possible in `app/templates/posts.hbs`.

<div class="break-out">

<pre><code class="language-markup">{{#each model as |post|}}
  &lt;h3&gt;{{post.title}}&lt;/h3&gt;
  &lt;hr&gt;
  {{post.body}}
{{/each}}</code></pre>
</div>

Next, we’ll want to find our posts’ data and hand it off to the template when the user visits `/posts`. We’ll fetch the posts in the model hook of our posts route, located at `app/routes/posts.js`.

<div class="break-out">

<pre><code class="language-javascript">export default Ember.Route.extend({
  // Add this method
  model() {
    return this.store.findAll('post');
  }
});</code></pre>
</div>

You might notice that we’ve used ECMAScript 6’s shorthand syntax for objects to define the `model` method. Because Ember CLI uses a JavaScript transpiler by default, expect to see modern JavaScript code in most Ember applications.

We could have just written some JavaScript objects for the post data in our route here and called it a day, but let’s go a little further and actually fetch posts from a server.

We’ll generate an [Express](https://expressjs.com/) web server to serve up some data to our application.

<div class="break-out">

<pre><code class="language-bash">
ember g http-mock posts
</code></pre></div>

Then, we’ll return some dummy data from `/api/posts`. Edit the generated `server/mocks/posts.js` file to return some data from the index route.

<div class="break-out">

<pre><code class="language-javascript">postsRouter.get('/', function(req, res) {
  res.send({
    'posts': [
      // Add these objects
      { id: 1, title: 'First Post', body: 'Blogging' },
      { id: 2, title: 'Second Post', body: 'Blogging again' }
    ]
  });
});</code></pre>
</div>

The last thing we’ll need is a customized [Ember Data](https://github.com/emberjs/data) adapter.

<div class="break-out">

<pre><code class="language-bash">ember g adapter application</code></pre></div>

To make sure Ember Data knows to find the posts at `/api/posts`, we’ll add a namespace to our adapter in `app/adapters/application.js`.

<div class="break-out">

<pre><code class="language-javascript">export default DS.RESTAdapter.extend({
  namespace: 'api' // Add this
});</code></pre>
</div>

Now, if you visit `localhost:4200/posts`, you will see the posts in all their glory.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f568a5a3-71e3-4923-984e-a48ca7bd2073/02-posts-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48c85cf-ae72-44e1-af6b-ccc5b1d51988/02-posts-opt-small.png" width="800" height="435" alt="Browser shows a rendered list of posts" /></a><figcaption>Your client-rendered list of posts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f568a5a3-71e3-4923-984e-a48ca7bd2073/02-posts-opt.png">Large preview</a>)</figcaption></figure>

Of course, you’ll probably want to hook up your application to a real web server at some point in the development process. When you’re ready, you can remove the mock server and run your app with the proxy option:

<div class="break-out">

<pre><code class="language-bash">ember s --proxy https://localhost:3000</code></pre>
</div>

In this command, replace `https://localhost:3000` with your local or remote web server.

This is a great way to build your front end immediately and transition to a production web server later.

{{% ad-panel-leaderboard %}}

## Using Ember Addons

If you’re familiar with using [Bower](https://bower.io/) and [npm](https://www.npmjs.com/) to install dependencies, then Ember Addons might impress you.

Let’s install and use a date&ndash;picker in our Ember app. My date&ndash;picker of choice is [Pikaday](https://dbushell.github.io/Pikaday/). Luckily, several people have already integrated this library with Ember CLI. Here, we’ll use the `ember-pikaday` addon.

<div class="break-out">

<pre><code class="language-bash">ember install ember-pikaday</code></pre>
</div>

Now, let’s create a file at `app/templates/index.hbs` and try it out.

<div class="break-out">

<pre><code class="language-markup">{{pikaday-input value=date format='MM/DD/YYYY'}}
&lt;p&gt;You picked: {{date}}&lt;/p&gt;</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3296eb02-ecab-4b57-87f3-1b9cab4dae9f/03-pikaday-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c1c2971-8a2a-4386-9d75-0f8dff30660b/03-pikaday-opt-small.png" width="800" height="521" alt="Browser showing the date-picker Pikaday rendered as an Ember component" /></a><figcaption>A Pikaday date-picker rendered as an Ember component. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3296eb02-ecab-4b57-87f3-1b9cab4dae9f/03-pikaday-opt.png">Large preview</a>)</figcaption></figure>

This addon installed Pikaday and [Moment.js](https://momentjs.com/), it provided an Ember component named `{{pikaday-input}}`, and it included the Pikaday CSS in our build &mdash; all with a single installation command.

## Testing

Integrating your application code, a testing framework and a test runner can be challenging. You’ll want to run unit tests against isolated parts of the code and integrated tests against the running application. You’ll also want to run tests from the command line for continuous&ndash;integration testing on a build server.

Let’s write a test for the posts page that we made earlier. We’ll start by generating an acceptance test called “posts.”

<div class="break-out">

<pre><code class="language-bash">ember g acceptance-test posts</code></pre>
</div>

Now, you can visit `https://localhost:4200/tests` to see the running test.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8625663f-be33-4d53-bc85-d37bb99c7eb4/04-all-tests-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af3c012c-06a7-429e-887e-125179509d10/04-all-tests-opt-small.png" width="800" height="463" alt="Browser showing a list with passing tests" /></a><figcaption>Sixteen passed tests already.(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8625663f-be33-4d53-bc85-d37bb99c7eb4/04-all-tests-opt.png">Large preview</a>)</figcaption></figure>

We already have 16 tests? That’s right. Our generators from earlier each created a test to help us get started, and each of our files was tested with JSHint for errors.

Let’s fill out the generated acceptance test with something that tells us that all of our posts are rendered.

<div class="break-out">

<pre><code class="language-javascript">test('visiting /posts', function(assert) {
  visit('/posts');

  andThen(function() {
    var titles = find('h3').toArray().map((el) =&gt; el.textContent);
    assert.deepEqual(titles, ['First Post', 'Second Post'], "Has both titles");
  });
});</code></pre>
</div>

This test starts up our Ember app in an isolated portion of the test runner, visits the posts path and then asserts that each post title is on the page. The `andThen` helper waits for asynchronous processing to stop before making assertions.

If you’re not an avid tester, you might find yourself running out of excuses with Ember CLI. If you do get excited by testing, you’ll find it easy than ever to get started. The blueprints put current best practices at your fingertips, so that you don’t have to spend time Googling “how to test [x] in Ember.”

## Going To Production

Before shipping the code to production, you’ll want to optimize for speed, minify the code, fingerprint your assets and link those fingerprinted assets in the `index.html` file.

You can accomplish all of that with a single command, which puts your production&ndash;ready files into the `/dist` directory.

<div class="break-out">

<pre><code class="language-bash">ember build --environment="production"</code></pre>
</div>

Once your assets are built for production, the next step is to deploy them to a remote server. Many Ember CLI users choose to integrate these build files with the same deployment process they use for back&ndash;end server code. However, an emerging best practice, [refined and championed by Luke Melia](https://youtu.be/4EDetv_Rw5U?t=11m1s), is to **use a separate front&ndash;end deployment workflow** that allows your Ember application to be deployed independently of your server code.

At EmberConf 2015, [Luke announced](https://youtu.be/4EDetv_Rw5U?t=18m59s) that the maintainers of prominent addons for deployment had joined forces to create one addon under the name Ember CLI Deploy. The newly formed team released its first joint effort, version 0.5.0 of the addon.

Ember CLI Deploy embraces a **“core and plugins” architecture**. The add&ndash;on provides the deployment workflow, but users install different plugins according to the exact infrastructure they use. For instance, one setup proposed by Luke uses Amazon’s S3 service to host files and Redis to store and link the Ember application’s `index.html` file.

You can install the current addon using the same installation command we saw before:

<div class="break-out">

<pre><code class="language-bash">ember install ember-cli-deploy</code></pre>
</div>

We’ll also install ember&ndash;cli&ndash;build to build our application for production.

<div class="break-out">

<pre><code class="language-bash">ember install ember-cli-build</code></pre>
</div>

From there, you can install the asset&ndash;adapter plugin that you need:

<div class="break-out">

<pre><code class="language-bash">ember install ember-cli-deploy-s3</code></pre>
</div>

Then, you’ll need to install an index&ndash;adapter plugin, which provides a way to link your `index.html` file to the server:

<div class="break-out">

<pre><code class="language-bash">ember install ember-cli-deploy-redis</code></pre>
</div>

Finally, you can edit your `config/deploy.js` file to include information about Redis and S3, so that Ember CLI Deploy can interact with these services.

With those adapters installed and configured, you can deploy with one command.

<div class="break-out">

<pre><code class="language-bash">ember deploy production --activate</code></pre>
</div>

This command will:

-   build your assets for production,
-   upload your JavaScript and CSS assets to S3,
-   upload your `index.html` file to Redis,
-   “activate” the last `index.html` file that was uploaded.

In this sequence of events, only the last step, activation, changes the version of the Ember application that is served to users. Previous versions of `index.html` are stored on Redis, and previous versions of your assets are stored on S3. To switch the version of the running Ember application, developers use the `activate` command to tell their server to use a particular `index.html` file that is pointing to single set of assets stored on S3.

<div class="break-out">

<pre><code class="language-bash">ember deploy:activate production --revision 44f2f92</code></pre>
</div>

To learn more about how you can deploy an Ember application with your infrastructure, checkout the documentation for ember&ndash;cli&ndash;deploy.

{{% ad-panel-leaderboard %}}

## Not Just For Ember

All of that talk about eliminating trivial choices might have left you with the impression that Ember CLI isn’t flexible or configurable. Because Ember CLI needs to accommodate a wide range of use cases from the community, it has a well&ndash;defined public interface for customization. In fact, despite the name, Ember isn’t a requirement for Ember CLI. For instance, the Firefox OS team has used Ember CLI with an [addon that it created](https://github.com/mozilla/ember-cli-fxos), rather than create its own build tool.

Suppose you want all of the wonderful features of Ember CLI without Ember. Again, you can follow along in the [accompanying GitHub repository](https://github.com/mitchlloyd/smashing-ember-cli-no-ember/commits/master) if you like. We’ll start with a new Ember CLI application:

<div class="break-out">

<pre><code class="language-bash">ember new no-ember</code></pre></div>

Next, we’ll get rid of Ember so that it isn’t in our JavaScript build. We’ll remove Ember and Ember Data from the `bower.json` file.

<div class="break-out">

<pre><code class="language-javascript">// In bower.json
{
  …
  "dependencies": {
    "ember": "2.2.0", // Delete
    …
    "ember-data": "^2.2.1", // Delete
    …
  },
  "resolutions": {
    "ember": "2.2.0" // Delete
  }
}</code></pre>
</div>

We also need to remove Ember Data from the `package.json` file.

<div class="break-out">

<pre><code class="language-javascript">// In package.json
{
  …
  "devDependencies": {
    …
    "ember-data": "^2.2.1", // Delete
    …
  }
}</code></pre>
</div>

Next, let’s delete most of the things in our application directory. To have a working application, we only need, `styles`, `app.js` and `index.html`.

<div class="break-out">

<pre><code class="language-bash">app/
├── app.js
├── index.html
└── styles</code></pre>
</div>

Ember CLI is expecting us to export an object from `app.js` that has a `create` method which mirrors the interface to an `Ember.Application`. Let’s replace the default content in that file with a simple exported object.

<div class="break-out">

<pre><code class="language-javascript">export default {
  create() {
  }
};</code></pre>
</div>

Finally, let’s create an ECMAScript 6 module that renders something in our application.

In `app/modules/render-something.js`, we’ll export a function that renders some content.

<div class="break-out">

<pre><code class="language-javascript">export default function renderSomething() {
  document.write("Who needs a framework?");
}</code></pre>
</div>

You can put the modules wherever you want in the `app` directory. You’ll use the same path when importing from your application’s namespace. Here is how we can import and use that module in our `app.js` file:

<div class="break-out">

<pre><code class="language-javascript">import renderSomething from 'no-ember/modules/render-something';

export default {
  create() {
    renderSomething();
  }
};</code></pre>
</div>

Now you can see your web app running at `https://localhost:4200`.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a70d01-893a-4706-81b4-894ed9954b3e/05-no-ember-app-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9cc906-8b12-4534-8618-f4687391111e/05-no-ember-app-opt-small.png" width="800" height="331" alt="Browser shows a web app with the sentence Who needs a Frameork?"/></a><figcaption>A pure and simple web app, free from framework tyranny.(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a70d01-893a-4706-81b4-894ed9954b3e/05-no-ember-app-opt.png">Large preview</a>)</figcaption></figure>

## The Future Of Ember CLI

Without question, Ember CLI is here to stay. Although the Ember community was the first of the modern front&ndash;end framework communities to take build tools into their own hands, others have begun to follow suite. AngularJS 2.0 has its own CLI tool, [angular&ndash;cli](https://github.com/angular/angular-cli), which is an Ember CLI addon. Because React has a narrower scope than AngularJS 2.0 or Ember, an official build tool is not planned, but something promising will hopefully emerge from its [current ecosystem of tools](https://github.com/facebook/react/wiki/Complementary-Tools#build-tools).

If you’ve been waiting to give Ember a try, why not start today with Ember CLI? All you need to get started is this:

<div class="break-out">

<pre><code class="language-bash">npm install -g ember-cli
ember new my-first-ember-project</code></pre>
</div>

### References

*   [Ember CLI](https://www.ember-cli.com/) The official documentation
*   “[Building Custom Apps With Ember CLI](https://www.youtube.com/watch?v=J6vPwvFdUiE)” (video), Brittany Storoz, EmberConf 2015 Storoz talks about using Ember CLI at Mozilla.
*   “[Keynote: 10 Years!](https://www.youtube.com/watch?v=9naDS3r4MbY)” (video), Yehuda Katz, RailsConf 2015 Katz explains why choices can be harmful.

## Further Reading on Smashing Magazine:

- “[React To The Future With Isomorphic Apps](https://www.smashingmagazine.com/2015/04/react-to-the-future-with-isomorphic-apps/),” Jonathan Creamer
- “[An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/),” Alejandro Hernandez
- “[Journey Through The JavaScript MVC Jungle](https://www.smashingmagazine.com/2012/07/journey-through-the-javascript-mvc-jungle/),” Addy Osmani
- “[Styled Components: Enforcing Best Practices In Component-Based Systems](https://www.smashingmagazine.com/2017/01/styled-components-enforcing-best-practices-component-based-systems/),” Max Stoiber

{{< signature "rb, ml, al, nl" >}}
