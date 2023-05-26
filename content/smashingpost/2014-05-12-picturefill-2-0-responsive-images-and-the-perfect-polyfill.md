---
title: 'Picturefill 2.0: Responsive Images And The Perfect Polyfill'
slug: picturefill-2-0-responsive-images-and-the-perfect-polyfill
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e06400-8f0c-4adf-9abd-c9df9ec06613/illu-picturefill.jpg
date: 2014-05-12T19:18:20.000Z
author: tim-wright
summary: >-
  We’ve come a long way with responsive images. We can see the light at the end of the tunnel, but a lot of work still has to be done.
description: >-
  We’ve come a long way with responsive images. We can see the light at the end of the tunnel, but a lot of work still has to be done.
categories:
  - Coding
  - CSS
  - JavaScript
  - Responsive Design
---
Not since the early days of web standards have I seen our community rally around a seemingly small issue: responsive images.

Over the last <a href="https://alistapart.com/article/responsive-web-design/">four years</a> (yeah, it’s been about four years), we’ve seen many permutations of images in responsive design. From the lazier days of setting <code>max-width: 100%</code> (the absolute minimum you should be doing) to more full-featured JavaScript implementations, such as Picturefill and Zurb’s <code>data-interchange</code> method, we’ve spent a lot of time spinning our wheels, banging our heads and screaming at the wall. I’m happy to say that our tireless journey is coming to a close. The W3C and browser makers got the hint.

## The State Of Responsive Images

In our search for the holy grail of serving the right image to the user, our attitude towards browser makers until now has largely been, “Forget you &mdash; we’ll do it ourselves.” I’m certainly no exception. We were so attentive to responsive images and were exposed to all of the guesswork and trials that are not typically released to the public that we got impatient (rightfully so) and did it with JavaScript.

<strong>The difference between a CSS transition and a responsive image is, of course, how they degrade</strong>. If a CSS transition doesn’t work, who really cares? Your interface might be a little jumpy, but the experience as a whole won’t really suffer because your users will still be able to accomplish their goal and consume the content they need.

That really isn’t the case with images. How does a new image tag degrade? The <code>img</code> tag is so widely accepted that I couldn’t even find when the W3C recommended it as a standard, other than a small reference in the <a href="https://www.w3.org/TR/html401/struct/objects.html#h-13.2">HTML 4.01 specification</a>. Replacing or even expanding on the <code>img</code> tag would be like telling Frank Sinatra to wear a baseball cap instead of a fedora &mdash; you’ll get some pushback.

### Resource Problems

As responsive design grew in popularity and as the media through which users consume information became uncontrollable, we slowly realized that <code>img</code> by itself wasn’t going to cut the mustard. We started asking questions like, “What screen size is the user on?” and “What’s the pixel density of the screen?” These questions fuelled our image techniques until we realized that screen size and pixel density have absolutely no relationship to the amount of bandwidth available to serve up a huge high-definition image.

<img loading="lazy" decoding="async" title="The RICG began working on the picture element, sharing its work with the W3C along the way." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee3fa72e-a1ec-4795-957a-05cf69b26b91/02-logo-ricg-opt.png" alt="The RICG began working on the picture element, sharing its work with the W3C along the way." width="500" height="183" /><br>
<em>The RICG began working on the <code>picture</code> element, sharing its work with the W3C along the way.</em>

The solutions got pretty complex. Talk of the <code>picture</code> element started, and a group called the Responsive Images Community Group (RICG) appeared. The RICG began working on the <code>picture</code> element, sharing its work with the W3C along the way. The result has led us to today and this discussion about all of the progress that’s been made.

### The Introduction of `srcset`

Because most of the responsive-image community was on board with the <code>picture</code> element and looking forward to it because of the great polyfills, such as Picturefill, it went ahead and released a well thought-out and fleshed-out document outlining something called <code>srcset</code>, which is an extension of the standard <code>img</code> tag. Yeah, I know &mdash; it feels like it came out of nowhere. It was also super-complicated and overly limiting by restricting you to (implied) pixel values and using a microsyntax that didn’t allow for scalability with media queries in the future. Luckily, the syntax has matured into what we have today, which is a fairly robust recommendation.

