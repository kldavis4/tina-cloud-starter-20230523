---
title: PostCSS – A Comprehensive Introduction
slug: introduction-to-postcss
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57535d5c-3ace-450f-a6ff-1d092596a63e/developer-opt.jpg'
date: 2015-12-08T00:15:57.000Z
author: drewminns
description: >-
  The **development of CSS**, like all languages, is an iterative process. With
  every major release, we get new features and syntaxes that help us write our
  styles. CSS Level 3 introduced features that enable us to design interactions
  that previously were possible only with JavaScript. With every new day, tools
  emerge to make styling easier and more flexible.

  One of the relatively recent tools introduced for styling is
  [PostCSS](https://github.com/postcss/postcss). PostCSS aims to reinvent CSS
  with an ecosystem of custom plugins and tools. Working with the same
  principles of preprocessors such as Sass and LESS, it **transforms extended
  syntaxes and features into modern, browser-friendly CSS**.
categories:
  - Coding
  - CSS
  - Techniques
  - Preprocessors
---
The <strong>development of CSS</strong>, like all languages, is an iterative process. With every major release, we get new features and syntaxes that help us write our styles. CSS Level 3 introduced features that enable us to design interactions that previously were possible only with JavaScript. With every new day, tools emerge to make styling easier and more flexible.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3426185f-6807-452d-a391-819adbac4ec5/post-css-opt.png" alt="An Introduction To PostCSS" width="300" height="300" /></figure>

One of the relatively recent tools introduced for styling is <a href="https://github.com/postcss/postcss">PostCSS</a>. PostCSS aims to reinvent CSS with an ecosystem of custom plugins and tools. Working with the same principles of preprocessors such as Sass and LESS, it <strong>transforms extended syntaxes and features into modern, browser-friendly CSS</strong>.

How you ask? JavaScript.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [It’s Time To Start Using CSS Custom Properties](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/)
*   [Houdini: Maybe The Most Exciting Development In CSS](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)

{{% feature-panel %}}

JavaScript has the ability to transform our styles much more quickly than other processors. Using task-runner tools like Gulp and Grunt, we can <strong>transform styles through the build process</strong>, much like Sass and LESS compilation. Libraries and frameworks like React and AngularJS allow us to write CSS directly in our JavaScript, opening the door for JavaScript transformation of our styles.</p>

## The History Of PostCSS

Developed by <a href="https://sitnik.ru/en">Andrey Sitnik</a>, creator of Autoprefixer, PostCSS was launched as a method to use JavaScript for CSS processing. PostCSS on its own is simply an API, which, when used with its vast ecosystem of plugins, offers powerful abilities. To provide helpful debugging, source maps are generated, and an abstract syntax tree (AST) exists to help us understand where and how code is being transformed.

Because PostCSS uses the Node.js framework, the abilities of the language and tools can be easily modified and customized as needed. Other tools such as Sass and LESS limit the abilities of the system to the methods available when the compiler was written.

Due to its use of an API, PostCSS allows us to <strong>create custom plugins and tools for any features</strong> they may need. This modular platform design makes the tool neutral, which in turn focuses features on project requirements. PostCSS is agnostic to language format and allows for the syntax style of different preprocessors, like Sass and LESS, if needed.</p>

## The Benefits Of Thinking Modularly

Most developers rarely start a project from scratch. Many start with a Sass boilerplate that holds variables, mixins and functions to be used in a given project. We’ll have a separate style sheet for functions, mixins, grid systems and general utilities to make production easier. At the end of the day, we end up with 10 or more style sheets to keep things organized.

<strong>Maintaining a library of Sass or LESS snippets</strong> can be an overwhelming task and can leave a project bloated. Many projects have unused mixins and functions, included as “just in case” code. PostCSS enables easily installable, plug-and-play modules, making the development process more flexible for the unique needs of a project.

PostCSS moves all of the code needed to create functions, utilities and mixins out of our production style sheets and wraps them as plugins. Now, for each project, we can pick and choose the tools needed by including plugins in our task runner.

An example of this power is the plugin <a href="https://github.com/seaneking/postcss-fontpath">PostCSS FontPath</a>. With Sass, we could include a mixin in our files that allows for custom web fonts; thus, we created <code>@font-face</code> tags.

<pre><code class="language-scss">@mixin importfont($font-family, $font-filename, $font-weight : normal, $font-style :normal, $font-stretch : normal) {
  @font-face {
    font-family: '#{$font-family}';
    src: url('#{$font-filename}.eot');
    src: url('#{$font-filename}.woff') format('woff'),
    url('#{$font-filename}.ttf') format('truetype');
    font-weight: $font-weight;
    font-style: $font-style;
    font-stretch: $font-stretch;
  }
}
@include importfont('mission script', 'fonts/mission-script-webfont', 300);</code></pre>

Using the <a href="https://github.com/seaneking/postcss-fontpath">PostCSS FontPath</a> plugin in our project, we no longer need to include Sass mixins like the one above. We can write the following code in our CSS, and PostCSS will transform it, via Grunt or Gulp, into the code we need.

<pre><code class="language-css">@font-face {
  font-family: 'My Font';
  font-path: '/path/to/font/file';
  font-weight: normal;
  font-style: normal;
}</code></pre>

As of the writing of this post, over 100 community plugins are currently available that allow for such things as future CSS syntax, shortcuts, tools and extensions of the language. It is beyond a “cool tool,” and it currently counts WordPress, Google and Twitter teams among its user base.</p>

## Adding PostCSS To Your Workflow

Because PostCSS is written in JavaScript, we can use task runners like <a href="https://gulpjs.com/">Gulp</a> and <a href="https://gruntjs.com/">Grunt</a> to transform the CSS in our projects. The tutorial below demonstrates how to incorporate PostCSS in your workflow via either Gulp or Grunt. Using one tool over the other is not crucial and is simply a matter of personal preference or what’s best for the project.

<strong>Note:</strong> A complete version of both the Gulp and Grunt versions of the tool is <a href="https://github.com/drewminns/postCSS-starter">available on GitHub</a>. Feel free to use it as a starter template and to expand on it as needed.</p>

### Setting Up PostCSS With Gulp

If you are unfamiliar with Gulp, I’d recommend reading “<a href="https://www.smashingmagazine.com/2014/06/building-with-gulp/">Building With Gulp</a>” by Callum Macrae to get up and running with the tool.

To install the PostCSS module in your project, run the following command in your terminal: <code>npm i gulp-postcss -D</code>.

In your project’s <code>Gulpfile.js</code>, we need to require our installed PostCSS module and then use it within a task. Be sure to update the paths to your development files and the directory where the transformed output will go.

<pre><code class="language-javascript">var postcss = require('gulp-postcss');

gulp.task('styles', function () {
    return gulp.src('path/to/dev/style.css')
        .pipe(postcss([]))
        .pipe(gulp.dest(path/to/prod))
});</code></pre>

To run the task, type <code>gulp styles</code> in the command line.</p>

### Setting Up PostCSS With Grunt

<strong>Note:</strong> If you are unfamiliar with Grunt, I’d recommend reading “<a href="https://www.smashingmagazine.com/2013/10/get-up-running-grunt/">Get Up and Running With Grunt</a>” by Mike Cunsolo to get comfortable with the tool.

To install the PostCSS module in your project, run the following command in the terminal: <code>npm i grunt-postcss -D</code>.

Once the plugin is installed on your system, enable it within the Gruntfile and create a task, as below. Be sure to update the <code>cwd</code> and <code>dest</code> values to reflect the structure of your app.

<pre><code class="language-javascript">module.exports = function(grunt) {
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    styles: {
      options: {
        processors: []
      },
      dist: {
        files: [{
          expand: true,
          cwd: 'dev/',
          src: ['**/*.css'],
          dest: 'prod/'
        }]
      }
    }
  });

  // Load post-css.
  grunt.loadNpmTasks('grunt-postcss');

};</code></pre>

