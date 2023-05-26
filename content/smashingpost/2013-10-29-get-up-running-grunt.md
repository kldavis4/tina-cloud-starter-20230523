---
title: Get Up And Running With Grunt
slug: get-up-running-grunt
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3588a664-646b-4c9a-9899-54d5f02f1557/grunt-js-opt.png'
date: 2013-10-29T11:21:33.000Z
author: mike-cunsolo
description: >-
  In this article, we’ll explore how to use [Grunt](https://gruntjs.com/) in a project to speed up and change the way you develop websites. We’ll look briefly at what Grunt can do, before jumping into how to set up and use its various plugins to do all of the heavy lifting in a project.
categories:
  - Coding
  - Tools
  - Workflow
  - JavaScript
  - HTML
---
In this article, we’ll explore how to use <a href="https://gruntjs.com/">Grunt</a> in a project to speed up and change the way you develop websites. We’ll look briefly at what Grunt can do, before jumping into how to set up and use its various plugins to do all of the heavy lifting in a project.

We’ll then look at how to build a simple input validator, using <a href="https://sass-lang.com/">Sass</a> as a preprocessor, how to use grunt-cssc and CssMin to combine and minify our CSS, how to use <a href="https://htmlhint.com/">HTMLHint</a> to make sure our HTML is written correctly, and how to build our compressed assets on the fly. Lastly, we’ll look at using <a href="https://github.com/mishoo/UglifyJS">UglifyJS</a> to reduce the size of our JavaScript and ensure that our website uses as little bandwidth as possible.

<a href="https://gruntjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d97820c-f3bd-4667-86f4-2f7c663a1eca/grund-js-opt.png" alt="Grunt JS" width="504" height="276" /></a><br>
<em><a href="https://gruntjs.com/">Grunt.js</a> is a JavaScript task runner that helps you perform repetitive tasks such as minification, compilation, unit testing or linting.</em>

## Getting Started With Grunt

Most developers would agree that the speed and pace of JavaScript development over the last few years has been pretty astounding. Whether with frameworks such as <a href="https://www.smashingmagazine.com/2013/02/introduction-backbone-marionette/">Backbone.js</a> and <a href="https://www.smashingmagazine.com/2013/11/an-in-depth-introduction-to-ember-js/">Ember.js</a> or with communities such as <a href="https://jsbin.com/welcome/1/edit">JS Bin</a>, the development of this language is changing not only the way we experience websites as users but also the way we build them.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Kickstart Your Project With INIT And Grunt](https://www.smashingmagazine.com/2014/02/kickstart-your-project-with-init-and-grunt/)
*   [Building With Gulp](https://www.smashingmagazine.com/2014/06/building-with-gulp/)
*   [How To Harness The Machines: Being Productive With Task Runners](https://www.smashingmagazine.com/2016/06/harness-machines-productive-task-runners/)
*   [Meet ImageOptim-CLI, A Batch Compression Tool](https://www.smashingmagazine.com/2013/12/imageoptim-cli-batch-compression-tool/)

When you are working with JavaScript, you will likely need to execute multiple tasks regularly. While this is pretty much a given in most projects, it’s a time-consuming and repetitive way to work. Being in such an active community, you would assume that tools are available to automate and speed up this process. This is where Grunt comes in.</p>

### What Is Grunt?

Built on top of Node.js, Grunt is a task-based command-line tool that speeds up workflows by reducing the effort required to prepare assets for production. It does this by wrapping up jobs into tasks that are compiled automatically as you go along. Basically, you can use Grunt on most tasks that you consider to be grunt work and would normally have to manually configure and run yourself.

While earlier versions came bundled with plugins like JSHint and Uglyify, the most recent release (version 0.4) relies on plugins for everything.

What kind of tasks? Well, the list is exhaustive. Suffice it to say, Grunt can handle most things you throw at it, from <a href="https://npmjs.org/package/grunt-minified">minifying</a> to <a href="https://github.com/gruntjs/grunt-contrib-concat">concatenating</a> JavaScript. It can also be used for a range of tasks unrelated to JavaScript, such as compiling CSS from LESS and Sass. We’ve even used it with <a href="https://blink1.thingm.com/">blink(1)</a> to notify us when a build fails.</p>

### Why Use Grunt?

One of the best things about it is the consistency it brings to teams. If you work collaboratively, you’ll know how frustrating inconsistency in the code can be. Grunt enables teams to work with a unified set of commands, thus ensuring that everyone on the team is writing code to the same standard. After all, nothing is more frustrating than a build that fails because of little inconsistencies in how a team of developers writes code.

Grunt also has an incredibly active community of developers, with new plugins being released regularly. The barrier to entry is relatively low because a vast range of tools and automated tasks are already available to use.</p>

## Setting Up

The first thing to do in order to use Grunt is to set up Node.js. (If you know nothing about Node.js, don’t worry — it merely needs to be installed in order for Grunt to be able to run.)

Once Node.js is installed, run this command:

<pre><code class="language-bash">
$ npm install -g grunt-cli
</code></pre>

To make sure Grunt has been properly installed, you can run the following command:

<pre><code class="language-bash">
$ grunt --version
</code></pre>

The next step is to create a <code>package.json</code> and a <code>gruntfile.js</code> file in the root directory of your project.</p>

### Creating the package.json File

The JSON file enables us to track and install all of our development dependencies. Then, anyone who works on the project will have the most current dependencies, which ultimately helps to keep the development environments in sync.

Create a file in the root of your project that contains the following:

<pre><code class="language-json">
{
    "name" : "SampleGrunt",
    "version" : "0.1.0",
    "author" : "Brandon Random",
    "private" : true,

    "devDependencies" : {
        "grunt" :                   "~0.4.0"
    }
}
</code></pre>

Once you have done this, run the following command:

<pre><code class="language-bash">
$ npm install
</code></pre>

This tells npm which dependencies to install and places them in a <code>node_modules</code> folder.</p>

### Creating the gruntfile.js File

<code>Gruntfile.js</code> is essentially made up of a wrapper function that takes <code>grunt</code> as an argument.

<pre><code class="language-javascript">
module.exports = function(grunt){

    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json')
    });

    grunt.registerTask('default', []);

};
</code></pre>

You are now set up to run Grunt from the command line at the root of your project. But if you do so at this stage, you will get the following warning:

<pre><code class="language-bash">
$ grunt</code></pre>

&gt; Task "default" not found. Use --force to continue.

We’d get this because we haven’t specified any tasks or dependencies yet other than Grunt. So, let’s do that. But first, let’s look at how to extend the <code>package.json</code> file.</p>

### Extending the package.json File

The best thing about working with Node.js is that it can find packages and install them in one go, simply based on the contents of the package file. To install all of the new dependencies, just add this to the file:

<pre><code class="language-javascript">
{
    "name" : "SampleGrunt",
    "version" : "0.1.0",
    "author" : "Mike Cunsolo",
    "private" : true,

    "devDependencies" : {
        "grunt" :                       "~0.4.0",
        "grunt-contrib-cssmin":         "*",
        "grunt-contrib-sass":           "*",
        "grunt-contrib-uglify":         "*",
        "grunt-contrib-watch":          "*",
        "grunt-cssc":                   "*",
        "grunt-htmlhint":               "*",
        "matchdep":                     "*"
    }
}
</code></pre>

And to complete the process? You guessed it:

<pre><code class="language-javascript">
$ npm install
</code></pre>

## Loading npm Tasks In Grunt

Now that the packages have been installed, they have to be loaded in Grunt before we can do anything with them. We can load all of the tasks automatically with a single line of code, using the <code>matchdep</code> dependency. This is a boon for development because now the dependency list will be included only in the package file.

At the top of <code>gruntfile.js</code>, above <code>grunt.initConfig</code>, paste this:

<pre><code class="language-javascript">
require("matchdep").filterDev("grunt-*").forEach(grunt.loadNpmTasks);
</code></pre>

Without <code>matchdep</code>, we would have to write <code>grunt.loadNpmTasks("grunt-task-name");</code> for each dependency, which would quickly add up as we find and install other plugins.

Because the plugins are loaded into Grunt, we may start specifying options. First off is the HTML file (<code>index.html</code>), which contains the following:

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;

    &lt;head&gt;

        &lt;meta charset="utf-8"&gt;
        &lt;meta name="viewport"   content="width=device-width; initial-scale=1.0; maximum-scale=1.0;"&gt;

        &lt;title&gt;Enter your first name&lt;/title&gt;

        &lt;link rel="stylesheet"  href="build/css/master.css"&gt;

    &lt;/head&gt;

    &lt;body&gt;

        &lt;label for="firstname"&gt;Enter your first name&lt;/label&gt;
        &lt;input id="firstname" name="firstname" type="text"&gt;
        &lt;p id="namevalidation" class="validation"&gt;&lt;/p&gt;

        &lt;script type="text/javascript" src="build/js/base.min.js"&gt;&lt;/script&gt;

    &lt;/body&gt;

&lt;/html&gt;
</code></pre>

## Validating With HTMLHint

Add this configuration to <code>grunt.initConfig</code>:

<pre><code class="language-markup">
htmlhint: {
    build: {
        options: {
            'tag-pair': true,
            'tagname-lowercase': true,
            'attr-lowercase': true,
            'attr-value-double-quotes': true,
            'doctype-first': true,
            'spec-char-escape': true,
            'id-unique': true,
            'head-script-disabled': true,
            'style-disabled': true
        },
        src: ['index.html']
    }
}
</code></pre>

A plugin is typically configured like this: the plugin’s name (without the <code>grunt-contrib-/grunt-</code> prefix), then one or more targets of your choosing (which can be used to create custom options for the plugin for different files), an <code>options</code> object, and the files it affects. Now, when we run <code>grunt htmlhint</code> from the terminal, it will check through the source file and make sure that our HTML has no errors! However, manually typing this command several times an hour would get tedious pretty quickly.</p>

## Automate Tasks That Run Every Time A File Is Saved

The <code>watch</code> task can run a unique set of tasks according to the file being saved, using targets. Add this configuration to <code>grunt.initConfig</code>:

<pre><code class="language-javascript">
watch: {
    html: {
        files: ['index.html'],
        tasks: ['htmlhint']
    }
}
</code></pre>

Then, run <code>grunt watch</code> in the terminal. Now, try adding a comment to <code>index.html</code>. You’ll notice that when the file is saved, validation is automatic! This is a boon for development because it means that <code>watch</code> will silently validate as you write code, and it will fail if the code hasn’t passed the relevant tests (and it will tell you what the problem is).

Note that <code>grunt watch</code> will keep running until the terminal is closed or until it is stopped (<code>Control + C</code> on a Mac).</p>

## Keeping The JavaScript As Lean As Possible

Let’s set up a JavaScript file to validate a user’s name. To keep this as simple as possible, we’ll check only for non-alphabetical characters. We’ll also use the <code>strict</code> mode of JavaScript, which prevents us from writing valid but poor-quality JavaScript. Paste the following into <code>assets/js/base.js</code>:

<pre><code class="language-javascript">
function Validator()
{
    "use strict";
}

Validator.prototype.checkName = function(name)
{
    "use strict";
    return (/[^a-z]/i.test(name) === false);
};

window.addEventListener('load', function(){
    "use strict";
    document.getElementById('firstname').addEventListener('blur', function(){
        var _this = this;
        var validator = new Validator();
        var validation = document.getElementById('namevalidation');
        if (validator.checkName(_this.value) === true) {
            validation.innerHTML = 'Looks good! :)';
            validation.className = "validation yep";
            _this.className = "yep";
        }
        else {
            validation.innerHTML = 'Looks bad! :(';
            validation.className = "validation nope";
            _this.className = "nope";
        }

    });
});
</code></pre>

Let’s use UglifyJS to minify this source file. Add this to <code>grunt.initConfig</code>:

<pre><code class="language-javascript">
uglify: {
    build: {
        files: {
            'build/js/base.min.js': ['assets/js/base.js']
        }
    }
}
</code></pre>

UglifyJS compresses all of the variable and function names in our source file to take up as little space as possible, and then trims out white space and comments — extremely useful for production JavaScript. Again, we have to set up a <code>watch</code> task to build our Uglify’ed JavaScript. Add this to the <code>watch</code> configuration:

<pre><code class="language-javascript">
watch: {
    js: {
        files: ['assets/js/base.js'],
        tasks: ['uglify']
    }
}
</code></pre>

## Building CSS From Sass Source Files

Sass is incredibly useful for working with CSS, especially on a team. Less code is usually written in the source file because Sass can generate large CSS code blocks with such things as functions and variables. Walking through Sass itself is a little beyond the scope of this article; so, if you are not comfortable with learning a preprocessor at this stage, you can skip this section. But we will cover a very simple use case, using variables, one mixin and the Sassy CSS (SCSS) syntax, which is very similar to CSS!

Grunt’s Sass plugin requires the Sass gem. You will need to install Ruby on your system (it comes preloaded in OS X). You can check whether Ruby is installed with this terminal command:

<pre><code class="language-bash">
ruby -v
</code></pre>

Install Sass by running the following:

<pre><code class="language-bash">
gem install sass
</code></pre>

Depending on your configuration, you might need to run this command via sudo — i.e. <code>sudo gem install sass:</code> — at which point you will be asked for your password. When Sass is installed, create a new directory named <code>assets</code> and, inside that, another named <code>sass</code>. Create a new file named <code>master.scss</code> in this directory, and paste the following in it:

<pre><code class="language-css">
@mixin prefix($property, $value, $prefixes: webkit moz ms o spec) {
    @each $p in $prefixes {
        @if $p == spec {
            #{$property}: $value;
        }
        @else {
            -#{$p}-#{$property}: $value;
        }
    }
}
$input_field:            #999;
$input_focus:           #559ab9;
$validation_passed:     #8aba56;
$validation_failed:     #ba5656;
$bg_colour:             #f4f4f4;
$box_colour:            #fff;
$border_style:          1px solid;
$border_radius:         4px;

html {
    background:         $bg_colour;
}

body {
    width:              720px;
    padding:            40px;
    margin:             80px auto;
    background:         $box_colour;
    box-shadow:         0 1px 3px rgba(0, 0, 0, .1);
    border-radius:      $border_radius;
    font-family:        sans-serif;
}

input[type="text"] {
    @include            prefix(appearance, none, webkit moz);
    @include            prefix(transition, border .3s ease);
    border-radius:      $border_radius;
    border:             $border_style $input_field;
    width:              220px;
}

input[type="text"]:focus {
    border-color:       $input_focus;
    outline:            0;
}

label,
input[type="text"],
.validation {
    line-height:        1;
    font-size:          1em;
    padding:            10px;
    display:            inline;
    margin-right:       20px;
}

input.yep {
    border-color:       $validation_passed;
}

input.nope {
    border-color:       $validation_failed;
}

p.yep {
    color:              $validation_passed;
}

p.nope {
    color:              $validation_failed;
}
</code></pre>

You will notice that the SCSS extension looks a lot more like CSS than conventional Sass. This style sheet makes use of two Sass features: mixins and variables. A mixin constructs a block of CSS based on some parameters passed to it, much like a function would, and variables allow common fragments of CSS to be defined once and then reused.

Variables are especially useful for hex colours; we can build a palette that can be changed in one place, which makes tweaking aspects of a design very fast. The mixin is used to prefix rules such as for appearance and transitions, and it reduces bulk in the file itself.

When working with a large style sheet, anything that can be done to reduce the number of lines will make the file easier to read when a team member other than you wants to update a style.

In addition to Sass, grunt-cssc combines CSS rules together, ensuring that the generated CSS has minimal repetition. This can be very useful in medium- to large-scale projects in which a lot of styles are repeated. However, the outputted file is not always the smallest possible. This is where the <code>cssmin</code> task comes in. It not only trims out white space, but transforms colors to their shortest possible values (so, <code>white</code> would become <code>#fff</code>). Add these tasks to <code>gruntfile.js</code>:

<pre><code class="language-css">
cssc: {
    build: {
        options: {
            consolidateViaDeclarations: true,
            consolidateViaSelectors:    true,
            consolidateMediaQueries:    true
        },
        files: {
            'build/css/master.css': 'build/css/master.css'
        }
    }
},

cssmin: {
    build: {
        src: 'build/css/master.css',
        dest: 'build/css/master.css'
    }
},

sass: {
    build: {
        files: {
            'build/css/master.css': 'assets/sass/master.scss'
        }
    }
}
</code></pre>

Now that we have something in place to handle style sheets, these tasks should also be run automatically. The <code>build</code> directory is created automatically by Grunt to house all of the production scripts, CSS and (if this were a full website) compressed images. This means that the contents of the <code>assets</code> directory may be heavily commented and may contain more documentation files for development purposes; then, the <code>build</code> directory would strip all of that out, leaving the assets as optimized as possible.

We’re going to define a new set of tasks for working with CSS. Add this line to <code>gruntfile.js</code>, below the default <code>task</code>:

<pre><code class="language-javascript">
grunt.registerTask('buildcss',  ['sass', 'cssc', 'cssmin']);
</code></pre>

Now, when <code>grunt buildcss</code> is run, all of the CSS-related tasks will be executed one after another. This is much tidier than running <code>grunt sass</code>, then <code>grunt cssc</code>, then <code>grunt cssmin</code>. All we have to do now is update the <code>watch</code> configuration so that this gets run automatically.

<pre><code class="language-css">
watch: {
    css: {
        files: ['assets/sass/**/*.scss'],
        tasks: ['buildcss']
    }
}
</code></pre>

This path might look a little strange to you. Basically, it recursively checks any directory in our <code>assets/sass</code> directory for <code>.scss</code> files, which allows us to create as many Sass source files as we want, without having to add the paths to <code>gruntfile.js</code>. After adding this, <code>gruntfile.js</code> should look like this:

<pre><code class="language-css">
module.exports = function(grunt){

    "use strict";
   require("matchdep").filterDev("grunt-*").forEach(grunt.loadNpmTasks);

    grunt.initConfig({

        pkg: grunt.file.readJSON('package.json'),

        cssc: {
            build: {
                options: {
                    consolidateViaDeclarations: true,
                    consolidateViaSelectors:    true,
                    consolidateMediaQueries:    true
                },
                files: {
                    'build/css/master.css': 'build/css/master.css'
                }
            }
        },

        cssmin: {
            build: {
                src: 'build/css/master.css',
                dest: 'build/css/master.css'
            }
        },

## Validating With HTMLHint

Add this configuration to <code>grunt.initConfig</code>:

<pre><code class="language-markup">
htmlhint: {
    build: {
        options: {
            'tag-pair': true,
            'tagname-lowercase': true,
            'attr-lowercase': true,
            'attr-value-double-quotes': true,
            'doctype-first': true,
            'spec-char-escape': true,
            'id-unique': true,
            'head-script-disabled': true,
            'style-disabled': true
        },
        src: ['index.html']
    }
}
</code></pre>

A plugin is typically configured like this: the plugin’s name (without the <code>grunt-contrib-/grunt-</code> prefix), then one or more targets of your choosing (which can be used to create custom options for the plugin for different files), an <code>options</code> object, and the files it affects. Now, when we run <code>grunt htmlhint</code> from the terminal, it will check through the source file and make sure that our HTML has no errors! However, manually typing this command several times an hour would get tedious pretty quickly.</p>

## Automate Tasks That Run Every Time A File Is Saved

The <code>watch</code> task can run a unique set of tasks according to the file being saved, using targets. Add this configuration to <code>grunt.initConfig</code>:

<pre><code class="language-javascript">
watch: {
    html: {
        files: ['index.html'],
        tasks: ['htmlhint']
    }
}
</code></pre>

Then, run <code>grunt watch</code> in the terminal. Now, try adding a comment to <code>index.html</code>. You’ll notice that when the file is saved, validation is automatic! This is a boon for development because it means that <code>watch</code> will silently validate as you write code, and it will fail if the code hasn’t passed the relevant tests (and it will tell you what the problem is).

Note that <code>grunt watch</code> will keep running until the terminal is closed or until it is stopped (<code>Control + C</code> on a Mac).</p>

## Keeping The JavaScript As Lean As Possible

Let’s set up a JavaScript file to validate a user’s name. To keep this as simple as possible, we’ll check only for non-alphabetical characters. We’ll also use the <code>strict</code> mode of JavaScript, which prevents us from writing valid but poor-quality JavaScript. Paste the following into <code>assets/js/base.js</code>:

<pre><code class="language-javascript">
function Validator()
{
    "use strict";
}

Validator.prototype.checkName = function(name)
{
    "use strict";
    return (/[^a-z]/i.test(name) === false);
};

window.addEventListener('load', function(){
    "use strict";
    document.getElementById('firstname').addEventListener('blur', function(){
        var _this = this;
        var validator = new Validator();
        var validation = document.getElementById('namevalidation');
        if (validator.checkName(_this.value) === true) {
            validation.innerHTML = 'Looks good! :)';
            validation.className = "validation yep";
            _this.className = "yep";
        }
        else {
            validation.innerHTML = 'Looks bad! :(';
            validation.className = "validation nope";
            _this.className = "nope";
        }

    });
});
</code></pre>

Let’s use UglifyJS to minify this source file. Add this to <code>grunt.initConfig</code>:

<pre><code class="language-javascript">
uglify: {
    build: {
        files: {
            'build/js/base.min.js': ['assets/js/base.js']
        }
    }
}
</code></pre>

UglifyJS compresses all of the variable and function names in our source file to take up as little space as possible, and then trims out white space and comments — extremely useful for production JavaScript. Again, we have to set up a <code>watch</code> task to build our Uglify’ed JavaScript. Add this to the <code>watch</code> configuration:

<pre><code class="language-javascript">
watch: {
    js: {
        files: ['assets/js/base.js'],
        tasks: ['uglify']
    }
}
</code></pre>

## Building CSS From Sass Source Files

Sass is incredibly useful for working with CSS, especially on a team. Less code is usually written in the source file because Sass can generate large CSS code blocks with such things as functions and variables. Walking through Sass itself is a little beyond the scope of this article; so, if you are not comfortable with learning a preprocessor at this stage, you can skip this section. But we will cover a very simple use case, using variables, one mixin and the Sassy CSS (SCSS) syntax, which is very similar to CSS!

Grunt’s Sass plugin requires the Sass gem. You will need to install Ruby on your system (it comes preloaded in OS X). You can check whether Ruby is installed with this terminal command:

<pre><code class="language-bash">
ruby -v
</code></pre>

Install Sass by running the following:

<pre><code class="language-bash">
gem install sass
</code></pre>

Depending on your configuration, you might need to run this command via sudo — i.e. <code>sudo gem install sass:</code> — at which point you will be asked for your password. When Sass is installed, create a new directory named <code>assets</code> and, inside that, another named <code>sass</code>. Create a new file named <code>master.scss</code> in this directory, and paste the following in it:

<pre><code class="language-css">
@mixin prefix($property, $value, $prefixes: webkit moz ms o spec) {
    @each $p in $prefixes {
        @if $p == spec {
            #{$property}: $value;
        }
        @else {
            -#{$p}-#{$property}: $value;
        }
    }
}
$input_field:            #999;
$input_focus:           #559ab9;
$validation_passed:     #8aba56;
$validation_failed:     #ba5656;
$bg_colour:             #f4f4f4;
$box_colour:            #fff;
$border_style:          1px solid;
$border_radius:         4px;

html {
    background:         $bg_colour;
}

body {
    width:              720px;
    padding:            40px;
    margin:             80px auto;
    background:         $box_colour;
    box-shadow:         0 1px 3px rgba(0, 0, 0, .1);
    border-radius:      $border_radius;
    font-family:        sans-serif;
}

input[type="text"] {
    @include            prefix(appearance, none, webkit moz);
    @include            prefix(transition, border .3s ease);
    border-radius:      $border_radius;
    border:             $border_style $input_field;
    width:              220px;
}

input[type="text"]:focus {
    border-color:       $input_focus;
    outline:            0;
}

label,
input[type="text"],
.validation {
    line-height:        1;
    font-size:          1em;
    padding:            10px;
    display:            inline;
    margin-right:       20px;
}

input.yep {
    border-color:       $validation_passed;
}

input.nope {
    border-color:       $validation_failed;
}

p.yep {
    color:              $validation_passed;
}

p.nope {
    color:              $validation_failed;
}
</code></pre>

You will notice that the SCSS extension looks a lot more like CSS than conventional Sass. This style sheet makes use of two Sass features: mixins and variables. A mixin constructs a block of CSS based on some parameters passed to it, much like a function would, and variables allow common fragments of CSS to be defined once and then reused.

Variables are especially useful for hex colours; we can build a palette that can be changed in one place, which makes tweaking aspects of a design very fast. The mixin is used to prefix rules such as for appearance and transitions, and it reduces bulk in the file itself.

When working with a large style sheet, anything that can be done to reduce the number of lines will make the file easier to read when a team member other than you wants to update a style.

In addition to Sass, grunt-cssc combines CSS rules together, ensuring that the generated CSS has minimal repetition. This can be very useful in medium- to large-scale projects in which a lot of styles are repeated. However, the outputted file is not always the smallest possible. This is where the <code>cssmin</code> task comes in. It not only trims out white space, but transforms colors to their shortest possible values (so, <code>white</code> would become <code>#fff</code>). Add these tasks to <code>gruntfile.js</code>:

<pre><code class="language-css">
cssc: {
    build: {
        options: {
            consolidateViaDeclarations: true,
            consolidateViaSelectors:    true,
            consolidateMediaQueries:    true
        },
        files: {
            'build/css/master.css': 'build/css/master.css'
        }
    }
},

cssmin: {
    build: {
        src: 'build/css/master.css',
        dest: 'build/css/master.css'
    }
},

sass: {
    build: {
        files: {
            'build/css/master.css': 'assets/sass/master.scss'
        }
    }
}
</code></pre>

Now that we have something in place to handle style sheets, these tasks should also be run automatically. The <code>build</code> directory is created automatically by Grunt to house all of the production scripts, CSS and (if this were a full website) compressed images. This means that the contents of the <code>assets</code> directory may be heavily commented and may contain more documentation files for development purposes; then, the <code>build</code> directory would strip all of that out, leaving the assets as optimized as possible.

We’re going to define a new set of tasks for working with CSS. Add this line to <code>gruntfile.js</code>, below the default <code>task</code>:

<pre><code class="language-javascript">
grunt.registerTask('buildcss',  ['sass', 'cssc', 'cssmin']);
</code></pre>

Now, when <code>grunt buildcss</code> is run, all of the CSS-related tasks will be executed one after another. This is much tidier than running <code>grunt sass</code>, then <code>grunt cssc</code>, then <code>grunt cssmin</code>. All we have to do now is update the <code>watch</code> configuration so that this gets run automatically.

<pre><code class="language-css">
watch: {
    css: {
        files: ['assets/sass/**/*.scss'],
        tasks: ['buildcss']
    }
}
</code></pre>

This path might look a little strange to you. Basically, it recursively checks any directory in our <code>assets/sass</code> directory for <code>.scss</code> files, which allows us to create as many Sass source files as we want, without having to add the paths to <code>gruntfile.js</code>. After adding this, <code>gruntfile.js</code> should look like this:

<pre><code class="language-css">
module.exports = function(grunt){

    "use strict";
   require("matchdep").filterDev("grunt-*").forEach(grunt.loadNpmTasks);

    grunt.initConfig({

        pkg: grunt.file.readJSON('package.json'),

        cssc: {
            build: {
                options: {
                    consolidateViaDeclarations: true,
                    consolidateViaSelectors:    true,
                    consolidateMediaQueries:    true
                },
                files: {
                    'build/css/master.css': 'build/css/master.css'
                }
            }
        },

        cssmin: {
            build: {
                src: 'build/css/master.css',
                dest: 'build/css/master.css'
            }
        },

        sass: {
            build: {
                files: {
                    'build/css/master.css': 'assets/sass/master.scss'
                }
            }
        },

        watch: {
            html: {
                files: ['index.html'],
                tasks: ['htmlhint']
            },
            js: {
                files: ['assets/js/base.js'],
                tasks: ['uglify']
            },
            css: {
                files: ['assets/sass/**/*.scss'],
                tasks: ['buildcss']
            }
        },

        htmlhint: {
            build: {
                options: {
                    'tag-pair': true,
// Force tags to have a closing pair
                    'tagname-lowercase': true,
// Force tags to be lowercase
                    'attr-lowercase': true,
// Force attribute names to be lowercase e.g. &lt;div id="header"&gt; is invalid
                    'attr-value-double-quotes': true,
// Force attributes to have double quotes rather than single
                    'doctype-first': true,
// Force the DOCTYPE declaration to come first in the document
                    'spec-char-escape': true,
// Force special characters to be escaped
                    'id-unique': true,
// Prevent using the same ID multiple times in a document
                    'head-script-disabled': true,
// Prevent script tags being loaded in the  for performance reasons
                    'style-disabled': true
// Prevent style tags. CSS should be loaded through 
                },
                src: ['index.html']
            }
        },

        uglify: {
            build: {
                files: {
                    'build/js/base.min.js': ['assets/js/base.js']
                }
            }
        }

    });

    grunt.registerTask('default',   []);
    grunt.registerTask('buildcss',  ['sass', 'cssc', 'cssmin']);

};
</code></pre>

We should now have a static HTML page, along with an <code>assets</code> directory with the Sass and JavaScript source, and a <code>build</code> directory with the optimized CSS and JavaScript inside, along with the <code>package.json</code> and <code>gruntfile.js</code> files.

By now, you should have a pretty solid foundation for exploring Grunt further. As mentioned, an incredibly active community of developers is building front-end plugins. My advice is to head on over to the <a href="https://gruntjs.com/plugins">plugin library</a> and explore the more than 300 plugins.

{{< signature "al" >}}

