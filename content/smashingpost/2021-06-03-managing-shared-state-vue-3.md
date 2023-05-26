---
title: 'Managing Shared State In Vue 3'
slug: managing-shared-state-vue3
author: shawn-wildermuth
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a70815d-28e5-44af-8306-0e992e99593a/managing-shared-state-vue3.jpg
date: 2021-06-03T10:30:00.000Z
summary: >-
  Writing large-scale Vue applications can be a challenge. Using shared state in your Vue 3 applications can be a solution to reducing this complexity. There are a number common solutions to solving state. In this article, I will dive into the pros and cons of approaches like factories, shared objects, and using Vuex. I’ll also show you what is coming in Vuex 5 that might change how we all use shared state in Vue 3.
description: >-
  Writing large-scale Vue applications can be a challenge. In this article, Shawn Wildermuth dives into the pros and cons of approaches like factories, shared objects, and using Vuex. He also explains what is coming in Vuex 5.0 that might change how we all use shared state in Vue 3.
categories:
  - Vue
  - Apps
  - JavaScript
---

State can be hard. When we start a simple Vue project, it can be simple to just keep our working state on a particular component:

<pre><code class="language-javascript">setup() {
  let books: Work[] = reactive([]);

  onMounted(async () =&gt; {
    // Call the API
    const response = await bookService.getScienceBooks();
    if (response.status === 200) {
      books.splice(0, books.length, ...response.data.works);
    }
  });

  return {
    books
  };
},
</code></pre>

When your project is a single page of showing data (perhaps to sort or filter it), this can be compelling. But in this case, this component will get data on every request. What if you want to keep it around? That’s where state management comes into play. As network connections are often expensive and occasionally unreliable, it would be better to keep this state around as you navigate through an application.

Another issue is communicating between components. While you can use events and props to communicate with direct children-parents, handling simple situations like error handling and busy flags can be difficult when each of your views/pages are independent. For example, imagine that you had a top-level control was wired up to show error and loading animation:

<pre><code class="language-javascript">// App.vue
&lt;template&gt;
  &lt;div class="container mx-auto bg-gray-100 p-1"&gt;
    &lt;router-link to="/"&gt;&lt;h1&gt;Bookcase&lt;/h1&gt;&lt;/router-link&gt;
    &lt;div class="alert" v-if="error"&gt;{{ error }}&lt;/div&gt;
    &lt;div class="alert bg-gray-200 text-gray-900" v-if="isBusy"&gt;
      Loading...
    &lt;/div&gt;
    &lt;router-view :key="$route.fullPath"&gt;&lt;/router-view&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>

Without an effective way to handle this state, it might suggest a publish/subscribe system, but in fact sharing data is more straightforward in many cases. If want to have shared state, how do you go about it? Let’s look at some common ways to do this.

