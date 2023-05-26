---
title: 'How To Build A Vue Survey App Using Firebase Authentication And Database'
slug: vue-survey-app-firebase-authentication-database
author: david-atanda
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fc5f678-e883-463c-a9fd-5c0bd1676db8/vue-survey-app-firebase-authentication-database.png
date: 2020-05-08T11:00:00.000Z
summary: >-
  This tutorial would take you on a step by step guide to build a functional survey app using Vue.js and Firebase. From validating the user’s data through Vuelidate, to authentication, storing the user’s data, route protection and sending data to Firebase servers. All the steps used in the tutorial are practical, and can be reproduced in any real-life project, even with a custom backend.
description: >-
  This tutorial would take you on a step by step guide to build a functional survey app using Vue.js and Firebase. From validating the user’s data through Vuelidate, to authentication, storing the user’s data, route protection and sending data to Firebase servers. All the steps used in the tutorial are practical, and can be reproduced in any real-life project, even with a custom backend.
categories:
  - JavaScript
  - Firebase
  - Authentication
  - Vue
---

In this tutorial, you’ll be building a Survey App, where we’ll learn to validate our users form data, implement Authentication in Vue, and be able to receive survey data using Vue and Firebase (a BaaS platform). 

As we build this app, we’ll be learning how to handle form validation for different kinds of data, including reaching out to the backend to check if an email is already taken, even before the user submits the form during sign up. 

Also, the app would handle logging in of the user with restful APIs. It’ll make use of Authguard in Vue router to prevent users that are not logged in from getting access to the survey form, and successfully send the survey data of logged-in users to a secure database.

Just so we’re on the same page, let’s clarify what Firebase is, and what it’ll be doing in this tutorial. Firebase is a toolset to “build, improve, and grow your app”, it gives you access to a large portion of the services that developers would normally have to build themselves, but don’t really want to build, because they’d rather be focusing on the app experience itself. This includes things like analytics, authentication, databases, file storage, and the list goes on.

This is different than traditional app development, which typically involves writing both frontend and backend software. The frontend code just invokes API endpoints exposed by the backend, and the backend code actually does the work. However, with Firebase products, the traditional backend is bypassed, putting the work into the client. This technically allows front-end engineers like myself to build full-stack applications writing just front end code. 

{{% feature-panel %}} 

The bottom line is that Firebase would act as our backend in this project by providing us with the necessary API endpoints to handle both our authentication and database needs. In the end, you’ll have built a functional survey app using Vue+ Firebase. After that, you can go ahead and build any web app of your choice using these same processes, even with a custom backend.

