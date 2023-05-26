---
title: 'Create An HTML/CSS Mobile Web App Using Sencha Touch'
slug: create-an-html-and-css-mobile-web-app-using-sencha-touch
image: >-
  https://www.smashingmagazine.com/general/2012/11/14/132971-revision-18/attachment/solution_senchaio_mini/
date: 2011-07-19T09:27:49.000Z
author: jen-gordon
summary: >-
  How to and why design a mobile Web app? Jen Gordon shares her knowledge as a designer to decide what’s best for you.
description: >-
  Questions in the world of mobile app development are endless. Jen Gordon shares her knowledge as a designer to decide what’s best for your client -and how to do it- regarding the audience they are trying to reach.
categories:
  - Mobile
  - Frameworks
  - CSS
  - HTML5
  - CSS3
---

The world of mobile app development is quickly becoming a crowded and complicated space, especially for those outside of the development niche. “Which development platform should I use?” “Do I go native or Web-based?” “Which devices should I plan for?” “Can I build my mobile website by hand or should I use a pre-built package?” The questions are endless.

As a designer, my job is to help my clients answer these questions. I try to stay in the category of “knowing enough to be dangerous,” and I keep tabs on the latest mobile development trends, one being the growing popularity of mobile Web apps.

{{% feature-panel %}}

## What Is A Mobile Web App?

A mobile Web app is an app that you access via a mobile browser (such as iPhone’s Safari). It is not a static mobile website. It is designed to work like a native app, but it is not accessible via the App Store or Android Marketplace. You pull it up right from the browser.

### Why Create A Mobile Web App Instead Of A Native App?

Deciding whether a native or Web-based app is best for your client comes down to the audience they are trying to reach. Mobile Web apps are a good fit if:

*   Your audience is searching for you primarily from a mobile Web browser;
*   Users are on a multitude of devices (iPhone, Android, BlackBerry, etc.);
*   The development team has more skill in HTML, CSS and JavaScript than Objective C, Java, etc.

## How To Design A Mobile Web App

Those of you who have designed iOS native apps are used to fixed-width and -height images that are positioned and aligned in the Interface Builder (or using code). Designing mobile Web apps is different: you’re designing for the browser again, just as you would for a typical website.

What does this mean? It means you can take advantage of a *lot* of cool CSS design tricks. In many cases, you can <a href="https://www.smashingmagazine.com/2011/04/21/css3-vs-css-a-speed-benchmark/">design an entire interface using CSS</a> instead of images.

### Technology Analysis: jQTouch Or Sencha Touch?

To help you determine which development platform best fits your project, I’ve done some research on two Web technologies that focus on mobile Web apps: jQTouch and Sencha Touch.

jQTouch is powered by jQuery, a highly popular JavaScript library, and is geared to Web designers and novice Web app developers. jQTouch progressively enhances HTML and CSS so that less capable phones are still able to browse content. The primary method of creating functionality in jQTouch is with HTML and CSS or with jQuery-style event callbacks.

Sencha Touch, on the other hand, is geared more to software developers and has a pure Javascript API for building powerful apps. It is powered by a custom core that is optimized for mobile, which inherently makes the core level in Sencha Touch lighter and better optimized than that in jQTouch. It offers a wider array of features and components and is better suited to mobile developers who are creating apps with advanced layouts, functionality and interfaces.

For myself, I wanted an interface that looked and felt like a native app as much as possible. I decided to go with the Sencha Touch development platform because of its ability to handle advanced layouts and interfaces.

Ultimately, you have to do your own research and answer these questions:

1.  What kind of functionality does the app need?
2.  What technology supports that functionality?
3.  How do the costs of these technologies compare?
4.  What can I afford?
5.  Do I know of high-quality developers of this technology?

Once you have this data, you can make an informed decision on the technology platform for your project.

### Where Does This Leave Us Non-Coding Designers?

If you fall squarely in the category of designer, don’t worry. You can still design the interface in Photoshop, as I did in the example below. I leave the CSS beauty to the experts, letting them translate my images into code that looks exactly like my design.

## Example Project: The Roookies App

Now, I’ll cover a practical example of how to create a mobile Web app using <a href="https://www.sencha.com/products/touch/">Sencha Touch</a>. I teamed up with Sencha’s CTO, James Pearce, to design an app called Roookies. Roookies helps Dribbble newbies gain exposure on the network by featuring *only* rookie artwork.

I designed the Roookies app as I would a native application, using a 640 × 960 iOS design template found on <a href="https://www.tapptics.com">Tapptics</a>. This gives my developer a reference when they create the CSS code that will mimic my images. And for any images that cannot be duplicated via CSS, my developer will slice out and insert transparent PNGs.

