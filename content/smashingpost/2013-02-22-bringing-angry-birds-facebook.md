---
title: Bringing Angry Birds To Facebook
slug: bringing-angry-birds-facebook
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b86faae6-ccdc-49ff-a136-2ba142d82de4/psych-7.jpg
date: 2013-02-22T22:24:23.000Z
author: richard-shepherd
summary: >-
  There’s no avoiding those Angry Birds. They are, quite literally, everywhere: toys, snacks, cartoons, plush toys and that wildly addictive game that seemingly everyone has downloaded at some point &mdash; 1 billion of us last year alone.
description: >-
  Angry Birds are, quite literally, everywhere: toys, snacks, cartoons, plush toys and that wildly addictive game that seemingly everyone has downloaded at some point.
categories:
  - Inspiration
  - Design
  - Workflow
  - Interviews
---
2012 was another landmark year at the Angry Birds aviary, otherwise known as <a href="https://www.rovio.com/">Rovio</a>. The Finnish-based developer not only released a slew of tie-ins &mdash; from [Green Day](https://www.billboard.com/articles/news/480358/green-day-partners-with-angry-birds) to [Star Wars](https://www.rovio.com/en/our-work/games/view/50/angry-birds-star-wars) &mdash; but also went social.

Not only did releasing Angry Birds on Facebook require the game’s engine to be rewritten in the all-new Flash 11, but the power of Facebook’s platform meant that the game’s mechanics could be tweaked further to take advantage of the social graph.

At the forefront of this project was <a href="https://villekoskela.org/">Ville Koskela</a>, a lead game programmer at Rovio. Ville has been a developer for his entire adult life, with a background in C++ and ActionScript. And when he’s not working on one of the biggest games in the world for the biggest social network in the world, he loves running in and around his home town of Espoo, Finland (he ran a 100-km race in under 12 hours).

<a href="https://villekoskela.org/"><img class="151330" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e2343fa-2843-4a0d-be29-96e94c0a8603/ville-koskela.jpg" alt="Ville sporting a 'play-off' beard from the last 3-4 weeks of the project!" width="500" height="413" /></a><br><em>Ville sported a playoff beard during the last few weeks of the project.</em>

{{% feature-panel %}}

I chatted with Ville about bringing Angry Birds to Facebook, and started by asking how he got the job.

<blockquote>"I worked as a software architect at Sulake, the company behind the teenage online chat world Habbo Hotel. At Sulake, I had been one of the two guys leading the conversion of Habbo Hotel from Shockwave to the Flash version. I had naturally read about the success of Angry Birds and checked Rovio’s website at some point, but back then there was no Web team yet, and even though I had done mobile programming myself, I wasn’t too interested in that anymore.

Then, during the summer of 2011, I was contacted through LinkedIn and asked if I was interested in coming in for an interview at Rovio. After hearing what the new job would be about, the decision to join Rovio was a really easy one."</blockquote>

What exactly does his role entail?
<blockquote>"As a lead game programmer, I am a supervisor for a team of ten other Flash and C++ programmers, varying from trainees to seniors. I go through job applications, do interviews, and try to make sure all the projects have right set of programmer resources available to launch on schedule &mdash; and that they meet our quality expectations. I also still do some (mostly engine) ActionScript programming myself, but mainly try to concentrate on <strong>helping others do their programming job the best way possible</strong>.

I work closely with the graphic designers, server programmers and producers &mdash; basically most of the different people involved in the development of every Angry Birds game."</blockquote>

So, what’s it like working at Rovio?
<blockquote>"The working environment is really nice, and the atmosphere is relaxed. We try to combine the good parts of traditional planning in advance with <a href="https://en.wikipedia.org/wiki/Agile_software_development">agile</a> methods to achieve the best possible results. Last but not least, working on something as hot as the Angry Birds brand ensures that everyone is giving their best in the different projects."</blockquote>

Angry Birds started life on the iPhone in December 2009 and has arguably become the biggest mobile franchise on the planet. With success came expansions, spin-offs and ports, and in 2010 Rovio started working on a Facebook version.

In March 2011, InsideMobileApps <a href="https://www.insidemobileapps.com/2011/03/13/rovio-angry-birds-facebook/">interviewed Peter Vesterback</a> (<a href="https://twitter.com/pvesterbacka">@pvesterbacka</a>), Chief Marketing Officer and “Mighty Eagle” at Rovio, and asked him why development was taking so long.
<blockquote>"You can’t take an experience that works in one environment and one ecosystem and force-feed it onto another. It’s like Zynga. They can’t just take FarmVille and throw it on mobile and see what sticks. The titles that have been successful for them on mobile are the ones they’ve built from the ground up for the platform."</blockquote>

<a href="https://www.facebook.com/angrybirds"><img class="aligncenter size-full wp-image-151382" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c8213e0-087c-47c0-baa5-099fd430f452/screen-shot-2012-12-18-at-13.48" alt="Angry Birds on Facebook" width="550" height="334" /></a>

The original release date for Angry Birds on Facebook, now known as Angry Birds Friends, was May 2011. It wasn’t until later that year that Ville joined Rovio, and the port still wasn’t finished.

{{% ad-panel-leaderboard %}}

<blockquote>"When I joined the company at the beginning of September 2011, there was a Flash 10 prototype of the original Angry Birds game available that had been done earlier in 2011.

The prototype’s performance was not too good, which was the reason to wait for Flash 11, with the support of GPU-accelerated Stage 3D graphics. Before continuing the development, I was hired both to lead the new team of Flash developers joining the company and to make sure a fully optimized Flash 11 version of the game was ready for release as soon as possible."</blockquote>

<strong>Flash? Yes, Flash.</strong> For those of us who have avoided Adobe’s waning flagship for the last few months or years, it turns out that it has gotten considerably better. Indeed, Flash 11 is Adobe’s attempt to reinvigorate the platform with cutting-edge 2-D and 3-D rendering.

The Stage 3D that Ville mentions is Adobe’s very low-level GPU-accelerated APIs. You can hack them directly using the AGAL language or, as Rovio has done, use a framework and ActionScript. For 2-D applications with 3-D acceleration, the open-source <a href="https://gamua.com/starling/">Starling Framework</a> is the choice of many. But as Rovio was developing Angry Birds for Facebook, the framework still hadn’t been completed.
<blockquote>"We started the development with an unreleased version of the Starling Framework. <strong>Back then, Starling’s performance was not too good</strong>, so I did lots of optimizations there myself, about which I also <a href="https://villekoskela.org/2011/12/12/starling-gets-wings/">wrote on my blog</a>. Now these optimizations (and also many others) have found their way into the current version of the Starling Framework, so other developers don’t have to go through this process themselves anymore.

It soon became clear that we could achieve the desired performance with GPU rendering, but machines with only CPU rendering were not doing too well. To get the game running smoothly on those machines meant we had to cut down some graphical detail &mdash; lowering rendering quality and dropping some layers and animations from the background graphics."</blockquote>

Flash 11 and Stage 3D have excited many people, and they represent a lifeline for a product that seemed to be <a href="https://en.wikipedia.org/wiki/Not_Waving_but_Drowning">drowning, not waving</a>. I asked Ville what he thought this meant for the future of the platform.
<blockquote>"In my opinion, with the release of Flash 11, Adobe has proven that it really wants to provide millions of developers with <strong>tools with which you can bring A-quality games to Web</strong>. Stage 3D graphics might not be a thousand times faster like some advertisements read, but they are still a lot faster, enabling 60-FPS full-screen gameplay for our 2-D Angry Birds and really high frame rates for some 3-D games out there. The release of Flash 11 has also made the “Flash is dead” chanters pretty quiet this year."</blockquote>

Or has it? Many proponents of HTML5-based apps are quick to dismiss Flash. And a certain Steve Jobs announced the end of support for it completely on iOS in a <a href="https://www.apple.com/hotnews/thoughts-on-flash/">well-publicized open letter</a> back in 2010.

Indeed, Google is <a href="https://www.theverge.com/2012/6/29/3125219/flash-mobile-android-4-1-not-supported">dropping support for Flash</a> on Android, and an HTML5 version of Angry Birds is <a href="https://chrome.angrybirds.com/">available in the Chrome Web Store</a>. Even Microsoft is getting in on the act, teaming up with ZeptoLab to create an <a href="https://www.crazygames.com/game/cut-the-rope">HTML5 version of Cut the Rope</a> to show off the latest version of Internet Explorer.

<a href="https://www.cuttherope.ie/"><img class="153853" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5339888-94bf-42d2-98a8-8d737308dcc5/cut-the-rope.jpg" alt="Microsoft used an HTML5 version of Cut the Rope to demo its latest browser." width="500" height="351" /></a><br>
<em>Microsoft used an HTML5 version of Cut the Rope to demo its latest browser.</em>

With all of the trash talk about HTML5 versus Flash, does Ville think comparing the two is even fair?

<blockquote>"Here at Rovio, <strong>we do not have “this technology” versus “that technology” thinking</strong>. If a new platform has the capabilities and a big enough audience, there’s a good chance that you will see Angry Birds there. I believe that all the technologies have their strengths, and when there’s competition, each participant will gain from that and become better in the long run."</blockquote>

As Peter Vesterback mentions in his interview with InsideMobileApps, <strong>a successful game needs to be built from the ground up for each platform</strong>. This presented an opportunity for Rovio to tweak the tried-and-trusted Angry Birds formula for a social environment.

{{% ad-panel-leaderboard %}}

I asked Ville just how far they pushed the envelope.

<blockquote>"Bringing the game to Facebook naturally added the social aspect. We tried to think of how players would like to either compete against or support their friends. Our game designer spent time playing other successful Facebook games and thinking about what ideas would work in Angry Birds and what wouldn’t. <strong>We came up with the crown concept</strong>; the three best players in your friends network would have crowns &mdash; gold, silver and bronze &mdash; for each of the levels, so that there is continual competition to be the best player on every single level.

The biggest change we introduced to the actual game was the power-ups, with which the players can achieve even higher scores on the levels. The power-ups provide a way to monetize the game since they are available as an in-application purchase; but they also help with retention since players who keep returning to the game get free power-ups, and it’s also possible to gift your friends with those."</blockquote>

Those two magic words, “social” and “monetize.” This is perhaps one of the main draws of Facebook for Rovio. And with over 23 million likes already, it is clearly delivering on the promise that the Angry Birds brand makes.

<a href="https://www.rovio.com/en/our-work/games/view/50/angry-birds-star-wars"><img class="aligncenter size-full wp-image-151326" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86358cd3-75ed-4c68-8d59-f7809520bff1/screen-shot-2012-12-17-at-13.32" alt="Angry Birds Star Wars on Facebook" width="550" height="323" /></a>

But with so many platforms, so many crossovers and licensing opportunities, what is now driving development for the team? Is it new game features? Or is it new content, like the recent tie-in with Green Day? <strong>Just how far can these birds fly?</strong><br>
<blockquote>"The guys making decisions [about licensing opportunities] go through the pros and cons in each individual case both before and after the project. All of the Angry Birds fans out there should be pretty confident that the brand will stay strong, and new and interesting things will keep coming at a steady pace."</blockquote>

As the Angry Birds empire continues to grow &mdash; and it certainly shows no signs of stopping &mdash; people such as Ville are the ones keeping the brand and experience consistent across all of the platforms that we now use.

We can only hope that the continued development of new angles and spin-offs &mdash; like Bad Piggies &mdash; do not dilute <strong>the experience that many of us fell in love with</strong>. There can be too much of a good thing, after all.

For games developers and designers, Angry Birds Friends also reminds us that Flash still has a prominent place in the market. By finally harnessing the power of the GPU, Adobe has opened up the floodgates to 3-D games that look and play just like their PC and console equivalents. The big question is whether it’s too little, too late.

Ultimately, the power now lies with Android and iOS, because the desktop market &mdash; and, thus, the market for Flash apps &mdash; is shrinking. But by covering all of its bases, Rovio has made sure that Angry Birds will be flying in and out of our lives for years to come.

### Resources

*   [Angry Birds on Facebook](https://www.facebook.com/angrybirds)
*   [Ville Koskela](https://villekoskela.org/)
*   “[Rovio Has Been Working on the Facebook Version of Angry Birds for a Year](https://www.insidemobileapps.com/2011/03/13/rovio-angry-birds-facebook/),” Kim-Mai Cutler, InsideMobileApps
*   [The Starling Framework](https://gamua.com/starling/)
*   [Stage 3D](https://www.adobe.com/devnet/flashplayer/stage3d.html) for Flash
*   [Rovio](https://www.rovio.com)

<em>Credits of image on front page: <a href="https://www.flickr.com/photos/tripletsisters/7394261682/">thethreesisters</a>.</em>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Social Influence: Incorporating Social Identity Theory Into Design](https://www.smashingmagazine.com/2014/07/incorporating-social-identity-theory/)
*   [How To Integrate Facebook, Twitter And Google+ In WordPress](https://www.smashingmagazine.com/2012/01/facebook-twitter-google-wordpress/)
*   [Tale Of A Top-10 App, Part 1: Idea And Design](https://www.smashingmagazine.com/2013/07/top-ten-app-part-1-idea-and-design/)
*   [The Art Of Launching An App: A Case Study](https://www.smashingmagazine.com/2012/04/art-of-launching-app-case-study/)

{{< signature "al, il" >}}
