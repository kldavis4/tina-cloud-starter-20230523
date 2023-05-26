---
title: 'The Essential Guide To JavaScript’s Newest Data Type: BigInt'
slug: essential-guide-javascript-newest-data-type-bigInt
author: farazkelhini
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fead15a6-e423-481e-a983-acc735caf56e/javascript-bigint-sharing-card.png
date: 2019-07-22T14:00:59+02:00
summary: >-
  In JavaScript, the <code>Number</code> type cannot safely represent integer values larger than 2<sup>53</sup>. This limitation has forced developers to use inefficient workarounds and third-party libraries. <code>BigInt</code> is a new data type intended to fix that.
description: >-
  In JavaScript, the Number type cannot safely represent integer values larger than 2⁵³. This limitation has forced developers to use inefficient workarounds and third-party libraries. <code>BigInt</code> is a new data type intended to fix that.
categories:
  - JavaScript
  - Techniques
---
The `BigInt` data type aims to enable JavaScript programmers to represent integer values larger than the range supported by the `Number` data type. The ability to represent integers with arbitrary precision is particularly important when performing mathematical operations on large integers. With `BigInt`, integer overflow will no longer be an issue.

Additionally, you can safely work with high-resolution timestamps, large integer IDs, and more without having to use a workaround. `BigInt` is currently a stage 3 proposal. Once added to the specification, it will become the second numeric data type in JavaScript, which will bring the total number of supported data types to eight:

-  Boolean
-  Null
-  Undefined
-  Number
-  BigInt
-  String
-  Symbol
-  Object

In this article, we will take a good look at `BigInt` and see how it can help overcome the limitations of the `Number` type in JavaScript.

## The Problem

The lack of an explicit integer type in JavaScript is often baffling to programmers coming from other languages. Many programming languages support multiple numeric types such as float, double, integer, and bignum, but that's not the case with JavaScript. In JavaScript, all numbers are represented in [double-precision 64-bit floating-point format](https://en.wikipedia.org/wiki/Double_precision_floating-point_format) as defined by the [IEEE 754-2008](https://en.wikipedia.org/wiki/IEEE_754-2008_revision) standard.

{{% feature-panel %}}

Under this standard, very large integers that cannot be exactly represented are automatically rounded. To be precise, the `Number` type in JavaScript can only safely represent integers between -9007199254740991 (-(2<sup>53</sup>-1)) and 9007199254740991 (2<sup>53</sup>-1). Any integer value that falls out of this range may lose precision.

This can be easily examined by executing the following code:

<pre><code class="language-javascript">console.log(9999999999999999);    // → 10000000000000000
</code></pre>

This integer is larger than the largest number JavaScript can reliably represent with the `Number` primitive. Therefore, it's rounded. Unexpected rounding can compromise a program's reliability and security. Here's another example:

<pre><code class="language-javascript">// notice the last digits
9007199254740992 === 9007199254740993;    // → true
</code></pre>

JavaScript provides the `Number.MAX_SAFE_INTEGER` constant that allows you to quickly obtain the maximum safe integer in JavaScript. Similarly, you can obtain the minimum safe integer by using the `Number.MIN_SAFE_INTEGER` constant:

<pre><code class="language-javascript">const minInt = Number.MIN_SAFE_INTEGER;

console.log(minInt);         // → -9007199254740991

console.log(minInt - 5);     // → -9007199254740996

// notice how this outputs the same value as above
console.log(minInt - 4);     // → -9007199254740996
</code></pre>

## The Solution

