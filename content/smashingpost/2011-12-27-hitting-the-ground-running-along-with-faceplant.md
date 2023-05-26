---
title: Teach Them How To Hit The Ground Running And Faceplant At The Same Time?
slug: hitting-the-ground-running-along-with-faceplant
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb8c2571-95e6-4464-a399-d9062dc1c372/teach-them-illu.png
date: 2011-12-27T21:14:51.000Z
author: christian-heilmann
description: >-
  A few days ago, a tutorial on how to [Create A Christmas Wish List With
  PHP](https://www.smashingmagazine.com/2011/12/22/create-a-christmas-wish-list-with-php/)
  was published on Smashing Magazine's _Coding_ section that frustrated me. It
  frustrated me as it was incredibly easy to predict the comment reactions it
  caused. It also frustrated me as it was a classic example of a tutorial
  resulting in very happy readers who will go out and cause a lot of terrible
  things on the Web unless they understand that this was meant as a "beginner
  tutorial". A lot of the bad feedback was about security — something we
  shouldn't take lightly.
categories:
  - Tutorials
  - Opinion Column
  - Community
  - Coding
---
A few days ago, a tutorial on how to [Create A Christmas Wish List With PHP](https://www.smashingmagazine.com/2011/12/22/create-a-christmas-wish-list-with-php/) was published on Smashing Magazine's _Coding_ section that frustrated me. It frustrated me as it was incredibly easy to predict the comment reactions it caused. It also frustrated me as it was a classic example of a tutorial resulting in very happy readers who will go out and cause a lot of terrible things on the Web unless they understand that this was meant as a "beginner tutorial". A lot of the bad feedback was about security — something we shouldn't take lightly.

It frustrated me mostly because it all happened on Smashing Magazine, a well-respected online publication that is read by many beginners (especially in back-end technologies) and one that is dedicated to quality content with an advisory board (one of which is me) meaning that **every article gets reviewed by experts** before it is published. This one slipped by in the rush of the holidays, and it was updated a couple of hours after it was published, i.e. the editors added an editor's note and addressed some important missing points. I am happy that it was published in its original form as it inspired me to point out some things that I see happening in online magazines a lot lately.

The predictable outcome of this kind of tutorial is:

*   Seasoned developers will find issues with the code and claim that it should not be done that way.
*   Other people will disagree and tell the old men to stop telling young kids to get off their lawn.
*   Real beginners will chime in and say that they are very happy about the article and getting the feeling that things are not as complex as they seem to be.
*   A lot of fanboys will mention technology XYZ that makes this much easier.
*   The author will add more disclaimers about the nature of the code within the article with some edits and add warning messages about its viability in the wild — saying that this is just demo code.</p>

## Quick Wins Full Of Traps

"Quick tutorials for beginners" are killing our craft. Instead of pointing to existing documentation and keeping it up to date (in the case of the wiki-based docs out there) every new developer turned to an author wanting the fame for themselves. And a lot of online magazines cater to these to achieve "new" content and thus visitors. We measure our success by the number of hits, the traffic, the comments and retweets. And to get all of that, we want to become known as someone who wrote that "very simple article that allowed me to do that complex thing in a matter of minutes".

{{% feature-panel %}}

[![Teacher/Learner](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48dfb905-ce2a-4dce-9f5d-b4e026d1917f/teacher-learner.jpg "Teacher/Learner")](https://www.flickr.com/photos/opensourceway/5538035618/)  
_Image credit: [Opensourceway](https://www.flickr.com/photos/opensourceway/5538035618/)._

Instead of teaching the underlying technology, we tend to show a quick, beautiful implementation and put a lot of effort into it. We teach a "create something amazing in 5 minutes" and hope people will care enough afterwards and look at learning the underlying technologies. We aim to whet their appetite whilst giving them full solutions. The reason is that this is exactly what we wished we had had when we learned that thing in the first place. Sadly, **this is not how teaching and learning works**.</p>

## Road Safety Begins In A Classroom

At this moment, let me go back in time a bit. Growing up in a small village having a driving license and subsequently a car was a vital part of your social life and also your work options. Therefore, I couldn't wait to get mine.

Now, what you want to do is to learn driving. You want to get into the car, go vroom-vroom and be off. The **reality of getting a driving license** though (at least in Germany where there are no speed limits on the motorway and therefore it is taken very seriously) is that you spend quite a lot of evenings in a boring classroom before you get behind the wheel. You learn about the code of the street, the different signs and what to do in all kind of situations in a car. You even learn about the different parts of the car and what they do.

The reason is that it scales better — you need to learn all that stuff and it is much easier to pack 40 students in a room to teach the basics before you try to make up a schedule where all of them can drive out on the road. As a driving school, instead of 40 cars you can get by with 5\. And students who already know what they should _not_ do and where things are in a car are less likely to crash them.</p>

### Educators Learning From Bad Experiences?

This is frustrating and annoying, the same way learning things at school without being told **what they are good for** is surely annoying. On the Web, we want to be different. We want to make learning fun and we are tempted to put in as much as possible for beginners so they can get past the basics very quickly and build the awesome of tomorrow instead. The author actually mentions that in the comments:

<blockquote>"I think teaching people to do things is very complicated, doubly so over the internet. If I were teaching a university class I would take a very different approach."</blockquote>

Yes, teaching is hard. That's why not every gifted developer is also good at explaining or a good trainer.

While it is a very good idea in our heads to give people quick solutions with real results instead of step-by-step basics, we forget _how_ we actually got there. Once we reached the level in a skill to be educators in it, we went through a lot of trial and error using the skill. By avoiding this, we strip others of the chance to learn a skill on their _own_ terms and with their _own_ obstacles to overcome.</p>

### How About Writing Beginner Tutorials Covering Beginner Tasks?

So, I think it is safe to assume that there are two needs/aims battling when we want to write a beginner tutorial, i.e. we want to teach people good practices and we want to get them as far as possible with the least effort. A lot of times these don't go well together.

jQuery is a poster child of great "new" Web development. "**Write less, achieve more**" is the mantra and I love that we have it. jQuery achieved this by replacing JavaScript and the unwieldy DOM with a clever and fast API and a totally new syntax: chaining. This is great. This is how to do it. jQuery abstracts the annoyances and complexities out into its core and lets developers write code. You cannot just take this approach and mantra and apply it to any technology without providing a simpler API/platform that abstracts the dangers and annoyances.</p>

## Teaching Non-Live Code On The Web?

The discussion that happened in the comments of the aforementioned article was mostly about security and the inability of implementing the code discussed in it in a real environment. And yes, they are very much valid. The code is good as an exercise but awful as a live example. Putting it on an live server means you are open to any kind of attacks and scripts looking for zombies to infect — not to mention how a botnet would have a field day with it!

And the author knows this. This is why a lot of the article is dedicated to explaining that this is not live code:

<blockquote>"Please notice that this article was written for beginners who already grasp HTML and CSS, know a bit of PHP and have seen phpMyAdmin before. I will not go into best practices, safety and all the rest of it; let’s just have fun with this one!"</blockquote>

And later on — as a response to some feedback, even more "don't do this" was added:

<blockquote><p>"Note that this is meant as a beginner’s exercise. The code you see here will give you the intended result, but a lot of it is not safe for production websites. It lacks a lot of safeguards, such as data validation, salts for passwords (for better security), htaccess rules and so on. The goal of this article is to let beginners forget about all of these things and just concentrate on building something nice.</p>

<p>Neither does this article promote best practices. You may find yourself adopting different methods later on, or I may write in another article that we shouldn’t do something you see here. The article is intended as a fun little example for beginners to spice up their boring theory sessions. I believe that the best way to learn is through increasingly difficult examples.</p>

<p>That said, I encourage you to try all of this out and play around with it at home or on your servers. If you put this on a live server, I recommend using an account that has only this website on it (or only test websites). I also recommend using passwords for user accounts that are not the same as your other passwords."</p></blockquote>

This, actually very much is against the very idea of a beginner tutorial. A beginner tutorial gets people on the way, i.e. it teaches them the first steps and what one can do with it. As these quotes show, teaching people PHP by starting with SQL and writing a login system and file uploader is obviously the wrong way.

Out of a sudden, the simple beginner tutorial is "intended as a fun little example for beginners to spice up their boring theory sessions" (cited). What boring theory sessions? I thought we are building something from scratch here?

## Piling On Too Much

The article tries to teach four things at once: SQL with PHP, login and session control, file uploads and how to build a beautiful Web interface powered by PHP. The login system and the file upload is where it gets very dangerous in terms of security. This is not a beginner tutorial — it is giving beginners the **wrong impression that everything is easy** and everybody else probably just does it wrong and cares far too much about boring details.

 We should not teach new developers that they can do things in a few lines of code and keep quiet about the bad effects this has. This is condescending and based on an assumption that people learn only from successes on the Web. The author mentions that in the comments:

<blockquote>"I don’t think beginners need to concern themselves with SQL injection attacks. The point here is to start to learn something, not to learn everything at once. When someone understands SQL at all, then teach them about the problems, not before."</blockquote>

 This is very dangerous thinking — if you teach how to do something, also make people aware of the consequences it has. I totally agree that the point is to learn something. Defining the "something" is the skill of a good tutorial writer or educator. We focus far too much on the final product to be built, rather than the components we use to get there.

This is where using a complex example like a "Christmas Wishlist" that needs a login, uses a database and has an upload feature for any file is a bad choice. There is no way to keep this "simple" unless you teach people how to write code exclusively for their own localhost.</p>

### Let's Not Assume That People Read And Care As Much As We Think They Do

One comment was quite interesting as a summary, as it very much sums up some of the comments and assumes good on the side of the readers:

<blockquote>"Good stuff just to have some fun and help the super beginners get a quick footing. I think a lot of the people commenting here are either A) Too seasoned to look this far back, and not doing things the “proper” way just irks them, or B) I’d be willing to bet some are just flexing their programmer’s ego a bit.

I think assuming that people will take this as serious programming and build from it, building the wrong way, is a bit too much of a stretch. Anyone who can read and who cares about doing things the right way will take the author’s disclaimer to heart. If not, odds are they’re looking for the easy route. If that’s the case, you can’t really stop them. This article isn’t ending the world."</blockquote>

I agree, it is not. But it also brings nothing new to the table. When I learned PHP coming from Perl in around 2000, I read thickbook.com and — except for the CSS styles — it had similar examples. Over the years we learned to protect our systems more. I think the assumption that readers will care much about the "this is not live code" doesn't cover one main use case of "beginner tutorials", i.e. that people will most probably find the article via a Google search and simply use the code example in a live environment without reading the tutorial or the comments. All they wanted was a quick, simple to understand example after all and beginner tutorials have those, right?

[![In My Humble Opinion](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51d3d656-f994-4499-b2af-68e9afff7f7a/imho-screenshot.jpg "In My Humble Opinion")](https://www.flickr.com/photos/opensourceway/4586670229/)<br /><em>Image credit: <a href="https://www.flickr.com/photos/opensourceway/4586670229/">Opensourceway</a>.</em>

Want proof of that? Look at the success of W3Schools.com. The Web is full of materials to learn the same things. The quick "here's the solution — don't worry about how it works right now" are the most successful ones. We also have a Web full of systems that lack very basic quality and security features and we spend months educating hires in companies what developing production code means when you protect the data of our users.

I think it is time to stop chasing the hollow success of creating a "quick tutorial" that is actually a "bad implementation with quick, sloppy code" in disguise and start curating what is already on the Web. We can then concentrate on the next level tutorials.

I think Web-based education will be a big thing in the near future, and creating [a new generation of Web makers](https://commonspace.wordpress.com/2011/08/31/generation-of-web-makers/) should be on all of our agendas. We do this with tools, great documentation and frameworks, and not with a "write this, it is awesome" approach.

{{< signature "il" >}}

