---
title: 'Taming <code>this</code> In JavaScript With Bind Operator'
slug: taming-this-javascript-bind-operator
author: willian-martins
image: >-
  https://res.cloudinary.com/indysigner/image/upload/v1538741952/taming-this-_javascript-bind_operator_xqzknr.png
date: 2018-10-05T14:20:22+02:00
summary: >-
  Dealing with <code>this</code> in JavaScript can be tricky. But what if instead of fight against it we could leverage on it to achieve nice stuff like function composition with virtual methods? This is what we are going to explore in this article about one of the potential upcoming JavaScript features: The Bind Operator.
description: >-
  Dealing with <code>this</code> in JavaScript can be tricky. But what if instead of fight against it we could leverage on it to achieve nice stuff like function composition with virtual methods? This is what we are going to explore in this article about one of the potential upcoming JavaScript features: The Bind Operator.
categories:
  - JavaScript
---
<p>Do you want to discover the next exciting JavaScript features that you didn’t even know you needed? In this article, I will introduce one of these proposals that if accepted may change the way you write code the same way the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax">spread operator</a> did.</p>

<p>However, here’s a small disclaimer: <strong>This feature is under development and discussion</strong>. The goal here is to add some hype around it and create awareness of the hard work that TC39 is doing to find consensus, fix all the syntax and semantics issues and have it shipped with the next releases of ECMAScript. If you have any concerns, comments or desire to express your support, please go to the <a href="https://github.com/tc39/proposals">TC39 proposals repository</a>, add a star to this feature to show your support, open an issue to voice your concerns and get involved.</p>

<p>But before, I want to ask a simple (but tricky) question:</p>

<p>What <em>is</em> <code>this</code>?</p>

<p>In ECMAScript, <code>this</code> has a different semantic than <code>this</code> in many other programming languages, where <code>this</code> often refers to the lexical scope. In general, this behaves differently in the global scope, within a function, in non-strict mode and strict mode. Let’s break this behavior down into small examples.</p>

{{% feature-panel %}}

## <code>this</code> In The Global Scope

<p>What is the value of <code>this</code> in this example?</p>

<pre><code class="language-javascript">console.info(this);</code></pre>

<p>At the global scope, <code>this</code> refers to the global object, like the <strong>window</strong> in the browser, <strong>self</strong> on web workers and the <strong>module.exports</strong> object in NodeJS.</p>

## <code>this</code> In The Function Scope

<p>At the function scope, <code>this</code> behaves depending on how the function is called, and this aspect makes it tricky to predict its value. We can understand it better by checking the following examples:</p>

### What Is The Value Of <code>this</code> Here?

<pre><code class="language-javascript">function foo() {
  return this;
}

console.info(this);
</code></pre>

<p>Inside a function, <code>this</code> starts to have an interesting behavior since its value depends on how the function is called. In the example above, <code>this</code> still refers to the global scope, with one difference. In NodeJs, this will point to the global object instead of <code>module.exports</code>.</p>

### Setting A Value Into <code>this</code>:

<pre><code class="language-javascript">function foo() {
  this.bar = 'baz';
  return this;
}

console.info(foo());
console.info(new foo());
</code></pre>

<p>Setting a value into <code>this</code> sets the value into the current context. The example above logs the global scope with the property <code>bar</code> with the value <code>baz</code> in the first <code>console.info</code>, but it logs only <code>{ bar: ‘baz’ }</code> in the second <code>console.info</code>. It happens because the <code>new</code> operator among other things bounds the value of <code>this</code> to the newly created object.</p>

## This Keyword In The Strict Mode

<p>In strict mode, the <code>this</code> variable doesn’t carry the value of the context implicitly, this means if its context isn’t set, the value of this is default to <code>undefined</code> as shown in the following snippet.</p>

<pre><code class="language-javascript">function foo() {
  "use strict";
  return this;
}

console.info(foo()); //undefined
</code></pre>

