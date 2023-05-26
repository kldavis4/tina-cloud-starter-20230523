---
title: 'What’s New In Vue 3?'
slug: new-vue3-update
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e67401-66eb-46b6-9a92-c855932f01bb/new-vue3-update.png
date: 2020-11-13T12:00:00.000Z
summary: >-
  Vue 3 comes with a lot of interesting new features and changes to some of the existing ones that are aimed at making development with the framework a lot easier and maintainable. In this article, we’re going to take a look at some of these new features and how to get started with them. We’re also going be taking a look at some of the changes done to the existing features.
description: >-
  In this article, we’re going to take a look at some of these new features and how to get started with them. We’re also going be taking a look at some of the changes done to the existing features.
categories:
  - Vue
  - JavaScript
  - Frameworks
---

With the release of Vue 3, developers have to make the upgrade from Vue 2 as it comes with a handful of new features that are super helpful in building easy-to-read and maintainable components and improved ways to structure our application in Vue. We’re going to be taking a look at some of these features in this article.

At the end of this tutorial, the readers will;

1. Know about `provide / inject` and how to use it.
2. Have a basic understanding of Teleport and how to use it.
3. Know about Fragments and how to go about using them.
4. Know about the changes made to the Global Vue API.
5. Know about the changes made to the Events API.

