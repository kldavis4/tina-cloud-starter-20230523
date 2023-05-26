---
title: 'Replacing jQuery With Vue.js: No Build Step Necessary'
slug: jquery-vue-javascript
author: sarahdrasner
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf4eec9-7e14-4689-9b68-055ea6dfd48f/pic1.png
date: 2018-02-13T17:50:34+01:00
summary: >-
  Did you know that you can incorporate Vue into your project the same way that you would incorporate jQuery &mdash; with no build step necessary? Let's cover some common use cases in jQuery and how we can switch them over to Vue, and why we’d even want to do so.
description: >-
  Did you know that you can incorporate Vue into your project the same way that you would incorporate jQuery &mdash; with no build step necessary? Let's cover some common use cases in jQuery and how we can switch them over to Vue, and why we’d even want to do so.
categories:
  - JavaScript
  - Vue
  - HTML
  - jQuery
  - Guides
disable_newsletterbox: true
---
It’s been impossible to ignore all of the hype surrounding JavaScript frameworks lately, but they might not be the right fit for your projects. Perhaps you don’t want to set up an entire build system for some small abstractions you could feasibly do without. Perhaps moving a project over to a build system and thus, different deployment method would mean a lot of extra time and effort that you might not be able to bill to a client. Perhaps you don’t want to write all of your HTML in JavaScript. The list goes on.

What some people might not know is, you can incorporate Vue into your project the same way that you would incorporate jQuery, no build step necessary. Vue is flexible in the sense that we can use it directly in the HTML.

So, if your current page structure looks like this:

<div class="break-out">

 <pre><code class="language-html">&lt;main&gt;
  &lt;div class="thing"&gt;
     &lt;p&gt;Some content here&lt;/p&gt;
  &lt;/div&gt;
&lt;/main&gt;
&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"&gt;&lt;/script&gt;
&lt;script&gt;
  //some jquery code here
&lt;/script&gt;
</code></pre>
</div>

You could literally change the script tag here and still use the HTML and JS in tandem just as you did before, refactoring only a few small bits of code. You don’t have to rewrite the HTML in JavaScript, you don’t have to use webpack, and you don’t have to set up a giant system:

<div class="break-out">

 <pre><code class="language-html">&lt;main&gt;
  &lt;div class="thing"&gt;
     &lt;p&gt;Some content here&lt;/p&gt;
  &lt;/div&gt;
&lt;/main&gt;
&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.3/vue.min.js"&gt;&lt;/script&gt;
&lt;script&gt;
  //some vue code here
&lt;/script&gt;
</code></pre>
</div>

You can replace the tags and leave the markup as is. The best part is, you might think the code will get more complicated, but you might find in reading through this article and seeing the examples, that Vue is extremely simple, legible, and easy to maintain and adapt. In terms of size, they’re pretty comparable as well- to use them as is from a CDN, minified, Vue version 2.5.3 is **86KB**. jQuery 3.2.1 is **87KB**.

Let’s cover some common use cases in jQuery and how we’d switch them over to Vue, and why we’d even want to do so.

## Capturing User Inputs

A really common use case for needing JavaScript on a site is capturing user input from a form, so let’s start there. We won’t actually incorporate the full form yet in the interest of simplicity and clarity, but we’ll work up to it by the end.

To capture information as a user types, here’s how we would do this in jQuery and Vue &mdash; side by side:

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="032e1d97c62121e7a3aacc5b98775b94" >}}
See the Pen <a href="https://codepen.io/sdras/pen/032e1d97c62121e7a3aacc5b98775b94/">jQuery capture information from a form input</a> by Sarah Drasner (<a href="https://codepen.io/sdras">@sdras</a>) on <a href="https://codepen.io">CodePen</a>.
{{< /codepen >}}

<pre><code class="language-html">&lt;div id="app"&gt;
  &lt;label for="thing"&gt;Name:&lt;/label&gt;
  &lt;input id="thing" type="text" /&gt;
  &lt;p class="formname"&gt;&lt;/p&gt;
&lt;/div&gt;
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">// this is an alias to $(document).ready(function() {
$(function() {
  //keypress wouldn't include delete key, keyup does. We also query the div id app and find the other elements so that we can reduce lookups
  $('#app').keyup(function(e) {
    var formname = $(this).find('.formname');
    //store in a variable to reduce repetition
    var n_input = $(this).find('#thing').val();
    formname.empty();
    formname.append(n_input);
  });
});
</code></pre>
</div>

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="17e61eb9e8d700cc1d7e1190b32ff0b5" >}}
See the Pen <a href='https://codepen.io/sdras/pen/17e61eb9e8d700cc1d7e1190b32ff0b5/'>Vue capture information from a form input </a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;label for="name"&gt;Name:&lt;/label&gt;
  &lt;input id="name" type="text" v-model="name" /&gt; &lt;!--v-model is doing the magic here--&gt;
  &lt;p&gt;{{ name }}&lt;/p&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-javascript">//this is a vue instance
