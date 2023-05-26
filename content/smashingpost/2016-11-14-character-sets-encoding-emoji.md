---
title: 'Everything You Need To Know About Emoji 🍭'
slug: character-sets-encoding-emoji
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc51c46-da42-40bb-97df-97812a1d35b9/twemoji-sampler-500px-preview-opt.png
date: 2016-11-14T19:35:40.000Z
author: robreed
summary: >-
  Depending on your browser, you may not be able to see all emoji featured in this article (especially the Tifinagh characters). Also, different platforms vary in how they display emoji as well. That’s why the article always provides textual alternatives. Don’t let it discourage you from reading though!
description: >-
  Depending on your browser, you may not be able to see all emoji featured in this article (especially the Tifinagh characters). Also, different platforms vary in how they display emoji as well. That’s why the article always provides textual alternatives. Don’t let it discourage you from reading though!
categories:
  - UX
  - Graphics
  - Graphic Design
  - Web Design
  - Icons
  - Design Principles
  - UX
  - Guides
---
We all recognize emoji. They’ve become the global pop stars of digital communication. But what are they, technically speaking? And what might we learn by taking a closer look at these images, characters, pictographs… whatever they are 🤔 (Thinking Face). We will dig deep to learn about how these thingamajigs work.

Now, let's start with a seemingly simple question.

### What Are Emoji?

<pre><code class="language-html">                                         ⛅
🎈
    🌲             🏡        🌲🌲     🏃  🌲
</code></pre>

<p>What we'll find is that they are born from, and depend on, the same technical foundation, character sets and document encoding that underlie the rest of our work as web-based designers, developers and content creators. So, we'll delve into these topics using emoji as motivation to explore this fundamental aspect of the web. We'll learn all about emoji as we go, including how we can effectively work them into our own projects, and we'll collect valuable resources along the way.</p>

<p>There is a lot of misinformation about these topics online, a fact made painfully clear to me as I was writing this article. Chances are you've encountered more than a little of it yourself. The recent release of Unicode 9 and the enormous popularity of emoji make now as good a time as any to take a moment to appreciate just how important this topic is, to look at it afresh and to fill in any gaps in our knowledge, large or small.</p>

<p>By the end of this article, you will know <strong>everything you need to know about emoji</strong>, regardless of the platform or application you're using, including the distributed web. What's more, you'll know where to find the authoritative details to answer any emoji-related question you may have now or in the future.</p>

<p>21 June 2016 brought the <a title="Announcing The Unicode Standard, Version 9.0 blog post" href="https://blog.unicode.org/2016/06/announcing-unicode-standard-version-90.html">official release of Unicode Version 9.0</a>, and with it 72 new emoji. What are they? Where do new emoji come from anyway? Why aren't your friends seeing the new ROFL, Fox Face, Crossed Fingers and Pancakes emoji you're sending them?! ? 😡 (Pouting Face emoji) Keep reading for the answers to these and many other questions.</p>

{{% feature-panel %}}

<p>A question to get us started:</p>

<blockquote>What is the plural form of the word "emoji"?</blockquote>

<p>It's a question that came up in the process of reviewing and editing this article. The good news is that I have an answer! The bad news (depending on how bothered you are by triviality) is that the answer is that there is no definitive answer. I believe the most accurate answer that can be given is to say that, currently, there is no established correct form for the plural of emoji.</p>

<p>An article titled "<a href="https://www.theatlantic.com/technology/archive/2016/01/whats-the-plural-of-emoji-emojis/422763/">What's the Plural of Emoji?</a>" by <a title="Author page at theatlantic.com" href="https://www.theatlantic.com/author/robinson-meyer/">Robinson Meyer</a>, published by <a title="The Atlantic homepage" href="https://www.theatlantic.com/">The Atlantic</a> on 6 January 2016, discusses exactly this issue. The author turns up recent conflicting uses of both forms "emoji" and "emojis," even within the same national publications:</p>

<blockquote>In written English right now, there's little consensus on this question. National publications have not settled on a regular style. The Atlantic, for instance, used both (<a href="https://www.theatlantic.com/technology/archive/2015/10/eagle-avocado-canoe-pregnant-woman-2016-new-emoji/410056/">emoji</a>, <a href="https://www.theatlantic.com/politics/archive/2015/12/emojis-2016-presidential-election/420840/">emojis</a>) in the last quarter of 2015. And in October alone in The New York Times, you could find the technology reporter Vindu Goel covering <a href="https://www.nytimes.com/2015/10/09/technology/facebook-to-test-emoji-as-reaction-icons.html">Facebook's "six new emoji,"</a> despite, two weeks later, Austin Ramzy detailing the Australian foreign minister's "<a href="https://www.nytimes.com/2015/10/23/world/australia/australia-emoji-julie-bishop-diplomacy-vladimir-putin.html">liberal use of emojis</a>." …</blockquote>

<p>The Unicode Emoji Subcommittee, which, as we will see, is the group responsible for emoji in the Unicode Standard, uses "emoji" as the plural form. This plural form appears in passages of documentation quoted in this article. Consider, for example, the very first sentence of the first paragraph of the <a title="Emoji Subcommittee site" href="https://unicode.org/emoji/">Emoji Subcommittee's official homepage at unicode.org</a>:</p>

<blockquote>Emoji are pictographs (pictorial symbols) that are typically presented in a colorful form and used inline in text. They represent things such as faces, weather, vehicles and buildings, food and drink, animals and plants, or icons that represent emotions, feelings, or activities.</blockquote>

<p>I have chosen the plural "emoji", for the sake of consistency if nothing else. At this point in time, you can confidently use whichever form you prefer, unless of course the organization or individual for whom you're writing has strong opinions one way or the other. You can and should consult your style guide if necessary.</p>

<p>We'll start at the beginning, with the basic building blocks not just of emoji, nor even digital communication, but of all written language: characters and character sets.</p>

### Table of Contents
<ol>
  <li>
    <a href="#">Character Sets And Document Encoding: An Overview</a>
    <ol>
      <li><a href="#">Characters</a></li>
      <li><a href="#">Character Sets</a></li>
      <li><a href="#">Coded Character Sets</a></li>
      <li><a href="#">Encoding</a></li>
    </ol>
  </li>
  <li>
    <a href="#">Declaring Character Sets And Document Encoding On The Web</a>
    <ol>
      <li>
        <a href="#"><code>content-type</code> HTTP Header Declaration</a>
      </li>
      <li>
        <a href="#">Checking HTTP Headers Using A Browser’s Developer Tools</a>
      </li>
      <li><a href="#">Checking HTTP Headers Using Web-based Tools</a></li>
      <li>
        <a href="#">Using A Meta Element With <code>charset</code> Attribute</a>
      </li>
      <li><a href="#">An Encoding By Any Other Name</a></li>
    </ol>
  </li>
  <li>
    <a href="#">What Were We Talking About Again? Oh Yeah, Emoji!</a>
    <ol>
      <li><a href="#">So What Are Emoji?</a></li>
      <li><a href="#">How Do We Use Emoji?</a></li>
      <li><a href="#">Character References</a></li>
      <li><a href="#">Glyphs</a></li>
      <li><a href="#">How Do We Know If We Have These Symbols?</a></li>
      <li><a href="#">The Great Emoji Proliferation Of 2016</a></li>
    </ol>
  </li>
  <li>
    <a href="#">Emoji OS Support</a>
    <ol>
      <li><a href="#">Emoji Support: Apple Platforms (macOS and iOS)</a></li>
      <li><a href="#">Emoji Support: Windows</a></li>
      <li><a href="#">Emoji Support: Linux</a></li>
      <li><a href="#">Emoji Support: Android</a></li>
    </ol>
  </li>
  <li>
    <a href="#">Emoji On The Web</a>
    <ol>
      <li><a href="#">Emoji One</a></li>
      <li><a href="#">Twemoji</a></li>
    </ol>
  </li>
  <li><a href="#">Conclusion</a></li>
</ol>

## Character Sets And Document Encoding: An Overview

### Characters

<p>A dictionary definition for a <em>character</em> will do to get us started: "A character is commonly a symbol representing a letter or number."</p>

<p>That's simple enough. But like so many other concepts, for it to be meaningful, we need to consider the broader context and put it into practice. Characters, in and of themselves, are not enough. I could draw a squiggle with a pencil on a piece of paper and rightfully call it a character, but that wouldn't be particularly valuable. Not only that, but it is difficult to convey a useful amount of information using a single character. We need more.</p>

### Character Sets

<p>A <em>character set</em> is "a set of characters."</p>

<p>Expanding on that a bit, we can take a step back and consider a slightly more precise but still general description of a set: a group or collection of things that belong together, resemble one another or are usually found together.</p>

<p>Because we're dealing with sets in the context of computing, we can be a little more precise. In the field of computer science a set is: a collection of a finite number of values in no particular order, with the added condition that none of the values are repeated.</p>

<p>What's this about a collection? Technically speaking, a collection is a grouping of a number of items, possibly zero, that have some shared significance.</p>

<p>So, a character set is a grouping of some finite number of characters (i.e. a collection), in no particular order, such that none of the characters are repeated.</p>

<p>That's a solid, precise, if pedantic, definition.</p>

<p>The World Wide Web Consortium (<a title="Official W3C site" href="https://www.w3.org/">W3C</a>), the international community of member organizations that work together to develop standards for the web, has its own definition, which is not far from the generic one we've arrived at on our own.</p>

<p>From the W3C's "<a title="Character set description" href="https://www.w3.org/International/articles/definitions-characters/#charsets">Character Encodings: Essential Concepts</a>":</p>

<blockquote>A character set or repertoire comprises the set of characters one might use for a particular purpose — be it those required to support Western European languages in computers, or those a Chinese child will learn at school in the third grade (nothing to do with computers).</blockquote>

<p>So, any arbitrary set of characters can be considered a character set. There are, however, some well-known standardized character sets that are much more significant than any random grouping we might put together. One such standardized character set, unarguably the most important character set in use today, is Unicode. Again, <a title="Unicode description" href="https://www.w3.org/International/articles/definitions-characters/#unicode">quoting the W3C</a>:</p>

<blockquote>Unicode is a universal character set, i.e. a standard that defines, in one place, all the characters needed for writing the majority of living languages in use on computers. It aims to be, and to a large extent already is, a superset of all other character sets that have been encoded.</blockquote>

<p>Text in a computer or on the Web is composed of characters. Characters represent letters of the alphabet, punctuation, or other symbols.</p>

<p>In the past, different organizations have assembled different sets of characters and created encodings for them — one set may cover just Latin-based Western European languages (excluding EU countries such as Bulgaria or Greece), another may cover a particular Far Eastern language (such as Japanese), others may be one of many sets devised in a rather ad hoc way for representing another language somewhere in the world.</p>

<p>Unfortunately, you can't guarantee that your application will support all encodings, nor that a given encoding will support all your needs for representing a given language. In addition, it is usually impossible to combine different encodings on the same Web page or in a database, so it is usually very difficult to support multilingual pages using ‘legacy' approaches to encoding.</p>

<p>The Unicode Consortium provides a large, single character set that aims to include all the characters needed for any writing system in the world, including ancient scripts (such as Cuneiform, Gothic and Egyptian Hieroglyphs). It is now fundamental to the architecture of the Web and operating systems, and is supported by all major web browsers and applications. The Unicode Standard also describes properties and algorithms for working with characters.</p>

<p>This approach makes it much easier to deal with multilingual pages or systems, and provides much better coverage of your needs than most traditional encoding systems.</blockquote>

<p><strong>Aside</strong>: This W3C document provides a number of understandable and useful definitions relevant to our discussion, so we'll come back to it a few times early in the article.</p>

<p>We just learned that the Unicode Consortium is the group responsible for the Unicode Standard. <a title="Official unicode consortium site" href="https://unicode.org/">From their website</a>:</p>

<blockquote>The Unicode Consortium enables people around the world to use computers in any language. Our freely-available specifications and data form the foundation for software internationalization in all major operating systems, search engines, applications, and the World Wide Web. An essential part of our mission is to educate and engage academic and scientific communities, and the general public.</blockquote>

<p>They provide the following answer to the question, <a href="https://unicode.org/standard/WhatIsUnicode.html">what is Unicode?</a>:</p>

<blockquote>Unicode provides a unique number for every character,
no matter what the platform,
no matter what the program,
no matter what the language.</blockquote>

<p>Fundamentally, computers just deal with numbers. They store letters and other characters by assigning a number for each one. Before Unicode was invented, there were hundreds of different encoding systems for assigning these numbers. No single encoding could contain enough characters: for example, the European Union alone requires several different encodings to cover all its languages. Even for a single language like English no single encoding was adequate for all the letters, punctuation, and technical symbols in common use.</p>

<p>These encoding systems also conflict with one another. That is, two encodings can use the same number for two different characters, or use different numbers for the same character. Any given computer (especially servers) needs to support many different encodings; yet whenever data is passed between different encodings or platforms, that data always runs the risk of corruption.</p>

<p>Unicode provides a unique number for every character, no matter what the platform, no matter what the program, no matter what the language. … The emergence of the Unicode Standard, and the availability of tools supporting it, are among the most significant recent global software technology trends.</blockquote>

<p>In short, Unicode is a single (very) large set of characters designed to encompass "all the characters needed for writing the majority of living languages in use on computers." As such, it "provides a unique number for every character, no matter what the platform, no matter what the program, no matter what the language."</p>

<p>Both the W3C and Unicode Consortium use the term "encoding" as part of their definitions. Descriptions like that, helpful as they may be, are a big part of the reason why there is often confusion around what are in fact simple concepts. Encoding is a more involved, difficult-to-grasp concept than character sets, and one we'll discuss shortly. Don't worry about encoding quite yet; before we get from character sets to encoding, we need one more step.</p>

{{% ad-panel-leaderboard %}}

### Coded Character Sets

<p>Going back to the same "Character Encodings: Essential Concepts" document, the <a title="Coded char set description" href="https://www.w3.org/International/articles/definitions-characters/#charsets">W3C has something to say about coded character sets</a>, too:</p>

<blockquote>A coded character set is a set of characters for which a unique number has been assigned to each character. Units of a coded character set are known as code points. A code point value represents the position of a character in the coded character set. For example, the code point for the letter ‘à' in the Unicode coded character set is 225 in decimal, or E1 in hexadecimal notation. (Note that hexadecimal notation is commonly used for referring to code points…)</blockquote>

<p><strong>Note</strong>: There is an unfortunate mistake in the passage above. The character displayed is "à" and the location given for that symbol in the Unicode coded character set is 225 in decimal, or E1 hexadecimal notation. But 225 (dec) / E1 (hex) is the location of "á," not "à," which is found at 224 (dec) / E0 (hex). Oops! ? 😒 (Unamused Face emoji)</p>

<p>That isn't too difficult to understand. Being able to describe any one character with a numeric code is convenient. Rather than writing "the Latin script letter ‘a' with a diacritic grave," we can say <code>\xE0</code>, the hexadecimal notation for the numeric location of that symbol ("à") in the coded character set known as Unicode. Among other advantages of this arrangement, we can look up that character without having to know what "Latin script letter ‘a' with a diacritic grave" means. The natural-language way of describing a character can be awkward for us, even more so for computers, which are both much better at looking up numeric references than we are and much worse at understanding natural-language descriptions.</p>

<p>So, a coded character set is simply a way to assign a numeric code to every character in a set such that there is a one-to-one correspondence between character and code. With that, not only is the Unicode Consortium's description of Unicode more understandable, but we're ready to tackle encoding.</p>

<pre><code class="language-html">                                           ⛅
🎈
    🌲                    🏡        🏃 🌲🌲         🌲</code></pre>

### Encoding

<p>We've quickly reviewed characters, character sets and coded character sets. That brings us to the last concept we need to cover before turning our attention to emoji. Encoding is both the hardest concept to wrap our heads around and also the easiest. It's the easiest because, as we'll see, in a practical sense, we don't need to know all that much about it.</p>

<p>We've come to an important point of transition. Character sets and coded character sets are in the <strong>human domain</strong>. These are concepts that we must have a good grasp of in order to confidently and effectively do our work. When we get to encoding, we're transitioning into the realm of the computing devices and, more specifically, the low-level storage, retrieval and transmission of data. Encoding is interesting, and it is important that we get right what little of it we are responsible for, but we need only a high-level understanding of the technical details in order to do our part.</p>

<p>The first thing to know is that "character sets" and "encodings" (or, for our purpose here, "document encodings") are not the same thing. That may seem obvious to you, especially now that we're clearly discussing them separately, but it is a common source of confusion. The relationship is a little easier to understand, and keep straight, if we think of the latter as "character set encodings."</p>

<p>It's back to the W3C's "Character Encodings: Essential Concepts" for a <a title="Encoding definition" href="https://www.w3.org/International/articles/definitions-characters/#charsets">definition of encoding</a> to get us started:</p>

<blockquote>The character encoding reflects the way the coded character set is mapped to bytes for manipulation by a computing device.</blockquote>

<p>In the table below, which reproduces the same information from a graphic appearing in the W3C document, the first 4 characters and corresponding code points are part of the Tifinagh alphabet, and the fifth is the more familiar exclamation point.</p>

<p><strong>Aside</strong>: The exclamation point is only more familiar for those of us who use the Latin alphabet or one of the <a title="Wikipedia link 2016-0611 13:51 UTC" href="https://en.wikipedia.org/wiki/Exclamation_mark#Languages">other languages that have adopted it</a>, including Russian, Chinese, Korean and Japanese, among others.The Tifinagh alphabet is associated with Berber script and languages and dialects used by people indigenous to North Africa. It's worth considering that the exclamation point might look as foreign to them as the Tifinagh letter yaz (ⵣ) looks to us.</p>

<table class="article-table three-columns"><caption>Table 1: A representation of the same information from a graphic that appears in the W3C document "<a href="https://www.w3.org/International/articles/definitions-characters/#charsets">Character Encodings: Essential Concepts</a>"</caption>
<tbody>
<tr>
<th>Character (glyph)</th>
<th>Hexadecimal representation of Unicode code point</th>
<th>UTF-8 encoding (bytes in memory)</th>
</tr>
<tr>
<td>ⴰ</td>
<td>2D30</td>
<td>E2 B4 BO</td>
</tr>
<tr>
<td>ⵣ</td>
<td>2D63</td>
<td>E2 B5 A3</td>
</tr>
<tr>
<td>ⵓ</td>
<td>2D53</td>
<td>E2 B5 93</td>
</tr>
<tr>
<td>ⵍ</td>
<td>2D4D</td>
<td>E2 B5 8D</td>
</tr>
<tr>
<td>!</td>
<td>21</td>
<td>21</td>
</tr>
</tbody>
</table>

