---
title: Optimizing Long Lists Of Yes / No Values With JavaScript
slug: optimizing-long-lists-of-yesno-values-with-javascript
image: null
date: 2011-10-19T18:55:34.000Z
author: lea-verou
description: >-
  Very frequently in Web development (and programming in general), you need to store a long list of boolean values (yes/no, true/false, checked/unchecked…
  you get the idea) into something that accepts only strings. Maybe it’s because you want to store them in `localStorage` or in a cookie, or send them through the body of an HTTP request. I’ve needed to do this countless times.
categories:
  - Coding
  - JavaScript
---
The last time I stumbled on such a case wasn’t with my own code. It was when Christian Heilmann showed me his then new slide deck, with a cool feature where you could toggle the visibility of individual slides in and out of the presentation. On seeing it, I was impressed. Looking more closely, though, I realized that the checkbox states did not persist after the page reloaded.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [A Quick Look Into The Math Of Animations With JavaScript](https://www.smashingmagazine.com/2011/10/quick-look-math-animations-javascript/)
*   [10 Oddities And Secrets About JavaScript](https://www.smashingmagazine.com/2011/05/10-oddities-and-secrets-about-javascript/)

So, someone could spend a long time carefully tweaking their slides, only to accidentally hit F5 or crash their browser, and then — boom! — all their work would be lost. Christian told me that he was already working on storing the checkbox states in <code>localStorage</code>. Then, naturally, we endlessly debated the storage format. That debate inspired me to write this article, to explore the various approaches in depth.

{{% feature-panel %}}

## Using An Array

We have two (reasonable) ways to model our data in an array. One is to store true/false values, like so:

<pre><code class="language-javascript">[false, true, true, false, false, true, true]</code></pre>

The other is to store an array of 0s and 1s, like so:

<pre><code class="language-javascript">[0, 1, 1, 0, 0, 1, 1]</code></pre>

Whichever solution we go with, we will ultimately have to convert it to a string, and then convert it back to an array when it is read. We have two ways to proceed: either with the old <code>Array#join()</code> (or <code>Array#toString()</code>) and <code>String#split()</code>, or with the fancier <code>JSON.stringify()</code> and <code>JSON.parse()</code>.

With the JSON way, the code will be somewhat shorter, although it is the JavaScript equivalent of slicing bread with a chainsaw. <a href="https://web.archive.org/web/20160320024859/https://jsperf.com/json-vs-split-join-for-simple-arrays">Not only there is a performance impact in most browsers</a>, but you’re also cutting down browser support quite a bit.

The main drawback of using array-based strings is their size in bytes. If you go with the number method, you would use almost 2 characters per number (or, more precisely, <code>2N − 1</code>, since you’d need one delimiter per number, except for the last one):

<pre><code class="language-javascript">[0, 1, 1, 0, 0, 1, 1].toString().length // 13, for 7 values</code></pre>

So, for 512 numbers, that would be 1023 characters or 2 KB, since <a href="https://es5.github.com/#x4.3.16">JavaScript uses UTF-16</a>. If you go with the boolean method, it’s even worse:

<pre><code class="language-javascript">[false, true, true, false, false, true, true].toString().length // 37, also for 7 values</code></pre>

That’s around 5 to 6 characters per value, so 2560 to 3072 characters for 512 numbers (which is 5 to 6 KB). <code>JSON.stringify()</code> even wastes 2 more characters in each case, for the opening and closing brackets, but its advantage is that you get your original value types back with <code>JSON.parse()</code> instead of strings.</p>

## Using A String

Using a string saves some space, because no delimiters are involved. For example, if you go with the number approach and store strings like <code>'01001101010111'</code>, you are essentially storing one character per value, which is 100% better than the better of the two previous approaches. You can then get the values into an array by using <code>String#split</code>:

<pre><code class="language-javascript">'01001101010111'.split(’); // ['0','1','0','0','1','1','0','1','0','1','0','1','1','1']</code></pre>

Or you could just loop over the string using <code>string.charAt(i)</code> — or even the string indexes (<code>string[i]</code>), if you don’t care about older browsers.</p>

## Using Bitfields

Did the previous method make you think of binary numbers? It’s not just you. The concept of <a href="https://en.wikipedia.org/wiki/Bit_field">bitfields</a> is quite popular in other programming languages, but not so much in JavaScript. In a nutshell, bitfields are used to pack a lot of boolean values into <strong>the bits</strong> of the boolean representation of a number. For example, if you have eight values (true, false, false, true, false, true, true, false), the number would be 10010110 in binary; so, 150 in decimal and 96 in hex. That’s 2 characters instead of 8, so <strong>75% saved</strong>. In general, 1 digit in the hex representation corresponds to exactly 4 bits. (That’s because <code>16 = 2<sup>4</sup></code>. In general, in a <code>base2<sup>n</sup></code> system, you can pack <code>n</code> bits into every <code>base2<sup>n</sup></code> digit.) So, <strong>we weren’t lucky with that 75%; it’s always that much</strong>.

Thus, instead of storing that string as a string and using 1 character per value, we can be smarter and convert it to a (hex) number first. How do we do that? It’s no more than a line of code:

<pre><code class="language-javascript">parseInt('10010110', 2).toString(16); // returns '96'</code></pre>

And how do we read it back? That’s just as simple:

<pre><code class="language-javascript">parseInt('96', 16).toString(2); // returns  '10010110'</code></pre>

From this point on, we can follow the same process as the previous method to loop over the values and do something useful with them.</p>

## Can We Do Better?

In fact, we can! Why convert it to a hex (base 16) number, which uses only 6 of the 26 alphabet letters? The <code>Number#toString()</code> method allows us to go up to <a href="https://en.wikipedia.org/wiki/Base_36">base 36</a> (throwing a <code>RangeError</code> for <code>&gt;= 37</code>), which effectively uses <em>all</em> letters in the alphabet, all the way up to z! This way, we can have a compression of up to 6 characters for 32 values, which means saving up to 81.25% compared to the plain string method! And the code is just as simple:

<pre><code class="language-javascript">parseInt( '1001011000', 2).toString(36); // returns 'go' (instead of '258', which would be the hex version)
parseInt('go', 36).toString(2); // returns  '1001011000'</code></pre>

For some of you, this will be enough. But I can almost hear the more inquisitive minds out there shouting, “But we have capital letters, we have other symbols, we are still not using strings to their full potential!” And you’d be right. There is a reason why every time you open a binary file in a text editor, you get weird symbols mixed with numbers, uppercase letters, lowercase letters and whatnot. Every character in an UTF-16 string is a 2 bytes (16 bits), which means that if we use the right compression algorithm, we should be able to store 16 yes/no values in it (saving 93.75% from the string method).

The problem is that JavaScript doesn’t offer a built-in way to do that, so the code becomes a bit more complicated.

## Packing 16 Values Into One Character

You can use <code>String.fromCharCode</code> to get the individual characters. It accepts a numerical value of up to 65,535 and returns a character (and for values greater than that, it returns an empty string).

So, we have to split our string into chunks of 16 characters in size. We can <a href="https://stackoverflow.com/questions/7033639/javascript-split-large-string-in-n-size-chunks">do that through <code>.match(/.{1,16}/g)</code></a>. To sum up, the full solution would look like this:

<pre><code class="language-javascript">function pack(/* string */ values) {
    var chunks = values.match(/.{1,16}/g), packed = ’;
    for (var i=0; i &lt; chunks.length; i++) {
        packed += String.fromCharCode(parseInt(chunks[i], 2));
    }
    return packed;
}

function unpack(/* string */ packed) {
    var values = ’;
    for (var i=0; i &lt; packed.length; i++) {
        values += packed.charCodeAt(i).toString(2);
    }
    return values;
}</code></pre>

It wasn’t that hard, was it?

With these few lines of code, you can pack the aforementioned 512 values into — drum roll, please — <strong>32 characters (64 bytes)</strong>!

Quite an improvement over our original 2 KB (with the array method), isn’t it?

## Limitations

Numbers in JavaScript have limits. For the methods discussed here that involve an intermediate state of converting to a number, the limit appears to be <strong>1023</strong> yes/no values, because <code>parseInt('1111…1111', 2)</code> returns <code>Infinity</code> when the number of aces is bigger than 1023. This limit does not apply to the last method, because we’re only converting blocks of bits instead of the whole thing. And, of course, it doesn’t apply to the first two methods (array and string) because they don’t involve packing the values into an integer.</p>

## “I Think You Took It A Bit Too Far”

This might be overkill for some cases. But it will definitely come in handy when you want to store a lot of boolean values in any limited space that can only store strings. And no optimization is overkill for things that go through the wire frequently. For example, cookies are sent on every single request, so they should be as tiny as possible. Another use case would be online multiplayer games, for which response times should be lightning-fast, otherwise the games wouldn’t be fun.

And even if this kind of optimization isn’t your thing, I hope you’ve found the thought process and the code involved educational.

{{< signature "al" >}}

<em>Thanks to <a href="https://eligrey.com">Eli Grey</a> and <a href="https://29a.ch/">Jonas Wagner</a> for their advice and corrections</em>

<em>Image on front page created by <a href="https://www.flickr.com/photos/7162499@N02/3260095534/">Ruiwen Chua</a>.</em>

