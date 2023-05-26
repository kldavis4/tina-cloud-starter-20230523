---
title: 'How To Do More With Vue Router'
slug: vue-router-features
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c79f83b-eeaa-47a7-a553-148e726a0b2d/vue-router-features.png
date: 2020-08-31T13:30:00.000Z
summary: >-
  Vue Router is the official router for Vue that is mostly used for creating multiple pages living on different routes (`/home`, `/profile`) in your application but has some features that some people do not know about. In this tutorial, we’re going to learn about some amazing features the Vue Router has and how we can make use of them in our app.
description: >-
  In this tutorial, we’re going to learn about some amazing features the Vue Router has and how we can make use of them in our app.
categories:
  - API
  - Vue
  - JavaScript
---

[Vue Router](https://router.vuejs.org/) is the official router for Vue. It deeply integrates with Vue core to make building Single Page Applications with Vue a breeze. Some of its popular features include:

1. Dynamic Route matching.
2. Named Routes.
3. Named views.
4. Programmatic navigation.

These features are heavily used when developing with Vue and this is because they are part of the basics you need to understand to efficiently use the Router. But the Vue Router has some very useful features that can be very helpful in development and in this article, we’re going to take a look at them. 

For the purpose of this tutorial, we’re going to be building a simple application that would help in understanding some of the concepts covered in this article. You can find all the code used in this article on [GitHub](https://github.com/Timibadass/vue-router-demo). If you are interested in doing more with the router, you’ll benefit from this tutorial.

***Note: This article requires a basic understanding of Vuejs and Vue Router.***

## Scroll Behaviour

This is the behavior that is observed when navigating from one page to another. The default behavior of Vue router is only noticeable after scrolling to a position that isn’t the top of the page. This is because, by default, the scroll position when navigating away from a page is maintained on a new page. What this means is, if you click on a link that leads to a new route ( i.e from `/home` to `/about`) in a position that is let’s say close to the footer of the current page, the new page would start from that same position instead of starting from the top of the page.

I have created a Vue application using the Vue CLI command `vue create vue-router-demo`, I also selected Vue Router as part of the options while setting up my app because we will be using it throughout this tutorial.

We will also need to make API calls to [JSONPlaceholder](https://jsonplaceholder.typicode.com/), to illustrate some of the concepts using Vue router. For this, we will be using Axios. To install [Axios](https://www.smashingmagazine.com/2020/05/getting-started-axios-nuxt/):

<pre><code class="language-bash"># using YARN
yarn add axios
# or NPM
npm install axios</code></pre>

After installing Axios, we can update our `Home.vue` to look like this:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="home"&gt;
        &lt;p v-if="loading" class="post--empty"&gt;Loading....&lt;/p&gt;
        &lt;ul v-else&gt;
            &lt;li v-for="post in posts" :key="post.id"&gt;
                &lt;router-link
                    :to="{ name: 'Post', params: { id: post.id, post: post } }"
                &gt;
                    {{ post.title }}
                &lt;/router-link&gt;
            &lt;/li&gt;
        &lt;/ul&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
    // @ is an alias to /src
    import axios from "axios";
    export default {
        name: "Home",
        data() {
            return {
                posts: null,
                loading: false,
            };
        },
        mounted() {
            this.getPosts();
        },
        methods: {
            async getPosts() {
                this.loading = true;
                try {
                    let res = await axios({
                        url: "https://jsonplaceholder.typicode.com/posts",
                        method: "GET",
                    });
                    let posts = res.data;
                    this.posts = posts;
                    this.loading = false;
                } catch (error) {
                    this.loading = false;
                }
            },
        },
    };
&lt;/script&gt;
&lt;style&gt;
    .home {
        padding: 0 30px;
        max-width: 800px;
        margin: 0 auto;
    }
    @keyframes blink {
        from {
            opacity: 1;
        }
        to {
            opacity: 0;
        }
    }
    .post--empty {
        height: 250px;
        margin-top: 30px;
        animation: blink 0.8s ease-in-out infinite alternate both;
        display: flex;
        align-items: center;
        justify-content: center;
        font-family: "Lobster", cursive;
    }
    ul {
        text-align: left;
    }
    a {
        color: inherit;
    }
&lt;/style&gt;</code></pre>
</div>
  
Here, we’re importing `axios` and using it to fetch a list of `posts` from JSONPlaceholder in the `getPost` method. We’re also assigning the array of posts gotten from this API call to `posts` from the `data` function from this page, this is because we want to use this data in our template section. After this, we loop through the array of posts in a list ( `<ul></ul>`) and also attach a link to each post using `id` of each post as the link param (this is called [dynamic route matching](https://router.vuejs.org/guide/essentials/dynamic-matching.html#reacting-to-params-changes)). We have also added a paragraph that would serve as a loading indicator.

{{% feature-panel %}}

At this point, here’s what this page looks like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cbdcd62-1743-4dca-896e-5c2e2c503eb8/01-landing-page-vue-router.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cbdcd62-1743-4dca-896e-5c2e2c503eb8/01-landing-page-vue-router.png" sizes="100vw" caption="List of posts from JSONPlaceholder. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cbdcd62-1743-4dca-896e-5c2e2c503eb8/01-landing-page-vue-router.png'>Large preview</a>)" alt="list of posts from JSONPlaceholder" >}}

The next thing would be to create the page that will display the info for each post and create a link for it in the router of our app.

***Post.vue***

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="about"&gt;
        &lt;div class="post"&gt;
            &lt;h1&gt;{{ post.title }}&lt;/h1&gt;
            &lt;p v-html="post.body"&gt;&lt;/p&gt;
        &lt;/div&gt;
        &lt;p&gt;End of page&lt;/p&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
    export default {
        name: "Post",
        props: &#91;"id", "post"&#93;,
    };
&lt;/script&gt;
&lt;style&gt;
    .post {
        padding: 0 30px;
        height: 110vh;
        margin: 0 auto;
    }
    p {
        margin: 10px 0;
    }
&lt;/style&gt;</code></pre>

Here, we make use of [passing props to route components](https://router.vuejs.org/guide/essentials/passing-props.html) to define `id` and `post` which we’re passing from the previous page in the form of route params. This is a neat way of accessing route params and query as opposed to doing this:

***Post.vue***

<pre><code class="language-javascript">&lt;script&gt;
    export default {
        name: "Post",
        data() {
            return {
                post: this.$route.post,
            };
        },
    };
&lt;/script&gt;</code></pre>
  
We then make use of this `post` value in the template section to display post title and body. Finally, we add a paragraph to the end of the page. We also add styling for the page in the styling section, which includes defining a `height` of `110vh`. This is because we need the page to have a height that is more than the default height `100vh` so we can observe the default scroll behavior of the router. 
 
The next thing would be to create a route that would display each post. Update your `index.js` file in the ***/router*** folder ( or ***router.js*** file) to look like this:

<div class="break-out">

<pre><code class="language-javascript">import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
Vue.use(VueRouter)
const routes = [{
        path: '/',
        name: 'Home',
        component: Home
    },
    {
        path: '/:id',
        name: 'Post',
        props: true,
        component: () =&gt;
            import ( /* webpackChunkName: "post" */ '../views/Post.vue')
    }
]
const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
})
export default router</code></pre>
</div>

Here, we define a new route that makes use of `id` that would be passed to this route from the homepage. We’re also decoupling the router param (in this case, `post` and `id`) using props.

The top of this page looks like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7972db9e-971d-40b2-9e41-2dbc4a5105df/02-top-post-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7972db9e-971d-40b2-9e41-2dbc4a5105df/02-top-post-page.png" sizes="100vw" caption="Top of post page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7972db9e-971d-40b2-9e41-2dbc4a5105df/02-top-post-page.png'>Large preview</a>)" alt="the top of post page" >}}

If we click on any of the posts on the home page that does not require us to scroll, we would not notice any weird behavior scroll wise, but if we scroll down a little and click on the last post in this list, this should be the position the `/post` page would land on:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/852b446c-4def-4e6d-b449-bb0e560a3945/03-default-scroll-position-vue-router.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/852b446c-4def-4e6d-b449-bb0e560a3945/03-default-scroll-position-vue-router.png" sizes="100vw" caption="Default scroll position. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/852b446c-4def-4e6d-b449-bb0e560a3945/03-default-scroll-position-vue-router.png'>Large preview</a>)" alt="default scroll position" >}}

This is bad for UX and this is because the user isn’t expecting this behavior and they might need to start from the top of a page to get the full information on the said page.

Vue Router comes with the option to customize this behavior to individual preferences, an example would be saving scroll position of a previous route when trying to move back/forward. To fix the current issue in our app, we would update our router file to include the following:

<pre><code class="language-javascript">import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
Vue.use(VueRouter)
const routes = [...]
const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes,
    //add this
    scrollBehavior(to, from, savedPosition) {
        return { x: 0, y: 0 }
    }
})
export default router</code></pre>

Now, if we scroll to the bottom of the home page and click on the last post, you should notice that it now starts from the top of the page.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d39f1661-8ce5-4d9c-8c41-11f7f78844ee/04-new-scroll-position-vue-router.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d39f1661-8ce5-4d9c-8c41-11f7f78844ee/04-new-scroll-position-vue-router.png" sizes="100vw" caption="New scroll position. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d39f1661-8ce5-4d9c-8c41-11f7f78844ee/04-new-scroll-position-vue-router.png'>Large preview</a>)" alt="new scroll position" >}}



## Data Fetching

When fetching data from an API, we either call the method in the `mounted` or `created` lifecycle hook, these are by far the most popular methods people use when developing in Vue. Vue router comes with another method in which we make this API request before navigating to a new route by making this request using the `beforeRouterEnter` guard in such a component. Here is an example of how to fetch data from JSONPlaceholder using this method:

<pre><code class="language-javascript">beforeRouteEnter(to, from, next) {
    axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then((res) =&gt; {
            next((vm) =&gt; vm.fetchData(res));
        })
        .catch((err) =&gt; {
            console.error(err);
        });
},
methods: {
    fetchData(res) {
        let post = res.data;
        this.posts = post;
    },
    
},</code></pre>

Here, we’re fetching a list of posts from an API using Axios and when this request is complete, we call `next`. At this point in the lifecycle of this component, `this` is not available because the component has not been created but we have access to `vm` which gives us access to the component’s instance. Inside this function, we pass the response from the API request `res` to our method `fetchData` which we’ve created to assign the value from this response to `post` so we can use it in our template. Now, if we refresh our `/` route, we would notice that the data gets updated very fast and at no time is there a blank or page ( provided the request is successful).

{{% ad-panel-leaderboard %}}

## Transitions

Vue comes with a `<transition></ transition>` component that enables easy implementation  of [CSS transitions](https://www.smashingmagazine.com/2020/07/css-transitions-vuejs-nuxtjs/) and animations. This feature can be extended to work for navigation between routes in Vue. Here’s an example:

<pre><code class="language-css">&lt;template&gt;
    &lt;div id="app"&gt;
        &lt;div id="nav"&gt;
            &lt;router-link to="/"&gt;Home&lt;/router-link&gt;
        &lt;/div&gt;
        &lt;transition name="slide-fade"&gt;
          &lt;router-view /&gt;
        &lt;/transition&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;style&gt;
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }
    #nav {
        padding: 30px;
    }
    #nav a {
        font-weight: bold;
        color: #2c3e50;
    }
    #nav a.router-link-exact-active {
        color: #42b983;
    }
    .slide-fade-enter-active {
        transition: transform 0.3s cubic-bezier(1, 0.5, 0.8, 1),
            color 0.5s cubic-bezier(1, 0.5, 0.8, 1);
    }
    .slide-fade-leave-active {
        transition: transform 1s cubic-bezier(1, 0.5, 0.8, 1),
            color 1s cubic-bezier(1, 0.5, 0.8, 1);
    }
    .slide-fade-enter {
        color: mediumblue;
        transform: translateY(20px);
    }
    .slide-fade-leave-to {
        transform: translateX(100px);
        color: cyan;
    }