new Vue({
  //this targets the div id app
  el: '#app',
  data: {
    name: '' //this stores data values for ‘name’
  }
})
</code></pre>

I use this example because it reveals a few of Vue’s strengths. Vue is [reactive](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754), which makes it particularly capable of responding to changes. You can see how, as we’re updating what we’re typing, it changes instantly- there’s no delay.

You can also see that in the jQuery version, the DOM is in control- we’re fetching things out of the DOM, listening to it, and responding to it. This ties us to the way that the DOM is currently set up, and forces us to think about how to traverse it. If the structure of the HTML elements were to change, we’d have to adapt our code to correspond to those changes.

In the Vue version, *we’re* storing the state- we keep track of one property we want to update and change, and track the element we want to change by a thing called a directive. This means it’s attached directly to the HTML element we need to target. The structure of the DOM can change, the HTML can move around, and none of this would impact our performance or capturing these events. In our case, we’re using that v-model attribute on the input to connect to the data we’re storing in the JavaScript.

But! This isn’t as common a use case as storing something as you hit the enter key, so let’s look at that next.

{{% feature-panel %}}

## Storing User Input On A Single Event

The interesting thing about the way Vue works is that it’s decoupled from having to think about specific DOM events when storing and retrieving data. In essence, we already have an idea of what we want to capture; we’re giving it shape by picking an event with which to alter it. In contrast, jQuery is tightly coupled to what the DOM does and rests on those DOM events to build out the variables it stores, which can be placed anywhere, rather than one consistent group (in data) for retrieval. We can see this in the updated version of the last example, where the information is gathered on an enter keypress:

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="18c5eafd88bddc993017f404568f192c" >}}
See the Pen <a href='https://codepen.io/sdras/pen/18c5eafd88bddc993017f404568f192c'>jQuery capture information from a form input- on enter</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<pre><code class="language-html">&lt;div id="app"&gt;
  &lt;label for="thing"&gt;Name:&lt;/label&gt;
  &lt;input id="thing" type="text" /&gt;
  &lt;p class="formname"&gt;&lt;/p&gt;
&lt;/div&gt;
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">// this is an alias to $(document).ready(function() {
$(function() {
  //We query the div id app and find the other elements so that we can reduce lookups
  $('#app').change(function(e) {
    var n_input = $(this).find('#thing').val();
    $(this).find('.formname').append(n_input);
  });
});
</code></pre>
</div>

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="824c7c56ec1dff9862587bba0b20c135" >}}
See the Pen <a href='https://codepen.io/sdras/pen/824c7c56ec1dff9862587bba0b20c135'>Vue capture information from a form input, enter key</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<pre><code class="language-html">&lt;div id="app"&gt;
  &lt;label for="name"&gt;Name:&lt;/label&gt;
  &lt;input id="name" type="text" v-model.lazy="name" /&gt;
  &lt;p&gt;{{ name }}&lt;/p&gt;
&lt;/div&gt;
</code></pre>

<pre><code class="language-javascript">new Vue({
  el: '#app',
  data: {
    name: ''
  }
});
</code></pre>

In this version, the jQuery is simplified somewhat because we don’t have to capture things on every keystroke, but we’re still fishing things out of the DOM and responding step by step to these changes. Our code in jQuery will always go a little something like this:

<blockquote>"Go get this element, see what it’s doing, hold on to these changes, do something with these changes."</blockquote>

In comparison: In Vue, we’re in control of what’s changing, and the DOM responds to those changes based on our commands. We attach it directly to the thing we’d like to update. In our case, we have a small abstraction called a modifier: `v-model.lazy`. Vue now knows not to start storing this until after a change event occurs. Pretty neat!

{{% ad-panel-leaderboard %}}

## Toggling Classes

The next thing we’ll cover is toggling CSS classes because, as the almighty, ever-watching Googly has informed me, it’s the most common jQuery functionality.

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="8dff4c085a5dcf52ea04d4b06d68b409" >}}
See the Pen <a href='https://codepen.io/sdras/pen/8dff4c085a5dcf52ea04d4b06d68b409'>Toggle Class jQuery</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;button aria-pressed="false"&gt;Toggle me&lt;/button&gt;
  &lt;p class="toggle"&gt;Sometimes I need to be styled differently&lt;/p&gt;
