---
title: Getting Started With Ruby On Rails
slug: getting-started-with-ruby-on-rails
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2a85d18-9b6d-41ff-b7e7-81054484acf9/ror.jpg
date: 2009-03-20T01:47:35.000Z
author: jan-varwig
description: >-
  If you're a Web developer who's been curious about Ruby on Rails but has never
  gotten around to trying it out because you couldn't find a suitable overview
  of its advantages, then this article is for you. **We want to bring Ruby on
  Rails closer** to those who want to take a peek first, without going through
  an entire tutorial. So, this article is structured a little different from
  most other introductions out there; hopefully it is more useful because of
  this.

  I assume you're **already familiar with some other form of Web development**,
  whether PHP, Python, Perl or Java, and relational databases like MySQL. First,
  we'll introduce Rails and Ruby and the basic ideas behind both. I'll teach you
  just enough Ruby so that you understand the code samples. I'll tell you how to
  get Ruby on Rails running on your computer, and I'll give you an overview of
  the basic functionality of Rails and demonstrate how Rails' main parts work
  together.

  **This tutorial consists of two articles**: in the current, first article we
  get started with some basic concepts and essential components of Ruby on
  Rails. In the second part (it will be published next week) you will learn how
  to install the engine; you'll also take a closer look at Rails’ inner workings
  and discover main advantages of Ruby on Rails. Please **stay tuned**.

  **After reading these parts, you should have an idea of whether Rails is** for
  you. If you get the feeling that it is, I'll point you to some good tutorials
  on the Web that you can use to learn Rails. I'll also provide a lot of further
  reading recommendations so you can dig as deep into the topic as you like.

  You may want to take a look at the following related posts:

  *   [10 Useful Tips For Ruby On Rails
  Developers](https://www.smashingmagazine.com/2009/02/25/ruby-on-rails-tips/)
categories:
  - Coding
  - Ruby on Rails
---
If you're a Web developer who's been curious about Ruby on Rails but has never gotten around to trying it out because you couldn't find a suitable overview of its advantages, then this article is for you.

We want to bring Ruby on Rails closer to those who want to take a peek first, without going through an entire tutorial. So, this article is structured a little different from most other introductions out there; hopefully it is more useful because of this.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Get Started With Ruby](https://www.smashingmagazine.com/2012/05/beginners-guide-ruby/)
*   [Get Started Writing iOS Apps With RubyMotion](https://www.smashingmagazine.com/2012/08/get-started-writing-ios-apps-with-rubymotion/)
*   [A Guide To Starting Your Own Rails Engine Gem](https://www.smashingmagazine.com/2011/06/a-guide-to-starting-your-own-rails-engine-gem/)
*   [How To Set Up An Ubuntu Local Machine For Ruby On Rails](https://www.smashingmagazine.com/2011/06/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/)

I assume you're <strong>already familiar with some other form of Web development</strong>, whether PHP, Python, Perl or Java, and relational databases like MySQL. First, we'll introduce Rails and Ruby and the basic ideas behind both. I'll teach you just enough Ruby so that you understand the code samples. I'll tell you how to get Ruby on Rails running on your computer, and I'll give you an overview of the basic functionality of Rails and demonstrate how Rails' main parts work together.

{{% feature-panel %}}

<strong>This tutorial consists of two articles</strong>: in the current, first article we get started with some basic concepts and essential components of Ruby on Rails. In the second part (it will be published next week) you will learn how to install the engine; you'll also take a closer look at Rails’ inner workings and discover main advantages of Ruby on Rails. Please <strong>stay tuned</strong>.

<strong>After reading these parts, you should have an idea of whether Rails is</strong> for you. If you get the feeling that it is, I'll point you to some good tutorials on the Web that you can use to learn Rails. I'll also provide a lot of further reading recommendations so you can dig as deep into the topic as you like.

I'm taking this approach because Rails is almost 5 years old now and has become very complex. There are a lot of "Create-your-own-blog-in-5-minutes"-type tutorials out there already, and rather than adding another one, I wanted to provide this kind of rough overview to help you decide whether to take this adventure.

You may want to take a look at the following related posts:

*   [10 Useful Tips For Ruby On Rails Developers](https://www.smashingmagazine.com/2009/02/25/ruby-on-rails-tips/)

## The Idea Behind Rails

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fed1dbb-78ee-407a-bdc0-b0f47bdacb7d/rails.jpg" alt="" />

Ruby on Rails was created by David Heinemeier Hansson as a kind of byproduct of Basecamp's development at 37signals in 2004. Basecamp was built in Ruby because Hansson found PHP and Java not powerful or flexible enough. It was quite an obscure language back then, without the large eco-system available today. To make development easier, Hansson rolled his own Web development framework, based on simple ideas that had proven successful elsewhere. Rails is founded on pragmatism and established paradigms instead of exotic new ideas. And that's what made it so successful.

Rails is based on the <strong>Model-View-Controller</strong> pattern that splits your application into three parts:

*   The **Models** are your business objects describing the structure and behavior of the problem your application is trying to solve. These are usually backed by an Object-Relational-Mapping framework that persists your objects to a database in the background.
*   The **Views** are the templates that render data to the user and all the logic surrounding presentational aspects of your app.
*   The **Controller** sits at the heart of everything, processing requests from clients, initiating changes in the models and triggering the rendering of the templates.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a94d1ca-98ee-493d-9f5b-7fa79ef70c5a/mvc.jpg)

Rails is "<strong>opinionated software</strong>." It doesn't want to be everything for everyone. It focuses on one way of doing things and streamlines all its parts around that way. That's not to say there's no possibility of doing things differently if you need to, but you'll definitely have it easier if you do things "the Rails way." And that way happened to be exactly the right one not only for Hansson but for a lot of other developers, too, another important reason for Rails' success.

Programmer productivity was the main goal during Rails' development, not performance. This has led to a <em>lot</em> of controversy and claims that arise over and over about how Rails can't scale. This is Rails' own fault to a certain degree. In its early days, it had the image of a Web development framework messiah of hope and wonder that would lead us all to the promised land were applications wrote themselves. The Rails team didn't do enough to keep expectations more realistic, and some people became disappointed.

While it's true that Ruby on Rails is slower than comparable stacks on PHP or Python, it certainly does scale, as hundreds of successful deployments are proving. You'll just need to scale sooner and put some thought into it. Remember also that Ruby's current default implementation is terribly inefficient, but alternatives are on the way. There's nothing inherently slow about the language, though, as blazing-fast implementations of Smalltalk (a language very similar to Ruby) prove. Ruby will only get faster. As the saying goes, you don't have a performance problem until you have a performance problem, and all this talk should not scare you yet. You haven't even started. ;)

Now, before I introduce you to the framework, let's get started with Ruby.</p>

## A Gem From Japan

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fca33f02-39f1-493a-994a-26b3cbdc5c4d/ruby.jpg" alt="" />

Ruby on Rails owes not only half its name but its entire feel and flexibility to "Ruby," that neat little language from Japan.

Ruby came out in 1995 and was developed by Yukihiro Matsumoto, or “Matz” as he's called in the community. Version 1.0 was released in 1999 and slowly gained recognition in the west from then on.

A key point in the spread of Ruby was the release of “Programming Ruby,” also called the "Pickaxe" (a reference to its cover illustration), by the Pragmatic Programmers. "Programming Ruby" was the first comprehensive English guide to the language and API.

Ruby was designed with simple principles in mind. Matz took the most successful and powerful elements from his favorite programming languages -- Perl, Smalltak and Lisp -- and combined them into one language with easy syntax. One goal was to make Ruby feel “natural, not simple” and to create a language “that was more powerful than Perl, and more object-oriented than Python.” This results in Ruby's core principle: Everything is an object.</p>

### Objects

Let's stop here and examine this. Really, <strong><em>everything</em> is an object in Ruby</strong>. <code>True</code> and <code>false</code> are objects, literals are objects, classes are objects. You can call a method on a numeric literal:

<pre><code class="language-markup tmp-ruby">&gt;&gt; 5.next
=&gt; 6</code></pre>

Operators in Ruby are nothing but methods:

<pre><code class="language-markup tmp-ruby">&gt;&gt; 5 * 10
=&gt; 50
&gt;&gt; 5.*(10)  # times-operator called as a method (dot-notation)
=&gt; 50       # with a parameter (in parentheses)</code></pre>

Ruby is extremely flexible and open. Almost everything about it can be changed or manipulated at runtime:

*   You can add and remove methods and variables to and from objects.
*   You can add and remove methods and variables to and from classes.
*   You can truly manipulate _any_ class this way, even core classes like `String` and `Integer`!

Here's an example:

<pre><code class="language-markup tmp-ruby">&gt;&gt; "hi".repeat(4)
NoMethodError: undefined method `repeat' for "hi":String
&gt;&gt; class String     # Open the string class and add the method
&gt;&gt;   def repeat(i)
&gt;&gt;     self * i
&gt;&gt;   end
&gt;&gt; end
=&gt; nil
&gt;&gt; "hi".repeat(4)   # Call it again on a fresh String literal
=&gt; "hihihihi"       # And there it is!</code></pre>

Here, I defined the method <code>repeat</code> on the String core class, and it was immediately available on a string literal.

And he who giveth, taketh away:

<pre><code class="language-markup tmp-ruby">&gt;&gt; class String             # Open up the method again
&gt;&gt;   undef_method :repeat   # And remove the method
&gt;&gt; end
=&gt; String
&gt;&gt; "hi".repeat(4)           # Try to call it
NoMethodError: undefined method `repeat' for "hi":String</code></pre>

I could have also done this with predefined methods. They are no more “special” than the methods we have defined.

Let's review the definition of <code>repeat</code> in the above example for some more interesting tidbits. Note that we're not saying <code>return</code> anywhere in the body. That is because in Ruby, <strong>methods always implicitly return the value of their last expression</strong>. You could of course always jump out of a method by using <code>return</code> before reaching the last statement, but you don't have to. The expression we're returning is <code>self * i</code>. <code>Self</code> is equal to <code>this</code> in Java and <code>$this</code> in PHP and always refers to the current object. The times-operator on a string repeats the string as often as told by the second operand/parameter, <code>i</code> in this case.</p>

### Loops

You rarely see manual iterations in Ruby, like <code>for</code> or <code>while</code> loops. Instead, Collections come with their own iterators that you can pass blocks to, which are executed for every element in the collection:

<pre><code class="language-markup tmp-ruby">a = "Hey "
[1, 2, 3].each do |num|
    puts a * num
end

# Outputs:
# Hey
# Hey Hey
# Hey Hey Hey</code></pre>

What you see here is an array literal containing numbers. On that array, the <code>each</code> method is called, an iterator that takes a block and calls the block for every element in the array. The block starts with the <code>do</code>, followed by a list of its parameters enclosed in pipe symbols. Here we have one parameter called <code>num</code> that will take on the value of the array element in each iteration. Inside the block, we're simply outputting the result of a * num. The definition of <code>*</code> on Strings is to repeat the string accordingly. We could have put the String inside the Block, but I wanted to demonstrate that blocks have access to their surrounding scope.</p>

### Syntax

Ruby likes to keep the syntax clean and friendly. You can see this in the above examples. Although heavily influenced by Perl, Ruby doesn't have Perl's excessive use of special characters. You can use semicolons to end lines, but you don't have to (and no Ruby programmer does). You don't need to surround method parameters with braces in unambiguous situations (although it is recommended you do so if they enhance readability), and you especially don't need to provide empty braces around an <em>empty</em> parameter list. That's what makes accessors look so much like native properties.

Blocks are framed by <code>do</code> and <code>end</code>. You should only use equivalent curly braces if your blocks don't span several lines. The only significant use of special characters is found at <strong>variable declaration</strong>. Variables in Ruby are prefixed with special characters to indicate their scope. Variables starting with a lowercase letter are local variables. Variables starting with an uppercase letter are constants. (This means that all classes are constants, too, since classes start with uppercase letters.) Instance variables start with an <code>@</code>. Class variables that are shared among all instances of a class start with <code>@@</code>. Finally, global variables all start with a <code>$</code>.

You'll often find methods ending in <code>?</code> or <code>!</code>. These are not special characters. It is merely conventional in Ruby to use question marks for methods that query an object for a Boolean condition, like <code>Array#empty?</code>, or exclamation marks for methods that are destructible:

<pre><code class="language-markup tmp-ruby">&gt;&gt; a = [5, 1, 9, 2, 7]   # Create an array and store it in a
=&gt; [5, 1, 9, 2, 7]
&gt;&gt; a.sort                # sort merely returns a new, sorted array
=&gt; [1, 2, 5, 7, 9]
&gt;&gt; a
=&gt; [5, 1, 9, 2, 7]       # a still is in its original order
&gt;&gt; a.sort!               # sort! instead sorts the original array
=&gt; [1, 2, 5, 7, 9]
&gt;&gt; a
=&gt; [1, 2, 5, 7, 9]       # a was changed</code></pre>

### Conditionals

Conditionals in Ruby are very similar to other programming languages, with two notable exceptions. First, it's possible to put a conditional <em>after</em> the statement it protects to make the code more readable:

<pre><code class="language-markup tmp-ruby">execute_dangerous_operation() if user.is_authorized?

# is equal to

if user.is_authorized?
  execute_dangerous_operation()
end</code></pre>

Secondly, Ruby has not only an <code>if</code> but an <code>unless</code>. This is a syntactic nicety for when you want to check for the <em>absence</em> of a condition in a more readable manner:

<pre><code class="language-markup tmp-ruby">unless user.is_admin?
  user.delete
else
  raise "Can't delete admins"
end</code></pre>

### Symbols

Sometimes you'll see names starting with a <code>:</code> (colon). These are a very special feature of Ruby called symbols. Symbols can be used to index hashes or mark states in a variable like you would with an ENUM in C. They are very similar to Strings but also very different. The point about symbols is that they don't really occupy space in memory, and the same symbol literal always resolves to the exact same symbol:

<pre><code class="language-markup tmp-ruby">&gt;&gt; "a".object_id  # object_id returns Ruby's internal identifier for an object
=&gt; 3477510
&gt;&gt; "a".object_id
=&gt; 3475550        # a new object on the heap
&gt;&gt; :a.object_id
=&gt; 184178
&gt;&gt; :a.object_id
=&gt; 184178         # the same literal refers to the exact same Symbol object</code></pre>

You'll find them very often as parameters to methods, where they indicate how a method should work,

<pre><code class="language-markup tmp-ruby">User.find(:all)   #find all users
User.find(:first) #find the first user</code></pre>

or as pointers to methods and variables (see the <code>undef_method</code> example in the "Objects" paragraph above).</p>

### Classes and Modules

Ruby supports single inheritance only, but for added flexibility it supports a feature called <strong>Mixins</strong>. In Ruby, it's possible to define <em>Modules</em> that contain Methods and constants and to include these modules in a class via the <code>include</code> method. This way, you can extend the functionality of a class very easily.

Many of Ruby's core classes even use this mechanism.<code>Array</code> and <code>Hash</code>, for example, both include the <code>Enumerable</code> module to provide a lot of convenience methods for iterating over their contents.

Often, Modules pose certain requirements to classes that include them. The <code>Enumerable</code> Module, for example, requires classes to provide at least an <code>each</code> method and an implementation of <code>&lt;=&gt;</code>, too, if its sorting features are to be used.

Modules also serve other purposes. Most importantly, they can be used to organize code into namespaces. Because classes are constants (which means you can't assign another class to the same name), they can be stored in modules. These modules can then be nested to form namespaces.

These paragraphs probably won't enable you to write Ruby programs, but you should be able to understand the code samples in this article now. If you want to explore Ruby a little, try the great interactive tutorial at Try Ruby, or take a peek at one of the books listed at the end of this article. If you just want to see some more code samples, check out the <a href="https://en.wikipedia.org/wiki/Ruby_(programming_language">Wikipedia page on Ruby</a>.

In the second part of this tutorial we will get rolling with Ruby on Rails, install the engine, take a closer look at Rails’ inner workings and discover main advantages of Ruby on Rails. Please stay tuned.

{{< signature "al" >}}

