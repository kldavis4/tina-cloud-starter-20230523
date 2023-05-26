---
title: 'Smashing Podcast Episode 38 With Ivan Akulov: Why Is My React App Slow?'
slug: smashing-podcast-episode-38
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6db8029d-7039-4beb-b787-f3a0df852f12/smashing-podcast-episode-38.jpg
date: 2021-06-01T14:00:00.000Z
summary: >-
  In this episode, we’re talking about React performance. What factors slow our React apps down, and how can we fix it? Drew McLellan talks to expert Ivan Akulov to find out.
description: >-
  In this episode, we’re talking about React performance. What factors slow our React apps down, and how can we fix it? Drew McLellan talks to expert Ivan Akulov to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re talking about React performance. What factors slow our React apps down, and how can we fix it? I spoke to expert Ivan Akulov to find out.

<iframe src="https://share.transistor.fm/e/3dc49f07/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- Ivan [on Twitter](https://twitter.com/iamakulov)
- Ivan’s consultancy [PerfPerfPerf](https://3perf.com)
- Smashing Workshop [The React Performance Masterclass](https://smashingconf.com/online-workshops/workshops/ivan-akulov#/) [SOLD OUT]

### Weekly Update

- [A Guide To Undoing Mistakes With Git (Part 2)](https://www.smashingmagazine.com/2021/05/undoing-mistakes-git-part2/) written by Tobias Günther
- [Accessible SVGs: Perfect Patterns For Screen Reader Users](https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/) written by Carie Fisher
- [How To Build And Launch Powerful Responsive Websites With Editor X](https://www.smashingmagazine.com/2021/05/build-launch-responsive-websites-editorx/) written by Miroslav Bekyarov
- [Useful VS Code Extensions For Front-End Developers](https://www.smashingmagazine.com/2021/05/useful-vs-code-extensions-web-developers/) written by Cosima Mielke
- [Adding A Commenting System To A WYSIWYG Editor](https://www.smashingmagazine.com/2021/05/commenting-system-wysiwyg-editor/) written by Shalabh Vyas

## Transcript

<p><a href="https://twitter.com/iamakulov"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d33601a9-8108-4c47-a74e-2434fd398059/ivan-akulov-250x250.jpg" width="200" height="200" alt="Photo of Ivan Akulov" /></a><span class="smashing-tv-host">Drew McLellan:</span>  He’s a Google developer expert, full-stack software engineer, and a performance consultant, and he’s the founder of web performance agency, PerfPerfPerf. He spends much of his time elbow deep in JavaScript and has contributed to different open source projects, often with a performance focus. We know he knows his stuff when it comes to web performance, but did you know he once rescued a panda from a rooftop using only a pogo stick? My smashing friends, please welcome, Ivan Akulov. Hi Ivan. How are you?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Smashing. Thank you.

<span class="smashing-tv-host">Drew McLellan:</span> I wanted to talk to you today about web performance, because that’s your professional focus and your area of expertise. But in particular, about performance with React. How much of your work involves working with reactive framework such as React? Is it something that’s becoming a lot more common?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. I think it’s 50-50. I think half of my work is dedicated to helping clients with low net performance and another half of my work is dedicated to helping clients with React runtime performance.

<span class="smashing-tv-host">Drew McLellan:</span> Is it increasing? Is that balance increasing? Do you see more clients adopting React over traditional methods or over other frameworks?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Well, to be honest, it’s hard to compare React with other ... There are two ways to answer this question. The first one is whether React is getting more popular than traditional like JavaScript libraries, jQuery, et cetera. That’s definitely true. That’s been going on for a while. Another one is whether React, like direct gross or false compared to Vue and other frameworks.

<span class="smashing-tv-speaker">Ivan Akulov:</span> To be honest, no. It’s really hard to judge from my corner. What I know is that React definitely seems to be most popular framework. Also, I have a few friends from different parts of the world and this is actually not true for different geographies. For example, In Georgia, which is the country, not the US State. As far as I remember, most of the local developers use Angular, and that’s fairly interesting. I came to do React talk there once, and the folks who were organizing, they went and told me that it will be harder to find attendees because React is not so popular with them.

<span class="smashing-tv-host">Drew McLellan:</span> That’s really interesting. IF someone was to come to you and say, "Hey Ivan, you’re a handsome man. Why is my React app slow?" Where would you start to look? Are there main sorts of problems that developers run across when it comes to React?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. When a developer comes to me and asks, "Hey my app is slow. Why is it happening? How can we approve it?" My first step would be to reproduce that locally. When I reproduce that locally, I would record from dev tools, performance profile, and React DevTools performance profile. So, that would be my two primary tools.

<span class="smashing-tv-host">Drew McLellan:</span> You mentioned React profiling tools, what do those tools tell you? Do they tell you, like for example, which components are being slow inside your app?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. My first step would be to look into the React DevTools. React DevTools have two types. They have the components tree tab, which are obviously all the components that you have on the app, obviously. There’s also a tab called profiler, which lets you record the profile of how the app renders, like how many times it renders, which components take the most time out of each render.

<span class="smashing-tv-speaker">Ivan Akulov:</span> My first step would be to reproduce that issue that the developer came to me with. Record a profile in session of it using React profiler, and then look into what exactly is happening. Typically, there are two primary issues that are making this slow, two low-hanging fruits that you would focus on first.

<span class="smashing-tv-speaker">Ivan Akulov:</span> The first one is components that are taking too much time rendering and that may be for multiple reasons. Perhaps there’s just a single component that’s doing something expensive. I had one client who ... Well, it’s basically the client that was a static site rendered through the React. What they were doing, they will login articles from the server, in the markdown format. And then they were parsing that markdown into HTML. They were converting that markdown into the HTML on the client, because the article is very large that were taking a few 100 milliseconds. That single component of parsing articles was taking a few 100 milliseconds to render. That’s one example.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Apart from a single component being slow, there could be just subarrays of components rendering unnecessarily and being a bottleneck. Another thing that happens is cascading renders. That’s when you’re doing a single action in the app, and that schedules a few renders one after another. So, there again might be a bunch of reasons for that. There are a lot of ways that could happen. That’s another thing I would look into and I would try to reduce the number of renders or move unnecessary renders scheduled by React.

<span class="smashing-tv-host">Drew McLellan:</span> Are there things you can do in the design of an Apple, the design of a page in traditional terms to make sure that you’re not running into these sorts of performance problems?

<span class="smashing-tv-speaker">Ivan Akulov:</span> In the design, you mean the UI/UX, right?

<span class="smashing-tv-host">Drew McLellan:</span> Yeah, in the user interface. Are there sort of common traps that is easy to fool into that would make a page, might cause unnecessary re-renders or things like that?

<span class="smashing-tv-speaker">Ivan Akulov:</span> I’m not sure. I can’t think of anything right now.

<span class="smashing-tv-host">Drew McLellan:</span> I had an issue, not in React, but in Vue. I’m a recovering React engineer. I work mostly in Vue now. I’ve dealt with some pages where I had a big list of data, and each line in the listing was a component that was being rendered, and this page might be 1,000 items long in some cases. You get that one component rendering 1,000 times. In situations like that, are there ways that you can architect it differently so that, that’s not a problem?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Right. Yeah. There are different ways to solve it. I can only call solution for this when you have a table with a huge number of rows or columns, or at least with a huge number of rows is virtualization, which is basically you take a library of React. We need to do a React virtualized and you have the list with it.

<span class="smashing-tv-speaker">Ivan Akulov:</span> What the library does is it uses the intersection of your API to find which components are off-screen, which components are on-screen, and it renders on the components that are on-screen. If you have a list of, say, 1,000 items, but at any given moment you could unlist 10 items, then that library would make sure that only 10 of these right items are rendered into the DOM. You get significantly smaller DOM tree, which helps with stellar calculations, which helps with layout recalculations, and a bunch of other stuff. You also get smaller React component tree, which helps with the React reconciliation and similar stuff.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Now, the API for this, which works a bit differently, but which is perhaps market-oriented is the recently-introduced content visibility API. So, this is a CSS property that was added into browsers, into Chrome half a year or a year ago. So, what it does is basically does the same thing that these libraries do. However, what it doesn’t practice is that it makes sure that the off-screen nets are not rendered. So, the browser skips them or ignores them completely.

<span class="smashing-tv-speaker">Ivan Akulov:</span> This also helps to reduce the rendering costs significantly. This is not going to help to reduce the React on a rendering cost; React would still reconcile the whole tree and arrange old relevant nodes of 1,000 components. But if your expensive part lies in the browser rendering and not in direct rendering, then that’s going to help.

<span class="smashing-tv-host">Drew McLellan:</span> That sounds promising, and that’s a native browser API, isn’t it, rather than part of React?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yes, exactly. It’s a single CSS property. There’s actually two CSS properties. The first property is called literally content-visibility. And the second one, I think, content-intrinsic-height, content-intrinsic-width, so two properties. The complex part, the complex thing about ... Actually, the challenging thing about both content visibility and about virtualization is that you can’t really do that if your list items have dynamic height, or dynamic width, if that’s the reason at least. Or actually, you can’t do that. The browser can’t know the height and the width of an element unless you’re trying to reduce it. Either gain the virtualization approach or in the content visibility approach.

<span class="smashing-tv-speaker">Ivan Akulov:</span> The problem is that if you have items with running width or we’re running height, and you don’t know their heights, for sure, then virtualizing them is going to be hard, because the scroll bar would be jumping all the time while you’re scrolling that list, because the browser would be rendering this element, rendering this weight and adjusting the page height. That’s the challenge of that.

<span class="smashing-tv-host">Drew McLellan:</span> That always is a classic challenge with laying things out in the web, isn’t it? Knowing what the heights are before they’ve rendered, even down to images and things like that.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah.

<span class="smashing-tv-host">Drew McLellan:</span> One of the key differences, building on a framework like React compared with just building HTML and CSS, sort of standard server side rendered pages, is you sort of have this balancing act of the loading performance versus the runtime performance. Is there a way? Is one of those more important than the other? Should you optimize for a site being performant once it’s done its initial load? Or is loading priority more important to stop visitors go away before things even loaded? Or is it a balance of the two?

<span class="smashing-tv-speaker">Ivan Akulov:</span> It really depends. My opinion is that it really depends on what kind of thing you’re doing. If you’re a static site, or if you’re a site or an app, or something that needs to optimize for, say, SEO or showing ads in that ranking and ad cost, then loading performance is going to be more important too, because that’s what search ranking is based on. That’s what ad costs are based on.

<span class="smashing-tv-speaker">Ivan Akulov:</span> And if you’re doing stuff, if you’re a complex single page app, which users come to and do some stuff for a while. I know, you’re some graphics editor, you’re some whatever, you do some complex stuff with JavaScript, then trend performance is perhaps much more important, because that’s actually much harder to measure. The effect of that is much harder to measure.

<span class="smashing-tv-speaker">Ivan Akulov:</span> I believe that runtime performance is much more important here, because that’s what users ... Because that’s what affects the overall user satisfaction. And if you are slow, then users are going to leave the app to competitors, and are going to complain to you. Actually, that’s one way to measure that.

<span class="smashing-tv-host">Drew McLellan:</span> With single page applications, is there a meaningful way that we can assess performance across the different parts of the app? Say this part of our app is slow, or that part of our app is slow, and this part is fine. I mean, traditionally, we look at the pages to see how they perform. But in a single page app, hat you’re loading in isn’t just one page, it’s actually you’re scaffolding an entire framework to get to that initial render. So, is there a good way to approach measuring performance across an entire app?

<span class="smashing-tv-speaker">Ivan Akulov:</span> That’s a good question. So, there are a few ways to approach this. The first way is the simplest one, but probably it’s often not what you’re looking for. One thing that you could do is you could use the built-in browser API to collect core web vitals data and collect that data and save it somewhere like in the Google analytics or another storage, and aggregate that data and look at your first input delay, your cumulative layout shift across the whole time the app was rendered, etc, etc. but that’s a very high level review, and it’s perhaps not going to be what you’re looking for.

<span class="smashing-tv-speaker">Ivan Akulov:</span> If I was doing that, what I would probably do is I would focus on the specifics of my app. So, let’s say my app is some text editor. Then what really matters to me that very few user metrics that really matter to me, it’s input latency. The faster the text is rendered after I press a key, the better is the performance. There are perhaps a few other metrics like switching between different menus or applying formatting like bold or italic, or etc.

<span class="smashing-tv-speaker">Ivan Akulov:</span> What I would do in this case is I would try to measure the duration of each of these interactions. I would try to measure the input latency, the duration of renders between I press the key and between the key appears on the screen duration of like applying the bold styling, and etc. I would try to collect this metrics in any real user monitoring software, and I would look in that to figure out whether I’m fast or slow, or whether I’m getting faster or I’m getting slower.

<span class="smashing-tv-host">Drew McLellan:</span> Is it more a case of measuring the things that your users are perhaps interacting with, rather than looking at a page and say how fast this page, because that doesn’t really make any sense when you’ve got more interactive interface?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah, exactly. I’ve heard multiple times that for some complex apps, login time is actually not a concern because users are used to ... When you’re opening a Photoshop, your use of that Photoshop is taking a while to load. You’re used to seeing that loading placeholder. It’s definitely not an issue when you’re opening, say, Google ... Google Sheets is not the right example, but any web drawing software. Again, it takes a while to load, that’s fine. That’s fine as long as it actually works quickly after that. If it takes a while to load but it works quickly after that, then users are actually not going to complain, because they’re used to this behavior.

<span class="smashing-tv-host">Drew McLellan:</span> You mentioned input delay as you’re typing. I saw a tweetstorm of yours where you went into the subject of components that seem to react too slowly like typing in a text field and the letters taking time to appear. That’s obviously a performance issue, because on a regular web page, typing in a text field is instantaneous. So, what causes those sorts of slowdowns?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Just like with a generic correct performance, there are a lot of things that could cause that. What typically is happening when you’re typing into a text field and it takes a while to render that key that you’ve just pressed is that you’re running too much JavaScript when you’re handling that event. And there could be multiple reasons for that. You could be rendering too many components. Perhaps you’re pressing the key, and that saves the text input state in the Redux store. And that gives us the whole app to render, because I know that invalidates a large part of that Redux store.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Or perhaps you are scheduling a few renders one after another. Or perhaps there’s some third-party library that’s taken a while to recompute something. Really, there’s no unique answers. Actually, rendering performance is really challenging to me. I think in general in this part.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Loading performance is way easier to profile, it’s way easier to analyze, it’s way easier to measure. I think we actually see the effect of that, and that there’s way more content about loading performance, way more tools for loading performance. It’s way easier to measure and profile in that it’s pretty much identical for every application. No matter what application is, no matter what it’s written in, no matter what kind of stuff it does, they all load more or less the same way. Whatever the application is, you could always focus on the same things, and you could teach people the same things, and that would be all right.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Whereas with runtime performance, the specifics of the slowdowns and specific offering time challenges are super different with every app. They could be optimized to some basic stuff, but it’s super hard to talk about them on the higher level, because with every app, they’re different with every single app.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Actually, one of my challenges of them hoping to solve with the version that I’m doing is to give some kind of high level enough introduction to runtime performance that people who attend this workshop can learn that it can apply that to their applications with their specific challenges, and with their specific business logic.

<span class="smashing-tv-host">Drew McLellan:</span> If there’s things that you need to be particularly interactive and respond very quickly in terms of rendering, say, to take our example, again, of typing in a text field, and there is other work to be done that’s unavoidable. Is there a way of prioritizing one over the other in React? Can you say, "I need to do this render?", and then once that’s finished, now we do all this updating of state. Is that possible?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Sure, yeah. There are, again, a few ways to do that. The first one is the one React has been working on for a while, which is the concurrent mode and prioritizing stuff that happens on this screen compared to stuff that happens on this screen, and etc, etc. I’ll be honest, I don’t have much knowledge about it yet, mostly because it haven’t stabilized. It’s nice to know about that and I enjoy reading about it, but I don’t think it makes sense to teach about it yet, because that’s not something that you could take and apply right now, but it could change a lot before it’s released to the public.

<span class="smashing-tv-speaker">Ivan Akulov:</span> When React eventually releases the concurrent mode and the whole prioritization thing, that’s likely going to be the universal answer or one of the best answers. Until that, what we could do is we could delay the computations by doing some throttling or advancing, or moving expensive computations to web workers. Or if the expensive works goes not by JavaScript, but by reconfiguring styles and reconfiguring layout, which is actually super common problem in some apps when you’re manipulating with the DOM, and it ends up causing first calculations, then perhaps optimizing these issues.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. If we have a text editor, and we need to make sure we are typing into it quickly, what I will do is I will try to, or on as few code as possible in every key press. And everything that could be delayed, try to delay it by a few 100 milliseconds, or perhaps a couple seconds to make sure it only runs when the user has finished typing. That’s like a high level overview. Again, specifics really depends on the app. So, there could be better architectural solutions, but that’s what I would start with, or that would be what I look into first.

<span class="smashing-tv-host">Drew McLellan:</span> Because with every bit of JavaScript we add to an app, there’s a potential for it to get slower and slower and slower. Is there any way to claw that back? Is it possible for a React app to have like a perfect Lighthouse score, for example?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. That was actually something. Yeah, getting back to the text, just one thing that I forgot to mention is that if there’s a single isolated component, which has performance of which is super critical and we can’t make it fast with reg, then one thing that I would perhaps try doing is making it work without React at all. So, making it work with direct DOM manipulation and plain JavaScript and stuff like that.

<span class="smashing-tv-speaker">Ivan Akulov:</span> The reason for that is that while React is great in terms of maintainability, like the reason we’ve switched from jQuery to React was that React allows us to write a code that’s much more maintainable, much easier to support. It’s also way easier to accidentally introduce major performance bottlenecks with React. You could accidentally render the whole app or you could accidentally have a component that renders fairly frequently it does some expensive stuff.

<span class="smashing-tv-speaker">Ivan Akulov:</span> If you switch to that specific component to plain JavaScript, then the chances of it accidentally getting slow would be way lower. Getting back to Lighthouse score, that’s actually the approach we’ve taken with the 3perf.com site. I ran from this consulting agency, and it has its own site. So, just really upgraded that site in Gatsby, simply because I wanted to try that stack and it seemed nice, so I did that. And it worked really well in general, apart from one thing, which is the Lighthouse score.

<span class="smashing-tv-speaker">Ivan Akulov:</span> I built this over to Gatsby and deployed to amplify and ensure that the site loads quickly or renders quickly. But the Lighthouse score was bad due to time-to-reactive and to the working time metrics. While the site was rendering quickly, it was loading a huge JavaScript bundle after that, and that JavaScript bundle was executing and taking a while to execute, taking a while to render the same page that the user is already seeing.

<span class="smashing-tv-speaker">Ivan Akulov:</span> One thing I did was I threw a weight of JavaScript that my site was using. In my case, that was fairly easy to do, because there was almost no JavaScript. There was only a few interactive elements, and I replaced them with inline scripts, and that worked great. I settled on the JavaScript. There are Gatsby plugins for that, like Gatsby plugin, no JavaScript. That was one of the most significant wins in terms of loading point. So, I think my Lighthouse score jumped from 60 something to 90 something thanks to this single case.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Actually, I have a friend called Andrey Sitnik. He’s a front-end engineer. He’s fairly known in the Russian front-end community, and Andrei is known for the fact that he’s heavily advocated for using React less. Basically, whenever you open Twitter and whenever you see some conversation about React being slow, you could frequently see him mentioning that, "Hey, you don’t need React to this site at all, because this is a static site. Why are you using React here? Just use some good old web technologies and it will be way faster. Because you don’t need React on the client."

<span class="smashing-tv-speaker">Ivan Akulov:</span> I would say I agree with him. There are a lot of cases where React is convenient for development experience, and I would totally support using it for ... There are a lot of cases including static sites where React is convenient for development experience, but it doesn’t mean it needs to be served to the user. One thing that you could do is use React on the server. Use it to set template engine, basically, but don’t serve it to the client. If you can do that, then that would be one of the greatest loading performance things you can do.

<span class="smashing-tv-host">Drew McLellan:</span> So, your top tip for performance is to get rid of all the JavaScript?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Top tip for the React, where you should get rid of React. Yes.

<span class="smashing-tv-host">Drew McLellan:</span> One of the things you hear with people adopting a framework like React is that it can be done for performance reasons. It’s much easier to build an asynchronous experience and get faster sort of perceived performance if you have a powerful framework managing your state, rather than relying on a server rendered page, for example, to compile a complete page all at once. You can load in a framework, and then asynchronously populate it.

<span class="smashing-tv-host">Drew McLellan:</span> On the other side, you have people who put out warnings that their experiences are that a big React app can be really slow and can be really harmful to performance. With all things, probably, it depends what you’re doing. But going into it, is there a way to judge whether your use is going to be good for performance or bad for performance?

<span class="smashing-tv-speaker">Ivan Akulov:</span> That’s a good question, to be honest. I haven’t heard of cases. That might be totally perhaps my view is skewed because I’m typically working with slow apps, not with fast apps. But I’d be honest, I haven’t heard of cases where people would be switching to React because it’s faster than the original approach to it. People are definitely switching because it’s more convenient to open twice, or because it’s easier to write maintainable codes, or because the ecosystem is larger, or something like that. But I have heard of cases of switching because it’s faster.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Actually, the speed was a thing that was heavily promoted back when React was created, like the whole group, (?), etc, etc. But React, a few years after that mode was introduced, React ditched it, because they oriented themselves on the development experience. I’m not actually sure what they are into themselves with, but I remember that it was pretty concrete thing that they ditched that model because it was not what people were buying React for anymore.

<span class="smashing-tv-host">Drew McLellan:</span> Likely, React is always going to be a bit slower than the traditional, but it comes with lots of upsides as well in terms of developer experience and maintainable code.

<span class="smashing-tv-speaker">Ivan Akulov:</span> I think yes. Jeff Edwards has a great article that is called, Our Pit of Success, or something like that. And in the article, he mentions that programming languages and ecosystems have a term of a pit of success. For example, C++ has a pit of success, or a pit of despair of memory issues. Whenever you’re writing code in C++, it’s super easy to write some code that does some direct memory access, and they’re introducing some bugs, or vulnerabilities or whatever.

<span class="smashing-tv-speaker">Ivan Akulov:</span> You have to keep thinking, you have to constantly keep thinking to make sure you are not writing the code that introduces memory issue, that introduces memory bugs. I think the JavaScript, the single pit of success or a pit of despair. JavaScript and React system has a lot of benefits. Again, it’s maintainability, it’s everything we’ve talked about.

<span class="smashing-tv-speaker">Ivan Akulov:</span> I think a pit of despair that’s a trap that’s too easy to fall into, unless you’re actively thinking, and unless you’re actively preventing yourself from falling to it is making an app that slow either in terms of loading performance. Because it’s too easy to install some NPM dependency and import it into the bundle and sub it into 100 kilobytes or 185 kilobytes to a bundle. Or in terms of return performance, because it’s too easy to create a component that would render over time and run in way too many codes or whichever.

<span class="smashing-tv-host">Drew McLellan:</span> I came across your work first about a year ago when you posted a case study analyzing the performance of a Notion page. I think we all love Notion, and there’s probably not one person who doesn’t wish it was faster. don’t think this wasn’t paid work, was it? This was just an educational exercise?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. Occasionally, when I have time to try to do case studies for some popular sites, I tremendously enjoy doing that. It’s also great educational material for whoever finds it useful.

<span class="smashing-tv-host">Drew McLellan:</span> And is that the sort of process that you follow when beginning an assessment of any sort of apps performance? Is the case study with Notion, does that follow the same sort of process that you would follow for anything?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. The (?) process is that you identify an issue, you reproduce an issue locally. In case of Notion, it was the Notion page taken a while to load, and then you profile that with all the tools you have and try to find any low hanging fruits or not so low hanging fruits. Try to figure out how to cut off this fruit. So, that’s the high level review. There are a lot of specifics.

<span class="smashing-tv-host">Drew McLellan:</span> It was a very fascinating read, and I’ll put a link to that in the show notes so that people can go and look at it if they’ve not seen it. I saw that you mentioned that React 17 removed one of your favorite performance features last year. What was that about?

<span class="smashing-tv-speaker">Ivan Akulov:</span> React has went through a few generations of performance features. Like React 15, I think up to 15.5 had a built in powerful object which gave you way to measure the most expensive components or components that rendered unnecessarily. You could have written in the console something like perf dot ... I don’t remember the concrete guide. It was like measure something.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah, the idea was that, that was fairly convenient for detection, which components rendered unnecessarily. I see in which components rendered, but the resulting DOM tree was identical to the previous DOM tree. But then React removed that. I don’t know why. I wasn’t actively joining performance back then.

<span class="smashing-tv-speaker">Ivan Akulov:</span> React removed that. I think they also introduced React profiler back then. But also, at some point, they introduced a different API, which was user timing. The idea was that whenever you are running the development version of React and you are recording a performance trace with the Chrome DevTools performance tab. What React would do is it would measure, it would mark the beginning and the end of each components, when each component renders and when each component effects run, like componentDidMount, componentDidUpdate.

<span class="smashing-tv-speaker">Ivan Akulov:</span> So, it would measure the beginning and the end of each of these components, and it’s lifecycle hooks. And it would part put them into the performance recording using the user timing API. This was super convenient for debugging, because when you record a performance recording of a single render or whatever, and you open the main thread pane, and you look into it, what you would see is you would see a lot of wrecked internal code, like its fiber algorithm working on the components, calling array component.

<span class="smashing-tv-speaker">Ivan Akulov:</span> It would be super hard to identify where each component rendering starts, where each component rendering ends. But if you scroll a bit higher and open the user timing session that you would be able to see that straight ahead, and you would be able to match what’s happening in the user timing app scene, which component is rendering right here to what’s happened in the performance pane. If you see some expensive salary calculation of the performance pane, you would be able to just scroll a bit higher and see that, "Hey, this matches this specific component or this specific inode, componentDidMount virtually."

<span class="smashing-tv-speaker">Ivan Akulov:</span> So, this was super convenient for debugging, like particular performance issues. However, the problem with this was that for React developers, it was fairly hard to maintain. There was a GitHub discussion with the description, with the particular reasoning. What React ended up doing was they removed this API in React 17. Removed this future in React 17.

<span class="smashing-tv-speaker">Ivan Akulov:</span> So, right now in React 17, the only way to debug React performance is to use the React profiler. While this works great for a lot of things, there are a few use cases like seeing lifecycle hooks, which React profiler doesn’t measure or my chain. Figuring out why a specific component takes a while to render, which again, React profiler shows you that this specific components takes 30 or 300 milliseconds to render, but it doesn’t show why and to figure out why you have to switch back to the performance pane.

<span class="smashing-tv-speaker">Ivan Akulov:</span> So, with user timings, that was easy to match a specific component to what’s happening inside of that component, and without user timing, with just the React profiler that’s actually harder. It’s a pity it get removed.

<span class="smashing-tv-host">Drew McLellan:</span> How are things looking for the future of performance with React? Do you know of any features and changes that are coming that might help?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah. There are two things that I’m looking forward to. I think the one is the concurrent mode, which lets React prioritize some stuff over another stuff. I think the defer was happening of this screen. I haven’t been really following its development. I know that it’s mostly close to be released. It could take another year, perhaps, but it’s fairly close to getting released.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Another thing is the recently introduced theme, which is React server components. That’s actually the thing I’m really looking forward to. So there are two areas where React apps may be slow. The one is the runtime performance, and the other is loading performance. And loading performance is not only about the huge bundle and etc, etc, which everyone is talking about. But it is also about the bundle execution, and more importantly, the React hydration process.

<span class="smashing-tv-speaker">Ivan Akulov:</span> So, whenever you have a React app that’s server-side rendered, and you serve that page to the client, and then a large React server act to that page, what React does is it gets through the hydration process. It gets all the DOM nodes that have been already ordered render. It reconstructs the virtual DOM tray, and it reattaches this ... Or resource the relationship between its virtual DOM and the actual DOM nodes.

<span class="smashing-tv-speaker">Ivan Akulov:</span> The problem with its process is that this is the single most expensive process during page loading. IF you’re loading a page, and that page runs a few chunks of JavaScript, then that chunk of JavaScript is going to be the most expensive. It could easily take a few 100 milliseconds, or like a second on slower device. This means that for the whole second of the whole few 100 milliseconds, the page would not responsive. So, if the user tries to scroll it or interact with it during that time, then the page could just not respond at all.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Yeah, hydration is typically, one of the most expensive things, and it’s hard to optimize, because React needs to hydrate all these components. There are only a few things that you could do with it today. One thing is partial hydration, which is, if you have some pieces of the site or of the app that you don’t need to rehydrate, which can stay static, but you could write a bit of code around that and bailout these subarrays from rehydration. If these subarrays are typically expensive, then not rehydrating them would save you a lot of time. But this is actually hard to do nowadays. There are a few libraries for that, but this is not a popular approach. It’s hard to do. We could do that, but it typically requires writing your own code around the subarrays.

<span class="smashing-tv-speaker">Ivan Akulov:</span> What server rendered components are going to do is they are going to take partial hydration. They’re basically going to introduce partial hydration and a bunch of other benefits in the code. So, taking back that example that we’ve talked about earlier, like a static site, which loads a huge pile of markdown from the server, and then converts it to HTML during hydration.

<span class="smashing-tv-speaker">Ivan Akulov:</span> One way to avoid paying that cost is to turn that component that converts markdown into HTML into server rendered component and do this conversion on the server, and serve the concrete HTML to the client. Ad that will save you a few 100 milliseconds of the markdown, if the markdown blob is large.

<span class="smashing-tv-speaker">Ivan Akulov:</span> I’m really looking forward towards React server components. So, they are going to be great for a lot of reasons, but also particularly for making hydration less expensive.

<span class="smashing-tv-host">Drew McLellan:</span> That sounds really good. You’ve got a workshop coming up at the end of May with Smashing. And this being 2021, of course, it’s all online. It’s called the React performance masterclass. What sort of things would an attendee expect to learn?

<span class="smashing-tv-speaker">Ivan Akulov:</span> My goal with this workshop is to take a few apps, a few example of apps that have the same issues that I see in client apps over and over again and again, and to show attendees, to walk attendees through ... Actually, ask attendees to do the same optimization to their apps. But also to guide attendees and to walk attendees through my mindset, through my process, which I applied to solving to identifying and solving each of these specific problems.

<span class="smashing-tv-speaker">Ivan Akulov:</span> We’ll talk about issues like expensive renders, like when you have a component that takes a while to render, how to identify it, how to optimize it. We will talk about expensive effects like componentDidMount. If you use a glass component or if you use a functional component. We will talk about net server renders. What to do when you click a button and that causes the whole app to render, and that makes the app slow. We will talk about cascading renders when you’re scheduling a few renders in it all.

<span class="smashing-tv-speaker">Ivan Akulov:</span> We will also talk about hydration, and about operation, and what to do with expensive layout and stellar calculations, and how to identify them, how to fix them. That’s the problems I’m planning to show. Perhaps also something else if it fits. Well, we would also talk about bunch of solutions for that starting from partial hydration, which is for hydration going through ways to correct hooks and more advanced third-party libraries that help with optimizing net server renders and making the components render fast.

<span class="smashing-tv-speaker">Ivan Akulov:</span> We would walk through tools which help with detecting what specific color are rendered, white rendered. And we would also talk through solutions like virtualization or on the content visibility, CSS property, or other stuff. The CSS contained property, which is rarely used, and not really known trick, but it helps with performance optimization.

<span class="smashing-tv-speaker">Ivan Akulov:</span> We would also look at solutions like virtualization and content visibility. The content visibility, CSS property, and other stuff that helps with optimizing layout thrashing, optimizing expensive stellar calculations. That’s what I’m planning to talk about. But the primary focus would be on showing attendees the most common departments, the most common issues that happened, and specific ways to identify them, to profile them and to fix them. So, that’s my goal.

<span class="smashing-tv-host">Drew McLellan:</span> It sounds like that, yes, you’re going to equip attendees with everything they need to identify and fix their own performance problems, which sounds really great. So, I’ve been learning all about React performance today. What have you been learning about lately, Ivan?

<span class="smashing-tv-speaker">Ivan Akulov:</span> One experience that I’ve been having lately is ... I’ve been helping a client to optimize a large conflict point for their site. It’s actually not about React or performance of React. It wasn’t performance. They don’t use React at all. But the challenge is that we’ve done pretty much everything we could have done with their site like pretty much all the ...

<span class="smashing-tv-speaker">Ivan Akulov:</span> We’ve got pretty much all the low hanging fruits. We’ve optimized everything that makes sense. The page is actually so large that the browser renders eight in steps. It renders. It parses it in steps. It parses a few 100 lines, then it renders these few 100 lines, and it parses the next few 100 lines, and renders these few 100 lines. It renders the header fields. It renders some parts of the main content field. After that, then it renders another part of the main content.

<span class="smashing-tv-speaker">Ivan Akulov:</span> What this ends up doing is this chunk rendering and pushing to large conflict point way higher than I would expect it to be if the browser rendered everything in one go. I don’t see any typical reasons that they typically see in apps that would push that large conflict point higher.

<span class="smashing-tv-speaker">Ivan Akulov:</span> Anyway, what I’m doing right now is I am going deep into Chrome internals and trying to figure out what exactly it does when it’s rendering that page and why exactly the chunked rendering is happening and what we can do to make sure it doesn’t happen. To make sure the page renders in one go. Actually, there isn’t learning experience for me. I just hope I don’t need to compile from scratch.

<span class="smashing-tv-host">Drew McLellan:</span> Let’s hope so. If you, dear listener, would like to hear more from Ivan, you can find him on Twitter where he’s at @iamakulov. And his personal website is iamakulov.com. His agency, Perf Perf Perf, can be found on the web at 3perf.com. And if you like to find out more about Ivan’s workshop on React performance, you can find all the information at smashingconf.com. Thanks for joining us today, Ivan. Do you have any parting words?

<span class="smashing-tv-speaker">Ivan Akulov:</span> Take care, be fast, and enjoy your life.

{{< signature "il" >}}