To run the task, type <code>grunt styles</code> in the command line.</p>

### Installing Plugins

Using PostCSS on its own is not entirely powerful; its strength lies in the plugins. You may have noticed that in the Gulp and Grunt implementations above there were empty arrays in the task declarations. These arrays are where we can import community-developed PostCSS plugins, the features we want to include in our tool.

A list of approved PostCSS plugins can be found on <a href="https://github.com/postcss/postcss">PostCSS’ GitHub page</a> and, like all NPM packages, the plugins can be installed through the command line. Many plugins can be used only as extensions of PostCSS and are agnostic to the task runner you are using. For this example, we will install the <a href="https://github.com/postcss/postcss-focus">PostCSS Focus</a> plugin, which will add a <code>:focus</code> to every hover state.

With all of the plugins in the following examples, we will need to use the command line and NPM to install the packages in our projects.</p>

### PostCSS Plugin Installation Example

<pre><code class="language-bash">npm i postcss-focus -D</code></pre>

The plugins can be passed into the method directly; however, for the sake of cleanliness, we can construct an array and pass it in as an argument. In the array, we can include the necessary <code>require</code> statements that return the plugins and that are then called immediately. If you would like to read more about this concept, look through “<a href="https://ryanchristiani.com/functions-as-first-class-citizens-in-javascript/">Functions as First-Class Citizens in JavaScript</a>” by Ryan Christiani.

