---
title: 'How To Run A Side Project: Screenings Case Study'
slug: screenings-side-project-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e10c58af-1509-452c-a3d8-016de7b1a4cb/07-producthunt-opt.png
date: 2015-09-28T21:13:04.000Z
author: sacha-greif
summary: >-
  Did you know you have a <strong>superpower</strong>? No, I’m not talking about super-strength, sticking to walls or pushing metal claws out of your forearms (although you might have those as well, for all I know). If you work on the web — which I assume you do if you’re reading this — your superpower is <strong>side projects</strong>.
description: >-
  Did you know you have a <strong>superpower</strong>? No, I’m not talking about super-strength, sticking to walls or pushing metal claws out of your forearms (although you might have those as well, for all I know). If you work on the web — which I assume you do if you’re reading this — your superpower is <strong>side projects</strong>.
categories:
  - Design
  - Workflow
  - Productivity
  - Case Studies
---

Unlike your regular job, where you have to listen to your boss or please your client, a side project lets you take on an alternate identity, one of which <em>you</em> are in charge and no one can stop you. And the best part: If your impact is big enough, the whole world will soon know your name (or at least your Twitter handle).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Guide To Personal Side Projects](https://www.smashingmagazine.com/2016/05/a-guide-to-personal-side-projects/)
*   [Work, Life And Side Projects](https://www.smashingmagazine.com/2012/06/work-life-and-side-projects/)
*   [How And Why To Make Side Projects Work At A Digital Agency](https://www.smashingmagazine.com/2015/01/how-why-make-side-projects-work-digital-agency/)
*   [Take The Initiative and Create Your Own Projects](https://www.smashingmagazine.com/2010/10/take-the-initiative-and-create-your-own-projects/)

So, today, my goal is to give you a <strong>play-by-play account of the process of building and launching one such side project</strong>. But first, let me tell you a little more about myself.

{{% feature-panel %}}

## My Side Project Track Record

The reason I feel like bringing up this topic in the first place is because I have a lot of experience launching various side projects.

Back in the day, I launched a simple pattern-generation tool, called <a href="https://patternify.com/">Patternify</a>. A couple years ago, I took a couple weeks off from freelancing to write a <a href="https://sachagreif.com/ebook/">short eBook about UI design</a>. More recently, I launched <a href="https://sidebar.io">Sidebar</a>, a daily newsletter of design links.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd2ca061-1f03-4b14-8209-a25fb6055d79/01-sidebar-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e79ac3f-3a3d-4e7b-b71a-c7ec92627c0e/01-sidebar-opt-small.png" alt="Sidebar" /></a><figcaption>Sidebar. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd2ca061-1f03-4b14-8209-a25fb6055d79/01-sidebar-opt.png">View large version</a>)</figcaption></figure>

Every project was a chance to learn new things, make new connections and have fun while doing it. Most importantly, it was also a chance to craft something that simply didn’t exist before, something I could truly call my own.</p>

## The Three S’

So, what makes a good side project idea? I believe it boils down to the <a href="https://speakerdeck.com/sachag/side-projects">three S’</a>: simple, specific and special.</p>

<strong>Simple</strong> means keeping the scope small and getting rid of as many features as you can. For example, do you really need user accounts? Could you maybe build the same thing entirely client-side, without the need for a back end?

<strong>Specific</strong> means solving a well-defined need and targeting a well-defined audience. <a href="https://quantityqueries.com/">QuantityQueries</a> focuses on a tiny aspect of CSS, but it’s probably the best tool around for this particular problem. It does one thing but does it very well.

Finally, <strong>special</strong> means having something that makes you stand out from the crowd. This could be the idea itself or something else, like your brand or design. “Form element autosizing” sounds like the most boring thing ever, but <a href="https://leaverou.github.io/stretchy/">Stretchy</a> makes it fun with a funky color scheme, script fonts and even a cat.</p>

## The 10-Hour Rule

Remember when I said that side projects are your superpower? Well, any superhero needs a nemesis, and yours is Chronotron, the Lord of Time.

Chronotron uses all kinds of dirty tricks (such as meetings, deadlines and time with your family) to rob you of the time you need to make use of your superpower. Fortunately, you can fight back using a simple principle: the 10-hour rule.

This rule states that your project should be <strong>ready to launch after 10 hours of work</strong>.

Stick to this rule and you’ll take care of your two biggest roadblocks: never starting and never finishing.

If you’ve been procrastinating about starting your side project, it’s probably because you haven’t been able to <strong>free up your schedule</strong>. By setting a hard 10-hour limit, finding time will suddenly become much easier. Just set aside three hours a day on the weekend, then two hours twice during the week, and you’re there!

Or maybe you <em>did</em> start your project but never finished it. Once again, the 10-hour rule helps, forcing you to avoid feature bloat and scope creep.

Does that mean you should never go over 10 hours, no matter what? Of course not. In some cases, you’ll be forced to go over the limit, and in fact I ended up breaking my own rule, as you’ll soon see. Still, it’s a good starting point, and especially if this happens to be your first side project, I do suggest sticking to the rule!

## Screenings: A Case Study

But rather than keep theorizing, let me give you a concrete example in the form of my own latest side project: <a href="https://screenings.io">Screenings</a>, a website to help you discover new and inspiring design videos.

I got the idea for Screenings from running <a href="https://sidebar.io">Sidebar</a>. People would often submit video links to Sidebar, but I wasn’t quite sure what to do with them. Sidebar readers often check the newsletter as part of their morning routine to get their quick fix of design news and links, which isn’t the best time to take a break and spend 10 to 15 minutes watching a video.

So, in the back of my mind, I always had this idea that a Sidebar just for videos could be pretty neat.

And it even met my own three S’ rule:

*   It was **simple**, because I knew I could rely on [Telescope](https://telescopeapp.org) (the open-source app that also powers Sidebar and a few other projects) to do most of the heavy lifting.
*   It was **specific**, because I wasn’t trying to build the next YouTube; instead, I would focus on the narrow niche of design videos.
*   It was **special** because, as far as I knew, nothing quite like it was out there yet.</p>

## A Solid Foundation

<a href="https://telescopeapp.org">Telescope</a> is an app I’ve been working on for the past few years to make it easier to build just this kind of project. It basically started off as a Hacker News or Product Hunt clone but has since evolved into a free, open-source platform that supports any kind of social app or community. Think WordPress but for communities instead of blogs.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f65638a0-cb51-46ca-acb3-44f92d45cf9d/02-telescope-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/023996e2-b86a-4adb-82b6-8f94214edb5f/02-telescope-opt-small.png" alt="Telescope, my secret weapon" /></a><figcaption>Telescope, my secret weapon. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f65638a0-cb51-46ca-acb3-44f92d45cf9d/02-telescope-opt.png">View large version</a>)</figcaption></figure>

Most of the features I needed (posts, comments, media previews, sorting, etc.) were already built into Telescope, so I knew my work would mainly focus on theming and customizing the app’s look and feel.

So, I cloned Telescope, created a new theme package and got to work.

## Customizing Telescope

I started by repurposing a few of Telescope’s features to better suit videos.

For example, out of the box, Telescope lets you upvote or downvote any post. For Screenings, I transformed the upvote icon into a like heart, while keeping the back-end logic identical.

I also added a new “short” sorting view that would filter out all videos longer than three minutes, for when you need a quick shot of inspiration during your coffee break. And I had some fun with <a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">flexbox</a> in trying to come up with a dynamic grid layout that would automatically resize for small screens.

Finally, I added a scrolling hover effect with CSS animations, to emulate the old <code>marquee</code> tag:

<pre><code class="language-css">
.marquee-outer {
   position: relative;
}

.marquee-inner {
   position: absolute;
   span {
      position: relative;
      animation: marquee 5s linear infinite;
      &amp;:after {
         content: attr(data-content);
         margin: 0 10px;
      }
   }
}

@keyframes marquee {
   0% { left: 0; }
   100% { left: -50%; }
}
</code></pre>

## Look And Feel

When you work on your own project without a client breathing down your neck and telling you to “Make it pop more” and ”Avoid green because my niece doesn’t like that color,” settling on a look and feel can be surprisingly hard.

Should you go serif or sans-serif? Light or dark? Solid color or gradient? You can do literally anything you want every step of the way, and that can drastically slow you down (or lead to some pretty grievous crimes against good taste, as you’ll soon see).

I started with a serious, classical style, trying to evoke the look and feel of respected print magazines, such as <a href="https://monocle.com/">Monocle</a>.

But maybe because I didn’t have the brand and history to go along with it, my design ended up looking boring and uninspired.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d774dba7-46e5-4fc4-8bb0-77db2ea339e5/03-screenings-original-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e85c34a6-876d-4443-8987-19f6f5fc99ec/03-screenings-original-opt-small.png" alt="The first version of Screenings" /></a><figcaption>The first version of Screenings. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d774dba7-46e5-4fc4-8bb0-77db2ea339e5/03-screenings-original-opt.png">View large version</a>)</figcaption></figure>

I then went a bit too far in the other direction. I tried so hard to be fresh and edgy that I ended up copying the iTunes icon’s colors without even realizing it. Sure, my design would appeal to 15-year-olds, but the neon gradient was taking focus away from the content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11513fa8-7313-4dbf-962b-d32bf8a5ef6d/04-screenings-gradient-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d783fe-5093-4818-9a21-30a3c39de1a4/04-screenings-gradient-opt-small.png" alt="The design goes through its rebellious teenage phase" /></a><figcaption>The design goes through its rebellious teenage phase. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11513fa8-7313-4dbf-962b-d32bf8a5ef6d/04-screenings-gradient-opt.png">View large version</a>)</figcaption></figure>

Refocusing on content turned out to be the key. I decided to keep things low key with a dark-blue background, but using a translucent overlay of the video thumbnail on individual video pages.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fea5c44-dc02-4558-93ea-8c942a7c0cee/05-screenings-video-page-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c51958f-e859-4217-abec-d18fc9ae4e54/05-screenings-video-page-opt-small.png" alt="The single video page uses the video thumbnail as background" /></a><figcaption>The single video page uses the video thumbnail as background. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fea5c44-dc02-4558-93ea-8c942a7c0cee/05-screenings-video-page-opt.png">View large version</a>)</figcaption></figure>

