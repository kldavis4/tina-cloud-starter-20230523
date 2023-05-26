---
title: 'Internationalization In Vue With The Vue I18n Plugin'
slug: internationalization-vue-i18n
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc2aaf03-1dea-4d35-97e3-010c01b26fd6/internationalization-vue-i18n.png
date: 2020-06-12T10:00:00.000Z
summary: >-
  Adding Internationalization to your Vue.js application has a lot of use cases and in this tutorial, we’re going to learn how to do this with the Vue I18n plugin and how to set it up in our application.
description: >-
  Adding Internationalization to your Vue.js application has a lot of use cases and in this tutorial, we’re going to learn how to do this with the Vue I18n plugin and how to set it up in our application.
categories:
  - JavaScript
  - Plugins
  - Apps
  - Internationalization
  - Vue
---

Building applications for people from different parts of the world comes with challenges like support for multiple locales and how to integrate it into your application. I remember the first time I faced this challenge, I had to build an application that was going to have multiple languages (English, Yoruba, and French). This was the first time I ever wondered how applications that supported multiple languages were built and also how I discovered “Internationalization”. 
 
In this tutorial, we’re going to learn about Internationalization and how to implement it in our Vue application using the Vue I18n plugin by building a simple app that uses this plugin. This plugin helps you configure your application to work with multiple locales and allows your user to choose between all the available locales without you having to do too much. 
  
