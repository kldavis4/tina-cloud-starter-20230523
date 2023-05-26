---
title: 'How To Build And Develop Websites With Gulp'
slug: building-with-gulp
author: callummacrae
image:
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16514ddb-b52b-4eae-849d-0b739b2606f4/gulp-intro.png
date: 2014-06-11T22:32:55.000Z
description: >-
  Gulp is one of quite a few build tools available in JavaScript, and other build tools not written in JavaScript are available, too, including Rake. Why should you choose it?
summary: >-
  Gulp is one of quite a few build tools available in JavaScript, and other build tools not written in JavaScript are available, too, including Rake. Why should you choose it?
categories:
  - Coding
  - Tools
  - Workflow
  - JavaScript
  - Optimization
---
Optimizing your website assets and testing your design across different browsers is certainly not the most fun part of the design process. Luckily, it consists of repetitive tasks that can be automated with the right tools to improve your efficiency. 

Gulp is a build system that can improve how you develop websites by automating common tasks, such as compiling preprocessed CSS, minifying JavaScript and reloading the browser.</p>

<img loading="lazy" decoding="async" title="Gulp – How To Build And Develop Websites" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42a79a91-13ef-4ed6-a64f-ee0845e81aec/00-gulp-intro.png" alt="Gulp – How To Build And Develop Websites" width="500" height="315" />

