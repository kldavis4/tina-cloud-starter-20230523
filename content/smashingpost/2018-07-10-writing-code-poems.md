---
title: 'Learning To Code By Writing Code Poems'
slug: writing-code-poems
author: murat-kemaldar
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/184d8bcf-8fb0-4c76-bf9f-adbae4ed746b/lovebits-start-page.png
date: 2018-07-11T14:00:32+02:00
summary: >-
  Learning to code can be tough. In this article, Murat shares his advice on how writing code differently and poetically has helped him overcome his initial struggles and insecurities.
description: >-
  Learning to code can be tough. In this article, Murat shares his advice on how writing code differently and poetically has helped him overcome his initial struggles and insecurities.
categories:
  - Tools
  - Case Studies
---
Back in 2008, I started studying design and clearly remember how the sheer sight of code just intimidated me. I had some coding classes, and without any prior coding experience, I had a tough time understanding the code I first got in touch with. Suddenly, the words that I was used to in the English language (such as "new," "return" and "throw/catch") took on a whole new meaning; the cryptic syntax, semicolons, brackets and completely new rules didn’t make things any easier for me.

If you are new to JavaScript and/or have struggles adding it to your skillset, I may have an approach for you to overcome those barriers. You are definitely not alone, and you have every right to think that learning to code is a tough nut to crack.

## Why Is Learning To Code So Tough?

Here are **some of the misconceptions** about why I think people are having a hard time learning or getting interested in JavaScript (or any coding language):

- Code is cryptic, purely functional and scary;
- Code is meant for machines only, so people do not feel addressed or engaged;
- Code is not treated as a language because it has a completely different use case and looks very different from anything they have seen before;
- People think of stereotypes (evil hackers, maybe some Matrix dudes), and thus do not identify themselves with it.

