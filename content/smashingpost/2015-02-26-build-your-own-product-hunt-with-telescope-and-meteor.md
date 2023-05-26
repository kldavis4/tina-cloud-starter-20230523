---
title: Build Your Own Product Hunt With Telescope And Meteor
slug: build-your-own-product-hunt-with-telescope-and-meteor
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d8a31f-78d2-4691-b1d0-ea115bc0089c/01-product-hunt-opt-small.jpg
date: 2015-02-26T22:57:32.000Z
author: sacha-greif
summary: >-
  Over in startup land, one of the big stories of 2014 was, without a doubt, the success of <a href="https://www.producthunt.com/">Product Hunt</a>. It's is a community where people post, vote on and comment on new products they’ve discovered or launched. Whether you’re looking for the next big thing to invest in or just want to find a better weather app, Product Hunt has got you covered.
description: >-
  Over in startup land, one of the big stories of 2014 was, without a doubt, the success of <a href="https://www.producthunt.com/">Product Hunt</a>. It's is a community where people post, vote on and comment on new products they’ve discovered or launched. Whether you’re looking for the next big thing to invest in or just want to find a better weather app, Product Hunt has got you covered.
categories:
  - Coding
  - Tools
  - Workflow
  - Techniques
---

Coincidentally, in addition to being a fan of the website, I also have a pretty personal connection to the company. I’ve been online friends with Product Hunt’s designer <a href="https://www.producthunt.com/Jonnotie">Jonno Riekwel</a> for years, and I was part of founder <a href="https://www.producthunt.com/rrhoover">Ryan Hoover</a>’s previous project, <a href="https://twitter.com/startupedition">Startup Edition</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c8c3ef8-987f-410b-99e8-74325e35d011/01-product-hunt-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d8a31f-78d2-4691-b1d0-ea115bc0089c/01-product-hunt-opt-small.jpg" alt="01-product-hunt-opt-small" /></a><figcaption>Product Hunt (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c8c3ef8-987f-410b-99e8-74325e35d011/01-product-hunt-opt.jpg">View large version</a>)</figcaption></figure>

