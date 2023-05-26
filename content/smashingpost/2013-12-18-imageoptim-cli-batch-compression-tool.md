---
title: 'How Optimized Are Your Images? Meet ImageOptim-CLI, A Batch Compression Tool'
slug: imageoptim-cli-batch-compression-tool
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3844a27a-9418-4cab-a2b2-7f3f4214d89c/imageopt-cli-illu.jpg
date: 2013-12-18T01:22:38.000Z
author: jamie-mason
description: >-
  Exporting images for the Web from one’s favorite graphics software is
  something many of us have done hundreds of times. Our eyes fixate on an
  image’s preview, carefully adjusting the quality and optimization settings
  until we’ve found that sweet spot, where the file size and quality are both
  the best they can possibly be.
categories:
  - Coding
  - Graphics
  - Freebies
  - Workflow
---
Exporting images for the Web from one’s favorite graphics software is something many of us have done hundreds of times. Our eyes fixate on an image’s preview, carefully adjusting the quality and optimization settings until we’ve found that sweet spot, where the file size and quality are both the best they can possibly be.

After exporting the image — usually using a feature called “Save for the Web” — and having gone to all that care and effort, we would be forgiven for thinking that our image is in the best shape possible. That’s not always the case, of course.

In fact, _much_ more data is usually left in such files, data that browsers have to download despite not requiring or even using it, **data that keeps our users waiting** just a bit longer than necessary.

