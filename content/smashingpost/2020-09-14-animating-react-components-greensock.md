---
title: 'Animating React Components With GreenSock'
slug: animating-react-components-greensock
author: blessing-krofegha
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52b8bc01-38e6-4382-85d3-0a2e5a9a2e7b/animating-react-components-greensock.png
date: 2020-09-14T11:00:00.000Z
summary: >-
  GreenSock Animation Platform (GSAP) is a set JavaScript functions that let you tween a value/attribute/CSS property over time and insert these tweens into a timeline for more complex animations. In this article, Blessing explains how GSAP plays well with the React library by integrating its functions into a React component in building an example landing page with a variety of animations.
description: >-
  In this article, Blessing explains how GSAP plays well with the React library by integrating its functions into a React component in building an example landing page with a variety of animations.
categories:
  - Apps
  - Native
  - React
  - Animation
  - JavaScript
---

During the early days of the World Wide Web, things were rather static and boring. Webpages were mostly based on graphic design and layouts from the print world until animations were introduced. Animation can engage and hold people’s attention longer than a static web page and communicates an idea or concept more clearly and effectively. 

However, when not done right, animations can hamper user interactions with your product and negatively impact traction. The [GreenSock Animation Platform](https://greensock.com/) AKA (GSAP) is a powerful JavaScript library that enables front-end developers, animators and designers to create performant timeline based animations. It allows animation lovers take precise control of their animation sequences rather than the sometimes [constraining](https://css-tricks.com/myth-busting-css-animations-vs-javascript/) `keyframe` and `animation` properties that CSS offers.

In this article, I’ll introduce you to some features of GSAP such as `scrollTriggers`, `Timelines`, `Easing` etc, at the end we’ll build an intuitive user interface by animating a React app with this features👌. Check out the finished project on [codesandbox](https://codesandbox.io/s/flamboyant-franklin-toite).

This article will be useful to you if:

- You have been building animations on web applications with HTML, CSS, and JavaScript.
- You are already building animated webpages in a React apps with packages like [animate.css,](https://animate.style/) [React-motion](https://www.npmjs.com/package/react-motion), [Framer-motion](https://www.framer.com/motion/), and [React-Spring](https://www.react-spring.io/), plus you want to check out alternatives.
- You are a React enthusiast, and you’d like to build complex animations on React-based web applications.

We will look at how to build a variety of animations from an existing web project. Let’s get to it!

**Note**: This article assumes you are comfortable with HTML, CSS, JavaScript, and React.js.

## What Is GSAP?

GreenSock Animation Platform also known as GSAP is an Ultra high-performance, professional-grade animation for the modern web that allows developers to animate their apps in a modular, declarative, and re-usable fashion. It is framework-agnostic and can be used across any JavaScript based project, it has a very minimal bundle size and will not bloat your app.

GSAP can perform canvas animations, used to create WebGL experiences, and create dynamic SVG animations and as great browser support.

{{% feature-panel %}} 

## Why Use GSAP?

Maybe you’re not quite ready to betray other frameworks yet, or you haven’t been convinced to embrace the goodies that come with GSAP. Allow me to give you a few reason why you may want to consider GSAP.

### You Can Build Complex Animations

GSAP JavaScript library makes it possible for developers to build simple to very complex physics-based animations like in the case of these [sites](https://www.awwwards.com/websites/gsap-animation/), it allows developers and designers sequence motion and controls the animation dynamically. It has lots of plugins such as [DrawSVGPlugin](https://greensock.com/docs/v2/Plugins/DrawSVGPlugin), [MorphSVGPlugin,](https://greensock.com/docs/v2/Plugins/MorphSVGPlugin) and [more](https://greensock.com/docs/v2/Plugins), which makes creating SVG based animations and 2D/3D animations a reality. Asides integrating GSAP on DOM elements, you can use them within [WebGL](https://greensock.com/PixiPlugin/)/[Canvas](https://greensock.com/easelplugin/)/ Three.js context-based animations.

Furthermore, the [easing](https://greensock.com/ease-visualizer) capacity of GSAP is quite sophisticated, hence making it possible to create advance effects with [multiple beziers](https://greensock.com/docs/v2/Plugins/BezierPlugin) as compared to the regular [CSS animation](https://www.smashingmagazine.com/2014/04/understanding-css-timing-functions/).

### Performance

GSAP has an impressive high performance across different browsers.

According to GSAP’s team, in their [website](https://greensock.com/why-gsap/), “GSAP is **20x faster** than jQuery, plus GSAP is the fastest full-featured scripted animation tool on the planet. It's even faster than [CSS3 animations and transitions](https://greensock.com/transitions/) in many cases.” Confirm [speed comparison](https://greensock.com/js/speed.html) for yourself.

Furthermore, the GSAP animations perform effortlessly on both desktop computers, tablets, and smartphones. It is not needed to add a long list of prefixes, this is all being taken care of under the hood by GSAP.

You can check out more [benefits](https://youtu.be/pFqBqgOv9E8) on GSAP or see what [Sarah Drasner](https://twitter.com/sarah_edo) as to say about it [here](https://css-tricks.com/how-to-animate-on-the-web-with-greensock/).

## Cons Of GSAP

Are you saying I should always use GSAP for every project? Of course not! I feel like, there’s only one reason you might not want to use GSAP. Let’s find out!

- GSAP is solely a JavaScript-based animation library, hence it requires some knowledge of JavaScript and DOM manipulation to effectively utilize its methods and APIs. This learning curve downside leaves even more room for complications for a beginner starting out with JavaScript.
- GSAP doesn’t cater to CSS based animations, hence if you are looking for a library for such, you might as well use `keyframes` in CSS animation.

If you’ve got any other reason, feel free to share it in the comment section. 

Alright, now that your doubts are cleared, let’s jump over to some nitty-gritty in GSAP.

## GSAP Basics

Before we create our animation using React, let’s get familiar with some methods and building blocks of GSAP.

If you already know the fundamentals of GSAP, you can skip this section and jump straight to the project section, where we’ll make a landing page skew while scrolling.

### Tween

A tween is a single movement in an animation. In GSAP, a tween has the following syntax:

<pre><code class="language-javascript">TweenMax.method(element, duration, vars)</code></pre>

Let’s take a look at what this syntax represents;

1. `method` refers to the GSAP method you’ll like to tween with.
2. `element` is the element you want to animate. If you want to create tweens for multiple elements at the same time, you can pass in an array of elements to `element`.
3. `duration` is the duration of your tween. It is an integer in seconds (without the `s` suffix!).
4. `vars` is an object of the properties you want to animate. More on this later.

### GSAP methods

GSAP provides numerous methods to create animations. In this article, we’d mention only a few such as `gsap.to`, `gsap.from`, `gsap.fromTo`. You can check out other cool methods in their [documentation](https://greensock.com/docs/). The methods discussed in this section will be used in building our project later in this tutorial.

- `gsap.to()` the values to which an object should be animated i.e the end property values of an animated object &mdash; as shown below:  

<pre><code class="language-css">gsap.to('.ball', {x:250, duration: 5})</code></pre>

To demonstrate the `to` method the codepen demo below shows that an element with a class of ball `250px` will move across the `x-axis` in five seconds when the components mounts. If a duration isn't given, a default of 500 milliseconds would be used.

{{< codepen height="480" theme_id="light" slug_hash="LYNrzMB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [GSAP REACT DEMO1](https://codepen.io/smashingmag/pen/LYNrzMB) by <a href="https://codepen.io/Beveloper">Blessing Krofegha</a>.{{< /codepen >}}

**Note**: `x` and `y-axis` represent the horizontal and vertical axis respectively, also in CSS transform properties such as `translateX` and `translateY` they are represented as `x` and `y` for `pixel-measured` transforms and `xPercent` and `yPercent` for percentage-based transforms.

To view the complete snippet of the code check the codepen playground.

- `gsap.from()` &mdash; Defines the values an object should be animated from &mdash; i.e., the start values of an animation:  

<pre><code class="language-css">gsap.from('.square', {duration:3, scale: 4})</code></pre>

The codepen demo show how an element with a class of `square` is resized from a scale of 4 in `3seconds` when the components mounts. Check for the complete code snippet on this codepen.

{{< codepen height="480" theme_id="light" slug_hash="bGpKoPV" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [GSAP REACT DEMO2](https://codepen.io/smashingmag/pen/bGpKoPV) by <a href="https://codepen.io/Beveloper">Blessing Krofegha</a>.{{< /codepen >}}

- `gsap.fromTo()` &mdash; lets you define the starting and ending values for an animation. It is a combination of both the `from()` and `to()` method.

Here’s how it looks;

<div class="break-out">

<pre><code class="language-css">gsap.fromTo('.ball',{opacity:0 }, {opacity: 1 , x: 200 , duration: 3 });
gsap.fromTo('.square', {opacity:0, x:200}, { opacity:1, x: 1 , duration: 3 });</code></pre>
</div>

This code would animates the element with a class of `ball` from an opacity of 0 to an opacity of `1` across the `x-axis` in `3 seconds`  and the `square` class is animated the from an opacity of `0` to `1` in `3 seconds` across the `x-axis` only when the component mounts. To see how the `fromTo` method works and the complete code snippet, check the demo on CodePen below.

{{< codepen height="480" theme_id="light" slug_hash="WNwyXex" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [React GSAP FromTo demo](https://codepen.io/smashingmag/pen/WNwyXex) by <a href="https://codepen.io/Beveloper">Blessing Krofegha</a>.{{< /codepen >}}

**Note**: Whenever we’re animating positional properties, such as `left` and `top`, we must ensure that the elements concerned must have a CSS position property of either `relative`, `absolute`, or `fixed`.

### Easing

GSAP [official documentation](https://greensock.com/docs/v3/Eases) defined easing as the primary way to change the timing of your Tweens. It determines how an object changes position at different points. Ease controls the rate of change of animation in GSAP and is used to set the style of an object’s animation.

GSAP provides different types of eases and options to give you more control over how your animation should behave. It also provides an [Ease Visualizer](https://greensock.com/docs/v3/Eases) to help you choose your preferred ease settings.

There are three types of eases, and they vary in their operations.

1. `in()` &mdash; Motion starts slowly, then picks up the pace toward the end of the animation.
2. `out()` &mdash; The animation starts fast then slows down at the end of the animation.
3. `inOut()` &mdash; The animation begins slow, picks up the pace halfway through, and ends slowly.

{{< codepen height="480" theme_id="light" slug_hash="abNKLaE" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [React GSAP Easing demo](https://codepen.io/smashingmag/pen/abNKLaE) by <a href="https://codepen.io/Beveloper">Blessing Krofegha</a>.{{< /codepen >}}

In these easing example, we chained the tweens that displayed the three types of eases `bounce.in`, `bounce.out` and `bounce.inOut`, and set a delay of the number of seconds it takes the animation to complete before starting the next one only when the component is mounts. This pattern is repetitive, in the next next section we would see how we could use a timeline to do this better.

{{% ad-panel-leaderboard %}}

### Timelines

A [**Timeline**](https://greensock.com/docs/v3/GSAP/Timeline) acts as a container for multiple tweens. It animates tweens in sequential order, and it is not dependent on the duration of the previous tween. Timeline makes it simple to control tweens as a whole and precisely manage their timing.

Timelines can be written by creating an instance of a timeline like so:

<pre><code class="language-javascript">gsap.timeline();</code></pre>

You can also chain multiple tweens to a timeline in two different ways, in the code below:

<div class="break-out">

<pre><code class="language-javascript">##Method 1
const tl = gsap.timeline(); // create an instance and assign it a variable
tl.add(); // add tween to timeline 
tl.to('element', {});
tl.from('element', {});

##Method 2
gsap.timeline()
    .add() // add tween to timeline 
    .to('element', {})
    .from('element', {})</code></pre>
</div>

Let’s recreate the previous example with a timeline:

<div class="break-out">

<pre><code class="language-javascript">const { useRef, useEffect } = React;

const Balls = () => {
    useEffect(() => {      
    const tl = gsap.timeline();
    tl.to('#ball1', {x:1000, ease:"bounce.in", duration: 3})
    tl.to('#ball2', {x:1000, ease:"bounce.out", duration: 3, delay:3 })
    tl.to('#ball3', {x:1000, ease:"bounce.inOut", duration: 3, delay:6 })
  }, []);
}

ReactDOM.render(<Balls />, document.getElementById('app'));</code></pre>
</div>

Inside a `useEffect` hook, we created a variable`(tl)` that holds an instance of a timeline, next we used the `tl` variable to animate our tween in sequential without depending on the previous tween to animate, passing the same properties as it were in the previous example. For the complete code snippet of this demo check the codepen playground below.

{{< codepen height="480" theme_id="light" slug_hash="zYqaEmE" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [React GSAP (Easing with Timeline) demo](https://codepen.io/smashingmag/pen/zYqaEmE) by <a href="https://codepen.io/Beveloper">Blessing Krofegha</a>.{{< /codepen >}}

Now that we have gotten a feel of some the basic building blocks of GSAP, let’s see how we could build a complete animation in a typical React app in the next section.
Let’s begin the flight! 🚀

### Building An Animated Landing Page With React And GSAP

Let’s get to animate a React App. Ensure you [**clone the repo**](https://github.com/smashingmagazine/Animated-page-with-Gsap) before you begin and run `npm install` in order to install the dependencies.

#### What Are We Building?

Currently, our landing page contains a few texts a white background, a menu that doesn’t drop down, with really no animation. The following are what we’ll be adding to the landing page;

- Animate the text and the logo on the homepage, so it eases out when the component is mounted.
- Animate the menu, so it drops down when the menu is clicked.
- Make the images in the gallery page skew `20deg` when the page scrolls.

<figure><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/601a6f43-d3c3-42fe-ae54-d2542d7dbd4b/1-animating-react-components-greensock.gif" alt="Animated Page" /></a><figcaption>Animated page.</figcaption></figure>

Check out the demo on [codesandbox](https://codesandbox.io/s/flamboyant-franklin-toite).

We’ll break the process of our landing page into components, so it will be easy to grasp. Here’s the process;

- Define the animation methods,
- Animate text and logo,
- Toggle menu,
- Make images skew `20deg` on page scroll.

**components**

- `Animate.js` &mdash; Defined all animation methods,
- `Image.js` &mdash; import galley images,
- `Menu.js` &mdash; Contains the menu toggle functionality,
- `Header.js` &mdash; Contains navigation links.

{{% ad-panel-leaderboard %}}

### Define animation methods

Create a `component` folder inside the `src` directory, and create an `animate.js` file. Copy and paste the following code into it.

<pre><code class="language-css">import gsap from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger";
//Animate text 
export const textIntro = elem =&gt; {
  gsap.from(elem, {
    xPercent: -20,
    opacity: 0,
    stagger: 0.2,
    duration: 2,
    scale: -1,
    ease: "back",
  });
};
</code></pre>

Here, we imported `gsap` . We wrote an exported arrow function that animates the text on the landing page. Remember that `gsap.from()` method defines the values an object should be animated from. The function has an `elem` parameter that represents the class which needs to be animated. It takes a few properties and assigns values such as `xPercent: -20` (transforms the object by -20%), gives the object no opacity, makes the object `scale` by `-1`, makes the object `ease` back in `2sec`. 

To see if this works, head over to `App.js` and include the following code.

<div class="break-out">

<pre><code class="language-javascript">...
//import textIntro
import {textIntro} from "./components/Animate"

...
//using useRef hook to access the textIntro DOM
 let intro = useRef(null)
  useEffect(() =&gt; {
    textIntro(intro)
  }, [])

function Home() {
  return (
    &lt;div className='container'&gt;
      &lt;div className='wrapper'&gt;
        &lt;h5 className="intro" ref={(el) =&gt; (intro = el)}&gt;&lt;/h5&gt;
          The &lt;b&gt;SHOPPER&lt;/b&gt;, is a worldclass, innovative, global online ecommerce platform,
          that meets your everyday daily needs.
        &lt;/h5&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}</code></pre>
</div>

Here, we import the `textIntro` method from the `Aminate` component. To access the DOM we used to `useRef` Hook. We created a variable `intro` whose value is set to `null`. Next, inside the `useEffect` hook, we called the `textIntro` method and the `intro` variable. Inside our home component, in the `h5` tag, we defined the `ref` prop and passed in the `intro` variable.

<figure><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d20deea-c368-4a81-a68c-060b6ed23c1c/2-animating-react-components-greensock.gif" alt="Animated text." /></a><figcaption>Animated text.</figcaption></figure>

Next, we have got a menu, but it isn’t dropping down when it’s clicked. Let’s make it work! Inside the `Header.js` Component, add the code below.

<div class="break-out">

<pre><code class="language-javascript">import React, { useState, useEffect, useRef } from "react";
import { withRouter, Link, useHistory } from "react-router-dom";
import Menu from "./Menu";
const Header = () =&gt; {
  const history = useHistory()
  let logo = useRef(null);
  //State of our Menu
  const [state, setState] = useState({
    initial: false,
    clicked: null,
    menuName: "Menu",
  });
  // State of our button
  const [disabled, setDisabled] = useState(false);
  //When the component mounts
  useEffect(() =&gt; {
    textIntro(logo);
    //Listening for page changes.
    history.listen(() =&gt; {
      setState({ clicked: false, menuName: "Menu" });
    });
  }, [history]);
  //toggle menu
  const toggleMenu = () =&gt; {
    disableMenu();
    if (state.initial === false) {
      setState({
        initial: null,
        clicked: true,
        menuName: "Close",
      });
    } else if (state.clicked === true) {
      setState({
        clicked: !state.clicked,
        menuName: "Menu",
      });
    } else if (state.clicked === false) {
      setState({
        clicked: !state.clicked,
        menuName: "Close",
      });
    }
  };
  // check if out button is disabled
  const disableMenu = () =&gt; {
    setDisabled(!disabled);
    setTimeout(() =&gt; {
      setDisabled(false);
    }, 1200);
  };
  return (
    &lt;header&gt;
      &lt;div className="container"&gt;
        &lt;div className="wrapper"&gt;
          &lt;div className="inner-header"&gt;
            &lt;div className="logo" ref={(el) =&gt; (logo = el)}&gt;
              &lt;Link to="/"&gt;SHOPPER.&lt;/Link&gt;
            &lt;/div&gt;
            &lt;div className="menu"&gt;
              &lt;button disabled={disabled} onClick={toggleMenu}&gt;
                {state.menuName}
              &lt;/button&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;Menu state={state} /&gt;
    &lt;/header&gt;
  );
};
export default withRouter(Header);</code></pre>
</div>  

In this component, we defined our menu and button state, inside the `useEffect` hook, we listened for page changes using `useHistory` hook, if the page changes we set the `clicked` and `menuName` state values to `false`  and `Menu` respectively.

To handle our menu, we checked if the value of our initial state is false, if true, we change the value of `initial` , `clicked` and `menuName` to `null`, `true` and `Close`. Else we check if the button is clicked, if true we’d change the `menuName` to `Menu`. Next, we have a `disabledMenu` function that disables our button for `1sec` when it’s clicked.

Lastly, in our `button`, we assigned  `disabled` to `disabled` which is a boolean value that will disable the button when its value is `true`. And the `onClick` handler of the button is tied to the `toggleMenu` function. All we did here was toggle our `menu` text and passed the state to a `Menu` component, which we would create soonest. Let’s write the methods that will make our menu dropdown before creating the actual `Menu` component. Head over to `Animate.js` and paste this code into it.

<pre><code class="language-javascript">....
//Open menu
export const menuShow = (elem1, elem2) =&gt; {
  gsap.from([elem1, elem2], {
    duration: 0.7,
    height: 0,
    transformOrigin: "right top",
    skewY: 2,
    ease: "power4.inOut",
    stagger: {
      amount: 0.2,
    },
  });
};
//Close menu
export const menuHide = (elem1, elem2) =&gt; {
  gsap.to([elem1, elem2], {
    duration: 0.8,
    height: 0,
    ease: "power4.inOut",
    stagger: {
      amount: 0.07,
    },
  });
};
</code></pre>

Here, we have a function called `menuShow`, which skews the menu horizontally by `2degrees`, eases the menu, offset’s the animation using the [`stagger`](https://greensock.com/docs/v3/Staggers) property, and transforms the menu from `right to top` in `0.7sec`, the same properties go for the `menuHide` function. To use these functions, create `Menu.js` file inside the `components` and paste this code into it. 

<div class="break-out">

<pre><code class="language-javascript">import React, {useEffect, useRef} from 'react'
import { gsap } from "gsap"
import { Link } from "react-router-dom"
import {
  menuShow,
  menuHide,
  textIntro,
} from './Animate'
const Menu = ({ state }) =&gt; {
   //create refs for our DOM elements
  
  let menuWrapper = useRef(null)
  let show1 = useRef(null)
  let show2 = useRef(null)
  let info = useRef(null)
  useEffect(() =&gt; {
    // If the menu is open and we click the menu button to close it.
    if (state.clicked === false) {
      // If menu is closed and we want to open it.
      menuHide(show2, show1);
      // Set menu to display none
      gsap.to(menuWrapper, { duration: 1, css: { display: "none" } });
    } else if (
      state.clicked === true ||
      (state.clicked === true && state.initial === null)
    ) {
      // Set menu to display block
      gsap.to(menuWrapper, { duration: 0, css: { display: "block" } });
      //Allow menu to have height of 100%
      gsap.to([show1, show2], {
        duration: 0,
        opacity: 1,
        height: "100%"
      });
      menuShow(show1, show2);
      textIntro(info);
      
    }
  }, [state])
  
  return (
    &lt;div ref={(el) =&gt; (menuWrapper = el)} className="hamburger-menu"&gt;
      &lt;div
        ref={(el) =&gt; (show1 = el)}
        className="menu-secondary-background-color"
      &gt;&lt;/div&gt;
      &lt;div ref={(el) =&gt; (show2 = el)} className="menu-layer"&gt;
        &lt;div className="container"&gt;
          &lt;div className="wrapper"&gt;
            &lt;div className="menu-links"&gt;
              &lt;nav&gt;
                &lt;ul&gt;
                  &lt;li&gt;
                    &lt;Link
                      ref={(el) =&gt; (line1 = el)}
                      to="/about-us"
                    &gt;
                      About
                    &lt;/Link&gt;
                  &lt;/li&gt;
                  &lt;li&gt;
                    &lt;Link
                      ref={(el) =&gt; (line2 = el)}
                      to="/gallery"
                    &gt;
                      Gallery
                    &lt;/Link&gt;
                  &lt;/li&gt;
                  &lt;li&gt;
                    &lt;Link
                      ref={(el) =&gt; (line3 = el)}
                      to="/contact-us"
                    &gt;
                      Contact us
                    &lt;/Link&gt;
                  &lt;/li&gt;
                  
                &lt;/ul&gt;
              &lt;/nav&gt;
              &lt;div ref={(el) =&gt; (info = el)} className="info"&gt;
                &lt;h3&gt;Our Vision&lt;/h3&gt;
                &lt;p&gt;
                  Lorem ipsum dolor sit amet consectetur adipisicing elit....
                &lt;/p&gt;
              &lt;/div&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}
export default Menu</code></pre>
</div>

What we did in the `Menu` component was to import the animated functions, which are `menuShow`, `menuHide`, and `textIntro`. Next, we assigned variables for each created `refs` for our `DOM` elements using the `useRef` hook and passed `null` as their values. Inside the `useEffect` hook, we check for the state of the `menu`, if `clicked` is `false`, we call the `menuHide` function, otherwise, if the `clicked` state is true we call the `menuShow` function. Lastly, we ensured that the `DOM` elements concerned are passed their specific `refs` which are `menuWrapper`, `show1`, `show2`. With that, we’ve got our menu animated.

Let’s see how it looks.

<figure><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dc09854-3f48-4c25-b71a-591770e7d9d9/3-animating-react-components-greensock.gif" alt="Animated Menu." /></a><figcaption>Animated Menu.</figcaption></figure>

The last animation we would implement is make our images in our gallery `skew` when it scrolls. Let’s see the state of our gallery now.

<figure><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1875058b-79f1-4169-8e89-0bd97d5332de/4-animating-react-components-greensock.gif" alt="Gallery without animation." /></a><figcaption>Gallery without animation.</figcaption></figure>

To implement the skew animation on our gallery, let’s head over to `Animate.js` and add a few codes to it.

<div class="break-out">

<pre><code class="language-javascript">....
//Skew gallery Images
export const skewGallery = elem1 => {
  //register ScrollTrigger
  gsap.registerPlugin(ScrollTrigger);
  // make the right edge "stick" to the scroll bar. force3D: true improves performance
    gsap.set(elem1, { transformOrigin: "right center", force3D: true });
    let clamp = gsap.utils.clamp(-20, 20) // don't let the skew go beyond 20 degrees. 
    ScrollTrigger.create({
      trigger: elem1,
      onUpdate: (self) =&gt; {
        const velocity = clamp(Math.round(self.getVelocity() / 300));
        gsap.to(elem1, {
          skew: 0,
          skewY: velocity,
          ease: "power3",
          duration: 0.8,
        });
      },
    });
}</code></pre>
</div>

We created a function called `skewGallery`, passed `elem1` as a param, and registered `ScrollTrigger`.

[**ScrollTrigger**](https://greensock.com/docs/v3/Plugins/ScrollTrigger) is a plugin in GSAP that enables us to trigger scroll-based animations, like in this case of skewing the images while the page scrolls.

To make the right edge stick to the scroll bar we passed `right center` value to the `transformOrigin` property, we also set the `force3D` property to true in other to improve the performance.

We declared a `clamp` variable that calculates our skew and ensures it doesn’t exceed `20degs`. Inside the `ScrollTrigger` object, we assigned the `trigger` property to the `elem1` param, which would be the element that needs to be triggered when we call this function. We have an `onUpdate` callback function, inside it is a `velocity` variable that calculates the current velocity and divides it by `300`.

Lastly, we animate the element from their current values by setting other values. We set `skew` to initially be at `0` and `skewY` to be the `velocity` variable at `0.8`.

Next, we’ve got to call this function in our `App.js` file.

<pre><code class="language-javascript">....
import { skewGallery } from "./components/Animate"
function Gallery() {
  let skewImage = useRef(null);
  useEffect(() =&gt; {
    skewGallery(skewImage)
  }, []);
  return (
    &lt;div ref={(el) =&gt; (skewImage = el)}&gt;
      &lt;Image/&gt;
    &lt;/div&gt;
  )
}

....</code></pre>

Here, we imported `skewGalley` from `./components/Animate`, created a `skewImage` ref that targets the image element. Inside the `useEffect` hook, we called the `skewGallery` function and passed the `skewImage` ref as a param. Lastly, we passed the `skewImage` to the `ref` to attribute.

You’d agree with me it was such a pretty cool journey thus far. Here’s the preview on CodeSanbox 👇

<iframe loading="lazy" src="https://codesandbox.io/embed/react-gsap-animation-toite?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="React-Gsap animation"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

*The supporting repo for this article is available on* [Github](https://github.com/smashingmagazine/Animated-page-with-Gsap).

## Conclusion

We’ve explored the potency of GSAP in a React project, we only scratched the surface in this article, there’s no limit to what you can do with GSAP as it concerns animation.
GSAP’s [official website](https://greensock.com/position-parameter) offers additional tips to help you gain a thorough understanding of methods and plugins. There’s a lot of demos that would blow your mind away with what people have done with GSAP. I’d love to hear your experience with GSAP in the comment section.

### Resources

1. [GSAP Documentation](https://greensock.com/docs/), GreenSock
2. “[The Beginner’s Guide To The GreenSock Animation Platform](https://www.freecodecamp.org/news/the-beginners-guide-to-the-greensock-animation-platform-7dc9fd9eb826/),” Nicholas Kramer, freeCodeCamp
3. “[An Introduction To Animations With Greensock Animation API (GSAP)](https://zellwk.com/blog/gsap/),” Zell Liew
 
{{< signature "ks, ra, yk, il" >}}