All this to explain that Product Hunt has been on my radar for a while now. In fact, what many people don’t know is that <a href="https://ryanhoover.me/post/69599262875/the-wisdom-of-the-20-minute-startup">Ryan initially considered</a> basing Product Hunt on <span class="removed_link" title="https://telesc.pe">Telescope</span>, an open-source app that I had just started working on! Sadly, Telescope was still too immature at the time, and Ryan wisely decided to build his own solution.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Building An App In 45 Minutes With Meteor](https://www.smashingmagazine.com/2013/06/build-app-45-minutes-meteor/)
*   [A Guide To Personal Side Projects](https://www.smashingmagazine.com/2016/05/a-guide-to-personal-side-projects/)
*   [Design Principles To Evaluate Your Product](https://www.smashingmagazine.com/2015/12/design-principles-to-evaluate-your-product/)
*   [Building A First-Class App That Leverages Your Website](https://www.smashingmagazine.com/2016/02/building-first-class-app-leverages-website-case-study/)

{{% feature-panel %}}

But I’m here to tell you that things have changed. As we know, Product Hunt has gone on to become Silicon Valley’s latest darling. But Telescope has also kept quietly evolving, and it’s now a full-featured solution for people to build their own communities. So, today, let me show you how you too can set up your own personal Product Hunt-style website.</p>

## Introducing Meteor

Product Hunt wasn’t the only success story of 2014. Another one was certainly <a href="https://meteor.com">Meteor</a>, the company behind the open-source JavaScript framework of the same name. Meteor completely changes the way we write apps by getting rid of the age-old client-server divide. Unlike other JavaScript frameworks such as AngularJS and Ember.js, Meteor runs not only in the browser, but also on the server. So, with Meteor, not only is your whole app written in JavaScript, but you can even share the same code and call the same functions in both environments!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c077110-2476-4681-bf47-187f657e8986/02-meteor-homepage-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f416d0a8-6820-471b-9b2a-76f81f295623/02-meteor-homepage-opt-small.jpg" alt="02-meteor-homepage-opt-small" /></a><figcaption>The Meteor JavaScript framework (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c077110-2476-4681-bf47-187f657e8986/02-meteor-homepage-opt.jpg">View large version</a>)</figcaption></figure>

I decided to pick Meteor to build Telescope, and in fact I liked the framework so much that I ended up <a href="https://discovermeteor.com">writing a book about it</a>. But that’s a story for another time. Don’t worry: Meteor may be cutting-edge, but it’s also very approachable. Even if you’re not a JavaScript expert, we’ll have you up and running in no time (about 45 minutes, to be exact)!

## Installing Meteor

If you’re on Mac OS or Linux, installing Meteor is as simple as opening a Terminal window and typing:

<pre><code class="language-bash">
curl https://install.meteor.com/ | sh
</code></pre>

Though Meteor doesn’t quite support Windows yet, a <a href="https://github.com/meteor/meteor/wiki/Preview-of-Meteor-on-Windows">preview release</a> is available, and an official version should be coming very soon.</p>

## Installing Telescope

Next, you’ll need to clone Telescope’s code base <a href="https://github.com/TelescopeJS/Telescope">from GitHub</a>. Just type:

<pre><code class="language-bash">
git clone https://github.com/TelescopeJS/Telescope.git
</code></pre>

If you don’t have Git, you can <a href="https://git-scm.com/downloads">download the command-line utility</a> or use an app, such as the free <a href="https://mac.github.com/">GitHub for Mac</a>.

## Running Telescope

Almost there! First, drill into the newly created <code>telescope</code> directory with this:

<pre><code class="language-bash">
cd Telescope
</code></pre>

Then, run your app with this:

<pre><code class="language-bash">
meteor
</code></pre>

Your app might take a minute or two to initialize the first time. But once it’s done, your brand new Telescope app should be up and running! Head to <code>https://localhost:3000</code> to check it out.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e6b3f67-f605-4ec8-aecc-46f77f50a91c/03-telescope-fresh-install-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/924c0727-9abb-48b5-8bb7-46341d127827/03-telescope-fresh-install-opt-small.jpg" alt="Your new Telescope app" /></a><figcaption>Your new Telescope app (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e6b3f67-f605-4ec8-aecc-46f77f50a91c/03-telescope-fresh-install-opt.jpg">View large version</a>)</figcaption></figure>

If at any point you need to stop your Meteor app (maybe it’s crashed or you want to get the command prompt back), you can do so by opening the Terminal tab where your app is running and hitting <code>Control + C</code>.</p>

## Configuring Telescope

Let’s personalize the app a bit. The first thing to do is create a user account by clicking the “Sign Up” link in the top navigation menu. Because this will be the first user account you’ve ever created, it will automatically be assigned administrative rights, which will let you access Telescope’s admin area.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f06f6a19-3b14-4d11-a73d-cbf17477ae7e/04-telescope-settings-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f9da350-2041-4c4c-ad23-b502a9948b1e/04-telescope-settings-opt-small.jpg" alt="Telescope's settings panel" width="500" height="297" /></a><figcaption>Telescope’s settings panel (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f06f6a19-3b14-4d11-a73d-cbf17477ae7e/04-telescope-settings-opt.jpg">View large version</a>)</figcaption></figure>

Once your account is created, head to the “Settings” page via the “Admin” menu. There, you can set various options, such as your website’s title, description and color scheme.

For example, try setting the header’s color to <code>#1282A2</code> (or any other color!), and then click the “Submit” button at the bottom of the form.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c53d35-0b6a-4323-8803-afa81ad52669/05-telescope-color-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc212db1-4a26-4cd0-a708-b193729ccbc1/05-telescope-color-opt-small.jpg" alt="Customizing colors" /></a><figcaption>Customizing colors (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c53d35-0b6a-4323-8803-afa81ad52669/05-telescope-color-opt.jpg">View large version</a>)</figcaption></figure>

## Activating “Product Hunt Mode”

Telescope was originally based on the popular hacker hangout Hacker News, which is why the default view is just a uninterrupted list of posts. But with the success of Product Hunt, more and more people started asking for an option to use a day-by-day view, which I like to call “Product Hunt mode.”

To enable it, just go to the “Settings” page, scroll down to the “Default View” option, and set it to “Daily.” Save the settings and refresh the home page. You should now see a much nicer layout!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d38e2eda-6227-4cb0-a3d5-5452363690ae/06-product-hunt-mode-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb841396-e215-449f-9c21-306d058341e0/06-product-hunt-mode-opt-small.jpg" alt="Product Hunt mode" /></a><figcaption>Product Hunt mode (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d38e2eda-6227-4cb0-a3d5-5452363690ae/06-product-hunt-mode-opt.jpg">View large version</a>)</figcaption></figure>

## Deploying

Let’s show the world the result of our hard work. Deploying an app is usually a painful process, but not today. It turns out that Meteor provides its own free hosting service for quickly deploying small apps and prototypes.

Open a new Terminal window, browse to your app’s directory, and then type the following:

<pre><code class="language-bash">
meteor deploy my-app
</code></pre>

Replace <code>my-app</code> with the name of your app.

If this is your first time deploying on Meteor’s service, you’ll be prompted to create a <a href="https://www.meteor.com/services/developer-accounts">developer account</a>.

Once the deployment process is finished, your app will be live at <code>https://my-app.meteor.com</code>!

Note that the settings of a Telescope app are stored in its database, which is <em>not</em> transferred as part of the deployment process. So, you’ll need to re-enter any settings that you’ve previously set.</p>

## Customizing Your App With Packages

So far, we’ve changed the default view and tweaked a few colors. We can take things much further than that. Let’s start by adding a few extra CSS customizations.

To do so, we’ll create our own package. At this point, we could just go ahead and modify Telescope’s code, but that could lead to Git conflicts when we try to update the app down the road.

Instead, we’ll use Meteor’s package system to make sure that any customizations we implement stay independent of the main code base and will not be overwritten even when we pull in future updates.

By the way, the code for this tutorial is also available on GitHub.

Inside your app, locate the <code>/packages</code> directory, and create a new <code>telescope-custom</code> directory inside it (either with the <code>mkdir</code> command or by going to <code>File → New Folder</code>). From now on, we’ll put the files we create inside this directory.

Each Meteor package needs a file named <code>package.js</code>, which contains the package’s <strong>manifest</strong>, a simple set of instructions that tell Meteor what the package actually contains.

So, create the <code>package.js</code> file inside <code>telescope-custom</code>, and type the following:

<pre><code class="language-javascript">
Package.describe({
  summary: 'Telescope custom package',
  version: '1.0.0',
  name: 'telescope-custom'
});

Package.onUse(function (api) {  
  api.addFiles('custom.css', 'client');
});
</code></pre>

The <code>Package.describe</code> block provides some basic information about the package. But the interesting part is the <code>Package.onUse</code> block, which tells Meteor which files to load in our package. In this case, we’ll say we want to add a <code>custom.css</code> file.

Remember I said Meteor could handle code on both the client and server? This is why we have to specify <em>where</em> we want to add our files — in this case, on the client.

All that’s left is to actually create this <code>custom.css</code> file!

## Customizing The CSS

Let’s open the <code>custom.css</code> file we just created and add Product Hunt-style yellow hover states to each of our posts:

<pre><code class="language-css">
.post:hover{
  background: #fcf5e2;
}
</code></pre>

We’re almost done. We still need to tell Meteor that we want to use this new package. We can do so with the following command:

<pre><code class="language-bash">
meteor add telescope-custom
</code></pre>

Once you’ve added the package, your browser tab should automatically refresh, and you’ll see that our new yellow hover state is working!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47138593-a877-4dd3-a49a-e250d54c3607/07-telescope-hover-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d10955f3-566c-4271-b876-bcc59c0be88e/07-telescope-hover-opt-small.jpg" alt="Hover effect" /></a><figcaption>Hover effect (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47138593-a877-4dd3-a49a-e250d54c3607/07-telescope-hover-opt.jpg">View large version</a>)</figcaption></figure>

But wait, we didn’t even tell Meteor where to import that new style sheet from. How can that even work?!

This is one of Meteor’s cool time-saving features. It’s smart enough to notice when you add a new CSS file to your code base. It will automatically concatenate it, minify it and load it in your app.</p>

## Customizing Templates

A nice touch in Product Hunt’s UI is how it includes banners between days. It’s a great way to link out to other content and break up the monotony of listed links, while maintaining a clean layout and not disrupting the experience. Let’s see how to do the same thing with Telescope.

Telescope already has templates before and after each day, but the default templates are empty. So, our mission will be to override the <code>afterDay</code> template with one that contains actual content.

Add a <code>banner.html</code> file to your package, and add a simple banner:

<pre><code class="language-markup">
&lt;template name="banner"&gt;
  &lt;div class="custom-banner"&gt;&lt;a href="https://twitter.com/telescpe"&gt;Follow us on Twitter!&lt;/a&gt;&lt;/div&gt;
&lt;/template&gt;
</code></pre>

Next, we’ll tell Telescope to override the default <code>afterDay</code> template with this one. To do so, we create a new <code>banner.js</code> JavaScript file at the root of our package:

<pre><code class="language-javascript">
templates["afterDay"] = "banner";
</code></pre>

Before calling the <code>afterDay</code> template, Telescope will check in the <code>templates</code> array to see whether we have provided a replacement. And since we have, it will use the template code from <code>banner.html</code> instead!

We’re not quite done yet, though! Just as before, we need to add our new files to the package’s manifest. And this time, we’ll also need to add package <strong>dependencies</strong> to it.

We’ll add the <code>templating</code> package, which lets us use templates, as well as the <code>telescope-base</code> package, which exposes the global <code>templates</code> object that we’re calling in <code>custom.js</code>. So, let’s go back to <code>package.js</code> and modify its contents:

<pre><code class="language-javascript">
Package.describe({
  summary: 'Telescope custom package',
  version: '1.0.0',
  name: 'telescope-custom'
});

Package.onUse(function (api) {

  api.use('telescope-base');
  api.use('templating');

  api.addFiles('custom.css', 'client');
  api.addFiles('banner.html', 'client');
  api.addFiles('banner.js', 'client');
});
</code></pre>

Finally, let's add a little CSS for good measure. Go back to <code>custom.css</code> and add this:

<pre><code class="language-css">
.custom-banner{
  background: #c4e6ef;
  padding: 20px;
  text-align: center;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7c908c-8211-4c65-a184-12e3b54ce4bc/08-banner-repeated-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/275f9921-2d17-4ec1-a877-fe99268a8eda/08-banner-repeated-opt-small.jpg" alt="Twitter banner" /></a><figcaption>Twitter banner (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7c908c-8211-4c65-a184-12e3b54ce4bc/08-banner-repeated-opt.jpg">View large version</a>)</figcaption></figure>

## Adding Some Logic

Things are looking good, but you’ll notice that our banner is repeated after every single day.

This might get a little repetitive. Let’s see how to show our banner after only the third day.

To do this, we’ll need a bit of JavaScript magic. First, we’ll use Meteor’s templating logic (known as Spacebars) to add an <code>if</code> statement to the template:

<pre><code class="language-markup">
&lt;template name="banner"&gt;
{{#if isThirdDay}}
  &lt;div class="custom-banner"&gt;&lt;a href="https://twitter.com/telescpe"&gt;Follow us on Twitter!&lt;/a&gt;&lt;/div&gt;
  {{/if}}
&lt;/template&gt;
</code></pre>

We haven’t yet defined what <code>isThirdDay</code> is supposed to be. We’ll do that through a <strong>template helper</strong>.

Template helpers are simply bits of JavaScript code you can assign to variables and use in your templates. Let’s open <code>banner.js</code> and add the following code to the file:

<pre><code class="language-javascript">
Template.banner.helpers({
  isThirdDay: function () {
    return this.index == 2;
  }
});
</code></pre>

Because our <code>afterDay</code> template is called from a loop, we can access the current day’s index using <code>this.index</code>. And because that index is zero-based, the third day will be the one whose index is <code>2</code>, which in turn gives us the contents of our helper.

Here you go! Now our banner is appearing after only the third day and no other.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3439dd45-1e9f-4350-a0cc-0003ed3ef3a5/09-banner-not-repeated-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ace945b2-dc69-4893-836f-7ba7af24544c/09-banner-not-repeated-opt-small.jpg" alt="Twitter banner, not repeated" /></a><figcaption>Twitter banner, not repeated (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3439dd45-1e9f-4350-a0cc-0003ed3ef3a5/09-banner-not-repeated-opt.jpg">View large version</a>)</figcaption></figure>

## Other Features

We’re running out of time, but this is by no means the extent of Telescope’s features. Out of the box, Telescope also makes the following possible:

*   Add a banner to sign people up to your email list.
*   Generate and send a newsletter of the best posts on your website.
*   Add thumbnail previews to each new posted link.
*   Automatically import posts from an RSS feed.
*   Require new posts to be approved by an admin.
*   And much more!

If you want to go further, a good place to start would be <a href="https://telesc.pe/docs">Telescope’s documentation</a>. You can also find a nice introduction to Meteor itself on the <a href="https://www.meteor.com/install">official website</a>.</p>

## Conclusion

As Product Hunt’s success has shown, there’s a big demand for websites that help us deal with information overload by streamlining and centralizing content. Telescope is a fast, modern platform on which to build your own community, social news app or link-sharing website. And, as you’ve just seen, extending it is very easy. I encourage you to give it a try. And if you end up building the next Product Hunt with Telescope, I hope you’ll remember who first told you about it!

<em>Thanks to Loren Sands-Ramshaw, Phil Pickering, Nigel Anderson, Austin Stoltzfus and others for reviewing a draft of this article.</em>

{{< signature "vf, il, al" >}}

