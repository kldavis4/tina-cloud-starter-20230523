---
title: 'How To Use Styled-Components In React'
slug: styled-components-react
author: adebiyi-adedotun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af37862f-c811-4e56-a9b9-96116da63a2b/styled-components-react.png
date: 2020-07-23T10:30:00.000Z
summary: >-
  While the component-driven approach has ushered in a new frontier in the way we build web applications, it isn’t without its imperfections &mdash; one being its usability and scalability with CSS. This has given birth to a new way to construct and manage our styles in a **component-specific** manner, otherwise knows as CSS-in-JS.
description: >-
  While the component-driven approach has ushered in a new frontier in the way we build web applications, it isn’t without its imperfections &mdash; one being its usability and scalability with CSS. This has given birth to a new way to construct and manage our styles in a **component-specific** manner, otherwise knows as CSS-in-JS.
categories:
  - CSS
  - React
  - CSS-in-JS
  - JavaScript
  - Tools
---

Styled components are a CSS-in-JS tool that bridges the gap between components and styling, offering numerous features to get you up and running in styling components in a functional and reusable way. In this article, you’ll learn the basics of styled components and how to properly apply them to your React applications. You should have worked on React previously before going through this tutorial. If you’re looking for various options in styling React components, you can check out our [previous post on the subject](https://www.smashingmagazine.com/2020/05/styling-components-react/).

At the core of CSS is the capability to target any HTML element &mdash; globally &mdash; no matter its position in the DOM tree. This can be a hindrance when used with components, because components demand, to a reasonable extent, colocation (i.e. keeping assets such as states and styling) closer to where they’re used (known as localization).

In React’s own words, styled components are “**visual primitives for components**”, and their goal is to give us a flexible way to style components. The result is a tight coupling between components and their styles.

Note: Styled components are available both for React and React Native, and while you should definitely check out the React Native guide, our focus here will be on styled components for React.

{{% feature-panel %}}

## Why Styled Components?

Apart from helping you to scope styles, styled components include the following features:

- **Automatic vendor prefixing**    
You can use standard CSS properties, and styled components will add vendor prefixes should they be needed.
- **Unique class names**    
Styled components are independent of each other, and you do not have to worry about their names because the library handles that for you.
- **Elimination of dead styles**    
Styled components remove unused styles, even if they’re declared in your code.
- and [many more](https://styled-components.com/docs/basics#motivation).

## Installation

Installing styled components is easy. You can do it through a [CDN](https://styled-components.com/docs/basics#installation) or with a package manager such as Yarn…

<pre><code class="language-bash">yarn add styled-components</code></pre>

… or npm:

<pre><code class="language-bash">npm i styled-components</code></pre>

Our demo uses [create-react-app](https://create-react-app.dev/).

## Starting Out

Perhaps the first thing you’ll notice about styled components is their syntax, which can be daunting if you don’t understand the [magic behind styled components](https://mxstbr.blog/2016/11/styled-components-magic-explained/). To put it briefly, styled components use JavaScript’s [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) to bridge the gap between components and styles. So, when you create a styled component, what you’re actually creating is a React component with styles. It looks like this:

<pre><code class="language-javascript">import styled from "styled-components";

// Styled component named StyledButton
const StyledButton = styled.button`
  background-color: black;
  font-size: 32px;
  color: white;
`;

function Component() {
  // Use it like any other component.
  return &lt;StyledButton&gt; Login &lt;/StyledButton&gt;;
}</code></pre>

Here, `StyledButton` is the styled component, and it will be rendered as an HTML button with the contained styles. `styled` is an internal utility method that transforms the styling from JavaScript into actual CSS.

In raw HTML and CSS, we would have this:

<pre><code class="language-css">button {
  background-color: black;
  font-size: 32px;
  color: white;
}

&lt;button&gt; Login &lt;/button&gt;</code></pre>

If styled components are React components, can we use props? Yes, we can.

## Adapting Based on Props

Styled components are **functional**, so we can easily style elements dynamically. Let’s assume we have two types of buttons on our page, one with a black background, and the other blue. We do not have to create two styled components for them; we can adapt their styling based on their props.

<div class="break-out">

<pre><code class="language-css">import styled from "styled-components";

const StyledButton = styled.button`
  min-width: 200px;
  border: none;
  font-size: 18px;
  padding: 7px 10px;
  /* The resulting background color will be based on the bg props. */
  background-color: ${props =&gt; props.bg === "black" ? "black" : "blue";
`;

function Profile() {
  return (
    &lt;div&gt;
      &lt;StyledButton bg="black"&gt;Button A&lt;/StyledButton&gt;
      &lt;StyledButton bg="blue"&gt;Button B&lt;/StyledButton&gt;
    &lt;/div&gt;
  )
}</code></pre>
</div>

Because `StyledButton` is a React component that accepts props, we can assign a different background color based on the existence or value of the `bg` prop.

You’ll notice, though, that we haven’t given our button a `type`. Let’s do that:

<div class="break-out">

<pre><code class="language-css">function Profile() {
  return (
    &lt;&gt;
      &lt;StyledButton bg="black" type="button"&gt;
        Button A
      &lt;/StyledButton&gt;
      &lt;StyledButton bg="blue" type="submit" onClick={() =&gt; alert("clicked")}&gt;
        Button B
      &lt;/StyledButton&gt;
    &lt;/&gt;
  );
}</code></pre>
</div>

Styled components can differentiate between the [types of props](https://styled-components.com/docs/basics#passed-props) they receive. They know that `type` is an HTML attribute, so they actually render `<button type="button">Button A</button>`, while using the `bg` prop in their own processing. Notice how we attached an event handler, too?

Speaking of attributes, an extended syntax lets us manage props using the [`attrs` constructor](https://styled-components.com/docs/api#attrs). Check this out:

<pre><code class="language-javascript">const StyledContainer = styled.section.attrs((props) =&gt; ({
  width: props.width || "100%",
  hasPadding: props.hasPadding || false,
}))`
  --container-padding: 20px;
  width: ${(props) =&gt; props.width}; // Falls back to 100%
  padding: ${(props) =&gt;
    (props.hasPadding && "var(--container-padding)") || "none"};
`;</code></pre>

Notice how we don’t need a ternary when setting the width? That’s because we’ve already set a default for it with `width: props.width || "100%",`. Also, we used [CSS custom properties](https://styled-components.com/docs/basics#passed-props) because we can!

Note: If styled components are React components, and we can pass props, then can we also use states? The library’s GitHub account has an [issue addressing this](https://github.com/styled-components/styled-components/issues/1746) very matter.

{{% ad-panel-leaderboard %}}

### Extending Styles

Let’s say you’re working on a landing page, and you’ve set your [container to a certain max-width](https://css-tricks.com/the-inside-problem/) to keep things centered. You have a `StyledContainer` for that:

<pre><code class="language-css">const StyledContainer = styled.section`
  max-width: 1024px;
  padding: 0 20px;
  margin: 0 auto;
`;</code></pre>

Then, you discover that you need a smaller container, with padding of 10 pixels on both sides, instead of 20 pixels. Your first thought might be to create another styled component, and you’d be right, but it wouldn’t take any time before you realize that you are duplicating styles.

<pre><code class="language-css">const StyledContainer = styled.section`
  max-width: 1024px;
  padding: 0 20px;
  margin: 0 auto;
`;

const StyledSmallContainer = styled.section`
  max-width: 1024px;
  padding: 0 10px;
  margin: 0 auto;
`;</code></pre>

Before you go ahead and create `StyledSmallContainer`, like in the snippet above, let’s learn the way to reuse and inherit styles. It’s more or less like how the `spread` operator works:

<pre><code class="language-javascript">const StyledContainer = styled.section`
  max-width: 1024px;
  padding: 0 20px;
  margin: 0 auto;
`;

// Inherit StyledContainer in StyledSmallConatiner
const StyledSmallContainer = styled(StyledContainer)`
  padding: 0 10px;
`;

function Home() {
  return (
    &lt;StyledContainer&gt;
      &lt;h1&gt;The secret is to be happy&lt;/h1&gt;
    &lt;/StyledContainer&gt;
  );
}

function Contact() {
  return (
    &lt;StyledSmallContainer&gt;
      &lt;h1&gt;The road goes on and on&lt;/h1&gt;
    &lt;/StyledSmallContainer&gt;
  );
}</code></pre>

In your `StyledSmallContainer`, you’ll get all of the styles from `StyledContainer`, but the padding will be overridden. Keep in mind that, ordinarily, you’ll get a section element rendered for `StyledSmallContainer`, because that’s what `StyledContainer` renders. But that doesn’t mean it’s carved in stone or unchangeable.

### The “as” Polymorphic Prop

With the [`as` polymorphic prop](https://styled-components.com/docs/api#as-polymorphic-prop), you can swap the **end** element that gets rendered. One use case is when you inherit styles (as in the last example). If, for example, you’d prefer a `div` to a `section` for `StyledSmallContainer`, you can pass the `as` prop to your styled component with the value of your preferred element, like so:

<pre><code class="language-javascript">function Home() {
  return (
    &lt;StyledContainer&gt;
      &lt;h1&gt;It’s business, not personal&lt;/h1&gt;
    &lt;/StyledContainer&gt;
  );
}

function Contact() {
  return (
    &lt;StyledSmallContainer as="div"&gt;
      &lt;h1&gt;Never dribble when you can pass&lt;/h1&gt;
    &lt;/StyledSmallContainer&gt;
  );
}</code></pre>

Now, `StyledSmallContainer` will be rendered as a `div`. You could even have a custom component as your value:

<pre><code class="language-javascript">function Home() {
  return (
    &lt;StyledContainer&gt;
      &lt;h1&gt;It’s business, not personal&lt;/h1&gt;
    &lt;/StyledContainer&gt;
  );
}

function Contact() {
  return (
    &lt;StyledSmallContainer as={StyledContainer}&gt;
      &lt;h1&gt;Never dribble when you can pass&lt;/h1&gt;
    &lt;/StyledSmallContainer&gt;
  );
}</code></pre>

Don’t take it for granted.

### SCSS-Like Syntax

The CSS preprocessor [Stylis](https://stylis.js.org/) enables styled components to support SCSS-like syntax, such as nesting:

<pre><code class="language-css">const StyledProfileCard = styled.div`
  border: 1px solid black;

  &gt; .username {
    font-size: 20px;
    color: black;
    transition: 0.2s;

    &:hover {
      color: red;
    }

    + .dob {
      color: grey;
    }
  }
`;

function ProfileCard() {
  return (
    &lt;StyledProfileCard&gt;
      &lt;h1 className="username"&gt;John Doe&lt;/h1&gt;
      &lt;p className="dob"&gt;
        Date: &lt;span&gt;12th October, 2013&lt;/span&gt;
      &lt;/p&gt;
      &lt;p className="gender"&gt;Male&lt;/p&gt;
    &lt;/StyledProfileCard&gt;
  );
}</code></pre>

### Animation

Styled components have a `keyframes` helper that assists with constructing (reusable) animation keyframes. The advantage here is that the keyframes will be detached from the styled components and can be exported and reused wherever needed.

<pre><code class="language-css">import styled, {keyframes} from "styled-components";

const slideIn = keyframes`
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
`;

const Toast = styled.div`
  animation: ${slideIn} 0.5s cubic-bezier(0.4, 0, 0.2, 1) both;
  border-radius: 5px;
  padding: 20px;
  position: fixed;
`;</code></pre>

### Global Styling

While the original goal of CSS-in-JS and, by extension, styled components is scoping of styles, we can also leverage styled components’ global styling. Because we’re mostly working with scoped styles, you might think that’s an invariable factory setting, but you’d be wrong. Think about it: What really is scoping? It’s technically possible for us &mdash; in the name of global styling &mdash; to do something similar to this:

<pre><code class="language-javascript">ReactDOM.render(
  &lt;StyledApp&gt;
    &lt;App /&gt;
  &lt;/StyledApp&gt;,
  document.getElementById("root")
);</code></pre>

But we already have a helper function &mdash; `createGlobalStyle` &mdash; whose sole reason for existence is global styling. So, why deny it its responsibility?

One thing we can use `createGlobalStyle` for is to [normalize the CSS](https://necolas.github.io/normalize.css/):

<pre><code class="language-javascript">import {createGlobalStyle} from "styled-components";

const GlobalStyle = createGlobalStyle`
    /* Your css reset here */
`;

// Use your GlobalStyle
function App() {
  return (
    &lt;div&gt;
      &lt;GlobalStyle /&gt;
      &lt;Routes /&gt;
    &lt;/div&gt;
  );
}</code></pre>

**Note:** Styles created with `createGlobalStyle` do not accept any children. Learn more [in the documentation](https://styled-components.com/docs/api#createglobalstyle).

At this point, you might be wondering why we should bother using `createGlobalStlye` at all. Here are a few reasons:

- We can’t target anything outside of the root render without it (for example, `html`, `body`, etc.).
- `createGlobalStyle` injects styles but does not render any actual elements. If you look at the last example closely, you’ll notice we didn’t specify any HTML element to render. This is cool because we might not actually need the element. After all, we’re concerned with global styles. We are targeting selectors at large, not specific elements.
- `createGlobalStyle` is not scoped and can be rendered anywhere in our app and will be applicable as long as it’s in the DOM. Think about the **concept**, not the **structure**.

<pre><code class="language-javascript">import {createGlobalStyle} from "styled-components";

const GlobalStyle = createGlobalStyle`
  /* Your css reset here */

  .app-title {
    font-size: 40px;
  }
`;

const StyledNav = styled.nav`
    /* Your styles here */
`;

function Nav({children}) {
  return (
    &lt;StyledNav&gt;
      &lt;GlobalStyle /&gt;
      {children}
    &lt;/StyledNav&gt;
  );
}

function App() {
  return (
    &lt;div&gt;
      &lt;Nav&gt;
        &lt;h1 className="app-title"&gt;STYLED COMPONENTS&lt;/h1&gt;
      &lt;/Nav&gt;
      &lt;Main /&gt;
      &lt;Footer /&gt;
    &lt;/div&gt;
  );
}</code></pre>

If you think about the structure, then `app-title` should not be styled as set in `GlobalStyle`. But it doesn’t work that way. Wherever you choose to render your `GlobalStyle`, it will be injected when your component is **rendered**.

**Be careful**: `createGlobalStyles` will only be rendered if and when it’s in the DOM.

{{% ad-panel-leaderboard %}}

### CSS Helper

Already we’ve seen how to adapt styles based on props. What if we wanted to go a little further? The CSS helper function helps to achieve this. Let’s assume we have two text-input fields with states: empty and active, each with a different color. We can do this:

<pre><code class="language-css">const StyledTextField = styled.input`
  color: ${(props) => (props.isEmpty ? "none" : "black")};
`;</code></pre>

All’s well. Subsequently, if we need to add another state of filled, we’d have to modify our styles:

<pre><code class="language-css">const StyledTextField = styled.input`
  color: ${(props) =>
    props.isEmpty ? "none" : props.active ? "purple" : "blue"};
`;</code></pre>

Now the ternary operation is growing in complexity. What if we add another state to our text-input fields later on? Or what if we want to give each state additional styles, other than color? Can you imagine cramping the styles into the ternary operation? The `css` helper comes in handy.

<pre><code class="language-css">const StyledTextField = styled.input`
  width: 100%;
  height: 40px;

  ${(props) =>
    (props.empty &&
      css`
        color: none;
        backgroundcolor: white;
      `) ||
    (props.active &&
      css`
        color: black;
        backgroundcolor: whitesmoke;
      `)}
`;</code></pre>

What we’ve done is sort of expanded our ternary syntax to accommodate more styles, and with a more understandable and organized syntax. If the previous statement seems wrong, it’s because the code is trying to do too much. So, let’s step back and refine:

<pre><code class="language-css">const StyledTextField = styled.input`
width: 100%;
height: 40px;

// 1. Empty state
${(props) =&gt;
  props.empty &&
  css`
    color: none;
    backgroundcolor: white;
  `}

// 2. Active state
${(props) =&gt;
  props.active &&
  css`
    color: black;
    backgroundcolor: whitesmoke;
  `}

// 3. Filled state
${(props) =&gt;
  props.filled &&
  css`
    color: black;
    backgroundcolor: white;
    border: 1px solid green;
  `}
`;</code></pre>

Our refinement splits the styling into three different manageable and easy-to-understand chunks. It’s a win.

### StyleSheetManager

Like the CSS helper, `StyleSheetManager` is a helper method for modifying how styles are processed. It takes certain props &mdash; like `disableVendorPrefixes` (you can check out the [full list](https://styled-components.com/docs/api#stylesheetmanager)) &mdash; that help you opt out of [vendor prefixes](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix) from its subtree.

<pre><code class="language-javascript">import styled, {StyleSheetManager} from "styled-components";

const StyledCard = styled.div`
  width: 200px;
  backgroundcolor: white;
`;

const StyledNav = styled.div`
  width: calc(100% - var(--side-nav-width));
`;

function Profile() {
  return (
    &lt;div&gt;
      &lt;StyledNav /&gt;
      &lt;StyleSheetManager disableVendorPrefixes&gt;
        &lt;StyledCard&gt; This is a card &lt;/StyledCard&gt;
      &lt;/StyleSheetManager&gt;
    &lt;/div&gt;
  );
}</code></pre>

`disableVendorPrefixes` is passed as a prop to `<StyleSheetManager>`. So, the styled components wrapped by `<StyleSheetManager>` would be disabled, but not the ones in `<StyledNav>`.

### Easier Debugging

When introducing styled components to one of my colleagues, one of their complaints was that it’s hard to locate a rendered element in the DOM &mdash; or in React Developer Tools, for that matter. This is one of the drawbacks of styled components: In trying to provide unique class names, it assigns unique hashes to elements, which happen to be cryptic, but it makes the `displayName` readable for easier debugging.

<pre><code class="language-javascript">import React from "react";
import styled from "styled-components";
import "./App.css";

const LoginButton = styled.button`
  background-color: white;
  color: black;
  border: 1px solid red;
`;

function App() {
  return (
    &lt;div className="App"&gt;
      &lt;LoginButton&gt;Login&lt;/LoginButton&gt;
    &lt;/div&gt;
  );
}</code></pre>

By default, styled components render `LoginButton` as `<button class="LoginButton-xxxx xxxx">Login</button>` in the DOM, and as `LoginButton` in React Developer Tools, which makes debugging easier. We can toggle the `displayName` boolean if we don’t want this behavior. This requires a Babel configuration.

**Note**: In the documentation, the package `babel-plugin-styled-components` is specified, as well as a `.babelrc` configuration file. The issue with this is that, because we’re using `create-react-app`, we can’t configure a lot of things unless we eject. This is where Babel macros come in.

We’ll need to install `babel-plugin-macros` with npm or Yarn, and then create a `babel-plugin-macros.config.js` at the root of our application, with the content:

<pre><code class="language-javascript">module.exports = {
  styledComponents: {
    displayName: true,
    fileName: false,
  },
};</code></pre>

With the `fileName` value inverted, the `displayName` will be prefixed with the file name for even more unique precision.

We also now need to import from the `macro`:

<pre><code class="language-javascript">// Before
import styled from "styled-components";

// After
import styled from "styled-components/macro";</code></pre>

## Conclusion

Now that you can programmatically compose your CSS, do not abuse the freedom. For what it’s worth, do your very best to maintain sanity in your styled components. Don’t try to compose heavy conditionals, nor suppose that every thing should be a styled component. Also, do not over-abstract by creating nascent styled components for use cases that you are only guessing are somewhere around the corner.

### Further Resources

1. [Documentation](https://styled-components.com/docs), Styled Components
2. “[Building a Reusable Component System with React.js and styled-components](https://levelup.gitconnected.com/building-a-reusable-component-system-with-react-js-and-styled-components-4e9f1018a31c)”, Lukas Gisder-Dubé
3. [Usage with Next.js](https://styled-components.com/docs/advanced#nextjs)
4. [Usage with Gatsby](https://styled-components.com/docs/advanced#gatsby)

{{< signature "ks, ra, yk, al, il" >}}