<pre><code class="language-javascript">require('postcss-focus')()</code></pre>

The modified code for Grunt, with our newly created <code>processorArray</code> arrays, is below:

<pre><code class="language-javascript">var processorArray = [
    require('postcss-plugin')()
];

// Snipped for brevity
styles: {
      options: {
        processors: processorArray
      },
      dist: {
        src: 'path/to/dev/style.css',
        dest: 'path/to/prod/style.css'
      }
    }</code></pre>

And here is the modified code for Gulp:

<pre><code class="language-javascript">var processorArray = [
    require('postcss-plugin')()
];

gulp.task('styles', function () {
    gulp.src('path/to/dev/style.css')
        .pipe(postcss(processorArray))
        .pipe(gulp.dest('path/to/prod'))
});
</code></pre>

## Plugins

Once we have installed a plugin and our build tool is prepared to compile our code, we can use PostCSS and the plugin features. The first thing to do is create a file with a <code>.css</code> extension in the directory where we store our development code.

“Wait! A CSS file?” Yup, a CSS file. Because PostCSS transforms our CSS, we don’t need to use a specialized syntax — just traditional CSS. If you are familiar with preprocessors, then it might feel unnatural to leave the <code>.sass</code>, <code>.scss</code>, <code>.styl</code> or <code>.less</code> files behind and return to <code>.css</code>. But, in fact, it’s not converting — it’s transforming.

To process our styles with our newly installed PostCSS plugins, we can run our task runners with <code>grunt styles</code> and <code>gulp styles</code>, respectively. Our development CSS file will be processed through the PostCSS plugin and the plugins provided, and then it will be outputted to our specified production directory.

Below are a few plugins of note that might be of benefit as you get started with PostCSS. Included are instructions on installing and using the plugin.</p>

### Autoprefixer

Writing styles to work on a wide gamut of browsers and devices can be a pain, and keeping up to date with which properties and values need a vendor prefix is a challenge in itself. Luckily, <a href="https://github.com/postcss/autoprefixer">Autoprefixer</a> figures out where and when to provide vendor prefixes. The plugin frees us to write styles with modern features and properties in mind, while taking care of vendor prefixes on the properties and values that need them.

Here is how to install this plugin via the command line:

<pre><code class="language-bash">npm i autoprefixer -D</code></pre>

When we add the plugin to our array, we can provide an object that contains an array of the browser scope the project will need to support. A list of options that can be provided is found at the <a href="https://github.com/ai/browserslist">Browserslist Github Account</a>.

Let’s add the Autoprefixer plugin to our processors:

<pre><code class="language-javascript">var processorsArray = [
  // snipped for brevity
  require('autoprefixer')({ browsers: ['last 2 versions', 'ie 6-8', 'Firefox &gt; 20']  })
];</code></pre>

The appropriate vendor prefixes will be outputted to any CSS properties and values in our styles that need them, according to the object provided.

Here is the development CSS:

