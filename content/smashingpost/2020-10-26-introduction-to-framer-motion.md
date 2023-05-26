---
title: 'Introducing Framer Motion'
slug: introduction-to-framer-motion
author: nefe-emadamerho-atori
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc5b83a6-864d-4f58-9894-0aea756c9412/introduction-to-framer-motion.png
date: 2020-10-26T14:00:00.000Z
summary: >-
  Animations, when done right, are powerful. However, creating eye-catching animations with CSS can be tricky. In comes Framer Motion. With Framer Motion, you don’t need to be a CSS expert to make beautiful animations. Framer Motion provides us with production-ready animations and a low-level API we can interact with to integrate these animations into our applications.
description: >-
  Animations, when done right, are powerful. However, creating eye-catching animations with CSS can be tricky. In comes Framer Motion. With Framer Motion, you don’t need to be a CSS expert to make beautiful animations. Framer Motion provides us with production-ready animations and a low-level API we can interact with to integrate these animations into our applications.
categories:
  - Apps
  - React
  - Animation
---

In this article, we’ll take a closer look at how Framer Motion helps us in creating awesome animations. We’ll learn how motion components work and learn how to chain animations together. We’ll look into how to make gesture-triggered, timed, and scroll animations with Framer motion. Along the way, we’ll use the things we learn to build five demo applications I’ve set up to show us how we can integrate Framer Motion into real-world applications.

This tutorial will be beneficial to readers who are interested in integrating animations in their React application.

**Note:** *This article requires a basic understanding of React and CSS.*

## What Is Framer Motion?

Framer Motion is an animation library that makes creating animations easy. Its simplified API helps us abstract the complexities behind animations and allows us to create animations with ease. 

### Motion Components

These are the building blocks of Framer motion. Motion components are created by prefixing `motion` to your regular HTML and SVG element (e.g, `motion.h1`). Motion components can accept several props, with the basic one being the `animate` prop. This prop takes in an object where we define the properties of that component we want to animate. The properties we define will be animated when the component mounts in the DOM. 

Let’s animate an h1 text using Framer Motion. First, we install the framer-motion library and import `motion`. 

<pre><code class="language-bash">npm i framer-motion
import { motion } from 'framer-motion';</code></pre>

Then we convert the h1 into a motion component.

<pre><code class="language-javascript">&lt;motion.h1 
  animate={{x: 20, y: -20}}&gt;
  This is a motion component
&lt;/motion.h1&gt;</code></pre>

This will cause the `h1` to slide 20px to the right and move 20px up when it loads. When units aren’t added, calculations are done using pixels. However, you can explicitly set the units you want the calculations to be based on,  `animate={{x: "20rem", y: "-20rem"}}>`.

{{% feature-panel %}}

By default, a motion component will be animated from the state defined from its styles to those in the `animate` prop. However, if we wanted to, we could hijack and define the initial animation state of the component using the `initial` prop. While the `animate` prop is used to define the behavior of components when they mount, the `initial` prop defines their behavior before they mount.  

If we want our h1 to come in from the left, we control that using the initial prop.

<pre><code class="language-javascript">&lt;motion.h1
    initial={{x: -1000}}
    animate={{x: 20}}&gt;
   This is a motion component
&lt;/motion.h1&gt;</code></pre>

Now, when the `h1` mounts, it slides in from the left.

<iframe loading="lazy" src="https://codesandbox.io/embed/fervent-lederberg-58nht?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="fervent-lederberg-58nht"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

We are not limited to a single animation. We can define a series of animations called `keyframes` in an array of values. Each value will get animated in sequence.

<pre><code class="language-javascript">&lt;motion.h1
    initial={{x: -1000}}
    animate={{x: [20, 50, 0, -70, 40] }}&gt;
   This is a motion component
&lt;/motion.h1&gt;</code></pre>
  
<iframe loading="lazy" src="https://codesandbox.io/embed/exciting-bohr-t0jue?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="exciting-bohr-t0jue"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

The `transition` prop allows us to define how the animations occur. With it, we define how values animate from one state to another. Among other things, we can define the `duration`, `delay`, and `type` of animation using this prop.

<pre><code class="language-javascript">&lt;motion.h1
    initial={{ x: -1000 }}
    animate={{ x: 0 }}
    transition={{
        type: "tween",
        duration: "2",
        delay: "1"
    }}&gt;
    This is a motion component
