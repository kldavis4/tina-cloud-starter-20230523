---
title: 'Useful Tools In Vue.js Web Development'
slug: useful-tools-vue-javascript-web-development
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a610e66-57fa-424d-8b5d-6cde226f5d18/useful-tools-vue-javascript-web-development.png
date: 2020-10-05T10:30:00.000Z
summary: >-
  There are some tools that developers that are just getting started with Vue or sometimes, have experience building with Vue sometimes do not know exist to make development in Vue a lot easier. In this article, we’re going to look at a few of these libraries, what they do, and how to use them during development.
description: >-
  There are some tools that developers that are just getting started with Vue or sometimes, have experience building with Vue sometimes do not know exist to make development in Vue a lot easier. In this article, we’re going to look at a few of these libraries, what they do, and how to use them during development.
categories:
  - Vue
  - Tools
  - JavaScript
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

When working on a new project, there are certain features that are necessary depending on how the application is supposed to be used. For example, if you’ll be storing user-specific data, you’ll need to handle authentications, this will require the setting up of a form that needs to be validated. Things such as authentication and form validations are common; there are solutions that possibly fit your use case.

To properly utilize your development time, it is better you use what is available, instead of inventing yours.

As a new developer, there’s the possibility that you won’t be aware of all that the Vue ecosystem provides you. This article will help with that; it will cover certain useful tools that will aid you in building better Vue applications. 

**Note**: *There are alternatives to these libraries and this article is in no way placing these few over the others. They are just the ones I’ve worked with.*

This tutorial is aimed at beginners that either just started learning about Vue or already have basic knowledge of Vue. All code snippets used in this tutorial can be found on [my GitHub](https://github.com/Timibadass/plugins-demo).

## Vue-notification

During user interaction, there is often a need to display a success message, error message, or random info to the user. In this section, we’re going to look at how to display messages and warnings to your user using `vue-notification`. This package provides an interface with a nice animation/transition for displaying errors, general information, and success messages to your user across your application and it does not require a lot of configuration to get up and running.

### Installation

You can install `vue-notification` in your project using either Yarn or NPM depending on the package manager for your project

#### Yarn

<pre><code class="language-bash">yarn add vue-notification
</code></pre>

#### npm

<pre><code class="language-bash">npm install --save vue-notification
</code></pre>

After the installation is complete, the next thing would be to add it to the entry point in your app, the ***main.js*** file.

#### main.js

<pre><code class="language-javascript">//several lines of existing code in the file
    import Notifications from 'vue-notification'
    Vue.use(Notifications)
  </code></pre>

At this point, we only need to add the notifications component in the ***App.vue*** file before we can display notifications in our app. The reason why we’re adding this component to the ***App.vue*** file is to avoid repetition in our application because no matter the page the user is on in our app, components in ***App.vue*** (e.g the header & footer components) would always be available. This takes the pain of having to register the notification component in every file that we need to display a notification to the user.

#### App.vue

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;div id="nav"&gt;
      &lt;router-link to="/"&gt;Home&lt;/router-link&gt; |
      &lt;router-link to="/about"&gt;Notifications&lt;/router-link&gt;
    &lt;/div&gt;
    &lt;notifications group="demo"/&gt;
    &lt;router-view /&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>

Here, we add one instance of this component which accepts a `group` prop which would be used in grouping the different types of notifications we have. This is because the notifications component accepts a number of props that dictate how the component behaves and we’re going to look at a few of these.

1. `group`  
This prop is used to specify the different types of notifications you might have in your app. For instance, you might decide to use different styles and behavior depending on what purpose the notification is supposed to serve, form validation, API response, etc.
2. `type`  
This prop accepts a value that serves as a ‘class name’ for each notification type we have in our application and examples can include `success`, `error`, and `warn`. If we use any one of these as a notification type, we can easily style the component by using this class format `vue-notification + '.' + type`, i.e `.vue-notification.warn` for `warn`, and so on.
3. `duration`  
This prop specifies how long the `notification` component should appear before disappearing. It accepts a number as a value in `ms` and also accepts a negative number (-1) if you want it to remain on your user’s screen till they click on it.
4. `position`  
This prop is used in setting the position you want notifications to appear from in your app. Some of the available options are `top left`, `top right`, `top center`, `bottom right`, `bottom left`, and `bottom center`.

We can add these props to our component in ***App.vue*** so it now looks like this;

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;div id="nav"&gt;
      &lt;router-link to="/"&gt;Home&lt;/router-link&gt; |
      &lt;router-link to="/about"&gt;Notifications&lt;/router-link&gt;
    &lt;/div&gt;
    &lt;notifications
      :group="group"
      :type="type"
      :duration="duration"
      :position="position"
    /&gt;
    &lt;router-view /&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    data() {
      return {
        duration: -1,
        group: "demo",
        position: "top center",
        type: "info",
      };
    },
  };
