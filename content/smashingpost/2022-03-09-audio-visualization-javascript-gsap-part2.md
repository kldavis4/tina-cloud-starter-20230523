---
title: 'A Guide To Audio Visualization With JavaScript And GSAP (Part 2)'
slug: audio-visualization-javascript-gsap-part2
author: jhey-tompkins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d02916da-2e33-4aed-ac5e-f1107fa44e57/audio-visualization-javascript-gsap-part1.jpg
date: 2022-03-09T13:00:00.000Z
summary: >-
  What started as a case study turned into a guide to visualizing audio with JavaScript. Although the output demos are in React, Jhey Tompkins isn’t going to dwell on the React side of things too much. The underlying techniques work with or without React. 
description: >-
  What started as a case study turned into a guide to visualizing audio with JavaScript. Although the output demos are in React, Jhey Tompkins isn’t going to dwell on the React side of things too much. The underlying techniques work with or without React. 
categories:
  - React
  - Coding
  - JavaScript
  - Techniques 
---

[Last week in Part 1](https://www.smashingmagazine.com/2022/03/audio-visualization-javascript-gsap-part1/), I explained how the idea about how to record audio input from users and then moved on to the [visualization](https://www.smashingmagazine.com/2022/03/audio-visualization-javascript-gsap-part1/#visualization). After all, without any visualization, any type of audio recording UI isn’t very engaging, is it? Today, we’ll be diving into more details in terms of adding features and any sort of extra touches you like!

We’ll be covering the following:

- [How To Pause A Recording](#pausing-a-recording)
- [How To Pad Out The Visuals](#padding-out-the-visuals)
- [How To Finish The Recording](#finishing-the-recording)
- [Scrubbing The Values On Playback](#scrubbing-the-values-on-playback)
- [Audio Playback From Other Sources](#audio-playback-from-other-sources)
- [Turning This Into A React Application](http://localhost:3000/2022/03/audio-visualization-javascript-gsap-part2/#turning-this-into-a-react-application)

Please note that in order to see the demos in action, you’ll need to open and test directly them on the CodePen website.

## Pausing A Recording

Pausing a recording doesn’t take much code at all.

<pre><code class="language-javascript">// Pause a recorder
recorder.pause()
// Resume a recording
recorder.resume()
</code></pre>

In fact, the trickiest part about integrating recording is designing your UI. Once you’ve got a UI design, it’ll likely be more about the changes you need for that.

Also, pausing a recording doesn’t pause our animation. So we need to make sure we stop that too. We only want to add new bars whilst we are recording. To determine what state the recorder is in, we can use the `state` property mentioned earlier. Here’s our updated toggle functionality:

<pre><code class="language-javascript">const RECORDING = recorder.state === 'recording'
// Pause or resume recorder based on state.
TOGGLE.style.setProperty('--active', RECORDING ? 0 : 1)
timeline[RECORDING ? 'pause' : 'play']()
recorder[RECORDING ? 'pause' : 'resume']()
</code></pre>

And here’s how we can determine whether to add new bars in the reporter or not.

<pre><code class="language-javascript">REPORT = () => {
  if (recorder && recorder.state === 'recording') {
</code></pre>

**Challenge**: *Could we also remove the report function from `gsap.ticker` for extra performance? Try it out.*

For our demo, we’ve changed it so the record button becomes a pause button. And once a recording has begun, a stop button appears. This will need some extra code to handle that state. React is a good fit for this but we can lean into the `recorder.state` value.

{{< codepen height="480" theme_id="light" slug_hash="BamgQEP" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [15. Pausing a Recording](https://codepen.io/smashingmag/pen/BamgQEP) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

## Padding Out The Visuals

Next, we need to pad out our visuals. What do we mean by that? Well, we go from an empty canvas to bars streaming across. It’s quite a contrast and it would be nice to have the canvas filled with zero volume bars on start. There is no reason we can’t do this either based on how we are generating our bars. Let’s start by creating a padding function, `padTimeline`:

<pre><code class="language-javascript">// Move BAR_DURATION out of scope so it’s a shared variable.
const BAR_DURATION =
  CANVAS.width / ((CONFIG.barWidth + CONFIG.barGap) * CONFIG.fps)

const padTimeline = () => {
  // Doesn’t matter if we have more bars than width. We will shift them over to the correct spot
  const padCount = Math.floor(CANVAS.width / CONFIG.barWidth)

  for (let p = 0; p < padCount; p++) {
    const BAR = {
      x: CANVAS.width + CONFIG.barWidth / 2,
      // Note the volume is 0
      size: gsap.utils.mapRange(
        0,
        100,
        CANVAS.height * CONFIG.barMinHeight,
        CANVAS.height * CONFIG.barMaxHeight
      )(volume),
    }
    // Add to bars Array
    BARS.push(BAR)
    // Add the bar animation to the timeline
    // The actual pixels per second is (1 / fps * shift) * fps
    // if we have 50fps, the bar needs to have moved bar width before the next comes in
    // 1/50 = 4 === 50 * 4 = 200
    timeline.to(
      BAR,
      {
        x: `-=${CANVAS.width + CONFIG.barWidth}`,
        ease: 'none',
        duration: BAR_DURATION,
      },
      BARS.length * (1 / CONFIG.fps)
    )
    }
  // Sets the timeline to the correct spot for being added to
  timeline.totalTime(timeline.totalDuration() - BAR_DURATION)
}
</code></pre>

The trick here is to add new bars and then set the playhead of the timeline to where the bars fill the canvas. At the point of padding the timeline, we know that we only have padding bars so `totalDuration` can be used.

<pre><code class="language-javascript">timeline.totalTime(timeline.totalDuration() - BAR_DURATION)
</code></pre>

Notice how that functionality is very like what we do inside the `REPORT` function? We have a good opportunity to refactor here. Let’s create a new function named `addBar`. This adds a new bar based on the passed `volume`.

<pre><code class="language-javascript">const addBar = (volume = 0) => {
  const BAR = {
    x: CANVAS.width + CONFIG.barWidth / 2,
    size: gsap.utils.mapRange(
      0,
      100,
      CANVAS.height * CONFIG.barMinHeight,
      CANVAS.height * CONFIG.barMaxHeight
    )(volume),
  }
  BARS.push(BAR)
  timeline.to(
    BAR,
    {
      x: `-=${CANVAS.width + CONFIG.barWidth}`,
      ease: 'none',
      duration: BAR_DURATION,
    },
    BARS.length * (1 / CONFIG.fps)
  )
}
</code></pre>

Now our `padTimeline` and `REPORT` functions can make use of this:

<pre><code class="language-javascript">const padTimeline = () => {
  const padCount = Math.floor(CANVAS.width / CONFIG.barWidth)
  for (let p = 0; p < padCount; p++) {
    addBar()
  }
  timeline.totalTime(timeline.totalDuration() - BAR_DURATION)
}

REPORT = () => {
  if (recorder && recorder.state === 'recording') {
    ANALYSER.getByteFrequencyData(DATA_ARR)
    const VOLUME = Math.floor((Math.max(...DATA_ARR) / 255) * 100)
    addBar(VOLUME)
  }
  if (recorder || visualizing) {
    drawBars()
  }
}
</code></pre>

Now, on load, we can do an initial rendering by invoking `padTimeline` followed by `drawBars`.

<pre><code class="language-javascript">padTimeline()
drawBars()
</code></pre>

Putting it all together and that’s another neat feature!

{{< codepen height="480" theme_id="light" slug_hash="OJOebYE" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [16. Padding out the Timeline](https://codepen.io/smashingmag/pen/OJOebYE) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

### How We Finish

Do you want to pull the component down or do a rewind, maybe a rollout? How does this affect performance? A rollout is easier. But a rewind is trickier and might have perf hits. 

{{% feature-panel %}}

## Finishing The Recording

You can finish up your recording any way you like. You could stop the animation and leave it there. Or, if we stop the animation we could roll back the animation to the start. This is often used in various UI/UX designs. And the GSAP API gives us a neat way to do this. Instead of clearing our timeline on stop, we can move this into where we start a recording to reset the timeline. But, once we’ve finished a recording, let’s keep the animation around so we can use it.

<pre><code class="language-javascript">STOP.addEventListener('click', () => {
  if (recorder) recorder.stop()
  AUDIO_CONTEXT.close()
  // Pause the timeline
  timeline.pause()
  // Animate the playhead back to the START_POINT
  gsap.to(timeline, {
    totalTime: START_POINT,
    onComplete: () => {
      gsap.ticker.remove(REPORT)
    }
  })
})
</code></pre>

In this code, we tween the `totalTime` back to where we set the playhead in `padTimeline`.
That means we needed to create a variable for sharing that.

<pre><code class="language-javascript">let START_POINT
</code></pre>

And we can set that within `padTimeline`.

<pre><code class="language-javascript">const padTimeline = () => {
  const padCount = Math.floor(CANVAS.width / CONFIG.barWidth)
  for (let p = 0; p < padCount; p++) {
    addBar()
  }
  START_POINT = timeline.totalDuration() - BAR_DURATION
  // Sets the timeline to the correct spot for being added to
  timeline.totalTime(START_POINT)
}
</code></pre>

We can clear the timeline inside the `RECORD` function when we start a recording:

<pre><code class="language-javascript">// Reset the timeline
timeline.clear()
</code></pre>

And this gives us what is becoming a pretty neat audio visualizer:

{{< codepen height="480" theme_id="light" slug_hash="LYOKbKW" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [17. Rewinding on Stop](https://codepen.io/smashingmag/pen/LYOKbKW) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

## Scrubbing The Values On Playback

Now we’ve got our recording, we can play it back with the `<audio>` element. But, we’d like to sync our visualization with the recording playback. With GSAP’s API, this is far easier than you might expect.

<pre><code class="language-javascript">const SCRUB = (time = 0, trackTime = 0) => {
  gsap.to(timeline, {
    totalTime: time,
    onComplete: () => {
      AUDIO.currentTime = trackTime
      gsap.ticker.remove(REPORT)
    },
  })
}
const UPDATE = e => {
  switch (e.type) {
    case 'play':
      timeline.totalTime(AUDIO.currentTime + START_POINT)
      timeline.play()
      gsap.ticker.add(REPORT)
      break
    case 'seeking':
    case 'seeked':
      timeline.totalTime(AUDIO.currentTime + START_POINT)
      break
    case 'pause':
      timeline.pause()
      break
    case 'ended':
      timeline.pause()
      SCRUB(START_POINT)
      break
  }
}

// Set up AUDIO scrubbing
['play', 'seeking', 'seeked', 'pause', 'ended']
  .forEach(event => AUDIO.addEventListener(event, UPDATE))
</code></pre>

We’ve refactored the functionality that we use when stopping to scrub the timeline. And then it’s a case of listening for different events on the `<audio>` element. Each event requires updating the timeline playhead.  We can add and remove `REPORT` to the `ticker` based on when we play and stop audio.  But, this does have an edge case. If you seek after the audio has "ended", the visualization won’t render updates. And that’s because we remove `REPORT` from the `ticker` in `SCRUB`. You could opt to not remove `REPORT` at all until a new recording begins or you move to another state in your app. It’s a matter of monitoring performance and what feels right.

The fun part here though is that if you make a recording, you can scrub the visualization when you seek 😎

{{< codepen height="480" theme_id="light" slug_hash="qBVzRaj" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [18. Syncing with Playback](https://codepen.io/smashingmag/pen/qBVzRaj) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

At this point, you know everything you need to know. But, if you want to learn about some extra things, keep reading.

## Audio Playback From Other Sources

One thing we haven’t looked at is how you visualize audio from a source other than an input device. For example, an mp3 file. And this brings up an interesting challenge or problem to think about.

Let’s consider a demo where we have an audio file URL and we want to visualize it with our visualization. We can explicitly set our `AUDIO` element’s `src` before visualizing.

<pre><code class="language-javascript">AUDIO.src = 'https://assets.codepen.io/605876/lobo-loco-spencer-bluegrass-blues.mp3'
// NOTE:: This is required in some circumstances due to CORS
AUDIO.crossOrigin = 'anonymous'
</code></pre>

We no longer need to think about setting up the recorder or using the controls to trigger it. As we have an audio element, we can set the visualization to hook into the source direct. 

<pre><code class="language-javascript">const ANALYSE = stream => {
  if (AUDIO_CONTEXT) return
  AUDIO_CONTEXT = new AudioContext()
  ANALYSER = AUDIO_CONTEXT.createAnalyser()
  ANALYSER.fftSize = CONFIG.fft
  const DATA_ARR = new Uint8Array(ANALYSER.frequencyBinCount)
  SOURCE = AUDIO_CONTEXT.createMediaElementSource(AUDIO)
  const GAIN_NODE = AUDIO_CONTEXT.createGain()
  GAIN_NODE.value = 0.5
  GAIN_NODE.connect(AUDIO_CONTEXT.destination)
  SOURCE.connect(GAIN_NODE)
  SOURCE.connect(ANALYSER)

  // Reset the bars and pad them out...
  if (BARS && BARS.length > 0) {
    BARS.length = 0
    padTimeline()
  }

  REPORT = () => {
    if (!AUDIO.paused || !played) {
      ANALYSER.getByteFrequencyData(DATA_ARR)
      const VOLUME = Math.floor((Math.max(...DATA_ARR) / 255) * 100)
      addBar(VOLUME)
      drawBars()  
    }
  }
  gsap.ticker.add(REPORT)
}
</code></pre>

By doing this we can connect our `AudioContext` to the `audio` element. We do this using `createMediaElementSource(AUDIO)` instead of `createMediaStreamSource(stream)`. And then the `audio` elements' controls will trigger data getting passed to the analyzer. In fact, we only need to create the `AudioContext` once. Because once we’ve played the audio track, we aren’t working with a different audio track after. Hence, the `return` if `AUDIO_CONTEXT` exists.

<pre><code class="language-javascript">if (AUDIO_CONTEXT) return
</code></pre>

One other thing to note here. Because we’re hooking up the `audio` element to an `AudioContext`, we need to create a gain node. This gain node allows us to hear the audio track.

<pre><code class="language-javascript">SOURCE = AUDIO_CONTEXT.createMediaElementSource(AUDIO)
const GAIN_NODE = AUDIO_CONTEXT.createGain()
GAIN_NODE.value = 0.5
GAIN_NODE.connect(AUDIO_CONTEXT.destination)
SOURCE.connect(GAIN_NODE)
SOURCE.connect(ANALYSER)
</code></pre>

Things do change a little in how we process events on the audio element. In fact, for this example, when we’ve finished the audio track, we can remove `REPORT` from the `ticker`. But, we add `drawBars` to the `ticker`. This is so if we play the track again or seek, etc. we don’t need to process the audio again. This is like how we handled playback of the visualization with the recorder.

This update happens inside the `SCRUB` function and you can also see a new `played` variable. We can use this to determine whether we’ve processed the whole audio track.

<pre><code class="language-javascript">const SCRUB = (time = 0, trackTime = 0) => {
  gsap.to(timeline, {
    totalTime: time,
    onComplete: () => {
      AUDIO.currentTime = trackTime
      if (!played) {
        played = true
        gsap.ticker.remove(REPORT)
        gsap.ticker.add(drawBars) 
      }
    },
  })
}
</code></pre>

Why not add and remove `drawBars` from the `ticker` based on what we are doing with the audio element? We could do this. We could look at `gsap.ticker._listeners` and determine if `drawBars` was already used or not. We may choose to add and remove when playing and pausing. And then we could also add and remove when seeking and finishing seeking. The trick would be making sure we don’t add to the `ticker` too much when "seeking". And this would be where to check if `drawBars` was already part of the ticker. This is of course dependent on performance though. Is that optimization going to be worth the minimal performance gain? It comes down to what exactly your app needs to do. For this demo, once the audio gets processed, we are switching out the `ticker` function. That’s because we don’t need to process the audio again. And leaving `drawBars` running in the `ticker` shows no performance hit.

<pre><code class="language-javascript">const UPDATE = e => {
  switch (e.type) {
    case 'play':
      if (!played) ANALYSE()
      timeline.totalTime(AUDIO.currentTime + START_POINT)
      timeline.play()
      break
    case 'seeking':
    case 'seeked':
      timeline.totalTime(AUDIO.currentTime + START_POINT)
      break 
    case 'pause':
      timeline.pause()
      break
    case 'ended':
      timeline.pause()
      SCRUB(START_POINT)
      break
  }
}
</code></pre>

Our `switch` statement is much the same but we instead only `ANALYSE` if we haven’t `played` the track.

And this gives us the following demo:

{{< codepen height="480" theme_id="light" slug_hash="rNYEjWe" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [19. Processing Audio Files](https://codepen.io/smashingmag/pen/rNYEjWe) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

**Challenge**: *Could you extend this demo to support different tracks? Try extending the demo to accept different audio tracks. Maybe a user can select from dropdown or input a URL.*

This demo leads to an interesting problem that arose when working on "Record a Call" for [Kent C. Dodds](https://twitter.com/kentcdodds). It’s not one I’d needed to deal with before. In the demo above, start playing the audio and seek forwards in the track before it finishes playing. Seeking forwards breaks the visualization because we are skipping ahead of time. And that means we are skipping processing certain parts of the audio.

How can you resolve this? It’s an interesting problem. You want to build the animation timeline before you play audio. But, to build it, you need to play through the audio first. Could you disable "seeking" until you’ve played through once? You could. At this point, you might start drifting into the world of custom audio players. Definitely out of scope for this article. In a real-world scenario, you may be able to put server-side processing in place. This might give you a way to get the audio data ahead of time before playing it.

{{% ad-panel-leaderboard %}}

For Kent’s “[Record a Call](https://kentcdodds.com/calls/record)”, we can take a different approach. We are processing the audio as it’s recorded. And each bar gets represented by a number. If we create an `Array` of numbers representing the bars, we already have the data to build the animation. When a recording gets submitted, the data can go with it. Then when we make a request for audio, we can get that data too and build the visualization before playback.

We can use the `addBar` function we defined earlier whilst looping over the audio data `Array`.

<pre><code class="language-javascript">// Given an audio data Array example
const AUDIO_DATA = [100, 85, 43, 12, 36, 0, 0, 0, 200, 220, 130]

const buildViz = DATA => {
  DATA.forEach(bar => addBar(bar))
}

buildViz(AUDIO_DATA)
</code></pre>

Building our visualizations without processing the audio again is a great performance win.

Consider this extended demo of our recording demo. Each recording gets stored in `localStorage`. And we can load a recording to play it. But, instead of processing the audio to play it, we build a new bars animation and set the audio element `src`.

**Note**: *You need to scroll down to see stored recordings in the &lt;details&gt; and &lt;summary&gt; element.*

{{< codepen height="480" theme_id="light" slug_hash="KKyjaaP" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [20. Saved Recordings ✨](https://codepen.io/smashingmag/pen/KKyjaaP) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

What needs to happen here to store and playback recordings? Well, it doesn’t take much as we have the bulk of functionality in place. And as we’ve refactored things into mini utility functions, this makes things easier.

Let’s start with how we are going to store the recordings in `localStorage`. On page load, we are going to hydrate a variable from `localStorage`. If there is nothing to hydrate with, we can instantiate the variable with a default value.

<pre><code class="language-javascript">const INITIAL_VALUE = { recordings: []}
const KEY = 'recordings'
const RECORDINGS = window.localStorage.getItem(KEY)
  ? JSON.parse(window.localStorage.getItem(KEY))
  : INITIAL_VALUE
</code></pre>

Now. It’s worth noting that this guide isn’t about building a polished app or experience. It’s giving you the tools you need to go off and make it your own. I’m saying this because some of the UX, you might want to put in place in a different way.

To save a recording, we can trigger a save in the `ondataavailable` method we’ve been using. 

<pre><code class="language-javascript">recorder.ondataavailable = (event) => {
  // All the other handling code
  // save the recording
  if (confirm('Save Recording?')) {
    saveRecording()
  }
}
</code></pre>

The process of saving a recording requires a little "trick". We need to convert our `AudioBlob` into a String. That way, we can save it to `localStorage`. To do this, we use the `FileReader` API to convert the `AudioBlob` to a data URL. Once we have that, we can create a new recording object and persist it to `localStorage`.

<pre><code class="language-javascript">const saveRecording = async () => {
  const reader = new FileReader()
  reader.onload = e => {
    const audioSafe = e.target.result
    const timestamp = new Date()
    RECORDINGS.recordings = [
      ...RECORDINGS.recordings,
      {
        audioBlob: audioSafe,
        metadata: METADATA,
        name: timestamp.toUTCString(),
        id: timestamp.getTime(),
      },
    ]
    window.localStorage.setItem(KEY, JSON.stringify(RECORDINGS))
    renderRecordings()
    alert('Recording Saved')  
  }
  await reader.readAsDataURL(AUDIO_BLOB)
}
</code></pre>

You could create whatever type of format you like here. For ease, I’m using the time as an `id`. The `metadata` field is the `Array` we use to build our animation. The `timestamp` field is being used like a "name". But, you could do something like name it based on the number of recordings. Then you could update the UI to allow users to rename the recording. Or you could even do it through the save step with `window.prompt`.

In fact, this demo uses the `window.prompt` UX so you can see how that would work.

{{< codepen height="480" theme_id="light" slug_hash="oNorBwp" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [21. Prompt for Recording Name 🚀](https://codepen.io/smashingmag/pen/oNorBwp) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

You may be wondering what `renderRecordings` does. Well, as we aren’t using a framework, we need to update the UI ourselves. We call this function on load and every time we save or delete a recording.

The idea is that if we have recordings, we loop over them and create list items to append to our recordings list. If we don’t have any recordings, we are showing a message to the user.

For each recording, we create two buttons. One for playing the recording, and another for deleting the recording.

<pre><code class="language-javascript">const renderRecordings = () => {
  RECORDINGS_LIST.innerHTML = ''
  if (RECORDINGS.recordings.length > 0) {
    RECORDINGS_MESSAGE.style.display = 'none'
    RECORDINGS.recordings.reverse().forEach(recording => {
      const LI = document.createElement('li')
      LI.className = 'recordings__recording'
      LI.innerHTML = `&lt;span&gt;${recording.name}&lt;/span&gt;`
      const BTN = document.createElement('button')
      BTN.className = 'recordings__play recordings__control'
      BTN.setAttribute('data-recording', recording.id)
      BTN.title = 'Play Recording'
      BTN.innerHTML = SVGIconMarkup
      LI.appendChild(BTN)
      const DEL = document.createElement('button')
      DEL.setAttribute('data-recording', recording.id)
      DEL.className = 'recordings__delete recordings__control'
      DEL.title = 'Delete Recording'
      DEL.innerHTML = SVGIconMarkup
      LI.appendChild(DEL)
      BTN.addEventListener('click', playRecording)
      DEL.addEventListener('click', deleteRecording)
      RECORDINGS_LIST.appendChild(LI)
    })
  } else {
    RECORDINGS_MESSAGE.style.display = 'block'
  }
}
</code></pre>

Playing a recording means setting the `AUDIO` element `src` and generating the visualization. Before playing a recording or when we delete a recording, we reset the state of the UI with a `reset` function.

<pre><code class="language-javascript">const reset = () => {
  AUDIO.src = null
  BARS.length = 0
  gsap.ticker.remove(REPORT)
  REPORT = null
  timeline.clear()
  padTimeline()
  drawBars()
}

const playRecording = (e) => {
  const idToPlay = parseInt(e.currentTarget.getAttribute('data-recording'), 10)
  reset()
  const RECORDING = RECORDINGS.recordings.filter(recording => recording.id === idToPlay)[0]
  RECORDING.metadata.forEach(bar => addBar(bar))
  REPORT = drawBars
  AUDIO.src = RECORDING.audioBlob
  AUDIO.play()
}
</code></pre>

The actual method of playback and showing the visualization comes down to four lines.

<pre><code class="language-javascript">RECORDING.metadata.forEach(bar => addBar(bar))
REPORT = drawBars
AUDIO.src = RECORDING.audioBlob
AUDIO.play()
</code></pre>

1. Loop over the metadata Array to build the `timeline`.
2. Set the `REPORT` function to `drawBars`.
3. Set the `AUDIO` src.
4. Play the audio which in turn triggers the animation `timeline` to play.

**Challenge**: *Can you spot any edge cases in the UX? Any issues that could arise? What if we are recording and then choose to play a recording? Could we disable controls when we are in recording mode?*

To delete a recording, we use the same `reset` method but we set a new value in `localStorage` for our recordings. Once we’ve done that, we need to `renderRecordings` to show the updates.

<pre><code class="language-javascript">const deleteRecording = (e) => {
  if (confirm('Delete Recording?')) {
    const idToDelete = parseInt(e.currentTarget.getAttribute('data-recording'), 10)
    RECORDINGS.recordings = [...RECORDINGS.recordings.filter(recording => recording.id !== idToDelete)]
    window.localStorage.setItem(KEY, JSON.stringify(RECORDINGS))
    reset()
    renderRecordings()    
  }
}
</code></pre>

At this stage, we have a functional voice recording app using `localStorage`. It makes for an interesting start point that you could take and add new features to and improve the UX. For example, how about making it possible for users to download their recordings? Or what if different users could have different themes for their visualization? You could store colors, speeds, etc. against recordings. Then it would be a case of updating the canvas properties and catering for changes in the timeline build. For “Record a Call”, we supported different canvas colors based on the team a user was part of.

This demo supports downloading tracks in the `.ogg` format.

{{< codepen height="480" theme_id="light" slug_hash="bGYPgqJ" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [22. Downloadable Recordings 🚀](https://codepen.io/smashingmag/pen/bGYPgqJ) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

But you could take this app in various directions. Here are some ideas to think about:

- Reskin the app with a different "look and feel"
- Support different playback speeds
- Create different visualization styles. For example, how might you record the metadata for a waveform type visualization?
- Displaying the recordings count to the user
- Improve the UX catching edge cases such as the recording to playback scenario from earlier.
- Allow users to choose their audio input device
- Take your visualizations 3D with something like ThreeJS
- Limit the recording time. This would be vital in a real-world app. You would want to limit the size of the data getting sent to the server. It would also enforce recordings to be concise.
- Currently, downloading would only work in `.ogg` format. We can’t encode the recording to `mp3` in the browser. But you could use serverless with [ffmpeg](https://www.npmjs.com/package/ffmpeg) to convert the audio to `.mp3` for the user and return it.

{{% ad-panel-leaderboard %}}

## Turning This Into A React Application

Well. If you’ve got this far, you have all the fundamentals you need to go off and have fun making audio recording apps. But, I did mention at the top of the article, we used React on the project. As our demos have got more complex and we’ve introduced "state", using a framework makes sense. We aren’t going to go deep into building the app out with React but we can touch on how to approach it. If you’re new to React, check out this "[Getting Started Guide](https://www.smashingmagazine.com/2021/05/get-started-whac-a-mole-react-game/)" that will get you in a good place.

The main problem we face when switching over to React land is thinking about how we break things up. There isn’t a right or wrong. And then that introduces the problem of how we pass data around via props, etc. For this app, it’s not too tricky. We could have a component for the visualization, the audio playback, and recordings. And then we may opt to wrap them all inside one parent component.

For passing data around and accessing things in the DOM, `React.useRef` plays an important part. This is “a” React version of the app we’ve built.

{{< codepen height="480" theme_id="light" slug_hash="ZEadLyW" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [23. Taking it to React Land 🚀](https://codepen.io/smashingmag/pen/ZEadLyW) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

As stated before, there are different ways to achieve the same goal and we won’t dig into everything. But, we can highlight some of the decisions you may have to make or think about.

For the most part, the functional logic remains the same. But, we can use refs to keep track of certain things. And it’s often the case we need to pass these refs in props to the different components.

<pre><code class="language-javascript">return (
  &lt;&gt;
    &lt;AudioVisualization
      start={start}
      recording={recording}
      recorder={recorder}
      timeline={timeline}
      drawRef={draw}
      metadata={metadata}
      src={src}
    /&gt;
    &lt;RecorderControls
      onRecord={onRecord}
      recording={recording}
      paused={paused}
      onStop={onStop}
    /&gt;
    &lt;RecorderPlayback
      src={src}
      timeline={timeline}
      start={start}
      draw={draw}
      audioRef={audioRef}
      scrub={scrub}
    /&gt;
    &lt;Recordings
      recordings={recordings}
      onDownload={onDownload}
      onDelete={onDelete}
      onPlay={onPlay}
    /&gt;
  &lt;/&gt;
)
</code></pre>

For example, consider how we are passing the `timeline` around in a prop. This is a `ref` for a GreenSock `timeline`.

<pre><code class="language-javascript">const timeline = React.useRef(gsap.timeline())
</code></pre>

And this is because some of the components need access to the visualization timeline. But, we could approach this a different way. The alternative would be to pass in event handling as props and have access to the `timeline` in the scope. Each way would work. But, each way has trade-offs.

Because we’re working in "React" land, we can shift some of our code to be "Reactive". The clue is in the name, I guess. 😅 For example, instead of trying to pad the timeline and draw things from the parent. We can make the canvas component react to audio `src` changes. By using `React.useEffect`, we can re-build the timeline based on the `metadata` available:

<pre><code class="language-javascript">React.useEffect(() => {
  barsRef.current.length = 0
  padTimeline()
  drawRef.current = DRAW
  DRAW()
  if (src === null) {
    metadata.current.length = 0      
  } else if (src && metadata.current.length) {
    metadata.current.forEach(bar => addBar(bar))
    gsap.ticker.add(drawRef.current)
  }
}, [src])
</code></pre>

The last part that would be good to mention is how we persist recordings to `localStorage` with React. For this, we are using a custom hook that we built before in our "Getting Started" guide.

<pre><code class="language-javascript">const usePersistentState = (key, initialValue) => {
  const [state, setState] = React.useState(
    window.localStorage.getItem(key)
      ? JSON.parse(window.localStorage.getItem(key))
      : initialValue
  )
  React.useEffect(() => {
    // Stringify so we can read it back
    window.localStorage.setItem(key, JSON.stringify(state))
  }, [key, state])
  return [state, setState]
}
</code></pre>

This is neat because we can use it the same as `React.useState` and we get abstracted away from persisting logic.

<pre><code class="language-javascript">// Deleting a recording
setRecordings({
  recordings: [
    ...recordings.filter(recording => recording.id !== idToDelete),
  ],
})
// Saving a recording
const audioSafe = e.target.result
const timestamp = new Date()
const name = prompt('Recording name?')
setRecordings({
  recordings: [
    ...recordings,
    {
      audioBlob: audioSafe,
      metadata: metadata.current,
      name: name || timestamp.toUTCString(),
      id: timestamp.getTime(),
    },
  ],
})
</code></pre>

I’d recommend digging into some of the React code and having a play if you’re interested. Some things work a little differently in React land. Could you extend the app and make the visualizer support different visual effects? For example, how about passing colors via props for the fill style?

## That’s It!

Wow. You’ve made it to the end! This was a long one.

What started as a case study turned into a guide to visualizing audio with JavaScript. We’ve covered a lot here. But, now you have the fundamentals to go forth and make audio visualizations as I did for Kent.

Last but not least, here’s one that visualizes a waveform using `@react-three/fiber`:

{{< codepen height="480" theme_id="light" slug_hash="oNoredR" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [24. Going to 3D React Land 🚀](https://codepen.io/smashingmag/pen/oNoredR) by <a href="https://codepen.io/jh3y">Jhey</a>.{{< /codepen >}}

That’s ReactJS, ThreeJS and GreenSock all working together! 💪

There’s so much to go off and explore with this one. I’d love to see where you take the demo app or what you can do with it!

As always, if you have any questions, you know [where to find me](https://twitter.com/jh3yy).

**Stay Awesome! ʕ •ᴥ•ʔ**

*P.S. There is a [CodePen Collection](https://codepen.io/collection/ZMOydK) containing all the demos seen in the articles along with some bonus ones.* 🚀

{{< signature "vf, il" >}}
