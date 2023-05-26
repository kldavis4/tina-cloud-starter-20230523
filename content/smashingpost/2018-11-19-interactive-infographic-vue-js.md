---
title: 'Building An Interactive Infographic With Vue.js'
slug: interactive-infographic-vue-js
author: krutie-patel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fb0fb94-82a0-4084-a097-e4e6e1412221/1-feature-image-800w.png
date: 2018-11-19T13:00:30+01:00
summary: >-
  Have you ever had a requirement in which you had to design and build an interactive web experience but the grid system fell short? Furthermore, the design elements turned into unusual shapes that just wouldn’t fit into the regular web layouts? In this article, we’re going to build an interactive infographic using Vue.js, SVG and GreenSock by using dynamic data and unusual layout.
description: >-
  Have you ever had a requirement in which you had to design and build an interactive web experience but the grid system fell short? Furthermore, the design elements turned into unusual shapes that just wouldn’t fit into the regular web layouts? In this article, we’re going to build an interactive infographic using Vue.js, SVG and GreenSock by using dynamic data and unusual layout.
categories:
  - Vue
  - SVG
  - JavaScript
  - Interaction Design
---
<p>This article presents a modern approach to building an interactive infographic. You sure can have plain infographic with all the information available upfront &mdash; without any user interaction. But, thinking of building an interactive experience &mdash; changes the technology landscape we choose. Therefore, let’s understand first, why Vue.js? And you’ll see why GSAP (GreenSock Animation Platform) and SVG (Scalable Vector Graphics) become obvious choices.</p>

<p>Vue.js provides practical ways to build component-based, dynamic user interfaces where you can manipulate and manage DOM elements in powerful ways. In this instance, it’s going to be SVG. You can easily update and manage different SVG elements &mdash; dynamically &mdash; using only a small subset of features available in Vue.js &mdash; some of the staple features that fit the bill here, are, data binding, list rendering, dynamic class binding to name a few. This also allows you to group relevant SVG elements together, and componentize them.</p>

<p>Vue.js plays nice with external libraries without losing its glory, that is GSAP here. There are many other benefits of using Vue.js, one of which is that, Vue.js allows you to isolate related templates, scripts, and styles for each component. This way, Vue.js promotes modular application structure.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/">Replacing jQuery With Vue.js: No Build Step Necessary</a></em></p>

<p>Vue.js also comes packaged with powerful lifecycle hooks that let you tap into the different stages of application to modify application behavior. Setting up and maintaining Vue.js applications doesn’t require a big commitment, meaning you can take phased-approach to scale your project as you go.</p>

<p>The infographic is very light-weight in a visual sense, as the main aim of this article is to learn how to think in terms of data, visual elements, and of course, Vue.js &mdash; the framework that makes all the interactivity possible. In addition, we’ll use GreenSock, a library for animating SVG elements. Before we dive in, <a href="https://tdf-demo.surge.sh/">take a look at the demo</a>.</p>

{{% feature-panel %}}

<p>We’ll start with:

<ol>
<li>The overview of the data for infographic;</li>
<li>SVG image preparation;</li>
<li>An overview of Vue components in context of the SVG artwork;</li>
<li>Code samples and diagrams of key interactivity.</li>
</ol>

<p>The infographic that we’re going to build is about Tour De France, the annual bicycle racing event held in France.
</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d018bd-2319-4fdd-a352-b41599588c67/1-feature-image.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d018bd-2319-4fdd-a352-b41599588c67/1-feature-image.png" sizes="100vw" caption="Tour De France  &mdash;  Interactive bicycle listing game stages (rear-wheel) and participating teams (front-wheel). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d018bd-2319-4fdd-a352-b41599588c67/1-feature-image.png'>Large preview</a>)" alt="Build an interactive infographic with Vue.js, SVG and GreenSock" >}}

## Overview Of Tour De France Data

<p>In infographic design, data drives the design of your infographic. Therefore, while planning your infographic design, it’s always a good idea to have all data, information, and statistics available for the given subject matter.</p>

