---
title: Declarative Programming And The Web
slug: declarative-programming
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ca0d9fa-3f26-49ec-8ae3-9af11b3d5605/illu-declarative.jpg
date: 2014-07-30T21:29:38.000Z
author: scottreynen
description: >-
  Like most web developers, I spend my days giving instructions to computers. These instructions generally involve some input (a request for a web page), some logic (get the right content from a database) and some output (send the content to the requesting browser). This process of telling a computer how to
  perform a task, such as generating a web page, is what we commonly call **“programming,”** but it’s only a subset of programming: imperative programming.
categories:
  - Coding
  - Programming
  - API
---
Like most web developers, I spend my days giving instructions to computers. These instructions generally involve some input (a request for a web page), some logic (get the right content from a database) and some output (send the content to the requesting browser). This process of telling a computer how to perform a task, such as generating a web page, is what we commonly call <strong>“programming,”</strong> but it’s only a subset of programming: imperative programming.

There’s another type of programming, declarative programming, that most web developers also use every day but don’t often recognize as programming. <strong>With declarative programming, we tell a computer what, not how</strong>. We describe the result we want, and the details of how to accomplish it are left to the language interpreter. This subtle shift in approach to programming has broad effects on how we build software, especially how we build the future web.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">An Introduction To Programming Type Systems</span>](https://www.smashingmagazine.com/2013/04/introduction-to-programming-type-systems/)
*   [An Introduction To Redux](https://www.smashingmagazine.com/2016/06/an-introduction-to-redux/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)

So, let’s take a moment to investigate declarative programming and the web we can build with it.

{{% feature-panel %}}

## Hidden In Plain Sight

Declarative languages tend to fade into the background of programming, in part because they’re closer to how we naturally interact with people. If you’re talking with a friend and you want a sandwich, you don’t typically give your friend step-by-step instructions on how to make the sandwich. If you did, it would feel like programming your friend. Instead, you’re far more likely to talk about the result you want, such as “Please make me a sandwich” (or, perhaps, “<a href="https://xkcd.com/149/">Sudo make me a sandwich</a>”). If your friend is willing and able to follow this instruction, then they would translate the phrase “Make me a sandwich” into a series of steps, such as finding a loaf of bread, removing two slices, applying toppings, etc.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3634893-bbac-430f-9778-885aa3a05421/01-sandwich-opt.png" alt="01-sandwich-opt" width="360" height="299" /></figure>

This type of <strong>result-focused instruction is how declarative programming works</strong>, by leaving the logic of how to implement requests to the system that is interpreting the language (for example, your friend). When we want an image in an HTML document, for example, we simply include an <code>&lt;img&gt;</code> tag, and then the system that interprets the HTML (typically, a browser) would handle all of the steps needed to display that image, such as fetching it from a server, determining where exactly to render it, decoding the binary data, scaling the image and rendering it to the screen. We don’t have to explain any of this, so we often forget that it’s all happening and that someone programmed both how it happens and how that complex process is derived from a simple <code>&lt;img&gt;</code>.

Another factor that makes declarative programming hard to see as programming on the web is that it “just works.” A lot of work went into making languages like HTML, CSS and SQL capable of providing enough clarity on what needs to be accomplished that the steps required to achieve a result can be determined without detailed instruction. But most web developers began using these declarative languages long after the <a href="https://www.w3.org/2005/10/Process-20051014/tr">hard work</a> of building them was complete, so we just see them as <a href="https://www.goodreads.com/quotes/39828-i-ve-come-up-with-a-set-of-rules-that-describe">normal and ordinary and just a natural part of the way the web works</a>.

When web developers <em>do</em> get involved in declarative programming before the interesting work is done, it’s typically while developing an API for a website. <strong>Most APIs are implemented via declarative programming</strong>. Rather than provide a way to give a website step-by-step instructions, APIs usually have a simple language that can be used to express the desired result. When we want to get some tweets from Twitter’s API, for example, we give a description of the tweets we want, such as “everything from @A_single_bear.” If the API is imperative, we would instead describe the specific steps we want Twitter to implement on our behalf, explaining how to load, format and return the tweets. Thankfully, <strong>the API hides all of that logic behind a simple declarative language</strong>, so we only need to describe what we want, not how to get it.</p>

## Two Paths Forward

Once we realize how widespread declarative programming languages are on the web, it’s hard to imagine the web without them. Hard, but not impossible. As JavaScript has grown to be ubiquitous, the tools we would need for an imperative-only web are easy to find. We could swap out HTML and CSS for <a href="https://vps2.etotheipiplusone.com:30176/redmine/projects/emscripten-qt/wiki">rendering directly in JavaScript</a>. We could swap out SQL for a <a href="https://www.taffydb.com/">JavaScript-native database</a> (or <a href="https://github.com/kripken/sql.js">two</a>). And we could swap out calls to declarative web APIs with imperative calls to JavaScript functions, even <a href="https://www.meteor.com/">across the gap between client and server</a>.

We could put all of this together and entirely stop using declarative languages on the web, even before we get into more advanced technologies heading in our direction, like <a href="https://asmjs.org/">asm.js</a>. We can, now, build the web equivalent of mainframes: large, powerful systems built not as a collection of disparate parts but as a cohesive whole. We can now <a href="https://www.quickmeme.com/img/8d/8d30a19413145512ad5a05c46ec0da545df5ed79e113fcf076dc03c7514eb631.jpg">JavaScript all the things</a>. We’ve tried this before, with technologies like Java and ActiveX. And some organizations, such as AOL, have even had success building a less messy web-like stack. The difference this time is that the technology available to build these “mainframes” is part of the open web stack, so that <strong>anyone can now make their own self-contained web-like stack</strong>.

An imperative-only JavaScript web is enticing if we understand the web as open technologies and connected documents. But if we expand our understanding of the web to include connected systems, then <strong>declarative programming is a key part of how we connect those systems</strong>. With that understanding, we should be heading in another direction. Rather building more complex systems by replacing declarative programming languages with imperative programming, we should be wrapping more and more of our imperative code in more and better declarative languages, so that we can build future complex systems on top of our current work. Rather than looking at JavaScript as the modern Java or C++, we should be treating it as the modern shell script, a powerful tool for connecting other tools.

By defining the implementation details in the language itself, declarative programming allows imperative languages such as JavaScript, PHP and Ruby to use the results as steps in more complex behaviors. This has the advantage of making a behavior available to a variety of languages, including languages that don’t exist yet, and it also gives us a solid foundation on which to build higher. While we <em>could</em> build our own document-rendering system in JavaScript or Python, we don’t need to because HTML has already solved that problem. And we can reuse that solution in any imperative language, freeing us to solve new, larger problems. JavaScript can draw an image on a canvas <em>and</em> place it into a document with HTML. Your friend can make you a sandwich <em>and</em> a fresh lemonade. But we’ll get to this future web only by valuing declarative programming as an approach worth maintaining, now that it’s no longer the only option.</p>

## Declarative First

When we start building a tool on the web, we often jump right into making it do what we want it to do. A declarative-first approach would instead start with defining a language to succinctly describe the results we want. Before we build a new JavaScript library for building sandwiches (or, of course, <a href="https://github.com/sudo-js/make-me-a-sandwich">another</a>), let’s consider how we might describe the results in a declarative programming language. One option would look something like <code>{"bread": "rye", "cheese": "cheddar"}</code>, while another would look more like <code>&lt;sandwich&gt;&lt;cheddar /&gt;&lt;rye /&gt;&lt;/sandwich&gt;</code>. There are many choices to make when designing a declarative language, from high-level format choices (JSON? XML? YAML?) to details of data structure (is cheese an attribute of a sandwich entity or an entity in the sandwich’s toppings list?). Making these decisions early could improve the organization of your later imperative implementation. And in the long run, the declarative language might prove to be more important than the amazing sandwich-making implementation, because <strong>a declarative language can be used far beyond an individual implementation</strong>.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73299473-bada-4da0-a486-8a27409f3bca/02-sandwich-opt.png" alt="02-sandwich-opt" width="500" height="416" /></figure>

We can see some of the advantages of a declarative-first approach in public projects that have taken both approaches. For example, three years ago the Sunlight Foundation started working on a project to make it easier for people to contact members of the US Congress. They began with a Ruby app to automate the submission of contact forms, <a href="https://github.com/sunlightlabs/formageddon">Formageddon</a>. This year, they launched a new declarative-first effort toward the same goal, the <a href="https://github.com/unitedstates/contact-congress/">Contact Congress</a> project, starting with a <a href="https://github.com/unitedstates/contact-congress/blob/master/documentation/schema.md">declarative language that describes contact forms</a>.

The <a href="https://github.com/sunlightlabs/formageddon/graphs/code-frequency">activity</a> <a href="https://github.com/unitedstates/contact-congress/graphs/code-frequency">graphs</a> and timelines of the two projects make it clear which approach won out, but the benefits of the declarative approach go beyond the direct results. The YAML files produced by the declarative approach can be used to build apps like Formageddon, but they can also be used for other purposes, ones not even intended by their creators. For example, you could build an app to analyze the descriptions of contact forms to see which topics members of Congress expect to hear about from their constituents.

Successful declarative programming is in some ways more challenging than imperative programming. It requires clear descriptions, but also requires knowing enough about imperative implementation to know what needs describing. You can’t just tell an app where a form is and expect a valid submission, nor can you say <code>&lt;greatwebsite&gt;</code> to a browser and get what you want. But if you’re up for the challenge, the rewards of a declarative-first approach are also greater. <strong>Declarative languages often outlive their imperative implementations</strong>.

Try starting your next web project with declarative programming. See what languages you can find that already describe what you’re making, and write your own simple languages when you can’t find anything. Once you have a declarative definition of what you want to make, build it with an interpreter of those languages. You’ll probably end up making something more useful than you would have with an imperative-first approach to the same problem, and you’ll improve your imperative approach in the process.

{{< signature "al, ml" >}}