&lt;/motion.h1&gt;</code></pre>

<iframe loading="lazy" src="https://codesandbox.io/embed/dazzling-rgb-i0c6d?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="dazzling-rgb-i0c6d"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Say we were to animate several motion components simultaneously, like in the code snippet below.

<pre><code class="language-javascript">&lt;div className="App"&gt;
      &lt;motion.h1
        initial={{ x: -1000 }}
        animate={{ x: 0 }}
        transition={{
          type: "tween",
          duration: "2",
          delay: "1"
        }}&gt;
        This is a motion h1
      &lt;/motion.h1&gt;
      &lt;motion.h2  
        initial={{ y: -1000 }}
        animate={{ y: 0 }}
        transition={{
          type: "tween",
          duration: "1",
          delay: ".4"
        }}&gt;This is a motion h2
      &lt;/motion.h2&gt;
      &lt;motion.h3
       initial={{ x: 100, opacity: 0 }}
       animate={{ x: 0, opacity: 1 }}&gt;
         This is a motion h3
      &lt;/motion.h3&gt;
      &lt;motion.h4
       initial={{ scale: 0.7 }}
       animate={{ scale: 1.7 }}
       transition={{
         type: "tween",
         duration: "2",
         delay: "1"
       }}&gt;
         This is a motion h4
      &lt;/motion.h4&gt;
    &lt;/div&gt;</code></pre>

While this works, the `variants` prop in Framer Motion enables us to extract our animation definitions into a variants object. Not only do `variants` make our code cleaner, but they allow us to create even more powerful and complex animations.

Extracting our animation definitions into variants objects, we have this:

<pre><code class="language-javascript">const H1Variants = {
  initial: { x: -1000 },
  animate: { x: 0 },
  transition: {
    type: "tween",
    duration: 2,
    delay: 1
  }
} 
const H2Variants = {
  initial: { y: -1000 },
  animate: { y: 0 },
  transition: {
    type: "tween",
    duration: 1,
    delay: .4
  }
}
const H3Variants = {
  initial:{ x: 100, opacity: 0 },
  animate:{ x: 0, opacity: 1 }
}
const H4Variants = {
  initial:{ scale: 0.7 },
  animate:{ scale: 1.7 },
  transition:{
    type: "tween",
    duration: "2",
    delay: "1"
  }
}</code></pre>
   
Instead of passing the animation definitions into a component’s `initial` and `animate` props directly, we extract these definitions into standalone variant objects. In the variant objects, we define variant names that describe each animation’s name as variants.

<pre><code class="language-javascript">&lt;div className="App"&gt;
      &lt;motion.h1
      variants={H1Variants}
      initial='initial'
      animate='animate'
      &gt;
        This is a motion h1
      &lt;/motion.h1&gt;
      &lt;motion.h2  
        variants={H2Variants}
        initial='initial'
        animate='animate'
       &gt;
        This is a motion h2
      &lt;/motion.h2&gt;
      &lt;motion.h3
        variants={H3Variants}
        initial='initial'
        animate='animate'
       &gt;
         This is a motion h3
      &lt;/motion.h3&gt;
      &lt;motion.h4
        variants={H4Variants}
        initial='initial'
        animate='animate'
       &gt;
         This is a motion h4
      &lt;/motion.h4&gt;
&lt;/div&gt;</code></pre>

In the `variants` prop, we pass in the name of the variant objects for each motion component and then pass in the animations to the `initial` and `animate` props.

We can take our current setup with variants further to reduce repetition. Using variants, we can propagate animation attributes down through the DOM from a parent motion component. For this to work, we create variants for the parent `motion.div` with similar animation names in its variant object as its children. By doing this, we won’t have to pass the animation names’ to each child component. Behind the scenes, the parent element handles that for us.

<pre><code class="language-javascript">const ContainerVariants = {
  initial: {},
  animate: {}
};
const H1Variants = {
  initial: { x: -1000 },
  animate: { x: 0 },
  transition: {
    type: "tween",
    duration: 2,
    delay: 1
  }
};
//more variants below

&lt;motion.div
      className="App"
      variants={ContainerVariants}
      initial="initial"
      animate="animate"
    &gt;
      &lt;motion.h1 variants={H1Variants}&gt;This is a motion h1&lt;/motion.h1&gt;
      &lt;motion.h2 variants={H2Variants}&gt;This is a motion h2&lt;/motion.h2&gt;
      &lt;motion.h3 variants={H3Variants}&gt;This is a motion h3&lt;/motion.h3&gt;
      &lt;motion.h4 variants={H4Variants}&gt;This is a motion h4&lt;/motion.h4&gt;