{{% feature-panel %}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce7d4c0-bc1d-428f-af64-7bb324419ce6/writing-code-poetically-baby.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce7d4c0-bc1d-428f-af64-7bb324419ce6/writing-code-poetically-baby.png" sizes="100vw" caption="Me, before any contact with code (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce7d4c0-bc1d-428f-af64-7bb324419ce6/writing-code-poetically-baby.png'>Large preview</a>)" alt="A young and unexperienced student with a pacifier and pillow" >}}

As a developer, you are expected to treat code in a very specific way &mdash; even to think in a quite different (and highly logical) way. Coding languages are quite strict and intolerant; a single character can make the machine fail to understand what you mean and make applications crash. You are expected to ignore and override certain things you know from speaking and writing a human language (which is, by the way, also the case when learning a new human language).

But not all programming languages, documentations or [video tutorials](https://www.guru99.com/) on the web are made with this “human to programming language transition” in mind. Of course, they don’t have to. After all, the main purpose of code is to tell machines what to do.

Still, due to that purpose, a chance for comparison is simply missing and the languages you speak (vocabulary and rules) seem to be rendered useless for learning a programming language. **There is no word for "love" in the JavaScript language**, nor does it make sense to say "I love you." A machine (or browser) simply does not know or care about love (yet?). This "completely new" and "don’t know where to start" feeling can be scary as hell.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba520005-77e6-471e-b5f5-4f1a69f3ca73/writing-code-poetically-baby2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba520005-77e6-471e-b5f5-4f1a69f3ca73/writing-code-poetically-baby2.png" sizes="100vw" caption="Me, after my first contact with code. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba520005-77e6-471e-b5f5-4f1a69f3ca73/writing-code-poetically-baby2.png'>Large preview</a>)" alt=" A student who is intimidated by coding languages" >}}

This is why I am here. I think that you can learn JavaScript in a much easier and artistic fashion, by holding on to your human language knowledge, and by treating JavaScript like any other human language. Let me demonstrate with a small example.

**Fun fact**: *Some programming languages actually have the transition from one programming language to another in mind. This is why it is so much easier to learn a lot of programming languages &mdash; just by learning a single one.*

## A Small Example

In a lot of cases, when you want to execute JavaScript code, you want the "document" (basically the website, a user is downloading on each visit) to be ready so that you can interact with HTML elements, for example. In pure JavaScript, you may stumble over something this:

<pre><code class="language-javascript">(function() {
   // Your code goes here
})();
</pre></code>

(Yuck! 😖 In this case, a function is defined in brackets, and then immediately called with another pair of brackets at the end. This is referred to as an [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE).)

Or sometimes like this:

<pre><code class="language-javascript">if (document.readyState === 'complete') {
  // Your code goes here
}
</pre></code>

The first snippet definitely requires an explanation, while with the second (and maybe some fantasy), one could comprehend that there is a condition which needs to be fulfilled so that something else happens just by just looking at it.

Imagine something like this, though:

<pre><code class="language-javascript">onceUponATime(function () {
  // Your code (story) goes here
})
</pre></code>

"Once upon a time" is something (dare I say) even a child might understand. It addresses the developer (by referring to childhood memories), while theoretically doing the same thing. This is what I consider "having the human to coding language transition" in mind.

**Quick note on "functions**": A function is basically a skill, which is dormant until you call upon it. "To read" is a skill `function read() { … }`, which is called upon when you are want to read something like this: `read()`. There is also something called “anonymous functions”, i.e. `"function() { … }` (has no name, like in the snippets above) which are basically "one-time / casual actions" that you wouldn’t consider to be a skill, such as "to push a button."

## Turning The Tables: From Message To Basics

So let’s take this idea a bit further. Let’s take the reasons and misconceptions above, and turn them upside-down:

<blockquote>A small poem.<br /><br />Written in JavaScript.<br /><br />Made for human beings.<br /><br />About the love between two individuals.</blockquote>

<pre><code class="language-javascript">// Love at first sight
if (me.getDistanceTo(you.position) < 200) {
  me.setFeelings({ 
    inLove: true,
  });
}
</pre></code>

It is not functional. It is currently not meant for machines. It is meant for you to read and understand.

If you got the message of the poem, you actually understood a piece of JavaScript code, which you might have compared to the English language. 

Now you might ask yourself: I understand this, but why is it written like this? What are the rules (grammar) of this language? What is the meaning of "me" (in a technical sense), and why does this code look so similar to English?

## Rules, Vocabulary, And Variables

One of the most important things to understand when learning a programming language is **the concept of variables**. 

Every human language has its rules (grammar) and a lot of vocabulary (pre-defined). Obviously, both of these first need to be learned in order to be able to speak the language.

JavaScript, like many other programming languages, also comes with its own set of rules (e.g. the `.` between the words or how `if` statements are written) and its own vocabulary (`if`, `document`, `window`, `Event`, and so on). These keywords are reserved (or ‘pre-defined’) by JavaScript (and the browser), and each one of them has its specific purpose.

But like I mentioned earlier, a chance to compare the words and sentences you know from the English language is seemingly missing because **there are no equivalents**.

This is where variables come in; you (the developer) can (or even have to) define the variables in order to make machines and developers understand what something stands for. Variables can take a lot of forms (hence the name): They can be a chain of words and letters (strings), a number, an action (function), or even a collection (array). You name it.

In all languages, there is probably a word for love. You kinda know what it means, but not really, because it is so subjective. But still, there is a word for it.

But in JavaScript, there is no "love," until you say there is. It can be whatever you want it to be.

<pre><code class="language-javascript">var love = { 
  color: 'red',
  duration: 365,
  loveTarget:  'cats',
};
// a simple variable expression,
// where love is an object "{ ... }", a thing
// with some properties (color, duration, loveTarget).

const love2 = { 
  color: 'purple',
  duration: 'forever',
  loveTarget: 'dogs',
};

// also a variable expression, where love2 (a constant),
// cannot be redefined / overwritten completely:
// love2 = undefined; // => will not work

// ("undefined" is a pre-defined javascript keyword,
// basically saying "has no value")
</pre></code>

It is crucial to be able to distinguish between what is pre-defined in JavaScript (JavaScript rules and vocabulary), and what is actually custom defined by the developer (also known as ‘application logic’ or ‘business logic’). 

Returning to the poem written above:

<pre><code class="language-javascript">// Love at first sight
if (me.getDistanceTo(you.position) < 200) {
  me.setFeelings({ 
    inLove: true,
  });
}
</pre></code>

These expressions come from the following JavaScript vocabulary/ruleset:

<div class="break-out">

<pre><code class="language-javascript">if (...) { ... } 
// if statement: when ... is met, do things in { ... }

{ 
    inLove: true, 
} 
// an "object" with some info, some thing in the world.
// can contain other info, and "skills" (functions).
// "inLove" is a custom property, 
// "true" is pre-defined in javascript, (meaning: "yes")
// and the value of "inLove".

. 
// needed to access an objects property "my name: me.name"

getDistanceTo() 
// an expression to "call" a function (a "skill").
// getDistanceTo is custom (not JavaScript), and a function, 
// so it can be executed / called upon with the "()" after. 
// sometimes you can pass arguments in those brackets (like "position")
// to change the outcome of a function.
</pre></div></code>

And these are the variables (where you have free reign over defining their names and behavior):

<div class="break-out">

<pre><code class="language-javascript">me // an object, some thing in the world
you // an object, some thing in the world
position // an info about "you", accessed by the "."
getDistanceTo // a skill of me, accessed by the "."
getDistanceTo() // the skill, with javascript grammar telling: do it.
getDistanceTo(position) // same, but do it with "position".
setFeelings // another skill of me, accessed by the "."
setFeelings({ inLove: true }); // the skill, with some instructions (an object).
</pre></div></code>

Let’s assume the poem is now human-readable. You might have understood the message, you also might see the difference between JavaScript language rules you need to follow, and the things you actually have to come up with yourself (the variables).

But what about the machine?

If the machine (the browser) were to read this poem, it would throw an error. The machine needs a definition of "me" and "you" because it tries to access its properties (via the `.` in `me.getDistanceTo()`). With the distinction ability mentioned above, you can actually engineer "me" and "you" to make the poem executeable/machine-readable, like this:

<pre><code class="language-javascript">// This is how the definition of a being (me/you) could look like

var me = {
  position: {x: 0, y: 0} // some coordinates, maybe
  getDistanceTo: function(position) { 
    // calculate the distance, relative to own position
  },
  setFeelings: function(feelings) { 
    // handle those feelings...
  }
}

var you = {
  position: {x: 0, y: 0} // some coordinates, maybe
}

// the poem itself
if (me.getDistanceTo(you.position) < 200) {
  me.setFeelings({ 
    inLove: true,
  });
}
</pre></code>

So what happened here?

- We read a JavaScript poem, written with JavaScript "grammar" with the only goal to be understood by human beings.
- After understanding the message, we distinguished between rules, vocabulary, and variables, to understand the structure of the poem (grammar and basics of JavaScript).
- With that distinction, we engineered the rest of the poems variables, with JavaScript rules in order to make it runnable by a machine (in the browser).

**This was possible, because we treated JavaScript just like the English language.**

{{% ad-panel-leaderboard %}}

## A Bigger Example: Interactive Code Poetry

This is how my personal project [LoveBits](https://lovebits.bilebile.net/) came to be. LoveBits is a code learning/storytelling experience. 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65065399-4008-4313-a3b5-2c45221d7f77/writing-code-poetically-lovebits-intro.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65065399-4008-4313-a3b5-2c45221d7f77/writing-code-poetically-lovebits-intro.gif" width="1800" height="1450" alt="Animated demonstration of the LoveBits project" /></a><figcaption>LoveBits: Code poetry project in JavaScript (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65065399-4008-4313-a3b5-2c45221d7f77/writing-code-poetically-lovebits-intro.gif">Large preview</a>)</figcaption></figure>

It tries to get people interested in JavaScript/coding by:

- Putting readability and human language first;
- Combining code with an art the reader might already be familiar with.

Storywise, it is about two Bits (rectangular beings); one of the Bits (blueBit) is the romantic one and writes JavaScript love poems to the other Bit (purpleBit).

When you start LoveBits, you can select one of the multiple love poems (written in JavaScript). Each poem has a code snippet which is written in a way that it is supposed to be understood by people who are not even familiar with programming. **The only requirement is the English language.**

"Love at first sight" (actually one of the LoveBits poems), for example, is about these two Bits in which the blueBit basically says, “If I get close enough to your position, I will ‘set my feelings’ to `inLove: true`.”

The special thing about these poems though is that you can "run" or "play" them simply by pressing the "play" button below. In the case of "Love at first sight," you would see a blue and purple rectangle along with a number. As you might've already guessed, those are the two Bits mentioned in the poem, and the number below the blueBit is actually the distance between the blueBit and the purpleBit. 

As the poem suggests, you may want to make the blueBit fall in love with the purpleBit by reducing the distance between them,  right? So what can you do? You can interact and drag the blueBit around, and make it fall in love. But be careful, sometimes there is more than just one outcome.

One might actually say that you are the machine here. You're the one who needs to interpret JavaScript code to be able to act and help two digital beings fall in love.

## Where To Go From Here?

If you are a struggling developer, try treating JavaScript like a human language, and just understand what code snippets are supposed to do first instead of what they actually end up doing.

This is what I would recommend you to do next:

- Always prefer going straight for examples and code for entire applications that combine rules, vocabulary, and variables together to form an application logic;
- Application logic will tell the stories that will help you fill the gaps like in the code examples above. Code libraries and utilities such as `lodash` will only provide you with new vocabulary which will become helpful after being able to read and understand JavaScript code;
- Review existing code, and try to break it down into small functions with names that reflect what they do. Write code which addresses humans and machines alike. Write code in such a way that it can be read like a sentence. Use comments wherever needed. Think about: How would I express this in a human language (to another developer)?

## Conclusion

Learning to code can become easier once you start treating code as a human language and not as something aliens may have invented. Learning to distinguish between language features (built-ins) and variables/custom code for application logic is crucial. Being able to understand the application logic will put you in a powerful position to improve and change things, without even knowing language features.

**Message before basics**: Understand the message of any code snippet, and the basics of JavaScript will naturally follow. How many times have you heard someone say, “I understand the language, but I do not speak it yet”? It is a natural process, which can and maybe *should* be applied for learning both human and coding languages.

Also, always keep in mind that code has a clear functional purpose, but it does not always have to be like that. Even human languages were purely functional once, but then there came poems and even songs (JavaScript songs, anyone?), which connected people in entirely different ways. I think, or hope, that the same can apply here.

Always [explore](https://github.com/explore) [code projects](https://codepen.io/pens/), and perhaps even try writing a poem yourself (maybe even in another programming language you are familiar with)? I enjoyed creating the [LoveBits](https://lovebits.bilebile.net/) project and would love to see some of your ideas in the comments below!

### Further Reading

- “[If Hemingway wrote JavaScript](https://nostarch.com/hemingway),” Angus Croll  
This is one of my favorite books which I actually stumbled upon after LoveBits. It’s about several famous poets and artists, and how they would have written JavaScript code snippets. It’s hilarious!

{{< signature "rb, ra, il" >}}
