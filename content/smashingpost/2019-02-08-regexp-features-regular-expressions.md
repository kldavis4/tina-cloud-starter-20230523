---
title: 'New JavaScript Features That Will Change How You Write Regex'
slug: regexp-features-regular-expressions
author: farazkelhini
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cdf20f7-3346-4811-b9b7-4ffd70e6a019/faraz-regex-new-js-features.png
date: 2019-02-08T13:00:32+01:00
summary: >-
  If you have ever done any sort of sophisticated text processing and manipulation in JavaScript, you’ll appreciate the new features introduced in ES2018. In this article, we take a good look at how the ninth edition of the standard improves the text processing capability of JavaScript.
description: >-
  If you have ever done any sort of sophisticated text processing and manipulation in JavaScript, you’ll appreciate the new features introduced in ES2018. In this article, we take a good look at how the ninth edition of the standard improves the text processing capability of JavaScript.
categories:
  - JavaScript
  - Browsers
---
There’s a good reason the majority of programming languages support regular expressions: they are extremely powerful tools for manipulating text. Text processing tasks that require dozens of lines of code can often be accomplished with a single line of regular expression code. While the built-in functions in most languages are usually sufficient to perform search and replace operations on strings, more complex operations &mdash; such as validating text inputs &mdash; often require the use of regular expressions.

Regular expressions have been part of the JavaScript language since the third edition of the ECMAScript standard, which was introduced in 1999. ECMAScript 2018 (or ES2018 for short) is the ninth edition of the standard and further improves the text processing capability of JavaScript by introducing four new features:

<ul>
    <li><a href="#lookbehind-assertions">Lookbehind assertions</a></li>
    <li><a href="#named-capture-groups">Named capture groups</a></li>
    <li><a href="#s-dotAll-flag"><code>s</code> (<code>dotAll</code>) Flag</a></li>
    <li><a href="#unicode-property-escapes">Unicode property escapes</a></li>
</ul>

These new features are explained in detail in the subsections that follow.

<div class="c-felix-the-cat">
<h4 class="h3">Debugging JavaScript</h4>
<p><code>console.log</code> can tell you a lot about your app, but it can't truly debug your code. For that, you need a full-fledged JavaScript debugger. <a href="https://www.smashingmagazine.com/2018/02/javascript-firefox-debugger/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## Lookbehind Assertions

The ability to match a sequence of characters based on what follows or precedes it enables you to discard potentially undesired matches. This is especially important when you need to process a large string and the chance of undesired matches is high. Fortunately, most regular expression flavors provide the lookbehind and lookahead assertions for this purpose.

Prior to ES2018, only lookahead assertions were available in JavaScript. A lookahead allows you to assert that a pattern is immediately followed by another pattern.

There are two versions of lookahead assertions: positive and negative. The syntax for a positive lookahead is `(?=...)`. For example, the regex `/Item(?= 10)/` matches `Item` only when it is followed, with an intervening space, by number 10:

<pre><code class="language-javascript">const re = /Item(?= 10)/;

console.log(re.exec('Item'));
// &rarr; null

console.log(re.exec('Item5'));
// &rarr; null

console.log(re.exec('Item 5'));
// &rarr; null

console.log(re.exec('Item 10'));
// &rarr; [&quot;Item&quot;, index: 0, input: &quot;Item 10&quot;, groups: undefined]
</code></pre>

This code uses the `exec()` method to search for a match in a string. If a match is found, `exec()` returns an array whose first element is the matched string. The `index` property of the array holds the index of the matched string, and the `input` property holds the entire string that the search performed on. Finally, if named capture groups are used in the regular expression, they are placed on the `groups` property. In this case, `groups` has a value of `undefined` because there is no named capture group.

The construct for a negative lookahead is `(?!...)`. A negative lookahead asserts that a pattern is not followed by a specific pattern. For example, the pattern `/Red(?!head)/` matches `Red` only if it not followed by `head`:

<pre><code class="language-javascript">const re = /Red(?!head)/;

console.log(re.exec('Redhead'));
// &rarr; null