<pre><code class="language-css">.item {
  display: flex;
  flex-flow: row wrap;
}</code></pre>

And here is the transformed output:

<pre><code class="language-css">.item {
  display: -webkit-flex;
  display: -ms-flexbox;
  display: -webkit-box;
  display: flex;
  -webkit-flex-flow: row wrap;
      -ms-flex-flow: row wrap;
          flex-flow: row wrap;
}</code></pre>

### Using Future Syntaxes With CSSNext

CSS4 will soon be upon us, and with it comes features such as <a href="https://www.w3.org/TR/css-variables/">native variables</a>, <a href="https://drafts.csswg.org/mediaqueries/#custom-mq">custom media queries</a>, <a href="https://drafts.csswg.org/css-extensions/#custom-selectors">custom selectors</a> and new <a href="https://drafts.csswg.org/selectors-4/#negation">pseudo-links</a>. While they are not yet supported in all browsers as of the writing of this article, they will be implemented in modern browsers as the specification gets approved.

<a href="https://cssnext.io/">CSSNext</a> is a tool that transforms any CSS4 features and properties into CSS3 that browsers can read. The tool can be used on its own or as a plugin through PostCSS. Again, we can add it to <code>processorsArray</code>, which contains our other PostCSS plugins.

Install the CSSNext plugin via the command line, like so:

<pre><code class="language-bash">npm i cssnext -D</code></pre>

Then, add the plugin to your processors:

<pre><code class="language-javascript">var processorsArray = [
  // snipped for brevity
  require('cssnext')()
];</code></pre>

Now, in your production code, you can write CSS4 features, and PostCSS will transform the syntax through the task runner, thereby supporting today’s browsers. When browsers come to support the newer syntax, you can replace the transformed output with the development CSS.

Here is the development CSS:

<pre><code class="language-css">// Custom Variables
:root {
  --linkColour: purple;
}

a {
  color: var(--linkColour);
}

// Custom media queries with ranges
@custom-media --only-medium-screen (width &gt;= 500px) and (width &lt;= 1200px);

@media (--only-medium-screen) {
  /* Medium viewport styles */
}

// Custom selectors
@custom-selector :--enter :hover, :focus;
@custom-selector :--input input, .input, .inputField;

a:--enter {
  /* Enter styles go here */
}

:--input {
  /* Input field styles go here */
}
</code></pre>

And here is the transformed output:

<pre><code class="language-css">a {
  color: purple;
}

@media (min-width:500px) and (max-width:1200px){
  body{
    background:#00f;
  }
}

a:focus,a:hover{
  background:#00f;
}

.input, .inputField, input{
  background:red;
}</code></pre>

If you would like to explore more CSSNext features, the website has a <a href="https://cssnext.io/playground/">playground</a> where you can experiment with current CSSNext-supported CSS4 features.</p>

### Sass Syntax

If Sass is your go-to preprocessor language, fear not: You can use the syntax and its tools with PostCSS. While traditional CSS doesn’t yet support variables, nesting and imports, plugins such as <a href="https://github.com/jonathantneal/precss">PreCSS</a> allow us to use these features and to write Sass syntax in our traditional CSS files.

If we add the plugin to our build via the command line and refer to the package in our array, we can start writing in Sass syntax immediately. If you’re making the switch from Sass to PostCSS, you can change the file extension to <code>.css</code> and immediately pipe it through your task runner.

Install the PreCSS plugin via the command line, like so:

<pre><code class="language-bash">npm i precss -D</code></pre>

And add the plugin to your processors:

<pre><code class="language-javascript">var processorsArray = [
  // snipped for brevity
  require('precss')()
];</code></pre>

Again, here is the development CSS:

<pre><code class="language-scss">/*Variables*/
$blue: #0000ff;
$green: #00ff00;
$radius: 10px;

.square {
  background: $blue;
  border-radius: $radius;
}

/*Imports*/
@import "partials/_base.css";

/*Mixins*/
@define-mixin square $dimension {
    width: $dimension;
    height: $dimension;
}

/*Nesting, variables and mixins*/
.button {
  @mixin square 200px;
  background: $green;
  &amp;:hover {
    background: $blue;
  }
}</code></pre>