**Note**: *You’ll find the code for this section in the “main” branch of the [example project on GitHub](https://github.com/smashingmagazine/SmashingBookcase).*

## Shared State In Vue 3

Since moving to Vue 3, I’ve migrated completely to using the Composition API. For the article, I’m also using TypeScript though that’s not required for examples I’m showing you. While you can share state any way you want, I’m going to show you several techniques that I find the most commonly used patterns. Each has it’s own pros and cons, so don’t take anything I talk about here as dogma.

The techniques include:

<ul>
  <li><a href="#factories">Factories</a>,</li>
  <li><a href="#shared-singletons">Shared Singletons</a>,</li>
  <li><a href="#vuex4">Vuex 4</a>,</li>
  <li><a href="#vuex5">Vuex 5</a>.</li>
</ul>

**Note**: *Vuex 5, as of the writing of this article, it’s in the RFC (Request for Comments) stage so I want to get you ready for where Vuex is going, but right now there is not a working version of this option.*

Let’s dig in...

### Factories

**Note**: *The code for this section is in the “Factories” branch of the example project on [GitHub](https://github.com/smashingmagazine/SmashingBookcase/tree/Factories).*

The factory pattern is just about creating an instance of the state you care about. In this pattern, you return a function that is much like the **start** function in the Composition API. You’d create a scope and build the components of what you’re looking for. For example:

<pre><code class="language-javascript">export default function () {

  const books: Work[] = reactive([]);

  async function loadBooks(val: string) {
      const response = await bookService.getBooks(val, currentPage.value);
      if (response.status === 200) {
        books.splice(0, books.length, ...response.data.works);
      }
  }

  return {
    loadBooks,
    books
  };
}
</code></pre>

You could ask for just the parts of the factory created objects you need like so:

<pre><code class="language-javascript">// In Home.vue
  const { books, loadBooks } = BookFactory();
</code></pre>

If we add an `isBusy` flag to show when the network request happens, the above code doesn’t change, but you could decide where you are going to show the `isBusy`:

<pre><code class="language-javascript">export default function () {

  const books: Work[] = reactive([]);
  const isBusy = ref(false);

  async function loadBooks(val: string) {
    isBusy.value = true;
    const response = await bookService.getBooks(val, currentPage.value);
    if (response.status === 200) {
      books.splice(0, books.length, ...response.data.works);
    }
  }

  return {
    loadBooks,
    books,
    isBusy
  };
}
</code></pre>

In another view (vue?) you could just ask for the isBusy flag without having to know about how the rest of the factory works:

<pre><code class="language-javascript">// App.vue
export default defineComponent({
  setup() {
    const { isBusy } = BookFactory();
    return {
      isBusy
    }
  },
})
</code></pre>

But you may have noticed an issue; every time we call the factory, we’re getting a new instance of all the objects. There are times when you want to have a factory return new instances, but in our case we’re talking about sharing the state, so we need to move the creation outside the factory:

<pre><code class="language-javascript">const books: Work[] = reactive([]);
const isBusy = ref(false);

async function loadBooks(val: string) {
  isBusy.value = true;
  const response = await bookService.getBooks(val, currentPage.value);
  if (response.status === 200) {
    books.splice(0, books.length, ...response.data.works);
  }
}

export default function () {
 return {
    loadBooks,
    books,
    isBusy
  };
}
</code></pre>

Now the factory is giving us a shared instance, or a singleton if you prefer. While this pattern works, it can be confusing to return a function that doesn’t create a new instance every time.

Because the underlying objects are marked as `const` you shouldn’t be able to replace them (and break the singleton nature). So this code should complain:

<pre><code class="language-javascript">// In Home.vue
  const { books, loadBooks } = BookFactory();

  books = []; // Error, books is defined as const
</code></pre>

So it can be important to make sure mutable state can be updated (e.g. using `books.splice()` instead of assigning the books).

Another way to handle this is to use shared instances.

{{% feature-panel %}}

### Shared Instances

*The code for this section is in the “SharedState” branch of the example project on [GitHub](https://github.com/smashingmagazine/SmashingBookcase/tree/SharedState).*

If you’re going to be sharing state, might as well be clear about the fact that the state is a singleton. In this case, it can just be imported as a static object. For example, I like to create an object that can be imported as a reactive object:

<pre><code class="language-javascript">export default reactive({

  books: new Array&lt;Work&gt;(),
  isBusy: false,

  async loadBooks() {
    this.isBusy = true;
    const response = await bookService.getBooks(this.currentTopic, this.currentPage);
    if (response.status === 200) {
      this.books.splice(0, this.books.length, ...response.data.works);
    }
    this.isBusy = false;
  }
});
</code></pre>

In this case, you just import the object (which I’m calling a store in this example):

<pre><code class="language-javascript">// Home.vue
import state from "@/state";

export default defineComponent({
  setup() {

    // ...

    onMounted(async () => {
      if (state.books.length === 0) state.loadBooks();
    });

    return {
      state,
      bookTopics,
    };
  },
});
</code></pre>

Then it becomes easy to bind to the state:

<pre><code class="language-javascript">&lt;!-- Home.vue --&gt;
&lt;div class="grid grid-cols-4"&gt;
  &lt;div
    v-for="book in state.books"
    :key="book.key"
    class="border bg-white border-grey-500 m-1 p-1"
  &gt;
  &lt;router-link :to="{ name: 'book', params: { id: book.key } }"&gt;
    &lt;BookInfo :book="book" /&gt;
  &lt;/router-link&gt;
&lt;/div&gt;
</code></pre>

Like the other patterns, you get the benefit that you can share this instance between views:

<pre><code class="language-javascript">// App.vue
import state from "@/state";

export default defineComponent({
  setup() {
    return {
      state
    };
  },
})
</code></pre>

Then this can bind to what is the same object (whether it is a parent of the `Home.vue` or another page in the router):

<pre><code class="language-javascript">&lt;!-- App.vue --&gt;
  &lt;div class="container mx-auto bg-gray-100 p-1"&gt;
    &lt;router-link to="/"&gt;&lt;h1&gt;Bookcase&lt;/h1&gt;&lt;/router-link&gt;
    &lt;div class="alert bg-gray-200 text-gray-900"   
         v-if="state.isBusy"&gt;Loading...&lt;/div&gt;
    &lt;router-view :key="$route.fullPath"&gt;&lt;/router-view&gt;
  &lt;/div&gt;
</code></pre>

Whether you use the factory pattern or the shared instance, they both have a common issue: mutable state. You can have accidental side effects of bindings or code changing state when you don’t want them to. In a trivial example like I’m using here, it isn’t complex enough to worry about. But as you’re building larger and larger apps, you will want to think about state mutation more carefully. That’s where Vuex can come to the rescue.

{{% ad-panel-leaderboard %}}

### Vuex 4

*The code for this section is in the “Vuex4” branch of the example project on [GitHub](https://github.com/smashingmagazine/SmashingBookcase/tree/Vuex4).*

Vuex is state manager for Vue. It was built by the core team though it is managed as a separate project. The purpose of Vuex is to separate the state from the actions you want to do to the state. All changes of state has to go through Vuex which means it is more complex, but you get protection from accidental state change.

The idea of Vuex is to provide a predictable flow of state management. Views flow to Actions which, in turn, use Mutations to change State which, in turn, updates the View. By limiting the flow of state change, you should have fewer side effects that change the state of your applications; therefore be easier to build larger applications. Vuex has a learning curve, but with that complexity you get predictability.

Additionally, Vuex does support development-time tools (via the Vue Tools) to work with the state management including a feature called time-travel. This allows you to view a history of the state and move back and forward to see how it affects the application.

There are times, too, when Vuex is important too.

To add it to your Vue 3 project, you can either add the package to the project:

<pre><code class="language-javascript">&gt; npm i vuex
</code></pre>

Or, alternatively you can add it by using the Vue CLI:

<pre><code class="language-javascript">&gt; vue add vuex
</code></pre>

By using the CLI, it will create a starting point for your Vuex store, otherwise you’ll need to wire it up manually to the project. Let’s walk through how this works.

First, you’ll need a state object that is created with Vuex’s createStore function:

<pre><code class="language-javascript">import { createStore } from 'vuex'

export default createStore({
  state: {},
  mutations: {},
  actions: {},
  getters: {}
});
</code></pre>

As you can see, the store requires several properties to be defined. State is just a list of the data you want to give your application access to:

<pre><code class="language-javascript">import { createStore } from 'vuex'

export default createStore({
  state: {
    books: [],
    isBusy: false
  },
  mutations: {},
  actions: {}
});
</code></pre>

Note that the state shouldn’t use **ref** or **reactive** wrappers. This data is the same kind of share data that we used with Shared Instances or Factories. This store will be a singleton in your application, therefore the data in state is also going to be shared.

Next, let’s look at actions. Actions are operations that you want to enable that involve the state. For example:

<pre><code class="language-javascript">  actions: {
    async loadBooks(store) {
      const response = await bookService.getBooks(store.state.currentTopic,
      if (response.status === 200) {
        // ...
      }
    }
  },
</code></pre>

Actions are passed an instance of the store so that you can get at the state and other operations. Normally, we’d destructure just the parts we need:

<pre><code class="language-javascript">  actions: {
    async loadBooks({ state }) {
      const response = await bookService.getBooks(state.currentTopic,
      if (response.status === 200) {
        // ...
      }
    }
  },
</code></pre>

The last piece of this are Mutations. Mutations are functions that can mutate state. Only mutations can affect state. So, for this example, we need mutations that change change the state:

<pre><code class="language-javascript">  mutations: {
    setBusy: (state) =&gt; state.isBusy = true,
    clearBusy: (state) =&gt; state.isBusy = false,
    setBooks(state, books) {
      state.books.splice(0, state.books.length, ...books);
    }
 },
</code></pre>

Mutation functions always pass in the state object so that you can mutate that state. In the first two examples, you can see that we’re explicitly setting the state. But in the third example, we’re passing in the state to set. Mutations always take two parameters: state and the argument when calling the mutation.

To call a mutation, you’d use the **commit** function on the store. In our case, I’ll just add it to the destructuring:

<pre><code class="language-javascript">  actions: {
    async loadBooks({ state, commit }) {
      commit("setBusy");
      const response = await bookService.getBooks(state.currentTopic, 
      if (response.status === 200) {
        commit("setBooks", response.data);
      }
      commit("clearBusy");
    }
  },
</code></pre>

What you’ll see here is how **commit** requires the name of the action. There are tricks to make this not just use magic strings, but I’m going to skip that for now. This use of magic strings is one of the limitations of using Vuex.

While using commit may seem like an unnecessary wrapper, remember that Vuex is not going to let you mutate state except inside the mutation, therefore only calls through **commit** will. 

You can also see that the call to **setBooks** takes a second argument. This is the second argument that is calling the mutation. If you were to need more information, you’d need to pack it into a single argument (another limitation of Vuex currently). Assuming you needed to insert a book into the books list, you could call it like this:

<pre><code class="language-javascript">commit("insertBook", { book, place: 4 }); // object, tuple, etc.
</code></pre>

Then you could just destructure into the pieces you need:

<pre><code class="language-javascript">mutations: {
  insertBook(state, { book, place }) =&gt; // ...    
}
</code></pre>

Is this elegant? Not really, but it works.

Now that we have our action working with mutations, we need to be able to use the Vuex store in our code. There are really two ways to get at the store. First, by registering the store with application (e.g. main.ts/js), you’ll have access to a centralized store that you have access to everywhere in your application:

<pre><code class="language-javascript">// main.ts
import store from './store'

createApp(App)
  .use(store)
  .use(router)
  .mount('#app')
</code></pre>

Note that this isn’t adding Vuex, but your actual store that you’re creating. Once this is added, you can just call `useStore` to get the store object:

<pre><code class="language-javascript">import { useStore } from "vuex";

export default defineComponent({
  components: {
    BookInfo,
  },
  setup() {
    const store = useStore();
    const books = computed(() =&gt; store.state.books);
    // ...
  </code></pre>

This works fine, but I prefer to just import the store directly:

<pre><code class="language-javascript">import store from "@/store";

export default defineComponent({
  components: {
    BookInfo,
  },
  setup() {
    const books = computed(() =&gt; store.state.books);
    // ...
  </code></pre>

Now that you have access to the store object, how do you use it? For state, you’ll need to wrap them with computed functions so that changes will be propagated to your bindings:

<pre><code class="language-javascript">export default defineComponent({
  setup() {

    const books = computed(() =&gt; store.state.books);

    return {
      books
    };
  },
});
</code></pre>

To call actions, you will need to call the **dispatch** method:

<pre><code class="language-javascript">export default defineComponent({
  setup() {

    const books = computed(() =&gt; store.state.books);

    onMounted(async () =&gt; await store.dispatch("loadBooks"));

    return {
      books
    };
  },
});
</code></pre>

Actions can have parameters that you add after the name of the method. Lastly, to change state, you’ll need to call commit just like we did inside the Actions. For example, I have a paging property in the store, and then I can change the state with **commit**:

<pre><code class="language-javascript">const incrementPage = () =&gt;
  store.commit("setPage", store.state.currentPage + 1);
const decrementPage = () =&gt;
  store.commit("setPage", store.state.currentPage - 1);
</code></pre>

Note, that calling it like this would throw an error (because you can’t change state manually):

<pre><code class="language-javascript">const incrementPage = () =&gt; store.state.currentPage++;
  const decrementPage = () =&gt; store.state.currentPage--;
</code></pre>

This is the real power here, we’d want control where state is changed and not have side effects that produce errors further down the line in development.

You may be overwhelmed with number of moving pieces in Vuex, but it can really help manage state in larger, more complex projects. I would not say you need it in every case, but there will be large projects where it helps you overall.

The big problem with Vuex 4 is that working with it in a TypeScript project leaves a lot to be desired. You can certainly make TypeScript types to help development and builds, but it requires a lot of moving pieces.

That’s where Vuex 5 is meant to simplify how Vuex works in TypeScript (and in JavaScript projects in general). Let’s see how that will work once it’s released next.

{{% ad-panel-leaderboard %}}

### Vuex 5

**Note**: *The code for this section is in the “Vuex5” branch of the example project on [GitHub](https://github.com/smashingmagazine/SmashingBookcase/tree/Vuex5).*

At the time of this article, Vuex 5 isn’t real. It’s a RFC (Request for Comments). It’s a plan. It’s a starting point for discussion. So a lot of what I may explain here likely will change somewhat. But to prepare you for the change in Vuex, I wanted to give you a view of where it’s going. Because of this the code associated with this example doesn’t build.

The basic concepts of how Vuex works have been somewhat unchanged since it’s inception. With the introduction of Vue 3, Vuex 4 was created to mostly allow Vuex to work in new projects. But the team is trying to look at the real pain-points with Vuex and solve them. To this end they are planning some important changes:

- No more mutations: actions can mutate state (and possibly anyone).
- Better TypeScript support.
- Better multi-store functionality.

So how would this work? Let’s start with creating the store:

<pre><code class="language-javascript">export default createStore({
  key: 'bookStore',
  state: () =&gt; ({
    isBusy: false,
    books: new Array&lt;Work&gt;()
  }),
  actions: {
    async loadBooks() {
      try {
        this.isBusy = true;
        const response = await bookService.getBooks();
        if (response.status === 200) {
          this.books = response.data.works;
        }
      } finally {
        this.isBusy = false;
      }
    }
  },
  getters: {
    findBook(key: string): Work | undefined {
      return this.books.find(b =&gt; b.key === key);
    }
  }
});
</code></pre>

First change to see is that every store now needs it own key. This is to allow you to retrieve multiple stores. Next you’ll notice that the state object is now a factory (e.g. returns from a function, not created on parsing). And there is no mutations section any more. Lastly, inside the actions, you can see we’re accessing state as just properties on the `this` pointer. No more having to pass in state and commit to actions. This helps not only in simplifying development, but also makes it easier to infer types for TypeScript.

To register Vuex into your application, you’ll register Vuex instead of your global store:

<pre><code class="language-javascript">import { createVuex } from 'vuex'

createApp(App)
  .use(createVuex())
  .use(router)
  .mount('#app')
</code></pre>

Finally, to use the store, you’ll import the store then create an instance of it:

<pre><code class="language-javascript">import bookStore from "@/store";

export default defineComponent({
  components: {
    BookInfo,
  },
  setup() {
    const store = bookStore(); // Generate the wrapper
    // ...
  </code></pre>

Notice that what is returned from the store is a factory object that returns thsi instance of the store, no matter how many times you call the factory. The returned object is just an object with the actions, state and getters as first class citizens (with type information):

<pre><code class="language-javascript">onMounted(async () =&gt; await store.loadBooks());

const incrementPage = () =&gt; store.currentPage++;
const decrementPage = () =&gt; store.currentPage--;
</code></pre>

What you’ll see here is that state (e.g. `currentPage`) are just simple properties. And actions (e.g. `loadBooks`) are just functions. The fact that you’re using a store here is a side effect. You can treat the Vuex object as just an object and go about your work. This is a significant improvement in the API.

Another change that’s important to point out is that you could also generate your store using a Composition API-like syntax:

<pre><code class="language-javascript">export default defineStore("another", () =&gt; {

  // State
  const isBusy = ref(false);
  const books = reactive(new Array&gl;Work&gt;());

  // Actions
  async function loadBooks() {
    try {
      this.isBusy = true;
      const response = await bookService.getBooks(this.currentTopic, this.currentPage);
      if (response.status === 200) {
        this.books = response.data.works;
      }
    } finally {
      this.isBusy = false;
    }
  }

  findBook(key: string): Work | undefined {
    return this.books.find(b =&gt; b.key === key);
  }

  // Getters
  const bookCount = computed(() =&gt; this.books.length);

  return {
    isBusy,
    books,
    loadBooks,
    findBook,
    bookCount
  }
});
</code></pre>

This allows you to build your Vuex object just like you would your views with the Composition API and arguably it’s simpler.

One main drawback in this new design is that you lose the non-mutability of the state. There are discussions happening around being able to enable this (for development only, just like Vuex 4) but there isn’t consensus how important this is. I personally think it’s a key benefit for Vuex, but we’ll have to see how this plays out.

## Where Are We?

Managing shared state in single page applications is a crucial part of development for most apps. Having a game plan on how you want to go about it in Vue is an important step in designing your solution. In this article, I’ve shown you several patterns for managing shared state including what’s coming for Vuex 5. Hopefully you’ll now have the knowledge to make the right decision for you own projects.

{{< signature "vf, yk, il" >}}
