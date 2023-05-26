---
title: 'Generic First CSS: New Thinking On Mobile First'
slug: generic-css-mobile-first
author: alastair-hodgson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2907cf63-61a5-4916-8041-365f072f9d7b/console-css-inspector-800w.png
date: 2018-12-21T11:45:16+01:00
summary: >-
  With the advent of responsive web design and the mobile-first approach, it’s been seven wonderful years since any new concepts have compelled us to adapt the way in which we write CSS at the base level. Well, I don’t have anything too groundbreaking to offer you, but I do have a small surprise. Behold: Generic First CSS.
description: >-
  With the advent of responsive web design and the mobile-first approach, it’s been seven wonderful years since any new concepts have compelled us to adapt the way in which we write CSS at the base level. Well, I don’t have anything too groundbreaking to offer you, but I do have a small surprise. Behold: Generic First CSS.
categories:
  - CSS
  - Responsive Design
---

<p>I think it’s safe to say that Ethan Marcotte’s <a href="https://alistapart.com/article/responsive-web-design">Responsive Web Design</a> was a welcome revelation for web developers the world over. It triggered a whole new wave of design thinking and wonderful new front-end techniques. The reign of the oft-despised m dot websites was also over. In the same era and almost as influential was Luke Wroblewski’s <a href="https://www.lukew.com/ff/entry.asp?933">Mobile First</a> methodology &mdash; a solid improvement that built upon Marcotte’s impressive foundations.</p>

<p>These techniques are at the bedrock of most web developers lives, and they’ve served us well, but alas, times change, and developers constantly iterate. As we increase the efficiency of our methods and the project requirements become more complex, new frustrations emerge.</p>

## The Journey To Generic First

<p>I can’t pinpoint exactly what made me change the way I write my CSS because it was really a natural progression for me that happened almost subconsciously. Looking back, I think it was more of a by-product of the development environment I was working in. The team I worked with had a nice SCSS workflow going on with a nifty little mixin for easily adding breakpoints within our CSS declarations. You probably use a similar technique.</p>

<p>This wonderful little SCSS mixin suddenly made it easy to write super granular media queries. Take a hypothetical biography block that looks a little something like this:</p>

<pre><code class="language-css">.bio {
  display: block;
  width: 100%;
  background-color: #ece9e9;
  padding: 20px;
  margin: 20px 0;

  @include media('>=small') {
    max-width: 400px;
    background-color: white;
    margin: 20px auto;
  }

  @include media('>=medium') {
    max-width: 600px;
    padding: 30px;
    margin: 30px auto;
  }

  @include media('>=large') {
    max-width: 800px;
    padding: 40px;
    margin: 40px auto;
  }

  @include media('>=huge') {
    max-width: 1000px;
    padding: 50px;
    margin: 50px auto;
  }
}
</code></pre>

<p><strong>Fig.1.</strong> <em>Typical mobile first with cascading media queries</em></p>

<p>This works nicely &mdash; I’ve written <em>a lot</em> of CSS like this in the past. However, one day it dawned upon me that overwriting CSS declarations as the device width increased just didn’t make sense. Why declare a CSS property for it only to be overwritten in the following declaration?</p>

{{% feature-panel %}}

<p>This is what lead me to begin writing <em> compartmentalized media queries</em> as opposed to the more common approach of media queries that cascade upwards (or downwards) like the example in Fig.1.</p>

<p>Instead of writing media queries that cascade upwards with increases in screen size, I began creating targeted media queries that would encapsulate styles at desired screen widths. The <a href="https://include-media.com/">media query mixin</a> would really come into its own here. Now my SCSS media queries are starting to look like this:</p>

<pre><code class="language-css">.bio {
  display: block;
  width: 100%;
  padding: 20px;
  margin: 20px 0;

  @include media('>=small', '<span><</span>medium') {
    max-width: 400px;
    margin: 20px auto;
  }

  @include media('>=medium', '<span><</span>large') {
    max-width: 600px;
    padding: 30px;
    margin: 30px auto;
  }

  @include media('>=large', '<span><</span>huge') {
    max-width: 800px;
    padding: 40px;
    margin: 40px auto;
  }

  @include media('>=huge') {
    max-width: 1000px;
    padding: 50px;
    margin: 50px auto;
  }
}
</code></pre>

<p><strong>Fig.2.</strong> <em>An example of compartmentalized media queries</em></p>

<p>This new approach just felt more intuitive to me, it cut down on having to reset styles from the previous breakpoint, and it was making the CSS easier to read. More importantly, it was making the media queries self-documenting in a more significant way.</p>

<p>I still wasn’t 100% happy with the above though, It seemed like there was still a major issue to overcome.</p>