And the transformed output:

<pre><code class="language-css">.square {
  background: #0000ff;
  border-radius: 10px;
}

.button {
  width: 200px;
  height: 200px;
  background: #00ff00;
}

.button:hover {
  background: #0000ff;
}</code></pre>

## Extending CSS With Community Plugins

While plugins are available to help us write code more efficiently, the power of PostCSS lies in the community plugins. These plugins give us quicker ways to write styles, or at least easier ways to implement creative styling. Using the PostCSS API, these plugins allow for custom properties, selectors and values in our projects, enabling us to write styles more efficiently and with less Googling.</p>

### Quantity Queries

<a href="https://github.com/pascalduez/postcss-quantity-queries">Quantity queries</a> are powerful. They allow us to <a href="https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/">count elements with CSS</a> and apply styles based on their number of siblings. While the selectors are a bit tricky to write, because they use some advanced CSS selectors, you can <a href="https://www.smashingmagazine.com/2015/07/constructing-css-quantity-queries-on-the-fly/">use them in your CSS today</a>. While online tools like <a href="https://quantityqueries.com/">QQ</a> exist to help us write these queries, we can use PostCSS to use custom selectors in our styles directly.

To use quantity queries, install the Quantity Queries plugin in your project like any other, via the command line:

<pre><code class="language-bash">npm i postcss-quantity-queries -D</code></pre>

And add the plugin to your processors:

<pre><code class="language-javascript">var processors = [
  // Snipped for brevity
  require('postcss-quantity-queries')()
];</code></pre>

Once it’s installed, you can use custom selectors, available only through the plugin, to apply styles based on matched elements.

Here is the development CSS:

<pre><code class="language-css">// To apply styles if 'at least' number of sibling elements present
.container &gt; .item:at-least(5) {
  background: blue;
}

// To apply styles if 'at most' number of sibling elements present
.item &gt; a:at-most(10) {
  color: green;
}

// To apply styles if number of sibling items 'between' a range is present
.gallery &gt; img:between(4, 7) {
  width: 25%;
}

// To apply styles if 'exactly' number of provided items is present
.profiles:exactly(4) {
  flex: 1 0 50%;
}</code></pre>

And the transformed output:

<pre><code class="language-css">// To apply styles if 'at least' number of sibling elements present
.container &gt; .item:nth-last-child(n+5), .container &gt; .item:nth-last-child(n+5) ~ .item {
  background: blue;
}

// To apply styles if 'at most' number of sibling elements present
.item &gt; a:nth-last-child(-n+10):first-child, .item &gt; a:nth-last-child(-n+10):first-child ~ a {
  color: green;
}

// To apply styles if number of sibling items 'between' a range is present
.gallery &gt; img:nth-last-child(n+4):nth-last-child(-n+7):first-child, .gallery &gt; img:nth-last-child(n+4):nth-last-child(-n+7):first-child ~ img {
  width: 25%;
}

// To apply styles if 'exactly' number of provided items is present
.profiles:nth-last-child(4):first-child, .profiles:nth-last-child(4):first-child ~ .profiles {
      flex: 1 0 50%;
}</code></pre>

### Extended Shorthand Properties With Short

When writing styles, you might encounter properties whose syntax makes you say, “That could be shorter.” Luckily, the <a href="https://github.com/jonathantneal/postcss-short">Short</a> plugin helps us do just that: write our styles more logically. It enables us to write shorthand properties for <code>position</code> and <code>size</code>, much like how <code>background</code> and <code>font</code> can be condensed into a single declaration.

Through the PostCSS API, the shorthand declarations are transformed into browser-digestible styles, allowing for a cleaner development style sheet and a more organized production style sheet.

Install Short via the command line:

<pre><code class="language-bash">npm i postcss-short -D</code></pre>

Add the plugin to your processors:

<pre><code class="language-javascript">var processors = [
  require('postcss-short')()
];</code></pre>

