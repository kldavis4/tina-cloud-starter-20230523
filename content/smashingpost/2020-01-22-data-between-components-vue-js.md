---
title: 'How To Pass Data Between Components In Vue.js'
slug: data-components-vue-js
author: matt-maribojoc
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3913ad56-67ad-4800-bcb3-d3b5614ca724/data-components-vue-js-sharing-card.png
date: 2020-01-22T13:00:00.000Z
summary: >-
  With so many different ways to share data across components, you should know which technique is best for your situation. Let’s analyze three of the most common ways to pass data in VueJS.
description: >-
  With so many different ways to share data across components, you should know which technique is best for your situation. Let’s analyze three of the most common ways to pass data in VueJS.
categories:
  - Vue
  - JavaScript
---
Sharing data across components is one of the core functionalities of VueJS. It allows you to design a more modular project, control data scopes, and create a natural flow of data across your app.

Unless you’re creating your entire Vue app in one component (which wouldn’t make any sense), you’re going to encounter situations where you need to share data between components.

By the end of this tutorial, you will know three ways to get this done.

<ul>
<li><a href="#propos-share-data-parent-child">Using props to share data</a> from parent to child,</li>
<li><a href="#emitting-custom-events-share-data-child-parent">Emitting custom events</a> to share data from child to parent,</li>
<li><a href="#vuex-application-level-shared-state">Using Vuex</a> to create an app-level shared state.</li>
</ul>
 
<p>Okay &mdash; let’s get right into it!</p>

<div class="c-felix-the-cat">
<h4 class="h3">Building An App With Nuxt</h4>
<p>With Spotify, your friends can check out what you’re jamming to. What if the rest of the Internet could experience your algo-rhythm, too? Learn how to compose your own app to share what you’re listening to on Spotify using Vue.js and Nuxt. <a href="https://www.smashingmagazine.com/2019/03/spotify-app-vue-nuxt-javascript/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## 1. Using Props To Share Data From Parent To Child

<p>VueJS props are the simplest way to share data between components. Props are custom attributes that we can give to a component. Then, in our template, we can give those attributes values and &mdash; BAM &mdash; we’re passing data from a parent to a child component!</p>

<p>For example, let’s say we’re working on a user profile page and want to have a child component accept a username prop. We’ll need two components.</p>

<ol>
<li>The child component accepting the prop, let’s call this <code>AccountInfo.vue</code>.</li>
<li>The parent component passing the prop, let’s call this <code>ProfilePage.vue</code>.</li>
</ol>

<p>Inside <code>AccountInfo.vue</code>, we can declare the props it accepts using the props option. So, inside the component options, let’s make it look like the following.</p>

<pre><code class="language-javascript">// AccountInfo.vue

&lt;template&gt;
 &lt;div id='account-info'&gt;
   {{username}}
 &lt;/div&gt;
&lt;/template&gt;
 
&lt;script&gt;
export default {
 props: ['username']
}
&lt;/script&gt;</code></pre>

<p>Then, to actually pass the data from the parent (<code>ProfilePage.vue</code>), we pass it like a custom attribute.</p>

<pre><code class="language-javascript">// ProfilePage.vue
 
&lt;account-info username='matt' /&gt;</code></pre>

<p>Now if we load our page, we can see that our <code>AccountInfo</code> component properly renders the value passed in by its parent.</p>

<p>As when working with other VueJS directives, we can use v-bind to dynamically pass props. For example, let’s say we want to set the username prop to be equal to a variable. We can accomplish this by using shorthand for the v-bind directive (or just <code>:</code> for short). The code would look a little like this:</p>

<pre><code class="language-javascript">&lt;template&gt;
 &lt;div&gt;
   &lt;account-info :username="user.username" /&gt;
 &lt;/div&gt;
&lt;/template&gt;
 
&lt;script&gt;
import AccountInfo from "@/components/AccountInfo.vue";
 
export default {
 components: {
   AccountInfo
 },
 data() {
   return {
     user: {
       username: 'matt'
     }
   }
 }
}
&lt;/script&gt;</code></pre>

