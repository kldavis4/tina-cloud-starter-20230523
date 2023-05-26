---
title: '3D CSS Flippy Snaps With React And GreenSock'
slug: 3d-css-flippy-snaps-react-greensock
author: jhey-tompkins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a865f227-d5a1-4a63-a889-288a84fa2bce/3d-css-flippy-snaps-react-greensock.jpg
date: 2021-11-29T12:30:00.000Z
summary: >-
  One of Jhey’s main mantras is to make learning fun.  In this article, he shows you ways to level up your skills by bringing your ideas to life, and not forgetting that [you can be playful with code](https://www.smashingmagazine.com/2020/11/playfulness-code-supercharge-fun-learning/). With that mindset, every idea is bound to become an opportunity to try something new.
description: >-
  One of Jhey’s main mantras is to make learning fun.  In this article, he shows you ways to level up your skills by bringing your ideas to life, and not forgetting that [you can be playful with code](https://www.smashingmagazine.com/2020/11/playfulness-code-supercharge-fun-learning/). With that mindset, every idea is bound to become an opportunity to try something new.
categories:
  - CSS
  - React
  - Tools
  - Apps
  - Techniques
---

Naming things is hard, right? Well, “Flippy Snaps” was the best thing I could come up with. 😂 I saw an effect like this on TV one evening and made a note to myself to make something similar.

Although this isn’t something I’d look to drop on a website any time soon, it’s a neat little challenge to make. It fits in with my whole stance on “[Playfulness in Code](https://www.smashingmagazine.com/2020/11/playfulness-code-supercharge-fun-learning/)” to learn. Anyway, a few days later, I sat down at the keyboard, and a couple of hours later I had this:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">3D CSS Flippy Snaps ✨<br><br>Tap to flip for another image 👇<br><br>⚒️ <a href="https://twitter.com/reactjs?ref_src=twsrc%5Etfw">@reactjs</a> &amp;&amp; <a href="https://twitter.com/greensock?ref_src=twsrc%5Etfw">@greensock</a> <br>👉 <a href="https://t.co/Na14z40tHE">https://t.co/Na14z40tHE</a> via <a href="https://twitter.com/CodePen?ref_src=twsrc%5Etfw">@CodePen</a> <a href="https://t.co/nz6pdQGpmd">pic.twitter.com/nz6pdQGpmd</a></p>&mdash; Jhey 🐻🛠️✨ (@jh3yy) <a href="https://twitter.com/jh3yy/status/1457830342413455369?ref_src=twsrc%5Etfw">November 8, 2021</a></blockquote>

My final demo is a React app, but we don’t need to dig into using React to explain the mechanics of making this work. We will create the React app once we’ve established how to make things work.

**Note**: *Before we get started. It’s worth noting that the performance of this demo is affected by the grid size and the demos are best viewed in Chromium-based browsers.*

Let’s start by creating a grid. Let’s say we want a 10 by 10 grid. That’s 100 cells (This is why React is handy for something like this). Each cell is going to consist of an element that contains the front and back for a flippable card.

<pre><code class="language-javascript">&lt;div class="flippy-snap"&gt;
  &lt;!-- 100 of these --&gt;
  &lt;div class="flippy-snap__card flippy-card"&gt;
    &lt;div class="flippy-card__front&gt;&lt;/div&gt;
    &lt;div class="flippy-card__rear&gt;&lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

The styles for our grid are quite straightforward. We can use `display: grid` and use a custom property for the grid size. Here we are defaulting to `10`.

<pre><code class="language-javascript">.flippy-snap {
  display: grid;
  grid-gap: 1px;
  grid-template-columns: repeat(var(--grid-size, 10), 1fr);
  grid-template-rows: repeat(var(--grid-size, 10), 1fr);
}</code></pre>

We won’t use `grid-gap` in the final demo, but, it’s good for seeing the cells easier whilst developing.

{{< codepen height="480" theme_id="light" slug_hash="porXNzB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [1. Creating a Grid](https://codepen.io/smashingmag/pen/porXNzB) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

Next, we need to style the sides of our cards and display images. We can do this by leveraging inline CSS custom properties. Let’s start by updating the markup. We need each card to know its `x` and `y` position in the grid.

<pre><code class="language-javascript">&lt;div class="flippy-snap"&gt;
  &lt;div class="flippy-snap__card flippy-card" style="--x: 0; --y: 0;"&gt;
    &lt;div class="flippy-card__front"&gt;&lt;/div&gt;
    &lt;div class="flippy-card__rear"&gt;&lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="flippy-snap__card flippy-card" style="--x: 1; --y: 0;"&gt;
    &lt;div class="flippy-card__front"&gt;&lt;/div&gt;
    &lt;div class="flippy-card__rear"&gt;&lt;/div&gt;
  &lt;/div&gt;
  &lt;!-- Other cards --&gt;
&lt;/div&gt;</code></pre>

For the demo, I'm using `Pug` to generate this for me. You can see the compiled HTML by clicking “View Compiled HTML” in the demo.

<pre><code class="language-javascript">- const GRID_SIZE = 10
- const COUNT = Math.pow(GRID_SIZE, 2)
.flippy-snap
  - for(let f = 0; f < COUNT; f++)
    - const x = f % GRID_SIZE  
    - const y = Math.floor(f / GRID_SIZE)
    .flippy-snap__card.flippy-card(style=`--x: ${x}; --y: ${y};`)
      .flippy-card__front
      .flippy-card__rear</code></pre>

Then we need some styles. 

<pre><code class="language-javascript">.flippy-card {
  --current-image: url("https://random-image.com/768");
  --next-image: url("https://random-image.com/124");
  height: 100%;
  width: 100%;
  position: relative;
}
.flippy-card__front,
.flippy-card__rear {
  position: absolute;
  height: 100%;
  width: 100%;
  backface-visibility: hidden;
  background-image: var(--current-image);
  background-position: calc(var(--x, 0) * -100%) calc(var(--y, 0) * -100%);
  background-size: calc(var(--grid-size, 10) * 100%);
}
.flippy-card__rear {
  background-image: var(--next-image);
  transform: rotateY(180deg) rotate(180deg);
}</code></pre>

The rear of the card gets its position using a combination of rotations via `transform`. But, the interesting part is how we show the image part for each card. In this demo, we are using a custom property to define the URLs for two images. And then we set those as the `background-image` for each card face.

{{% feature-panel %}}

But the trick is how we define the `background-size` and `background-position`. Using the custom properties `--x` and `--y` we multiply the value by `-100%`. And then we set the `background-size` to `--grid-size` multiplied by `100%`. This gives displays the correct part of the image for a given card.

{{< codepen height="480" theme_id="light" slug_hash="gOxNLPz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [2. Adding an Image](https://codepen.io/smashingmag/pen/gOxNLPz) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

You may have noticed that we had `--current-image` and `--next-image`. But, currently, there is no way to see the next image. For that, we need a way to flip our cards. We can use another custom property for this.

Let’s introduce a `--count` property and set a `transform` for our cards:

<pre><code class="language-javascript">.flippy-snap {
  --count: 0;
  perspective: 50vmin;
}
.flippy-card {
  transform: rotateX(calc(var(--count) * -180deg));
  transition: transform 0.25s;
  transform-style: preserve-3d;
}</code></pre>

We can set the `--count` property on the containing element. Scoping means all the cards can pick up that value and use it to `transform` their rotation on the x-axis. We also need to set `transform-style: preserve-3d` so that we see the back of the cards. Setting a `perspective` gives us that 3D perspective.

This demo lets you update the `--count` property value so you can see the effect it has.

{{< codepen height="480" theme_id="light" slug_hash="LYjKbZW" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [3. Turning Cards](https://codepen.io/smashingmag/pen/LYjKbZW) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

At this point, you could wrap it up there and set a simple click handler that increments `--count` by one on each click.

<pre><code class="language-javascript">const SNAP = document.querySelector('.flippy-snap')
let count = 0
const UPDATE = () =&gt; SNAP.style.setProperty('--count', count++)
SNAP.addEventListener('click', UPDATE)</code></pre>

Remove the `grid-gap` and you’d get this. Click the snap to flip it.

{{< codepen height="480" theme_id="light" slug_hash="eYEwBdN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [4. Boring Flips](https://codepen.io/smashingmag/pen/eYEwBdN) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

Now we have the basic mechanics worked out, it’s time to turn this into a React app. There’s a bit to break down here.

<pre><code class="language-javascript">const App = () =&gt; {
  const [snaps, setSnaps] = useState([])
  const [disabled, setDisabled] = useState(true)
  const [gridSize, setGridSize] = useState(9)
  const snapRef = useRef(null)

  const grabPic = async () =&gt; {
    const pic = await fetch('https://source.unsplash.com/random/1000x1000')
    return pic.url
  }

  useEffect(() =&gt; {
    const setup = async () =&gt; {
      const url = await grabPic()
      const nextUrl = await grabPic()
      setSnaps([url, nextUrl])
      setDisabled(false)
    }
    setup()
  }, [])

  const setNewImage = async count =&gt; {
    const newSnap = await grabPic()
    setSnaps(
      count.current % 2 !== 0 ? [newSnap, snaps[1]] : [snaps[0], newSnap]
    )
    setDisabled(false)
  }

  const onFlip = async count =&gt; {
    setDisabled(true)
    setNewImage(count)
  }

  if (snaps.length !== 2) return &lt;h1 className="loader"&gt;Loading...&lt;/h1&gt;

  return (
    &lt;FlippySnap
      gridSize={gridSize}
      disabled={disabled}
      snaps={snaps}
      onFlip={onFlip}
      snapRef={snapRef}
    /&gt;
  )
}</code></pre>

Our `App` component handles grabbing images and passing them to our `FlippySnap` component. That’s the bulk of what’s happening here. For this demo, we’re grabbing images from [Unsplash](https://source.unsplash.com).

<pre><code class="language-javascript">const grabPic = async () =&gt; {
  const pic = await fetch('https://source.unsplash.com/random/1000x1000')
  return pic.url
}

// Initial effect grabs two snaps to be used by FlippySnap
useEffect(() =&gt; {
  const setup = async () =&gt; {
    const url = await grabPic()
    const nextUrl = await grabPic()
    setSnaps([url, nextUrl])
    setDisabled(false)
  }
  setup()
}, [])</code></pre>

If there aren’t two snaps to show, then we show a “Loading...” message.

<pre><code class="language-javascript">if (snaps.length !== 2) return &lt;h1 className="loader"&gt;Loading...&lt;/h1&gt;</code></pre>

If we are grabbing a new image, we need to disable `FlippySnap` so we can’t spam-click it.

<pre><code class="language-javascript">&lt;FlippySnap
  gridSize={gridSize}
  disabled={disabled} // Toggle a "disabled" prop to stop spam clicks
  snaps={snaps}
  onFlip={onFlip}
  snapRef={snapRef}
/&gt;</code></pre>

We’re letting `App` dictate the snaps that get displayed by `FlippySnap` and in which order. On each flip, we grab a new image, and depending on how many times we’ve flipped, we set the correct snaps. The alternative would be to set the snaps and let the component figure out the order.

<pre><code class="language-javascript">const setNewImage = async count =&gt; {
  const newSnap = await grabPic() // Grab the snap
  setSnaps(
    count.current % 2 !== 0 ? [newSnap, snaps[1]] : [snaps[0], newSnap]
  ) // Set the snaps based on the current "count" which we get from FlippySnap
  setDisabled(false) // Enable clicks again
}

const onFlip = async count =&gt; {
  setDisabled(true) // Disable so we can't spam click
  setNewImage(count) // Grab a new snap to display
}</code></pre>

How might `FlippySnap` look? There isn’t much to it at all!

<pre><code class="language-javascript">const FlippySnap = ({ disabled, gridSize, onFlip, snaps }) =&gt; {
  const CELL_COUNT = Math.pow(gridSize, 2)
  const count = useRef(0)

  const flip = e =&gt; {
    if (disabled) return
    count.current = count.current + 1
    if (onFlip) onFlip(count)
  }

  return (
    &lt;button
      className="flippy-snap"
      ref={containerRef}
      style={{
        '--grid-size': gridSize,
        '--count': count.current,
        '--current-image': `url('${snaps[0]}')`,
        '--next-image': `url('${snaps[1]}')`,
      }}
      onClick={flip}&gt;
      {new Array(CELL_COUNT).fill().map((cell, index) =&gt; {
        const x = index % gridSize
        const y = Math.floor(index / gridSize)
        return (
          &lt;span
            key={index}
            className="flippy-card"
            style={{
              '--x': x,
              '--y': y,
            }}&gt;
            &lt;span className="flippy-card__front"&gt;&lt;/span&gt;
            &lt;span className="flippy-card__rear"&gt;&lt;/span&gt;
          &lt;/span&gt;
        )
      })}
    &lt;/button&gt;
  )
}</code></pre>

The component handles rendering all the cards and setting the inline custom properties. The `onClick` handler for the container increments the `count`. It also triggers the `onFlip` callback. If the state is currently `disabled`, it does nothing. That flip of the `disabled` state and grabbing a new snap triggers the flip when the component re-renders.

{{< codepen height="480" theme_id="light" slug_hash="wvqLdGY" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [5. React Foundation](https://codepen.io/smashingmag/pen/wvqLdGY) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

We have a React component that will now flip through images for as long as we want to keep requesting new ones. But, that flip transition is a bit boring. To spice it up, we’re going to make use of [GreenSock](https://greensock.com) and its utilities. In particular, the “[distribute](https://greensock.com/docs/v3/GSAP/UtilityMethods/distribute)” utility. This will allow us to distribute the delay of flipping our cards in a grid-like burst from wherever we click. To do this, we’re going to use GreenSock to animate the `--count` value on each card.

{{% ad-panel-leaderboard %}}

It’s worth noting that we have a choice here. We could opt to apply the styles with GreenSock. Instead of animating the `--count` property value, we could animate `rotateX`. We could do this based on the `count` ref we have. And this also goes for any other things we choose to animate with GreenSock in this article. It’s down to preference and use case. You may feel that updating the custom property value makes sense. The benefit being that you don’t need to update any JavaScript to get a different styled behavior. We could change the CSS to use `rotateY` for example.

Our updated `flip` function could look like this:

<div class="break-out">

<pre><code class="language-javascript">const flip = e =&gt; {
  if (disabled) return
  const x = parseInt(e.target.parentNode.getAttribute('data-snap-x'), 10)
  const y = parseInt(e.target.parentNode.getAttribute('data-snap-y'), 10)
  count.current = count.current + 1
  gsap.to(containerRef.current.querySelectorAll('.flippy-card'), {
    '--count': count.current,
    delay: gsap.utils.distribute({
      from: [x / gridSize, y / gridSize],
      amount: gridSize / 20,
      base: 0,
      grid: [gridSize, gridSize],
      ease: 'power1.inOut',
    }),
    duration: 0.2,
    onComplete: () =&gt; {
      // At this point update the images
      if (onFlip) onFlip(count)
    },
  })
}</code></pre>
</div>

Note how we’re getting an `x` and `y` value by reading attributes of the clicked card. For this demo, we’ve opted for adding some `data` attributes to each card. These attributes communicate a card's position in the grid. We’re also using a new `ref` called `containerRef`. This is so we reference only the cards for a `FlippySnap` instance when using GreenSock.

<pre><code class="language-javascript">{new Array(CELL_COUNT).fill().map((cell, index) =&gt; {
  const x = index % gridSize
  const y = Math.floor(index / gridSize)
  return (
    &lt;span
      className="flippy-card"
      data-snap-x={x}
      data-snap-y={y}
      style={{
        '--x': x,
        '--y': y,
      }}&gt;
      &lt;span className="flippy-card__front"&gt;&lt;/span&gt;
      &lt;span className="flippy-card__rear"&gt;&lt;/span&gt;
    &lt;/span&gt;
  )
})}</code></pre>

Once we get those `x` and `y` values, we can make use of them in our animation. Using `gsap.to` we want to animate the `--count` custom property for every `.flippy-card` that’s a child of `containerRef`.

To distribute the delay from where we click, we set the value of `delay` to use `gsap.utils.distribute`. The `from` value of the `distribute` function takes an Array containing ratios along the x and y axis. To get this, we divide `x` and `y` by `gridSize`. The `base` value is the initial value. For this, we want `0` delay on the card we click. The `amount` is the largest value. We've gone for `gridSize / 20` but you could experiment with different values. Something based on the `gridSize` is a good idea though. The `grid` value tells GreenSock the grid size to use when calculating distribution. Last but not least, the `ease` defines the ease of the `delay` distribution.

<pre><code class="language-javascript">gsap.to(containerRef.current.querySelectorAll('.flippy-card'), {
  '--count': count.current,
  delay: gsap.utils.distribute({
    from: [x / gridSize, y / gridSize],
    amount: gridSize / 20,
    base: 0,
    grid: [gridSize, gridSize],
    ease: 'power1.inOut',
  }),
  duration: 0.2,
  onComplete: () =&gt; {
    // At this point update the images
    if (onFlip) onFlip(count)
  },
})</code></pre>

As for the rest of the animation, we are using a flip duration of `0.2` seconds. And we make use of `onComplete` to invoke our callback. We pass the flip `count` to the callback so it can use this to determine snap order. Things like the duration of the flip could get configured by passing in different `props` if we wished.

Putting it all together gives us this:

{{< codepen height="480" theme_id="light" slug_hash="VwzJbpM" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [6. Distributed Flips with GSAP](https://codepen.io/smashingmag/pen/VwzJbpM) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

Those that like to push things a bit might have noticed that we can still “spam” click the snap. And that’s because we don’t disable `FlippySnap` until GreenSock has completed. To fix this, we can use an internal ref that we toggle at the start and end of using GreenSock.

<div class="break-out">

<pre><code class="language-javascript">const flipping = useRef(false) // New ref to track the flipping state

const flip = e =&gt; {
  if (disabled || flipping.current) return
  const x = parseInt(e.target.parentNode.getAttribute('data-snap-x'), 10)
  const y = parseInt(e.target.parentNode.getAttribute('data-snap-y'), 10)
  count.current = count.current + 1
  gsap.to(containerRef.current.querySelectorAll('.flippy-card'), {
    '--count': count.current,
    delay: gsap.utils.distribute({
      from: [x / gridSize, y / gridSize],
      amount: gridSize / 20,
      base: 0,
      grid: [gridSize, gridSize],
      ease: 'power1.inOut',
    }),
    duration: 0.2,
    onStart: () =&gt; {
      flipping.current = true
    },
    onComplete: () =&gt; {
      // At this point update the images
      flipping.current = false
      if (onFlip) onFlip(count)
    },
  })
}</code></pre>
</div>

And now we can no longer spam click our `FlippySnap`!

{{< codepen height="480" theme_id="light" slug_hash="jOLjmXE" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [7. No Spam Clicks](https://codepen.io/smashingmag/pen/jOLjmXE) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

Now it’s time for some extra touches. At the moment, there’s no visual sign that we can click our `FlippySnap`. What if when we hover, the cards raise towards us? We could use `onPointerOver` and use the “distribute” utility again.

<pre><code class="language-javascript">const indicate = e =&gt; {
  const x = parseInt(e.currentTarget.getAttribute('data-snap-x'), 10)
  const y = parseInt(e.currentTarget.getAttribute('data-snap-y'), 10)
  gsap.to(containerRef.current.querySelectorAll('.flippy-card'), {
    '--hovered': gsap.utils.distribute({
      from: [x / gridSize, y / gridSize],
      base: 0,
      amount: 1,
      grid: [gridSize, gridSize],
      ease: 'power1.inOut'
    }),
    duration: 0.1,
  })
}</code></pre>

Here, we are setting a new custom property on each card named `--hovered`. This is set to a value from `0` to `1`. Then within our CSS, we are going to update our card styles to watch for the value.

<pre><code class="language-javascript">.flippy-card {
  transform: translate3d(0, 0, calc((1 - (var(--hovered, 1))) * 5vmin))
             rotateX(calc(var(--count) * -180deg));
}</code></pre>

Here we are saying that a card will move on the z-axis at most `5vmin`.

{{% ad-panel-leaderboard %}}

We then apply this to each card using the `onPointerOver` prop.

<pre><code class="language-javascript">{new Array(CELL_COUNT).fill().map((cell, index) =&gt; {
  const x = index % gridSize
  const y = Math.floor(index / gridSize)
  return (
    &lt;span
      onPointerOver={indicate}
      className="flippy-card"
      data-snap-x={x}
      data-snap-y={y}
      style={{
        '--x': x,
          '--y': y,
      }}&gt;
      &lt;span className="flippy-card__front"&gt;&lt;/span&gt;
      &lt;span className="flippy-card__rear"&gt;&lt;/span&gt;
    &lt;/span&gt;
  )
})}</code></pre>

And when our pointer leaves our `FlippySnap` we want to reset our card positions.

<pre><code class="language-javascript">
const reset = () =&gt; {
  gsap.to(containerRef.current.querySelectorAll('.flippy-card'), {
    '--hovered': 1,
    duration: 0.1,
  })
}</code></pre>

And we can apply this with the `onPointerLeave` prop.

<pre><code class="language-javascript">&lt;button
  className="flippy-snap"
  ref={containerRef}
  onPointerLeave={reset}
  style={{
    '--grid-size': gridSize,
    '--count': count.current,
    '--current-image': `url('${snaps[0]}')`,
    '--next-image': `url('${snaps[1]}')`,
  }}
  onClick={flip}&gt;</code></pre>

Put that all together and we get something like this. Try moving your pointer over it.

{{< codepen height="480" theme_id="light" slug_hash="wvqLdZL" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [8. Visual Inidication with Raised Cards](https://codepen.io/smashingmag/pen/wvqLdZL) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

What next? How about a loading indicator so we know when our `App` is grabbing the next image? We can render a loading spinner when our `FlippySnap` is `disabled`.

<pre><code class="language-javascript">{disabled && &lt;span className='flippy-snap__loader'&gt;&lt;/span&gt;}</code></pre>

He styles for which could make a rotating circle.

<pre><code class="language-javascript">.flippy-snap__loader {
  border-radius: 50%;
  border: 6px solid #fff;
  border-left-color: #000;
  border-right-color: #000;
  position: absolute;
  right: 10%;
  bottom: 10%;
  height: 8%;
  width: 8%;
  transform: translate3d(0, 0, 5vmin) rotate(0deg);
  animation: spin 1s infinite;
}
@keyframes spin {
  to {
    transform: translate3d(0, 0, 5vmin) rotate(360deg);
  }
}</code></pre>

And this gives us a loading indicator when grabbing a new image.

{{< codepen height="480" theme_id="light" slug_hash="qBXzmzx" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [9. Add Loading Indicator](https://codepen.io/smashingmag/pen/qBXzmzx) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

## That’s it!

That’s how we can create a `FlippySnap` with React and GreenSock. It’s fun to make things that we may not create on a day-to-day basis. Demos like this can pose different challenges and can level up your problem-solving game.

I took it a little further and added a slight parallax effect along with some audio. You can also configure the grid size! (Big grids affect performance though.)

{{< codepen height="480" theme_id="light" slug_hash="QWMXgLb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [3D CSS Flippy Snaps v2 (React &amp;&amp; GSAP)](https://codepen.io/smashingmag/pen/QWMXgLb) by <a href="https://codepen.io/jh3y">JHEY</a>{{< /codepen >}}

*It’s worth noting that this demo works best in Chromium-based browsers.*

So, where would you take it next? I’d like to see if I can recreate it with Three.js next. That would address the performance. 😅 

Stay Awesome!  ʕ•ᴥ•ʔ

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

{{< signature "vf, yk, il" >}}