As for the logo, I tried out various serif and script fonts but couldn’t decide on something I liked. I eventually decided to keep things simple and go with a text-only logo, highlighting with a CSS text-shadow effect for now.</p>

## Prioritizing The Design

As it turns out, the 80/20 rule still holds true. Getting 80% of the way to a finished product was easy; the remaining 20% wasn’t going to be as smooth.

The big problem I ran into was how to display grid items. Here’s all of the meta data associated with a single video:

*   title
*   description
*   author
*   number of comments
*   commenters
*   number of likes
*   timestamp
*   duration
*   thumbnail

Add to this the like and share buttons, the edit icon and, for administrators, the approve/unapprove link (because videos require moderation before appearing publicly on the website), and you can understand my problem: How could I fit all of this in a single grid item without ending up with a complete mess?

After pondering the question for a good while, I decided to <strong>get rid of the share buttons, commenter avatars and video duration</strong>. Things were already starting to look a bit saner!

Displaying the title and summary would also prove tricky. I knew I wanted to stick them on top of the video thumbnail, but some kind of overlay would be needed to make it work, even when the thumbnail was white or light.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37985b36-aa22-47b9-98a0-3a5a6328e79e/06-screenings-grid-item-evolution-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5c1b812-2d62-4db1-bc75-933e575c2b34/06-screenings-grid-item-evolution-opt-small.png" alt="The evolution of the grid item’s design" /></a><figcaption>The evolution of the grid item’s design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37985b36-aa22-47b9-98a0-3a5a6328e79e/06-screenings-grid-item-evolution-opt.png">View large version</a>)</figcaption></figure>

