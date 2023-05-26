---
title: 'Using Slots In Vue.js'
slug: using-slots-vue-js
author: joseph-zimmerman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d8acd7-adb1-46d4-bc25-392624bb006f/using-slots-vue-js.png
date: 2019-07-03T12:30:59+02:00
summary: >-
  Slots are a powerful tool for creating reusable components in Vue.js, though they aren’t the simplest feature to understand. Let’s take a look at how to use slots and some examples of how they can be used in your Vue applications.
description: >-
  Slots are a powerful tool for creating reusable components in Vue.js, though they aren’t the simplest feature to understand. Let’s take a look at how to use slots and some examples of how they can be used in your Vue applications.
categories:
  - Vue
  - JavaScript
---
With the recent release of Vue 2.6, the syntax for using slots has been made more succinct. This change to slots has gotten me re-interested in discovering the potential power of slots to provide reusability, new features, and clearer readability to our Vue-based projects. What are slots truly capable of?

If you’re new to Vue or haven’t seen the changes from version 2.6, read on. Probably the best resource for learning about slots is [Vue’s own documentation](https://vuejs.org/v2/guide/components-slots.html), but I’ll try to give a rundown here. 

## What Are Slots?

Slots are a mechanism for Vue components that allows you to compose your components in a way other than the strict parent-child relationship. Slots give you an outlet to place content in new places or make components more generic. The best way to understand them is to see them in action. Let’s start with a simple example:

<pre><code class="language-html">// frame.vue
&lt;template&gt;
  &lt;div class="frame"&gt;
    &lt;slot&gt;&lt;/slot&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>

This component has a wrapper `div`. Let’s pretend that `div` is there to create a stylistic frame around its content. This component is able to be used generically to wrap a frame around any content you want. Let’s see what it looks like to use it. The `frame` component here refers to the component we just made above.

<pre><code class="language-html">// app.vue
&lt;template&gt;
  &lt;frame&gt;&lt;img src="an-image.jpg"&gt;&lt;/frame&gt;
&lt;/template&gt;
</code></pre>

The content that is between the opening and closing `frame` tags will get inserted into the `frame` component where the `slot` is, replacing the `slot` tags. This is the most basic way of doing it. You can also specify default content to go into a slot simply by filling it in:

<div class="break-out">

 <pre><code class="language-html">// frame.vue
&lt;template&gt;
  &lt;div class="frame"&gt;
    &lt;slot&gt;This is the default content if nothing gets specified to go here&lt;/slot&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

So now if we use it like this instead:

<pre><code class="language-html">// app.vue
&lt;template&gt;
  &lt;frame /&gt;
&lt;/template&gt;
</code></pre>

The default text of "This is the default content if nothing gets specified to go here" will show up, but if we use it as we did before, the default text will be overridden by the `img` tag. 

{{% feature-panel %}}

### Multiple/Named Slots

You can add multiple slots to a component, but if you do, all but one of them is required to have a name. If there is one without a name, it is the default slot. Here’s how you create multiple slots:

<div class="break-out">

 <pre><code class="language-html">// titled-frame.vue
&lt;template&gt;
  &lt;div class="frame"&gt;
    &lt;header&gt;&lt;h2&gt;&lt;slot name="header"&gt;Title&lt;/slot&gt;&lt;/h2&gt;&lt;/header&gt;
    &lt;slot&gt;This is the default content if nothing gets specified to go here&lt;/slot&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

We kept the same default slot, but this time we added a slot named `header` where you can enter a title. You use it like this:

<pre><code class="language-html">// app.vue
&lt;template&gt;
  &lt;titled-frame&gt;
    &lt;template v-slot:header&gt;
      &lt;!-- The code below goes into the header slot --&gt;
      My Image’s Title
    &lt;/template&gt;
    &lt;!-- The code below goes into the default slot --&gt;
    &lt;img src="an-image.jpg"&gt;
  &lt;/titled-frame&gt;
&lt;/template&gt;
</code></pre>

Just like before, if we want to add content to the default slot, just put it directly inside the `titled-frame` component. To add content to a named slot, though, we needed to wrap the code in a `template` tag with a `v-slot` directive. You add a colon (`:`) after `v-slot` and then write the name of the slot you want the content to be passed to. Note that `v-slot` is new to Vue 2.6, so if you’re using an older version, you’ll need to read the [docs about the deprecated slot syntax](https://vuejs.org/v2/guide/components-slots.html#Deprecated-Syntax).

### Scoped Slots

One more thing you’ll need to know is that slots can pass data/functions down to their children. To demonstrate this, we’ll need a completely different example component with slots, one that’s even more contrived than the previous one: let’s sorta copy the example from the docs by creating a component that supplies the data about the current user to its slots:

<pre><code class="language-html">// current-user.vue
&lt;template&gt;
  &lt;span&gt;
    &lt;slot v-bind:user="user"&gt;
      {{ user.lastName }}
    &lt;/slot&gt;
  &lt;/span&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  data () {
    return {
      user: ...
    }
  }
}
&lt;/script&gt;
</code></pre>

This component has a property called `user` with details about the user. By default, the component shows the user’s last name, but note that it is using `v-bind` to bind the user data to the slot. With that, we can use this component to provide the user data to its descendant:

<div class="break-out">

 <pre><code class="language-html">// app.vue
&lt;template&gt;
  &lt;current-user&gt;
    &lt;template v-slot:default="slotProps"&gt;{{ slotProps.user.firstName }}&lt;/template&gt;    
  &lt;/current-user&gt;
&lt;/template&gt;
</code></pre>
</div>

To get access to the data passed to the slot, we specify the name of the scope variable with the value of the `v-slot` directive. 

There are a few notes to take here:

- We specified the name of `default`, though we don’t need to for the default slot. Instead we could just use `v-slot="slotProps"`. 
- You don’t need to use `slotProps` as the name. You can call it whatever you want.
- If you’re only using a default slot, you can skip that inner `template` tag and put the `v-slot` directive directly onto the `current-user` tag.
- You can use object destructuring to create direct references to the scoped slot data rather than using a single variable name. In other words, you can use `v-slot="{user}"` instead of `v-slot="slotProps"` and then you can use `user` directly instead of `slotProps.user`.

Taking those notes into account, the above example can be rewritten like this:

<pre><code class="language-html">// app.vue
&lt;template&gt;
  &lt;current-user v-slot="{user}"&gt;
    {{ user.firstName }}
  &lt;/current-user&gt;
&lt;/template&gt;
</code></pre>

A couple more things to keep in mind:

- You can bind more than one value with `v-bind` directives. So in the example, I could have done more than just `user`.
- You can pass functions to scoped slots too. Many libraries use this to provide reusable functional components as you’ll see later.
- `v-slot` has an alias of `#`. So instead of writing `v-slot:header="data"`, you can write `#header="data"`. You can also just specify `#header` instead of `v-slot:header` when you’re not using scoped slots. As for default slots, you’ll need to specify the name of `default` when you use the alias. In other words, you’ll need to write `#default="data"` instead of `#="data"`.

There are a few more minor points you can learn about from [the docs](https://vuejs.org/v2/guide/components-slots.html), but that should be enough to help you understand what we’re talking about in the rest of this article.

{{% ad-panel-leaderboard %}}

## What Can You Do With Slots?

Slots weren’t built for a single purpose, or at least if they were, they’ve evolved way beyond that original intention to be a powerhouse tool for doing many different things.

### Reusable Patterns

Components were always designed to be able to be reused, but some patterns aren’t practical to enforce with a single "normal" component because the number of `props` you’ll need in order to customize it can be excessive or you'd need to pass large sections of content and potentially other components through the `props`. Slots can be used to encompass the "outside" part of the pattern and allow other HTML and/or components to placed inside of them to customize the "inside" part, allowing the component with slots to define the pattern and the components injected into the slots to be unique. 

<p class="c-pre-sidenote--left">For our first example, let’s start with something simple: a button. Imagine you and your team are using <a href="https://getbootstrap.com/">Bootstrap</a>*. With Bootstrap, your buttons are often strapped with the base `btn` class and a class specifying the color, such as `btn-primary`. You can also add a size class, such as `btn-lg`.</p><p class="c-sidenote c-sidenote--right">* I neither encourage nor discourage you from doing this, I just needed something for my example and it’s pretty well known.</p>

Let’s now assume, for simplicity’s sake that your app/site always uses `btn-primary` and `btn-lg`. You don’t want to always have to write all three classes on your buttons, or maybe you don’t trust a rookie to remember to do all three. In that case, you can create a component that automatically has all three of those classes, but how do you allow customization of the content? A `prop` isn’t practical because a `button` tag is allowed to have all kinds of HTML in it, so we should use a slot.

<pre><code class="language-html">&lt;!-- my-button.vue --&gt;
&lt;template&gt;
  &lt;button class="btn btn-primary btn-lg"&gt;
    &lt;slot&gt;Click Me!&lt;/slot&gt;
  &lt;/button&gt;
&lt;/template&gt;
</code></pre>

Now we can use it everywhere with whatever content you want:

<div class="break-out">

 <pre><code class="language-html">&lt;!-- somewhere else, using my-button.vue --&gt;
&lt;template&gt;
  &lt;my-button&gt;
    &lt;img src="/img/awesome-icon.jpg"&gt; SMASH THIS BUTTON TO BECOME AWESOME FOR ONLY $500!!!
  &lt;/my-button&gt;
&lt;/template&gt;
</code></pre>
</div>

Of course, you can go with something much bigger than a button. Sticking with Bootstrap, let’s look at a modal, or least the HTML part; I won’t be going into functionality... yet.

<div class="break-out">

 <pre><code class="language-html">&lt;!-- my-modal.vue --&gt;
&lt;template&gt;
&lt;div class="modal" tabindex="-1" role="dialog"&gt;
  &lt;div class="modal-dialog" role="document"&gt;
    &lt;div class="modal-content"&gt;
      &lt;div class="modal-header"&gt;
        &lt;slot name="header"&gt;&lt;/slot&gt;
        &lt;button type="button" class="close" data-dismiss="modal" aria-label="Close"&gt;
          &lt;span aria-hidden="true"&gt;&times;&lt;/span&gt;
        &lt;/button&gt;
      &lt;/div&gt;
      &lt;div class="modal-body"&gt;
        &lt;slot name="body"&gt;&lt;/slot&gt;
      &lt;/div&gt;
      &lt;div class="modal-footer"&gt;
        &lt;slot name="footer"&gt;&lt;/slot&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
&lt;/template&gt;
</code></pre>
</div>

Now, let’s use this:

<div class="break-out">

 <pre><code class="language-html">&lt;!-- somewhere else, using my-modal.vue --&gt;
&lt;template&gt;
  &lt;my-modal&gt;
    &lt;template #header&gt;&lt;!-- using the shorthand for `v-slot` --&gt;
      &lt;h5&gt;Awesome Interruption!&lt;/h5&gt;
    &lt;/template&gt;
    &lt;template #body&gt;
      &lt;p&gt;We interrupt your use of our application to
      let you know that this application is awesome 
      and you should continue using it every day for 
      the rest of your life!&lt;/p&gt;
    &lt;/template&gt;
    &lt;template #footer&gt;
      &lt;em&gt;Now back to your regularly scheduled app usage&lt;/em&gt;
    &lt;/template&gt;
  &lt;/my-modal&gt;
&lt;/template&gt;
</code></pre>
</div>

The above type of use case for slots is obviously very useful, but it can do even more.

### Reusing Functionality

Vue components aren’t all about the HTML and CSS. They’re built with JavaScript, so they’re also about functionality. Slots can be useful for creating *functionality* once and using it in multiple places. Let’s go back to our modal example and add a function that closes the modal:

<div class="break-out">

 <pre><code class="language-html">&lt;!-- my-modal.vue --&gt;
&lt;template&gt;
&lt;div class="modal" tabindex="-1" role="dialog"&gt;
  &lt;div class="modal-dialog" role="document"&gt;
    &lt;div class="modal-content"&gt;
      &lt;div class="modal-header"&gt;
        &lt;slot name="header"&gt;&lt;/slot&gt;
        &lt;button type="button" class="close" data-dismiss="modal" aria-label="Close"&gt;
          &lt;span aria-hidden="true"&gt;&times;&lt;/span&gt;
        &lt;/button&gt;
      &lt;/div&gt;
      &lt;div class="modal-body"&gt;
        &lt;slot name="body"&gt;&lt;/slot&gt;
      &lt;/div&gt;
      &lt;div class="modal-footer"&gt;
        &lt;!--
          using `v-bind` shorthand to pass the `closeModal` method
          to the component that will be in this slot
        --&gt;
        &lt;slot name="footer" :closeModal="closeModal"&gt;&lt;/slot&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  //...
  methods: {
    closeModal () {
      // Do what needs to be done to close the modal... and maybe remove it from the DOM
    }
  }
}
&lt;/script&gt;
</code></pre>
</div>

Now when you use this component, you can add a button to the footer that can close the modal. Normally, in the case of a Bootstrap modal, you could just add `data-dismiss="modal"` to a button, but we want to hide Bootstrap specific things away from the components that will be slotting into this modal component. So we pass them a function they can call and they are none the wiser about Bootstrap’s involvement:

<div class="break-out">

 <pre><code class="language-html">&lt;!-- somewhere else, using my-modal.vue --&gt;
&lt;template&gt;
  &lt;my-modal&gt;
    &lt;template #header&gt;&lt;!-- using the shorthand for `v-slot` --&gt;
      &lt;h5&gt;Awesome Interruption!&lt;/h5&gt;
    &lt;/template&gt;
    &lt;template #body&gt;
      &lt;p&gt;We interrupt your use of our application to
      let you know that this application is awesome 
      and you should continue using it every day for 
      the rest of your life!&lt;/p&gt;
    &lt;/template&gt;
    &lt;!-- pull in `closeModal` and use it in a button’s click handler --&gt;
    &lt;template #footer="{closeModal}"&gt;
      &lt;button @click="closeModal"&gt;
        Take me back to the app so I can be awesome
      &lt;/button&gt;
    &lt;/template&gt;
  &lt;/my-modal&gt;
&lt;/template&gt;
</code></pre>
</div>

### Renderless Components

And finally, you can take what you know about using slots to pass around reusable functionality and strip practically all of the HTML and just use the slots. That’s essentially what a renderless component is: a component that provides only functionality without any HTML.

Making components truly renderless can be a little tricky because you’ll need to write `render` functions rather than using a template in order to remove the need for a root element, but it may not always be necessary. Let’s take a look at a simple example that does let us use a template first, though:

<pre><code class="language-html">&lt;template&gt;
  &lt;transition name="fade" v-bind="$attrs" v-on="$listeners"&gt;
    &lt;slot&gt;&lt;/slot&gt;
  &lt;/transition&gt;
&lt;/template&gt;
&lt;style&gt;
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
&lt;/style&gt;
</code></pre>

This is an odd example of a renderless component because it doesn’t even have any JavaScript in it. That’s mostly because we’re just creating a pre-configured reusable version of a built-in renderless function: `transition`.

Yup, Vue has built-in renderless components. This particular example is taken from an article on [reusable transitions by Cristi Jora](https://vuejsdevelopers.com/2018/02/26/vue-js-reusable-transitions/) and shows a simple way to create a renderless component that can standardize the transitions used throughout your application. Cristi’s article goes into a lot more depth and shows some more advanced variations of reusable transitions, so I recommend checking it out.

{{% ad-panel-leaderboard %}}

For our other example, we’ll create a component that handles switching what is shown during the different states of a Promise: pending, successfully resolved, and failed. It’s a common pattern and while it doesn’t require a lot of code, it can muddy up a lot of your components if the logic isn’t pulled out for reusability.

<div class="break-out">

 <pre><code class="language-html">&lt;!-- promised.vue --&gt;
&lt;template&gt;
  &lt;span&gt;
    &lt;slot  name="rejected"  v-if="error" :error="error"&gt;&lt;/slot&gt;
    &lt;slot  name="resolved"  v-else-if="resolved" :data="data"&gt;&lt;/slot&gt;
    &lt;slot  name="pending"  v-else&gt;&lt;/slot&gt;
  &lt;/span&gt;
&lt;/template&gt;

&lt;script&gt;
export  default {
  props: {
    promise:  Promise
  },

  data: () =&gt; ({
    resolved:  false,
    data:  null,
    error:  null
  }),  

  watch: {
    promise: {
      handler (promise) {
        this.resolved  =  false
        this.error  =  null

        if (!promise) {
          this.data  =  null
          return
        }

        promise.then(data  =&gt; {
          this.data  =  data
          this.resolved  =  true
        })
        .catch(err  =&gt; {
          this.error  =  err
          this.resolved  =  true
        })
      },
      immediate:  true
    }
  }
}
&lt;/script&gt;
</code></pre>
</div>

So what is going on here? First, note that we are receiving a prop called `promise` that is a `Promise`. In the `watch` section we watch for changes to the promise and when it changes (or immediately on component creation thanks to the `immediate` property) we clear the state, and call `then` and `catch` on the promise, updating the state when it either finishes successfully or fails.

Then, in the template, we show a different slot based on the state. Note that we failed to keep it truly renderless because we needed a root element in order to use a template. We’re passing `data` and `error` to the relevant slot scopes as well.

And here’s an example of it being used:

<pre><code class="language-html">&lt;template&gt;
  &lt;div&gt;
    &lt;promised :promise="somePromise"&gt;
      &lt;template #resolved="{ data }"&gt;
        Resolved: {{ data }}
      &lt;/template&gt;
      &lt;template #rejected="{ error }"&gt;
        Rejected: {{ error }}
      &lt;/template&gt;
      &lt;template #pending&gt;
        Working on it...
      &lt;/template&gt;
    &lt;/promised&gt;
  &lt;/div&gt;
&lt;/template&gt;
...
</code></pre>

We pass in `somePromise` to the renderless component. While we’re waiting for it to finish, we’re displaying "Working on it..." thanks to the `pending` slot. If it succeeds we display "Resolved:" and the resolution value. If it fails we display "Rejected:" and the error that caused the rejection. Now we no longer need to track the state of the promise within this component because that part is pulled out into its own reusable component.

So, what can we do about that `span` wrapping around the slots in `promised.vue`? To remove it, we’ll need to remove the `template` portion and add a `render` function to our component:

<pre><code class="language-javascript">render () {
  if (this.error) {
    return this.$scopedSlots['rejected']({error: this.error})
  }

  if (this.resolved) {
    return this.$scopedSlots['resolved']({data: this.data})
  }

  return this.$scopedSlots['pending']()
}
</code></pre>

There isn’t anything too tricky going on here. We’re just using some `if` blocks to find the state and then returning the correct scoped slot (via `this.$scopedSlots['SLOTNAME'](...)`) and passing the relevant data to the slot scope. When you’re not using a template, you can skip using the `.vue` file extension by pulling the JavaScript out of the `script` tag and just plunking it into a `.js` file. This should give you a very slight performance bump when compiling those Vue files.

This example is a stripped-down and slightly tweaked version of [vue-promised](https://github.com/posva/vue-promised), which I would recommend over using the above example because they cover over some potential pitfalls. There are plenty of other great examples of renderless components out there too. [Baleada](https://baleada.netlify.com/docs) is an entire library full of renderless components that provide useful functionality like this. There’s also [vue-virtual-scroller](https://github.com/Akryum/vue-virtual-scroller) for controlling the rendering of list item based on what is visible on the screen or [PortalVue](https://github.com/LinusBorg/portal-vue) for "teleporting" content to completely different parts of the DOM.

## I’m Out

Vue’s slots take component-based development to a whole new level, and while I’ve demonstrated a lot of great ways slots can be used, there are countless more out there. What great idea can you think of? What ways do you think slots could get an upgrade? If you have any, make sure to bring your ideas to the Vue team. God bless and happy coding.

{{< signature "dm, il" >}}
