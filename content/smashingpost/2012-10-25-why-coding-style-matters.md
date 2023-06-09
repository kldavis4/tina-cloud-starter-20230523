---
title: Why Coding Style Matters
slug: why-coding-style-matters
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3af898-fcf6-44ad-b927-9d8d8eb17cb9/07-encoding-500.jpg
date: 2012-10-25T13:06:12.000Z
author: nicholas-c-zakas
description: >-
  When I was studying computer science in college, I had one extremely tough
  professor. His name was Dr. Maxey and he taught the more complicated courses
  like data structures and computer architecture. He was a wonderful teacher
  with a talent for articulating difficult concepts, but also an extremely tough
  grader. Not only would he look over your code to make sure that it worked, he
  would take off points for stylistic issues.
categories:
  - Coding
  - CSS
  - JavaScript
---
When I was studying computer science in college, I had one extremely tough professor. His name was Dr. Maxey and he taught the more complicated courses like data structures and computer architecture. He was a wonderful teacher with a talent for articulating difficult concepts, but also an extremely tough grader. Not only would he look over your code to make sure that it worked, he would take off points for stylistic issues.

If you were missing appropriate comments, or even if you misspelled a word or two in your comments, he would deduct points. If your code was “messy” (by his standards), he would deduct points. The message was clear: the quality of your code is not just in its execution but also in its appearance. That was my first experience with coding style.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/7-principles-of-clean-and-optimized-css-code/)
*   [12 Principles For Keeping Your Code Clean](https://www.smashingmagazine.com/2008/11/12-principles-for-keeping-your-code-clean/)
*   [How To Keep Your Coding Workflow Organized](https://www.smashingmagazine.com/2011/01/cleaning-up-the-mess-how-to-keep-your-coding-workflow-organized/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)

## What's A Style Anyway?

Coding style is how your code looks, plain and simple. And by “your,” I actually mean you, the person who is reading this article. Coding style is extremely personal and everyone has their own preferred style. You can discover your own personal style by looking back over code that you've written when you didn't have a style guide to adhere to.

{{% feature-panel %}}

Everyone has their own style because of the way they learned to code. If you used an integrated development environment (IDE) like Visual Studio to learn coding, your style probably matches the one enforced by the editor. If you learned using a plain text editor, your style likely evolved from what you thought was more readable.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="122954" title="Style Guide" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b27d31c3-1dd2-4086-b88f-d03588f41cfe/start-image-500.jpg" alt="Style Guide" width="500" height="332" /><br>
<em>Not only publishing houses need a style guide. If you want to keep your code readable and easy to maintain even years after you've released a website, a coding style guide is helpful and necessary. <a href="https://www.flickr.com/photos/wikidave/7118464049/sizes/c/">(Image credit: Wikidave)</a></em>

You may even notice that your style changes from language to language. The decisions that you made in JavaScript might not carry over to your CSS. For instance, you might decide JavaScript strings should use double quotes while CSS strings should use single quotes. This isn't uncommon as we tend to context switch when we switch back and forth between languages. Still, it's an interesting exercise in self-observation.

Coding style is made up of numerous small decisions based on the language:

*   How and when to use comments,
*   Tabs or spaces for indentation (and how many spaces),
*   Appropriate use of white space,
*   Proper naming of variables and functions,
*   Code grouping an organization,
*   Patterns to be used,
*   Patterns to be avoided.

This is by no means an exhaustive list, as coding style can be extremely fine-grained, such as the <a href="https://github.com/google/styleguide">Google JavaScript Style Guide</a>, or more general, such as the <a href="https://docs.jquery.com/JQuery_Core_Style_Guidelines">jQuery Core Style Guidelines</a>.</p>

## It's Personal

The personal nature of coding style is a challenge in a team atmosphere. Oftentimes, seeking to avoid lengthy arguments, teams defer creating style guides under the guise of not wanting to “discourage innovation and expression.” Some see team-defined style guides as a way of forcing all developers to be the same. Some developers rebel when presented with style guides, believing that they can't properly do their job if someone is telling them how to write their code.

I liken the situation to a group of musicians trying to form a band. Each one comes in believing that their way of doing things is best (their “method” or “process”). The band will struggle so long as everyone is trying to do their own thing. It's impossible to create good music unless everyone in the band agrees on the tempo, the style and who should take lead during a song. Anyone who has ever heard a high school band perform knows this to be true. Unless everyone is on the same page, you aren't going to accomplish much.

That's why I strongly recommend style guides for software development teams. Getting everyone on the same page is difficult, and the style guide is a great place to start. By having everyone write code that looks the same, you can avoid a lot of problems down the road.</p>

## Communication Is Key

<blockquote>“Programs are meant to be read by humans and only incidentally for computers to execute.”

— H. Abelson and G. Sussman (in “Structure and Interpretation of Computer Programs”)</blockquote>

The most important thing when working on a team is communication. People need to be able to work together effectively and the only way to do that is by communicating. As developers, we communicate primarily through code. We communicate with other parts of the software through code and we communicate with other developers through code.

While the software your code communicates with doesn't care how the code looks, the other developers on your team certainly do. The way code looks adds to our understanding of it. How many times have you opened up a piece of code that somebody else wrote, and, before doing anything else, re-indented it the way that you like? That's your brain not being able to figure out the code because of how it looks. When everyone is writing code that looks different, everyone is constantly trying to visually parse the code before being able to understand it. When everyone is writing code that looks the same, your brain can relax a bit as the understanding comes faster.

<a href="https://www.bbc.co.uk/gel"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="122964" title="BBC GEL" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f91b60-7e40-47a5-b854-ae0215f523e1/gel2-500.jpg" alt="BBC GEL" width="448" height="317" /></a><br>
<em>Not only designers can use style guides to ensure consistent visual design and informed design decisions (like in BBC's <a href="https://www.bbc.co.uk/gel">GEL</a> example above). We could use them on the macrolevel as well: for the little fine details in our code.</em>

When you start thinking of code as communication with other developers, you start to realize that you're not simply writing code, you're crafting code. Your code should clearly communicate its purpose to the casual observer. Keep in mind, your code is destined to be maintained by somebody other than you. You are not just communicating with other members of your team in the present, you're also communicating with members of your team in the future.

I recently received an email from someone who is working on code that I wrote 10 years ago. Apparently, much to my shock and horror, my code is still being used in the product. He felt compelled to email me to say that he enjoyed working with my code. I smiled. My future teammate actually did appreciate the coding style I followed.</p>

## Leave Yourself Clues

<blockquote>“If you know your enemies and know yourself, you will not be imperiled in a hundred battles.”

— Sun Tzu (in “The Art of War”)</blockquote>

Knowing yourself is important in life as well as coding. However, you'll never know yourself well enough to remember exactly what you were thinking when you wrote each line of code. Most developers have experienced looking at a very old piece of code that they wrote and not having any idea why they wrote it. It's not that your memory is bad, it's just that you make so many of these little decisions while writing code that it's impossible to keep track of them all.

Writing code against a style guide outsources that information into the code itself. When you decide when and where to use comments, as well as which patterns should and shouldn't be used, you are leaving a breadcrumb trail for your future self to find your way back to the meaning of the code. It's incredibly refreshing to open up an old piece of code and have it look like a new piece of code. You're able to acclimate quickly, sidestepping the tedious process of relearning what the code does before you can start investigating the real issue.

As <a href="https://chriseppstein.github.com/">Chris Epstein</a> once said during a talk, “be kind to your future self.”

## Make Errors Obvious

One of the biggest reasons to have a coherent style guide is to help make errors more obvious. Style guides do this by acclimating developers to certain patterns. Once you're acclimated, unfamiliar patterns jump out of the code when you look at it. Unfamiliar patterns aren't always errors, but they definitely require a closer look to make sure that nothing is amiss.

For example, consider the JavaScript <code>switch</code> statement. It's a very common error to mistakenly allow one <code>case</code> to fall through into another, such as this:

<pre><code class="language-javascript">switch(value) {
    case 1:
        doSomething();

    case 2:
        doSomethingElse();
        break;

    default:
        doDefaultThing();
}</code></pre>

The first case falls through into the second case so if <code>value</code> is 1, then both <code>doSomething()</code> and <code>doSomethingElse()</code> are executed. And here's the question: is there an error here? It's possible that the developer forgot to include a <code>break</code> in the first case, but it's also equally possible that the developer intended for the first case to fall through to the second case. There's no way to tell just from looking at the code.

Now suppose you have a JavaScript style guide that says something like this:
<blockquote>“All <code>switch</code> statement cases must end with <code>break</code>, <code>throw</code>, <code>return</code>, or a comment indicating a fall-through.”</blockquote>

With this style guide, there is definitely a stylistic error, and that means there could be a logic error. If the first case was supposed to fall through to the second case, then it should look like this:

<pre><code class="language-javascript">switch(value) {
    case 1:
        doSomething();
        //falls through

    case 2:
        doSomethingElse();
        break;

    default:
        doDefaultThing();
}</code></pre>

If the first case wasn't supposed to fall through, then it should end with a statement such as <code>break</code>. In either case, the original code is wrong according to the style guide and that means you need to double check the intended functionality. In doing so, you might very well find a bug.

When you have a style guide, code that otherwise seems innocuous immediately raises a flag because the style isn't followed. This is one of the most overlooked aspects of style guides: by defining what correct code looks like, you are more easily able to identify incorrect code and therefore potential bugs before they happen.

## Devil In The Details

In working with clients to develop their code style guides, I frequently get asked if the minutia is really that important. A common question is, “aren't these just little details that don't really matter?” The answer is yes and no. Yes, code style doesn't really matter to the computer that's running it; no, the little details matter a lot to the developers who have to maintain the code. Think of it this way: a single typo in a book doesn't disrupt your understanding or enjoyment of the story. However, if there are a lot of typos, the reading experience quickly becomes annoying as you try to decipher the author's meaning despite the words being used.

Coding style is a lot like that. You are defining the equivalent of spelling and grammar rules for everyone to follow. Your style guide can get quite long and detailed, depending on which aspects of the language you want to focus on. In my experience, once teams get started on coding style guides, they tend to go into more and more detail because it helps them organize and understand the code they already have.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="122958" title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21b2f74e-fd89-4212-b034-0eb724286627/coding-500.jpg" alt="Order In Your Code" width="500" height="333" /><br>
<em>In art, numbers are usually chaotic and serve a visual purpose. But you need order in your code. <a href="https://www.flickr.com/photos/73807667@N02/8021619893/sizes/c/">(Image credit: Alexflx54)</a></em>

I've never seen a coding style guide with too much detail, but I have seen them with too little detail. That's why it's important for the team to develop a style guide together. Getting everyone in the same room to discuss what's really important to the team will result in a good baseline for the style guide. And keep in mind, the style guide should be a living document. It should continue to grow as the team gets more familiar with each other and the software on which they are working.</p>

## Tools To Help

Don't be afraid of using tools to help enforce coding style. Web developers have an unprecedented number of tools at their fingertips today, and many of them can help ensure that a coding style guide is being followed. These range from command line tools that are run as part of the build, to plugins that work with text editors. Here are a few tools that can help keep your team on track:

*   [Eclipse Code Formatter](https://eclipseone.wordpress.com/2009/12/13/automatically-format-and-cleanup-code-every-time-you-save/) The Eclipse IDE has built-in support for code formatting. You can decide how specific languages should be formatted and Eclipse can apply the formatting either automatically or on demand.
*   [JSHint](https://jshint.com) A JavaScript code quality tool that also checks for stylistic issues.
*   [CSS Lint](https://csslint.net) A CSS code quality tool by Nicole Sullivan and me that also checks for stylistic issues.
*   [Checkstyle](https://checkstyle.sourceforge.net/) A tool for checking style guidelines in Java code, which can also be used for other languages.

These are just a small sampling of the tools that are currently available to help you work with code style guides. You may find it useful for your team to share settings files for various tools so that everyone's job is made easier. Of course, building the tools into your continuous integration system is also a good idea.</p>

## Conclusion

Coding style guides are an important part of writing code as a professional. Whether you're writing JavaScript or CSS or any other language, deciding how your code should look is an important part of overall code quality. If you don't already have a style guide for your team or project, it's worth the time to start one. There are a bunch of style guides available online to get you started. Here are just a few:

*   [jQuery Core Style Guidelines](https://docs.jquery.com/JQuery_Core_Style_Guidelines)
*   [Google JavaScript Style Guide](https://github.com/google/styleguide)
*   [Google HTML/CSS Style Guide](https://github.com/google/styleguide)
*   [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js/)
*   [Principles of Writing Consistent, Idiomatic CSS](https://github.com/necolas/idiomatic-css)
*   [GitHub Style Guide (Ruby, HTML, CSS and JavaScript)](https://github.com/styleguide/)

It's important that everybody on the team participates in creating the style guide so there are no misunderstandings. Everyone has to buy in for it to be effective, and that starts by letting everyone contribute to its creation.

{{< signature "cp" >}}

