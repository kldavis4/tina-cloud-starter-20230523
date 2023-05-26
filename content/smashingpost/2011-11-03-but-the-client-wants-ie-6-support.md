---
title: But The Client Wants IE 6 Support!
slug: but-the-client-wants-ie-6-support
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5fe87a2-fb9e-4ff3-bcfb-59283d17a574/internet-explorer-blue-illu.jpg
date: 2011-11-03T12:35:56.000Z
author: lea-verou
description: >-
  Frequently, when I discuss CSS3 with other developers, the issue of stubborn clients comes up. They tell me that even though they personally don’t think a website should look the same in all browsers and they’re eager to try all of these new techniques, their clients insist that their website should look the same, so the developers are stuck with the same Web development techniques that we used five to ten years ago. Their clients just don’t “get” graceful degradation.
categories:
  - Coding
  - Workflow
  - Clients
  - Bugs
  - Opinion Column
  - Discussions
---
Is this really the issue? Are our clients incapable of understanding these things? Is the problem that our clients don’t “get” the Web and need to be educated? I don’t think so. We got ourselves into this. We are the ones who caused this problem for our industry. We are the ones giving ourselves this trouble and making our profession less creative and enjoyable than it could be. It’s entirely our fault and no one else’s.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [CSS Differences in Internet Explorer 6, 7 and 8](https://www.smashingmagazine.com/2009/10/css-differences-in-internet-explorer-6-7-and-8/)
*   [Old Browsers Are Holding Back The Web](https://www.smashingmagazine.com/2012/07/old-browsers-are-holding-back-the-web/)
*   [The Life and Death of Internet Explorer 6 (Comic Strip)](https://www.smashingmagazine.com/2010/02/the-life-times-and-death-of-internet-explorer-6-comic-strip/)
*   [How To Support Internet Explorer and Still Be Cutting Edge](https://www.smashingmagazine.com/2009/12/how-to-support-internet-explorer-and-still-be-cutting-edge/)

## Wait, What?

If we choose to make a website pixel-perfect in Internet Explorer 6 to 8, then we are doing up to 100% more work. No matter how many frameworks, polyfills and other scripts we use to ease our pain, we will always be doing at least 30% more work for those browsers. How many of us actually charge 30-100% extra for this work? I haven’t heard of many who do. <strong>Clients get this kind of extra work for free</strong>, so of course they will say that they want IE 6 support. If I was a client, maybe I’d say so, too, especially if I didn’t know how these technologies work. <strong>They won’t care about our extra time if we don’t care enough ourselves to charge for it accordingly.</strong>

{{% feature-panel %}}

Of course, faster download times and better SEO are compelling arguments, but let’s face it: one of the biggest advantages of the new CSS features and new JavaScript APIs is the huge chunk of development time they save us, including making maintenance easier and quicker. As long as that doesn’t translate to reduced costs, clients will not care. And that’s perfectly understandable and natural.

<a href="https://www.flickr.com/photos/hikingartist/5727283114/sizes/m/in/photostream/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f68adde1-1ff7-412a-94e9-7ce4d46a8fdc/money-wins.jpg" alt="Money always wins." width="500" height="328" /></a><br>
<em>Money always wins the argument. (Image: <a href="https://www.flickr.com/photos/hikingartist/5727283114/sizes/m/in/photostream/">HikingArtist</a>)</em>

I don’t do much client work these days, but every time I’ve taken on a client project in my career, I’ve always presented options for browser support to my client. They want pixel perfection in IE 7? It will cost them more. They want IE 6 support? It will cost double. I explain to them that this is because I will have to do double as much work for this browser. <strong>I’ve never had a single client opt to pay more to fully support older browsers.</strong> If it doesn’t come free, you’d be surprised at how many don’t care about it as much as you think. But even if they do, at least I will have enough motivation to do it without hating them, my job, browser makers and the universe. It’s fairer for everyone, including me.</p>

## “They’ll Just Go To Another Professional Who Doesn’t Charge Extra”

Whatever you do, don’t let the client think that you are charging extra for doing the <em>same</em> work as another professional. Not only will that look bad, but it’s also inaccurate. Explain to them that you just want to give them <strong>options</strong> and not decide on your own which browsers to support and charge for accordingly, without ever involving them in the process and letting them have a say about it.</p>

## How Much More?

You might have noticed that I implied above that supporting old Internet Explorers requires 30 to 100% more time. That’s a huge range, isn’t it? Actually, it should be even wider. I remember a case of a client coming to me with a CSS challenge that his developers weren’t able to solve. Making something that worked in modern browsers took me half an hour, then an hour to make it work in IE 8, and then three(!) more hours to get it to work in IE 7. Who knows how much longer it would’ve taken if I had to support IE 6, too! And that wasn’t the only occasion when it took me very little time to build a prototype that works in modern browsers and then a grossly disproportionate amount of extra time to make it work the same way in old Internet Explorers. If you’ve been in the field for more than a year, I’m sure this has happened to you, too.

On the other hand, if you don’t use any modern technology and you stick to CSS 2.1, then I guess you would only have to face the old IE bugs, which would take some extra time but not double. Or, if you used a ton of frameworks and polyfills, you would still have to spend some time making them work together and debugging potential conflicts, but still not double the time. 30% was an estimate for cases like those.

As you can see, the range is huge and depends on a number of different factors, including but not limited to the following:

*   **You**.  How modern are your development techniques? The more cutting-edge they are, then the more effort you will need to put into making good fallbacks or coming up with alternative techniques for old Internet Explorers (but less effort to make the original prototype)
*   **The project**.  If it’s a brochure website, the main thing that will need extra effort in order to work in old IEs is the styling. If it’s a Web application, it gets way trickier (and more time-consuming).
*   **Level of support**.  Supporting a browser is not black and white, either no support or full support. How good your fallbacks need to be will greatly determine how much extra time you have to spend on them.

So, I’m sorry but I can’t tell you how much extra you will need to charge to support old Internet Explorers. You’ll have to decide yourself, case by case, taking all relevant factors into consideration.</p>

## “But What If They Just Want To Pay For Firefox?”

Of course, there is a baseline of browser support that I won’t go below, even if the client doesn’t want to pay for it. <strong>We have a responsibility to ourselves and to the Web to follow the principle of <a href="https://www.w3.org/People/Berners-Lee/UU.html">universality</a>.</strong> Even if a client wants to pay only for Firefox support, for example, my responsibility is to ensure that the website is still functional in the other browsers. Even if they are not willing to pay for mobile support, my responsibility as a Web developer is to at least add some media queries and make it decent there. Even if they don’t care about accessibility, my responsibility is to make the website somewhat accessible. These things don’t take up much time anyway, and they should be factored into even your lowest price.</p>

## So, What To Do With Old IEs?

So, what do I do for those wise clients who don’t want to pay for support of old Internet Explorers? Usually, I try to keep graceful degradation in mind and provide decent fallbacks for old browsers, so that at least the content is accessible in them. But in cases of really naughty browsers, like IE 6 and 7, sometimes even graceful degradation doesn’t work very well. Then, what I usually do is split my CSS into three files:

*   _base.css_ Fonts, basic colors, etc.
*   _screen.css_ Everything specific to the screen. Most of the CSS goes here.
*   _print.css_ Print-specific styles, such as for hiding contact forms, etc.

Then, I just don’t serve <em>screen.css</em> to IE 7 and below. They get something like a print style sheet, without the hidden elements. It’s not very pretty, and it’s not modern, but at least they get the content. The same could be done with JavaScript. Check whether an API is present before using it, or simply don’t serve those script files to old Internet Explorers. If you’ve coded your JavaScript properly and it’s unobtrusive and all, then old browsers won’t get that extra functionality, but they won’t get JavaScript errors and broken functionality either. All of those require minimal effort on your part.</p>

## “Does That Mean I Always Have To Charge Less For Using Modern Stuff?"

While discussing my point of view with another developer, he asked me, “So, you’re saying that I shouldn’t charge more if I use responsive design and add a bunch of media queries?” Absolutely not! I’m not saying we should feel sorry for being cutting-edge or punish ourselves for that with less income! What I’m barely advocating is the common-sense idea of charging more for more hours of work. If you code some JavaScript that does the same thing that media queries do, then of course you should charge more for the JavaScript, because it will take you more time. But if you weren’t going to do anything like that, and the media queries were icing on the cake, then of course you should charge them more than you would for a non-responsive version of the website.</p>

## Conclusion

We may love what we do, but we certainly don’t love catering to the whims of old browsers. We do a lot of extra work to hide their incompetence, and that work needs to be compensated for properly. You don’t have to work for free, especially on something you don’t like doing. Explain the situation to your clients and they’ll understand how it goes, I promise. After all, “extra work = higher costs” is an established rule in every industry. The concept is not hard to grasp, and it makes the benefit of modern Web technologies much more tangible for technologically unsavvy clients.</p>

### What do you think?

How do you account for browser support in the pricing of your work? Do you charge extra for legacy browsers or do you provide a basic version of the design to legacy browsers? Let us know and leave a comment!

{{< signature "al" >}}

