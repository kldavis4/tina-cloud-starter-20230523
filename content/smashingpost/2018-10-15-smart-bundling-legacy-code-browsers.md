---
title: 'Smart Bundling: How To Serve Legacy Code Only To Legacy Browsers'
slug: smart-bundling-legacy-code-browsers
author: shubham-kanodia
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d37f1046-f2cb-41d0-847d-599b4f3d8025/01-shipping-a-modern-frontend-800w.png
date: 2018-10-15T14:30:13+02:00
summary: >-
  While effective bundling of resources on the web has received a great deal of mindshare in recent times, how we ship front-end resources to our users has remained pretty much the same. The average weight of JavaScript and style resources that a website ships with is rising &mdash; even though build tooling to optimize the website has never been better. With the marketshare of evergreen browsers rising fast and browsers launching support for new features in lockstep, is it time we rethink asset delivery for the modern web?
description: >-
  With the marketshare of evergreen browsers rising fast and browsers launching support for new features in lockstep, is it time we rethink asset delivery for the modern web?
categories:
  - Browsers
  - Performance
  - JavaScript
  - Tools
---
A website today receives a large chunk of its traffic from evergreen browsers &mdash; most of which have good support for ES6+, new JavaScript standards, new web platform APIs and CSS attributes. However, legacy browsers still need to be supported for the near future &mdash; their usage share is large enough not to be ignored, depending on your user base.