console.log(re.exec('Redberry'));
// &rarr; [&quot;Red&quot;, index: 0, input: &quot;Redberry&quot;, groups: undefined]

console.log(re.exec('Redjay'));
// &rarr; [&quot;Red&quot;, index: 0, input: &quot;Redjay&quot;, groups: undefined]

console.log(re.exec('Red'));
// &rarr; [&quot;Red&quot;, index: 0, input: &quot;Red&quot;, groups: undefined]
</code></pre>

ES2018 complements lookahead assertions by bringing lookbehind assertions to JavaScript. Denoted by `(?<=...)`, a lookbehind assertion allows you to match a pattern only if it is preceded by another pattern.

Let’s suppose you need to retrieve the price of a product in euro without capturing the euro symbol. With a lookbehind, this task becomes a lot simpler:

<pre><code class="language-javascript">const re = /(?&lt;=&euro;)\d+(\.\d*)?/;

console.log(re.exec('199'));
// &rarr; null

console.log(re.exec('$199'));
// &rarr; null

console.log(re.exec('&euro;199'));
// &rarr; [&quot;199&quot;, undefined, index: 1, input: &quot;&euro;199&quot;, groups: undefined]
</code></pre>

**Note**: *Lookahead and lookbehind assertions are often referred to as “lookarounds”.*

The negative version of lookbehind is denoted by `(?<!...)` and enables you to match a pattern that is not preceded by the pattern specified within the lookbehind. For example, the regular expression `/(?<!\d{3}) meters/` matches the word "meters" if three digits do not come before it:

<pre><code class="language-javascript">const re = /(?&lt;!\d{3}) meters/;

console.log(re.exec('10 meters'));
// &rarr; [&quot; meters&quot;, index: 2, input: &quot;10 meters&quot;, groups: undefined]

console.log(re.exec('100 meters'));    
// &rarr; null
</code></pre>

As with lookaheads, you can use several lookbehinds (negative or positive) in succession to create a more complex pattern. Here’s an example:

<pre><code class="language-javascript">const re = /(?&lt;=\d{2})(?&lt;!35) meters/;

console.log(re.exec('35 meters'));
// &rarr; null

console.log(re.exec('meters'));
// &rarr; null

console.log(re.exec('4 meters'));
// &rarr; null

console.log(re.exec('14 meters'));
// &rarr; [&quot;meters&quot;, index: 2, input: &quot;14 meters&quot;, groups: undefined]
</code></pre>

This regex matches a string containing meters only if it is immediately preceded by any two digits other than 35. The positive lookbehind ensures that the pattern is preceded by two digits, and then the negative lookbehind ensures that the digits are not 35.

{{% ad-panel-leaderboard %}}

## Named Capture Groups

You can group a part of a regular expression by encapsulating the characters in parentheses. This allows you to restrict alternation to a part of the pattern or apply a quantifier on the whole group. Furthermore, you can extract the matched value by parentheses for further processing.

The following code gives an example of how to find a file name with *.jpg* extension in a string and then extract the file name:

<pre><code class="language-javascript">const re = /(\w+)\.jpg/;
const str = 'File name: cat.jpg';
const match = re.exec(str);
const fileName = match[1];

// The second element in the resulting array holds the portion of the string that parentheses matched
console.log(match);
// &rarr; [&quot;cat.jpg&quot;, &quot;cat&quot;, index: 11, input: &quot;File name: cat.jpg&quot;, groups: undefined]

console.log(fileName);
// &rarr; cat
</code></pre>

In more complex patterns, referencing a group using a number just makes the already cryptic regular expression syntax more confusing. For example, suppose you want to match a date. Since the position of day and month is swapped in some regions, it’s not clear which group refers to the month and which group refers to the day:

<pre><code class="language-javascript">const re = /(\d{4})-(\d{2})-(\d{2})/;
const match = re.exec('2020-03-04');

console.log(match[0]);    // &rarr; 2020-03-04
console.log(match[1]);    // &rarr; 2020
console.log(match[2]);    // &rarr; 03
console.log(match[3]);    // &rarr; 04
</code></pre>

ES2018’s solution to this problem is named capture groups, which use a more expressive syntax in the form of `(?<name>...)`:

<pre><code class="language-javascript">const re = /(?&lt;year&gt;\d{4})-(?&lt;month&gt;\d{2})-(?&lt;day&gt;\d{2})/;
const match = re.exec('2020-03-04');

console.log(match.groups);          // &rarr; {year: &quot;2020&quot;, month: &quot;03&quot;, day: &quot;04&quot;}
console.log(match.groups.year);     // &rarr; 2020
console.log(match.groups.month);    // &rarr; 03
console.log(match.groups.day);      // &rarr; 04
</code></pre>

Because the resulting object may contain a property with the same name as a named group, all named groups are defined under a separate object called `groups`.

A similar construct exists in many new and traditional programming languages. Python, for example, uses the `(?P<name>)` syntax for named groups. Not surprisingly, Perl supports named groups with syntax identical to JavaScript (JavaScript has imitated its regular expression syntax from Perl). Java also uses the same syntax as Perl.

In addition to being able to access a named group through the `groups` object, you can access a group using a numbered reference &mdash; similar to a regular capture group:

<pre><code class="language-javascript">const re = /(?&lt;year&gt;\d{4})-(?&lt;month&gt;\d{2})-(?&lt;day&gt;\d{2})/;
const match = re.exec('2020-03-04');

console.log(match[0]);    // &rarr; 2020-03-04
console.log(match[1]);    // &rarr; 2020
console.log(match[2]);    // &rarr; 03
console.log(match[3]);    // &rarr; 04
</code></pre>

The new syntax also works well with destructuring assignment:

<pre><code class="language-javascript">const re = /(?&lt;year&gt;\d{4})-(?&lt;month&gt;\d{2})-(?&lt;day&gt;\d{2})/;
const [match, year, month, day] = re.exec('2020-03-04');

console.log(match);    // &rarr; 2020-03-04
console.log(year);     // &rarr; 2020
console.log(month);    // &rarr; 03
console.log(day);      // &rarr; 04
</code></pre>

The `groups` object is always created, even if no named group exists in a regular expression:

<pre><code class="language-javascript">const re = /\d+/;
const match = re.exec('123');

console.log('groups' in match);    // &rarr; true
</code></pre>

If an optional named group does not participate in the match, the `groups` object will still have a property for that named group but the property will have a value of `undefined`:

<pre><code class="language-javascript">const re = /\d+(?&lt;ordinal&gt;st|nd|rd|th)?/;

let match = re.exec('2nd');

console.log('ordinal' in match.groups);    // &rarr; true
console.log(match.groups.ordinal);         // &rarr; nd

match = re.exec('2');

console.log('ordinal' in match.groups);    // &rarr; true
console.log(match.groups.ordinal);         // &rarr; undefined
</code></pre>

You can refer to a regular captured group later in the pattern with a backreference in the form of `\1`. For example, the following code uses a capture group that matches two letters in a row, then recalls it later in the pattern:

<pre><code class="language-javascript">console.log(/(\w\w)\1/.test('abab'));    // &rarr; true

// if the last two letters are not the same 
// as the first two, the match will fail
console.log(/(\w\w)\1/.test('abcd'));    // &rarr; false
</code></pre>

To recall a named capture group later in the pattern, you can use the `/\k<name>/` syntax. Here is an example:

<pre><code class="language-javascript">const re = /\b(?&lt;dup&gt;\w+)\s+\k&lt;dup&gt;\b/;

const match = re.exec(&quot;I'm not lazy, I'm on on energy saving mode&quot;);        

console.log(match.index);    // &rarr; 18
console.log(match[0]);       // &rarr; on on
</code></pre>

This regular expression finds consecutive duplicate words in a sentence. If you prefer, you can also recall a named capture group using a numbered back reference:

<pre><code class="language-javascript">const re = /\b(?&lt;dup&gt;\w+)\s+\1\b/;

const match = re.exec(&quot;I'm not lazy, I'm on on energy saving mode&quot;);        

console.log(match.index);    // &rarr; 18
console.log(match[0]);       // &rarr; on on 
</code></pre>

