---
title: Responsive Web Design With Physical Units
slug: responsive-web-design-with-physical-units
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb4e4dfd-7ceb-4391-9502-578b48ec29ce/device-screen.png
date: 2013-03-21T13:08:18.000Z
author: radu-chelariu
description: >-
  This post should be titled “Getting Ahead of Yourself.” “…By a Few Years,” actually. Here’s the deal: at the time I’m writing this, early 2013, there’s no way to accurately design for the Web using physical units, nor will there be for a very long time. But there is a way to design while knowing the physical characteristics of the device — or, at least, there will be in the very near future.
categories:
  - Mobile
  - Responsive Design
---
This post should be titled “Getting Ahead of Yourself.” “…By a Few Years,” actually. Here’s the deal: at the time I’m writing this, early 2013, there’s no way to accurately design for the Web using physical units, nor will there be for a very long time. But there is a way to design while knowing the physical characteristics of the device — or, at least, there will be in the very near future.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc84e727-842f-48f8-b6bb-8ff720086f86/mobile-devices.jpg" alt="Mobile devices" width="500" height="281" /><br>
<figcaption>Different devices can have a similar screen resolution, yet entirely different physical factors. iPad (1st generation) has the diagonal size of 9.7", the resolution 1024 × 768 and 132 ppi. Kindle Keyboard 3G has the diagonal size of 6", also the resolution 768 × 1024, yet 212 ppi. Image source: <a href="https://www.flickr.com/photos/kodomut/5154254605/sizes/m/in/photostream/">kodomut</a>.</figcaption></figure>

