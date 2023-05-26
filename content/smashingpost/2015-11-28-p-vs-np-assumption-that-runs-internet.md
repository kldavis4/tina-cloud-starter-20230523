---
title: 'P Vs. NP: The Assumption That Runs The Internet'
slug: p-vs-np-assumption-that-runs-internet
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3784dcc-6a6c-49f8-ad1f-20c9ec39018d/04-map-1-opt-43.png
date: 2015-11-28T00:11:17.000Z
author: zack-grossbart
description: >-
  Let’s get a few things out of the way first. **This isn’t your regular
  Smashing Magazine article**. It’s not a “how to“; it won’t show you how to
  build a better menu or improve your project tomorrow. This article shows you
  how a core problem in computer science works and why we're all pretending we
  know something for certain when we really have no idea.

  You’re looking at Smashing Magazine right now because you’re standing on the
  shoulders of a **giant assumption called "P versus NP"**. It’s a math problem
  that protects governments, runs the Internet and makes online shopping
  possible.
categories:
  - Coding
  - Performance
  - Security
---
Let’s get a few things out of the way first. **This isn’t your regular Smashing Magazine article**. It’s not a “how to“; it won’t show you how to build a better menu or improve your project tomorrow. This article shows you how a core problem in computer science works and why we're all pretending we know something for certain when we really have no idea.

You’re looking at Smashing Magazine right now because you’re standing on the shoulders of a **giant assumption called "P versus NP"**. It’s a math problem that protects governments, runs the Internet and makes online shopping possible.

You may have never heard of P versus NP, but this article will walk you through it, show you how it works and **explain why it matters**. There’s a little math, but don’t worry; it’s all pretty easy.

P versus NP is a mathematical question masquerading as a philosophical one. It describes the **difference between solving a problem and knowing whether you’ve solved it**. Let’s start with a simple example known as the "traveling salesman" problem.

Our salesman is walking through a town with houses spread across a number of streets. He needs to visit every house once and only once. The salesman wants to find the fastest route that takes him to every house but requires as little walking as possible.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5541cd3e-8da1-414c-a8fa-44c55acaceb9/01-map-base-opt.png" alt="Travelling salesman map" /><figcaption>Our travelling salesman and the map of houses he has to visit.</figcaption></figure>

The salesman doesn’t know whether it’s better to start from the upper right, or to walk to the middle first, or to walk around the town and start from the other side. The only way he can know for sure is to try each route and measure how long it takes. There’s no formula he can follow to figure out the fastest route; he has to find the answer with brute force. Finding the answer is the “NP” part, which we’ll define soon.

Knowing whether he’s found the answer is easy. If he’s visited each house, then he’s done the job; if he’s skipped one, then he has to start over. That’s the “P” part. All P versus NP problems are tough to solve but easy to verify.</p>

## Yeah, There Are Some Big Words

The “P” in P versus NP stands for **polynomial** time. That just means we can predict the maximum amount of time it will take to solve the problem. The classic example of polynomial time is a quick sort. Here’s a set of blocks:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab4db2d1-0aee-4fac-8fad-466870b61378/02-messy-blocks-opt.png" alt="Starting point of quick-sort algorithm" /><figcaption>Starting point for a quick-sort algorithm. (Image: <a href="https://commons.wikimedia.org/wiki/File:Sorting_quicksort_anim.gif">RolandH</a>)</figcaption></figure>

We want to sort them in order from shortest to tallest. The easiest way to do that is by dividing the group in half, pushing the tall blocks to the right and the short blocks to the left. Then, we’d cut each half in half, and repeat.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/160859b0-954c-44c7-b486-de69422ecc1c/03-sorting-quicksort-anim.gif" alt="Animation of the quick-sort algorithm"/><figcaption>The quick-sort algorithm in action. (Image: <a href="https://commons.wikimedia.org/wiki/File:Sorting_quicksort_anim.gif">RolandH</a>)</figcaption></figure>