&lt;/script&gt;
&lt;style&gt;
  .vue-notification.info {
    border-left: 0;
    background-color: orange;
  }
  .vue-notification.success {
    border-left: 0;
    background-color: limegreen;
  }
  .vue-notification.error {
    border-left: 0;
    background-color: red;
  }
&lt;/style&gt;
</code></pre>

We also add styling for the different notification types that we would be using in our application. Note that other than `group`, we can pass each of the remaining props on the fly whenever we want to display a notification and it would still work accordingly. To display a notification in any of your Vue files, you can do the following.

#### vueFile.vue

<pre><code class="language-javascript">this.$notify({
  group: "demo",
  type: "error",
  text: "This is an error notification",
});
</code></pre>

Here, we create a notification of `type` `error` under the `group` notification of `demo`. The property `text` accepts the message you want the notification to contain and in this case, the message is ‘*This is an error notification’.* This is what the notification would look like in your app.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49084b57-3b8b-4d8b-b210-0275a76114fb/01-notifications-in-action.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49084b57-3b8b-4d8b-b210-0275a76114fb/01-notifications-in-action.png" sizes="100vw" caption="<code>vue-notification</code> in action: error notification displaying in the browser. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49084b57-3b8b-4d8b-b210-0275a76114fb/01-notifications-in-action.png'>Large preview</a>)" alt="vue-notification with type ‘error’ in action" >}}