It’s called the “resolution media query”, and it’s been in the specification for media queries for some time. However, while it has been in the spec, that doesn’t mean anyone has actually implemented it yet. Fortunately, <a title="Kenneth did something awesome!" href="https://www.webkit.org/blog/2194/last-week-in-webkit-resolution-media-queries-and-timeouts-for-xhr/">WebKit is leading the way</a> and pushing for this feature to be implemented. So, how will we use this nifty little feature, exactly? Here’s how.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Techniques For Gracefully Degrading Media Queries](https://www.smashingmagazine.com/2011/08/techniques-for-gracefully-degrading-media-queries/)
*   [<span class="headline">Automatically Art-Directed Responsive Images? Here You Go.</span>](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/)
*   [Logical Breakpoints For Your Responsive Design](https://www.smashingmagazine.com/2013/03/logical-breakpoints-responsive-design/)

{{% feature-panel %}}

## The Thin Line Between Queries

First off, I posit that there will be only one use case for a resolution-only media query. Something along the lines of

<pre><code class="language-css">
@media (min-resolution: 250dpi) {

}
</code></pre>

has, at this time, only one good use: swapping out low- for high-resolution images. I’ve tried imagining other uses and, as far as I can tell, there just aren’t any. But resolution is not what we, as Web designers, are truly interested in. Since we are designing for humans, shouldn't we be thinking about the physical side of human data consumption and designing using this kind of a metric? And in a perfect world we could simply say <code>width: 1in</code> and have a one-inch wide element, regardless of the device. Unfortunately, we live in a digital world in which the physical and digital pixels are not the same. We need something to bridge the gap. That something is the resolution media query.

Good. Now that that’s out of the way, let me show you how this one little piece of code can make so much difference that your head will promptly explode. (I take no responsibility for actual blown heads as a result of this post.)

Let’s compare two media-query declarations:

<pre><code class="language-css">
@media (min-resolution: 341dpi) and (min-width: 767px) &gt; {

}
</code></pre>

and

<pre><code class="language-css">
@media (max-resolution: 131dpi) and (min-width: 767px) &gt; {

}
</code></pre>

At first glance, this doesn’t seem like much of a separation, right? Wrong. The numbers I’ve used are specific to the HTC Windows Phone 8X (the first snippet) and the iPad 2 (the second snippet). By using the resolution query, one can basically separate physically small devices from large devices.

As it currently stands, a query that looks like <code>@media (min-width: 767px){ }</code> will affect both the HTC and the iPad, with no other possibility of separation, because both have a resolution that is 768 pixels wide. In fact, the iPad has a lower resolution, at 1024 × 768, whereas the HTC is 1280 × 768. In case you haven’t realized yet, the problem with all of this is that the iPad is a 10-inch device, while the HTC is a 4.3-inch one. That’s less than half the physical size!

By using the resolution media query together with a width query, we can distinguish between physically small and large devices to adjust design elements and layouts accordingly. While, as mentioned above, screen resolution isn't <em>really</em> what we are interested in since we use <a href="https://www.smashingmagazine.com/2013/03/01/logical-breakpoints-responsive-design/">logical breakpoints in responsive design</a>, it <em>is</em> useful to know whether a site is being displayed on a small or a large physical display — e.g. to increase font size or rearrange design elements in the layout. But where do we draw the line between small and large? Quite simply, we can’t. Each of us has to draw the line, possibly on a project-by-project basis, between “This is a small device” and “This is a large device.” As far as ballpark numbers go, I’ve done a few calculations and have developed a theorem that should give you a clearer idea of how this works more or less.

## The Physical Size Inquiry Non-Exhaustive Theorem (PSINET)

Here’s the theory: In a combined query, if the ratio between the smaller of the width and height and the resolution, called a <strong>PSINET</strong> score, is higher than <strong>5</strong>, then the result falls in the category of a physically large device. If the resulting number is lower than 5, then it is a physically small device. Devices that score very close to 5 are considered to be medium-sized, close to the physical size of an A4 sheet of paper (21 × 29.7 cm).

Here’s a non-exhaustive list of devices to test the formula above. I’ve listed each device’s score according to the formula, along with its diagonal size, resolution and density, and PSINET score.</p>

### Physically Large Devices

<table class="table-overview">
<thead>
<tr>
<th>Device name</th>
<th style="width: 5em">Diagonal size (inches)</th>
<th>Resolution</th>
<th>PPI</th>
<th>PSINET score</th>
</tr>
</thead>
<tbody>
<tr>
<td>Apple iMac</td>
<td>27</td>
<td>2560 × 1440</td>
<td>109</td>
<td>13.00</td>
</tr>
<tr>
<td>Sony Vaio F</td>
<td>16.4</td>
<td>1920 × 1080</td>
<td>134</td>
<td>8.05</td>
</tr>
<tr>
<td>Apple MacBook Pro RD</td>
<td>13</td>
<td>2560 × 1600</td>
<td>227</td>
<td>7.04</td>
</tr>
</tbody>
</table>

### Physically Small Devices

<table class="table-overview">
<thead>
<tr>
<th>Device name</th>
<th style="width: 5em">Diagonal size (inches)</th>
<th>Resolution</th>
<th>PPI</th>
<th>PSINET score</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sony PSP</td>
<td>4.3</td>
<td>480 × 272</td>
<td>128</td>
<td>3.75</td>
</tr>
<tr>
<td>Kindle Keyboard 3G</td>
<td>6</td>
<td>768 × 1024</td>
<td>212</td>
<td>3.62</td>
</tr>
<tr>
<td>Kindle Fire</td>
<td>7</td>
<td>1024 × 600</td>
<td>169</td>
<td>3.55</td>
</tr>
<tr>
<td>Samsung Galaxy S</td>
<td>4</td>
<td>480 × 800</td>
<td>160</td>
<td>3.00</td>
</tr>
<tr>
<td>Samsung Galaxy NoteII</td>
<td>5.5</td>
<td>720 × 1280</td>
<td>267</td>
<td>2.69</td>
</tr>
<tr>
<td>Samsung Galaxy S IV</td>
<td>5</td>
<td>1080 × 1920</td>
<td>441</td>
<td>2.62</td>
</tr>
<tr>
<td>HTC Butterfly</td>
<td>5</td>
<td>1080 × 1920</td>
<td>441</td>
<td>2.62</td>
</tr>
<tr>
<td>Samsung Galaxy Grand I9082</td>
<td>5</td>
<td>480 × 800</td>
<td>187</td>
<td>2.56</td>
</tr>
<tr>
<td>Palm Pre</td>
<td>3.1</td>
<td>480 × 320</td>
<td>186</td>
<td>2.5</td>
</tr>
<tr>
<td>Sony Xperia Z</td>
<td>5</td>
<td>1920 × 1080</td>
<td>443</td>
<td>2.43</td>
</tr>
<tr>
<td>Samsung Galaxy SIII</td>
<td>4.8</td>
<td>720 × 1280</td>
<td>306</td>
<td>2.35</td>
</tr>
<tr>
<td>LG Nexus 4 E960</td>
<td>4.7</td>
<td>768 × 1280</td>
<td>318</td>
<td>2.41</td>
</tr>
<tr>
<td>Nokia Lumia 920</td>
<td>4.5</td>
<td>1280 × 768</td>
<td>332</td>
<td>2.31</td>
</tr>
<tr>
<td>HTC One</td>
<td>4.7</td>
<td>1080 × 1920</td>
<td>469</td>
<td>2.30</td>
</tr>
<tr>
<td>HTC One X</td>
<td>4.7</td>
<td>720 × 1280</td>
<td>312</td>
<td>2.30</td>
</tr>
<tr>
<td>HTC Desire HD</td>
<td>4.3</td>
<td>480 × 800</td>
<td>217</td>
<td>2.21</td>
</tr>
<tr>
<td>BlackBerry Q10</td>
<td>3.1</td>
<td>720 × 720</td>
<td>328</td>
<td>2.19</td>
</tr>
<tr>
<td>BlackBerry Z10</td>
<td>4.2</td>
<td>768 × 1280</td>
<td>355</td>
<td>2.16</td>
</tr>
<tr>
<td>Motorola Droid X</td>
<td>4.3</td>
<td>854 × 480</td>
<td>228</td>
<td>2.10</td>
</tr>
<tr>
<td>Sony Ericsson S</td>
<td>4.3</td>
<td>720 × 1280</td>
<td>342</td>
<td>2.10</td>
</tr>
<tr>
<td>Motorola RAZR i XT890</td>
<td>4.3</td>
<td>540 × 960</td>
<td>256</td>
<td>2.10</td>
</tr>
<tr>
<td>iPhone 5</td>
<td>4</td>
<td>640 × 1136</td>
<td>326</td>
<td>1.96</td>
</tr>
<tr>
<td>Apple iPod Touch</td>
<td>3.5</td>
<td>960 × 640</td>
<td>326</td>
<td>1.96</td>
</tr>
<tr>
<td>Nokia Lumia 620</td>
<td>3.8</td>
<td>480 × 800</td>
<td>246</td>
<td>1.95</td>
</tr>
<tr>
<td>HTC Wildfire</td>
<td>3.2</td>
<td>240 × 320</td>
<td>125</td>
<td>1.92</td>
</tr>
<tr>
<td>Nokia Lumia 710</td>
<td>3.7</td>
<td>800 × 480</td>
<td>252</td>
<td>1.90</td>
</tr>
<tr>
<td>Motorola Defy</td>
<td>3.7</td>
<td>854 × 480</td>
<td>265</td>
<td>1.81</td>
</tr>
<tr>
<td>LG Optimus One</td>
<td>3.2</td>
<td>320 × 480</td>
<td>180</td>
<td>1.77</td>
</tr>
<tr>
<td>Nokia N96</td>
<td>2.8</td>
<td>240 × 320</td>
<td>143</td>
<td>1.67</td>
</tr>
<tr>
<td>Sony Ericsson W810i</td>
<td>1.9</td>
<td>176 × 220</td>
<td>148</td>
<td>1.18</td>
</tr>
</tbody>
</table>

### Medium-Sized Devices

<table class="table-overview">
<thead>
<tr>
<th>Device name</th>
<th style="width: 5em">Diagonal size (inches)</th>
<th>Resolution</th>
<th>PPI</th>
<th>PSINET score</th>
</tr>
</thead>
<tbody>
<tr>
<td>Apple iPad (1 &amp; 2)</td>
<td>9.7</td>
<td>1024 × 768</td>
<td>132</td>
<td>5.81</td>
</tr>
<tr>
<td>Apple iPad (3rd Gen)</td>
<td>9.7</td>
<td>2048 × 1536</td>
<td>264</td>
<td>5.81</td>
</tr>
<tr>
<td>Amazon Kindle DX</td>
<td>9.7</td>
<td>824 × 1200</td>
<td>150</td>
<td>5.49</td>
</tr>
<tr>
<td>Acer Iconia Tab A500</td>
<td>10.1</td>
<td>800 × 1280</td>
<td>149</td>
<td>5.36</td>
</tr>
<tr>
<td>Samsung Galaxy Tab</td>
<td>10.1</td>
<td>1280 × 800</td>
<td>149</td>
<td>5.36</td>
</tr>
<tr>
<td>Motorola Xoom</td>
<td>10.1</td>
<td>1280 × 800</td>
<td>149</td>
<td>5.36</td>
</tr>
<tr>
<td>Asus Transformer Pad Infinity</td>
<td>10.1</td>
<td>1920 × 1200</td>
<td>224</td>
<td>5.35</td>
</tr>
<tr>
<td>Microsoft Surface</td>
<td>10.1</td>
<td>1366 × 768</td>
<td>148</td>
<td>5.18</td>
</tr>
<tr>
<td>Asus VivoTab RT TF600T</td>
<td>10.1</td>
<td>1366 × 768</td>
<td>155</td>
<td>4.95</td>
</tr>
<tr>
<td>iPad Mini</td>
<td>7.9</td>
<td>768 × 1024</td>
<td>162</td>
<td>4.74</td>
</tr>
<tr>
<td>Amazon Kindle Fire HD</td>
<td>8.9</td>
<td>1920 × 1200</td>
<td>254</td>
<td>4.72</td>
</tr>
</tbody>
</table>

Is this method of determining device size foolproof? Hardly — that’s why it’s a theorem. It’s based on solid reasoning and empirical evidence and has come about by using the scientific method, but it is not a rule, law or axiom. Take it with a pinch of salt (or, better yet, a truckload of NaCl) and refine it. It is a theorem, a proposition, to be remembered in the future when the resolution media query and our work with it become a mainstay of the Web.</p>

### Breaking the Theorem

Like any self-respecting follower of the scientific method, I’ve tried to break my own theorem. Thus, I imagined a freak of a device, 2 inches long and 20 inches wide, putting its diagonal size at 20.09 inches, with a 240 × 40 pixel display, yielding a resolution of just 11.94 PPI. It gets a PSINET score of 2.01, which puts it well into the small device category, even though it’s almost half a meter long. The reason is simple: it’s that 2-inch-wide dimension. Because the PSINET score ignores the longer of the device’s physical width and height, the greater the difference between those two dimensions, the less accurate the PSINET score will be. Sure, this beast of a device is unlikely to ever become reality, but it’s worth understanding the reasons why it would break the theorem.
<table class="table-overview">
<thead>
<tr>
<th>Device name</th>
<th style="width: 5em">Diagonal size (inches)</th>
<th>Resolution</th>
<th>PPI</th>
<th>PSINET score</th>
</tr>
</thead>
<tbody>
<tr>
<td>ThinLong</td>
<td>20.09</td>
<td>24 × 240</td>
<td>11.94</td>
<td>2.01</td>
</tr>
</tbody>
</table>

## Real-World Applications

Apart from the obvious visual changes and tweaks mentioned above, there are other ways to use the resolution media query.

Enter <a href="https://wicky.nillia.ms/enquire.js/">Enquire.js</a>. For those of you who haven’t heard of it, it’s a very nice JavaScript library that helps you execute particular scripts on matching media queries.

We could use Enquire.js or even just <a href="https://developer.mozilla.org/en-US/docs/DOM/window.matchMedia">window.matchMedia</a>, which is a native JavaScript method, to differentiate between mobile, tablet and computer users much more reliably than by using width queries alone. Here’s a not-very-polite example using Enquire.js:

<pre><code class="language-javascript">
enquire.register("screen and max-resolution: 150dpi and max-width: 300px", function() {
    alert('My, what a small screen you have there, Grandma!')
});
</code></pre>

Combining media query types with CSS and using a resolution-aware JavaScript library is just the right formula to give us real future-proof control over what I call the “physical Web.” Imagine being able to view a priceless sculpture located in a museum halfway across the Earth on a 1:1 ratio on any device, or shopping for an engagement ring online and seeing exactly how big that 24-carat diamond is. The real-world applications, pun intended, are nearly endless.

In our world of responsive Web design, we’d very much like to provide the best experience to users, whatever their device. In light of the sans-resolution media query above, that task becomes less of a challenge and more a windmill fight. Assigning blame is pointless, because none of us can do anything to change the current ecosystem of devices. Manufacturers will continue to put out devices with resolutions and pixel densities that they’ve pulled out of their butts, and that’s fine — that’s their business. Staying on top of the situation by providing us designers with the tools we need (but can’t easily build ourselves) to create the best user experience possible is the job of browser makers, and I salute the good people at WebKit for spearheading the implementation of the resolution media query.

{{< signature "al" >}}

