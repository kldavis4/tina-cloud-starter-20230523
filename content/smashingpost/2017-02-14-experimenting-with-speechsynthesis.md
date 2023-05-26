---
title: Experimenting With speechSynthesis
slug: experimenting-with-speechsynthesis
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6646d871-0ecb-4521-9869-0cacd12c5056/speechsynthesis-feature-image.png
date: 2017-02-14T22:37:29.000Z
author: aarongustafson
summary: >-
  Wondering how to get started with the Web Speech API? Aaron guides you through this experimental API and covers everything you need to know to help you get a better understanding of how it works.
description: >-
  Wondering how to get started with the Web Speech API? Aaron guides you through this experimental API and covers everything you need to know to help you get a better understanding of how it works.
categories:
  - Coding
  - JavaScript
  - Browsers
  - API
---
I’ve been thinking a lot about speech for the last few years. In fact, it’s been a major focus in several of my talks of late, including my well-received Smashing Conference talk “[Designing the Conversation](https://vimeo.com/184234783)”. As such, I’ve been keenly interested in the development of the Web Speech API.

If you’re unfamiliar, this API gives you (the developer) the ability to voice-enable your website in two directions: listening to your users via the [SpeechRecognition interface](https://developer.mozilla.org/docs/Web/API/SpeechRecognition) and talking back to them via the [SpeechSynthesis interface](https://developer.mozilla.org/docs/Web/API/SpeechSynthesis). All of this is done via a JavaScript API, making it easy to test for support. This testability makes it an excellent candidate for progressive enhancement, but more on that in a moment.

A lot of my interest stems from my own personal desire to experiment with new ways of interacting with the web. I’m also a big fan of podcasts and love listening to great content while I’m driving and in other situations where my eyes are required elsewhere or are simply too tired to read. The Web Speech API opens up a whole range of opportunities to create incredibly useful and natural user interactions by being able to listen for and respond with natural language:

<blockquote>– Hey Instapaper, start reading from my queue!<br /><br />&mdash; Sure thing, Aaron...</blockquote>

The possibilities created by this relatively simple API set are truly staggering. There are applications in accessibility, Internet of Things, automotive, government, the list goes on and on. Taking it a step further, imagine combining this tech with real-time translation APIs (which also recently began to appear). All of a sudden, we can open up the web to millions of people who struggle with literacy or find themselves in need of services in a country where they don’t read or speak the language. This. Changes. Everything.

But back to the Web Speech API. As I said, I’d been keeping tabs on the specification for a while, checked out several of the demos and such, but hadn’t made the time to play yet. Then Dave Rupert finally spurred me to action with a single tweet:

<figure><a href="https://twitter.com/davatron5000/status/818493871961341953"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/831532e8-609b-491c-92db-9d720c90041d/tweet-by-dave-rupert-opt.png" alt="Tweet by Dave Rupert" width="635" height="365" /></a></figure>

Within an hour or so, I’d gotten a basic implementation together for <a href="https://www.aaron-gustafson.com/notebook/">my blog</a> that would enable users to listen to a <a href="https://www.aaron-gustafson.com/notebook/insert-clickbait-headline-about-progressive-enhancement-here/">blog post</a> rather than read it. A few hours later, I had added more features, but it wasn’t all wine and roses, and I ended up having to back some functionality out of the widget to improve its stability. But I’m getting ahead of myself.

I’ve decided to hit the pause button for a few days to write up what I’ve learned and what I still don’t fully understand in the hope that we can begin to hash out some best practices for using this awesome feature. Maybe we can even come up with some ways to improve it.

{{% feature-panel %}}

## Hello, World

So far, my explorations into the Web Speech API have been wholly in the realm of speech synthesis. Getting to “Hello world” is relatively straightforward and merely involves creating a new <code>SpeechSynthesisUtterance</code> (which is what you want to say) and then passing that to the <code>speechSynthesis</code> object’s <code>speak()</code> method:

<pre><code class="language-javascript">var to_speak = new SpeechSynthesisUtterance('Hello world!');
window.speechSynthesis.speak(to_speak);</code></pre>

Not all browsers support this API, although <a href="https://caniuse.com/#feat=speech-synthesis">most modern ones do</a>. That being said, to avoid throwing errors, we should wrap the whole thing in a simple conditional that tests for the feature’s existence <em>before</em> using it:

<pre><code class="language-javascript">if ( 'speechSynthesis' in window ) {
  var to_speak = new SpeechSynthesisUtterance('Hello world!');
      window.speechSynthesis.speak(to_speak);
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="qRZgzx" default_tab="result" user="aarongustafson" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/aarongustafson/pen/qRZgzx/">Experimenting with speechSynthesis, example 1</a> by Aaron Gustafson (<a href="https://codepen.io/aarongustafson">@aarongustafson</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<blockquote><a target="_blank" href="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/302386555&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false&amp;visual=true">Link to the example on soundcloud.com</a></blockquote>

Once you’ve got a basic example working, there’s quite a bit of tuning you can do. For instance, you can tweak the reading speed by adjusting the <code>SpeechSynthesisUtterance</code> object’s <code>rate</code> property. It accepts values from 0.1 to 10. I find 1.4 to be a pretty comfortable speed; anything over 3 just sounds like noise to me.

{{< codepen height="480" theme_id="light" slug_hash="qRZgzx" default_tab="result" user="aarongustafson" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/aarongustafson/pen/qRZgzx/">Experimenting with speechSynthesis, example 1</a> by Aaron Gustafson (<a href="https://codepen.io/aarongustafson">@aarongustafson</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

You can also tune things such as the <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/pitch">pitch</a>, the <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/volume">volume</a> of the voice, even the <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/lang">language being spoken</a> and the <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/voice">voice itself</a>. I’m a big fan of defaults in most things, so I’ll let you explore those options on your own time. For the purpose of my experiment, I opted to change the default <code>rate</code> to 1.4, and that was about it.

## A Basic Implementation: Play And Pause

When I began working with this code on my own website, I was keen to provide four controls for my readers:

*   play
*   pause
*   increase reading speed
*   decrease reading speed

The first two were relatively easy. The latter two caused problems, which I’ll discuss shortly.

To kick things off, I parroted the code Dave had tweeted:

<pre><code class="language-javascript">var to_speak = new SpeechSynthesisUtterance(
  document.querySelector('main').textContent
);
window.speechSynthesis.speak(to_speak);</code></pre>

This code grabs the text content (<code>textContent</code>) of the <code>main</code> element and converts it into a <code>SpeechSynthesisUtterance</code>. It then triggers the synthesizer to speak that content. Simple enough.

Of course, I didn’t want the content to begin reading immediately, so I set about building a user interface to control it. I did so in JavaScript, within the feature-detection conditional, rather than in HTML, because I did not want the interface to appear if the feature was not available (or if JavaScript failed for some reason). That would be frustrating for users.

I created the buttons and assigned some event handlers to wire up the functionality. My first pass looked something like this:

<pre><code class="language-javascript">var $buttons = document.createElement('p'),
    $button = document.createElement('button'),
    $play = $button.cloneNode(),
    $pause = $button.cloneNode(),
    paused = false,
    to_speak;

if ( 'speechSynthesis' in window ) {

  // content to speak
  to_speak = new SpeechSynthesisUtterance(
    document.querySelector('main').textContent
  );

  // set the rate a little faster than 1x
  to_speak.rate = 1.4;

  // event handlers
  to_speak.onpause = function(){
    paused = true;
  };

  // button events
  function play() {
    if ( paused ) {
      paused = false;
      window.speechSynthesis.resume();
    } else {
      window.speechSynthesis.speak( to_speak );
    }
  }
  function pause() {
    window.speechSynthesis.pause();
  }

  // play button
  $play.innerText = 'Play';
  $play.addEventListener( 'click', play, false );
  $buttons.appendChild( $play );

  // pause button
  $pause.innerText = 'Pause';
  $pause.addEventListener( 'click', pause, false );
  $buttons.appendChild( $pause );

} else {

  // sad panda
  $buttons.innerText = 'Unfortunately your browser doesn’t support this feature.';

}

document.body.appendChild( $buttons );</code></pre>

This code creates a play button and a pause button and appends them to the document. It also assigns the corresponding event handlers. As you’d expect, the play button calls <code>speechSynthesis.speak()</code>, as we saw earlier, but because pause is also in play, I set it up to either speak the selected text or resume speaking — using <code>speechSynthesis.resume()</code> — if the speech is paused. The pause button controls that by triggering <code>speechSynthesis.pause()</code>. I tracked the state of the speech engine using the boolean variable <code>paused</code>. You can kick the tires of this code <a href="https://codepen.io/aarongustafson/pen/ygOrNj">over on CodePen</a>.

I want to (ahem) pause for a moment to tuck into the <code>speak()</code> command, because it’s easy to misunderstand. At first blush, you might think it causes the supplied <code>SpeechSynthesisUtterance</code> to be read aloud from the beginning, which is why I’d want to <code>resume()</code> after pausing. That is true, but it’s only part of it. The speech synthesis interface actually maintains a queue for content to be spoken. Calling <code>speak()</code> pushes a new <code>SpeechSynthesisUtterance</code> to that queue and causes the synthesizer to start speaking that content if it’s not already speaking. If it’s in the process of reading something already, the new content takes its spot at the back of the queue and patiently waits its turn. If you want to see this in action, check out my <a href="https://s.codepen.io/aarongustafson/pen/ggryNo/">fork of the reading speed demo</a>.

If you want to clear the queue entirely at any time, you can call <code>speechSynthesis.cancel()</code>. When testing speech synthesis with long-form content, having this at the ready in the browser’s console is handy.

{{% ad-panel-leaderboard %}}

## Taking It Further: Adjusting Reading Speed

As I mentioned, I also wanted to give users control over the reading speed used by the speech synthesizer. We can tune this using the <code>rate</code> property on a <code>SpeechSynthesisUtterance</code> object. That’s fantastic, but you can’t (currently, at least) adjust the rate of a <code>SpeechSynthesisUtterance</code> once the synthesizer starts playing it — not even while it’s paused. I don’t know enough about the inner workings of speech synthesizers to know whether this is simply an oversight in the interface or a hard limitation of the synthesizers themselves, but it did force me to find a creative way around this limitation.

I experimented with a bunch of different approaches to this and eventually settled on one that works reasonably well, despite the fact that it feels like overkill. But I’m getting ahead of myself again.

Every <code>SpeechSynthesisUtterance</code> object offers a handful of events you can plug in to do various things. As you’d expect, <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/onpause"><code>onpause</code></a> fires when the speech is paused, <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/onend"><code>onend</code></a> fires when the synthesizer has finished reading it, etc. The <a href="https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesisEvent"><code>SpeechSynthesisEvent</code></a> object passed to each of these includes information about what’s going on with the synthesizer, such as the position of the virtual cursor (<a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisEvent/charIndex"><code>charIndex</code></a>), the length of time after the current <code>SpeechSynthesisUtterance</code> started being read (<a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisEvent/elapsedTime"><code>elapsedTime</code></a>), and a reference to the <code>SpeechSynthesisUtterance</code> itself (<a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisEvent/utterance"><code>utterance</code></a>).

Originally, my plan to allow for real-time reading-speed adjustment was to capture the virtual cursor position via a pause event so that I could stop and start a new recording at the new speed. When the user adjusted the reading speed, I would pause the synthesizer, grab the <code>charIndex</code>, backtrack in the text to the previous space, slice from there to the end of the string to collect the remainder of what should be read, clear the queue, and start the synthesizer again with the remainder of the content. That would have worked, and it should have been reliable, but Chrome kept giving me a <code>charIndex</code> of <code>0</code>, and in Edge it was always <code>undefined</code>. Firefox tracked <code>charIndex</code> perfectly. I’ve filed a <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=681026">bug for Chromium</a> and <a href="https://twitter.com/aarongustafson/status/819944910308646913">one for Edge</a>, too.

Thankfully, another event, <a href="https://developer.mozilla.org/docs/Web/API/SpeechSynthesisUtterance/onboundary"><code>onboundary</code></a>, fires whenever a word or sentence boundary is reached. It’s a little noisier, programmatically speaking, than <code>onpause</code> because the event fires so often, but it reliably tracked the position of the virtual cursor in every browser that supports speech synthesis, which is what I needed.

Here’s the tracking code:

<pre><code class="language-javascript">var progress_index = 0;

to_speak.onboundary = function( e ) {
  if ( e.name == 'word' ) {
    progress_index = e.charIndex;
  }
};</code></pre>

Once I was set up to track the cursor, I added a numeric input to the UI to allow users to change the speed:

<div class="break-out">

<pre><code class="language-javascript">var $speed = document.createElement('p'),
    $speed_label = document.createElement('label'),
    $speed_value = document.createElement('input');

// label the field
$speed_label.innerText = 'Speed';
$speed_label.htmlFor = 'speed_value';
$speed.appendChild( $speed_label );

// insert the form control
$speed_value.type = 'number';
$speed_value.id = 'speed_value';
$speed_value.min = '0.1';
$speed_value.max = '10';
$speed_value.step = '0.1';
$speed_value.value = Math.round( to_speak.rate * 10 ) / 10;
$speed.appendChild( $speed_value );

document.body.appendChild($speed);</code></pre></div>

Then, I added an event listener to track when it changes and to update the speech synthesizer:

<div class="break-out">

<pre><code class="language-javascript">function adjustSpeed() {
  // cancel the original utterance
  window.speechSynthesis.cancel();

  // find the previous space
  var previous_space = to_speak.text.lastIndexOf( ' ', progress_index );

  // get the remains of the original string
  to_speak.text = to_speak.text.slice( previous_space );

  // math to 1 decimal place
  speed = Math.round( $speed_value.value * 10 ) / 10;

  // adjust the rate
  if ( speed &gt; 10 ) {
    speed = 10;
  } else if ( speed &lt; 0.1 ) {
    speed = 0.1;
  }
  to_speak.rate = speed;

  // return to speaking
  window.speechSynthesis.speak( to_speak );
}

$speed_value.addEventListener( 'change', adjustSpeed, false );</code></pre></div>

This works reasonably well, but ultimately I decided that I was not a huge fan of the experience, nor was I convinced it was really necessary, so this functionality remains commented out in <a href="https://github.com/aarongustafson/aarongustafson.github.io/blob/source/source/_javascript/post/speak.js">my website’s source code</a>. You can make up your mind after seeing it <a href="https://codepen.io/aarongustafson/pen/vgKpMg?editors=0010">in action over on CodePen</a>.

## Taking It Further: Tweaking What’s Read

At the top of every blog post, just after the title, I include quite a bit of meta data about the post, including things like the publication date, tags for the post, comment and webmention counts, and so on. I wanted to selectively control which content from that collection is read because only some of it is really relevant in that context. To keep the configuration out of the JavaScript and in the declarative markup where it belongs, I opted to have the JavaScript look for a specific <code>class</code> name, “dont-read”, and exclude those elements from the content that would be read. To make it work, however, I needed revisit how I was collecting the content to be read in the first place.

You may recall that I’m using the <code>textContent</code> property to extract the content:

<pre><code class="language-javascript">var to_speak = new SpeechSynthesisUtterance(
  document.querySelector('main').textContent
);</code></pre>

That’s all well and good when you want to grab everything, but if you want to be more selective, you’re better off moving the content into memory so that you can manipulate it without causing repaints and such.

<div class="break-out">

<pre><code class="language-javascript">var $content = document.querySelector('main').cloneNode(true);</code></pre></div>

With a clone of <code>main</code> in memory, I can begin the process of winnowing it down to only the stuff I want:

<div class="break-out">

<pre><code class="language-javascript">var to_speak = new SpeechSynthesisUtterance()
    $content = document.querySelector('main').cloneNode(true),
    $skip = $content.querySelectorAll('.dont-read');

// don’t read
Array.prototype.forEach.call( $skip, function( $el ){
  $el.innerHTML = '';
});

to_speak.text = $content.textContent;</code></pre></div>

Here, I’ve separated the creation of the <code>SpeechSynthesisUtterance</code> to make the code a little clearer. Then, I’ve cloned the <code>main</code> element (<code>$content</code>) and built a <code>nodeList</code> of elements that I want to be ignored (<code>$skip</code>). I’ve then looped over the <code>nodeList</code> — borrowing <code>Array</code>’s handy <code>forEach</code> method — and set the contents of each to an empty string, effectively removing them from the content. At the end, I’ve set the text property to the cloned <code>main</code> element’s <code>textContent</code>. Because all of this is done to the cloned <code>main</code>, the page remains unaffected.

Done and done.

{{% ad-panel-leaderboard %}}

## Taking It Further: Synthetic Pacing Tweaks

Sadly, the value of a <code>SpeechSynthesisUtterance</code> can only be text. If you pipe in HTML, it will read the tag names and slashes. That’s why most of the demos use an input to collect what you want read or rely on <code>textContent</code> to extract text from the page. The reason this saddens me is that it means you lose complete control over the pacing of the content.

But not all is lost. Speech synthesizers are pretty awesome at recognizing the effect that punctuation should have on intonation and pacing. To go back to the first example I shared, consider the difference when you drop a comma between “hello” and “world”:

<div class="break-out">

<pre><code class="language-javascript">if ( 'speechSynthesis' in window ) {
  var to_speak = new SpeechSynthesisUtterance('Hello, world!');
  window.speechSynthesis.speak(to_speak);
} </code></pre></div>

{{< codepen height="480" theme_id="light" slug_hash="dNMrYq" default_tab="result" user="aarongustafson" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/aarongustafson/pen/dNMrYq/">Experimenting with speechSynthesis, example 2</a> by Aaron Gustafson (<a href="https://codepen.io/aarongustafson">@aarongustafson</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<blockquote><a target="_blank" href="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/302386511&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false&amp;visual=true">Link to the example on soundcloud.com</a></blockquote>

Here’s the original again, just so you can compare:

{{< codepen height="480" theme_id="light" slug_hash="qRZgzx" default_tab="result" user="aarongustafson" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/aarongustafson/pen/qRZgzx/">Experimenting with speechSynthesis, example 1</a> by Aaron Gustafson (<a href="https://codepen.io/aarongustafson">@aarongustafson</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<blockquote><a target="_blank" href="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/302386555&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false&amp;visual=true">Link to the example on soundcloud.com</a></blockquote>

With this in mind, I decided to tweak the pacing of the spoken prose by artificially inserting commas into the specific elements that follow the pattern I just showed for hiding content:

<div class="break-out">

<pre><code class="language-javascript">var $pause_before = $content.querySelectorAll(
  'h2, h3, h4, h5, h6, p, li, dt, blockquote, pre, figure, footer'
);

// synthetic pauses
Array.prototype.forEach.call( $pause_before, function( $el ){
  $el.innerHTML = ' , ' + $el.innerHTML;
});</code></pre></div>

While I was doing this, I also noticed some issues with certain elements running into the content around them. Most notably, this was happening with <code>pre</code> elements. To mitigate that, I used the same approach to swap carriage returns, line breaks and such for spaces:

<div class="break-out">

<pre><code class="language-javascript">var $space = $content.querySelectorAll('pre');

// spacing out content
Array.prototype.forEach.call( $space, function( $el ){
  $el.innerHTML = ' ' + $el.innerHTML.replace(/[\r\n\t]/g, ' ') + ' ';
});
</code></pre></div>

With those tweaks in place, I’ve been incredibly happy with the listening experience. If you’d like to see all of this code in context, head over to <a href="https://github.com/aarongustafson/aarongustafson.github.io/blob/source/source/_javascript/post/speak.js">my GitHub repository</a>. The code you use to drop the UI into the page will likely need to be different from what I did, but the rest of the code should be plug-and-play.

## Is `speechSynthesis` Ready For Production?

As it stands right now, the Web Speech API has not become a standard and <a href="https://dvcs.w3.org/hg/speech-api/raw-file/tip/webspeechapi.html#status">isn’t even on a standards track</a>. It’s an experimental API and some of the details of the specification remain in flux. For instance, the <code>elapsedTime</code> property of a <code>SpeechSynthesisEvent</code> originally tracked milliseconds and then switched to seconds. If you were doing math that relied on that number to do something else in the interface, you might get widely different experiences in Chrome (which still uses milliseconds) and Edge (which uses seconds).

If I was granted one wish for this specification—apart from standardization—it would be for real-time speed, pitch and volume adjustment. I can understand the need to restart things to get the text read in another voice, but the others feel like they should be manipulable in real time. But again, I don’t know anything about the inner workings of speech synthesizers, so that might not be technically possible.

In terms of actual browser implementations, basic speech synthesis like I’ve covered here is pretty solid in <a href="https://caniuse.com/#feat=speech-synthesis">browsers that support the API</a>. As I mentioned, Chrome and Edge currently fail to accurately report the virtual cursor position when speech synthesis is paused, but I don’t think that’s a deal-breaker. What is problematic is how unstable things get when you start to combine features such as real-time reading-speed adjustments, pausing and such. Often, the synthesizer just stops working and refuses to start up again. If you’d like to see that happen, take a look at a <a href="https://codepen.io/aarongustafson/pen/ZLOxLe">demo I set up</a>. Chances are that this issue would go away if the API allowed for real-time manipulation of properties such as <code>rate</code> because you wouldn’t have to <code>cancel()</code> and restart the synthesizer with each adjustment.

Long story short, if you’re looking at this as a progressive enhancement for a content-heavy website and only want the most basic features, you should be good to go. If you want to get fancy, you might be disappointed or have to come up with more clever coding acrobatics than I’ve mustered.

## Want To Learn More?

As with most things on the web, I learned a ton by viewing other people’s source, demos and such — and the documentation, naturally. Here are some of my favorites (some of which I linked to in context):

*   “[Web Speech API Specification: Editor’s Draft](https://dvcs.w3.org/hg/speech-api/raw-file/tip/webspeechapi.html),” W3C
*   “[Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API),” Mozilla Developer Network
*   “[Speech Synthesis API](https://caniuse.com/#feat=speech-synthesis),” Can I Use? (chart of browser support)
*   “[Web Apps That Talk: Introduction to the Speech Synthesis API](https://developers.google.com/web/updates/2014/01/Web-apps-that-talk-Introduction-to-the-Speech-Synthesis-API),” Eric Bidelman, Google Developers
*   “[Speech Synthesis API](https://developer.microsoft.com/en-us/microsoft-edge/testdrive/demos/speechsynthesis/),” Microsoft Developer (demo for Edge)

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Enhancing User Experience With The Web Speech API](https://www.smashingmagazine.com/2014/12/enhancing-ux-with-the-web-speech-api/)
*   [Guidelines For Designing With Audio](https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/)
*   [What Is User Experience Design? Overview, Tools And Resources](https://www.smashingmagazine.com/2010/10/what-is-user-experience-design-overview-tools-and-resources/)

{{< signature "rb, yk, il, al" >}}