## The Problem With Mobile First

<p>The issue with mobile first is that by definition you will most likely have to override mobile-first styles in subsequent media-queries. This feels like a bit of an anti-pattern.</p>

<p>So &mdash; to me &mdash; the answer was obvious: let’s take the idea of media query compartmentalization to its logical conclusion &mdash; we will also compartmentalize the mobile specific styles into their very own media queries. I know, I know, this goes against the common convention we’ve learned over the years. “Mobile First” is so ubiquitous that it’s usually one of the “skills” questions a hiring manager will ask. So surely any alternative must be wrong, shouldn’t it? This is usually the part where people shake their heads at me whilst uttering <em>mobile first</em> over and over.</p>

<p>Okay, so we’re going to break through the mobile first dogma and compartmentalize all our styles into the relevant media queries. What we’re now left with is pure generic styles declared on a CSS selector, with all other device specific styles encapsulated in media queries that only apply to the relevant screen dimensions. We now have <em>Generic First CSS</em>:</p>

<pre><code class="language-css">.bio {
  display: block;
  width: 100%;

  @include media('>=0', '<span><</span>small') {
    padding: 20px;
    margin: 20px 0;
  }

  @include media('>=small', '<span><</span>medium') {
    max-width: 400px;
    margin: 20px auto;
  }

  @include media('>=medium', '<span><</span>large') {
    max-width: 600px;
    padding: 30px;
    margin: 30px auto;
  }

  @include media('>=large', '<span><</span>huge') {
    max-width: 800px;
    padding: 40px;
    margin: 40px auto;
  }

  @include media('>=huge') {
    max-width: 1000px;
    padding: 50px;
    margin: 50px auto;
  }
}
</code></pre>

<p><strong>Fig.3.</strong> <em>An example of Generic First CSS</em></p>

<p>Yes, there are slightly more media queries, however, I see this as a benefit, any developer can now looks at this CSS and see exactly what styles are applied at each and every screen size without the cognitive overhead of having to pick apart media-query specificity.</p>

<p>This can be great for people unfamiliar with the code base or even the future you!</p>

### When Not To Compartmentalize

<p>There are still times when media query compartmentalization is a burden, and in some cases a good old >= media query is fine. Remember, all we’re trying to do is avoid property overwrites.</p>

{{% ad-panel-leaderboard %}}

## Dev Tool Bliss

<p>One major unintended consequence of writing compartmentalized Generic First CSS is the experience you will get from your developer tools style panel. Without the media query cascade, you will now have a clearer overview of which styles are applied &mdash; You won’t have a style panel full of struck-out declarations from overwritten media query rules &mdash; <strong>The noise is gone!</strong> This &mdash; for me &mdash; is one of the biggest benefits of the Generic First CSS technique. It brings a little extra sanity to the CSS debugging experience, and this is worth its weight in gold. Thank me later.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b90c5aa-5d8e-4d75-b005-1c3430521962/console-css-inspector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b90c5aa-5d8e-4d75-b005-1c3430521962/console-css-inspector.png" sizes="100vw" caption="<strong>Fig.4.</strong> How generic first, compartmentalized css can help bring joy and sanity to your dev console. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b90c5aa-5d8e-4d75-b005-1c3430521962/console-css-inspector.png'>Large preview</a>)" alt="Before and after screenshot of how the generic first CSS approach affects chrome dev tools style panel." >}}

## Performance Implications

<p>So all these Generic First CSS benefits are starting to sound pretty good, but I think there is one last key question that I think needs to be addressed. It’s on the subject of performance optimization. Now I don’t know for certain yet, but I have an inkling that fully compartmentalized media queries may have a slight performance benefit.</p>

<p>Browsers perform a rendering task called <em>computed style calculation</em>. It’s the browsers way of calculating which styles need to be applied to an element at any given moment. This task is always performed on initial page load, but it can also be performed if page content changes or if other browser actions take place. Any boost you can give to the speed of the process is going to be great for initial page load, and it could have a compound effect on the lifecycle of your websites pages.</p>

<p>So going back to generic first CSS: Are there any performance issues related to the browser having to work out the CSS specificity of a multitude of cascading media queries?</p>

<p>To answer that, I’ve devised a test case that can be used to measure any speed benefits or indeed drawbacks.</p>

### The Test Case

<p>The test case is comprised of a basic HTML page that outputs a “bio” block 5000 times, the markup is the same for each block, but the classes are slightly different (numeric differentiator), the CSS for this block is also outputted 5000 times, with class names being the only thing to differ. The outputted CSS is piped through a tool called <a href="https://github.com/hail2u/node-css-mqpacker">CSS MQPacker</a>, this helps dramatically reduce file size of CSS that uses a lot of inline media queries by combining all the separate instances of a specific media query into one &mdash; It’s a great tool that will probably benefit most modern CSS codebases &mdash; I’ve used it as a standalone cli tool via a npm task in the test projects package.json, you can also use it as a postcss plugin, which is nice and convenient!</p>