<p>During Tour De France of 2017, I learned everything about this biggest cycling event that I could in 21 days of the game in July, and I familiarized myself with the subject.</p>

<p>Basic entities of the race that I decided to go for in my design are,</p>

<ul>
<li>Stages,</li>
<li>Teams,</li>
<li>Routes,</li>
<li>Winners,</li>
<li>Length and classifications of each routes.</li>
</ul>

<p>This next part of the process depends on your thinking style, so you can be creative here.</p>

<p>I created two sets of data, one for stages and other for teams. These two datasets have multiple rows of data (but <code>within limit</code>)  &mdash;  which matched with two wheels of the bicycle with multiple spokes in each. And that defined the key element of the design, <code>The Bicycle Art</code> that you saw at the beginning  &mdash;  where each spoke will be interactive & responsible to drive what information is revealed on screen.</p>

<p>I mentioned <code>within limits</code> above, because what we’re aiming for in this instance is not a full-blown data-visualization in context of big data but rather an infographic with high-level data.</p>

{{% ad-panel-leaderboard %}}

<p>Therefore, spend quality time with data and look for similarities, differences, hierarchy or trends that can help you convey a visual story. And don’t forget about the amazing combination of SVG and Vue.js while you’re at it, as it will help you bring about the right balance between information (data), interactivity (Vue.js) and design elements (SVG Artwork) of infographic.</p>

<p>Here’s the snippet of a stage data object:</p>

<div class="break-out">

<pre><code class="language-javascript">{
    "ID": 1,
    "NAME": "STAGE 01",
    "DISTANCE": "14",
    "ROUTE": "KMDÜSSELDORF / DÜSSELDORF",
    "WINNER": "THOMAS G.",</code>
    <code class="language-javascript" style="background-color: #fffbd7">"UCI_CODE": "SKY",</code>
    <code class="language-javascript">"TYPE": "Individual Time Trial",</code>
    <code class="language-javascript">"DATE": "Saturday July 1st",</code>
    <code class="language-javascript">"KEY_MOMENT": " Geraint Thomas takes his first win at 32"</code>
<code class="language-javascript">}</code></pre></div>

<p>And team data object snippet as below:</p>

<pre><code class="language-javascript">{
    "ID": 1,</code>
    <code class="language-javascript" style="background-color: #fffbd7">"UCI_CODE": "SKY",</code>
    <code class="language-javascript">"NAME": " TEAM SKY",</code>
    <code class="language-javascript">"COUNTRY": "Great Britain",</code>
    <code class="language-javascript">"STAGE_VICTORIES": 1,</code>
    <code class="language-javascript">"RIDERS": 8</code>
<code class="language-javascript">}</code></pre>

<p>This infographic is operated by a very simple logic.</p>

<p><strong>UCI_CODE</strong> (<a href="https://en.wikipedia.org/wiki/Union_Cycliste_Internationale">Union Cycliste Internationale</a>) is the connecting key between the stage and the team object. When a stage is clicked, first we’ll activate that stage, but also use <code>UCI_CODE</code> key to activate corresponding winning team.</p>

## SVG Preparation

<p>Having a couple of datasets and a rough concept of bicycle art ready, here’s the static SVG CodePen of the infographic I came up with.</p>

