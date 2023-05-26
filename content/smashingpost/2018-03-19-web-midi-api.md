---
title: 'Getting Started With The Web MIDI API'
author: peter-anglea
slug: web-midi-api
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e8852ae-f094-4c8f-a2ef-71fe2e705d6d/web-midi-api-image1.jpg
date: 2018-03-19T13:15:56+01:00
summary: >-
  Is it possible to use digital musical instruments as browser inputs? With the Web MIDI API, the answer is yes! The best part is, it’s fairly quick and easy to implement and even create a really fun project.
description: >-
  Is it possible to use digital musical instruments as browser inputs? With the Web MIDI API, the answer is yes! The best part is, it’s fairly quick and easy to implement and even create a really fun project.
categories:
  - JavaScript
  - API
  - Apps
---
As the web continues to evolve and new browser technologies continue to emerge, the line between native and web development becomes more and more blurred. New APIs are unlocking the ability to code entirely new categories of software in the browser.

Until recently, the ability to interact with digital musical instruments has been limited to native, desktop applications. The Web MIDI API is here to change that.

In this article, we’ll cover the basics of MIDI and the Web MIDI API to see how simple it can be to create a web app that responds to musical input using JavaScript.

## What Is MIDI?

MIDI has been around for a long time but has only recently made its debut in the browser. MIDI (**M**usical **I**nstrument **D**igital **I**nterface) is a technical standard that was first published in 1983 and created the means for digital instruments, synthesizers, computers, and various audio devices to communicate with each other. MIDI messages relay musical and time-based information back and forth between devices.

{{% feature-panel %}}

A typical MIDI setup might consist of a digital piano keyboard which can send messages relaying information such as pitch, velocity (how loudly or softly a note is played), vibrato, volume, panning, modulation, and more to a sound synthesizer which converts that into audible sound. The keyboard could also send its signals to desktop music scoring software or a digital audio workstation (DAW) which could then convert the signals into written notation, save them as a sound file, and more.

MIDI is a fairly versatile protocol, too. In addition to playing and recording music, it has become a standard protocol in stage and theater applications, as well, where it is often used to relay cue information or control lighting equipment.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e8852ae-f094-4c8f-a2ef-71fe2e705d6d/web-midi-api-image1.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e8852ae-f094-4c8f-a2ef-71fe2e705d6d/web-midi-api-image1.jpg" sizes="100vw" caption="MIDI lets digital instruments, synthesizers, and software talk to each other and is frequently used in live shows and theatrical productions. Photo by Puk Khantho on <a href='https://unsplash.com/photos/sWbGwr1fOUk'>Unsplash</a>." alt="A performer plays a digital piano onstage" >}}

## MIDI In The Browser

The WebMIDI API brings all the utility of MIDI to the browser with some pretty simple JavaScript. We only need to learn about a few new methods and objects.

### Introduction

First, there’s the `navigator.requestMIDIAccess()` method. It does exactly what it sounds like—it will request access to any MIDI devices (inputs or outputs) connected to your computer. You can confirm the browser supports the API by checking for the existence of this method.

<pre><code class="language-javascript">if (navigator.requestMIDIAccess) {
    console.log('This browser supports WebMIDI!');
} else {
    console.log('WebMIDI is not supported in this browser.');
}
</code></pre>

Second, there’s the `MIDIAccess` object which contains references to all available inputs (such as piano keyboards) and outputs (such as synthesizers). The `requestMIDIAccess()` method returns a promise, so we need to establish success and failure callbacks. And if the browser is successful in connecting to your MIDI devices, it will return a `MIDIAccess` object as an argument to the success callback.

<pre><code class="language-javascript">navigator.requestMIDIAccess()
    .then(onMIDISuccess, onMIDIFailure);

function onMIDISuccess(midiAccess) {
    console.log(midiAccess);

    var inputs = midiAccess.inputs;
    var outputs = midiAccess.outputs;
}

function onMIDIFailure() {
    console.log('Could not access your MIDI devices.');
}
</code></pre>

Third, MIDI messages are conveyed back and forth between inputs and outputs with a `MIDIMessageEvent` object. These messages contain information about the MIDI event such as pitch, velocity (how softly or loudly a note is played), timing, and more. We can start collecting these messages by adding simple callback functions (listeners) to our inputs and outputs.