*This article is aimed at those that have a proper understanding of Vue 2.x. You can find all the code used in this example in [GitHub](https://github.com/Timibadass/vue-3-examples).*

## `provide / inject`

In Vue 2.x, we had [`props`](https://v3.vuejs.org/guide/component-props.html) that made it easy to pass data (string, arrays, objects, etc) from a parent component directly to its children component. But during development, we often found instances where we needed to pass data from the parent component to a deeply nested component which was more difficult to do with `props`. This resulted in the use of Vuex Store, [Event Hub](https://css-tricks.com/using-event-bus-to-share-props-between-vue-components/), and sometimes passing data through the deeply nested components. Let’s look at a simple app;

*It is important to note that Vue 2.2.0 also came with [`provide / inject`](https://vuejs.org/v2/api/#provide-inject) which was not recommended to use in generic application code.*

<div class="break-out">

 <pre><code class="language-javascript"># parentComponent.vue

&lt;template&gt;
  &lt;div class="home"&gt;
    &lt;img alt="Vue logo" src="../assets/logo.png" /&gt;
    &lt;HelloWorld msg="Vue 3 is liveeeee!" :color="color" /&gt;
    &lt;select name="color" id="color" v-model="color"&gt;
      &lt;option value="" disabled selected&gt; Select a color&lt;/option&gt;
      &lt;option :value="color" v-for="(color, index) in colors" :key="index"&gt;{{
        color
      }}&lt;/option&gt;&lt;/select
    &gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import HelloWorld from "@/components/HelloWorld.vue";
  export default {
    name: "Home",
    components: {
      HelloWorld,
    },
    data() {
      return {
        color: "",
        colors: ["red", "blue", "green"],
      };
    },
  };
&lt;/script&gt;
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript"># childComponent.vue

&lt;template&gt;
  &lt;div class="hello"&gt;
    &lt;h1&gt;{{ msg }}&lt;/h1&gt;
    &lt;color-selector :color="color"&gt;&lt;/color-selector&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import colorSelector from "@/components/colorComponent.vue";
  export default {
    name: "HelloWorld",
    components: {
      colorSelector,
    },
    props: {
      msg: String,
      color: String,
    },
  };
&lt;/script&gt;
&lt;!-- Add "scoped" attribute to limit CSS to this component only --&gt;
&lt;style scoped&gt;
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
&lt;/style&gt;
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-javascript"># colorComponent.vue

&lt;template&gt;
  &lt;p :class="[color]"&gt;This is an example of deeply nested props!&lt;/p&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    props: {
      color: String,
    },
  };
&lt;/script&gt;
&lt;style&gt;
  .blue {
    color: blue;
  }
  .red {
    color: red;
  }
  .green {
    color: green;
  }
&lt;/style&gt;
</code></pre>
</div>

Here, we have a landing page with a dropdown containing a list of colors and we’re passing the selected `color` to `childComponent.vue` as a prop. This child component also has a `msg` prop that accepts a text to display in the template section. Finally, this component has a child component (`colorComponent.vue`) that accepts a `color` prop from the parent component which is used in determining the class for the text in this component. This is an example of passing data through all the components.

But with Vue 3, we can do this in a cleaner and short way using the new Provide and inject pair. As the name implies, we use `provide` as either a function or an object to make data available from a parent component to any of its nested component regardless of how deeply nested such a component is. We make use of the object form when passing hard-coded values to `provide` like this;

<div class="break-out">

 <pre><code class="language-javascript"># parentComponent.vue

&lt;template&gt;
  &lt;div class="home"&gt;
    &lt;img alt="Vue logo" src="../assets/logo.png" /&gt;
    &lt;HelloWorld msg="Vue 3 is liveeeee!" :color="color" /&gt;
    &lt;select name="color" id="color" v-model="color"&gt;
      &lt;option value="" disabled selected&gt; Select a color&lt;/option&gt;
      &lt;option :value="color" v-for="(color, index) in colors" :key="index"&gt;{{
        color
      }}&lt;/option&gt;&lt;/select
    &gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import HelloWorld from "@/components/HelloWorld.vue";
  export default {
    name: "Home",
    components: {
      HelloWorld,
    },
    data() {
      return {
        colors: ["red", "blue", "green"],
      };
    },
    provide: {
      color: 'blue'
    }
  };
&lt;/script&gt;
</code></pre>
</div>

But for instances where you need to pass a component instance property to `provide`, we use the function mode so this is possible;

<div class="break-out">

 <pre><code class="language-javascript"># parentComponent.vue

&lt;template&gt;
  &lt;div class="home"&gt;
    &lt;img alt="Vue logo" src="../assets/logo.png" /&gt;
    &lt;HelloWorld msg="Vue 3 is liveeeee!" /&gt;
    &lt;select name="color" id="color" v-model="selectedColor"&gt;
      &lt;option value="" disabled selected&gt; Select a color&lt;/option&gt;
      &lt;option :value="color" v-for="(color, index) in colors" :key="index"&gt;{{
        color
      }}&lt;/option&gt;&lt;/select
    &gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import HelloWorld from "@/components/HelloWorld.vue";
  export default {
    name: "Home",
    components: {
      HelloWorld,
    },
    data() {
      return {
        selectedColor: "blue",
        colors: ["red", "blue", "green"],
      };
    },
    provide() {
      return {
        color: this.selectedColor,
      };
    },
  };
&lt;/script&gt;
</code></pre>
</div>

Since we don’t need the `color` props in both the `childComponent.vue` and `colorComponent.vue`, we’re getting rid of it. The good thing about using `provide` is that the parent component does not need to know which component needs the property it is providing.

To make use of this in the component that needs it in this case, `colorComponent.vue` we do this;

<div class="break-out">

 <pre><code class="language-javascript"># colorComponent.vue

&lt;template&gt;
  &lt;p :class="[color]"&gt;This is an example of deeply nested props!&lt;/p&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    inject: ["color"],
  };
&lt;/script&gt;
&lt;style&gt;
  .blue {
    color: blue;
  }
  .red {
    color: red;
  }
  .green {
    color: green;
  }
&lt;/style&gt;
</code></pre>
</div>

Here, we use `inject` which takes in an array of the required variables the component needs. In this case, we only need the `color` property so we only pass that. After that, we can use the `color` the same way we use it when using props.

We might notice that if we try to select a new color using the dropdown, the color does not update in `colorComponent.vue` and this is because by default the properties in `provide` are not reactive. To Fix that, we make use of `computed` method.

<div class="break-out">

 <pre><code class="language-javascript"># parentComponent.vue

&lt;template&gt;
  &lt;div class="home"&gt;
    &lt;img alt="Vue logo" src="../assets/logo.png" /&gt;
    &lt;HelloWorld msg="Vue 3 is liveeeee!" /&gt;
    &lt;select name="color" id="color" v-model="selectedColor"&gt;
      &lt;option value="" disabled selected&gt; Select a color&lt;/option&gt;
      &lt;option :value="color" v-for="(color, index) in colors" :key="index"&gt;{{
        color
      }}&lt;/option&gt;&lt;/select
    &gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import HelloWorld from "@/components/HelloWorld.vue";
  import { computed } from "vue";
  export default {
    name: "Home",
    components: {
      HelloWorld,
    },
    data() {
      return {
        selectedColor: "",
        todos: ["Feed a cat", "Buy tickets"],
        colors: ["red", "blue", "green"],
      };
    },
    provide() {
      return {
        color: computed(() =&gt; this.selectedColor),
      };
    },
  };
&lt;/script&gt;
</code></pre>
</div>

Here, we import [`computed`](https://v3.vuejs.org/guide/reactivity-computed-watchers.html#computed-values) and pass our `selectedColor` so that it can be reactive and update as the user selects a different color. When you pass a variable to the computed method it returns an object which has a `value`. This property holds the *value* of your variable so for this example, we would have to update `colorComponent.vue` to look like this;

<div class="break-out">

 <pre><code class="language-javascript"># colorComponent.vue

&lt;template&gt;
  &lt;p :class="[color.value]"&gt;This is an example of deeply nested props!&lt;/p&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    inject: ["color"],
  };
&lt;/script&gt;
&lt;style&gt;
  .blue {
    color: blue;
  }
  .red {
    color: red;
  }
  .green {
    color: green;
  }
&lt;/style&gt;
</code></pre>
</div>

Here, we change `color` to `color.value` to represent the change after making `color` reactive using the `computed` method. At this point, the `class` of the text in this component would always change whenever `selectedColor` changes in the parent component.

{{% feature-panel %}}

## Teleport

There are instances where we create components and place them in one part of our application because of the logic the app uses but are intended to be displayed in another part of our application. A common example of this would be a modal or a popup that is meant to display and cover the whole screen. While we can create a workaround for this using CSS’s `position`  property on such elements, with Vue 3, we can also do using using Teleport.

Teleport allows us to take a component out of its original position in a document, from the default `#app` container Vue apps are wrapped in and move it to any existing element on the page it’s being used. A good example would be using Teleport to move an header component from inside the `#app` div to an `header` It is important to note that you can only Teleport to elements that are existing outside of the Vue DOM. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f57653-0c97-49c4-ac2a-d1623f60d045/error-message-vue3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f57653-0c97-49c4-ac2a-d1623f60d045/error-message-vue3.png" sizes="100vw" caption="Teleport error message in console: Invalid Teleport target error message in terminal. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f57653-0c97-49c4-ac2a-d1623f60d045/error-message-vue3.png'>Large preview</a>)" alt="error message in console when you teleport to an invalid element" >}}

The Teleport component accepts two props that determine the behavior of this component and they are;

1. `to`  
This prop accepts either a class name, an id, an element or a [data-&#42;](https://www.w3schools.com/tags/att_data-.asp) attribute. We can also make this value dynamic by passing a `:to` prop as opposed to `to` and change the Teleport element dynamically.
2. `:disabled`  
This prop accepts a `Boolean` and can be used to toggle the Teleport feature on an element or component. This can be useful for dynamically changing the position of an element.

An ideal example of using Teleport looks like this;

<div class="break-out">

 <pre><code class="language-javascript"># index.html**

&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="utf-8" /&gt;
    &lt;meta http-equiv="X-UA-Compatible" content="IE=edge" /&gt;
    &lt;meta name="viewport" content="width=device-width,initial-scale=1.0" /&gt;
    &lt;link rel="icon" href="&lt;%= BASE_URL %&gt;favicon.ico" /&gt;
    &lt;title&gt;
        &lt;%= htmlWebpackPlugin.options.title %&gt;
    &lt;/title&gt;
&lt;/head&gt;
&lt;!-- add container to teleport to --&gt;
&lt;header class="header"&gt;&lt;/header&gt;
&lt;body&gt;
    &lt;noscript&gt;
      &lt;strong
        &gt;We're sorry but &lt;%= htmlWebpackPlugin.options.title %&gt; doesn't work
        properly without JavaScript enabled. Please enable it to
        continue.&lt;/strong
      &gt;
    &lt;/noscript&gt;
    &lt;div id="app"&gt;&lt;/div&gt;
    &lt;!-- built files will be auto injected --&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

In the default `index.html` file in your Vue app, we add an `header` element because we want to Teleport our header component to that point in our app. We also added a class to this element for styling and for easy referencing in our Teleport component.

<pre><code class="language-javascript"># Header.vue**

&lt;template&gt;
  &lt;teleport to="header"&gt;
    &lt;h1 class="logo"&gt;Vue 3 🥳&lt;/h1&gt;
    &lt;nav&gt;
      &lt;router-link to="/"&gt;Home&lt;/router-link&gt;
    &lt;/nav&gt;
  &lt;/teleport&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    name: "app-header",
  };
&lt;/script&gt;
&lt;style&gt;
  .header {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .logo {
    margin-right: 20px;
  }
&lt;/style&gt;
</code></pre>

Here, we create the header component and add a logo with a link to the homepage on our app. We also add the Teleport component and give the `to` prop a value of `header` because we want this component to render inside this element. Finally, we import this component into our app;

<pre><code class="language-javascript"># App.vue

&lt;template&gt;
  &lt;router-view /&gt;
  &lt;app-header&gt;&lt;/app-header&gt;
&lt;/template&gt;
&lt;script&gt;
  import appHeader from "@/components/Header.vue";
  export default {
    components: {
      appHeader,
    },
  };
&lt;/script&gt;
</code></pre>

In this file, we import the header component and place it in the template so it can be visible in our app.

Now if we inspect the element of our app, we would notice that our header component is inside the `header`element;

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9b8adad-ba8d-42bd-9d7d-921410f20d7a/teleported-element-vue3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9b8adad-ba8d-42bd-9d7d-921410f20d7a/teleported-element-vue3.png" sizes="100vw" caption="Header component in DevTools (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9b8adad-ba8d-42bd-9d7d-921410f20d7a/teleported-element-vue3.png'>Large preview</a>)" alt="Header component in DevTools" >}}

{{% ad-panel-leaderboard %}}

## Fragments

With Vue 2.x, it was impossible to have multiple root elements in the `template` of your file and as a workaround, developers started wrapping all elements in a parent element. While this doesn’t look like a serious issue, there are instances where developers want to render a component without a container wrapping around such elements but have to make do with that.

With Vue 3, a new feature called Fragments was introduced and this feature allows developers to have multiple elements in their root template file. So with Vue 2.x, this is how an input field container component would look like;

<pre><code class="language-javascript"># inputComponent.vue

&lt;template&gt;
  &lt;div&gt;
    &lt;label :for="label"&gt;label&lt;/label&gt;
    &lt;input :type="type" :id="label" :name="label" /&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    name: "inputField",
    props: {
      label: {
        type: String,
        required: true,
      },
      type: {
        type: String,
        required: true,
      },
    },
  };
&lt;/script&gt;
&lt;style&gt;&lt;/style&gt;
</code></pre>

Here, we have a simple form element component that accepts two props, `label` and `type`, and the template section of this component is wrapped in a div. This is not necessarily an issue but if you want the label and input field to be directly inside your `form` element. With Vue 3, developers can easily rewrite this component to look like this;

<pre><code class="language-javascript"># inputComponent.vue

&lt;template class="testingss"&gt;
  &lt;label :for="label"&gt;{{ label }}&lt;/label&gt;
  &lt;input :type="type" :id="label" :name="label" /&gt;
&lt;/template&gt;
</code></pre>

With a single root node, ***attributes*** are always attributed to the root node and they are also known as [**Non-Prop Attributes**](https://v3.vuejs.org/guide/component-attrs.html#non-prop-attributes)**.** They are events or attributes passed to a component that do not have corresponding properties defined in `props` or `emits`. Examples of such attributes are `class` and `id`. It is, however, required to explicitly define which of the elements in a multi-root node component should be attributed to. 

Here’s what this means using the `inputComponent.vue` from above;

1. When adding `class` to this component in the parent component, it must be specified which component would this `class` be attributed to otherwise the attribute has no effect.
    

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="home"&gt;
    &lt;div&gt;
      &lt;input-component
        class="awesome__class"
        label="name"
        type="text"
      &gt;&lt;/input-component&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;style&gt;
  .awesome__class {
    border: 1px solid red;
  }
&lt;/style&gt;
</code></pre>

When you do something like this without defining where the attributes should be attributed to, you get this warning in your console;

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfecbf5-f21a-4639-ab39-6c04e598e9af/fragments-warning-message.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfecbf5-f21a-4639-ab39-6c04e598e9af/fragments-warning-message.png" sizes="100vw" caption="Error message in terminal when attributes are not distributed (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfecbf5-f21a-4639-ab39-6c04e598e9af/fragments-warning-message.png'>Large preview</a>)" alt="error message in terminal when attributes are not distributed" >}}

And the `border` has no effect on the component;

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7947b504-5573-4387-b5bd-1706ddbb119f/inputcomponent-vue3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7947b504-5573-4387-b5bd-1706ddbb119f/inputcomponent-vue3.png" sizes="100vw" caption="Component without attribute distribution (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7947b504-5573-4387-b5bd-1706ddbb119f/inputcomponent-vue3.png'>Large preview</a>)" alt="component without attribute distribution" >}}

2. To fix this, add a `v-bind="$attrs"` on the element you want such attributes to be distributed to;

<pre><code class="language-javascript">&lt;template&gt;
  &lt;label :for="label" v-bind="$attrs"&gt;{{ label }}&lt;/label&gt;
  &lt;input :type="type" :id="label" :name="label" /&gt;
&lt;/template&gt;
</code></pre>

Here, we’re telling Vue that we want the attributes to be distributed to the `label` element which means we want the `awesome__class` to be applied to it. Now, if we inspect our element in the browser we would see that the class has now been added to `label` and hence a border is now around the label.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e25f0a6-014e-4491-a2ee-7aa9413fd15e/attribute-distributed-vue3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e25f0a6-014e-4491-a2ee-7aa9413fd15e/attribute-distributed-vue3.png" sizes="100vw" caption="Component with attribute distribution (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e25f0a6-014e-4491-a2ee-7aa9413fd15e/attribute-distributed-vue3.png'>Large preview</a>)" alt="component with attribute distribution" >}}

## Global API

It was not uncommon to see `Vue.component` or `Vue.use` in `main.js` file of a Vue application. These types of methods are known are Global APIs and there are quite a number of them in Vue 2.x. One of the challenges of this method is that it makes it impossible to isolate certain functionalities to one instance of your app (if you have more than one instance in your app) without it affecting other apps because they are all mounted on Vue. This is what I mean;

<pre><code class="language-javascript">Vue.directive('focus', {
  inserted: el =&gt; el.focus()
})

Vue.mixin({
  /&#42; ... &#42;/
})

const app1 = new Vue({ el: '#app-1' })
const app2 = new Vue({ el: '#app-2' })
</code></pre>

For the above code, it is impossible to state that the [Vue Directive](https://v3.vuejs.org/guide/custom-directive.html) be associated with `app1` and the Mixin with `app2` but instead, they’re both available in the two apps.

Vue 3 comes with a new Global API in an attempt to fix this type of problem with the introduction of `createApp`. This method returns a new instance of a Vue app. An app instance exposes a subset of the current global APIs. With this, all APIs (component, mixin, directive, use, etc) that mutate `Vue` from Vue 2.x are now going to be moved to individual app instances and now, each instance of your Vue app can have functionalities that are unique to them without affecting other existing apps.

Now, the above code can be rewritten as;

<pre><code class="language-javascript">const app1 = createApp({})
const app2 = createApp({})
app1.directive('focus', {
    inserted: el => el.focus()
})
app2.mixin({
    /&#42; ... &#42;/
})
</code></pre>

It is however possible to create functionalities that you want to be share among all your apps and this can be done by using a [factory function](https://medium.com/javascript-scene/javascript-factory-functions-with-es6-4d224591a8b1#:~:text=A%20factory%20function%20is%20any,keyword%2C%20it's%20a%20factory%20function.).

{{% ad-panel-leaderboard %}}

## Events API

One of the most common ways developers adopted for passing data among components that don’t have a parent to child relationship other than using the [Vuex Store](https://vuex.vuejs.org/) is the use of [Event Bus](https://css-tricks.com/using-event-bus-to-share-props-between-vue-components/). One of the reasons why this method is common is because of how easy it is to get started with it;

<pre><code class="language-javascript"># eventBus.js

const eventBus = new Vue()

export default eventBus;
</code></pre>

After this, the next thing would be to import this file into `main.js` to make it globally available in our app or to import it in files that you need it;

<pre><code class="language-javascript"># main.js

import eventBus from 'eventBus'
Vue.prototype.$eventBus = eventBus
</code></pre>

Now, you can emit events and listen for emitted events like this;

<pre><code class="language-javascript">this.$eventBus.$on('say-hello', alertMe)
this.$eventBus.$emit('pass-message', 'Event Bus says Hi')
</code></pre>

There is a lot of Vue codebase that is filled with code like this. However, with Vue 3, it would be impossible to do because `$on`, `$off`, and `$once` have all been removed but `$emit` is still available because it is required for children component to emit events to their parent components. An alternative to this would be using `provide / inject` or any of the recommended [third-party libraries](https://v3.vuejs.org/guide/migration/events-api.html#migration-strategy).

## Conclusion

In this article, we have covered how you can pass data around from a parent component down to a deeply nested child component using the `provide / inject` pair. We have also looked at how we can reposition and transfer components from one point in our app to another. Another thing we looked at is the multi-root node component and how to ensure we distribute attributes so they work properly. Finally, we also covered the changes to the Events API and Global API.

### Further Resources

- “[JavaScript Factory Functions with ES6+](https://medium.com/javascript-scene/javascript-factory-functions-with-es6-4d224591a8b1#:~:text=A%20factory%20function%20is%20any,keyword%2C%20it's%20a%20factory%20function),” Eric Elliott, Medium
- “[Using Event Bus to Share Props Between Vue Components](https://css-tricks.com/using-event-bus-to-share-props-between-vue-components/),” Kingsley Silas, CSS-Tricks
- [Using Multiple Teleports On The Same Target](https://v3.vuejs.org/guide/teleport.html#using-multiple-teleports-on-the-same-target), Vue.js Docs
- [Non-Prop Attributes](https://v3.vuejs.org/guide/component-attrs.html#non-prop-attributes), Vue.js Docs
- [Working With Reactivity](https://v3.vuejs.org/guide/component-provide-inject.html#working-with-reactivity), Vue.js Docs
- [`teleport`](https://v3.vuejs.org/api/built-in-components.html#teleport), Vue.js Docs
- [Fragments](https://v3.vuejs.org/guide/migration/fragments.html), Vue.js Docs
- [2.x Syntax](https://v3.vuejs.org/guide/migration/events-api.html#_2-x-syntax), Vue.js Docs

{{< signature "ks, ra, il" >}}