<p>The first test case is a mobile-first cascading media queries example, the second test case is a generic first compartmentalized variant of the CSS. The CSS for these cases is a little verbose and could probably be written in much more concise terms, but it really just serves as a rough example to test the argument.</p>

<p>The test was run 20 times for each CSS variation in desktop Google Chrome v70, not a massive set of data, but enough to give me a rough idea of a performance gain/loss.</p>

{{% ad-panel-leaderboard %}}

<p>The test metrics I have chosen to use are:</p>

<ul>
<li><strong>Overall page load time</strong><br />A basic metric to check page load time using the Performance API markers in the the start of the &lt;head&gt; and very end of &lt;body&gt;</li>
<li><strong>The Recalculate Style</strong><br />Time from within the dev tools performance pane.</li>
<li><strong>The Overall Page Rendering</strong><br />Time from within the dev tools performance pane.</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a1c456-6859-491b-92c2-e8829cb04070/console-perf-inspector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a1c456-6859-491b-92c2-e8829cb04070/console-perf-inspector.png" sizes="100vw" caption="<strong>Fig.5.</strong> The key metric being measured is “Recalculate Style”. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a1c456-6859-491b-92c2-e8829cb04070/console-perf-inspector.png'>Large preview</a>)" alt="Table of results from the Google Chrome performance profiler" >}}

<p><strong>Results Table (all times in milliseconds)</strong></p>

<div class="scroll-pane">
<table class="break-out">
  <thead>
    <tr>
      <th></th>
      <th>Mobile First</th>
      <th></th>
      <th></th>
      <th></th>
      <th>Generic First</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td></td>
      <td>Load time</td>
      <td>Calculate styles</td>
      <td>Total render time</td>
      <td></td>
      <td>Load time</td>
      <td>Calculate styles</td>
      <td>Total render time</td>
    </tr>
    <tr>
      <td></td>
      <td>1135</td>
      <td>565.7</td>
      <td>1953</td>
      <td></td>
      <td>1196</td>
      <td>536.9</td>
      <td>2012</td>
    </tr>
    <tr>
      <td></td>
      <td>1176</td>
      <td>563.5</td>
      <td>1936</td>
      <td></td>
      <td>1116</td>
      <td>506.9</td>
      <td>1929</td>
    </tr>
    <tr>
      <td></td>
      <td>1118</td>
      <td>563.1</td>
      <td>1863</td>
      <td></td>
      <td>1148</td>
      <td>514.4</td>
      <td>1853</td>
    </tr>
    <tr>
      <td></td>
      <td>1174</td>
      <td>568.3</td>
      <td>1929</td>
      <td></td>
      <td>1124</td>
      <td>507.1</td>
      <td>1868</td>
    </tr>
    <tr>
      <td></td>
      <td>1204</td>
      <td>577.2</td>
      <td>1924</td>
      <td></td>
      <td>1115</td>
      <td>518.4</td>
      <td>1854</td>
    </tr>
    <tr>
      <td></td>
      <td>1155</td>
      <td>554.7</td>
      <td>1991</td>
      <td></td>
      <td>1177</td>
      <td>540.8</td>
      <td>1905</td>
    </tr>
    <tr>
      <td></td>
      <td>1112</td>
      <td>554.5</td>
      <td>1912</td>
      <td></td>
      <td>1111</td>
      <td>504.3</td>
      <td>1886</td>
    </tr>
    <tr>
      <td></td>
      <td>1110</td>
      <td>557.9</td>
      <td>1854</td>
      <td></td>
      <td>1104</td>
      <td>505.3</td>
      <td>1954</td>
    </tr>
    <tr>
      <td></td>
      <td>1106</td>
      <td>544.5</td>
      <td>1895</td>
      <td></td>
      <td>1148</td>
      <td>525.4</td>
      <td>1881</td>
    </tr>
    <tr>
      <td></td>
      <td>1162</td>
      <td>559.8</td>
      <td>1920</td>
      <td></td>
      <td>1095</td>
      <td>508.9</td>
      <td>1941</td>
    </tr>
    <tr>
      <td></td>
      <td>1146</td>
      <td>545.9</td>
      <td>1897</td>
      <td></td>
      <td>1115</td>
      <td>504.4</td>
      <td>1968</td>
    </tr>
    <tr>
      <td></td>
      <td>1168</td>
      <td>566.3</td>
      <td>1882</td>
      <td></td>
      <td>1112</td>
      <td>519.8</td>
      <td>1861</td>
    </tr>
    <tr>
      <td></td>
      <td>1105</td>
      <td>542.7</td>
      <td>1978</td>
      <td></td>
      <td>1121</td>
      <td>515.7</td>
      <td>1905</td>
    </tr>
    <tr>
      <td></td>
      <td>1123</td>
      <td>566.6</td>
      <td>1970</td>
      <td></td>
      <td>1090</td>
      <td>510.7</td>
      <td>1820</td>
    </tr>
    <tr>
      <td></td>
      <td>1106</td>
      <td>514.5</td>
      <td>1956</td>
      <td></td>
      <td>1127</td>
      <td>515.2</td>
      <td>1986</td>
    </tr>
    <tr>
      <td></td>
      <td>1135</td>
      <td>575.7</td>
      <td>1869</td>
      <td></td>
      <td>1130</td>
      <td>504.2</td>
      <td>1882</td>
    </tr>
    <tr>
      <td></td>
      <td>1164</td>
      <td>545.6</td>
      <td>2450</td>
      <td></td>
      <td>1169</td>
      <td>525.6</td>
      <td>1934</td>
    </tr>
    <tr>
      <td></td>
      <td>1144</td>
      <td>565</td>
      <td>1894</td>
      <td></td>
      <td>1092</td>
      <td>516</td>
      <td>1822</td>
    </tr>
    <tr>
      <td></td>
      <td>1115</td>
      <td>554.5</td>
      <td>1955</td>
      <td></td>
      <td>1091</td>
      <td>508.9</td>
      <td>1986</td>
    </tr>
    <tr>
      <td></td>
      <td>1133</td>
      <td>554.8</td>
      <td>2572</td>
      <td></td>
      <td>1001</td>
      <td>504.5</td>
      <td>1812</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td><strong>AVG</strong></td>
      <td><strong>1139.55</strong></td>
      <td><strong>557.04</strong></td>
      <td><strong>1980</strong></td>
      <td></td>
      <td><strong>1119.1</strong></td>
      <td><strong>514.67</strong></td>
      <td><strong>1903.15</strong></td>
      </tr>
    </tbody>
  </table>