{{< codepen height="480" theme_id="light" slug_hash="QZMVOX" default_tab="result" user="krutie" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/krutie/pen/QZMVOX/">Static Bicycle SVG</a> by Krutie(<a href="https://codepen.io/krutie">@krutie</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<p>We have created only one spoke for each wheel, that is because we’ll dynamically create rest of the spokes using a number of records found in the dataset, and animate them using GreenSock Library.</p>

<p>The workflow to create this SVG code is also very simple. Create your Infographic artwork in Adobe Illustrator and save as SVG. Make sure to name each <code>group</code> and <code>layer</code> while working in Illustrator, because you will need those ids to separate parts of SVG code that will eventually populate <code>&lt;template></code> area of Vue components. Remember that layer names given in Illustrator become <code>element ids</code> in SVG markup.</p>

<p>You can also use <a href="https://jakearchibald.github.io/svgomg/">SVGOMG</a> and further optimize SVG code exported from Adobe Illustrator.</p>

<p><strong>Important Note:</strong> If you use SVGOMG to optimize SVG markup, your code certainly will look neat, but note that it will convert all &lt;rect> elements into &lt;path> with <code>d</code> attribute. This results into losing <code>x</code> and <code>y</code> values of the rectangle, in case you wish to adjust few pixels manually later-on.</p>

<p>Second thing, make sure to uncheck <code>Clean Id</code> option (right-hand side options in SVGOMG interface), this will help maintain all groups and ids intact that were created in Illustrator.</p>

{{% ad-panel-leaderboard %}}

## Vue Component Overview

<p>Even if interactivity and data-flow in your infographic project is quite simple in nature, you should always take a moment to draw up a tree diagram of components.</p>

<p>This will especially help in case you’re not using any shared-data mechanism, where child components are dependent on the values sent from the parent component (i.e. via props) or vice-versa (i.e. this.$emit events). This is your chance to brainstorm these prop values, emit events and local data &mdash; and document them before starting to write the code.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e20506d-a3e6-4a37-8c19-a54f734baefd/2-vue-component-tree-large.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e20506d-a3e6-4a37-8c19-a54f734baefd/2-vue-component-tree-large.jpeg" sizes="100vw" caption="Vue component tree. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e20506d-a3e6-4a37-8c19-a54f734baefd/2-vue-component-tree-large.jpeg'>Large preview</a>)" alt="Vue component tree" >}}

<p>Diagram above is the snapshot of Vue components that is partially derived from interactivity requirements and partially based on SVG markup. You should be able to see how SVG markup will be split up based on this tree structure. It’s pretty self-explanatory from hierarchy view-point.</p>

<ol>
<li>Chain-wheel will imitate rotation of spokes.</li>
<li>Stage component is the rear wheel that will list all 21 stages.</li>
<li>Stage-detail component will display related information on a curved path (left-hand side).</li>
<li>Team component is the front wheel that will list all participating teams on spokes.</li>
<li>Team-detail component will display related information on a curved path (right-hand side).</li>
<li>Navigation will include back and next button to access stages.</li>
</ol>

<p>The diagram below represents the same Vue components seen above, but in the context of the infographic design.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b44397-fe45-477e-a3ae-ce437e7414bf/3-vue-components-blended-into-svg.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b44397-fe45-477e-a3ae-ce437e7414bf/3-vue-components-blended-into-svg.jpeg" sizes="100vw" caption="Vue Components blended into SVG. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b44397-fe45-477e-a3ae-ce437e7414bf/3-vue-components-blended-into-svg.jpeg'>Large preview</a>)" alt="Vue Components blended into SVG" >}}

<p>Less is more &mdash; should be the approach you should try to take while working on similar projects. Think through the animation and transition requirements you have, if you can get away with using TweenLite instead of TweenMax &mdash; do so. If you have the option to choose elementary shapes and simpler paths over complex ones &mdash; by all means try to opt-in for light-weight elements that are easy to animate &mdash; without any performance penalty.</p>

<p>Next section will take you through an exciting part with GreenSock animation and Vue.js.</p>

## GreenSock Animation

<p>Let’s take a closer look at:

<ol>
<li>Text animation on a curved path;</li>
<li>Spoke animation on a wheel.</li>
</ol>

### Animating Text On A Curved Path

<p>Remember the curve path seen around the bicycle wheel, that curved path is slightly bigger than the radius of the bicycle wheel. Therefore, when we animate text on this path, it will look as if it follows the shape of the wheel.</p>

{{< codepen height="480" theme_id="light" slug_hash="zmPzvj" default_tab="result" user="krutie" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/krutie/pen/zmPzvj/">Text on a Curved Path</a> by Krutie (<a href="https://codepen.io/krutie">@krutie</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<p><code>path</code> and <code>textPath</code> is a sweet combination of SVG elements that allows you to set text on any path using <code>xlink:href</code> attribute.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;path id="</code><code class="language-javascript" style="background-color: #fffbd7">curvedPath</code><code class="language-javascript">" stroke="none" fill="none" d="..."/&gt;</code>

<code class="language-javascript">&lt;text&gt; </code>
  <code class="language-javascript">&lt;textPath xlink:href="</code><code class="language-javascript" style="background-color: #fffbd7">#curvedPath</code><code class="language-javascript">"</code>
          <code class="language-javascript">class="stageDetail"</code>
          <code class="language-javascript">startOffset="0%"&gt;</code>
          <code class="language-javascript">{{ stage.KEY_MOMENT }}</code>
   <code class="language-javascript">&lt;/textPath&gt; </code>
<code class="language-javascript">&lt;/text&gt;</code></pre></div>

<p>To animate text along the path, we’ll simply animate its <code>startOffset</code> attribute using GreenSock.</p>

<pre><code class="language-javascript">tl.fromTo( ".stageDetail", 1, 
{
  opacity: 0, </code>
  <code class="language-javascript" style="background-color: #fffbd7">attr: { startOffset: "0%" } </code>
<code class="language-javascript">},</code>
 <code class="language-javascript">{</code> 
  <code class="language-javascript">opacity: 1, </code>
  <code class="language-javascript" style="background-color: #fffbd7">attr: { startOffset: "10%" } </code>
<code class="language-javascript">}, 0.5 );</code>
</code></pre>

<p>As you increase the <code>startOffset</code> percentage, text will travel further through the circle perimeter.
</p>

<p>
In our final project, this animation is triggered every time any spoke is clicked. Now, let’s move on to a more exciting part of the animation.

</p>

### Animating Stages/Spokes Inside The Wheel

<p>It’s visible from the demo that <code>stage</code> and <code>team</code> components are similar in nature with couple of small differences. So, let’s focus on just one wheel of the bicycle.</p>

<p>The CodePen example below zooms in on just the three key ideas:</p>

<ol>
<li>Fetch stage data;</li>
<li>Arrange spokes dynamically based on the data;</li>
<li>Re-arrange spokes when stage (spoke) is clicked.</li>
</ol>

{{< codepen height="480" theme_id="light" slug_hash="xyLmdR" default_tab="result" user="krutie" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/krutie/pen/xyLmdR/">TDF Wheel Animation</a> by Krutie (<a href="https://codepen.io/krutie">@krutie</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<p>You may have noticed in the static SVG CodePen above that the spokes are nothing but SVG rectangles and text grouped together. I have grouped them together since I wanted to pick both text and rectangle for the purpose of animation.</p>

<pre><code class="language-javascript" style="background-color: #fffbd7">&lt;g v-for="stage in stages"</code> <code class="language-javascript">class="stage"&gt;</code>

    <code class="language-javascript">&lt;rect x="249" y="250" width="215" height="1" stroke="#3F51B5" stroke-width="1"/&gt;</code>

    <code class="language-javascript">&lt;text transform="translate(410 245)" fill="#3F51B5" &gt; </code>
      <code class="language-javascript" style="background-color: #fffbd7">{{ stage.NAME }} </code>
    <code class="language-javascript">&lt;/text&gt;</code>

<code class="language-javascript" style="background-color: #fffbd7">&lt;/g&gt;</code></pre>

<p>We will render them in <code>&lt;template></code> area of the Vue component using values fetched from the data-source.</p>

<p>When all 21 stages are available on screen, we’ll set their initial positions by calling, let’s say, <code>setSpokes()</code>.</p>

<pre><code class="language-javascript">// setSpokes()

let stageSpokes = document.querySelectorAll(".stage")
let stageAngle = 360/this.stages.length

_.map(stageSpokes, (item, index) => {
    TweenMax.to(item, 2, 
    { rotation: stageAngle*index, 
      transformOrigin: "0% 100%"
    }, 1)
}
</code></pre>

<p>Three key elements of setting the stage are:</p>

<ol>
<li><strong>Rotation</strong><br />To rotate spokes, we’ll simply map through all elements with className <code>stage</code>, and set dynamic <code>rotation</code> value that is calculated for each spoke.
</li>
<li><strong>Transform Origin</strong><br />Notice <code>transformOrigin</code> value in the code above, which is as important as <code>index</code> value, because “0% 100%” enables each spoke to rotate from the center of the wheel.
</li>
<li><strong>stageAngle</strong><br />This is calculated using total number of stages divided by 360-degree. This will help us lay every spokes evenly in 360-degree circle.</li>
</ol>

### ADDING INTERACTIVITY

<p>Next step would be to add click-event on each stage to make it interactive and reactive to data changes  &mdash;  hence, it will breathe more life into an SVG image!</p>

<p>Let’s say, if stage/spoke is clicked, it executes <code>goAnimate()</code>, which is responsible to activate and rotate the stage being clicked using the <code>stageId</code> parameter.</p>

<pre><code class="language-javascript">goAnimate (stageId) {

  // activate stage id
  this.activeId = stageId

  // rotate spokes

}
</code></pre>

<p>We’ll use <a href="https://greensock.com/docs/Plugins/DirectionalRotationPlugin">DirectionalRotationPlugin</a>…which is a key ingredient for this interactivity. And yes, it is included in TweenMax.</p>

<p>There are three different ways of using this plugin. It animates rotation property in 1) clockwise, 2) counter-clockwise and 3) in the shortest distance calculated to the destination.</p>

<p>As you’d have guessed by now, we’re using the third option to rotate the shortest distance between the current stage and new stage.</p>

<p>Review the CodePen above and you’ll see how <strong>Stage 01</strong> is constantly moving around the circle, leaving its original spot for new active stage at 0-degree angle.</p>

<p>First, we need to find the angle of a stage being clicked, and interchange its rotation with <strong>Stage 01</strong>. So, how do we find the rotation value of the stage being clicked? Check out the diagram below.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4837cf9-0c5c-4868-a13b-6e5a260d7ee1/4-distance-calculation-large.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4837cf9-0c5c-4868-a13b-6e5a260d7ee1/4-distance-calculation-large.jpeg" sizes="100vw" caption="Distance calculation from Stage 01 to the ‘clicked’ stage. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4837cf9-0c5c-4868-a13b-6e5a260d7ee1/4-distance-calculation-large.jpeg'>Large preview</a>)" alt="Distance calculation from Stage 01 to the ‘clicked’ stage" >}}

<p>For example, if <strong>Stage 05</strong> is clicked (as you can see above), the journey from <strong>Stage 01</strong> to <strong>Stage 05</strong>  &mdash;  requires 4 x angle-value.</p>

<p>And therefore, we can get the correct angle using, <code>(Active stage Id - 1) * 17 degree,</code> followed by ‘_short’ string postfix to trigger directional rotation plugin.</p>

<pre><code class="language-javascript">angle = 360/21 stages = 17
activeId = 5</code>
<code class="language-javascript">new angle = (</code><code class="language-javascript" style="background-color: #fffbd7">(activeId-1)</code><code class="language-javascript">*angle)+'_short'</code>
          <code class="language-javascript">= ((5-1)\*17)+'_short'</code>
          <code class="language-javascript">= 68</code></pre>

<p>The final <code>goAnimate()</code> function will look something like below:</p>

<pre><code class="language-javascript">_.map(spokes, (item, index) => {

  if(activeId == index+1) { 
    // active stage
    TweenMax.to(item, 2, 
    { rotation: 0+'_short', 
      transformOrigin: "0 100%"
    })   

  } else if (index == 0) { 
    // first stage
    TweenMax.to(item, 2,</code>
    <code class="language-javascript" style="background-color: #fffbd7">{ rotation: (activeId*angle)-angle+'_short',</code>
      <code class="language-javascript">transformOrigin: "0 100%"</code>
    <code class="language-javascript">})</code>

  <code class="language-javascript">} else {</code>
    <code class="language-javascript">TweenMax.to(item, 2,</code> 
    <code class="language-javascript">{ rotation: index*angle+'_short',</code> 
      <code class="language-javascript">transformOrigin: "0 100%"</code>
    <code class="language-javascript">})</code>
  <code class="language-javascript">}</code>

<code class="language-javascript">}) // end of map</code></pre>

<p>Once we have the rear wheel ready, the front wheel (for team) should follow the same logic with a couple of tweaks.</p>

<p>Instead of stage, we’ll fetch team data and update registration point of <code>transformOrigin</code> attribute to enable spokes generation from opposite registration point than the stage wheel.</p>

<pre><code class="language-javascript">// set team spokes

map(teamSpokes, (index, key) => {
  TweenMax.to(index, 2, 
  { rotation: angle*key, 
    <code class="language-javascript" style="background-color: #fffbd7">transformOrigin: "100% 100%"</code>
  <code class="language-javascript">}, 1)</code>
<code class="language-javascript">})</code>
</code></pre>

## Final Project

<p>Like me, if you have written all animation and data related functions in Vue components itself. It’s time to clean them up using Vuex and Mixins.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e298de5-57fa-4248-988b-387dbb99e1a7/5-vuex-with-vue-components.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e298de5-57fa-4248-988b-387dbb99e1a7/5-vuex-with-vue-components.jpeg" sizes="100vw" caption="Using Vuex state management to power both wheels with data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e298de5-57fa-4248-988b-387dbb99e1a7/5-vuex-with-vue-components.jpeg'>Large preview</a>)" alt="Using Vuex state management to power both wheels with data" >}}

### VUEX

<p>Vuex eases up the management of shared data among components, and more importantly, it streamlines your code, keeping <code>methods</code> and <code>data()</code> clean and tidy, leaving components only to render the data, not to handle it.</p>

<p>Lifecycle hooks are a very suitable place to perform any HTTP requests. We fetch initial data in <code>created</code> hook, when the Vue application has initialized, but hasn’t yet mounted into the DOM.</p>

<p>Empty state variables, <code>stages</code> and <code>teams</code> are updated using mutations at this stage. We then, use watcher (only once) to keep track of these two variables, and soon as they’re updated, we call in animation script (from <code>mixin.js</code>).</p>

<p>Every time user interacts with stage or team component, it will communicate with Vuex store, executes <code>setActiveData</code>, and updates current stage and current team values. That is how we set active data.</p>

<p>And when the active data is set after state update, <code>goAnimate</code> will kick in to animate (directional rotate) spokes using updated values.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2017/08/creating-custom-inputs-vue-js/">Creating Custom Inputs With Vue.js</a></em></p>

### Mixins

<p>Now that the data is handled by Vuex, we’ll separate out GreenSock animations. This will prevent our Vue components being cluttered with long animation scripts. All GreenSock functions are grouped together in <code>mixin.js</code> file.</p>

<p>Since you have access to Vuex Store within Mixins, all GSAP functions use <code>state</code> variables to animate SVG elements. You can see fully functional <code>store.js</code> and <code>mixin.js</code> in the <a href="https://codesandbox.io/embed/y2kx79mnrv">CodeSandbox example over here</a>.</p>

## Conclusion

<p>Creating interactive and engaging infographics requires you to be analytical with the data, creative with visuals and efficient with the technology you use, which in this case is Vue.js. You can further use these concepts in your project. As a closing note, I’ll leave you with this circular interactive color wheel below that uses an idea similar to the one we’ve discussed in this article.</p>

{{< codepen height="480" theme_id="light" slug_hash="LjWRqZ" default_tab="result" user="krutie" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/krutie/pen/LjWRqZ/">Material UI Circular Colour Palette made with Vue JS and GSAP</a> by Krutie (<a href="https://codepen.io/krutie">@krutie</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<p>With no doubt, Vue.js has many great features; we’re able to create interactive infographics with just a few things, such as watchers, computed properties, mixins, directive (see color-wheel example) and a few other methods. Vue.js is the glue that holds both SVG and GreenSock animation together efficiently, giving you ample of opportunity to be creative with any number of subject matter and custom interactivity at the same time.</p>

{{< signature "rb, ra, yk, il" >}}
