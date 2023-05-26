---
title: 'Pattern Library First: An Approach For Managing CSS'
slug: pattern-library-first-css
author: rachel-andrew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40d6ffb9-61a3-4715-ac63-7a65a466e926/component-layout.png
date: 2018-07-09T14:00:35+02:00
summary: >
  CSS can be hard to manage across a project, especially when you need to include media queries for various breakpoints and fallbacks for older browsers. In this article, we will take a look at using Fractal to manage components which use CSS Grid.
description: >
  CSS can be hard to manage across a project, especially when you need to include media queries for various breakpoints and fallbacks for older browsers. In this article, we will take a look at using Fractal to manage components which use CSS Grid.
categories:
  - CSS
  - Workflow
  - Pattern Libraries
---
<p>In this article, based on the talk that I gave at Smashing Conference in Toronto, I’m going to describe a method of working that I’ve adopted over the past two years that helps me to manage CSS across my projects.</p>

<p>I’ll be showing you how to use the pattern library tool <a href="https://fractal.build/">Fractal</a>, to manage your CSS on a component by component basis, while allowing you to use the tools you are already familiar with. While this serves as an introduction to Fractal, and why we have selected this particular pattern library, it is likely this way of working would transfer to other solutions. </p>

### Our Projects

<p>My company has a couple of products &mdash; Perch and Perch Runway CMS and Notist, a software as a service application for public speakers. These products are quite different, especially given that Perch is a self-hosted system and Notist is SaaS, however, they both have a lot of user interface to develop. We also have all of the associated websites and documentation for these products, plus other things that we work on such as the 24 Ways website. After discovering Fractal two years ago, we have moved every new project &mdash; large and small &mdash; into Fractal.</p>

### Problems we wanted to solve

<p>I began investigating pattern library solutions two years ago when I started work rebuilding the Perch UI for version 3. A feature of Perch is that the templates you create for the output of content on your website become the schema of the admin UI. This means that any fieldtype used in a template needs to be able to exist alongside any other fieldtype. We don’t know how our customers might combine these, and there are a huge number of possible combinations. It's also not a "website", and I didn't want to try and force the pattern library into something designed for organizing website patterns.</p>

<p>As Perch is self-hosted &mdash; people download it and host it on their own servers &mdash; we need to use the simplest tech stack possible in order to not place any additional barriers to entry in front of people, many of who are new to using a CMS. To add an extra level of fun, we support back to Internet Explorer 9, yet I intended to use a lot of Flexbox &mdash; as this was before Grid Layout shipped.</p>

{{% feature-panel %}}

<p>I was also keen to avoid using tools which came with a lot of relearning how we worked, and completely changing our process. Any additional tool or change to the way that you work on your projects brings with it new friction. You can solve one problem, but bring in a whole new set of problems if you make large changes to the way that you work. In our case, we were using Sass in a fairly limited way, and processing that using Gulp. None of our projects use a Javascript framework, we’re just writing HTML, CSS and JavaScript.</p>

<p>Fractal fit our needs perfectly. It is agnostic as to the way you develop or the tools you want to use. Importantly for our purposes, it didn’t assume we were building a website. The experiment was so successful that we found ourselves using Fractal for every project large or small, as it makes the process of working on CSS far more straightforward. Even small sites I create on my own often start life in Fractal, because there are more benefits than you might think in terms of working with a pattern library, and many of those benefits make as much sense for a team of one as a large team.</p>

<p>Before we think about how to develop using Fractal and why I think it makes sense for small projects as well as large ones, let’s take a look at how to get the environment set up.</p>

### Getting Started With Fractal

<p>The most straightforward approach for working with Fractal is to go to the Fractal website and take a look at the <a href="https://fractal.build/guide/getting-started">Getting Started Guide</a>. You will first need to install Fractal globally, you can then follow the steps listed here to create a new Fractal project.</p>

<p>With your new project installed, at the command line change into the folder you have just created and run the command:</p>

<pre><code class="language-bash">fractal start --sync</code></code></pre>

<p>This will start up a little server at port 3000, so you should be able to go to <code>https://localhost:3000</code> in a web browser and see your project.</p>

<p>Now that your project is up and running, open up the project folder in your favorite text editor and find the example component under <code>components/example</code>. You will find a config file and a file named <em>example.hbs</em>. The <em>example.hbs</em> template is the HTML of your component, you can add some more HTML to that and Fractal will automatically reload and display it. Change the file to:</p>

