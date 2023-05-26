---
title: 'Creating Custom Inputs With Vue.js'
slug: creating-custom-inputs-vue-js
image: //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c878ef7-7d73-4bdc-bd2b-0bbd50de3dac/vue-js.png
date: 2017-08-01T20:01:07.000Z
author: joseph-zimmerman
summary: >-
  This tutorial aims to help you understand how v-model works on native inputs and on custom components by default. Also, you’ll learn how to create custom checkboxes and radios that emulate how v-model works on them natively.
description: >-
  This tutorial aims to help you understand how v-model works on native inputs and on custom components by default. Also, you’ll learn how to create custom checkboxes and radios that emulate how v-model works on them natively.
categories:
  - Vue
  - Frameworks
  - JavaScript
---
In particular, form inputs tend to have plenty of complexity that you'd want to hide in a component, such as [custom designs](https://codepen.io/AngelaVelasquez/pen/Eypnq), labels, validation, help messages, and making sure each of these pieces are in the correct order so that they render correctly.

On top of that though, Vue has a built-in directive called `v-model` that **simulates 2-way binding** by binding a value and capturing input events. If you're going to build a custom input component, then you'll definitely want to support the `v-model` directive.

Sadly, when I looked around for examples of custom inputs in Vue for radio buttons or checkboxes, they either didn't take `v-model` into consideration at all, or they failed to implement it correctly. There is some decent [documentation for custom text inputs](https://vuejs.org/v2/guide/components.html#Form-Input-Components-using-Custom-Events), but since it doesn't explain customizing radios or checkboxes, we'll discuss that here.

<div class="c-felix-the-cat">
<h4 class="h3">Writing Reusable Modules in ES6</h4>
<p>Are you excited to <strong>take advantage of new JavaScript language features</strong> but not sure <em>where</em> to start, or <em>how</em>? <a href="https://www.smashingmagazine.com/2016/02/writing-next-generation-reusable-javascript-modules/" class="btn btn--medium btn--blue">Read a related article&nbsp;→</a></p>
</div>

By the end of this tutorial, I hope I'll help you:

1.  Understand how `v-model` works on native inputs, focusing primarily on radios and checkboxes,
2.  Understand how `v-model` works on custom components by default,
3.  Learn how to create custom checkboxes and radios that emulate how `v-model` works on them natively.

_Quick note before we get started_: ES2015+ code will be used throughout the code examples. I'll also be favoring the [Single File Component](https://vuejs.org/v2/guide/single-file-components.html) syntax over using `Vue.component` or `new Vue`.</p>

{{% feature-panel %}}

## How Does `v-model` Work Normally?