You can find out the other available props and other ways to configure the notification on the [official docs page](https://github.com/euvl/vue-notification#props).



## Vuelidate

One of the most common elements used on the web are form elements (`input[type='text']`, `input[type='email']`, `input[type='password']`, and so on) and there is always a need to validate user input to make sure they’re sending the right data and/or using the right format in the input field. With [Vuelidate](https://vuelidate.js.org/), you can add validation to the forms in your Vue.js application, saving time and benefitting from the time put into this package. I had been hearing about [Vuelidate](https://vuelidate.js.org/) for a while but I was a little reluctant to take a look at it because I thought it would be too complex which meant I was writing validations from scratch for most of the form fields in the apps I worked on.

When I eventually looked at the docs, I found out it was not difficult to get started with and I could validate my form fields in no time and move on to the next thing.

### Installation

You can install Vuelidate using any of the following package managers.

#### Yarn

<pre><code class="language-bash">yarn add vuelidate
</code></pre>

#### npm

<pre><code class="language-bash">npm install vuelidate --save
</code></pre>

After installation, the next thing would be to add it to your app’s config in the ***main.js*** file so you can use it in your vue files.

<pre><code class="language-javascript">import Vuelidate from 'vuelidate'
Vue.use(Vuelidate)
</code></pre>

Assuming you have a form that looks like this in your app;

#### vuelidate.vue

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;form @submit.prevent="login" class="form"&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="fullName" class="input__label"&gt;Full Name&lt;/label&gt;
      &lt;input
        type="text"
        name="fullName"
        id="fullName"
        v-model="form.fullName"
        class="input__field"
      /&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="email" class="input__label"&gt;Email&lt;/label&gt;
      &lt;input
        type="email"
        name="email"
        id="email"
        v-model="form.email"
        class="input__field"
      /&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="email" class="input__label"&gt;Age&lt;/label&gt;
      &lt;input
        type="number"
        name="age"
        id="age"
        v-model="form.age"
        class="input__field"
      /&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="password" class="input__label"&gt;Password&lt;/label&gt;
      &lt;input
        type="password"
        name="password"
        id="password"
        v-model="form.password"
        class="input__field"
      /&gt;
    &lt;/div&gt;
    &lt;input type="submit" value="LOGIN" class="input__button" /&gt;
    &lt;p class="confirmation__text" v-if="submitted"&gt;Form clicked&lt;/p&gt;
  &lt;/form&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    data() {
      return {
        submitted: false,
        form: {
          email: null,
          fullName: null,
          age: null,
          password: null,
        },
      };
    },
    methods: {
      login() {
        this.submitted = true;
      },
    },
  };
&lt;/script&gt;
</code></pre>
</div>

Now to validate this type of form, you first need to decide on what type of validation you need for each form field. For instance, you can decide you need the minimum length of the `fullName` to be `10` and the minimum age to be `18`.

Vuelidate comes with built-in validators that we only need to import it to use. We can also choose to validate the password field based on a particular format, e.g `Password should contain at least a lower case letter, an upper case letter, and a special character`. We can write our own little validator that does this and plug it into the list of Vuelidate’s plugin.

Let’s take it step by step.

#### Using Built-In Validators

<pre><code class="language-javascript">&lt;script&gt;
  import {
    required,
    minLength,
    minValue,
    email,
  } from "vuelidate/lib/validators";
  export default {
    validations: {
      form: {
        email: {
          email,
          required,
        },
        fullName: {
          minLength: minLength(10),
          required,
        },
        age: {
          required,
          minValue: minValue(18),
        },
      },
    },
  };
&lt;/script&gt;
</code></pre>

Here, we import some validators that we need to properly validate our form. We also add a `validations` property where we define the validation rules for each form field that we want to validate.

At this point, if you inspect the devTools for your app, you should see something that looks like this;

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3c4c78c-5982-4dd9-9426-4eca5634bcf9/02-vuelidate-computed-property.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3c4c78c-5982-4dd9-9426-4eca5634bcf9/02-vuelidate-computed-property.png" sizes="100vw" caption="<code>vuelidate</code> computed property (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3c4c78c-5982-4dd9-9426-4eca5634bcf9/02-vuelidate-computed-property.png'>Large preview</a>)" alt="vuelidate computed property" >}}

The `$v` computed property contains a number of methods that are useful in confirming the validity of our form but we’re only going to focus on a few of them:

1. `$invalid`  
To check if the form passes all validation.
2. `email`  
To check that the value is a valid email address.
3. `minValue`  
To check that the value of `age` passes the `minValue` check.
4. `minLength`  
To verify the length of `fullName`.
5. `required`  
To ensure all required fields are provided.

If you enter a value for `age` less than the minimum age set in the validation and check `$v.form.age.minValue`, it would be set to `false` and this means the value in the input field doesn’t pass the `minValue` validation check.

#### Using Custom Validators

We also need to validate our password field and ensure it contains the required format but Vuelidate does not have a built-in validator that we can use to achieve this. We can write our own custom validator that does this using [RegEx](https://developer.mozilla.org/en/docs/Web/JavaScript/Guide/Regular_Expressions). This custom validator would look like this;

<div class="break-out">

 <pre><code class="language-javascript">&lt;script&gt;
  import {
    required,
    minLength,
    minValue,
    email,
  } from "vuelidate/lib/validators";
  export default {
    validations: {
      form: {
//existing validator rules
        password: {
          required,
          validPassword(password) {
            let regExp = /^(?=.*[0-9])(?=.*[!@#$%^&*])(?=.*[A-Z]+)[a-zA-Z0-9!@#$%^&*]{6,}$/;
            return regExp.test(password);
          },
        },
      },
    },
  };
&lt;/script&gt;
</code></pre>
</div>

Here, we create a custom validator that uses a Regex to check that the password contains the following;

1. At least one uppercase letter;
2. At least one lowercase letter;
3. At least one special character;
4. At least one number;
5. Must have a minimum length of 6.

If you try to enter any password that doesn’t meet any of the requirements listed above, the `validPassword` would be set to `false`.

Now that we’re sure our validations are working, we have to display the appropriate error messages so the user knows why they can’t proceed. This would look like this:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;form @submit.prevent="login" class="form"&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="fullName" class="input__label"&gt;Full Name&lt;/label&gt;
      &lt;input
        type="text"
        name="fullName"
        id="fullName"
        v-model="form.fullName"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="!$v.form.fullName.required"&gt;
        This field is required
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="email" class="input__label"&gt;Email&lt;/label&gt;
      &lt;input
        type="email"
        name="email"
        id="email"
        v-model="form.email"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="!$v.form.email.required"&gt;
        This field is required
      &lt;/p&gt;
      &lt;p class="error__text" v-if="!$v.form.email.email"&gt;
        This email is invalid
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="email" class="input__label"&gt;Age&lt;/label&gt;
      &lt;input
        type="number"
        name="age"
        id="age"
        v-model="form.age"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="!$v.form.age.required"&gt;
        This field is required
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="password" class="input__label"&gt;Password&lt;/label&gt;
      &lt;input
        type="password"
        name="password"
        id="password"
        v-model="form.password"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="!$v.form.password.required"&gt;
        This field is required
      &lt;/p&gt;
      &lt;p class="error__text" v-else-if="!$v.form.password.validPassword"&gt;
        Password should contain at least a lower case letter, an upper case
        letter, a number and a special character
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;input type="submit" value="LOGIN" class="input__button" /&gt;
  &lt;/form&gt;
&lt;/template&gt;
</code></pre>
</div>

Here, we add a paragraph that displays either a text telling the user that a field is required, an inputted value for email is not valid or that the password doesn’t contain the required characters. If we look at this in your browser, you would see the errors already appearing under each input field.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21382733-5852-4c49-b782-0fb7468a0c69/03-form-error-texts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21382733-5852-4c49-b782-0fb7468a0c69/03-form-error-texts.png" sizes="100vw" caption="Error texts for each input field (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21382733-5852-4c49-b782-0fb7468a0c69/03-form-error-texts.png'>Large preview</a>)" alt="error texts in the form" >}}

This is bad for user experience as the user is yet to interact with the form and as such the error texts should not be visible at least, till the user tries to submit the form. To fix this, we would add `submitted` to the condition required for the error texts to show and also switch the value of `submitted` to `true` when the user clicks on the submit button.

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;form @submit.prevent="login" class="form"&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="fullName" class="input__label"&gt;Full Name&lt;/label&gt;
      &lt;input
        type="text"
        name="fullName"
        id="fullName"
        v-model="form.fullName"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="submitted && !$v.form.fullName.required"&gt;
        This field is required
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="email" class="input__label"&gt;Email&lt;/label&gt;
      &lt;input
        type="email"
        name="email"
        id="email"
        v-model="form.email"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="submitted && !$v.form.email.required"&gt;
        This field is required
      &lt;/p&gt;
      &lt;p class="error__text" v-if="submitted && !$v.form.email.email"&gt;
        This email is invalid
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="email" class="input__label"&gt;Age&lt;/label&gt;
      &lt;input
        type="number"
        name="age"
        id="age"
        v-model="form.age"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="submitted && !$v.form.age.required"&gt;
        This field is required
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="input__container"&gt;
      &lt;label for="password" class="input__label"&gt;Password&lt;/label&gt;
      &lt;input
        type="password"
        name="password"
        id="password"
        v-model="form.password"
        class="input__field"
      /&gt;
      &lt;p class="error__text" v-if="submitted && !$v.form.password.required"&gt;
        This field is required
      &lt;/p&gt;
      &lt;p
        class="error__text"
        v-else-if="submitted && !$v.form.password.validPassword"
      &gt;
        Password should contain at least a lower case letter, an upper case
        letter, a number and a special character
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;input type="submit" value="LOGIN" class="input__button" /&gt;
  &lt;/form&gt;
&lt;/template&gt;
</code></pre>
</div>

Now the error texts do not appear until the user clicks on the submit button and this is much better for the user. Each validation error would appear if the value inputted in the form does not satisfy the validation.

Finally, we would only want to process the user’s input when all validations on our form have passed and one way we can do this would be to use the `$invalid` property on the `form` which is present in the `$v` computed property. Let us take a look at how to do that:

<pre><code class="language-javascript">methods: {
      login() {
        this.submitted = true;
        let invalidForm = this.$v.form.$invalid;
        //check that every field in this form has been entered correctly.
        if (!invalidForm) {
          // process the form data
        }
      },
    },
</code></pre>

Here, we’re checking to ensure that the form has been completely filled and filled correctly. If it returns `false`, that means the form is valid and we can process the data from the form but if it is `true` , it means that the form is still invalid and the user still needs to tend to some errors in the form. We can also use this property to disable or style the submit button depending on your preference.

## Vuex-persistedstate

During development, there are instances where you would store data like a user’s info and token in your Vuex store. But your Vuex store data would not persist if your users try to refresh your app from the browser or enter a new route from the URL tab of your browser and the current state of your application gets lost with it. This causes the user to be redirected to the login page if the route is being protected with [navigation guard](https://www.smashingmagazine.com/2020/08/vue-router-features/) which is abnormal behavior for your app to have. This can be fixed with `vuex-persistedstate`, let look at how.

### Installation

You can install this plugin using any one of the two methods:

#### Yarn

<pre><code class="language-bash">yarn add vuex-persistedstate
</code></pre>

#### npm

<pre><code class="language-bash">npm install --save vuex-persistedstate
</code></pre>

After the installation process is complete, the next step would be to configure this plugin to be ready for use in your Vuex store.

<pre><code class="language-javascript">import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from "vuex-persistedstate";
Vue.use(Vuex)
export default new Vuex.Store({
    state: {},
    mutations: {},
    actions: {},
    modules: {},
    plugins: [createPersistedState()]
})
</code></pre>

At this point, all of our Vuex Store would be stored in localStorage (by default) but `vuex-persistedstate` comes with the option to use `sessionStorage` or `cookies`.

<pre><code class="language-javascript">import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from "vuex-persistedstate";
Vue.use(Vuex)
export default new Vuex.Store({
    state: {},
    mutations: {},
    actions: {},
    modules: {},
  // changes storage to sessionStorage
    plugins: [createPersistedState({ storage: window.sessionStorage });
]
})
</code></pre>

To confirm that our Store would persist after refreshing or closing the browser tab, let us update our store to look like this:

<pre><code class="language-javascript">import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from "vuex-persistedstate";
Vue.use(Vuex)
export default new Vuex.Store({
    state: {
        user: null
    },
    mutations: {
        SET_USER(state, user) {
            state.user = user
        }
    },
    actions: {
        getUser({ commit }, userInfo) {
            commit('SET_USER', userInfo)
        }
    },
    plugins: [createPersistedState()]
})
</code></pre>

Here, we add a `user` state that would store user data from the form created in the previous section. We also add a `SET_USER` mutation that would be used in modifying the `user` state. Finally, we add a `getUser` action that would receive the user object and pass it to the `SET_USER` mutation property. The next would be to dispatch this action after validating our form successfully. This looks like this:

<pre><code class="language-javascript">methods: {
    login() {
      this.submitted = true;
      let invalidForm = this.$v.form.$invalid;
      let form = this.form;
      //check that every field in this form has been entered correctly.
      if (!invalidForm) {
        // process the form data
        this.$store.dispatch("getUser", form);
      }
    },
  },
</code></pre>

Now, if you correctly fill the form, submit it, and open the `localStorage`  section in the ***applications*** tab in the devTools of your browser, you should see a `vuex` property that looks like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/419daa58-a9fb-455e-a51f-fa9974ecf1de/04-vuex-persistedstate-in-localstorage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/419daa58-a9fb-455e-a51f-fa9974ecf1de/04-vuex-persistedstate-in-localstorage.png" sizes="100vw" caption="Vuex store in localStorage (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/419daa58-a9fb-455e-a51f-fa9974ecf1de/04-vuex-persistedstate-in-localstorage.png'>Large preview</a>)" alt="vuex-persistedstate in localStorage" >}}

At this point, if you refresh your browser or open your app in a new tab, your `user` state would still persist across these tabs/session (on localStorage).

## Conclusion

There are a lot of libraries that can be very useful in Vuejs web development and sometimes it can be hard to choose the one to use or where to find them. The following links contain libraries that you can use in your Vue.js application.

1. [vuejsexamples.com](https://vuejsexamples.com/).
2. [madewithvuejs.com](https://madewithvuejs.com/).

There is often more than one library that does the same thing that you’re trying to achieve in your application when searching for a ‘library’, the important thing is to make sure the option you settle for works for you and is being maintained by its creator(s) so it doesn’t cause your application to ***break***.

### Further Resources

- “[Vue.js Notifications](https://github.com/euvl/vue-notification),” Official docs, GitHub
- “[Vuelidate](https://vuelidate.js.org/),” Official website
- “[Form Validation In Under An Hour With Vuelidate ](https://css-tricks.com/form-validation-in-under-an-hour-with-vuelidate/),” Sarah Drasner, CSS-Tricks
- “[`vuex-persistedstate`](https://yarnpkg.com/package/vuex-persistedstate),” Yarn

{{< signature "ks, ra, il" >}}