I have put together a simple application for the purpose of this tutorial and it can be found on [Github](https://github.com/Timibadass/vue-i18n-app).
 
*This article requires basic knowledge of the Vue.js framework. For those looking to get started with Vuejs, I recommend you start from their* [*official documentation*](https://vuejs.org/)*.*

<div class="c-felix-the-cat">
<h4 class="h3">React Internationalization</h4>
<p>How can we build an internationalized React front-end application? Yury Dymov explains how you can detect the user’s locale, save it in the cookie, let the user change their locale, translate the user interface, and render currencies in their appropriate formats. <a href="https://www.smashingmagazine.com/2017/01/internationalizing-react-apps/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## What Are i18n And Vue-i18n?

### Internationalization (i18n)

Internationalization (sometimes shortened to "I18N, meaning "I &mdash; eighteen letters &mdash; N") is the process of planning and implementing products and services so that they can easily be adapted to specific local languages and cultures, a process called [localization](https://searchcio.techtarget.com/definition/localization). Imagine you’re building a product for people in the USA and France, without internationalization, this would mean building two separate applications in different locales to run on different domains (English version on amazingproduct.us and French version on amazingproduct.fr).

This is where Internationalization comes in. It helps people from both countries easily use the application in the locale of their choice (English or French). Internationalizing your application comes with benefits such as:

1. Single source code for all languages of the product.
2. Greater in-country customer acceptance and satisfaction.
3. It makes the maintenance of the product easier and simpler.
4. Reduced time, cost, and effort for localization (L10n).

### Internationalization in Vue

Internationalization can be implemented in Vue using the *Vue I18n* plugin. It easily integrates some localization features to your Vue.js application. It can be added to your application in one of the following ways:

- By direct download/CDN &mdash; using this [CDN link](https://unpkg.com/vue-i18n/dist/vue-i18n) for the latest release on NPM.

After which it would be included in head section of your html file.

<pre><code class="language-html">&lt;script src="https://unpkg.com/vue-i18n/dist/vue-i18n.js"&gt;&lt;/script&gt;</code></pre>

- By installing from NPM or Yarn.
    

<pre><code class="language-bash">npm install vue-i18n
// or
yarn add vue-i18n</code></pre>   

- By adding it using the Vue Cli 3.x (You need Vue cli 3.x).
    

<pre><code class="language-bash">vue add i18n</code></pre>   

## Setting Up Vue-i18n In Your App

To set this plugin up in your application, we’re going to use the Vue CLI method. That can be done using this command:

<pre><code class="language-bash">vue add i18n</code></pre>   

On running this command, you would be prompted to select config options to choose from. For this tutorial, I’ve gone ahead to select all the default options for setting up this plugin. This looks like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e5e4f1c-0886-4d91-9c43-02b6b017c8c8/01-config.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e5e4f1c-0886-4d91-9c43-02b6b017c8c8/01-config.png" sizes="100vw" caption="Config options for Vue I18n plugin. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e5e4f1c-0886-4d91-9c43-02b6b017c8c8/01-config.png'>Large preview</a>)" alt="config options for Vue I18n plugin." >}}

Let’s take a look at what they do:

1. The first option is to set the default locale the application would be in and in this case, I have gone ahead to set it to English.
2. The second option is to set a fallback locale for the application and fallback is going to serve as a backup locale for your application if you fail to provide a translation in another locale and I selected English. This would be talked about later on in this article.
3. The third option is for choosing a directory for storing all the **locale** json files to be used for localization in the app and I selected the default option which is **locales.**
4. The last option is for enabling component-based localization in Single File Components. This means deciding whether or not you want to enable translation inside a component and I enabled it in my configuration. We would talk about this later on in the article.

Once this is done, your plugin would be configured to work in your app and you would be notified of some extra files that this plugin has added to your app.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02cd59e9-7d78-47aa-8653-7bb9d7559ecb/02-config-files.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02cd59e9-7d78-47aa-8653-7bb9d7559ecb/02-config-files.png" sizes="100vw" caption="Vue-i18n config files. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02cd59e9-7d78-47aa-8653-7bb9d7559ecb/02-config-files.png'>Large preview</a>)" alt="A list of files added/modified by the plugin." >}}

Let us take a look at some of the files that were added to our app so we can understand their purpose:

### /locales folder

This folder serves as a base for all the locales that would be used in our app. If you open this folder, you will find an **en.json** file and this is because `en` was my selected locale for this project. What this means is that the file you will find inside your locale folder is dependent on your choice while setting up the plugin.

### /locales/en.json

This file is for adding texts in the particular locale(file name e.g en, fr) so that when a user switches to that locale, your app fetches all your texts from the JSON file that matches the locale. By default, this file contains one property that serves as a demo for setting up your application, it looks like this:

<pre><code class="language-javascript">{
  "message": "hello i18n !!"
}</code></pre>

Here, we have a `message` property that we can use anywhere in our file using this format:

<pre><code class="language-javascript">&lt;p&gt; {{ $t('message') }} &lt;/p&gt;
</code></pre>

if we view this in our browser, what we would see would be the value of `message` and not *"message".*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b90bbaf1-565b-4f7c-ac30-efbb07c1f3cf/03-plugin-text.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b90bbaf1-565b-4f7c-ac30-efbb07c1f3cf/03-plugin-text.png" sizes="100vw" caption="What vue-i18n displays in the browser. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b90bbaf1-565b-4f7c-ac30-efbb07c1f3cf/03-plugin-text.png'>Large preview</a>)" alt="Hello i18n." >}}

Now if you change the value of `message` in your file, it would be updated in your browser accordingly.

{{% ad-panel-leaderboard %}}

### HelloI18n.vue

This file serves as an example of how to use the plugin in [Single File Components](https://vuejs.org/v2/guide/single-file-components.html). If you inspect the file, you would find a `<i18n>` tag in the script section of this component. According to the documentation you would need to install [vue-i18n-loader](https://github.com/kazupon/vue-i18n-loader) to use this tag but you do not have to worry about this if you added it as a config option when installing the plugin. Inside this tag, we have an object which contains `en` (or your default locale) property which has a `hello` property with a value. This looks like this:

<pre><code class="language-javascript">&lt;i18n&gt;
{
  "en": {
    "hello": "Hello i18n in SFC!"
  }
}
&lt;/i18n&gt;</code></pre>
    
What this means is that you have given a component a value that is different from the value found in the **en.json** file inside the ***locales*** folder. In the template section of this component, we have:
 

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;{{ $t('hello') }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;</code></pre>
 
Here, we see `$t('')`, this is the syntax for referencing texts(**t** stands for texts) from our plugin, and in this component, we're using the value of `hello` that we added inside the `i18n` tag. If we check our browser, we should see *Hello i18n in SFC!* even if there is no `hello` property in the **en.json** file. This is called Component-based localization and we would go deeper into it later on in [this article](https://www.dropbox.com/scl/fi/83fwmb6d7d6ki9grnpwjs/Internationalization-in-Vue.paper?dl=0&rlkey=p375ayihwuka1bxedf2pfaih9#:uid=985977966247627244079005&h2=Component-Based-localization). 

## Formatting Texts

This plugin comes with the option to format your texts in different ways which can be helpful in enhancing user experience and we’re going to be looking at some of these formats.

### Named Formatting

This type of format option allows you add a dynamic value inside your text which would be defined when rendering the text in your browser. This type of format is useful when you want to add a personalized text with a user's info on login or after performing an action. To see how that works, we're going to add a new page to our app and call it **formatting.vue**, we're also going to add this as a route in our app.

First, let's create the file and add the following lines of code:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;section&gt;
    &lt;h1&gt;{{$t('formattingTitle')}}&lt;/h1&gt;
    &lt;p v-show="showMessage"&gt;{{ $t('hello', {name: name}) }}&lt;/p&gt;
    &lt;form @submit.prevent="showMessage = true"&gt;
      &lt;label for="name"&gt;{{ $t('name') }}&lt;/label&gt;
      &lt;input type="text" name="name" id="name" v-model="name" /&gt;
      &lt;input type="submit" :disabled="name.length &lt; 1" value="send" /&gt;
      &lt;label for="hideMessage" v-if="showMessage"&gt;
        &lt;input type="checkbox" name="hideMessage" id="hideMessage" v-model="showMessage" /&gt; Show Message
      &lt;/label&gt;
    &lt;/form&gt;
  &lt;/section&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  data() {
    return {
      name: "",
      showMessage: false
    };
  }
};
&lt;/script&gt;
&lt;style&gt;
form {
  width: 100%;
  max-width: 300px;
  margin: 20px auto;
}
label {
  display: block;
  width: 100%;
  text-align: left;
  margin-bottom: 5px;
}
input[type="text"] {
  width: 100%;
  height: 30px;
  border-radius: 3px;
  border: 1px solid #eee;
  padding-left: 10px;
  box-sizing: border-box;
  margin-bottom: 10px;
}
input[type="submit"] {
  width: 80px;
  height: 30px;
  border-radius: 3px;
  border: 0;
}
&lt;/style&gt;</code></pre>
</div>
   
In the template section of this file, we make use of this plugin to add a title (which we're yet to add) to this page. Inside the `<p>` tag, we make use of the named format to add a personalized message for the user which only displays if (`v-show`) `showMessage` is true. We have a form with an input field (connected to our data using v-model) that accepts a name that is passed to our plugin when the user submits the form. We have a checkbox that hides the message and a submit button that toggles `showMessage` to `true`.

In the script section, we have `name` and `showMessage` inside our data. Both of these variables are used in our form to store the user’s input and toggle the message respectively.

Now, let us add this `hello` to our **en.json** file (your default locale file). This looks like this:

<pre><code class="language-javascript">{
  "formattingTitle": "How to format your texts",
  "name": "What is your Name?",
  "hello": "Hi {name}, today is a good day"
}</code></pre>
   
Here, `formattingTitle` is the title for our formatting page while `hello` makes use of the name format that we used on the same page.

Finally, let us add this page to our router file. This looks like this:

<div class="break-out">

<pre><code class="language-javascript">import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'
Vue.use(Router)
export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [{
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/formatting',
      name: 'formatting',
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () =&gt; import( /* webpackChunkName: "format" */ './views/formatting.vue')
    }
  ]
})</code></pre>
</div>

In the router file, we make use of [route level code-splitting](https://router.vuejs.org/guide/advanced/lazy-loading.html) to load our component into its route (i.e `/formatting` ) which is another way of adding a component to a route in Vue.

Now, if we navigate to `/formatting` in our browser, we should see this:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf285a18-0d4d-4308-a7b6-60dfc75bdaca/04-formatting-landing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf285a18-0d4d-4308-a7b6-60dfc75bdaca/04-formatting-landing.png" sizes="100vw" caption="Current formatting page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf285a18-0d4d-4308-a7b6-60dfc75bdaca/04-formatting-landing.png'>Large preview</a>)" alt="Formatting page with an input field for name." >}}

Now, when you enter a value into the input field and press enter, you would see a personalized text above your form field.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5263926c-f473-492c-b4b1-7db13fc2b9ba/05-named-formatting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5263926c-f473-492c-b4b1-7db13fc2b9ba/05-named-formatting.png" sizes="100vw" caption="Named formatting in action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5263926c-f473-492c-b4b1-7db13fc2b9ba/05-named-formatting.png'>Large preview</a>)" alt="Formatting page containing a personalized greeting text with an input field with a name." >}}

{{% ad-panel-leaderboard %}}

### HTML Formatting

This involves using valid HTML in your text instead of plain text. This can be useful when you’re trying to display HTML formatted text to the user. Let us see how that works in our app.

Add the following to your locale file.

<pre><code class="language-javascript">{
  "htmlText": "&lt;h1&gt;HTML Rocks ❤❤&lt;/h1&gt;"
}</code></pre>

In our **formatting.vue** file, add the following lines of code after your form to the `template` section of this file.

<pre><code class="language-javascript">&lt;div v-html="$t('htmlText')"&gt;&lt;/div&gt;</code></pre>

Here, we make use of Vue’s [HTML directive](https://vuejs.org/v2/guide/syntax.html#Raw-HTML) to bind our text to this `div`. If you check it out in your browser, you should see the value of `htmlText` being rendered and if you inspect the div element, you should see the `h1` element nested inside this div.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce50f29-d292-4ca1-b302-1d6360103c22/06-html-formatting.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce50f29-d292-4ca1-b302-1d6360103c22/06-html-formatting.png" sizes="100vw" caption="Representation of HTML formatting. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce50f29-d292-4ca1-b302-1d6360103c22/06-html-formatting.png'>Large preview</a>)" alt="Formatting page with devtools open below it." >}}

## Switching Between Locale

Switching from one locale to another can be done by adding a file with this format to your locale folder.

<pre><code class="language-javascript">locale abbrevation + json
//eg en.json, fr.json, ru.json, de.json</code></pre>

After creating this file and adding a text(e.g ‘hello’) we want to use in our app, you can reference a text in that locale in two ways: 

- Per text:

<pre><code class="language-javascript">&lt;p&gt;{{ $t('hello', 'de') }} &lt;/p&gt;</code></pre>

This would render `hello`, but in Deutsch assuming we have it defined in that locale.

- Globally using `this.$i18n.locale`:

<pre><code class="language-javascript">console.log(this.$i18n.locale)
// prints 'en.json' because 'en' is my selected locale
this.$i18n.locale = 'de'
// sets your locale to 'de'</code></pre>

Let us add another use case to our application. The first thing we're going to do is add a new file to our locale folder and name it **de.json** then add this line object to the file.

<pre><code class="language-javascript">{
  "home": "Zuhause",
  "formatting": "Formatieren Sie Ihre Texte",
  "formattingTitle": "So formatieren Sie Ihre Texte",
  "name": "Wie heißen Sie?",
  "hello": "Hallo {name}, heute ist ein guter Tag",
  "htmlText": "<h1>HTML Rocks ❤❤</h1>"
}</code></pre>

We already have the `en` version of everything here in our **en.json** file but we want to be able to switch between `en` and `de` so we add the Deutsch translation of this to our **de.json** file.

The next thing would be to add a button that switches between `en` and `de` inside our **formatting.vue** file. Add this to your file:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;section&gt;
    &lt;!-- existing div element --&gt;
    &lt;div v-html="$t('htmlText')"&gt;&lt;/div&gt;
    &lt;button @click="switchLocale"&gt;Switch to {{locale}}&lt;/button&gt;
  &lt;/section&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  data() {
    return {
      name: "",
      showMessage: false,
      locale: "Deutsch"
    };
  },
  methods: {
    switchLocale() {
      this.$i18n.locale = this.locale === "English" ? "en" : "de";
      this.locale = this.$i18n.locale === "en" ? "Deutsch" : "English";
    }
  }
};
&lt;/script&gt;</code></pre>
</div>

In the template section, we have added a button with a click event that changes the locale from either `en` to `de` or vice versa. We also have a `locale` variable that dynamically changes from *English* to *Deutsch*. In the script section, we have added a `locale` variable to the data function of this component. Finally, we have a `switchLocale` method that is called whenever a user clicks on the button. This method changes the value of `this.$i18n.locale` using a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) to determine it’s own value between `de` and `en` based on what `locale` is. This means if `locale` is *English*, `this.$i18n.locale` will be `en` and if `this.$i18n.locale` is `de`, `locale` will be *English*.

If you view this in your browser, you should see this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a29a1894-6806-4cf1-aaf8-098eb4e7e066/07-en-locale.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a29a1894-6806-4cf1-aaf8-098eb4e7e066/07-en-locale.png" sizes="100vw" caption="Formatting page in default locale. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a29a1894-6806-4cf1-aaf8-098eb4e7e066/07-en-locale.png'>Large preview</a>)" alt="Formatting Page translated in English." >}}

And when you click on the button, you should see that every text on your page; in this component and globally, has changed from the default locale to Deutsch.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b830c82b-2316-4dbf-9a5c-6da07f5e4c44/08-de-locale.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b830c82b-2316-4dbf-9a5c-6da07f5e4c44/08-de-locale.png" sizes="100vw" caption="Formatting page in changed locale(de). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b830c82b-2316-4dbf-9a5c-6da07f5e4c44/08-de-locale.png'>Large preview</a>)" alt="Formatting page transalted in Deutsch." >}}

If you enter your name and submit the form, you should also see that it has been translated and looks like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8733a34-6b5f-4204-9b37-5337475b039f/09-de-locale.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8733a34-6b5f-4204-9b37-5337475b039f/09-de-locale.png" sizes="100vw" caption="Formatting page with personalized message in Deutsch. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8733a34-6b5f-4204-9b37-5337475b039f/09-de-locale.png'>Large preview</a>)" alt="Formatting page with personalized message in Deutsch." >}}

## Fallback Localization And Pluralization

### Fallback Localization

There are cases where you would not have the value of a property available in a selected locale. Instead of your app crashing as a result, it fetches the value of the text from the default locale and prints a warning error to your console. Let us look at an example.

We're going to add this text to our **en.json** file:

<pre><code class="language-javascript">  {
  "fallbackLocale": "Fallback Localization",
  "placeholder": "This is the fallback text"
}</code></pre>

And in our **de.json** file, we're only going to add this:

<pre><code class="language-javascript">{
  "fallbackLocale": "Fallback-Lokalisierung"
}</code></pre>

In our **formatting.vue** file, add this piece of code inside the file:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;section&gt;
    &lt;!-- last button --&gt;
    &lt;button @click="switchLocale"&gt;Switch to {{locale}}&lt;/button&gt;
    &lt;div&gt;
      &lt;h1&gt;{{ $t('fallbackLocale') }}&lt;/h1&gt;
    &lt;/div&gt;
    
  &lt;/section&gt;
&lt;/template&gt;
&lt;/style&gt;</code></pre>

Here, we have added a text with the property name `fallbackLocale` inside an `h1` tag that serves as the heading for this page. We also have a `p` tag that has a property name `placeholder` inside the plugin but with another parameter, `de` which as we’ve seen earlier, is a way of telling the plugin to fetch that property in the specified locale (`de` in this case).

Now, we should see this in our browser.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc8d3385-27c1-4614-99b6-101efbc6e32e/10-fallback.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc8d3385-27c1-4614-99b6-101efbc6e32e/10-fallback.png" sizes="100vw" caption="Formatting page with fallback text. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc8d3385-27c1-4614-99b6-101efbc6e32e/10-fallback.png'>Large preview</a>)" alt="formatting page with fallback text." >}}

We can notice that although we set `placeholder` to `de`, the text displayed is in `en`. This is because although we have set `placeholder` to display in another locale, it isn’t translated in the selected locale, and hence, the plugin would display this property in the default locale while printing a warning message to your console.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c7d25d-97ce-4615-a7a3-5ebf5c7660a3/11-fallback-warning.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c7d25d-97ce-4615-a7a3-5ebf5c7660a3/11-fallback-warning.png" sizes="100vw" caption="Fallback warning in console. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c7d25d-97ce-4615-a7a3-5ebf5c7660a3/11-fallback-warning.png'>Large preview</a>)" alt="Formatting page with fallback warning in devtools console." >}}

### Pluralization

This is the process of giving plural form to a word. For instance, you’re building an eCommerce application and you want to render an item in a user’s shopping cart based on the number they have in their cart. You can handle pluralization in your plugin by using a pipe `|` separator between all the plural forms in your locale.

To see how that works, let us add this to our **en.json** file.

<pre><code class="language-javascript">{
  "developer": "no developer | one developer | {n} developers"
}</code></pre>

*Note that the variable can be called anything but I have called it `n`.*

And in your **formatting.vue** file, instead of using `$t('')`, we would use `$tc('')` which also accepts a number as a second parameter ( `n` which we added in our locale file). So, if we add the following lines of code to our template.

<pre><code class="language-javascript">&lt;p&gt;{{ $tc('developer', 0) }}&lt;/p&gt;
&lt;p&gt;{{ $tc('developer', 1) }}&lt;/p&gt;
&lt;p&gt;{{ $tc('developer', 2) }}&lt;/p&gt;</code></pre>
   
Here, we set the first value for `n` to be zero, the second one is set to 1 and the last one is set to 2. Let us see what this looks like in our browser.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/648fef3d-b6c4-4be4-86aa-38f5eb1301af/12-pluralization.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/648fef3d-b6c4-4be4-86aa-38f5eb1301af/12-pluralization.png" sizes="100vw" caption="Implementation of pluralization. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/648fef3d-b6c4-4be4-86aa-38f5eb1301af/12-pluralization.png'>Large preview</a>)" alt="Pluralization of texts on formatting page." >}}

We can see that the plugin has translated each value and used the appropriate plural depending on the value of `n`. 

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2014/12/how-to-conduct-website-localization/">How To Conduct Website Localization: Don’t Get Lost In Translation</a></em></p>

## Component-Based Localization

There are cases where you’re only going to need some words or sentences in a component alone or instances where a global text has a different meaning in a particular component and in cases like this, component-based localization comes in handy. Component-based localization is the process of translating text/group of texts inside a component thereby making it only available inside such component. One thing we have to note is that the translation available inside your component takes precedence over the global translation so that if for instance, you're using `hello` in more than one place in your app and you want it to have a longer text or more personalized for a component, you only need to create a localization config for that component and define your new translation of `hello`.

If we open our **Components** folder, we should see a **Helloi18n.vue** file that was added to our app when we installed the plugin, this component was added to serve as a guide on how component-based localization works. 

To understand better, let us add the following translation inside our `<i18n>` element.

<pre><code class="language-javascript">&lt;i18n&gt;
{
  "en": {
    "hello": "Hello, {name}, this is i18n in SFC!",
    "greetings": "Component-Based Localization",
    "placeholder": "This is a component-based fallback text"
  }
}
&lt;/i18n&gt;</code></pre>

Here, we add a translation for `hello`, `greetings` and `placeholder`, all of which are also translated in the global **en.json** file. 

And in our component, let us add the following:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;h1&gt;{{ $t("greetings") }}&lt;/h1&gt;
    &lt;p v-if="name.length &gt; 0"&gt;{{ $t('hello', {name: name }) }}&lt;/p&gt;
    &lt;p&gt;{{ $t('placeholder') }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
  name: "HelloI18n",
  props: ["name"]
};
&lt;/script&gt;</code></pre>
</div>

Here, we have a heading that displays a translated `greetings` text, a paragraph tag that makes use of named formatting to display a personalized `hello` text from a `name` variable that would be passed to the component as a prop.

Finally we’re going to display this component in **formatting.vue**. Let us import it into this file:

<pre><code class="language-javascript">&lt;script&gt;
// @ is an alias to /src
import HelloI18n from "@/components/HelloI18n.vue";
export default {
  // existing code
  components: {
    HelloI18n
  }
};</code></pre>   

Here, we import the **Helloi18n.vue** component using `@` alias and define it inside the `components` property of our component.

And add it to our template like this:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;section&gt;
    &lt;!-- existing code --&gt;
    &lt;HelloI18n :name="name" /&gt;
  &lt;/section&gt;
&lt;/template&gt;</code></pre>
 
We defined a prop value `name` inside the `Helloi18n` component, so we pass it a value of `name` which we would get from the input field in the **formatting.vue** page.

Now, if we view this page in our browser, we should see this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8af9e3e0-fd32-40fb-b4be-458978d399b6/13-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8af9e3e0-fd32-40fb-b4be-458978d399b6/13-component.png" sizes="100vw" caption="Component-based localization. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8af9e3e0-fd32-40fb-b4be-458978d399b6/13-component.png'>Large preview</a>)" alt="Component-based localization." >}}

We can see that although we're using the same `greetings`, `hello` and `placeholder` text from the global translation file, the translation in the component is exactly what we defined inside the `<i18n>` tag.

## Conclusion

The *Vue I18n* plugin has a lot of use cases like:

- DataTime localization,
- Number localization,
- Locale message syntax,
- Lazy-loading translation, and so on.

All of which help in completely achieving internationalization of your application, so I would recommend you go through the full documentation and play around with some of them to get yourself familiarized with them. 

## Resources

- “[What Is i18n?](https://lingoport.com/what-is-i18n/),” Lingoport
- “[internationalization (I18N)](https://whatis.techtarget.com/definition/internationalization-I18N),” Margaret Rouse, WhatIs.com
- “[Vue I18n](https://kazupon.github.io/vue-i18n/),” an internationalization plugin for Vue.js created by Kazuya Kawaguchi

{{< signature "ks, ra, yk, il" >}}