### Going Deeper

Let’s dig in. To send MIDI messages from our MIDI devices to the browser, we’ll start by adding an `onmidimessage` listener to each input. This callback will be triggered whenever a message is sent by the input device, such as the press of a key on the piano.

We can loop through our inputs and assign the listener like this:

<pre><code class="language-javascript">function onMIDISuccess(midiAccess) {
    for (var input of midiAccess.inputs.values())
        input.onmidimessage = getMIDIMessage;
    }
}

function getMIDIMessage(midiMessage) {
    console.log(midiMessage);
}
</code></pre>

The `MIDIMessageEvent` object we get back contains a lot of information, but what we’re most interested in is the data array. This array typically contains three values (e.g. `[144, 72, 64]`). The first value tells us what type of command was sent, the second is the note value, and the third is velocity. The command type could be either “note on,” “note off,” controller (such as pitch bend or piano pedal), or some other kind of system exclusive (“sysex”) event unique to that device/manufacturer.

For the purposes of this article, we’ll just focus on properly identifying “note on” and “note off” messages. Here are the basics:

- A command value of 144 signifies a “note on” event, and 128 typically signifies a “note off” event.
- Note values are on a range from 0–127, lowest to highest. For example, the lowest note on an 88-key piano has a value of 21, and the highest note is 108. A “middle C” is 60.
- Velocity values are also given on a range from 0–127 (softest to loudest). The softest possible “note on” velocity is 1.
- A velocity of 0 is sometimes used in conjunction with a command value of 144 (which typically represents “note on”) to indicate a “note off” message, so it’s helpful to check if the given velocity is 0 as an alternate way of interpreting a “note off” message.

Given this knowledge, we can expand our `getMIDIMessage` handler example above by intelligently parsing our MIDI messages coming from our inputs and passing them along to additional handler functions.

<div class="break-out">

<pre><code class="language-javascript">function getMIDIMessage(message) {
    var command = message.data[0];
    var note = message.data[1];
    var velocity = (message.data.length > 2) ? message.data[2] : 0; // a velocity value might not be included with a noteOff command

    switch (command) {
        case 144: // noteOn
            if (velocity > 0) {
                noteOn(note, velocity);
            } else {
                noteOff(note);
            }
            break;
        case 128: // noteOff
            noteOff(note);
            break;
        // we could easily expand this switch statement to cover other types of commands such as controllers or sysex
    }
}
</code></pre></div>

### Browser Compatibility And Polyfill

As of the writing of this article, the Web MIDI API is only available natively in Chrome, Opera, and Android WebView.

{{< rimg href="https://caniuse.bitsofco.de/embed/index.html?feat=midi&periods=future_1,current,past_1,past_2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2c554cc-d1a5-45aa-82ee-e7dbb7124f2e/web-midi-api-image5.png" sizes="100vw" caption="The Web MIDI API is only available natively in Chrome, Opera, and Android WebView." alt="Browser support for Web MIDI API from caniuse.com" >}}