In this article, we’ll see how you can <strong>use Gulp to change your development workflow</strong>, making it faster and more efficient.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Harness The Machines: Being Productive With Task Runners](https://www.smashingmagazine.com/2016/06/harness-machines-productive-task-runners/)
*   [Why You Should Stop Installing Your WebDev Environment Locally](https://www.smashingmagazine.com/2016/04/stop-installing-your-webdev-environment-locally-with-docker/)
*   [Using A Static Site Generator At Scale: Lessons Learned](https://www.smashingmagazine.com/2016/08/using-a-static-site-generator-at-scale-lessons-learned/)
*   [Building Web Software With Make](https://www.smashingmagazine.com/2015/10/building-web-applications-with-make/)

{{% feature-panel %}}

## What Is Gulp?

<a href="https://gulpjs.com/">gulp.js</a> is a build system, meaning that you can use it to automate common tasks in the development of a website. It’s built on Node.js, and both the Gulp source and your Gulp file, where you define tasks, are written in JavaScript (or something like CoffeeScript, if you so choose). This makes it perfect if you’re a front-end developer: You can write tasks to lint your JavaScript and CSS, parse your templates, and compile your LESS when the file has changed (and these are just a few examples), and in a language that you’re probably already familiar with.

The system by itself doesn’t really do much, but a huge number of plugins are available, which you can see on the <a href="https://gulpjs.com/plugins">plugins page</a> or by searching <code>gulpplugin</code> on npm. For example, there are plugins to <a href="https://www.npmjs.org/package/gulp-jshint/">run JSHint</a>, <a href="https://www.npmjs.org/package/gulp-coffee/">compile your CoffeeScript</a>, <a href="https://npmjs.org/package/gulp-mocha">run Mocha tests</a> and even <a href="https://npmjs.org/package/gulp-bump">update your version number</a>.

Other build tools are available, such as <a href="https://www.smashingmagazine.com/2013/10/get-up-running-grunt/">Grunt</a> and, more recently, <a href="https://www.solitr.com/blog/2014/02/broccoli-first-release/">Broccoli</a>, but I believe Gulp to be superior (see the “Why Gulp?” section below). I’ve compiled a longer <a href="https://gist.github.com/callumacrae/9231589">list of build tools written in JavaScript</a>.

Gulp is open source and can be <a href="https://github.com/gulpjs/gulp/">found on GitHub</a>.</p>

## Installing

Installing is pretty easy. First, install the package globally:

<pre><code class="language-bash">npm install -g gulp
</code></pre>

Then, install it in your project:

<pre><code class="language-bash">npm install --save-dev gulp
</code></pre>

## Using

Let’s create a task to minify one of our JavaScript files. Create a file named <code>gulpfile.js</code>. This is where you will define your Gulp tasks, which will be run using the <code>gulp</code> command.

Put the following in your <code>gulpfile.js</code> file:

<pre><code class="language-javascript">var gulp = require('gulp'),
   uglify = require('gulp-uglify');

gulp.task('minify', function () {
   gulp.src('js/app.js')
      .pipe(uglify())
      .pipe(gulp.dest('build'))
});
</code></pre>

Install <code>gulp-uglify</code> through npm by running <code>npm install --save-dev gulp-uglify</code>, and then run the task by running <code>gulp minify</code>. Assuming that you have a file named <code>app.js</code> in the <code>js</code> directory, a new <code>app.js</code> will be created in the build directory containing the minified contents of <code>js/app.js</code>.

What actually happened here, though?

We’re doing a few things in our <code>gulpfile.js</code> file. First, we’re loading the <code>gulp</code> and <code>gulp-uglify</code> modules:

<pre><code class="language-javascript">var gulp = require('gulp'),
    uglify = require('gulp-uglify');
</code></pre>

Then, we’re defining a task named <code>minify</code>, which, when run, will call the function provided as the second argument:

<pre><code class="language-javascript">gulp.task('minify', function () {

});
</code></pre>

Finally — and this is where it gets tricky — we’re defining what our task should actually do:

<pre><code class="language-javascript">gulp.src('js/app.js')
   .pipe(uglify())
   .pipe(gulp.dest('build'))
</code></pre>

Unless you’re familiar with streams, which most front-end developers are not, the code above won’t mean much to you.</p>

### Streams

Streams enable you to pass some data through a number of usually small functions, which will modify the data and then pass the modified data to the next function.

In the example above, the <code>gulp.src()</code> function takes a string that matches a file or number of files (known as a “glob”), and creates a stream of objects representing those files. They are then passed (or piped) to the <code>uglify()</code> function, which takes the file objects and returns new file objects with a minified source. That output is then piped to the <code>gulp.dest()</code> function, which saves the changed files.

In diagram form, this is what happens:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaecf7f5-4042-432f-a525-019692e2748f/01-streams-opt.png" alt="Stream diagram." width="413" height="360" /></figure>

When there is only one task, the function doesn’t really do much. However, consider the following code:

<pre><code class="language-javascript">gulp.task('js', function () {
   return gulp.src('js/*.js')
      .pipe(jshint())
      .pipe(jshint.reporter('default'))
      .pipe(uglify())
      .pipe(concat('app.js'))
      .pipe(gulp.dest('build'));
});
</code></pre>

To run this yourself, install <code>gulp</code>, <code>gulp-jshint</code>, <code>gulp-uglify</code> and <code>gulp-concat</code>.

This task will take all files matching <code>js/*.js</code> (i.e. all JavaScript files from the <code>js</code> directory), run JSHint on them and print the output, uglify each file, and then concatenate them, saving them to <code>build/app.js</code>. In diagram form:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a50f94d-144e-41c1-b1b3-09f6cdb8e8b6/02-steams-2-opt.png" alt="Stream diagram." width="500" height="309" /></figure>

If you’re familiar with Grunt, then you’ll notice that this is pretty different to how Grunt does it. Grunt doesn’t use streams; instead, it takes files, runs a single task on them and saves them to new files, repeating the entire process for every task. This results in a lot of hits to the file system, making it slower than Gulp.

For a more comprehensive read on streams, check out the “<a href="https://github.com/substack/stream-handbook">Stream Handbook</a>.”

### gulp.src()

The <code>gulp.src()</code> function takes a glob (i.e. a string matching one or more files) or an array of globs and returns a stream that can be piped to plugins.

Gulp uses <a href="https://github.com/isaacs/node-glob">node-glob</a> to get the files from the glob or globs you specify. It’s easiest to explain using examples:

*   `js/app.js` Matches the exact file
*   `js/*.js` Matches all files ending in `.js` in the `js` directory only
*   `js/**/*.js` Matches all files ending in `.js` in the `js` directory and all child directories
*   `!js/app.js` Excludes `js/app.js` from the match, which is useful if you want to match all files in a directory except for a particular file
*   `*.+(js|css)` Matches all files in the root directory ending in `.js` or `.css`

Other features are available, but they’re not commonly used in Gulp. Check out out the <a href="https://github.com/isaacs/minimatch">Minimatch</a> documentation for more.

Let’s say that we have a directory named <code>js</code> containing JavaScript files, some minified and some not, and we want to create a task to minify the files that aren’t already minified. To do this, we match all JavaScript files in the directory and then exclude all files ending in <code>.min.js</code>:

<pre><code class="language-javascript">gulp.src(['js/**/*.js', '!js/**/*.min.js'])
</code></pre>

### Defining Tasks

To define a task, use the <code>gulp.task()</code> function. When you define a simple task, this function takes two attributes: the task’s name and a function to run.</p>

<pre><code class="language-javascript">gulp.task('greet', function () {
   console.log('Hello world!');
});
</code></pre>

Running <code>gulp greet</code> will result in “Hello world” being printed to the console.

A task may also be a list of other tasks. Suppose we want to define a <code>build</code> task that runs three other tasks, <code>css</code>, <code>js</code> and <code>imgs</code>. We can do this by specifying an array of tasks, instead of the function:

<pre><code class="language-javascript">gulp.task('build', ['css', 'js', 'imgs']);
</code></pre>

These will be run asynchronously, so you can’t assume that the <code>css</code> task will have finished running by the time <code>js</code> starts — in fact, it probably won’t have. To make sure that a task has finished running before another task runs, you can specify dependencies by combining the array of tasks with the function. For example, to define a <code>css</code> task that checks that the <code>greet</code> task has finished running before it runs, you can do this:

<pre><code class="language-javascript">gulp.task('css', ['greet'], function () {
   // Deal with CSS here
});
</code></pre>

Now, when you run the <code>css</code> task, Gulp will execute the <code>greet</code> task, wait for it to finish, and then call the function that you’ve specified.</p>

### Default Tasks

You can define a default task that runs when you just run <code>gulp</code>. You can do this by defining a task named <code>default</code>.</p>

<pre><code class="language-javascript">gulp.task('default', function () {
   // Your default task
});
</code></pre>

### Plugins

You can use a number of plugins — over 600, in fact — with Gulp. You will find them listed on the <a href="https://gulpjs.com/plugins/">plugins page</a> or by searching <code>gulpplugin</code> on npm. Some plugins are tagged “gulpfriendly”; these aren’t plugins but are designed to work well with Gulp. Be aware when searching directly on npm that you won’t be able to see whether a plugin has been blacklisted (scrolling to the bottom of the plugins page, you will see that many are).

Most plugins are pretty easy to use, have good documentation and are run in the same way (by piping a stream of file objects to it). They’ll then usually modify the files (although some, such as validators, will not) and return the new files to be passed to the next plugin.

Let’s expand on our <code>js</code> task from earlier:

<pre><code class="language-javascript">var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat');

gulp.task('js', function () {
   return gulp.src('js/*.js')
      .pipe(jshint())
      .pipe(jshint.reporter('default'))
      .pipe(uglify())
      .pipe(concat('app.js'))
      .pipe(gulp.dest('build'));
});
</code></pre>

We’re using three plugins here, <a href="https://github.com/wearefractal/gulp-jshint">gulp-jshint</a>, <a href="https://github.com/terinjokes/gulp-uglify">gulp-uglify</a> and <a href="https://github.com/wearefractal/gulp-concat">gulp-concat</a>. You can see in the <code>README</code> files for the plugins that they’re pretty easy to use; options are available, but the defaults are usually good enough.

You might have noticed that the JSHint plugin is called twice. That’s because the first line runs JSHint on the files, which only attaches a <code>jshint</code> property to the file objects without outputting anything. You can either read the <code>jshint</code> property yourself or pass it to the default JSHint reporter or to another reporter, such as <a href="https://github.com/sindresorhus/jshint-stylish">jshint-stylish</a>.

The other two plugins are clearer: the <code>uglify()</code> function minifies the code, and the <code>concat('app.js')</code> function concatenates all of the files into a single file named <code>app.js</code>.</p>

### gulp-load-plugins

A module that I find really useful is gulp-load-plugins, which automatically loads any Gulp plugins from your <code>package.json</code> file and attaches them to an object. Its most basic usage is as follows:

<pre><code class="language-javascript">var gulpLoadPlugins = require('gulp-load-plugins'),
    plugins = gulpLoadPlugins();
</code></pre>

You can put that all on one line (<code>var plugins = require('gulp-load-plugins')();</code>), but I’m not a huge fan of inline <code>require</code> calls.

After running that code, the <code>plugins</code> object will contain your plugins, camel-casing their names (for example, <code>gulp-ruby-sass</code> would be loaded to <code>plugins.rubySass</code>). You can then use them as if they were required normally. For example, our <code>js</code> task from before would be reduced to the following:

<pre><code class="language-javascript">var gulp = require('gulp'),
    gulpLoadPlugins = require('gulp-load-plugins'),
    plugins = gulpLoadPlugins();

gulp.task('js', function () {
   return gulp.src('js/*.js')
      .pipe(plugins.jshint())
      .pipe(plugins.jshint.reporter('default'))
      .pipe(plugins.uglify())
      .pipe(plugins.concat('app.js'))
      .pipe(gulp.dest('build'));
});
</code></pre>

This assumes a <code>package.json</code> file that is something like the following:

<pre><code class="language-javascript">{
   "devDependencies": {
      "gulp-concat": "~2.2.0",
      "gulp-uglify": "~0.2.1",
      "gulp-jshint": "~1.5.1",
      "gulp": "~3.5.6"
   }
}
</code></pre>

In this example, it’s not actually much shorter. However, with longer and more complicated Gulp files, it reduces a load of includes to just one or two lines.

Version 0.4.0 of gulp-load-plugins, released in early March, added lazy plugin loading, which improves performance. Plugins are not loaded until you call them, meaning that you don’t have to worry about unused plugins in <code>package.json</code> affecting performance (although you should probably clean them up anyway). In other words, if you run a task that requires only two plugins, it won’t load all of the plugins that the other tasks require.</p>

### Watching Files

Gulp has the ability to watch files for changes and then run a task or tasks when changes are detected. This feature is amazingly useful (and, for me, probably Gulp’s single most useful one). You can save your LESS file, and Gulp will turn it into CSS and update the browser without your having to do anything.

To watch a file or files, use the <code>gulp.watch()</code> function, which takes a glob or array of globs (the same as <code>gulp.src()</code>) and either an array of tasks to run or a callback.

Let’s say that we have a <code>build</code> task that turns our template files into HTML, and we want to define a <code>watch</code> task that watches our template files for changes and runs the task to turn them into HTML. We can use the <code>watch</code> function as follows:

<pre><code class="language-javascript">gulp.task('watch', function () {
   gulp.watch('templates/*.tmpl.html', ['build']);
});
</code></pre>

Now, when we change a template file, the <code>build</code> task will run and the HTML will be generated.

You can also give the <code>watch</code> function a callback, instead of an array of tasks. In this case, the callback would be given an <code>event</code> object containing some information about the event that triggered the callback:

<pre><code class="language-javascript">gulp.watch('templates/*.tmpl.html', function (event) {
   console.log('Event type: ' + event.type); // added, changed, or deleted
   console.log('Event path: ' + event.path); // The path of the modified file
});
</code></pre>

Another nifty feature of <code>gulp.watch()</code> is that it returns what is known as a <code>watcher</code>. Use the <code>watcher</code> to listen for additional events or to add files to the <code>watch</code>. For example, to both run a list of tasks and call a function, you could add a listener to the <code>change</code> event on the returned <code>watcher</code>:

<pre><code class="language-javascript">var watcher = gulp.watch('templates/*.tmpl.html', ['build']);
watcher.on('change', function (event) {
   console.log('Event type: ' + event.type); // added, changed, or deleted
   console.log('Event path: ' + event.path); // The path of the modified file
});
</code></pre>

In addition to the <code>change</code> event, you can listen for a number of other events:

*   `end` Fires when the watcher ends (meaning that tasks and callbacks won’t be called anymore when files are changed)
*   `error` Fires when an error occurs
*   `ready` Fires when the files have been found and are being watched
*   `nomatch` Fires when the glob doesn’t match any files

The <code>watcher</code> object also contains some methods that you can call:

*   `watcher.end()` Stops the `watcher` (so that no more tasks or callbacks will be called)
*   `watcher.files()` Returns a list of files being watched by the `watcher`
*   `watcher.add(glob)` Adds files to the `watcher` that match the specified glob (also, accepts an optional callback as a second argument)
*   `watcher.remove(filepath)` Removes a particular file from the `watcher`

## Reloading Changes In The Browser

You can get Gulp to reload or update the browser when you — or, for that matter, anything else, such as a Gulp task — changes a file. There are two ways to do this. The first is to use the LiveReload plugin, and the second is to use BrowserSync

### LiveReload

<a href="https://livereload.com/">LiveReload</a> combines with browser extensions (including a <a href="https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei">Chrome extension</a>) to reload your browser every time a change to a file is detected. It can be used with the <a href="https://www.npmjs.org/package/gulp-watch">gulp-watch</a> plugin or with the built-in <code>gulp.watch()</code> that I described earlier. Here’s an example from the <code>README</code> file of the <a href="https://github.com/vohof/gulp-livereload">gulp-livereload repository</a>:

<pre><code class="language-javascript">var gulp = require('gulp'),
    less = require('gulp-less'),
    livereload = require('gulp-livereload'),
    watch = require('gulp-watch');

gulp.task('less', function() {
   gulp.src('less/*.less')
      .pipe(watch())
      .pipe(less())
      .pipe(gulp.dest('css'))
      .pipe(livereload());
});
</code></pre>

This will watch all files matching <code>less/*.less</code> for changes. When a change is detected, it will generate the CSS, save the files and reload the browser.</p>

### BrowserSync

An alternative to LiveReload is available. <a href="https://browsersync.io/">BrowserSync</a> is similar in that it displays changes in the browser, but it has a lot more functionality.

When you make changes to code, BrowserSync either reloads the page or, if it is CSS, injects the CSS, meaning that the page doesn’t need to be refreshed. This is very useful if your website isn’t refresh-resistant. Suppose you’re developing four clicks into a single-page application, and refreshing the page would take you back to the starting page. With LiveReload, you would need to click four times every time you make a change. BrowserSync, however, would just inject the changes when you modify the CSS, so you wouldn’t need to click back.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6837998d-98fd-468c-93c8-3a95a7108b8c/03-browsersync-opt.gif"><img style="filter: url('#toggleGifsIndicatorFilter');" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b3d8afb-acd1-4b3f-a1d0-1733dbc28de3/03-browsersync-opt-500.gif" alt="BrowserSync is a better way to test your design across browsers." width="500" height="355" /></a><figcaption>BrowserSync is a better way to test your design across browsers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6837998d-98fd-468c-93c8-3a95a7108b8c/03-browsersync-opt.gif">View large version</a>)</figcaption></figure>

BrowserSync also synchronizes clicks, form actions and your scroll position between browsers. You could open a couple of browsers on your desktop and another on an iPhone and then navigate the website. The links would be followed on all of them, and as you scroll down the page, the pages on all of the devices would scroll down (usually smoothly, too!). When you input text in a form, it would be entered in every window. And when you don’t want this behavior, you can turn it off.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4029904d-67c2-489c-83df-81cb852cc6aa/04-browsersync-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02fe2d28-b4dc-4e24-bd15-b553328eb2b3/04-browsersync-opt-500.gif" alt="BrowserSync doesn’t require a browser plugin because it serves your files for you." width="500" height="349" /></a><figcaption>BrowserSync doesn’t require a browser plugin because it serves your files for you. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4029904d-67c2-489c-83df-81cb852cc6aa/04-browsersync-opt.gif">View large version</a>)</figcaption></figure>

BrowserSync doesn’t require a browser plugin because it serves your files for you (or proxies them, if they’re dynamic) and serves a script that opens a socket between the browser and the server. This hasn’t caused any problems for me in the past, though.

There isn’t actually a plugin for Gulp because BrowserSync doesn’t manipulate files, so it wouldn’t really work as one. However, the <a href="https://www.npmjs.org/package/browser-sync">BrowserSync module on npm</a> can be called directly from Gulp. First, install it through npm:

<pre><code class="language-bash">npm install --save-dev browser-sync
</code></pre>

Then, the following <code>gulpfile.js</code> will start BrowserSync and watch some files:

<pre><code class="language-javascript">var gulp = require('gulp'),
    browserSync = require('browser-sync');

gulp.task('browser-sync', function () {
   var files = [
      'app/**/*.html',
      'app/assets/css/**/*.css',
      'app/assets/imgs/**/*.png',
      'app/assets/js/**/*.js'
   ];

   browserSync.init(files, {
      server: {
         baseDir: './app'
      }
   });
});
</code></pre>

Running <code>gulp browser-sync</code> would then watch the matching files for changes and start a server that serves the files in the <code>app</code> directory.

The developer of BrowserSync has written about some other things you can do in his <a href="https://github.com/shakyShane/gulp-browser-sync">BrowserSync + Gulp</a> repository.</p>

## Why Gulp?

As mentioned, Gulp is one of <a href="https://gist.github.com/callumacrae/9231589">quite a few</a> build tools available in JavaScript, and other build tools not written in JavaScript are available, too, including Rake. Why should you choose it?

The two most popular build tools in JavaScript are Grunt and Gulp. Grunt was <a href="https://www.smashingmagazine.com/2013/10/29/get-up-running-grunt/">very popular in 2013</a> and completely changed how a lot of people develop websites. Thousands of plugins are available for it, doing everything from linting, minifying and concatenating code to installing packages using Bower and starting an Express server. This approach is pretty different from Gulp’s, which has only plugins to perform small individuals tasks that do things with files. Because tasks are just JavaScript (unlike the large object that Grunt uses), you don’t need a plugin; you can just start an Express server the normal way.

Grunt tasks tend to be over-configured, requiring a large object containing properties that you really wouldn’t want to have to care about, while the same task in Gulp might take up only a few lines. Let’s look at a simple <code>gruntfile.js</code> that defines a <code>css</code> task to convert our LESS to CSS and then run <a href="https://github.com/ai/autoprefixer">Autoprefixer</a> on it:

<pre><code class="language-javascript">grunt.initConfig({
   less: {
      development: {
         files: {
            "build/tmp/app.css": "assets/app.less"
         }
      }
   },

   autoprefixer: {
      options: {
         browsers: ['last 2 version', 'ie 8', 'ie 9']
      },
      multiple_files: {
         expand: true,
         flatten: true,
         src: 'build/tmp/app.css',
         dest: 'build/'
      }
   }
});

grunt.loadNpmTasks('grunt-contrib-less');
grunt.loadNpmTasks('grunt-autoprefixer');

grunt.registerTask('css', ['less', 'autoprefixer']);
</code></pre>

Compare this to the <code>gulpfile.js</code> file that does the same:

<pre><code class="language-javascript">var gulp = require('gulp'),
   less = require('gulp-less'),
   autoprefix = require('gulp-autoprefixer');

gulp.task('css', function () {
   gulp.src('assets/app.less')
      .pipe(less())
      .pipe(autoprefix('last 2 version', 'ie 8', 'ie 9'))
      .pipe(gulp.dest('build'));
});
</code></pre>

The <code>gulpfile.js</code> version is considerably more readable and smaller.

Because Grunt hits the file system far more often than Gulp, which uses streams, it is nearly always much faster than Grunt. For a small LESS file, the <code>gulpfile.js</code> file above would usually take about 6 milliseconds. The <code>gruntfile.js</code> would usually take about 50 milliseconds — more than eight times longer. This is a tiny example, but with longer files, the amount of time increases significantly.

{{< signature "ds, al, ml" >}}

