---
title: Enhancing User Experience With The Web Speech API
slug: enhancing-ux-with-the-web-speech-api
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535f26fc-04b7-4070-9d54-c5cf7c312f17/siri-microphone-opt.jpg
date: 2014-12-05T23:00:23.000Z
author: ruthjohn
summary: >-
  It’s an exciting time for web APIs, and one to watch out for is the Web Speech API. It enables websites and web apps not only to speak to you, but to listen, too. It’s still early days, but this functionality is set to open a whole array of use cases. I’d say that’s pretty awesome.
description: >-
  The Web Speech API enables websites and web apps not only to speak to you, but to listen, too. It’s still early days, but this functionality is set to open a whole array of use cases, which makes it pretty awesome.
categories:
  - Coding
  - Techniques
  - Technology
  - Accessibility
  - API
---
In this article, we’ll look at the technology and its proposed usage, as well as some great examples of how it can be used to enhance the user experience.

**Disclaimer**: *This technology is pretty cutting-edge, and the specification is currently with the W3C as an “unofficial editor’s draft” (as of 6 June 2014). The likelihood that usage will differ slightly from the code snippets in this article is high. [Checking the specification](https://dvcs.w3.org/hg/speech-api/raw-file/tip/webspeechapi.html) and testing thoroughly before releasing code are always wise.*

<figure><a href="https://slides.com/schold/web-speech-api#/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535f26fc-04b7-4070-9d54-c5cf7c312f17/siri-microphone-opt.jpg" width="500" height="283" /></a><figcaption>Image credit: <a href="https://slides.com/schold/web-speech-api#/">Sebastian Schöld</a></figcaption></figure>

## Speech Synthesis

<p>The API comes in two parts. To start, let’s look at the speech synthesis part, the bit that speaks to you. If your website has some textual content — whether body copy, forms inputs, <code>alt</code> tags, etc. — you could run some lovely functions and the device would speak the words to the user.</p>

<p>Let’s look at some of the code needed to make this happen. First, you would create a new instance of the <code>SpeechSynthesisUtterance</code> interface. Then, you would specify the text to be spoken. Then, you would add this instance to a queue, which tells the browser what to speak and when.</p>

{{% feature-panel %}}

<p>Below I have wrapped all of this in a function for us to call, named <code>speak</code>, with the text we want spoken as a parameter.</p>

<pre><code class="language-javascript">function speak(textToSpeak) {
   // Create a new instance of SpeechSynthesisUtterance
   var newUtterance = new SpeechSynthesisUtterance();

   // Set the text
   newUtterance.text = textToSpeak;

   // Add this text to the utterance queue
   window.speechSynthesis.speak(newUtterance);
}
</code></pre>

All we need to do now is call this function and pass in some words to be spoken:

<pre><code class="language-javascript">speak('Welcome to Smashing Magazine');
</code></pre>

<p>More functionality is included in <code>SpeechSynthesisUtterance</code>. You can stop, start and pause the queue, as well as set the language, rate and voice for each utterance. Stopping, starting or pausing an utterance fires an event that you can hook into, as does changing the voice. Plenty to play around with!</p>

At the moment, speech synthesis is supported only in Chrome and Safari (both on desktop and mobile devices). Also, the voices available to you via the API largely depend on the operating system. Google has its own set of default voices for Chrome, available on Mac OS X, Windows and Ubuntu. However, Mac OS X’s voices are also available and, thus, are the same as in Safari on OSX. You can easily see which voices are available in the Developer Tools console:

<pre><code class="language-javascript">window.speechSynthesis.getVoices();
</code></pre>

Tip: If you’re on OS X, check out the voice “Zarvox.”

## Speech Recognition

The other part of the Web Speech API is speech recognition, which enables the user to speak into the device’s microphone and have their speech recognized by the website or web app.

<p>Let’s run through some code. This time, we’ll create a new instance of the <code>SpeechRecognition</code> interface. Because this part is supported only in Chrome, we’ll have to include the <code>webkit</code> prefix.</p>

<pre><code class="language-javascript">var newRecognition = webkitSpeechRecognition();
</code></pre>

<p><code>SpeechRecognition</code> comes with quite a few attributes. One that we are likely to change is <code>continuous</code>, whose default state of <code>false</code> means that the browser will stop listening after a break in speech. If you want your website or web app to keep listening, then set the attribute to <code>true</code>:</p>

<pre><code class="language-javascript">newRecognition.continuous = true;
</code></pre>

<p>To start and stop speech recognition, call the <code>start()</code> and <code>stop()</code> methods:</p>

<pre><code class="language-javascript">// start recognition
newRecognition.start();

// stop recognition
newRecognition.stop();
</code></pre>

<p>Again, we can hook into plenty of events, such as <code>soundstart</code>, <code>speechstart</code>, <code>result</code> and <code>error</code>. I have <a href="https://codepen.io/Rumyra/pen/bCphe">prepared a demo</a> that shows how to access the words detected, from the <code>result</code> event method. The code goes on to match the words spoken against some simple navigation, activating the appropriate link if detected.</p>

## Uses

### Dictation

<p>At the moment, the most common use of the Speech API is as a dictation or reading mechanism. That is, the user speaks into the mic and the device translates the speech into text (as <a href="https://www.google.com/intl/en/chrome/demos/speech.html">demoed by Chrome’s development team</a>), or the user passes in text to be read out by the device.</p>

Having a device speak out some information definitely has its advantages. Imagine your mirror telling you what the weather will be like first thing in the morning.

Plenty of car manufacturers have installed text-to-speech capabilities over the last couple of years. Imagine, in the not-too-distant future, your browser’s reading list being read out to you as you drive.

### Voice Control

Dictation could easily be turned into voice control, as we saw with the recognition demo above, which could be modified to allow for navigation around a website. Add it to web-enabled TVs and we might just be living in the 2015 of Back to the Future 2.

I’m fortunate to work with some very talented colleagues, one of whom created a tennis scoring app. I was delighted to find that he could control the app with his voice, speaking the score out loud as he was playing a game.

### Translation

<p>Translation would look very different when done in real time. Someone could converse in one language, and another person’s device would speak out what is being said in their own language. Hook that up to a Bluetooth ear piece and eat your heart out <a href="https://en.wikipedia.org/wiki/Arthur_Dent">Arthur Dent</a>. We’re getting a little closer to each person having their own <a href="https://en.wikipedia.org/wiki/List_of_races_and_species_in_The_Hitchhiker%27s_Guide_to_the_Galaxy#Babel_fish">Babel fish</a>.</p>

## Limitations

Offline capability needs more consideration. As it stands, Chrome sends the recorded audio to its servers and pings back the result. Thus, an Internet connection is needed for it to work — not ideal.

## Conclusion

Nevertheless, it is still exciting, and the technology is opening up. I look forward to the day when looking for the remote is a thing of the past, and I can just tell the TV to stream the latest Sin City movie.

Would we actually use the web for this? Why not? It’s already universal. You can take the web and its speech wherever you go.

I have met some resistance when talking about this API. People either can’t see a need for it with the web, or they would feel uncomfortable talking to their device — both valid views. However, I hope I have inspired you to at least give it a go and think about it the next time you are building something. Start welcoming speech: It might be just what you’re listening for.

### <span class="rh">Further Reading</span> on SmashingMag:

- [Experimenting With speechSynthesis](https://www.smashingmagazine.com/2017/02/experimenting-with-speechsynthesis/)
- [Improving The UX Of Names With Vocalizer.js](https://www.smashingmagazine.com/2016/12/improving-ux-names-vocalizer-js/)
- [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)
- [Conversational Interfaces: Where Are We Today?](https://www.smashingmagazine.com/2016/07/conversational-interfaces-where-are-we-today-where-are-we-heading/)

{{< signature "ml, al, il" >}}
