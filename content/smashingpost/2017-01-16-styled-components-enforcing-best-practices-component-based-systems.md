---
title: 'Styled Components: Enforcing Best Practices In Component-Based Systems'
slug: styled-components-enforcing-best-practices-component-based-systems
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bd504a1-9377-4289-a293-8759a459a845/code-atom-500w-opt.png
date: 2017-01-16T20:12:25.000Z
author: maxstoiber
description: >-
  The rise of JavaScript
  frameworks such as React, Ember and recently Angular 2, the effort of the W3C
  to standardize a web-native component system, pattern libraries and style
  guides being considered the "right way" to build web applications, and many
  other things have illuminated this revolution.
categories:
  - Coding
  - JavaScript
  - Web Components
---
After this shift in mindset towards building component-based user interfaces, we are now in what we like to call the "component age." The rise of JavaScript frameworks such as <a href="https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/">React</a>, <a href="https://www.smashingmagazine.com/2013/11/an-in-depth-introduction-to-ember-js/">Ember</a> and recently Angular 2, the effort of the W3C to standardize a web-native component system, pattern libraries and style guides being considered the "right way" to build web applications, and many other things have illuminated this revolution.</p>

<figure><a href="https://styled-components.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/499aa095-99d8-4397-beb5-96e6a1d7b36e/code-atom-preview-opt.png" alt="Styled Components - A screenshot of styled-components code" width="780" height="428" /></a><figcaption>A <code>Button</code> React component written with styled components. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d86b726-eb63-4457-9b10-68bba172460f/code-atom-opt.png">View large version</a>)</figcaption></figure>

## Best Practices In Component-Based Systems