&lt;/style&gt;</code></pre>

Here, we’re adding a transition with the name `slide-fade` to our application and wrapping it around all the route navigation that would take place in the app. We’re also adding a set of styles that control/define the way the transitions would work in our app. Without these rules, there would be no visible transition taking place. Now, if we try to navigate from the homepage to the individual posts, we would notice a sliding and fading transition taking place during the navigation process.

There are two types of route based transitions.

### 1. Per-route Transition

This type of transition is defined in the component that renders a route and so, it only affects the navigation to and from such a page. This gives us the ability to define a special transition for individual routes if we want. Here is an example of how to do that.

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
 // add a transition component with name and mode props
    &lt;transition name="slide-fade" mode="in-out"&gt;
        &lt;div class="about"&gt;
            &lt;div class="post"&gt;
                &lt;h1&gt;{{ post.title }}&lt;/h1&gt;
                &lt;p v-html="post.body"&gt;&lt;/p&gt;
            &lt;/div&gt;
            &lt;p&gt;End of page&lt;/p&gt;
        &lt;/div&gt;
    &lt;/transition&gt;
&lt;/template&gt;
&lt;script&gt;
    export default {
        name: "Post",
        props: ["id", "post"],
    };
&lt;/script&gt;
&lt;style&gt;
    //...

    .slide-fade-enter-active {
        transition: transform 2s cubic-bezier(1, 0.5, 0.8, 1), opacity 2s ease-in;
    }
    .slide-fade-leave-active {
        transition: transform 2s cubic-bezier(1, 0.5, 0.8, 1), opacity 2s ease-out;
    }
    .slide-fade-enter {
        opacity: 1;
        transform: skewY(20deg);
    }
    .slide-fade-leave-to {
        transform: skewY(-45deg);
        opacity: 0.5;
    }
