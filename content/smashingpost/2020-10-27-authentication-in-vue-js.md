---
title: 'Authentication In Vue.js'
slug: authentication-in-vue-js
author: precious-ndubueze
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/900e3cd6-cd49-4400-a2b3-70b252d04098/authentication-in-vue-js.png
date: 2020-10-27T14:30:00.000Z
summary: >-
  Every web application that handles user-specific data needs to implement authentication. Knowing how to do this is important for Vue developers, and that’s what this article aims to shed the spotlight on. This tutorial will prove to be useful for beginner developers who want to learn about authentication in Vue. In order to be able to follow along, you’ll need to have a good knowledge of Vue and Vuex.
description: >-
  This article is aimed at beginner developers who want to learn about authentication in Vue. In order to be able to follow along, you’ll need to have a good knowledge of Vue and Vuex.
categories:
  - Vue
  - Apps
  - JavaScript
  - Authentication
---

Authentication is a very necessary feature for applications that store user data. It’s a process of verifying the identity of users, ensuring that unauthorized users cannot access private data &mdash; data belonging to other users. This leads to having restricted routes that can only be accessed by authenticated users. These authenticated users are verified by using their login details (i.e. username/email and password) and assigning them with a token to be used in order to access an application’s protected resources.

In this article, you’re going to be learning about:

<ol>
  <li><a href="#vuex-configuration-with-axios">Vuex Configuration with Axios</a></li>
  <li><a href="#defining-routes">Defining Routes</a></li>
  <li><a href="#handling-users">Handling Users</a></li>
  <li><a href="#handling-expired-token">Handling Expired Token</a></li>
</ol>

### Dependencies

We will be working with the following dependencies that help in authentication:

- **Axios**  
For sending and retrieving data from our API
- **Vuex**  
For storing data gotten from our API 
- **Vue-Router**  
For navigation and protection of Routes

We will be working with these tools and see how they can work together to provide robust authentication functionality for our app. 

## The Backend API

