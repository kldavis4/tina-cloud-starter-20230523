---
title: 'Sliding In And Out Of Vue.js'
slug: vue-framework-third-party-javascript
author: kevin-ball
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/517356c5-d59d-42ab-a8d3-3b3efc53203c/vuejs-kball-sharing-card.png
date: 2019-02-26T12:00:34+01:00
summary: >-
  One of the key advantages of Vue.js is that it plays nicely with other code: it is easy to embed progressively into other applications, but it is also easy to wrap up non-Vue code into Vue. This article explores this second advantage, covering three distinct types of third-party JavaScript and ways to embed each of them in Vue.
description: >-
  One of the key advantages of Vue.js is that it plays nicely with other code: it is easy to embed progressively into other applications, but it is also easy to wrap up non-Vue code into Vue. This article explores this second advantage, covering three distinct types of third-party JavaScript and ways to embed each of them in Vue.
categories:
  - Vue
  - Frameworks
  - JavaScript
---
Vue.js has achieved phenomenal adoption growth over the last few years. It has gone from a barely known open-source library to the second most popular front-end framework (behind only React.js).

One of the biggest reasons for its growth is that Vue is a *progressive* framework &mdash; it allows you to adopt bits and pieces at a time. Don’t need a full single page application? Just embed a component. Don’t want to use a build system? Just drop in a script tag, and you’re up and running.

This progressive nature has made it very easy to begin adopting Vue.js piecemeal, without having to do a big architecture rewrite. However, one thing that is often overlooked is that it’s not just easy to embed Vue.js into sites written with other frameworks, **it’s also easy to embed other code inside of Vue.js**. While Vue likes to control the DOM, it has lots of escape hatches available to allow for non-Vue JavaScript that also touches the DOM.

This article will explore the different types of third-party JavaScript that you might want to use, what situations you might want to use them inside of a Vue project, and then cover the tools and techniques that work best for embedding each type within Vue. We’ll close with some considerations of the drawbacks of these approaches, and what to consider when deciding if to use them.