<pre><code class="language-html">&#x3C;h1&#x3E;This is my heading&#x3C;/h1&#x3E;
&#x3C;p&#x3E;{{ text }}&#x3C;/p&#x3E;</code></pre>

<p>You should see the heading appear in the browser. The config file can be used to add content and otherwise configure your component. If you want to read your heading text out of that file then edit that file to look like the following example:</p>

<pre><code class="language-html">title: Example component
context:
    text: This is an example component!
    heading: My heading</code></pre>

<p>Now change your <em>example.hbs</em> file to read in that text.</p>

<pre><code class="language-html">&#x3C;h1&#x3E;{{ heading }}&#x3C;/h1&#x3E;
&#x3C;p&#x3E;{{ text }}&#x3C;/p&#x3E;</code></pre>

#### Adding Additional Components

<p>You can follow the pattern of the example component to add your own. At a minimum, you need a folder (the name of the component) and a <em>.hbs</em> file using the same name. You can add the config file if you want to set configuration options.</p>

<p>Components can be nested into folders to make it easier to locate particular components, and how you structure the folders is completely up to you.</p>

<p><strong>Note</strong>: <em>It is really easy to find yourself spending a lot of time worrying about how to name your components. In Fractal at least, renaming and also reorganizing components into folders is straightforward. You can rename or move them and Fractal will update to show the new structure. I find that often the ideal structure only becomes apparent as I’m developing so I don’t worry too much at the outset and then firm it up later.</em></p>

### Adding a CSS Workflow

<p>So far, we are able to create HTML components as handlebars templates, and a config file to insert data, however, we haven’t added any CSS. Ideally, we want to add the CSS for each component into the same folder as the rest of the component files and then combine it all together.</p>

<p>I mentioned that Fractal makes very few assumptions about your workflow; due to this, it does far less out of the box than it might if it were forcing you down a particular way of working. However, we can fairly easily get Fractal working with a Gulp setup.</p>

#### Combining Fractal, Sass, And Gulp

<p>The following describes a minimal setup using Gulp and Sass to create a single output CSS file. Hopefully, you can follow this process to do anything else that you would normally do in Gulp. The key thing to note is that most of this is not Fractal specific, so once you get the Fractal part working you can add in anything else following the same patterns. If you are familiar with another build tool then it is likely that you could create a similar process; if you do, and are happy to share, let us know in the comments.</p>

<p>First some setup, the following will enable you to follow along with the code listed in this tutorial, the locations of your Sass files and output CSS might ultimately be different to mine. The key thing is that the output CSS file needs to be somewhere in the public folder.</p>

<ol>
    <li>Inside the <em>public</em> folder in your Fractal install, add a folder named <em>css</em>.</li>
    <li>In the root folder of your Fractal, install add a folder <em>assets</em> inside which is a folder <em>scss</em>. Create a Sass file named <em>global.scss</em> inside that folder. Inside that file add the following line:<br/>

    <pre><code class="language-html">@import &quot;../../components/**/*.scss&quot;;</code></pre>
  </li>
    <li>Create a file named <em>example.scss</em> in your <code>example</code> component directory.</li>
    <li>Create <em>gulpfile.js</em> in the root of your Fractal project and add the below code.</li>
</ol>

<pre><code class="language-javascript">'use strict';

const gulp         = require('gulp');
const fractal      = require('./fractal.js');
const logger       = fractal.cli.console;
const sass         = require('gulp-sass');
const sassGlob     = require('gulp-sass-glob');
const plumber      = require('gulp-plumber');
const notify       = require('gulp-notify');
const path         = require('path');

gulp.task('sass',function() {
    return gulp.src('assets/scss/**/*.scss')
    .pipe(customPlumber('Error running Sass'))
    .pipe(sassGlob())
    .pipe(sass())
    .pipe(gulp.dest('public/css'))
});

gulp.task('watch', ['sass'], function() {
   gulp.watch([
        'components/**/*.scss',
        'assets/scss/**/*.scss'
        ], ['sass']);
});

function customPlumber(errTitle) {
    return plumber({
        errorHandler: notify.onError({
            title: errTitle || "Error running Gulp",
            message: "Error: <%= error.message %>",
        })
    });
}

gulp.task('fractal:start', function(){
    const server = fractal.web.server({
        sync: true
    });
    server.on('error', err => logger.error(err.message));
    return server.start().then(() => {
        logger.success(`Fractal server is now running at ${server.url}`);
    });
});

gulp.task('default', ['fractal:start', 'sass', 'watch']);</code></pre>