The <code>text</code> property includes these typographical properties: <code>color</code>, <code>font-style</code>, <code>font-variant</code>, <code>font-weight</code>, <code>font-stretch</code>, <code>text-decoration</code>, <code>text-align</code>, <code>text-rendering</code>, <code>text-transform</code>, <code>white-space</code>, <code>font-size</code>, <code>line-height</code>, <code>letter-spacing</code>, <code>word-spacing</code> and <code>font-family</code>.

And here is the development CSS:

<pre><code class="language-css">p {
  text: 300 uppercase dimgrey center 1.6rem 1.7 .05em;
}</code></pre>

And the transformed output:

<pre><code class="language-css">p {
  color: dimgrey;
  font-weight: 300;
  text-align: center;
  text-transform: uppercase;
  font-size: 25px;
  font-size: 1.6rem;
  line-height: 1.7;
  letter-spacing: .05em;
}</code></pre>

The <code>position</code> property allows for <code>top</code>, <code>left</code>, <code>right</code>, <code>bottom</code> values to be included in the declaration. The <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties#Tricky_edge_cases">order of the values</a> is clockwise, in a syntax with values from <code>1</code> to <code>4</code>. If there is a value you care to exclude, simply pass an <code>*</code> in its place.

Here is the development CSS, then:

<pre><code class="language-css">section {
  position: absolute 10px * *;
}

.topNav {
  position: fixed 0 * * 0;
}

.modal {
  position: fixed 40% 25%;
}</code></pre>

And the transformed output:

<pre><code class="language-css">section {
  position: absolute;
  top: 10px;
}

.topNav {
  position: fixed;
  top: 0;
  left: 0;
}

.modal {
  position: fixed;
  top: 40%;
  right: 25%;
  bottom: 40%;
  left: 25%;
}</code></pre>

## What Does This Mean For Our Industry?

<pre><code class="language-bash">npm i cssnext -D</code></pre>

Then, add the plugin to your processors:

<pre><code class="language-javascript">var processorsArray = [
  // snipped for brevity
  require('cssnext')()
];</code></pre>

Now, in your production code, you can write CSS4 features, and PostCSS will transform the syntax through the task runner, thereby supporting today’s browsers. When browsers come to support the newer syntax, you can replace the transformed output with the development CSS.

Here is the development CSS:

<pre><code class="language-css">// Custom Variables
:root {
  --linkColour: purple;
}

a {
  color: var(--linkColour);
}

// Custom media queries with ranges
@custom-media --only-medium-screen (width &gt;= 500px) and (width &lt;= 1200px);

@media (--only-medium-screen) {
  /* Medium viewport styles */
}

// Custom selectors
@custom-selector :--enter :hover, :focus;
@custom-selector :--input input, .input, .inputField;

a:--enter {
  /* Enter styles go here */
}

:--input {
  /* Input field styles go here */
}
</code></pre>

And here is the transformed output:

<pre><code class="language-css">a {
  color: purple;
}

@media (min-width:500px) and (max-width:1200px){
  body{
    background:#00f;
  }
}

a:focus,a:hover{
  background:#00f;
}

.input, .inputField, input{
  background:red;
}</code></pre>

If you would like to explore more CSSNext features, the website has a <a href="https://cssnext.io/playground/">playground</a> where you can experiment with current CSSNext-supported CSS4 features.</p>

### Sass Syntax

If Sass is your go-to preprocessor language, fear not: You can use the syntax and its tools with PostCSS. While traditional CSS doesn’t yet support variables, nesting and imports, plugins such as <a href="https://github.com/jonathantneal/precss">PreCSS</a> allow us to use these features and to write Sass syntax in our traditional CSS files.

If we add the plugin to our build via the command line and refer to the package in our array, we can start writing in Sass syntax immediately. If you’re making the switch from Sass to PostCSS, you can change the file extension to <code>.css</code> and immediately pipe it through your task runner.

Install the PreCSS plugin via the command line, like so:

<pre><code class="language-bash">npm i precss -D</code></pre>

And add the plugin to your processors:

<pre><code class="language-javascript">var processorsArray = [
  // snipped for brevity
  require('precss')()
];</code></pre>

Again, here is the development CSS:

<pre><code class="language-scss">/*Variables*/
$blue: #0000ff;
$green: #00ff00;
$radius: 10px;

