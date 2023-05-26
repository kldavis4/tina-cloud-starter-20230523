---
title: 'Inside Google’s User Experience Lab: An Interview With Google’s Marcin Wichary'
slug: interview-google-marcin-wichary
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a937e2-4a0c-4e91-8f10-234970eada05/marcin.jpg
date: 2011-07-08T11:51:07.000Z
author: dan-redding
summary: >-
  Marcin Wichary joined Smashing Magazine author Dan Redding for a conversation regarding his fascination with the relationship between humans and machines, his professional career, his interest in photography and a curious creation known as the Crushinator.
description: >-
  Marcin Wichary joined Smashing Magazine author Dan Redding for a conversation regarding his fascination with the relationship between humans and machines, his professional career, his interest in photography and a curious creation known as the Crushinator.
categories:
  - UX
  - Inspiration
  - Workflow
  - Interviews
  - Opinion Column
---

Marcin Wichary’s fascination with the relationship between humans and machines began at an early age. As a boy in Poland, he was mesmerized by the interaction between arcade patrons and the video games they played. Years later, Marcin would help shape the way that millions of computer users interact with some of the world’s most popular websites. He would even recreate one of those arcade games for the Web.

Marcin is **Senior User Experience Designer at Google**, but his numerous roles and broad influence at the company are not conveniently definable. His fingerprints are on the code of Google products ranging from Search to Chrome. He gained publicity for his work on the <a title="Google Pac-Man" href="https://www.google.com/pacman/">Google Pac-Man Doodle</a>, which he co-created with fellow Googler <a title="Ryan Germick Interview" href="https://www.magneticstate.com/blogdept/2009/interview-google-designer-ryan-germick/">Ryan Germick</a>. According to Ryan, “Marcin is a genius. He’s a UX designer but he’s also maybe one of the best front-end programmers on the planet.”

Marcin joined Smashing Magazine author Dan Redding for a conversation regarding his professional career, his interest in photography and a curious creation known as the Crushinator.

{{% feature-panel %}}

## The Interview

<figure><img class="103688" title="Marcin Wichary" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a937e2-4a0c-4e91-8f10-234970eada05/marcin.jpg" alt="Marcin Wichary" width="500" height="340" /><figcaption>Marcin Wichary.</figcaption></figure>

**Question: Hi, Marcin! I understand that you’re involved in a variety of departments and projects at Google. Can you summarize your professional roles at the company?**

**Marcin Wichary:** Sure. So, I’ve been at Google for the past five and a half years, and I’ve always been kind of a weird mix of a user experience designer and a developer. I guess I kinda grew more comfortable with it as time went by. I started working on the Internal Tools team, working on our Internet &mdash; or the experience of our Internet &mdash; and some of the tools that Googlers use that you can’t really show to anybody outside, programs that you can’t tell your Mom, “Hey, this is what I did this week!” I’d been doing that for about two and a half years, and then I moved to kind of the proper User Experience team, the global team that works on products that actually people can use. I’ve been on Search for, well, two and a half years as well, I think.

**Question: And you also work on the Doodles, for example, right?**

**Marcin:** Yeah! So, that has always been kind of on the side. And then I just joined the Chrome team this year. So, that is kind of my second or third big change within Google. Google is great because it allows you to do a number of things, kind of as your twenty percent project, and one of mine has always been this ongoing collaboration with the Doodle team, as a… I don’t even know what to call it… a “technology consultant” collaborator! \[Laughs\]

**Question: What was your involvement in the Martha Graham doodle?**

**Marcin:** I developed a technique to animate it. The proper visuals had been done elsewhere. There’s a number of technologies that you could think of if you wanted to put something on the Google home page that’s animated, right? There’s an animated GIF. It could maybe be a YouTube video, and we’ve done that. It could be a number of other techniques. But all of them have pros and cons.

For this particular doodle, none of the ones we knew of were good enough. Especially on the home page, we have a number of constraints. You know, we need to serve it to the user as fast as possible. We really care a lot about speed. And we also wanna make sure that it’s gonna work on every possible platform. So, for example, that would exclude Flash animation, just because a number of touch-based devices wouldn’t support that.