As we've built more and more apps with components, we've discovered some best practices when working with them. I want to talk about three main ones today: building small, focused and independent components; splitting container and presentational components; and having single-use CSS class names.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Styling Web Components Using A Shared Style Sheet](https://www.smashingmagazine.com/2016/12/styling-web-components-using-a-shared-style-sheet/)
*   [A Glimpse Into The Future With React Native For Web](https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/)
*   [Finally, CSS In JavaScript! Meet CSSX](https://www.smashingmagazine.com/2016/04/finally-css-javascript-meet-cssx/)

### Build-Small Components

Instead of relying on classes for composition, use components to your advantage and compose them together. For example, imagine a <code>Button</code> component that renders <code class="language-markup">&lt;button class="btn"&gt;</code> to the DOM. One could also render a bigger, more important button. Making a bigger button would be as easy as attaching the <code>btn--primary</code> class in the DOM: <code class="language-markup">&lt;button class="btn btn--primary"&gt;</code>.

Instead of forcing users of the component to know which particular class to attach, the <code>Button</code> component should have a <code>primary</code> property. Making a primary button would be as easy as <code class="language-markup">&lt;Button primary /&gt;</code>! Here is how we could implement this:

<pre><code class="language-javascript">// Button.js

function Button(props) {
  const className = `btn${props.primary ? ' btn—-primary' : ''}`
  return (
    &lt;button className={className}&gt;{props.children}&lt;/button&gt;
  );
}
</code></pre>

Now, users no longer need to know which particular class it applies; they just render a primary button. What happens when the <code>primary</code> property is set is an <strong>implementation detail</strong> of the component. Changing the styling, classes or behavior of the button now requires editing only a single file where the component is created, instead of hundreds of files where it is used.</p>

### Split Container and Presentational Components

With React, some of your components may have state associated with them. Try to split components that handle data and/or logic (for example, data formatting) from components that handle styling. By separating these two concerns, reasoning about changes in your code base will be a lot easier.

If the back-end API format has to change, all you have to do is go into your container components and make sure you render the same presentational components as before, even with the new format, and everything will work perfectly fine.

On the other hand, if the visual design or user experiences of your app have to change, all you have to do is go into your presentational components and make sure they look correct on their own. Because these components don't care about when and where they're rendered, and you haven't changed which components get rendered, everything will work perfectly fine.

By separating these two types of components, you avoid doing multiple unrelated changes at the same time, thus avoiding accidental errors.</p>

### Have Single-Use Class Names

Going back to our <code>Button</code> component, it has a <code>.btn</code> class. Changing the styles of that class should not affect anything except the <code>Button</code>. If changing the <code>background-color</code> in my <code>.btn</code> class messes up the layout of the header and gives the footer two columns instead of three, then something is wrong. That violates the entire premise of having independent components.

This essentially boils down to using every class in your CSS only once (outside of "mixins" like <code>.clearfix</code>). This way, bugs like the one above can never happen.

The problem, as always, is us humans. Ever encountered a bug in a program? It was only there because a human put it there. If programs could exist without humans, then bugs would not be a thing. Human error accounts for every single bug you've ever found and squashed.

There is a <a href="https://twitter.com/thomasfuchs/status/493790680397803521">famous joke</a> in the front-end development world:
<blockquote>Two CSS properties walk into a bar. A barstool in an entirely different bar falls over.</blockquote>

The reception and repetition this joke has gotten tells you how many developers have seen this type of bug before. It happens, especially in teams, no matter how hard you try to avoid it.

With that and a few other things in mind, <a href="https://twitter.com/glenmaddern">Glen Maddern</a> and I sat down and started thinking about styling in this new era. We didn't want to reinvent or get rid of CSS; it's a language that's made for styling and that browsers natively support. Let's instead take the best parts of CSS and make human error in component-based systems almost impossible.</p>

## Enforcing Best Practices

The basic idea of styled components is to enforce best practices by <strong>removing the mapping between styles and components</strong>. If you think about any styling method you've used, there is always a mapping between a style fragment and your HTML.

With standard CSS, this would be a class name (or maybe an ID). With styles in JavaScript libraries in React, it's either setting a class from a variable or passing a JavaScript object to the <code>style</code> property.

Because we want to use each class only once, what if we just removed that mapping?

As it turns out, by doing so, we also enforce the split between container and presentational components, and we make sure that developers can only build small and focused components.

Another interesting feature of styled components is that it allows you to write <strong>actual CSS</strong> in your JavaScript (not just CSS-as-JavaScript objects). It leverages an infrequently used feature of ECMAScript 2015 (the new version of the JavaScript standard), called tagged template literals, to make that work a pleasant experience for the developer.</p>

## The Basics

Now, you might be wondering what that looks like. Well, let's take a look!

<div class="break-out">

<pre><code class="language-javascript">const Title = styled.h1`
  color: palevioletred;
  font-size: 1.5em;
  text-align: center;
`;</code>
</pre></div>

You can now use this React component like any other:

<div class="break-out">

<pre><code class="language-markup">&lt;Wrapper&gt;
  &lt;Title&gt;Hello World, this is my first styled component!&lt;/Title&gt;
&lt;/Wrapper&gt;</code></pre></div>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b61ba3b-2b87-4b84-a454-5e08efdefc70/hello-world-preview-opt.png" alt="A screenshot showing the text 'Hello World, this is my first styled component!' in palevioletred and centered on a papayawhip background." width="780" height="252" /></a><figcaption>This is what the component above looks like in the browser. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9645851-1e7c-45f7-8180-64fff4ab4d4f/hello-world-opt.png">View large version</a>)</figcaption></figure>

Quite a few things are going on here, so let's dissect this code snippet.</p>

<code>styled.h1</code> is a function that, when called, returns a React component that renders an <code>&lt;h1&gt;</code> into the DOM. If you're wondering, "Where do we call that function? I see only backticks, no parentheses!" that's exactly where the ECMAScript 2015 features come into play.

What you're seeing above is a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals"><strong>tagged template literal</strong></a>, which is a new feature of JavaScript the language. (No special tooling is needed to use styled-components.) You can call functions with backticks (like <code>styled.h1``</code>), and they will receive the string passed in as the first argument. As we go along, you'll see how this differs from calling functions normally with parentheses, but let's leave it at this for now.

So, this <code>styled.h1</code> call returns a React component. This React component has a class attached to it that styled components automatically generates and uniquifies. This class name has the styles associated with it that you pass to the template literal.

Summed up, this means that the <code>styled.h1</code> call returns a React component that has the styles applied that you pass to the template literal.</p>

### Full CSS Support

Because styled-components is just CSS, it supports all of CSS perfectly fine. Media queries, pseudo-selectors, even nesting just work. We are generating a class name and injecting the CSS into the DOM; so, whatever works in CSS works with styled-components, too.</p>

<div class="break-out">

<pre><code class="language-javascript">const Input = styled.input`
  font-size: 1.25em;
  border: none;
  background: papayawhip;
  /* ...more styles here... */

  &amp;:hover {
    box-shadow: inset 1px 1px 2px rgba(0,0,0,0.1);
  }

  @media (min-width: 650px) {
    font-size: 1.5em;
  }
`;</code></pre></div>

This <code>Input</code> component will now have nice hover styles and will resize itself to be a bit bigger on large screens. Let's see what one of these inputs looks like with and without a placeholder:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/056e0514-6f2c-4640-9c07-1346f341e909/input-preview-opt.png" alt="One input without any content showing the placeholder, and one with some content" width="780" height="119" /></a><figcaption>This is what the component above looks like in the browser. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c9dc82-a7c3-43a2-9e47-3258136dc4bb/input-opt.png">View large version</a>)</figcaption></figure>

As you can see, making a container component that has styling or making a presentational component that has logic is impossible. We are also building a lot of small components and combining them into bigger containers, and because there are no visible classes, we cannot use them more than once.

Essentially, by using styled-components, we have to build a good component system — there is no other way. It enforces the best practices for us — no special architectural code review needed.</p>

## Wrapping Up

Styled components offers a lot more great features, such as built-in theming and full React Native support. I encourage you to dive into <a href="https://github.com/styled-components/styled-components">the documentation</a> and try it out on one of your projects. Not having to worry about best practices makes the development experience so much better and quicker. I'm obviously very biased, but I don't ever want to go back to another way of styling React apps.

Here are a few miscellaneous links related to styles in JavaScript that aren't specific to styled components but that talk about the topic more generally:

*   "[React JS Style Components](https://www.youtube.com/watch?v=gNeavlJ7lNY)" (video), Michael Chan, Full Stack Talks An amazing talk about leveraging components as a styling construct. If you're using React and haven't heard this talk yet, stop what you're doing and watch it right now.
*   "[The magic behind ?  styled-components](https://mxstbr.blog/2016/11/styled-components-magic-explained/)", Max Stoiber This article by yours truly dives deep into tagged template literals, how they work and why they are super useful, based on the example of styled-components.
*   "[The Future of Reusable CSS](https://www.youtube.com/watch?v=XR6eM_5pAb0)" (video), Glen Maddern, ColdFront16 This talk by styled-components' cocreator doesn't talk about the library itself, but explains how theming component-based systems _should_ work. A lot of these ideas have made their way into the library.
*   "[Rendering Khan Academy's Learn Menu Wherever I Please](https://medium.com/@jdan/rendering-khan-academys-learn-menu-wherever-i-please-4b58d4a9432d#.w9nshye05)," Jordan Scales A great article that documents the move of a complex code base from a Handlebars and LESS combo to React and styles in JavaScript. Highly recommended if you're not sure whether either React or Styles in JavaScript are for you.

{{< signature "rb, vf, il, yk, al" >}}