For all other browsers that don’t support it natively, [Chris Wilson’s WebMIDIAPIShim library](https://github.com/cwilso/WebMIDIAPIShim) is a polyfill for the Web MIDI API, of which Chris is a co-author. Simply including the shim script on your page will enable everything we’ve covered so far.

<pre><code class="language-html">&lt;script src="WebMIDIAPI.min.js"&gt;&lt;/script&gt;
&lt;script&gt;
if (navigator.requestMIDIAccess) { //... returns true
&lt;/script&gt;
</code></pre>

This shim also requires [Jazz-Soft.net’s Jazz-Plugin](https://jazz-soft.net/) to work, unfortunately, which means it’s an OK option for developers who want the flexibility to work in multiple browsers, but an extra barrier to mainstream adoption. Hopefully, within time, other browsers will adopt the Web MIDI API natively.

### Making Our Job Easier With WebMIDI.js

We’ve only really scratched the surface of what’s possible with the WebMIDI API. Adding support for additional functionality besides basic “note on” and “note off” messages starts to get much more complex.

If you’re looking for a great JavaScript library to radically simplify your code, check out [WebMidi.js](https://github.com/cotejp/webmidi) by Jean-Philippe Côté on Github. This library does a great job of abstracting all the parsing of `MIDIAccess` and `MIDIMessageEvent` objects and lets you listen for specific events and add or remove listeners in a much simpler way.

<div class="break-out">

<pre><code class="language-javascript">WebMidi.enable(function () {

    // Viewing available inputs and outputs
    console.log(WebMidi.inputs);
    console.log(WebMidi.outputs);

    // Retrieve an input by name, id or index
    var input = WebMidi.getInputByName("My Awesome Keyboard");
    // OR...
    // input = WebMidi.getInputById("1809568182");
    // input = WebMidi.inputs[0];

    // Listen for a 'note on' message on all channels
    input.addListener('noteon', 'all',
        function (e) {
            console.log("Received 'noteon' message (" + e.note.name + e.note.octave + ").");
        }
    );

    // Listen to pitch bend message on channel 3
    input.addListener('pitchbend', 3,
        function (e) {
            console.log("Received 'pitchbend' message.", e);
        }
    );

    // Listen to control change message on all channels
    input.addListener('controlchange', "all",
        function (e) {
            console.log("Received 'controlchange' message.", e);
        }
    );

    // Remove all listeners for 'noteoff' on all channels
    input.removeListener('noteoff');

    // Remove all listeners on the input
    input.removeListener();

});
</code></pre></div>

## Real-World Scenario: Building A Breakout Room Controlled By A Piano Keyboard

A few months ago, my wife and I decided to build a “breakout room” experience in our house to entertain our friends and family. We wanted the game to include some kind of special effect to help elevate the experience. Unfortunately, neither of us have mad engineering skills, so building complex locks or special effects with magnets, lasers, or electrical wiring was outside the realm of our expertise. I do, however, know my way around the browser pretty well. And we have a digital piano.

Thus, an idea was born. We decided that the centerpiece of the game would be a series of passcode locks on a computer that players would have to “unlock” by playing certain note sequences on our piano, a la Willy Wonka.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8427246c-8cb9-42d2-86f0-b33ad96311eb/web-midi-api-image2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8427246c-8cb9-42d2-86f0-b33ad96311eb/web-midi-api-image2.gif" alt="This is a musical lock" /></a><figcaption>This is a musical lock</figcaption></figure>

Sound cool? Here’s how I did it.

### Setup

We’ll begin by requesting WebMIDI access, identifying our keyboard, attaching the appropriate event listeners, and creating a few variables and functions to help us step through the various stages of the game.

<div class="break-out">

<pre><code class="language-javascript">// Variable which tell us what step of the game we're on.
// We'll use this later when we parse noteOn/Off messages
var currentStep = 0;

// Request MIDI access
if (navigator.requestMIDIAccess) {
    console.log('This browser supports WebMIDI!');

    navigator.requestMIDIAccess().then(onMIDISuccess, onMIDIFailure);

} else {
    console.log('WebMIDI is not supported in this browser.');
}

// Function to run when requestMIDIAccess is successful
function onMIDISuccess(midiAccess) {
    var inputs = midiAccess.inputs;
    var outputs = midiAccess.outputs;

    // Attach MIDI event "listeners" to each input
    for (var input of midiAccess.inputs.values()) {
        input.onmidimessage = getMIDIMessage;
    }
}

// Function to run when requestMIDIAccess fails
function onMIDIFailure() {
    console.log('Error: Could not access MIDI devices.');
}

// Function to parse the MIDI messages we receive
// For this app, we're only concerned with the actual note value,
// but we can parse for other information, as well
function getMIDIMessage(message) {
    var command = message.data[0];
    var note = message.data[1];
    var velocity = (message.data.length > 2) ? message.data[2] : 0; // a velocity value might not be included with a noteOff command

    switch (command) {
        case 144: // note on
            if (velocity > 0) {
                noteOn(note);
            } else {
                noteOff(note);
            }
            break;
        case 128: // note off
            noteOffCallback(note);
            break;
        // we could easily expand this switch statement to cover other types of commands such as controllers or sysex
    }
}

// Function to handle noteOn messages (ie. key is pressed)
// Think of this like an 'onkeydown' event
function noteOn(note) {
    //...
}

// Function to handle noteOff messages (ie. key is released)
// Think of this like an 'onkeyup' event
function noteOff(note) {
    //...
}

// This function will trigger certain animations and advance gameplay
// when certain criterion are identified by the noteOn/noteOff listeners
// For instance, a lock is unlocked, the timer expires, etc.
function runSequence(sequence) {
    //...
}
</code></pre></div>

### Step 1: Press Any Key To Begin

To kick off the game, let’s have the players press any key to begin. This is an easy first step which will clue them into how the game works and also start a countdown timer.

<div class="break-out">

<pre><code class="language-javascript">function noteOn(note) {
    switch(currentStep) {
        // If the game hasn't started yet.
        // The first noteOn message we get will run the first sequence
        case 0:
            // Run our start up sequence
            runSequence('gamestart');

            // Increment the currentStep so this is only triggered once
            currentStep++;

            break;
    }
}

function runSequence(sequence) {
    switch(sequence) {
        case 'gamestart':
            // Now we'll start a countdown timer...
            startTimer();

            // code to trigger animations, give a clue for the first lock
            break;
    }
}
</code></pre></div>

### Step 2: Play The Correct Note Sequence

For the first lock, the players must play a particular sequence of notes in the right order. I’ve actually seen this done in a real breakout room, only it was with an acoustic upright piano rigged to a lock box. Let’s re-create the effect with MIDI.

For every “note on” message received, we’ll append the numeric note value to an array and then check to see if that array matches a predefined array of note values.

We’ll assume some clues in the breakout room have told the players which notes to play. For this example, it will be the beginning of the tune to “Amazing Grace” in the key of F major. That note sequence would look like this.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a13be12b-1678-4199-bceb-2e20b1383cb8/web-midi-api-image3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a13be12b-1678-4199-bceb-2e20b1383cb8/web-midi-api-image3.png" sizes="100vw" caption="This is the correct sequence of notes that we’ll be listening for as the solution to the first lock." alt="A visual representation of the first nine notes of “Amazing Grace” on a piano" >}}

The MIDI note values in array form would be: `[60, 65, 69, 65, 69, 67, 65, 62, 60]`.

<div class="break-out">

<pre><code class="language-javascript">var correctNoteSequence = [60, 65, 69, 65, 69, 67, 65, 62, 60]; // Amazing Grace in F
var activeNoteSequence = [];

function noteOn(note) {
    switch(currentStep) {
        // ... (case 0)

        // The first lock - playing a correct sequence
        case 1:
            activeNoteSequence.push(note);

            // when the array is the same length as the correct sequence, compare the two
            if (activeNoteSequence.length == correctNoteSequence.length) {
                var match = true;
                for (var index = 0; index < activeNoteSequence.length; index++) {
                    if (activeNoteSequence[index] != correctNoteSequence[index]) {
                        match = false;
                        break;
                    }
                }

                if (match) {
                    // Run the next sequence and increment the current step
                    runSequence('lock1');
                    currentStep++;
                } else {
                    // Clear the array and start over
                    activeNoteSequence = [];
                }
            }
            break;
    }
}

function runSequence(sequence) {
    switch(sequence) {
        // ...

        case 'lock1':
            // code to trigger animations and give clue for the next lock
            break;
    }
}
</code></pre></div>

### Step 3: Play The Correct Chord

The next lock requires the players to play a combination of notes at the same time. This is where our “note off” listener comes in. For every “note on” message received, we’ll add that note value to an array; for every “note off” message received, we’ll remove that note value from the array. Therefore, this array will reflect which notes are currently being pressed at any time. Then, it’s a matter of checking that array every time a note value is added to see if it matches a master array with the correct values.

For this clue, we’ll make the correct answer a C7 chord in root position starting on middle C. That looks like this.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e750f58-a607-41e6-bb5f-73c25fc72fc5/web-midi-api-image4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e750f58-a607-41e6-bb5f-73c25fc72fc5/web-midi-api-image4.png" sizes="100vw" caption="These are the four notes that we’ll be listening for as the solution to the second lock." alt="A visual representation of a C7 chord on a piano" >}}

The correct MIDI note values for this chord are: `[60, 64, 67, 70]`.

<div class="break-out">

<pre><code class="language-javascript">var correctChord = [60, 64, 67, 70]; // C7 chord starting on middle C
var activeChord = [];

function noteOn(note) {
    switch(currentStep) {
        // ... (case 0, 1)

        case 2:
            // add the note to the active chord array
            activeChord.push(note);

            // If the array is the same length as the correct chord, compare
            if (activeChord.length == correctChord.length) {
                var match = true;
                for (var index = 0; index < activeChord.length; index++) {
                    if (correctChord.indexOf(activeChord[index]) < 0) {
                        match = false;
                        break;
                    }
                }

                if (match) {
                    runSequence('lock2');
                    currentStep++;
                }
            }
            break;
    }

function noteOff(note) {
    switch(currentStep) {
        case 2:
            // Remove the note value from the active chord array
            activeChord.splice(activeChord.indexOf(note), 1);
            break;
    }
}

function runSequence(sequence) {
    switch(sequence) {
        // ...

        case 'lock2':
            // code to trigger animations, stop clock, end game
            stopTimer();

            break;
    }
}
</code></pre></div>

Now all that’s left to do is to add some additional UI elements and animations and we have ourselves a working game!

Here’s a video of the entire gameplay sequence from start to finish. This is running in Google Chrome. Also shown is a virtual MIDI keyboard to help visualize which notes are currently being played. For a normal breakout room scenario, this can run in full-screen mode and with no other inputs in the room (such as a mouse or computer keyboard) to prevent users from closing the window.

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/cGXqjWvG_6k" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>WebMIDI Breakout Game Demo (watch in <a href="https://www.youtube.com/watch?v=cGXqjWvG_6k&feature=youtu.be">Youtube</a>)</figcaption></figure>

If you don’t have a physical MIDI device laying around and you still want to try it out, there are a number of virtual MIDI keyboard apps out there that will let you use your computer keyboard as a musical input, such as [VMPK](https://vmpk.sourceforge.net/). Also, if you’d like to further dissect everything that’s going on here, [check out the complete prototype](https://codepen.io/peteranglea/pen/KZrGxo) on CodePen.

{{< codepen height="480" theme_id="light" slug_hash="KZrGxo" default_tab="result" user="peteranglea" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/peteranglea/pen/KZrGxo/">WebMIDI Breakout Room Demo</a> by Peter Anglea (<a href="https://codepen.io/peteranglea">@peteranglea</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

## Conclusion

[MIDI.org](https://www.midi.org/articles/about-web-midi) says that “Web MIDI has the potential to be one of the most disruptive music [technologies] in a long time, maybe as disruptive as MIDI was originally back in 1983.” That’s a tall order and some seriously high praise.

I hope this article and sample app has gotten you excited about the potential that this API has to spur the development of new and exciting kinds of browser-based music applications. In the coming years, hopefully, we’ll start to see more online music notation software, digital audio workstations, audio visualizers, instrument tutorials, and more.

If you want to read more about Web MIDI and its capabilities, I recommend the following:

- "[Making the Web Rock: Web MIDI](https://webaudiodemos.appspot.com/slides/webmidi.html#/)," Chris Wilson, co-editor of Web MIDI (slide deck)
- "[Introduction to Web MIDI](https://code.tutsplus.com/tutorials/introduction-to-web-midi--cms-25220)," Stuart Memo, Envato Tuts+
- "[Creating Browser-Based Audio Applications Controlled by MIDI Hardware](https://www.toptal.com/web/creating-browser-based-audio-applications-controlled-by-midi-hardware)," Stéphane P. Péricat, Toptal

And for further inspiration, here are some other examples of the Web MIDI API in action:

- [Web Audio MIDI Synthesizer](https://webaudiodemos.appspot.com/midi-synth/index.html)
A simple synthesizer UI which can be controlled via a MIDI device
- [Web Audio Drum Machine](https://webaudiodemos.appspot.com/MIDIDrums/index.html)
A fun app to create your own drum loops
- [Noteflight](https://www.noteflight.com/)
An online music notation software which uses Web MIDI as a potential input method

{{< signature "rb, ra, hj, il" >}}