There’s an algorithm that will tell us how long this will take. It doesn’t matter how many blocks we have or how disorganized they are, **we can always predict the worst-case scenario** for how long it will take to sort any number of blocks. The predictable part is what makes it take only polynomial time. All of the common math we use — addition, algebra, balancing your checkbook — can be done in polynomial time.

NP stands for **nondeterministic polynomial** time. It’s basically the opposite of P: There’s no equation or formula to predict how long it will take to solve a problem. Normally, the only way to solve this kind of problem is to keep trying answers until we find one that works. Figuring out the best route for our salesman is an NP-complete problem.

Let’s look at a few routes our salesman could take. He could start from the top and go down the left:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a0920d1-8554-4015-9a54-6a3f17093bc8/04-map-1-opt.png" property="image" alt="The first potential travelling salesman solution" title="The first potential travelling salesman solution" /><figcaption>The first route our travelling salesman tries to visit all of the houses.</figcaption></figure>

That’s about 75 steps. He could also start by walking to the middle and looping around counterclockwise:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e4911f-b953-4f8f-8a60-04adc8992b9a/05-map-2-opt.png" alt="The second potential travelling salesman solution" title="The second potential travelling salesman solution" /><figcaption>The second route our travelling salesman tries to visit all of the houses.</figcaption></figure>

That one’s about 95 steps. The salesman could also turn the map around and start from the top right. Now he can avoid looping all the way around:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ceef0aa-dbd7-4023-9d6a-9da6184d941f/06-map-3-opt.png" alt="The third potential travelling salesman solution" title="The third potential travelling salesman solution" /><figcaption>The third route our travelling salesman tries to visit all of the houses.</figcaption></figure>

That route’s about 80 steps.

While we can measure each route to see which is shortest, there’s **no way to tell the lengths without trying them out**. We can make guesses, but pretty soon we just have to start walking. The traveling salesman problem is famous because visiting every house along the shortest route is NP (very difficult), but making sure to visit every house is P (very easy).

We could figure out this map in a few minutes, but adding a few more houses would make the solution take hours. Add enough houses and the solution would take years.</p>

## Why This All Matters

The traveling salesman is a cute problem, but the implications are giant.

**Change the salesman to a page request** and the houses to servers and you’ve got Internet packet routing. When my computer in Boston wants to send requests to a computer in London, it has to figure out a path to get there by bouncing from one server to another along the way. The data could take thousands of different routes through thousands of different computers in between Boston and London. Finding the fastest route is a bigger version of our salesman problem.

Google, Facebook and Apple try to make the problem easier by building data centers near major cities. They’re trying to make the map smaller when people make requests.