&lt;/div&gt;
</code></pre>
</div>

<div class="break-out">

 <pre><code class="language-css">.red {
  color: red;
}

JS
$(function() {
  $('button').click(function(e) {
    $('.toggle').toggleClass('red');
    $(this).attr('aria-pressed', ($(this).attr('aria-pressed') == "false" ? true : false));
  });
});
</code></pre>
</div>

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="32ae6c7cb52e5b04d68d1203fab420bc" >}}
See the Pen <a href='https://codepen.io/sdras/pen/32ae6c7cb52e5b04d68d1203fab420bc'>Toggle Class Vue</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;button @click="active = !active" :aria-pressed="active ? 'true' : 'false'"&gt;Toggle me&lt;/button&gt;
  &lt;p :class="{ red: active }"&gt;Sometimes I need to be styled differently&lt;/p&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-css">.red {
  color: red;
}

JS
new Vue({
  el: '#app',
  data: {
    active: false
  }
})
</code></pre>

Again, what we see here is that in the jQuery version we’re storing the state in the DOM. The element has the class, and jQuery makes a decision based on the presence of the class, which it checks by pinging the DOM. In the Vue version, we store a condition, and we style it according to that state. We’re not asking the DOM for this information, we hold it ourselves.

We store `active` in the data, the button switches the condition, and `.red` is altered based on that condition. Even the states for accessibility, `aria-pressed`, are stated much quicker, as we don’t have to set anything in the script in Vue, we’re able to switch between states directly inline in the template based on the state of ‘`active`.’

You’ll also note in the last few examples, you might have thought it would be a lot more code to start working with Vue.js than jQuery, but they’re actually pretty comparable.

## Hiding And Showing

Another common jQuery use case is hiding and showing something. jQuery has always done a really good job of making this task really simple, so let’s take a look at what it looks like side to side with Vue.

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="bf643cbbed3c73457bcecb6e0d7b6815" >}}
See the Pen <a href='https://codepen.io/sdras/pen/bf643cbbed3c73457bcecb6e0d7b6815'>jQuery show hide</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<pre><code class="language-html">&lt;div id="app"&gt;
  &lt;button type="button" id="toggle" aria-expanded="false"&gt;
    Toggle Panel
  &lt;/button&gt;
  &lt;p class="hello"&gt;hello&lt;/p&gt;
&lt;/div&gt;
</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">$(function() {
  $('#toggle').on('click', function() {
    $('.hello').toggle();
    $(this).attr('aria-expanded', ($(this).attr('aria-expanded') == "false" ? true : false));
  });
});
</code></pre>
</div>

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="cd01c3bdc61692bd43095711c24010ca" >}}
See the Pen <a href='https://codepen.io/sdras/pen/cd01c3bdc61692bd43095711c24010ca'>Vue show hide</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;button @click="show = !show" :aria-expanded="show ? 'true' : 'false'"&gt;
    Toggle Panel
  &lt;/button&gt;
  &lt;p v-if="show"&gt;hello&lt;/p&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-javascript">new Vue({
  el: '#app',
  data: {
    show: true
  }
})
</code></pre>

Both jQuery and Vue do a nice job of keeping this task simple, but there are a couple of reasons that I really working with Vue for something like a toggle. Vue has a tool called [Vue devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en). This is not unlike the Chrome devtools, but when we use it, we get some special information about what’s going on with Vue.

In both the jQuery and Vue version, we can see that the element hides and appears. But what if something were to go wrong? What if something about our code wasn’t working the way we expected? In order to start debugging with jQuery, we’d probably add in some `console.log`s or set some breakpoints to try to track down where things were erroring.

Now, there ain’t nothin’ wrong with `console.log`s, but with the aid of the Vue devtools, we can actually get a hands-on Vue (couldn’t resist) of what Vue thinks is happening. In this gif below, you can see as we toggle the button, the Vue devtools updates the state of true/false accordingly. If the DOM was ever not to be working the way we expected, we could see the data in Vue in real time. This makes it much so much easier to debug; it’s actually quite wonderful.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22b5ef66-569f-4407-bc2a-ecfcb7a0e473/data-vue-real-time.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22b5ef66-569f-4407-bc2a-ecfcb7a0e473/data-vue-real-time.gif" width="800" alt="data in vue in real time" /></a></figure>