I tried a black-to-transparent gradient, but, while this looked great on dark images, it made light images look dirty and grimy. In the end, I resorted to a solid translucent overlay instead.

Another consideration was how much text to display: too little and the video might fail to trigger a user's interest, too much and the items would look more like blog posts and less like videos.

After many iterations, I finally had something that more or less worked. It wasn't perfect by any means, but it would do for now. It was time for the big launch.</p>

## The Launch

Launching a project is always a delicate operation. It’s the only part of the process where you can’t iterate. You get one shot, and if you blow it, then that’s it.

Big companies can rely on their press contacts and PR teams to set up a successful launch, but you’re on your own with a side project. Thankfully, the rise of websites like <a href="https://news.ycombinator.com">Hacker News</a>, <a href="https://reddit.com">Reddit</a> and <a href="https://producthunt.com">Product Hunt</a> has helped to even up the scales.

This is particularly true of Product Hunt: It gets a lot fewer link submissions per day, meaning that each one is more likely to get a fair shot. And its focus on products, instead of general news or discussion, makes it the perfect place to launch any kind of project.

So, for Screenings, I decided to focus all of my initial effort on Product Hunt. I got in touch with Product Hunt’s administrators to show them a preview of the website, asking them if they thought it was a good fit for the website. They said it was and even suggested a good time for the launch.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e10c58af-1509-452c-a3d8-016de7b1a4cb/07-producthunt-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2f2b2ed-a2a0-4e3f-8baa-586e6eb2eb3d/07-producthunt-opt-small.png" alt="Screenings on Product Hunt" /></a><figcaption>Screenings on Product Hunt. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e10c58af-1509-452c-a3d8-016de7b1a4cb/07-producthunt-opt.png">View large version</a>)</figcaption></figure>