<p>I then install the dependencies listed at the top of the file. If you were to install those at the command line you would run:</p>

<p><code>npm install gulp gulp-sass gulp-sass-glob gulp-plumber gulp-notify</code></p>

<p>The <code>sass</code> function compiles the Sass from assets into a single file, and outputs it into the folder in <code>public</code>.</p>

<pre><code class="language-javascript">gulp.task(&#39;sass&#39;,function() {
return gulp.src(&#39;src/assets/scss/**/*.scss&#39;)
.pipe(customPlumber(&#39;Error running Sass&#39;))
.pipe(sassGlob())
.pipe(sass())
.pipe(gulp.dest(&#39;public/css&#39;))
});
</code></pre>

<p>I then create a <code>watch</code> function that will watch my Sass in <code>assets</code> and also that in individual components and compile it into the folder in public.</p>

<pre><code class="language-javascript">gulp.task(&#39;watch&#39;, [&#39;sass&#39;], function() {
   gulp.watch([
&#39;components/**/*.scss&#39;,
&#39;assets/scss/**/*.scss&#39;
], [&#39;sass&#39;]);
});
</code></pre>

<p>That’s my CSS building. I now want to make it so that I can run gulp and it will kick off the watching of the CSS file as well as starting fractal. I do this by creating a gulp task to run the fractal start command.</p>

<pre><code class="language-javascript">gulp.task(&#39;fractal:start&#39;, function(){
const server = fractal.web.server({
sync: true
});
server.on(&#39;error&#39;, err =&gt; logger.error(err.message));
return server.start().then(() =&gt; {
logger.success(Fractal server is now running at ${server.url});
});
});</code></pre>

<p>Finally, I need to ensure that the Sass building and Fractal start run when I run gulp and the command line:</p>

<p><code class="language-javascript">gulp.task(&#39;default&#39;, &#39;fractal:start&#39;, &#39;sass&#39;, &#39;watch&#39;);</code></p>

<p>That’s my completed <em>gulpfile.js</em>. If you add this into your default Fractal project, make sure the folders are in place for the paths mentioned. You should be able to go to the command line, run <code>gulp</code>, and Fractal will start.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f5f567-218a-4813-9ccd-dfffbadbcfb7/cli.png" sizes="100vw" caption="Starting Fractal with gulp (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f5f567-218a-4813-9ccd-dfffbadbcfb7/cli.pngg'>View large version</a>)" alt="Commandline output" >}}

<p>We can test out our Sass by adding a variable in the <em>global.scss</em> file; you will need to add this above the line that includes the components so that the variable is available for those components.</p>

<pre><code class="language-css">$color1: rebeccapurple;</code></pre>

<p>Then in <code>example.scss</code> add a rule for the level 1 heading we added earlier:</p>

<pre><code class="language-css">h1 {
  color: $color1;
}</code></pre>

<p>If everything is set up correctly, you should find you have a <em>.css</em> file in public/css which contains the rule:</p>

<pre><code class="language-css">h1 {
  color: rebeccapurple;
}</code></pre>

<p>We need to do one more thing so that we can preview our components using the CSS we are building. We need to create a preview file, which will link in the stylesheet from the public folder. </p>

<p>Inside your components folder, create a file named <em>_preview.hbs</em>.</p>

<p>The preview file is essentially an HTML document, linking in our CSS and anything else you need to include. In the body is a tag <code>{{ yield }}</code>, and this is where a component will be placed.</p>

<div class="break-out">

 <pre><code class="language-html">&#x3C;!doctype html&#x3E;
&#x3C;html lang=&#x22;en&#x22;&#x3E;
&#x3C;head&#x3E;
&#x9;&#x3C;meta charset=&#x22;utf-8&#x22; /&#x3E;
&#x9;&#x3C;title&#x3E;Preview Layout&#x3C;/title&#x3E;
&#x9;&#x3C;meta name=&#x22;viewport&#x22; content=&#x22;width=device-width, initial-scale=1, shrink-to-fit=no&#x22;&#x3E;
&#x9;&#x3C;link rel=&#x22;stylesheet&#x22; href=&#x22;{{ path &#x27;/css/global.css&#x27; }}&#x22;&#x3E;
&#x3C;/head&#x3E;
&#x3C;body&#x3E;
&#x9;{{{ yield }}}
&#x3C;/body&#x3E;
&#x3C;/html&#x3E;</code></pre>
</div>

<p><strong>Note</strong>: <em>The public folder can also house any other assets that you need to display in components such as images, fonts and so on.</em></p>

#### The Pattern Library As Source Of Truth

<p>As we have seen, Fractal can build our CSS. In our projects, we make it so that Fractal is the <em>only</em> place we build and process CSS and other assets for the site. What this means is that our pattern library and site or application do not drift. Drift happens after you deploy the site if people start editing the CSS of the site and not bringing those changes back to the pattern library. If you can make the pattern library the place where CSS is processed then changes have to start there &mdash; which prevents drift between the live site and library.</p>

<p>We build everything in Fractal and then copy those public assets over to the live sites to be deployed. In addition to preventing drift between the systems, it also makes managing CSS in source control much easier. When multiple people work on one CSS file, merge conflicts can be reasonably hard to deal with. With people working on individual components in the pattern library, you can usually avoid two people committing changes to the same file at once, and if they do it is only a small file to sort out and not all of your CSS.</p>

{{% ad-panel-leaderboard %}}

## Using A Pattern Library First Approach For Managing Fallbacks

<p>I have found that working pattern library first makes dealing with fallbacks in your code far more straightforward and less overwhelming than attempting to fix up a complete site or application at once. It also allows us to concentrate on the best possible case, and be creative with new techniques, rather than limit what we do due to being worried about how we will get it to work well in non-supporting browsers.</p>

<p>We can look at a simple case of a media object component to see how that might work. To follow along, create a <em>media</em> folder inside components in Fractal, and add the files <em>media.hbs</em> and <em>media.scss</em>.</p>

#### Start With Good Markup

<p>Your starting point should always be well-structured markup. In the pattern library, it may be that you will use this component with a range of markup, for example, you could use a component with content marked up as a figure in one place and just with divs in another. Your content should, however, be structured in a way that makes sense and can be read from top to bottom.</p>

<p>This ensures that your content is accessible at a very basic level, but it also means you can take advantage of normal flow. Normal Flow is how browsers display your content by default, with block elements progressing one after the other in the block dimension and inline elements &mdash; such as words in a sentence &mdash; running along the inline axis. For a lot of content that is exactly what you want, and by taking advantage of normal flow rather than fighting against it you make your job far easier as you create your layout.</p>

<p>Therefore, my component has the following markup which I add to <em>media.hbs</em>.</p>

<div class="break-out">

 <pre><code class="language-html">&#x3C;div class=&#x22;media&#x22;&#x3E;

  &#x3C;div class=&#x22;img&#x22;&#x3E;
    &#x3C;img src=&#x22;/img/placeholder.jpg&#x22; alt=&#x22;Placeholder&#x22;&#x3E;
  &#x3C;/div&#x3E;
  &#x3C;h2 class=&#x22;title&#x22;&#x3E;This is my title&#x3C;/h2&#x3E;
  &#x3C;div class=&#x22;content&#x22;&#x3E;
      &#x3C;p&#x3E;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis vehicula vitae ligula sit amet maximus. Nunc auctor neque ipsum, ac porttitor elit lobortis ac. Vivamus ultrices sodales tellus et aliquam. Pellentesque porta sit amet nulla vitae luctus. Praesent quis risus id dolor venenatis condimentum.&#x3C;/p&#x3E;
  &#x3C;/div&#x3E;
  &#x3C;div class=&#x22;footer&#x22;&#x3E;
    An optional footer goes here.
  &#x3C;/div&#x3E;
&#x3C;/div&#x3E;</code></pre>
</div>

<p>You can see how this then displays inside Fractal:</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb40e309-8190-48c4-ab26-83d7bb641ca8/component-markedup.png" sizes="100vw" caption="My component after adding the markup. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb40e309-8190-48c4-ab26-83d7bb641ca8/component-markedup.png'>View large version</a>)" alt="The fractal UI with the added component" >}}

<p>Once I’ve got the markup that I want, I am going to work on the desktop display that I have in mind. I’m going to use CSS Grid Layout and the <code>grid-template-areas</code> method of doing so. Add the following to <em>media.scss</em>.</p>

<pre><code class="language-css">img { max-width: 100%; }

.media &gt; .title { 
  grid-area: title; 
}

.media &gt; .img { 
  grid-area: img; 
}

.media &gt; .content { 
  grid-area: bd; 
}

.media &gt; .footer { 
  grid-area: ft; 
}

.media {
  margin-bottom: 2em;
  display: grid;
  grid-column-gap: 20px;
  grid-template-columns: 200px 3fr;
  grid-template-areas:
    &quot;img title&quot;
    &quot;img bd&quot;
    &quot;img ft&quot;;
  }</code></pre>

<p>We now have a simple media object layout:</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40d6ffb9-61a3-4715-ac63-7a65a466e926/component-layout.png" sizes="100vw" caption="The Media Object layout. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40d6ffb9-61a3-4715-ac63-7a65a466e926/component-layout.png'>View large version</a>)" alt="A two column layout, image on the left text on the right" >}}

<p>Something you can do in Fractal is to add variations of a component. You might want to flip the media object so that the image is on the right.</p>

<p>Now add the CSS to <em>media.scss</em> in order to flip the layout:</p>

<pre><code class="language-css">.media.media-flip {
grid-template-columns: 3fr 200px ;
grid-template-areas:
  &quot;title img&quot;
  &quot;bd img&quot;
  &quot;ft img&quot;;
  }
</code></pre>

<p>There are two ways to create variants: file-based and configuration based. File-based is simplest and is also useful if your variant has different markup. To create a file-based variant, make a copy of your component in the media folder with the name media <em>--flip.hbs</em> (that’s two dashes in the filename).</p>

<p>This component should have identical markup with the class <code>media-flip</code> added to the first line, and you will then be able to see both versions.</p>

<pre><code>&lt;div class=&quot;media media-flip&quot;&gt;</code></pre>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4498b4db-aec4-4fa9-ae93-d8f3d8253729/component-flipped.png" sizes="100vw" caption="The flipped version. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4498b4db-aec4-4fa9-ae93-d8f3d8253729/component-flipped.pngg'>View large version</a>)" alt="A two column layout, image on the right text on the left" >}}

<p>Alternately, as in this case all we need to do is add a class, you can create a variant using a config file.</p>

<p>If you want to do this, remove your variant file, and instead add a config file named <em>media.config.json</em> containing the following code:</p>

<pre><code class="language-javascript">{
    &quot;title&quot;: &quot;Media Object&quot;,
    &quot;context&quot;: {
        &quot;modifier&quot;: &quot;default&quot;
    },
    &quot;variants&quot;: [
        {
            &quot;name&quot;: &quot;Flipped&quot;,
            &quot;context&quot;: {
                &quot;modifier&quot;: &quot;flip&quot;
            }
        }
    ]
}
</code></pre>

<p>Then modify the first line of <em>media.hbs</em> as follows:</p>

<p><code class="language-html">&lt;div class=&quot;media media-{{ modifier }}&quot;&gt;</code></p>

<p><strong>Note</strong>: <em>You can add as many variants as you like (take a look at the <a href="https://fractal.build/guide/components/variants">documentation for variants</a> to read more).</em></p>

<p>We might now think about adding some CSS to change the layout based on screen size. Wrapping the layout we have created in a media query and above that creating a single column layout for smaller devices.</p>

<pre><code class="language-css">img {
  max-width: 100%;
}

.media &gt; .title { 
  grid-area: title; 
}

.media &gt; .img { 
  grid-area: img; 
}

.media &gt; .content { 
  grid-area: bd; 
}

.media &gt; .footer { 
  grid-area: ft; 
}

.media {
  display: grid;
  grid-column-gap: 20px;
  grid-template-areas:
    &quot;title&quot;
    &quot;img&quot;
    &quot;bd&quot;
    &quot;ft&quot;;
  }

  @media (min-width: 600px) {
    .media {
      margin-bottom: 2em;
      display: grid;
      grid-column-gap: 20px;
      grid-template-columns: 200px 3fr;
      grid-template-areas:
        &quot;img title&quot;
        &quot;img bd&quot;
        &quot;img ft&quot;;
    }

    .media.media-flip {
      grid-template-columns: 3fr 200px ;
      grid-template-areas:
        &quot;title img&quot;
        &quot;bd img&quot;
        &quot;ft img&quot;;
    }
}</code></pre>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d1eb900-b706-448f-bf69-5ebd5e3ae81b/component-narrow.png" sizes="100vw" caption="The object for mobile devices. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d1eb900-b706-448f-bf69-5ebd5e3ae81b/component-narrow.png'>View large version</a>)" alt="A single column layout" >}}

<p>Then, just as we manage the view for smaller devices within our component, we can manage the layout for older browsers which do not support grid.</p>

<p>In this case, I’m going to build a float-based fallback (this will work for pretty much any legacy browser). I’m only going to worry about it for wider screen sizes and leave the component displaying in normal flow for older mobile devices.</p>

<p>Just inside the media query, add the following CSS:</p>

<pre><code class="language-css">.media:after {
  content: &quot;&quot;;
  display: table;
  clear: both;
}

.media &gt; .media {
  margin-left: 160px;
  clear: both;
}

.media .img {
  float: left;
  margin: 0 10px 0 0;
  width: 150px;
}

.media.media-flip .img {
  float: right;
  margin: 0 0 0 10px;
}

.media &gt; * {
  margin: 0 0 0 160px;
}

.media.media-flip &gt; * {
  margin: 0 160px 0 0;
}</code></pre>

<p>This should sort out the display in non-grid browsers. For browsers that do support grid, you don’t need to worry about floats, i.e. when the floated item becomes a grid item, the float is removed. What will be a problem are any margins. The layout in grid supporting browsers will now be all spaced out due to the extra margins.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c5b1cbe-b879-4c6e-bace-839efd3a7a29/component-gaps.png" sizes="100vw" caption="The layout is spaced out due to the extra margins. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c5b1cbe-b879-4c6e-bace-839efd3a7a29/component-gaps.png'>View large version</a>)" alt="Two column layout with big gaps" >}}

<p>This is where we can add a feature query, removing the margins if we know that our browser supports grid.</p>

<pre><code class="language-css">@supports(display: grid) {
  .media &gt; *,
  .media.media-flip &gt; * {
    margin: 0;
  }

  .media .img,
  .media.media-flip .img {
    width: auto;
    margin: 0;
  }

  .media:after {
    content: none;
  }
}</code></pre>

<p>That’s our small component finished. While a simple example &mdash; and it might be argued that it’s one which doesn’t really need grid at all if you <em>need</em> to have a fallback &mdash; it demonstrates the approach I’m taking across all of my projects, large and small.</p>

<p>To get my CSS file into production, we can take the CSS file from the public folder and add that to our production site. You could even script this process to copy it over to your site folder as it builds.</p>

#### Reduced Test Case First Development

<p>Something I have discovered as a key benefit in working this way, is that it really does make the browser support piece of the puzzle easier. Not only is it easier to see what fallback CSS is being included with this component, but also if we are having problems with a browser, it makes it far easier to debug them.</p>

<p>When you are battling with a browser issue then the thing you will generally be told to do is create a <a href="https://css-tricks.com/reduced-test-cases/">reduced test case</a>. Reduce the problem down to the smallest thing that exhibits the issue. A component in a pattern library is often very close to that reduced test case already. Certainly far closer than if you are trying to debug a problem while looking at your entire website.</p>

<p>In addition to making browser debugging easier, having your fallbacks included alongside the rest of the CSS makes it easier to remove the fallback code once it is no longer needed, it’s obvious this fallback code is for this component. I know that removing it won’t change the way anything else displays.</p>

<p>This ease of organizing our code is really why Fractal makes sense even in small projects. Given that we tend to use Gulp and Sass anyway (even on smaller projects), adding Fractal to the mix isn't a big overhead. We don't need to see it as only for our bigger projects, as even a small site might have a reasonable amount of CSS.</p>

## See The Code

<p>I've created a <a href="https://github.com/rachelandrew/smashing-fractal">GitHub Project</a> which has all of the code mentioned in the article. I would suggest setting up Fractal as described in the article and then grabbing any bits - such as the gulpfile or preview layout, from my repository.</p>

<p>As an additional reference and to see some published Fractal projects, we have the published version of the <a href="https://patterns.perchcms.com/">Perch Pattern Library</a>, and also the Pattern Library for <a href="https://bits.24ways.org/">24 Ways</a> (built by <a href="https://twitter.com/paulrobertlloyd">Paul Robert Lloyd</a>), which you can take a look at. These are good examples of a non-website pattern library, and a more traditional one used for a site.</p>

## How Do <em>You</em> Manage CSS?

<p>I really like this way of working; it allows me to write CSS in a straightforward, progressively enhanced way. Depending on the project, we may include far more tooling and processing of files. Or, I may be building a simple site in which case the setup will be pretty much as we have seen in this article &mdash; with some light processing of Sass. The fact that Fractal means we can have the same process for sites big and small, for web applications or websites. It means we can always work in a familiar way. </p>

<p>This works for us, and I hope this article might give you some things to experiment with. However, I would love to know the ways in which you and your team have approached managing CSS in your projects and the strengths and weaknesses of the approaches you have tried. I’d be especially interested in hearing from anyone who has developed a similar process using another pattern library solution. Add your experiences in the comments.</p>

{{< signature "il" >}}