The other thing I like about this is that the `v-if` is easy to extend to other conditions. I can decide to use a thing called `v-show` instead of `v-if` if the thing I’m toggling will show and hide frequently: `v-if` will completely unmount the element, while `v-show` will merely toggle the visibility of it. This distinction is really important because it is much more performant to toggle the visibility in a style rather than completely unmounting/mounting the DOM node. I can show or hide something based on a lot of conditions, or even the presence of user input or other conditions as well. This is usually where jQuery can get a bit messy, pinging the DOM in multiple locations and coordinating them. Below is an example of coordinating showing something based on the presence of user input:

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="e1ca171e6b3bae93fc7ba70349d9d3bc" >}}
See the Pen <a href='https://codepen.io/sdras/pen/e1ca171e6b3bae93fc7ba70349d9d3bc'>Show button based on content Vue</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;label for="textarea"&gt;What is your favorite kind of taco?&lt;/label&gt;
  &lt;textarea id="textarea" v-model="tacos"&gt;&lt;/textarea&gt;
  &lt;br&gt;
  &lt;button v-show="tacos"&gt;Let us know!&lt;/button&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-javascript">new Vue({
  el: '#app',
  data() {
    return {
      tacos: ''
    }
  }
})
</code></pre>

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="da9cf10fd32971dc934494137c3dc2f2" >}}
See the Pen <a href='https://codepen.io/sdras/pen/da9cf10fd32971dc934494137c3dc2f2'>Show button based on content jQuery</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;label for="textarea"&gt;What is your favorite kind of taco?&lt;/label&gt;
  &lt;textarea id="textarea"&gt;&lt;/textarea&gt;
  &lt;br&gt;
  &lt;button v-show="tacos"&gt;Let us know!&lt;/button&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-javascript">$(function() {
  var button = $('.button');
  var textarea = $('#textarea');

  button.hide();
  textarea.keyup(function() {
    if (textarea.val().length > 0) {
      button.show();
    } else {
      button.hide();
    }
  })
});
</code></pre>

In this example, you can see the value of having Vue hold the state- we’re reacting to the changes very naturally and with less code altogether. Once you get used to the style, it’s faster to understand because you don’t have to trace the logic line by line. A lot of people call this difference "[imperative vs. declarative](https://www.redotheweb.com/2015/09/18/declarative-imperative-js.html)."

{{% ad-panel-leaderboard %}}

## Submitting A Form

The canonical use case for jQuery has historically been submitting a form with an AJAX call, so we should take a look at that as well. Vue actually does not have a built-in thing like AJAX; it’s typical in Vue application to use something like Axios (a JavaScript library for making HTTP requests) to help with this task.

This example is a little more complicated than the rest. We’re going to do a few things here:

1. The button will appear grey before we start typing in our form, then it will receive an “active” class and turn blue;
2. When we submit the form, we’ll keep the page from loading;
3. When the form is submitted, we’ll show the response data on the page.

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="100e681e2a5aa5259f5fec0920c88d12" >}}
See the Pen <a href='https://codepen.io/sdras/pen/100e681e2a5aa5259f5fec0920c88d12'>jQuery form submission AJAX</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;form action="/"&gt;
    &lt;div&gt;
      &lt;label for="name"&gt;Name:&lt;/label&gt;&lt;br&gt;
      &lt;input id="name" type="text" name="name" required/&gt;
    &lt;/div&gt;
    &lt;div&gt;
      &lt;label for="email"&gt;Email:&lt;/label&gt;&lt;br&gt;
      &lt;input id="email" type="email" name="email"  required/&gt;
    &lt;/div&gt;
    &lt;div&gt;
      &lt;label for="caps"&gt;HOW DO I TURN OFF CAPS LOCK:&lt;/label&gt;&lt;br&gt;
      &lt;textarea id="caps" name="caps" required&gt;&lt;/textarea&gt;
    &lt;/div&gt;
    &lt;button class="submit" type="submit"&gt;Submit&lt;/button&gt;
    &lt;div&gt;
      &lt;h3&gt;Response from server:&lt;/h3&gt;
      &lt;pre class="response"&gt;&lt;/pre&gt;
    &lt;/div&gt;
  &lt;/form&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-javascript">$(function() {
  var button = $("button");
  var name = $("input[name=name]");

  name.keyup(function() {
    if (name.val().length > 0) {
      button.addClass('active');
    } else {
      button.removeClass('active');
    }
  });

  $("form").submit(function(event) {
    event.preventDefault();

    //get the form data
    var formData = {
      name: $("input[name=name]").val(),
      email: $("input[name=email]").val(),
      caps: $("input[name=caps]").val()
    };

    // process the form
    $.ajax({
      type: "POST",
      url: "//jsonplaceholder.typicode.com/posts",
      data: formData,
      dataType: "json",
      encode: true
    }).done(function(data) {
      $(".response")
        .empty()
        .append(JSON.stringify(data, null, 2));
    });
  });
});
</code></pre>