All of this preparation paid off: Screenings reached second place on the day I submitted it (behind Product Hunt’s own new “<a href="https://www.producthunt.com/books">Books</a>” category).</p>

## Scaling Issues

It was not all smooth sailing (or should I say, smooth scaling).

The website held up fine under traffic throughout the day, even while being featured on Product Hunt. But I then made the mistake of emailing an announcement to the entire Sidebar mailing list, and this pushed my poor overworked server over the edge.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8a99700-2be8-4bba-ab24-9d2ab86d60d0/08-google-analytics-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3616ea9-bc89-4961-a097-6d6eed4ae43c/08-google-analytics-opt-small.png" alt="Screenings’ traffic statistics since launch" /></a><figcaption>Screenings’ traffic statistics since launch. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8a99700-2be8-4bba-ab24-9d2ab86d60d0/08-google-analytics-opt.png">View large version</a>)</figcaption></figure>

Of course, I should also mention that I did this at 11:00 pm, at the end of the big launch day. Faced with an increasingly unresponsive server, I knew I had a few hours of development work ahead of me if I wanted to accomodate this influx of traffic.

Yet, I then did something that might surprise you: I decided to <strong>go to bed</strong>.

I knew the traffic spike would die down eventually. Fiddling with servers while tired, possibly making things worse, just wasn’t worth it. And I knew that the traffic spike on launch day has little to do with a project’s long-term success.

Sure enough, when I woke up the next day, the spike was over, and my server was back to chugging along just fine. If you want to hear more, I’ve written about the whole episode in more detail <a href="https://www.telescopeapp.org/blog/screenings-launch-meteor-scaling-case-study/">on the Telescope blog</a>.</p>

## A Few Stats

Here’s a few statistics for the two weeks since the initial launch:

*   total page views: 513,000
*   total unique users: 28,143
*   newsletter registrations: 946
*   user registrations: 322
*   videos posted: 94
*   tweets: 452

Overall, a pretty good result for about 16 hours of work!

I know: I broke my own 10-hour rule. In my defence, a big chunk of that time was spent fidgeting over fonts!

## The Aftermath

This brings me to the last part of my journey: the aftermath. After a launch, I always get this weird, disoriented feeling: “So, what now?”

Up to launch day, you have this clear, well-defined <strong>goal with a tangible payoff attached to it</strong>. But once your website is out there and the initial interest has died down, you’re faced with a very different challenge.

Compared to the all-out, take-no-prisoners war of the pre-launch period, you now face a long, slow battle of attrition, in which the aim is to make a tiny bit of progress every day.

This is where a lot of side projects fade out. And nothing is wrong with that: You’ve had fun, you’ve learned a ton, and now’s the time to go back to your day job (or maybe to think about your next side project).

But there’s also something to be said for embracing the grind and trying to make your side project into, well, a <em>project</em>.

This is what I’m trying to do with Screenings. It’s now up to me to slowly improve the website, get more people to sign up and get the word out.

And guess what? This article is the first step in that long process!

## Conclusion

I really believe that <strong>side projects are underused</strong> by the vast majority of designers and developers out there. We create school projects as students, and they're almost always a great learning experience, but somehow, once we enter the “real world,” work gets in the way, and we forget that side projects are even a possibility.

So, with this article, I want to awaken your latent side-project powers. First, remember the three S’ (simple, specific and special) when coming up with an idea.

Then, stick to the 10-hour rule while working on the project.

Finally, once you're ready to launch, press that big red button. And then start thinking about your next side project!

One final note: I decided to <a href="https://github.com/TelescopeJS/Zeiss">open-source the Screenings theme</a>, so that anyone can easily build their own video website!

{{< signature "vf, ml, al" >}}