Most recently, Andrew Clark said it best <a href="https://twitter.com/Malarkey/status/458336077934522368">when he tweeted</a>, “Looked at the responsive images srcset &amp; sizes attributes for the first time. Blimey it’s complicated.”

I couldn’t have said it better myself. Let’s look at what we’re dealing with:

<pre><code class="language-markup">&lt;img alt="dog" src="dog.jpg" srcset="dog-HD.jpg 2x, dog-narrow.jpg 300w, dog-narrow-HD.jpg 600w 2x"&gt;  
</code></pre>

Three major attributes are in the snippet above: <code>alt</code>, <code>src</code> and <code>srcset</code>. The <code>alt</code> attribute is the same as it’s always been; <code>src</code> is the fallback if <code>srcset</code> isn’t supported; and <code>srcset</code> is obviously the meat and potatoes here.

We can see three arguments in <code>srcset</code>. The first is the image path. The second gives the browser information about the natural widths of the sources, so that it knows which resource to serve to the user (based on the user’s preferences and cross-referencing with <a href="https://ericportis.com/posts/2014/srcset-sizes/">the <code>sizes</code> attribute</a> – I told you it was complicated). The last piece sets the optional pixel ratio (<code>2x</code> in this example specifies the high-definition image).

One thing I really love about <code>srcset</code> is that the specification states that the browser should contain image-allocation preferences for certain bandwidth situations. This means you don’t have to worry about serving a <code>2x</code> image to a high-definition screen if that device is on a cruddy 3G connection. The user’s preferences should take over, and the browser would choose the appropriate image to serve.

### Preparing for the `picture` Element

After much complaining about our new weird friend, <code>srcset</code>, the RICG continued working on the <code>picture</code> element, which is finally getting some serious traction with browser makers… well, that is, with Chrome. The proposed syntax for the <code>picture</code> element might look familiar because we saw it largely in the first version of Picturefill, and it’s not unlike how <code>&lt;audio&gt;</code> and <code>&lt;video&gt;</code> are marked up.

<pre><code class="language-markup">&lt;picture&gt;
  &lt;source media="(min-width: 600px)" srcset="large-1.jpg, large-2.jpg 2x"&gt;
  &lt;img alt="A fat dog" src="small-1.jpg"&gt;
&lt;/picture&gt;  
</code></pre>

As you can see, a <code>source</code> tag is in the <code>picture</code> element, along with a normal <code>img</code> tag. Just as we saw with <code>src</code> in <code>srcset</code>, the <code>img</code> is a fallback. In the <code>source</code> tag, we have what looks like a media query, alongside a <code>srcset</code> attribute that contains the same image-source and pixel-density arguments as before. This seems like a nice clean way to popularize responsive images; we’re generally familiar with the syntax, so it should be easily adopted.

### Browser Support

The <code>srcset</code> attribute has been <a href="https://caniuse.com/#search=srcset">supported in Chrome</a> since version 34. At the time of writing, it is not supported anywhere else. Mozilla appears to be working on an implementation (fingers crossed). Internet Explorer is nowhere in sight.

The <code>picture</code> element has even worse support; it isn’t even in Chrome yet. But like Mozilla with <code>srcset</code>, Google is currently working on implementing it. If you can stomach reading through a specification, I highly recommend it. Even though there isn’t much of a plot and the character development is pretty weak, it’s still a pretty good read.

<strong>Picturefill 2.0 was created because native support is reasonably close</strong>. You know we’ll need a rock-solid polyfill to use when the time officially comes, so let’s take a look at it!

{{% feature-panel %}}

## Introducing Picturefill 2.0

<a href="https://scottjehl.github.io/picturefill/">Picturefill 2.0</a> was recently released as beta, and it’s quite a large jump from version 1. The RICG really aimed to create <strong>a one-stop solution for responsive images</strong>. The challenge was to create a script that allows you, the developer, to use any combination of the solutions currently being standardized, without bloating it to the point that not using it at all would be more lightweight.

