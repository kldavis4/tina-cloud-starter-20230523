---
title: 'Useful React APIs For Building Flexible Components With TypeScript'
slug: react-apis-building-flexible-components-typescript
author: gaurav-khanna
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fbb65d7-6494-4494-9a78-099e178b83da/react-apis-building-flexible-components-typescript.jpg
date: 2021-10-12T12:00:00.000Z
summary: >-
  React with JSX is a fantastic tool for making easy-to-use components. Typescript components make it an absolute pleasure for developers to integrate your components into their apps and explore your APIs. Learn about three lesser-known React APIs that can take your components to the next level, and help you build even better React Components in this article.
description: >-
  React with JSX is a fantastic tool for making easy-to-use components. Typescript components make it an absolute pleasure for developers to integrate your components into their apps and explore your APIs. Learn about three lesser-known React APIs that can take your components to the next level, and help you build even better React Components in this article.
categories:
  - API
  - Tools
  - React
  - TypeScript
---

Have you ever used `React.createElement` directly? What about `React.cloneElement`? React is more than just transforming your JSX into HTML. Much more, and to help you level up your knowledge of lesser-known (but very useful) APIs the React library ships with. We’re going to go over a few of them and some of their use cases that can drastically enhance your components' integration and usefulness. 

In this article, we’ll go over a few useful React APIs that are not as commonly known but extremely useful for web developers. Readers should be experienced with React and JSX syntax, Typescript knowledge is helpful but not necessary. Readers will walk away with everything they need to know in order to greatly enhance React components when using them in React applications.

## `React.cloneElement`

