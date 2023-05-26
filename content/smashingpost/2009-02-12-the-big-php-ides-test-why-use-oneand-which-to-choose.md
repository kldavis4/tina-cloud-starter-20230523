---
title: 'The Big PHP IDE Test: Why Use One And Which To Choose'
slug: the-big-php-ides-test-why-use-oneand-which-to-choose
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39442f29-7fb5-45af-9346-bd963c215dce/php-01.jpg
date: 2009-02-12T00:54:51.000Z
author: alexander-makarov
description: >-
  Everyone wants to be more productive, make fewer mistakes and write good code.
  Of course, that all depends on you, but in most cases integrated development
  environments (IDEs) can help you achieve those goals more easily.
  Unfortunately, choosing the right IDE is very difficult because a lot needs to
  be considered. And the website of almost every IDE [tells us it is the best
  one](https://www.zend.com/en/products/studio/compare).
categories:
  - Coding
  - PHP
---
Everyone wants to be more productive, make fewer mistakes and write good code. Of course, that all depends on you, but in most cases integrated development environments (IDEs) can help you achieve those goals more easily. Unfortunately, choosing the right IDE is very difficult because a lot needs to be considered. And the website of almost every IDE <a href="https://www.zend.com/en/products/studio/compare">tells us it is the best one</a>.

You may also want to check out the following Smashing Magazine articles:

*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)
*   [50 Powerful Time-Savers For Web Designers](https://www.smashingmagazine.com/2010/06/50-powerful-time-savers-for-web-designers/)

In this post, we'll <strong>take a close look at the most popular PHP IDEs</strong>, exploring their functions, comparing them in a table and drawing some conclusions. Hopefully, you'll get an idea of what each PHP IDE has to offer and which one best fits your needs.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5860de2-bf42-4adf-ae81-803a38d1d892/ides-best.png" alt="I am the best!" width="577" height="299" />

{{% feature-panel %}}

For a long time, I worked in PHP only for fun. I've developed Java Web applications with Eclipse and IntelliJ IDEA. These are a great Java IDEs. Not surprisingly, I wanted something similar for PHP. The following are some of the features that I found needed to be considered.</p>

## IDE Features

### 1. Syntax highlighting

Good syntax highlighting improves code readability a lot. Really! Just look at this:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ba2360d-ad09-46bc-8857-856b6591ca3b/syntax-highlighting.png" alt="Syntax highlighting" width="622" height="400" />

### 2. Code completion

Automatic code suggestions can help the developer avoid having to type so much. If it supports custom classes and <a href="https://www.phpdoc.org/">phpDoc</a>, it can even save you from having to read project documentation.

Good code completion can also prevent typos. For example, if typing <kbd>$cotroller-&gt;</kbd> does not show you any suggestions, you'll know something is wrong. Uh oh… it should be <kbd>$co<strong>n</strong>troller</kbd>!

Poor code completion can slow you down if too many variants are shown or your class methods are not picked up.

![Code completion](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f10800a8-ee7a-4e4f-bbab-aa8f48229e1b/code-completion.png)

It is also good to have file name completion in HTML <kbd>src="</kbd> and PHP <kbd>include</kbd> and <kbd>require</kbd>.</p>

### 3. Navigation

One of the most boring things is trying to find where a certain variable has been defined or used. Some good IDEs can help with "GoTo" actions, like go to definition.

Another important feature is search. Searching should not take a long time, even with large projects. Even better is if the IDE lets you move quickly to the next occurrence of a search phrase, like Firefox does with its Quick Find feature.

![Code navigation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0a5cb6c-e4d6-4400-98fd-5061ca0ed49e/code-navigation.png)

### 4. Errors and warnings highlighting

On-the-fly syntax checking can prevent various typos and common programming mistakes. In the example below, the IDE indicates that you may have used <strong>=</strong> instead of <strong>==</strong>:

![Warning and errors](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a08b51c-5d66-4481-85ba-6c0188cddb86/warinigs-and-errors.png)

The more the IDE detects, the better -- except false positives, of course.</p>

### 5. Refactoring and code generation

Refactoring is basically a set of techniques for turning weak code into solid code. Its implementation in PHP IDEs is very weak compared to that of compiled-language IDEs, such as Java and C, but it's still very useful.

Very basic PHP refactoring includes:

*   "Move," which updates all includes and requires when moving a file to another directory.
*   "Rename," which renames something and ensures it is renamed throughout the project.
*   "Safe delete," which ensures deletion of a file does not harm other parts of the project.

![Refactoring](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7cdbea2-be65-4cdc-8459-a5a8ade4462e/refactor-rename.png)

In addition to basic refactoring, some IDEs can generate code for class constructors, getters/setters and even stub methods for a parent class.

![Code generation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229d98e2-845b-4fdb-9a4a-e166bb116a38/code-generation.png)

### 6. Debugging

Debugging is not so critical in PHP because you can add <kbd>echo</kbd>s or use something like FirePHP without even having to recompile your code. But for complex applications in which you need to add <kbd>echo</kbd> after each line to see what's going on, debugging can save you hours.

![Debugger](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e853f249-0567-476c-9125-b7f84a80c214/debugger.png)

If the IDE is good enough, it provides you with step-by-step debugging and lets you see the current values of variables in scope.</p>

### 7. Versioning system

Versioning is extremely useful for both team and one-person development. It shows what changes have been made to a file, when they were made and by whom. A good IDE allows you to visually compare revisions, copy changes from one version to another, revert to previous states and merge changes made by different team members.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58861f27-097e-4eac-9eca-76e21530333d/code-diff.png" alt="Visual diff" width="683" height="268" />

When performing common checks and commits, integrating a versioning system such as CVS, SVN, git or Mercurial in your IDE is usually much better than running a separate application.</p>

### 8. Client-side features

Using PHP alone is very rare. CSS and JavaScript are almost always somewhere in your application. So, good code completion, highlighting, navigation and perhaps some refactoring would be just as beneficial for the other languages and technologies you use in conjunction with PHP.

![HTML code completion](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42632473-ec27-4eaa-915b-0d806c80eb75/html-completion.png)

## How To Choose A Good One?

Every IDE provides a lot of features. Some of those features are very useful, some are not. Here are some guidelines to follow to narrow down the one for you:

*   Try free ones first. Their feature set may be enough for you, and you wouldn't need to pay for a license.
*   First, make sure the features you want are ones you _really_ need. If they are, check that they work properly in your IDE of choice.
*   If you find one IDE that fits well but is missing one or two features, try specialized tools.
*   Once you choose an IDE, play with it for a week before implementing it in a big project. You may find your current working habits are too strong to allow you to feel comfortable with it.</p>

## A Comparison Table

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68cefdd4-905f-4249-9cb8-38e486f39a38/ide-filter.png" alt="The great IDE filter" width="300" height="420" />

Along with <a href="https://simplecoding.org/">Vladimir Statsenko</a>, who helped with the section on Aptana, I've prepared this <a href="https://spreadsheets.google.com/ccc?key=pV8XyUSUOM7ET07rn4n7NYA">comparison table</a>.</p>

### What Was Covered

<strong>Eclipse-based IDEs</strong>
PDT, Zend Studio 6, Aptana PHP and Aptana Studio Pro are built on the Eclipse platform. That means you can use any of the thousands of Eclipse plug-ins out there. If a feature you need is not integrated in the IDE itself, it is most likely available as a third party plug-in.

Eclipse PHP IDEs were the first freeware IDEs with true IDE capabilities, such as complex code completion, code navigation, projects support, etc. Most of them are still free and very powerful.

<strong>NetBeans</strong>
NetBeans is the new bright kid on the block, but not built on the Eclipse platform. It has most of the features of other IDEs and yet more still. And it's free, too.

Development of this IDE is very public, open and rapid. Following the development blog and testing new builds as they come out is very interesting, even if there is already a stable version available (v6.5).</p>

### What Was Not Covered

There are plenty of powerful notepads such as PSPad, Notepad++, TextMate, vim and Emacs. Some are very similar to IDEs and even better if you want a good text editor but not the full IDE experience. Reviewing all of the good IDEs out there would not be possible (there are so many), so only the major players are compared here.</p>

### PHP IDEs We Tested

Here is the list of PHP IDEs we included in our review:

*   PDT 1
*   PDT 2.0
*   Zend Studio 6
*   NetBeans 6.5
*   NetBeans 7 (development version)
*   Aptana PHP
*   Aptana Studio Pro
*   Codelobster *
*   Nusphere PhpED 5.6 *

We thought it would be interesting to allow our readers to edit the table, which is hosted on Google Docs. Feel free to add your favorite IDE if it's not there, or note some features on the ones that are.

<a href="https://spreadsheets.google.com/ccc?key=pV8XyUSUOM7ET07rn4n7NYA"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5338b74-3ff8-44c7-b0dc-090dc07c13d2/net.gif" alt="Comparison table" width="541" height="457" /></a>

<a href="https://spreadsheets.google.com/ccc?key=pV8XyUSUOM7ET07rn4n7NYA">The full table at Google Docs</a> (<a href="https://spreadsheets1.google.com/ccc?key=pV8XyUSUOM7GsmVMLVit0Hw">not editable snapshot</a>)

<em>* Codelobster and Nusphere PhpED were filled in by Russian community members.</em>

## Conclusion

Still not using IDE? You may be wasting time. Try it. You'll see the difference.

Both PDT and NetBeans are good. If you need a lot of plug-ins, Eclipse is the better choice. If editing tools and code completion are more important to you, then pick NetBeans. NetBeans is a bit more responsive, too.

If you are mostly editing HTML and CSS, try Notepad++, vim, TextMate or Emacs. They all have very good HTML editing capabilities and can be configured for simple code completion. And they are faster and lighter than fully featured IDEs.

If you are editing complex JavaScript, try Aptana, which is amazing for JavaScript, or the <a href="https://spket.com/">Spket plug-in</a> for Eclipse, which has nearly the same features.

And remember, IDEs are not meant to change the way you think. They simply speed up the development process.</p>

### Commercial vs. Freeware

Strange as it may sound, commercial PHP IDEs such as Zend Studio and Aptana Studio Pro do not have significantly more advantages than free alternatives such as PDT2.0 and NetBeans, both of which are very good.

With Aptana Studio Pro, you get a good IE JavaScript debugger, SFTP, FTPS and some other less-than-useful features for $99.

Like NetBeans, Zend Studio offers a bit more code completion and error detection than PDT. It also has a very good customizable code formatter, refactoring capabilities (which NetBeans also has) and some wizards for the Zend Framework. It starts at $399.</p>

## Resources

*   [PDT Project](https://www.eclipse.org/pdt/) Official Eclipse PHP Development Tools website.
*   [Zend Studio](https://www.zend.com/en/products/studio/) Official Zend Studio website.
*   [NetBeans](https://www.netbeans.org/) Official NetBeans website.
*   [NetBeans for PHP weblog](https://blogs.sun.com/netbeansphp/) Here you can learn about new features to be included in upcoming releases and discuss them as they are being developed.
*   [Aptana](https://www.aptana.com/) Official Aptana website.

{{< signature "al" >}}

