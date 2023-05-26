---
title: 'Responsive Image Container: A Way Forward For Responsive Images?'
slug: responsive-image-container
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aa34dfa-11ca-4700-b57d-e2990e8d1aa7/mobile-01.jpg
date: 2013-09-24T09:10:14.000Z
author: yoav-weiss
description: >-
  It’s been a year since I last wrote about it, but the dream of a “magical”
  image format that will solve world hunger and/or the responsive images problem
  (whichever comes first) lives on. A few weeks back, I started wondering if
  such an image format could be used to solve both the art direction and
  resolution-switching use cases.
categories:
  - Mobile
  - Responsive Design
---
<em>The aim of republishing the <a href="https://blog.yoav.ws/2013/09/Responsive-Image-Container">original article by Yoav</a> is to raise awareness and support the discussion about solutions for responsive images. We look forward to your opinions and thoughts in the comments section! – Ed.</em>

It’s been a year since <a href="https://blog.yoav.ws/2012/08/Fetching-responsive-image-format">I last wrote about it</a>, but the dream of a “magical” image format that will solve world hunger and/or the responsive images problem (whichever comes first) lives on. A few weeks back, I started wondering if such an image format could be used to solve both the <a href="https://usecases.responsiveimages.org/#art-direction">art direction</a> and <a href="https://usecases.responsiveimages.org/#resolution-switching">resolution-switching</a> use cases.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [<span class="headline">Automatically Art-Directed Responsive Images?</span>](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

I had a few ideas on how this could be done, so <strong>I created a prototype</strong> to prove its feasibility. The prototype is <a href="https://github.com/yoavweiss/Responsive-Image-Container">now available</a>, ready to be tinkered with. In this post, I’ll explain what this prototype does, what it cannot do, how it works, and its advantages and disadvantages relative to markup solutions. I’ll also try to de-unicorn the concept of a responsive-image format and make it more tangible and less magical.

{{% feature-panel %}}

## "Got Something Against Markup Solutions?"

No, I don’t! Honestly! Some of my best friends are markup solutions.

I’ve been participating in the Responsive Images Community Group for a while now, prototyping, promoting and presenting markup solutions. Current markup solutions (<code>picture</code> <em>and</em> <code>srcset</code>) are great and can cover all of the important use cases for responsive images. And if it was up to me, I’d vote to start shipping both <code>picture</code> and <code>srcset</code> (i.e. its resolution-switching version) in all browsers tomorrow.

But the overall markup-based solution has some flaws. Here’s some of the criticism I’ve been hearing for the last year or so when talking about markup solutions for responsive images.</p>

### Too Verbose

Markup solution are, by definition, verbose because they must enumerate all of the various resources. When art direction is involved, they must also list the breakpoints, which add to that verbosity.</p>

### Mixing Presentation and Content

A markup solution that is art direction-oriented needs to keep layout breakpoints in the markup. This mixes presentation and content and means that any layout changes would force changes to the markup.

<a href="https://lists.w3.org/Archives/Public/www-style/2013May/0638.html">Constructive discussions</a> have taken place on how this can be resolved — particularly by bringing back the media query definitions into CSS — but it’s not certain when any of this will be defined and implemented.</p>

### Define Viewport-Based Breakpoints

This one is proposed often by developers. For performance reasons, markup-based solutions are based on viewport size, rather than on image dimensions. Because the layout dimensions of images are not yet known to the browser by the time it starts fetching images, it cannot rely on them to decide which resources to fetch.

This means that developers will need to store some sort of table of viewports and dimensions on the server side, or maintain one in their head, in order to create images that are ideally sized for certain viewport dimensions and layouts.

While the addition of a build step could resolve this issue in many cases, it can get complicated in cases where a single component is used over multiple pages, with varying dimensions on each.</p>

### Results in Excessive Downloading in Some Cases

OK, this one I hear mostly in my head (and from other Web performance freaks on occasion).

From a performance perspective, any solution that’s based on separate resources for different screen sizes and dimensions will require the entire images to be redownloaded if the screen size or dimensions change to a higher resolution. Because most of that image data will very likely already be in the browser’s memory or cache, having to redownload everything from scratch would be sad.

All of the above makes me wonder (again) how wonderful life would be if we had a solution based on a file format that addresses these issues.</p>

## Why Would A File Format Be Better?

A solution based on a file format would do better for the following reasons:

*   The burden is put on the image encoder. The markup would remain identical to what it is today: a single tag with a single resource.
*   Automatically converting websites to such a responsive-image solution might be easier because the automation layer would focus only on the images themselves, rather than on the page’s markup and layout.
*   Changes to image layout (as a result of changes to the viewport’s dimensions) could be handled by downloading only the difference between current image and the higher-resolution one, without having to redownload the data that the browser already has in memory.
*   Web developers would not need to maintain multiple versions of each image resource, although they would have to keep a non-responsive version of the image for the purpose of content negotiation.

This is my attempt at a simpler solution based on file format that would relieve Web developers of much grunt work and would avoid useless image data from having to be downloaded (even when conditions change), while keeping preloaders working.</p>

## Why Not Progressive JPEG?

Progressive JPEG could <a href="https://blog.yoav.ws/2012/05/Responsive-image-format">serve this role</a> for the resolution-switching case, but it’s extremely rigid. It comes with strict limits on the lowest image quality and, from what I’ve seen, is often too data-heavy. Also, the minimal difference between resolutions is limited and doesn’t give enough control to encoders that want to do better. Furthermore, progressive JPEG cannot handle art direction at all.</p>

## What Would It Look Like?

We’re talking about a responsive image container, containing internal layers that could be WebP or JPEG-XR or any future format. It uses resizing and cropping operations to cover both the resolution-switching and the art direction use cases.

The decoder (i.e. the browser) would then be able to download just the number of layers it needs (and their bytes) in order to show a certain image. Each layer would enhance the layer before it, giving the decoder the data it needs to show it properly at a higher resolution.

## How Does It Work?

1.  The encoder takes the original image, along with a description of the required output resolutions and, optionally, directives on art direction.
2.  It then outputs one layer per resolution that the final image should be perfectly rendered in.
3.  Each layer represents the difference in image data between the previous layer (when “stretched” on the current layer’s canvas) and the current layer’s “original” image. This way, **the decoder can construct the layers one by one**, each time using the previous layer to recreate the current one, creating a higher resolution image as it goes.

Support for resolution-switching is obvious in this case, but art direction could also be supported by positioning the previous layer on the current one and being able to give it certain dimensions. Let’s look at some examples.</p>

### Art Direction

Here’s a photo that is often used in discussions about the art direction use case:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/098d588e-5a6e-4b92-9c3d-dca713275a3e/crop-mini.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138893" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88edbef8-bece-4a85-976e-601ebbf01e27/crop-500-mini.jpg" alt="Obama in a jeep factory - original with context" width="500" height="332" /></a>

Let’s see what the smallest layer would look like:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a2a1c4-1321-4cf5-8efb-0d2bb51dbf50/crop.jpg_layer1"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138895" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a2a1c4-1321-4cf5-8efb-0d2bb51dbf50/crop.jpg_layer1" alt="Obama in a jeep factory - cropped to show only Obama" width="200" height="200" /></a>

That’s just a cropped version of the original. Nothing special.

Now, one layer above that:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77e707aa-2c94-45c0-b014-df29e52348ec/crop.jpg_layer2"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138897" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77e707aa-2c94-45c0-b014-df29e52348ec/crop.jpg_layer2" alt="Obama in a jeep factory - some context + diff from previous layer" width="400" height="288" /></a>

You can see that <strong>pixels that don’t appear in the previous layer are shown as normal</strong>, while pixels that do appear there contain only the difference between them and the equivalent ones in the previous layer.

And here’s the third, final layer:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88c7a981-fb14-4e0a-a9e0-95b911a55c08/crop.jpg_layer3"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138898" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88c7a981-fb14-4e0a-a9e0-95b911a55c08/crop.jpg_layer3" alt="Obama in a jeep factory - full context + diff from previous layer" width="500" height="332" /></a>

### Resolution-Switching

A high-resolution photo of a fruit:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0baecb80-662b-4cc2-8e6f-ef19ac5ed7fb/res-switch-shrink-mini.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138899" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0baecb80-662b-4cc2-8e6f-ef19ac5ed7fb/res-switch-shrink-mini.png" alt="iPhone - original resolution" width="336" height="635" /></a>

Here is the first layer, showing a significantly downsized version:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83b023a3-4d14-4660-8f7c-be6ac0dc797a/res-switch.png_layer1"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138900" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83b023a3-4d14-4660-8f7c-be6ac0dc797a/res-switch.png_layer1" alt="iPhone - significantly downsized" width="106" height="200" /></a>

The second layer shows the difference between a medium-sized version and the
“stretched” previous layer:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ce7d5fe-0bca-4c55-a187-67755b436757/res-switch.png_layer2"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138901" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ce7d5fe-0bca-4c55-a187-67755b436757/res-switch.png_layer2" alt="iPhone - medium sized diff" width="211" height="400" /></a>

The third layer shows the difference between the original and the “stretched” previous layer:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733c2028-b25c-448f-ab90-5f5d630923ca/res-switch.png_layer3"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="138902" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733c2028-b25c-448f-ab90-5f5d630923ca/res-switch.png_layer3" alt="iPhone - full sized diff" width="336" height="635" /></a>

If you’re interested in more detail, you can go to the <a href="https://github.com/yoavweiss/Responsive-Image-Container">repository</a>. More detail on the <a href="https://github.com/yoavweiss/Responsive-Image-Container/blob/master/container.md">container’s structure</a> is also there.</p>

### “But I Need More From Art Direction”

I’ve seen cases where rotation and image repositioning are required for art direction, usually in order to add a logo at different locations around the image itself, depending on the viewport’s dimensions.

This use case is probably better served by CSS. CSS transforms can handle rotation, while CSS positioning, along with media-specific background images, could probably handle the rest.

<em><strong>Note</strong>: If your art direction is special and can’t be handled by either one of these, I’d love to hear about it.</em>

## How Is It Fetched?

This is where things get tricky. A special fetching mechanism must be created to fetch this type of image. I can’t say that I have figured that part out, but here’s my rough idea on how it could work.

<strong>My proposed mechanism relies on HTTP ranges</strong>, similar to the fetching mechanisms of the <code>&lt;video&gt;</code> element, when seeks are involved.

More specifically:

*   Resources that should be fetched progressively should be flagged as such. One possibility is to add a `progressive` attribute to the element that describes the resource.
*   Once the browser detects an image resource with a `progressive` attribute on it, it picks the initial requested range for that resource. The initial range request could be:
    *   a relatively small fixed range for all images (like 8 KB);
    *   specified by the author (for example, as a value of the `progressive` attribute);
    *   some heuristic;
    *   based on a manifest (which we’ll get to later).
*   The browser can fetch this initial range at the same time that it requests the entire resource today, or even sooner, because the chances of starving critical path resources (including CSS and JavaScript) are slimmer once the payloads are of a known size.
*   Once the browser has downloaded the image’s initial range, it has the file’s offset table box, which links byte offset to resolution. This means that once the browser has calculated the page’s layout, it will know exactly which byte range it needs in order to display the image correctly.
*   Assuming that the browser sees fit, it could heuristically fetch follow-up layers (i.e. of higher resolutions) even before it knows for certain that they are needed.
*   Once the browser has the page’s layout, it can complete fetching all of the required image layers.

The mechanism above will increase the number of HTTP requests, which in an HTTP/1.1 world would introduce some delay in many cases.

This mechanism <strong>may be optimized by defining a manifest</strong> that describes the byte ranges of the image resources to the browser. The idea of adding a manifest was proposed by <a href="https://twitter.com/cconcolato">Cyril Concolato</a> at the W3C’s Technical Plenary / Advisory Committee meetings week last year, and it makes a lot of sense, borrowing from our collective experience with video streaming. It enables browsers to avoid fetching an arbitrary initial range (at least once the manifest is downloaded itself).

Adding a manifest will prevent these extra requests for everything requested after the layout, and it might help to prevent them (using heuristics) even before the layout.

Creating a manifest could be easily delegated either to development tools or to the server-side layer, so that developers don’t have to manually deal with these image-specific details.</p>

### “Couldn’t We Simply Reset the Connection?”

In theory, we could address this by fetching the entire image, and then reset the connection once the browser has all the necessary data, but that would most likely introduce serious performance issues.

Here are the problems with reseting a TCP connection during a browsing session:

*   It terminates an already connected, warmed-up TCP connection, whose set-up had a significant performance cost and which could have been reused for future resources.
*   It sends at least a round-trip time’s worth of data down the pipe, the time it takes for the browser’s reset to reach the server. That data is never read by the browser, which means wasted bandwidth and slower loading times.</p>

## Downsides To This Approach

There are a few downsides to this approach:

*   It involves touching and modifying many pieces of the browser stack, which means that standardization and implementation could be painful and take a while.
*   The [monochrome and print use case](https://usecases.responsiveimages.org/#matching-media-features-and-media-types) cannot be addressed by this type of a solution.
*   The decoding algorithm involves per-layer upscaling, which could be processing-heavy. Therefore, decoding performance could be an issue. Moving this to the GPU might help, but I don’t know that area well enough to judge. If you have an opinion on the subject, I’d appreciate your comments.
*   Introducing a new file format is a long process. As we have seen with the introduction of previous image formats, the **lack of a client-side mechanism** makes this a painful process for Web developers. Because new file formats start out being supported in some browsers but not others, a server-side mechanism must be used (hopefully based on the `Accept` header, rather than on the `User-Agent` header). I’m hoping that this new file format’s simplicity and reliance on other file formats to do the heavy lifting help here, but I’m not sure they would.
*   As discussed, it would likely increase the number of requests, and could introduce some delay in HTTP/1.1.
*   This solution **cannot address the need for “pixel-perfect” images**, which is mainly needed to improve decoding speed. Even if it did, it’s not certain that decoding speed would benefit from it.
*   Relying on HTTP ranges for the fetching mechanism could result in some problem with intermediate cache servers, which don’t support it.</p>

## So, Should We Dump Markup-Based Solutions?

Not at all. This is a prototype, showing how most of the responsive-image use cases would have been solved by such a container.

Reaching consensus on this solution, defining it in detail and implementing it in an interoperable way could be a long process. The performance implications on HTTP/1.1 websites and decoding speed still need to be explored.

I believe this might be a way to simplify responsive images in the future, but I don’t think we should wait for the ideal solution.</p>

## To Sum Up

If you’ve just skipped to here, that’s OK. This is a long post.

To sum it up, I’ve demonstrated (along with a prototype) how a responsive-image format could work and how it could resolve most responsive-image use cases. I also went into some detail about which other bits would have to be added to the solution in order to make it a viable solution.

I consider this to be a long-term solution because some key issues need to be addressed before it can be made practical. In my opinion, <strong>the main issue is decoding performance</strong>, with the impact of downloading performance on HTTP/1.1 being a close second.

Continuing to explore this option is worthwhile, but let’s not wait for it. Responsive images need an in-browser, real-life solution <del>two years ago</del> today, not two years from now.

{{< signature "al, ea, il" >}}