Thankfully, a number of popular tools can help us optimize images even further, but which should we use? We assumed, for a time at least, that our graphics editing software properly optimized our files, but what do we _really_ know about our image optimization tools?

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)
*   [Clever PNG Optimization Techniques](https://www.smashingmagazine.com/2009/07/clever-png-optimization-techniques/)
*   [Clever JPEG Optimization Techniques](https://www.smashingmagazine.com/2009/07/clever-jpeg-optimization-techniques/)
*   [How To Optimize Images With HTML5 Canvas](... "Read 'How To Optimize Images With HTML5 Canvas'")

{{% feature-panel %}}

## Image Optimization Tools

If you’re not currently using any image optimization tool, I would urge you to [choose one](https://addyosmani.com/blog/image-optimization-tools/). Any is better than none. Regardless of which you choose, you will likely speed up your website and keep users happy.

To inform our work, I ran the most popular image optimization tools over a varied sample of images (kindly donated by [Daan Jobsis](https://twitter.com/daanjobsis) via his “[Retina Revolution](https://www.netvlies.nl/blog/design-interactie/retina-revolutie-follow-up)” article), and I’ve published the [results on GitHub](https://jamiemason.github.io/ImageOptim-CLI).

<p>The report shows us how much data each tool saves and <strong>how much quality was lost statistically</strong>. However, <stong>how great a loss in quality is noticeable</strong>and how much is acceptable will vary from person to person, project to project and image to image.</p>

## Aim For The Biggest Gains

I’ve been using [ImageOptim](https://imageoptim.com) for many years, with [ImageAlpha](https://pngmini.com) and [JPEGmini](https://itunes.apple.com/us/app/jpegmini/id498944723) joining it more recently.

With this trio, we have a specialist in JPEGs, another in PNGs, and a great all-round application, ImageOptim, which also supports GIF and other formats. Each uses different techniques to deliver impressive savings, but they complement each other when combined to offer better savings still.</p>

### ImageOptim

ImageOptim beats any single lossless optimizer by bundling all of them. It works by finding the best combination of compression parameters and removes unnecessary comments and color profiles.</p>

### ImageAlpha

ImageAlpha is unique in its lossy conversion of PNG24 to PNG8, delivering savings many times bigger than popular PNG optimizers such as Smush.it and TinyPNG. The conversion even maintains alpha-transparency in all browsers, including on iOS and even in IE 6.</p>

### JPEGmini

JPEGmini is a “patent-pending photo recompression technology, which significantly reduces the size of photographs without affecting their perceptual quality.” The creators claim it **reduces a file’s size by up to 80%**, while maintaining quality that is visually identical to the original.

The savings are quite remarkable, but you will need to purchase the software to use it without restriction.</p>

## Prioritize Convenience

In terms of performance, the comparative data is reassuring, and to date I’ve been happy with my decisions. **But there’s a real problem: all of these tools are GUI applications for OS X.**

This has some benefits because everything is local. You don’t need to upload and download files to a Web server, so there’s no risk of the service being temporarily unavailable. This also means that your images don’t need to leave your machine either.

But at some point ahead of every launch, I had to remember to open each application, manually process new images, then wait for the tool to finish, before doing the same in the next application.

This soon gets tedious: We need to automate! This is why (with [James Stout](https://zoooot.com) and [Kornel Lesiński](https://twitter.com/pornelski)) I’ve created [ImageOptim-CLI](https://github.com/JamieMason/ImageOptim-CLI), automated image optimization from the command line interface (CLI).</p>

## ImageOptim-CLI

Though other image optimization tools are available from the command line, ImageOptim-CLI exists because the [current benchmarks](https://jamiemason.github.io/ImageOptim-CLI) suggest that ImageOptim, ImageAlpha and JPEGmini currently outperform those alternatives over lossless and lossy optimizations.

I wanted to take advantage of this.

Given a folder or other set of images, **ImageOptim-CLI automates the process of optimizing** them with ImageAlpha, JPEGmini _and_ ImageOptim. In one command, we can run our chosen images through all three optimizers — giving us automated, multi-stage image optimization right from the command line.

This gives us the levels of optimization of all three applications, with the convenience of the command line, opening up all kinds of possibilities for integration with other utilities:

*   Integrate it with [Alfred](https://www.alfredapp.com/powerpack/) workflows.
*   Extend OS X with folder actions and more using [Automator](https://macosxautomation.com/automator/).
*   Optimize images whenever they change with the [Guard](https://guardgem.org/) RubyGem.
*   Ensure that images are optimized when you [Git commit](https://github.com/JamieMason/ImageOptim-CLI#adding-to-git-pre-commit-hook).

Do you know of other ways to integrate image optimization in your workflow? If so, please share your ideas in the comments.</p>

### Installation and Usage

The CLI can be downloaded as a ZIP archive or cloned using Git, but the easiest way is by running this:

<pre><code class="language-bash">npm install -g imageoptim-cli</code></pre>

Running all three applications before closing them afterwards can be achieved with this:

<pre><code class="language-bash">imageoptim --image-alpha --jpeg-mini --quit --directory ~/Sites/MyProject</code></pre>

Or you can do it with the equivalent shorthand format:

<pre><code class="language-bash">imageoptim -a -j -q -d ~/Sites/MyProject</code></pre>

You will find more installation and usage examples on the [project page](https://github.com/JamieMason/ImageOptim-CLI) on GitHub.</p>

## Case Study: Myspace

Earlier this week, I visited [Myspace](https://www.myspace.com) and found that 4.1 MB of data was transferred to my machine. With the home page’s beautiful magazine-style layout, it’s no surprise that roughly 76% (or 3.1 MB) of that were images.

I was curious whether any data could be saved by running the images through ImageOptim-CLI. So, I recorded the video below to show the tool being installed and then run over Myspace’s home page.

<iframe loading="lazy" width="500" height="375" src="//www.youtube.com/embed/_asZ7fbuxvs?rel=0" frameborder="0" allowfullscreen></iframe>

As you can see, the total size of images before running the command was 3,186 KB, and ImageOptim-CLI was able to remove **986 KB** of data, while preserving **99.93%** of image quality.</p>

## grunt-imageoptim

There is a companion Grunt plugin for ImageOptim-CLI, called [grunt-imageoptim](https://github.com/JamieMason/grunt-imageoptim), which offers full support for the optimization of folders and collections of images. It can also be paired with [grunt-contrib-watch](https://github.com/gruntjs/grunt-contrib-watch) to run whenever any images are modified in your project.

Smashing Magazine has a great article for those who want to [get up and running with Grunt](https://www.smashingmagazine.com/2013/10/29/get-up-running-grunt/).</p>

## Summary

Image optimization is an essential step in a designer’s workflow, and with so many tools to choose from, there’s bound to be one that suits your needs.

Data should bear heavily in your decision, so that you reap bigger rewards, but **choose one that is convenient** — using a weak tool every time is better than using than a strong tool sometimes. You’ll rarely make a decision in your career that doesn’t have some kind of trade-off, and this is no different.</p>

### Resources

*   [ImageOptim](https://imageoptim.com)
*   [ImageAlpha](https://pngmini.com)
*   [JPEGmini](https://itunes.apple.com/us/app/jpegmini/id498944723)
*   [ImageOptim-CLI](https://github.com/JamieMason/ImageOptim-CLI)
*   [grunt-imageoptim](https://github.com/JamieMason/grunt-imageoptim)

If you’ve made it this far, I thank you for reading and welcome your questions, comments and ideas.

{{< signature "al, ea" >}}