When I look at Web development, a lot of what’s necessary is weird ingenuity, where you look at the limited number of tools at your disposal and try to put them together in a funny way. Eventually, I developed this technique to create this big sprite. Instead of just having hundreds of frames and sending them down the wire and possibly costing a lot of bandwidth, you would just construct a sprite with the smallest possible rectangle that contains the difference between two frames. It would be kind of like you had a first frame and then every other frame would be the delta. And there was this little mechanism to construct it and then play it back. It worked pretty well, so we were happy. I’m not an illustrator: I’m a designer, but I cannot draw. I’m the worst Pictionary player ever. So, I won’t ever be allowed to draw anything on the home page, for the good of humanity.

As a designer, in many cases, I’m invisible. I can help with technology, but the technology is ultimately invisible. Many people really did enjoy the Martha Graham doodle, and I’ve got the quiet satisfaction that I helped make it possible.

<figure><img class="103670" style="margin: 0 auto" title="Blend Right In" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/854ac1ae-5c91-4bdb-a5ff-a0dad3ad772c/blend.jpg" alt="Blend Right In" width="500" height="333" align="middle" /><figcaption>Marcin says, “This is from the San Diego Zoo, 2009. I don’t photograph living creatures often, but when I do, it’s usually a lot of fun.” (Image: Marcin Wichary)</figcaption></figure>

**Question: What is the Crushinator?**

**Marcin:** \[Laughs\] Okay, so that’s actually the \[name of the animation\] technique that I just described. I’m trying to convince the Doodle team to set up a proper blog where they can talk about stuff like this, both as artists and technologists. The great thing about the Web is that you can always right-click, “View source” or “Inspect element” and try to figure it out. And, as a matter of fact, I do recall there being a blog post somewhere on the day that the Martha Graham doodle came out, where somebody reverse-engineered the whole thing to figure out how it works. They didn’t know that the technique was called Crushinator because that’s my stupid *Futurama* reference.

**Question: I think that the Crushinator, as you call it, and this style of JavaScript-powered sprite animation are actually a very innovative animation style that is lightweight and available cross-browser, as you’ve said. Do you see the potential for that technique to become a widely adopted tool for animation on the Web?**

**Marcin:** I don’t think about it that way, because it’s kind of what I do. I’ve been doing Web development for many, many years. A lot of Web development is, as I mentioned, putting [technologies] together and seeing what happens. After a while, I developed an attitude that pretty much nothing’s impossible. You know that with HTML5 around and all of these cool things happening in the browser, something’s probably gonna help you. So, I do a lot of putting things together, and they actually don’t seem like that big a deal to me because that’s what I do. And sometimes you just throw [your experiment] at random people inside Google, and some of them become more popular, and others nobody cares about. So, I don’t think I’m the right person to talk about whether anything that I hack together has more utility than anything else. A lot of what I’m hoping to do with this kind of random hackery is figuring out, how can we push HTML5 further this week? You know, just hoping to inspire some people.

**Question: Well, I think you should give yourself some credit. Some of the work you guys are doing is very innovative. And it’s also very visible; it gets a lot of attention. There’s potential there for you to be a real influencer of these kinds of technologies.**

**Marcin:** I’m kind of recognizing that, for better or worse, people sometimes come to me and treat me as if I know something about what I’m doing. \[Laughter\] And maybe I do. Sometimes I feel like it’s my first day with a new video game, and I’m just randomly pressing buttons and things happen on the screen and I don’t know exactly why, but it’s cool, right? Because HTML5 is cool.

<figure><img title="creatures3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f425d17-be45-4e40-a630-30c70d4d5eaa/creatures3.jpg" alt="" width="500" height="500" /><figcaption>“This is a photo a friend and I took of me against a Cylon replica. This is a dramatic recreation of my typical day.” (Image: Marcin Wichary)</figcaption></figure>

**Question: What is the most useful usability or user experience finding you have learned recently?**

**Marcin:** There are a number of those, but unfortunately, I can’t really talk about them because they are internal.

