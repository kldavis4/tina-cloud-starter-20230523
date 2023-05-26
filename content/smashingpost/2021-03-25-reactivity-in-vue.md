---
title: 'Reactivity In Vue'
slug: reactivity-in-vue
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ed0a8b-a98c-4689-a7a1-6117ec1642a3/reactivity-in-vue.jpg
date: 2021-03-25T10:00:00.000Z
summary: >-
  Reactivity is the ability for a variable (array, string, number, object, etc) to update when its value or any other variable that it makes reference to is changed after declaration.
description: >-
  Reactivity is the ability for a variable (array, string, number, object, etc) to update when its value or any other variable that it makes reference to is changed after declaration.
categories:
  - Vue
  - JavaScript
  - Frameworks
---

In this article, we’re going to look at reactivity in Vue, how it works, and how we can create reactive variables using newly created methods and functions. This article is targeted at developers who have a good understanding of how Vue 2.x works and are looking to get familiar with the new [Vue 3](https://v3.vuejs.org/).

We’re going to build a simple application to better understand this topic. The code for this app can be found [on GitHub](https://github.com/Timibadass/vue-reactivity).

By default, **JavaScript isn’t reactive**. This means that if we create the variable `boy` and reference it in part A of our application, then proceed to modify `boy` in part B, part A will not update with the new value of `boy`.

<pre><code class="language-javascript">let framework = 'Vue';
let sentence = `${framework} is awesome`;
console.log(sentence)
 // logs "Vue is awesome"
framework = 'React';
console.log(sentence)
//should log "React is awesome" if 'sentence' is reactive.</code></pre>

The snippet above is a perfect example of the non-reactive nature of JavaScript &mdash; hence, why the change isn’t reflected in the `sentence` variable.

In Vue 2.x, `props`, `computed`, and `data()` were all reactive by default, with the exception of properties that are not present in `data` when such components are created. This means that when a component is injected into the [DOM](https://en.wikipedia.org/wiki/Document_Object_Model), only the [existing properties in the component](https://vuejs.org/v2/guide/instance.html#Data-and-Methods)’s [`data`](https://vuejs.org/v2/guide/instance.html#Data-and-Methods) object would cause the component to update if and when such properties change.

Internally, Vue 3 uses the [`Proxy` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) (an ECMAScript 6 feature) to ensure that these properties are reactive, but it still provides the option to use `Object.defineProperty` from [Vue 2](https://vuejs.org/v2/guide/reactivity.html#How-Changes-Are-Tracked) for Internet Explorer support (ECMAScript 5). This method defines a new property directly on an object, or modifies an existing property on an object, and returns the object.

At first glance and since most of us already know that reactivity is not new in Vue, it might seem unnecessary to make use of these properties, but the Options API has its limitations when you’re dealing with a large application with reusable functions in several parts of the application. To this end, the new [Composition API](https://v3.vuejs.org/guide/composition-api-introduction.html) was introduced to help with abstracting logic in order to make a code base easier to read and maintain. Also, we can now easily make any variable reactive regardless of its [data type](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures) using any of the new properties and methods.

When we use the `setup` option, which serves as the entry point for the Composition API, the `data` object, `computed` properties, and `methods` are inaccessible because the component instance has not yet been created when `setup` is executed. This makes it impossible to take advantage of the **built-in reactivity** in any of these features in `setup`. In this tutorial, we’re going to learn about all of the ways we can do this.

{{% feature-panel %}}

## The Reactive Method

According to the documentation, the `reactive` method, which is the equivalent of `Vue.observable()` in Vue 2.6, can be useful when we’re trying to create an object all of whose properties are reactive (such as the `data` object in the Options API). Under the hood, the `data` object in the Options API uses this method to make all of the properties in it reactive.

But we can create our own reactive object like this:

<div class="break-out">

<pre><code class="language-javascript">import { reactive } from 'vue'

// reactive state
let user = reactive({
        "id": 1,
        "name": "Leanne Graham",
        "username": "Bret",
        "email": "Sincere@april.biz",
        "address": {
            "street": "Kulas Light",
            "suite": "Apt. 556",
            "city": "Gwenborough",
            "zipcode": "92998-3874",
            "geo": {
                "lat": "-37.3159",
                "lng": "81.1496"
            }
        },
        "phone": "1-770-736-8031 x56442",
        "website": "hildegard.org",
        "company": {
            "name": "Romaguera-Crona",
            "catchPhrase": "Multi-layered client-server neural-net",
            "bs": "harness real-time e-markets"
        },
        "cars": {
            "number": 0
        }
    })</code></pre>
</div>

Here, we imported the `reactive` method from Vue, and then we declared our `user` variable by passing its value to this function as an argument. In doing so, we’ve made `user` reactive, and, thus, if we use `user` in our template and if either the object or a property of this object should change, then this value will get automatically updated in this template.

## `ref`

Just as we have a method for making objects reactive, we also need one to make **other standalone primitive values** (strings, booleans, undefined values, numbers, etc.) and arrays reactive. During development, we would work with these other data types while also needing them to be reactive. The first approach we might think of would be to use `reactive` and pass in the value of the variable that we want to make reactive.

<pre><code class="language-javascript">import { reactive } from 'vue'

const state = reactive({
  users: [],
});</code></pre>

Because `reactive` has deep reactive conversion, `user` as a property would also be reactive, thereby achieving our goal; hence, `user` would always update anywhere it is used in the template of such an app. But with the `ref` property, we can make any variable with any data type reactive by passing the value of that variable to `ref`. This method also works for objects, but it nests the object one level deeper than when the `reactive` method is used.

<pre><code class="language-javascript">let property = {
  rooms: '4 rooms',
  garage: true,
  swimmingPool: false
}
let reactiveProperty = ref(property)
console.log(reactiveProperty)
// prints {
// value: {rooms: "4 rooms", garage: true, swimmingPool: false}
// }</code></pre>

Under the hood, `ref` takes this argument passed to it and converts it into an object with a key of `value`. This means, we can access our variable by calling `variable.value`, and we can also modify its value by calling it in the same way.

<pre><code class="language-javascript">import {ref} from 'vue'
let age = ref(1)

console.log(age.value)
//prints 1
age.value++
console.log(age.value)
//prints 2</code></pre>

With this, we can import `ref` into our component and create a reactive variable:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="home"&gt;
    &lt;form @click.prevent=""&gt;
      &lt;table&gt;
        &lt;tr&gt;
          &lt;th&gt;Name&lt;/th&gt;
          &lt;th&gt;Username&lt;/th&gt;
          &lt;th&gt;email&lt;/th&gt;
          &lt;th&gt;Edit Cars&lt;/th&gt;
          &lt;th&gt;Cars&lt;/th&gt;
        &lt;/tr&gt;
        &lt;tr v-for="user in users" :key="user.id"&gt;
          &lt;td&gt;{{ user.name }}&lt;/td&gt;
          &lt;td&gt;{{ user.username }}&lt;/td&gt;
          &lt;td&gt;{{ user.email }}&lt;/td&gt;
          &lt;td&gt;
            &lt;input
              type="number"
              style="width: 20px;"
              name="cars"
              id="cars"
              v-model.number="user.cars.number"
            /&gt;
          &lt;/td&gt;
          &lt;td&gt;
            &lt;cars-number :cars="user.cars" /&gt;
          &lt;/td&gt;
        &lt;/tr&gt;
      &lt;/table&gt;
      &lt;p&gt;Total number of cars: {{ getTotalCars }}&lt;/p&gt;
    &lt;/form&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  // @ is an alias to /src
  import carsNumber from "@/components/cars-number.vue";
  import axios from "axios";
  import { ref } from "vue";
  export default {
    name: "Home",
    data() {
      return {};
    },
    setup() {
      let users = ref([]);
      const getUsers = async () =&gt; {
        let { data } = await axios({
          url: "data.json",
        });
        users.value = data;
      };
      return {
        users,
        getUsers,
      };
    },
    components: {
      carsNumber,
    },
    created() {
      this.getUsers();
    },
    computed: {
      getTotalCars() {
        let users = this.users;
        let totalCars = users.reduce(function(sum, elem) {
          return sum + elem.cars.number;
        }, 0);
        return totalCars;
    },
  };
&lt;/script&gt;</code></pre>

Here, we imported `ref` in order to create a reactive `users` variable in our component. We then imported `axios` to fetch data from a JSON file in the `public` folder, and we imported our `carsNumber` component, which we’ll be creating later on. The next thing we did was create a reactive `users` variable using the `ref` method, so that `users` can update whenever the response from our JSON file changes.

We also created a `getUser` function that fetches the `users` array from our JSON file using [axios](https://github.com/axios/axios), and we assigned the value from this request to the `users` variable. Finally, we created a computed property that computes the total number of cars that our users have as we have modified it in the template section.

It is important to note that when accessing `ref` properties that are returned in the template section or outside of `setup()`, they are [automatically shallow unwrapped](https://v3.vuejs.org/guide/reactivity-fundamentals.html#ref-unwrapping). This means that `refs` that are an object would still require a `.value` in order to be accessed. Because `users` is an array, we could simply use `users` and not `users.value` in `getTotalCars`.

In the template section, we displayed a table that displays each user’s information, together with a `<cars-number />` component. This component accepts a `cars` prop that is displayed in each user’s row as the number of cars they have. This value updates whenever the value of `cars` **changes in the user object**, which is exactly how the `data` object or `computed` property would work if we were working with the Options API.

{{% ad-panel-leaderboard %}}

## `toRefs`

When we use the Composition API, the `setup` function accepts two arguments: `props` and `context`. This `props` is passed from the component to `setup()`, and it makes it possible to access the props that the component has from inside this new API. This method is particularly useful because it allows for the **destructuring of objects** without losing its reactivity.

<pre><code class="language-javascript">&lt;template&gt;
  &lt;p&gt;{{ cars.number }}&lt;/p&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    props: {
      cars: {
        type: Object,
        required: true,
      },
      gender: {
        type: String,
        required: true,
      },
    },
    setup(props) {
      console.log(props);
   // prints {gender: "female", cars: Proxy}
    },
  };
&lt;/script&gt;
&lt;style&gt;&lt;/style&gt;</code></pre>

To use a value that is an object from `props` in the Composition API while ensuring it maintains its reactivity, we make use of `toRefs`. This method takes a reactive object and converts it into a plain object in which each property of the original reactive object becomes a `ref`. What this means is that the `cars` prop…

<pre><code class="language-javascript">cars: {
  number: 0
}</code></pre>

… would now become this:

<pre><code class="language-javascript">{
  value: cars: {
    number: 0
  }</code></pre>

With this, we can make use of `cars` inside any part of the setup API while still maintaining its reactivity.

<pre><code class="language-javascript"> setup(props) {
      let { cars } = toRefs(props);
      console.log(cars.value);
      // prints {number: 0}
    },</code></pre>

We can watch this new variable using the Composition API’s `watch` and react to this change however we might want to.

<pre><code class="language-javascript">setup(props) {
      let { cars } = toRefs(props);
      watch(
        () =&gt; cars,
        (cars, prevCars) =&gt; {
          console.log("deep ", cars.value, prevCars.value);
        },
        { deep: true }
      );
    }</code></pre>

{{% ad-panel-leaderboard %}}

## `toRef`

Another common use case we could be faced with is **passing a value** that is not necessarily an object but rather one of the data types that work with `ref` (array, number, string, boolean, etc.). With `toRef`, we can create a reactive property (i.e. `ref`) from a source reactive object. Doing this would ensure that the property remains reactive and would update whenever the parent source changes.

<pre><code class="language-javascript">const cars = reactive({
  Toyota: 1,
  Honda: 0
})

const NumberOfHondas = toRef(state, 'Honda')

NumberOfHondas.value++
console.log(state.Honda) // 1

state.Honda++
console.log(NumberOfHondas.value) // 2</code></pre>

Here, we created a reactive object using the `reactive` method, with the properties `Toyota` and `Honda`. We also made use of `toRef` to create a reactive variable out of `Honda`. From the example above, we can see that when we update `Honda` using either the reactive `cars` object or `NumberOfHondas`, the value gets updated in both instances.

This method is similar and yet so different from the `toRefs` method that we covered above in the sense that it maintains its connection to its source and can be used for strings, arrays, and numbers. Unlike with `toRefs`, we do not need to worry about the existence of the property in its source at the time of creation, because if this property does not exist at the time that this `ref` is created and instead returns `null`, it would still be stored as a valid property, with a form of [`watcher`](https://v3.vuejs.org/guide/reactivity-computed-watchers.html#watch) put in place, so that when this value changes, this `ref` created using `toRef` would also be updated.

We can also use this method to create a **reactive property** from `props`. That would look like this:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;p&gt;{{ cars.number }}&lt;/p&gt;
&lt;/template&gt;
&lt;script&gt;
  import { watch, toRefs, toRef } from "vue";
  export default {
    props: {
      cars: {
        type: Object,
        required: true,
      },
      gender: {
        type: String,
        required: true,
      },
    },
    setup(props) {
      let { cars } = toRefs(props);
      let gender = toRef(props, "gender");
      console.log(gender.value);
      watch(
        () =&gt; cars,
        (cars, prevCars) =&gt; {
          console.log("deep ", cars.value, prevCars.value);
        },
        { deep: true }
      );
    },
  };
&lt;/script&gt;</code></pre>

Here, we created a `ref` that would be based on the `gender` property gotten from `props`. This comes in handy when we want to perform extra operations on the prop of a particular component.

## Conclusion

In this article, we have looked at how reactivity in Vue works using some of the newly introduced methods and functions from Vue 3. We started by looking at what reactivity is and how Vue makes use of the [`Proxy` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) behind the scenes to achieve this. We also looked at how we can create reactive objects using `reactive` and how to create reactive properties using `ref`.

Finally, we looked at how to convert reactive objects to plain objects, each of whose properties are a [`ref`](https://v3.vuejs.org/api/refs-api.html#ref) pointing to the corresponding property of the original object, and we saw how to create a [`ref`](https://v3.vuejs.org/api/refs-api.html#ref) for a property on a reactive source object.

### Further Resources

- “[Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)” (object), MDN Web Docs
- “[Reactivity Fundamentals](https://v3.vuejs.org/guide/reactivity-fundamentals.html#ref-unwrapping)”, Vue.js
- “[Refs](https://v3.vuejs.org/api/refs-api.html#refs)”, Vue.js
- “[Lifecycle Hook Registration Inside `setup`](https://v3.vuejs.org/guide/composition-api-introduction.html#lifecycle-hook-registration-inside-setup)”, Vue.js

{{< signature "ks, vf, yk, il, al" >}}