.square {
  background: $blue;
  border-radius: $radius;
}

/*Imports*/
@import "partials/_base.css";

/*Mixins*/
@define-mixin square $dimension {
    width: $dimension;
    height: $dimension;
}

/*Nesting, variables and mixins*/
.button {
  @mixin square 200px;
  background: $green;
  &amp;:hover {
    background: $blue;
  }
}</code></pre>

And the transformed output:

<pre><code class="language-css">.square {
  background: #0000ff;
  border-radius: 10px;
}

.button {
  width: 200px;
  height: 200px;
  background: #00ff00;
}

.button:hover {
  background: #0000ff;
}</code></pre>

## Extending CSS With Community Plugins

While plugins are available to help us write code more efficiently, the power of PostCSS lies in the community plugins. These plugins give us quicker ways to write styles, or at least easier ways to implement creative styling. Using the PostCSS API, these plugins allow for custom properties, selectors and values in our projects, enabling us to write styles more efficiently and with less Googling.</p>

### Quantity Queries

<a href="https://github.com/pascalduez/postcss-quantity-queries">Quantity queries</a> are powerful. They allow us to <a href="https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/">count elements with CSS</a> and apply styles based on their number of siblings. While the selectors are a bit tricky to write, because they use some advanced CSS selectors, you can <a href="https://www.smashingmagazine.com/2015/07/constructing-css-quantity-queries-on-the-fly/">use them in your CSS today</a>. While online tools like <a href="https://quantityqueries.com/">QQ</a> exist to help us write these queries, we can use PostCSS to use custom selectors in our styles directly.

To use quantity queries, install the Quantity Queries plugin in your project like any other, via the command line:

<pre><code class="language-bash">npm i postcss-quantity-queries -D</code></pre>

And add the plugin to your processors:

<pre><code class="language-javascript">var processors = [
  // Snipped for brevity
  require('postcss-quantity-queries')()
];</code></pre>

Once it’s installed, you can use custom selectors, available only through the plugin, to apply styles based on matched elements.

Here is the development CSS:

<pre><code class="language-css">// To apply styles if 'at least' number of sibling elements present
.container &gt; .item:at-least(5) {
  background: blue;
}

// To apply styles if 'at most' number of sibling elements present
.item &gt; a:at-most(10) {
  color: green;
}

// To apply styles if number of sibling items 'between' a range is present
.gallery &gt; img:between(4, 7) {
  width: 25%;
}

// To apply styles if 'exactly' number of provided items is present
.profiles:exactly(4) {
  flex: 1 0 50%;
}</code></pre>

And the transformed output:

<pre><code class="language-css">// To apply styles if 'at least' number of sibling elements present
.container &gt; .item:nth-last-child(n+5), .container &gt; .item:nth-last-child(n+5) ~ .item {
  background: blue;
}

// To apply styles if 'at most' number of sibling elements present
.item &gt; a:nth-last-child(-n+10):first-child, .item &gt; a:nth-last-child(-n+10):first-child ~ a {
  color: green;
}

// To apply styles if number of sibling items 'between' a range is present
.gallery &gt; img:nth-last-child(n+4):nth-last-child(-n+7):first-child, .gallery &gt; img:nth-last-child(n+4):nth-last-child(-n+7):first-child ~ img {
  width: 25%;
}

// To apply styles if 'exactly' number of provided items is present
.profiles:nth-last-child(4):first-child, .profiles:nth-last-child(4):first-child ~ .profiles {
      flex: 1 0 50%;
}</code></pre>

### Extended Shorthand Properties With Short

When writing styles, you might encounter properties whose syntax makes you say, “That could be shorter.” Luckily, the <a href="https://github.com/jonathantneal/postcss-short">Short</a> plugin helps us do just that: write our styles more logically. It enables us to write shorthand properties for <code>position</code> and <code>size</code>, much like how <code>background</code> and <code>font</code> can be condensed into a single declaration.

Through the PostCSS API, the shorthand declarations are transformed into browser-digestible styles, allowing for a cleaner development style sheet and a more organized production style sheet.

Install Short via the command line:

<pre><code class="language-bash">npm i postcss-short -D</code></pre>

Add the plugin to your processors:

<pre><code class="language-javascript">var processors = [
  require('postcss-short')()
];</code></pre>

The <code>text</code> property includes these typographical properties: <code>color</code>, <code>font-style</code>, <code>font-variant</code>, <code>font-weight</code>, <code>font-stretch</code>, <code>text-decoration</code>, <code>text-align</code>, <code>text-rendering</code>, <code>text-transform</code>, <code>white-space</code>, <code>font-size</code>, <code>line-height</code>, <code>letter-spacing</code>, <code>word-spacing</code> and <code>font-family</code>.

And here is the development CSS:

<pre><code class="language-css">p {
  text: 300 uppercase dimgrey center 1.6rem 1.7 .05em;
}</code></pre>

And the transformed output:

<pre><code class="language-css">p {
  color: dimgrey;
  font-weight: 300;
  text-align: center;
  text-transform: uppercase;
  font-size: 25px;
  font-size: 1.6rem;
  line-height: 1.7;
  letter-spacing: .05em;
}</code></pre>

The <code>position</code> property allows for <code>top</code>, <code>left</code>, <code>right</code>, <code>bottom</code> values to be included in the declaration. The <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties#Tricky_edge_cases">order of the values</a> is clockwise, in a syntax with values from <code>1</code> to <code>4</code>. If there is a value you care to exclude, simply pass an <code>*</code> in its place.

Here is the development CSS, then:

<pre><code class="language-css">section {
  position: absolute 10px * *;
}

.topNav {
  position: fixed 0 * * 0;
}

.modal {
  position: fixed 40% 25%;
}</code></pre>

And the transformed output:

<pre><code class="language-css">section {
  position: absolute;
  top: 10px;
}

.topNav {
  position: fixed;
  top: 0;
  left: 0;
}

.modal {
  position: fixed;
  top: 40%;
  right: 25%;
  bottom: 40%;
  left: 25%;
}</code></pre>

## What Does This Mean For Our Industry?

Using PostCSS today and reaping the benefits are completely possible. Much like how we compile Sass and LESS, you can incorporate it in your workflow by modifying your task runner to process PostCSS. Incorporating a plugin like PreCSS allows your existing Sass projects to be ported over to PostCSS without needing any conversion of the syntax.

As of the writing of this article, a discussion is ongoing about where is the best place to write our CSS. With libraries such as <a href="https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/">React</a> gaining popularity, the idea of writing styles <a href="https://facebook.github.io/react/tips/inline-styles.html">within the components</a> themselves, which allows us to transform styles with JavaScript directly on compilation, is gaining momentum. While this is still very much a discussion, it is indeed one way to transform styles with PostCSS.

Another project making waves in the industry is <a href="https://github.com/css-modules/css-modules">CSS Modules</a>, which scopes styles to local files and requires them as needed. This concept is already popular in JavaScript circles. And as the lines between front-end languages such as <a href="https://facebook.github.io/react/docs/jsx-in-depth.html">React and JSX</a> continue to blur, it becomes hard to ignore the combined power of CSS and JavaScript.

While PostCSS extends CSS in brand new ways through custom syntaxes and properties, it could present challenges to beginners who are trying to get comfortable with the language and its intricacies. If you use PostCSS in a project with a junior developer, try to encourage in them a deep understanding of the language and of how PostCSS, much like Sass, is simply a production tool that allows styles to be written efficiently.</p>

## Adopting PostCSS Today

Over the next few years, the way we use CSS will change in many different ways. Every project will have different requirements, to which we will have to adapt our production methods. Working within a modular ecosystem like PostCSS allows us to pick and choose the features we want to complete a project.

I encourage you to explore the PostCSS world and all of the plugins available in it. Because it is a community project, the ecosystem will grow only if people use it and create plugins. To explore more plugins, view the <a href="https://www.npmjs.com/browse/keyword/postcss-plugin">available packages</a> on NPM and test their abilities in the <a href="https://sneakertack.github.io/postcss-playground/">Post CSS Playground</a>.

{{< signature "rb, al, ml" >}}