<figure><img loading="lazy" decoding="async"  title="Design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/140ff772-6e91-48a0-85b9-515a51c40e62/image00-500.jpg" alt="screenshot" width="500" height="276" /><figcaption>The Roookies App using Sencha Touch.</figcaption></figure>

## Coding The Roookies App

Now I’ll demonstrate how to use CSS, Sass and Compass to style and theme mobile Web applications built with HTML5 and the Sencha Touch JavaScript framework.

<figure><img loading="lazy" decoding="async"  title="Rookies App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f7b512a-c05d-4952-bd9e-f76d359d77cd/image05-300.png" alt="screenshot" width="300" height="564" /><figcaption>Coding The Roookies App.</figcaption></figure>

### An Introduction To Sass And Compass

Sass is an extension of CSS that adds new syntax to allow for things like variables, mixins, nesting, and math and color functions. This makes it much simpler to create CSS that is easy to maintain and that doesn’t repeat itself.

For example, in Sass we can write the following:

<pre><code class="language-css">$blue: #3bbfce;
$margin: 16px;

.content-navigation {
border-color: $blue;
color: darken($blue, 9%);
}

.border {
padding: $margin / 2;
margin: $margin / 2;
border-color: $blue;
}</code></pre>

When we compile it to CSS, the output will look like this:

<pre><code class="language-css">.content-navigation {
border-color: #3bbfce;
color: #2b9eab;
}

.border {
padding: 8px;
margin: 8px;
border-color: #3bbfce;
}</code></pre>

This is extremely powerful, because it means we can potentially change color schemes, layouts and more with one set of simple parameters &mdash; and assuming that the Sass has been structured well, those changes will cascade throughout all of the resulting CSS. (You can do much more than this, and you should check out the <a href="https://sass-lang.com/">Sass website</a> for more information on how the language works.)

Compass is an extension to Sass, and it provides a whole set of CSS3 mixins and an extension system. It’s particularly useful for handling cross-browser CSS prefixes. Take this:

<pre><code class="language-css">$boxheight: 10em;
.mybox {
@include border-radius($boxheight/4);
}</code></pre>

This will compile to the following CSS:

<pre><code class="language-css">.mybox {
-webkit-border-radius: 2.5em;
-moz-border-radius: 2.5em;
-o-border-radius: 2.5em;
-ms-border-radius: 2.5em;
-khtml-border-radius: 2.5em;
border-radius: 2.5em;
}</code></pre>

You can learn more about what Compass brings to the styling process on its website.

{{% ad-panel-leaderboard %}}

## Using Sass And Compass With Sencha Touch

<a href="https://www.sencha.com/products/touch/">Sencha Touch</a> is an HTML5, CSS3 and JavaScript framework that allows you to develop mobile Web apps that look and feel native on iPhone, Android and BlackBerry touch devices.

Because the framework uses Web technology to create apps that run in the browser, these apps can easily be themed using tried and trusted CSS. And because Sencha Touch uses Sass and Compass, we can use these techniques to also create beautiful and elegant themes for mobile applications that were built this way.

For this article, we’ve built a simple Sencha Touch app called Roookies. It uses a JSON API to create a gallery of shots by first-time users of Dribbble, a popular design showcase service. (While we won’t get into how the app was built, you can read a sister article <a href="https://www.sencha.com/learn/Tutorial:Building_The_Roookies_App">about how it works</a>.)

To follow along here, we recommend you grab a copy of the app’s source code, because it also includes the theming components you’ll need. It’s <a href="https://github.com/senchalearn/roookies">hosted on GitHub</a>, so you can either fork that repository or simply download it as a <a href="https://github.com/senchalearn/roookies/zipball/master">ZIP file.</a> An unthemed version of the app is also <a href="https://senchalearn.github.com/roookies/">hosted online</a>; you can try it out with a touch device or a WebKit-based desktop browser.

<figure><img loading="lazy" decoding="async"  title="Rookies App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a8c7bd-3ac9-4a17-83b3-a339f4da51d5/image03-300.png" alt="screenshot" width="300" height="564" /><figcaption>Using Sass and Compass with Sencha Touch.</figcaption></figure>

Before you do any theming on this app, you’ll need to install Compass (which has Sass built in). The command line tool itself is Ruby-based, which means that Ruby is a dependency. If you’re a Mac user, Ruby is already installed on your operating system, and the easiest way to install Compass is as a Gem from the command line:

<pre><code class="language-css">&gt; sudo gem install compass --pre</code></pre>