<p>This means that we can change our data and have any child props using that value will also update.</p>

### Tip: Always Verify Your Props

<p>If you’re looking to write clearer Vue code, an important technique is to verify your props. In short, this means that you need to specify the requirements for your prop (i.e. type, format, and so on). If one of these requirements is not met (e.g. if the prop is passed an incorrect type), Vue will print out a warning.</p>

<p>Let’s say we want our username prop to only accept Strings. We would have to modify our props object to look like this:</p> 

<pre><code class="language-javascript">export default {
 props: {
   username: String
 }
}</code></pre>

<p>Verifying props is essential when working in large-scale Vue apps or when designing plugins. It helps ensure that everyone is on the same page and use props the way that they were intended.</p>

<p>For a full list of the verifications we can include on props, I’d definitely recommend checking out the official documentation for an in-depth review.</p>

### Tip: Follow Prop Naming Conventions

<p>According to the VueJS style guide, the best way to name your props is by using <code>camelCase</code> when declaring them in your script and kebab-case when referencing them in template code.</p>

<p>The reasoning behind this is actually quite simple. In Javascript, <code>camelCase</code> is the standard naming convention and in HTML, it’s kebab-case.</p>

<p>So, Vue recommends that we stick to the norms of each language. Thankfully, Vue is able to automatically convert between the two styles so there’s no additional setup for developers.</p>

<pre><code class="language-javascript">// GOOD
&lt;account-info :my-username="user.username" /&gt;
props: {
   myUsername: String
}
 
// BAD
&lt;account-info :myUsername="user.username" /&gt;
props: {
   "my-username": String
}</code></pre>

{{% ad-panel-leaderboard %}}

## 2. Emitting Events To Share Data From Child To Parent

<p>Now that we have data passing down the hierarchy, let’s pass it the other way: from a child component to a parent. We can’t use props, but we can use custom events and listeners.</p>

<p>Every Vue instance can call a <code>.$emit(eventName)</code> method that triggers an event. Then, we can listen for this event in the same way as any other, using the v-on directive.</p>

### Creating a Custom Event

<p>Let’s build on our user profile example by adding a button that changes the username. Inside our child component (<code>AccountInfo.vue</code>), let’s create the button.</p>

<p>Then, when this button is clicked, we’ll emit an event called <code>changeUsername</code>.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
 &lt;div id='account-info'&gt;
   &lt;button @click='changeUsername()'&gt;Change Username&lt;/button&gt;
   {{username}}
 &lt;/div&gt;
&lt;/template&gt;
 
&lt;script&gt;
export default {
 props: {
   username: String
 },
 methods: {
   changeUsername() {
     this.$emit('changeUsername')
   }
 }
}
&lt;/script&gt;</code></pre>
</div>
 
<p>Inside the parent, we handle this event and change the <code>user.username</code> variable. Like we were discussing earlier, we can listen to events using the v-on directive or "@" for short.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
 &lt;div&gt;
   &lt;account-info :username="user.username" @changeUsername="user.username = 'new name'"/&gt;
 &lt;/div&gt;
&lt;/template&gt;</code></pre>
</div>

<p>Let’s try it out. You should see that when you click the button, the username changes to "new name".</p>

### Tip: Custom Events Can Accept Arguments

<p>The most common use case for passing arguments to your events is when you want a child component to be able to set a specific value for its prop. You <strong>never</strong> want to directly edit the value of a prop from the component itself.</p>

<p>However, luckily we can use pass arguments with our custom events to make the parent component change values.</p>

<p>Let’s say we want to modify the <code>changeUsername</code> event so that we can pass it a value.</p>

<p>The <code>$emit</code> method takes an optional second parameter for arguments. So all we do is add our new username value after the name of our event.</p>

<pre><code class="language-javascript">this.$emit('changeUsername', 'mattmaribojoc')</code></pre>

<p>Then, in our parent component, we can either access these values inline by using a special <code>$event</code> variable, or we can write a handler method that takes a parameter.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;account-info :username="user.username" @changeUsername="user.username = $event"/&gt;
 
