---
title: Crucial Concepts Behind Advanced Regular Expressions
slug: introduction-to-advanced-regular-expressions
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a024702-2258-4d4f-a1ff-4478b6cdcc3c/regex.jpg
date: 2009-05-06T15:39:02.000Z
author: karthik-viswanathan
description: >-
  Regular expressions (or regex) are a powerful way to traverse large strings in
  order to find information. They rely on underlying patterns in a string’s
  structure to work their magic. Unfortunately, simple regular expressions are
  unable to cope with complex patterns and symbols. To deal with this dilemma,
  you can use **advanced regular expressions**.

  [![Recursion](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034e0c67-55bd-44bc-a003-06e5c823e97f/recursion.jpg)](https://www.smashingmagazine.com/2009/05/06/introduction-to-advanced-regular-expressions/)

  Below, we present an **introduction to advanced regular expressions**, with
  eight commonly used concepts and examples. Each example outlines a simple way
  to match patterns in complex strings. If you do not yet have experience with
  basic regular expressions, have a look at [this
  article](https://www.lateralcode.com/regular-expressions/) to get started. The
  syntax used here matches PHP regular expressions.
categories:
  - Coding
  - Regular Expressions
---
Regular expressions (or regex) are a powerful way to traverse large strings in order to find information. They rely on underlying patterns in a string’s structure to work their magic. Unfortunately, simple regular expressions are unable to cope with complex patterns and symbols. To deal with this dilemma, you can use <strong>advanced regular expressions</strong>.

You may also be interested in the following related posts:

*   [Essential Guide To Regular Expressions: Tools and Tutorials](https://www.smashingmagazine.com/2009/06/essential-guide-to-regular-expressions-tools-tutorials-and-resources/)
*   [Introduction To URL Rewriting](https://www.smashingmagazine.com/2011/11/introduction-to-url-rewriting/)

Below, we present an <strong>introduction to advanced regular expressions</strong>, with eight commonly used concepts and examples. Each example outlines a simple way to match patterns in complex strings. If you do not yet have experience with basic regular expressions, have a look at <a href="https://www.lateralcode.com/regular-expressions/">this article</a> to get started. The syntax used here matches PHP's Perl-compatible regular expressions.</p>

## 1\. Greediness/Laziness

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b9a1ac3-1044-458b-bd8c-59f2bb3757c5/greed.jpg" alt="Greed" width="400" height="300" />

{{% feature-panel %}}

All regex repetition operators are <strong>greedy</strong>. They try to match as much as possible in a string. Unfortunately, this might not always be a desired effect. Thus, lazy operators are used to solve this problem. They only match the smallest possible pattern and are used by adding a '?' after the respective greedy operator. Alternatively, the 'U' modifier may be used to make all repetiton operators lazy. Differentiating between greediness and laziness is key to fully understanding advanced regular expressions.</p>

### Greedy Operators

The * operator matches the previous expression 0 or more times. It is a greedy operator. Consider the following expression:

<pre><code class="language-php">preg_match( '/&lt;h1&gt;.*&lt;/h1&gt;/', '&lt;h1&gt;This is a heading.&lt;/h1&gt;
&lt;h1&gt;This is another one.&lt;/h1&gt;', $matches );</code></pre>

Recall that a . means any character except a new line. The above regular expression is looking for an h1 tag and all of its contents. It uses the . and * operators to constantly match anything inside the tag. This pattern will match:

<pre><code class="language-php">&lt;h1&gt;This is a heading.&lt;/h1&gt;&lt;h1&gt;This is another one.&lt;/h1&gt;</code></pre>

It returns the whole string. The * operator will continuously match everything -- even the middle closing h1 tag -- because it is greedy. Matching the whole string is the best it can do.</p>

### Lazy Operators

Let's change the above operator by adding a '?' after it. This will make it lazy:

<pre><code class="language-php">/&lt;h1&gt;.*?&lt;/h1&gt;/</code></pre>

The regex now fulfills its duty and matches only the first h1 tag. Another greedy operator that uses this same property is {n,}. This matches the previous expression n or more times. If it is used without a question mark, it looks for the most repetitions possible. Otherwise, it starts from n repetitions:

<pre><code class="language-php"># Set up a String
$str = 'hihi';

# Match it using the greedy {n,} operator
preg_match( '/(hi){1,}/', $str, $matches ); # matches[0] will be 'hihi'

# Match it with the lazy {n,}? operator
preg_match( '/(hi){1,}?/', $str, $matches ); # matches[0] will be 'hi'</code></pre>

## 2\. Back Referencing

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024f66da-69fe-4ca9-b78b-b84974d42ce5/back.jpg" alt="Back Referencing" width="300" height="290" />

### What it does

<strong>Back referencing</strong> is a way to refer to previously matched patterns inside a regular expression. For example, take a look at this simple regex that matches an expression in quotes:

<pre><code class="language-php"># Set up an array of matches
$matches = array();

# Create a String
$str = ""This is a 'string'"";

# Traverse it with regular expressions
preg_match( "/("|').*?("|')/", $str, $matches );

# Print the whole match
echo  $matches[0];</code></pre>

Unfortunately, this will not correctly match the string. Instead, it will print:

<pre><code class="language-php">"This is a '</code></pre>

This regular expression matches the opening double quote but finds a different type of quote to close it. This is because it was given the option of picking a double or single quote at the end. In order to fix this, you can use back referencing. The <strong>expressions 1, 2, ...., 9</strong> hold references to previously captured subpatterns. The first matched quote, in this case, will be held by the variable 1.</p>

### How to Use It

In order to apply this concept to the aforementioned example, use 1 in place of the last quote:

<pre><code class="language-php">preg_match( '/("|').*?1/', $str, $matches );</code></pre>

This will now correctly return:

<pre><code class="language-php">"This is a 'string'"</code></pre>

Remember that back referencing may also be used by <code>preg_replace</code>. Note that instead of 1 ... 9, you should use $1 ... $9 ... $n (any number of these will work). For example, if you want to replace all paragraph tags with text that represents them, use:

<pre><code class="language-php">$text = preg_replace( '/&lt;p&gt;(.*?)&lt;/p&gt;/', 
"&amp;lt;p&amp;gt;$1&amp;lt;/p&amp;gt;", $html );</code></pre>

The $1 back reference holds the text inside the paragraph and is being used in the replace pattern itself. This completely valid expression shows an easy way to access matched patterns even while replacing.</p>

## 3\. Named Groups

When using multiple back references, a regular expression can quickly become confusing and hard to understand. An alternative way to back reference is by using <strong>named groups</strong>. A named group is specified by using <code>(?P&lt;name&gt;pattern)</code>, where name is the name of the group and pattern is the regular expression in the group itself. The group can then be referred to by (?P=name). For example, consider the following:

<pre><code class="language-php">/(?P&lt;quote&gt;"|').*?(?P=quote)/</code></pre>

The above expression will create the same effect as the previous back reference example, but by instead using named groups. It is also significantly easier to read.

Named groups are also useful when sifting through the array of matches. The name given to a specific pattern is also the key of the corresponding matches array.

<pre><code class="language-php">preg_match( '/(?P&lt;quote&gt;"|')/', "'String'", $matches );

# This will print "'"
echo $matches[1];

# This will also print "'", as it is a named group
echo $matches['quote'];</code></pre>

Thus, named groups not only make code easier to read but also organize it.</p>

## 4\. Word Boundaries

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1c1b2f-de72-4f32-82f1-1d537dcfdcf1/boundary.jpg" alt="Word Boundaries" width="400" height="284" />

<strong>Word boundaries</strong> are places in a string that come between a word character and a non-word character. The specialty of these boundaries is the fact that they don't actually match a character. Their length is <em>zero</em>. The <code>b</code> regular expression matches any word boundary.

Unfortunately, boundaries are so often skimmed over that many do not recognize their real significance. For example, let's say you want to match the word "import":

<pre><code class="language-php">/import/</code></pre>

Watch out! Regular expressions can be tricky. The above expression will also match:

<pre><code class="language-php">important</code></pre>

You may think it is as simple as adding a space before and after import to prevent these bogus matches:

<pre><code class="language-php">/ import /</code></pre>

But what about this case?

<pre><code class="language-php">The trader voted for the import</code></pre>

When import is at the beginning or the end of a string, the modified regex will fail. Thus, splitting this up into cases is required:

<pre><code class="language-php">/(^import | import | import$)/i</code></pre>

Looking back at our regular expression, it does not take periods or other punctuation into account. Just to match this single word, a regular expressions may look like this:

<pre><code class="language-php">/(^import(:|;|,)? | import(:|;|,)? | import(.|?|!)?$)/i</code></pre>

That's a lot of code to match just a single word. This is why word boundaries are so significant. To accomplish the above statement and <strong>many other variations</strong> with word boundaries, all that is necessary is:

<pre><code class="language-php">/bimportb/</code></pre>

This will match every case above and more. <code>b</code>'s flexibility comes from the fact that it matches a zero-length string. All it matches is an imaginary space between two characters. It checks if one of the characters is a non-word character and the other is a word character. If so, it matches it. If the beginning or end of a string is encountered, <code>b</code> treats it as a non-word character. Because the <code>i</code> in import is still considered a word character, it will match import.

Note that the opposite of b is B. This operator will match the space in-between two word or two non-word characters. Thus, if you would like to match 'hi' inside another word, you could use:

<pre><code class="language-php">BhiB</code></pre>

## 5\. Atomic Groups

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/397abd24-6793-499a-8bc3-2a49bf86b741/groups.jpg" alt="Advanced Operators" width="400" height="266" />

<strong>Atomic groups</strong> are special regex groups that are non-capturing. They are usually used to increase the efficiency of a regular expression, but may also be applied to eliminate certain matches. An atomic group is specified by using (?&gt;pattern):

<pre><code class="language-php">/(?&gt;his|this)/</code></pre>

When the regex engine matches an atomic group, it will discard backtracting positions that came with all tokens inside it. Consider the word 'smashing'. Using the above regular expression, the regex engine will first try to match the pattern 'his' in 'smashing'. It will not find a match. At this point, the atomic group will kick in. The engine will discard all backtracking positions. This means that it will not search for 'this' inside 'smashing'. Why? If 'his' did not return a match, then obviously 'this' (which includes 'his') will not return positive either.

The above example did not have many practical uses. We might as well have used <code>/t?his?/</code> instead. Look at the following:

<pre><code class="language-php">/b(engineer|engrave|end)b/</code></pre>

If the regex engine is given the word 'engineering', it will correctly match 'engineer'. The next word boundary, b, will not match. Thus, it will move on to the next match: engrave. It realizes that the 'eng' matches, but the rest do not. Finally, 'end' is attempted and also failed. If you look carefully, you will realize that once the engine matches 'engineer' and fails the last word boundary, it can not possibly match 'engrave' or 'end'. These two matches are smaller words than 'engineer', and thus the regex engine should not continue with the other trials.

<pre><code class="language-php">/b(?&gt;engineer|engrave|end)b/</code></pre>

The above is a much better alternative that will save the regex engine time and improve the code's efficiency.</p>

## 6\. Recursion

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034e0c67-55bd-44bc-a003-06e5c823e97f/recursion.jpg" alt="Recursion" width="400" height="300" />

<strong>Recursion</strong> in regular expressions can be used to match nested constructs, such as parentheses, (this (that)), and HTML tags, <code>&lt;div&gt;&lt;/div&gt;</code>. They require the use of <code>(?R)</code>, an operator that matches recursive sub-patterns. Consider the regular expression that matches nested parentheses:

<pre><code class="language-php">/(((?&gt;[^()]+)|(?R))*)/</code></pre>

The outermost parentheses in this regular expression match the beginning of the nested constructs. Then comes an optional operator, which can either match non-parenthetical characters (<code>?&gt;[^()]+</code>) or the whole expression again in a sub-pattern, (?R). Notice that this operator is repeated as many times as possible to match all nested parentheses.

Another example of recursion at work is the following:

<pre><code class="language-php">/&lt;([w]+).*?&gt;((?&gt;[^&lt;&gt;]+)|((?R)))*/</code></pre>

The above expression combines character groups, greedy operators, back-tracking, and atomic groups to match nested tags. The first parenthesized group ([w]+) matches the tag name for use later in the regular expression. It then proceeds to match the rest of the tag. The next parenthesized sub-expression is very similar to the one above. It either matches non-tag (?&gt;[^&lt;&gt;]+) characters or recurses over another tag (?R). Finally, the last part of the expression matches the close tag.</p>

## 7\. Callbacks

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc2c18f6-3137-403d-b531-e90c858ac7ae/call.jpg" alt="Callbacks" width="400" height="290" />

Certain matches in a pattern may require special modifications. In order to apply multiple or complex changes, <strong>callbacks</strong> can be used. A callback is used for dynamic substitution Strings in the <code>preg_replace_callback</code> function. They take in a function as a parameter to use when a match is found. This function receives the match array as a parameter and returns a modified string that is used as a replacement.

As an example, consider a regular expression that changes all words to uppercase in a given string. Unfortunately, PHP does not have a regex operator that changes a character to a different case. To accomplish this task, a callback may be used. First, the expression must match all letters that need to be capitalized:

<pre><code class="language-php">/bw/</code></pre>

The above uses both word boundaries and character classes to work. Now that we have this expression, we can write a callback function:

<pre><code class="language-php">function upper_case( $matches ) {
	return strtoupper( $matches[0] );
}</code></pre>

<code>upper_case</code> takes in an array of matches and returns the whole matched pattern in uppercase. <code>$matches[0]</code>, in this case, represents the letter that needs to be capitalized. All of this can now be put together using the <code>preg_replace_callback</code> function:

<pre><code class="language-php">preg_replace_callback( '/bw/', "upper_case", $str );</code></pre>

That is the power of a simple callback.</p>

## 8\. Commenting

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc88e1af-f131-4b2b-954f-760a08f3f025/comment.jpg" alt="Commenting" width="400" height="300" />

<strong>Commenting</strong> is not a way to actually match strings, but it is one of the most important parts of regular expressions. As you dive deep into larger, more complex expressions, it becomes hard to decipher what is actually being matched. Using comments in the middle of regular expressions is the perfect way to minimize such confusion.

To place a comment inside a regular expression, use the <code>(?#comment)</code> format. Replace "comment" with the word(s) of your choice:

<pre><code class="language-php">/(?#digit)d/</code></pre>

It is especially important to comment regular expressions that you release to the public. Users of your regex will be able to easily understand and modify the pattern to meet their needs. It can even go so far as to help you decode it when revisiting a program.

Consider using the "x" or (?x) modifier for free-spacing mode with comments. This causes a regular expression to ignore white space between tokens. All spaces can still be represented with <code>[ ]</code> or <code> </code> (a backslash and a space):

<pre><code class="language-php">/
d    #digit
[ ]   #space
w+   #word
/x</code></pre>

The above is the same as:

<pre><code class="language-php">/d(?#digit)[ ](?#space)w+(?#word)/</code></pre>

Always create well-documented code.</p>

## Further Resources

*   [Regular-Expressions.info](https://www.regular-expressions.info/) Comprehensive website on regular expressions
*   [Cheat Sheet](https://www.addedbytes.com/cheat-sheets/regular-expressions-cheat-sheet/) Informative regular expressions cheat sheet
*   Regex Generator JavaScript regular expressions generator

{{< signature "al" >}}