&lt;/style&gt;</code></pre>
</div>

If you try to navigate away from this page, we would notice the page gets skewed and fades for a duration of `2s` as the navigation changes.

### 2. Route-Based Dynamic Transition

This is similar to the general method of adding transitions to all routes in your application but it has one major difference, that is, it accepts a dynamic transition `name` prop which gives you the ability to change the transition type any way you want. Let us create an example of how to do this.

We’re going to update our `App.vue` file with a dynamic `name` prop and configure it to choose a transition name depending on a value.

<div class="break-out">

<pre><code class="language-javascript"> &lt;template&gt;
    &lt;div id="app"&gt;
        &lt;div id="nav"&gt;
            &lt;router-link to="/"&gt;Home&lt;/router-link&gt;
        &lt;/div&gt;
        &lt;transition :name="transitionName"&gt;
            &lt;router-view /&gt;
        &lt;/transition&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
    export default {
        data() {
            return {
                transitionName: "slide-fade",
            };
        },
        watch: {
            $route(to, from, params) {
                const toParam = to.params && to.params.id ? to.params.id : 0;
                this.transitionName = toParam % 2 === 0 ? "slide-left" : "slide-fade";
            },
        },
    };
&lt;/script&gt;
&lt;style&gt;
    /* add transition styles */
    .slide-fade-enter-active {
        transition: transform 0.3s cubic-bezier(1, 0.5, 0.8, 1),
            color 0.5s cubic-bezier(1, 0.5, 0.8, 1);
    }
    .slide-fade-leave-active {
        transition: transform 1s cubic-bezier(1, 0.5, 0.8, 1),
            color 1s cubic-bezier(1, 0.5, 0.8, 1);
    }
    .slide-fade-enter {
        color: mediumblue;
        transform: translateY(20px);
    }
    .slide-fade-leave-to {
        transform: translateX(100px);
        color: cyan;
    }
    .slide-left-enter-active {
        transition: transform 0.3s cubic-bezier(1, 0.5, 0.8, 1),
            color 0.5s cubic-bezier(1, 0.5, 0.8, 1);
    }
    .slide-left-leave-active {
        transition: transform 1s cubic-bezier(1, 0.5, 0.8, 1),
            color 1s cubic-bezier(1, 0.5, 0.8, 1);
    }
    .slide-left-enter {
        color: mediumblue;
        transform: translateY(20px);
    }
    .slide-left-leave-to {
        transform: skewY(90deg);
        color: cyan;
    }