It’s also possible to use a numbered back reference and a named backreference at the same time:

<pre><code class="language-javascript">const re = /(?&lt;digit&gt;\d):\1:\k&lt;digit&gt;/;

const match = re.exec('5:5:5');        

console.log(match[0]);    // &rarr; 5:5:5
</code></pre>

Similar to numbered capture groups, named capture groups can be inserted into the replacement value of the `replace()` method. To do that, you will need to use the `$<name>` construct. For example:

<pre><code class="language-javascript">const str = 'War &amp; Peace';

console.log(str.replace(/(War) &amp; (Peace)/, '$2 &amp; $1'));    
// &rarr; Peace &amp; War

console.log(str.replace(/(?&lt;War&gt;War) &amp; (?&lt;Peace&gt;Peace)/, '$&lt;Peace&gt; &amp; $&lt;War&gt;'));    
// &rarr; Peace &amp; War
</code></pre>

If you want to use a function to perform the replacement, you can reference the named groups the same way you would reference numbered groups. The value of the first capture group will be available as the second argument to the function, and the value of the second capture group will be available as the third argument:

<div class="break-out">

 <pre><code class="language-javascript">const str = 'War &amp; Peace';

const result = str.replace(/(?&lt;War&gt;War) &amp; (?&lt;Peace&gt;Peace)/, function(match, group1, group2, offset, string) {
    return group2 + ' &amp; ' + group1;
});

console.log(result);    // &rarr; Peace &amp; War
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## <code>s</code> (<code>dotAll</code>) Flag

By default, the dot (`.`) metacharacter in a regex pattern matches any character with the exception of line break characters, including line feed (`\n`) and carriage return (`\r`):

<pre><code class="language-javascript">console.log(/./.test('\n'));    // &rarr; false
console.log(/./.test('\r'));    // &rarr; false
</code></pre>

Despite this shortcoming, JavaScript developers could still match all characters by using two opposite shorthand character classes like `[\w\W]`, which instructs the regex engine to match a character that’s a word character (`\w`) or a non-word character (`\W`):

<pre><code class="language-javascript">console.log(/[\w\W]/.test('\n'));    // &rarr; true
console.log(/[\w\W]/.test('\r'));    // &rarr; true
</code></pre>

ES2018 aims to fix this problem by introducing the `s` (`dotAll`) flag. When this flag is set, it changes the behavior of the dot (`.`) metacharacter to match line break characters as well:

<pre><code class="language-javascript">console.log(/./s.test('\n'));    // &rarr; true
console.log(/./s.test('\r'));    // &rarr; true
</code></pre>

The `s` flag can be used on per-regex basis and thus does not break existing patterns that rely on the old behavior of the dot metacharacter. Besides JavaScript, the `s` flag is available in a number of other languages such as Perl and PHP.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2017/05/abridged-cartoon-introduction-webassembly/">An Abridged Cartoon Introduction To WebAssembly</a></em></p>

## Unicode Property Escapes

Among the new features introduced in ES2015 was Unicode awareness. However, shorthand character classes were still unable to match Unicode characters, even if the `u` flag was set.

Consider the following example:

<pre><code class="language-javascript">const str = '𝟠';

console.log(/\d/.test(str));     // &rarr; false
console.log(/\d/u.test(str));    // &rarr; false
</code></pre>

`𝟠` is considered a digit, but `\d` can only match ASCII [0-9], so the `test()` method returns `false`. Because changing the behavior of shorthand character classes would break existing regular expression patterns, it was decided to introduce a new type of escape sequence.

In ES2018, Unicode property escapes, denoted by `\p{...}`, are available in regular expressions when the `u` flag is set. Now to match any Unicode number, you can simply use `\p{Number}`, as shown below:

<pre><code class="language-javascript">const str = '𝟠';
console.log(/\p{Number}/u.test(str));     // &rarr; true
</code></pre>

And to match any Unicode alphabetic character, you can use `\p{Alphabetic}`:

<pre><code class="language-javascript">const str = '漢';

console.log(/\p{Alphabetic}/u.test(str));     // &rarr; true

