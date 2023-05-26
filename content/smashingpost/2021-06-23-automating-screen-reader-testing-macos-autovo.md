---
title: 'Automating Screen Reader Testing On macOS Using Auto VO'
slug: automating-screen-reader-testing-macos-autovo
author: cameron-cundiff
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c81018b9-c45e-4c21-9762-dff84dd2682c/automating-screen-reader-testing-macos-autovo.jpg
date: 2021-06-23T09:30:00.000Z
summary: >-
  Automated testing is an important part of any software project, including testing for accessibility. There are already tools for linting and integration testing accessibility, but what about end-to-end testing with real assistive technology? Since I hadn’t seen this before, I set out to build Auto VO, a driver for the VoiceOver screen reader.
description: >-
  Automated testing is an important part of any software project, including testing for accessibility. There are already tools for linting and integration testing accessibility, but what about end-to-end testing with real assistive technology? Since I hadn’t seen this before, I set out to build Auto VO, a driver for the VoiceOver screen reader.
categories:
  - Tools
  - Accessibility
disable_ads: true
---

If you’re an accessibility nerd like me, or just curious about assistive technology, you’ll dig Auto-VO. Auto-VO is a node module and CLI for automated testing of web content with the VoiceOver screen reader on macOS.

I created [Auto VO](https://github.com/ckundo/auto-vo) to make it easier for developers, PMs, and QA to more quickly perform repeatable, automated tests with real assistive technology, without the intimidation factor of learning how to use a screen reader.

## Let’s Go!

First, let’s see it in action, and then I’ll go into more detail about how it works. Here’s running `auto-vo` CLI on smashingmagazine.com to get all the VoiceOver output as text.

<pre><code class="language-bash">$ auto-vo --url https://smashingmagazine.com --limit 200 > output.txt
$ cat output.txt
link Jump to all topics
link Jump to list of all articles
link image Smashing Magazine
list 6 items
link Articles
link Guides 2 of 6
link Books 3 of 6
link Workshops 4 of 6
link Membership 5 of 6
More menu pop up collapsed button 6 of 6
end of list
end of navigation
...(truncated)
</code></pre>

Seems like a reasonable page structure: we’ve got skip navigation links, well-structured lists, and semantic navigation. Great work! Let’s dig a little deeper though. How’s the heading structure?

<pre><code class="language-bash">$ cat output.txt | grep heading
heading level 2 link A Complete Guide To Accessibility Tooling
heading level 2 link Spinning Up Multiple WordPress Sites Locally With DevKinsta
heading level 2 link Smashing Podcast Episode 39 With Addy Osmani: Image Optimization
heading level 2 2 items A SMASHING GUIDE TO Accessible Front-End Components
heading level 2 2 items A SMASHING GUIDE TO CSS Generators & Tools
heading level 2 2 items A SMASHING GUIDE TO Front-End Performance 2021
heading level 4 LATEST POSTS
heading level 1 link When CSS Isn’t Enough: JavaScript Requirements For Accessible Components
heading level 1 link Web Design Done Well: Making Use Of Audio
heading level 1 link Useful Front-End Boilerplates And Starter Kits
heading level 1 link Three Front-End Auditing Tools I Discovered Recently
heading level 1 link Meet :has, A Native CSS Parent Selector (And More)
heading level 1 link From AVIF to WebP: A New Smashing Book By Addy Osmani
</code></pre>

Hmm! Something’s a little funky with our heading hierarchy. We ought to see an outline, with one heading level one and an ordered hierarchy after that. Instead, we see a bit of a mishmash of level 1, level 2, and an errant level 4. This needs attention since it impacts screen reader users' experience navigating the page.

Having the screen reader output as text is great because this sort of analysis becomes much easier.

## Some Background

VoiceOver is the screen reader on macOS. Screen readers let people read application content aloud, and also interact with content. That means that people with low vision or who are blind can in theory access content, including web content. In practice though, 98% of landing pages on the web have obvious errors that can be captured with automated testing and review.

There are many automated testing and review tools out there, including [AccessLint.com](https://accesslint.com) for automated code review (disclosure: I built AccessLint), and Axe, a common go-to for automation. These tools are important and useful, but they are only part of the picture. Manual testing is equally or perhaps more important, but it’s also more time-consuming and can be intimidating.

You may have heard guidance to "just turn on your screen reader and listen" to give you a sense of the blind experience. I think this is misguided. Screen readers are sophisticated applications that can take months or years to master, and are overwhelming at first. Using it haphazardly to simulate the blind experience might lead you to feel sorry for blind people, or worse, try to "fix" the experience the wrong ways.

I’ve seen people panic when they enable VoiceOver, not knowing how to turn it off. Auto-VO manages the lifecycle of the screen reader for you. It automates the launch, control, and closing of VoiceOver, so you don’t have to. Instead of trying to listen and keep up, the output is returned as text, which you can then read, evaluate, and capture for later as a reference in a bug or for automated snapshotting.

## Usage

### Caveat

Right now, because of the requirement to enable AppleScript for VoiceOver, this may require custom configuration of CI build machines to run.

#### Scenario 1: QA & Acceptance

Let’s say I (the developer) have a design with blueline annotations - where the designer has added descriptions of things like accessible name and role. Once I’ve built the feature and reviewed the markup in Chrome or Firefox dev tools, I want to output the results to a text file so that when I mark the feature as complete, my PM can compare the screen reader output with the design specs. I can do that using the auto-vo CLI and outputting the results to a file or the terminal. We saw an example of this earlier in the article:

<pre><code class="language-bash">$ auto-vo --url https://smashingmagazine.com --limit 100
</code></pre>

#### Scenario 2: Test Driven Development

Here I am again as the developer, building out my feature with a blueline annotated design. I want to test drive the content so that I don’t have to refactor the markup afterward to match the design. I can do that using the auto-vo node module imported into my preferred test runner, e.g. Mocha.

<pre><code class="language-bash">$ npm install --save-dev auto-vo
import { run } from 'auto-vo';
import { expect } from 'chai';

describe('loading example.com', async () => {
  it('returns announcements', async () => {
    const options = { url: 'https://www.example.com', limit: 10, until: 'Example' };

    const announcements = await run(options);

    expect(announcements).to.include.members(['Example Domain web content']);
  }).timeout(5000);
});
</code></pre>

## Under the Hood

Auto-VO uses a combination of shell scripting and AppleScript to drive VoiceOver. While digging into the VoiceOver application, I came across a CLI that supports starting VoiceOver from the command line.

<pre><code class="language-bash">/System/Library/CoreServices/VoiceOver.app/Contents/MacOS/VoiceOverStarter
</code></pre>

Then, a series of JavaScript executables manage the AppleScript instructions to navigate and capture VoiceOver announcements. For example, this script gets the last phrase from the screen reader announcements:

<pre><code class="language-javascript">function run() {
  const voiceOver = Application('VoiceOver');
  return voiceOver.lastPhrase.content();
}
</code></pre>

## In Closing

I’d love to hear your experience with `auto-vo`, and welcome contributions on GitHub. Try it out and let me know how it goes!

{{% feature-panel %}}

{{< signature "vf, il" >}}