&lt;/style&gt;</code></pre>
</div>

Here, we’re adding a dynamic transition name which is defined in the script section of our app. We’re also watching the `$route` so that whenever it changes, we run the function that checks if the current route has a param of `id` otherwise, we give it a value of `0`. We also determine the transition name based on the type of number the `id` is (i.e even or odd number). Now, if we navigate between the landing page and the different posts available, we would observe there are two types of transitions occurring as we navigate.

{{% ad-panel-leaderboard %}}

## Meta Fields And Navigation Guards

### Meta Fields

Meta fields help provide extra context to a certain route. An example of such context would be if a user needs to be authenticated to access such route or not. Here’s what this looks like:

<pre><code class="language-javascript">import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
Vue.use(VueRouter)
const routes = [{
        path: '/',
        name: 'Home',
        component: Home,
        // add meta to this route
        meta: {
            requiresAuth: true
        }
    },
]
const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
})
export default router</code></pre>
  
Here, we’ve added a meta property `requiresAuth` to the `/` route meaning we want users to be authenticated before they can access that route. Note that ‘requiresAuth’ is not a standard property, so you can choose any name you prefer. Whatever value you select at the end can be accessible in the `$route` object. This meta field at this point would not prevent unauthorized users from accessing that route, we need to hook it up to the Navigation guard.

