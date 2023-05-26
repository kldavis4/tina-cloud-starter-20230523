---
title: Backpack Algorithms And Public-Key Cryptography Made Easy
slug: backpack-algorithms-and-public-key-cryptography-made-easy
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e7a57e1-39c0-4825-aa39-29225e69e2d8/backpack211.png'
date: 2012-05-17T10:04:45.000Z
author: zack-grossbart
description: >-
  E-commerce runs on secrets. Those secrets let you update your blog, shop at
  Amazon and share code on GitHub. Computer security is all about keeping your
  secrets known only to you and the people you choose to share them with.

  We’ve been sharing secrets for centuries, but the Internet runs on a special
  kind of secret sharing called public-key cryptography. Most secret messages
  depend on a shared secret—a key or password that everyone agrees on ahead of
  time. Public-key cryptography shares secret messages without a shared secret
  key and makes technologies like SSL possible.
categories:
  - Coding
  - Security
---
E-commerce runs on secrets. Those secrets let you update your blog, shop at Amazon and share code on GitHub. Computer security is all about keeping your secrets known only to you and the people you choose to share them with.

We’ve been sharing secrets for centuries, but the Internet runs on a special kind of secret sharing called public-key cryptography. Most secret messages depend on a shared secret—a key or password that everyone agrees on ahead of time. Public-key cryptography shares secret messages without a shared secret key and makes technologies like SSL possible.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [P Vs. NP: The Assumption That Runs The Internet](https://www.smashingmagazine.com/2015/11/p-vs-np-assumption-that-runs-internet/)
*   [Why Passphrases Are More User-Friendly Than Passwords](https://www.smashingmagazine.com/2015/12/passphrases-more-user-friendly-passwords/)
*   [The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
*   [Obfuscating Blacklisted Words In WordPress With ROT13](https://www.smashingmagazine.com/2014/12/encrypting-blacklisted-words-in-wordpress-with-rot13/)

Cryptography is a scary word: it conjures thoughts of complex equations and floating-point arithmetic. Cryptography does have a lot of math, but it’s more about keeping and sharing secrets.

{{% feature-panel %}}

## A Simple Secret

Telling my best friends a secret is easy: I find a private place and whisper it in their ears. As long as no one is listening in, I’m totally secure. But the Internet is full of eavesdroppers, so we need codes.

We’ve all been inventing codes since we were children. I created this simple number code (actually a cipher) when I was 5:

<pre><code class="language-javascript">
a=1, b=2, c=3, d=4, e=5…
</code></pre>

It fooled my friends, but not my parents. Simple substitution ciphers are based on a lack of knowledge. If you know how they work, then you can decode every message. The experts call this “<a href="https://en.wikipedia.org/wiki/Security_through_obscurity">security through obscurity</a>.” Letter and number substitutions don’t work on the Internet, because anyone can look them up on Wikipedia. For computer security, we need codes that are still secure even if the bad guys, or your parents, know how they work.

The most secure code is still easy to use: a “<a href="https://en.wikipedia.org/wiki/One-time_pad">one-time pad</a>.” One-time pads have been used for centuries, so they don’t even need computers. They played a big part in World War II, when each pad of paper with the key numbers was used only once.

Let’s say I wanted to send you this secret message:

<pre><code class="language-javascript">
I love secrets
</code></pre>

First, I’d turn the message into numbers using my simple cipher from when I was 5. (I’ve heard rumors that other people had this idea first, but I don’t believe it.)

<img loading="lazy" decoding="async" class="alignright size-full wp-image-118927" title="One-time pad step 1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0a0798c-81c2-4394-8fc2-4679898755f0/one-time-pad-1-2.png" alt="One-time pad step 1" width="582" height="118" />

Then I’d mash my keyboard to generate a random key string for my one-time pad.

<img loading="lazy" decoding="async" class="alignright size-full wp-image-118926" title="One-time pad step 2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a39758e4-9537-4a65-967e-0a3da1111bea/one-time-pad-2-2.png" alt="One-time pad step 2" width="582" height="126" />

Now I can add the two strings together. If my number is greater than 26, I would just wrap it around to the beginning. So, <code>i(9) + e(5) = n(14)</code>, and <code>o(15) + t(20) = i(35 - 26 = 9)</code>. The result is an encrypted string:

<img loading="lazy" decoding="async" class="alignright size-full wp-image-120060" title="One-time pad diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f9b19a9-cf93-48b9-8264-a01c85940175/one-time-pad2.png" alt="One-time pad diagram" width="562" height="375" />

Decrypting the string to get the secret back is easy. We just subtract the one-time pad: <code>n(14) - e(5) = i(9)</code>. Follow that pattern through the entire message, and you can securely share a secret. You don’t even need a computer: just work it out with a pen and paper.

This function is called a <a href="https://en.wikipedia.org/wiki/Symmetric-key_algorithm">symmetric-key algorithm</a>, or a shared-key algorithm, since it uses the same key to encrypt and decrypt the message. Modern systems can safely use the pad more than once, but the basic idea is the same.

The one-time pad is totally secure because the bad guys don’t know how we got the encoded letter. The <code>n</code> could be <code>i + e</code>, <code>j + d</code> or any other combination. We can use our shared secret (the one-time pad) once to share another secret.

But there’s a fatal flaw. We need to share the one-time pad ahead of time before we can start sharing secrets. That’s a chicken-and-egg problem because we can’t share the pad without worrying that someone will snoop. If the bad guys get the one-time pad, then they would be able to read everything.

One-time pads help me share secrets with my best friends, but I can’t use them with strangers such as Amazon or Facebook. I need a way to share something publicly that doesn’t compromise my one-time pad. I need a public key.</p>

## The Public-Key Backpack

Public-key encryption focuses on a single problem: how do I prove that I know something without saying what it is? An easy concept to help us understand this is a <a href="https://en.wikipedia.org/wiki/Knapsack_problem">backpack full of weights</a>.

<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-120066" title="Backpack algorithm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e665392f-ac8f-40f6-a162-8f806f2d43b8/backpack2.png" alt="Backpack algorithm" width="500" height="262" />

I want to prove that I know which weights are in my pack, but I don’t want to tell you what they are. Instead of showing you all of the weights separately, I’ll just tell you the total. Now you can weigh the pack and see if I’m right without ever opening it.

If the pack weighs 20 kilos, then you wouldn’t know if it has one 20-kilo weight, twenty 1-kilo weights or something in between. With a large number, you can be pretty confident that I know what’s in the pack if I know the total; you don’t have to see inside. The weight of the backpack is the public part, and the individual weights are the private part.

This basic backpack enables us to share a secret without really sharing it. If we each have a backpack, then we can both share secrets.

The backpack works well enough for smaller numbers, but it isn’t useful in the real world. Backpack algorithms were a mere curiosity for decades. Then <a href="https://en.wikipedia.org/wiki/RSA_(algorithm)">RSA</a> changed everything.</p>

## RSA

RSA was the first public-key encryption system that worked in the real world. Invented more than 30 years ago, it coincided with the introduction of the more powerful computers that were needed to run the big numbers. RSA is still the most popular public-key encryption system in the world.

The basic premise of RSA is that <a href="https://en.wikipedia.org/wiki/Factorization">factoring</a> large numbers is difficult. Let’s choose two <a href="https://en.wikipedia.org/wiki/Prime_number">prime numbers</a>: 61 and 53. I’m using the numbers from Wikipedia’s article on “<a href="https://en.wikipedia.org/wiki/RSA_(algorithm)#A_working_example">RSA</a>” in case you want more details.

Multiply these two numbers and you get 3233:

<pre><code class="language-javascript">
61 × 53 = 3233
</code></pre>

The security of RSA comes from the difficulty of getting back to 61 and 53 if you only know 3233. There’s no good way to get the factors of 3233 (i.e. the numbers that multiply to make the result) without just <a href="https://en.wikipedia.org/wiki/Proof_by_exhaustion">looking for all of them</a>. To think of this another way, the weight of our backpack is 3233 kilos, and inside are 61 weights weighing 53 kilos each. If you make the resulting number large enough, then finding the numbers that produced it would be very difficult.

## Public And Private Keys

<img loading="lazy" decoding="async" class="alignright size-full wp-image-118921" style="float: right;" title="Public-key encryption diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545b4bcc-41b0-494f-9637-f69c9a353bfe/pke.png" alt="Public-key encryption diagram" width="310" height="507" />
Unlike the one-time pad, RSA uses the public key to encrypt information and the private key to decrypt it. This works because of the special relationship between the public and private keys when they were generated, which allows you to encrypt with one and decrypt with the other.

You can share the public key with anyone and never reveal the private key. If you want to send me a secret message, just ask for my public key and use it to encrypt the message. You can then send it to anyone you want, and you’ll know that I’m the only one who can decrypt the message and read it.

I could send you a message in the same way. I would ask for your public key, encrypt the message using it and then send it to you to decrypt. The popular program <a href="https://en.wikipedia.org/wiki/Pretty_Good_Privacy">Pretty Good Privacy</a> (PGP) worked like that. We’re secure as long as we both keep our private keys private.

Exchanging keys is made even easier by special key servers that allow you to search for people and find their public keys.

Public-key encryption also works in reverse to provide digital signatures. Let’s say I want to write a message and prove that I wrote it. I just encrypt it with my private key and post it. Then anyone who wants to check can decrypt it with my public key. If the decryption works, then it means I have the private key and I wrote the message.

RSA is relatively simple: take two numbers (the private key), apply some math, and get a third number (the public key). You can write out all of the math in a few lines, and yet RSA changed the world. Business doesn’t work on the Internet without public-key encryption.</p>

## RSA And HTTPS

We use public-key encryption every day with <a href="https://en.wikipedia.org/wiki/Secure_Socket_Layer">HTTPS</a>. When you access Facebook, Twitter or Amazon with HTTPS, you’re using a simple encryption mechanism like the one-time pad, but you’re creating the pad with public-key encryption. Without HTTPS, anyone else at Starbucks could read your credit-card number, Facebook password or private email while sipping a latte.

Amazon has a certificate from a company named <a href="https://en.wikipedia.org/wiki/Verisign">VeriSign</a>. The certificate certifies that Amazon is Amazon, and it contains its public key. Your browser creates a special key just for that session and encrypts it using Amazon’s public key. Then it sends it over the Internet, knowing that only Amazon can decrypt the session key. Once you’ve exchanged that secret key, you can use it as the one-time pad to protect your password and credit-card number.

<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-118922" title="SSL key exchange diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ba0a2c-a188-4948-a11a-5bc65c5cf304/ssl.png" alt="SSL key exchange diagram" width="582" height="374" />

You could keep using public-key encryption for the whole session, but because of all the math, it’s much slower than the one-time pad.</p>

## RSA And GitHub

Another place many of us use RSA is <a href="https://github.com/">GitHub</a>. Every time you push a change to GitHub or pull from a master branch, GitHub has to make sure you have permission to make the change. It gets its security through a <a href="https://en.wikipedia.org/wiki/Secure_Shell">secure command shell</a> using RSA.

Remember when you set up your GitHub account and followed some commands to generate keys?

<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-118919" title="GitHub key generation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9aaaf5-8ca2-4b1a-a688-c804c6b8a1cf/github-key.png" alt="GitHub key generation" width="557" height="308" />

You used the <a href="https://en.wikipedia.org/wiki/Ssh-keygen">SSH-Keygen</a> tool to generate a new RSA private/public key pair. Then you went to your GitHub account page and entered your public key.

Now, when GitHub needs to authenticate you, it asks your computer to sign something with your private key and return the signed data. With your public key, GitHub can confirm that the signature is authentic and could only have been produced by someone who has the corresponding private key—even though GitHub itself doesn’t have that private key.

That’s better than a simple password because nobody can snoop it. And if GitHub ever gets hacked, your private key won’t be in danger because only you have it.</p>

### Sharing Passwords

When <a href="https://techcrunch.com/2011/06/21/wordpress-org-possibly-hacked-forces-password-resets">WordPress.org was “hacked”</a>, it wasn’t really hacked. WordPress plugin developers, like everyone else, have accounts on other websites. They also reuse their passwords. When hackers cracked those other websites, they used the stolen passwords to log into WordPress.org and make malicious changes to plugins.

Most people use the same user name and password on multiple websites. That makes your website only as secure as everyone else’s. Public-key encryption changes that. Because you never have to share your private key, it doesn’t matter if other websites get hacked. If an attacker breaks into GitHub and gets your public key, they can’t use it to impersonate you or log in as you on other websites. Only someone with your private key can do that, which is why your private key remains safe on your computer. Using public-key cryptography makes GitHub much more secure.</p>

### GitHub Gets Hacked

GitHub was <a href="https://www.extremetech.com/computing/120981-github-hacked-millions-of-projects-at-risk-of-being-modified-or-deleted">hacked recently</a>, but not because the encryption failed. Real-world security breaches are caused by problems in implementation, not in math.

In this case, the hacker was able to exploit a hole and add his public key to the <a href="https://github.com/rails/rails">Ruby on Rails repository</a>. Once the key was added, GitHub used it to verify the hacker’s identity and granted him access. We’re lucky this hacker was friendly and told GitHub about the issue.

Once the problem was fixed, you could keep using your private key because GitHub never had it to lose; it stayed on your machine. Public keys saved GitHub from serious problems.

The weakest link in GitHub’s security was in the mechanism that allowed clever users to add public keys to other projects without being authorized. The math was perfect, but the implementation wasn’t.</p>

## Public Keys In The Wild

Knowing the fundamentals is essential (you might say the <em>key</em>) to writing secure applications. The math is complex, but the basics are simple:

*   There are two main types of encryption: shared-key encryption, such as a one-time pad, and public-key encryption, which uses public and private keys.
*   Shared-key encryption is faster, but sharing the keys is difficult.
*   RSA is the most popular public-key encryption algorithm, but a few others are in general use, as well as some cool [experimental systems](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography).
*   Public-key cryptography works best in combination with other technologies.
*   Don’t ever share your private key with anyone.

When it comes time to implement public-key cryptography in your application, don’t. RSA and other algorithms are already implemented in all major languages. These libraries include extra security features such as <a href="https://en.wikipedia.org/wiki/Padding_(cryptography)">padding</a> and <a href="https://en.wikipedia.org/wiki/Cryptographic_salt">salts</a>, and they have a lot of testing behind them.

Most security flaws come from poor implementations and misunderstanding about the libraries. You don’t have to write your own cryptography libraries, but you do have to know the fundamentals so that you can use the ones that are out there.

<em>Illustrations in this article were provided by Robb Perry.</em>

<em>(al) (km)</em>