<p>To set the context of <code>this</code> in strict mode you can set the function as member of an object, use <code>new</code> operator, <code>Function.prototype.call()</code>, <code>Function.prototype.apply()</code> or <code>Function.prototype.bind()</code> methods for example.</p>

<pre><code class="language-javascript">function foo() {
  "use strict";
  return this;
}

var a = { foo };

foo(); // undefined
a.foo(); // { foo: ƒunction }
new foo(); // Object foo {}
foo.call(this); // Window / Global Object
foo.apply(this); // Window / Global Object
foo.bind(this)(); // Window / Global Object
</code></pre>

## Making <code>this</code> Variable Predictable

<p>At this point, you may realize that the value of <code>this</code> in ECMAScript is quite tricky to predict. To demonstrate the available techniques to make it predictable, I’d like to present the following example that mimics a common use case of <code>this</code>.</p>

<pre><code class="language-javascript">&lt;button id="button">🐱 🐾&lt;/button>
&lt;script>
  class MeowctComponent {
    constructor() {
      this.paw = document.getElementById('button');
    }

    meow() {
      console.info('🐱 on this: ', this.paw);
    }
  }

  const cat = new MeowctComponent();
  cat.paw.addEventListener('click', cat.meow);
&lt;/script>
</code></pre>

<p>In the example above, I created a <code>MeowctComponent</code>, which has only one property <code>paw</code> that points to the button element and one method called <code>meow</code> that should print the paw instance property into the console.</p>

<p>The tricky part is that the meow method is executed only when the button is clicked, and because of that, <code>this</code> has the button tag as context, and since the button tag does not have any paw property, it logs the <strong>undefined</strong> value into the console. Tricky, isn’t it?</p>

<p>To fix this specific behavior we can leverage on the <code>Function.prototype.bind()</code> method to explicitly bind this to the cat instance, like in the following example:</p>

<pre><code class="language-javascript">&lt;button id="button">Meow&lt;/button>
&lt;script>
  class MeowctComponent {
    constructor() {
      this.paw = document.getElementById('button');
    }

    meow() {
      console.info('🐱 on this: ', this.paw);
    }
  }

  const cat = new MeowctComponent();
  cat.paw.addEventListener('click', cat.meow.bind(cat));
&lt;/script>
</code></pre>

<p>The method <code>.bind()</code> returns a new permanently bound function to the first given parameter, which is the context. Now, because we bound the <code>cat.meow</code> method to the <code>cat</code> instance, <code>this.paw</code> inside the meow method correctly points to the <em>button element</em>.</p>

<p>As an alternative to the <code>Function.prototype.bind()</code> method, we can use the arrow function to achieve the same result. It keeps the value of the lexical <code>this</code> of the surrounding context and dispenses the need to bind the context explicitly, like in the next example:</p>

<pre><code class="language-javascript">&lt;button id="button">🐱 Meow&lt;/button>
&lt;script>
  class MeowctComponent {
    constructor() {
      this.paw = document.getElementById('button');
    }

    meow() {
      console.info('🐱 on this: ', this.paw);
    }
  }

  const cat = new MeowctComponent();
  cat.paw.addEventListener('click', () => cat.meow());
&lt;/script>
</code></pre>

<p>Although arrow functions solve the majority of use cases where we need to bind the lexical <code>this</code> explicitly, we still have two use cases for which the use of the explicit bind is needed.</p>

### Calling A Known Function Using <code>this</code> To Provide Context:

<pre><code class="language-javascript">let hasOwnProp = Object.prototype.hasOwnProperty;
let obj = Object.create(null);

obj.hasOwnProperty('x') // Type Error...

hasOwnProp.call(obj, "x"); //false

obj.x = 100;

hasOwnProp.call(obj, "x"); // true
</code></pre>

