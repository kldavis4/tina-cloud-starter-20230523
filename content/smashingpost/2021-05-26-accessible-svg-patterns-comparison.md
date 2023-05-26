---
title: 'Accessible SVGs: Perfect Patterns For Screen Reader Users'
slug: accessible-svg-patterns-comparison
author: carie-fisher
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bf2e3a-ae5b-49a3-843a-318b4c81f5af/accessible-svg-patterns.jpg
date: 2021-05-26T13:20:00.000Z
summary: >-
  Discover which SVG patterns we should avoid and which patterns are the most inclusive when comparing different combinations of OSs, browsers, and screen readers. Carie will also be running an online workshop on <a href='https://smashingconf.com/online-workshops/workshops/carie-fisher'>Accessible Front-End Patterns</a> all around front-end accessibility.
description: >-
  Discover which SVG patterns we should avoid and which patterns are the most inclusive when comparing different combinations of OSs, browsers, and screen readers.
categories:
  - SVG
  - Tools
  - Techniques
  - Accessibility
---

While Scalable Vector Graphics (SVGs) were first introduced in the late 90s, they have seen a massive resurgence in popularity in the last decade due to their extreme flexibility, high fidelity, and relative lightness in a world where bandwidth and performance matter more than ever. Advancements in JavaScript and the introduction of CSS media queries such [@prefers-color-scheme](https://caniuse.com/?search=prefers-color-scheme) and [@prefers-reduced-motion](https://caniuse.com/?search=prefers-reduced-motion) have extended the functionality of SVGs way beyond their initial use case of simply displaying vector images on a website.

As SVG technology advances, our understanding of how we design and develop SVGs needs to advance as well. Part of that advancement includes considering the impact of such designs and code on actual humans, aka our end users. 

This article outlines **twelve distinct SVG patterns** found “in the wild” and each alternative description announced when accessed by different combinations of operating systems, browsers, and screen readers.

Of course, the following examples are not meant to be an exhaustive list of all the possible patterns being used in the digital sphere, but they do highlight some of the more popular or **ubiquitous SVG patterns** you might encounter. Continue reading to discover which SVG patterns you should avoid and which patterns are the most inclusive!

## Basic Alternative Descriptions Using The `<img>` Tag

The first group of four patterns utilizes the `<img>` tag linking out to an SVG file. This is a good choice for basic, uncomplicated images on your website, app, or other digital product. While the drawback to using this pattern is that you cannot easily control many visual elements or animations as an inline SVG, this pattern should render lighter and faster images overall and allow for easier maintenance on SVGs that you use in multiple locations.

### Pattern #1: `<img>` + `alt="[words]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48790836-d63d-4447-b508-69a444240f88/1-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48790836-d63d-4447-b508-69a444240f88/1-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<div class="break-out">

 <pre><code class="language-svg">&lt;img class="fox" alt="What does the fox say?" src="https://upload.wikimedia.org/wikipedia/commons/3/39/Toicon-icon-fandom-howl.svg"&gt;
</code></pre>
</div>

### Pattern #2: `<img>` + `role="img"` + `alt="[words]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab0d4e8-cc8e-4d36-8569-d698dbb69c90/2-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab0d4e8-cc8e-4d36-8569-d698dbb69c90/2-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<div class="break-out">

 <pre><code class="language-svg">&lt;img role="img" class="fox" alt="What does the fox say?" src="https://upload.wikimedia.org/wikipedia/commons/3/39/Toicon-icon-fandom-howl.svg"&gt;
</code></pre>
</div>

### Pattern #3: `<img>` + `role="img"` + `aria-label="[words]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2248286f-d55a-4d49-967f-76a3c153a7c5/3-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2248286f-d55a-4d49-967f-76a3c153a7c5/3-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<div class="break-out">

 <pre><code class="language-svg">&lt;img role="img" class="fox" aria-label="What does the fox say?" src="https://upload.wikimedia.org/wikipedia/commons/3/39/Toicon-icon-fandom-howl.svg"&gt;
</code></pre>
</div>

### Pattern #4: `<img>` + `role="img"` + `aria-labelledby="[ID]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbe384a-56c6-4577-bc9b-f587b8c05663/4-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbe384a-56c6-4577-bc9b-f587b8c05663/4-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<div class="break-out">

 <pre><code class="language-svg">&lt;p id="caption1" class="visually-hidden"&gt;What does the fox say?&lt;/p&gt;
&lt;img role="img" aria-labelledby="caption1" class="fox" src="https://upload.wikimedia.org/wikipedia/commons/3/39/Toicon-icon-fandom-howl.svg"&gt;
</code></pre>
</div>

## Basic Alternative Descriptions Using The `<svg>` Tag

The second group of four patterns utilizes the `<svg>` tag with an inline SVG file. Although adding the SVG code directly into the markup could potentially make the page a bit slower to load, that minor inefficiency will be offset by having more control over the visual elements or animations of your images. By adding your SVG to the HTML directly, you also have more options when it comes to providing image information to your screen reader users.

### Pattern #5: `<svg>` + `role="img"` + `<title>`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1be2146-4ed3-4dd0-b8aa-88ea70112d03/5-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1be2146-4ed3-4dd0-b8aa-88ea70112d03/5-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<pre><code class="language-svg">&lt;svg role="img" ...&gt;
   &lt;title&gt;What does the fox say?&lt;/title&gt;
   [design code]
&lt;/svg&gt;
</code></pre>

### Pattern #6: `<svg>` + `role="img"` + `<text>`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1db57e58-5d73-4fe5-b15f-23fec976b17d/6-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1db57e58-5d73-4fe5-b15f-23fec976b17d/6-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<div class="break-out">

 <pre><code class="language-svg">&lt;svg role="img" ...&gt;
   &lt;text class="visually-hidden" font-size="0"&gt;What does the fox say?&lt;/text&gt;
   [design code]
&lt;/svg&gt;
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

### Pattern #7: `<svg>` + `role="img"` + `<title>` + `aria-describedby="[ID]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/533e5f3a-d0b0-4e89-8642-fd355fb557f8/7-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/533e5f3a-d0b0-4e89-8642-fd355fb557f8/7-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<pre><code class="language-svg">&lt;svg role="img" aria-describedby="fox7" ...&gt;
   &lt;title id="fox7"&gt;What does the fox say?&lt;/title&gt;
   [design code]
&lt;/svg&gt;
</code></pre>

### Pattern #8: `<svg>` + `role="img"` + `<title>` + `aria-labelledby="[ID]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c90ea4-a060-4ea4-a073-0fff9f08a12c/8-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c90ea4-a060-4ea4-a073-0fff9f08a12c/8-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<pre><code class="language-svg">&lt;svg role="img" aria-labelledby="fox8" ...&gt;
   &lt;title id="fox8"&gt;What does the fox say?&lt;/title&gt;
   [design code]
&lt;/svg&gt;
</code></pre>

{{% feature-panel id="accessibility-workshop" %}}

## Extended Alternative Descriptions Using The `<svg>` Tag

The last group of four patterns utilizes the `<svg>` tag with an inline SVG file, much like the second group. However, in this case, we are extending the simple alternative descriptions with additional information due to the complexity of the image.

This would be a good pattern choice for more complicated images that need more explanation. However, it is important to keep in mind that there are some people with disabilities — like cognitive disorders — who might benefit from having this additional image information readily available on the screen instead of buried in the SVG code.

Depending on the type and amount of information you need to add to your SVG, you might consider taking a different approach altogether.

### Pattern #9: `<svg>` + `role="img"` + `<title>` + `<text>`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b20fc272-e17f-4feb-ade6-a3b918b6d535/9-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b20fc272-e17f-4feb-ade6-a3b918b6d535/9-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<div class="break-out">

 <pre><code class="language-svg">&lt;svg role="img" ...&gt;
   &lt;title&gt;What does the fox say?&lt;/title&gt;
   &lt;text class="visually-hidden" font-size="0"&gt;Will we ever know?&lt;/text&gt;
   [design code]
&lt;/svg&gt;
</code></pre>
</div>

### Pattern #10: `<svg>` + `role="img"` + `<title>` + `<desc>`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62bed3c-3367-4e55-a4a1-06b350a5d239/10-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62bed3c-3367-4e55-a4a1-06b350a5d239/10-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<pre><code class="language-svg">&lt;svg role="img" ...&gt;
   &lt;title&gt;What does the fox say?&lt;/title&gt;
   &lt;desc&gt;Will we ever know?&lt;/desc&gt;
   [design code]
&lt;/svg&gt;
</code></pre>

### Pattern #11: `<svg>` + `role="img"` + `<title>` + `<desc>` + `aria-labelledby="[ID]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4061618-7397-4957-a887-bb259347df0b/11-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4061618-7397-4957-a887-bb259347df0b/11-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<pre><code class="language-svg">&lt;svg role="img" aria-labelledby="fox11 description11" ...&gt;
   &lt;title id="fox11"&gt;What does the fox say?&lt;/title&gt;
   &lt;desc id="description11"&gt;Will we ever know?&lt;/desc&gt;
   [design code]
&lt;/svg&gt;
</code></pre>

### Pattern #12: `<svg>` + `role="img"` + `<title>` + `<desc>` + `aria-describedby="[ID]"`

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23280c8b-5499-42b9-8628-728172b891e2/12-accessible-svg-pattern-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23280c8b-5499-42b9-8628-728172b891e2/12-accessible-svg-pattern-comparison.png" width="800" height="613" sizes="100vw" caption="" alt="fox illustration presented in the codepen example" >}}

<pre><code class="language-svg">&lt;svg role="img" aria-describedby="fox12 description12" ...&gt;
   &lt;title id="fox12"&gt;What does the fox say?&lt;/title&gt;
   &lt;desc id="description12"&gt;Will we ever know?&lt;/desc&gt;
   [design code]
&lt;/svg&gt;
</code></pre>

{{< codepen height="800" theme_id="light" slug_hash="dyvvbKj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the full CodePen [Accessible SVG Pattern Comparison (Fox Version)](https://codepen.io/smashingmag/pen/dyvvbKj) by <a href="https://codepen.io/cariefisher/pen/QWpjded">Carie Fisher</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

## SVG Pattern Winners And Losers

By running various screen readers on different combinations of operating systems and browsers, we see definite patterns emerging in the <a href="#testing-results">final results</a> table. There are some <strong>clear SVG pattern winners and losers</strong>, plus a few patterns somewhere in the middle that you could implement as long as you are aware of, and can accept their limitations. Looking over the results table, we can conclude the following:

### Basic Alternative Descriptions Using The `<img>` Tag (Group 1)

#### Best In Show

- **Pattern 2**: `<img> + role="img"` + `alt="[words]"`
- **Pattern 3**: `<img>` + `role="img"` + `aria-label="[words]"`

#### Use Caution

- **Pattern 4**: `<img>` + `role="img"` + `aria-labelledby="[ID]"`

#### Not Recommended

- **Pattern 1**: `<img>` + `alt="[words]"`

### Basic Alternative Descriptions Using The `<svg>` Tag (Group 2)

#### Best In Show

- **Pattern 5**: `<svg>` + `role="img"` + `<title>`
- **Pattern 8**: `<svg>` + `role="img"` + `<title>` + `aria-labelledby="[ID]"`

#### Use Caution

- **Pattern 7**: `<svg>` + `role="img"` + `<title>` + `aria-describedby="[ID]"`

#### Not Recommended

- **Pattern 6**: `<svg>` + `role="img"` + `<text>`

### Extended Alternative Descriptions Using The `<svg>` Tag (Group 3)

#### Best In Show

- **Pattern 11**: `<svg>` + `role="img"` + `<title>` + `<desc>` + `aria-labelledby="[ID]"`

**Note**: *While this pattern is not perfect as it repeated alternative descriptions, it did not ignore any of the elements in the testing, unlike the “use caution” patterns.*

### Use Caution

- **Pattern 9**: `<svg>` + `role="img"` + `<title>` + `<text>`
- **Pattern 10**: `<svg>` + `role="img"` + `<title>` + `<desc>`
- **Pattern 12**: `<svg>` + `role="img"` + `<title>` + `<desc>` + `aria-describedby="[ID]"`

#### Not Recommended

- None of the patterns in this group completely failed the tests.

## Testing Results

{{< codepen height="480" theme_id="light" slug_hash="YzZQBwG" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Testing Results](https://codepen.io/smashingmag/pen/YzZQBwG) by <a href="https://codepen.io/cariefisher/pen/QWpjded">Carie Fisher</a>.{{< /codepen >}}

## Wrapping Up

It is important to note that part of interpreting the results of the SVG pattern tests is understanding that creators of each screen reader have a **recommended browser(s)** that they fully support. This doesn’t mean you shouldn’t or couldn’t use a screen reader on a different browser, this just means that if you do, the results may not be as accurate as if you used the recommended one(s). 

The pattern testing for this article did include some **combinations of browsers and screen readers** that may fall into the “fringe” category, but there are also notes on which [combinations of operating systems, browsers, and screen readers](https://dequeuniversity.com/screenreaders/) are recommended for your own testing. The results of these tests should help you make the best SVG pattern decision possible, based on your pattern needs and constraints.

A reminder that before you settle on a pattern, please make sure you know the basics of [how and when to create accessible images](https://www.smashingmagazine.com/2020/05/accessible-images/) and that you fully understand the [required alternative information needed](https://www.w3.org/WAI/tutorials/images/) for the different image types.

If you need additional help deciding on which pattern to use for your environment, check out the article [Good, Better, Best: Untangling The Complex World Of Accessible Patterns](https://www.smashingmagazine.com/2021/03/good-better-best-untangling-complex-world-accessible-patterns/) to help you navigate the tricky waters of accessible patterns. Armed with all of this information and just a little bit of effort, your SVGs are well on their way to being more inclusive to all. 

*Editor’s note*: You can learn **best practices on accessibility** with Carie in her upcoming online workshop on <strong><a href='https://smashingconf.com/online-workshops/workshops/carie-fisher'>Accessible Front-End Patterns</a></strong> — with guidelines, testing tools, assistive technology and inclusive design patterns. Online, and live.

{{< signature "vf, il" >}}
