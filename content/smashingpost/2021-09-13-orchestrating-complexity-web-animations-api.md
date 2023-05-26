---
title: 'Orchestrating Complexity With Web Animations API'
slug: orchestrating-complexity-web-animations-api
author: kirill-myshkin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc4a9b5f-fd83-4fc0-9966-6f98707d1466/orchestrating-complexity-web-animations-api.jpg
date: 2021-09-13T09:00:00.000Z
summary: >-
  There are way too many options in Web Animations API to pick them up that easily. Learning how timing works and how to control the playback of several animations at once makes for a solid foundation on which to base your projects on.
description: >-
  There are way too many options in Web Animations API to pick them up that easily. Learning how timing works and how to control the playback of several animations at once makes for a solid foundation on which to base your projects on.
categories:
  - API
  - Animation
  - Interfaces
  - JavaScript
---

There’s no middle ground between simple transitions and complex animations. You’re either fine with what CSS Transitions and Animations provide or you suddenly need all the power you can get. Web Animations API gives you a lot of tools to work with animations. But you need to know how to handle them. This article will walk you through the **main points and techniques** that might help you deal with complex animations while staying flexible.

Before we dive into the article it is vital that you’re familiar with the basics of the Web Animations API and JavaScript. To make it clear and avoid distraction from the problem at hand the code examples provided are plain. There won’t be anything more complex than functions and objects. As nice entry points into animations themselves I would suggest [MDN as a general reference](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API), [Daniel C. Wilson’s excellent series](https://danielcwilson.com/blog/2015/07/animations-intro/), and [CSS Animations vs Web Animations API by Ollie Williams](https://css-tricks.com/css-animations-vs-web-animations-api/). We won’t go through the ways to define effects and tuning them to achieve the outcome you want. This article assumes you have your animations defined and need ideas and techniques to handle them.

We start with an **overview of interfaces** and what they are for. Then we’ll look at timing and levels of control to define what, when, and for how long. After that, we’ll learn how to treat several animations as one by wrapping them in objects. That would be a good start on your way to using Web Animations API.

## Interfaces

Web Animations API gives us a new dimension of control. Before that, CSS Transitions and Animation while providing a powerful way of defining effects still had a **single point of actuation**. Like a light switch, it was either on or off. You could play with delays and easing functions to create quite complex effects. Still, at a certain point, it becomes cumbersome and hard to work with.

Web Animations API turns this single point of actuation into **complete control over playback**. The light switch turns into a dimmer switch with a slider. If you want you could turn it into the whole smart home thing, because additionally to the playback control you now can define and change effects at runtime. You now can adapt effects to context or you could implement an animations editor with real-time preview.

We start with the Animation interface. To get an animation object, we can use the `Element.animate` method. You give it keyframes and options and it plays your animation immediately. What it also does is it returns an `Animation` object instance. Its purpose is to control the playback.

Think of it as a **cassette player**, if you remember these. I’m aware that some of the readers might not be familiar with what it is. It’s inevitable that any attempt to apply real-world concepts to describe abstract computery things will fall apart quickly. But let it reassure you &mdash; a reader who doesn’t know the joy of rewinding a tape with a pencil &mdash; that people who know what a cassette player is will be confused even more by the end of this article.

Imagine a box. It has a slot where the cassette goes and it has buttons to play, stop and rewind. That’s what the Animation interface instance is &mdash; a **box that holds defined animation** and provides ways to interact with its playback. You give it something to play and it gives you back controls.

The controls you get are conveniently similar to the ones you get from audio and video elements. They are *play* and *pause* methods, and the *current time* property. With those three controls, you can build anything when it comes to playback.

The cassette itself is a **package that contains a reference** to the element that is animated, the definition of effects, and options which include timing among other things. And that is what the `KeyframeEffect` is. Our cassette tape is something that holds all the recordings and info about the length of the recordings. I will leave it for the older audience’s imagination to match all those properties with the components of a physical cassette. What I will show you is how it looks like in code.

When you create an animation through `Element.animate`, you’re using a shortcut that does three things. It creates a `KeyframeEffect` instance. It puts in into a new `Animation` instance. It immediately starts playing it.

<pre><code class="language-javascript">const animation = element.animate(keyframes, options);
</code></pre>

Let’s break it down and see the equivalent code that does the same thing.

<pre><code class="language-javascript">const animation = new Animation( // (2)
    new KeyframeEffect(element, keyframes, options) // (1)
);
animation.play(); (3)
</code></pre>

Get the cassette (1), put it into a player (2), then hit the Play button (3).

The point of knowing how it works behind the scenes is to be able to separate the definition of keyframes and deciding when to play it. When you have a lot of animations to coordinate it might be helpful to gather them all first so you know they are ready to play. Generating them on the fly and hoping they would start playing at the right moment is not something you would want to hope for. It’s too easy to break the desired effect by a few frames drag. In case of a long sequence that drag accumulates resulting in not at all convincing experience.

{{% feature-panel %}}

## Timing

As in comedy, timing is everything in animations. To make an effect work, to achieve a certain feel you need to be able to fine-tune the way properties change. There are **two levels of timing** you can control in Web Animations API.

On the level of individual properties, we have `offset`. Offset gives you **control over single property timing**. By giving it a value from zero to one you define when does each effect kick in. When omitted it equals zero.

You might remember from `@keyframes` in CSS how you can use percentages instead of `from`/`to`. That’s what `offset` is but divided by one hundred. The value of `offset` is a **portion of the duration of a single iteration**.

The `offset` allows you to arrange keyframes within a `KeyframeEffect`. Being a relative number offset makes sure that no matter the duration or the rate of playback all your keyframes start at the same moment relative to each other.

As we stated previously, `offset` is a **portion of duration**. Now I want you to avoid my mistakes and loss of time on this. It’s important to understand that duration of animation isn’t the same thing as the overall duration of an animation. Usually, they are the same and that’s what could confuse you, and what definitely confused me.

*Duration* is the **amount of time in milliseconds** that one iteration takes to finish. It will be equal to the overall duration by default. Once you add a delay or increase the number of iterations in an animation duration stops telling you the number you want to know. That is important to understand to use it to your advantage.

When you need to coordinate a keyframe playback within a bigger context, like media playback, you need to use timing options. The whole duration of the animation from start to “finished” event in the following equation:

<pre><code class="language-javascript">delay + (iterations × duration) + end delay
</code></pre>

You can see it in action in the following demo:

{{< codepen height="480" theme_id="light" slug_hash="VwWWrzz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [What is the actual duration of an animation?](https://codepen.io/smashingmag/pen/VwWWrzz) by <a href="https://codepen.io/kirillmyshkin">Kirill Myshkin</a>.{{< /codepen >}}

What this allows us to do is to **align several animations** within the context of fixed-length media. Keeping the desired duration of animation intact you could “pad” it with `delay` at the start and `delayEnd` at the end in order to embed it into a context with a longer duration. If you think about it `delay` in this sense would act as the offset does in keyframes. Just remember that delay is set in milliseconds so you might want to convert it to a relative value.

One more timing option that would help to align animation is `iterationStart`. It sets the starting position of an iteration. Take the [pool ball demo](https://codepen.io/kirillmyshkin/pen/Vwbdzqd). By adjusting `iterationStart` slider you can set the starting position of the ball and the rotation, for instance, you can set it to start jumping from the center of the screen and make the number be straight in the camera in the last frame.

{{< codepen height="480" theme_id="light" slug_hash="qBjjVPR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Tweak interationStart](https://codepen.io/smashingmag/pen/qBjjVPR) by <a href="https://codepen.io/kirillmyshkin">Kirill Myshkin</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

## Control Several As One

When I worked on animation editor for a presentation app I had to arrange several animations for a single element on a timeline. My first attempt was to use `offset` to put my animation at the right starting point on a timeline.

That quickly proved to be the wrong way of using `offset`. In terms of this particular UI moving animation on the timeline meant to shift its starting position without changing animation’s duration. With `offset` that meant I needed to change several things, the `offset` itself and also change the `offset` of closing property to make sure the duration doesn’t change. The solution proved to be too complex to comprehend.

The second problem came with the `transform` property. Due to the fact that it can represent **several characteristic changes** to an element, it can get tricky to make it do what you want. In case of a desire to change those properties independently of each other, it could become even harder. Change of scale function influences all the functions following it. Here’s why that happens.

Transform property can **take several functions in a sequence** as a value. Depending on the order of function the result changes. Take `scale` and `translate`. Sometimes it’s handy to define `translate` in percentage, which means relative to the size of an element. Say you want a ball to jump exactly three own diameters high. Now depending on where you place the scale function &mdash; before or after the `translate` &mdash; the result changes from three heights of the original size or the scaled one.

It is an important trait of `transform` property. You need it to achieve quite a complex transformation. But when you need those transformations to be distinct and independent of other transformations of an element it gets in your way.

There are cases when you cannot put all of the effects in one `transform` property. It can get too much pretty quickly. Especially if your keyframes come from different places you would need to have a **very complex merging of a transformed string**. You could hardly rely on an automatic mechanism because the logic isn’t straightforward. Also, it could get hard to understand what to expect. To simplify this and retain flexibility we need to separate those into different channels.

One solution is to **wrap our elements into `div`s** that each could be animated separately, e.g. a div for positioning on the canvas, another one for scaling, and a third one for rotation. That way, not only do you vastly simplify the definition of animations, you also open up the possibility of defining different transform origins where applicable.

It might seem that things get out of control with that trick. That we are multiplying the number of problems we had before. In fact, when I first found this trick I discarded it as being too much. I thought that I could just make sure my `transform` property is **compiled out of all the pieces** in the right order in one piece. It took one more `transform` function to make things too complex to manage and certain things impossible to do. My `transform` property string compiler started taking more and more time to get right so I gave up.

It turned out that controlling the playback of several animations is **not that hard** as it seems to be initially. Remember the cassette tape player analogy from the beginning? What if you could use your own player that takes any number of cassettes? More than that you could add as many buttons as you want on that player.

The only difference between calling `play` on a single animation and an array of animations is that you need to iterate. Here’s the code that you can use for any method of `Animation` instances:

<pre><code class="language-javascript">// To play just call play on all of them
animations.forEach((animation) => animation.play());
</code></pre>

We will use this to create all kinds of functions for our player.

Let’s create that box the would hold the animations and play them. You can create those boxes in any way that’s suitable. To make it clear, I’ll show you an example of doing it with a function and an object. The `createPlayer` function takes an array of animations that are to be played in sync. It returns an object with a single `play` method.

<pre><code class="language-javascript">function createPlayer(animations) {
    return Object.freeze({
        play: function () {
            animations.forEach((animation) => animation.play());
        }
    });
}
</code></pre>

That is enough for you to know to start expanding the functionality. Let’s add pause and `currentTime` methods.

<pre><code class="language-javascript">function createPlayer(animations) {
    return Object.freeze({
        play: function () {
            animations.forEach((animation) => animation.play());
        },
        pause: function () {
            animations.forEach((animation) => animation.pause());
        },
        currentTime: function (time = 0) {
            animations.forEach((animation) => animation.currentTime = time);
        }
    });
}
</code></pre>

The `createPlayer` with those three methods gives you **enough control to orchestrate any number of animations**. But let’s push it a bit further. Let’s make it so our player could not only take any number of cassettes but other players as well.

As we saw earlier, `Animation` interface is similar to media interfaces. Using that similarity you could put all kinds of things in your player. To accommodate for that let’s tweak the `currentTime` method to make it work with both animations objects and objects that came from `createPlayer`.

<pre><code class="language-javascript">function currentTime(time = 0) {
    animations.forEach(function (animation) {
        if (typeof animation.currentTime === "function") {
            animation.currentTime(time);
        } else {
            animation.currentTime = time;
        }
    });
}
</code></pre>

The player we just created is what will allow you to **hide the complexity** of several `div`s for single-element animations channels. Those elements could be grouped in a scene. And each scene could be a part of something bigger. All that could be done with this technique.

To demonstrate the timing demo, I divided all the animations into three players. The first one is to **control the playback** of the preview on the right. The second one combines jumping animation of all the balls’ outlines to the left and of the one in preview.

Finally, the third one is a player that **combined position animations** of the balls in a left container. That player allows the balls to spread in a continuous demonstration of the animation with about 60 frames per second slices.

{{% ad-panel-leaderboard %}}

## Conclusion

Web interfaces like Web Animations API expose for us certain things that browsers did all along. Browsers know how to render fast by passing on work to the GPU. With Web Animations API, we have control over it. Even though that control might seem a bit foreign or confusing, it doesn’t mean that using it should also be confusing. With an understanding of timing and playback control, you have tools to tame that API to your needs. You should be able to define how complex it should be.

### Further Reading

- “[Practical Techniques On Designing Animation](https://www.smashingmagazine.com/2015/06/practical-techniques-on-designing-animation/),” Sarah Drasner
- “[Designing With Reduced Motion For Motion Sensitivities](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/),” Val Head
- “[An Alternative Voice UI To Voice Assistants](https://www.smashingmagazine.com/2021/06/alternative-voice-ui-voice-assistants/),” Ottomatias Peura
- “[Designing Better Tooltips For Mobile User Interfaces](https://www.smashingmagazine.com/2021/02/designing-tooltips-mobile-user-interfaces/),” Eric Olive

{{< signature "vf, il" >}}