// the \w shorthand cannot match 漢
console.log(/\w/u.test(str));    // &rarr; false
</code></pre>

`\P{...}` is the negated version of `\p{...}` and matches any character that `\p{...}` does not:

<pre><code class="language-javascript">console.log(/\P{Number}/u.test('𝟠'));    // &rarr; false
console.log(/\P{Number}/u.test('漢'));    // &rarr; true

console.log(/\P{Alphabetic}/u.test('𝟠'));    // &rarr; true
console.log(/\P{Alphabetic}/u.test('漢'));    // &rarr; false
</code></pre>

*A full list of supported properties is available on the [current specification proposal](https://tc39.github.io/proposal-regexp-unicode-property-escapes/#sec-static-semantics-unicodematchproperty-p).*

Note that using an unsupported property causes a `SyntaxError`:

<pre><code class="language-javascript">console.log(/\p{undefined}/u.test('漢'));    // &rarr; SyntaxError
</code></pre>

## Compatibility Table

### Desktop Browsers

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist"></th>
            <th>Chrome</th>
            <th>Firefox</th>
            <th>Safari</th>
            <th>Edge</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Lookbehind Assertions</td>
            <td>62</td>
            <td>X</td>
            <td>X</td>
            <td>X</td>
        </tr>
        <tr>
            <td>Named Capture Groups</td>
            <td>64</td>
            <td>X</td>
            <td>11.1</td>
            <td>X</td>
        </tr>
        <tr>
            <td><code>s</code> (<code>dotAll</code>) Flag</td>
            <td>62</td>
            <td>X</td>
            <td>11.1</td>
            <td>X</td>
        </tr>
        <tr>
            <td>Unicode Property Escapes</td>
            <td>64</td>
            <td>X</td>
            <td>11.1</td>
            <td>X</td>
    </tbody>
</table>

### Mobile Browsers

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist"></th>
            <th>ChromeFor Android</th>
            <th>FirefoxFor Android</th>
            <th>iOS Safari</th>
            <th>Edge Mobile</th>
            <th>Samsung Internet</th>
            <th>Android Webview</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Lookbehind Assertions</td>
            <td>62</td>
            <td>X</td>
            <td>X</td>
            <td>X</td>
            <td>8.2</td>
            <td>62</td>
        </tr>
        <tr>
            <td>Named Capture Groups</td>
            <td>64</td>
            <td>X</td>
            <td>11.3</td>
            <td>X</td>
            <td>X</td>
            <td>64</td>
        </tr>
        <tr>
            <td><code>s</code> (<code>dotAll</code>) Flag</td>
            <td>62</td>
            <td>X</td>
            <td>11.3</td>
            <td>X</td>
            <td>8.2</td>
            <td>62</td>
        </tr>
        <tr>
            <td>Unicode Property Escapes</td>
            <td>64</td>
            <td>X</td>
            <td>11.3</td>
            <td>X</td>
            <td>X</td>
            <td>64</td>
    </tbody>
</table>

### Node.js

- **8.3.0** (requires `--harmony` runtime flag)
- **8.10.0** (support for `s` (`dotAll`) flag and lookbehind assertions)
- **10.0.0** (full support)

## Wrapping Up

ES2018 continues the work of previous editions of ECMAScript by making regular expressions more useful. New features include lookbehind assertion, named capture groups, `s` (`dotAll`) flag, and Unicode property escapes. Lookbehind assertion allows you to match a pattern only if it is preceded by another pattern. Named capture groups use a more expressive syntax compared to regular capture groups. The `s` (`dotAll`) flag changes the behavior of the dot (`.`) metacharacter to match line break characters. Finally, Unicode property escapes provide a new type of escape sequence in regular expressions.

When building complicated patterns, it’s often helpful to use a regular-expressions tester. A good tester provides an interface to test a regular expression against a string and displays every step taken by the engine, which can be especially useful when trying to understand patterns written by others. It can also detect syntax errors that may occur within your regex pattern. Regex101 and RegexBuddy are two popular regex testers worth checking out.

Do you have some other tools to recommend? Share them in the comments!

{{< signature "dm, il" >}}
