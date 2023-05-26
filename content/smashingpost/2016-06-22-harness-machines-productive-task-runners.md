---
title: 'How To Harness The Machines: Being Productive With Task Runners'
slug: harness-machines-productive-task-runners
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40bc16a2-b008-49fc-9fb7-1f65afa16be6/00-sublime-preview-opt.jpg
date: 2016-06-22T18:13:58.000Z
author: adamsimpson
description: >-
  Task runners are the heroes (or villains, depending on your point of view)
  that quietly toil behind most web and mobile applications. Task runners
  provide value through the automation of numerous development tasks such as
  concatenating files, spinning up development servers and compiling code.

  In this article, we’ll cover Grunt, Gulp, Webpack and npm scripts. We’ll also
  provide some examples of each one to get you started. Near the end, I’ll throw
  out some easy wins and tips for integrating ideas from this post into your
  application.
categories:
  - Mobile
  - JavaScript
  - Node.js
---
Task runners are the heroes (or villains, depending on your point of view) that quietly toil behind most web and mobile applications. Task runners provide value through the automation of numerous development tasks such as concatenating files, spinning up development servers and compiling code. In this article, we’ll cover Grunt, Gulp, Webpack and npm scripts. We’ll also provide some examples of each one to get you started. Near the end, I’ll throw out some easy wins and tips for integrating ideas from this post into your application.

