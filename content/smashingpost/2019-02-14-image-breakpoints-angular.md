---
title: 'Managing Image Breakpoints With Angular'
slug: image-breakpoints-angular
author: tamas-piros
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdf1b2c-36d4-4dd2-816b-d124e11b3459/breakpoints-constant-step-size-x4ywzn.svg
date: 2019-02-14T13:00:08+01:00
summary: >-
  A built-in Angular feature called BreakPoint Observer gives us a powerful interface for dealing with responsive images. Let’s take a look at a service that allows us to serve, transform and manage images in the cloud. Having such compelling tools at our hands helps us create immersive visual web experiences &mdash; without losing visitors.
description: >-
  A built-in Angular feature called BreakPoint Observer gives us a powerful interface for dealing with responsive images. Let’s take a look at a service that allows us to serve, transform and manage images in the cloud.
categories:
  - JavaScript
  - Angular
  - Media
  - Responsive Images
---
As web developers, we are often required to create applications that are responsive as well as media-rich. Having such requirements in place means that we need to work with image breakpoints, as well as media queries since we want to provide the best experience to the end users. Adding to the list of requirements we may need to use a front-end framework such as Angular which is great for creating SPAs and other application types.

In this article, we’ll take a look at image breakpoints, their use-cases and throughout a hands-on example; we’ll implement them in an Angular application using Angular’s own BreakPoint Observer. While using this approach, we’ll also highlight why this popular framework helps us work with the aforementioned techniques in a seamless way.

## Image Breakpoints And Responsive Images

In the era of responsive layouts (where we capture breakpoints based on the viewport size and based on the breakpoint we change the layout of the page), we also need to make sure that images can be displayed with the right dimensions &mdash; even after a layout change. Selecting the right image is quite challenging for modern responsive websites.

Let’s discuss two options that developers can utilize at the moment.

{{% feature-panel %}}

### `srcset`

`srcset` lets us define a list of images that the browser switches between based on the rendered `<img>` size and the density of the display.

Let’s take a look at an example:

<div class="break-out">

 <pre><code class="language-html">&lt;img
  srcset="tuscany-sm.jpg 600w, tuscany-md.jpg 900w, tuscany-lg.jpg 1440w" sizes="100vw"
  src="tuscany.jpg" /&gt;
</code></pre>
</div>

In the above, we specify 3 images, with the `w` indicating the pixel width for the image. When using the above with `srcset` we also need to specify the `sizes` attribute (this is required because the spec mandates that if we use `srcset` and `w` we must have a sizes attribute as well). What is the purpose of this attribute? Browsers need to pick which resource to load out of a source set before they layout the page (before they know how big the image will end up being). We can think of `sizes` as a hint to the browser that, after layout, the image will occupy 100% of the width of the viewport (that’s what `vw` refers to). The browser knows the actual viewport width (as well as the DPR of the image) at load-time, so it can do the math to figure out what size resource it needs and pick one out of the source set.

The `<picture>` and `<source media="">` element combinations let us switch out image resources in response to media queries, like the ones at layout breakpoints.

Let’s take a look at an example of this as well:

<div class="break-out">

 <pre><code class="language-html">&lt;picture&gt;
    &lt;source media="(min-width: 1440px)" srcset="../assets/images/tuscany-lg.jpg"&gt;
    &lt;source media="(min-width: 900px)" srcset="../assets/images/tuscany-md.jpg"&gt;
    &lt;source media="(min-width: 600px)" srcset="../assets/images/tuscany-sm.jpg"&gt;
    &lt;img src="../assets/images/tuscany-sm.jpg" /&gt;
  &lt;/picture&gt;
</code></pre>
</div>

Change the code above locally with an image of your choice that has a small, medium and large size. Notice how, by resizing the browser, you get a different image.

The key takeaway from all the above is that if we want to swap out images at specific breakpoints, we can use the `<picture>` element to put media queries right into the markup.

<p><strong>Note</strong>: <em>If you’re interested in exploring the differences between </em><code>&lt;picture&gt;</code><em> and </em><code>srcset</code><em> + </em><code>sizes</code>, <em>I recommend reading Eric Portis’ great article:</em> <a href="https://ericportis.com/posts/2014/srcset-sizes/"><code>srcset</code> <em>and</em> <code>sizes</code></a>.</p>