</tbody>
</div>

<p class="pfix"><strong>Fig.6.</strong> <em>20 test runs measuring key load/render metrics of mobile first vs generic first CSS.</em></p>

<p>From my admittedly small dataset, it does seem like my initial suspicion may be correct. On average, I see the Style Recalculation task take 42ms less time which is a 7.6% speed increase, and therefore the overall rendering time also decreases. The difference isn’t mind-blowing, but it is an improvement. I don’t think the dataset is big enough to be 100% conclusive and the test case is a little unrealistic, but I’m very glad not to be seeing a performance degradation.</p>

<p>I would be very interested to see the generic first methodology applied to a real-world existing codebase that has been written in the mobile-first way &mdash; the before after metrics would be much more realistic to everyday practice.</p>

<p>And if anyone has suggestions on how to automate this test over a broader set of iterations, please let me know in the comments! I’d imagine there must be a tool that can do this.</p>

## Conclusion

<p>To recap on the benefits of this new development methodology...</p>

<ul>
<li>CSS that does exactly as intended, no second guessing;</li>
<li>Self-documenting media-queries;</li>
<li>A better dev tools experience;</li>
<li>Pages that render faster.</li>
</ul>

<p>I’d like to think I’m not the only person espousing the writing of CSS in this style. If you have already adopted the generic first mindset, hurray! But if not, I think you’ll really like the benefits it brings. I’ve personally benefited greatly from the uncluttered dev tools experience, which in itself will be a huge positive to a lot of devs. the self-documenting nature of this way of writing your media-queries will also have benefits to yourself and the wider team (if you have one). And finally, these benefits won’t cost you anything in performance terms, and in fact have been shown to have marginal speed gains!</p>

#### Final Word

<p>Like all development methodologies, it may not be for everyone, but I’ve fallen into Generic First CSS quite naturally, I now see it as a valuable way of working that gives me all the benefits of mobile first with some positive new additions that make the tough job of front-end development that little be easier.</p>

## Resources

#### Test Case Repo

<p>If you’d like to fire up the test case and give it a go yourself, you can <a href="https://github.com/stikoo/generic-first-css-perf">find it on GitHub</a>, I’d love to see some reports from others.</p>

#### Tools

<ul>
<li><a href="https://www.npmjs.com/package/css-mqpacker">CSS MQPacker</a></li>
<li><a href="https://github.com/eduardoboucas/include-media">Include Media</a></li>
</ul>

{{< signature "dm, ra, yk, il" >}}