<p>The table shows, from left to right, the symbol itself, the corresponding code point and the way the code point maps to a sequence of bytes using the UTF-8 encoding scheme. Each byte in memory is represented by a two-digit hexadecimal number. So, for example, in the first row we see that the UTF-8 encoding of the Tifinagh letter ya (ⴰ) requires 3 bytes of storage (E2 B4 BO).</p>

<p><strong>Important</strong>: It may be that you are not seeing the Tifinagh characters in that table at all, but rather generic placeholders. That <em>does not mean</em> the article (or the information in it) is broken. 😥 (Disappointed but relieved face emoji)</p>

<p>There is a perfectly good explanation for those placeholders. Moreover, they are not just any old generic character. They serve a purpose, and each has a meaning. If you are desperate to know more, you can jump right to the <a href="#glyphs-sec">glyphs section</a> of this article where you will find more information. But I'd recommend that you just keep reading, and we'll get there soon enough.If those characters are missing for you, and you want to know what they look like, <a title="Wikipedia link 2016-0624 17:55" href="https://en.wikipedia.org/wiki/Tifinagh">the Wikipedia entry for Tifinagh</a> includes images representing each as well as the characters themselves. That's as good a place to see them as any other.</p>

<p>There are two important points to take away from the information in this table:</p>

<p>First, <strong>encodings are distinct from the coded character sets</strong>. The coded character set is the information that is stored, and the encoding is the manner in which it is stored. (Don't worry about the specifics.)</p>

<p>Secondly, note how under the UTF-8 encoding scheme the Tifinagh code points map to three bytes, but the exclamation point maps to a single byte.</p>

<p><a href="https://www.w3.org/International/articles/definitions-characters/#charsets">From the W3C</a>:</p>

<blockquote>Although the code point for the letter à in the Unicode coded character set is always 225 (in decimal), in UTF-8 it is represented in the computer by two bytes. … there isn't a trivial, one-to-one mapping between the coded character set value and the encoded value for this character. … the letter à can be represented by two bytes in one encoding and four bytes in another.</blockquote>

<p>The encoding forms that can be used with Unicode are called UTF-8, UTF-16, and UTF-32.</blockquote>

<p>The W3C's explanation is accurate, concise, informative and, for many readers, clear as mud. At this point, we're dealing with pretty low-level stuff. Let's keep pushing ahead; as is often the case, learning more will give us the context we need to better understand what we've already seen.</p>

<p>UTF is a set of encodings specifically created for the implementation of Unicode. It is part of the core specification of Unicode itself.</p>

<p>The Unicode Consortium maintains an <a href="https://www.unicode.org/versions/Unicode9.0.0/">official website for Unicode 9.0</a> (as well as all previous versions of the specification). A PDF of the <a title="Unicode Version 9.0 Core Spec — PDF" href="https://www.unicode.org/versions/Unicode9.0.0/UnicodeStandard-9.0.pdf">core specification</a> was just recently published to the website in August 2016. You'll find the discussion of UTF in "Section 2.5: Encoding Forms."</p>

<blockquote>Computers handle numbers not simply as abstract mathematical objects, but as combinations of fixed-size units like bytes and 32-bit words. A character encoding model must take this fact into account when determining how to associate numbers with the characters.</blockquote>

<p>Actual implementations in computer systems represent integers in specific code units of particular size—usually 8-bit (= byte), 16-bit, or 32-bit. In the Unicode character encoding model, precisely defined encoding forms specify how each integer (code point) for a Unicode character is to be expressed as a sequence of one or more code units. The Unicode Standard provides three distinct encoding forms for Unicode characters, using 8-bit, 16-bit, and 32-bit units. These are named UTF-8, UTF-16, and UTF-32, respectively. The "UTF" is a carryover from earlier terminology meaning Unicode (or UCS) Transformation Format. Each of these three encoding forms is an equally legitimate mechanism for representing Unicode characters; each has advantages in different environments.</blockquote>

<p><strong>Note</strong>: These encoding forms are consistent from one version of the specification to the next. In fact, their stability is vital to maintaining the integrity of the Unicode standard. Whatever we read about the encoding forms in the Version 9.0 specification was true of <a title="official site for Unicode 8.0" href="https://www.unicode.org/versions/Unicode8.0.0/">Version 8.0</a> as well, and will hold going forward.</p>

<p>The Unicode specification discusses at length the pros and cons and preferred usage of these three forms — UTF-8, UTF-16 and UTF-32 — endorsing the use of all three as appropriate. For the purposes of this brief discussion of UTF encoding, it's enough to know the following:</p>

*   UTF-8 uses 1 byte to represent characters in the ASCII set, 2 bytes for characters in several more alphabetic blocks, 3 bytes for the rest of the BMP, and 4 bytes as needed for supplementary characters.
*   UTF-16 uses 2 bytes for any character in the BMP, and 4 bytes for supplementary characters.
*   UTF-32 uses 4 bytes for all characters.

<p><strong>Aside</strong>: What is the BMP? We've said that Unicode is a very large character set intended to encompass every other character set. A plane is a part of the organizational structure of Unicode consisting of a contiguous group of 65,536 (2<sup>16</sup>) code points. There are 17 such planes. Let's do a little math to fill out the picture…

<pre>    65,536 code points * 17 planes = 1,114,112 code points
</pre>

<p>So, there are theoretically 1,114,112 possible code points without extending this basic arrangement.</p>

<p><strong>Note</strong>: Although it would technically be possible to expand the code point space that uses UTF-8 encoding, because of the changes that would require and the <a title="Character encoding stability policies" href="https://unicode.org/policies/stability_policy.html">Unicode Consortium's stability policies</a>, which are intended to ensure continuity and backward-compatibility, the space will probably not be expanded within the period of time anyone is likely to be reading this article. If I'm wrong about that, let me say hello to you, future reader. 👋 (Waving Hand Sign emoji) How are things? I hope you've figured out how to clean up some of the mess we've created in the world today. (I assure you that many of us feel bad about it. 😔 (Pensive Face emoji))</p>

<p>The BMP is plane 0 (i.e. the first plane). What is the significance, if any, of the BMP? The BMP alone contains most of the characters of all modern languages. The arrangement of the BMP is nicely visualized in the chart below, taken from the <a title="Wikipedia link 2016-0609 20:45" href="https://en.wikipedia.org/wiki/Plane_(Unicode)">Wikipedia entry for Unicode planes</a>, in which the BMP is shown as a series of boxes such that each box represents 256 code points (16 rows × 16 columns × 256 code points per box = 65,536 code points).</p>

<p>Let's quickly look at where some actual characters would fit into this table. Take, for example, the Latin script letter "a". The code point for "a" is <code>U+0061</code>, which puts it in box <code>00</code>. That is to say, it is one of 256 characters represented in the chart by box <code>00</code>. The code points for these characters are in the range of <code>U+0000</code> (assigned to the NULL character) and <code>U+00FF</code> (the code point for "ÿ," the Latin lowercase letter "y" with a diaeresis). These 256 characters comprise the first two Unicode blocks, referred to as "C0 Controls and Basic Latin" (<code>U+0000</code> to <code>U+007F</code>) and "C1 Controls and Latin-1 Supplement" (<code>U+0080</code> to <code>U+00FF</code>). It is here where you will find the 52 letters of the ISO basic Latin alphabet (a to z, A to F) and the rest of the characters from the US-ASCII encoding standard. It is also home to the code points corresponding to characters from ISO 8859-1 (Latin-1), with its many accented characters for representing Western European languages (Italian, French, Spanish, German, Portuguese and Dutch, among others). For a more detailed look at these blocks, refer to the <a href="https://en.wikibooks.org/wiki/Unicode/Character_reference/0000-0FFF">Wikibooks Unicode character reference for <code>0000</code> to <code>0FFF</code></a>.</p>

<p>This is a good illustration both of what it means and of the way in which Unicode encompasses other character sets. Those other sets — disparate, overlapping, isolated from one another, and easily confused — are <strong>carried over and integrated as part of Unicode</strong>. The importance of Unicode simply cannot be overstated. (It would not be possible for me to write this article, or for you to read it, were it not for Unicode.)</p>

<p>What about the Ethiopic syllable "ቈ" (QWA)? That's code point <code>U+1248</code>, box <code>12</code>, which the chart tells us contains African scripts. You'll notice that, as you might expect, most of the space in the BMP is allocated to code points for Chinese, Japanese and Korean characters.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e06511c3-d76f-4b1b-bf97-71bc05722e2e/roadmap-to-unicode-bmp.svg-1024x683"><img title="Map of the Basic Multilingual Plane" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d68df3-c352-4087-8d34-17414e181286/roadmap-to-unicode-bmp.svg-650px-preview-opt" alt="Map of the Basic Multilingual Plane" width="650" height="434" /></a><figcaption>Figure 1: A map of Unicode's basic multilingual plane (plane 0), visualized as 256 boxes of 256 code points each and color-coded (Image: <a title="Wikipedia site" href="https://wikipedia.org">Wikipedia</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e06511c3-d76f-4b1b-bf97-71bc05722e2e/roadmap-to-unicode-bmp.svg-1024x683">Large preview</a>)</figcaption></figure>

<p>You might ask, "Are 17 planes and 1,114,112 code points a lot?"</p>

<p>Beyond the BMP, the majority of planes are entirely unassigned. Only six, including the BMP, have any assigned characters at all.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cbf3d42-7a1e-4914-82a3-8b51fab72ef8/unicode-planes-20160611-1024x799.png"><img title="Unicode planes and used code point ranges" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74839ee0-19aa-4078-86d9-5b4862fe2701/unicode-planes-20160611-500x391.png" alt="Unicode planes and used code point ranges" /></a><figcaption>Figure 2: Table (reproduced here as an image) depicting Unicode planes and code point ranges, both used and unused (Image: <a title="Wikipedia site" href="https://wikipedia.org">Wikipedia</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cbf3d42-7a1e-4914-82a3-8b51fab72ef8/unicode-planes-20160611-1024x799.png">Large preview</a>)</figcaption></figure>

<p>There are "only" 120,672 Unicode characters in <a title="Summary of changes in Unicode 8" href="https://www.unicode.org/versions/Unicode8.0.0/">Unicode Version 8</a>, released on 17 June 2015. <a title="Summary of changes in Unicode 9" href="https://www.unicode.org/versions/Unicode9.0.0/">Version 9.0</a>, the current version, which was officially released 21 June 2016, adds 7,500 additional characters, for a total of 128,172. If the Unicode Consortium adds an average of 7,500 characters a year, it would take approximately 131 years to fill the code space. That's assuming we don't run out of characters first. So, there is certainly plenty of space left… for future emoji. 😁 (Grinning Face with Smiling Eyes emoji)</p>

<p>Speaking of emoji, where do they fit in? As an example, let's look at 🐘 (Elephant emoji). The code point for the Elephant emoji is <code>U+1F418</code>. That's in the BMP, and it fits into figure 1 at box 1F, an address space generally reserved for non-Latin European scripts. The elephant was part of the original set of emoji implemented in Unicode Version 6. A more recent addition ? (Unicorn Face emoji), introduced in Version 8.0, is at <code>U+1F984</code>.</p>

<p>For those of you who have never before given much thought to Unicode, and character encodings more generally, or have been confused or intimidated by the topic, I hope you're already beginning to see that it's not so very hard to figure out.</p>

<p>From the brief description of storage requirements for the various UTF encodings above, you might guess that UTF-8 is more complicated to implement (owing to the fact that it is not fixed-width) but more space efficient than say UTF-32, which is more regular but less space-efficient, with every character taking up exactly 4 bytes.</p>

<table class="article-table six-columns"><caption>Table 1: A representation of the same information from a graphic that appears in the W3C document "<a href="https://www.w3.org/International/articles/definitions-characters/#charsets">Character Encodings: Essential Concepts</a>"</caption>
<tbody>
<tr>
<th>Encoding</th>
<td>ⴰ</td>
<td>ⵣ</td>
<td>ⵓ</td>
<td>ⵍ</td>
<td>!</td>
</tr>
<tr>
<th>UTF-8</th>
<td>E2 B4 BO</td>
<td>E2 B5 A3</td>
<td>E2 B5 93</td>
<td>E2 B5 8D</td>
<td>21</td>
</tr>
<tr>
<th>UTF-16</th>
<td>2D 30</td>
<td>2D 63</td>
<td>2D 53</td>
<td>2D 4D</td>
<td>00 21</td>
</tr>
<tr>
<th>UTF-32</th>
<td>00 00 2D 30</td>
<td>00 00 2D 63</td>
<td>00 00 2D 53</td>
<td>00 2D 4D</td>
<td>00 00 00 21</td>
</tr>
</tbody>
</table>

<p>Ignoring the Berber characters and focusing on the exclamation point in the rightmost column, we see that the same character would take up a single byte in UTF-8, 2 bytes (two times the storage) in UTF-16, and 4 bytes (four times the storage) in UTF-32. That's three very different amounts of storage to convey the exact same information. Multiply that difference in storage requirements by the size of the web, <a title="Estimate based on pages indexed by major search engines" href="https://www.worldwidewebsize.com/">estimated to be at least 4.83 billion pages</a> currently, and it's easy to appreciate that the storage requirements of these encodings is not an inconsequential consideration.</p>

<p>Whether or not that all made sense to you, here's the good news…</p>

<p>When dealing with HTML, the character set we'll use is Unicode, and the <strong>character encoding is always UTF-8</strong>. It turns out that that's all we'll ever need to concern ourselves with. 😌 (Relieved Face emoji, <code>U+1F60C</code>)</p>

<p>Regardless, it's no less important to be aware of the general concepts, as well as the simple fact that there are other character sets and encodings.</p>

<p>Now, we can bring all of this to the context of the web, and start working our way toward emoji.</p>

<pre><code class="language-html">                                      ⛅
🎈
    🌲                    🏡   🏃      🌲🌲         🌲</code></pre>

## Declaring Character Sets And Document Encoding On the Web

<p>We need to tell user agents (web browsers, screen readers, etc.) how to correctly interpret our HTML documents. In order to do that, we need to specify both the character set and the encoding. There are two (overlapping) ways to go about this:</p>

*   utilizing HTTP headers,
*   declaring within the HTML document itself.

<p>A brief aside about HTML5, WHATWG and W3C: This is hardly an article about HTML5, much less the sort of in-depth treatment of HTML5 that would warrant a discussion of its history and the complicated technical and political issues surrounding this critically important standard. Regardless, not only do I mention HTML5 and show fragments of markup, but I refer to the HTML5 specification (more than once), and that probably crosses the line, requiring me to say at least a little something about what has become a thorny issue.It is not my intention to add anything new to this discussion. (I wouldn't be one to do that, by any stretch.) I've said before and will say again that I believe the distributed web is the single best piece of evidence that we can do good on a global scale. So, I genuinely care about this stuff. I want to get it right, and I also want to be respectful of the hard work, dedication and passion of all parties involved.</p>

<p>First, there are two HTML5 specifications, one the work of the WHAT
 and the other maintained by the W3C. The WHATWG's own FAQ says as much:</p>

<blockquote>Which group has authority in the event of a dispute?</blockquote>

<p>The two groups have different specs, so each has authority over its spec. The specs can and have diverged on some topics; unfortunately, these differences are not documented anywhere.</blockquote>

<p>Setting aside for a brief moment the issue of what it means in practice to have two divergent specifications ostensibly describing the same standard, not an insignificant issue, the situation seems clear enough. There are two separate specifications, and two different organizations, each authoritative over its own work. The situation is much less straightforward than that would make it seem. However, the complications are what allow us to make some sense of the notion that there are two specifications for one standard. Before we get to the current state of affairs, we need a brief history lesson.</p>

<p>Rather than retell the history myself (badly), I'll let the WHATWG and W3C do it. The current versions of both specifications include a history section that very nearly match. The WHATWG spec is published as a continually updated "<a title="History section of WHATWG HTML spec" href="https://html.spec.whatwg.org/multipage/introduction.html#history-2">Living Standard</a>." The W3C spec, on the other hand, follows a rigorous publication process, moving through distinct phases: candidate recommendation (CR), proposed recommendation (PR) and W3C recommendation (REC). Most recently, the "<a title="History section of the W3C 5.1 CR" href="https://www.w3.org/TR/2016/CR-html51-20160621/introduction.html#introduction-history">HTML 5.1: W3C Proposed Recommendation</a>" was published on 15 September 2016.</p>

<p>It is these 2 specs, the <a title="History section of WHATWG HTML spec" href="https://html.spec.whatwg.org/multipage/introduction.html#history-2">WHATWG's "Living Standard" for HTML</a> and the <a title="History section of the W3C 5.1 CR" href="https://www.w3.org/TR/2016/CR-html51-20160621/introduction.html#introduction-history">W3C's HTML 5.1 candidate Recommendation,</a> that I'll be referring to here.</p>

<p>It would be excessive to copy and paste the entire history section of both specifications. So, please go ahead and read about the history from the source for yourself by following one of the links above. They are very nearly identical. In fact, let's look at the passages that differ the most between the two:</p>

<p>From WHATWG's version of the spec:</p>

<blockquote>For a number of years, both groups then worked together. In 2011, however, the groups came to the conclusion that they had different goals: the W3C wanted to publish a "finished" version of "HTML5", while the WHATWG wanted to continue working on a Living Standard for HTML, continuously maintaining the specification rather than freezing it in a state with known problems, and adding new features as needed to evolve the platform.</blockquote>

<p>Since then, the WHATWG has been working on this specification (amongst others), and the W3C has been copying fixes made by the WHATWG into their fork of the document (which also has other changes).</blockquote>

<p>Here is the corresponding passage from the W3C's HTML 5.1 candidate recommendation:</p>

<blockquote>Since then, the W3C HTML WG has been cherry picking patches from the WHATWG that resolved bugs registered on the W3C HTML specification or more accurately represented implemented reality in user agents. At time of publication of this document, patches from the WHATWG HTML specification have been merged until January 12, 2016. The W3C HTML editors have also added patches that resulted from discussions and decisions made by the W3C HTML WG as well a bug fixes from bugs not shared by the WHATWG.</blockquote>

<p>That gives us a very quick summary. After a period of officially working together, these two standards bodies have parted ways. However, there is still an awkward collaboration of sorts on the HTML5 standard itself. The WHATWG works on its specification, rolling in changes continually. Much like a modern evergreen operating system (OS) or application with an update feature, the latest changes are incorporated without waiting for the next official release. This is what the WHATWG means by "living standards," which it describes as follows:</p>

<blockquote>This means that they are standards that are continuously updated as they receive feedback, either from Web designers, browser vendors, tool vendors, or indeed any other interested party. It also means that new features get added to them over time, at a rate intended to keep the specifications a little ahead of the implementations but not so far ahead that the implementations give up.</blockquote>

<p>Despite the continuous maintenance, or maybe we should say as part of the continuing maintenance, a significant effort is placed on getting the specifications and the implementations to converge — the parts of the specification that are mature and stable are not changed willy nilly. Maintenance means that the days where the specifications are brought down from the mountain and remain forever locked, even if it turns out that all the browsers do something else, or even if it turns out that the specification left some detail out and the browsers all disagree on how to implement it, are gone. Instead, we now make sure to update the specifications to be detailed enough that all the implementations (not just browsers, of course) can do the same thing. Instead of ignoring what the browsers do, we fix the spec to match what the browsers do. Instead of leaving the specification ambiguous, we fix the the [sic] specification to define how things work.</blockquote>

<p>For its part, the W3C will from time to time package these updates (at least some of them), as well as its own changes possibly, to arrive at a new version of its HTML 5.x standard.</p>

<p>Assuming that the WHATWG process works as advertised — and that may be a pretty good assumption considering that many of the people directly involved with the WHATWG also work for the organizations responsible for the implementation of the standard (e.g. Apple, Google, Mozilla and Opera) — the best strategy is probably to refer to the WHATWG spec first. That is what I have done in this article. Where I quote from an HTML5 spec, I am referencing the WHATWG specification. I do, however, make use of informational documents from the W3C throughout the article because they are helpful and not inconsistent with either spec.</p>

<p>Honestly, for our purposes here, it hardly matters. The sections I pull from are nearly (though not strictly) identical. But I suppose that's really part of the problem, rather than evidence of cohesiveness. To get a sense of just how messy the situation is, take a look at the <a href="https://wiki.whatwg.org/wiki/Fork_tracking">"Fork Tracking" page on the WHATWG's wiki</a>.</p>

{{% ad-panel-leaderboard %}}

### `content-type` HTTP Header Declaration

<p>As long as we're talking about the web, there's good reason to believe that the <a title="HTTP header info" href="https://www.w3.org/International/articles/definitions-characters/#httpheader">W3C has something to say</a> about the topic:</p>

<blockquote>When you retrieve a document, a web server sends some additional information. This is called the HTTP header. Here is an example of the kind of information about the document that is passed as part of the header with a document as it travels from the server to the client.</blockquote>

<pre><code class="language-html"> HTTP/1.1 200 OK
Date: Wed, 05 Nov 2003 10:46:04 GMT
Server: Apache/1.3.28 (Unix) PHP/4.2.3
Content-Location: CSS2-REC.en.html
Vary: negotiate,accept-language,accept-charset
TCN: choice
P3P: policyref=https://www.w3.org/2001/05/P3P/p3p.xml
Cache-Control: max-age=21600
Expires: Wed, 05 Nov 2003 16:46:04 GMT
Last-Modified: Tue, 12 May 1998 22:18:49 GMT
ETag: "3558cac9;36f99e2b"
Accept-Ranges: bytes
Content-Length: 10734
Connection: close
Content-Type: text/html; charset=UTF-8
Content-Language: en</code></pre>

<blockquote>If your document is dynamically created using scripting, you may be able to explicitly add this information to the HTTP header. If you are serving static files, the server may associate this information with the files. The method of setting up a server to pass character encoding information in this way will vary from server to server. You should check with the documentation or your server administrator.</blockquote>

<p>Without getting too heavily into the details, while still coming away from the discussion with some sense of how this works, let's clarify some of the terminology.</p>

<p>HTTP is the network application protocol underlying communication on the web. (The same protocol is also used in other contexts, but was originally designed for the web.) HTTP is a client-server protocol and facilitates communication between the software making a request (the client) and the software fulfilling or responding to the request (the server) by exchanging request and response messages. These messages all must follow a well-defined, standardized structure so that they can be anticipated and interpreted properly by the recipient.</p>

<p>Part of this structure is a header providing information about the message itself, about the capabilities or requirements of the originator or of the recipient of the message, and so on. The header consists of a number of individual header lines. Each line represents a single header field comprising a lone key-value pair. One of the approximately 45+ defined fields is <code>Content-Type</code>, which identifies both the encoding and character set of the content of the message.</p>

<p><strong>Note</strong>: The <a title="IETF site" href="https://www.ietf.org/">Internet Engineering Task Force</a> (IETF) is the group responsible for developing and maintaining many of the open standards that are the foundation of communication on the Internet, including HTTP. The IETF documents the HTTP standard, as well as their other work, in a series of formal specifications referred to as "<a title="RFC description and brief history" href="https://www.livinginternet.com/i/ia_rfc.htm">Request for Comments</a>" (RFCs).</p>

<p>In the example above, among the header lines, we see:</p>

<pre><code class="language-html">Content-Type: text/html; charset=UTF-8</code></pre>

<p>The field contains two pieces of information.</p>

<p>The first is the <a title="Wikipedia link 2016-0615 16:55 UTC" href="https://en.wikipedia.org/wiki/Media_type">media type</a>, <code>text/html</code>, which identifies the content of the message as an HTML document, which a web server can process directly. There are other media types, like <code>application/pdf</code> (a PDF document), which generally need to be handled differently.</p>

<p>The second piece of information is the document encoding and character set, <code>charset=UTF-8</code>. As we've already seen, UTF-8 is exclusively used with Unicode. So UTF-8 alone is enough to identify both the encoding and character set.</p>

<p>You can view these HTTP headers yourself. Options for doing so include, among others:</p>

*   Browser development tools
*   web-based tools

### Checking HTTP Headers Using A Browser's Developer Tools

<p><strong>Checking HTTP Headers with Firefox (Recent Versions)</strong></p>

<ol>
  <li>Open the "Web Console" from the "Tools" → "Web Developer" menu.</li>
<li>Select the "Network" tab in the pane that appears (at the bottom of the browser window, if you haven't changed this default).</li>
<li>Navigate to a web page you'd like to inspect. You'll see a list consisting of all resources that contribute to the page fill-in, including the root document, at the top (with component resources listed underneath).</li>
<li>Select any one of these resources from the list for which you'd like to look at the accompanying headers. (The pane should split.)</li>
<li>Select the "headers" tab in the new pane that appears.</li>
<li>You'll see response and request headers corresponding to both ends of the exchange, and among the response headers you should find the `Content-Type` field.</li></ol>

<p><strong>Checking HTTP Headers with Chrome (Recent Versions)</strong></p>

<ol>
<li>Open the "Developer Tools" from the "View" → "Developer" menu.</li>
<li>Select the "Network" tab in the pane that appears (at the bottom of the browser window, if you haven't changed this default).</li>
<li>Navigate to a web page you'd like to inspect. You'll see a list of all resources that contribute to the page fill-in, including the root document, at the top (with component resources listed underneath).</li>
<li>Select any one of these resources from the list for which you'd like to look at the accompanying headers. (The pane should split.)</li>
<li>Select the "headers" tab in the new pane that appears.</li>
<li>You'll see response and request headers corresponding to both ends of the exchange, and among the response headers you should find the `Content-Type` field.</li></ol>

### Checking HTTP Headers Using Web-Based Tools

<p>Many websites allow you to view the HTTP headers returned from the server for any public website, some much better than others. One reliable option is the W3C's own <a title="W3C validator for internationalization-friendliness" href="https://validator.w3.org/i18n-checker/">Internationalization Checker</a>.</p>

<p>Simply type a URL into the provided text-entry field, and the page will return a table with information related to the internationalization and language of the document at that address. You should see a section titled "Character Encoding," with a row for the "HTTP Content-Type" header. You're hoping to see a value of <code>utf-8</code>.</p>

### Using A Meta Element With charset Attribute

<p>We can also declare the character set and encoding in the document itself. More specifically, we can use an HTML <code>meta</code> element to specify the character set and encoding.</p>

<p>There are two different, widely used, equally valid formats (both interpreted in exactly the same way).</p>

<p>There is the older HTML 4.x format:</p>

<pre><code class="language-html">&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"&gt;
</code></pre>

<p>And the newer, equivalent, HTML5 version:</p>

<pre><code class="language-html">&lt;meta charset="UTF-8"&gt;
</code></pre>

<p>The latter form is shorter and, so, easier to type and harder to get wrong accidentally, and it takes up less space. For these reasons, it's the one we should use.</p>

<p>It might occur to you to ask (or not), "If the browser needs to know the character set and encoding before it can read the document, how can it read the document to find the meta element and get the value of the charset attribute?"</p>

<p>That's a good question. How clever of you. 🐙 (Octopus emoji, <code>U+1F419</code> — widely considered to be among the <a title="Scientific American: Are Octopuses Smart?" href="https://www.scientificamerican.com/article/are-octopuses-smart/">cleverest of all animal emoji</a>) I probably wouldn't have thought to ask that. I had to learn to ask that question. (Sometimes it's not just the answers we need to learn, but the questions as well.)</p>

<p>For the answer to this apparent riddle, I'll quote an often-cited blog post by Joel Spolsky on the topic of character sets and encoding, titled "<a title="Weblog post" href="https://www.joelonsoftware.com/articles/Unicode.html">The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets (No Excuses!)</a>":</p>

<blockquote>It would be convenient if you could put the Content-Type of the HTML file right in the HTML file itself, using some kind of special tag. Of course this drove purists crazy… how can you read the HTML file until you know what encoding it's in?! Luckily, almost every encoding in common use does the same thing with characters between 32 and 127, so you can always get this far on the HTML page without starting to use funny letters:</blockquote>

<pre><code class="language-http">
&lt;html&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"&gt;
</code></pre>

<p>But that meta tag really has to be the very first thing in the &lt;head&gt; section because as soon as the web browser sees this tag it's going to stop parsing the page and start over after reinterpreting the whole page using the encoding you specified.</blockquote>

<p>Notice the use of the older-style <code>meta</code> element. This post is from 2003 and, therefore, predates HTML5.</p>

<p>That makes sense, right? Let's also take a look at what the HTML spec has to say about it. From the WHATWG HTML5 spec on "<a title="WHATWG HTML5 Living Standard updated 1 June 2016" href="https://html.spec.whatwg.org/multipage/semantics.html#charset">Specifying the Document's Character Encoding</a>":</p>

<blockquote>The element containing the character encoding declaration must be serialized completely within the first 1024 bytes of the document.</blockquote>

<p>In order to satisfy this condition as safely as possible, it's best practice to have the <code>meta</code> element specifying the charset as the first element in the <code>head</code> section of the page.</p>

<p>This means that every HTML5 document should begin very much like the following (the only differences being the <code>title</code> text, possibly the value of the <code>lang</code> attribute, the use of white space, single versus double quotation marks around attribute values, and capitalization).</p>

<pre><code class="language-html">&lt;!doctype html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="utf-8"&gt;
  &lt;title&gt;Example title&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;&lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>Now you might be thinking, "Great, I can specify the character set and encoding in the HTML document. I'd much rather do that than worry about HTTP header field values."</p>

<p>I don't blame you. But that begs the question, "What happens if the character set and encoding are set in both places?"</p>

<p>Maybe somewhat surprisingly the <strong>information in the HTTP headers takes precedence</strong>. Yes, that's right, the meta element and <code>charset</code> attribute do not override the HTTP headers. (I think I remember being surprised by this.) 🙁 (Slightly Frowning Face emoji, <code>U+1F641</code>)</p>

<p>The W3C tells us in "<a href="https://www.w3.org/International/questions/qa-html-encoding-declarations#quickanswer">Declaring Character Encodings in HTML</a>":</p>

<blockquote>If you have access to the server settings, you should also consider whether it makes sense to use the HTTP header. Note however that, since the HTTP header has a higher precedence than the in-document meta declarations, content authors should always take into account whether the character encoding is already declared in the HTTP header. If it is, the meta element must be set to declare the same encoding.</blockquote>

<p>There's no getting away from it. To avoid problems, we should always make sure the value is properly set in the HTTP header as well as in the HTML document.</p>

### An Encoding By Any Other Name

<p>Before we finish with character sets and encoding and move on to emoji, there are two other complications to consider. The first is as subtle as it is obvious.</p>

<p>It's not enough to declare a document is encoded in UTF-8 — it must be encoded in UTF-8! To accomplish this, your editor needs to be set to encode the document as UTF-8. It should be a preference within the application.</p>

<p>Say, I have a joke for you… What time is it when you have an editor that doesn't allow you to set the encoding to UTF-8?</p>

<p>Punchline: Time to get a new editor! 🙄 (Face with rolling eyes emoji, <code>U+1F644</code>)</p>

<p>So, we've specified the character set and encoding both in the HTTP headers and in the document itself, and we've taken care that our files are encoded in UTF-8. Now, thanks to Unicode and UTF-8, we can know, without any doubt, that our documents will be interpreted and displayed properly for every visitor using any browser or other user agent on any device, running any software, anywhere in the world. But is that true? No, it's not quite true.</p>

<p>There is still a missing piece of the puzzle. We'll come back to this. Building suspense, that's good writing! 😃 (Smiling Face with Mouth Open emoji, <code>U+1F603</code>)</p>

<pre><code class="language-html">                                 ⛅
🎈
    🌲            🏃      🏡           🌲🌲         🌲</code></pre>

### So What Are Emoji?

<p>We've already mentioned the Unicode Consortium, the non-profit responsible for the Unicode standard.</p>

<p>There's a subcommittee of the Unicode Consortium dedicated to emoji, called, unsurprisingly, the <a title="Emoji Subcommittee site" href="https://unicode.org/emoji/">Unicode Emoji Subcommittee</a>. As with the rest of the Unicode standard, the Unicode Consortium and its website (<a href="https://unicode.org">unicode.org</a>) are the authoritative source for information about emoji. Fortunately for us, it provides a wealth of accessible information, as well as some more formal technical documents, which can be a little harder to follow. An example of the former is its <a href="https://unicode.org/faq/emoji_dingbats.html">"Emoji and Dingbats" FAQ</a>.</p>

<blockquote>Q: What are emoji?</blockquote>

<p>A: Emoji are "picture characters" originally associated with cellular telephone usage in Japan, but now popular worldwide. The word emoji comes from the Japanese 絵 (e ≅ picture) + 文字 (moji ≅ written character).</blockquote>

<p><strong>Note</strong>: See those Japanese characters in this primarily English-language document? Thanks Unicode!</p>

<blockquote>Emoji are often pictographs — images of things such as faces, weather, vehicles and buildings, food and drink, animals and plants — or icons that represent emotions, feelings, or activities. In cellular phone usage, many emoji characters are presented in color (sometimes as a multicolor image), and some are presented in animated form, usually as a repeating sequence of two to four images — for example, a pulsing red heart.</blockquote>

<p>Q: Do emoji characters have to look the same wherever they are used?</p>

<p>A: No, they don't have to look the same. For example, here are just some of the possible images for U+1F36D LOLLIPOP, U+1F36E CUSTARD, U+1F36F HONEY POT, and U+1F370 SHORTCAKE:</p>

<p>In other words, any pictorial representation of a lollipop, custard, honey pot or shortcake respectively, whether a line drawing, gray scale, or colored image (possibly animated) is considered an acceptable rendition for the given emoji. However, a design that is too different from other vendors' representations may cause interoperability problems: see <a title="Design Guidelines section of UTR 51" href="https://www.unicode.org/reports/tr51/index.html#Design_Guidelines">Design Guidelines</a> in <a title="Unicode Technical Report 51" href="https://www.unicode.org/reports/tr51/index.html">UTR #51</a>.</blockquote>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc572ca-7393-4478-8e9f-ae1aa77120a0/emoji-examples549x346.png"><img title="Ex representations of 4 emoji" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/745f0246-500e-47d2-80b8-f4fa7d664878/emoji-examples500x380.png" alt="Ex representations of 4 emoji" /></a><figcaption>Figure 3: Example representations of four emoji shown in four styles each. (Image: <a title="Unicode Consortium site" href="https://unicode.org">Unicode, Inc.</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc572ca-7393-4478-8e9f-ae1aa77120a0/emoji-examples549x346.png">Large preview</a>)</figcaption></figure>

<p>Read through just that one FAQ — and this article, of course ? (Grinning face with Smiling Eyes emoji, <code>U+1F601</code>) — and you'll have a better handle on emoji than most people ever will.</p>

### How Do We Use Emoji?

<p>The short answer is, the same way we use every other character. As we've already discussed, emoji are symbols associated with code points. What's special about them is just semantics — i.e. the meaning we ascribe to them, not the mechanics of them.</p>

<p>If you have a key on a keyboard mapped to a particular character, producing that character is as simple as pressing the key. However, considering that, as we've seen, more than 120,000 characters are currently in use, and the space defined by Unicode allows for more than 1.1 million of them, creating a keyboard large enough to assign a character to each key is probably not a good strategy.</p>

<p><strong>Aside</strong>: It's worth noting that there are emoji keyboards — both the software keyboards like those you'll find on touch devices such as smartphones and at least one physical keyboard as well. The "Emoji Keyboard," a product of a company named EmojiWorks, is a Bluetooth wireless keyboard for Windows, macOS and iOS that combines a standard English-language layout with special emoji keys, labels and modifiers. From EmojiWorks' website:</p>

<blockquote>TYPE OVER 120 NEW EMOJI like poo, heart, monkey, kiss, 100, unicorn ?, and skin tone modifiers faster than a touchscreen right on your keyboard keys.</blockquote>

<p>This is not an endorsement of the Emoji Keyboard, which I have never used. In fact, the description of the product hints at the limitations of the very idea. Though there are well over 1800 emoji at present, this physical keyboard allows for direct entry of only 120 of them, even while assigning multiple emoji to the same keys. 🙃 (Upside-down Face, <code>U+1F643</code>)</p>

<p>When we exhaust the reach of our keyboards, we can use a software utility to insert characters.</p>

<p>Recent versions of macOS include an "Emojis and Symbols" panel that can be accessed from anywhere in the OS (via the menu bar or the keyboard shortcut <code>Control + Command + Space</code>). Other OS' offer similar capabilities to view and click or to copy and paste emoji into text-entry fields. Applications may offer additional app-specific features for inserting emoji beyond the system-wide utilities.</p>

<p><strong>Note</strong>: The current version of Apple's desktop OS has officially been rebranded as "macOS" with version 10.12 (macOS Sierra), bringing it inline with the naming scheme of the company's other platforms: iOS, tvOS, watchOS. The previous version, 10.11 (El Capitan), was officially "OS X," which had been the name of Apple's desktop OS since version 10.8 (Mountain Lion). Earlier versions were known as "Mac OS X." Throughout this article I will use "macOS" generally as well as for references to the current version. When referring to a prior release of the OS, I will use the name appropriate to that version.</p>

<p>Lastly, we can take advantage of character references to enter emoji (and any other character we like, for that matter) on the web.</p>

### Character References

<p>Character references are commonly used as a way to include syntax characters as part of the content of an HTML document, and also can be used to input characters that are hard to type or not available otherwise.</p>

<p><strong>Note</strong>: I'm sure many of you are familiar with character references. But if you keep reading this section, it wouldn't surprise me if you learn something new.</p>

<p>HTML is a markup language, and, as such, HTML documents contain both content and the instructions describing the document together as plain text in the document itself. Typically, the vast majority of characters are part of the document's content. However, there are other "special" characters in the mix. In HTML, these form the tags corresponding to the HTML elements that define the structure and semantics of the document. Moreover, it's worth taking a moment to recognize that the syntax itself — i.e. its implementation — creates a need for additional markup-specific characters. The ampersand is a good example. The ampersand (&amp;) is special because it marks the beginning of all other character references. If the ampersand itself were not treated specially, we'd need another mechanism altogether.</p>

<p>Syntax characters are treated as special, and should never be used as part of the content of a document, because they are always interpreted specially, regardless of the author's intent. Mistakenly using these characters as content makes it difficult or impossible for a browser or other user agent to parse the document correctly, leading to all sorts of structural and display issues. But aside from their special status, markup-related characters are characters like any other, and very often we need to use them as content. If we can't type the literal characters, then we need some other way to represent them. We can use character references for this, referred to as "escaping" the character, as in getting outside of (i.e. escaping) the character's markup-specific meaning.</p>

<p>What characters need to be escaped? According to the W3C <a href="https://www.w3.org/International/questions/qa-escapes">three characters should always be escaped</a>: the less-than symbol (&lt;, <code>&amp;lt;</code>), the greater-than symbol (&gt;, <code>&amp;gt;</code>) and the ampersand (&amp;, <code>&amp;amp;</code>) — just those three.</p>

<p>Two others, the double quote (", <code>&amp;quot;</code>) and single quote (', <code>&amp;apos;</code>) are often escaped based on context; in particular, when they appear as part of the value of an attribute and the same character is used as the delimiter of the attribute value.</p>

<p><strong>Note</strong>: Even this is a bit of a fib, though it comes from a typically reliable source. To be safe, we can always escape those characters. But in fact, because of the way document parsing works, we can often get away without escaping one or more of them.</p>

<p><strong>Aside</strong>: More about context-specific characters: If you've been around web design and development for even a little while, you have probably read something much like what I've written above many times. Words like "special" are thrown around as if their inherent specialness is a property of the universe. The problem with that way of thinking is that it impedes the sort of understanding that comes from discovering where a thing is documented, and eventually figuring out how it works. Unless we get into the habit of looking for authoritative information, it's easy to be misled and contribute to the sorts of problems we're trying to avoid. In fact, this seemingly innocuous issue has been, and no doubt will continue to be, a matter of not just healthy debate but also of futile bickering within the community.Let's start with the W3C's answer. The document "<a href="https://www.w3.org/International/questions/qa-escapes">Using Character Escapes in Markup and CSS</a>" tells us:</p>

<blockquote>There are three characters that should always appear in content as escapes, so that they do not interact with the syntax of the markup. These are part of the language for all documents based on XML and for HTML.</blockquote>

<p>You may also want to represent the double-quote (") as &amp;quot; and the single quote (') as &amp;apos; — particularly in attribute text when you need to use the same type of quotes as those that surround the attribute value.</blockquote>

<p>But we can do even better than that. Rather than take at face value what we read in some W3C informational document, we can dig deeper for an authoritative answer to the question "Why must these characters be escaped?" or alternatively, "What is it about the HTML5 specification that requires these characters to be escaped?"</p>

<p>For an authoritative answer to those questions, we can consult the HTML5 spec itself and gain some insight into HTML5 parsing as prescribed by the standard, discussed in "<a href="https://html.spec.whatwg.org/multipage/syntax.html#parsing">Section 12.2: Parsing HTML Documents</a>." From <a href="https://html.spec.whatwg.org/multipage/syntax.html#overview-of-the-parsing-model">Section 12.2.1: Overview of the Parsing Model</a>:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfacb2ab-85af-4628-adf9-5d3cf59938fe/parsing-model-overview708x1084.png"><img title="Parsing model diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85ece96a-77fb-4a41-b69a-3bac1400fc1c/parsing-model-overview392x600.png" alt="Parsing model diagram" /></a><figcaption>Figure 4: Parsing model diagram (reproduced here as an image) from the HTML5 specification, section 12.2.1 (Image: <a title="WHATWG site" href="https://whatwg.org/">WHATWG</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfacb2ab-85af-4628-adf9-5d3cf59938fe/parsing-model-overview708x1084.png">Large preview</a>)</figcaption></figure>

<blockquote>The input to the HTML parsing process consists of a stream of <a href="https://html.spec.whatwg.org/multipage/infrastructure.html#unicode-code-point">Unicode</a> code points, which is passed through a <a href="https://html.spec.whatwg.org/multipage/syntax.html#tokenization">tokenization</a> stage followed by a <a href="https://html.spec.whatwg.org/multipage/syntax.html#tree-construction">tree construction</a> stage. The output is a <a href="https://html.spec.whatwg.org/multipage/dom.html#document">Document</a> object.</blockquote>

<p>The special status of these characters is dictated by the HTML5 specification and enforced by the tokenization process. According to the HTML5 spec, implementations must behave as if operating as a <a title="Wikipedia link 2016-0615 18:29 UTC" href="https://en.wikipedia.org/wiki/Finite-state_machine">state machine</a> while tokenizing an HTML document.</p>

<p>The concept of a state machine comes to us from computer science and is, generally speaking, an abstract model of computing in which a theoretical machine (the state machine) can only exist in one of a finite number of states. In each state, the machine performs one of some number of actions in response to an event or trigger (e.g. transitioning into the state, receiving input, etc.), and then possibly transitions into a new state, where it will behave differently, according to the rules associated with that new state (the rules of the original state no longer being applicable).</p>

<p><em>Tokenization</em> is a process whereby a continuous stream of text is broken up into a collection of "tokens," which are meaningful words or word phrases, for further processing. This is very much like the way we, as natural-language parsers, break up the stream of characters in an article like this one into meaningful chunks — words, phrases, sentences and so on.</p>

<p>It is this state machine behavior and the tokenization process that explains why we must escape syntax characters, and when we don't need to. Encountering a "special" character causes the parser to change states.</p>

<p>From "<a href="https://html.spec.whatwg.org/multipage/syntax.html#tokenization">Section 12.2.4 Tokenization</a>":</p>

<blockquote>Implementations must act as if they used the following state machine to tokenize HTML. The state machine must start in the <a href="https://html.spec.whatwg.org/multipage/syntax.html#data-state">data state</a>. Most states consume a single character, which may have various side-effects, and either switches the state machine to a new state to <a href="https://html.spec.whatwg.org/multipage/syntax.html#reconsume">reconsume</a> the <a href="https://html.spec.whatwg.org/multipage/syntax.html#current-input-character">current input character</a>, or switches it to a new state to consume the <a href="https://html.spec.whatwg.org/multipage/syntax.html#next-input-character">next character</a>, or stays in the same state to consume the next character. Some states have more complicated behaviour and can consume several characters before switching to another state. In some cases, the tokenizer state is also changed by the tree construction stage.</blockquote>

<p>When a state says to reconsume a matched character in a specified state, that means to switch to that state, but when it attempts to consume the <a href="https://html.spec.whatwg.org/multipage/syntax.html#next-input-character">next input character</a>, provide it with the <a href="https://html.spec.whatwg.org/multipage/syntax.html#current-input-character">current input character</a> instead.</p>

<p>The exact behavior of certain states depends on the <a href="https://html.spec.whatwg.org/multipage/syntax.html#insertion-mode">insertion mode</a> and the <a href="https://html.spec.whatwg.org/multipage/syntax.html#stack-of-open-elements">stack of open elements</a>. Certain states also use a temporary buffer to track progress, and the <a href="https://html.spec.whatwg.org/multipage/syntax.html#character-reference-state">character reference state</a> uses a return state to return to the state it was invoked from.</p>

<p>The output of the tokenization step is a series of zero or more of the following tokens: DOCTYPE, start tag, end tag, comment, character, end-of-file. …</blockquote>

<p><strong>Note</strong>: I said that we can sometimes get away without escaping markup-related characters — the greater-than character (<code>&gt;</code>), for example. The description above of the HTML5 tokenization process hints at why that is. In order for the <code>&gt;</code> to be interpreted as special, the tokenizer must have previously seen a less-than symbol (<code>&lt;</code>) to go through the transitions necessary to put it in a state where <code>&gt;</code> is recognized as "special." A standalone greater-than symbol will not itself initiate that sequence of steps.</p>

<p>If you're interested in a more detailed run-through of just how complicated and fiddly the exceptions to the syntax-character rules can get in practice, have a look at the blog post "<a href="https://mathiasbynens.be/notes/ambiguous-ampersands">Ambiguous Ampersands</a>," in which Mathias Bynens considers precisely when these characters must be escaped and when they don't need be in practice.</p>

<p>But here's the thing: These types of liberties can, and frequently do, cascade through our markup when we inevitably make other mistakes. For that reason alone, you may want to stick to the advice from the W3C. Not only is it the safer approach, it's a lot easier to remember, and that's not a bad thing.</p>

<p>If you're still not convinced about the benefits of preferring overly conservative general rules in the name of consistency, and about sparing yourself from the technical details of arcane exceptions, then take a look at "<a href="https://html.spec.whatwg.org/multipage/syntax.html#optional-tags">Section 12.1.2.4 Optional Tags</a>," where it is explained exactly when and under what circumstances "certain tags can be omitted."In this section, we learn that many of the tags we are accustomed to thinking of as mandatory are, in fact, optional. It is not that the elements aren't required. On the contrary, the elements are absolutely required, and because they are required, the associated tags are implied if left out and, so, optional. Though leaving these tags out will not affect the validity of the HTML document, it may or may not affect the DOM  , depending on the precise structure of the raw markup. See how simple? ? 😖 (Confounded Face, <code>U+1F616</code>)</p>

<p>We have this example <a title="12.1.2.4 Optional tags" href="https://html.spec.whatwg.org/multipage/syntax.html#optional-tags">from the spec</a>:</p>

<pre><code>&lt;!DOCTYPE HTML&gt;
&lt;title&gt;Hello&lt;/title&gt;
&lt;p&gt;Welcome to this example.
</code></pre>

<p>This would be equivalent to this document, with the omitted tags shown in their parser-implied positions; the only white-space text node that results from this is the new line at the end of the <code>head</code> element:</p>

<pre><code>&lt;!DOCTYPE HTML&gt;
&lt;html&gt;&lt;head&gt;&lt;title&gt;Hello&lt;/title&gt;
&lt;/head&gt;&lt;body&gt;&lt;p&gt;Welcome to this example.&lt;/p&gt;&lt;/body&gt;&lt;/html&gt;
</code></pre>

<p>Even if this does not come as a surprise to you, I wouldn't bet on the likelihood of getting this exactly right every time, and then keeping track of these optional tags throughout your documents. The whole thing strikes me as being counterproductive. A standards-compliant browser or other user agent will get it right every time, unless we get it wrong first. Its knowledge of the specs may be programmed in, and its recognition nearly instantaneous and flawless. Ours isn't. It's probably better to err on the side of the simplicity that comes with fewer, more generalizable rules and patterns.</p>

<p>In addition to these few syntax characters, there are similar references for every other Unicode character as well, all 120,000+ of them. These references come in two types:</p>

<p>*   named character references (named entities)
*   numeric character references (NCRs)</p>

<p><strong>Note</strong>: It is perfectly confusing that the term "numeric character reference" is abbreviated NCR, which could just as easily be used as the abbreviation for <strong>n</strong>amed <strong>c</strong>haracter <strong>r</strong>eference. 😩 (Weary Face, <code>U+1F629</code>)</p>

<p><strong>Named character references</strong></p>

<p><em>Named character references</em> (also known as named entities, entity references or character entity references) are pre-defined word-like references to code points. There are quite a few of them. The WHATWG provides a handy <a title="Named character references" href="https://html.spec.whatwg.org/multipage/syntax.html#named-character-references">comprehensive table of character reference names supported by HTML5</a>, listing 2,231 of them. That's far, far more than you will ever likely see used in practice. After all, the idea is that these names will serve as mnemonics (memory aids). But it's difficult to remember 2,231 of anything. If you don't know that a named reference exists, you won't use it.</p>

<p>But where does this information come from? How can we be certain that the information in the table referenced above, which I describe as "comprehensive," is in fact comprehensive? Not only are those perfectly valid questions, it's exactly the type of questioning we need more of, to cut through the clutter of hearsay and other misinformation that is all too common online.</p>

<p>The very best sources of authoritative information are the specifications themselves, and that "handy, comprehensive table" is in fact is a link to <a title="Named character references" href="https://html.spec.whatwg.org/multipage/syntax.html#named-character-references">section 12.5 of the WHATWG's HTML5 spec</a>.</p>

<p>You may have heard the number 252, as in, "There are 252 named entities." This comes from HTML 4.x and, more specifically, the HTML 4.x <a title="Wikipedia link 2016-0604 17:27 UTC" href="https://en.wikipedia.org/wiki/Document_type_definition">document type definitions</a> (DTDs).From the Wikipedia article "<a title="Wikipedia link 2016-0604 17:29 UTC" href="https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references">List of XML and HTML Character Entity References</a>":</p>

<blockquote>The HTML 4 DTDs define 252 named entities, references to which act as mnemonic aliases for certain Unicode characters.</blockquote>

<p>You'll find the list of those named entities in the Wikipedia article, although, because we're dealing with HTML5, which does not use the HTML 4.x DTDs, that's probably unimportant at best, and misleading at worst.</p>

<p>Let's say you wanted to include a greater-than symbol (<code>&gt;</code>) in the content of your document.</p>

<p>As we have just seen, and as you probably already knew, we can't just press the key bearing that symbol on your keyboard. That literal character is special and may be treated as markup, not content. There is a named character reference for the greater-than symbol. It looks like <code>&amp;gt;</code>. Typing that in your document will get you the character you're looking for every time, <code>&gt;</code>.</p>

<p>But if <code>&amp;gt;</code> is treated as an entity, how would one (how did I) type that entity reference without having it be replaced by the corresponding character? Well, we use an entity reference for the leading ampersand (a reserved character). So, to have the entity reference appear on the page, rather than the greater-than symbol itself, you would type <code>&amp;amp;</code> followed by <code>gt;</code>. (By the way, to get this <code>&amp;amp;</code>, I had to type <code>&amp;amp;amp;</code>.) Situations like this are the reason why we have so many facial expression emoji. 😓 (Face with Cold Sweat <code>U+1F613</code>)</p>

<p>So, in summary, <strong>named entities are predefined mnemonics for certain Unicode characters</strong>.</p>

<p>Essentially, a group of people thought it would be nice if we could refer to <code>&amp;</code> as <code>&amp;amp;</code>, so they arranged to make that possible, and now <code>&amp;amp;</code> corresponds to the code point for <code>&amp;</code>.</p>

<p><strong>Numeric Character References</strong></p>

<p>There isn't a named reference for every Unicode character. We just saw that there are 2,231 of them. That's a lot, but certainly not all. You won't find any emoji in that list, for one thing. But while there are not always named references, there are always numeric character references. We can use these for any Unicode character, both those that have named references and those that don't.</p>

<p>An NCR is a reference that uses the code point value in decimal or hexadecimal form. Unlike the names, there is nothing easy to remember about these.</p>

<p>We've looked at the ampersand (<code>&amp;</code>), for which there is a named character reference, <code>&amp;amp;</code>. We can also write this as a numeric reference in decimal or hexadecimal form:</p>

<p>*   decimal: `&` (`&#38;`)
*   hexadecimal: `&` (`&#x00026;`)</p>

<p><strong>Note</strong>: The <code>#</code> indicates that what follows is a numeric reference, and <code>#x</code> indicates that the numeric reference is in hexadecimal notation.</p>

<p>You'll find a table containing a complete list of emoji in the document "<a title="Up-to-date table of emoji" href="https://unicode.org/emoji/charts/full-emoji-list.html">Full Emoji Data</a>," maintained by the Unicode Consortium's Emoji Subcommittee. It includes several different representations of each emoji for comparison and, importantly, the Unicode code point in hexadecimal form, as well as the name of the character and some additional information. It's a great resource and makes unnecessary any number of other websites that often contain incomplete, out of date or otherwise partially inaccurate information.</p>

<p><strong>Note</strong>: If you look carefully, you might spot some unfamiliar emoji in this list. As I write this, the list includes new emoji from the just recently released Unicode Version 9.0. So, you can find 🤠 Face with Cowboy Hat (<code>U+1F920</code>), 🤷 Shrug (<code>U+1F937</code>), 🤞 Selfie (<code>U+1F91E</code>), 🥔 Potato (<code>U+1F954</code>) and 68 others from the <a title="Emoji Recently Added" href="https://www.unicode.org/emoji/charts/emoji-released.html">newest version of Unicode</a>.</p>

<p>To look at just a few:</p>

<ul>
  <li>💩 (<code>💩</code>): Pile of Poo</li>
  <li>🍩 (<code>🍩</code>): Doughnut (that's one delicious-looking emoji)</li>
  <li>🤸 (<code>🤸</code>): Person Doing a Cartwheel (new with version 9)</li>
</ul>

<p>Are you seeing a box or other generic symbol, rather than an image for the last emoji in the list (and the preceding paragraph as well)? That makes perfect sense, if you're reading this around the time I wrote it. In fact, it would be more remarkable if you were seeing emoji there. That last emoji, Person Doing a Cartwheel (<code>U+1F938</code>), is new as of <a title="Unicode 9 release summary" href="https://unicode.org/versions/Unicode9.0.0/">Unicode Version 9.0</a>, released on 21 June 2016. It isn't surprising at all if your platform or application doesn't yet support an emoji released within the past several days (or weeks). Of course, as this newest release of Unicode begins to roll out, <a title="Blog post discussing new Version 9 emoji" href="https://blog.unicode.org/2016/06/72-new-emoji-characters.html">Version 9.0's 72 new emoji</a> will begin to appear, including ? (Person Doing a Cartwheel, <code>U+1F938</code>), the symbol for which will automatically replace the blank here and in the list above.</p>

<p>Do we really have to type in these references? No, if the platform or application you're using allows you to enter emoji in some other way, that will work just fine. In fact, it's preferred. Emoji are not syntax characters and so can always be entered directly.</p>

<p>Here's a basketball emoji I inserted into this document from OS X's "Emojis and Symbols" panel: 🏀 (Basketball, <code>U+1F3C0</code>).</p>

<p>If I pause for a moment to think, it's pretty cool that these emoji show up as images in plain-text editors. Of course, it makes perfect sense, emoji are characters every bit as much as the Latin alphabet letter "a." On the other hand, there's an image in my plain-text document!</p>

<p>This brings up a more general question, "If there's a reference for every Unicode character, when should we use them?"</p>

<p>The W3C provides us with a perfectly reasonable, well-justified answer to this question in a Q&amp;A document titled "<a href="https://www.w3.org/International/questions/qa-escapes">Using Character Escapes in Markup and CSS</a>". The short version of its answer to the question of when should we use character references is, as little as possible:</p>

<blockquote>When not to use escapes

It is almost always preferable to use an encoding that allows you to represent characters in their normal form, rather than using character entity references or NCRs.

Using escapes can make it difficult to read and maintain source code, and can also significantly increase file size.

Many English-speaking developers have the expectation that other languages only make occasional use of non-ASCII characters, but this is wrong.

Take for example the following passage in Czech.

Jako efektivnější se nám jeví pořádání tzv. Road Show prostřednictvím našich autorizovaných dealerů v Čechách a na Moravě, které proběhnou v průběhu září a října.

If you were to require NCRs for all non-ASCII characters, the passage would become unreadable, difficult to maintain and much longer. It would, of course, be much worse for a language that didn't use Latin characters at all.

Jako efektivn&amp;#x115;j&amp;#x161;&amp;#xED; se n&amp;#xE1;m jev&amp;#xED; po&amp;#x159;&amp;#xE1;d&amp;#xE1;n&amp;#xED; tzv. Road Show prost&amp;#x159;ednictv&amp;#xED;m na&amp;#x161;ich autorizovan&amp;#xFD;ch dealer&amp;#x16F; v &amp;#x10C;ech&amp;#xE1;ch a na Morav&amp;#x11B;, kter&amp;#xE9; prob&amp;#x11B;hnou v pr&amp;#x16F;b&amp;#x11B;hu z&amp;#xE1;&amp;#x159;&amp;#xED; a &amp;#x159;&amp;#xED;jna.

As we said before, use characters rather than escapes for ordinary text.</blockquote>

<p>So, we should only use character references when we absolutely must, such as when escaping markup-specific characters, but not for "ordinary text" (including emoji). Still, it is nice to know that we can always use a numeric character reference to input any Unicode character at all into our HTML documents. Literally, a world 🌎 (Earth Globe Americas, <code>U+1F30E</code>) of characters are open to us.</p>

<p>The final point I will make before moving on has to do with case-sensitivity. This is another one of those issues about which there is much confusion and debate, despite the fact that it is not open to interpretation.</p>

<p><strong>Character References and Case-Sensitivity</strong></p>

<p>Named character references are case-sensitive and must match the case of the names given in the <a title="Named character references" href="https://html.spec.whatwg.org/multipage/syntax.html#named-character-references">table of named character references supported by HTML</a> that is part of the HTML5 spec. Having said that, if you look at the named references in that table carefully, you will see more than one name that maps to the same code point (and, so, the same character).</p>

<p>Take the ampersand. You'll find the following four entries in the table for this single character:</p>

<pre><code>AMP;</code> — <code>U+00026</code> (&amp;)
<code>AMP</code> — <code>U+00026</code> (&amp;)
<code>amp;</code> — <code>U+00026</code> (&amp;)
<code>amp</code> — <code>U+00026</code> (&amp;)
</pre>

<p>This may be where some of the confusion originates. One could easily be fooled into assuming that this simulated, limited case-insensitivity is the real thing. But it would be a mistake to think that these kinds of variations are consistent. They definitely are not. For example, the one and only one valid named reference for the backslash character is <code>Backslash;</code>.</p>

<pre><code>Backslash;</code> — <code>U+02216</code> (∖)
</pre>

<p>You won't find any other references to <code>U+02216</code> in that table, and so no other form is valid.</p>

<p>If we look closely at the four named entities for the ampersand (<code>U+00026</code>) again, you'll see that half of them include a trailing semicolon (<code>;</code>) and the other half don't. This, too, may have led to confusion, with some people mistakenly believing that the semicolon is optional. It isn't. There are some explicitly defined named character references, such as <code>AMP</code> and <code>amp</code>, without it, but the vast majority of named references and all numeric references include a semicolon. Furthermore, none of the named references without the trailing semicolon can be used in HTML5. 😮 (Face with Mouth Open, <code>U+1F62E</code>) <a href="https://html.spec.whatwg.org/multipage/syntax.html#character-references">Section 12.1.4 of the HTML5 specification</a> tells us (emphasis added):</p>

<blockquote>Character references must start with a U+0026 AMPERSAND character (&amp;). Following this, there are three possible kinds of character references:</blockquote>

Named character references

<strong>The ampersand must be followed by one of the names given in the <a href="https://html.spec.whatwg.org/multipage/syntax.html#named-character-references">named character references</a> section, using the same case. The name must be one that is terminated by a U+003B SEMICOLON character (;).</strong>

Decimal numeric character reference

The ampersand must be followed by a U+0023 NUMBER SIGN character (#), followed by one or more <a href="https://html.spec.whatwg.org/multipage/infrastructure.html#ascii-digits">ASCII digits</a>, representing a base-ten integer that corresponds to a Unicode code point that is allowed according to the definition below. The digits must then be followed by a U+003B SEMICOLON character (;).

Hexadecimal numeric character reference

The ampersand must be followed by a U+0023 NUMBER SIGN character (#), which must be followed by either a U+0078 LATIN SMALL LETTER X character (x) or a U+0058 LATIN CAPITAL LETTER X character (X), which must then be followed by one or more <a href="https://html.spec.whatwg.org/multipage/infrastructure.html#ascii-hex-digits">ASCII hex digits</a>, representing a hexadecimal integer that corresponds to a Unicode code point that is allowed according to the definition below. The digits must then be followed by a U+003B SEMICOLON character (;).</blockquote>

<p>"The ampersand must be followed by one of the names given in the named character references section, <strong>using the same case</strong>. The name <strong>must be one that is terminated by a U+003B SEMICOLON character (;)</strong>."</p>

<p>That answers that.</p>

<p>By the way, the alpha characters in hexadecimal numeric character references (a to f, A to F) are always case-insensitive.</p>

<pre><code class="language-html">                            ⛅
🎈
    🌲     🏃             🏡           🌲🌲         🌲</code></pre>

### Glyphs

<p>At the end of the encoding section, I asked whether Unicode and UTF-8 encoding are enough to ensure that our documents, interfaces and all of the characters in them will display properly for all visitors to our websites and all users of our applications. The answer was no. But if you remember, I left this as a cliffhanger. 😯 (Hushed Face, U+1F62F) There's just one thing left to complete our picture of emoji (pun intended) 😬 (Grimacing Face U+1F62C).</p>

<p>Unicode and UTF-8 do most of the heavy lifting, but something is missing. We need a glyph associated with every character in order to be able to see a representation of the character.</p>

<p>From the <a title="Wikipedia link 2016-0606 18:23 UTC" href="https://en.wikipedia.org/wiki/Glyph">Wikipedia entry for glyph</a>:</p>

<blockquote>In typography, a glyph /'ɡlɪf/ is an elemental symbol within an agreed set of symbols, intended to represent a readable character for the purposes of writing and thereby expressing thoughts, ideas and concepts. As such, glyphs are considered to be unique marks that collectively add up to the spelling of a word, or otherwise contribute to a specific meaning of what is written, with that meaning dependent on cultural and social usage.

For example, in most languages written in any variety of the Latin alphabet the dot on a lower-case i is not a glyph because it does not convey any distinction, and an i in which the dot has been accidentally omitted is still likely to be recognized correctly. In Turkish, however, it is a glyph because that language has two distinct versions of the letter i, with and without a dot.</blockquote>

<p>The relationship between the terms glyph, font and typeface is that a glyph is a component of a font that is composed of many such glyphs with a shared style, weight, slant and other characteristics. Fonts, in turn, are components of a typeface (also known as a font family), which is a collection of fonts that share common design features but each of which is distinctly different.</p>

<p>Essentially, we need a font that includes a representation for the code point of the emoji we want to display. If we don't have that symbol we'll get a blank space, an empty box or some other generic character as an indication that the symbol we're after isn't available. You've probably seen this. Now you understand why, if you didn't before.</p>

<p>Going back to the figure from the W3C's "<a href="https://www.w3.org/International/articles/definitions-characters">Character Encodings: Essential Concepts</a>," the original diagram featured the following five characters:</p>

<table class="article-table six-columns break-out"><caption>Table 3: A representation of the information from a graphic that appears in the W3C document "<a href="https://www.w3.org/International/articles/definitions-characters/#charsets">Character Encodings: Essential Concepts</a>"</caption>
<tbody>
<tr>
<th>Character</th>
<td>ⴰ</td>
<td>ⵣ</td>
<td>ⵓ</td>
<td>ⵍ</td>
<td>!</td>
</tr>
<tr>
<th>Name</th>
<td>Tifinagh Letter Ya</td>
<td>Tifinagh Letter Yaz</td>
<td>Tifinagh Letter Yu</td>
<td>Tifinagh Letter Yal</td>
<td>Exclamation Point</td>
</tr>
<tr>
<th>Code point</th>
<td><code>U+2D30</code></td>
<td><code>U+2D63</code></td>
<td><code>U+2D53</code></td>
<td><code>U+2D4D</code></td>
<td><code>U+0021</code></td>
</tr>
<tr>
<th>NCR</th>
<td><code>&amp;#x2d30;</code></td>
<td><code>&amp;#x2d63;</code></td>
<td><code>&amp;#x2d53;</code></td>
<td><code>&amp;#x2d4d;</code></td>
<td><code>&amp;#x0021;</code></td>
</tr>
</tbody>
</table>

<p>What would happen if you tried to insert those characters into a web page using a numeric character reference? Let's see:</p>

<p>*   ⴰ (`&#x2d30;`)
*   ⵣ (`&#x2d63;`)
*   ⵓ (`&#x2d53;`)
*   ⵍ (`&#x2d4d;`)
*   ! (`&#x0021;`)</p>

<p>Chances are you can see the exclamation point, but some of the others might be missing, replaced by a box or other generic symbol.</p>

<p>As has already been mentioned, those symbols are Tifinagh characters. <a title="Wikipedia link 2016-0609 23:27 UTC" href="https://en.wikipedia.org/wiki/Tifinagh">Tifinagh</a> is "a series of abjad and alphabetic scripts used to write Berber languages." <a title="Wikipedia link 2016-0609 23:27 UTC" href="https://en.wikipedia.org/wiki/Berber_languages">According to Wikipedia</a>:</p>

<blockquote>Berber or the Amazigh languages or dialects (Berber name: Tamaziɣt, Tamazight, ⵜⴰⵎⴰⵣⵉⵖⵜ [tæmæˈzɪɣt], [θæmæˈzɪɣθ]) are a family of similar and closely related languages and dialects indigenous to North Africa. They are spoken by large populations in Algeria and Morocco, and by smaller populations in Libya, Tunisia, northern Mali, western and northern Niger, northern Burkina Faso, Mauritania, and in the Siwa Oasis of Egypt. Large Berber-speaking migrant communities have been living in Western Europe since the 1950s. In 2001, Berber became a constitutional national language of Algeria, and in 2011 Berber became a constitutionally official language of Morocco, after years of persecution.</blockquote>

<p>Not long ago, it would have been surprising if your platform displayed any of the Tifinagh characters. But wide internationalization support has improved dramatically and is getting better all the time, thanks in large part to Unicode. There is now a good chance you'll see them.</p>

<p><strong>More About Missing Characters: a Deep (Short) Dive</strong>Anyone paying attention closely enough has encountered missing characters on the web. We usually, well most of us at least, shrug it off as some sort of undiagnosed font or encoding issue. But dear reader, you are not "most of us". You aspire to know more. 🤓 (Nerd face, <code>U+1F913</code>)</p>

<p>As you will see shortly this is pretty low-level stuff and really beyond the scope of the article but let's discuss it briefly just to make sure there really is nothing tricky (or broken) going on.</p>

<p>Those Tifinagh characters are intentionally obscure. That's why I chose them. If, on the computer of the person viewing an HTML page, there is no font installed that includes glyphs for those characters then something else has to be displayed (or nothing at all).</p>

<p>With CSS, we're used to thinking in terms of the font-family property and lists of fonts that look something like:</p>

<pre><code class="language-html">font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;</code></pre>

<p>Notice that we're including lots of emoji in this document, and there is at least one Japanese character too, among other exotic characters, but no fonts with glyphs for those characters are included in any font-family list in any rule applied to this page. That seems odd at first, right? Maybe you've just assumed it has something to do with the the generic family typically included at the end of our font lists. We don't really bother to think about it I suppose.</p>

<p>Every modern OS has a system for handling cascading font fallbacks that is part of the lower-level system, and so typically works across all applications.</p>

<p>In theory it's similar fonts lists in CSS, just more complex.</p>

<p>For example, On the macOS and iOS platforms this is handled by <a href="https://developer.apple.com/reference/coretext">Core Text</a>, a low-level text layout and font handling engine.</p>

<p>No single font covers the entire Unicode space. When a code point is encountered for which there is no glpyh in the chosen font, a list of fallback fonts will be tried, in order to find a glyph for the code point somewhere else (i.e. in some other font).</p>

<p>This excerpt from <a href="https://developer.apple.com/library/content/documentation/StringsTextFonts/Conceptual/CoreText_Programming/Overview/Overview.html">Apple's Core Text Programming Guide</a> essentially says the same thing:</p>

<blockquote>Core Text font references provide a sophisticated, automatic font-substitution mechanism called font cascading, which picks an appropriate font to substitute for a missing font while taking font traits into account. Font cascading is based on cascade lists, which are arrays of ordered font descriptors. There is a system default cascade list (which is polymorphic, based on the user's language setting and current font) and a font cascade list that is specified at font creation time. Using the information in the font descriptors, the cascading mechanism can match fonts according to style as well as matching characters…</blockquote>

<p>This is why you can select a single display font for an application like a text editor, maybe "Source Code Pro" for example, and still copy and paste emoji chracters into the document. There are no emoji symbols in Source Code Pro. That's the font-substitution mechanism at work.</p>

<p>But what if a glyph still can't be found. The font handling subsystem is not out of options quite yet. There are 3 unique fonts that may come into play at this point:
<ul>
 	<li>The Unicode BMP Fallback font</li>
 	<li>The Unicode Last Resort font</li>
 	<li>GNU Unifont</li>
</ul>

<p>The Unicode BMP Fallback font contains a glyph for every character in the Unicode BMP. Each one of these glyphs displays as a box containing the hexadecimal digits corresponding to the code point value.</p>

<p>If those Tifinagh characters are missing, and instead you're seeing boxes containing hex digits then you're looking at a glyph from the BMP Fallback font.</p>

<p>Next, the Last Resort font, is just that. It is literally named "LastResort". Unlike the Unicode BMP Fallback font, the Last Resort font contains glyphs that provide information about the missing characters.</p>

<p><a href="https://www.unicode.org/policies/lastresortfont_eula.html">This font can be downloaded from the Unicode Consortium</a>, although there is probably no good reason to do that. The idea is that the font should be bundled into the OS and part of its text handling mechanism.</p>

<p>From the Last Resort font download page:</p>

<blockquote>The Last Resort font is a collection of glyphs to represent types of Unicode characters. These glyphs are designed to allow users to recognize that an encoded value is one of the following:
<ul>
 	<li>a specific type of Unicode character</li>
 	<li>in the Private Use Area (no private agreement exists)</li>
 	<li>unassigned (reserved for future assignment)</li>
 	<li>one of the illegal character codes.</li>
</ul>
These glyphs are used as the backup of "last resort" to any other font; if the font cannot represent any particular Unicode character, the appropriate missing glyph from the Last Resort font is used instead. This provides users with the ability to tell what sort of character it is, and gives them a clue as to what type of font they would need to display the characters correctly.</blockquote>

<p>More information can be found in in the <a href="https://unicode.org/versions/Unicode9.0.0/">Unicode Core Spec</a> itself in "Section 5.3: Unknown and Missing Characters".</p>

<p>The last fallback I'll mention is the <a href="https://unifoundry.com/unifont.html">GNU Unifont</a>, which attempts to accomplish the same thing as the Unicode BMP Fallback font, but takes a different approach. The goal here is to create "lite" bitmapped versions of all of the fonts in the Unicode BMP. (The font has grown to include characters beyond the BMP as well.)</p>

<p>Whereas the the BMP Fallback font just tells us the code point value of missing glyphs, the GNU Unifont attempts to show us what the characters look like. It's intended to be a better middle ground.</p>

<p>Now let's pick up our story. For those of you who are seeing all of the Tifinagh characters…</p>

<p>We can still reliably stump our platforms with references to characters that have been only very recently released, as we saw earlier with ? (Person Doing a Cartwheel, <code>U+1F938</code>).</p>

<p>For those of you who really appreciate missing characters, here are some others:</p>

<ul>
  <li>🤤 — (Drooling Face, <code>U+1F924</code>)</li>
  <li>🤷 — (Shrug, <code>U+1F937</code>)</li>
  <li>🤦 — (Face Palm, <code>U+1F9260</code>)</li>
  <li>🤳 — (Selfie, <code>U+1F933</code>)</li>
  <li>🦉 — (Owl, <code>U+1F989</code>)</li>
  <li>🥕 — (Carrot, <code>U+1F955</code>)</li>
  <li>🥘 — (Shallow Pan of Food, <code>U+1F958</code>)</li>
  <li>🛒 — (Shopping Trolley, <code>U+1F6D2</code>)</li>
</ul>

<p><strong>Note</strong>: If you are seeing the eight emoji in that list, then it's safe to say you have support for the newest emoji introduced with Unicode Version 9.0. As we'll see, that support could be coming from your OS or application or it could even be loaded via Javascript for a particular website (but not all of the others).</p>

<p>Regardless of what you or I do or do not see, Unicode is doing its part.</p>

<p>OK, so emoji are symbols (i.e. glyphs) that correspond to a specific code point — that's a clean, easy-to-understand arrangement… well, it's not quite so simple. There is one more thing we need to cover — the zero-width joiner.</p>

<p><strong>Zero-Width Joiner: The Most Important Character You'll Never See</strong></p>

<p>The zero-width joiner (ZWJ) has a code point but no corresponding symbol. It is used to connect two or more other Unicode code points to create a new "compound character" with a unique glyph all its own.</p>

<p>The ZWJ is a part of Unicode, so let's see what the <a title="UTR #51 Section 2.3 Emoji ZWJ Sequences" href="https://unicode.org/reports/tr51/#Emoji_ZWJ_Sequences">Unicode Consortium has to say about it.</a>:</p>

<blockquote>The U+200D ZERO WIDTH JOINER (ZWJ) can be used between the elements of a sequence of characters to indicate that a single glyph should be presented if available. An implementation may use this mechanism to handle such an emoji zwj sequence as a single glyph, with a palette or keyboard that generates the appropriate sequences for the glyphs shown. So to the user, these would behave like single emoji characters, even though internally they are sequences.</blockquote>

<p>When an emoji zwj sequence is sent to a system that does not have a corresponding single glyph, the ZWJ characters would be ignored and a fallback sequence of separate emoji would be displayed. Thus an emoji zwj sequence should only be supported where the fallback sequence would also make sense to a recipient. …</blockquote>

<p>So, a ZWJ is exactly what it says it is: It does not have any appearance (i.e. it is "zero width"), and it joins other characters.</p>

<p><strong>Note</strong>: Though we are only concerned with emoji here, I want to point out that the ZWJ is not only used with emoji. The character, which existed in the Unicode before emoji were incorporated into the standard, is a more general purpose mechanism for combining characters used with complex writing systems, notably the Arabic script and Indic script.</p>

<p>One important use of the ZWJ related to emoji are the skin tone modifiers that have already been mentioned. We've said that these skin tones were added to Unicode in version 8.0 to bring diversity to the appearance of emoji depicting human beings by allowing for a range of skin color. More specifically, Unicode has adopted the Fitzpatrick scale, a numeric classification scheme for skin tones specifying six broad groups or "types" of skin (Type I to Type VI) that represent in a general way at least a majority of people. From the <a href="https://en.wikipedia.org/wiki/Fitzpatrick_scale">Wikipedia entry for the Fitzpatrick scale</a>:</p>

<blockquote>It was developed in 1975 by Thomas B. Fitzpatrick, a Harvard dermatologist, as a way to estimate the response of different types of skin to ultraviolet (UV) light. It was initially developed on the basis of skin and eye color, but when this proved misleading, it was altered to be based on the patient's reports of how their skin responds to the sun; it was also extended to a wider range of skin types. The Fitzpatrick scale remains a recognized tool for dermatological research into human skin pigmentation.

<ul>
 	<li>Type I (scores 0–6) always burns, never tans (pale white; blond or red hair; blue eyes; freckles).</li>
 	<li>Type II (scores 7–13) usually burns, tans minimally (white; fair; blond or red hair; blue, green, or hazel eyes)</li>
 	<li>Type III (scores 14–20) sometimes mild burn, tans uniformly (cream white; fair with any hair or eye color)</li>
 	<li>Type IV (scores 21–27) burns minimally, always tans well (moderate brown)</li>
 	<li>Type V (scores 28–34) very rarely burns, tans very easily (dark brown)</li>
 	<li>Type VI (scores 35–36) Never burns, never tans (deeply pigmented dark brown to darkest brown)</li>
</ul>
</blockquote>

<p>Without getting too philosophical, I want to point out that any effort to represent increased diversity also means increasing specificity. As a result, there is a bit of tension that comes with these skin tone modifiers. Does every human being neatly fit into one of five categories of appearance based solely on skin tone? Certainly not. The skin tones in and of themselves are problematic. They may be accurate and varied enough to represent the ways different human skin reacts to UV light, but they do not represent the full range of human skin in terms of appearance.</p>

<p>That's to say nothing about the great variety in appearance of facial features.Another approach to the problem of inclusion is decreasing specificity. If there is only one highly stylized representation of every human being that doesn't bear a strong resemblance to one group more than any other, then that depiction can be said to represent all. It is this sort of inclusiveness that was the original design goal for emoji. Let's go back to the <a title="Section 2.4 What about diversity" href="https://unicode.org/faq/emoji_dingbats.html#2.4">Unicode Consortium's emoji FAQ</a>, also referenced at the beginning of the article, to see what it has to say about the issue of diversity and emoji:</p>

<blockquote>Q: What about diversity?</blockquote>

A: As with the examples of emoji characters representing food items above, The Unicode Standard does not require a particular appearance for characters that depict people or body parts, such as U+1F474 OLDER MAN or U+270B RAISED HAND. In fact, <a title="Design guidelines section UTR 51" href="https://unicode.org/reports/tr51/#Design_Guidelines">UTR #51 recommends</a> that such depictions be as neutral or generic as possible with respect to physical appearance, for example using non-realistic colors for skin tone. Similarly, characters whose name does not require a particular gender, such as U+1F477 CONSTRUCTION WORKER, should be depicted in a gender-neutral way.

However, many emoji users desire to use emoji for people and body parts that display a variety of more realistic skin tones. To support this, many such emoji may be followed by an emoji modifier character that can indicate one of 5 skin tones, based on the <a title="Wikipedia link 2016-0615 17:01 UTC" href="https://en.wikipedia.org/wiki/Fitzpatrick_scale">Fitzpatrick scale</a>. See <a title="Diversity section UTR 51" href="https://www.unicode.org/reports/tr51/index.html#Diversity">Diversity</a> in UTR #51.

Of course, there are many other types of diversity in human appearance besides different skin tones, including different hair styles and color. It is beyond the scope of Unicode to provide an encoding-based mechanism for representing every aspect of human appearance diversity that emoji users might want to indicate. The best approach for communicating very specific human images — or any type of image in which preservation of specific appearance is very important — is the use of embedded graphics as described in <a title="Emoji FAQ: Longer term plan" href="https://unicode.org/faq/emoji_dingbats.html#14">What is the longer term plan for emoji?</a></blockquote>

<p>One gets the sense that it is the opinion of the Unicode Consortium that less specificity is the better approach to inclusiveness than the greater, but still woefully inadequate, diversity afforded by any reasonable mechanism available to it. Furthermore, it seems like the skin tone modifiers have been somewhat grudgingly adopted in response to demand. It's an interesting issue with a lot of questions.</p>

<p>Getting back to the ZWJ, let's take a closer look at this in practice using the Boy emoji (<code>U+1F466</code>). To illustrate that this really works as described, I'm going to write out all of the emoji using numeric references. (You can take a look at the page source if you want to confirm this.)</p>

<p>So, we'll start with our base emoji:</p>

<ul>
  <li>👦 — (Boy, <code>👦</code>)</li>
</ul>

<p>Although the Fitzpatrick scale specifies six skin types, the depiction of the first two types using emoji are combined under Unicode. So, only five skin tone modifiers are actually available to us:</p>

<ul>
  <li>🏻 — Emoji Modifer Fitzpatrick Type 1-2 (<code>🏻</code>)</li>
  <li>🏼 — Emoji Modifer Fitzpatrick Type 3 (<code>🏼</code>)</li>
  <li>🏽 — Emoji Modifer Fitzpatrick Type 4 (<code>🏽</code>)</li>
  <li>🏾 — Emoji Modifer Fitzpatrick Type 5 (<code>🏾</code>)</li>
  <li>🏿 — Emoji Modifer Fitzpatrick Type 6 (<code>🏿</code>)</li>
</ul>

<p>These skin tone modifiers appear in the list "<a href="https://unicode.org/emoji/charts/full-emoji-list.html">Full Emoji Data</a>," along with all of the other emoji that are part of Unicode. They are represented as a square or some other shape of the appropriate color (i.e. skin tone) when used alone. That's what you should be seeing in the list above.</p>

<p>We can manually build up the skin-type variants of the Boy emoji by combining the base emoji with each of the skin-type symbols:</p>

<ul>
  <li>👦🏻 — Boy Type 1 to 2 (👦 <img style="margin: 0;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08f92dc0-455c-42a6-9344-2e2c10ee2bf2/zwj.png" alt="ZWJ placeholder" width="16" /> 🏻)</li>
  <li>👦🏼 — Boy Type 3 (👦 <img style="margin: 0;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08f92dc0-455c-42a6-9344-2e2c10ee2bf2/zwj.png" alt="ZWJ placeholder" width="16" /> 🏼)</li>
  <li>👦🏽 — Boy Type 4 (👦 <img style="margin: 0;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08f92dc0-455c-42a6-9344-2e2c10ee2bf2/zwj.png" alt="ZWJ placeholder" width="16" /> 🏽)</li>
  <li>👦🏾 — Boy Type 5 (👦 <img style="margin: 0;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08f92dc0-455c-42a6-9344-2e2c10ee2bf2/zwj.png" alt="ZWJ placeholder" width="16" /> 🏾)</li>
  <li>👦🏿 — Boy Type 6 (👦 <img style="margin: 0;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08f92dc0-455c-42a6-9344-2e2c10ee2bf2/zwj.png" alt="ZWJ placeholder" width="16" /> 🏿)</li>
</ul>

<p><strong>Note</strong>: The <img style="margin: 0;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08f92dc0-455c-42a6-9344-2e2c10ee2bf2/zwj.png" alt="ZWJ placeholder" width="16" /> used in the list above is just an image I've used as a placeholder for the ZWJ character, which is not visible itself.</p>

<p>Family and other groups are built up in exactly same way, one character at a time, with ZWJs in between. But don't forget we've already learned that we should use character references only when we absolutely must. So, although we could build up the group "Family, Man, Woman, Girl, Boy" manually…</p>

<pre>👨 ‍ 👩 ‍ 👧 ‍ 👦 — 👨‍👩‍👧‍👦</pre>

<p>…it's preferable (and also easier and less error-prone) to use the emoji symbol itself. So, of course that is what we should do. — 👨‍👩‍👧‍👦</p>

<p>We could also write the Latin lowercase "a" as either simply "a" or <code>a</code> (a). Imagine writing an entire HTML document out using only numeric character references, and you will probably appreciate the pointlessness of the exercise.</p>

### How Do We Know If We Have These Symbols?

<p>Like any other character, in order to display a specific emoji, a symbol must be included in some font available on the device you are using. Otherwise, the OS will find no way to graphically represent the code point.</p>

<p>An OS, be it a desktop operating system such as Apple's macOS, or a mobile OS like iOS and Android, ships with quite a few preinstalled fonts. (Many more can be acquired and installed separately.) The fonts available may differ by geographic region or primary language of the intended users across localized versions.</p>

<p>Many of these fonts will overlap, offering the same characters but presenting them in different styles. From one font to the next, these differences may be subtle or extreme. However, not all fonts overlap. Fonts intended for use with Western languages, for example, will not contain the symbols for Chinese, Japanese or Korean characters, and the reverse is also true. Even overlapping fonts may have extended characters that differ.</p>

<p>It is the responsibility of the font designer to decide which characters will be included in a given font. It is the responsibility of developers of an OS to make sure that the total collection of fonts covers all of the intended languages and provides a wide range of styles and decorative, mathematic and miscellaneous symbols and so on, so that platform is as expressively powerful as possible.</p>

<p>The current versions of all major platforms (Windows, macOS, Linux, iOS and Android) support emoji. Precisely what that means differs from one platform to the next, version to version and, in the case of Linux, from distribution to distribution.</p>

### The Great Emoji Proliferation Of 2016

<p>In this article we've covered a little about the history of emoji through the current version of the Unicode Standard, Version 9.0 (released 21 June 2016). We've seen that Version 9.0 introduced 72 entirely new emoji, not counting variants. (The number is 167 if we add skin tone modifers.)</p>

<p>Before moving on I should mention that the emoji included in Unicode 9.0 are referred to separately as "Unicode Emoji Version 3.0". That is to say that "Unicode Version 9.0 emoji" and "Unicode Emoji Version 3.0" are the same set of characters.</p>

<p>As we begin to look at Emoji support with the next section, and considering everything we've learned about emoji so far, it would seem to be a relatively straight-forward to know what we're looking for. Ideally we would like to see full support for all Version 3.0 emoji, including skin tone modifiers, and multi-person groupings. After all, a platform can't possibly do better than full support for the current version of the Standard. That would be madness! Have you heard the Nietzsche quote:</p>

<blockquote>There is always some madness in technology. But there is also always some reason in madness.</blockquote>

<p>Nietzsche was talking about love, but isn't it just as true of tech? 😉 (Winking face, <code>U+1F609</code>)</p>

<p>It turns out you can do "better" than 100% support, that is depending on your definition of better. Let's say that you can do <em>more</em> than 100% support. This isn't a unique concept in technology, or even web design and development. For example, implementators doing more than 100% support for CSS led to vendor prefixes. Somehow more than 100% always seems good at first, but tends to lead to problems. It's a little like how spending more than 100% of the money you have starts out as a solution to a problem, but tends to eventually lead to more problems 😦 (Frowning face with open mouth, U+1F626).</p>

<p>What does more than 100% support look like in the context of emoji?</p>

<p>First, let's agree that simply calling something an emoji does not make it an emoji. You may remember (or not) <a href="https://design.pepsico.com/pepsimoji.php">Pepsi's global PepsiMoji campaign</a>. A PepsiMoji is not an emoji, it's an image. We won't concern ourselves with gimmicky marketing ploys like that. There are still a couple of ways platforms are exceeding 100% support:</p>

<p>*   Using Zero Width Joiners to create non-standard symbols by combining standard emoji.
*   Rolling out proposed emoji before they are officially released.</p>

<p>An example of the former are Microsoft's somewhat silly (IMO) Ninja Cat emoji, which I discuss in the section on Windows' emoji support. But cat-inspired OS mascots are not the only place we see this sort of unofficial emoji sequence. More practical uses have to do with multi-person groupings and diversity, i.e. gender and skin tones.</abbr>

<p>The Unicode Consortium has this to say about <a href="https://unicode.org/reports/tr51/#Multi_Person_Groupings">multi-person groupings in UTR51</a>, the Unicode Version 3.0 Technical Report.</p>

<blockquote>Emoji for multi-person groupings present some special challenges:<br /><br /><strong>Gender combinations.</strong> Some multi-person groupings explicitly indicate gender: MAN AND WOMAN HOLDING HANDS, TWO MEN HOLDING HANDS, TWO WOMEN HOLDING HANDS. Others do not: KISS, COUPLE WITH HEART, FAMILY (the latter is also non-specific as to the number of adult and child members). While the default representation for the characters in the latter group should be gender-neutral, implementations may desire to provide (and users may desire to have available) multiple representations of each of these with a variety of more-specific gender combinations.<br /><br /><strong>Skin tones.</strong> In real multi-person groupings, the members may have a variety of skin tones. However, this cannot be indicated using an emoji modifier with any single character for a multi-person grouping.<br /><br />The basic solution for each of these cases is to represent the multi-person grouping as a sequence of characters—a separate character for each person intended to be part of the grouping, along with characters for any other symbols that are part of the grouping. Each person in the grouping could optionally be followed by an emoji modifier. For example, conveying the notion of COUPLE WITH HEART for a couple involving two women can use a sequence with WOMAN followed by an emoji-style HEAVY BLACK HEART followed by another WOMAN character; each of the WOMAN characters could have an emoji modifier if desired.<br /><br />This makes use of conventions already found in current emoji usage, in which certain sequences of characters are intended to be displayed as a single unit.</blockquote>

<p>We're told, "the default … should be gender-neutral, implementations may desire to provide … multiple representations of each of these with a variety of more-specific gender combinations."</p>

<p>This is in fact what implementations are doing, and pretty aggressively. As we will see, with its Windows 10 Anniversary Update, Microsoft now allows for as many as 52,000 combinations of multi-person groupings. Is this a good thing?</p>

<p>It is certainly laudable effort. Having said that, it's worth keeping in mind what it means from a standards perspective. Though Microsoft has greatly increased universality of its emoji through its flexibly diverse emoji handling, it comes at the expense of compatibility with other platforms. Be aware that users of every other platform, including every version of Windows other than Windows 10 Anniversary Update, will not see many of these groupings as intended.</p>

<p>Microsoft is not the only implementor to do this, but they've taken it further than others.</p>

<p>That leaves the idea of rolling out proposed emoji before they are officially released. Everyone is getting in on this, and it is a new phenomenon. First, let's take a brief moment to understand the situation.</p>

<p>Like most other standards bodies, the Unicode Consortium doesn't wait for the release of one version of a standard to begin working on the next. As soon as the door closes on inclusion for one release, changes and new proposals are evaluated for the next.</p>

<p>Generally speaking, the Unicode Consortium invites outside parties to participate in selecting future emoji, the process for which is outlined in the document "<a href="https://www.unicode.org/emoji/selection.html">Submitting Emoji Character Proposals</a>". As that page describes, the process is somewhat drawn out, and proposals can be rejected for many reasons, but those that fair well are eventually added as "candidates".</p>

<p>From the same page:</p>

<blockquote>…proposals that are accepted as candidates are added to <a title="Emoji candidates page at unicode.org" href="https://www.unicode.org/emoji/charts/emoji-candidates.html">Emoji Candidates</a>, with placeholder code points…</blockquote>

<p>So proposed Emoji are made public in some cases well before inclusion in the Unicode Emoji Standard. However the proposals carry this warning:</p>

<blockquote>Candidates are tentative: they may be removed or their code point, glyph, or name changed. No code point values for candidates are final, until (and if) the candidates are included as characters in a version of Unicode. Do not deploy any of these.</blockquote>

<p>That would seem pretty cut and dry. Promising proposals are added to a publicly available candidates list with the disclaimer that they should not be used until officially released. But rarely are these kinds of issues so simple for long. Seemingly more often than not, the exception is the rule, and by that measure, emoji are following the rules.</p>

<p>It started with a proposal submitted by Google titled, "<a title="Link to PDF" href="https://unicode.org/L2/L2016/16160-emoji-professions.pdf">Expanding Emoji Professions: Reducing Gender Inequality</a>" which begins:</p>

<blockquote>Google wants to increase the representation of women in emoji and would like to propose that Unicode implementers do the same. Our proposal is to create a new set of emoji that represents a wide range of professions for women and men with a goal of highlighting the diversity of women's careers and empowering girls everywhere.</blockquote>

<p>That proposal, well worth reading, was submitted in May 2016, a little over a month before the release of Unicode Version 9.0 with its 72 new emoji. It has led to a flurry of activity resulting in a <a href="https://www.unicode.org/reports/tr51/tr51-8.html">Proposed Update to UTR #51</a>, and making way for Unicode Emoji Version 4.0 much more quickly than might have been expected. How quickly — right about now.</p>

<p>The original proposal led to another by the Unicode Subcommittee, "<a href="https://www.unicode.org/L2/L2016/16181-gender-zwj-sequences.pdf">Gender Emoji ZWJ Sequences</a>", published on 14 July 2016, that fast-tracked new officially recognized sequences providing greater gender parity among existing emoji characters as well as new profession emoji.</p>

<p>From the proposal:</p>

<blockquote>This document describes how vendors can support a set of both female and male versions of many emoji characters, including new profession emoji. Because these emoji use sequences of existing Unicode characters composed according to UTR#51: Unicode Emoji, vendors can begin design and implementation work now and can deploy before the end of 2016, rather than waiting for Unicode v10.0 to come out in June of 2017.<br /><br />Unicode itself does not normally specify the gender for emoji characters: the emoji character is RUNNER, not MAN RUNNER; POLICE OFFICER not POLICEMAN. Even where the name may appear to be exclusively one gender, such as U+2603 SNOWMAN or U+1F482 GUARDSMAN the character can be treated as neutral regarding gender.<br /><br />To get a greater sense of realism for these characters, however, vendors typically have picked the appearance of a particular gender to display. This has led to gender disparities in the emoji that people can use. There is also a lack of emoji representing professions and roles, and the few that are present (like POLICE OFFICER) do not provide for both genders; a vendor has to choose one or the other, but can't represent both.</blockquote>

<p>You can also read more about this in the Unicode Consortium blog post, "<a href="https://blog.unicode.org/2016/08/proposed-update-utr-51-unicode-emoji.html">Proposed Update UTR #51, Unicode Emoji (Version 4.0)</a>".</p>

<p>At present all of this has resulted in a parallel <a href="https://unicode.org/emoji/charts-beta/index.html">beta standard for Unicode Emoji Version 4.0</a>.</p>

<p>How big a change are we talking about? There are a total of 88 new sequences combining existing emoji in new ways to provide gender alternates for current characters and also professions, for which there are male and female representations. However, adding skin tone variants to these new alternate characters and professions means that in total the number of emoji has increased from 1,788 in Version 3.0 to 2,243 in the proposed Version 4.0. That's 455 new emoji in approximately 2 months. ? (Rocket, <code>U+1F680</code>)</p>

<p>So why am I bothering to discuss unreleased, "beta" emoji? After all, the review period for the new proposed standard doesn't close until 24 October 2016 (coincidentally the date this article is scheduled to be published). I'm covering all of this because implementations are already rolling out these changes. It's no longer possible to accurately describe the current level of emoji support on these platforms without mentioning the proposed Version 4.0. Now that we have covered all of the officially-official emoji through the current version of the Standard, and unofficially-official emoji included in the post-current Standard, we can make sense of emoji support for across popular platforms. 😵 (Dizzy face, <code>U+1F635</code>)</p>

## Emoji OS Support

### Emoji Support: Apple Platforms (macOS and iOS)

<p>The current version of Apple's Mac operating system, "macOS Sierra" (10.12) released on 20 September 2016, includes well over 100 fonts, and among them one named "Apple Color Emoji". It's this font that contains all of the symbols for the platform's native emoji. The same font is used by the current version of Apple's mobile OS, iOS 10.</p>

<p>Users of Apple's OS' have typically enjoyed very good emoji support, and the newest versions continue the trend. To begin with, iOS 10 and macOS Sierra support all emoji through Unicode Version 9.0. Apple's OS release cycle is nicely timed as far as emoji are concerned. Unicode updates are happening in the Summer, and bring with them changes to Emoji. Apple is able to roll them out across all of their platforms in the Fall.</p>

<p>Beyond Unicode Emoji Version 3.0, macOS Sierra and iOS 10 support the gendered ZWJ sequences that are key part of the proposed Unicode Version 4.0. However new professions and sequences that add skin tone modifiers to existing multi-person groupings didn't make the update. As a bonus Apple threw in the Version 4.0 draft specification 🏳️‍🌈 (Rainbow flag sequence — White flag, <code>U+1F3F3</code> + Emoji variation selector, <code>U+FE0F</code> + ZWJ, <code>U+200D</code> + Rainbow, <code>U+1F308</code>).</p>

<p>In total, Apple's newest OS updates include 632 changes and additions. Some of these changes are minor and reflect nothing more than an evolution of design sensibilities of those involved at Apple. Others are more dramatic however, most notably 🔫 (pistol, <code>U+1F52B</code>), which has been changed from a realistic looking weapon to a cartoonish sci-fi water gun.</p>

<p>Coincidentally Microsoft has gone in the opposite direction with their pistol emoji. The representation of 🔫 (pistol, <code>U+1F52B</code>) in Windows 10 had the appearance of a cartoonishly futuristic ray gun, but with Windows 10 Anniversary Update in the Summer of 2016, the same emoji now depicts a more realistic looking revolver.</p>

### Emoji Support: Windows

<p>Windows 10, 8.1 and 8 all shipped with support for emoji. Limited support was <a href="https://www.microsoft.com/en-us/download/details.aspx?id=30521">added to Windows 7 through a software update</a>. For more information, there is an associated informational article titled "<a href="https://support.microsoft.com/en-us/kb/2729094">An Update for the Segoe UI Symbol Font in Windows 7 and in Windows Server 2008 R2 Is Available</a>").</p>

<p>Windows 8 included a limited set of black-and-white emoji with the "Segoe UI Symbol" font. This same font was eventually added to Windows 7, providing that version of the OS with its basic emoji symbols.</p>

<p>Windows 8.1 was the first Windows OS to support color emoji by default, shipping with the "Segoe UI Emoji" font, which provides Windows with its unique set of color emoji symbols.</p>

<p>Windows 10 continues to build on increasingly good support, adding all Unicode Version 8.0 emoji, including <a title="Diversity section in UTR #51 at unicode.org" href="https://www.unicode.org/reports/tr51/tr51-2.html#Diversity">skin tone modifiers</a>. However, Windows 10 did not include symbols for national flags 🇺🇸 (Flag of the United States of America, <code>U+1F1FA</code>, <code>U+1F1F8</code>) 🇩🇪 (Flag of Germany <code>U+1F1E9</code>, <code>U+1F1EA</code>), which are displayed as two-character country-code identifiers instead.</p>

<p><strong>Note</strong>: Flag emoji are each associated with pairs of 26 individual "regional indicator symbols." These combinations are referred to as an "emoji_flag_sequence". It is the combination of pairs of code points together that produce a single flag emoji. For more information about flag symbols, refer to "<a title="Annex B: Flags in UTR #51 at unicode.org" href="https://unicode.org/reports/tr51/index.html#Flags">Annex B: Flags</a>" in the document "<a title="Unicode Technical Report #51" href="https://www.unicode.org/reports/tr51/index.html">Unicode Technical Report #51</a>."</p>

<p><a title="Windows Update FAQ" href="https://support.microsoft.com/en-us/help/12373/windows-update-faq">Windows 10 Anniversary Update</a> released on 2 August 2016 (and available now via the Windows Update facility on your Windows 10 PC), brings with it a wealth of changes to emoji on Windows. The update (officially, version 1607, and the second major update to Windows 10) includes all of the new Unicode Version 9.0 emoji, but that's just the beginning.</p>

<p>Microsoft took the Anniversary Update as an opportunity to completely rethink and rework emoji on Windows, an effort dubbed "Project Emoji." In a <a title="Windows Experience blog homepage" href="https://blogs.windows.com/windowsexperience/">Windows Experience blog</a> post titled "<a href="https://blogs.windows.com/windowsexperience/2016/08/04/project-emoji-the-complete-redesign/">Project Emoji: The Complete Redesign</a>" we're told:</p>

<blockquote>The Microsoft Design Language Team embarked on Project Emoji, redesigning the emoji set from scratch in under a year. From early sketches to creating a new scripting method, the team knew only emoji. Illustrators, graphic designers, program managers, font technicians, production designers, and scripting gurus all worked with an impressive singular focus.</blockquote>

<p>It's a testament to the acknowledged significance of emoji that Microsoft would make this kind of an effort.</p>

<p>The update includes "over 1700 new glyphs, with a possible 52,000 combinations of diverse women, men, kids, babies, and families." As we've already discussed, Unicode 9.0 adds only 72 new emoji. The fact that Microsoft added 1700 new symbols clearly demonstrates that diversity was a critical focus of the update. Support for diversity begins with the same skin tone modifiers available under previous editions of Windows 10, now extended to more emoji. But the most ambitious effort is expansive support for family and other multi-person groups.</p>

<p>From the same "Project Emoji" blog post:</p>

<blockquote>So if you're a single mother with three kids, you'll be able to create that image. If your husband is dark-toned and you're light-toned and your two kids are a blend of both, you can apply all of those modifiers to create your own personal family emoji, one that's sincerely representative. It extends to the couple emoji, where you can join a woman, a heart, and a woman — both with unique skin tones — for a more inclusive emoji. Because they're created dynamically, there are tens of thousands of permutations. And no other platform supports that today.</blockquote>

<p>Emoji in Windows 10 Anniversary Update gives us a good sense of the scale of expanding skin tone modifiers across flexible multi-person groupings. However this effort seems to be largely independent of Unicode Emoji Version 4.0. Missing are all of the gendered and profession emoji that are the hallmark of proposed version.</p>

<p>The first thing you might notice are the bold outlines surrounding each of the new emoji. But the changes go much further than that. On the minor end of the scale, virtually all emoji have a more geometric look, which contributes to an overall stronger, more readable appearance. Beyond this, many emoji are drastically different, going so far as to be essentially new interpretations. Generally speaking, the new emoji are less generic, willowy and neutral, which is to say that they are more iconic, bold and dynamic. They've gone from looking like designs you might see on the wallpaper in a nursery to what you'd expect of the signage in a modern building. Some examples will give you a better sense of what I'm trying to describe:</p>

<figure><figcaption>Figure 5: Emoji in Windows 10 before and after the Anniversary Update</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea0a5f0d-1ec1-4e6b-9271-667312a99914/smiling-face-with-open-mouth-win10au-ba.png" alt="Smiling Face with Open Mouth emoji before and after Anniversay Update compared" width="144" height="72" /><br>
<figcaption>Smiling Face with Open Mouth, <code>U+1F603</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dc51266-9b83-4813-80f4-0ddf5174d9d1/happy-person-raising-one-hand-win10au-ba.png" alt="Happy Person Raising One Hand emoji before and after Anniversay Update compared" width="144" height="72" /><br>
<figcaption>Happy Person Raising One Hand, <code>U+1F64B</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a84c21a-522f-4706-96cf-b45eeb7a6d60/man-and-woman-holding-hands-win10au-ba.png" alt="Man and Woman Holding Hands emoji before and after Anniversay Update compared" width="144" height="72" /><br>
<figcaption>Man and Woman Holding Hands, <code>U+1F46B</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9782ca28-e21c-46a0-a501-91a588d90905/dromedary-camel-emoji-win10au-ba.png" alt="Dromedary Camel emoji before and after Anniversay Update compared" width="144" height="72" /><br>
<figcaption>Dromedary Camel, <code>U+1F42A</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f79f640-92d2-49ea-ae3b-d91c03b16416/soft-ice-cream-emoji-win10au-ba.png" alt="Soft Ice Cream emoji before and after Anniversay Update compared" width="144" height="72" /><br>
<figcaption>Soft Ice Cream, <code>U+1F366</code></figcaption></figure></figure>

<p>For more information on all things emoji in Windows 10 Anniversary Update, I highly recommend the <a href="https://blogs.windows.com/windowsexperience/">Windows Experience Blog</a> post "<a href="https://blogs.windows.com/windowsexperience/2016/08/04/project-emoji-the-complete-redesign/">Project Emoji: The Complete Redesign</a>," written by Danielle McClune (4 August 2016). It does a good job of covering the changes introduced with the Anniversary Update and also provides a bit of an insider's perspective. For those of you not particularly interested in Windows, the article offers some useful general information, including a brief illustrated discussion of the emoji skin tone modifiers and the Fitzpatrick scale.</p>

<p>If you still can't get enough of Windows 10 emoji goodness, the next place to turn to is Emojipedia's blog post "<a href="https://blog.emojipedia.org/diverse-emoji-families-come-to-windows/">Avalanche of New Emojis Arrive on Windows</a>," which nicely displays an overview of the changes to emoji in Anniversary Update. Beyond that, the <a href="https://emojipedia.org/microsoft/windows-10-anniversary-update/">Emojipedia page dedicated to the Anniversary Update</a> lists all of the emoji for this version of Windows, with an option to narrow the list to just the new symbols.</p>

<p>If all of this wasn't enough, Microsoft has added a new emoji keyboard to improve the experience of working with its updated emoji.</p>

<p>It's fair to say Microsoft has really upped its emoji game with the Windows 10 Anniversary Update. Are there any notable gaps or other issues related to Windows' emoji support other than the absent Version 4.0 symbols? I'll mention two…</p>

<p>First, the flag emoji are still missing. You will continue to see country-code identifiers, as in earlier versions of Windows 10.</p>

<p>Second is something of an oddity that's specific to Windows 10 Anniversary Update (and incompatible with every other platform): Ninja Cat.</p>

<p>Ninja Cat is a character that started out as something of an unofficial mascot for Windows 10 among developers, making its first appearance in a presentation about the OS in mid-2014 (before its release). Apparently, Ninja Cat has proven to be popular and enduring enough over the past couple of years to justify some <a href="https://blogs.windows.com/windowsexperience/2016/07/29/windows-insider-program-next/">desktop wallpapers and an animated GIF</a>, coinciding with the Anniversary Update, and — you know what's coming — there are ninja cat emoji as well.</p>

<p>I'm making a point of mentioning Ninja Cat because it is another example of the use of zero-width joiners. All Ninja Cat emoji (yes there's more than one) are sequences of the 🐱 (Cat face, <code>U+1F431</code>) emoji in combination with other standard emoji, connected with the ZWJ character, and resulting in new unofficial symbols.</p>

<p><strong>Note</strong>: If skin tone modifiers and flexible multi-person groups are among the more important uses of ZWJ, then non-standardized mascots and gimmicks have to be among the worst, as fun as they may be.</p>

<p>The basic Ninja Cat is a combination of 🐱 (Cat Face, <code>U+1F431</code>) and 👤 (Bust in Silhouette, <code>U+1F464</code>). Other combinations include:</p>

<ul>
  <li>Astro Cat — 🐱 (Cat Face, <code>U+1F431</code>) and 🚀 (Rocket, <code>U+1F680</code>)</li>
  <li>Dino Cat — 🐱 (Cat Face, <code>U+1F431</code>) and 🐉 (Dragon, <code>U+1F409</code>)</li>
  <li>Hacker Cat — 🐱 (Cat Face, <code>U+1F431</code>) and 💻 (Personal Computer, <code>U+1F4BB</code>)</li>
  <li>Hipster Cat — 🐱 (Cat Face, <code>U+1F431</code>) and 👓 (Eyeglasses, <code>U+1F453</code>)</li>
  <li>Stunt Cat — 🐱 (Cat Face, <code>U+1F431</code>) and 🏍 (Racing motorcycle, <code>U+1F3CD</code>)</li>
</ul>

<p>Here is what those symbols look like in Windows 10 Anniversary Update (the only place you will see them):</p>

<figure><figcaption>Figure 6: Ninja Cat emoji in Windows 10 Anniversary Update</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3041e9b5-bed2-4382-b42c-ac9476da0516/ninja-cat-ninja72x72.png" alt="Ninja Cat" width="72" height="72" /><br>
<figcaption>Ninja Cat</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242d5038-34e5-4cb7-9555-05d34f4d13d2/ninja-cat-astro72x72.png" alt="Astro Cat" width="72" height="72" /><br>
<figcaption>Astro Cat</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efedd1d4-5654-437c-8b28-dd85faa89e5d/ninja-cat-dino72x72.png" alt="Dino Cat" width="72" height="72" /><br>
<figcaption>Dino Cat</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/850f2dc2-644b-49a8-b7fe-3742830a451c/ninja-cat-hacker72x72.png" alt="Hacker Cat" width="72" height="72" /><br>
<figcaption>Hacker Cat</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f122bd30-1e52-4420-870a-d16c0e971ca4/ninja-cat-hipster72x72.png" alt="Hipster Cat" width="72" height="72" /><br>
<figcaption>Hipster Cat</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1309ad69-c2c6-4b68-a13d-0b1b65354d01/ninja-cat-stunt72x72.png" alt="Stunt Cat" width="72" height="72" /><br>
<figcaption>Stunt Cat</figcaption></figure></figure>

### Emoji Support: Linux

<p>If you're a Linux user, you'll know that these kinds of things tend to be distribution-dependent. The Unicode underpinnings are there. What may be missing is a font providing the symbols for displaying the emoji. Adding an emoji font is a relatively simple matter, and good options are available, including some that we'll see shortly.</p>

### Emoji Support: Android

<p>Android has supported emoji since Jelly Bean (4.1) and color emoji since Kit Kat (4.4). The latest version of Android, the recently released "Nougat" version 7.1 includes substantial changes. Like Microsoft, Google has made a big push toward ensuring its emoji support is second to none. The prior version of Android, "Marshmallow" (6.0.1), supported all of the official emoji through Unicode Version 8, with the notable exception of skin tone modifiers.</p>

<p>"Noto" and "Roboto" are the standard font families on recent versions of Android and Chrome. Unlike "Apple Color Emoji" and Window's "Segoe UI Emoji," <a title="Google's official Noto font site" href="https://www.google.com/get/noto/">Noto</a> and <a title="Roboto font downloads" href="https://material.google.com/resources/roboto-noto-fonts.html">Roboto</a> are freely available for download, including "Noto Color Emoji," the primary emoji font on Android.</p>

<p>For starters, Google is beginning to move away from the amorphous blobs that Android users are familiar with. However, Android is keeping the same gumdrops for generic faces:</p>

<figure><figcaption>Figure 8: Generic face emoji in Android Nougat (version 7.0)</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46a2e2a7-6ac5-437f-bdd7-1c9fb2ee676f/slightly-smiling-face-android-n-dev-2.png" alt="Slightly Smiling Face emoji in Android Dev Preview 2" width="72" height="72" /><br>
<figcaption>Slightly Smiling Face, <code>U+1F642</code> (Look familiar? Yep, it's unchanged from Android 6.0.1)</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7e9979-272c-4ed6-9eb0-a76000607191/smiling-face-with-open-mouth-android-n-dev-2.png" alt="Smiling Face with Open Mouth emoji in Android Dev Preview 2" width="72" height="72" /><br>
<figcaption>Smiling Face With Open Mouth, <code>U+1F603</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe9a8a7-a218-4363-a95e-2e429658e1a6/face-with-stuck-out-tongue-android-n-dev-2.png" alt="Face with Stuck-out Tongue emoji in Android Dev Preview 2" width="72" height="72" /><br>
<figcaption>Face With Stuck-out Tongue, <code>U+1F61B</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236c51fd-ed43-4260-a963-6179a4516fc8/drooling-face-android-n-dev-2.png" alt="Drooling Face emoji in Android Dev Preview 2" width="72" height="72" /><br>
<figcaption>Drooling Face, <code>U+1F924</code> (New with Unicode 9.0)</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a71842b-0670-4632-bc60-5d96ddb20ebb/rofl-face-android-n-dev-2.png" alt="Rolling on the Floor Laughing emoji in Android Dev Preview 2" width="72" height="72" /><br>
<figcaption>Rolling on the Floor Laughing emoji, <code>U+1F923</code> (New with Unicode 9.0)</figcaption></figure></figure>

<p>Those last two, both introduced in Unicode 9.0, are proof that Google is not entirely abandoning its gumdrops. But emoji are changing where it matters most, with human-looking depictions for less generic faces, actions and groups, complete with skin tone modifiers (conspicuously absent from Android to date).</p>

<p>Here are a few examples to give you some sense of how much the situation has improved:</p>

<figure><figcaption>Figure 9: Comparison of Android emoji from 6.0.1 to 7.0 Dev Preview 2</figcaption><figure><figcaption>Man with Turban</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fa062ef-eab4-4a22-8ee7-1ef0c8c86b86/man-w-turban-android-601.png" alt="Man with Turban in Android 6.0.1" width="72" height="72" /><br>
<figcaption>Android 6.0.1: Man With Turban, <code>U+1F473</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16433348-9d39-438b-9261-6617b32a3076/man-w-turban-android-n-dev-2.png" alt="Man with Turban in Android N Dev Preview 2" width="410" height="72" /><br>
<figcaption>Android N Dev Preview 2: Man With Turban, <code>U+1F473</code> (<code>U+200D U+1F3FB</code>, <code>U+200D U+1F3FC</code>, <code>U+200D U+1F3FD</code>, <code>U+200D U+1F3FE</code>, <code>U+200D U+1F3FF</code>)</figcaption></figure></figure><figure><figcaption>Girl</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2604ea-88d7-44ea-8f31-fdfc70312e41/girl-android-601.png" alt="Girl in Android 6.0.1" width="72" height="72" /><br>
<figcaption>Android 6.0.1: Girl, <code>U+1F467</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a721a2f3-42d8-4aa5-8de0-9044831b7d85/girl-android-n-dev-2.png" alt="Girl in Android N Dev Preview 2" width="410" height="72" /><br>
<figcaption>Android N Dev Preview 2: Girl, <code>U+1F467</code> (<code>U+200D U+1F3FB</code>, <code>U+200D U+1F3FC</code>, <code>U+200D U+1F3FD</code>, <code>U+200D U+1F3FE</code>, <code>U+200D U+1F3FF</code>)</figcaption></figure></figure><figure><figcaption>Happy Person Raising One Hand</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/850e9304-238c-4c93-a587-05d91f9096b9/happy-person-raising-one-hand-android-601.png" alt="Happy Person Raising One Hand in Android 6.0.1" width="72" height="72" /><br>
<figcaption>Android 6.0.1: Happy Person Raising One Hand, <code>U+1F467</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a4a974f-7251-482f-93ee-c66a6660efb1/happy-person-raising-one-hand-android-n-dev-2.png" alt="Happy Person Raising One Hand in Android N Dev Preview 2" width="410" height="72" /><br>
<figcaption>Android N Dev Preview 2: Happy Person Raising One Hand, <code>U+1F64B</code> (<code>U+200D U+1F3FB</code>, <code>U+200D U+1F3FC</code>, <code>U+200D U+1F3FD</code>, <code>U+200D U+1F3FE</code>, <code>U+200D U+1F3FF</code>)</figcaption></figure></figure><figure><figcaption>Man and Woman Holding Hands</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca354b42-9167-43ee-a713-6e02a44f8a0b/man-and-woman-holding-hands-android-601.png" alt="Man and Woman Holding Hands in Android 6.0.1" width="72" height="72" /><br>
<figcaption>Android 6.0.1: Man and Woman Holding Hands, <code>U+1F46B</code></figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc4b0aa7-97f3-41d0-8a0e-c0c46c0e3274/man-and-woman-holding-hands-win10au-ba-78x36.png" alt="Man and Woman Holding Hands in Android N Dev Preview 2" width="72" height="72" /><br>
<figcaption>Android N Dev Preview 2: Man and Woman Holding Hands, <code>U+1F46B</code></figcaption></figure></figure><figure><figcaption>Couple with Heart</figcaption><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac298f5a-e510-4d1e-b757-c6b24898ad4d/couple-various-android-601.png" alt="Couple with Heart: Woman Woman, Man Man, Woman Man in Android 6.0.1" width="246" height="72" /><br>
<figcaption>Android 6.0.1: Couple With Heart: Woman, Woman (<code>U+1F469 U+200D U+2764 U+FE0F U+200D U+1F469</code>); Man, Man (<code>U+1F468 U+200D U+2764 U+FE0F U+200D U+1F468</code>); Woman, Man (<code>U+1F469 U+200D U+2764 U+FE0F U+200D U+1F468</code>)</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/138dbcca-31f8-4ebe-b3ef-a49f6ae2522a/couple-various-android-n-dev-preview-2.png" alt="Couple with Heart: Woman Woman, Man Man, Woman Man in Android N Dev Preview 2" width="246" height="72" /><br>
<figcaption>Android N Dev Preview 2: Couple with Heart: Woman, Woman (<code>U+1F469 U+200D U+2764 U+FE0F U+200D U+1F469</code>); Man, Man (<code>U+1F468 U+200D U+2764 U+FE0F U+200D U+1F468</code>); Woman, Man (<code>U+1F469 U+200D U+2764 U+FE0F U+200D U+1F468</code>)</figcaption></figure></figure></figure>

<p>Nougat includes all of the <a title="Blog post discussing new Version 9 emoji" href="https://blog.unicode.org/2016/06/72-new-emoji-characters.html">new emoji introduced with Unicode Version 9</a>. However, despite it originally being Google's proposal, and their continued close involvement with the beta standard, Version 4.0 emoji, including gendered emoji and professions, didn't make the original Nougat (7.0) update.</p>

<p>However, just in the past few days, on 20 October 2016, Google released Android 7.1 with support for those Emoji Version 4.0 sequences. The 7.1 update is the first version of Android to include the new professions and genered emoji, as well as an expansion of multi-person groupings to include single parent families. For good measure Android 7.1 also includes ?️‍? (Rainbow flag sequence — White flag, <code>U+1F3F3</code> + Emoji variation selector, <code>U+FE0F</code> + ZWJ, <code>U+200D</code> + Rainbow, <code>U+1F308</code>).</p>

<p>Once again, Emojipedia is a good resource for platform-specific emoji information. A <a href="https://emojipedia.org/google/android-7.1/">page dedicated to Android Nougat 7.1</a> shows all of the emoji for the most recent version the OS. You can find pages for earlier releases as well.</p>

## Emoji On The Web

<p>The person viewing your website or application must have emoji support to see the intended symbols. We've specified the character set and encoding, and written emoji into our documents and UIs. The user agent renders the page and all of the characters on it, and that's what emoji are, of course.</p>

<p>You'll recognize that this is no more than the usual arrangement. However, emoji are newer than the other elements we're used to working with, and what's more, they occupy an odd space somewhere between text and images. Also, many of us begin with a shaky understanding of character sets and encodings. Altogether, it leads to confusion and consternation 😕 (Confused Face, <code>U+1F615</code>) in the way that only something similar to but not exactly the same as what we already know well can. Though this should come as no surprise, it's critically important, and for that reason I'm mentioning it here at the end of the article.</p>

<p>A code point without a glyph is just a code point. <code>U+2D53</code> (Tifinagh letter Yu) is clearly different than <code>U+1F32E</code> (Taco emoji). But, ultimately, we care only about the corresponding symbols ⵓ (<code>U+2D53</code>) and 🌮 (<code>U+1F32E</code>). As usual, we're at the mercy of our audience.</p>

<p>What about polyfills, shims and fallbacks? Is there anything like that we can use to improve the situation? I'm happy to say that the answer is yes.</p>

### Emoji One

<p>The <a title="Emoji One site" href="https://emojione.com/">Emoji One</a> project is aimed at creating a collection of up-to-date, high-quality and universal emoji resources. The largest component of the project by far is a comprehensive set of emoji that can be freely used by anyone for any purpose, both non-commercial or commercial (with attribution).</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b33444a-60cd-4102-af87-caaee087eb2d/emoji-one-sampler-650px-preview-opt.png" alt="Emoji One set sampler" width="650" height="359" /><figcaption>Figure 10: Emoji One set sampler</figcaption></figure>

<p>In the words of the people responsible for the project, Emoji One is:</p>

<blockquote>The web's first and only complete open source emoji set. It is 100% free and super easy to integrate.</blockquote>

<p>In December 2015, Emoji One announced the upcoming release of an updated and redesigned set of all of their emoji, branded "The 2016 Collection" (<a title="Listing of design changes" href="https://emojione.com/releases/2.1.0/">Q1 2016 Version 2.1.0, January 29, 2016</a>). More importantly, they committed to <a title="New releases page at emojione.com" href="https://emojione.com/releases/">quarterly design updates</a>, a promise they have made good on to date.</p>

<p>On May 30th, Emoji One officially released its 2nd quarterly update (<a title="Listing of design changes" href="https://emojione.com/releases/2.2.0/">Q2 2016 update, Version 2.2.0</a>), with a total of 624 "design upgrades," encompassing changes to existing symbols and entirely new (to the set) emoji.</p>

<p>Shortly thereafter, on June 21st, and coinciding with the official release of Unicode 9.0, Emoji One released <a title="Listing of all new emoji" href="https://emojione.com/releases/2.2.4/">version 2.2.4</a>, updating its set to include the 72 new Unicode emoji along with associated skin tone sequences.</p>

<p>Version 2.2.4 is the current version, though Emoji One has recently begun promoting the next major update, version 3.0, teasing "The revolution begins this December."</p>

<p>Currently, the Emoji One set comprises 1834 emoji, organized in nine categories, all of which can be browsed on the Emoji One website in the <a title="Emoji One complete gallery" href="https://emojione.com/#gallery">Emoji Gallery</a> and searched via <a title="Emoji One demo" href="https://emojione.com/demo/">The Demo</a>.</p>

<p>Emoji One has also created two web apps:</p>

*   [emojicopy](https://emojicopy.com)
*   [emoji.codes](https://emoji.codes/)

<p>emojicopy provides a responsive interface for searching emoji and copying selected symbols, with optional text, to paste into other apps.</p>

<p>emoji.codes offers a number of useful features, including a "<a href="https://emoji.codes/">Cheat Sheet</a>" for browsing and searching Emoji One short codes, a method of inputting emoji in applications and websites with built-in support for Emoji One.</p>

<p>emoji.codes' "<a href="https://emoji.codes/family">Family Tree</a>" is a table comparing emoji symbols across as many as 10 platforms (Symbola, Emoji One, Apple, Google, Windows, Twitter, Mozilla, LG, Samsung and Facebook). It's essentially a prettier version of the same sort of table on the Unicode Consortium's "<a title="Up-to-date table of emoji" href="https://unicode.org/emoji/charts/full-emoji-list.html">Full Emoji Data</a>" page previously mentioned.</p>

<p>The Family Tree is certainly much cleaner and provides a beneficial search interface. Just keep in mind that, when in doubt, the Unicode Consortium is the authoritative source.</p>

<p>Lastly, an <a href="https://emoji.codes/rolodex">Emoji Rolodex</a> lists links to quite a few resources: information, libraries, scripts, plugins, standalone apps and more. There are valuable tools here and some purely fun links, too.</p>

<p>All Emoji One art files are available for personal and commercial use under a Creative Commons license (<a title="License details" href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>). Emoji are available as PNG, SVG and font files (for Android, macOS and iOS) and can be downloaded as a complete set from the <a title="Developer resources" href="https://emojione.com/developers/">Emoji One developer page</a> or individually from <a title="Emoji One Gallery" href="https://emojione.com/#gallery">the gallery</a>.</p>

<p>In addition to the emoji art itself, the developer resources include a toolkit of conversion scripts, style sheets, sprite files and more.</p>

<p>The project also offers an extension for Google Chrome, called, fittingly, "<a href="https://emojione.com/chrome/">EmojiOne for Chrome</a>" which is described as "four game-changers in one," providing:</p>

*   a panel in Chrome for inputting emoji
*   emoji character search
*   set-once toggling between skin tones
*   well, the last "game changer" is Emoji One itself (which is cheating, but I think we can let it slide)

<p>Emoji One is, without a doubt, an important (assuming you think emoji are important) well-executed, well-maintained and ambitious project. If all of that wasn't enough, Emoji One has paid up to become a voting member of the Unicode Consortium.</p>

<p>Let's hope the project has a bright future.</p>

<p>We can include Emoji One in our websites and applications and know that not only will visitors see the emoji we intend, but also that the emoji we use will maintain a consistent, high-quality appearance across devices, OS' and browsers. Come on, that's pretty great!</p>

### How do we use Emoji One?

<p>To get started, you'll want to read through the information in <a title="Emoji One at GitHub" href="https://github.com/Ranks/emojione">Emoji One's GitHub repository</a>, or download the complete <a title="Developer resources at emojione.com" href="https://emojione.com/developers">developer toolkit</a>. Presently, the toolkit is around 60 MB and includes all emoji symbols as PNG files in three sizes (64, 128 and 512 pixels), and SVG vector images as well.</p>

<p>If you just want to read through the instructions for getting started, the <a title="README.md at GitHub" href="https://github.com/Ranks/emojione/blob/master/README.md">Emoji One readme on GitHub</a> is probably a better option.</p>

<p>You will learn that Emoji One has partnered with <a title="JSDeliver homepage" href="https://www.jsdelivr.com/">JSDeliver</a>, a "free super-fast CDN for developers and webmasters" (their words, not mine) to make it easy to install on any Javascript-capable website. It's a matter of adding a script and link element to the CDN-hosted Javascript and CSS files in the usual way.</p>

<p>There are also options for installing via npm, Bower, Composer and Meteor package managers. If any of those are relevant to you, then you should have no trouble at all.</p>

### Twemoji

<p>I would be remiss if I didn't mention that Emoji One is not your only option for open source emoji sets. In November 2014, Twitter announced on its blog that it was "<a title="Blog post" href="https://blog.twitter.com/2014/open-sourcing-twitter-emoji-for-everyone">Open Sourcing Twitter emoji for Everyone</a>."</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a70d2e49-35d7-4c54-85ee-626bfc8b2eb4/twemoji-sampler-650px-preview-opt.png" alt="Twemoji set sampler" width="650" height="383" /><figcaption>Figure 11: Twemoji set sampler</figcaption></figure>

<p>From the blog post:</p>

<blockquote>The project ships with the simple twemoji.js library that can be easily embedded in your project. We strongly recommend looking at the <a href="https://github.com/twitter/twemoji/blob/gh-pages/preview.html">preview.html source code</a> to understand some basic usage patterns and how to take advantage of the library, which is hosted by our friends at <a href="https://www.maxcdn.com/blog/emojis-ftw/">MaxCDN</a>.…</blockquote>

<p>For more advanced uses, the twemoji library has one main method exposed: <code>parse</code>. You can parse a simple string, that should be sanitized, which will replace emoji characters with their respective images.</blockquote>

<p><a href="https://github.com/twitter/twemoji">Twemoji</a> is hosted on GitHub and includes, among other resources, a set of emoji images as PNG files at 16 × 16, 36 × 36, 72 × 72 sizes, and SVG vectors as well.</p>

<p>After the initial release, a version 2 included emoji from Unicode Version 8 (as well as other changes). Subsequently, version 2.1 added symbols for all of the Unicode 9 emoji, for a total of over 1830 symbols. Presently, the current version of Twemoji is 2.2, which includes support for the gendered and profession emoji from the Unicode Emoji Version 4.0 draft, bringing the total number of symbols to 2,477. A complete download of the current version of the project is an over 400 MB ZIP file. You can read about the latest updates in <a href="https://github.com/twitter/twemoji/blob/gh-pages/README.md">the project's ReadMe file</a>.</p>

## Conclusion

<pre><code class="language-html">                       ⛅
🎈
🏃  🌲                    🏡           🌲🌲         🌲</code></pre>

<p>Are we done? Could it be? Do we know everything there is to know about emoji? 😫 (Tired Face, U+1F62B)</p>

<p>It might be a stretch to say we know absolutely everything there is to know, but we know what we need to know to find and understand everything there is to know. 😤 (Face with Look of Triumph U+1F624)</p>

<pre><code class="language-html">                  ⛅
🎈
🚶   🌲                    🏡           🌲🌲         🌲</code></pre>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Unicode For A Multi-Device World](https://www.smashingmagazine.com/2014/05/unicode-for-a-multi-device-world/)
*   [Designing For The Internet Of Emotional Things](https://www.smashingmagazine.com/2016/04/designing-for-the-internet-of-emotional-things/)
*   [Giving Your Product A Soul](https://www.smashingmagazine.com/2016/10/giving-your-product-a-soul/)
*   [All About Unicode, UTF8 & Character Sets](https://www.smashingmagazine.com/2012/06/all-about-unicode-utf8-character-sets/)</p>

{{< signature "rb, al, il, vf" >}}