<p>Let's suppose for any reason we have this <code>obj</code> object that doesn't extend <code>Object.prototype</code> but we need to check if <code>obj</code> has an <code>x</code> property by using the <code>hasOwnProperty</code> method from <code>Object.prototype</code>. To achieve that, we have to use the call method and explicitly pass <code>obj</code> as the first parameter to make it work as expected, which appears not to be so idiomatic.</p>

{{% ad-panel-leaderboard %}}

### Extracting A Method

<p>The second case can be spotted when we need to extract a method from an object like in our <code>MeowctComponent</code> example:</p>

<pre><code class="language-javascript">&lt;button id="button">🐱 🐾&lt;/button>
&lt;script>
  class MeowctComponent {
    constructor() {
      this.paw = document.getElementById('button');
    }

    meow() {
      console.info('🐱 on this: ', this.paw);
    }
  }

  const cat = new MeowctComponent();
  cat.paw.addEventListener('click', cat.meow.bind(cat));
&lt;/script>
</code></pre>

<p>These use cases are the baseline problem that the bind operator tries to solve.</p>

## The Bind Operator <code>::</code>

<p>The <strong>Bind operator</strong> consists of an introduction of a new operator <code>::</code> (double colon), which acts as syntax sugar for the previous two use cases. It comes in two formats: <strong>binary</strong> and <strong>unary</strong>.</p>

<p>In its binary form, the bind operator creates a function with its left side is bound to <code>this</code> of the right side, like in the following example:</p>

<pre><code class="language-javascript">let hasOwnProp = Object.prototype.hasOwnProperty;
let obj = Object.create(null);

obj.hasOwnProperty('x') // Type Error...

obj::hasOwnProp("x"); //false

obj.x = 100;

obj::hasOwnProp("x"); // true
</code></pre>

<p>That looks more natural, doesn’t it?</p>

<p>In its unary form, the operator creates a function bound to the base of the provided reference as a value for <code>this</code> variable, like in the following example:</p>

<pre><code class="language-javascript">...
cat.paw.addEventListener('click', ::cat.meow);
// which desugars to
cat.paw.addEventListener('click', cat.meow.bind(cat));
...
</code></pre>

<p>What’s so cool about the bind operator is the fact that it opens up new opportunities for creating virtual methods, as in this example of lib for iterable.</p>

<pre><code class="language-javascript">import { map, takeWhile, forEach } from "iterlib";

getPlayers()
  ::map(x => x.character())
  ::takeWhile(x => x.strength > 100)
  ::forEach(x => console.log(x));
</code></pre>

<p>It’s super useful because the developer doesn’t need to download the whole lib to do small stuff, which reduces the amount of imported JavaScript. Besides, it makes those kinds of libs easier to extend.</p>

## How To Develop Using Bind Operator

<p>To keep the example simple, let’s suppose we need to create a math module which the developer can chain the operations to form an math expression that, given a number as an entry it could make all calculations into a pipeline. The code to achieve this is simple and could be written as the following.</p>

<pre><code class="language-javascript">function plus(x) {
  return this + x;
}

function minus(x) {
  return this - x;
}

function times(x) {
  return this * x;
}

function div(x) {
  return this / x;
}
</code></pre>

<p>As you can spot in the example above, we expect to have the value as a context and we use this to make the calculation, so then using the bind operator, we could make an expression like the following:</p>

<pre><code class="language-javascript">1::plus(2)::times(4)::div(3)::minus(1); // returns 3
</code></pre>

<p>Which is equivalent to:</p>

<pre><code class="language-javascript">minus.call(div.call(times.call(plus.call(1, 2), 4), 3), 1);
</code></pre>

<p>The first snippet looks more idiomatic, isn’t?</p>

<p>Going a little further, we can use it to convert a temperature from Celsius to Fahrenheit, this can be accomplished by the following function expression:</p>

<pre><code class="language-javascript">const toFahrenheit = x => x::times(9)::div(5)::plus(32);
console.info(toFahrenheit(20)); // 68
</code></pre>