To follow along, you need to have Node and npm/yarn installed on your machine. If you do not have that done already, follow these quick guides to install [yarn](https://classic.yarnpkg.com/en) or [npm](https://riptutorial.com/node-js/example/29249/yarn-installation) on your machine. You also need to have a basic understanding of Vue, [Vuex](https://vuex.vuejs.org/installation.html) and [Vue router](https://router.vuejs.org/installation.html) syntax for this tutorial. 

The starter files for this tutorial are right [here](https://github.com/Atanda1/vue-survey-starterfile), which contains the base files for this project, and here is the [repo](https://github.com/Atanda1/vue-survey-sample) for the completed  [demo](https://vueauth.netlify.com). You can clone or download the repos and run `npm install` in your terminal.

After installing the starter file, you’ll see a welcome page, which has the options to sign up and sign in. After getting logged in you can then have access to the survey.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5c6b424-ae77-4ad0-a07f-f2cd3177fc62/app-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5c6b424-ae77-4ad0-a07f-f2cd3177fc62/app-architecture.png" sizes="100vw" caption="This describes how our survey app is going to be functioning. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5c6b424-ae77-4ad0-a07f-f2cd3177fc62/app-architecture.png'>Large preview</a>)" alt="Survey App architecture" >}}

Feel free to create a new project if you’ll like to build this project entirely on your own, just make sure to install [Vuex](https://vuex.vuejs.org/installation.html), [Vue router](https://router.vuejs.org/installation.html), [Vuelidate](https://www.npmjs.com/package/vuelidate) and [axios](https://www.npmjs.com/package/axios) into your Vue project. So let’s jump right in:

First, we’ll need a Firebase account to set up this project which is very much like creating a container for our app, giving us access to the database, various means of authentication, hosting, etc. It’s straight forward to set up once you’re on the Firebase site.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f865475f-26ac-4241-a848-d7806292fddc/firebase-home-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f865475f-26ac-4241-a848-d7806292fddc/firebase-home-page.png" sizes="100vw" caption="The landing page where you can sign up and start your Firebase journey. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f865475f-26ac-4241-a848-d7806292fddc/firebase-home-page.png'>Large preview</a>)" alt="Firebase landing page" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636b4877-d323-49c6-acda-b6ad50a29a36/firebase-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636b4877-d323-49c6-acda-b6ad50a29a36/firebase-project.png" sizes="100vw" caption="Creating Firebase projects (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636b4877-d323-49c6-acda-b6ad50a29a36/firebase-project.png'>Large preview</a>)" alt="Create new Firebase projects" >}}

Now that we have our project, the next thing is to set up both our authentication system and database (Realtime database) on Firebase. 

- Click on the "authentication" option;
- Set up the "sign-in method" we want (in this case email/password).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e923f7e-dfad-4093-9331-044804140079/email-and-password-auth.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e923f7e-dfad-4093-9331-044804140079/email-and-password-auth.png" sizes="100vw" caption="Setup email/password Auth method for the project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e923f7e-dfad-4093-9331-044804140079/email-and-password-auth.png'>Large preview</a>)" alt="Setup sign-in method" >}}

-  Click on "database".
- Choose "Realtime database" and copy this link that’s right on top.

It’ll be very useful as the API endpoint when we want to send the data to our firebase database. 

We’ll refer to this API as the database API. To use it, you’ll have to add the name of the database of your choice when sending it. For example, to send to a database called user. You simply add *user.json* at the end:

<pre><code class="language-json">{databaseAPI}/user.json</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3762e1f4-41ea-4d25-a094-0eb791d2c31d/firebase-databse.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3762e1f4-41ea-4d25-a094-0eb791d2c31d/firebase-databse.png" sizes="100vw" caption="Use the API above the database itself to send data to the database. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3762e1f4-41ea-4d25-a094-0eb791d2c31d/firebase-databse.png'>Large preview</a>)" alt="Real time database" >}}

After this, we’ll then go to [Firebase auth rest API](https://firebase.google.com/docs/reference/rest/auth#section-create-email-password) documentation to get our sign up and sign in API endpoints. Within these endpoints, there will be a need for our project’s API key, which can be found in our project settings. 
 
## Validation

Back to our code, there’ll be a validation of the signup data before been sent to the server, just to make sure the user is sending appropriate information. We’ll be using [Vuelidate](https://vuelidate.js.org/) which is a cool library that makes validation easier in Vue. First of all, install Vuelidate into the project:

<pre><code class="language-bash">npm i vuelidate</code></pre>

Go to `src/components/auth/signup.vue` and within the script tag import vuelidate and all the necessary events that we’ll need from the library as seen below.

**Note**: *You can check the docs for a full overview of the library and all [available events](https://vuelidate.js.org/#sub-basic-form).*

<div class="break-out">

<pre><code class="language-javascript">import { required, email, numeric, minValue, minLength, sameAs } from 'vuelidate/lib/validators'</code></pre>
</div>

A quick explanation:

<figure class="scroll-pane">
<table class="layout-fixed">
  <thead>
  <tr>
  <th>Value</th>
  </th>Description</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>required</code></td>
      <td>The value is compulsory</td>
    </tr>
    <tr>
      <td><code>email</code></td>
      <td>Value must be an email</td>
    </tr>
    <tr>
      <td><code>numeric</code></td>
      <td>Must be a number</td>
    </tr>
    <tr>
      <td><code>minValue</code></td>
      <td>Least numerical value the user can input.</td>
    </tr>
    <tr>
      <td><code>sameAs</code></td>
      <td>Used to compare between two values to make sure they’re the same</td>
    </tr>
  </tbody>
</table>
</div>

Also import [`axios`](https://github.com/axios/axios) to be able to send an HTTP request to the server:

<pre><code class="language-javascript">import axios from 'axios'</code></pre>

Before we go on, we’ll need to add some rules to the database to be able to validate the email as we should, just as seen below: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e152b0e2-863f-4b3c-b2f4-f50006c258a7/firebase-database-rules.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e152b0e2-863f-4b3c-b2f4-f50006c258a7/firebase-database-rules.png" sizes="100vw" caption="The database rules help decide you can or cannot access the database at any point in time. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e152b0e2-863f-4b3c-b2f4-f50006c258a7/firebase-database-rules.png'>Large preview</a>)" alt="Firebase rules" >}}

<pre><code class="language-javascript">"read" = "true"</code></pre>

Meaning that the database can be read without any hindrance from the client-side.

<pre><code class="language-javascript">"write" = "auth" !== null</code></pre>          

You can’t write on the database except you’re an authenticated user.

<pre><code class="language-javascript">"Users" = {
  "onIndex" : ["email"]
}</code></pre>

This allows us to query the `users` document with an index of `email`. That is, you can literally filter the database for a unique email.

Then add a custom computed property with the name `validations` just like we have methods, computed, etc.

Under `validations` we’ll have methods to validate the necessary data starting from `email` where it’s required and obviously must be an email. Also, we want to be able to tell a user when an email has already been taken by someone else, by checking the database after the user has typed it using something called async validators all within a custom validator and it’s all supported by [vuelidate.](https://vuelidate.js.org/#sub-asynchronous-validation)

<div class="break-out">

<pre><code class="language-javascript">
    validations : {
      email: {
        required,
        email,
        unique: val => {
          if (val === '') return true
          return axios.get('https://vue-journal.firebaseio.com/users.json?orderBy="email"&equalTo="' + val + '"')
            .then(res => {
              return Object.keys(res.data).length === 0
            })
        }
      }
    }</code></pre>
</div>

Then under unique, query the database using axios and use the default Object.keys to return the response only if it’s length is 0.

For the age, you’ll add required, numeric, and a min value of 18 that’s assigned to `minVal` as its properties.

<pre><code class="language-javascript">age: {
        required,
        numeric,
        minVal: minValue(18)
      }</code></pre>

Password’s properties are required, with a minimum length of 6 assigned to `minLen`.

<pre><code class="language-javascript">password: {
        required,
        minLen: minLength(6)
      }</code></pre>
  
`confirmPassword` properties are basically to be the same as the password.

<pre><code class="language-javascript">confirmPassword: {
        sameAs: sameAs(vm => {
          return vm.password
        })
      }</code></pre>

To tell the user that the email is taken, use `v-if` to check if `unique` is true or false. If true, then it means that the returned Object’s length is 0, and email can still be used as well as vice versa.

In the same manner, you can check if the user input is an actual email using `v-if`.

And for all the surrounding divs on the individual input, we will add a class of invalid that becomes active once there’s an error on that input.

To bind the validation events to each of the input in the HTML, we use [`$touch()`](https://vuelidate.js.org/#sub-without-v-model) as seen with the `email` below.

<div class="break-out">

<pre><code class="language-javascript">&lt;div class="input" :class="{invalid: $v.email.$error}"&gt;
  &lt;h6 v-if="!$v.email.email"&gt;Please provide a valid email address.&lt;/h6&gt;
  &lt;h6 v-if="!$v.email.unique"&gt;This email address has been taken.&lt;/h6&gt;
&lt;input
  type="email"
  placeholder="Email"
  id="email"
  @blur="$v.email.$touch()"
  v-model="email"&gt;
&lt;/div&gt;</code></pre>
</div>

`Age`, `password`, and `confirmPassword` will be binded to their HTML input in a similar manner as the `email`.

And we’ll make the ‘Submit’ button inactive if there’s an error in any of the input.

<pre><code class="language-javascript">&lt;button type="submit" :disabled="$v.$invalid"&gt;create&lt;/button&gt;</code></pre>
  
Here’s a complete [CodePen example](https://codepen.io/atanda1/pen/Yzyqrjv) for this vuelidate section.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dfeceab-a610-4ef1-b4c9-2e0d5ead8f65/vuelidate-implementation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dfeceab-a610-4ef1-b4c9-2e0d5ead8f65/vuelidate-implementation.png" sizes="100vw" caption="Vuelidate is used here to determine the kind of data been sent to the database. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dfeceab-a610-4ef1-b4c9-2e0d5ead8f65/vuelidate-implementation.png'>Large preview</a>)" alt="Vuelidate implementation" >}}

{{% ad-panel-leaderboard %}}

## Authentication

This app is an SPA and doesn’t reload like traditional sites, so we’ll be using Vuex, as our single "source of truth" to allow every component in our app to be aware of the general authentication status. We go to our store file, and create both sign-in/sign-up method within actions.

The response (`token` and `userId`) received when we send the users data, are going to be stored within our state. This is important because the token is going to be used to know if we’re still logged in or not at any point within our app.

The `token`, `userId`, and user are created in the state with an initial value of null. We’ll get to the user much later, but for now, we’ll focus on the first two.

<pre><code class="language-javascript">state: {
  idToken: null,
  userId: null,
  user: null
}</code></pre>

Mutations are then created to change the state when needed.

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>authUser</code></td>
      <td>Saves the token and <code>userId</code></td>
    </tr>
    <tr>
      <td><code>storeUser</code></td>
      <td>Stores the user info</td>
    </tr>
    <tr>
      <td><code>clearAuthData</code></td>
      <td>Erases the data back to the initial state</td>
    </tr>
  </tbody>
</table>

<pre><code class="language-javascript">mutations: {
  authUser (state, userData) {
    state.idToken = userData.token
    state.userId = userData.userId
  },
  storeUser (state, user) {
    state.user = user
  },
  clearAuthData (state) {
    state.idToken = null
    state.userId = null
    state.user = null
  }
}</code></pre>

For sign-up/sign-in, we’ll have to create individual actions for both, where we send our auth requests to the server. After which our response(token and userId) from sign-up/sign-in is committed to authUser, and saved on the local storage.

<div class="break-out">

<pre><code class="language-javascript">signup ({commit, dispatch}, authData) {
      axios.post('https://www.googleapis.com/identitytoolkit/v3/relyingparty/signupNewUser?key=AIzaSyCFr-OMMzDGp4Mmr0t66w2cTGfNazYjptQ', {
        email: authData.email,
        password: authData.password,
        returnSecureToken: true
      })
        .then(res => {
          console.log(res)
          commit('authUser', {
            token: res.data.idToken,
            userId: res.data.localId
          })
          localStorage.setItem('token', res.data.idToken)
          localStorage.setItem('userId', res.data.localId)
          localStorage.setItem('email', res.data.email)
          dispatch('storeUser', authData)
       
          setTimeout(function () {
            router.push('/dashboard')
          }, 3000)
        })
        .catch(error => console.log(error))
    }</code></pre>
</div>
 
<div class="break-out">

<pre><code class="language-javascript">login ({commit}, authData) {
      axios.post('https://www.googleapis.com/identitytoolkit/v3/relyingparty/verifyPassword?key=AIzaSyCFr-OMMzDGp4Mmr0t66w2cTGfNazYjptQ', {
        email: authData.email,
        password: authData.password,
        returnSecureToken: true
      })
        .then(res => {
          console.log(res)
          localStorage.setItem('token', res.data.idToken)
          localStorage.setItem('userId', res.data.localId)
          localStorage.setItem('email', res.data.email)
          commit('authUser', {
            token: res.data.idToken,
            userId: res.data.localId
          })
          router.push('/dashboard')
        })
        .catch(error => console.log(error.message))
    }</code></pre>
</div>

But here’s the tricky part, what we’ll do with the sign-up action particularly is to send only the email and password to be registered in the authentication database. In the real sense, we don’t have access to use the data in this authentication database, and we did not send any of our sign-up data besides email/password.

So what we’ll do is to create another action to send the complete sign-up data to another database. In this separate database document, we’ll have complete access to all the information we choose to save there. We’ll call this new action is called `storeUser`

We then go to our sign-up action and dispatch the entire object containing our sign-up data to a database we now have access to through `storeUser`. 

**Note:** You might not want to send your user’s password with `storeUser` to the database for security reasons.

<div class="break-out">

<pre><code class="language-javascript">storeUser ({ state}, userData) {
      if (!state.idToken) {
        return
      }
      axios.post('https://vue-journal.firebaseio.com/users.json' + '?auth=' + state.idToken, userData)
        .then(res => console.log(res))
        .catch(error => console.log(error))
    }
  }</code></pre>
</div>

`storeUser` adds a query using our newly gotten token and database API while posting to the database. 

This is because we cannot write to our database, except we’re authenticated with our proof( the token). That’s the rule we gave Firebase at the beginning, remember? 

<pre><code class="language-javascript">“write” = “auth” !== null</code></pre>

The complete code for sign-up/sign-in actions are right [here](https://codepen.io/atanda1/pen/mdePKqj).

Then dispatch both the sign-up and sign-in from their components within the `onSubmit` method to the respective actions in the store.

<pre><code class="language-javascript">methods : { 
  onSubmit () {
    const signupData = {
      email : this.email,
      name : this.name,
      age : this.age,
      password : this.password,
      confirmPassword : this.co
      nfirmPassword
    }
    this.$store.dispatch('signup', signupData)
    }
  }
}</code></pre>

**Note:** `signupData` contains the form’s data.

<div class="break-out">

<pre><code class="language-javascript">methods : {
  onSubmit = {
    const formData = {
      email : this.email,
      password : this.password
    }
    this.$store.dispatch('login', {email: formData.email, password: formData.password})
  }
}</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## AuthGuard

There’s a need for AuthGuard to prevent users that are not logged in from getting access to the dashboard where they’ll send the survey.

Go to the route file and import our store.

<pre><code class="language-javascript">import store from './store'</code></pre>

Within the route, go to the dashboard’s path and add the following:

<pre><code class="language-javascript">const routes = [
  { path: '/', component: WelcomePage },
  { path: '/signup', component: SignupPage },
  { path: '/signin', component: SigninPage },
  {
    path: '/dashboard',
    component: DashboardPage,
    beforeEnter (to, from, next) {
      if (store.state.idToken) {
        next()
      } else {
        next('/signin')
      }
    }
  }
]</code></pre>

All this does is to check whether there’s a token in the state, if yes, we give access to the dashboard and vice versa.

## LogOut

To create our logout option we’ll make use of `clearAuth` that we created earlier under `mutations` which just sets both the `token` and `userId` to `null`.

We now create a new `logout`  `action` , that commits to `clearAuth`, delete local storage and add `router.replace('/')` to redirect the user completely. 

<pre><code class="language-javascript">actions: {
  logout ({commit}) {
    commit('clearAuth')
    localStorage.removeItem('token')
    localStorage.removeItem('userId')
    router.replace('/')
  }
 }</code></pre>

In the header component, we have an `onLogout` method which dispatches our logout action in the store. 

<pre><code class="language-javascript">methods: {
      onLogout() {
        this.$store.dispatch('logout')
      }
    }</code></pre>

We then add a `@click` to the button which fires the `onLogout` method as we can see [here](https://codepen.io/atanda1/pen/jObqKNd).

<pre><code class="language-javascript">&lt;ul @click="onLogout"&gt;Log Out&lt;/ul&gt;</code></pre>

## UI_State

Now that we’ve given conditional access to the dashboard, the next step is to remove it from the nav bar, so only authenticated users can view it. To do that, we would add a new method under the `getters` called `ifAuthenticated` which checks if the token within our state is null. When there’s a token, it shows that that the user is authenticated and we want them to see the survey dashboard option on the nav bar.
 

<pre><code class="language-javascript">getters: {
  isAuthenticated (state) {
    return state.idToken !== null
  }
}</code></pre>

After which, you go back to the header component and create a method `auth` under computed, which dispatches to our `isAuthenticated` within the  `getters` we’ve just created in the store. What this does is that `isAuthenticated` would return false if there’s no token, which means `auth` would also be null and vice versa. 

<pre><code class="language-javascript">computed: {
      auth () {
        return this.$store.getters.ifAuthenticated
      }
    }</code></pre>

After this, we add a `v-if` to our HTML to check if `auth` is null or not, determining whether that option would show on the nav bar. 

<pre><code class="language-javascript">&lt;li v-if='auth'&gt;
          &lt;router-link to="/dashboard"&gt;Dashboard&lt;/router-link&gt;
        &lt;/li&gt;
        &lt;li  v-if='!auth'&gt;
          &lt;router-link to="/signup"&gt;Register&lt;/router-link&gt;
        &lt;/li&gt;
        &lt;li  v-if='!auth'&gt;
          &lt;router-link to="/signin"&gt;Log In&lt;/router-link&gt;
        &lt;/li&gt;</code></pre>

- You’ll find the complete code of the UI State section [here](https://codepen.io/atanda1/pen/QWjNxyo).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfbfe18-4998-4fc8-9355-46948c9eeb35/ui-state.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b513cd0-d56e-4ca3-81e5-66bbbba595ce/ui-state-opt.gif" width="800" height="410" alt="UI State" /></a><figcaption>There’s change in the header based on the authentication status of the user. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfbfe18-4998-4fc8-9355-46948c9eeb35/ui-state.gif">Large preview</a>)</figcaption></figure>

## AutoLogin

When we reload our app we lose the data and are signed out, having to start all over. This is because our token and Id are stored in Vuex, which is javascript, and this means that our app gets reloaded with the browser when refreshed. 

And so finally, what we’ll be doing is to retrieve the token within our local storage. By so doing, we can have the user’s token on the browser regardless of when we refresh the window, and have a method auto log-in our user in as much as the token is still valid.

A new `actions` method called `AutoLogin` is created, where we’ll get the token and `userId` from the local storage, and commit our data to the `authUser` method in the mutations.

<pre><code class="language-javascript">actions : {
  AutoLogin ({commit}) {
      const token = localStorage.getItem('token')
      if (!token) {
        return
      }
      const userId = localStorage.getItem('userId')
      const token = localStorage.getItem('token')
      commit('authUser', {
        idToken: token,
        userId: userId
      })
  }
}</code></pre>

We then go to our App.vue and write a `created` method, that’ll dispatch the  `autoLogin` from our store every time the app is loaded. 

<pre><code class="language-javascript">created () {
    this.$store.dispatch('AutoLogin')
  }</code></pre>

## Fetch_User_Data

We want to welcome the user on the dashboard by displaying the user’s name. And so, another action called `fetchUser` is created which first checks if there’s a token as usual. Then, it goes on to get the email from local storage and queries the database as done earlier with the email validation. 

This returns an object containing the user’s data initially submitted during sign-up. We then convert this object into an array and commit it to the `storeUser` mutation initially created.

<div class="break-out">

<pre><code class="language-javascript">fetchUser ({ commit, state}) {
  if (!state.idToken) {
    return
  }
  const email = localStorage.getItem('email')
  axios.get('https://vue-journal.firebaseio.com/users.json?orderBy="email"&equalTo="' + email + '"')
    .then(res => {
      console.log(res)
    
     // const users = [] 
      console.log(res.data)
      const data = res.data
      const users = []
      for (let key in data) {
        const user = data[key]
        user.id = key
        users.push(user)
        console.log(users)
      }
     commit('storeUser', users[0])
    })
    .catch(error => console.log(error))
}</code></pre>
</div>
       
After which we create another getter called `user` which returns the `state.user` already committed through `storeUser`.

<pre><code class="language-javascript">getters: {
  user (state) {
    return state.user
  },
  isAuthenticated (state) {
    return state.idToken !== null
  }
}</code></pre>

Back to the dashboard, we create a new computed method called `name` that returns `state.user.name` only if the user exists.

<div class="break-out">

<pre><code class="language-javascript">computed: {
  name () {
      return !this.$store.getters.user ? false : this.$store.getters.user.name
    }
  },
  created () {
    this.$store.dispatch('fetchUser')
  }
}</code></pre>
</div>

And we’ll also add the `created` computed property to dispatch the `fetchUser` action once the page is loaded. We then use the `v-if`  in our HTML in order to display the name if the name exists.

<pre><code class="language-javascript"> &lt;p v-if="name"&gt;Welcome, {{ name }} &lt;/p&gt;</code></pre>
 
## Send_Survey

To send the survey, we’ll create a `postData` action that sends the data to the database using the database API, with the token to show the server that the user is logged in. 

<div class="break-out">

<pre><code class="language-javascript">postData ({state}, surveyData) {
  if (!state.idToken) {
    return
  }
  axios.post('https://vue-journal.firebaseio.com/survey.json' + '?auth=' + state.idToken , surveyData)
    .then(res => {
     console.log(res)
    })
    .catch(error => console.log(error))
}</code></pre>
</div>
     
We come back to the dashboard component and dispatch the data to our `postData` action in the store.

<pre><code class="language-javascript">methods : {
  onSubmit () {
    const postData = {
      price: this.price,
      long: this.long,
      comment: this.comment
    }
    console.log(postData)
    this.$store.dispatch('postData', postData)
  }
}</code></pre>
       
There we have it, we’ve got a lot of useful features implemented into our demo application while communicating with our Firebase server. Hopefully, you’ll be using these powerful features in your next project as they’re very critical to building modern web apps today.

If you have any questions, you can leave them in the comments section and I’ll be happy to answer every single one of them!

- The demo for the tutorial is live [here](https://vueauth.netlify.com).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26f66764-1e87-4203-8ba0-30b5febe3cf6/final-survey-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26f66764-1e87-4203-8ba0-30b5febe3cf6/final-survey-app.png" sizes="100vw" caption="The completed survey app (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26f66764-1e87-4203-8ba0-30b5febe3cf6/final-survey-app.png'>Large preview</a>)" alt="Vue survey app" >}}

Other resources that may prove useful includes:

- To understand more about Firebase and the other services it offers, check out Chris Esplin’s article, “[What Is Firebase?](https://howtofirebase.com/what-is-firebase-fcb8614ba442)”
- Vuelidate is a really nice library you should really dig into. You should read through its documentation to gain full insight.https://vuelidate.js.org/.
- You can also explore [axios](https://www.sitepoint.com/axios-beginner-guide/) on its own, especially if you want to use it in bigger projects.

{{< signature "ra, yk, il" >}}
