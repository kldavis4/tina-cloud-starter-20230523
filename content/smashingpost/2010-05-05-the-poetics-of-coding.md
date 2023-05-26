---
title: The Poetics Of Coding
slug: the-poetics-of-coding
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/035b873b-395c-4167-bca8-612307c4631e/coding.jpg
date: 2010-05-05T12:34:57.000Z
author: matt-ward
description: >-
  There is little doubt that WordPress is one of the most popular blogging and content management platforms out there today. This is not an article about WordPress, though, but rather a more general musing on one of its thought-provoking taglines: “**Code Is Poetry**.”
categories:
  - Coding
  - Workflow
  - CSS
---

That's an interesting metaphor. I've written about the relationship between these coding languages and proper human language (specifically, English). As someone who graduated from university with a degree in English Literature and came to Web design in a roundabout way, this kind of thinking has always interested me. 

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Why Coding Style Matters</span>](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [An Interviews With Matt Mullenweg And Mike Little](https://www.smashingmagazine.com/2014/02/interview-matt-mullenweg-mike-little-wordpress/)
*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/7-principles-of-clean-and-optimized-css-code/)

As has this apparent connection between code and poetry. What does the metaphor mean? I took some time to really think about this relationship and discovered that the people at WordPress got it right (again). Code really is similar to poetry!

{{% feature-panel %}}

## A Superficial Similarity

To start off, code and poetry have a somewhat obvious and entirely superficial similarity, and we may as well begin there. Here is a poem I wrote a few years ago:
<blockquote>A man in a suit,
<span style="margin-left: 1em;">standing on an old stone bridge,</span>
sees the reflection
<span style="margin-left: 1em;">of himself in the water</span>
flowing, unhindered, below.</blockquote>

I promise this will be the only work of mine that I include here, but let's compare it to some snippets of simple code, starting with HTML:

<pre><code class="language-markup tmp-xml">&lt;body&gt;
  &lt;div id=”content”&gt;
    &lt;h1&gt;The Title&lt;/h1&gt;
    &lt;p&gt;Some content&lt;/p&gt;
  &lt;/div&gt;
&lt;/body&gt;</code></pre>

Now look at some CSS:

<pre><code class="language-css">div {
  border: 1em 0px;
  background-color: #444
  border: 1px solid #222;
}</code></pre>

And finally some JavaScript:

<pre><code class="language-javascript">function cubeMe(x){
  var answer = x*x*x;
  alert(answer);
}</code></pre>

I want to highlight two key elements: the short lengths and the prominent indentation. These are both common elements of poetry and code (though not absolutely necessary to either).

This comparison is superficial at best, and there is a much stronger connection to explore. Still, this basic similarity reveals a certain visual relationship between code and poetry, which gives us an interesting entry point to discuses the subject.</p>

## A Master's Art

This code-is-poetry metaphor comes at least partly from a perception of poetry as the master's craft. Whether you love or hate it (and I know a lot of people hate it), there has always been a general sense that poetry sits at the apex of the written word, as though poets sit in an ivory tower, composing lines with a golden pen.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93afa488-25c2-4070-b0d7-d2b48dd04d2b/masters-art.jpg" width="500" height="335" />

Of course, the reality is strikingly different. A lot of really bad poetry is out there, written by people who call themselves poets just because they can rhyme words at the end of two lines.

Does that sound familiar?

How similar is this to the proverbial “nephew”? You know the one: that kid who read the introduction to a high-school textbook about the Web, figured out a few HTML tags and is now driving you crazy with his offer of a “Web design” for $100 and a six-pack of beer. Makes you want to tear your hair out, doesn't he?

Anyone who has been at this Web design thing for a while (or at least anyone who takes themselves seriously) would agree that there's more to the job than hacking out content wrapped in a bunch of poorly structured and entirely non-semantic HTML. For those of us who strive to be masters of our craft, code is so much more.

Code has purpose and meaning. It requires structure. It should be lightweight and elegant, not bogged down with lines and lines of garbage. Writing great code isn't something that just happens. It takes discipline and work! It's an art unto itself.

Feeling impassioned yet? If so, you might have the heart of a poet. I'll tell you why.</p>

## Of Pen And Purpose

Every good poem has a purpose. The purpose need not be so lofty as to change the world or to establish a new school of thinking, but every good poem needs a purpose. Of course, nothing is surprising about this. Many mediocre and poor poems are written with a purpose. The difference is in execution.

If a poem is written for a particular purpose, then the composition should reflect that purpose. The structure, word choice, subject and tone should all work together to support the primary purpose. For example, the purpose of Coleridge's “Kubla Khan” is to capture the imagery of one of the poet's (opium-induced) dreams. It famously opens:
<blockquote>In Xanadu did Kubla Khan
A stately pleasure-dome decree:
Where Alph, the sacred river, ran
Through caverns measureless to man
<span style="margin-left: 2em;">Down to a sunless sea.</span></blockquote>

The poem continues on in much the same tone, fully of lyrical and Romantic language by which Coleridge captures the essence of his dream. His word choice and form help the poem achieve its purpose.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6719c03c-9928-49f5-a3f2-602bfb5d3909/pen-and-purpose.jpg" alt="Screenshot" width="500" height="335" />

A limerick is a different kind of poem altogether, one generally intended to be witty or humorous (and sometimes just plain crude). Here is one of the limericks I remember best:
<blockquote>There was an old man from the Cape,
Who made himself garments of crepe.
When asked if they tear
he replied, "Here and there,
But they keep such a beautiful shape!"</blockquote>

All limericks follow this structure and share this cadence, which contribute to the overall effect. The rhythm makes the text sound silly and light-hearted, whatever the actual words. While the poem is vastly different from Coleridge's Romantic vision, it too demonstrates a keen understanding of its purpose.

Our code should be much the same. Different kinds of code serve different purposes and should be used accordingly. In Web design, the most cliched example is using tables for layout purposes. The HTML table tags were intended to present information in tabular format, not to structure an entire document. Using it in the latter way is a misappropriation of its purpose.

Any experienced coder would attest that tabular layouts are far more inflexible than CSS. They really limit you to the confines of the table itself. Styles, however, give you a great deal more flexibility and allow you to do a lot more. We may harp on about it a lot, to the point of being annoying, but it's a perfect example of how failing to understand purpose can render code less effective!

CSS also provides a great example of the difference between inline, embedded and external styles. Each has a different purpose, and using it the wrong way can really weigh down your code. The external style sheet is used to implement universal styles that can be applied to an entire website (or, in some cases, multiple websites). The embedded style sheet, which is less frequently used, overwrites external styles. This is great for custom artistic posts. Inline styles can be used to overwrite the styling of a single element.

It's all pretty straightforward for a seasoned Web designer. For the uninitiated, though, mixing up these purposes is all too easy, and it potentially results in bloated code, full of unnecessary inline styling and redundant elements, all from a lack of understanding CSS' rules of precedence.

So, whether you code HTML or CSS, if you believe in the importance of understanding your purpose, then you certainly have something in common with the great poets.

## Meaning

Another important aspect of poetry is meaning. Like any text, a poem means something on the surface: it literally means what it says, even if what it says is sometimes difficult to understand (especially with some archaic works). However, a good poem always has a secondary meaning, hidden beneath the surface.

The incomparable Robert Frost demonstrates this, in a stanza from his popular “Stopping by Woods on a Snowy Evening:”
<blockquote>The woods are lovely, dark, and deep,
But I have promises to keep.
And miles to go before I sleep,
And miles to go before I sleep.</blockquote>

On the surface, the poem's closing lines simply state that the narrator thinks the woods are lovely but that he has promises to keep and a long journey before he gets to bed. But there is also critical discussion about the meaning that lurks below the surface of these lines. Not to go into too much analysis here, but it has been suggested that these lines indicate a deep yearning in the narrator to abandon the responsibilities of society and retreat to the embrace of nature, possibly even to death.

<img loading="lazy" decoding="async"  title="meaning" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55ba1af5-5fc8-4923-ac52-8b7a25c755b3/meaning.jpg" alt="meaning" width="500" height="335" />

Again, code can be very similar, though in a different way. Instead of having a surface meaning and an underlying meaning, code (and specifically HTML) creates meaning through both its semantics and its structure. For example, consider these two lines:

<pre><code class="language-markup tmp-xml">&lt;p&gt;The Wasteland&lt;/p&gt;</code></pre>

<pre><code class="language-markup tmp-xml">&lt;h1&gt;The Wasteland&lt;/h1&gt;</code></pre>

The content is identical, but the context created by the mark-up is entirely different. In the first instance, the content is a paragraph (or simple body text). In the second, it is a first-level heading. The two are very different. Here's another example:

<pre><code class="language-markup tmp-xml">&lt;p&gt;This is a paragraph.&lt;/p&gt;</code></pre>

<pre><code class="language-markup tmp-xml">&lt;p&gt;This &lt;em&gt;is&lt;/em&gt; a paragraph.&lt;/p&gt;</code></pre>

The first sentence is a simple statement. But the emphasis in the second sentence on the word “is” changes the meaning. Now it becomes more of an affirmation against the (quite legitimate) claim that a single sentence does not really constitute a paragraph. Also, notice the choice of tag, using the semantic <code>em</code> tag for emphasis, instead of the simple italics tag.

Similarly, a language such as PHP provides contextual meaning through conditional logic. For example, here is a snippet of WordPress code that I often use to generate the content of the <code>title</code> tag:

<pre><code class="language-php">&lt;?php if(is_home()){
  echo "Home :: ";
}
elseif(is_single()){
  echo the_title() . " :: ";
}
elseif(is_page()){
  echo the_title() . " :: ";
}
elseif(is_category()){
  echo single_cat_title() . " :: ";
}
elseif(is_tag()){
  echo "Articles tagged as "";
  echo single_tag_title() . "" :: ";
}
elseif(is_date()){
  echo "Articles posted in ";
  echo the_time('F, Y') . " :: ";
}
?&gt;</code></pre>

In this case, the code produces a different title, based on the type of content being generated. It's much different than our HTML example, but it still demonstrates the ability of a block of code to provide extra meaning to content—the same way that a poem's subtext adds a layer of meaning below the surface.</p>

## The Importance Of Being Structured

A key similarity in the code-as-poetry metaphor is the need for structure. Poetry is traditionally a very structured form of writing. Take the sonnet, which was once widely considered one of the most elevated forms of poetry and is quite difficult to write (trust me, I've tried). Here is Elizabeth Barret-Browning's famous “How Do I Love Thee”:
<blockquote>How do I love thee? Let me count the ways.
I love thee to the depth and breadth and height
My soul can reach, when feeling out of sight
For the ends of Being and ideal Grace.
I love thee to the level of everyday's
Most quiet need, by sun and candlelight.
I love thee freely, as men might strive for Right;
I love thee purely, as they turn from Praise.
I love thee with the passion put to use
In my old griefs, and with my childhood's faith.
I love thee with a love I seemed to lose
With my lost saints,–I love thee with the breath,
Smiles, tears, of all my life!–and, if God choose,
I shall but love thee better after death.</blockquote>

This poem, which appears on so much sentimental merchandise these days, follows the sonnet structure very closely. It has the standard 14 lines, with a specific rhyming structure. For the most part, it also follows the traditional meter, called iambic pentameter. I won't break down the sonnet's adherence to and deviation from traditional structure (because I would probably lose your interest). Suffice it to say, this poem is constructed on a very strict and rigid scheme.

<img loading="lazy" decoding="async"  title="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7fe48fa-d0d5-48d3-8a43-d3ac2f91c1f5/being-structured.jpg" alt="Screenshot" width="500" height="335" />

There are other types of poetic structures, too, such as the brief haiku and the silly limerick (which we looked at). Some might suggest that much modern poetry is even more “free” and <em>un</em>structured. This may be the case with lesser poems, but not with the best modern works. While these poems may <em>appear</em> not to follow a pattern, they are always structured in some way. You just have to look harder to find it.

The structure of code, though, is very obvious—in fact, probably more so than the rigid sonnet form. Let's look at a basic HTML document:

<pre><code class="language-markup tmp-xml">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;A Simple Document&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;h1&gt;A Simple Document&lt;/h1&gt;
    &lt;p&gt;This is just a simple document.&lt;/p&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

As with the sonnet, a clear structure is at work here, one that is significantly different. The <code>html</code>, <code>head</code> and <code>body</code> tags all give form to the document as a whole, while the <code>title</code>, <code>h1</code> and <code>p</code> tags wrap and semantically define different bits of content. For every opening tag, there is a closing tag, appearing at the appropriate place in the document's hierarchy. It's all basic HTML.

It's also highly structured, and without this structure, the code degrades. In some cases, it could be a semantic issue, which often goes unnoticed, because browsers will usually correct these issues. For instance, we all know that the <code>title</code> tag should appear between the <code>head</code> tags, right? Well, if the <code>title</code> tag is placed somewhere else, most modern browsers will still understand the tag and render it properly. Semantically and structurally, though, it's all wrong.

The same is true of improperly nested tags. Something like the following would likely render properly in the browser:

<pre><code class="language-markup tmp-xml">&lt;p&gt;A link to &lt;em&gt;&lt;strong&gt;&lt;a href="https://www.smashingmagazine.com"&gt;Smashing Magazine&lt;/em&gt;&lt;/strong&gt;&lt;/a&gt;&lt;/p&gt;</code></pre>

And yet, it is structurally flawed, because tags should always be closed in the order that they were opened. Of course, things get really dicey when tags are unbalanced or when block-level elements intersect. I can't be the only one who has been hijacked by a rogue <code>div</code> tag!

The point here is not to dig into the structural semantics of HTML, but to emphasize the importance of the structure in both code and poetry. If you're nodding along with me here and agree on the importance of properly structured documents, then that's another trait you share with poets and another bit of support for our code-is-poetry metaphor.</p>

## Trim And Efficient

Finally, in a well-crafted poem, every single word has meaning and purpose. Despite what may appear to be overly complex words or flowery lines, the entire piece is meticulously crafted. A poet can spend hours struggling for just the right word, or set aside a poem for days before coming back to it for a fresh perspective.

Let's look at another of Robert Frost's shorter works, this one entitled “Fire and Ice”:
<blockquote>Some say the world will end in fire,
Some say in ice.
From what I've tasted of desire
I hold with those who favor fire.
But if it had to perish twice,
I think I know enough of hate
To say that for destruction ice
Is also great
And would suffice.</blockquote>

It may be somewhat grim, but it is also exceptionally well crafted. Each word here is so carefully placed that not a single one could be removed without detracting from the meaning of the poem.

Ezra Pound's “In The Station of the Metro” is even more succinct:
<blockquote>The apparition of these faces in the crowd;
Petals on a wet, black bough.</blockquote>

In just two lines and fourteen simple words, Pound paints a striking image, ripe with meaning and begging to be devoured by scholars and critics. Now, that's efficiency.

<img loading="lazy" decoding="async"  title="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24ca3f14-119d-4b44-9f29-1fdc308360cd/trim-and-efficient.jpg" alt="Screenshot" width="500" height="335" />

Would you not agree that the same should hold true for code? Shouldn't every tag, selector, rule and line of PHP have an explicit purpose? Unfortunately, making HTML and CSS bloated with unnecessary tags and styles is all too easy. Take this code:

<pre><code class="language-markup tmp-xml">&lt;div&gt;
  &lt;p&gt;&lt;span&gt;This is a paragraph.&lt;/span&gt;&lt;/p&gt;
&lt;/div&gt;

div{margin: 1em 20px}
div p {font-family: sans-serif; font-size: 14px}
div p span {color: blue}</code></pre>

Now, compare it to this:

<pre><code class="language-markup tmp-xml">&lt;p&gt;This is a paragraph&lt;/p&gt;

p{margin: 1em 20px; font-family: sans-serif; font-size: 14px; color: blue}</code></pre>

Assuming no extra margins or padding are applied to the original <code>div</code>, the second bit of code will render exactly the same as the first—a more economical way to achieve the same result.

As we mentioned in the section on purpose, code can also become bloated by unnecessary inline styles, where an external or even embedded style sheet would be more efficient (depending on the purpose, of course). Yet another example would be to use the <code>onmouseover</code> event to execute simple JavaScript effects that could be achieved more efficiently by CSS.

For the master craftsperson, great code and great poetry are lean and trim, with no excess of words or other unnecessary elements.</p>

## Conclusion

Part of the beauty of metaphor is its ability to highlight meaningful similarities between two seemingly unrelated ideas. Still, I have to admit that when I really considered this code-is-poetry metaphor, I was surprised by just how deep the similarities run. In some ways, the metaphor almost blurs into reality.

Perhaps code really is a form of poetry, and the coder a new kind of poet.

What does it all mean? I can't answer that entirely, at least not here and now. But if more people regarded code as its own kind of poetry or at the very least put the two on more even footing, it would raise the bar and lead to higher-quality work. And that would only be a good thing!

{{< signature "al" >}}

