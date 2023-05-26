---
title: 'Testing Vue Applications With The Vue Testing Library'
slug: vue-applications-vue-testing-library
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/649282cb-7e04-465e-aa15-ddc5f2eae960/vue-applications-vue-testing-library.png
date: 2020-11-24T10:30:00.000Z
summary: >-
  The Vue Testing library can help you to test your applications by mirroring the way that a user would interact with them. Here’s everything you need to know if you want to get started right away.
description: >-
  The Vue Testing library can help you to test your applications by mirroring the way that a user would interact with them. Here’s everything you need to know if you want to get started right away.
categories:
  - JavaScript
  - Vue
  - Coding
---

In this article, we will look at testing Vue applications using the Vue Testing Library &mdash; a lightweight library that emphasizes testing your front-end application from the user’s perspective.

The following assumptions are made throughout this article:

* The reader is familiar with Vue.
* The reader is familiar with testing application UI.

Conventionally, in Vue userland, when you want to test your application, you reach out for `@vue/test-utils` &mdash; the official testing library for Vue. `@vue/test-utils` provides APIs to test instances of rendered Vue components. Like so:

<pre><code class="language-javascript">// example.spec.js
import { shallowMount } from '@vue/test-utils'
import HelloWorld from '@/components/HelloWorld.vue'

describe('HelloWorld.vue', () =&gt; {
  it('renders props.msg when passed', () =&gt; {
    const msg = 'new message'
    const wrapper = shallowMount(HelloWorld, {
      propsData: { msg }
    })
    expect(wrapper.text()).toMatch(msg)
  })
})</code></pre>

You can see we are mounting an instance of the Vue component using the `shallowMount` function provided by `@vue/test-utils`.

The problem with the above approach to testing Vue applications is that the end-user will be interacting with the DOM and has no knowledge of how Vue renders the UI. Instead, he/she will be finding UI elements by text content, the label of the input element, and some other visual cues on the page. 

A better approach will be writing tests for your Vue applications in such a way that mirrors how an actual user will interact with it e.g looking for a button to increment the quantity of a product in a checkout page, hence Vue Testing Library.

{{% feature-panel %}}

## What Is Vue Testing Library?

Vue Testing Library is a lightweight testing library for Vue that provides lightweight utility functions on top of `@vue/test-utils`. It was created with a simple guiding principle:

> The more your tests resemble the way your software is used, the more confidence they can give you.  
&mdash; [testing-library.com](https://testing-library.com/docs/guiding-principles)

## Why Use Vue Testing Library

* You want to write tests that are not focused on implementation details i.e testing how the solution is implemented rather than if it produces the desired output.

* You want to write tests that focus on the actual DOM nodes and not rendered Vue components.

* You want to write tests that query the DOM in the same way a user would.

## How Vue Testing Library Works

Vue Testing Library functions by providing utilities for querying the DOM in the same way a user would interact with the DOM. These utilities allow you to find elements by their label text, find links and buttons from their text content and assert that your Vue application is fully accessible.

For cases where it doesn't make sense or is not practical to find elements by their text content or label, Vue testing Library provides a recommended way to find these elements by using `data-testid` attribute as an escape hatch for finding these elements.

The `data-testid` attribute is added to the HTML element you plan on querying for in your test. E.g

<pre><code class="language-html">&lt;button data-testid="checkoutButton"&gt;Check Out&lt;/button&gt;</code></pre>

{{% ad-panel-leaderboard %}} 

## Getting Started With Vue Testing Library

Now that you have seen why you should use Vue Testing Library and how it works, let's proceed by setting it up in a brand new Vue CLI generated Vue project. 

First, we will generate a new Vue application by running the below command in the terminal (assuming you have Vue CLI installed on your machine):

<pre><code class="language-javascript">vue create vue-testing-library-demo</code></pre>

To run our tests, we will be using [Jest](https://jestjs.io/) &mdash; a test runner developed by Facebook. Vue CLI has a plugin that easily sets up Jest. Let's add that plugin:

<pre><code class="language-javascript">vue add unit-jest</code></pre>

You will notice the plugin added a new script in package.json:

<pre><code class="language-javascript"> "test:unit": "vue-cli-service test:unit",</code></pre>

This would be used to run the tests. It also added a new tests folder in src and inside the tests folder a unit folder with an example test file called `example.spec.js`. Based on the configuration of Jest, when we run `npm run test:unit` Jest will look for files in `tests` directory and run the test files. Let's run the example test file:

<pre><code class="language-javascript">npm run test:unit</code></pre>

This should run the `example.spec.js` test file in `tests/unit` directory. Let's look at the content of this file:

<pre><code class="language-javascript">import { shallowMount } from '@vue/test-utils'
import HelloWorld from '@/components/HelloWorld.vue'

describe('HelloWorld.vue', () =&gt; {
  it('renders props.msg when passed', () =&gt; {
    const msg = 'new message'
    const wrapper = shallowMount(HelloWorld, {
      propsData: { msg }
    })
    expect(wrapper.text()).toMatch(msg)
  })
})</code></pre>

By default, installing Jest with the Vue CLI plugin will install `@vue/test-utils`, hence the above test file is using the `shallowMount` function from `@vue/test-utils`. A quick way to get familiar with Vue Testing Library is to quickly modify this same test file to use Vue Testing Library instead of `@vue/test-utils`. 

We would do this by first uninstalling `@vue/test-utils` as we won't be needing it.

<pre><code class="language-javascript">npm uninstall @vue/test-utils --save-dev</code></pre>

Then we install Vue Testing Library as a development dependency:

<pre><code class="language-javascript">npm install @testing-library/vue --save-dev</code></pre>

Then we proceed to modify `tests/unit/example.spec.js` to this:

<pre><code class="language-javascript">import { render } from '@testing-library/vue'
import HelloWorld from '@/components/HelloWorld.vue'

describe('HelloWorld.vue', () =&gt; {
  it('renders props.msg when passed', () =&gt; {
    const msg = 'new message'
    const { getByText } = render(HelloWorld, {
      props: { msg }
    })
    getByText(msg)
  })
})
</code></pre>

Run the test again and it should still pass. Let's look at what we did:

* We use the `render` function exposed by Vue Testing Library to render the `HelloWorld` components. `render` is the only way of rendering components in Vue Testing Library. When you call render, you pass in the Vue component and an optional `options` object. 

* We then use the options object to pass in the `msg` props needed by the `HelloWorld` component. `render` will return an object with helper methods to query the DOM and one of those methods is `getByText`. 

* We then use `getByText` to assert if an element with the text content of 'new message' exist in the DOM.

By now you might have noticed the shift from thinking about testing the rendered Vue component to what the user sees in the DOM. This shift will allow you test your applications from the user perspective as opposed to focusing more on the implementation details.

{{% ad-panel-leaderboard %}} 

## Our Demo App

Now that we have established how testing is done in Vue using Vue Testing Library, we will proceed to test our demo application. But first, we will flesh out the UI for the app. Our demo app is a simple checkout page for a product. We will be testing if the user can increment the quantity of the product before checkout, he/she can see the product name and price, and so on. Let’s get started.

First, create a new Vue component called checkout in `components/` directory and add the snippet below to it:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
    &lt;div class="checkout"&gt;
        &lt;h1&gt;{{ product.name }} - &lt;span data-testid="finalPrice"&gt;${{ product.price }}&lt;/span&gt;&lt;/h1&gt;
        &lt;div class="quantity-wrapper"&gt;
            &lt;div&gt;
                &lt;label for="quanity"&gt;Quantity&lt;/label&gt;
                &lt;input type="number" v-model="quantity" name="quantity" class="quantity-input" /&gt;
            &lt;/div&gt;
           &lt;div&gt;
                &lt;button @click="incrementQuantity" class="quantity-btn"&gt;+&lt;/button&gt;
                &lt;button @click="decrementQuantity" class="quantity-btn"&gt;-&lt;/button&gt;
           &lt;/div&gt;
        &lt;/div&gt;
          &lt;p&gt;final price - $&lt;span data-testId="finalPrice"&gt;{{ finalPrice }}&lt;/span&gt;&lt;/p&gt;
        &lt;button @click="checkout" class="checkout-btn"&gt;Checkout&lt;/button&gt;
    &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
export default {
    data() {
        return {
            quantity: 1,
        }
    },
    props: {
    product: {
        required: true
        }
    },
    computed: {
        finalPrice() {
            return this.product.price * this.quantity
        }
    },
    methods: {
        incrementQuantity() {
            this.quantity++;
        },
        decrementQuantity() {
            if (this.quantity == 1) return;
            this.quantity--;
        },
        checkout() {

        }
    }
}
&lt;/script&gt;

&lt;style scoped&gt;
.quantity-wrapper {
    margin: 2em auto;
    width: 50%;
    display: flex;
    justify-content: center;
}

.quantity-wrapper div {
    margin-right: 2em;
}
.quantity-input {
    margin-left: 0.5em;
}
.quantity-wrapper button {
    margin-right: 1em;
}
button {
    cursor: pointer;
}
&lt;/style&gt;
</code></pre>
</div>

Then modify `App.vue` to:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;check-out :product="product" /&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import CheckOut from './components/CheckOut.vue'

export default {
  name: 'App',
  data() {
     return {
          product: {
          name: 'Shure Mic SM7B',
          price: 200,
      }
    }
  },
  components: {
    CheckOut
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
  margin-top: 60px;
}
&lt;/style&gt;
</code></pre>

For our test case we will be testing the following scenarios:

1. Can the user see the product name?
2. Can the user see the product price?
3. Can the user increment product quantity?
4. Can the user decrement product quantity?
5. Can the user see the updated total price in real-time as the quantity changes?

Our UI is pretty minimalistic as the emphasis is on testing with Vue Testing Library. Let's proceed to test the Checkout component. Create a new test file in `tests/unit/` called `checkout.spec.js`.

We will then proceed to scaffold the test file:

<pre><code class="language-javascript">import { render, fireEvent } from '@testing-library/vue'
import CheckOut from '@/components/CheckOut.vue'

const product = {
    name: 'Korg Kronos',
    price: 1200
}
describe('Checkout.vue', () =&gt; {
  // tests goes here
})
</code></pre>

Our very first test case will be to check if the product name is rendered. We would do so like so:

<pre><code class="language-javascript"> it('renders product name', () =&gt; {
        const { getByText } = render(CheckOut, {
            props: { product }
        })

        getByText(product.name)
 })</code></pre>

Then we will check if the product price is rendered:

<pre><code class="language-javascript">it('renders product price', () =&gt; {
        const { getByText } = render(CheckOut, {
            props: { product }
        })

        getByText("$" + product.price)
 })</code></pre>

Going forward with testing the Checkout component, we will test if the initial quantity the user sees is 1 using the `getByDisplayValue` helper method:

<pre><code class="language-javascript">it('renders initial quantity as 1', () =&gt; {
        const { getByDisplayValue, getByText } = render(CheckOut, {
            props: { product }
        })
        getByDisplayValue(1)
    })</code></pre>

Next up, we will be checking if when the user clicks the button to increment product quantity, the quantity is incremented. We will do this by firing the click event using the `fireEvent` utility from Vue Testing Library. Here is the complete implementation:

<pre><code class="language-javascript">it('increments product quantity', async () =&gt; {
        const { getByDisplayValue, getByText } = render(CheckOut, {
            props: { product }
        })
        const incrementQuantityButton = getByText('+')
        await fireEvent.click(incrementQuantityButton)
        getByDisplayValue(2)
})</code></pre>

We will do the same for decrement when the quantity is 1 &mdash; in this case, we don't decrement the quantity. And also when the quantity is 2. Let's write both test cases.

<pre><code class="language-javascript">it('does not decrement quantity when quanty is 1', async () =&gt; {
        const { getByDisplayValue, getByText } = render(CheckOut, {
            props: { product }
        })
        const decrementQuantityButton = getByText('-')
        await fireEvent.click(decrementQuantityButton)
        getByDisplayValue(1)
    })

 it('decrement quantity when quantity greater than 1', async () =&gt; {
        const { getByDisplayValue, getByText } = render(CheckOut, {
            props: { product }
        })
        const incrementQuantityButton = getByText('+')
        const decrementQuantityButton = getByText('-')
        await fireEvent.click(incrementQuantityButton)
        await fireEvent.click(decrementQuantityButton)
        getByDisplayValue(1)
    })</code></pre>
    
Lastly, we will test if the final price is being calculated accordingly and displayed to the user when both the increment and decrement quantity buttons are clicked.

<div class="break-out">

<pre><code class="language-javascript">it('displays correct final price when increment button is clicked', async () =&gt; {
        const {  getByText, getByTestId } = render(CheckOut, {
            props: { product }
        })
        const incrementQuantityButton = getByText('+')
        await fireEvent.click(incrementQuantityButton)
        getByText(product.price * 2)
    })

it('displays correct final price when decrement button is clicked', async () =&gt; {
        const {  getByText} = render(CheckOut, {
            props: { product }
        })
        const incrementQuantityButton = getByText('+')
        const decrementQuantityButton = getByText('-')
        await fireEvent.click(incrementQuantityButton)
        await fireEvent.click(decrementQuantityButton)
        getByText(product.price)
    })</code></pre>
</div>

All throughout our test cases, you will notice that we were more focused on writing our tests from the perspective of what the user will see and interact with. Writing tests this way ensures that we are testing what matters to the users of the application.

## Conclusion

This article introduces an alternative library and approach for testing Vue applications called Vue Testing Library, we see how to set it up and write tests for Vue components with it.

### Resources

* [Introduction to Vue Testing Library](https://testing-library.com/docs/vue-testing-library/intro/)
* [Introduction to Testing Library](https://testing-library.com/docs/)
* [Guiding Principles](https://testing-library.com/docs/guiding-principles)
* [API](https://testing-library.com/docs/vue-testing-library/api)

You can find the [demo project](https://github.com/DominusKelvin/vue-testing-library-demo) on GitHub.

{{< signature "ra, yk, il" >}}
