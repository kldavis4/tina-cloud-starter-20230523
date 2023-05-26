---
title: 'ESLint: The Next-Generation JavaScript Linter'
slug: eslint-the-next-generation-javascript-linter
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33d81810-6ce4-404c-8ed9-13046777a8df/eslint-opt.png'
date: 2015-09-29T18:58:56.000Z
author: nicholas-c-zakas
description: >-
  It was the summer of 2013 and I was working on a project for my employer,
  _Box_. I had just finished wiring up [JSDoc](https://usejsdoc.org) as a nightly
  build using a plugin to detect [T3](https://t3js.org) patterns in our code and
  document them automatically. It occurred to me that these patterns might be
  easy to get wrong, and I started looking for a **way to automatically detect
  incorrect patterns**. I immediately turned to [JSHint](https://jshint.com)
  because we were already using it and I thought it could **support plugins**.
  Unfortunately, it could not.

  Still, I couldn’t get the idea of a linter with pluggable runtime rules out of
  my head. I had just spent a bunch of time learning about
  [Esprima](https://esprima.org) and abstract syntax trees (ASTs), and I thought
  to myself, “It can’t be all that hard to create a pluggable JavaScript linter
  using an AST.” It was from those initial thoughts that
  [ESLint](https://eslint.org) was born.
categories:
  - Coding
  - Workflow
  - JavaScript
  - Testing
---
It was the summer of 2013 and I was working on a project for my employer, <em>Box</em>. I had just finished wiring up <a href="https://usejsdoc.org">JSDoc</a> as a nightly build using a plugin to detect <a href="https://t3js.org">T3</a> patterns in our code and document them automatically. It occurred to me that these patterns might be easy to get wrong, and I started looking for a <strong>way to automatically detect incorrect patterns</strong>. I immediately turned to <a href="https://jshint.com">JSHint</a> because we were already using it and I thought it could <strong>support plugins</strong>. Unfortunately, it could not.

Still, I couldn’t get the idea of a linter with pluggable runtime rules out of my head. I had just spent a bunch of time learning about <a href="https://esprima.org">Esprima</a> and abstract syntax trees (ASTs), and I thought to myself, “It can’t be all that hard to create a pluggable JavaScript linter using an AST.” It was from those initial thoughts that <a href="https://eslint.org">ESLint</a> was born.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Terrible JavaScript Mistakes To Avoid With A Static Code Analyzer](https://www.smashingmagazine.com/2015/02/avoid-javascript-mistakes-with-static-code-analyzer/)
*   [Stylelint: The Style Sheet Linter We’ve Always Wanted](https://www.smashingmagazine.com/2016/05/stylelint-the-style-sheet-linter-weve-always-wanted/)
*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)

Note: The “ES” in “ESLint” stands for “ECMAScript”, the name for the core of the JavaScript language. This term has become more popular thanks to ECMAScript 6.

{{% feature-panel %}}

<figure><a href="https://eslint.org"><img title="ESLint: The Next-Generation JavaScript Linter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/609271b4-5f8d-4f19-a70e-7d1391f8dadd/eslint-opt1.png" alt="ESlint" width="500" height="301" /></a><figcaption>Meet <a href="https://eslint.org/">ESLint</a>, a tool that allows you to automatically detect incorrect patterns in JavaScript.</figcaption></figure>

## Legacy Problems

I had made a couple small contributions to JSHint over the years, and had also co-created <a href="https://csslint.net">CSS Lint</a>, so I had a decent amount of experience both writing and modifying linters. There were some things about JSHint that bothered me, and we tried to address them in CSS Lint. Even so, I felt that CSS Lint wasn’t anywhere near where I’d want a modern linter to be. Across JSHint and CSS Lint, I saw some problems and decided that if I were to create a new linter then it must solve as many of these problems as possible.

A lot of the problems are artifacts of legacy: this is simply the way things have always been done. JSHint, in particular, was suffering from some of the legacy of JSLint (from which it was forked). But since I was starting from scratch, I had an opportunity to look at these problems with fresh eyes and no constraints around their solutions. The problems I was most interested in solving were:

1.  **Single runtime** Both JSHint and CSS Lint run in both Rhino and Node.js; something I initially saw as a benefit in the past quickly became a significant cost. The amount of time spent trying to abstract away the underlying JavaScript engine, as well as maintaining compatibility between the engines, is a huge source of pain and a hole into which many hours disappear on a regular basis. Not only was getting the runtime working correctly in both engines difficult, it was also difficult getting the tests to run in both engines.
2.  **Disabling Rules** One aspect of JSHint that always bothered me was how you had to figure out which rules were off and on by default. While you can turn them off, the rules have strange names and some of them have no names at all, just codes (`W030`, for example). This was a problem we addressed in CSS Lint by making it obvious which rules were enabled and giving rules human-readable names.
3.  **Documentation** JSHint has always been fairly sparse when it comes to documentation. JSLint had almost no documentation, so the JSHint documentation was an improvement. Still, figuring out what `W030` meant was really hard. We went further with [CSS Lint rules documentation](https://github.com/CSSLint/csslint/wiki), and people seemed to appreciate the extra examples. I felt strongly that this was the direction any new linter would have to go.
4.  **Configuring Rules** Another issue I had with JSHint was how some rules had to be set to `true` to enable, while others had to be set to `false` to enable. This wasn’t really JSHint’s fault, as that strange behavior was inherited from its predecessor, JSLint. Still, even after years of using JSHint, I always had to look up which rules needed to be configured in which way.
5.  **Rule Error Levels** JSHint, like JSLint before it, forces all rules to have the same severity: error. In my experience, you often want to phase in the use of certain rules, allowing them to be set as warnings that don’t break the build and then later strictly enforcing them. CSS Lint allowed you to configure warnings and errors separately, and that ended up working very well, so I wanted ESLint to have the same capability.
6.  **Write Your Own Rules** I saw both JSHint and CSS Lint struggle with the problem of not being able to keep up with the demand for rules. There were endless debates about whether a rule was general enough to be included, and if it wasn’t, then the user was stuck. I didn’t want ESLint to be the single source of rules. I didn’t want to have those same debates, and the only way that would happen was if everyone could write their own rules. So I resolved that ESLint shouldn’t just be a tool, it should be the center of an ecosystem that allowed other developers to extend it easily.

With all of this in mind, and with the help of over 200 contributors in the past two years, ESLint has become the solid, flexible JavaScript linter I always hoped it could be.</p>

## Getting Started

The hardest part about incorporating a new linter in your project is getting it set up for the first time. From installation to initial configuration, it can take a significant amount of time just to get those first linting results to show up and be useful. With ESLint, the team has worked hard to make getting started as fast as possible.

You can install ESLint from <a href="https://npmjs.com">npm</a> by typing:

<pre><code class="language-bash">
$ npm install -g eslint
</code></pre>

This installs ESLint globally, which is useful for demonstration purposes. Many projects install ESLint locally (just remove the <code>-g</code>) so that it can interact with their build process.

Most linters require you to manually go through and set up configuration options before linting for the first time. This can involve digging through documentation to try to figure out which rules you want to apply. While you may want to do that eventually, ESLint can guide you through the basics of setting up your initial configuration. Switch to a directory with files you want to lint and type:

<pre><code class="language-bash">
$ eslint --init
</code></pre>

You’ll be prompted to answer some questions about the style of JavaScript you write that lets ESLint set up a proper configuration file to get started.

<pre><code class="language-bash">
$ eslint --init
? What style of indentation do you use? Tabs
? What quotes do you use for strings? Double
? What line endings do you use? Unix
? Do you require semicolons? Yes
? Are you using ECMAScript 6 features? No
? Where will your code run? Browser
? Do you use JSX? No
? What format do you want your config file to be in? css
Successfully created .eslintrc file in c:\Users\Nicholas\projects\personal\tmp
</code></pre>

Notice that you are asked if you’re using ECMAScript 6 and JSX; out of the box, ESLint supports both through <a href="https://eslint.org/docs/user-guide/configuring#specifying-language-options">language options</a>. In fact, ESLint was the first linter to fully support ECMAScript 6 and JSX, which has made it quite popular among those who are using <a href="https://facebook.github.io/react">React</a> and <a href="https://webpack.github.io/">webpack</a>.

The <code>eslint --init</code> process sets up an ESLint configuration file, <i>.eslintrc</i>, in the current directory. ESLint uses this file to determine which rules to apply when evaluating your code. Configuration files can be in JSON format or css, and we find most users prefer css.

After that, you can start linting files by passing in one or more filenames or directories:

<pre><code class="language-bash">
$ eslint test.js src/
</code></pre>

## Configuration Files

<a href="https://eslint.org/docs/user-guide/configuring">Configuration files</a> are what make ESLint so flexible. Inside your <i>.eslintrc</i> file, you can specify multiple settings, including:

*   Rules you want to run on files
*   Global variables that should be present in files
*   Environments in which files run
*   A base configuration to inherit
*   Plugins to load
*   Alternate parsers to use

To better understand configuration files, it’s helpful to look at an example. Here’s an example file generated from <code>eslint --init</code>:

<pre><code class="language-css">
rules:
  indent:
    - 2
    - tab
  quotes:
    - 1
    - double
  linebreak-style:
    - 2
    - unix
  semi:
    - 2
    - always
env:
  browser: true
extends: 'eslint:recommended'
</code></pre>

The first section in this file is <code>rules</code>, which specifies <a href="https://eslint.org/docs/user-guide/configuring#configuring-rules">rule settings</a>. The names <code>indent</code>, <code>quotes</code>, <code>linebreak-style</code> and <code>semi</code> all correspond to ESLint rules. Each rule is configured with an array, the first item of which is the rule severity. The rule severity is one of three values:

*   `0`: disable the rule completely
*   `1`: enable the rule as a warning
*   `2`: enable the rule as an error

The difference between warnings and errors is that warnings will not affect the exit code of ESLint. For instance, if you have ten warnings and no errors, the exit code is still 0. Rules configured as errors will cause the exit code to be 1 if that error is present. In this way, you can enable new rules without blocking a build process by setting them as warnings. You can change the rules to be errors later on when you're ready.

Each rule may also have several options associated with it. In the previous example, the <code>indent</code> rule has <code>tab</code> specified as an option. That tells the rule that these files should use tabs for indentation instead of spaces. Other rules have their own options, and every rule’s options are spelled out on its own <a href="https://eslint.org/docs/rules/">documentation page</a>.

You can specify <a href="https://eslint.org/docs/user-guide/configuring#specifying-environments">environments</a> using the <code>env</code> key. Environments provide predefined global variables and, in some cases, slightly alter how the parser works. The two most popular environments are <code>browser</code> and <code>node</code>.

Perhaps the most powerful aspect of configuration files is the <code>extends</code> key, which allows you to <a href="https://eslint.org/docs/user-guide/configuring#extending-configuration-files">inherit settings</a> from one or more other configuration files. The <code>eslint:recommended</code> configuration is built into ESLint and contains the rules that the team recommends to avoid common errors (you can see which rules are recommended on the <a href="https://eslint.org/docs/rules">documentation page</a>). You can also inherit from a <a href="https://eslint.org/docs/developer-guide/shareable-configs">shareable configs</a>, which is a configuration file defined as an npm package so that it can easily be shared among projects.

## Understanding the Output

The default formatter for ESLint output, designed by <a href="https://twitter.com/sindresorhus">Sindre Sorhus</a>, is another great example of how ESLint works hard to be useful to users. Here’s some example output:

<pre><code class="language-bash">
$ eslint test.js

test.js
  1:11  error    Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  2:1   error    Unexpected console statement                     no-console
  3:9   warning  Strings must use doublequote                     quotes

✖ 3 problems (2 errors, 1 warning)
</code></pre>

The results for each file are separated out with a header (in this case, <code>test.js</code>) and then each error and warning is listed beneath with four pieces of information:

1.  The line number and column number that triggered the rule
2.  The rule severity (error or warning)
3.  The message
4.  The rule that generated the message

We’ve found that all of this information is key to helping developers understand what to fix. In JSLint and JSHint, it’s hard to know how to eliminate a message (which gave rise to the <a href="https://jslinterrors.com/">JSLint Errors</a> site). With ESLint, the rule to configure is right there in the output.

ESLint also ships with <a href="https://eslint.org/docs/user-guide/command-line-interface#f-format">other formatters</a> designed to make integration with other tools easy. And because ESLint is all about extensibility, you can also create and distribute <a href="https://www.npmjs.com/search?q=eslint%20formatter">your own formatters</a>.</p>

## Plugins

As mentioned previously, one of ESLint’s original goals was to enable developers to write their own custom rules and plug them in at runtime. ESLint accomplishes this through <a href="https://eslint.org/docs/developer-guide/working-with-plugins">plugins</a>. An ESLint plugin can contain any number of custom rules that can then be distributed and used.

For instance, <a href="https://www.npmjs.com/package/eslint-plugin-react">eslint-plugin-react</a> is a popular ESLint plugin that has additional rules specifically targeting the React library. To use eslint-plugin-react, you must first install it via npm:

<pre><code class="language-bash">
$ npm install eslint-plugin-react --save-dev
</code></pre>

Then, in your configuration file, you indicate that eslint-plugin-react should be loaded by using the <code>plugins</code> array. After that, you can configure individual rules inside the plugin just like you would any other ESLint rule:

<pre><code class="language-css">
plugins:
  - react
rules:
  react/display-name: 2
  indent:
    - 2
    - tab
  quotes:
    - 1
    - double
  linebreak-style:
    - 2
    - unix
  semi:
    - 2
    - always
env:
  browser: true
ecmaFeatures:
  jsx: true
extends: 'eslint:recommended'
</code></pre>

You can safely omit the <code>eslint-plugin-</code> prefix when using a plugin name in the configuration file, so just <code>react</code> is enough to identify the plugin. The rule <code>react/display-name</code> is set to be an error. The <code>react/</code> prefix lets ESLint know that this rule is from a plugin rather than the core.

There are over 80 <a href="https://www.npmjs.com/browse/keyword/eslintplugin">ESLint plugins</a> published to npm, and many that teams use internally at their own companies. Anyone can create their own <a href="https://eslint.org/docs/developer-guide/working-with-rules">custom rules</a> and the <a href="https://npmjs.com/package/generator-eslint">ESLint Yeoman Generator</a> to guide you through the process.</p>

## Custom Parsers

Another way you can customize ESLint is by specifying <a href="https://eslint.org/docs/user-guide/configuring#specifying-parser">custom parsers</a>. By default, ESLint uses the <a href="https://github.com/eslint/espree">Espree</a> parser (a fork of Esprima) that provides ECMAScript 6 and JSX support natively. However, ESLint can use any parser that generates an ESTree-compatible AST. It’s this capability that led ESLint to be the first linter to support <a href="https://www.babeljs.io">Babel</a> through the use of <a href="https://npmjs.com/package/babel-eslint">babel-eslint</a>.

The babel-eslint parser is an adapter that makes Babel output an AST format that ESLint can understand. As a result, using babel-eslint means that ESLint can understand and work with almost every experimental syntax that Babel supports (there are, of course, some compatibility issues when dealing with experimental features). To use babel-eslint, first install it:

<pre><code class="language-bash">
$ npm install babel-eslint --save-dev
</code></pre>

Then specify the <code>parser</code> key in your configuration file:

<pre><code class="language-css">
parser: babel-eslint
rules:
  react/display-name: 2
  indent:
    - 2
    - tab
  quotes:
    - 1
    - double
  linebreak-style:
    - 2
    - unix
  semi:
    - 2
    - always
env:
  browser: true
ecmaFeatures:
  jsx: true
extends: 'eslint:recommended'
</code></pre>

When ESLint runs using this configuration file, it will swap in babel-eslint for Espree when it parses your code.

Decoupling the linter from the parser is one of the significant innovations in ESLint that has allowed us to move quickly to support a wide variety of use cases.</p>

## Linting Improvements

Linters have traditionally worked in the same way: figure out a list of files to lint, lint each file, then report the results. The ESLint team, however, is always looking for ways to make the linting experience more effective and efficient. Recently, the team added a couple of new features that really emphasize just how powerful ESLint is:

*   The `--fix` command line option tells ESLint to attempt to automatically fix as many problems as possible. Fixes are only applied when it is safe to do so, and you'll see any problems that were left unfixed. So now instead of going back into your files to insert a missing semicolon or properly indent some code, ESLint can do it for you. This is especially useful when you first introduce ESLint into a project as it means you don't have to manually fix every file.
*   The `--cache` command line options tells ESLint to keep track of files that had no problems so that future runs will only lint files that have changed. If you're repeatedly running ESLint over a large codebase, this can save you a lot of time

## Conclusion

<a href="https://eslint.org/">ESLint</a> is a JavaScript linter that has learned from our collective past of JavaScript development. Our development paradigms have moved away from walled-garden, one-size-fits-all approaches into an era of small components and composability. The ESLint team knows that JavaScript development in 2015 is a lot different from when JSLint was first released, and that no single team can ever properly account for all the different variations and desires of developers all around the world.

That’s why ESLint is committed to not only being a great linter out of the box, but also to being the center of a great and growing ecosystem of plugins, shareable configs and parsers.

{{< signature "ml, og" >}}

