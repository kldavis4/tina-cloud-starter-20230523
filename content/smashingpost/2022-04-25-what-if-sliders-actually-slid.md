---
title: 'What If Our Sliders Actually Slid?'
slug: what-if-sliders-actually-slid-html-element-input-range
author: jhey-tompkins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9d1d14c-98fc-463e-82b5-df98f5556b72/what-if-sliders-actually-slid-html-element-input-range.jpg
date: 2022-04-25T09:30:00.000Z
summary: >-
  In this article, Jhey Tompkins explores one of GreenSocks’ newest plugins alongside React to create an impractical whimsical spin on a well-known native element: `<input type="range"/>`.
description: >-
  In this article, Jhey Tompkins explores one of GreenSocks’ newest plugins alongside React to create an impractical whimsical spin on a well-known native element: `<input type="range"/>`.
categories:
  - HTML
  - Coding
  - Techniques
---

One of my main mantras is using “Creative Coding” to level up your skills. It’s one of the main reasons I have gotten to where I am. But when so much of the web is very “set in its way”, it takes a little more for us to think “outside the box” and have fun!

{{< codepen height="480" theme_id="light" slug_hash="mdpYwZW" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [“Think” Outside The Box Toggle w/ CSS @property ✨](https://codepen.io/smashingmag/pen/mdpYwZW) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}  

It’s a muscle that you can train for sure. To have your ideas become more than ideas. To not get deterred by practicality.

Today, we’re going to do all those things. Let’s have some fun and think outside the box with a native HTML element. What if our sliders (`<input type="range"/>`) actually slid?

Today’s weapon of choice? GreenSock.

[GreenSock](https://greensock.com) has some of the best plugins and utilities that are perfect for our task. The idea for our whimsical slider is to respect physics &mdash; those being inertia and momentum. GreenSock has some awesome plugins for this. I’m thinking of the “Draggable” and “Inertia” plugins to start with.

For today, let’s make this a React component too. Let’s start by creating a component that renders the `input` for us:

<pre><code class="language-javascript">import React from 'https://cdn.skypack.dev/react'
import ReactDOM from 'https://cdn.skypack.dev/react-dom'

const ROOT_NODE = document.querySelector('#app')

const SlideySlider = ({ min = 0, max = 100, step = 1, value = 0}) =&gt; {
  return (
    &lt;input type="range" min={min} max={max} step={step} value={value} /&gt;
  )
}

const App = () =&gt; &lt;SlideySlider value={gsap.utils.random(0, 100)}/&gt;

ReactDOM.render(&lt;App/&gt;, ROOT_NODE)</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="YzYLeJo" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [1. Rendering our Slider Component](https://codepen.io/smashingmag/pen/YzYLeJo) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}  

We have a component that accepts props for the standard “range” attributes. But we can’t update the `value`. We aren’t updating that `value` anywhere. Keeping the `input` uncontrolled for this demo makes sense. We could keep the value in the state of the parent component. And any changes we make, we can send back up to the parent. Let’s change it so that the `value` we pass gets used as the `defaultValue`:

<div class="break-out">

<pre><code class="language-javascript">const SlideySlider = ({ min = 0, max = 100, step = 1, value = 0}) =&gt; {
  return (
    &lt;input type="range" min={min} max={max} step={step} defaultValue={value} /&gt;
  )
}</code></pre>
</div>

{{< codepen height="480" theme_id="light" slug_hash="wvpjyOz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [1.b. Changing to Uncontrolled](https://codepen.io/smashingmag/pen/wvpjyOz) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Now we can change the `input` value, but its value isn’t getting tracked anywhere. We’ll come back to syncing the `value` up later on.

Now let’s bring in [Draggable](https://greensock.com/docs/v3/Plugins/Draggable) to get things progressing. Any setup code, etc. we run inside an effect with `React.useEffect`. Now you might think to make our `Draggable`, we reach straight for this:

<pre><code class="language-javascript">const SlideySlider = ({
  min = 0,
  max = 100,
  step = 1,
  value = 0
}) =&gt; {

  React.useEffect(() =&gt; {
    Draggable.create('input', {
      type: 'x',
    })
  }, []);

  return (
    &lt;input
      type="range"
      min={min}
      max={max}
      step={step}
      defaultValue={value}
    /&gt;
  );
};</code></pre>

But that would make the input itself Draggable. Which makes for an interesting user experience!

{{< codepen height="480" theme_id="light" slug_hash="WNdJMqj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [2. Adding Draggable 😮](https://codepen.io/smashingmag/pen/WNdJMqj) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Instead, we could use a little trick I picked up when making this demo for a [Tuggable Light Bulb](https://codepen.io/jh3y/pen/VwjgdLj):

{{< codepen height="480" theme_id="light" slug_hash="gOozvVP" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Tuggable Light Bulb! 💡(GSAP Draggable &amp;&amp; MorphSVG)](https://codepen.io/smashingmag/pen/gOozvVP) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

The idea is that we can create a proxy element for our `Draggable`. That gets “fake dragged” when we interact with our input because of the `trigger` property. The `trigger`  property tells us to initiate dragging when interacting with our `input`. Note how we are also limiting the drag to the `x-axis` with the `type` property:

<pre><code class="language-javascript">const SlideySlider = ({
  min = 0,
  max = 100,
  step = 1,
  value = 0
}) =&gt; {
  const proxy = React.useRef(document.createElement('div'))
  const inputRef = React.useRef(null)

  React.useEffect(() =&gt; {
    Draggable.create(proxy.current, {
      trigger: inputRef.current,
      type: 'x',
    })
  }, []);

  return (
    &lt;input
      ref={inputRef}
      type="range"
      min={min}
      max={max}
      step={step}
      defaultValue={value}
    /&gt;
  );
};</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="PoEeRoz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [3. Attaching Draggable via Proxy](https://codepen.io/smashingmag/pen/PoEeRoz) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Now we have `Draggable` in place, it’s time to make use of the `Inertia` plugin. This will allow us to track the velocity of our dragging. With that velocity, we can animate the value of our input based on the momentum of our sliding:

<pre><code class="language-javascript">React.useEffect(() =&gt; {
  const PROXY_PROPS = gsap.getProperty(proxy.current)
  const TRACKER = InertiaPlugin.track(proxy.current, 'x')[0]
  
  const slide = () =&gt; {
    gsap.to(inputRef.current, {
      inertia: {
        value: TRACKER.get('x'),
      },
    })
  }
  
  Draggable.create(proxy.current, {
    trigger: inputRef.current,
    type: 'x',
    onPress: () =&gt; {
      gsap.killTweensOf(inputRef.current)
    },
    onDragEnd: slide,
  })
}, []);</code></pre>

With this solution we need to ensure we kill any tweens on the input `onPress`. That way we don’t interrupt or block the user from interacting with the `input`:

<pre><code class="language-javascript">onPress: () =&gt; {
  gsap.killTweensOf(inputRef.current)
},</code></pre>

Once we’ve made those updates, we have the foundations of our `SlideySlider`!

{{< codepen height="480" theme_id="light" slug_hash="MWrGVwV" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [4. A Basic Slide ✨](https://codepen.io/smashingmag/pen/MWrGVwV) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

It’s very slidey! A little too slidey. But we can revisit the friction, as we go. At this stage, we’ve also added a `label` for the input, and we are “controlling” the `input` value in the parent component:

<pre><code class="language-javascript">const App = () =&gt; {
  const [value, setValue] = React.useState(gsap.utils.random(0, 100, 1))  
  return (
    &lt;&gt;
      &lt;label htmlFor="slidey"&gt;{value}&lt;/label&gt;
      &lt;SlideySlider value={value} id="slidey" /&gt;
    &lt;/&gt;
  )
}</code></pre>

We aren’t done there. If you throw a ball against a wall, does it hit the wall and stop? No! So, why should the thumb for our input?

{{% feature-panel %}}

The trick is to check the input value on an update, as we animate. We know the `min` and `max` values for our `input`. If the value hits one of them, we know that we are going to bounce in the opposite direction:

<pre><code class="language-javascript">const checkForBounce = () =&gt; {
  let vx = TRACKER.get('x')
  const current = parseInt(inputRef.current.value, 10)

  if (Math.abs(vx) !== 0 && (current === max || current === min)) {
    vx &#42;= FRICTION
    slide(vx)
  }
}
    
const slide = vx =&gt; {
  let value = vx !== undefined ? vx : TRACKER.get('x')
  gsap.to(inputRef.current, {
    overwrite: true,
    inertia: {
      value,
      resistance: 200,
    },
    onUpdate: checkForBounce,
  })
}</code></pre>

But that doesn’t work! It starts to work.

{{< codepen height="480" theme_id="light" slug_hash="popVLga" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [5. Handling the &quot;Bounce&quot;](https://codepen.io/smashingmag/pen/popVLga) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Though after one bounce, it gives up. This confused me at first, because of this demo from the GSAP docs. Throw that ball around.

{{< codepen height="480" theme_id="light" slug_hash="popVLga" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [5. Handling the &quot;Bounce&quot;](https://codepen.io/smashingmag/pen/popVLga) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

{{< codepen height="480" theme_id="light" slug_hash="WNdaGqJ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Draggable Bounce](https://codepen.io/smashingmag/pen/WNdaGqJ) by <a href="https://codepen.io/osublake">Blake Bowen</a>.{{< /codepen >}}

What about wrapping the `input` with a `div`? And then using another element as a proxy handle? If we try using a “fake” proxy handle, it “can” work. It’s also an easy way to increase the thumb size. But now we’re trying to sync the input value to the thumb which isn’t ideal. It kinda puts the control in the opposite direction.

{{< codepen height="480" theme_id="light" slug_hash="XWVqENo" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [6. Using Proxy Drag Handle](https://codepen.io/smashingmag/pen/XWVqENo) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Notice how the “Handle” doesn’t stay centered on the input thumb. Also, if you were to click the track and start dragging, we wouldn’t get our slide. This is because we would have to tell our handle to start dragging with “[startDrag](https://greensock.com/docs/v3/Plugins/Draggable/startDrag())”. But it would work! 🙌

So, why didn’t it work without the proxy handle then? Well, it’s a case of things being a little too quick for our scenario.

<blockquote>“The main problem was that inertia tracking by its very nature is time-dependent, meaning it sorta keeps track of a certain amount of history so that it can do the calculations. You were creating a scenario where you inverted the velocity via a tween, but it took a little time for that to actually get reflected in the tracked velocity (as it should). So, let’s say it’s moving super fast in one direction, so maybe 3000px/s and then you suddenly start moving it in the opposite direction at half the speed, but it’s taking data points once every tick and must average them out &mdash; if it hits the other limit quickly enough, it’ll still have some historical data from when it was going 3000px/s that offsets things. So in your case, that’d result in it still being a positive velocity and you were multiplying it by a negative, thus heading in the same direction as before.”<br /><br />&mdash; <a href="https://greensock.com/forums/topic/31365-momentum-based-range-input-with-draggable/#comment-157941">Jack @ GreenSock</a></blockquote>

Jack did suggest another way to implement things by using another GSAP utility [`wrapYoyo`](https://greensock.com/docs/v3/GSAP/UtilityMethods/wrapYoyo()). This does give us the effect we are after. It also reduces the code significantly. But it lacks a couple of features that I’d like for other ideas I had for our slider.

{{< codepen height="480" theme_id="light" slug_hash="GRyaaWP" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Jack’s Solution ✨](https://codepen.io/smashingmag/pen/GRyaaWP) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Those being how to detect when we hit a side? And also we don’t want any velocity when we click the track away from the thumb. If you click the track further away from the thumb in that demo, you’ll get distance-based velocity.

So, what do we do? Well, the timing couldn’t have been better. With the latest version of GSAP (3.10 at the time of writing), [a new plugin is now available](https://greensock.com/docs/v3/Plugins/Observer). The “[Observer](https://greensock.com/docs/v3/Plugins/Observer)” plugin allows developers to tap into interaction events. And the callback system means you can grab things like the velocity on a certain axis. This is perfect for what we are trying to do.

I was fortunate to get early access to this plugin. But I hadn’t considered this use case until Jack mentioned it. I did make a spinny globe with React and ThreeJS &mdash; let me know if you want an article about how to do that! 🙌

{{< codepen height="480" theme_id="light" slug_hash="VwyxXXa" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Spinning Globe 🌎 w/ GSAP ScrollTrigger.Observe](https://codepen.io/smashingmag/pen/VwyxXXa) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Let’s start again with our `SlideySlider` component.

{{< codepen height="480" theme_id="light" slug_hash="rNpvddR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [7. Starting Over](https://codepen.io/smashingmag/pen/rNpvddR) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

<pre><code class="language-javascript">const SlideySlider = ({
  id,
  min = 0,
  max = 100,
  step = 1,
  value = 0,
}) =&gt; {

  const inputRef = React.useRef(null)

  React.useEffect(() =&gt; {

  }, []);

  return (
    &lt;input
      id={id}
      ref={inputRef}
      type="range"
      min={min}
      max={max}
      step={step}
      defaultValue={value}
    /&gt;
  );
};</code></pre>

This time we aren’t going to use `Draggable` and track the invisible proxy. Instead, we will track the `value` of the `input` with the `InertiaPlugin`. And then we can use the new `Observer` plugin to catch the “drag”.

{{% ad-panel-leaderboard %}}

Let’s start with that tracking within an effect:

<pre><code class="language-javascript">React.useEffect(() =&gt; {
  InertiaPlugin.track(inputRef.current, "value");
}, []);</code></pre>

Here we are tracking the `value` on the `input`. And this means we can tween the `value` of the `input` with a value of `auto` where the plugin will calculate it for us. See [the docs for more](https://greensock.com/docs/v3/Plugins/InertiaPlugin/static.track()) on this.

Here comes the important bit &mdash; setting up the `Observer`:

<pre><code class="language-javascript">React.useEffect(() =&gt; {
  InertiaPlugin.track(inputRef.current, "value");

  Observer.create({
    target: inputRef.current,
    type: "touch,pointer",
    dragMinimum: 3,
    onPress: () =&gt; tweenRef.current && tweenRef.current.kill(),
    onDragEnd: () =&gt; {
      tweenRef.current = gsap.to(inputRef.current, {
        inertia: {
          resistance: 200,
          value: "auto"
        }
      });
    }
  });
}, []);</code></pre>

We are telling the `Observer` to watch any `touch` or `pointer` events on the `input`. If we drag at least 3 pixels, this gets considered a drag. We keep a reference to the sliding tween so that we can destroy it whenever we interact with the `input`. This means we can click the track anywhere, and there will be no inertia or velocity to deal with. Once we’ve finished dragging, we can tween the `value` of the `input` based on the velocity at which we dragged. This is great!

{{< codepen height="480" theme_id="light" slug_hash="vYpjRQg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [8. Basic Observer Integration 🙌](https://codepen.io/smashingmag/pen/vYpjRQg) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

All we need now is that bounce! How can we animate the bounce instead of it stopping dead? And also, how do we detect when there is a bounce?

This is where that `wrapYoyo` utility we mentioned earlier comes into play. [Given two parameters (or an Array of values)](https://greensock.com/docs/v3/GSAP/UtilityMethods/wrapYoyo()), we create a wrapping function that can calculate a value for us. In our case, this is the `min` and `max` for our `input` element:

<pre><code class="language-javascript">const WRAP = gsap.utils.wrapYoyo(min, max)</code></pre>

How do we use this? Well, we can make use of the “[Modifiers](https://greensock.com/docs/v3/GSAP/CorePlugins/ModifiersPlugin)” plugin. This allows us to intercept values that GSAP is going to use and run our own custom logic before returning a value. Let’s get the bounce working first. Using a `modifier`, we can wrap the `auto` defined `value` for our `input`:

<pre><code class="language-javascript">const WRAP = gsap.utils.wrapYoyo(min, max)
Observer.create({
  target: inputRef.current,
  type: "touch,pointer",
  dragMinimum: 3,
  onPress: () =&gt; tweenRef.current && tweenRef.current.kill(),
  onDragEnd: () =&gt; {
    tweenRef.current = gsap.to(inputRef.current, {
      inertia: {
        resistance: 200,
        value: "auto"
      },
      modifiers: {
        value: v =&gt; WRAP(v)
      }
    });
  }
});</code></pre>

It’s as easy as that! Boom!

{{< codepen height="480" theme_id="light" slug_hash="xxpjWBG" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [9. Animating the Bounce!](https://codepen.io/smashingmag/pen/xxpjWBG) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Now to detect a collision. There’s a nifty little way to do this. At the end of each drag, we can detect the number of bounces by dividing the inertia value by the `max` value. Then if the number changes, we know we’ve had a bounce! We can also tap into the `Inertia` tracking to get the current value and work out which side is being bounced.

Update our `track` to instantiate a variable. Note how we are setting, as the first value of the `Array` returned:

<div class="break-out">

<pre><code class="language-javascript">const TRACKER = InertiaPlugin.track(inputRef.current, "value")[0];</code></pre>
</div>

Then update our `onDragEnd` as follows:

<div class="break-out">

<pre><code class="language-javascript">onDragEnd: () =&gt; {
  let lastCycle = 0;
  tweenRef.current = gsap.to(inputRef.current, {
    inertia: {
      resistance: 200,
      value: "auto"
    },
    modifiers: {
      value: (v) =&gt; {
        const cycle = Math.floor(v / max);
        if (cycle !== lastCycle) {
          // Bounce!!!
          console.info(`BOUNCE ${TRACKER.get('value') &lt; 0 ? 'LEFT' : 'RIGHT'}`);
        }
        // Update the cycle count
        lastCycle = cycle;
        return WRAP(v);
      }
    }
  });
}</code></pre>
</div>

Now we can start doing some more fun things with it!

How about if we bumped the sides a little based on the velocity? Well, as we can detect which side is getting knocked, we can also tween the `input` itself. Let’s update our `modifiers` code:

<pre><code class="language-javascript">modifiers: {
  value: (v) =&gt; {
    const cycle = Math.floor(v / max);

    if (cycle !== lastCycle) {
      // Bounce!!!
      const vx = TRACKER.get("value");
      const xPercent = gsap.utils.clamp(
        -bump,
        bump,
        gsap.utils.mapRange(-600, 600, -bump, bump, vx)
      );
      gsap.to(inputRef.current, {
        xPercent,
        yoyo: true,
        repeat: 1
      });
    }
    // Update the cycle count
    lastCycle = cycle;
    return WRAP(v);
  }
}</code></pre>

The idea is that if we bounce, we can calculate an `xPercent` to animate our `input` by. To do that, we can use another GSAP utility &mdash; `mapRange`. Given some velocity, map an input range to an output range. And we can clamp the value with `gsap.utils.clamp`. For our `xPercent` value, we are clamping a `bump` value (set to `10` in the component props). Then we are mapping the input range `-600` to `600` against `-10` to `10`. We pass the current velocity (`vx`) into that and `clamp` the result. The number `600` could also be configured via the component props if we wish:

<pre><code class="language-javascript">const xPercent = gsap.utils.clamp(
  -bump,
  bump,
  gsap.utils.mapRange(-600, 600, -bump, bump, vx)
);</code></pre>

Translating alone won’t look great. There are some extra things we can do to make this “feel” better. We could make the `duration` of that animation be dependent on the velocity too. Again, these numbers could be configured via `props`:

<pre><code class="language-javascript">const duration = gsap.utils.clamp(
  0.05,
  0.2,
  gsap.utils.mapRange(0, 600, 0.2, 0.05, Math.abs(vx))
);</code></pre>

And how about if we play a knocking noise at the start of the animation? We could set the volume based on the velocity:

<pre><code class="language-javascript">const volume = gsap.utils.clamp(
  0.1,
  1,
  gsap.utils.mapRange(0, 600, 0, 1, Math.abs(vx))
)</code></pre>

These values are then used to animate the `input` element. Notice how we use `yoyo` with `repeat: 1` to return the `input` to its original position. We also reset the audio and play it on each `onStart`:

<pre><code class="language-javascript">gsap.to(inputRef.current, {
  onStart: () =&gt; {
    KNOCK.pause()
    KNOCK.currentTime = 0
    KNOCK.volume = volume
    KNOCK.play()
  },
  xPercent,
  duration,
  yoyo: true,
  repeat: 1
});</code></pre>

Awesome!

{{< codepen height="480" theme_id="light" slug_hash="eYyrrmq" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [11. Add Some Whimsy! ✨](https://codepen.io/smashingmag/pen/eYyrrmq) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

Now we’ve got a little whimsy in, let’s get practical. We need the value to be in sync with whatever `React` state we have in place. It’d be neat to keep a `label` value in sync too. We can do that!

{{% ad-panel-leaderboard %}}

Let’s start by updating the parent component:

<pre><code class="language-javascript">const App = () =&gt; {
  const labelRef = React.useRef(null)
  const [value, setValue] = React.useState(gsap.utils.random(0, 100, 1));

  return (
    &lt;&gt;
      &lt;label htmlFor="slidey" ref={labelRef}&gt;{value}&lt;/label&gt;
      &lt;SlideySlider
        id="slidey"
        value={value}
        labelRef={labelRef}
        onChange={setValue}
      /&gt;
      &lt;span&gt;{`State value: ${value}`}&lt;/span&gt;
    &lt;/&gt;
  );
};</code></pre>

We’re controlling the `input` value in this `App` component. We are also going to pass a `labelRef` and an `onChange` prop to our `SlideySlider`. The first prop gives our slider access to the `label` element. The second provides a way for our `SlideySlider` to communicate `value` changes. We also have a `span` in place to show you when the `state` is getting updated.

The key is using an `onChange` handler like we usually would. But we also need to invoke that `onChange` handler at the end of our sliding tween.

Here’s the updated `render` using the `onChange` prop:

<pre><code class="language-javascript">return (
  &lt;input
    id={id}
    ref={inputRef}
    onChange={e =&gt; onChange(e.target.value)}
    type="range"
    min={min}
    max={max}
    step={step}
    defaultValue={value}
  /&gt;
);</code></pre>

And we can add an `onComplete` inside our `onDragEnd` tween:

<pre><code class="language-javascript">onDragEnd: () =&gt; {
  let lastCycle = 0;
  tweenRef.current = gsap.to(inputRef.current, {
    inertia: {
      resistance: 200,
      value: "auto"
    },
    onComplete: () =&gt; {
      if (onChange) onChange(inputRef.current.value)
    },
    /&#42; Rest of tween &#42;/
  }
  /&#42; Rest of onDragEnd &#42;/
}</code></pre>

The last piece is to `set` the visual value of the `label` as we animate. Inside our `value` modifier we can use `gsap.set` if we have a `labelRef` to use:

<div class="break-out">

<pre><code class="language-javascript">if (labelRef.current) gsap.set(labelRef.current, { innerText: Math.floor(WRAP(v)) })</code></pre>
</div>

And now we are keeping everything in sync!

{{< codepen height="480" theme_id="light" slug_hash="XWVqqjb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [12. Syncing Values](https://codepen.io/smashingmag/pen/XWVqqjb) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

And that’s it! What if our sliders actually slid? Well, I guess we have an idea now! What else could we do with this? What other input controls could have “interesting” behavior?

{{< codepen height="480" theme_id="light" slug_hash="bGaMMwm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [What if Sliders actually slid?  ✨ (GSAP Observer)](https://codepen.io/smashingmag/pen/bGaMMwm) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

We can do so much with the code, and the web platform is always evolving. The only limit is our imagination, not the tech stack we bring it to life with. But collaboration is the key. Hop in some forums, ask some questions, have fun! And most importantly, stay awesome! ʕ •ᴥ•ʔ

### Further Reading And Resources

- [The Whimsical Web](https://whimsical.club)  
*A curated list of sites with an extra bit of fun.*
- “[In Defense Of A Fussy Website](https://css-tricks.com/in-defense-of-a-fussy-website/),” Sarah Drasner, CSS-Tricks
- “[Playfulness In Code: Supercharge Your Learning By Having Fun](https://www.smashingmagazine.com/2020/11/playfulness-code-supercharge-fun-learning/),” Jhey Tompkins, Smashing Magazine

{{< signature "vf, yk, il" >}}