We will be building a simple blog site, which will make use of this [API](https://gabbyblog.herokuapp.com). You can check out the [docs](https://gabbyblog.herokuapp.com/docs) to see the endpoints and how requests should be sent. 

From the docs, you’ll notice few endpoints are attached with a lock. This is a way to show that only authorized users can send requests to those endpoints. The unrestricted endpoints are the `/register` and `/login`  endpoints. An error with the status code `401` should be returned when an unauthenticated user attempts to access a restricted endpoint.

After successfully logging in a user, the access token alongside some data will be received in the Vue app, which will be used in setting the cookie and attached in the request header to be used for future requests. The backend will check the request header each time a request is made to a restricted endpoint. [Don’t be tempted to store](https://dev.to/rdegges/please-stop-using-local-storage-1i04) [the](https://dev.to/rdegges/please-stop-using-local-storage-1i04) [access token in the local storage.](https://dev.to/rdegges/please-stop-using-local-storage-1i04)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65e9dec2-7442-4946-af09-4a701475e2d0/auth-diagram.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65e9dec2-7442-4946-af09-4a701475e2d0/auth-diagram.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65e9dec2-7442-4946-af09-4a701475e2d0/auth-diagram.png'>Large preview</a>)" alt="" >}}

{{% feature-panel %}}

## Scaffold Project 

Using the Vue CLI, run the command below to generate the application:

<pre><code class="language-javascript">vue create auth-project
</code></pre>

Navigate into your new folder:

<pre><code class="language-bash">cd auth-project
</code></pre>

Add the vue-router and install more dependencies &mdash; vuex and axios:

<pre><code class="language-javascript">vue add router
    npm install vuex axios
</code></pre>

Now run your project and you should see what I have below on your browser:

<pre><code class="language-bash">npm run serve
</code></pre>

## 1. Vuex Configuration with Axios

Axios is a JavaScript library that is used to send requests from the browser to APIs. According to the Vuex [documentation](https://vuex.vuejs.org/); 

<blockquote>“Vuex is a <strong>state management pattern + library</strong> for Vue.js applications. It serves as a centralized store for all the components in an application, with rules ensuring that the state can only be mutated in a predictable fashion.”</blockquote>

What does that mean? Vuex is a store used in a Vue application that allows us to *save* data that will be available to every component and provide ways to change such data. We’ll use Axios in Vuex to send our requests and make changes to our state (data). Axios will be used in Vuex `actions` to send `GET` and `POST`, response gotten will be used in sending information to the `mutations` and which updates our store data.

To deal with Vuex resetting after refreshing we will be working with [`vuex-persistedstate`](https://www.npmjs.com/package/vuex-persistedstate), a library that saves our Vuex data between page reloads.

<pre><code class="language-bash">npm install --save vuex-persistedstate
</code></pre>

Now let’s create a new folder `store` in `src`, for configuring the Vuex store. In the `store` folder, create a new folder;  `modules` and a file `index.js`. It’s important to note that you only need to do this if the folder does not get created for you automatically.

<pre><code class="language-javascript">import Vuex from 'vuex';
import Vue from 'vue';
import createPersistedState from "vuex-persistedstate";
import auth from './modules/auth';

// Load Vuex
Vue.use(Vuex);
// Create store
export default new Vuex.Store({
  modules: {
    auth
  },
  plugins: [createPersistedState()]
});
</code></pre>

Here we are making use of `Vuex` and importing an auth `module` from the `modules` folder into our store.

### Modules

[Modules](https://vuex.vuejs.org/guide/modules.html) are different segments of our store that handles similar tasks together, including:

<ul>
  <li><a href="#state">state</a></li>
  <li><a href="#actions">actions</a></li>
  <li><a href="#mutations">mutations</a></li>
  <li><a href="#getters">getters</a></li>
</ul>

Before we proceed, let’s edit our `main.js` file.

<pre><code class="language-javascript">import Vue from 'vue'
import App from './App.vue'
import router from './router';
import store from './store';
import axios from 'axios';

axios.defaults.withCredentials = true
axios.defaults.baseURL = 'https://gabbyblog.herokuapp.com/';

Vue.config.productionTip = false
new Vue({
  store,
  router,
  render: h => h(App)
}).$mount('#app')
</code></pre>

We imported the `store` object from the `./store` folder as well as the Axios package.

As mentioned earlier, the access token cookie and other necessary data got from the API need to be set in the request headers for future requests. Since we’ll be making use of Axios when making requests we need to configure Axios to make use of this. In the snippet above, we do that using `axios.defaults.withCredentials = true`, this is needed because by default cookies are not passed by Axios.

`aaxios.defaults.withCredentials = true` is an instruction to Axios to send all requests with credentials such as; authorization headers, TLS client certificates, or cookies (as in our case).
 
We set our `axios.defaults.baseURL` for our Axios request to our `API` This way, whenever we’re sending via Axios, it makes use of this base URL. With that, we can add just our endpoints like `/register` and `/login` to our actions without stating the full URL each time.

Now inside the `modules` folder in `store` create a file called `auth.js`

<pre><code class="language-javascript">//store/modules/auth.js

import axios from 'axios';
const state = {

};
const getters = {

};
const actions = {

};
const mutations = {

};
export default {
  state,
  getters,
  actions,
  mutations
};
</code></pre>

#### <code>state</code>

In our [`state`](https://vuex.vuejs.org/guide/state.html) dict, we are going to define our data, and their default values:

<pre><code class="language-javascript">const state = {
  user: null,
  posts: null,
};
</code></pre>

We are setting the default value of `state`, which is an object that contains `user` and `posts` with their initial values as `null`.

#### Actions

[Actions](https://vuex.vuejs.org/guide/actions.html) are functions that are used to `commit` a mutation to change the state or can be used to `dispatch` i.e calls another action. It can be called in different components or views and then commits mutations of our state;

**Register Action**

Our `Register` action takes in form data,  sends the data to our `/register` endpoint, and assigns the response to a variable `response`. Next, we will be dispatching our form `username` and `password` to our `login` action. This way, we log in the user after they sign up, so they are redirected to the `/posts` page.

<pre><code class="language-javascript">async Register({dispatch}, form) {
  await axios.post('register', form)
  let UserForm = new FormData()
  UserForm.append('username', form.username)
  UserForm.append('password', form.password)
  await dispatch('LogIn', UserForm)
},
</code></pre>

**Login Action**

Here is where the main authentication happens. When a user fills in their username and password, it is passed to a `User` which is a FormData object, the `LogIn` function takes the `User`  object and makes a `POST` request to the `/login` endpoint to log in the user.

The `Login` function finally commits the `username` to the `setUser` mutation. 

<pre><code class="language-javascript">async LogIn({commit}, User) {
  await axios.post('login', User)
  await commit('setUser', User.get('username'))
},
</code></pre>

**Create Post Action**

Our `CreatePost` action is a function, that takes in the `post` and sends it to our `/post` endpoint, and then dispatches the `GetPosts` action. This enables the user to see their posts after creation. 

<pre><code class="language-javascript">async CreatePost({dispatch}, post) {
  await axios.post('post', post)
  await dispatch('GetPosts')
},
</code></pre>

**Get Posts Action**

Our `GetPosts` action sends a `GET` request to our `/posts` endpoint to fetch the posts in our API and commits `setPosts` mutation.

<pre><code class="language-javascript">async GetPosts({ commit }){
  let response = await axios.get('posts')
  commit('setPosts', response.data)
},
</code></pre>

**Log Out Action**

<pre><code class="language-javascript">async LogOut({commit}){
  let user = null
  commit('logout', user)
}
</code></pre>

Our `LogOut` action removes our `user`  from the browser cache. It does this by committing a `logout`:

#### Mutations

<pre><code class="language-javascript">const mutations = {
    setUser(state, username){
        state.user = username
    },
    setPosts(state, posts){
        state.posts = posts
    },
    LogOut(state){
        state.user = null
        state.posts = null
    },
};
</code></pre>

Each [mutation](https://vuex.vuejs.org/guide/mutations.html) takes in the `state` and a value from the action committing it, aside `Logout`. The value gotten is used to change certain parts or all or like in  `LogOut` set all variables back to null.

#### Getters

[Getters](https://vuex.vuejs.org/guide/getters.html) are functionalities to get the state. It can be used in multiple components to get the current state.
The `isAuthenticatated` function checks if the `state.user` is defined or null and returns `true` or `false` respectively. `StatePosts` and `StateUser` return `state.posts` and `state.user` respectively value.

<pre><code class="language-javascript">const getters = {
    isAuthenticated: state => !!state.user,    
    StatePosts: state => state.posts,
    StateUser: state => state.user,
};
</code></pre>

Now your whole `auth.js` file should resemble my code on [GitHub](https://github.com/gabbyprecious/vue-blog/blob/master/src/store/modules/auth.js).

{{% ad-panel-leaderboard %}}

## Setting Up Components

### 1. `NavBar.vue` And `App.vue` Components

In your `src/components` folder, delete the `HelloWorld.vue` and a new file called `NavBar.vue`.

This is the component for our navigation bar, it links to different pages of our component been routed here. Each router link points to a route/page on our app. 

The `v-if="isLoggedIn"` is a condition to display the `Logout`  link if a user is logged in and hide the `Register` and `Login` routes. We have a `logout` method which can only be accessible to signed-in users, this will get called when the `Logout` link is clicked. It will dispatch the `LogOut` action and then direct the user to the login page.

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="nav"&gt;
    &lt;router-link to="/"&gt;Home&lt;/router-link&gt; |
    &lt;router-link to="/posts"&gt;Posts&lt;/router-link&gt; |
    &lt;span v-if="isLoggedIn"&gt;
      &lt;a @click="logout"&gt;Logout&lt;/a&gt;
    &lt;/span&gt;
    &lt;span v-else&gt;
      &lt;router-link to="/register"&gt;Register&lt;/router-link&gt; |
      &lt;router-link to="/login"&gt;Login&lt;/router-link&gt;
    &lt;/span&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  name: 'NavBar',
  computed : {
      isLoggedIn : function(){ return this.$store.getters.isAuthenticated}
    },
    methods: {
      async logout (){
        await this.$store.dispatch('LogOut')
        this.$router.push('/login')
      }
    },
}
&lt;/script&gt;
&lt;style&gt;
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
a:hover {
  cursor: pointer;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
&lt;/style&gt;
</code></pre>
</div>

Now edit your `App.vue` component to look like this:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;NavBar /&gt;
    &lt;router-view/&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue'
export default {
  components: {
    NavBar
  }
}
&lt;/script&gt;
&lt;style&gt;
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
&lt;/style&gt;
</code></pre>

Here we imported the NavBar component which we created above and placed in the template section before the `<router-view />`.

### 2. Views Components

Views components are different pages on the app that will be defined under a route and can be accessed from the navigation bar. To get started Go to the `views` folder, delete the `About.vue` component, and add the following components:

<ul>
  <li><a href="#home-vue"><code>Home.vue</code></a></li>
  <li><a href="#register-vue"><code>Register.vue</code></a></li>
  <li><a href="#login-vue"><code>Login.vue</code></a></li>
  <li><a href="#posts-vue"><code>Posts.vue</code></a></li>
</ul>

#### <code>Home.vue</code>

Rewrite the `Home.vue` to look like this:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="home"&gt;
  &lt;p&gt;Heyyyyyy welcome to our blog, check out our posts&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;

export default {
  name: 'Home',
  components: {
  }
}
&lt;/script&gt;
</code></pre>

This will display a welcome text to the users when they visit the homepage.

#### <code>Register.vue</code>

This is the Page we want our users to be able to sign up on our application. When the users fill the form, their information is been sent to the API and added to the database then logged in.

Looking at the API, the `/register` endpoint requires a `username`, `full_name` and `password` of our user. Now let’s create a page and a form to get those information:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="register"&gt;
      &lt;div&gt;
          &lt;form @submit.prevent="submit"&gt;
            &lt;div&gt;
              &lt;label for="username"&gt;Username:&lt;/label&gt;
              &lt;input type="text" name="username" v-model="form.username"&gt;
            &lt;/div&gt;
            &lt;div&gt;
              &lt;label for="full_name"&gt;Full Name:&lt;/label&gt;
              &lt;input type="text" name="full_name" v-model="form.full_name"&gt;
            &lt;/div&gt;
            &lt;div&gt;
              &lt;label for="password"&gt;Password:&lt;/label&gt;
              &lt;input type="password" name="password" v-model="form.password"&gt;
            &lt;/div&gt;
            &lt;button type="submit"&gt; Submit&lt;/button&gt;
          &lt;/form&gt;
      &lt;/div&gt;
      &lt;p v-if="showError" id="error"&gt;Username already exists&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

In the <code>Register</code> component, we’ll need to call the `Register` action which will receive the form data.

<pre><code class="language-javascript">&lt;script&gt;
import { mapActions } from "vuex";
export default {
  name: "Register",
  components: {},
  data() {
    return {
      form: {
        username: "",
        full_name: "",
        password: "",
      },
      showError: false
    };
  },
  methods: {
    ...mapActions(["Register"]),
    async submit() {
      try {
        await this.Register(this.form);
        this.$router.push("/posts");
        this.showError = false
      } catch (error) {
        this.showError = true
      }
    },
  },
};
&lt;/script&gt;
</code></pre>

We start by importing `mapActions` from Vuex, what this does is to import actions from our store to the component. This allows us to call the action from the component.

`data()` contains the local state value that will be used in this component, we have a `form` object that contains `username`, `full_name` and `password`, with their initial values set to an empty string. We also have `showError` which is a boolean, to be used to either show an error or not.

In the `methods` we import the `Register` action using the `Mapactions` into the component, so the `Register` action can be called with `this.Register` .

We have a submit method this calls the `Register` action which we have access to using `this.Register`, sending it `this.form`. If no `error` is encountered we make use of `this.$router` to send the user to the login page. Else we set `showError` to true.

Having done that, we can include some styling.

<pre><code class="language-javascript">&lt;style scoped&gt;
* {
  box-sizing: border-box;
}
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}
button[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  cursor: pointer;
  border-radius:30px;
}
button[type=submit]:hover {
  background-color: #45a049;
}
input {
  margin: 5px;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  padding:10px;
  border-radius:30px;
}
#error {
  color: red;
}
&lt;/style&gt;
</code></pre>

#### <code>Login.vue</code>

Our LogIn page is where registered users, will enter their `username`  and `password` to get authenticated by the API and logged into our site.

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="login"&gt;
    &lt;div&gt;
      &lt;form @submit.prevent="submit"&gt;
        &lt;div&gt;
          &lt;label for="username"&gt;Username:&lt;/label&gt;
          &lt;input type="text" name="username" v-model="form.username" /&gt;
        &lt;/div&gt;
        &lt;div&gt;
          &lt;label for="password"&gt;Password:&lt;/label&gt;
          &lt;input type="password" name="password" v-model="form.password" /&gt;
        &lt;/div&gt;
        &lt;button type="submit"&gt;Submit&lt;/button&gt;
      &lt;/form&gt;
      &lt;p v-if="showError" id="error"&gt;Username or Password is incorrect&lt;/p&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

Now we’ll have to pass our form data to the action that sends the request and then push them to the secure page `Posts`

<pre><code class="language-javascript">&lt;script&gt;
import { mapActions } from "vuex";
export default {
  name: "Login",
  components: {},
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
      showError: false
    };
  },
  methods: {
    ...mapActions(["LogIn"]),
    async submit() {
      const User = new FormData();
      User.append("username", this.form.username);
      User.append("password", this.form.password);
      try {
          await this.LogIn(User);
          this.$router.push("/posts");
          this.showError = false
      } catch (error) {
        this.showError = true
      }
    },
  },
};
&lt;/script&gt;
</code></pre>

We import `Mapactions` and use it in importing the `LogIn` action into the component, which will be used in our `submit` function. 

After the `Login` action, the user is redirected to the `/posts` page. In case of an error, the error is caught and `ShowError` is set to true.

{{% ad-panel-leaderboard %}}

Now, some styling:

<pre><code class="language-javascript">&lt;style scoped&gt;
* {
  box-sizing: border-box;
}
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}
button[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  cursor: pointer;
  border-radius:30px;
}
button[type=submit]:hover {
  background-color: #45a049;
}
input {
  margin: 5px;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  padding:10px;
  border-radius:30px;
}
#error {
  color: red;
}
&lt;/style&gt;
</code></pre>

#### <code>Posts.vue</code>

Our Posts page is the secured page that is only available to authenticated users. On this page, they get access to posts in the API’s database. This allows the users to have access to posts and also enables them to create posts to the API. 

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="posts"&gt;
      &lt;div v-if="User"&gt;
        &lt;p&gt;Hi {{User}}&lt;/p&gt;
      &lt;/div&gt;
      &lt;div&gt;
          &lt;form @submit.prevent="submit"&gt;
            &lt;div&gt;
              &lt;label for="title"&gt;Title:&lt;/label&gt;
              &lt;input type="text" name="title" v-model="form.title"&gt;
            &lt;/div&gt;
            &lt;div&gt;
              &lt;textarea name="write_up" v-model="form.write_up" placeholder="Write up..."&gt;&lt;/textarea&gt;
            &lt;/div&gt;
            &lt;button type="submit"&gt; Submit&lt;/button&gt;
          &lt;/form&gt;
      &lt;/div&gt;
      &lt;div class="posts" v-if="Posts"&gt;
        &lt;ul&gt;
          &lt;li v-for="post in Posts" :key="post.id"&gt;
            &lt;div id="post-div"&gt;
              &lt;p&gt;{{post.title}}&lt;/p&gt;
              &lt;p&gt;{{post.write_up}}&lt;/p&gt;
              &lt;p&gt;Written By: {{post.author.username}}&lt;/p&gt;
            &lt;/div&gt;
          &lt;/li&gt;
        &lt;/ul&gt;
      &lt;/div&gt;
      &lt;div v-else&gt;
        Oh no!!! We have no posts
      &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

In the above code, we have a form for the user to be able to create new posts. Submitting the form should cause the post to be sent to the API &mdash; we’ll add the method that does that shortly. We also have a section that displays posts obtained from the API (in case the user has any). If the user does not have any posts, we simply display a message that there are no posts.

The `StateUser` and `StatePosts` getters are mapped i.e imported using `mapGetters` into `Posts.vue` and then they can be called in the template. 

<pre><code class="language-javascript">&lt;script&gt;
import { mapGetters, mapActions } from "vuex";
export default {
  name: 'Posts',
  components: {
    
  },
  data() {
    return {
      form: {
        title: '',
        write_up: '',
      }
    };
  },
  created: function () {
    // a function to call getposts action
    this.GetPosts()
  },
  computed: {
    ...mapGetters({Posts: "StatePosts", User: "StateUser"}),
  },
  methods: {
    ...mapActions(["CreatePost", "GetPosts"]),
    async submit() {
      try {
        await this.CreatePost(this.form);
      } catch (error) {
        throw "Sorry you can't make a post now!"
      }
    },  
  }
};
&lt;/script&gt;
</code></pre>

We have an initial state for `form`, which is an object which has `title` and `write_up` as its keys and the values are set to an empty string. These values will change to whatever the user enters into the form in the template section of our component.

When the user submits the post, we call the `this.CreatePost` which receives the form object.

As you can see in the `created` lifecycle, we have `this.GetPosts` to fetch posts when the component is created.

Some styling,

<pre><code class="language-css">&lt;style scoped&gt;
&#42; {
  box-sizing: border-box;
}
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}
button[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  cursor: pointer;
  border-radius:30px;
  margin: 10px;
}
button[type=submit]:hover {
  background-color: #45a049;
}
input {
  width:60%;
  margin: 15px;
  border: 0;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  padding:10px;
  border-radius:30px;
}
textarea {
  width:75%;
  resize: vertical;
  padding:15px;
  border-radius:15px;
  border:0;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  height:150px;
  margin: 15px;
}
ul {
  list-style: none;
}
#post-div {
  border: 3px solid #000;
  width: 500px;
  margin: auto;
  margin-bottom: 5px;;
}
&lt;/style&gt;
</code></pre>
    
## 2. Defining Routes

In our `router/index.js` file, import our views and define routes for each of them

<pre><code class="language-javascript">import Vue from 'vue'
import VueRouter from 'vue-router'
import store from '../store';
import Home from '../views/Home.vue'
import Register from '../views/Register'
import Login from '../views/Login'
import Posts from '../views/Posts'

Vue.use(VueRouter)
const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/register',
    name: "Register",
    component: Register,
    meta: { guest: true },
  },
  {
    path: '/login',
    name: "Login",
    component: Login,
    meta: { guest: true },
  },
  {
    path: '/posts',
    name: Posts,
    component: Posts,
    meta: {requiresAuth: true},
  }
]
const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
</code></pre>