But… this is going to sound funny. A while back, there was this report that came out — <a href="https://www.princeton.edu/main/news/archive/S28/82/93O80/index.xml?section=research">from Princeton University</a>, I think — that said using Comic Sans will make your material easier to remember. The harder your typeface is to read, the better the chance that people will remember what you wrote. And everybody I know perversely sends me links to this study, even literally last week, because they know how much I hate Comic Sans… [Laughter] … with passion. And people are sending this study to me, saying “You were wrong, and we were right.” You know, tongue in cheek.

But of course, that really isn’t what the study is about. First of all, you don’t have to use Comic Sans. Second of all, it’s just one factor, the same way there’s typically always a battle between usability and security, right? In order to make things more secure, sometimes it means you have to make them less usable. Like the simple fact that whenever you type a password, you can’t see it. It’s asterisks or dots or whatever, because it makes it harder for other people to eavesdrop on you. But it also makes it easier for you to mistype. So there’s a ton of these kind of choices that you have to make. You have to find a nice medium between security and usability. Those decisions are really, really hard and require a lot of thought. So, the same thing with Comic Sans and that study. You could use another font. Or use Comic Sans &mdash; it will make the learning easier. That‘s cool. But if your students develop an intense hatred for typography in general or design or, I don’t know, the universe, \[Laughter\] I don’t think you’ve won much. I‘m kind of tongue in cheek now, too. But not really.

**Question: When did your interest in code and computer programming begin?**

**Marcin:** It actually all kind of ties together in a number of funny ways. When I was very little, my dad had the best job ever… for a nerd like me. His job was fixing arcade games and pinball machines. So, I could follow him to all of these little arcade parlours in Poland, where I’m from. I could play for free, first of all, which was awesome. But actually, I much preferred watching other people play games. Of course, I would play games &mdash; I loved games and still do. But I could also get a little sneak peek — if you opened the arcade game, what happens there? If you went into debug mode or testing mode, which many of the arcade games had, there were a number of tools, if you had access to them, to see the graphic elements in the video game, the sound effects and all of the settings. And I was fascinated! It was like looking under the hood of a car &mdash; except, you know, a much cooler car. Maybe that’s what got me into computers.

As I was finishing my computer science degree in Poland, working on my Masters, I discovered this whole area of human-computer interaction &mdash; which people work on for a living, and it’s important, and it matters, and you can make a career out of it. That was a revelation to me. Suddenly, the past God-knows-how-many years that I was doing [amateur computer programming] were cast in a very different light.

<figure><img class="103671" style="margin: 0 auto" title="Photo by Marcin Wichary" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb5259ea-28ae-4b8c-93bf-3be4760d3de7/wichary.jpg" alt="Photo by Marcin Wichary" width="427" height="640" /><figcaption>Marcin says that photos like this one are an attempt to “anthropomorphize machines.” (Image: Marcin Wichary)</figcaption></figure>

{{% ad-panel-leaderboard %}}

**Question: Do you think that when you were in that arcade in Poland, when you were a kid, and you were watching a patron play Space Invaders, that you were monitoring the user experience by watching that person play?**

**Marcin:** Maybe! It’s an interesting thing. I used to be fascinated by books by the Polish author Stanisław Lem. Probably my favorite book of his is called *Tales of Pirx the Pilot*. I was fascinated by it because it’s about space and aliens and the future &mdash; it was awesome for a kid. But reading this book today, the whole theme is Pirx interacting with machines. The machines are robots, or spaceship A.I., but it really is about human-computer interaction. And the question now is whether I was already interested in that when I was very little. Or maybe the books actually shaped me. Or maybe it was both. And the same maybe with the arcades. Maybe I was watching people play and kind of thinking about what it meant. Or maybe I was so inspired by how much fun you could have with technology and how much delight that I started trying to do it myself in whatever way I could &mdash; and today it happens to be HTML5. And who knows what’s gonna happen ten years from now.

**Question: What do you think the Internet might look like at that time?**