Most developers may never have heard of `cloneElement` or ever used it. It was relatively recently introduced to replace the [now deprecated `cloneWithProps` function](https://reactjs.org/docs/react-api.html#cloneelement). `cloneElement` clones an element, it also lets you merge new props with the existing element, modifying them or overriding them as you see fit. This opens up extremely powerful options for building world-class APIs for functional components. Take a look at the signature.

<pre><code class="language-javascript">function cloneElement( element, props?, ...children)</code></pre>

Here’s the condensed Typescript version:

<pre><code class="language-javascript">function cloneElement( 
   element: ReactElement, 
   props?: HTMLAttributes, 
   ...children: ReactNode[]): ReactElement</code></pre>

You can take an element, modify it, even override its children, and then return it as a new element. Take a look at the following example. Let’s say we want to create a **TabBar** component of links. That might look something like this.

<pre><code class="language-javascript">export interface ITabbarProps {
  links: {title: string, url: string}[]
}
 
export default function Tabbar(props: ITabbarProps) {
 return (
   &lt;&gt;
     {props.links.map((e, i) =&gt;
       &lt;a key={i} href={e.url}&gt;{e.title}&lt;/a&gt;
     )}
   &lt;/&gt;
 )
}</code></pre>

The TabBar is a list of links, but we need a way to define two pieces of data, the title of the link, and the URL. So we’ll want a data structure passed in with this information. So our developer would make our component like so.

<pre><code class="language-javascript">function App() {
 return (
   &lt;Tabbar links={[
     {title: 'First', url: '/first'},
     {title: 'Second', url: '/second'}]
   } /&gt;
 )
}</code></pre>

This is great, but what if the user wants to render `button` elements instead of `a` elements? Well, we could add another property that tells the component what type of element to render. 

But you can see how this will quickly get unwieldy, we would need to support more and more properties to handle various use cases and edge cases for maximum flexibility. 

Here’s a better way, using `React.cloneElement`.

We’ll start by changing our interface to reference the `ReactNode` type. This is a generic type that encompasses anything React can render, typically JSX Elements but also can be strings and even `null`. This is useful for designating you to want to accept React components or JSX as arguments inline.

<pre><code class="language-javascript">export interface ITabbarProps {
 links: ReactNode[]
}</code></pre>

Now we’re asking the user to give us some React Elements, and we’ll render them how we want. 

<pre><code class="language-javascript">function Tabbar(props: ITabbarProps) {
 return (
   &lt;&gt;
     {props.links.map((e, i) =&gt;
       e // simply return the element itself
     )}
   &lt;/&gt;
 )
}</code></pre>

This is perfectly valid and would render our elements. But we’re forgetting a couple of things. For one, `key`! We want to add keys so React can render our lists efficiently. We also want to alter our elements to make necessary transformations so they fit into our styling, such as `className`, and so on.
 
We can do these with `React.cloneElement`, and another function `React.isValidElement` for checking the argument conforms to what we’re expecting!

{{% feature-panel %}}

## `React.isValidElement`

This function returns `true` if an element is a valid React Element and React can render it. Here’s an example of modifying the elements from the previous example.

<pre><code class="language-javascript">function Tabbar(props: ITabbarProps) {
 return (
   &lt;&gt;
     {props.links.map((e, i) =&gt;
       isValidElement(e) && cloneElement(e, {key: `${i}`, className: 'bold'})
     )}
   &lt;/&gt;
 )
}</code></pre>

Here we’re adding a key prop to each element we’re passing in and making every link bold at the same time! We can now accept arbitrary React Elements as props like so:

<pre><code class="language-javascript">function App() {
 return (
   &lt;Tabbar links={[
     &lt;a href='/first'&gt;First&lt;/a&gt;,
     &lt;button type='button'&gt;Second&lt;/button&gt;
   ]} /&gt;
 )
}</code></pre>

{{% pull-quote %}}
We can override any of the props set on an element, and easily accept various kinds of elements making our component much more flexible and easy to use.
{{% /pull-quote %}}

The advantage here is if we wanted to set a custom `onClick` handler to our button, we could do so. Accepting React elements themselves as arguments is a powerful way to give flexibility to your component design.

## `useState` Setter Function

Use Hooks! The `useState` hook is extremely useful and a fantastic API for quickly building state into your components like so: 

<pre><code class="language-javascript">const [myValue, setMyValue] = useState()</code></pre>

Due to the JavaScript runtime, it can have some hiccups. Remember closures?

In certain situations, a variable might not be the correct value because of the context it is in, such as in for-loops commonly or asynchronous events. This is because of lexical scoping. When a new function is created the lexical scope is preserved. Because there is no new function, the lexical scope of `newVal` is not preserved, and so the value is actually dereferenced by the time it is used. 

<pre><code class="language-javascript">setTimeout(() =&gt; {
 setMyValue(newVal) // this will not work
}, 1000)</code></pre>

What you’ll need to do is utilize the setter as a function. By creating a new function the variables reference is preserved in lexical scope and the currentVal is passed in by the React useState Hook itself.

<pre><code class="language-javascript">setTimeout(() =&gt; {
 setMyValue((currentVal) =&gt; {
   return newVal
 })
}, 1000)</code></pre>

This will ensure that your value is updated correctly because the setter function is called in the correct context. What React does here is call your function in the correct context for a React state update to occur. This can also be used in other situations where it’s helpful to act on the current value, React calls your function with the first argument as the current value.

**Note**: *For additional reading on the topic of async and closures, I recommend reading “[`useState` Lazy Initialization And Function Updates](https://kentcdodds.com/blog/use-state-lazy-initialization-and-function-updates)” by Kent C. Dodds.*

{{% ad-panel-leaderboard %}}

## JSX Inline Functions

Here’s a Codepen demo of a JSX inline function:

{{< codepen height="480" theme_id="light" slug_hash="QWgQQKR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Hello World in React](https://codepen.io/smashingmag/pen/QWgQQKR) by <a href="https://codepen.io/gvkhna">Gaurav Khanna</a>.{{< /codepen >}}

Not exactly a React API per-say.

{{% pull-quote %}}
JSX does support inline functions and it can be really useful for declaring simple logic with variables inline, as long as it returns a JSX Element.
{{% /pull-quote %}}

Here’s an example:

<pre><code class="language-javascript">function App() {
  return (
    &lt;&gt;
     {(() =&gt; {
       const darkMode = isDarkMode()
       if (darkMode) {
         return (
           &lt;div className='dark-mode'&gt;&lt;/div&gt;
         )
       } else {
         return (
           &lt;div className='light-mode'&gt;&lt;/div&gt;
         ) // we can declare JSX anywhere!
       }
      
     })()} // don't forget to call the function!
    &lt;/&gt;
  )
}</code></pre>

Here we’re declaring code inside of JSX, we can run arbitrary code and all we have to do is return a JSX function to be rendered. 

We can make it conditional, or simply perform some logic. Take note of the parentheses surrounding the inline function. Also particularly here where we are calling this function, we could even pass an argument into this function from the surrounding context if we wanted to!

<pre><code class="language-javascript">})()}</code></pre>

This can be useful in situations where you want to act on a collection data structure in a more complex way than a standard `.map` allows for inside of a JSX element.

<pre><code class="language-javascript">function App() {
  return (
    &lt;&gt;
      {(() =&gt; {
        let str = ''
        for (let i = 0; i &lt; 10; i++) {
          str += i
        }
        return (&lt;p&gt;{str}&lt;/p&gt;) 
      })()}
    &lt;/&gt;
  )
}</code></pre>

Here we can run some code to loop through a set of numbers and then display them inline. If you use a static site generator such as Gatsby, this step would be pre-computed as well.

{{% ad-panel-leaderboard %}}

## `component extends type`

Immensely useful for creating autocomplete-friendly components, this feature allows you to create components that extend existing `HTMLElements` or other components. Mostly useful for correctly typing an elements interface in Typescript but the actual application is the same for JavaScript.

Here’s a simple example, let’s say we want to override one or two properties of a `button` element, but still give developers the option to add other properties to the button. Such as setting `type='button'` or `type='submit'`. We obviously don’t want to recreate the entire button element, we just want to extend its existing properties, and maybe add one more prop. 

<pre><code class="language-javascript">import React, { ButtonHTMLAttributes } from 'react'</code></pre>

First we import React and the [`ButtonHTMLAttributes`](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/1349b640d4d07f40aa7c1c6931f18e3fbf667f3a/types/react/index.d.ts#L1957) class, a type that encompasses the props of a `HTMLButtonElement`. You can read the source code for this type of interface here: 

And you can see the React team has reimplemented all of the web’s APIs in TypeScript so can be type-checked.

Next, we declare our interface like so, adding our `status` property.

<pre><code class="language-javascript">interface ButtonProps extends ButtonHTMLAttributes&lt;HTMLButtonElement&gt; {
 status?: 'primary' | 'info' | 'danger'
}</code></pre>

And finally, we do a couple of things. We use ES6 destructuring to pull out the props that we care about (`status`, and `children`), and declare any other properties as `rest`. And in our JSX output, we return a button element, with ES6 structuring to add any additional properties to this element. 

<pre><code class="language-javascript">function Button(props: ButtonProps) {
 const { status, children, ...rest } = props // rest has any other props
 return (
   &lt;button
     className={`${status}`}
     {...rest} // we pass the rest of the props back into the element
   &gt;
     {children}
   &lt;/button&gt;
 )
}</code></pre>

So now a developer can add a `type` prop or any other prop that a button would typically have. We’ve given an additional prop that we’ve utilized in the `className` to set the style of the button.

Here’s the entire example:

<pre><code class="language-javascript">import React, { ButtonHTMLAttributes } from 'react'
 
export interface ButtonProps extends ButtonHTMLAttributes&lt;HTMLButtonElement&gt; {
 status?: 'primary' | 'info' | 'danger'
}
 
export default function Button(props: ButtonProps) {
 const { status, children, ...rest } = props
 return (
   &lt;button
     className={`${status}`}
     {...rest}
   &gt;
     {children}
   &lt;/button&gt;
 )
}</code></pre>

This makes for a great way of creating reusable internal components that conform to your style guidelines without rebuilding entire HTML elements! You can simply override entire props such as setting the `className` based on the status or allow for additional class names to be passed in as well.

<pre><code class="language-javascript">import React, { ButtonHTMLAttributes } from 'react'
 
export interface ButtonProps extends ButtonHTMLAttributes&lt;HTMLButtonElement&gt; {
 status?: 'primary' | 'info' | 'danger'
}
 
export default function Button(props: ButtonProps) {
 const { status, children, className, ...rest } = props
 return (
   &lt;button
     className={`${status || ''} ${className || ''}`}
     {...rest}
   &gt;
     {children}
   &lt;/button&gt;
 )
}</code></pre>

Here we take the prop `className` passed to our Button element, and insert it back in, with a safety check in the case of the prop being `undefined`. 

## Conclusion

React is an extremely powerful library, and there’s a good reason why it has quickly gained popularity. It gives you a great tool-set to build performant and easy-to-maintain web apps. It’s extremely flexible and yet very strict at the same time, which can be incredibly useful if you know how to use it. These are just a few APIs that are noteworthy and are largely overlooked. Give them a try in your next project!

For further reading about the latest React APIs, hooks, I would recommend reading [useHooks(🐠)](https://usehooks.com/). The [Typescript Cheatsheet](https://github.com/typescript-cheatsheets/react) also has some great information for React and Typescript Hooks.

{{< signature "ks, vf, yk, il" >}}
