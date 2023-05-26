---
title: 'Precise Timing With Web Animations API'
slug: precise-timing-web-animations-api
author: kirill-myshkin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/942ab9f6-c68c-4eab-9dba-b98905b2b8b7/precise-timing-web-animations-api.jpg
date: 2022-06-20T09:00:00.000Z
summary: >-
  In JavaScript, it’s natural to reach for timers when something is to happen on time. But when something is to happen at the exact moment because other things depend on it, you quickly learn timers are more of a problem than a solution. They are never on time, really. Web Animations API could eliminate the need for timers in certain cases while being precise.
description: >-
  In JavaScript, it’s natural to reach for timers when something is to happen on time. But when something is to happen at the exact moment because other things depend on it, you quickly learn timers are more of a problem than a solution. They are never on time, really. Web Animations API could eliminate the need for timers in certain cases while being precise.
categories:
  - API
  - Animation
  - Interfaces
  - JavaScript
---

I previously viewed animations as something playful. Something that adds fuzziness to interfaces. Apart from that, in good hands, animation can make interfaces clearer. One property of animations on the Web that I didn’t hear much about is their precision. That Web Animations API allows us to drop workarounds concerned with JavaScript timing issues. In this article, you’ll see how not to do animations and how to coordinate animation of several elements.

When you work on a visual presentation of something that requires to be precise, you quickly learn that you spend too much time working around JavaScript’s inability to be exact about when code will actually execute. Try to implement something that relies on rhythm or shared timing and you will get my point. You might get close in certain cases but it’s never perfect.

One of the things I find helpful when working on complex problems is to **break them down into smaller, simpler problems**. It happens that smaller pieces &mdash; even if plenty &mdash; have something that unifies them. Something that allows you to treat them uniformly. In the case of animations, now that you have many more elements to deal with, you need something that will guarantee a level of timing precision that would exclude the possibility of drift, of elements going “off-beat”.

First, let’s see what could go wrong with typical tools JavaScript has to offer.

## JavaScript Timing Issues: In Order But Off Beat

In JavaScript, every task goes through a queue. Your code, user interactions, network events. Each task waits its turn to be performed by an event loop. That way, it guarantees that things happen in order: when you call a function, you can be sure no sudden mouse move would inject itself in the middle. When you need things to happen later, you can register an event listener or a timer.

When event fires or a timer is due, the task you defined in a callback goes into the queue. Once the event loop gets to it, your code gets executed. It’s a powerful concept that allows us to mostly ignore concurrency. It works well, but you better understand how it works.