**Marcin:** That’s always pretty tricky! I actually make a point of not trying to predict the future because I’m really terrible at that. But I can tell you one thing I’m excited about. A number of things are happening right now that get me really excited about the idea of computer-user interfaces that for the first time don’t feel like they’re coming out of a computer. One idea is that the retina display and other technologies that will probably arrive make it very easy to put something on the screen that mimics the imperfections of the real world. Maybe the typography doesn’t have to be so perfect, because it’s never so perfect in books. Maybe there’s gonna be something with interfaces being actually broken in some way — broken to mimic real life, not broken because we’re bad at developing things.

I’m especially excited about the implication of this in relation to typography. Over the course of hundreds of years, we built up \[a typographic practice\] with total nuance, with a lot of history, and we arrived at this very rich era where typography is amazing, right? It can do so much. There’s so much history there and so much beauty. And then the computer came around in the nineteen eighties and took all that away! \[Laughter\] You got monospace fonts and “underline”… Now we’ve got Unicode, and HTML5/CSS3 allow you to use different typefaces, and maybe, slowly, we’re gonna get all of this back again — and maybe even more. Maybe we’ll get all of the things we love in books and all of the things we love in computers combined.

**Question: Can you give me an example of a day in the life of Google’s UX design team?**

**Marcin:** There’s really no template for a day. Probably the most important part of my day, and the one I treasure most, is just talking to other designers. Either ranting like we do about everything that has to do with design, [Laughter] or showing them something I’m working on and getting feedback. We have so many amazing kinds of designers here.

For me, a lot of the day is spent staring at a computer. In my case, it’s a lot of HTML5, so some kind of text editor is in front of me &mdash; or, in some cases, Photoshop. I’ve spent so much time in HTML5 that it’s actually easy for me to just treat it as a design tool.

**Question: What else can you tell me about your set-up and workflow at Google?**

**Marcin:** I’ve always had a kind of low-level, old-school approach. I coded one site in FrontPage many, many years ago. \[Laughter\] But ever since then, I’ve pretty much coded everything by hand, from scratch, in a very simple text editor. These days it happens to be TextMate, although I don’t actually use any of the advanced TextMate features. I feel that gives me more control.

I actually make a point of starting things from scratch, even if they have been written elsewhere, or even by me before, because it allows me &mdash; you know, in a fast-moving environment where HTML5 and CSS3 change a lot &mdash; it allows me to learn all of those new things, to try a different approach, to think about how I did it the last time and try to do it differently, just for the sake of doing it differently. And that always feels really great. That approach probably only works for, like, little projects, little goofy experiments that I do. I don’t know… you can’t really rewrite Gmail every single month from scratch. [Laughter] But it’s kind of been working for me.

Other than that, it’s really very simple. Browser in one window, TextMate in another window, and a lot of Command-Tab’ing and a lot of Command-R’ing. You know, simple old habits. Muscle memory.

I have a couple of little tools that I made for myself and others at Google that I should open source, and I feel really bad for not having done that. One of them has another funny name. It’s called Transmogrifier, which is a nod to *Calvin and Hobbes*, which I love a lot. It’s a little tool that allows me to very easily test different types, or different parameters of my prototypes. You know, JavaScript is not very good at CGI parameters, so Transmogrifier gives me this nice UI, and I don’t have to worry about the innards and switching and hiding the options panel. I just plug in one line of JavaScript, and the tool takes care of most of that for me.

A number of other tools are floating around at Google that are pretty great, and I helped with some of those. And writing tools is actually a cool experience, too. You can learn a lot. Like, for example, writing a tool that you can embed in another page and it doesn’t ever break that page. This should be super-easy, but it’s not, with cascading styles just waiting for you to trip up. So, you can learn a lot of different skills.

**Question: Google has a reputation for reliance on data and intensive testing of products and design. How does this affect the user’s experience of Google websites?**

**Marcin:** We’ve historically been very focused on the efficiency of user experiences. For a lot of the products we have, including Google Search, our main consideration was the efficiency of getting to the proper response as fast as possible, and the answer being as precise as possible. We’ve gotten a lot of different comments over the years, with people suggesting that we don’t design our interfaces, that they kind of just *are* &mdash; they just exist. In most cases, the most deliberate design decision on our part is for our interfaces not to feel like they’re designed. They will seem more objective. Less editorialized. Relying on data is a very important part of this.

