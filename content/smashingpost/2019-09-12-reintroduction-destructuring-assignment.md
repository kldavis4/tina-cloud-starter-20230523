---
title: 'A Re-Introduction To Destructuring Assignment'
slug: reintroduction-destructuring-assignment
author: laurie-barth
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca422639-1037-4d76-b063-b3a0bf75f000/reintroduction-destructuring-assignment.png
date: 2019-09-12T14:00:59+02:00
summary: >-
  Sick of chaining lots of keys together with dots to access nested values in objects? Frustrated that `arr[0]` isn’t a very descriptive name? Destructuring assignment has incredible value when accessing values in arrays and objects. Read on to learn a number of use cases in which this syntax can come in handy.
description: >-
  Sick of chaining lots of keys together with dots to access nested values in objects? Frustrated that `arr[0]` isn’t a very descriptive name? Destructuring assignment has incredible value when accessing values in arrays and objects. Read on to learn a number of use cases in which this syntax can come in handy.
categories:
  - JavaScript
disable_newsletterbox: true
---
<p>If you write JavaScript you’re likely familiar with ES2015 and all the new language standards that were introduced. One such standard that has seen incredible popularity is destructuring assignment. The ability to “dive into” an array or object and reference something inside of it more directly. It usually goes something like this.</p>

<pre><code class="language-javascript">const response = {
   status: 200,
   data: {}
}

// instead of response.data we get...
const {data} = response //now data references the data object directly


const objectList = [ { key: 'value' }, { key: 'value' }, { key: 'value' } ]

// instead of objectList[0], objectList[1], etc we get...
const [obj, obj1, obj2] = objectList // now each object can be referenced directly
</code></pre>

<p>However, destructuring assignment is such a powerful piece of syntax that many developers, even those who have been using it since it was first released, forget some of the things it can do. In this post, we’ll go through five real-world examples for both object and array destructuring, sometimes both! And just for fun, I’ll include a wonky example I came across just the other day.</p>

## 1. Nested Destructuring

<p>Being able to access a top-level key inside an object, or the first element of an array is powerful, but it’s also somewhat limiting. It only removes one level of complexity and we still end up with a series of dots or <code>[0]</code> references to access what we’re really after.</p>

<p>As it turns out, destructuring can work beyond the top level. And there can be valid reasons for doing so. Take this example of an object response from an HTTP request. We want to go beyond the data object and access just the user. So long as we know the keys we’re looking for, that isn’t a problem.</p>

<div class="break-out">

<pre><code class="language-javascript">const response = {
  status: 200,
  data: { 
    user: {
       name: 'Rachel', 
      title: 'Editor in Chief' 
    }, 
    account: {},
    company: 'Smashing Magazine' 
  }
}

const {data: {user}} = response // user is { name: 'Rachel', title: 'Editor in Chief'}</code></pre>
</div>

<p>The same can be done with nested arrays. In this case, you don’t need to know the key since there is none. What you need to know is the position of what you’re looking for. You’ll need to provide a reference variable (or comma placeholder) for each element up and until the one you’re looking for (we’ll get to that later). The variable can be named anything since it is not attempting to match a value inside the array.</p>

<div class="break-out">

<pre><code class="language-javascript">const smashingContributors = [['rachel', ['writer', 'editor', 'reader']], ['laurie', ['writer', 'reader']]]

const [[rachel, roles]] = smashingContributors
// rachel is 'rachel'
// roles is [ 'writer', 'editor', 'reader' ]</code></pre>
</div>

<p>Keep in mind that these features should be used judiciously, as with any tool. Recognize your use case and the audience of your code base. Consider readability and ease of change down the road. For example, if you’re looking to access a subarray only, perhaps a map would be a better fit.</p>

{{% feature-panel %}}

## 2. Object And Array Destructuring

<p>Objects and arrays are common data structures. So common, in fact, that one often appears inside the other. Beyond nested destructuring, we can access nested properties even if they are in a different type of data structure than the external one we’re accessing.</p>

<p>Take this example of an array inside an object.</p>

<pre><code class="language-javascript">const organization = { 
    users: ['rachel', 'laurie', 'eric', 'suzanne'],
    name: 'Smashing Magazine',
    site: 'https://www.smashingmagazine.com/' 
}

const {users:[rachel]} = organization // rachel is 'rachel'</code></pre>

<p>The opposite use case is also valid. An array of objects.</p>

<div class="break-out">

<pre><code class="language-javascript">const users = [{name: 'rachel', title: 'editor'}, {name: 'laurie', title: 'contributor'}]

const [{name}] = users // name is 'rachel'</code></pre>
</div>

<p>As it turns out, we have a bit of a problem in this example. We can only access the name of the first user; otherwise, we’ll attempt to use ‘name’ to reference two different strings, which is invalid. Our next destructuring scenario should sort this out.</p>