## 3. Handling Users

- **Unauthorized Users**  
If you noticed in defining our posts routes we added a `meta` key to indicate that the user must be authenticated, now we need to have a `router.BeforeEach` navigation guard that checks if a route has the `meta: {requiresAuth: true}` key. If a route has the `meta` key, it checks the store for a token; if present, it redirects them to the `login` route. 

<pre><code class="language-javascript">const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})
router.beforeEach((to, from, next) => {
  if(to.matched.some(record => record.meta.requiresAuth)) {
    if (store.getters.isAuthenticated) {
      next()
      return
    }
    next('/login')
  } else {
    next()
  }
})

export default router
</code></pre>

- **Authorized Users**  
We also have a `meta` on the `/register` and `/login` routes.  The `meta: {guest: true}` stops users that are logged in from accessing the routes with the `guest` meta.

<pre><code class="language-javascript">router.beforeEach((to, from, next) => {
  if (to.matched.some((record) => record.meta.guest)) {
    if (store.getters.isAuthenticated) {
      next("/posts");
      return;
    }
    next();
  } else {
    next();
  }
});
</code></pre>   

In the end, your file should be like [this](https://github.com/gabbyprecious/vue-blog/blob/master/src/router/index.js):

<pre><code class="language-javascript">import Vue from "vue";
import VueRouter from "vue-router";
import store from "../store";
import Home from "../views/Home.vue";
import Register from "../views/Register";
import Login from "../views/Login";
import Posts from "../views/Posts";

Vue.use(VueRouter);

const routes = [
  {
    path: "/",
    name: "Home",
    component: Home,
  },
  {
    path: "/register",
    name: "Register",
    component: Register,
    meta: { guest: true },
  },
  {
    path: "/login",
    name: "Login",
    component: Login,
    meta: { guest: true },
  },
  {
    path: "/posts",
    name: "Posts",
    component: Posts,
    meta: { requiresAuth: true },
  },
];

const router = new VueRouter({
  mode: "history",
  base: process.env.BASE_URL,
  routes,
});

router.beforeEach((to, from, next) => {
  if (to.matched.some((record) => record.meta.requiresAuth)) {
    if (store.getters.isAuthenticated) {
      next();
      return;
    }
    next("/login");
  } else {
    next();
  }
});

router.beforeEach((to, from, next) => {
  if (to.matched.some((record) => record.meta.guest)) {
    if (store.getters.isAuthenticated) {
      next("/posts");
      return;
    }
    next();
  } else {
    next();
  }
});

export default router;
</code></pre>

## 4.Handling Expired Token (Forbidden Requests)

Our API is set to expire tokens after 30 minutes, now if we try accessing the `posts` page after 30 minutes,  we get a `401` error, which means we have to log in again, so we will set an interceptor that reads if we get a `401` error then it redirects us back to the `login` page.

Add the snippet below after the Axios default URL declaration in the `main.js` file.

<pre><code class="language-javascript">axios.interceptors.response.use(undefined, function (error) {
  if (error) {
    const originalRequest = error.config;
    if (error.response.status === 401 && !originalRequest._retry) {
  
        originalRequest._retry = true;
        store.dispatch('LogOut')
        return router.push('/login')
    }
  }
})
</code></pre>

This should take your code to the same state as the example on [GitHub](https://github.com/gabbyprecious/vue-blog/blob/master/src/main.js).

## Conclusion

If you've been able to follow along until the end, you should now be able to build a fully functional and secure front-end application. Now you’ve learned more about Vuex and how to integrate it with Axios, and also how to save its data after reloading. 

- [The code is available on GitHub&nbsp;&rarr;](https://github.com/gabbyprecious/vue-blog)

- Hosted site: `https://nifty-hopper-1e9895.netlify.app/`
- API: `https://gabbyblog.herokuapp.com`
- API Docs: `https://gabbyblog.herokuapp.com/docs`

### Resources

- “[Handling Cookies With Axios](https://medium.com/acmvit/handling-cookies-with-axios-872790241a9b),” Aditya Srivastava, Medium
- “[Creating An Authentication Navigation Guard In Vue](https://tenmilesquare.com/creating-an-authentication-navigation-guard-in-vue/),” Laurie Barth, Ten Mile Square Blog
- “[Getting Started With Vuex](https://vuex.vuejs.org/guide/),” Official Guide
- “[Vue.js JWT Authentication With Vuex And Vue Router](https://bezkoder.com/jwt-vue-vuex-authentication/),” BezKoder

{{< signature "ks, ra, il" >}}