We’ll look into the consequences of this in the context of animations. I encourage you to learn this topic deeper. Understanding the nature of how JavaScript work, will save you hours and will keep color in your hair. [Jake Archibald](https://github.com/jakearchibald/) has done a great job of breaking it all down in his “[Tasks, Microtasks, Queues and Schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)” article and more recently in his “[In The Loop](https://www.youtube.com/watch?v=cCOL7MC4Pl0)” talk at JSConf.

Here’s what awaits you once you’ve decided to do animations with `setTimeout` or `setInteval`:

- [Low Precision](#low-precision)
- [Pile Ups](#pile-ups)
- [Crowded Queue ](#crowded-queue)

### Low Precision

We can define exactly how long a timeout should wait before placing our task in the queue. What we cannot predict is what will be in the queue at the moment. It is possible to implement self-adjusting timers by checking the difference between the planned tick length and the actual moment the code is executed. That difference is applied to the next tick timeout.

It mostly works, but if the required distance between ticks is measured in two-digit milliseconds or less, it will rarely hit at the right moment. Also, its nature (that it adjusts on execution) makes it hard to visualize something rhythmical. It will show the precise state when it was called, but not the exact moment the state has changed.

That is because `setTimeout` guarantees minimum delay before a thing gets put in the queue. But there’s no way to tell what will be in the queue already.

### Pile Ups

If low precision is fine for you occasionally, you’ll get a pile. Things you’ve meant to be spaced out in time might be executed all at once if there were many tasks for the event loop to work on &mdash; or it could all get suspended.
  
Advancements in battery life come with better hardware and efficient software. Browser tabs might get suspended to reduce power consumption when not in use. When the tabs are in focus again, the event loop might find itself with a handful of callbacks &mdash; some of which are issued by timers &mdash; in the queue to process.
  
Once I had to implement randomly flipping tiles for a website, and one of the bugs was caused by sleepy tabs. Because each tile maintained its own timer, they all fired simultaneously when the tab became active.

{{< codepen height="480" theme_id="light" slug_hash="BaYVLGo" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}Notice how the top row blocks are delayed and then flip three at once. (See the Pen [CodePen Home Timeouts vs DocumentTimeline](https://codepen.io/smashingmag/pen/BaYVLGo) by <a href='https://codepen.io/kirillmyshkin'>Kirill Myshkin</a>){{< /codepen >}}

### Crowded Queue 

Likely, your code is already constrained by libraries and frameworks. That means callbacks from your timers are more likely to be put in a queue at an unfortunate moment. You might not have much opportunity for optimization, as there is already much code running around.
  
The shortcomings above might be resolved in certain cases. You decide for yourself what’s valued more in each particular project. If all your elements could be managed by a single timer, you might be able to make it work.

Still, I would look at `requestAnimationFrame` instead of timers to manage animations. The talk by Jake I linked to above illustrates it brilliantly. What it gives you is rhythm. You can be sure that **your code will be executed right before the user is able to see anything**. Because you have a timestamp of when your function is called, you can use that to calculate the exact state you need to have.

It’s up to you what’s worth your time to deal with. It might well be that a particular workaround is fine, and you can move on with whatever you’re trying to implement. You are a better judge of what works in your case.

If the thing you’re trying to implement fits into animations realm, you will benefit from moving it off the queue. Let’s see how we get to a place where time is king.

{{% feature-panel %}}

## Web Animations API: Where Things Are In Sync

In my previous article, “[Orchestrating Complexity With Web Animations API](https://www.smashingmagazine.com/2021/09/orchestrating-complexity-web-animations-api/),” we looked at ways to make several animations be controllable as if they were one. Now we’ll look into how to make sure that all your animations start at the right moment.

### Timeline

Web Animations API introduces a notion of a timeline. By default, all the animations are tied to the [timeline of the `document`](https://developer.mozilla.org/en-US/docs/Web/API/Document/timeline). That means animations share the same “inner clock” &mdash; a clock that starts at the page load.

That shared clock is what allows us to coordinate animations. Whether it’s a certain rhythm or a pattern, you don’t need to worry that something will drag or go ahead of itself.

### Start Time

To make an animation start at a certain moment, you use the[`startTime` property](https://developer.mozilla.org/en-US/docs/Web/API/Animation/startTime). The value of `startTime` is measured in milliseconds from the page load. Animations with a start time set to `1000.5` will start their playback exactly when the document timeline’s `currentTime` property equals `1000.5`.

Notice the dot in the start time value? Yes, you can use fractions of milliseconds, it’s that precise. However, exact precision depends on [browser settings](https://developer.mozilla.org/en-US/docs/Web/API/AnimationTimeline/currentTime#reduced_time_precision).

Another useful thing is that start time can be negative as well. You’re free to set it to a moment in the future or a moment in the past. Set the value to `-1000`, and your animation state would be like it has been played for a second already when the page loads. For the user, it would seem as if the animation had started playing before they even thought to visit your page.

**Note**: *Beware that `timeline` and `startTime` are still experimental technologies.*

### Demo

To demonstrate how you can use it, I’ve set up a demo. I’ve implemented an indicator that, more than any other, depends on time precision &mdash; a clock. Well I did two, that way, one would reveal the greatness of the other. Certain things in this demo are simple enough to demonstrate the basics. There’re also some tricky parts that show you where this approach is lacking.

{{< codepen height="480" theme_id="light" slug_hash="BaYVLMj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}Digital and analog clock, both implemented digitally. (See the Pen [Clock](https://codepen.io/smashingmag/pen/BaYVLMj) by <a href='https://codepen.io/kirillmyshkin'>Kirill Myshkin</a>){{< /codepen >}}  

The movement of the analog clock is quite simple. Three hands do the same single-turn rotation &mdash; quite optimistically &mdash; infinite times. Because the clock is a precise instrument, I’ve made the seconds and minutes hands change their position at the exact moment their corresponding values change. That helps to illustrate that they change at the exact moment as their cousins on the digital clock below.

<pre><code class="language-javascript">const clock = document.getElementById("analog-clock");
const second = clock.querySelector(".second");
const minute = clock.querySelector(".minute");
const hour = clock.querySelector(".hour");

const s = 1000;
const m = s * 60;
const h = m * 60;
const d = h * 24;

const hands = [second, minute, hour];
const hand_durations = [m, h, d];
const steps = [60, 60, 120];

const movement = hands.map(function (hand, index) {
    return hand.animate(
        [
            {transform: "rotate(0turn)"},
            {transform: "rotate(1turn)"}
        ],
        {
            duration: hand_durations[index],
            iterations: Infinity,
            easing: `steps(${steps[index]}, end)`
        }
    );
});

movement.forEach(function (move) {
    move.startTime = start_time;
});
</code></pre>

Animation for each of the three hands differs in how long they do their rotation and in how many steps it’s divided. Seconds hand does a single revolution in sixty thousand milliseconds. Minutes hand does it sixty times slower than that. Hours hand &mdash; because it’s a [twenty-four-hour clock](https://en.wikipedia.org/wiki/24-hour_analog_dial) &mdash; does one in equal time it takes the minutes hand to make twenty four revolutions.

To tie the clock hands operation to the same notion of time (to make sure the minutes hand updates its position exactly at the moment the seconds hand finishes its rotation), I used the `startTime` property. All the animations in this demo are set to the same start time. And that’s all you need. Don’t worry about the queue, suspended tabs, or piles of timeouts. Define it *once* and it’s done.

The digital clock, on the other hand, is a bit counterintuitive. Each digit is a container with `overflow: hidden;`. Inside, there’s a row of numbers from zero to one sitting in equal width cells. Each digit is revealed by translating the row horizontally by width of a cell times the digit value. As with the hands on the analog clock, it was a question of setting the right duration for each digit. While all the digits from milliseconds to minutes were easy to do, the hours required some tricks &mdash; which I’ll cover below.

Let’s look at the value of `start_time` variable:

<pre><code class="language-javascript">const start_time = (function () {
    const time = new Date();
    const hour_diff = time.getHours() - time.getUTCHours();
    const my_current_time = (Number(time) % d) + (hour_diff * h);

    return document.timeline.currentTime - my_current_time;
}());
</code></pre>

To calculate the exact moment all the elements have to be started at (which is past midnight), I took the value of `Date.now()` (milliseconds since January 1, 1970), stripped full days from it, and adjusted it by the difference with UTC time. That left me with the number of milliseconds that have passed since the start of today. It is the only piece of data my clock needs to show what it is destined to show: **hours**, **minutes** and **seconds**.

To convert that value to the realm of the document, I need to adjust it based on how much time has passed since the load of this demo’s page until `Date.now()` call. To do that, I subtracted it from the `currentTime` of the document. Applying the result to an animation means that this particular animation has been playing since midnight. Apply that to all the animations, and you get a demo that has been playing since midnight.

Theoretically, we could have a clock that runs since January 1, 1970 (52 years as of this writing), but some browsers have undocumented limits for the value of animation’s duration. It would also feel right to apply some CSS to artificially age such clock &mdash; as there won’t be any other distinction from the one that has run since last night. Both of those clocks would be in perfect sync.

{{% ad-panel-leaderboard %}}

## Shortcomings Of This Approach

It is empowering to be able to implement something of this precision without any sophisticated calculations. But it only works for cases where the things you’re trying to implement could be defined with keyframes. You should decide, based on your particular case, where it would be beneficial and where it would become more cumbersome and costly to deal with shortcomings.

An alternative to Web Animations API would be to use `requestAnimationFrame` or `performance.now()`. With those, you would need to calculate interpolation yourself.

If you choose to rely on Web Animations API, you would have to face the fact that **things fit differently into a keyframe definition**. Some things might take practically no work to define because they naturally fit. Others require workarounds. Whether those workarounds add much cost or not to what you’re trying to implement should dictate your approach.

The clock demo has examples of both cases. The hands themselves were the easiest thing to do. It is a keyframe of one turn rotation with `steps` easing function to make them tick. In the end, the main movement of the demo clock took almost no work to do. I wish I could say that the digital clock was as easy to implement. But that is due to my own shortcomings, I would say.

There are three examples of workarounds I had to revert to. I hope they give you an idea of what you might need to do if you go with the animations approach. They aren’t a good representation of Web Animations API limits, they only show how a particular implementation I’ve chosen had to be changed to fit. Let’s see where I had to do additional work.

### Some Properties Won’t Animate As You Want Them To

If you look closely, each hand on the analog clock has a shadow. They add some depth and make the clock look nicer. Shadows are easily applied using `box-shadow` or `filter` CSS properties. It is animatable to a degree, but where it comes short is in the animation of the shadow direction. You don’t set it with angle value but by coordinates.

I couldn’t find a way to implement a circular movement of a shadow using two coordinates. Instead, I broke down each hand into three elements animated separately (see my previous article “[Orchestrating Complexity With Web Animations API](https://www.smashingmagazine.com/2021/09/orchestrating-complexity-web-animations-api/)” for that technique). The first one is a wrapper that contains the other two parts of a hand: body and shadow. The wrapper is the element to which the main rotation is applied to. The body defines shape, size, and color of a hand, while the shadow copies the body properties (except for the color). Plus, it has its own animation defined &mdash; it rotates around the center of its hand.

Multiplying the number of elements to deal with might seem harder to do. In the case of the shadow, though, the fact that it was eventually separated from the hand gave more flexibility. You could style it using the CSS. And because the timing has already been dealt with, having more elements doesn’t make it harder.

### Division Doesn’t Always Result In Equal Shares

The second workaround was required for the hours section of the digital clock. The clock is implemented with single digit elements. Three for milliseconds, two for seconds, and two for minutes. Hour digits don’t fit in a logic of looping keyframe.

The loops aren’t regular because there are only four hours in the twenties. I had to introduce a “wide” digit to tackle this. The wide digit has the same logic as a normal digit would have, only that it supports numbers from zero to ninety-nine &mdash; which is plenty for this case. In the end, the digital clock’s hour indicator reused the same timing options as the hours hand on the analog clocks.

### You Never Know How Long The Next Month Would Be Without Checking The Calendar

The third workaround is for the date complication. Now that I had “wide” digits element, I’ve reused it to show dates and just increased the duration from hours to days.

The problem with that approach was that the month length didn’t map perfectly with the same length animations used in the demo. You see, the calendar we use today has a messy history and is hard to fit into a simple loop. One would have to define all the exceptions of the Gregorian calendar in a single keyframe. I’ll skip doing that. I’m here to show you a workaround.

I chose to rely on `Date` instead of defining yet another flawed calendar. Who knows how many days the months will have in the future, right?

<pre><code class="language-javascript">function month() {
    const now = new Date();
    return digits(
        (new Date(now.getFullYear(), now.getMonth() + 1, 0)).getDate(),
        false
    );
}

function create_animation(digit) {
    const nr_digits = digit.firstElementChild.children.length;
    const duration = d * nr_digits;
    return digit.firstElementChild.animate(
        [
            {transform: "translateX(0)"},
            {transform: "translateX(calc(var(--len) * -2ch)"}
        ],
        {
            duration,
            easing: `steps(${nr_digits}, end)`,
            iterationStart: (d * ((new Date()).getDate() - 1)) / duration
        }
    );
}

(function set_up_date_complication() {
    const day = document.querySelector(".day");

    const new_day = day.cloneNode();
    new_day.append(month());
    day.replaceWith(new_day);

    Array.from(new_day.children).forEach(function (digit) {
        const complication = create_animation(digit);
        complication.startTime = start_time;
        complication.finished.then(set_up_date_complication);
    });
}());
</code></pre>

To make the date complication bulletproof, I defined its duration to be the length of the current month. To keep using the same start time and to avoid the limit on `duration` value, we “rewind” the animation to the correct date using `iterationStart` property.

When the month ends, we need to rebuild the date complication for the next month. The right moment to do that would be when the complication animations had finished. Unlike other animations in this demo, the date doesn’t iterate, so we will create a new date using the `finished` promise of the current month animation.

That approach suffers from the shortcomings described at the start of this article. But in the case of months, we might close our eyes on slight imprecision.

You would have to believe my word that it works. Otherwise, return to this article any last day of a month close to midnight. Who knows, you could find me on the same page, with eyes full of hope and fingers crossed.

{{% ad-panel-leaderboard %}}

## Conclusion

Animations share the same time reference, and by adjusting their `startTime` property, you can align them to any pattern you need. You can be sure they won’t drift.

Web Animations API comes with powerful tools that allow you to dramatically reduce the amount of work that your application and you have to do. It also comes with a precision that opens possibilities to implement new kinds of applications.

That power is contained in the animations realm. Whether it is suitable for your case or not is something you decide based on your needs. I hope the examples I provided in this article will give you a better idea of what path to choose.

### Further Reading On Smashing Magazine  

- “[Orchestrating Complexity With Web Animations API](https://www.smashingmagazine.com/2021/09/orchestrating-complexity-web-animations-api/),” Kirill Myshkin
- “[Understanding Easing Functions For CSS Animations And Transitions](https://www.smashingmagazine.com/2021/04/easing-functions-css-animations-transitions/),” Adrian Bece  
- “[Practical Techniques On Designing Animation](https://www.smashingmagazine.com/2015/06/practical-techniques-on-designing-animation/),” Sarah Drasner
- “[Designing With Reduced Motion For Motion Sensitivities](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/),” Val Head

{{< signature "nl, il" >}}
