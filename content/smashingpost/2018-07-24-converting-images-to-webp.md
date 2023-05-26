---
title: 'Converting Images To WebP'
slug: converting-images-to-webp
author: jeremywagner
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52545f9d-e051-4e88-bd93-a3570598f1c3/04-converting-images-to-webp-chapter-800w.png
date: 2018-07-24T11:00:30+02:00
summary: >-
  In this excerpt from his eBook “[The WebP Manual](/2018/07/webp-manual/),” developer and author Jeremy Wagner will show you the many ways you can convert your existing images to the WebP format. [To the table of contents](/2018/07/webp-manual/#toc).
description: >
  In this excerpt from his eBook “The WebP Manual,” developer and author Jeremy Wagner will show you the many ways you can convert your existing images to the WebP format.
categories:
  - Performance
  - Optimization
  - Images
  - Media
disable_ads: true
disable_panels: true
---
To use WebP, you’ll first need to convert your existing images to the format. This can be done in a myriad of ways, from something as simple as exporting from your preferred design program, to cloud services, to the official cwebp encoder, and even in Node.js-based build systems. Here, we’ll cover all avenues.

## Sketch

Sketch is able to export any resource in a design document to WebP natively. To export an image to WebP, select a resource on the canvas, open the **Export** panel on the right hand side, and choose “WEBP” in the format dropdown.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7acdc6b5-f289-4b7d-a3ad-9c70b1e18a8d/01-converting-images-to-webp-chapter.png" sizes="100vw" caption="The resource export panel in Sketch, with the WebP format chosen in the format dropdown. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7acdc6b5-f289-4b7d-a3ad-9c70b1e18a8d/01-converting-images-to-webp-chapter.png'>Large preview</a>)" alt="The resource export panel in Sketch, with the WebP format chosen in the format dropdown." >}}

After you make your selection, click the **Export Bitmap...** button. The resulting dialog will predictably ask where you want the image to be exported to. Within that dialog, a slider will appear at the bottom that prompts you to specify the quality of the WebP image from 0 to 100, implying the output is lossy WebP.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97df1aea-4a37-41ef-87c7-10910ebd9725/02-converting-images-to-webp-chapter.png" sizes="100vw" caption="The quality slider in the export dialog when exporting a resource to WebP. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97df1aea-4a37-41ef-87c7-10910ebd9725/02-converting-images-to-webp-chapter.png'>Large preview</a>)" alt="A slider shown in sketch for exporting lossy WebP images. The slider goes from 0 to 100, where 0 is the lowest quality, and 100 is the highest." >}}

If you’re using design software to export to WebP, Sketch is probably one of the easier programs to use. Although, there _are_ other programs capable of doing this, such as Photoshop.

## Photoshop

Exporting images to WebP in Photoshop is possible, but is not as convenient as in Sketch. You’ll need to rely on a plug-in to get the job done. The good news, however, is that the Photoshop plug-in _does_ give you a bit more flexibility than Sketch does. To obtain the Photoshop plug-in for exporting WebP images, visit the [Telegraphics site](https://telegraphics.com.au/sw/product/WebPFormat#webpformat) and grab the version for your system. Once installed, start Photoshop and open an image. Once opened, you can export an image to WebP through the **Save As...** dialog. At the bottom of the dialog where you choose a format, you’ll notice two options: WebP, and WebP Lossless.

What happens from here depends on what you choose in the dropdown. If you choose WebP Lossless, the file will be exported, and that will be that. If you choose WebP, however, you’ll be presented with a dialog with several configuration options:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/009581bc-a12d-4c6a-85e7-c648020d0ea1/03-converting-images-to-webp-chapter.png" sizes="100vw" caption="The Photoshop plug-in’s lossy WebP export dialog. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/009581bc-a12d-4c6a-85e7-c648020d0ea1/03-converting-images-to-webp-chapter.png'>Large preview</a>)" alt="A dialogue in Photoshop for the WebP plugin showing various options for export quality, denoising, and filtering." >}}

In most cases, you’ll merely adjust the encoding quality, but feel free to experiment with the filtering, denoising, and sharpness options to obtain the desired result. Unfortunately, this plug-in lacks the ability to show a preview of the image before you save it. If you’re accustomed to using the **Save for Web** tool, this is kind of a bummer, as you’ll have to go at it blind.

Of course, if you’re not a fan of tinkering around in imaging software, the easiest possible option for using WebP might just be to rely on an image optimization CDN. Cloudinary is one such service.

## Cloudinary

Using WebP is not a frictionless experience, and the easiest way to use it is to never have to convert to the format on your own in the first place. Some online services can do this work for you, and Cloudinary is one of them.

You only need to upload images to the service. From there, Cloudinary will optimize your images for you. These optimizations are highly customizable, and one such optimization is to automatically serve whatever image format is optimal for your users. If you use Cloudinary to serve your site’s images _and_ your visitors are using WebP-capable browsers, Cloudinary takes on the hassle of serving WebP images for you, provided you choose the proper URL parameters. When you upload an image, Cloudinary’s control panel will provide a URL to your image that looks something like this:

<pre><code class="language-bash">https://res.cloudinary.com/drp9iwjqz/image/upload/v1508291830/jeremywagner.me/using-webp-images/tacos-2x.jpg</code></pre>

Using any number of URL parameters, you can change how Cloudinary serves images to you, including serving WebP images automatically to clients that can best handle them. The parameter that controls this behavior is _f_auto_, which tells Cloudinary to automatically pick the best format for the client issuing the request. Parameters are added after the _/upload/_ portion in the URL like so:

<pre><code class="language-bash">https://res.cloudinary.com/drp9iwjqz/image/upload/f_auto/v1508291830/jeremywagner.me/using-webp-images/tacos-2x.jpg</code></pre>

Though Cloudinary preserves the extension, you can tell what the content type of the image is by looking at the image’s _Content-Type_ response header. If you’re using a browser that supports WebP, that header will have a value of _image/webp_. Of course, Cloudinary is capable of more than simply serving the best format for a given browser. You can combine multiple parameters by separating them with commas. For example, here’s how you could tell Cloudinary to automatically pick the best format _and_ the best quality setting (represented by <code>q_auto</code>):

<pre><code class="language-bash">https://res.cloudinary.com/drp9iwjqz/image/upload/f_auto,q_auto/v1508291830/jeremywagner.me/using-webp-images/tacos-2x.jpg</code></pre>

To learn more about what Cloudinary is capable of, [check out their documentation](https://cloudinary.com/documentation).

While Cloudinary is a convenient tool that does the work of image optimization for you, you may yet feel compelled to encode your own images. And there are plenty of good reasons to do so! Beyond using imaging software, you can accomplish this with perhaps the most flexibility by using the Google’s official WebP command line encoder.

## The Official cwebp Command Line Encoder

The official tool for encoding images to the WebP format is Google’s own command line utility. While a command line program may not be as easy to use as a graphical interface, it offers much more flexibility in controlling the output. Most graphical front-ends that export to WebP abstract away features that don’t neatly fit into a dialog, and thus aren’t the best tools for achieving the best result for your site. Before you can use the command line encoder, however, you’ll need to install it.

### Installing

Your installation method will depend on your operating system. The easiest way to install the WebP encoder will be through your operating system’s package manager. macOS users can install the encoder and related tools using the [Homebrew package manager](https://brew.sh/):

<pre><code class="language-bash">brew install webp
</code></pre>

Windows users can install the encoder using [Chocolatey](https://chocolatey.org/):

<pre><code class="language-bash">choco install webp
</code></pre>

Users of Red Hat and Red Hat-derived Linux distros such as CentOS or Fedora can use yum to install the encoder:

<pre><code class="language-bash">yum install libwebp-tools
</code></pre>

Other platforms may use different package managers (such as `apt-get` for Debian Linux), but the mere presence of a package manager doesn’t mean it will provide a way to install the encoder. If your operating system package manager somehow fails you, the WebP encoder is available via [Node.js’s own package manager](https://www.npmjs.com/) (npm):

If none of these options work for you, [you can always download the source](https://github.com/webmproject/libwebp) and compile your own binaries. It’s a bit onerous, but the option _is_ there.

With the encoder installed, let’s take a look at some quick examples of how you can use it.

### Simple Command Line Examples

The WebP encoder can be invoked with the `cwebp` command. For starters, let’s examine what is arguably the most common use case of converting an image to lossy WebP:

<pre><code class="language-bash">cwebp -q 75 source.png -o output.webp
</code></pre>

This command takes a PNG and outputs it to lossy WebP by way of the `-o` parameter. By default, the encoder outputs lossy WebP images, and the quality of the output can be set from 0 to 100 via the `-q` parameter. The default lossy quality setting is 75.

You may remember reading earlier that WebP is capable of full alpha transparency, even for lossy images. You can control the quality of this transparency in the same fashion via the `-alpha_q` parameter:

<pre><code class="language-bash">cwebp -q 75 -alpha_q 10 source.png -o output.web
</code></pre>

`-alpha_q` applies lossy compression to the transparency in an image. The default for `-alpha_q` is 100, which is lossless. You can further reduce output size by lowering this value, which will apply lossy compression to the transparency, but lowering it _too_ much can significantly degrade the quality of transparent regions in the image.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/642ec547-e4b8-43ae-b257-67f42d2c4938/04-converting-images-to-webp-chapter.png" sizes="100vw" caption="A lossy transparent WebP with best transparency quality (left), and a lossy transparent WebP with low transparency quality (right). Note the loss of fine details at the cloud’s edges. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/642ec547-e4b8-43ae-b257-67f42d2c4938/04-converting-images-to-webp-chapter.png'>Large preview</a>)" alt="A side-by-side comparison of two transparent WebP images of a cloud on a checkered background. The image on the left is a lossy WebP exported at a quality of 75 at 26.88 kB. The image on the right is a lossy WebP exported at the same quality, but with a much poorer transparency quality of 10/100 (albeit at a much smaller file size of 8.45 kB)." >}}

If you’re conservative in adjusting `-alpha_q`, you can reduce the size of transparent images even further, but be sure to examine the output to ensure it’s acceptable to you. If you’re automating conversion of images (through a shell script, for example), you might want to shy away from setting this parameter at all. It’s also worth noting that `-alpha_q` has no effect when encoding lossless WebP images.

We’ve discussed encoding lossy WebP images with cwebp, but what if you want to export to lossless WebP? Just use the `-lossless` option:

<pre><code class="language-bash">cwebp -lossless source.png -o output.webp
</code></pre>

Depending on image content, you may not realize as much of a reduction in output file size when compared to lossy WebP. You _can_ control the aggressiveness of the compression via the `-z` parameter, though:

<pre><code class="language-bash">cwebp -lossless -z 9 source.png -o output.webp
</code></pre>

The `-z` parameter accepts a value between 0 (no compression) and 9 (most compression). Higher compression yields lower file sizes, but requires more time to encode images. You can also set the `-m` parameter to influence output size, which specifies a compression method from 0 to 6:

<pre><code class="language-bash">cwebp -lossless -m 6 -z 9 source.png -o output.webp
</code></pre>

You can also use the `-q` parameter to tell cwebp how aggressively to compress the image, which can be slightly confusing because `-q` means something entirely different for lossless WebP than it does for lossy images For lossless WebP, `-q 100` applies the most compression, whereas `-q 0` applies the least. You can use `-q` in tandem with the `-m` and `-z` parameters to achieve very high compression, like so:

<pre><code class="language-bash">cwebp -lossless -m 6 -z 9 -q 100 source.png -o output.webp
</code></pre>

This level of compression takes by far the longest, but it can go quite a ways further in reducing your lossless image payloads. Experiment to find what works best for you. You might shave off more kilobytes than you thought possible!

Of course, these are just some quick examples of what’s possible. cwebp is an amazingly flexible encoder. To get the full list of available options, type `cwebp -longhelp` and poke around.

There’s a good chance you’ll need to convert a whole bunch of images at once. Next, I’ll show you a couple ways you can convert multiple files with short commands for Unix-like systems on bash.

### Bulk Conversion in Bash

If you’re using Bash on a Unix-like operating system such as macOS or Ubuntu, and you have a directory of images you need to convert to WebP, the `find` command does an excellent job. As the name would imply, `find` finds objects in the file system. The syntax for finding files by a specific extension is very straightforward:

<pre><code class="language-bash">find ./ -type f -name '*.png'
</code></pre>

In case you’re not familiar with how `find` works, let’s step through this example command.

1. The first argument is the file system path to search, which in this case, is the current directory.
2. The second argument specifies the type of file system object. You can find directories with `-type d`. We’re finding files in this case, however, which means we’re going with `-type f`.
3. Lastly, the `-name` argument is the pattern by which to find files. In this instance, we’re finding all files ending in _.png_. When we run this command in a directory tree containing PNG files, the output might look something like this:

<pre><code class="language-bash">./sources/5-1024w.png
./sources/14-768w.png
./sources/old/15-768w.png
</code></pre>

This might not seem very useful by itself, but here’s where the magic happens: you can take the files found by `find` and redirect them as input to any other program you want via the `-exec` parameter. Here’s how you could use `-exec` with cwebp to encode all PNGs in a subtree to lossy WebP images at a quality setting of 75:

<pre><code class="language-bash">find ./ -type f -name '*.png' -exec sh -c 'cwebp -q 75 $1 -o "${1%.png}.webp"' _ {} \;
</code></pre>

This may look a bit convoluted, but let’s step through what’s going on so we can better understand it together:

1. The initial part of the command finds all files ending with a _.png_ extension in the current directory (and subdirectories), just as we described earlier.
2. Files found are sent to the `-exec` parameter, which invokes an instance of the `sh` shell. The `-c` parameter accepts a command to run.
3. The command invoked is the `cwebp` encoder. The `-q` argument is the quality setting.
4. The `$1` placeholder represents the file found by `find` as an argument passed into `sh`. The `-o "${1%.png}.webp"` portion is the output file name. The pattern expressed replaces the _.png_ extension with a _.webp_ extension.
5. The final part passes the reference to the file found by `find` (represented by `{}`) to `sh`, and the entire command is terminated by `\;`.

While this is admittedly a bit unwieldy, it’s quite useful when you need to convert a number of images to WebP quickly. When invoking cwebp in this fashion, feel free to adjust parameters as necessary to achieve the desired results. Just be aware this example command dumps the converted images into the same folder as the source images, so adjust as needed to control the location of the output.

The only drawback of this approach is it may take a long time to finish if you’re processing a large number of files, since images are processed one after the other rather than concurrently. If you need to speed up processing a bit, you might consider parallelizing image processing, which we’ll talk about next.

### Concurrent Bulk Conversion in Bash

Here’s a potential scenario. You have hundreds, perhaps thousands of images you need to convert to WebP. While cwebp is reasonably fast, it can still take a very long time if you’re not processing images concurrently. Serialized processing doesn’t make the best use of your CPU’s potential like concurrent processing does. To get around this, you can augment the earlier command used for serialized batch conversion with `xargs` like so:

<pre><code class="language-bash">find ./ -type f -name '*.png' | xargs -P 8 -I {} sh -c 'cwebp -q 75 $1 -o "${1%.png}.webp"' _ {} \;
</code></pre>

This isn’t much different than the command from earlier, except with some key differences:

1. The `-exec` parameter is notably absent. Instead, the output from `find` is piped directly to `xargs`, which handles processing in lieu of `-exec`.
2. The `xargs` command immediately follows the `|` character with three specific parts. The first is the `-P` parameter, which specifies the maximum amount of concurrent processes (8 in this example). The second is the `-I` parameter, which is the input `xargs` acts on (the value of which is the file found by `find`, represented by the `{}` placeholder). The final argument is the command `xargs` will execute, which is exactly the same as in the serialized bulk conversion command from before.

If you want to increase the amount of concurrent processes, simply change the value you pass to the `-P` parameter. Unlike other asynchronous approaches, `xargs` allows you to throttle concurrency to a specified maximum so you don’t render your system unresponsive. While this approach may only shave off a few seconds for small batches of images, it shines when operating on very large ones. For example, when converting a batch of roughly 10,000 JPEGs to WebP, a serialized approach using only `find` took 21 minutes and 26 seconds, whereas a concurrent approach using _both_ `find` and `xargs` took **9 minutes and 8 seconds**. This is approximately a **57% decrease** in processing time, and with a relatively conservative concurrency of 8 processes at a time. If you can afford to bump up concurrency, you may realize further reductions in processing time.

{{% ad-panel %}}

Of course, these commands aren’t limited to merely converting images to WebP. Whatever shell commands you can think of that will work with `find` and/or `xargs` will be just as serviceable. Experiment and see what you can pull off.

If converting images to WebP this way isn’t to your liking, maybe you’d prefer to accomplish the task in JavaScript. Next, we’ll talk about how to convert your images to WebP using Node.js, as well as within the various build systems available in the Node.js ecosystem.

## Convert Images to WebP with Node.js

Node.js’s only use isn’t just a JavaScript application stack. Even in environments where JavaScript isn’t used in an application back-end, Node.js still proves useful as a build tool. The tool used for exporting images to WebP in Node.js or any Node.js-based build system is imagemin. [Imagemin](https://github.com/imagemin/imagemin) is a tool that converts and optimizes images of all formats, but it can be extended to support WebP conversion via [imagemin-webp](https://github.com/imagemin/imagemin-webp). Whether you’re writing scripts to run with Node.js, or using one of many Node.js-based build systems (gulp, et al.), imagemin is the ticket. Let’s get started by demonstrating how you can convert images to WebP in a simple Node.js script.

### Using a Node.js Script

Perhaps you’re not the type to reach for an opinionated build system first, and prefer to use Node.js scripts instead. That’s reasonable enough, and if you know how to write JavaScript, the learning curve isn’t very steep, since you don’t need to learn the syntax of a build system. To get started on converting images to WebP in Node.js, install the imagemin and imagemin-webp modules in your project root directory:

<pre><code class="language-bash">npm install imagemin imagemin-webp
</code></pre>

This command installs two modules: the first is imagemin itself, and the second is the imagemin-webp plug-in that extends imagemin so it can convert images to WebP. With these two modules installed locally in our project, we can then write a small script that will process JPEG images in a directory and convert them to WebP:

<pre><code class="language-javascript">const imagemin = require("imagemin");
const webp = require("imagemin-webp");

imagemin(["sources/*.png"], "images", {
  use: [
    webp({
      quality: 75
    })
  ]
}).then(function() {
  console.log("Images converted!");
});
</code></pre>

This short script imports the imagemin and imagemin-webp modules into the current script as two constants (`imagemin` and `webp`, respectively). We then run imagemin’s main method, which takes three arguments:

1. The location of the source images. In this case, we’re converting all files ending in _.png_ in the sources directory, which is assumed to be located in the same directory as the script itself.
2. The destination directory, which in this case is _images_. This directory is created if it doesn’t already exist.
3. An options object for the imagemin program. In this case, we’re specifying the use option, which allows us to pass plug-ins into imagemin. The only plug-in we’re using here is an instance of imagemin-webp (represented by the `webp` constant). The plug-in itself also accepts a configuration object, which we have used to specify that we want all PNGs converted to lossy WebP (implied, as lossy encoding is the default) with a `quality` setting of 75.

Imagemin will convert images for us, and when it’s finished, it will return a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). In that Promise, we output to the console that all of the images have been converted. If we save this script as _webp.js_, we can run it with the `node` command like so:

<pre><code class="language-bash">node webp.js
</code></pre>

Assuming everything is successful, a message will appear in the console:

<pre><code class="language-bash">Images converted!
</code></pre>

When all is done, WebP images should now exist in the _images_ directory, relative to the location of where you saved _webp.js_. If you want to tweak the output, [you can do so through a variety of options](https://github.com/imagemin/imagemin-webp#api). For example, if you wanted to to generate lossless WebP images, you would instead use the `lossless` option like so:

<pre><code class="language-javascript">webp({
  lossless: true
})
</code></pre>

Just be aware that [as stated earlier](This needs to link back to the description for the -q setting), the quality setting for lossless mode adjusts the compression. The compression is still lossless, but higher settings will generate smaller files.

Pro tip: the options you can pass to this plug-in are the same, no matter where you invoke the imagemin-webp plug-in, be it in a Node.js script, or the build system of your choice. Speaking of build systems, let’s next cover how you might convert images using gulp.

### Using gulp

As far as build systems go, [gulp](https://gulpjs.com/) is pretty common. Thanks to a huge ecosystem of plug-ins, gulp can do almost anything you’d need it to, including converting images to WebP! If you have gulp installed and configured for your project, you only need to install a few extra node modules at the command line:

<pre><code class="language-bash">npm install gulp-imagemin imagemin-webp gulp-ext-replace
</code></pre>

[gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin) is a plug-in that allows imagemin to interface with gulp. As in the previous example using a plain Node.js script, imagemin-webp is the plug-in that allows imagemin to export images to the WebP format. The final plug-in, gulp-ext-replace, just allows us to change the extension of files output by gulp. By default, gulp outputs files with the same extension as their input source. [gulp-ext-replace](https://github.com/tjeastmond/gulp-ext-replace) helps us to overcome this so we can write WebP images to the disk with the proper _.webp_ extension.

Once you have these plug-ins installed, you’d just need to write a quick gulp task that reads source images from the disk and outputs them to WebP format. That task might look something like this:

<div class="break-out">

<pre><code class="language-javascript">const gulp = require("gulp");
const imagemin = require("gulp-imagemin");
const webp = require("imagemin-webp");
const extReplace = require("gulp-ext-replace");

gulp.task("exportWebP", function() {
  let src = "src/images/**/*.png"; // Where your PNGs are coming from.
  let dest = "dist/images"; // Where your WebPs are going.

  return gulp.src(src)
    .pipe(imagemin([
      webp({
        quality: 75
      })
    ]))
    .pipe(extReplace(".webp"))
    .pipe(gulp.dest(dest));
});
</code></pre></div>

There’s a lot going on here, so let’s break it down:

1. Like any Node.js-driven program, the first part of the script imports the modules necessary for the script to work.
2. Using the `gulp.task` method, we create a task named `exportWebP`, which starts with two variables: `src` points to the image files we want to process (PNG files in this example). `dest` points to the directory where the resulting WebP images will be written to.
3. The `gulp.src` method reads the PNG images from the location specified by the `src` variable.
4. Images are ferried to imagemin by the `gulp.pipe` method. The sole argument passed to imagemin is an array of imagemin plug-ins, which in this case is the sole imagemin-webp plug-in. As is the case with using imagemin in any environment, the arguments passed to the imagemin-webp plug-in (or any imagemin plug-in) will follow the same format.
5. Before we write the converted WebP images to the disk, we want to ensure the resulting files are written with a _.webp_ extension by using the gulp-ext-replace plug-in.
6. Using gulp’s `dest` method, we write all the converted images to the location specified earlier by the `dist` variable.

When everything’s in place, we can invoke gulp on the command line to convert images in the _src/images_ directory like so:

<pre><code class="language-bash">gulp exportWebP
</code></pre>

Once the command finishes, your destination directory will contain WebP images you converted from whatever gulp finds in the source directory. That simple!

If you prefer Grunt over gulp, you’re in luck. Next, we’ll show an example of how you can use Grunt to convert images to WebP.

### Using Grunt

Much like gulp, [Grunt](https://gruntjs.com/) is a task runner, albeit with a different syntax. It can be used for many of the same things gulp is used for, including optimization and conversion of images to different formats via imagemin. Unsurprisingly, it too can convert images to WebP by way of imagemin’s imagemin-webp plug-in. If you have a project currently using Grunt that you would like to modify to generate WebP images, it’s a relatively trivial task. In the directory containing _Gruntfile.js_, simply install these two modules like so:

<pre><code class="language-bash">npm install grunt-contrib-imagemin imagemin-webp
</code></pre>

This command installs the imagemin plug-in for Grunt (provided by [grunt-contrib-imagemin](https://github.com/gruntjs/grunt-contrib-imagemin)), as well as the familiar imagemin-webp plug-in used to convert images to WebP. Once the installation finishes, you’ll need to set up a Grunt task in _Gruntfile.js_ like so:

<pre><code class="language-javascript">const grunt = require("grunt");
const webp = require("imagemin-webp");

grunt.initConfig({
  imagemin: {
    dist: {
      options: {
        use: [webp({
          quality: 75
        })]
      },
      files: [{
        expand: true,
        cwd: "src/images/",
        src: ["**/*.png"],
        dest: "dist/images",
        ext: ".webp"
      }]
    }
  }
});

grunt.loadNpmTasks("grunt-contrib-imagemin");
</code></pre>

Once again, let’s step through this code and find out what’s going on:

1. Initially, we `require` the necessary grunt and imagemin-webp modules that we’ll need for the imagemin Grunt task.
2. In the imagemin task, we create a `dist` target, which is what we’ll run from the command line. This target contains an `options` object for Grunt’s imagemin plug-in that allows us to specify configuration options. In this case, we supply an instance of the imagemin-webp plug-in and pass the usual options to it.
3. The `files` object is the guts of the operation. cwd specifies which directory we want to work within. `src` specifies the files within `cwd` that we want to convert to WebP. `dest` specifies the directory we want to output the converted images to. Finally, `ext` specifies that we want the converted images to be saved with a _.webp_ extension.
4. The last line of code loads the grunt-contrib-imagemin plug-in so we can use it in the Gruntfile.

Once you have this in place, you can convert images to WebP like so:

<pre><code class="language-bash">grunt imagemin:dist
</code></pre>

Once this command finishes, images ending in _.png_ in the directory specified in `files.cwd` will be converted to WebP, and output to the directory specified in `files.dest`.

Grunt is not quite as intuitive as gulp is, and is falling out of use somewhat. However, it’s still a serviceable choice for a build system, and you may yet encounter it in some situations.

To round out our documentation of how to convert images to WebP within the the Node.js ecosystem, let’s discuss how you might accomplish that same task in webpack.

{{% ad-panel-leaderboard %}}

## Using Webpack

If you’re developing modern JavaScript applications, chances are high that [webpack](https://webpack.js.org/) is in your midst. In contrast to gulp and Grunt, which style themselves as task runners, webpack is a module bundler that analyzes your code starting from one or more entry points and generates optimized output. While much of what webpack does is accomplished through loaders, it does have a large ecosystem of plug-ins, too. imagemin is represented in that space by imagemin-webpack-plugin.

How webpack works and how to write a config for it are complex subjects, especially if you’re used to using task runners like gulp. I’m going to assume you have at least _some_ familiarity with webpack basics, and just show you how to add imagemin to an existing webpack config to convert images to WebP. Like gulp and Grunt before, you’ll need to use npm to install a few necessary Node.js modules:

<pre><code class="language-bash">npm install imagemin-webpack-plugin imagemin-webp copy-webpack-plugin
</code></pre>

Similar to how gulp has its own imagemin plug-in, webpack has one as well, in the form of [imagemin-webpack-plugin](https://github.com/Klathmon/imagemin-webpack-plugin). And as is the case with all imagemin-related use cases, the imagemin-webp plug-in provides the WebP conversion functionality. The [copy-webpack-plugin](https://github.com/webpack-contrib/copy-webpack-plugin) module is used in this case to help us copy images from a source folder, and tell imagemin to process those images for us. Webpack can be rigged up with loaders (e.g., [file-loader](https://github.com/webpack-contrib/file-loader)) to pipe the files it encounters in its dependency graph to imagemin intelligently, but it may be more expedient to specify a source directory on the disk and let imagemin churn through everything it finds and spit out images to the destination directory. Such code might look something like this:

<div class="break-out">

<pre><code class="language-javascript">ImageminWebpackPlugin = require("imagemin-webpack-plugin").default;
ImageminWebP = require("imagemin-webp");
CopyWebpackPlugin = require("copy-webpack-plugin");

module.exports = {
  // Omitted required entry, output, and loader configs for brevity...
  plugins: [
    new CopyWebpackPlugin([{
      from: "./src/images/*.png",
      to: "./images/[name].webp"
    }]),
    new ImageminWebpackPlugin({
      plugins: [
        ImageminWebP({
          quality: 75
        })
      ]
    })
  ]
};
</code></pre></div>

As we have with other code examples, let’s step through everything and get a handle on what’s happening:

1. As noted, the required entry, output, and loader configurations have been omitted for brevity and relevance, as we’re assuming you have _some_ familiarity with webpack.
2. The `plugins` config is merely an array of plug-ins we want to use. The first plug-in in the array is an instance of copy-webpack-plugin. To start, we specify in `from` the files we want to copy from the source directory. In this example, we include all files ending in _.png_ from a specific source directory.
3. Next, we tell copy-webpack-plugin where we want the optimized images to go in the `to` option. It’s important to note in this option that we’re using a placeholder of `[name]` to tell copy-webpack-plugin that we want the name of the output file to be the same as its corresponding source. However, because we’re outputting WebP files, we don’t want to preserve the source file’s extension, so we’re hardcoding the output file’s extension to _.webp_. It’s also important to remember that files will be written to a location relative to whatever is set in `output.path` earlier in your webpack config.
4. The next plug-in in the sequence is an instance of imagemin-webpack-plugin, which should look familiar to other imagemin use cases. Here, we’re simply passing an instance of the imagemin-webp plug-in to the imagemin instance.

Using this configuration, all images ending in _.png_ found in _./src/images_ will be converted to WebP and output to the images directory relative to your configuration’s `output.path` directory.

While there are multiple approaches to converting images to WebP within webpack, this aims to be the most straightforward. Compared to other build systems, webpack is an incredibly rich (and at times complex) tool. This example is not meant to be _the_ authoritative approach to generating WebP images within webpack, but rather to show that it’s possible.

## Did You Like This Excerpt? Here’s Why This eBook May Be, Just May Be, For You 😉
<p><em>The WebP Manual</em> will get you ready for the new image format that is capable to significantly less data-intensive user experiences for a majority of your audience:</p>
<ul>
<li>Learn how lossy and lossless WebP compare to JPEGs and PNGs exported by a number of image encoders.</li>
<li>Learn which services and plugins you can use to export or convert images to WebP with your preferred design tool or command line tool.</li>
<li>Learn how to can use WebP in production, and how to implement proper fallbacks for browsers that don’t support WebP just yet.</li>
<li>Learn how to use the full potential of the WebP format. It will substantially improve loading performance for many of your users, customers, and clients, and it will become one of your favorite tools for making websites as lean as possible. </li>
</ul>

<p><em>The eBook is <a href="https://www.smashingmagazine.com/membership#plans">free for Smashing Members</a> (you can cancel anytime, of course)</em>.</p>

<figure><img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1531926616/webp-manual-ipad-opt_akcnzz.png" width="800" height="800" alt="A mockup of The WebP Manual’s cover on a white iPad" /></a></figure>

<div class="book-cta" data-handler="ContentTabs" data-mq="(max-width: 480px)">
  <nav class="content-tabs content-tabs--books">
  <ul>
     <li class="content-tab">
     <button class="btn btn--small btn--white btn--white--bordered">eBook</button>
     </li>
     <li class="content-tab">
     <button class="btn btn--small btn--white btn--white--bordered">Free for Members</button>
     </li>
   </ul>
 </nav>
  <div id="getthebook" class="book-cta__col book-cta__hardcover content-tab--content">
  <span class="book-cta__price"><span class="green">$14.90</span></span><a class="btn btn--full btn--large btn--green" data-product-sku="the-webp-manual" data-component="AddToCart" data-product-path="/ebooks/the-webp-manual/">Get the eBook</a>
  <p class="book-cta__desc">PDF, ePUB, Kindle.</p>
  </div>
  <div class="book-cta__col book-cta__ebook content-tab--content">
  <span class="book-cta__price"><span class="green">$0.00 </span><span class="book-cta__price--del"><del>$14.90</del></span></span> <a class="btn btn--full btn--large btn--green" href="/membership/signup/member">Free for Members&nbsp;&rarr;</a>
   <p class="book-cta__desc">...along with <a href="https://www.smashingmagazine.com/membership/smashing/#webinars"><span class="small-caps">12</span> webinars</a> and <a href="https://www.smashingmagazine.com/ebooks"><span class="small-caps">56</span> other eBooks</a>.</em></small></p>
    </div>
</div>
