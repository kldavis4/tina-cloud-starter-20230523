---
title: 'Stylelint: The Style Sheet Linter We’ve Always Wanted'
slug: stylelint-the-style-sheet-linter-weve-always-wanted
author: alekshudochenkov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b4022ec-3494-4744-b35c-eb3df64082c8/terminal-gulp-reporter-preview-500px-opt.png
date: 2016-05-25T16:02:51.000Z
summary: >-
  We will learn why linting a style sheet matters, how stylelint brings order to
  a style sheet and how we can avoid errors.
description: >-
  Everyone wants a clean, consistent code base, no matter the language.
  Developers are accustomed to setting up linters in programming languages such
  as JavaScript and Python, but they rarely use a linter for style sheets. In
  this article, we’ll look at [stylelint](https://stylelint.io/), a linter for
  style sheets.
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
---
Everyone wants a clean, consistent code base, no matter the language. Developers are accustomed to setting up linters in programming languages such as JavaScript and Python, but they rarely use a linter for style sheets. In this article, we’ll look at <a href="https://stylelint.io/">stylelint</a>, a linter for style sheets.

We will learn why linting a style sheet matters, how stylelint brings order to a style sheet and how we can avoid errors. Finally, we will learn how to use stylelint and start linting as soon as possible.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)
*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/7-principles-of-clean-and-optimized-css-code/)
*   [ESLint: The Next-Generation JavaScript Linter](https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/)
*   [An Introduction To PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)

## Why Linting Is Important

A linter is a tool that <strong>analyzes code and reports errors</strong> when a piece of code doesn’t pass the rules defined in the linter’s configuration.

Many of us work on code bases that many people have access to. If no strict rules on coding style are adhered to, the code could become a mess very fast. Maybe your code is already a mess, and you want to <strong>clean it up</strong> and maintain this cleanliness over time. Even if you work on style sheets alone, you’ll still want the code to be consistent.

{{% feature-panel %}}

Of course, your team might have code styles rules written in plain text in some wiki somewhere. But there is always the human factor to account for: People make mistakes — never on purpose.

And even if you are obsessed with following the rules of a proper coding style, your colleagues or the contributors to your open-source project might not be. Without a linter, you’d need to check the code for styling and errors by yourself. No person should spend time on things that can be automated. A linter will significantly <strong>decrease the time spent on code review</strong> because you will not be spending time checking styles and writing a pile of comments about every error. You will be free to examine what the code does, rather how it looks.</p>

## Stylelint

<a href="https://stylelint.io/">Stylelint</a> is a mighty, modern style sheet linter written in JavaScript by <a href="https://davidtheclark.com/">David Clark</a>, <a href="https://richardhallows.com/">Richard Hallows</a>, <a href="https://github.com/evilebottnawi">Evilebot Tnawi</a> and <a href="https://github.com/stylelint/stylelint/graphs/contributors">community</a>. It is powerful in its speed, variety and quality of rules, and it’s <strong>totally unopinionated</strong>. Stylelint has over a hundred rules, and the number is growing. Fear not, though: All rules are disabled by default, and you enable only the ones you want. Stylelint can lint not only CSS but also <a href="https://sass-lang.com/">Sass</a>, <a href="https://github.com/postcss/sugarss">SugarSS</a> and any other syntaxes that <a href="https://postcss.org">PostCSS</a> can parse (because stylelint is based on it).

Stylelint is to style sheets what <a href="https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/">ESLint</a> is to JavaScript.</p>

## Rules

Stylelint has <a href="https://stylelint.io/user-guide/rules/">over a hundred rules</a>, which can be divided into three groups: rules for <strong>styling</strong>, rules for the <strong>maintainability</strong> of code, and rules that <strong>check errors</strong> that would change what the code does in a browser. Style rules check for spacing (such as around colons), line breaks, indentation, etc. Rules for maintainability might report if an ID is used in a selector or if the <code>!important</code> keyword is used in a declaration. Rules for checking for errors might report an incorrect HEX color or a shorthand property that overrides another declaration.

I will not go over the style rules here (there are a ton of them). Rather, I want to describe some of the rules that help with maintainability and prevent errors.