*This article assumes some familiarity with Vue.js, and the concepts of components and directives. If you are looking for an introduction to Vue and these concepts, you might check out Sarah Drasner’s excellent [introduction to Vue.js series](https://css-tricks.com/intro-to-vue-1-rendering-directives-events/) or the official [Vue Guide](https://vuejs.org/v2/guide/).*

{{% feature-panel %}}

## Types Of Third-Party JavaScript

There are three major types of third-party JavaScript that we’ll look at in order of complexity:

<ol>
<li><a href="#non-dom-libraries">Non-DOM Touching Libraries</a></li>
<li><a href="#element-augmentation-libraries">Element Augmentation Libraries</a></li>
<li><a href="#components-and-component-libraries">Components And Component Libraries</a></li>
</ol>

### Non-DOM Libraries

The first category of third-party JavaScript is libraries that provide logic in the abstract and have no direct access to the DOM. Tools like [moment.js](https://momentjs.com/) for handling dates or [lodash](https://lodash.com/) for adding functional programming utilities fall into this category.

These libraries are trivial to integrate into Vue applications, but can be wrapped up in a couple of ways for particularly ergonomic access. These are very commonly used to provide utility functionality, the same as they would in any other type of JavaScript project.

### Element Augmentation Libraries

Element augmentation is a time-honored way to add just a bit of functionality to an element. Examples include tasks like lazy-loading images with [lozad](https://github.com/ApoorvSaxena/lozad.js) or adding input masking using [Vanilla Masker](https://github.com/vanilla-masker/vanilla-masker).

These libraries typically impact a single element at a time, and expect a constrained amount of access to the DOM. They will likely be manipulating that single element, but not adding new elements to the DOM.

These tools typically are tightly scoped in purpose, and relatively straightforward to swap out with other solutions. They’ll often get pulled into a Vue project to avoid re-inventing the wheel.

### Components And Component Libraries

These are the big, intensive frameworks and tools like [Datatables.net](https://datatables.net/) or [ZURB Foundation](https://foundation.zurb.com/). They create a full-on interactive component, typically with multiple interacting elements.

They are either directly injecting these elements into the DOM or expect a high level of control over the DOM. They were often built with another framework or toolset (both of these examples build their JavaScript on top of jQuery).

These tools provide *extensive* functionality and can be challenging to replace with a different tool without extensive modifications, so a solution for embedding them within Vue can be key to migrating a large application.

## How To Use In Vue

### Non-DOM Libraries

Integrating a library that doesn’t touch the DOM into a Vue.js project is relatively trivial. If you’re using JavaScript modules, simply `import `or `require` the module as you would in another project. For example:

<pre><code class="language-javascript">import moment from 'moment';

Vue.component('my-component', {
  //…
  methods: {
    formatWithMoment(time, formatString) {
      return moment(time).format(formatString);
    },
});
</code></pre>

If using global JavaScript, include the script for the library before your Vue project:

<div class="break-out">

 <pre><code class="language-javascript">&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.24.0/moment.js"&gt;&lt;/script&gt;
&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.22/vue.min.js"&gt;&lt;/script&gt;
&lt;script src="/project.js"&gt;&lt;/script&gt;
</code></pre>
</div>

One additional common way to layer on a bit more integration is to wrap up your library or functions from the library using a filter or method to make it easy to access from inside your templates.

#### Vue Filters

Vue [Filters](https://vuejs.org/v2/guide/filters.html) are a pattern that allows you to apply text formatting directly inline in a template. Drawing an example from the documentation, you could create a 'capitalize' filter and then apply it in your template as follows:

<pre><code class="language-javascript">{{myString | capitalize}}
</code></pre>

When importing libraries having to do with formatting, you may want to wrap them up as a filter for ease of use. For example, if we are using `moment` to format all or many of our dates to relative time, we might create a `relativeTime` filter.

<pre><code class="language-javascript">const relativeTime = function(value) {
  if (!value) return '';
  return moment(value).fromNow();
}
</code></pre>

We can then add it globally to all Vue instances and components with the `Vue.filter` method:

<pre><code class="language-javascript">Vue.filter(’relativeTime', relativeTime);
</code></pre>

Or add it to a particular component using the `filters` option:

<pre><code class="language-javascript">const myComponent = {
  filters: {
    ’relativeTime': relativeTime,
  } 
}
</code></pre>

You can play with this on CodePen here: 

{{< codepen height="480" theme_id="light" slug_hash="drbQOo" default_tab="result" user="smashing-magazine" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashing-magazine/pen/drbQOo/">Vue integrations: Moment Relative Value Filter</a> by <a href="https://codepen.io/kball/">Kevin Ball</a>.{{< /codepen >}}

### Element Augmentation Libraries

Element augmentation libraries are slightly more complex to integrate than libraries that don’t touch the DOM &mdash; if you’re not careful, Vue and the library can end up at cross purposes, fighting each other for control.

To avoid this, you need to hook the library into Vue’s lifecycle, so it runs after Vue is done manipulating the DOM element, and properly handles updates that Vue instigates.

This could be done in a component, but since these libraries typically touch only a single element at a time, a more flexible approach is to wrap them in a custom directive.

{{% ad-panel-leaderboard %}}

#### Vue Directives 

Vue directives are modifiers that can be used to add behavior to elements in your page. Vue ships with a number of built-in directives that you are likely already comfortable with &mdash; things like `v-on`, `v-model`, and `v-bind`. It is also possible to create *custom* directives that add any sort of behavior to an element &mdash; exactly what we’re trying to achieve.

Defining a custom directive is much like defining a component; you create an object with a set of methods corresponding to particular lifecycle hooks, and then add it to Vue either globally by running:

<pre><code class="language-javascript">Vue.directive('custom-directive', customDirective);
</code></pre>

Or locally in a component by adding it to the `directives` object in the component:

<pre><code class="language-javascript">const myComponent = {
  directives: {
    'custom-directive': customDirective,
  } 
}
</code></pre>

#### Vue Directive Hooks

Vue directives have the following hooks available to define behavior. While you can use all of them in a single directive, it is also not uncommon to only need one or two. They are all optional, so use only what you need.

- `bind(el, binding, vnode)`  
Called once and only once, when the directive is first bound to an element. This is a good place for one-time setup work, but be cautious, i.e. the element exists, may not yet actually be in the document.
- `inserted(el, binding, vnode)`  
Called when the bound element has been inserted into its parent node. This also does not guarantee presence in the document, but does mean if you need to reference the parent you can.
- `update(el, binding, vnode, oldVnode)`  
Called whenever the containing component’s VNode has updated. There are no guarantees that other children of the component will have updated, and the value for the directive may or may not have changed. (You can compare `binding.value` to `binding.oldValue` to see and optimize away any unnecessary updates.)
- `componentUpdated(el, binding, vnode, oldVnode)`  
Similar to `update`, but called after all children of the containing component have updated. If the behavior of your directive depends on its peers (e.g. `v-else`), you would use this hook instead of update.
- `unbind(el, binding, vnode)`  
Similar to `bind`, this is called once and only once, when the directive is unbound from an element. This is a good location for any teardown code.

The arguments to these functions are:

- `el`: The element the directive is bound to;
- `binding`: An object containing information about the arguments and value of the directive;
- `vnode`: The virtual node for this element produced by Vue’s compiler;
- `oldVNode`: The previous virtual node, only passed to `update` and `componentUpdated`.

*More information on these can be found in the [Vue Guide on custom directives](https://vuejs.org/v2/guide/custom-directive.html#Directive-Hook-Arguments).*

{{% ad-panel-leaderboard %}}

#### Wrapping The Lozad Library In A Custom Directive

Let’s look at an example of doing this type of wrapping using [lozad](https://www.npmjs.com/package/lozad), a lazy-loading library built using the Intersection Observer API. The API for using lozad is simple: use `data-src` instead of `src` on images, and then pass a selector or an element to `lozad()` and call `observe` on the object that is returned:

<pre><code class="language-javascript">const el = document.querySelector('img');
const observer = lozad(el); 
observer.observe();
</code></pre>

We can do this simply inside of a directive using the `bind` hook.

<pre><code class="language-javascript">const lozadDirective = {
  bind(el, binding) {
    el.setAttribute('data-src', binding.value) ;
    let observer = lozad(el);
    observer.observe();
  }
}
Vue.directive('lozad', lozadDirective)
</code></pre>

With this in place, we can change images to lazy load by simply passing the source as a string into the v-lozad directive:

<pre><code class="language-javascript">&lt;img v-lozad="'https://placekitten.com/100/100'" /&gt;
</code></pre>

You can observe this at work in this CodePen:

{{< codepen height="480" theme_id="light" slug_hash="aMoQLe" default_tab="result" user="smashing-magazine" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashing-magazine/pen/aMoQLe/">Vue integrations: Lozad Directive Just Bind</a> by <a href="https://codepen.io/kball">Kevin Ball</a>).{{< /codepen >}}

We’re not quite done yet though! While this works for an initial load, what happens if the value of the source is dynamic, and Vue changes it? This can be triggered in the pen by clicking the “Swap Sources” button. If we only implement bind, the values for `data-src` and `src` are not changed when we want them to be!

To implement this, we need to add an `updated` hook:

<pre><code class="language-javascript">const lozadDirective = {
  bind(el, binding) {
    el.setAttribute('data-src', binding.value) ;
    let observer = lozad(el);
    observer.observe();
  },
  update(el, binding) {
    if (binding.oldValue !== binding.value) {
      el.setAttribute('data-src', binding.value);
      if (el.getAttribute('data-loaded') === 'true') {
        el.setAttribute('src', binding.value);
      }
    }
  }
}
</code></pre>

With this in place, we’re set! Our directive now updates everything lozad touches whenever Vue updates. The final version can be found in this pen:

{{< codepen height="480" theme_id="light" slug_hash="gEYQvR" default_tab="result" user="smashing-magazine" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashing-magazine/pen/gEYQvR/">Vue integrations: Lozad Directive With Updates</a> by <a href="https://codepen.io/kball">Kevin Ball</a>.{{< /codepen >}}

### Components And Component Libraries

The most complex third-party JavaScript to integrate is that which controls entire regions of the DOM, full-on components and component libraries. These tools expect to be able to create and destroy elements, manipulate them, and more.

For these, the best way to pull them into Vue is to wrap them in a dedicated component, and make extensive use of Vue’s lifecycle hooks to manage initialization, passing data in, and handling events and callbacks.

Our goal is to completely abstract away the details of the third-party library, so that the rest of our Vue code can interact with our wrapping component like a native Vue component.

#### Component Lifecycle Hooks

To wrap around a more complex component, we’ll need to be familiar with the full complement of lifecycle hooks available to us in a component. Those hooks are:

- `beforeCreate()`  
Called before the component is instantiated. Pretty rarely used, but useful if we’re integrating profiling or something similar.
- `created()`  
Called after the component is instantiated, but before it is added to the DOM. Useful if we have any one-off setup that doesn’t require the DOM.
- `beforeMount()`  
Called just before the component is mounted in the DOM. (Also pretty rarely used.)
- `mounted()`  
Called once the component is placed into the DOM. For components and component libraries that assume DOM presence, this is one of our most commonly used hooks.
- `beforeUpdate()`  
Called when Vue is about to update the rendered template. Pretty rarely used, but again useful if integrating profiling.
- `updated()`  
Called when Vue has finished updating the template. Useful for any re-instantiation that is needed.
- `beforeDestroy()`  
Called before Vue tears down a component. A perfect location to call any destruction or deallocation methods on our third-party component
- `destroyed()`  
Called after Vue has torn down a component.

#### Wrapping A Component, One Hook At A Time

Let’s take a look at the popular [jquery-multiselect](https://loudev.com/) library. There exist many fine multiselect components already written in Vue, but this example gives us a nice combination: complicated enough to be interesting, simple enough to be easy to understand.

The first place to start when implementing a third-party component wrapper is with the `mounted` hook.  Since the third-party component likely expects the DOM to exist before it takes charge of it, this is where you will hook in to initialize it.

For example, to start wrapping jquery-multiselect, we could write: 

<pre><code class="language-javascript">mounted() { 
  $(this.$el).multiselect();
}
</code></pre>

You can see this functioning in this CodePen:

{{< codepen height="480" theme_id="light" slug_hash="WmeYKy" default_tab="result" breakout="true" user="smashing-magazine" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashing-magazine/pen/WmeYKy/">ue integrations: Simple Multiselect Wrapper</a> by <a href="https://codepen.io/kball">Kevin Ball</a>.{{< /codepen >}}

This is looking pretty good for a start. If there were any teardown we needed to do, we could also add a `beforeDestroy` hook, but this library does not have any teardown methods that we need to invoke.

#### Translating Callbacks To Events

The next thing we want to do with this library is add the ability to notify our Vue application when the user selects items. The jquery-multiselect library enables this via callbacks called `afterSelect` and `afterDeselect`, but to make this more vue-like, we’ll have those callbacks emit events. We could wrap those callbacks naively as follows:

<div class="break-out">

 <pre><code class="language-javascript">mounted() { 
  $(this.$el).multiSelect({
     afterSelect: (values) => this.$emit('select', values),
     afterDeselect: (values) => this.$emit('deselect', values)
   });
}
</code></pre>
</div>

However, if we insert a logger in the event listeners, we’ll see that this does not provide us a very vue-like interface. After each select or deselect, we receive a list of the values that have changed, but to be more vue-like, we should probably emit a change event with the current list. 

We also don’t have a very vue-like way to set values. Instead of this naive approach then, we should look at using these tools to implement something like the v-model approach that [Vue provides for native select elements](https://vuejs.org/v2/guide/forms.html#Select).

#### Implementing `v-model`

To implement `v-model` on a component, we need to enable two things: accepting a `value` prop that will accept an array and set the appropriate options as selected, and then emit an `input` event on change that passes the new complete array.

There are four pieces to handle here: initial setup for a particular value, propagate any changes made up to the parent, and handle any changes to value starting outside the component, and finally handle any changes to the content in the slot (the options list).

Let’s approach them one at a time.

<ol>
  <li><strong>Setup With A Value Prop</strong><br />First, we need to teach our component to accept a value prop, and then when we instantiate the multiselect we will tell it which values to select.<br />

<pre><code class="language-javascript">export default {
  props: {
    value: Array,
    default: [],
  },
  mounted() { 
    $(this.$el).multiSelect();
    $(this.$el).multiSelect('select', this.value);
  },
}
</code></pre>
</li>
<li><strong>Handle Internal Changes</strong><br />To handle changes occurring due to the user interacting with the multiselect, we can go back to the callbacks we explored before &mdash; but ‘less naively’ this time. Instead of simply emitting what they send us, we want to turn a new array that takes into account our original value and the change made.<br />

<div class="break-out">

 <pre><code class="language-javascript">mounted() { 
  $(this.$el).multiSelect({
    afterSelect: (values) => this.$emit('input', [...new Set(this.value.concat(values))]),
    afterDeselect: (values) => this.$emit('input', this.value.filter(x => !values.includes(x))),
  });
  $(this.$el).multiSelect('select', this.value);
},
</code></pre>
</div>
<br />Those callback functions might look a little dense, so let’s break them down a little.<br /><br />The <code>afterSelect</code> handler concatenates the newly selected value with our existing values, but then just to make sure there are no duplicates, it converts it to a Set (guarantees uniqueness) and then a destructuring to turn it back to an array.<br /><br />The <code>afterDeselect</code> handler simply filters out any deselected values from the current value list in order to emit a new list.</li>
<li><strong>Handling External Updates To Value</strong><br />The next thing we need to do is to update the selected values in the UI whenever the <code>value</code> prop changes. This involves translating from a <em>declarative</em> change to the props into an <em>imperative</em> change utilizing the functions available on multiselect. The simplest way to do this is to utilize a watcher on our <code>value</code> prop:<br />

<pre><code class="language-javascript">watch:
  // don’t actually use this version. See why below
  value() {
    $(this.$el).multiselect('select', this.value);
  }
}
</code></pre>
<br />However, there’s a catch! Because triggering that select will actually result in our <code>onSelect</code> handler, and thus use updating values. If we do this naive watcher, we will end up in an infinite loop.</br /><br />Luckily,for us, Vue gives us the ability to see the old as well as the new values. We can compare them, and only trigger the select if the value has changed. Array comparisons can get tricky in JavaScript, but for this example, we’ll take advantage of the fact that our arrays are simple (not containing objects) and use JSON stringify to do the comparison. After taking into account that we need to also deselect any that options that have been removed, our final watcher looks like this:<br />

<pre><code class="language-javascript">watch: {
    value(newValue, oldValue) {
      if (JSON.stringify(newValue) !== JSON.stringify(oldValue)) {
        $(this.$el).multiSelect('deselect_all');
        $(this.$el).multiSelect('select', this.value);
      }
    }
  },
</code></pre>
</li>
<li><strong>Handling External Updates To Slot</strong><br />We have one last thing that we need to handle: our multiselect is currently utilizing option elements passed in via a slot. If that set of options changes, we need to tell the multiselect to refresh itself, otherwise the new options don’t show up. Luckily, we have both an easy API for this in multiselect (the ’refresh' function and an obvious Vue hook to hook into) updated. Handling this last case is as simple as:<br />

<pre><code class="language-javascript">updated() {
  $(this.$el).multiSelect(’refresh');
},
</code></pre>
<br />You can see a working version of this component wrapper in this CodePen:<br />
{{< codepen height="480" theme_id="light" slug_hash="QoLJJV" default_tab="result" user="smashing-magazine" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashing-magazine/pen/QoLJJV/">Vue integrations: Multiselect Wrapper with v-model</a> by <a href="https://codepen.io/kball">Kevin Ball</a>.{{< /codepen >}}
</li>
</ol>

## Drawbacks And Other Considerations

Now that we’ve looked at how straightforward it is to utilize third-party JavaScript within Vue, it’s worth discussing drawback of these approaches, and when it appropriate to use them.

### Performance Implications

One of the primary drawbacks of utilizing third-party JavaScript that is *not* written for Vue within Vue is performance &mdash; particularly when pulling in components and component libraries or things built using entire additional frameworks. Using this approach can result in a lot of additional JavaScript that needs to be downloaded and parsed by the browser before the user can interact with our application.

For example, by using the multiselect component, we developed above means pulling in not only that component’s code, but all of jQuery as well. That can double the amount of framework related JavaScript our users will have download, just for this one component! Clearly finding a component built natively with Vue.js would be better.

Additionally, when there are large mismatches between the APIs used by third-party libraries and the declarative approach that Vue takes, you may find yourself implementing patterns that result in a lot of extra execution time. Also using the multiselect example, we had to refresh the component (requiring looking at a whole bunch of the DOM) every time a slot changed, while a Vue-native component could utilize Vue’s virtual DOM to be much more efficient in its updates.

### When To Use

Utilizing third-party libraries can save you a ton of development time, and often means you’re able to use well-maintained and tested software that you don’t have the expertise to build. The primary drawback is performance, particularly when bringing in large frameworks like jQuery.

For libraries that don’t have those large dependencies, and particularly those that don’t heavily manipulate the DOM, there’s no real reason to favor Vue-specific libraries over more generic ones. Because Vue makes it so easy to pull in other JavaScript, you should go based on your feature and performance needs, simply picking the best tool for the job, without worrying about something Vue-specific.

For more extensive component frameworks, there are three primary cases in which you’d want to pull them in.

1. **Prototyping**  
In this case, speed of iteration matters far more than user performance; use whatever gets the job done fastest.
2. **Migrating an existing site.**  
If you’re migrating from an existing site to Vue, being able to wrap whatever framework you’re already using within Vue will give you a graceful migration path so you can gradually pull out the old code piece by piece, without having to do a big bang rewrite.
3. **When the functionality simply isn’t available yet in a Vue component.**  
If you have a specific and challenging requirement you need to meet, for which a third-party library exists but there isn’t a Vue specific component, by all means consider wrapping the library that does exist.

{{% pull-quote %}}
 When there are large mismatches between the APIs used by third-party libraries and the declarative approach that Vue takes, you may find yourself implementing patterns that result in a lot of extra execution time.
{{% /pull-quote %}}

### Examples In The Wild

The first two of these patterns are used all over the open-source ecosystem, so there are a number of different examples you can investigate. Since wrapping an entire complex component or component library tends to be more of a stopgap/migration solution, I haven’t found as many examples of that in the wild, but there are a couple out there, and I’ve used this approach for clients occasionally as requirements have dictated. Here is a quick example of each:

1. [Vue-moment](https://www.npmjs.com/package/vue-moment) wraps the moment.js library and creates a set of handy Vue filters;
2. [Awesome-mask](https://www.npmjs.com/package/awesome-mask) wraps the vanilla-masker library and creates a directive for masked inputs;
3. [Vue2-foundation](https://www.npmjs.com/package/vue2-foundation) wraps up the ZURB Foundation component library inside of Vue components. 

## Conclusion

The popularity of Vue.js shows no signs of slowing down, with a huge amount of credit being due to the framework’s progressive approach. By enabling incremental adoption, Vue’s progressive nature means that individuals can start using it here and there, a bit at a time, without having to do massive rewrites.

As we’ve looked at here, that progressive nature extends in the other direction as well. Just as you can embed Vue bit by bit in another application, you can embed other libraries bit by bit inside of Vue.

Need some piece of functionality that hasn’t been ported to a Vue component yet? Pull it in, wrap it up, and you’re good to go.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
  <li><a title="Read 'Replacing jQuery With Vue.js: No Build Step Necessary'" href="https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/" rel="bookmark">Replacing jQuery With Vue.js: No Build Step Necessary</a> by Sarah Drasner</li>
  <li><a title="Read 'Creating Custom Inputs With Vue.js'" href="https://www.smashingmagazine.com/2017/08/creating-custom-inputs-vue-js/" rel="bookmark">Creating Custom Inputs With Vue.js</a> by Joseph Zimmerman</li>
  <li><a title="Read 'Hit The Ground Running With Vue.js And Firestore'" href="https://www.smashingmagazine.com/2018/04/vuejs-firebase-firestore/" rel="bookmark">Hit The Ground Running With Vue.js And Firestore</a> by Lukas van Driel</li>
  <li><a title="Read 'Serverless Functions And Vue.js'" href="https://vimeo.com/296938039" rel="bookmark">Serverless Functions And Vue.js</a> by Sarah Drasner (Video, SmashingConf NYC 2018)</li>
</ul>

{{< signature "rb, ra, il" >}}