We’ve been looking at this in more detail recently. We’ve been thinking that, maybe for some of our projects that we’re working on currently, we should approach design a little bit differently. It’s going to be very interesting to see what happens.

**Question: How did your interest in photography come about?**

**Marcin:** I’ve always dabbled in photography. Back when I was in Poland, we had one of the first digital cameras &mdash; you know, a very primitive one with half a megapixel or whatever. But I never really considered myself a photographer. Really, it was kind of an impulse buy in late 2007, as I was heading out on a trip to New York. I started chatting with a friend of mine who is a photographer, and I ended up overnighting my first DLSR with my first lens, and I kind of fell in love with it.

<figure><img title="Piano Photo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3963e59d-4884-4400-b890-5b6e4796bc93/piano2.jpg" alt="Piano Photo" width="500" height="333" /><figcaption>“I am sure no one played [this piano] seriously for a long, long time, so I did. I just sat down and started playing — the sonatas I’ve learned, the things I’ve put together myself. I had to be a bit creative, since some of the keys no longer worked.” (Image: Marcin Wichary)</figcaption></figure>

I play piano occasionally, and I’m terrible at it. I think I’m good at being terrible at it, trying to figure it out on my own. When playing piano, the most interesting part to me is emotion. Can I learn to play things that mean a lot to me? Or can I compose something in which I evoke a certain emotion in other people — or even in myself? It’s less to do with technical proficiency.

In photography, what I realized is that the technology is the driver for me. A big part of me is fascinated with the technology of photography. I know that’s not true for other people. Maybe other people are interested in emotion or some other things.

Photography has been around for much, much longer [than computers], and it’s great to realize that there’s so much to photography that you could pretty much learn something new forever. Not only is there already so much that’s happened, but it’s also still happening right now. We’re at this really, really amazing time when digital photography is becoming commonplace — it’s already commonplace. What that means is that first of all, we have photographers everywhere, which is great. It’s gonna be exciting to see what happens in the next couple years, or ten years, or twenty years. And that’s another thing that gets me excited about photography in the same way I’m excited about HTML5 — because the best is yet to come.

## More Information

*   [Marcin’s website](https://www.aresluna.org/ "Marcin’s Website")
*   [Marcin and Ryan’s Google Pac-Man I/O presentation](https://youtube.com/watch?v=ttavBa4giPc "Google I/O 2011: The Secrets of Google Pac-Man: A Game Show ")
*   [Ryan Germick explains the Crushinator](https://www.magneticstate.com/blogdept/2011/crushinator "Ryan Germick Explains the Crushinator")
*   [Marcin’s Pac-Man bug story](https://www.aresluna.org/stories/blocked/ "Blocked: The Pac-Man Bug Story")
*   [HTML5 Presentation created by Marcin and Google Chrome team](https://github.com/html5rocks/slides.html5rocks.com "HTML5 Slide Deck")
*   [Marcin talks Pac-Man, HTML5 and more](https://ajaxian.com/archives/web-ninja-interview-marcin-wichary-creator-of-google-pacman-logo-html5-slide-deck-and-more "Marcin Wichary Ajaxian Interview")

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Things You Didn’t Know Your Doodles Could Accomplish](https://www.smashingmagazine.com/2013/10/things-you-can-accomplish-with-hand-sketching-doodling/)
*   [Retro Video/DOS Games For The Weekend](https://www.smashingmagazine.com/2010/10/its-retro-video-dos-game-day-take-a-stroll-down-memory-lane/)
*   [50 Incredible Photography Techniques and Photo Tutorials](https://www.smashingmagazine.com/2009/04/the-ultimate-photography-round-up/)
*   [What Is User Experience Design? Overview, Tools And Resources](https://www.smashingmagazine.com/2010/10/what-is-user-experience-design-overview-tools-and-resources/)

{{< signature "al, mrn" >}}