&lt;/motion.div&gt;</code></pre>

Now we have a cleaner code with no repetitions. We turned the container div to a motion component so we could pass in the `ContainerVariants` object we defined. Since we don’t define any animations on the container, we pass in empty objects to `initial` and `animate`. Your animation names must be the same in every variant object for the propagation to work. 

<iframe loading="lazy" src="https://codesandbox.io/embed/hidden-mountain-ts9mx?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="hidden-mountain-ts9mx"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Now we understand the basics of Framer Motion. Let’s begin building our fist of 5 demo applications.

{{% ad-panel-leaderboard %}}

## Icon Shop

We can create interactive animations based on gestures. Motion components are currently able to listen for hover, tap, pan, and drag gesture detection. We’ll be building this [Icon Shop](https://codesandbox.io/s/icon-shop-0t3qg) app using the `whileHover` prop. 

<iframe loading="lazy" src="https://codesandbox.io/embed/icon-shop-0t3qg?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Icon Shop"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

### Components

- `App.js`: this holds the heading texts.  
- `Card.jsx`: here, we define the animations for the icon cards. 
- `CardContainer.jsx`: we import and loop through the icons.  
- `styles.js`: create, style, and export the motion components. I used styled-components for styling the components.

Let’s start with `App.js`.

<pre><code class="language-javascript">import { H1, H2 } from "./Styles";
import CardContainer from "./CardContainer";

  return (
    &lt;div&gt;
      &lt;H1 
        initial={{ y: -100 }} 
        animate={{ y: 0, transition: { delay: 1 } }}&gt;
        Icon Shop
      &lt;/H1&gt;
      &lt;H2 
        initial={{ x: -1000 }} 
        animate={{ x: 0, transition: { delay: 1 } }}&gt;
        Hover over the cards to see the motion magic
      &lt;/H2&gt;
      &lt;CardContainer /&gt;
    &lt;/div&gt;
  );</code></pre>

We import the `H1` and `H2` motion components we created in the `Styles.js` file. Since they are motion components, we use the `initial` and `animate` props to define their behavior before and when they mount. Here, we also import and display the `CardContiner` component.

Now, the `CardContainer.js`.

<pre><code class="language-javascript">import { Container } from "./Styles";
import Card from "./Card";
import { ReactComponent as AddIcon } from "./assets/add.svg";
import { ReactComponent as AirplaneIcon } from "./assets/airplane.svg";
import { ReactComponent as AlarmIcon } from "./assets/alarm.svg";
//more svg imports below...

const icons = [
  &lt;AddIcon /&gt;,
  &lt;AirplaneIcon /&gt;,
  &lt;AlarmIcon /&gt;,
  //more icons below
];

const CardContainer = () =&gt; {
  return (
    &lt;Container initial={{ x: -1000 }} animate={{ x: 0 }}&gt;
      {icons.map((icon) =&gt; (
        &lt;Card icon={icon} /&gt;
      ))}
    &lt;/Container&gt;
  );
};</code></pre>

Here, we import the SVGs, the `Container` motion component, and the `Card` component.

Similar to `H1` and `H2` in `App.js`, we define animations of the `Container` using the `initial` and `animate` props. When it loads, it will create a cool effect of sliding in from the left of the browser. 

Now, `Card.js`

<div class="break-out">

<pre><code class="language-javascript">import { CardBox, IconBox } from "./Styles";
const CardVariants = {
  beforeHover: {},
  onHover: {
    scale: 1.1
  }
};
const IconVariants = {
  beforeHover: {
    opacity: 0,
    y: -50
  },
  onHover: {
    opacity: 1,
    y: 0,
    scale: 1.5,
    transition: {
      type: "tween"
    }
  }
};

const Card = ({ icon }) =&gt; {
  console.log(icon);
  return (
    &lt;CardBox variants={CardVariants} initial="beforeHover" whileHover="onHover"&gt;
      &lt;IconBox variants={IconVariants}&gt;{icon}&lt;/IconBox&gt;
    &lt;/CardBox&gt;
  );
};</code></pre>
</div>

Here, we create two variant objects with `beforeHover` and `onHover` animations. In the `CardVariants` object, we don’t want to do anything initially, so `beforeHover` is an empty object. `onHover` we increase the scale of the card box.

In the `IconVariants` object, we define the initial state of the `IconBox` in its `beforeHover`. We set its opacity to 0 and push it upwards by 50px. Then, in `onHover`, we set the opacity back to 1, push it back to its default position, and change the transition type to `tween`. Then we pass in the variants to their respective motion components. We make use of the propagation, so we don’t need to explicitly set the `initial` and `animate` props to the `IconBox` component.

## Animated Navbar

We’ll build a simple Navigation component, and we’ll see how we can create timing relationships between parent and children motion components.

<iframe loading="lazy" src="https://codesandbox.io/embed/navbar-237pm?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Navbar"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

### Components

- `App.js`: this holds the heading texts.  
- `Styles.js`: create, style, and export the motion components. The components are styled using styled-components.

Let’s take a look at the `App.js` file.

<pre><code class="language-javascript">import { Header, Nav, Link, SvgBox } from "./Styles";

function App() {
  const [isOpen, setIsOpen] = useState(false);
  const iconVariants = {
    opened: {
      rotate: 135
    },
    closed: {
      rotate: 0
    }
  };
  const menuVariants = {
    opened: {
      top: 0,
      transition: {
        when: "beforeChildren",
        staggerChildren: 0.5
      }
    },
    closed: {
      top: "-90vh"
    }
  };
  const linkVariants = {
    opened: {
      opacity: 1,
      y: 50
    },
    closed: {
      opacity: 0,
      y: 0
    }
  };
</code></pre>

We create an `isOpen` state that will be used to check if the Navbar is open or not. We create 3 variant objects, `iconVariants`, `menuVariants`, and `linkVariants` where we define the animations for the `SvgBox`, `Nav`, and `Link` motion components respectively. The `iconVariants` is used to rotate the `SvgBox` 135deg when it’s hovered over. We don’t need to add “deg” to the value. In the `menuVariants`, we control the top position of the `Nav` like you would using the `position` property in CSS. We toggle the top position of the `Nav` based on the `isOpen` state.

With variants, we can create timing relationships between parent and children motion components. We define the relationship between parent `Nav` and its child, `Link` using the `when` property in the transition object. Here, set it to `beforeChildren`, so the parent component’s animations will finish before the child’s animation begins.

Using the `staggerChildren` property, we set a timing order for each link. Each link will take 0.5 seconds to appear one after the other. This creates a nice visual cue when the `Nav` is opened. In the `linkVariants` we animate the opacity and the vertical position of each link.

<div class="break-out">

<pre><code class="language-javascript">&lt;div className="App"&gt;
      &lt;Header&gt;
        &lt;SvgBox
          variants={iconVariants}
          animate={isOpen ? "opened" : "closed"}
          onClick={() =&gt; setIsOpen(!isOpen)}
        &gt;
          &lt;svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="https://www.w3.org/2000/svg"
          &gt;
            &lt;path
              d="M12 4C11.4477 4 11 4.44772 11 5V11H5C4.44772 11 4 11.4477 4 12C4 12.5523 4.44772 13 5 13H11V19C11 19.5523 11.4477 20 12 20C12.5523 20 13 19.5523 13 19V13H19C19.5523 13 20 12.5523 20 12C20 11.4477 19.5523 11 19 11H13V5C13 4.44772 12.5523 4 12 4Z"
              fill="#fff"
            /&gt;
          &lt;/svg&gt;
        &lt;/SvgBox&gt;
      &lt;/Header&gt;
      &lt;Nav
        initial={false}
        variants={menuVariants}
        animate={isOpen ? "opened" : "closed"}
      &gt;
        &lt;Link variants={linkVariants}&gt;home&lt;/Link&gt;
        &lt;Link variants={linkVariants}&gt;about&lt;/Link&gt;
        &lt;Link variants={linkVariants}&gt;gallery&lt;/Link&gt;
      &lt;/Nav&gt;
&lt;/div&gt;</code></pre>
</div>

Here, we pass in the variants to their respective components. In the `SvgBox`, we toggle the state of `isOpen` whenever it’s clicked, then conditionally animate it based on the state. Like the `SvgBox`, we conditionally animate the `Nav` and the `Link`s based on `isOpen`'s state.

{{% ad-panel-leaderboard %}}

## Animated Modal

We’ll build a modal component and learn about Framer Motion’s `AnimatePresence`, and how it allows us animate elements as they leave the DOM.

<iframe loading="lazy" src="https://codesandbox.io/embed/modal-rrc74?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Modal"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

 Components: 

-  `App.js`: we set up the `showModal` state here.
- `Modal.jsx`: the actual animation work takes place here.
- `Styles.js`: create, style, and export the motion components. The components are styled using styled-components.

Let’s look into `App.js`

<pre><code class="language-javascript">import { ToggleButton, Container } from "./Styles";
import Modal from "./Modal";

function App() {
  const [showModal, setShowModal] = useState(false);
  const toggleModal = () =&gt; {
    setShowModal(!showModal);
  };
  return (
    &lt;Container&gt;
      &lt;ToggleButton
        initial={{ x: -700 }}
        animate={{
          x: 0,
          transition: { duration: 0.5 }
        }}
        onClick={toggleModal}
      &gt;
        Toggle Modal
      &lt;/ToggleButton&gt;
      &lt;Modal showModal={showModal} /&gt;
    &lt;/Container&gt;
  );
}
</code></pre>

We create a `showModal` state that will be used to conditionally render the modal. The `toggleModal` function will toggle the state whenever the `ToggleButton` is clicked. `ToggleButton` is a motion component, so we can define animations for it. When it mounts, it slides in from the left. This animation runs for 0.5 seconds. We also pass in the `showModal` state to the `Modal` through props.

Now, `Modal.jsx`

<pre><code class="language-javascript">import { AnimatePresence } from "framer-motion";
import { ModalBox, ModalContent, Container } from "./Styles";

&lt;Container&gt;
  &lt;AnimatePresence&gt;
    {showModal && (
      &lt;ModalBox
        initial={{ opacity: 0, y: 60, scale: 0.3 }}
        animate={{
          opacity: 1,
          y: 0,
          scale: 1,
          transition: { type: "spring", stiffness: 300 }
        }}
        exit={{ opacity: 0, scale: 0.5, transition: { duration: 0.6 } }}
        &gt;
        &lt;ModalContent
          initial={{ y: -30, opacity: 0 }}
          animate={{ y: 0, opacity: 1, transition: { delay: 1 } }}
        &gt;
           Modal content!!!!
        &lt;/ModalContent&gt;
      &lt;/ModalBox&gt;
    )}
  &lt;/AnimatePresence&gt;
&lt;/Container&gt;</code></pre>

We import `AnimatePresence` from `framer-motion`. It allows us to set exit animations for components when they leave DOM. We conditionally render the `Modal` based on the `showModal` state. We define the animations for the `ModalBox` and `ModalContent` through their `initial` and `animate` props. There’s also a new prop here, `exit`. Having `AnimatePresence` as a wrapper allows us to add exit animations to `ModalBox` in the `exit` prop. 

## Scroll Animation

We’ll use a combination of the `useAnimation` hook and `react-intersection-observer` to create scroll-triggered animations.

<iframe loading="lazy" src="https://codesandbox.io/embed/scroll-reveal-2vces?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Scroll Reveal"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Components

- `App.js`: we set up the animations for the `Box` component and render it in `App` 
- `Styles.js`: create, style, and export the motion components. The components are styled using styled-components.

<pre><code class="language-javascript">import React, { useEffect } from "react";
import { useAnimation } from "framer-motion";
import { useInView } from "react-intersection-observer";
import { Container, H1,StyledBox } from "./Styles";

const BoxVariants = {
  visible: { opacity: 1, x: 0, transition: { duration: 1 } },
  hidden: { opacity: 0, x: 300 },
};

const Box = () =&gt; {
  const controls = useAnimation();
  const [ref, inView] = useInView();
  useEffect(() =&gt; {
    if (inView) {
      controls.start("visible");
    }
  }, [controls, inView]);
  return (
    &lt;StyledBox
      ref={ref}
      animate={controls}
      initial="hidden"
      variants={BoxVariants}
    /&gt;
  );
};</code></pre>

The `useAnimation` hook allows us to control the sequences in which our animations occur. We have access to `controls.start` and `controls.stop` methods that we can use to manually start and stop our animations. We pass in the initial `hidden` animaton to `StyledBox`. We pass in the controls we defined with the `start` method to `StyledBox` animate prop.  
 
`react-intersection-observer`’s `useInView` hook allows us to track when a component is visible in the viewport. The `useInView` hook gives us access to `ref`, which we pass to the component we want to watch, and the `inView` boolean, that tells us if that element is `inView` or not. We use the `useEffect` to call `controls.start` whenever the element we’re watching, `StyledBox` is in view. We pass in `controls` and `inView` as  `useEffect`’s dependencies. Also, we pass in the variants we defined, `BoxVariants` to `StyledBox`.

## Hero Animation

We’ll build a cool hero banner animation using the `useCycle` hook. We’ll understand how `useCycle` allows us to cycle through animations.

<iframe loading="lazy" src="https://codesandbox.io/embed/hero-animation-zwh9y?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="hero animation"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<div class="break-out">

<pre><code class="language-javascript">import React, { useEffect } from "react";
import { useCycle } from "framer-motion";
import { Container, H1, HeroSection, Banner, TextBox } from "./Styles";
import { ReactComponent as BannerIllustration } from "./bighead.svg";

const H1Variants = {
  initial: { y: -200, opacity: 0 },
  animate: { y: 0, opacity: 1, transition: { delay: 1 } },
};
const TextVariants = {
  initial: { x: 400 },
  animate: { x: 0, transition: { duration: 0.5 } },
};
const BannerVariants = {
  animationOne: { x: -250, opacity: 1, transition: { duration: 0.5 } },
  animationTwo: {
    y: [0, -20],
    opacity: 1,
    transition: { yoyo: Infinity, ease: "easeIn" },
  },
};</code></pre>
</div>

We define 3 variants, `H1Variants`, `TextVariants`, and `BannerVariants`. However, our focus is `BannerVariants`. We define 2 animations, `animationOne` and `animationTwo` in `BannerVariants`. These are the animations we pass into the `useCycle` to cycle through.

<div class="break-out">

<pre><code class="language-javascript">const [animation, cycleAnimation] = useCycle("animationOne", "animationTwo");
  useEffect(() =&gt; {
    setTimeout(() =&gt; {
      cycleAnimation();
    }, 2000);
  }, []);</code></pre>
</div>

`useCycle` works similar to the `useState` hook. In the destructured array, `animation` represents the animation that is active, whether `animationOne` or `animationTwo`. The `cylceAnimation` function that cycles between the animation we defined. We pass in the animations we want to cycle through into `useCycle` and call `cylceAnimation` after 2 seconds in `useEffect`.

<div class="break-out">

<pre><code class="language-javascript">&lt;div className="App"&gt;
      &lt;Container&gt;
        &lt;H1 variants={H1Variants} initial="initial" animate="animate"&gt;
          Cool Hero Section Anmiation
        &lt;/H1&gt;
        &lt;HeroSection&gt;
          &lt;TextBox variants={TextVariants} initial="initial" animate="animate"&gt;
            Storage shed, troughs feed bale manure, is garden wheat oats at
            augers. Bulls at rose garden cucumbers mice sunflower wheat in pig.
            Chainsaw foal hay hook, herbs at combine harvester, children is
            mallet. Goat goose hen horse. Pick up truck livestock, pets and
            storage shed, troughs feed bale manure, is garden wheat oats at
            augers. Lamb.
          &lt;/TextBox&gt;
          &lt;Banner variants={BannerVariants} animate={animation}&gt;
            &lt;BannerIllustration /&gt;
          &lt;/Banner&gt;
        &lt;/HeroSection&gt;
      &lt;/Container&gt;
    &lt;/div&gt;</code></pre>
</div>

At the end of everything, we pass in the variants to their respective components and watch the magic happen. With this, the `Banner` will initially slide in from the right based on the animations we defined in `animationOne`, and after 2 seconds, `cycleAnimation` will be called which will trigger `animationTwo`.

As a wise Pig once said, “that’s all folks.”

## Conclusion

We’ve gone through the basics of Framer Motion and seen some demo projects that give us a glimpse of the range of animations we can create. However, you can do so much more with it. I encourage you to dive into the docs and go wild.

### Resources

- [Framer Motion Api Docs](https://www.framer.com/api/motion/), Framer Motion 
- [react-intersection-observer](https://www.npmjs.com/package/react-intersection-observer), npm 
- [Framer Motion for React,](https://www.youtube.com/playlist?list=PL4cUxeGkcC9iHDnQfTHEVVceOEBsOf07i) NetNinja

{{< signature "ks, ra, yk, il" >}}