The official [Vue documentation](https://vuejs.org/v2/guide/forms.html) is actually pretty good on this topic, but there are a few minor blind spots. In any case, we'll be trying to cover it pretty thoroughly here.

In essence, `v-model` is just a shorthand directive that gives us 2-way data binding, and the code it is shorthand for depends on what type of input it is being used on.</p>

### Text Boxes

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;input v-model="message" placeholder="edit me"&gt;
&lt;p&gt;Message: {{ message }}&lt;/p&gt;

&lt;!-- OR --&gt;

&lt;p&gt;message:&lt;/p&gt;
&lt;p style="white-space: pre-line"&gt;{{ message }}&lt;/p&gt;
&lt;textarea v-model="message" placeholder="add multiple lines"&gt;&lt;/textarea&gt;
&lt;/div&gt;
</code></pre>
</div>

When using a text `input` (including types such as `email`, `number`, etc.) or `textarea`, `v-model="varName"` is equivalent to `:value="varName" @input="e => varName = e.target.value"`. This means that the value of the input is set to `varName` after each update to the input `varName` is updated to the value of the input. A normal `select` element will act like this too, though a `multiple` select will be different.</p>

## Radio Buttons

So, what about radio buttons?

<pre><code class="language-markup">&lt;div&gt;&lt;input type="radio" value="One" v-model="picked"&gt;
&lt;input type="radio" value="Two" v-model="picked"&gt;
&lt;span&gt;Picked: {{ picked }}&lt;/span&gt;
&lt;/div&gt;
</code></pre>

This is equivalent to:

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;input type="radio" value="One" :checked="picked == 'One'" @change="e =&gt; picked = e.target.value"&gt;
&lt;input type="radio" value="Two" :checked="picked == 'Two'" @change="e =&gt; picked = e.target.value"&gt;
&lt;span&gt;Picked: {{ picked }}&lt;/span&gt;
&lt;/div&gt;
</code></pre>
</div>

Note how `v-model` isn't even touching `value` anymore. It's still doing the same thing in the `change` event handler (though it was changed to `change` instead of `input`), but now it's determining whether `checked` should be true or false depending on whether `picked` is the same as the value of that radio button.</p>

{{% ad-panel-leaderboard %}}

## Checkboxes

Checkboxes are a bit more difficult to talk about because they have two different behaviors depending on whether there is only a single checkbox with a given `v-model` or multiple.

If you are using a single checkbox, `v-model` will treat it like a boolean and ignore the `value`.

<pre><code class="language-markup">&lt;div&gt;&lt;input type="checkbox" value="foo" v-model="isChecked"&gt;
&lt;/div&gt;
</code></pre>

is the same as...

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;input type="checkbox" value="foo" :checked="!!isChecked" @change="e =&gt; isChecked = e.target.checked"&gt;
&lt;/div&gt;
</code></pre>
</div>

If you want it to be something other than `true` and `false`, you can use the `true-value` and `false-value` attribute, which control what values your model will be set to when the checkbox is checked or not.

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;input type="checkbox" value="foo" v-model="isChecked" true-value="1" false-value="0"&gt;
&lt;/div&gt;
</code></pre>
</div>

is the same as...

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;input type="checkbox" value="foo" :checked="isChecked == '1'" @change="e =&gt; isChecked = e.target.checked ? '1' : '0'"&gt;
&lt;/div&gt;
</code></pre>
</div>

That's pretty much it for single-checkbox examples. If you have multiple checkboxes that share a model, then those checkboxes will fill an array with values of all the checkboxes that are checked, but make sure the model that you pass in is already an array or you'll get some odd behavior. Also, the `true-value` and `false-value` attributes no longer affect anything.

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;template&gt;
  &lt;div&gt;
    &lt;input type="checkbox" value="foo" v-model="checkedVals"&gt;
    &lt;input type="checkbox" value="bar" v-model="checkedVals"&gt;
    &lt;input type="checkbox" value="baz" v-model="checkedVals"&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;&lt;span class="javascript"&gt;
  export default {
    data: () =&gt; ({
      checkedVals: ['bar']
    })
  }
&lt;/script&gt;
&lt;/div&gt;
</code></pre>
</div>

The equivalent is a bit more difficult to keep inside the template, so I'll move some of the logic to methods on the component:

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;template&gt;
  &lt;div&gt;
    &lt;input type="checkbox" value="foo" v-model="checkedVals"&gt;
    &lt;input type="checkbox" value="bar" v-model="checkedVals"&gt;
    &lt;input type="checkbox" value="baz" v-model="checkedVals"&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;&lt;span class="javascript"&gt;
  export default {
    data() {
      return { checkedVals: ['bar'] }
    },
    methods: {
      shouldBeChecked(val) {
        return this.checkedVals.includes(val)
      },
      updateVals(e) {
        let isChecked = e.target.checked
        let val = e.target.value

        if (isChecked) {
          this.checkedVals.push(val)
        } else {
          this.checkVals.splice(this.checkedVals.indexOf(val), 1)
        }
      }
    }
  }
&lt;/script&gt;
&lt;/div&gt;
</code></pre>
</div>

That's a lot more complicated than what we've seen before, but if you break it down, it's not too bad. `shouldBeChecked` is `true` when that checkbox's value is included in the array and `false` if it isn't. `updateVals` adds the checkbox's value to the array when it gets checked and removes it when it gets unchecked.

## How Does `v-model` Work On Components?

Since Vue doesn't know how your component is supposed to work, or if it's trying to act as a replacement for a certain type of input, it treats all components the same with regards to `v-model`. It actually works the exact same way as it does for text inputs, except that in the event handler, it doesn't expect an event object to be passed to it, rather it expects the value to be passed straight to it. So...

<pre><code class="language-markup">&lt;div&gt;&lt;my-custom-component v-model="myProperty" /&gt;
&lt;/div&gt;
</code></pre>

...is the same thing as...

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;my-custom-component :value="myProperty" @input="val =&gt; myProperty = val" /&gt;
&lt;/div&gt;
</code></pre>
</div>

A component can change this to a small extent using the `model` property:

<pre><code class="language-javascript">&lt;div&gt;export default {
  name: 'my-custom-component',
  model: {
    prop: 'foo',
    event: 'bar'
  },
  // ...
}
&lt;/div&gt;
</code></pre>

`v-model` will look at these properties and instead of using the `value` attribute, it'll use the attribute you specify in `prop` and instead of listening for the `input` event, it'll use the event you specified in `event`. So the above `my-custom-component` example would actually expand out to the following:

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;my-custom-component :foo="myProperty" @bar="val =&gt; myProperty = val" /&gt;
&lt;/div&gt;
</code></pre>
</div>

This is nice, but if we're making a custom radio or checkbox, this doesn't work very well. With some work, though, we can move the logic that `v-model` uses on radios and checkboxes inside our custom components.</p>

{{% ad-panel-leaderboard %}}

## Supporting `v-model` On Custom Radios

Compared to a checkbox, custom radios are quite simple. Here's a very basic custom radio that I build that just wraps the `input` in a label and accepts a `label` property to add the label text.

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;template&gt;
  &lt;label&gt;
    &lt;input type="radio" :checked="shouldBeChecked" :value="value" @change="updateInput"&gt;
    {{ label }}
  &lt;/label&gt;
&lt;/template&gt;
&lt;script&gt;&lt;span class="javascript"&gt;
export default {
  model: {
    prop: 'modelValue',
    event: 'change'
  },
  props: {
    value: {
      type: &lt;span class="hljs-built_in"&gt;String,
    },
    modelValue: {
      default: ""
    },
    label: {
      type: &lt;span class="hljs-built_in"&gt;String,
      required: true
    },
  },
  computed: {
    shouldBeChecked() {
      return this.modelValue == this.value
    }
  }
  methods: {
    updateInput() {
      this.$emit('change', this.value)
    }
  }
}
&lt;/script&gt;
&lt;/div&gt;
</code></pre>
</div>

**Note**: *I only included `props` that are helpful for explaining how these should work with `v-model`, but `input` tags can take advantage of several other attributes (such as `name` or `disabled`), so make sure you create all of the `props` you'll need and pass them on to `input`. You'll also want to consider accessibility by adding [WAI-ARIA attributes](https://www.w3.org/WAI/intro/aria), as well as using [slots](https://vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots) for adding content rather than props like I did here with `label`.*

You may think that since I didn't include `name` in this example, a group of radios wouldn't actually sync up with one another. Actually the updating of the model will in turn update the other radio buttons that share that model, so they don't need to share a name like they do in plain HTML forms as long as they share the same model.</p>

## Supporting `v-model` On Custom Checkboxes

Making custom checkboxes is noticeably more complex than the radio buttons, primarily because we have to support two different use cases: a single true/false checkbox (that may or may not use `true-value` and/or `false-value`) and multiple checkboxes that combine all the checked values into an array.

So how do we determine which use case it is? You might think that we need to determine if there are other checkboxes with the same `name` attribute, but that's not actually what Vue's built-in system uses. Just like the radios, Vue doesn't take the `name` attribute into consideration at all. That's only used when natively submitting a form. So then you might think it determines it based on whether there are other checkboxes that share the same model, but that's not it either. It's determined by whether or not the model is an array. That's it.

So the code will be structured similarly to the custom radio button's code, but inside `shouldBeChecked` and `updateInput` the logic will split depending on whether or not `modelValue` is an array.

<div class="break-out">

 <pre><code class="language-markup">&lt;div&gt;&lt;template&gt;
  &lt;label&gt;
    &lt;input type="checkbox" :checked="shouldBeChecked" :value="value" @change="updateInput"&gt;
    {{ label }}
  &lt;/label&gt;
&lt;/template&gt;
&lt;script&gt;&lt;span class="javascript"&gt;
export default {
  model: {
    prop: 'modelValue',
    event: 'change'
  },
  props: {
    value: {
      type: &lt;span class="hljs-built_in"&gt;String,
    },
    modelValue: {
      default: false
    },
    label: {
      type: &lt;span class="hljs-built_in"&gt;String,
      required: true
    },
    // We set `true-value` and `false-value` to the default true and false so
    // we can always use them instead of checking whether or not they are set.
    // Also can use camelCase here, but hyphen-separating the attribute name
    // when using the component will still work
    trueValue: {
      default: true
    },
    falseValue: {
      default: false
    }
  },
  computed: {
    shouldBeChecked() {
      if (this.modelValue instanceof &lt;span class="hljs-built_in"&gt;Array) {
        return this.modelValue.includes(this.value)
      }
      // Note that `true-value` and `false-value` are camelCase in the JS
      return this.modelValue === this.trueValue
    }
  },
  methods: {
    updateInput(event) {
      let isChecked = event.target.checked

      if (this.modelValue instanceof &lt;span class="hljs-built_in"&gt;Array) {
        let newValue = [...this.modelValue]

        if (isChecked) {
          newValue.push(this.value)
        } else {
          newValue.splice(newValue.indexOf(this.value), 1)
        }

        this.$emit('change', newValue)
      } else {
        this.$emit('change', isChecked ? this.trueValue : this.falseValue)
      }
    }
  }
}
&lt;/script&gt;
&lt;/div&gt;
</code></pre>
</div>

And there you have it. It may be better, though, to split this into two different components: one for handling the single true/false toggle and one for use in lists of options. That would allow it to more closely follow the Single-Responsibility Principle, but if you're looking for a drop-in replacement to checkboxes, this is what you're looking for (plus the addition of all the other useful attributes and custom features you might want).</p>

### Further Reading

There's plenty more to learn about Custom Inputs, Vue Components, and Vue in general. I recommend giving some of these resources a look-through.

- [Awesome-Vue's Component Sets](https://github.com/vuejs/awesome-vue#frameworks)  
Awesome-Vue is a huge list of Vue-related projects and resources, so feel free to peruse anything and everything on that list, but in particular I want to point out the UI Libraries and Component Sets because they pretty much all have examples of Checkboxes and Radios you can look at if you feel like diving into their source code.
- [Vue Curated](https://curated.vuejs.org/)  
This is a list similar to Awesome-Vue, but is more strictly curated so you know that everything on the list is worth taking a look at.
- [Vue Component Guide](https://vuejs.org/v2/guide/)  
The official Vue guide is a great place to learn the basics about anything related to Vue.
- [Vue API Documentation](https://vuejs.org/v2/api/)  
This documentation is where you get into the really deep details of Vue.

{{< signature "rb, vf, al, il" >}}