Imagine polyfilling an image that would normally take 2 seconds to load using a JavaScript file that takes 10 seconds to load &mdash; it wouldn’t make much sense. Picturefill 2.0 avoids this by following the specification very closely (with some intentional omissions, which we’ll go over in a bit) and letting you use either <code>srcset</code> or <code>picture</code> or a combination of the two.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f39c9dd-4b70-4c16-abe3-1453cb3373dd/01-devices-opt.jpg"><img loading="lazy" decoding="async" title="Picturefill is an responsive image approach that mimics the proposed picture element using divs." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5752c3bc-eb29-4b29-9526-d1fc7f2e67eb/01-devices-opt-500.jpg" alt="Picturefill is an responsive image approach that mimics the proposed picture element using divs." width="500" height="325" /></a><br>
<em>Picturefill is an responsive image approach that mimics the proposed picture element using <code>div</code>s. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f39c9dd-4b70-4c16-abe3-1453cb3373dd/01-devices-opt.jpg">Larger version</a>)</em>

While we can’t reliably achieve everything in the specification using JavaScript (such as reasonably detecting bandwidth, which would be a user setting anyway), we can certainly take care of all of the pieces that are meant to be in HTML (i.e. elements and attributes). This version of Picturefill gets us one step closer to not needing Picturefill, which is the ultimate goal of anyone who has ever written a polyfill.

If you’re currently using version 1.0, I highly recommend upgrading to 2.0. It’s a big step towards a better solution to serving the correct image to the user. Some big changes have been made to the syntax and functionality. Let’s look at what’s new.

### What’s New in 2.0

One thing that makes this polyfill different from others that I’ve seen is that it polyfills a concept, not just an unsupported block of HTML. Picturefill 1.0 used spans and custom attributes to mimic how we thought responsive images should work. For the record, it is a great solution, and I currently use it for many of my projects that haven’t been converted to 2.0.

In the last year or so, the specification for <code>srcset</code> and <code>picture</code> have matured so much, so we can now actually get to use something close to the real syntax. Picturefill is starting to look like a true polyfill, one we can strip away when real support shows up.

### Installing and Using the Polyfill

If you’ve read this far, then you’ve probably dealt with some form of polyfill in the past. This one isn’t much different. Polyfills are supposed to be set-it-and-forget-it (to steal a line from <a href="https://www.ronco.com/">Ronco</a>), but because this is an HTML polyfill, you’ll need either to create the <code>picture</code> element manually or use some form of HTML shiv to do it for you. Luckily, HTML shivs are pretty common and ship with toolkits such as <a href="https://modernizr.com/">Modernizr</a>; just verify that <code>picture</code> is supported in whatever shiv you choose.

<pre><code class="language-markup">&lt;!-- Create the actual picture element if you haven’t already. --&gt;
&lt;script&gt;
  document.createElement( "picture" );
&lt;/script&gt;

&lt;!-- Asynchronously load the polyfill. --&gt;
&lt;script src="picturefill.js" async&gt;&lt;/script&gt;  
</code></pre>

Other than creating the <code>picture</code> element, you simply have to link to the script. Using the <code>async</code> attribute is also recommended, so that Picturefill doesn’t block your page from loading.

### Using Picturefill 2.0 With srcset

Let’s look at the syntax that provides the best support and that uses <code>srcset</code>. It should look familiar because it has the same attributes that we saw when discussing the specification.

<pre><code class="language-markup">&lt;img sizes="100vw, (min-width: 40em) 80vw"
srcset="pic-small.png 400w, pic-medium.png 800w, pic-large.png 1200w" alt="Obama"&gt;  
</code></pre>

The most glaring difference between this snippet and the specification is the absence of a fallback <code>src</code> attribute, which was intentionally removed to prevent images from being downloaded twice in unsupported browsers. And, really, what would be the point of this if images were downloaded twice? Other than that, it’s pretty faithful to the specification, but it will probably evolve over time as the specification fleshes out and the polyfill matures.

The <code>sizes</code> attribute tells the browser of the image’s size relative to the viewport. This often gets overlooked because <code>srcset</code> is the buzzword now, but this attribute is equally important. If you’d like to learn more, <a href="https://ericportis.com/posts/2014/srcset-sizes/">Eric Portis makes a lot of sense</a> of this “blimey complicated mess.”

{{% ad-panel-leaderboard %}}