## 3. Aliases

<p>As we saw in the above example (when we have repeating keys inside different objects that we want to pull out), we can’t do so in the “typical” way. Variable names can’t repeat within the same scope (that’s the simplest way of explaining it, it’s obviously more complicated than that).</p>

<div class="break-out">

<pre><code class="language-javascript">const users = [{name: 'rachel', title: 'editor'}, {name: 'laurie', title: 'contributor'}]

const [{name: rachel}, {name: laurie}] = users // rachel is 'rachel' and laurie is 'laurie'</code></pre>
</div>

<p>Aliasing is only applicable to objects. That’s because arrays can use any variable name the developer chooses, instead of having to match an existing object key.</p>

{{% ad-panel-leaderboard %}}

## 4. Default Values

<p>Destructuring often assumes that the value it’s referencing is there, but what if it isn’t? It’s never pleasant to litter code with undefined values. That’s when default values come in handy.</p>

<p>Let’s look at how they work for objects.</p>

<pre><code class="language-javascript">const user = {name: 'Luke', organization: 'Acme Publishing'}
const {name='Brian', role='publisher'} = user
// name is Luke
// role is publisher</code></pre>

<p>If the referenced key already has a value, the default is ignored. If the key does not exist in the object, then the default is used.</p>

<p>We can do something similar for arrays.</p>

<pre><code class="language-javascript">const roleCounts = [2]
const [editors = 1, contributors = 100] = roleCounts
// editors is 2
// contributors is 100</code></pre>

<p>As with the objects example, if the value exists then the default is ignored. Looking at the above example you may notice that we’re destructuring more elements than exist in the array. What about destructuring fewer elements?</p>

## 5. Ignoring Values

<p>One of the best parts of destructuring is that it allows you to access values that are part of a larger data structure. This includes isolating those values and ignoring the rest of the content, if you so choose.</p>

<p>We actually saw an example of this earlier, but let’s isolate the concept we’re talking about.</p>

<pre><code class="language-javascript">const user = {name: 'Luke', organization: 'Acme Publishing'}
const {name} = user
// name is Luke</code></pre>

<p>In this example, we never destructure <code>organization</code> and that’s perfectly ok. It’s still available for reference inside the <code>user</code> object, like so.</p>

<pre><code class="language-javascript">user.organization</code></pre>

<p>For arrays, there are actually two ways to “ignore” elements. In the objects example we’re specifically referencing internal values by using the associated key name. When arrays are destructured, the variable name is assigned by position. Let’s start with ignoring elements at the end of the array.</p>

<pre><code class="language-javascript">const roleCounts = [2, 100, 100000]
const [editors, contributors] = roleCounts
// editors is 2
// contributors is 100</code></pre>

<p>We destructure the first and second elements in the array and the rest are irrelevant. But how about later elements? If it’s position based, don’t we have to destructure each element up until we hit the one we want?</p>

<p>As it turns out, we do not. Instead, we use commas to imply the existence of those elements, but without reference variables they’re ignored.</p>

<pre><code class="language-javascript">const roleCounts = [2, 100, 100000]
const [, contributors, readers] = roleCounts
// contributors is 100
// readers is 100000</code></pre>

<p>And we can do both at the same time. Skipping elements wherever we want by using the comma placeholder. And again, as with the object example, the “ignored” elements are still available for reference within the <code>roleCounts</code> array.</p>

{{% ad-panel-leaderboard %}}

## Wonky Example

<p>The power and versatility of destructuring also means you can do some truly bizarre things. Whether they’ll come in handy or not is hard to say, but worth knowing it’s an option!</p>

<p>One such example is that you can use destructuring to make shallow copies.</p>

<pre><code class="language-javascript">const obj = {key: 'value', arr: [1,2,3,4]}
const {arr, arr: copy} = obj
// arr and copy are both [1,2,3,4]</code></pre>

<p>Another thing destructuring can be used for is dereferencing.</p>

<pre><code class="language-javascript">const obj = {node: {example: 'thing'}}
const {node, node: {example}} = obj
// node is { example: 'thing' }
// example is 'thing'</code></pre>

<p>As always, readability is of the utmost importance and all of these examples should be used judicially. But knowing all of your options helps you pick the best one.</p>

## Conclusion

<p>JavaScript is full of complex objects and arrays. Whether it’s the response from an HTTP request, or static data sets, being able to access the embedded content efficiently is important. Using destructuring assignment is a great way to do that. It not only handles multiple levels of nesting, but it allows for focused access and provides defaults in the case of undefined references.</p>

<p>Even if you’ve used destructuring for years, there are so many details hidden in the spec. I hope that this article acted as a reminder of the tools the language gives you. Next time you’re writing code, maybe one of them will come in handy!</p>

{{< signature "dm, yk, il" >}}