(We use the <code>--pre</code> flag to ensure that the latest and greatest version of Compass is installed. Sencha Touch requires version 0.11 or later.)

If you are on Windows or a system that doesn’t have Ruby already installed, then you’ll need to install Ruby and Gem first, using something like <a href="https://rubyinstaller.org/">RubyInstaller for Windows</a>.

## How Sencha Touch Uses Sass

Each component of the Sencha Touch user interface library has its own Sass file, which you can easily take and edit. But sometimes, the easiest changes can be made by altering certain important Sass variables (as we did in the examples above) to make changes globally across the application’s theme.

In the Roookies application, you’ll find a folder named *theming*. In it, create a new Sass file named *mytheme.scss*. The *.scss* extension is the convention for Sass files. In this file you can link to the parts of the Sencha Touch theming system that are used in the Roookies application:

<pre><code class="language-css">@import 'sencha-touch/default/all';
@include sencha-panel;
@include sencha-buttons;
@include sencha-sheet;
@include sencha-tabs;
@include sencha-toolbar;
@include sencha-list;
@include sencha-layout;
@include sencha-loading-spinner;</code></pre>

The first line links to all of Sencha Touch’s sub-theming files, and the subsequent lines call mixins for the UI elements used in our application. Mixins are really just functions: they basically insert blocks of CSS into your document.

Most of these mixins use a set of global variables to alter the appearance of different parts of the user interface. For example, the <code>$base-color</code> variable modifies the overall color of the application. Set the following variable before the <code>@includes</code> so that they all use this new value, a tasteful green:

<pre><code class="language-css">$base-color: #709e3f;

@import 'sencha-touch/default/all';
@include sencha-panel;
@include sencha-buttons;
…</code></pre>

When you save that file, you will be good to compile the CSS. In the same directory, run Compass on the command line, like so:

<pre><code class="language-css">&gt; compass compile mytheme.scss</code></pre>