The rule for preventing shorthand properties from overriding other declarations (or, in stylelint parlance, <code>declaration-block-no-shorthand-property-overrides</code>) would prevent a situation like this:

<pre><code class="language-css">div {
    padding-left: 20px; /* This property is overridden. */
    padding: 10px;
}</code></pre>

Stylelint also prevents invalid HEX colors (<code>color-no-invalid-hex</code>):

<pre><code class="language-css">p {
    color: #44;
}</code></pre>

And it prevents duplicate properties (<code>declaration-block-no-duplicate-properties</code>):

<pre><code class="language-css">p {
    color: #000; /* This property is overridden. */
    margin: 0 0 1.25em;
    color: #777;
}</code></pre>

You may use the old syntax for gradients. Stylelint will check for it (<code>function-linear-gradient-no-nonstandard-direction</code>):

<pre><code class="language-css">/* incorrect property */
.block {
    background: linear-gradient(bottom, #fff, #000);
}

/* correct property */
.block {
    background: linear-gradient(to bottom, #fff, #000);
}</code></pre>

Using the <code>!important</code> keyword on a property can cause problems down the line when you need to override the property with another rule. Just avoid <code>!important</code> altogether with the <code>declaration-no-important</code> rule.

Using an ID in a selector (<code>#main</code>) and using a type selector (i.e. a selector based on an HTML element — for example, <code>.block p</code>) might be forbidden in your development methodology (for example, <a href="https://en.bem.info/method/naming-convention/#css-selector-naming-convention">BEM</a>). In this case, <code>selector-no-id</code> and <code>selector-no-type</code> come in handy.

Sometimes you’ll misspell something or forget to add something to a style sheet. In the case of animation, <code>no-unknown-animations</code> will report if an animation’s name has no corresponding <code>@keyframes</code> rule.

And why would you want to bother with prefixes in values, properties names and selectors when we have <a href="https://github.com/postcss/autoprefixer">Autoprefixer</a>? Let Autoprefixer take care of that, and prevent prefixes from being added with the rules <code>value-no-vendor-prefix</code>, <code>property-no-vendor-prefix</code> and <code>selector-no-vendor-prefix</code>.

There are, of course, <a href="https://stylelint.io/user-guide/rules/">many more rules</a> in stylelint.</p>

## Plugins

Beside the default rules, stylelint also supports plugins, so you can extend it with new rules. Not many <a href="https://www.npmjs.com/search?q=stylelint-plugin">plugins are available</a> right now, but the ones we have are very handy.

Sometimes developers over-nest. While all preprocessors support nesting, nesting rules very deep results in increased selector specificity and leads to problems with maintaining those rules. Here is a typical example:

<pre><code class="language-scss">.header {
    .nav {
        .item {
            .link {
                color: blue;

                &amp;:hover {
                    color: red;
                }
            }
        }
    }
}</code></pre>

This renders as follows:

<pre><code class="language-css">.header .nav .item .link {
    color: blue;
}
.header .nav .item .link:hover {
    color: red;
}</code></pre>

Stylelint has no rule for this problem out of the box, but <a href="https://github.com/davidtheclark/stylelint-statement-max-nesting-depth">there is a plugin</a> (<code>stylelint-statement-max-nesting-depth</code>) that adds a rule for nesting depth.

To use any plugin, install it first:

<pre><code class="language-bash">npm install stylelint-statement-max-nesting-depth --save-dev</code></pre>

Then, add the plugin to the configuration file in the <code>plugins</code> array. Add the new rule and configure it:

<pre><code class="language-javascript">{
    "plugins": [
        "stylelint-statement-max-nesting-depth"
    ],
    "rules": {
        "statement-max-nesting-depth": 2
    }
}</code></pre>

In the configuration above, we’ve set the nesting depth to a maximum of two. So, we would be prompted to simplify our earlier example to a lower nesting depth (in this case, two levels):

<pre><code class="language-scss">.nav {
    .link {
        color: blue;

        &amp;:hover {
            color: red;
        }
    }
}</code></pre>

Or we could simplify further to one level:

<pre><code class="language-scss">.nav-link {
    color: blue;

    &amp;:hover {
        color: red;
    }
}</code></pre>

I will not go over all of the plugins here, but rather will recommend a few:

*   [Prevent qualified selectors](https://github.com/timothyneiljohnson/stylelint-selector-qualifying-element), such as `ul.nav`, `div#main` and `input[type="submit"]`. (Each option can be enabled separately.)
*   Enforce [shorthand values](https://github.com/timothyneiljohnson/stylelint-value-shorthand) whenever possible.
*   If you are following the BEM or SUIT methodology, then you might want to check the validity of your selectors against it. [Plugin](https://github.com/davidtheclark/stylelint-selector-bem-pattern) `stylelint-selector-bem-pattern` has predefined patterns for BEM and SUIT and can be configured for other methodologies.

If you want a new rule, you can <a href="https://stylelint.io/developer-guide/plugins/">write your own plugin</a>.

## Configuration Files

Configuring is the most difficult part about using a linter — and the most time-consuming. But there are shortcuts and different strategies that make stylelint easier to configure.

Your configuration can grow to be very big, so the most convenient way to store stylelint’s configuration is in a separate JSON file, named <code>.stylelintrc</code>. This way, the file can be used in the command line interface, in a build tool and in a code editor.

A very simple configuration might look like this:

<pre><code class="language-javascript">{
    "rules": {
        "color-hex-case": "lower",
        "color-hex-length": "short",
        "color-no-invalid-hex": true
    }
}</code></pre>

There are <strong>three strategies</strong> for configuration. The <strong>first</strong>, a simple one, is to extend someone else’s configuration (which stylelint supports) and then add, disable or tweak the rules you want to change. Developers have made configuration that probably fit most needs. You can install one as an npm package:

<pre><code class="language-bash">npm install stylelint-config-standard --save-dev</code></pre>

Then, in your own configuration file, you would extend theirs and override any rules as needed:

<pre><code class="language-javascript">{
    "extends": "stylelint-config-standard",
    "rules": {
        "indentation": "tab",
        "number-leading-zero": null
    }
}</code></pre>

In this example, we’ve extended <code>stylelint-config-standard</code> and changed the <code>indentation</code> rule to be “tabs” and disabled the <code>number-leading-zero</code> rule.

You can extend not only configurations shared via npm, but local ones, too. The documentation has <a href="https://stylelint.io/user-guide/configuration/#extends">more on extending and sharing configurations</a>.

The <strong>second strategy</strong> is to start with an empty file and progress slowly by adding rules as you need them. For example, you might not care about coding style just yet and just want to focus on preventing errors:

<pre><code class="language-javascript">{
    "rules": {
        "color-no-invalid-hex": true,
        "declaration-block-no-duplicate-properties": true,
        "declaration-block-no-shorthand-property-overrides": true,
        "function-linear-gradient-no-nonstandard-direction": true
    }
}</code></pre>

Later, you can add more rules.

The <strong>third strategy</strong> is to go over all of the rules and configure every one. I prefer this strategy because I want to check as much as possible and use stylelint at its full power. Sure, it’s the most time-consuming strategy, but it yields the best result. To make it easier, stylelint’s developers have created an <a href="https://stylelint.io/user-guide/example-config/">example configuration file</a> with all rules.

Every enabled rule has an error severity. This means that any rule that is not met will fail the test. The severity level for any rule <strong>can be lowered</strong> to a warning, which will prevent a test from failing. This is useful if you have just introduced a rule and don’t want a build to fail as the team is adjusting to the new rule.</p>

<pre><code class="language-javascript">{
    "rules": {
        "color-hex-case": ["lower", { "severity": "warning" }]
    }
}</code></pre>

In this example, stylelint will warn if a HEX color is miswritten, but it won’t throw an error.

Sometimes we need to put something in a style sheet that our stylelint configuration forbids. For example, we are forbidden to use the <code>!important</code> keyword, but we might need to use it in one place to override some third-party widget. We wouldn’t want to disable the rule because of this exceptional case. But we wouldn’t want to see the error every time either. Luckily, we can <strong>disable a particular rule</strong> in a line of CSS by adding a comment:

<pre><code class="language-css">.widget {
  display: none !important; /* stylelint-disable-line declaration-no-important */
}</code></pre>

Or we can disable stylelint for a chunk of CSS:

<pre><code class="language-css">/* stylelint-disable */
.third-party-code {}
/* stylelint-enable */</code></pre>

## Usage

Stylelint can be <a href="https://stylelint.io/user-guide/">used in many ways</a>: in the command line, in a build tool (such as Gulp, Grunt or Webpack), in a <a href="https://stylelint.io/user-guide/complementary-tools/">code editor</a> or as a <a href="https://github.com/okonet/lint-staged">Git pre-commit hook</a> for staged changes in Git repository. I will focus here on two ways.</p>

### Command Line

Using the command line is useful when you want to lint a project that doesn’t have stylelint or you want to use stylelint in an npm script.

Install stylelint globally:

<pre><code class="language-bash">npm install stylelint -g</code></pre>

Then, it will be available everywhere in your terminal:

<pre><code class="language-bash">stylelint "styles/**/*.css"</code></pre>

This command will lint all CSS files in the <code>styles</code> directory and any of its subdirectories.

To lint SCSS or SugarSS files, add the <code>syntax</code> option:

<pre><code class="language-bash">stylelint "styles/*.scss" --syntax scss</code></pre>

The configuration file can be specified explicitly:

<pre><code class="language-bash">stylelint "styles/*.css" --config bar/myStylelintConfig.json</code></pre>

If it’s not specified explicitly, stylelint will look for a <code>.stylelintrc</code> file in the current working directory.</p>

### Gulp

To use stylelint with Gulp, use it as PostCSS plugin. You’ll need to install the following packages:

<pre><code class="language-bash">npm install gulp-postcss stylelint postcss-reporter --save-dev</code></pre>

<a href="https://github.com/postcss/gulp-postcss">gulp-postcss</a> is a runner for all PostCSS plugins, and <a href="https://github.com/postcss/postcss-reporter">postcss-reporter</a> outputs much nicer errors and warnings from stylelint.</p>

<pre><code class="language-javascript">var postcss = require('gulp-postcss');
var reporter = require('postcss-reporter');
var stylelint = require('stylelint');

gulp.task('lint:css', function() {
    return gulp.src('src/**/*.css')
        .pipe(postcss([
            stylelint({ /* options */ }),
            reporter({ clearMessages: true })
        ]));
});</code></pre>

The output would look like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9075853f-f42c-4377-8102-cbe051f4e3ba/terminal-gulp-reporter-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b4022ec-3494-4744-b35c-eb3df64082c8/terminal-gulp-reporter-preview-500px-opt.png" alt="The terminal window with results from a stylelint Gulp task" width="656" height="297" /></a><figcaption>The terminal window with results from a stylelint Gulp task (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9075853f-f42c-4377-8102-cbe051f4e3ba/terminal-gulp-reporter-opt.png">View large version</a>)</figcaption></figure>

To lint a style sheet other than CSS, you’ll need to install the appropriate syntax. For example, to lint SCSS, we’d need to install <a href="https://github.com/postcss/postcss-scss">postcss-scss</a>:

<pre><code class="language-bash">npm install postcss-scss --savedev</code></pre>

Then, configure <code>gulp-postcss</code> to use this syntax:

<pre><code class="language-javascript">var postcss = require('gulp-postcss');
var reporter = require('postcss-reporter');
var stylelint = require('stylelint');
var scss = require("postcss-scss");

gulp.task('lint:css', function() {
    return gulp.src('src/**/*.scss')
        .pipe(postcss(
            [
                stylelint({ /* options */ }),
                reporter({ clearMessages: true })
            ],
            {
                syntax: scss
            }
        ));
});</code></pre>

You can specify the configuration file explicitly; otherwise, stylelint will look for <code>.stylelintrc</code>.</p>

## Conclusion

<a href="https://stylelint.io/">Stylelint</a> is a powerful style sheet linter. It brings clarity to code and saves you from errors. It’s useful for everyone: individual developers, teams and open-source maintainers. Once you start using it, you will hear no more comments like, “You forgot to add a space here” or “You forgot to remove it there.” Happy developing, and may you have a peaceful code review.

{{< signature "rb, ml, al, il" >}}