A quick look at [caniuse.com](https://caniuse.com/usage-table)’s usage table reveals that evergreen browsers occupy a lion’s share of the browser market &mdash; more than 75%. In spite of this, the norm is to prefix CSS, transpile all of our JavaScript to ES5, and include polyfills to support every user we care about.

While this is understandable from a historical context &mdash; the web has always been about progressive enhancement &mdash; the question remains: Are we slowing down the web for the majority of our users in order to support a diminishing set of legacy browsers?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cd8cff3-2517-4109-9bf4-cae93f62bb9b/01-shipping-a-modern-frontend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cd8cff3-2517-4109-9bf4-cae93f62bb9b/01-shipping-a-modern-frontend.png" sizes="100vw" caption="The different compatibility layers of a web app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cd8cff3-2517-4109-9bf4-cae93f62bb9b/01-shipping-a-modern-frontend.png'>View large version</a>)" alt="Transpilation to ES5, web platform polyfills, ES6+ polyfills, CSS prefixing" >}}

## The Cost Of Supporting Legacy Browsers

Let’s try to understand how different steps in a typical build pipeline can add weight to our front-end resources:

### Transpiling To ES5

To estimate how much weight transpiling can add to a JavaScript bundle, I took a few popular JavaScript libraries originally written in ES6+ and compared their bundle sizes before and after transpilation:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
<tr>
<th data-tablesaw-priority="persist">Library</th>
<th>Size<br />(minified ES6)</th>
<th>Size<br />(minified ES5)</th>
<th>Difference</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>TodoMVC</strong></td>
<td>8.4 KB</td>
<td>11 KB</td>
<td>24.5%</td>
</tr>
<tr>
<td><strong>Draggable</strong></td>
<td>53.5 KB</td>
<td>77.9 KB</td>
<td>31.3%</td>
</tr>
<tr>
<td><strong>Luxon</strong></td>
<td>75.4 KB</td>
<td>100.3 KB</td>
<td>24.8%</td>
</tr>
<tr>
<td><strong>Video.js</strong></td>
<td>237.2 KB</td>
<td>335.8 KB</td>
<td>29.4%</td>
</tr>
<tr>
<td><strong>PixiJS</strong></td>
<td>370.8 KB</td>
<td>452 KB</td>
<td>18%</td>
</tr>
</tbody>
</table>

On average, untranspiled bundles are about 25% smaller than those that have been transpiled down to ES5. This isn’t surprising given that ES6+ provides a more compact and expressive way to represent the equivalent logic and that transpilation of some of these features to ES5 can require a lot of code.

### ES6+ Polyfills

While Babel does a good job of applying syntactical transforms to our ES6+ code,  built-in features introduced in ES6+ &mdash; such as `Promise`, `Map` and `Set`, and new array and string methods &mdash; still need to be polyfilled. Dropping in `babel-polyfill` as is can add close to 90 KB to your minified bundle.

{{% feature-panel %}}

### Web Platform Polyfills

Modern web application development has been simplified due to the availability of a plethora of new browser APIs. Commonly used ones are `fetch`, for requesting for resources, `IntersectionObserver`, for efficiently observing the visibility of elements, and the `URL` specification, which makes reading and manipulation of URLs on the web easier.

Adding a spec-compliant polyfill for each of these features can have a noticeable impact on bundle size.

### CSS Prefixing

Lastly, let’s look at the impact of CSS prefixing. While prefixes aren’t going to add as much dead weight to bundles as other build transforms do &mdash; especially because they compress well when Gzip’d &mdash; there are still some savings to be achieved here.  

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Library</th>
<th>Size<br />(minified, prefixed for last 5 browser versions)</th>
<th>Size<br />(minified, prefixed for last browser version)</th>
<th>Difference</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Bootstrap</strong></td>
<td>159 KB</td>
<td>132 KB</td>
<td>17%</td>
</tr>
<tr>
<td><strong>Bulma</strong></td>
<td>184 KB</td>
<td>164 KB</td>
<td>10.9%</td>
</tr>
<tr>
<td><strong>Foundation</strong></td>
<td>139 KB</td>
<td>118 KB</td>
<td>15.1%</td>
</tr>
<tr>
<td><strong>Semantic UI</strong></td>
<td>622 KB</td>
<td>569 KB</td>
<td>8.5%</td>
</tr>
</tbody>
</table>

## A Practical Guide To Shipping Efficient Code

It’s probably evident where I’m going with this. If we leverage existing build pipelines to ship these compatibility layers only to browsers that require it, we can deliver a lighter experience to the rest of our users &mdash; those who form a rising majority &mdash; while maintaining compatibility for older browsers.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ab53df-3320-4556-bf20-440530dec8a1/modern-vs-legacy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ab53df-3320-4556-bf20-440530dec8a1/modern-vs-legacy.png" sizes="100vw" caption="Forking our bundles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ab53df-3320-4556-bf20-440530dec8a1/modern-vs-legacy.png'>View large version</a>)" alt="The modern bundle is smaller than the legacy bundle because it forgoes some compatibility layers." >}}

This idea isn’t entirely new. Services such as [Polyfill.io](https://github.com/Financial-Times/polyfill-service) are attempts to dynamically polyfill browser environments at runtime. But approaches such as this suffer from a few shortcomings:

- The selection of polyfills is limited to those listed by the service &mdash; unless you host and maintain the service yourself.
- Because the polyfilling happens at runtime and is a blocking operation, page-loading time can be significantly higher for users on old browsers.
- Serving a custom-made polyfill file to every user introduces entropy to the system, which makes troubleshooting harder when things go wrong.

Also, this doesn’t solve the problem of weight added by transpilation of the application code, which at times can be larger than the polyfills themselves.

Let see how we can solve for all of the sources of bloat we’ve identified till now.

{{% ad-panel-leaderboard %}}

## Tools We'll Need

- **Webpack**  
This will be our build tool, although the process will remain similar to that of other build tools, like Parcel and Rollup.
- **Browserslist**  
With this, we’ll manage and define the browsers we'd like to support.
- And we’ll use some **Browserslist support plugins**.

## 1. Defining Modern And Legacy Browsers

First, we’ll want to make clear what we mean by “modern” and “legacy” browsers. For ease of maintenance and testing, it helps to divide browsers into two discrete groups: adding browsers that require little to no polyfilling or transpilation to our modern list, and putting the rest on our legacy list.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97c66848-0e54-4756-ba67-b6fcdee3ef26/modern-browsers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97c66848-0e54-4756-ba67-b6fcdee3ef26/modern-browsers.png" sizes="100vw" caption="Browsers that support ES6+, new CSS attributes, and browser APIs like Promises and Fetch. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97c66848-0e54-4756-ba67-b6fcdee3ef26/modern-browsers.png'>View large version</a>)" alt="Firefox >= 53; Edge >= 15; Chrome >= 58; iOS >= 10.1" >}}

A Browserslist configuration at the root of your project can store this information. “Environment” subsections can be used to document the two browser groups, like so:

<pre><code class="language-javascript">[modern]
Firefox >= 53
Edge >= 15
Chrome >= 58
iOS >= 10.1

[legacy]
> 1%
</code></pre>

The list given here is only an example and can be customized and updated based on your website’s requirements and the time available. This configuration will act as the source of truth for the two sets of front-end bundles that we will create next: one for the modern browsers and one for all other users.

## 2. ES6+ Transpiling And Polyfilling

To transpile our JavaScript in an environment-aware manner, we’re going to use `babel-preset-env`.

Let's initialize a `.babelrc` file at our project’s root with this:

<pre><code class="language-javascript">{
  "presets": [
    ["env", { "useBuiltIns": "entry"}]
  ]
}
</code></pre>

Enabling the `useBuiltIns` flag allows Babel to selectively polyfill built-in features that were introduced as part of ES6+. Because it filters polyfills to include only the ones required by the environment, we mitigate the cost of shipping with `babel-polyfill` in its entirety.

For this flag to work, we will also need to import `babel-polyfill` in our entry point.

<pre><code class="language-css">// In
import "babel-polyfill";
</code></pre>

Doing so will replace the large `babel-polyfill` import with granular imports, filtered by the browser environment that we’re targeting.

<pre><code class="language-javascript">// Transformed output
import "core-js/modules/es7.string.pad-start";
import "core-js/modules/es7.string.pad-end";
import "core-js/modules/web.timers";
…
</code></pre>

## 3. Polyfilling Web Platform Features

To ship polyfills for web platform features to our users, we will need to create two entry points for both environments:

<pre><code class="language-javascript">require('whatwg-fetch');
require('es6-promise').polyfill();
// … other polyfills
</code></pre>  

And this:

<pre><code class="language-javascript">// polyfills for modern browsers (if any)
require('intersection-observer');
</code></pre>

This is the only step in our flow that requires some degree of manual maintenance. We can make this process less error-prone by adding [eslint-plugin-compat](https://github.com/amilajack/eslint-plugin-compat) to the project. This plugin warns us when we use a browser feature that hasn’t been polyfilled yet.

{{% ad-panel-leaderboard %}}

## 4. CSS Prefixing

Finally, let’s see how we can cut down on CSS prefixes for browsers that don’t require it. Because `autoprefixer` was one of the first tools in the ecosystem to support reading from a `browserslist` configuration file, we don’t have much to do here.

Creating a simple PostCSS configuration file at the project’s root should suffice:

<pre><code class="language-javascript">module.exports = {
  plugins: [ require('autoprefixer') ],
}
</code></pre>

## Putting It All Together

Now that we’ve defined all of the required plugin configurations, we can put together a webpack configuration that reads these and outputs two separate builds in `dist/modern` and `dist/legacy` folders.

<div class="break-out">

<pre><code class="language-javascript">const MiniCssExtractPlugin = require('mini-css-extract-plugin')
const isModern = process.env.BROWSERSLIST_ENV === 'modern'
const buildRoot = path.resolve(__dirname, "dist")

module.exports = {
  entry: [
    isModern ? './polyfills.modern.js' : './polyfills.legacy.js',
    "./main.js"
  ],
  output: {
    path: path.join(buildRoot, isModern ? 'modern' : 'legacy'),
    filename: 'bundle.[hash].js',
  },
  module: {
    rules: [
      { test: /\.jsx?$/, use: "babel-loader" },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader', 'postcss-loader']
      }
    ]},
    plugins: {
      new MiniCssExtractPlugin(),
      new HtmlWebpackPlugin({
      template: 'index.hbs',
      filename: 'index.html',
    }),
  },
};
</code></pre></div>

To finish up, we’ll create a few build commands in our `package.json` file:

<div class="break-out">

<pre><code class="language-javascript">"scripts": {
  "build": "yarn build:legacy && yarn build:modern",
  "build:legacy": "BROWSERSLIST_ENV=legacy webpack -p --config webpack.config.js",
  "build:modern": "BROWSERSLIST_ENV=modern webpack -p --config webpack.config.js"
}
</code></pre></div>

That’s it. Running `yarn build` should now give us two builds, which are equivalent in functionality.

## Serving The Right Bundle To Users

Creating separate builds helps us achieve only the first half of our goal. We still need to identify and serve the right bundle to users.

Remember the Browserslist configuration we defined earlier? Wouldn’t it be nice if we could use the same configuration to determine which category the user falls into?

Enter [browserslist-useragent](https://github.com/browserslist/browserslist-useragent). As the name suggests, `browserslist-useragent` can read our `browserslist` configuration and then match a user agent to the relevant environment. The following example demonstrates this with a Koa server:

<div class="break-out">

<pre><code class="language-javascript">const Koa = require('koa')
const app = new Koa()
const send = require('koa-send')
const { matchesUA } = require('browserslist-useragent')
var router = new Router()

app.use(router.routes())

router.get('/', async (ctx, next) => {
  const useragent = ctx.get('User-Agent')  
  const isModernUser = matchesUA(useragent, {
      env: 'modern',
      allowHigherVersions: true,
   })
   const index = isModernUser ? 'dist/modern/index.html', 'dist/legacy/index.html'
   await send(ctx, index);
});
</code></pre></div>

Here, setting the `allowHigherVersions` flag ensures that if newer versions of a browser are released &mdash; ones that are not yet a part of Can I Use’s database &mdash; they will still report as truthy for modern browsers.

One of `browserslist-useragent`'s functions is to ensure that platform quirks are taken into account while matching user agents. For example, all browsers on iOS (including Chrome) use WebKit as the underlying engine and will be matched to the respective Safari-specific Browserslist query.

It might not be prudent to rely solely on the correctness of user-agent parsing in production. By falling back to the legacy bundle for browsers that aren’t defined in the modern list or that have unknown or unparseable user-agent strings, we ensure that our website still works.

## Conclusion: Is It Worth It?

We have managed to cover an end-to-end flow for shipping bloat-free bundles to our clients. But it’s only reasonable to wonder whether the maintenance overhead this adds to a project is worth its benefits. Let’s evaluate the pros and cons of this approach:

### 1. Maintenance And Testing

One is required to maintain only a single Browserslist configuration that powers all of the tools in this pipeline. Updating the definitions of modern and legacy browsers can be done anytime in the future without having to refactor supporting configurations or code. I’d argue that this makes the maintenance overhead almost negligible.

There is, however, a small theoretical risk associated with relying on Babel to produce two different code bundles, each of which needs to work fine in its respective environment.

While errors due to differences in bundles might be rare, monitoring these variants for errors should help to identify and effectively mitigate any issues.

### 2. Build Time vs. Runtime

Unlike other techniques prevalent today, all of these optimizations occur at build time and are invisible to the client.

### 3. Progressively Enhanced Speed

The experience of users on modern browsers becomes significantly faster, while users on legacy browsers continue to get served the same bundle as before, without any negative consequences.

### 4. Using Modern Browser Features With Ease

We often avoid using new browser features due to the size of polyfills required to use them. At times, we even choose smaller non-spec-compliant polyfills to save on size. This new approach allows us to use spec-compliant polyfills without worrying much about affecting all users.

## Differential Bundle Serving In Production

Given the significant advantages, we adopted this build pipeline when creating a new mobile checkout experience for customers of Urban Ladder, one of India’s largest furniture and decor retailers.

In our already optimized bundle, we were able to squeeze savings of approximately 20% on the Gzip’d CSS and JavaScript resources sent down the wire to modern mobile users. Because more than 80% of our daily visitors were on these evergreen browsers, the effort put in was well worth the impact.

### Further Resources

- “[Loading Polyfills Only When Needed](https://philipwalton.com/articles/loading-polyfills-only-when-needed/)”, Philip Walton
- [`@babel/preset-env`](https://babeljs.io/docs/en/babel-preset-env)  
A smart Babel preset
- [Browserslist “Tools”](https://github.com/browserslist/browserslist#tools)  
Ecosystem of plugins built for Browserslist
- [Can I Use](https://caniuse.com/usage-table)  
Current browser marketshare table

{{< signature "dm, ra, yk, il, al" >}}