If you could figure out a better way to route data on the Internet, you could make stock trades faster than everyone else and [make billions of dollars](https://en.wikipedia.org/wiki/Flash_Boys).

Another version of this problem is all about secrets.

Most of the Internet runs on secrets. I want to give my credit-card number to Amazon, but not to the guy sitting next to me at Starbucks. I don’t want to share my bank password with my neighbours, and I don’t want to let my frenemies read my email. You can shop, share and work on the Internet because of secrets, and all of those secrets are based on math.

Most of the secrets on the Internet are protected by [public-key cryptography](https://www.smashingmagazine.com/2012/05/17/backpack-algorithms-and-public-key-cryptography-made-easy/). That cryptography is based on finding two large numbers that, multiplied together, equal a very large number. The two large numbers are **factors** of the very large number. (Think of a backpack full of weights. You may know that the pack weighs 10 kilograms, but you don’t know whether it has one 10-kilogram weight, 10 one-kilogram weights or anything in between.)

For example, take the number 26\. It has four factors: 1, 2, 13 and 26\. Every number contains 1 and the number itself, so we’ll ignore those factors; the important ones are 2 and 13.</p>

<pre><code>2 &#215; 13 = 26</code></pre>

You can find the factors of 26 by trying every number between 1 and 26\. It’s a lot tougher with a mindbendingly large number like:

<pre>33478071698956898786044169848212690817704794983713768568912431388982883793878002287614711652531743087737814467999489</pre>

Can you find factors of that number? I’ll give you one answer.</p>

<pre><code>36746043666799590428244633799627952632279158164343087642676032283815739666</code></pre>

and

<pre><code>511279233373417143396810270092798736308917</code></pre>

Those numbers are dizzyingly large. You could never work them out on a piece of paper, and neither could a computer. There’s no good way to write a computer program to find the factors of large numbers quickly. The best you can do is to discard the numbers that clearly don’t work, and then search for factors one by one among the trillions and trillions of numbers remaining. Finding factors is an NP problem.

I had to work hard to find those factors (well, I looked them up on Wikipedia, but someone worked hard to find them). Making sure I’m right is easy. You could write a small computer program to multiply the second and third numbers. If they produce the first number, then I’m right and they are factors. Your job is simple; this is a P-level problem.

If finding those factors were easy, then the Internet would fall over.

## P Vs. NP

Having a secret is not very useful if I can’t prove I have it, but I can’t just tell you the secret because then it wouldn’t be a secret. I need to prove that I know the value without telling you what it is. That’s where the factors come in. The larger first number proves that I know the factors without ever telling you what those numbers are. Take a look at “[Backpack Algorithms and Public-Key Cryptography Made Easy](https://www.smashingmagazine.com/2012/05/17/backpack-algorithms-and-public-key-cryptography-made-easy/)” if you’re interested in how the factoring turns into cryptography.

If you could come up with a way to quickly find large factors, then you could steal my secrets. Robert Redford starred in a [movie about this](https://www.imdb.com/title/tt0105435/).

Many smart people have been working on a way to find those factors, and they haven’t found one yet. We’ve based the entire security of the Internet on the “fact” that there’s no easy way to find the factors of large numbers, but it isn’t really a fact. We don’t know whether a fast way to find factors or get directions for our salesman exists. Maybe it’s out there and we just haven’t found it yet. Maybe someone will find it tomorrow. That’s what P versus NP is all about.</p>

### P ≠ NP

Right now we assume that P does not equal NP. This means that some problems are easy and others are hard. We think our secrets are safe, but we can’t prove it.

Mathematics is based on a lot of assumptions. Some of those assumptions last decades before being proved true or false. As long as the assumption that P doesn’t equal NP remains true, then we can keep sharing secrets, email and credit-card numbers on the Internet without any problems. If you proved that P does equal NP, then you could cause some big trouble.</p>

### P = NP

Some people make the philosophical argument that P just can’t equal NP. If it did, then it would mean that finding the solution to a problem has always been as easy as verifying that the solution is correct and that factoring our large numbers is easy. That would break all public-key cryptography on the Internet. SSL would stop protecting anything, and you could never give your credit card safely to anyone.

It has even larger implications. If P equals NP, then you could solve anything as easily as you could verify it. Anyone who could drive a car could build one, and anyone who could listen to a symphony could write one. This makes my head hurt, but it’s not the real problem.

If you could create a practical example of P equaling NP, then you could solve the traveling salesman problem and change the entire way that Internet routing works. And that’s just the beginning.

A practical solution proving that P equals NP would give you enormous control over information everywhere.</p>

## What Comes Next?

Basing the whole Internet on an assumption is scary. We want to know whether or not P equals NP. The answer has practical applications, but it also asks a larger question about how we figure things out. Do we know them first and figure them out second, or do we need to work at a solution before we can find it?

Some problems are hard and some just look hard. P versus NP gives us a framework to figure out which is which.

If you can prove P versus NP one way or the other, you’d [win a million dollars](https://en.wikipedia.org/wiki/Millennium_Prize_Problems#P_versus_NP).

{{< signature "da, ml, al" >}}

