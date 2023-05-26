---
title: Building An App In 45 Minutes With Meteor
slug: build-app-45-minutes-meteor
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97258973-fc41-4ac8-9eb0-df04099e1672/iphone-05.png
date: 2013-06-13T18:17:53.000Z
author: sacha-greif
summary: >-
  The other day, I finally accomplished one of my long-standing goals: to go from one of those “Wouldn’t it be cool…” ideas to a working, live app in less than 1 hour. 45 minutes, actually.
description: >-
  The other day, I finally accomplished one of my long-standing goals: to go from one of those “Wouldn’t it be cool…” ideas to a working, live app in less than 1 hour. 45 minutes, actually.
categories:
  - Mobile
  - Web Design
  - JavaScript
  - Apps
---

It all started with a <a href="https://designerpotluck.eventbrite.com/">design meet-up in San Francisco</a>. I can honestly say this was the best meet-up I’ve ever been to: Even though it was announced only two days in advance, more than 200 people RSVPed, and a good number of them showed up. It was a great chance to put faces to familiar names, as well as to make new friends.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Build Your Own Product Hunt With Telescope And Meteor](https://www.smashingmagazine.com/2015/02/build-your-own-product-hunt-with-telescope-and-meteor/)
*   [Building A First-Class App That Leverages Your Website](https://www.smashingmagazine.com/2016/02/building-first-class-app-leverages-website-case-study/)
*   [Four Ways To Build A Mobile Application, Part 1: Native iOS](https://www.smashingmagazine.com/2013/11/four-ways-to-build-a-mobile-app-part1-native-ios/)
*   [Facing The Challenge: Building A Responsive Web Application](https://www.smashingmagazine.com/2013/06/building-a-responsive-web-application/)

But I got to talking with so many people that I didn’t have a chance to get contact info for everybody. So, the next day, I asked the organizers about it and they suggested that everyone who attended leave a link to their Twitter account in a shared Google Doc.

{{% feature-panel %}}

That would work, but I was afraid it would prove to be too much effort. <strong>If I’ve learned one thing in my years as a designer, it’s that people are lazy</strong>. Instead, what if I built an app that lets the user add their Twitter account to a list in a single click?

The app would work something like this:

1.  The user signs into Twitter,
2.  A link to their Twitter profile appears on the page,
3.  That’s pretty much it!

With my list of requirements complete, I set to work to see how fast I could build this, and I thought it’d be interesting to walk you through the process.

At first, take a peek at how the final app looked like:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb1d1a1a-9611-498d-909f-d89e8e28bdce/whowasthere-ss-500.png"><img class="162210" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb1d1a1a-9611-498d-909f-d89e8e28bdce/whowasthere-ss-500.png" alt="Our very bare-bones (but working!) app." width="500" height="516" /></a><br>
<em>Our final bare-bones (but working!) app.</em>

You can also see a demo of the finished product, and find the <a href="https://github.com/DiscoverMeteor/twitterList">code on GitHub</a>. (<strong>Note:</strong> Give it some time to load. Apps hosted on Meteor’s free hosting service often slow down under a lot of traffic.)

A word of warning: This won’t be a traditional tutorial. Instead, it will be a play-by-play walkthrough of how I coded the app in one hour, including the usual dumb mistakes and wrong turns.</p>

## Introducing Meteor

I decided to build the app with <a href="https://meteor.com">Meteor</a>. Meteor is a fairly young JavaScript framework that works on top of Node and has a few interesting characteristics.

<a href="https://meteor.com/"><img class="162206" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f31204cb-d068-48f7-8e6e-8191b845c123/meteor-ss-500.png" alt="The Meteor homepage" width="500" height="288" /></a><br>
<em>Meteor’s home page</em>

First, it’s <strong>all JavaScript</strong>, so you don’t need to deal with one language in the browser and another on the server. That’s right: the same language you use to set up jQuery slider plugins can also be used to query your app’s database! The added benefit of this is that your app now has only a single code base — meaning you can make the same code accessible from both the client and server if you need to.

Meteor is also <strong>reactive</strong>, meaning that any change to your data is automatically reflected everywhere throughout the app (including the user interface) without the need for callbacks. This is a powerful feature. Imagine adding a task to a to-do list. With reactivity, you don’t need a callback to insert the new HTML element into the list. As soon as Meteor receives the new item, it automatically propagates the change to the user interface, without any intervention on your part!

What’s more, Meteor is <strong>real time</strong>, so both your changes and the changes made by other users are instantly reflected in the UI.

Like many other modern frameworks, Meteor also speeds up your Web app by transforming it into a single-page Web app. This means that instead of refreshing the whole browser window every time the user changes the page or performs an action, Meteor modifies only the part of the app that actually changes without reloading the rest, and then it uses the HTML5 pushState API to change the URL appropriately and make the back button work.

Not having to update the whole page enables another very powerful feature. Instead of sending HTML code over the network, Meteor sends the raw data and lets the client decide how to render it.

Finally, one of my favorite features of Meteor is simply that it <strong>automates a lot of boring tasks</strong>, such as linking up and minifying style sheets and JavaScript code. It also takes care of routine stuff for you on the back end, letting you add user accounts to the app with a single line of code.

I’ve been experimenting with Meteor for the past six months, using it first to build <span class="removed_link" title="https://telesc.pe">Telescope</span> (an open-source social news app), and then in turn using Telescope as a base to create <a href="https://sidebar.io">Sidebar</a> (a design links website), and I’ve just <a href="https://www.discovermeteor.com">released a book</a> about it. I believe that, more than any other framework, Meteor helps you get from idea to app in the shortest possible amount of time. So, if all of this has made you curious, I recommend you give it a try and follow along this short walkthrough.</p>

### Step 0: Install Meteor (5 Minutes)

First, let’s install Meteor. If you’re on Mac or Linux, simply open a Terminal window and type:

<pre><code class="language-markup">
curl https://install.meteor.com | /bin/sh
</code></pre>

Installing Meteor on Windows is a little trickier; you can refer to <span class="removed_link" title="https://win.meteor.com/">this handy guide</span> to get started.</p>

### Step 1: Create The App (1 Minute)

Creating a Meteor app is pretty easy. Once you’ve installed Meteor, all you need to do is go back to the Terminal and type this:

<pre><code class="language-markup">
meteor create myApp
</code></pre>

You’ll then be able to run your brand new app locally with this:

<pre><code class="language-markup">
cd myApp
meteor myApp
</code></pre>

In my case, I decided to call my app twitterList, but you can call yours whatever you want!

Once you run the app, it will be accessible at <code>https://localhost:3000/</code> in your browser.</p>

### Step 2: Add Packages (1 Minute)

Because I want users to be able to log in with Twitter, the first step is to set up user accounts. Thankfully, Meteor makes this trivially easy as well. First, add the required Meteor packages, <code>accounts-ui</code> and (since we want users to log in with Twitter) <code>accounts-twitter</code>.

Open up a new Terminal window (since your app is already running in the first one) and enter:

<pre><code class="language-markup">
meteor add accounts-ui
meteor add accounts-twitter</code></pre>

You’ll now be able to display a log-in button just by inserting <code>{{loginButtons}}</code> anywhere in your Handlebars code.

<span class="removed_link" title="https://telesc.pe/"><img class="162211" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9e1faf2-da1e-4063-b889-ba7e0cb50c17/accounts-ui-ss-500.png" alt="A more complex version of the accounts-ui widget, as seen in Telescope" width="500" height="378" /></span>
<em>A more complex version of the <code>accounts-ui</code> widget, as seen in <span class="removed_link" title="https://telesc.pe">Telescope</span>.</em>

I didn’t want to have to bother with styling, so I decided to also include Twitter Bootstrap with my app.

I went to the Twitter Bootstrap website, downloaded the framework, extracted the ZIP file, copied it to my app’s Meteor directory, and then hooked up the required CSS files in the head of my app’s main file.

Ha ha, not really. What is this, 2012? That’s not how it works with Meteor. Instead, we just go back to the Terminal and type:

<pre><code class="language-markup">
meteor add bootstrap
</code></pre>

## Client Vs. Server

I guess at this point I should briefly tell you more about how Meteor apps work. First, we’ve already established that a Meteor app’s code is all JavaScript. This JavaScript can be executed in the browser like regular JavaScript code (think a jQuery plugin or an <code>alert()</code> message), but can additionally be executed on the server (like PHP or Ruby code). What’s more, the same code can even be executed in both environments!

So, how do you keep track of all this? It turns out Meteor has two mechanisms to keep client and server code separate: the <code>Meteor.isClient</code> and <code>Meteor.isServer</code> booleans, and the <code>/client</code> and <code>/server</code> directories.

I like to keep things clean; so, unlike the default Meteor app that gets generated with <code>meteor create</code> (which uses the booleans), I’d rather use separate directories.

Also, note that anything that <em>isn’t</em> in the <code>/client</code> or <code>/server</code> directories will be executed in both environments by default.

Since our app is pretty simple, we won't actually have any custom server-side code (meaning that Meteor will take care of that part for us). So you can go ahead and create a new <code>/client</code> directory, and  move <code>twitterList.html</code> and <code>twitterList.js</code> (or however your files are called) to it now.</p>

### Step 3: Create the Markup (10 Minutes)

I like to start from a static template and then fill in the holes with dynamic data, so that’s what I did. Just write your template as if it were static HTML, except replace every “moving part” with <a href="https://handlebarsjs.com">Handlebars</a> tags. So, something like this…

<pre><code class="language-markup">
 &lt;a href="https://twitter.com/SachaGreif"&gt;Sacha Greif&lt;/a&gt;&lt;/p&gt;
</code></pre>

… becomes this:

<pre><code class="language-markup">
 &lt;a href="https://twitter.com/{{userName}}"&gt;{{fullName}}&lt;/a&gt;
</code></pre>

Of course, those tags won’t do anything yet and will appear blank. But we’ll match them up with real data pretty soon. Next, I deleted the contents of <code>twitterlist.html</code> and got to work on my HTML. This is the code I had after this step:

<pre><code class="language-markup">
&lt;head&gt;
  &lt;title&gt;Who Was There?&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div class="container"&gt;
    &lt;div class="row"&gt;
    &lt;div class="span6"&gt;
      &lt;div class="well"&gt;
        &lt;h4&gt;Did you go to the &lt;a href="https://www.meetup.com/Meteor-SFBay/events/115875132/"&gt;Designer Potluck&lt;/a&gt;? Sign in with Twitter to add your name.&lt;/h4&gt;
        {{loginButtons}}
      &lt;/div&gt;
      &lt;table class="table"&gt;
         &lt;tr&gt;
&lt;td&gt;
  &lt;a target="_blank" href="https://twitter.com/{{userName}}"&gt;&lt;img src="{{image}}"/&gt; {{fullName}}&lt;/a&gt;

&lt;/td&gt;
&lt;/tr&gt;
      &lt;/table&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
&lt;/body&gt;
</code></pre>

### Step 4: Configure Twitter Sign-In (3 Minutes)

You’ll have noticed the <code>{{loginButtons}}</code> Handlebars tag, which inserts a log-in button on your page. If you try to click it right now, it won’t work, and Meteor will ask you for additional information.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb78d1a-9378-4f6c-a1b9-daba223bf4b8/sm-meteor-app-1-tiny.png"><img class="162213" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f30080f-6991-4894-a837-3366e786fc06/twitter-error-ss-500.png" alt="You need to fill in your app's Twitter credentials." width="500" height="273" /></a><br>
<em>You’ll need to fill in your app’s Twitter credentials. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb78d1a-9378-4f6c-a1b9-daba223bf4b8/sm-meteor-app-1-tiny.png">Larger view</a>.</em>

To get this information, we first need to tell Twitter about our app. Follow the steps on the screen and create a new Twitter app; once you’re done, try logging in. If everything has worked right, you should now have a user account in the app!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4230827a-2a58-4e30-a18c-bf8bc9438742/sm-meteor-app-2-tiny.png"><img class="162214" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4ba7e1b-07fd-40dd-a106-2588767728fb/twitter-new-app-ss-500.png" alt="Creating a new Twitter app." width="500" height="324" /></a><br>
<em>Creating a new Twitter app. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4230827a-2a58-4e30-a18c-bf8bc9438742/sm-meteor-app-2-tiny.png">Larger view</a>.</em>

To test this out, open your browser’s console (in the WebKit inspector or in Firebug) and type this:

<pre><code class="language-markup">
Meteor.user()
</code></pre>

This will retrieve the currently logged-in user, and, if everything has gone right, it will give you your own user object in return (something like <code>Object {_id: "8ijhgK5icGrLjYTS7", profile: Object, services: Object}</code>).</p>

### Step 5: Split It Into Templates (5 Minutes)

You’ll have noticed that our HTML has room to display only a single user. We’ll need some kind of loop to iterate over the whole list. Thankfully, Handlebars provides us with the <code>{{#each xyz}}</code> … <code>{{/each}}</code> helper (where <code>xyz</code> are the objects you want to iterate on, usually an array), which does just that.

We’ll also split the code into a few templates to keep things organized. The result is something like this:

<pre><code class="language-markup">
&lt;head&gt;
  &lt;title&gt;Who Was There?&lt;/title&gt;
&lt;/head&gt;

&lt;body&gt;
  &lt;div class="container"&gt;
    {{&gt; content}}
  &lt;/div&gt;
&lt;/div&gt;
&lt;/body&gt;

&lt;template name="content"&gt;
  &lt;div class="row"&gt;
    &lt;div class="span6"&gt;
      &lt;div class="well"&gt;
        {{loginButtons}}
      &lt;/div&gt;
      &lt;table class="table"&gt;
      {{#each users}}
        {{&gt; user}}
      {{/each}}
      &lt;/table&gt;
    &lt;/div&gt;
&lt;/template&gt;

&lt;template name="user"&gt;
 &lt;tr&gt;
&lt;td&gt;
  &lt;a target="_blank" href="https://twitter.com/{{userName}}"&gt;&lt;img src="{{image}}"/&gt; {{fullName}}&lt;/a&gt;
&lt;/td&gt;
&lt;/tr&gt;
&lt;/template&gt;
</code></pre>

### Step 6: Hook Up Our Template (5 Minutes)

Our template is all set up, but it’s iterating over empty air. We need to tell it what exactly this <code>users</code> variable in the <code>{{#each users}}</code> block is. This block is contained in the <code>content</code> template, so we’ll give that template a <a href="https://docs.meteor.com/#template_helpers">template helper</a>.

Delete the contents of <code>twitterlist.js</code>, and write this instead:

<pre><code class="language-markup">
Template.content.users = function () {
  return Meteor.users.find();
};
</code></pre>

What we’re doing here is defining <code>Template.content.users</code> as a function that returns <code>Meteor.users.find()</code>.

<code>Meteor.users</code> is a special collection created for us by Meteor. Collections are Meteor’s equivalent of MySQL tables. In other words, they’re a list of items of the same type (such as users, blog posts or invoices). And <code>find()</code> simply returns all documents in the collection.

We’ve now told Meteor where to find that list of users, but nothing’s happening yet. What’s going on?

### Step 7: Fix Our Tags (5 Minutes)

Remember when we typed this?

<pre><code class="language-markup">
&lt;a target="_blank" href="https://twitter.com/{{userName}}"&gt;&lt;img src="{{image}}"/&gt; {{fullName}}&lt;/a&gt;
</code></pre>

The <code>{{userName}}</code>, <code>{{image}}</code> and <code>{{fullName}}</code> are just random placeholders that I picked for the sake of convenience. We’d be pretty lucky if they corresponded to actual properties of our user object! (Hint: they don’t.)

Let’s find out the “real” properties with the help of our friend, the browser console. Open it up, and once more type this:

<pre><code class="language-markup">
Meteor.user()
</code></pre>

The object returned has all of the fields we need. By exploring it, we can quickly find out that the real properties are actually these:

*   `{{services.twitter.screenName}}`
*   `{{services.twitter.profile_image_url}}`
*   `{{profile.name}}`

Let’s make the substitutions in our template and see what happens.

It works! Our first and only user (you!) should now appear in the list. We’re still missing some fields, though, and only the user’s full name appears. We need to dig deeper into Meteor to understand why.</p>

## A Database On The Client

We haven’t really touched on what Meteor does behind the scenes yet. Unlike, say, PHP and MySQL, with which your data lives only on the server (and stays there unless you extract it from the database), Meteor replicates your server-side data in the client and automatically syncs both copies.

This accomplishes two things. First, reading data becomes very fast because you’re reading from the browser’s own memory, and not from a database somewhere in a data center.

Secondly, modifying data is extremely fast as well, because you can just modify the local copy of the data, and Meteor will replicate the changes for you server-side in the background. But this new paradigm comes with a caveat: We have to be more careful with data security.</p>

### Step 8: Make the App Secure (1 Minute)

We’ll address data security in terms of both writing and reading. First, let’s prevent people from writing whatever they want to our database. This is simple enough because all we need to do is remove Meteor’s <code>insecure</code> package:

<pre><code class="language-markup">
meteor remove insecure
</code></pre>

This package comes bundled with every new Meteor app to speed up development (letting you insert data client-side without having to set up all of the necessary checks and balances first), but it is obviously not meant for production. And because <strong>our app won’t need to write to the database at all</strong> (except for creating new users — but that’s a special case that Meteor already takes care of), we’re pretty much done!

## More On Security

While we’re on the topic of security, Meteor apps also come with a second default package, <code>autopublish</code>, which takes care of sending all of the data contained in your server-side collections to the client.

Of course, for a larger app, you probably won’t want to do that. After all, some of the information in your database is supposed to remain private, and even if all your data is public, sending <em>all</em> of it to the client might not be good for performance.

In our case, this doesn’t really matter because we do want to “publish” (i.e. send from the server to the client) all of our users. Don’t worry, though — Meteor is still smart enough not to publish sensitive information, such as passwords and authentication tokens, even with <code>autopublish</code> on.</p>

### Step 9: Add Follow Buttons (8 Minutes)

<pre><code class="language-markup">
Template.content.users = function () {
  return Meteor.users.find();
};
</code></pre>

What we’re doing here is defining <code>Template.content.users</code> as a function that returns <code>Meteor.users.find()</code>.

<code>Meteor.users</code> is a special collection created for us by Meteor. Collections are Meteor’s equivalent of MySQL tables. In other words, they’re a list of items of the same type (such as users, blog posts or invoices). And <code>find()</code> simply returns all documents in the collection.

We’ve now told Meteor where to find that list of users, but nothing’s happening yet. What’s going on?

### Step 7: Fix Our Tags (5 Minutes)

Remember when we typed this?

<pre><code class="language-markup">
&lt;a target="_blank" href="https://twitter.com/{{userName}}"&gt;&lt;img src="{{image}}"/&gt; {{fullName}}&lt;/a&gt;
</code></pre>

The <code>{{userName}}</code>, <code>{{image}}</code> and <code>{{fullName}}</code> are just random placeholders that I picked for the sake of convenience. We’d be pretty lucky if they corresponded to actual properties of our user object! (Hint: they don’t.)

Let’s find out the “real” properties with the help of our friend, the browser console. Open it up, and once more type this:

<pre><code class="language-markup">
Meteor.user()
</code></pre>

The object returned has all of the fields we need. By exploring it, we can quickly find out that the real properties are actually these:

*   `{{services.twitter.screenName}}`
*   `{{services.twitter.profile_image_url}}`
*   `{{profile.name}}`

Let’s make the substitutions in our template and see what happens.

It works! Our first and only user (you!) should now appear in the list. We’re still missing some fields, though, and only the user’s full name appears. We need to dig deeper into Meteor to understand why.</p>

## A Database On The Client

We haven’t really touched on what Meteor does behind the scenes yet. Unlike, say, PHP and MySQL, with which your data lives only on the server (and stays there unless you extract it from the database), Meteor replicates your server-side data in the client and automatically syncs both copies.

This accomplishes two things. First, reading data becomes very fast because you’re reading from the browser’s own memory, and not from a database somewhere in a data center.

Secondly, modifying data is extremely fast as well, because you can just modify the local copy of the data, and Meteor will replicate the changes for you server-side in the background. But this new paradigm comes with a caveat: We have to be more careful with data security.</p>

### Step 8: Make the App Secure (1 Minute)

We’ll address data security in terms of both writing and reading. First, let’s prevent people from writing whatever they want to our database. This is simple enough because all we need to do is remove Meteor’s <code>insecure</code> package:

<pre><code class="language-markup">
meteor remove insecure
</code></pre>

This package comes bundled with every new Meteor app to speed up development (letting you insert data client-side without having to set up all of the necessary checks and balances first), but it is obviously not meant for production. And because <strong>our app won’t need to write to the database at all</strong> (except for creating new users — but that’s a special case that Meteor already takes care of), we’re pretty much done!

## More On Security

While we’re on the topic of security, Meteor apps also come with a second default package, <code>autopublish</code>, which takes care of sending all of the data contained in your server-side collections to the client.

Of course, for a larger app, you probably won’t want to do that. After all, some of the information in your database is supposed to remain private, and even if all your data is public, sending <em>all</em> of it to the client might not be good for performance.

In our case, this doesn’t really matter because we do want to “publish” (i.e. send from the server to the client) all of our users. Don’t worry, though — Meteor is still smart enough not to publish sensitive information, such as passwords and authentication tokens, even with <code>autopublish</code> on.</p>

### Step 9: Add Follow Buttons (8 Minutes)

While visitors can now click on a name to go to their Twitter profile, simply displaying follow buttons for each user would be much better. This step took a little tinkering to get right. It turns out that Twitter’s default follow button code doesn’t play nice with Meteor.

After 15 minutes of unsuccessful attempts, I turned to the Google and quickly found that for single-page apps, Twitter suggests using an iframe instead.

This worked great:

<pre><code class="language-markup">
&lt;iframe style="width: 300px; height: 20px;" src="//platform.twitter.com/widgets/follow_button.html?screen_name={{services.twitter.screenName}}" height="240" width="320" frameborder="0" scrolling="no"&gt;&lt;/iframe&gt;</code></pre>

### Step 10: Deploy (1 Minute)

The last step is to deploy our app and test it in production. Once again, Meteor makes this easy. No need to find a hosting service, register, launch an instance, and do a Git push. All you need to do is go back to the Terminal and type this:

<pre><code class="language-markup">
meteor deploy myApp
</code></pre>

Here, <code>myApp</code> is a unique subdomain that you pick (it doesn’t have to be the same as the app’s name). Once you’ve deployed, your app will live at <code></code>. Go ahead and ask a few people to register: You’ll see their Twitter profiles added to the list in real time!

## Going Further

Of course, I had to gloss over a lot of key Meteor concepts to keep this tutorial light. I barely mentioned collections and publications, and I didn’t even really talk about Meteor’s most important concept, reactivity. To learn more about Meteor, here are a few good resources:

*   [Documentation](https://docs.meteor.com), Meteor This is a required reference for any Meteor developer. And it’s cached, meaning you can even access it offline.
*   [EventedMind](https://eventedmind.com) Chris Mather puts out two Meteor screencasts every Friday. They’re a great help when you want to tackle Meteor’s more advanced features.
*   [_Discover Meteor_](https://www.discovermeteor.com) I’m obviously biased, but I think our book is one of the best resources to get started with Meteor. It takes you through building a real-time social news app (think [Reddit](https://reddit.com) or [Hacker News](https://news.ycombinator.com)) step by step.
*   [Blog](https://www.discovermeteor.com/blog), Discover Meteor We also make a lot of information available for free on our blog. We suggest looking at “[Getting Started With Meteor](https://www.discovermeteor.com/2013/01/30/getting-started-with-meteor/)” and “Useful Meteor Resources.”
*   “[Prototyping With Meteor](https://net.tutsplus.com/tutorials/javascript-ajax/prototyping-with-meteor/)” A tutorial we wrote for NetTuts that takes you through building a simple chat app.

I truly believe Meteor is one of the best frameworks out there for quickly building apps, and it’s only going to get better. Personally, I’m really excited to see how the framework evolves in the next couple of months. I hope this short tutorial has given you a taste of what Meteor’s all about and has made you curious to learn more!

<em>(il) (ea) (al)</em>