OR 
 
&lt;account-info :username="user.username" @changeUsername="changeUsername($event)"/&gt;
 
export default {
...
methods: {
   changeUsername (username) {
     this.user.username = username;
   }
}
}</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## 3. Using Vuex To Create An Application-Level Shared State

<p>Okay &mdash; we know how to share data between parents/children, but what about other components? Do we have to create an extremely complex hierarchy system if we want to pass data?</p>

<p>Thankfully not. The wonderful Vuex state management library has been simplifying developers' lives for years. In short, it creates a centralized data store that is accessible by all components.</p>

<p>In the methods we used previously (props / emitting events), each component has its own data state that we then share between components. However, Vuex lets us extract all the shared data into a single state that each component can access easily. This shared state is called a store.</p>

<p><strong>Let’s try it out.</strong></p>

<p>Because Vuex is separate from the core code of Vue, we’ll first have to install and import it into our project. First, we’ll have to run <code>npm install vuex --save</code> inside our project CLI.</p>

<p>Then, create a src/store folder with an index.js file that contains the following code.</p>

<pre><code class="language-javascript">// store/index.js
 
import Vue from "vue";
import Vuex from "vuex";
 
Vue.use(Vuex);
 
export default new Vuex.Store({
 state: {},
 getters: {},
 mutations: {},
 actions: {}
});</code></pre>

<p>To include this in our root Vue instance, we have to import our store/index.js file and pass it in our Vue constructor.</p>

<pre><code class="language-javascript">// main.js
 
import store from "./store";
 
