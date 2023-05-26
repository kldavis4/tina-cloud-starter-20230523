---
title: A Better Way To Request App Ratings
slug: a-better-way-to-request-app-ratings
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5c2e474-12f0-4d62-bf00-f8a20af7bc90/ideal-ratings-500-opt.png
date: 2014-06-26T22:00:36.000Z
author: joshua-mauldin
description: >-
  No one really wants to be interrupted, much less for something silly while
  they’re in the middle of doing a billion things. So, why do app ratings follow
  this pattern? And why don’t developers attempt to talk more with their
  customers?
categories:
  - Mobile
  - Business
  - Apps
  - UX
  - Design
---
No one really wants to be interrupted, much less for something silly while they’re in the middle of doing a billion things. So, why do app ratings follow this pattern? And why don’t developers attempt to talk more with their customers?

In this article, we’ll investigate the various tactics of prompting for app reviews and ratings and how to make them better. We’ll also talk about how to ask users for feedback in a way that benefits everyone.</p>

<strong>Getting feedback on your app is important.</strong> How else can people tell you that your app is doing well or poorly? I’ve seen some great ways to prompt for reviews, and a few apps get it right, but there’s still room for improvement.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Keeping Your Android App Popular After Launch](https://www.smashingmagazine.com/2015/10/keep-your-android-app-popular-after-launch/)
*   [Lessons Learned From An App Graveyard](https://www.smashingmagazine.com/2013/11/lessons-from-an-app-graveyard/)
*   [Improving Reviews And Testimonials Using Science-Based Design](https://www.smashingmagazine.com/2016/02/improving-reviews-testimonials-using-science/)
*   [How To Engage Customers In Your E-Commerce Website](https://www.smashingmagazine.com/2010/06/engage-customers-in-your-business/)

{{% feature-panel %}}

The reason why app store reviews aren’t as effective as they could be is that they’re a one-way conversation, asking the user to say something positive to everyone else. There should be something better, something more conversational, especially when things aren’t going well.</p>

## Why Ratings And Reviews Are Important

Both Apple and Google put ratings right alongside an app’s icon and title, giving users a quick way to judge the app’s quality. People are unlikely to download an app that doesn’t have at least three stars, so developers are incentivized to get the best rating possible.

This system, while mostly effective, breaks down in a few places. For example, a ton of non-developers on beta operating systems might complain that a particular app doesn’t work on their device. You’ll also hear folks <strong>blame an app for something that isn’t its fault</strong> — for example, blaming an alarm app for not going off, even though the phone’s battery died. (I’ll let you Google around for silly app store reviews. They’re fun!)

Some <a href="https://daringfireball.net/linked/2013/12/05/eff-your-review">tech pundits recommend</a> giving one star if an app prompts you for a rating, which is a reaction to ratings being asked for the wrong reasons. Simply asking for a rating leaves a tremendous opportunity on the table, one where you get to engage with users. You could be asking what you could do better, or you could be helping them with their questions.</p>

## Why Reviews Don’t Work As Well As They Should

When the waiter at a restaurant asks me how my dinner is, without fail, they do it when I’ve just planted my face in the dish. Now I’ve got to grunt my approval like an animal. It’s awkward. (Incidentally, I haven’t experienced this outside of the US, so not everyone will have experienced this.) This is what it feels like when a user is asked for feedback. <strong>Don’t bother them when they’re in middle of something.</strong>

Think of how this plays out for your typical user. They’ve just opened your app — let’s say to tweet something — and are interrupted with, “Hey, could you rate my app, plz!” <a href="https://img.pandawhale.com/58321-Louis-CK-nope-gif-uvTq.gif">Guess what their reaction will be.</a> They opened the app to complete a task, and now you’re interrupting them to give a rating. They’ve got a lot to do, and rating an app is at the bottom of the list.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8fad159-417d-4d90-9426-f7b06d06d620/header-image-500-opt.png" alt="header-image-500" width="500" height="281" /><figcaption>Find the right time to ask for feedback and then ask your question.</figcaption></figure>

<span class="removed_link" title="https://dancounsell.com/articles/prompting-for-app-reviews">Dan Counsell has some good insight</span> on the right time to ask for feedback. Developers should find the right moment to ask, and that moment will be different for each app. Here’s what he says about Clear, a lovely little to-do app:
<blockquote>"Clear for iOS shows the 'Rate app' dialog after a few conditions have been met. First, the user must have been using the app for a few weeks. Secondly, Clear will only ask after the user has cleared the remaining tasks from a list. This is a great moment in the app; users are feeling good for having just cleared their to-do list and in most cases are just about to exit the app."</blockquote>

To return to our example of tweeting, feedback should be requested only after the user has tweeted a few times. In a photo-editing app, it could be after the user has edited and saved a couple of photos. Whatever the app, the point is to ask at the right time and to time the interruption well.</p>

<figure><img loading="lazy" decoding="async" class="at" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a688d6d2-8f3e-44b3-b621-63377011fd4f/ember-rating-500-opt.png" alt="ember-rating-500" width="500" height="500" /><figcaption>I love how Ember does it, a great way to solicit feedback.</figcaption></figure>

## Shifting From A Rating Module To A Feedback Module: A Win-Win For Everyone

You might have noticed that I use the word “feedback“ more than “rating” here. I do it because we need to fundamentally shift our perception of app ratings. <strong>Developers should engage with the user to learn about their experience</strong>, whether good or bad. If things are peachy, then asking them to leave a review seems reasonable. If not, find out why so that you can make things better for them.

How do you do that? Ask them to email you.

This tactic is especially useful with frustrated users. If you don’t attempt to talk to them, they’ll likely post a nasty review in the app store, which you can’t reply to. Not being able to reply to reviews publicly is a good thing, by the way — public disagreements can get awkward, and at least one party won’t come out of it looking good. Email gets past that and puts two humans in touch to talk through a problem.

Hearing from the user directly gives you <strong>a chance to understand their problem</strong> and often yields actionable feedback, which will be a helpful supplement to crash logs or when you want to find holes in the user experience.</p>

## How We Implemented This Idea

After thinking through how to solicit feedback, my company implemented its feedback module in a business news app named <a href="https://itunes.apple.com/us/app/business-journals-local-business/id579066124?mt=8">The Business Journals</a>. Here’s how the idea originally worked:

*   Three days after opening the app, the user would see a dialog box asking whether their experience is good or bad.
    *   If the feedback is positive, the user is asked to leave a review.
    *   If the feedback is negative, the user is asked to get in touch.
*   Users can dismiss the dialog box if they are too busy.

We thought that waiting for three days was a good compromise, giving users a decent amount of time to try out the app and gather their thoughts. The decision to wait a certain number of days, rather than a certain number of launches, was dictated by our users’ habits. Some of them launch the app a few times a day for a few moments and so would have a difficult time getting a feel for the app after just a few launches.

When a user would write to us, our support team would reply to them to help with their problem. Some complained about our update to the design, but most had lost their password or had a legitimate problem that we wouldn’t have been able to identify on our own. Ultimately, these emails were directly responsible for our considerable improvements to the app, helping us to squash bugs and remove obstacles between users and their content. The app went from 1.5 to 4.5 stars.</p>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5c2e474-12f0-4d62-bf00-f8a20af7bc90/ideal-ratings-500-opt.png"><img loading="lazy" decoding="async" class="alignnone size-medium wp-image-195448" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5c2e474-12f0-4d62-bf00-f8a20af7bc90/ideal-ratings-500-opt.png" alt="ideal ratings-500" width="500" height="281" /></a>

In short, the ideal solution is to open a dialog box at the right time with a simple question and answer. Where and how you implement it will depend on the app.

We’re planning to improve ours even more by asking users only after they have shared an article, thus minimizing interruptions further.</p>

## Feedback Modules: A Dark Pattern?

Some would call this approach to app ratings a dark pattern because it directs positive feedback one way and negative feedback another. But it has more to do with how it’s implemented. It’s a tool, inherently neither good nor bad.

Sure, it could be used for evil and to silence all dissent. Just don a black helmet and cape, build a Death Star and force choke all bad reviews to death by forwarding them to a never-monitored inbox.

Or you could use the approach for good to gather meaningful feedback from real users, in turn helping them to solve their problems and improving your product.

Not to mention, no matter how many barriers you put up, if your app is doing something evil, users will find a way to share their unhappiness with the world.

## Closing Thoughts

Hopefully, this has shed some light on how to balance your need for feedback with your need for a high rating. It’s not just about how many stars you get, but about <strong>how well you communicate with users</strong>. Whatever your method, make sure it respects the user’s time and energy. I’ve had great results with this pattern and will continue iterating on it.

I’d love to hear how you make this work for your users and to answer any questions in the comments section.</p>

### Further Reading

*   “[The Right Way to Ask Users for iOS Permissions](https://techcrunch.com/2014/04/04/the-right-way-to-ask-users-for-ios-permissions/),” Brenden Mulligan, TechCrunch

{{< signature "da, al, il" >}}