<p>So far, we demonstrate how create functions to interact with the values, but what about extending the object with virtual methods? We can do new stream compositions mixing built-in methods with custom ones. To demonstrate it, we can compose string methods with custom ones. First, let's check the module with the custom methods with its implementation.</p>

<pre><code class="language-javascript">function capitalize() {
  return this.replace(/(?:^|\s)\S/g, a => a.toUpperCase());
}

function doubleSay() {
  return `${this} ${this}`;
}

function exclamation() {
  return `${this}!`;
}
</code></pre>

<p>With this module in place we can do cool things like the following:</p>

<pre><code class="language-javascript">const { trim, padEnd } = String.prototype;

console.info(
  '   hello world   '
    ::trim()
    ::capitalize()
    ::doubleSay()
    ::exclamation()
    ::padEnd(30)
);

// "Hello World Hello World!      "
</code></pre>

<p>In the example above, you can spot that I extracted two methods from the <code>String.prototype</code>, <code>trim()</code> and <code>padEnd()</code>. Since these methods are extracted, I can use them to compose my stream of methods alongside with my virtual methods <code>capitalize()</code>, <code>doubleSay()</code> and <code>exclamation()</code>. This aspect is what makes bind operator so exciting and promising.</p>

{{% ad-panel-leaderboard %}}

## Advantages And Disadvantages Of Bind Operator

<p>As you may realize at this point, there are some aspects that Bind Operator shines. Those are the following:</p>

<ul>
<li>It covers the only two missing use cases that explicit bind is necessary;</li>
<li>It makes easy to make <code>this</code> variable to be predictable;</li>
<li>It adds a new way to extend functionality by using virtual methods;</li>
<li>It helps to extend built-in objects without extending the prototype chain. Do you remember <a href="https://developers.google.com/web/updates/2018/03/smooshgate">Smoosh Gate</a>?</li>
</ul>

<p>In the other side, to compose functions with bind operator you need to rely on this to be bound, that can lead to some issues like in this example:</p>

<pre><code class="language-javascript">const plus = (x) => this + x;

console.info(1::plus(1));
// "[object Window]1"
</code></pre>

<p>As it becomes clear in the example above, it’s not possible to compose arrow function with bind operator, since it’s not possible to bind <code>this</code> to an arrow function. Sometimes users don’t want to rely on <code>this</code> to be bound to compose their behavior through a function chain, which could be a problem if you only use bind operator to achieve this.</p>

<p>Another issue that is often said is the possible syntax overload that the bind operator can bring which can be a problem to onboard newcomers to the language. Realizing that a specific operator works in binary and unary form is tricky as well. One possible solution for this is to introduce the binary form to the language separately of the unary form. So once the binary form is integrated to the language, the committee can reassess if the unary form is still necessary. Meanwhile, users can get used to the binary form, and the syntax overload could potentially be mitigated.</p>

## Conclusion

<p>Predict the value of <code>this</code> in JavaScript is trick. The language has some rules to explain how the context is assigned to this, but in the daily basis we want to make this value predictable. The <code>Function.prototype.bind()</code> method and arrow functions help us to make the value of <code>this</code> predictable. The <strong>bind operator</strong> comes to play to cover the two use cases that we still need to explicitly bind <code>this</code>.</p>

<p>The advent of bind operator opens an opportunity to create a new set of function composition via virtual methods, but it can add a syntax overload making difficult to onboard newcomers to the language.</p>

<p>The author of the bind operator is Kevin Smith, and <a href="https://github.com/tc39/proposal-bind-operator">this proposal is in Stage 0</a>. The TC39 is open to feedback. If you like this feature and think that it’s useful, please add a star in the repository, if you have an Idea to solve the issues presented here, if you have another way to shape the syntax or semantics of this features or if you spot another issue with it, please open an issue in the repo and share your thoughts/ideas with the committee.</p>

{{< signature "dm, ra, yk, il" >}}