As a workaround to these limitations, some JavaScript developers represent large integers using the `String` type. The [Twitter API](https://developer.twitter.com/en/docs/basics/twitter-ids), for example, adds a string version of IDs to objects when responding with JSON. Additionally, a number of libraries such as [bignumber.js](https://github.com/MikeMcl/bignumber.js/) have been developed to make working with large integers easier.

With `BigInt`, applications no longer need a workaround or library to safely represent integers beyond `Number.MAX_SAFE_INTEGER` and `Number.Min_SAFE_INTEGER`. Arithmetic operations on large integers can now be performed in standard JavaScript without risking loss of precision. The added benefit of using a native data type over a third-party library is better run-time performance.

To create a `BigInt`, simply append `n` to the end of an integer. Compare:

<pre><code class="language-javascript">console.log(9007199254740995n);    // → 9007199254740995n
console.log(9007199254740995);     // → 9007199254740996
</code></pre>

Alternatively, you can call the `BigInt()` constructor:

<pre><code class="language-javascript">BigInt("9007199254740995");    // → 9007199254740995n
</code></pre>

`BigInt` literals can also be written in binary, octal or hexadecimal notation:

<div class="break-out">

<pre><code class="language-javascript">
// binary
console.log(0b100000000000000000000000000000000000000000000000000011n);
// → 9007199254740995n

// hex
console.log(0x20000000000003n);
// → 9007199254740995n

// octal
console.log(0o400000000000000003n);
// → 9007199254740995n

// note that legacy octal syntax is not supported
console.log(0400000000000000003n);
// → SyntaxError
</code></pre>
</div>

Keep in mind that you can't use the strict equality operator to compare a `BigInt` to a regular number because they are not of the same type:

<pre><code class="language-javascript">console.log(10n === 10);    // → false

console.log(typeof 10n);    // → bigint
console.log(typeof 10);     // → number
</code></pre>

{{% ad-panel-leaderboard %}}

Instead, you can use the equality operator, which performs implicit type conversion before compering its operands:

<pre><code class="language-javascript">console.log(10n == 10);    // → true
</code></pre>

All arithmetic operators can be used on `BigInt`s except for the unary plus (`+`) operator:

<div class="break-out">

<pre><code class="language-javascript">10n + 20n;    // → 30n
10n - 20n;    // → -10n
+10n;         // → TypeError: Cannot convert a BigInt value to a number
-10n;         // → -10n
10n * 20n;    // → 200n
20n / 10n;    // → 2n
23n % 10n;    // → 3n
10n ** 3n;    // → 1000n

let x = 10n;
++x;          // → 11n
--x;          // → 10n
</code></pre>
</div>

The reason that the unary plus (`+`) operator is not supported is that some programs may rely on the invariant that `+` always produces a `Number`, or throws an exception. Changing the behavior of `+` would also break asm.js code.

Naturally, when used with `BigInt` operands, arithmetic operators are expected to return a `BigInt` value. Therefore, the result of the division (`/`) operator is automatically truncated. For example:

<pre><code class="language-javascript">25 / 10;      // → 2.5
25n / 10n;    // → 2n
</code></pre>

## Implicit Type Conversion

Because implicit type conversion could lose information, mixed operations between `BigInt`s and `Number`s are not allowed. When mixing large integers and floating-point numbers, the resulting value may not be accurately representable by `BigInt` or `Number`. Consider the following example:

<pre><code class="language-javascript">(9007199254740992n + 1n) + 0.5
</code></pre>

The result of this expression is outside of the domain of both `BigInt` and `Number`. A `Number` with a fractional part cannot be accurately converted to a `BigInt`. And a `BigInt` larger than 2<sup>53</sup> cannot be accurately converted to a `Number`.

As a result of this restriction, it’s not possible to perform arithmetic operations with a mix of  `Number` and `BigInt` operands. You also cannot pass a `BigInt` to Web APIs and built-in JavaScript functions that expect a `Number`. Attempting to do so will cause a `TypeError`:

<pre><code class="language-javascript">10 + 10n;    // → TypeError
Math.max(2n, 4n, 6n);    // → TypeError
</code></pre>

Note that relational operators do not follow this rule, as shown in this example:

<pre><code class="language-javascript">10n > 5;    // → true
</code></pre>

If you want to perform arithmetic computations with `BigInt` and `Number`, you first need to determine the domain in which the operation should be done. To do that, simply convert either of the operands by calling `Number()` or `BigInt()`:

<pre><code class="language-javascript">BigInt(10) + 10n;    // → 20n
// or
10 + Number(10n);    // → 20
</code></pre>

When encountered in a `Boolean` context, `BigInt` is treated similar to `Number`. In other words, a `BigInt` is considered a truthy value as long as it's not `0n`:

<pre><code class="language-javascript">if (5n) {
    // this code block will be executed
}

if (0n) {
    // but this code block won't
}
</code></pre>

No implicit type conversion between `BigInt` and `Number` types occurs when sorting an array:

<pre><code class="language-javascript">const arr = [3n, 4, 2, 1n, 0, -1n];

arr.sort();    // → [-1n, 0, 1n, 2, 3n, 4]
</code></pre>

Bitwise operators such as `|`, `&`, `<<`, `>>`, and `^` operate on `BigInt`s in a similar way to `Number`s. Negative numbers are interpreted as infinite-length two's complement. Mixed operands are not allowed. Here are some examples:

<pre><code class="language-javascript">90 | 115;      // → 123
90n | 115n;    // → 123n
90n | 115;     // → TypeError
</code></pre>

{{% ad-panel-leaderboard %}}

## The BigInt Constructor

As with other primitive types, a `BigInt` can be created using a constructor function. The argument passed to `BigInt()` is automatically converted to a `BigInt`, if possible:

<pre><code class="language-javascript">BigInt("10");    // → 10n
BigInt(10);      // → 10n
BigInt(true);    // → 1n
</code></pre>

Data types and values that cannot be converted throw an exception:

<pre><code class="language-javascript">BigInt(10.2);     // → RangeError
BigInt(null);     // → TypeError
BigInt("abc");    // → SyntaxError
</code></pre>

You can directly perform arithmetic operations on a `BigInt` created using a constructor:

<pre><code class="language-javascript">BigInt(10) * 10n;    // → 100n
</code></pre>

When used as operands of the strict equality operator, `BigInt`s created using a constructor are treated similar to regular ones:

<pre><code class="language-javascript">BigInt(true) === 1n;    // → true
</code></pre>

## Library Functions

JavaScript provides two library functions for representing `BigInt` values as signed or unsigned integers:

- `BigInt.asUintN(width, BigInt)`: wraps a `BigInt` between 0 and 2<sup>width</sup>-1
- `BigInt.asIntN(width, BigInt)`: wraps a `BigInt` between -2<sup>width-1</sup> and 2<sup>width-1</sup>-1

These functions are particularly useful when performing 64-bit arithmetic operations. This way you can stay within the intended range.

## Browser Support And Transpiling

At the time of this writing, Chrome +67 and Opera +54 fully support the `BigInt` data type. Unfortunately, Edge and Safari haven't implemented it yet. Firefox doesn't support `BigInt` by default, but it can be enabled by setting `javascript.options.bigint` to `true` in `about:config`. An up-to-date list of supported browsers is available on [Can I use…](https://caniuse.com/#search=bigint).

Unluckily, transpiling `BigInt` is an [extremely complicated process](https://github.com/GoogleChromeLabs/jsbi#why), which incurs hefty run-time performance penalty. It's also impossible to directly polyfill `BigInt` because the proposal changes the behavior of several existing operators. For now, a better alternative is to use the [JSBI](https://github.com/GoogleChromeLabs/jsbi) library, which is a pure-JavaScript implementation of the `BigInt` proposal.

This library provides an API that behaves exactly the same as the native `BigInt`. Here's how you can use JSBI:

<pre><code class="language-javascript">import JSBI from './jsbi.mjs';

const b1 = JSBI.BigInt(Number.MAX_SAFE_INTEGER);
const b2 = JSBI.BigInt('10');

const result = JSBI.add(b1, b2);

console.log(String(result));    // → '9007199254741001'
</code></pre>

An advantage of using JSBI is that once browser support improves, you won't need to rewrite your code. Instead, you can automatically compile your JSBI code into native `BigInt` code by using a [babel plugin](https://github.com/GoogleChromeLabs/babel-plugin-transform-jsbi-to-bigint). Furthermore, the performance of JSBI is on par with native `BigInt` implementations. You can expect wider browser support for `BigInt` soon.

## Conclusion

`BigInt` is a new data type intended for use when integer values are larger than the range supported by the `Number` data type. This data type allows us to safely perform arithmetic operations on large integers, represent high-resolution timestamps, use large integer IDs, and more without the need to use a library.

It's important to keep in mind that you cannot perform arithmetic operations with a mix of `Number` and `BigInt` operands. You'll need to determine the domain in which the operation should be done by explicitly converting either of the operands. Moreover, for compatibility reasons, you are not allowed to use the unary plus (`+`) operator on a `BigInt`.

What do you think? Do you find `BigInt` useful? Let us know in the comments!

{{< signature "dm, yk, il" >}}