### Navigation Guard

Just as the name implies, the navigation guard helps protect and guard routes based on your preferences (i.e redirect to another page or preventing the navigation). This feature works together with the Route Meta Fields to effectively guard the routes of your application. There are 3 ways of adding router guard in our app:

#### 1. **In-component**

Vue offers the option to configure your router guard for a particular route directly inside your components. Here’s an example in our `Home.vue` file:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="home"&gt;
        &lt;p v-if="loading" class="post--empty"&gt;Loading....&lt;/p&gt;
        &lt;ol v-else&gt;
             &lt;!-- add this text to your template --&gt;
            &lt;p v-if="guest"&gt;Hi Guest&lt;/p&gt;
            &lt;li v-for="post in posts" :key="post.id"&gt;
                &lt;router-link
                    :to="{ name: 'Post', params: { id: post.id, post: post } }"
                &gt;
                    {{ post.title }}
                &lt;/router-link&gt;
            &lt;/li&gt;
        &lt;/ol&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
    // @ is an alias to /src
    import axios from "axios";
    export default {
        name: "Home",
        data() {
            return {
                posts: null,
                // add this property
                guest: false,
                loading: false,
            };
        },
        // add this function
        beforeRouteEnter(to, from, next) {
            if (to.matched.some((record) =&gt; record.meta.requiresAuth)) {
                // this route requires auth, check if logged in
                // if not, display guest greeting.
                const loggedIn = JSON.parse(localStorage.getItem("loggedIn"));
                if (!loggedIn) {
                    next((vm) =&gt; {
                        vm.guest = true;
                    });
                } else {
                    next();
                }
            } else {
                next(); // make sure to always call next()!
            }
        },
        methods: {...}
    };
&lt;/script&gt;
&lt;style&gt;...&lt;/style&gt;</code></pre>
</div>  
  
Here, we’re adding a paragraph that is only visible to unauthenticated users. We also add a property that controls the visibility of this text. Finally we have a router method `beforeRouteEnter` in which we also connect the router guard and check if the user is authenticated or not using a value that would be manually added later. We also have an `if/else` statement, and inside this statement, we change the value of `guest` depending on the authentication of the user.

And in your `App.vue`, add this lifecycle to the file.

<pre><code class="language-javascript">export default {
        mounted() {
            localStorage.setItem("loggedIn", false);
        }
    };</code></pre>

So if you refresh your app, we should see the text we added in the `Home.vue` file.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ee779b8-99de-4a61-a61a-20ac2dcdf988/05-guest-user-text.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ee779b8-99de-4a61-a61a-20ac2dcdf988/05-guest-user-text.png" sizes="100vw" caption="Guest text visible. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ee779b8-99de-4a61-a61a-20ac2dcdf988/05-guest-user-text.png'>Large preview</a>)" alt="guest text on homepage" >}}

#### 2. **Per-route**

We can also add a router guard to our apps per-route in our router file as another property inside the specific route object. Here’s an example:

<pre><code class="language-javascript">{
        path: '/',
        name: 'Home',
        component: Home,
        // add meta to this route
        meta: {
            requiresAuth: true
        },
        beforeEnter: (to, from, next) =&gt; {
            if (to.name !== 'Home') {
                console.log('Per-Route navigation guard ti wa online');
                next()
            } else next()
        }
    }</code></pre>

Here, we add a router guard to the `/` route and we’re currently just logging a random text to the console but we can do a couple of things inside this guard. Now, each time you visit the home page, you would see this in your console:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545e8950-9776-4648-be89-1acc3840fa6b/06-message-in-terminal-vue-router.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545e8950-9776-4648-be89-1acc3840fa6b/06-message-in-terminal-vue-router.png" sizes="100vw" caption="Message printed in terminal. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545e8950-9776-4648-be89-1acc3840fa6b/06-message-in-terminal-vue-router.png'>Large preview</a>)" alt="router guard message printed in terminal" >}}

#### 3. **Globally**

We also have the option of creating a router guard that works globally for every part of the app (provided it meets the guard condition). This global guard is created in the router file just like the ***per-route guard*** but instead of defining it inside a specific route object, it is defined as a method of the `router` instance. For an example of how it works, we’re going to create a new file and route in our app and name it `guest.vue`, then add the following lines of code to the file.

<pre><code class="language-html">&lt;template&gt;
    &lt;div&gt;
        &lt;h1&gt;Guest page&lt;/h1&gt;
        &lt;p&gt;You're seeing this page because you are not logged in&lt;/p&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
&lt;/script&gt;
&lt;style&gt;&lt;/style&gt;</code></pre>

Next, we create a `/login` route with this newly created page and add a meta property to other existing routes.

<div class="break-out">

<pre><code class="language-javascript">    // create new route
    {
        path: '/login',
        name: 'login',
        component: () =&gt;
            import ( /* webpackChunkName: "auth" */ '../views/guest.vue')
    }, {
        path: '/:id',
        name: 'Post',
        props: true,a        // add meta property
        meta: {
            requiresAuth: true
        },
        component: () =&gt;
            import ( /* webpackChunkName: "post" */ '../views/Post.vue')
    }</code></pre>
</div>

The next thing would be to create the global navigation guard for all routes that require authentication and check the user’s authentication using `localStorage` (previously created). We would redirect users that have a `loggedIn` value of false to `/login`.

<div class="break-out">

<pre><code class="language-javascript">router.beforeEach((to, from, next) =&gt; {
    if (to.matched.some((record) =&gt; record.meta.requiresAuth)) {
        // this route requires auth, check if logged in
        // if not, display guest greeting.
        const loggedIn = JSON.parse(localStorage.getItem("loggedIn"));
        if (!loggedIn) {
            next({
                path: '/login'
            });
        } else {
            next();
        }
    } else {
        next(); // make sure to always call next()!
    }
})</code></pre>
</div>

So if you check your app in your browser, you would notice it is currently on this page:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efe12761-3cc2-4b9f-a857-f37ddb265b02/07-guest-page-vue-router.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efe12761-3cc2-4b9f-a857-f37ddb265b02/07-guest-page-vue-router.png" sizes="100vw" caption="Guest page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efe12761-3cc2-4b9f-a857-f37ddb265b02/07-guest-page-vue-router.png'>Large preview</a>)" alt="guest page" >}}

If we try to navigate to any of the existing routes, we would automatically get redirected to this page no what we do and that means our router guard is effectively guarding those routes.

## Conclusion

We can see that the Vue Router is a very powerful tool that can be used for more than just creating routes in your application. We have learned how to configure the scroll behavior of routes in our application, the different ways to add transitions to routes in our app, how to fetch data from an API before a component gets mounted, how to use meta property for our routes and the different ways to set up router guard.

### Resources

1. [Vue Router](https://router.vuejs.org/)
2. [CSS Transitions In Vuejs And Nuxtjs](https://www.smashingmagazine.com/2020/07/css-transitions-vuejs-nuxtjs/)

{{< signature "ks, ra, yk, il" >}}