So far we have discussed how to use image breakpoints along with media queries in a pure HTML environment. Wouldn’t it be a lot better to have a convenient, almost semi-automated way of generating image breakpoints as well as the corresponding images for the breakpoints even without having to specify media queries at all? Luckily for us Angular has a built-in mechanism to help us out and we’ll also take a look at generating the appropriate images dynamically based on certain conditions by using a third-party service.

### Angular Layout Module

Angular comes with a Layout Module which lives in the CDK (Component Dev Kit) toolset. The [Angular CDK](https://material.angular.io/cdk/categories) contains well-tested tools to aid with component development. One part of the CDK is the Layout Module which contains a `BreakpointObserver`. This helper gives access to media-query breakpoints, meaning that components (and their contents) can adapt to changes when the browser size (screen size) is changed intuitively.

<p><strong>Recommended reading</strong>: <em><a href="https://material.angular.io/cdk/layout/overview">Layout Module</a></em></p>

Now that we have the theory out of the way let’s get down to business and create an application that will implement responsive image breakpoints. In this first iteration, we’ll create the shell of the application via the Angular CLI: `ng new bpo` and select the necessary options.

To use the `BreakpointObserver` we also need to install the Angular’s CDK Layout Module, which we can do via npm: `npm i @angular/cdk`.

After the installation, we will be able to add the necessary import statements to any component that we wish:

<div class="break-out">

 <pre><code class="language-typescript">// app.component.ts
import { BreakpointObserver, Breakpoints } from '@angular/cdk/layout';
</code></pre>
</div>

Using the `BreakpointObserver` we can subscribe to changes in the viewport width and Angular gives us convenient accessors which mean that we don’t need to use media queries at all! Let’s go ahead and try this out:

<pre><code class="language-typescript">// app.component.ts
constructor(public breakpointObserver: BreakpointObserver) { }

ngOnInit() {
    this.breakpointObserver.observe([
      Breakpoints.XSmall,
      Breakpoints.Small,
      Breakpoints.Medium,
      Breakpoints.Large,
      Breakpoints.XLarge
    ]).subscribe(result => {
      if (result.breakpoints[Breakpoints.XSmall]) {
       // handle XSmall breakpoint
      }
      if (result.breakpoints[Breakpoints.Small]) {
       // handle Small breakpoint
      }
      if (result.breakpoints[Breakpoints.Medium]) {
      // handle Medium breakpoint
      }
      if (result.breakpoints[Breakpoints.Large]) {
        // handle Large breakpoint
      }
      if (result.breakpoints[Breakpoints.XLarge]) {
        // handle XLarge breakpoint
      }
    });
  }
</code></pre>

As mentioned before the accessor properties above reflect media queries in the following way:

- `Breakpoints.XSmall`: max-width = 599.99px
- `Breakpoints.Small`: min-width = 600px and max-width = 959.99px
- `Breakpoints.Medium`: min-width = 960px and max-width = 1279.99px
- `Breakpoints.Large`: min-width = 1280px and max-width = 1919.99px
- `Breakpoints.XLarge`: min-width = 1920px

We now have everything in place which means, we can start to generate the appropriate images.

{{% ad-panel-leaderboard %}}

## Responsive Breakpoints For Images

We have a few options to generate responsive images:

1. [Responsive Image Breakpoints Generator](https://www.responsivebreakpoints.com)  
Using this tool, we can upload any image, setup various options, e.g. the number of images that we wish to generate. After running the tool, we’ll have a visual representation about the generated images, and we can download them as a zip file along with some generated code which uses the previously mentioned `<picture>` element.
2. Another solution would be to create a build step for our project to generate breakpoints via some packages available in the NPM repository, such as [`gulp-responsive`](https://www.npmjs.com/package/gulp-responsive) or [`grunt-responsive-images`](https://github.com/andismith/grunt-responsive-images). Both of these depend on additional libraries that we are required to install for our operating system. (Please check the appropriate repositories for additional information.)
3. Yet another solution would be to use a service such as Cloudinary to store the images and serve them in a size and format that we need only by modifying the URL for the requested resource. This will be our approach since this gives us the most flexibility.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2016/09/automating-art-direction-with-the-responsive-image-breakpoints-generator/">Automating Art Direction With The Responsive Image Breakpoints Generator</a> by Eric Portis</em></p>

I have uploaded the original image to my Cloudinary account which means that I can access that image via the following URL:

<div class="break-out">

 <pre><code class="language-bash">https://res.cloudinary.com/tamas-demo/image/upload/breakpoints-article/tuscany.jpg
</code></pre>
</div>

This is the full-sized, raw, original and unchanged image that we’ll work with.

We can modify the URL of the image to generate a much smaller version. For example, if we want to have an image with a width of 600 pixels, we could update the Cloudinary URL&#42; to be the following:

<div class="break-out">

 <pre><code class="language-bash">https://res.cloudinary.com/tamas-demo/image/upload/w_600/breakpoints-article/tuscany.jpg
 </code></pre>
</div>

*&#42; Note the `w_600` added to the URL.*

Hopefully, by this point, you see where all this is going. Based on the approach above, we can very quickly start to generate the right image for the right breakpoint.

{{% ad-panel-leaderboard %}}

Using Cloudinary means that we don’t need to create, store and manage multiple version of the same image &mdash; it is done for us by Cloudinary on-the-fly.

Let’s update our code:

<pre><code class="language-html">&lt;!-- app.component.html --&gt;
&lt;div&gt;
  &lt;h1&gt;Current breakpoint: {{ breakpoint }}&lt;/h1&gt;
  &lt;img [src]="imagePath"&gt;
&lt;/div&gt;
</code></pre>

<pre><code class="language-typescript">// app.component.ts
import { Component, OnInit } from '@angular/core';
// ...
export class AppComponent implements OnInit {
  imagePath;
  constructor(public breakpointObserver: BreakpointObserver) { }
  ngOnInit() {
    this.breakpointObserver.observe([ ...
  }
}
</code></pre>

We can pick any number of breakpoints to observe from the list mentioned previously, and since we have an Observer we can subscribe to the changes and act on them:

<pre><code class="language-typescript">this.breakpointObserver.observe([
  Breakpoints.XSmall,
  Breakpoints.Small,
  Breakpoints.Medium,
  Breakpoints.Large,
  Breakpoints.XLarge
]).subscribe(result => {
  if (result.breakpoints[Breakpoints.XSmall]) {
    // handle this case
  }
});
</code></pre>

To handle the options for the different images in Cloudinary, we’ll utilize an approach that will be very easy to follow. For each case, we’ll create an options variable and update the final Cloudinary URL.

Add the following at the top of the component definition:

<div class="break-out">

 <pre><code class="language-typescript">// app.component.ts
imagePath;
  breakpoint;
  cloudinaryOptions;
  baseURL = 'https://res.cloudinary.com/tamas-demo/image/upload/breakpoints-article/tuscany.jpg';
</code></pre>
</div>

And add the following as well to the first `if` statement:

<pre><code class="language-typescript">// app.component.ts
let url = this.baseURL.split('/');
let insertIndex = url.indexOf('upload');
const options = 'c_thumb,g_auto,f_auto,q_auto,w_400';
url.splice(insertIndex + 1, 0, options);
this.imagePath = url.join('/');
this.breakpoint = Breakpoints.XSmall;
</code></pre>

The result is going to be an updated Cloudinary URL:

<div class="break-out">

 <pre><code class="language-bash">https://res.cloudinary.com/tamas-demo/image/upload/c_thumb,g_auto,f_auto,q_auto,w_400/breakpoints-article/tuscany.jpg
</code></pre>
</div>

What are the options that we are setting here?

- `c_thumb` (generates a thumbnail of the image);
- `g_auto` (focuses on the most interesting part; we see the cathedral in the thumbnail);
- `f_auto` (serves the most appropriate format for a given browser, i.e. WebP for Chrome);
- `q_auto` (reduces the quality &mdash; and therefore the overall size &mdash; of the image without impacting the visuals);
- `w_400` (sets the width of the image to 400px).

For the sake of curiosity, let’s compare the original image size with this newly generated image: 2.28 MBs vs 29.08 KBs!

We now have a straightforward job: we need to create different options for different breakpoints. I created a sample application on [StackBlitz](https://stackblitz.com/edit/angular-tesbey) so you can test it out immediately (you can also see a preview [here](https://angular-tesbey.stackblitz.io)).

## Conclusion

The variety of desktop and mobile devices and the amount of media used in today’s web has reached an outstanding number. As web developers, we must be at the forefront of creating web applications that work on any device and doesn’t impact the visual experience.

There are a good number of methods that make sure the right image is loaded to the right device (or even when resizing a device). In this article, we reviewed an approach that utilizes a built-in Angular feature called BreakPoint Observer which gives us a powerful interface for dealing with responsive images. Furthermore, we also had a look at a service that allows us to serve, transform and manage images in the cloud. Having such compelling tools at our hands, we can still create immersive visual web experiences, without losing visitors.

{{< signature "dm, il" >}}