If all goes well, Compass should output the *mytheme.css* file in the same directory. As with all websites and apps, you’ll need to reference this new CSS file in the application itself. You can do this either by adding a magic query string to the Roookies application URL (something like <code>https://myserver.com/roookies?style=theming/mytheme.css</code>) or, more traditionally, by hardcoding the reference into *index.html*:

<pre><code class="language-css">&lt;link rel="stylesheet" type="text/css"
href="theming/mytheme.css"/&gt;</code></pre>

(If you do hardcode the theme like this, you should remove the <code>script</code> block in *index.html*, which is responsible for supporting the query-string theme-switching technique.)

If all goes well, the theme should now appear with the new color, both in the toolbar and in a lighter shade for selections of the list itself:

<figure><img loading="lazy" decoding="async"  title="Rookies App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf3798b5-cbf3-4e61-8346-bc34e3493014/image01-300.png" alt="screenshot" width="300" height="564" /><figcaption>How Sencha Touch uses Sass.</figcaption></figure>

(The fact that the color of the list selection is derived from, but not exactly the same as, the base is another clever Sass trick. Color functions such as <code>darken</code> and <code>saturate</code> allow you to formulaically link color values.)

Sencha Touch has a full list of the variables that can be altered to change the look and theme of an app.

## Embedding Regular CSS

If all this talk of Sass and Compass is confusing, the good news is that even an *.scss* file can contain regular old CSS, too. So, in addition to your variables, mixins and functions, you can just start doing static styling to finesse the theme.

Let’s say we want to frame the images in the list. In the Roookies app, all of the images have the HTML class attribute <code>shot-image</code>, so we can easily style them as normal:

<pre><code class="language-css">img.shot-image {
display:block;
padding: 8px;
margin: 0px auto;
border: 1px solid #666;
-webkit-box-shadow: 0 0 4px rgba(#333, .5);
background:#eee;
clear:both;
width:304px;
}</code></pre>

Also, the container in which each image is placed is a div with the class <code>shot</code>, and we can easily adjust its padding so that our framed image still fits well within the list’s width:

<pre><code class="language-css">.shot {
padding: 8px 0!important;
}</code></pre>

One useful way to find out the classes of elements in a mobile Web application is to use the inspector tool in a WebKit-based browser such as Chrome. Right-click on an element to inspect it and see how it looks in the browser’s DOM:

<figure><img loading="lazy" decoding="async"  title="HTML Inspector" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d150fc0-beb8-401e-acda-b4f6dddfe519/image06-500.png" alt="screenshot" width="500" height="580" /><figcaption>Embedding Regular CSS.</figcaption></figure>

Add these to the bottom of the *.scss* file and compile again. The app’s images should now have more subtle styling, making the gallery look slightly smarter:

<figure><img loading="lazy" decoding="async"  title="Rookies App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71ef372b-d9a3-4460-971c-633ec78621cd/image02-300.png" alt="screenshot" width="300" height="564" /></figure>

## Embedding Images In CSS

One consideration when building mobile Web apps is the number of requests that the browser needs to make to the server to display a page. And it’s often the case that CSS points to external files, such as images, in the theme. One thing that is very easy to do with Compass, though, is to embed images in the CSS itself, using base64 encoding inside a “Data URL.” These are URLs that start with data and that allow you to specify binary resources inline. This means that the entire theme is encapsulated in one file, and the device has to make only one request to the server to receive all of the parts.

The inline image function is an easy way to do this. In our theming environment, it pulls in images from the images sub-directory. So, the *wood.jpg* image in that directory can be embedded in the CSS as the background of the gallery, like so:

<pre><code class="language-css">.shot {
background:inline-image("wood.jpg", "image/jpg");
}</code></pre>

In the resulting CSS, it appears like this:

<pre><code class="language-css">.shot{
background:url('data:"image/jpg";base64,/9j/4AAQSkZJR…');
}</code></pre>

This gives the app a tasteful wooden background:

<figure><img loading="lazy" decoding="async"  title="Rookies App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0114414-deba-44b0-bec2-a22168e845eb/image04-300.png" alt="screenshot" width="300" height="564" /><figcaption>Embedding images in CSS.</figcaption></figure>

## Font Support

Many current mobile browsers support Web fonts, and there’s nothing like a custom typeface to distinguish your mobile application. One of the easiest ways to put a Web font on a website or application is with <a href="https://www.google.com/webfonts">Google’s WebFont</a> service, which requires you to declare an extra CSS rule by linking to your chosen font in the *index.html* file:

<pre><code class="language-css">&lt;link href='https://fonts.googleapis.com/css?family=Pacifico'
rel='stylesheet' type='text/css'&gt;</code></pre>

You can also use the CSS <code>@import</code> rule to pull this into the *.scss* file itself:

<pre><code class="language-css">@import "https://fonts.googleapis.com/css?family=Pacifico";</code></pre>

Both of these techniques create an <code>@font-face</code> rule that allows you to use <code>font-family:'Pacifico'</code> anywhere in your CSS.

Below, we’ve applied a style to the user interface &mdash; in this case, the text in the toolbar, which uses the class <code>x-toolbar-title</code>:

<pre><code class="language-css">.x-toolbar-title {
font-family: 'Pacifico';
}</code></pre>

The result is as follows. A little quirkiness in the title bar and a distinctive look and feel to our application.

<figure><img loading="lazy" decoding="async"  title="Rookies App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f7b512a-c05d-4952-bd9e-f76d359d77cd/image05-300.png" alt="screenshot" width="300" height="564" /><figcaption>Font support.</figcaption></figure>

## Conclusion

Of course, we’ve just scratched the surface here. There are many more powerful (and dramatic) ways to style and theme a mobile Web application. We’ve continued this process to create a fully featured theme for the Roookies app, and you can <a href="https://senchalearn.github.com/roookies/?style=demo">see the results for yourself</a>, including the styled image meta data and the styled details page when you click on an icon under the images. You can also see the <a href="https://github.com/senchalearn/roookies/blob/master/theming/roookies.scss">complete *.scss* file</a> that was used to create this theme; it’s distributed as part of the GitHub project.

Have you created a mobile Web app with an extraordinary design aesthetic? Let us know in the comments section below!

### Mobile Web App Resources

*   “[Mobile Web vs. Native App: Give It a Rest](https://globalmoxie.com/blog/mobile-web-vs-native.shtml)”
*   “[Mobile Web vs. Native App](https://sandhill.com/opinion/daily_blog.php?id=33&post=773)”
*   “[How Mobile Web Will Prevail Over Native App](https://blog.roound.com/post/4557025779/how-mobile-web-will-prevail-over-native-app)”
*   “[Web App Masters: Native or Web-Based Mobile Apps?](https://www.lukew.com/ff/entry.asp?1281)”

{{% ad-panel-leaderboard %}}

### Further Reading

*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [Facing The Challenge: Building A Responsive Web Application](https://www.smashingmagazine.com/2013/06/building-a-responsive-web-application/)
*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)
*   [The Building Blocks Of Progressive Web Apps](https://www.smashingmagazine.com/2016/09/the-building-blocks-of-progressive-web-apps/)

{{< signature "kw, mrn" >}}