new Vue({
  store,
  ...</code></pre>
  
### Accessing Vue Store Inside Components

<p>Since we added our Vuex store onto our root Vue instance, it gets injected into all of the root’s children. If we want to access the store from a component, we can via <code>this.$store</code>.</p>

<p>Now, let’s dive into the specifics of each of the four parts of a Vuec store.</p>

### 1. State

<p>The Vuex state is an object that contains application-level data. All Vue instances will be able to access this data.</p>

<p>For our store, let’s create a user object that stores some more user profile data.</p>

<pre><code class="language-javascript">export default new Vuex.Store({
 state: {
   user: {
     username: 'matt',
     fullName: 'Matt Maribojoc'
   }
 },
 getters: {},
 mutations: {},
 actions: {}
});</code></pre>

<p>We can access this data inside any instance component like this.</p>

<pre><code class="language-javascript">mounted () {
   console.log(this.$store.state.user.username);
},</code></pre>

### 2. Getters

<p>We use Vuex getters to return a modified value of state data. A good way to think of getters is to treat them like computed properties. For example, getters, like computed properties, cache their results and only re-evaluate when a dependency is modified.</p>
 
<p>Building onto our earlier store, let’s say we want to make a method that returns a user’s first name based off the full name attribute.</p>

<pre><code class="language-javascript">getters: {
   firstName: state => {
     return state.user.fullName.split(' ')[0]
   }
 }</code></pre>
 
 <p>Vuex getter properties are available to components on the <code>store.getters</code> object.</p>
 

 <pre><code class="language-javascript">mounted () {
   console.log(this.$store.getters.firstName);
}</code></pre>

#### Tip: Know the Default Getter Arguments

<p>By default, Vuex getters accept two arguments.</p>

<ol>
<li>state &mdash; the state object for our application;</li>
<li>getters &mdash; the store.getters object, meaning that we can call other getters in our store.</li>
</ol>

<p>Every getter you declare will require the first state argument. And depending on how you design your code, your getters can reference each other using the second 'getters' argument.</p>

<p>Let’s make a last name getter that simply removes our first name value from our full name state property. This example would require both the state and getters objects.</p>

<div class="break-out">

<pre><code class="language-javascript">lastName (state, getters) {
     return state.user.fullName.replace(getters.firstName, '');
}</code></pre>
</div>

#### Tip: Pass Custom Arguments to Vuex Getters

<p>Another cool feature of getters is that we can pass them custom arguments by making our getter return a method.</p>

<pre><code class="language-javascript">prefixedName: (state, getters) => (prefix) => {
     return prefix + getters.lastName;
}
 
// in our component
console.log(this.$store.getters.prefixedName("Mr."));</code></pre>

### 3. Mutations

<p>Mutations are the <strong>only</strong> way to properly change the value of the state object. An important detail to note is that mutations <strong>must be synchronous</strong>.</p>

<p>Like getters, mutations always accept the Vuex state property as their first argument. They also accept a custom argument &mdash; called a payload &mdash; as the second argument.</p>

<p>For example, let’s make a mutation to change a user’s name to a specific value.</p>

<pre><code class="language-javascript">mutations: {
   changeName (state, payload) {
     state.user.fullName = payload
   }
},</code></pre>

<p>Then, we can call this method from our component using the <code>store.commit</code> method, with our payload as the second argument.</p>

<pre><code class="language-javascript">this.$store.commit("changeName", "New Name");</code></pre>

<p>More often than not, you are going to want your payload to be an object. Not only does this mean that you can pass several arguments to a mutation, but also, it makes your code more readable because of the property names in your object.</p>

<pre><code class="language-javascript">changeName (state, payload) {
     state.user.fullName = payload.newName
}</code></pre>

<p>There are two different ways to call mutations with a payload.</p>

<ol>
<li>You can have the mutation type as the first argument and the payload as the second.</li>
<li>You can declare pass a single object, with one property for the type and another for the payload.</li>
</ol>

<pre><code class="language-javascript">this.$store.commit("changeName", {
       newName: "New Name 1",
});
 
     // or
 
 this.$store.commit({
       type: "changeName",
       newName: "New Name 2"
});</code></pre>

<p>There isn’t a real difference between how the two work so it’s totally up to personal preference. Remember that it’s always best to be consistent throughout your entire project, so whichever one you choose, stick with it!</p>

### 4. Actions

<p>In Vuex, actions are fairly similar to mutations because we use them to change the state. However, actions don’t change the values themselves. Instead, actions commit mutations.</p>

<p>Also, while Vuex mutations have to be synchronous, actions do not. Using actions, we can call a mutation after an API call, for example.</p>

<p>Whereas most of the Vuex handlers we’ve seen accept state as their main parameter, actions accept a context object. This context object allows us to access the properties in our Vuex store (e.g. state, commit, getters).</p>

<p>Here’s an example of a Vuex action that waits two seconds and then commits the <code>changeName</code> mutation.</p>

<pre><code class="language-javascript">actions: {
   changeName (context, payload) {
     setTimeout(() => {
       context.commit("changeName", payload);
     }, 2000);
   }
}</code></pre>

<p>Inside our components, we use the store.dispatch method in order to run our function. We pass arguments just like we did with mutations. We declare the type and we pass any custom arguments in the second argument.</p>

<pre><code class="language-javascript">this.$store.dispatch("changeName", {
      newName: "New Name from Action"
});</code></pre>

## Wrapping Up

<p>Now, you should know three different ways to share data across components in VueJS: props, custom events, and a Vuex store.</p>

<p>I hope this tutorial helped give you some more insight into some different Vue methods and best practices. Let me know how you’ve implemented them into your projects!</p>

### Further Reading

<p>If you’re interested in going even deeper into the technical side/capabilities of each technique, here are some great places to start.</p>

<ul>
<li><a href="https://vuex.vuejs.org/guide">Vuex Official Guide</a> website</li>
<li>VueJS Docs for <a href="https://vuejs.org/v2/guide/components-props.html">Props</a> and <a href="https://vuejs.org/v2/guide/components-custom-events.html">Custom Events</a></li>
<li>“<a href="https://vuejsdevelopers.com/2017/05/15/vue-js-what-is-vuex/">WTF Is Vuex? A Beginner’s Guide To Vue’s Application Data Store</a>,” Anthony Gore, Vue.js Developers</li>
</ul>

{{< signature "dm, yk, il" >}}
