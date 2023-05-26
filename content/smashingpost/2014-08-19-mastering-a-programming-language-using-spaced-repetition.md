---
title: Tips For Mastering A Programming Language Using Spaced Repetition
slug: mastering-a-programming-language-using-spaced-repetition
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36a6dec1-b69e-489e-921e-36ee8a0a7512/programming-illu-345143.jpg
date: 2014-08-19T20:39:02.000Z
author: mattangriffel
description: >-
  Since first hearing of spaced repetition a few years back, I’ve used it for a
  wide range of things, from learning people’s names to memorizing poetry to
  increasing my retention of books. Today, I’ll share best practices that I’ve
  discovered from using spaced repetition to learn and master a programming
  language.

  Some great articles on this topic are already out there, including
  “[Memorizing a Programming Language Using Spaced Repetition
  Software](https://sivers.org/srs)” by Derek Sivers and “[Janki
  Method](https://www.jackkinsella.ie/2011/12/05/janki-method.html)” by Jack
  Kinsella. But because you’re busy, I’ll quickly summarize some of the best
  practices that I’ve learned along the way.
categories:
  - Coding
  - Tools
  - Techniques
  - Programming
---
Since first hearing of spaced repetition a few years back, I’ve used it for a wide range of things, from learning people’s names to memorizing poetry to increasing my retention of books.

Today, I’ll share best practices that I’ve discovered from using spaced repetition to learn and master a programming language.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Get Started With Ruby](https://www.smashingmagazine.com/2012/05/beginners-guide-ruby/)
*   [Crucial Concepts Behind Advanced Regular Expressions](https://www.smashingmagazine.com/2009/05/introduction-to-advanced-regular-expressions/)
*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [An Introduction To Object Oriented CSS (OOCSS)](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)

Some great articles on this topic are already out there, including “<a href="https://sivers.org/srs">Memorizing a Programming Language Using Spaced Repetition Software</a>” by Derek Sivers and “<a href="https://www.jackkinsella.ie/2011/12/05/janki-method.html">Janki Method</a>” by Jack Kinsella. But because you’re busy, I’ll quickly summarize some of the best practices that I’ve learned along the way.

{{% feature-panel %}}

First things first.</p>

## What Is Spaced Repetition?

Spaced repetition is a system for permanently remembering something using the minimum number of repetitions necessary. The most popular tool for this is <a href="https://ankisrs.net/">Anki</a>, a free desktop app that enables you to create and review digital flashcards organized by deck.

In short, whenever you want to remember something, you would create a card in Anki and review it regularly.

The cool part about Anki is that, if you do it right, you’ll need to spend only about 5 to 10 minutes a day reviewing your cards. If you do this, you’ll be able to remember way more than you ever imagined, and you’ll be much more productive.

Let’s dive into the specifics.</p>

### How to Use Anki

For anything you want to learn, create a flashcard with a front and a back. When you review a card, Anki will show you the front, hiding the answer side.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b46218f-714c-4b58-9728-932c02175440/01-flashcard-front-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d662a687-ffa0-4479-9f5c-555ff8fb0b51/01-flashcard-front-opt-500.jpg" alt="Front side of Anki flashcard on coding" width="500" height="225" /></a><figcaption>Front side of flashcard (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b46218f-714c-4b58-9728-932c02175440/01-flashcard-front-opt.jpg">View large version</a>)</figcaption></figure>

Answer the question in your head, and then reveal the other side to see whether you got it right.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed5715af-b26f-4bc3-8d65-021099c87ac3/02-flashcard-back-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e0b40af-11f2-45de-bd68-626a03dbd8d6/02-flashcard-back-opt-500.jpg" alt="Back side of Anki flashcard on coding" width="500" height="283" /></a><figcaption>Back side of flashcard (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed5715af-b26f-4bc3-8d65-021099c87ac3/02-flashcard-back-opt.jpg">View large version</a>)</figcaption></figure>

Then, assess how easily you answered the question, and select one of four options: “again,” “hard,” “good” or “easy.” Based on your selection, Anki figures out when to show you that card again.

And, yes, you can even use images in your cards.

By now, you’re excited to get started. But before you do, let me share a few tips.

## 1\. Break Down Your Knowledge Into The Smallest Possible Units

Though not obvious at first, there are good and bad ways to create cards. For example, here’s a bad way to write a card:

*   **Front**.  What does Ruby’s `strip` method do?
*   **Back**.  It trims spaces and blank lines from the beginning and end of a string.</p>

### Why Is This bad?

First, you probably won’t be able to remember how exactly you phrased the answer because it will have been so long ago. So, each time you answer the card, you’ll have to judge whether the way you’ve explained it corresponds to what you wrote on the back of the card.

Secondly, answers that are open-ended and that consist of more than just one or two words take longer to answer. Even if it takes only a few extra seconds, those extra seconds add up over time.