### Using Picturefill 2.0 With the `picture` Element

The RICG did such a good job with this second version of Picturefill that the syntax of the <code>picture</code> element should come as no surprise. It matches the specification very closely:

<pre><code class="language-markup">&lt;picture&gt;
  &lt;source srcset="extralarge.jpg, extralarge.jpg 2x" media="(min-width: 1000px)"&gt;
  &lt;source srcset="large.jpg, large.jpg 2x" media="(min-width: 800px)"&gt;
  &lt;source srcset="medium.jpg"&gt;
  &lt;img srcset="medium.jpg" alt="Cambodia Map"&gt;
&lt;/picture&gt;  
</code></pre>

The biggest change between versions 1.0 and 2.0 is the removal of some traditional HTML (divs and spans) and the addition of newer elements (<code>picture</code> and <code>source</code>). Also, <code>srcset</code> support is built in (heck, why not, right? It’s in the spec!). This is great step forward for this polyfill.

Use as many or as few of these options as you’d like. In line with the specification, if you don’t want to use the <code>2x</code> option, you don’t have to (and so on). <strong>The difference between this and the official <code>picture</code> element is the <code>img</code> fallback</strong>. You’ll notice here that the <code>img</code> fallback also has a <code>srcset</code> attribute, instead of a normal <code>src</code> (which is widely supported). Again, this is to prevent double-downloading (it’s a real problem). The <code>srcset</code> in the <code>img</code> tag would also cause double-downloading if the browser supports <code>srcset</code> but not <code>picture</code>. This bug should get worked out in the beta version.

Like many good polyfills, Picturefill 2.0 can be executed programmatically by exposing a global function, <code>picturefill()</code>. This allows you to use it in any ultra-hip JavaScript framework that you’d like. You can read about a few options for targeting specific images <a href="https://scottjehl.github.io/picturefill/#api">in the API documentation</a>.

### Degrading Gracefully

Earlier in the article, I alluded to the challenge of degrading the <code>img</code> tag gracefully in unsupported browsers. This was another problem in creating Picturefill 2.0. Because it is a polyfill, the concept of unsupported browsers doesn’t really exist (kind of) &mdash; we’re using JavaScript to force it to work.

The edge case is this: If a browser doesn’t natively support <code>picture</code> or <code>srcset</code> <em>and</em> has JavaScript turned off, then you’ll get a frowny face. I can already feel your eyes rolling, but knowing the limitations of a system is important before you rely on it on a large scale. If a user were to come across a Picturefill’ed image in an unsupported browser with JavaScript turned off, they would see the image’s <code>alt</code> text &mdash; a nice little way to reinforce the importance of descriptive and meaningful <code>alt</code> text, isn’t it?

Alternative text is the fallback because the previous <code>&lt;noscript&gt;</code> solution caused problems with browsers that support <code>picture</code> or <code>srcset</code> but have JavaScript disabled (two images would render). The group also explored adding a <code>src</code> attribute to <code>img</code> (as in the specification), but that results in double-downloading, which defeats the purpose of allocating the appropriate image assets to the user.

We’ve come a long way with responsive images. We can see the light at the end of the tunnel, but a lot of work still has to be done. And we’d love your help!

{{% ad-panel-leaderboard %}}

## How To Get Involved

If you’d like to get involved and help out with the responsive-images movement, join the <a href="https://www.w3.org/community/respimg/">RICG</a> via the W3C. If that’s too much, we’re always looking for people to try out Picturefill’s beta version and submit bugs through the <a href="https://github.com/scottjehl/picturefill/issues">issue tracker on GitHub</a>.

You can also spread the word about great tools like Sizer Soze, which calculates the performance cost of not using responsive images.

### Resources And Further Reading

*   [Responsive Images Community Group](https://responsiveimages.org/)
*   “[The `picture` Element](https://picture.responsiveimages.org/)” (specification), RICG
*   “The `srcset` Attribute” (specification), W3C
*   [@respimg](https://twitter.com/respimg), RICG on Twitter
*   [One Solution To Responsive Images](https://www.smashingmagazine.com/2014/02/one-solution-to-responsive-images/)
*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

{{< signature "al, ml" >}}