There is a sentiment that task runners, and JavaScript advances in general, are over-complicating the front-end landscape. I agree that spending the entire day tweaking build scripts isn’t always the best use of your time, but task runners have some benefits when used properly and in moderation. That’s our goal in this article, to quickly cover the basics of the most popular task runners and to provide solid examples to kickstart your imagination regarding how these tools can fit in your workflow.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Become A Command-Line Power User With Oh-My-ZSH And Z](https://www.smashingmagazine.com/2015/07/become-command-line-power-user-oh-my-zsh-z/)
*   [An Introduction To PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)
*   [Get Up And Running With Grunt](https://www.smashingmagazine.com/2013/10/get-up-running-grunt/)
*   [Building With Gulp](https://www.smashingmagazine.com/2014/06/building-with-gulp/)

### A Note on the Command Line

Task runners and build tools are primarily command-line tools. Throughout this article, I’ll assume a decent level of experience and competence in working with the command line. If you understand how to use common commands like <code>cd</code>, <code>ls</code>, <code>cp</code> and <code>mv</code>, then you should be all right as we go through the various examples. If you don’t feel comfortable using these commands, a great <a href="https://www.smashingmagazine.com/2012/01/introduction-to-linux-commands/">introductory post is available</a> on Smashing Magazine. Let’s kick things off with the granddaddy of them all: Grunt.

{{% feature-panel %}}

## Grunt

<a href="https://gruntjs.com">Grunt</a> was the first popular JavaScript-based task runner. I’ve been using Grunt in some form since 2012. The basic idea behind Grunt is that you use a special JavaScript file, <code>Gruntfile.js</code>, to configure various plugins to accomplish tasks. It has a vast ecosystem of plugins and is a very mature and stable tool. Grunt has a <a href="https://gruntjs.com/plugins">fantastic web directory</a> that indexes the majority of plugins (about 5,500 currently). The simple genius of Grunt is its combination of JavaScript and the idea of a common configuration file (like a makefile), which has allowed many more developers to contribute to and use Grunt in their projects. It also means that Grunt can be placed under the same version control system as the rest of the project.

Grunt is battle-tested and stable. Around the time of writing, <a href="https://gruntjs.com/blog/2016-02-11-grunt-1.0.0-rc1-released">version 1.0.0 was released</a>, which is a huge accomplishment for the Grunt team. Because Grunt largely configures various plugins to work together, it can get tangled (i.e. messy and confusing to modify) pretty quickly. However, with a little care and organization (breaking tasks into logical files!), you can get it to do wonders for any project.

In the rare case that a plugin isn’t available to accomplish the task you need, Grunt provides <a href="https://gruntjs.com/creating-plugins">documentation on how to write your own plugin</a>. All you need to know to create your own plugin is JavaScript and the <a href="https://gruntjs.com/api/grunt">Grunt API</a>. You’ll almost never have to create your own plugin, so let’s look at how to use Grunt with a pretty popular and useful plugin!

### An Example

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95e635d-e5c5-4ee7-a88d-faee6a4b65d3/01-grunt-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc25ef4a-3ada-4547-afcd-62379d65e580/01-grunt-example-preview-opt.png" alt="Screenshot of the grunt-example directory" width="500" height="463" /></a><figcaption>What our Grunt directory looks like (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95e635d-e5c5-4ee7-a88d-faee6a4b65d3/01-grunt-example-opt.png">View large version</a>)</figcaption></figure>

Let’s look at how Grunt actually works. Running <code>grunt</code> in the command line will trigger the Grunt command-line program that looks for <code>Gruntfile.js</code> in the root of the directory. The <code>Gruntfile.js</code> contains the configuration that controls what Grunt will do. In this sense, <code>Gruntfile.js</code> can be seen as a kind of cookbook that the cook (i.e. Grunt, the program) follows; and, like any good cookbook, <code>Gruntfile.js</code> will contain many recipes (i.e. tasks).

We’re going to put Grunt through the paces by using the <a href="https://github.com/filamentgroup/grunticon">Grunticon plugin</a> to generate icons for a hypothetical web app. Grunticon takes in a directory of SVGs and spits out several assets:

*   a CSS file with the SVGs base-64-encoded as background images;
*   a CSS file with PNG versions of the SVGs base-64-encoded as background images;
*   a CSS file that references an individual PNG file for each icon.

The three different files represent the various capabilities of browsers and mobile devices. Modern devices will receive the high-resolution SVGs as a single request (i.e. a single CSS file). Browsers that don’t handle SVGs but handle base-64-encoded assets will get the base-64 PNG style sheet. Finally, any browsers that can’t handle those two scenarios will get the “traditional” style sheet that references PNGs. All this from a single directory of SVGs!

The configuration of this task looks like this:

<pre><code class="language-json">module.exports = function(grunt) {

  grunt.config("grunticon", {
    icons: {
      files: [
        {
          expand: true,
          cwd: 'grunticon/source',
          src: ["*.svg", ".png"],
          dest: 'dist/grunticon'
        }
      ],
      options: [
        {
          colors: {
            "blue": "blue"
          }
        }
      ]
    }
  });

  grunt.loadNpmTasks('grunt-grunticon');
};</code></pre>

Let’s walk through the various steps here:

1.  You must [have Grunt installed globally](https://gruntjs.com/getting-started).
2.  Create the `Gruntfile.js` file in the root of the project. It’s best to also install Grunt as an npm dependency in your `package.json` file along with Grunticon via `npm i grunt grunt-grunticon --save-dev`.
3.  Create a directory of SVGs and a destination directory (where the built assets will go).
4.  Place a [small script in the `head`](https://github.com/filamentgroup/grunticon/blob/master/site/src/js/head.js) of your HTML, which will determine what icons to load.

Here is what your directory should look like before you run the Grunticon task:

<pre><code class="language-json">
|-- Gruntfile.js
|-- grunticon
|   `-- source
|       `-- logo.svg
`-- package.json
</code>
</pre>

Once those things are installed and created, you can copy the code snippet above into <code>Gruntfile.js</code>. You should then be able to run <code>grunt grunticon</code> from the command line and see your task execute.

The snippet above does a few things:

*   adds a new `config` object to Grunt on line 32 named `grunticon`;
*   fills out the various options and parameters for Grunticon in the `icons` object;
*   finally, pulls in the Grunticon plugin via `loadNPMTasks`.

Here is what your directory should look like post-Grunticon:

<pre><code class="language-json">
|-- Gruntfile.js
|-- dist
|   `-- grunticon
|       |-- grunticon.loader.js
|       |-- icons.data.png.css
|       |-- icons.data.svg.css
|       |-- icons.fallback.css
|       |-- png
|       |   `-- logo.png
|       `-- preview.html
|-- grunticon
|   `-- source
|       `-- logo.svg
`-- package.json
</code>
</pre>

There you go — finished! In a few lines of configuration and a couple of package installations, we’ve automated the generation of our icon assets! Hopefully, this begins to illustrate the power of task runners: reliability, efficiency and portability.</p>

## Gulp: LEGO Blocks For Your Build System

Gulp emerged sometime after Grunt and aspired to be a build tool that wasn’t all configuration but actual code. The idea behind code over configuration is that code is much more expressive and flexible than the modification of endless config files. The hurdle with Gulp is that it requires more technical knowledge than Grunt. You will need to be familiar with the <a href="https://nodejs.org/api/stream.html">Node.js streaming API</a> and be comfortable writing basic JavaScript.

Gulp’s use of Node.js streams is the main reason it’s faster than Grunt. Using streams means that, instead of using the file system as the “database” for file transformations, Gulp uses in-memory transformations. For more information on streams, check out the <a href="https://nodejs.org/api/stream.html">Node.js streams API documentation</a>, along with the <a href="https://github.com/substack/stream-handbook">stream handbook</a>.</p>

### An Example

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87a613a1-850e-44c8-9a2a-a03592fcf13b/02-gulp-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c49ccf4-c943-4e64-b31a-2b0c96e8e366/02-gulp-example-preview-opt.png" alt="Screenshot of the Gulp example directory" width="500" height="463" /></a><figcaption>What our Gulp directory looks like (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87a613a1-850e-44c8-9a2a-a03592fcf13b/02-gulp-example-opt.png">View large version</a>)</figcaption></figure>

As in the Grunt section, we’re going to put Gulp through the paces with a straightforward example: concatenating our JavaScript modules into a single app file.

Running Gulp is the same as running Grunt. The <code>gulp</code> command-line program will look for the cookbook of recipes (i.e. <code>Gulpfile.js</code>) in the directory in which it’s run.

Limiting the number of requests each page makes is considered a web performance best practice (especially on mobile). Yet collaborating with other developers is much easier if functionality is split into multiple files. Enter task runners. We can use Gulp to combine the multiple files of JavaScript for our application so that mobile clients have to load a single file, instead of many.

Gulp has the same massive ecosystem of plugins as Grunt. So, to make this task easy, we’re going to lean on the <a href="https://github.com/contra/gulp-concat">gulp-concat plugin</a>. Let’s say our project’s structure looks like this:

<pre><code class="language-json">|-- dist
|   `-- app.js
|-- gulpfile.js
|-- package.json
`-- src
    |-- bar.js
    `-- foo.js</code></pre>

Two JavaScript files are in our <code>src</code> directory, and we want to combine them into one file, <code>app.js</code>, in our <code>dist/</code> directory. We can use the following Gulp task to accomplish this.</p>

<pre><code class="language-javascript">var gulp = require('gulp');
var concat = require('gulp-concat');

gulp.task('default', function() {
  return gulp.src('./src/*.js')
    .pipe(concat('app.js'))
    .pipe(gulp.dest('./dist/'));
});</code></pre>

The important bits are in the <code>gulp.task</code> callback. There, we use the <a href="https://github.com/gulpjs/gulp/blob/master/docs/API.md#gulpsrcglobs-options"><code>gulp.src</code> API</a> to get all of the files that end with <code>.js</code> in our <code>src</code> directory. The <code>gulp.src</code> API returns a stream of those files, which we can then pass (via the <a href="https://nodejs.org/api/stream.html#stream_readable_pipe_destination_options"><code>pipe</code> API</a>) to the gulp-concat plugin. The plugin then concatenates all of the files in the stream and passes it on to the <a href="https://github.com/gulpjs/gulp/blob/master/docs/API.md#gulpdestpath-options"><code>gulp.dest</code></a> function. The <code>gulp-dest</code> function simply writes the input it receives to disk.

You can see how Gulp uses streams to give us “building blocks” or “chains” for our tasks. A typical Gulp workflow looks like this:

1.  Get all files of a certain type.
2.  Pass those files to a plugin (concat!), or do some transformation.
3.  Pass those transformed files to another block (in our case, the `dest` block, which ends our chain).

As in the Grunt example, simply running <code>gulp</code> from the root of our project directory will trigger the <code>default</code> task defined in the <code>Gulpfile.js</code> file. This task concatenates our files and let’s us get on with developing our app or website.</p>

## Webpack

The newest addition to the JavaScript task runner club is <a href="https://webpack.github.io">Webpack</a>. Webpack bills itself as a “module bundler,” which means it can dynamically build a bundle of JavaScript code from multiple separate files using module patterns such as the <a href="https://webpack.github.io/docs/commonjs.html">CommonJS</a> pattern. Webpack also has plugins, which it calls <a href="https://webpack.github.io/docs/using-loaders.html">loaders</a>.

Webpack is still fairly young and has rather dense and confusing documentation. Therefore, I’d recommend <a href="https://github.com/petehunt/webpack-howto">Pete Hunt’s Webpack repository</a> as a great starting point before diving into the official documentation. I also wouldn’t recommend Webpack if you are new to task runners or don’t feel proficient in JavaScript. Those issues aside, it’s still a more specific tool than the general broadness of Grunt and Gulp. Many people use Webpack alongside Grunt or Gulp for this very reason, letting Webpack excel at bundling modules and letting Grunt or Gulp handle more generic tasks.

Webpack ultimately lets us write Node.js-style code for the browser, a great win for productivity and making a clean separation of concerns in our code via modules. Let’s use Webpack to achieve the same result as we did with the Gulp example, combining multiple JavaScript files into one app file.</p>

### An Example

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768d362f-0f6f-4e17-b7f8-e3dfaa71a3dd/03-webpack-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0325c661-5cb1-438b-b29a-bd7e52ffeeeb/03-webpack-example-preview-opt.png" alt="Screenshot of the webpack-example directory" width="500" height="463" /></a><figcaption>What our Webpack directory looks like (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768d362f-0f6f-4e17-b7f8-e3dfaa71a3dd/03-webpack-example-opt.png">View large version</a>)</figcaption></figure>

Webpack is often used with <a href="https://babeljs.io">Babel</a> to transpile ES6 code to ES5. Transpiling code from ES6 to ES5 lets developers use the emerging ES6 standard while serving up ES5 to browsers or environments that don’t fully support ES6 yet. However, in this example, we’ll focus on building a simple bundle of our two files from the Gulp example. To begin, we need to install Webpack and create a config file, <code>webpack.config.js</code>. Here’s what our file looks like:

<pre><code class="language-javascript">module.exports = {
    entry: "./src/foo.js",
    output: {
        filename: "app.js",
        path: "./dist"
    }
};</code></pre>

In this example, we’re pointing Webpack to our <code>src/foo.js</code> file to begin its work of walking our dependency graph. We’ve also updated our <code>foo.js</code> file to look like this:

<pre><code class="language-javascript">//foo.js
var bar = require("./bar");

var foo = function() {
  console.log('foo');
  bar();
};

module.exports = foo;</code></pre>

And we’ve updated our <code>bar.js</code> file to look like this:

<pre><code class="language-javascript">//bar.js
var bar = function() {
  console.log('bar');
};

module.exports = bar;</code></pre>

This is a very basic CommonJS example. You’ll notice that these files now “export” a function. Essentially, CommonJS and Webpack allow us to begin organizing our code into self-contained modules that can be imported and exported throughout our application. Webpack is smart enough to follow the import and export keywords and to bundle everything into one file, <code>dist/app.js</code>. We no longer need to maintain a concatenation task, and we simply need to adhere to a structure for our code instead. Much better!

### Extending

Webpack is akin to Gulp in that “It’s just JavaScript.” It can be extended to do other task runner tasks via its loader system. For instance, you can use <a href="https://github.com/webpack/css-loader">css-loader</a> and <a href="https://github.com/jtangelder/sass-loader">sass-loader</a> to compile Sass into CSS and even to use the Sass in your JavaScript by <a href="https://webpack.github.io/docs/stylesheets.html#using-css">overloading the <code>require</code> CommonJS pattern</a>! However, I typically advocate for using Webpack solely to build JavaScript modules and for using another more general-purpose approach for task running (for example, Webpack and npm scripts or Webpack and Gulp to handle everything else).</p>

## npm Scripts

<a href="https://docs.npmjs.com/misc/scripts">npm scripts</a> are the latest hipster craze, and for good reason. As we’ve seen with all of these tools, the number of dependencies they might introduce to a project could eventually spin out of control. The first post I saw advocating for npm scripts as the entry point for a build process was by <a href="https://github.com/substack">James Halliday</a>. <a href="https://substack.net/task_automation_with_npm_run">His post</a> perfectly sums up the ignored power of npm scripts (emphasis mine):
<blockquote>There are some fancy tools for doing build automation on JavaScript projects that I’ve never felt the appeal of because the lesser-known <code>npm run</code> command has been perfectly adequate for everything I’ve needed to do while maintaining a <strong>very tiny configuration footprint</strong>.</blockquote>

Did you catch that last bit at the end? The primary appeal of npm scripts is that they have a “very tiny configuration footprint.” This is one of the main reasons why npm scripts have started to catch on (almost four years later, sadly). With Grunt, Gulp and even Webpack, one eventually begins to drown in plugins that wrap binaries and double the number of dependencies in a project.

Keith Cirkel has the <a href="https://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/">go-to tutorial</a> on using npm to replace Grunt or Gulp. He provides the blueprint for how to fully leverage the power of npm scripts, and he’s introduced an essential plugin, <a href="https://github.com/keithamus/parallelshell">Parallel Shell</a> (and a <a href="https://github.com/mysticatea/npm-run-all/issues/10">host of others</a> just like it).</p>

### An Example

In our section about Grunt, we took the popular module Grunticon and created SVG icons (with PNG fallbacks) in a Grunt task. This used to be the one pain point with npm scripts for me. For a while, I would keep Grunt installed for projects just to use Grunticon. I would literally “shell out” to Grunt in my npm task to achieve task-runner inception (or, as we started calling it at work, a build-tool turducken). Thankfully, <a href="https://www.filamentgroup.com">The Filament Group</a>, the fantastic group behind Grunticon, released a standalone (i.e. Grunt-free) version of their tool, <a href="https://github.com/filamentgroup/grunticon-lib">Grunticon-Lib</a>. So, let’s use it to create some icons with npm scripts!

This example is a little more advanced than a typical npm script task. A typical npm script task is a call to a command-line tool, with the appropriate flags or config file. Here’s a more typical task that compiles our Sass to CSS:

<pre><code class="language-json">"sass": "node-sass src/scss/ -o dist/css",</code></pre>

See how it’s just one line with various options? No task file needed, no build tool to spin up — just <code>npm run sass</code> from the command line, and you’re Sass is now CSS. One really nice feature of npm scripts is how you can chain script tasks together. For instance, say we want to run some task before our Sass task runs. We would create a new script entry like this:

<pre><code class="language-json">"presass": "echo 'before sass',</code></pre>

That’s right: npm understands the <code>pre-</code> prefix. It also understands the <code>post-</code> prefix. Any script entry with the same name as another script entry with a <code>pre-</code> or <code>post-</code> prefix will run before or after that entry.

Converting our icons will require an actual Node.js file. It’s not too serious, though. Just create a <code>tasks</code> directory, and create a new file named <code>grunticon.js</code> or <code>icons.js</code> or whatever makes sense to those working on the project. Once the file is created, we can write some JavaScript to fire off our Grunticon process.

Note: All of these examples use ES6, so we’re going to use babel-node to run our task. You can easily use ES5 and Node.js, if that’s more comfortable.</p>

<pre><code class="language-javascript">import icons from "grunticon-lib";
import globby from "globby";

let files = globby.sync('src/icons/*');
let options = {
  colors: {
    "blue": "blue"
  }
};

let icon = new icons(files, 'dist/icons', options);

icon.process();</code></pre>

Let’s get into the code and figure out what’s going on.

1.  We `import` (i.e. require) two libraries, `grunticon-lib` and `globby`. [Globby](https://github.com/sindresorhus/globby) is one of my favorite tools, and it makes working with files and globs so easy. Globby enhances [Node.js Glob](https://github.com/isaacs/node-glob) (select all JavaScript files via `./*.js`) with Promise support. In this case, we’re using it to get all files in the `src/icons` directory.
2.  Once we do that, we set a few options in an `options` object and then call Grunticon-Lib with three arguments:
    *   the icon files,
    *   the destination,
    *   the options.The library takes over and chews away on those icons and eventually creates the SVGs and PNG versions in the directory we want.
3.  We’re almost done. Remember that this is in a separate file, and we need to add a “hook” to call this file from our npm script, like this: `"icons": "babel-node tasks/icons.js"`.
4.  Now we can run `npm run icons`, and our icons will get created every time.

npm scripts offer a similar level of power and flexibility as other task runners, without the plugin debt.</p>

## Breakdown Of Task Runners Covered Here

<table class="tablesaw">
<thead>
<tr>
<th>Tool</th>
<th>Pros</th>
<th>Cons</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://gruntjs.com">Grunt</a></td>
<td>No real programming knowledge needed</td>
<td>The most verbose of the task runners covered here</td>
</tr>
<tr>
<td><a href="https://gulpjs.com">Gulp</a></td>
<td>Configure tasks with actual JavaScript and streams</td>
<td>Requires knowledge of JavaScript</td>
</tr>
<tr>
<td></td>
<td></td>
<td>Adds code to a project (potentially more bugs)</td>
</tr>
<tr>
<td><a href="https://webpack.github.io">Webpack</a></td>
<td>Best in class at module-bundling</td>
<td>More difficult for more generic tasks (for example, Sass to CSS)</td>
</tr>
<tr>
<td>npm scripts</td>
<td>Direct interaction with command-line tools.</td>
<td>Some tasks aren’t possible without a task runner.</td>
</tr>
</tbody>
</table>

## Some Easy Wins

All of these examples and task runners might seem overwhelming, so let’s break it down. First, I hope you don’t take away from this article that whatever task runner or build system you are currently using needs to be instantly replaced with one mentioned here. Replacing important systems like this shouldn’t be done without much consideration. Here’s my advice for upgrading an existing system: Do it incrementally.</p>

### Wrapper Scripts!

One incremental approach is to look at writing a few “wrapper” npm scripts around your existing task runners to provide a common vocabulary for build steps that is outside of the actual task runner used. A wrapper script could be as simple as this:

<pre><code class="language-json">{
  "scripts": {
    "start": "gulp"
  }
}</code></pre>

Many projects utilize the <code>start</code> and <code>test</code> npm script blocks to help new developers get acclimatized quickly. A wrapper script does introduce another layer of abstraction to your task runner build chain, yet I think it’s worth being able to standardize around the npm primitives (e.g. <code>test</code>). The npm commands have better longevitiy than an individual tool.</p>

### Sprinkle in a Little Webpack

If you or your team are feeling the pain of maintaining a brittle “bundle order” for your JavaScript, or you’re looking to upgrade to ES6, consider this an opportunity to introduce Webpack to your existing task-running system. Webpack is great in that you can use as much or as little of it as you want and yet still derive value from it. Start just by having it bundle your application code, and then add babel-loader to the mix. Webpack has such a depth of features that it’ll be able to accommodate just about any additions or new features for quite some time.</p>

### Easily Use PostCSS With npm Scripts

<a href="https://github.com/code42day/postcss-cli">PostCSS</a> is a great collection of plugins that transform and enhance CSS once it’s written and preprocessed. In other words, it’s a post-processor. It’s easy enough to leverage PostCSS using npm scripts. Say we have a Sass script like in our previous example:

<pre><code class="language-json">"sass": "node-sass src/scss/ -o dist/css",</code></pre>

We can use npm script’s <code>lifecycle</code> keywords to add a script to run automatically after the Sass task:

<pre><code class="language-json">"postsass": "postcss --use autoprefixer -c postcss.config.json dist/css/*.css -d dist/css",</code></pre>

This script will run every time the Sass script is run. The postcss-cli package is great, because you can <a href="https://github.com/code42day/postcss-cli#--config-c">specify configuration</a> in a separate file. Notice that in this example, we add another script entry to accomplish a new task; this is a common pattern when using npm scripts. You can create a workflow that accomplishes all of the various tasks your app needs.</p>

## Conclusion

Task runners can solve real problems. I’ve used task runners to compile different builds of a JavaScript application, depending on whether the target was production or local development. I’ve also used task runners to compile <a href="https://handlebarsjs.com">Handlebars</a> templates, to deploy a website to production and to automatically add vendor prefixes that are missed in my Sass. These are not trivial tasks, but once they are wrapped up in a task runner, they became effortless.

Task runners are constantly evolving and changing. I’ve tried to cover the most used ones in the current zeitgeist. However, there are others that I haven’t even mentioned, such as <a href="https://github.com/broccolijs/broccoli">Broccoli</a>, <a href="https://brunch.io">Brunch</a> and <a href="https://harpjs.com">Harp</a>. Remember that these are just tools: Use them only if they solve a particular problem, not because everyone else is using them. Happy task running!

{{< signature "da, ml, al, il" >}}