Thirdly, you wouldn’t be learning how to apply this concept. Definitions are not as practical as clear examples.

Instead, I would do this:

*   **Front**.  What Ruby method would you use to format `" Jessica "`?
*   **Back** `strip`

That’s much easier.

For a great guide to formatting knowledge, check out “<a href="https://www.supermemo.com/articles/20rules.htm">20 Rules of Formulating Knowledge</a>” by Piotr Wozniak.</p>

## 2\. Use Cloze Deletion

Following the rule above about Ruby methods was pretty easy until someone told me that class names, module names and constants start with an uppercase letter in Ruby. So, I created the following card:

*   **Front**.  In Ruby, which things begin with an uppercase letter? (Hint: three things)
*   **Back**.  Class names, module names and constants

The problem is that I had to recall three things, and the question was ambiguous, so it took a long time to understand.

Then, I learned about a feature of Anki called cloze deletion.

Instead of setting a front and back of a card, you would use cloze deletion to set a block of text and then tell Anki which bits of the text to remove from the card and to test you on. It looks something like this:

*   **Text**.  In Ruby, `{{c1::class names}}`, `{{c2::module names}}` and `{{c3::constants}}` start with `{{c4::an uppercase letter.}}`.”

This generates four cards, each of which blanks out only one of those variables.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a69e656b-63b8-480e-8a3a-d40750865f2d/03-deletioncard-front-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68977ffc-95b9-4fe3-a567-67c039afd944/03-deletioncard-front-opt-500.jpg" alt="Front of cloze deletion card" width="500" height="133" /></a><figcaption>Front of cloze deletion card (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a69e656b-63b8-480e-8a3a-d40750865f2d/03-deletioncard-front-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f3bd5ac-48f4-4277-9b95-4beca54d24e0/04-deletioncard-back-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9efbbd1-d0ce-40fb-81a6-3dd11b60b71e/04-deletioncard-back-opt-500.jpg" alt="Back of cloze deletion card" width="500" height="153" /></a><figcaption>Back of cloze deletion card (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f3bd5ac-48f4-4277-9b95-4beca54d24e0/04-deletioncard-back-opt.jpg">View large version</a>)</figcaption></figure>

There’s even a bad-ass plugin, <a href="https://ankiweb.net/shared/info/282798835">Image Occlusion</a>, to apply cloze deletion to images.

## 3\. Add A Card Only After You’ve Tested It

While Anki is an incredible learning aid, it’s only one way to retain information. At the end of the day, you need to apply what you’re learning. Remembering a concept will be much easier if you have experience applying it.

If you only read about a programming concept without trying it out for yourself, then your understanding will probably be incomplete. When I think something is trivial or obvious, like where to put a space or comma, I’ll usually have a hard time remembering it when it matters. For example:

*   **Front**.  In Ruby, create getter and setter methods for `name` and `email`.
*   **Back** `attr_accessor :name, :email`

Without actually trying this out, I might forget whether <code>attr_accessor</code> has a colon after it, whether it accepts strings, where the commas go, etc.

A nice side effect of this is that if you brush up on this every once in a while, you’ll sometimes find that a card is no longer accurate.</p>

## 4\. Save Cool Tricks And Best Practices

Always save tricks and best practices that you read about, see in a video or notice in other people’s code.

I once saw someone do a cool trick in the command line to display all of Ruby’s core methods in the interactive Ruby shell (IRB). So, I made this card:

*   **Front**.  How do you display all of the core methods in the IRB?
*   **Back** `Kernel:: + (Tab) + (Tab)`

Doing this guarantees that your code will get better over time. Even experienced developers should look out for best practices and clever techniques. It could mean the difference between quickly remembering the name of that obscure command and hunting through StackOverflow for half an hour.</p>

## 5\. Practice Every Morning For About 10 Minutes

The real value comes from frequent, short practice sessions. If you take more than a few days off, then your review backlog will grow, and you’ll have trouble recalling facts that you’ve recently learned. (Don’t worry: Anki caps each deck at 60 cards, and you can adjust this number.)

I like to practice my spaced repetition in the morning on the subway. As long as I stay up to date, it usually takes around 5 to 10 minutes to finish.

One last thing. I know that some of you will ask to see my deck. I highly recommend creating your own. Sure, you could download some decks out there to get started — such as Jack Kinsella’s web development deck or Derek Sivers’ decks for <a href="https://sivers.org/file/Ruby-sivers.apkg.zip">Ruby</a> (ZIP) and <a href="https://sivers.org/file/JavaScript-sivers.apkg.zip">JavaScript</a> (ZIP) — but your own cards will be much more personal, formatted to how you learn and recall facts. You won’t learn or remember nearly as well by using someone else’s deck.

I’m sure that my techniques will change over the next few years, so I’ll try to keep this post up to date. Have you used spaced repetition or any other techniques to master a programming language? Do you have any tips to share? Please do so in the comments below.

{{< signature "al, ml, il" >}}

