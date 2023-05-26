---
title: 'Getting Started With Axios In Nuxt'
slug: getting-started-axios-nuxt
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5d3cd68-7e44-474e-a8e3-a1ecccd6d1c9/getting-started-axios-nuxt.png
date: 2020-05-26T09:00:00.000Z
summary: >-
  In this tutorial, we will learn how to make a request in our Nuxt.js applications using the Axios module. We will also learn how to use the `ayncData` and `fetch` methods to fetch data on the server-side using Axios and the differences between the two methods. Finally, we will learn how to add authentication to our application using the Auth module.
description: >-
  In this tutorial, we will learn how to make a request in our Nuxt.js applications using the Axios module. We will also learn how to use the `ayncData` and `fetch` methods to fetch data on the server-side and the differences between the two methods.
categories:
  - Vue
  - Node.js
  - Nuxt.js
  - Authentication
  - JavaScript
---

Nuxt.js provides an Axios module for easy integration with your application. Axios is a promise-based HTTP client that works in the browser and Node.js environment or, in simpler terms, it is a tool for making requests (e.g API calls) in client-side applications and Node.js environment.

In this tutorial, we’re going to learn how to use the Axios module and how to make a request on the server-side using [asyncData](https://nuxtjs.org/guide/async-data/) and fetch. These two methods make a request on the server-side but they have some differences which we’re also going to cover. Finally, we’ll learn how to perform authentication and secure pages/routes using the auth module and auth middleware.

*This article requires basic knowledge of Nuxtjs and Vuejs as we’ll be building on top of that. For those without experience with Vuejs, I recommend you start from their [official documentation](https://vuejs.org/) and the [Nuxt official page](https://nuxtjs.org/) before continuing with this article.*

## What Is The Nuxt.js Axios Module?

According to the [official Documentation](https://axios.nuxtjs.org/),

<blockquote>“It is a Secure and easy Axios integration with Nuxt.js.”</blockquote>

Here are some of its features:

1. Automatically set base URL for client-side & server-side.
2.  Proxy request headers in SSR (Useful for auth).
3. Fetch Style requests.
4. Integrated with Nuxt.js Progressbar while making requests.

To use the axios module in your application, you will have to first install it by using either `npm` or `yarn`.

**YARN**

<pre><code class="language-bash">yarn add @nuxtjs/axios</code></pre>

**NPM** 

<pre><code class="language-bash">npm install @nuxtjs/axios</code></pre>

Add it into your `nuxt.config.js` file:

<pre><code class="language-javascript">modules: [
    '@nuxtjs/axios',
  ],

  axios: {
    // extra config e.g
    // BaseURL: 'https://link-to-API'
  }</code></pre>

The `modules` array accepts a list of Nuxt.js modules such as dotenv, auth and in this case, Axios. What we've done is to inform our application that we would be using the Axios module, which we reference using `@nuxtjs/axios`. This is then followed by the `axios` property which is an object of configurations like the baseURL for both client-side and server-side. 

Now, you can access Axios from anywhere in your application by calling `this.$axios.method` or `this.$axios.$method`. Where *method* can be `get`, `post`, or `delete`.

{{% feature-panel %}}

## Making Your First Request Using Axios

For this tutorial, I’ve put together a simple application on [Github](https://github.com/Timibadass/nuxt-report-app). The repository contains two folders, start and finish, the [*start*](https://github.com/Timibadass/nuxt-report-app/tree/master/start) [folder](https://github.com/Timibadass/nuxt-report-app/tree/master/start) contains all you need to get right into the tutorial. The *finish* folder contains a completed version of what we would be building. 

After cloning the repo and opening the `start` folder, we would need to install all our packages in the `package.json` file so open your terminal and run the following command:

<pre><code class="language-bash">npm install</code></pre>

Once that is done, we can start our app using the `npm run dev` command. This is what you should see when you go to `localhost:3000`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf9d008b-7a43-4886-af85-12c628cbe3e1/01-landing-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf9d008b-7a43-4886-af85-12c628cbe3e1/01-landing-page.png" sizes="100vw" caption="Our application’s landing page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf9d008b-7a43-4886-af85-12c628cbe3e1/01-landing-page.png'>Large preview</a>)" alt="A page with header containing a logo and navigation links." >}}

The next thing we have to do is to create a `.env` file in the root folder of our application and add our API URL to it. For this tutorial, we’ll be using a sample API built to collect reports from users.

<pre><code class="language-javascript">API_URL=https://ireporter-endpoint.herokuapp.com/api/v2/</code></pre>
    
This way, we do not have to hard code our API into our app which is useful for working with two APIs (development and production).

The next step would be to open our `nuxt.config.js` file and add the environmental variable to our axios config that we added above.

<div class="break-out">

<pre><code class="language-javascript">/*
   ** Axios module configuration
   */
  axios: {
    // See https://github.com/nuxt-community/axios-module#options
    baseURL: process.env.API_URL,
  },</code></pre>
</div>

Here, we tell Nuxt.js to use this `baseURL` for both our *client-side* and *server-side* requests whenever we use this Axios module. 

Now, to fetch a list of reports, let us open the `index.vue` file and add the following method to the script section. 

<pre><code class="language-javascript">async getIncidents() {
  let res = await this.$store.dispatch("getIncidents");
  this.incidents = res.data.data.incidents;
}</code></pre>

What we have done is to create an async function that we call `getIncidents()` and we can tell what it does from the name &mdash; it fetches a list of incidents using the Vuex store action method `this.$store.dispatch`. We assign the response from this action to our incidents property so we can be able to make use of it in the component.

We want to call the `getIncidents()` method whenever the component mounts. We can do that using the `mounted` hook.

<pre><code class="language-javascript">mounted() {
    this.getIncidents()
  }</code></pre>

`mounted()` is a [lifecycle hook](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram) that gets called when the component mounts. That will cause the call to the API to happen when the component mounts. Now, let us go into our `index.js` file in our store and create this action where we’ll be making our Axios request from. 

<pre><code class="language-javascript">export const actions = {
  async getIncidents() {
    let res = await this.$axios.get('/incidents')
    return res;
  }
}</code></pre>

Here, we created the action called `getIncidents` which is an async function, then we *await* a response from the server and return this response. The response from this action is sent back to our `getIncidents()` method in our `index.vue` file.

If we refresh our application, we should now be able to see a long list of incidents rendered on the page. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ced60dd9-f9bb-4886-8a79-5a292ec74905/02-landing-page-with-incidents-list.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ced60dd9-f9bb-4886-8a79-5a292ec74905/02-landing-page-with-incidents-list.png" sizes="100vw" caption="List of incidents on landing page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ced60dd9-f9bb-4886-8a79-5a292ec74905/02-landing-page-with-incidents-list.png'>Large preview</a>)" alt="A list of dummy incidents." >}}

We have made our first request using Axios but we won’t stop there, we are going to be trying out `asyncData` and `fetch` to see the differences between them and using Axios. 

### AsyncData

AsyncData fetches data on the server-side and it’s called before loading the page component. It does not have access to `this` because it is called before your page component data is created. `this`  is only available after the `created` hook has been called so Nuxt.js automatically merges the returned data into the component’s data.

Using `asyncData` is good for SEO because it fetches your site’s content on the server-side and also helps in loading content faster.
Note that `asyncData` method can only be used in the pages folder of your application as it would not work in the components folder. This is because `asyncData` hook gets called before your component is created.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90aed40f-ad71-4e16-9beb-9c7c9341ab02/03-new-fetch-lifecycle-hooks.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90aed40f-ad71-4e16-9beb-9c7c9341ab02/03-new-fetch-lifecycle-hooks.png" sizes="100vw" caption="Image from Nuxt blog. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90aed40f-ad71-4e16-9beb-9c7c9341ab02/03-new-fetch-lifecycle-hooks.png'>Large preview</a>)" alt="An Image showing the Nuxt life cycle." >}}

Let us add `asyncData` to our `index.vue` file and observe how fast our *incidents* *data* loads. Add the following code after our *components* property and let us get rid of our mounted hook.

<pre><code class="language-javascript">async asyncData({ $axios }) {
    let { data } = await $axios.get("/incidents");
    return { incidents: data.data.incidents };
  },
  // mounted() {
  //   this.getIncidents();
  // },</code></pre>

Here, the `asyncData` method accepts a property from [the context](https://nuxtjs.org/api/context) `$axios`. We use this property to fetch the list of incidents and the value is then returned. This value is automatically injected into our component. Now, you can notice how fast your content loads if you refresh the page and *at no time* is there no incident to render. 

### Fetch

The Fetch method is also used to make requests on the server-side. It is called after the created hook in the life cycle which means it has access to the component’s data. Unlike the `asyncData` method, the fetch method can be used in all **.vue** files and be used with the *Vuex store.* This means that if you have the following in your data function. 

<pre><code class="language-javascript">data() {
    return {
      incidents: [],
      id: 5,
      gender: 'male'
    };
}</code></pre>

You can easily modify *id* or *gender* by calling `this.id` or `this.gender`.

{{% ad-panel-leaderboard %}}

## Using Axios As A Plugin

During the process of development with Axios, you might find that you need extra configuration like creating instances and interceptors for your request so your application can work as intended and thankfully, we can do that by extending our Axios into a plugin. 

To extend `axios`, you have to create a plugin (e.g. *axios.js*) in your `plugins` folder.

<div class="break-out">

<pre><code class="language-javascript">export default function ({
  $axios,
  store,
  redirect
}) {
  $axios.onError(error => {
    if (error.response && error.response.status === 500) {
      redirect('/login')
    }
  })
  $axios.interceptors.response.use(
    response => {
      if (response.status === 200) {
        if (response.request.responseURL && response.request.responseURL.includes('login')) {
          store.dispatch("setUser", response);
        }
      }
      return response
    }
  )
}</code></pre>
</div>

This is an example of a plugin I wrote for a Nuxt application. Here, your function takes in a [context object](https://nuxtjs.org/api/context) of `$axios`, `store` and `redirect` which we would use in configuring the plugin. The first thing we do is to listen for an error with a status of `500` using `$axios.onError` and redirect the user to the login page.

We also have an interceptor that intercepts every request response we make in our application checks if the status of the response we get is `200`. If that is true we proceed and check that there is a `response.request.responseURL` and if it includes login. If this checks out to be true, we then send this response using our store’s dispatch method where it then mutated in our state. 

Add this plugin to your `nuxt.config.js` file:

<pre><code class="language-javascript">plugins: [
    '~/plugins/axios'
  ]</code></pre>

After doing this, your Axios plugin would intercept any request you make and check if you have defined a special case for it. 

## Introduction To The Auth Module

The auth module is used for performing authentication for your Nuxt application and can be accessed from anywhere in your application using `$this.auth`. It is also available in `fetch`, `asyncData`, `middleware` and `NuxtInitServer` from the context object as `$auth`.

The `context` provides additional objects/params from Nuxt to Vue components and is available in special nuxt lifecycle areas like those mentioned above.

To use the auth module in your application, you would have to install it using `yarn` or `npm`.

**YARN**

<pre><code class="language-bash">yarn add @nuxtjs/auth</code></pre>

**NPM**

<pre><code class="language-bash">npm install @nuxtjs/auth</code></pre>

Add it to your `nuxt.config.js` file.

<pre><code class="language-javascript">modules: [
  '@nuxtjs/auth'
],
auth: {
  // Options
}</code></pre>

The *auth* property accepts a list of properties such as `strategies` and `redirect`. Here, `strategies` accepts your preferred authentication method which can be:

- `local`  
For username/email and password-based flow.
- `facebook`  
For using Facebook accounts as a means of authentication.
- `Github`  
For authenticating users with Github accounts.
- `Google`  
For authenticating users with Google accounts. 
- Auth0
- Laravel Passport

<p id="redirect">The <strong>redirect property</strong> accepts an object of links for:</p>

- `login`  
Users would be redirected to this link if login is required.
- `logout`  
Users would be redirected here if after logout current route is protected.
- `home`  
Users would be redirected here after login. 

Now, let us add the following to our `nuxt.config.js` file.

<pre><code class="language-javascript">/*
 ** Auth module configuration
 */
auth: {
  redirect: {
    login: '/login',
    logout: '/',
    home: '/my-reports'
  },
  strategies: {
    local: {
      endpoints: {
        login: {
          url: "/user/login",
          method: "post",
          propertyName: "data.token",
        },
        logout: false,
        user: false,
      },
      tokenType: '',
      tokenName: 'x-auth',
      autoFetchUser: false
    },
  },
}</code></pre>

*Please note that the `auth` method works best when there is a `user` endpoint provided in the option above.*

Inside the `auth` config object, we have a `redirect` option in which we set our *login* route to `/login`, *logout* route to `/` and *home* route to `/my-reports` which would all behave as expected. We also have a `tokenType` property which represents the Authorization type in the header of our Axios request. It is set to `Bearer` by default and can be changed to work with your API.

For our API, there is no token type and this is why we’re going to leave it as an empty string. The `tokenName` represents the Authorization name (or the header property you want to attach your token to) inside your header in your Axios request.

By default, it is set to `Authorization` but for our API, the Authorization name is  `x-auth`. The `autoFetchUser` property is used to enable user fetch object using the `user` endpoint property after login. It is `true` by default but our API does not have a `user` endpoint so we have set that to `false`.

For this tutorial, we would be using the local strategy. In our strategies, we have the local option with endpoints for login, user and logout but in our case, we would only use the `*login*` option because our demo API does not have a `*logout*` endpoint and our user object is being returned when `*login*` is successful. 

**Note:** *The `auth` module does not have a register endpoint option so that means we’re going to register the traditional way and redirect the user to the login page where we will perform the authentication using `this.$auth.loginWith`. This is the method used in authenticating your users. It accepts a ‘strategy’ (e.g `local`) as a first argument and then an object to perform this authentication with. Take a look at the following example.*

<pre><code class="language-javascript">let data {
          email: 'test@test.com',
          password: '123456'
}
this.$auth.loginWith('local', { data })
</code></pre>

{{% ad-panel-leaderboard %}}

## Using The Auth Module

Now that we have configured our auth module, we can proceed to our registration page. If you visit the `/register` page, you should see a registration form. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a25907a-2bb7-4f40-abd4-9f93fa0a1beb/04-register-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a25907a-2bb7-4f40-abd4-9f93fa0a1beb/04-register-page.png" sizes="100vw" caption="Register page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a25907a-2bb7-4f40-abd4-9f93fa0a1beb/04-register-page.png'>Large preview</a>)" alt="Register form page" >}}

Let us make this form functional by adding the following code:

<pre><code class="language-javascript">methods: {
  async registerUser() {
    this.loading = true;
    let data = this.register;
    try {
      await this.$axios.post("/user/create", data);
      this.$router.push("/login");
      this.loading = false;
      this.$notify({
        group: "success",
        title: "Success!",
        text: "Account created successfully"
      });
    } catch (error) {
      this.loading = false;
      this.$notify({
        group: "error",
        title: "Error!",
        text: error.response
          ? error.response.data.error
          : "Sorry an error occured, check your internet"
      });
    }
  }
}</code></pre>

Here, we have an *async* function called `registerUser` which is tied to a click event in our template and makes an Axios request wrapped in a *try/catch block* to an endpoint `/user/create`. This redirects to the `/login` page and notifies the user of a successful registration. We also have a catch block that alerts the user of any error if the request is not successful. 

If the registration is successful, you would be redirected to the login page.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3705795a-6ccb-4493-916f-b93eeb161f80/05-login-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3705795a-6ccb-4493-916f-b93eeb161f80/05-login-page.png" sizes="100vw" caption="Login page with notification component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3705795a-6ccb-4493-916f-b93eeb161f80/05-login-page.png'>Large preview</a>)" alt="Login form page" >}}

Here, we’re going to make use of auth authentication method `this.$auth.loginWith('local', loginData)` after which we would use the `this.$auth.setUser(userObj)` to set the user in our `auth` instance.

To get the login page working, let’s add the following code to our `login.vue` file.

<pre><code class="language-javascript">methods: {
  async logIn() {
    let data = this.login;
    this.loading = true;
    try {
      let res = await this.$auth.loginWith("local", {
        data
      });
      this.loading = false;
      let user = res.data.data.user;
      this.$auth.setUser(user);
      this.$notify({
        group: "success",
        title: "Success!",
        text: "Welcome!"
      });
    } catch (error) {
      this.loading = false;
      this.$notify({
        group: "error",
        title: "Error!",
        text: error.response
          ? error.response.data.error
          : "Sorry an error occured, check your internet"
      });
    }
  }
}</code></pre>

We created an async function called `logIn` using the auth method `this.$auth.loginWith('local, loginData)`. If this login attempt is successful, we then assign the user data to our auth instance using `this.$auth.setUser(userInfo)` and redirect the user to the `/my-report` page. 

You can now get user data using `this.$auth.user` or with Vuex using `this.$store.state.auth.user` but that’s not all. The `auth` instance contains some other properties which you can see if you log in or check your state using your Vue dev tools.

If you log `this.$store.state.auth` to the console, you’ll see this:

<pre><code class="language-bash">{
  "auth": {
    "user": {
      "id": "d7a5efdf-0c29-48aa-9255-be818301d602",
      "email": "tmxo@test.com",
      "lastName": "Xo",
      "firstName": "Tm",
      "othernames": null,
      "isAdmin": false,
      "phoneNumber": null,
      "username": null
    },
    "loggedIn": true,
    "strategy": "local",
    "busy": false
  }
}</code></pre>

The `auth` instance contains a `loggedIn` property that is useful in switching between authenticated links in the nav/header section of your application. It also contains a strategy method that states the type of strategy the instance is running (e.g local).

Now, we will make use of this `loggedIn` property to arrange our `nav` links. Update your `navBar` component to the following:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;header class="header"&gt;
    &lt;div class="logo"&gt;
      &lt;nuxt-link to="/"&gt;
        &lt;Logo /&gt;
      &lt;/nuxt-link&gt;
    &lt;/div&gt;
    &lt;nav class="nav"&gt;
      &lt;div class="nav__user" v-if="auth.loggedIn"&gt;
        &lt;p&gt;{{ auth.user.email }}&lt;/p&gt;
        &lt;button class="nav__link nav__link--long"&gt;
          &lt;nuxt-link to="/report-incident"&gt;Report incident&lt;/nuxt-link&gt;
        &lt;/button&gt;
        &lt;button class="nav__link nav__link--long"&gt;
          &lt;nuxt-link to="/my-reports"&gt;My Reports&lt;/nuxt-link&gt;
        &lt;/button&gt;
        &lt;button class="nav__link" @click.prevent="logOut"&gt;Log out&lt;/button&gt;
      &lt;/div&gt;
      &lt;button class="nav__link" v-if="!auth.loggedIn"&gt;
        &lt;nuxt-link to="/login"&gt;Login&lt;/nuxt-link&gt;
      &lt;/button&gt;
      &lt;button class="nav__link" v-if="!auth.loggedIn"&gt;
        &lt;nuxt-link to="/register"&gt;Register&lt;/nuxt-link&gt;
      &lt;/button&gt;
    &lt;/nav&gt;
  &lt;/header&gt;
&lt;/template&gt;
&lt;script&gt;
import { mapState } from "vuex";
import Logo from "@/components/Logo";
export default {
  name: "nav-bar",
  data() {
    return {};
  },
  computed: {
    ...mapState(["auth"])
  },
  methods: {
    logOut() {
      this.$store.dispatch("logOut");
      this.$router.push("/login");
    }
  },
  components: {
    Logo
  }
};
&lt;/script&gt;
&lt;style&gt;&lt;/style></code></pre>
</div>

In our template section, we have several links to different parts of the application in which we are now using `auth.loggedIn` to display the appropriate links depending on the authentication status. We have a logout button that has a `click` event with a `logOut()` function attached to it. We also display the user’s email gotten from the auth property which is accessed from our Vuex store using the `mapState` method which maps our state auth to the computed property of the nav component. We also have a `logout` method that calls our Vuex action `logOut` and redirects the user to the `login` page. 

Now, let us go ahead and update our store to have a `logOut` action.

<pre><code class="language-javascript">export const actions = {
    // ....
  logOut() {
    this.$auth.logout();
  }
}</code></pre>

The `logOut` action calls the auth `logout` method which clears user data, deletes tokens from `localStorage` and sets `loggedIn` to `false`.

Routes like `/my-reports` and `report-incident` should not be visible to *guests* but at this point in our app, that is not the case. Nuxt does not have a [navigation guard](https://router.vuejs.org/guide/advanced/navigation-guards.html) that can protect your routes, but it has is the [auth middleware](https://auth.nuxtjs.org/guide/middleware.html). It gives you the freedom to create your own middleware so you can configure it to work the way you want.  

It can be set in two ways:

1. Per route.
2. Globally for the whole app in your `nuxt.config.js` file.

<pre><code class="language-javascript">router: {
  middleware: ['auth']
}</code></pre>

This `auth` middleware works with your `auth` instance so you do not need to create an `auth.js` file in your middleware folder.

Let us now add this middleware to our `my-reports.vue` and `report-incident.vue` files. Add the following lines of code to the script section of each file.

<pre><code class="language-javascript">middleware: 'auth'</code></pre>

Now, our application would check if the user trying to access these routes has an `auth.loggedIn` value of `true`. It’ll redirect them to the login page using our <a href="#redirect">redirect option</a> in our *auth* config file &mdash; if you’re not logged in and you try to visit either `/my-report` or `report-incident`, you would be redirected to `/login`.

If you go to `/report-incidents`, this is what you should see.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742bd579-15dd-4f0f-ab5c-06f42a933924/06-report-incident-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742bd579-15dd-4f0f-ab5c-06f42a933924/06-report-incident-page.png" sizes="100vw" caption="Report incident page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742bd579-15dd-4f0f-ab5c-06f42a933924/06-report-incident-page.png'>Large preview</a>)" alt="Form for reporting incidents" >}}

This page is for adding incidents but that right now the form does not send *incident* to our server because we are not making the call to the server when the user attempts to submit the form. To solve this, we will add a `reportIncident` method which will be called when the user clicks on **Report**. We’ll have this in the script section of the component. This method will send the form data to the server.
Update your  `report-incident.vue` file with the following:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;section class="report"&gt;
    &lt;h1 class="report__heading"&gt;Report an Incident&lt;/h1&gt;
    &lt;form class="report__form"&gt;
      &lt;div class="input__container"&gt;
        &lt;label for="title" class="input__label"&gt;Title&lt;/label&gt;
        &lt;input
          type="text"
          name="title"
          id="title"
          v-model="incident.title"
          class="input__field"
          required
        /&gt;
      &lt;/div&gt;
      &lt;div class="input__container"&gt;
        &lt;label for="location" class="input__label"&gt;Location&lt;/label&gt;
        &lt;input
          type="text"
          name="location"
          id="location"
          v-model="incident.location"
          required
          class="input__field"
        /&gt;
      &lt;/div&gt;
      &lt;div class="input__container"&gt;
        &lt;label for="comment" class="input__label"&gt;Comment&lt;/label&gt;
        &lt;textarea
          name="comment"
          id="comment"
          v-model="incident.comment"
          class="input__area"
          cols="30"
          rows="10"
          required
        &gt;&lt;/textarea&gt;
      &lt;/div&gt;
      &lt;input type="submit" value="Report" class="input__button" @click.prevent="reportIncident" /&gt;
      &lt;p class="loading__indicator" v-if="loading"&gt;Please wait....&lt;/p&gt;
    &lt;/form&gt;
  &lt;/section&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  name: "report-incident",
  middleware: "auth",
  data() {
    return {
      loading: false,
      incident: {
        type: "red-flag",
        title: "",
        location: "",
        comment: ""
      }
    };
  },
  methods: {
    async reportIncident() {
      let data = this.incident;
      let formData = new FormData();
      formData.append("title", data.title);
      formData.append("type", data.type);
      formData.append("location", data.location);
      formData.append("comment", data.comment);
      this.loading = true;
      try {
        let res = await this.$store.dispatch("reportIncident", formData);
        this.$notify({
          group: "success",
          title: "Success",
          text: "Incident reported successfully!"
        });
        this.loading = false;
        this.$router.push("/my-reports");
      } catch (error) {
        this.loading = false;
        this.$notify({
          group: "error",
          title: "Error!",
          text: error.response
            ? error.response.data.error
            : "Sorry an error occured, check your internet"
        });
      }
    }
  }
};
&lt;/script&gt;
&lt;style&gt;
&lt;/style&gt;</code></pre>
</div>

Here, we have a form with input fields for title, location, and comment with two-way data binding using `v-model`. We also have a `submit` button with a click event. In the script section, we have a `reportIncident` method that collects all the information provided in the form and is sent to our server using [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) because the API is designed to also accept images and videos.

This `formData` is attached to a Vuex action using the dispatch method, if the request is successful, you get redirected to `/my-reports` with a notification informing you that this request was successful otherwise, you would be notified of an error with the error message. 

At this point, we don’t have `reportIncident` action in our store yet so in your browser console, you would see an error if you try to click submit on this page.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f5d686f-0554-4ab4-aae5-0b3f154a0abb/07-action-error-message.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f5d686f-0554-4ab4-aae5-0b3f154a0abb/07-action-error-message.png" sizes="100vw" caption="Vuex error message. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f5d686f-0554-4ab4-aae5-0b3f154a0abb/07-action-error-message.png'>Large preview</a>)" alt="error message that reads ‘[Vuex] unknown action type: reportIncident'" >}}

To fix this, add the *reportIncident* action your `index.js` file.

<pre><code class="language-javascript">   
export const actions = {
  // ...
  async reportIncident({}, data) {
    let res = await this.$axios.post('/incident/create', data)
    return res;
  }
}</code></pre>

Here, we have a `reportIncident` function that takes in an empty context object and the data we’re sending from our form. This data is then attached to a `post` request that creates an incident and returns back to our `report-incident.vue` file.

At this point, you should be able to add a report using the form after which you would be redirected to `/my-reports` page. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/874438ff-c0d2-4a72-97fc-4682cf88104e/08-my-reports.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/874438ff-c0d2-4a72-97fc-4682cf88104e/08-my-reports.png" sizes="100vw" caption="My reports page empty. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/874438ff-c0d2-4a72-97fc-4682cf88104e/08-my-reports.png'>Large preview</a>)" alt="An empty my reports page" >}}

This page should display a list of incidents created by the user but right now it only shows what we see above, let’s go ahead to fix that. 

We’re going to be using the `fetch` method we learned about to get this list. Update your `my-reports.vue` file with the following:

<pre><code class="language-javascript">&lt;script&gt;
import incidentCard from "@/components/incidentCard.vue";
export default {
  middleware: "auth",
  name: "my-reports",
  data() {
    return {
      incidents: []
    };
  },
  components: {
    incidentCard
  },
  async fetch() {
    let { data } = await this.$axios.get("/user/incidents");
    this.incidents = data.data;
  }
};
&lt;/script&gt;</code></pre>

Here, we use `fetch` method to get user-specific incidents and assign the response to our incidents array.

If you refresh your page after adding an incident, you should see something like this.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e58ac7f3-674c-4cea-a6b7-a488a83829ea/09-my-reports-filled.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e58ac7f3-674c-4cea-a6b7-a488a83829ea/09-my-reports-filled.png" sizes="100vw" caption="My Reports page with a report. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e58ac7f3-674c-4cea-a6b7-a488a83829ea/09-my-reports-filled.png'>Large preview</a>)" alt="My reports page with one report" >}}

At this point, we would notice a difference in how `fetch` method and `asyncData` loads our data.

## Conclusion

So far, we have learned about the Axios module and all of its features. We have also learned more about asyncData, and how we can fetch both of them together despite their differences. We’ve also learned how to perform authentication in our application using the auth module and how to use the auth middleware to protect our routes. Here are some useful resources that talk more about all we’ve covered.

- Getting started with [meta tags](https://nuxtjs.org/api/pages-head/) in [Nuxjs](https://vue-meta.nuxtjs.org/).
- Using the [dotenv module](https://github.com/nuxt-community/dotenv-module) in [Nuxt](https://nuxtjs.org/api/configuration-env/).
- Using [Fetch in your Nuxt app](https://nuxtjs.org/blog/understanding-how-fetch-works-in-nuxt-2-12/).
- Getting started with [asyncData](https://nuxtjs.org/api/).

### Resources

1. “[Auth Module](https://auth.nuxtjs.org/),” NuxtJS.org
2. “[Axios Module: Introduction](https://axios.nuxtjs.org/),” NuxtJS.org
3. [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData), MDN web docs
4. “[API: The `asyncData` Method](https://nuxtjs.org/api/),” NuxtJS.org
5. “[The Vue Instance: Lifecycle Diagram](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram),” VueJS.org
6. “[Understanding How `fetch` Works In Nuxt 2.12](https://nuxtjs.org/blog/understanding-how-fetch-works-in-nuxt-2-12/),” NuxtJS.org

{{< signature "ks, ra, yk, il" >}}