In here, we’ll see lines 2-10 deal with the handling of the button class, similarly to how we did this before. We pass in a parameter called event to the form, and then say `event.preventDefault()` to keep from reloading the page. Then we collect all of the form data from the form inputs, process the form, and then put the response into the `.done()` call from the AJAX request.

{{< codepen height="480" theme_id="light" default_tab="result" user="sdras" editable="true" data-editable="true" slug_hash="aa180b495814b39d46af43ca4e624c6c" >}}
See the Pen <a href='https://codepen.io/sdras/pen/aa180b495814b39d46af43ca4e624c6c'>Vue form submission</a> by Sarah Drasner (<a href='https://codepen.io/sdras'>@sdras</a>) on <a href='https://codepen.io'>CodePen</a>.
{{< /codepen >}}

<div class="break-out">

 <pre><code class="language-html">&lt;div id="app"&gt;
  &lt;form @submit.prevent="submitForm"&gt;
    &lt;div&gt;
      &lt;label for="name"&gt;Name:&lt;/label&gt;&lt;br&gt;
      &lt;input id="name" type="text" v-model="name" required/&gt;
    &lt;/div&gt;
    &lt;div&gt;
      &lt;label for="email"&gt;Email:&lt;/label&gt;&lt;br&gt;
      &lt;input id="email" type="email" v-model="email" required/&gt;
    &lt;/div&gt;
    &lt;div&gt;
      &lt;label for="caps"&gt;HOW DO I TURN OFF CAPS LOCK:&lt;/label&gt;&lt;br&gt;
      &lt;textarea id="caps" v-model="caps" required&gt;&lt;/textarea&gt;
    &lt;/div&gt;
    &lt;button :class="[name ? activeClass : '']" type="submit"&gt;Submit&lt;/button&gt;
    &lt;div&gt;
      &lt;h3&gt;Response from server:&lt;/h3&gt;
      &lt;pre&gt;{{ response }}&lt;/pre&gt;
    &lt;/div&gt;
  &lt;/form&gt;
&lt;/div&gt;
</code></pre>
</div>

<pre><code class="language-javascript">new Vue({
  el: '#app',
  data() {
    return {
      name: '',
      email: '',
      caps: '',
      response: '',
      activeClass: 'active'
    }
  },
  methods: {
    submitForm() {
      axios.post('//jsonplaceholder.typicode.com/posts', {
        name: this.name,
        email: this.email,
        caps: this.caps
      }).then(response => {
        this.response = JSON.stringify(response, null, 2)
      })
    }
  }
})
</code></pre>

In the Vue version, we decide what fields we need to populate in the form, and then attach them with that v-model we used earlier. We check for the presence of name in order to toggle the class. Instead of passing in event and writing `event.preventDefault()`, all we have to do is write `@submit.prevent` on our form element, and that’s taken care of for us. To submit the post itself, we use Axios, and we’ll store the response in the Vue instance in response.

There are still many things we’d want to do to have a production-ready form, including [validation](https://vuejs.org/v2/cookbook/form-validation.html), error handling, and [writing tests](https://eddyerburgh.me/unit-test-vue-components-beginners), but in this small example, you can see how clean and legible Vue can be while handling a lot of things updating and changing, including user input.

## Conclusion

It is definitely ok to use jQuery if it suits you! This article serves to show that Vue is also a pretty nice abstraction for small sites that don’t need a lot of overhead. Vue is comparable in size, easy to reason about, and it’s fairly trivial to switch small pieces of functionality to Vue without rewriting your HTML in JavaScript and adopting a build system if you don’t have the bandwidth. This all makes it pretty compelling to consider.

Due to Vue’s flexibility, it’s also easy to transition this code to a build step and component structures if you’d like to adopt a more complex structure over time. It’s actually pretty fun to try it out, so when you’re ready to do so, [check out the vue-cli](https://github.com/vuejs/vue-cli). What this tool does is give you the ability to scaffold an entire production-level Vue and webpack build with just a couple of terminal commands. This allows you to work with single-file components, where you can use HTML, CSS, and Script in tandem in one file that makes up single, reusable components. You don’t have to configure the webpack build unless you’d like to do something special, so you save a lot of time setting things up. They even have a built-in command to get everything ready for production deployment.

The nice thing about the flexibility to choose either way of incorporating Vue into your project means that you’re not pressed to change your style of working all at once, and you can even make changes slowly over time. This is why people call Vue the progressive framework.

{{< signature "ra, il" >}}
