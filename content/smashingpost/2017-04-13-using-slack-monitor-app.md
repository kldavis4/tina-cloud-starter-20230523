---
title: Using Slack To Monitor Your App
slug: using-slack-monitor-app
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fbeac0b-706d-4e70-82d5-2ba1bacc4635/payment-preview-opt.png
date: 2019-02-15T18:23:34.000Z
author: coryshaw
description: >-
  For the past few months, I’ve been building a software-as-a-service (SaaS)
  application, and throughout the development process I’ve realized what a
  powerful tool Slack (or team chat in general) can be to monitor user and
  application behavior.

  After a bit of integration, it’s provided a real-time view into our
  application that previously didn’t exist, and it’s been so invaluable that I
  couldn’t help but write up this show-and-tell.
categories:
  - Coding
  - JavaScript
  - Techniques
  - Apps
  - Node.js
---
It all started with a visit to a small startup in Denver, Colorado. During my visit, I started hearing a subtle and enchanting “ding” in the corner of the office every few minutes. When I went to investigate this strange noise, I found a service bell hooked up to a Raspberry Pi, with a tiny metal hammer connected to the circuit board. As it turned out, the Pi was receiving messages from the team’s server, and it swung that little hammer at the bell **every time a new customer signed up**.

I always thought that was a great team motivator, and it got me thinking of how I could use team chat to achieve a similar experience and how we could [analyze and visualize log data](https://www.loggly.com/product/log-analysis/).

Because we were already using Slack for team chat, and because it has a beautifully documented [API](https://api.slack.com/custom-integrations), it was an obvious choice for the experiment.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Conversational Interfaces: Where Are We Today? Where Are We Heading?](https://www.smashingmagazine.com/2016/07/conversational-interfaces-where-are-we-today-where-are-we-heading/)
*   [Team Collaboration And Closing Efficiency Gaps In Responsive Design](https://www.smashingmagazine.com/2014/05/team-collaboration-closing-efficiency-gaps-responsive-design/)
*   [What You Should Know About The App Design Process](https://www.smashingmagazine.com/2016/11/what-everyone-should-know-about-the-process-behind-app-design/)
*   [Off To The Races: Getting Started With Design Sprints](https://www.smashingmagazine.com/2014/08/getting-started-with-design-sprints/)

{{% feature-panel %}}

## Set Up Slack

First, we had to obtain a “webhook URL” from Slack in order to programmatically post messages to our Slack channel.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bd3a9c2-1b37-4a5f-9e76-bdee9624855e/slack-setup-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/116219c9-2c11-422e-9ee5-02c342a8cd9d/slack-setup-preview-opt.png" width="780" height="1390" alt="Set up Slack" /></a><figcaption>Follow the steps above to obtain a webhook URL from Slack (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bd3a9c2-1b37-4a5f-9e76-bdee9624855e/slack-setup-large-opt.png">View large version</a>)</figcaption></figure>

Now that we had a webhook URL, it was time to integrate Slack messages into our Node.js application. To do this, I found a handy Node.js module named [node-slack](https://github.com/xoxco/node-slack).

First, we installed the Node.js module:

<pre><code class="language-javascript">npm install node-slack --save
</code></pre>

Now, we could send Slack messages to our channel of choice with a few lines of code.</p>

<pre><code class="language-javascript">// dependency setup
var Slack = require('node-slack');
var hook_url = 'hook_url_goes_here';
var slack = new Slack(hook_url);
// send a test Slack message
slack.send({
 text: ':rocket: Nice job, I\'m all set up!',
 channel: '#test',
 username: 'MyApp Bot'
});
</code></pre>

(You can find similar Slack integration packages for [Ruby](https://github.com/stevenosloan/slack-notifier), [Python](https://github.com/slackapi/python-slackclient) and just about any other language.)

When executed, this code produced the following message in our #test Slack channel:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce5858e8-8614-4d5a-a493-8949dd767e8c/all-setup-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce5858e8-8614-4d5a-a493-8949dd767e8c/all-setup-preview-opt.png" width="512" height="" alt="Slack Setup" /></a></figure>

The code above is minimal, but it’s specific to the Slack API and the node-slack module. I didn’t want to be locked into any particular messaging service, so I created a generic Node.js module function to execute the service-specific code:

<pre><code class="language-javascript">// Messenger.js
// dependency setup
var hook_url = my_hook_url;
var Slack = require('node-slack');
var slack = new Slack(hook_url);
module.exports = {
 sendMessage: function(message, channel, username) {
 if (!message){
 console.log('Error: No message sent. You must define a message.')
 } else {
 // set defaults if username or channel is not passed in
 var channel = (typeof channel !== 'undefined') ? channel : "#general";
 var username = (typeof username !== 'undefined') ? username : "MyApp";
 // send the Slack message
 slack.send({
 text: message,
 channel: channel,
 username: username
 });
 return;
 }
 }
};
</code></pre>

Now we can use this module anywhere in the application with two lines of code, and if we ever decide to send messages to another service in the future, we can easily swap that out in Messenger.js.</p>

<pre><code class="language-javascript">var messenger = require('./utilities/messenger');
messenger.sendMessage(':rocket: Nice job, I\'m all set up!', '#test');
</code></pre>

Now that we had the basics set up, we were ready to start firing off messages from within the application.</p>

### Track Registrations

The first order of business was to achieve service-bell parity. I located the success callback of the user registration function, and I added this code:

<pre><code class="language-javascript">messenger.sendMessage('New user registration! ' + user.email);
</code></pre>

Now, when someone registered, we’d get this message:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d27c3c-5ad9-4e16-af52-d20f81faec84/new-user-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d27c3c-5ad9-4e16-af52-d20f81faec84/new-user-preview-opt.png" width="715" height="" alt="New User Message" /></a></figure>

It even dings! This was a good start, and it gave me that satisfying service-bell feeling, but it made me thirsty for more.</p>

## Dive Deeper

As my curiosity grew with each ding, I began to wonder things like, What if there was a failure to create a new user? What if a user registered, logged in but didn’t complete the onboarding process? What is the result of our scheduled tasks? Now that the groundwork was in place, answering these questions was a piece of cake.</p>

### Monitor Exceptions and Critical Errors on Back End

One of the most important errors we wanted to know about was if there was a failure to create a new user. All we had to do was find the error callback in the user registration function, and add this code:

<pre><code class="language-javascript">messenger.sendMessage(':x: Error While adding a new user ' + formData.email + ' to the DB. Registration aborted!' + error.code + ' ' + error.message);
</code></pre>

Now we knew instantly when registrations failed, why they failed and, more importantly, who they failed for:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a9acee-0773-4a39-be72-3cf671951abe/registration-error-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff975e5b-a926-42a5-9ea1-f99f39f06680/registration-error-preview-opt.png" width="780" height="185" alt="User Registration Error" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a9acee-0773-4a39-be72-3cf671951abe/registration-error-large-opt.png">View large version</a>)</figcaption></figure>

There were all kinds of interesting places where we could send messages (pretty much anywhere with an error callback). One of those places was this generic catch-all error function:

<pre><code class="language-javascript">app.use(function(err, req, res, next) {
 var message = ':x: Generic Server Error! '+ err + '\n Request: \n' + req.protocol + '://' + req.get('host') + req.originalUrl + '\n' + JSON.stringify(req.headers) + 'Request Payload:\n' + JSON.stringify(req.body);
 messenger.sendMessage(message, '#server-errors');
 res.status(err.status || 500);
 res.json({'error': true });
});
</code></pre>

This code helped us to uncover what a request looks like for unhanded exceptions. By looking at the request that triggered these errors, we could track down the root causes and fix them until there were no more generic errors.

With all of these error notifications in place, we now had comfort in knowing that if something major failed in the app, we would know about it instantly.</p>

### Monitor Financials

Next, I wanted to send a notification when a financial event happens in the application. Because our SaaS product integrates with Stripe, we created a webhook endpoint that gets pinged from Stripe when people upgrade their plan, downgrade their plan, add payment info, change payment info and many other events related to subscription payments, all of which are sent to Slack:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fbeac0b-706d-4e70-82d5-2ba1bacc4635/payment-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fbeac0b-706d-4e70-82d5-2ba1bacc4635/payment-preview-opt.png" width="712" height="" alt="Payment Message" /></a></figure>

### Monitor User Behavior on Front End

There were a few cases on the front end where we wanted to understand user behavior in ways that the back end couldn’t provide, so we created an endpoint to send Slack messages directly from the front end. Because our Slack webhook URL is protected behind a `POST` endpoint, it was a minimal risk to expose sending Slack messages to our team via an endpoint.

With the endpoint in place, we could now fire off Slack messages with a simple AngularJS `$http.post` call:

<pre><code class="language-javascript">// send Slack notification from the front end
var message = ":warning: Slack disconnected by " + $scope.user.username;
$http.post('/endpoint', message);
</code></pre>

This helps us to answer important questions about the business: Are people registering and adding a domain name? Are they not? If someone is, is it for a really high-profile domain whose owner we would want to reach out to personally soon after they’ve added it. We can now tap into this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f6720bc-b5be-457a-a80e-57ce5759aaad/user-messages-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d13004-a148-4526-b19a-8f064ed5c28c/user-messages-preview-opt.png" width="780" height="159" alt="User Messages" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f6720bc-b5be-457a-a80e-57ce5759aaad/user-messages-large-opt.png">View large version</a>)</figcaption></figure>

At one point, we saw a pattern of people adding a domain, removing it, then readding it within a few minutes, which clued us into an obscure bug that we probably would never have discovered otherwise.

There are also signals that a user is unhappy with the service, and these are valuable to know about. Did someone remove a domain name? Did they disconnect Slack?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b799c9ca-3a2a-4ea3-978c-47de964081ff/user-disconnected-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00833e79-481d-4aa4-a6ab-28b20b892fd4/user-disconnected-preview-opt.png" width="780" height="206" alt="User Disconnected Messages" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b799c9ca-3a2a-4ea3-978c-47de964081ff/user-disconnected-large-opt.png">View large version</a>)</figcaption></figure>

This feedback gives us an opportunity to proactively reach out and offer delightful customer support when it matters most.</p>

### Monitor Scheduled Tasks

One of the most interesting things to see in Slack is the result of scheduled tasks. Our SaaS product runs tasks to notify people about their website’s performance (our core service), to send transactional emails, to clean up the database and a few other things. The firing and results of these tasks sends a message to Slack:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93340e3-e82a-42fb-93c9-d43830363530/task-messages-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7393a67-e666-4622-9901-afa2ee6a559d/task-messages-preview-opt.png" width="780" height="313" alt="Server Task Messages" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93340e3-e82a-42fb-93c9-d43830363530/task-messages-large-opt.png">View large version</a>)</figcaption></figure>

Now we know when a task function fires, what the result of that function is (in this case, it sends out several emails) and whether it fails for any reason.</p>

## Apply This Concept To Your Application

The case study above is a practical example of what we did to monitor the [GoFaster.io](https://gofaster.io) application and service. It has worked fantastic for us, but how would this concept scale to large applications that send hundreds, maybe even thousands, of messages per day? As you can imagine, this would quickly turn into a “Slackbot who cried wolf” situation, and the value would get lost in the noise.</p>

### Don’t Treat All Notifications Equally

Some notifications are more important than others, and importance will vary depending on the employee and their role. For example, software development and IT operations (DevOps) folk might only care about the server messages, whereas customer service folk would care most about what’s going on with users.

Luckily, Slack has a great solution to this problem: **channels**.

Channels can be created by anyone, made public or private to your organization, and shared with anyone. Once you’ve subscribed to a channel, you can control how that channel’s activities alert you. Does a new message in the channel ding every time? Does it alert your phone, too? Does it only bold the channel? All of this can be controlled for each channel by each team member to suit their needs.

Putting this idea into practice, here’s how a larger organization might organize monitor-based notifications in Slack via channels:

### #Critical-Server-Errors

*   **What:** registration errors, login errors, database read and write errors
*   **Who:** system administrators, DevOps, CTO, CEO, developers
*   **Alert settings:** Always notify on phone or desktop.</p>

### #Non-Critical-Server-Errors

*   **What:** 404 errors, catch-all server errors, etc.
*   **Who:** DevOps, developers
*   **Alert settings:** Make bold but don’t ding.</p>

### #Financials

*   **What:** payment transactions, failed transactions, upgrades, downgrades, expired cards
*   **Who:** CFO, CEO
*   **Alert settings:** Make it rain.</p>

### #User-Behavior

*   **What:** registering, onboarding process, updating plan type, adding information, removing information, deleting account
*   **Who:** customer support, social media managers, developers, CEO
*   **Alert settings:** Always notify on phone or desktop.</p>

### #Application-Stats

*   **What:** scheduled task results, housekeeping, transactional email statistics, user count and growth metrics
*   **Who:** email marketers, system administrators, anyone interested
*   **Alert settings:** Make bold but don’t ding.</p>

## Conclusion

Having built on this idea for a few months and digested the results, we’ve found it to be an invaluable extension of our application. Without it, we would feel out of touch with what is going on with the service and would have to manually hunt down the same information via the dashboard, or database queries would be a chore.

Every application and user base is different, which means that this concept cannot be built into a service and offered to the masses. In order to be valuable, it requires a small up-front investment of time and resources to deeply integrate in your application. Once it’s up and running, the investment will pay off in the form of your team’s connectedness to your application and its users.

In conclusion, here’s a recap of the benefits of using team chat to monitor your application:

### Gain a Fresh Perspective on User and Server Behavior

Having a real-time live feed of the metrics that matter most to you and your business will keep you closely connected to what users are doing and how the server is responding.</p>

### React Quickly When Things Fail

You will be able to react faster than ever before. You will know about failures at the same time your users do. You can immediately react to that failing endpoint, lost database connection or DDoS attack.</p>

### Offer Exceptional Customer Service

Reach out to that customer who has just disabled their account to offer them a discount, give personal thanks to customers who have upgraded, or just follow up with people to understand their intentions. When you know what users are doing and when they are doing it, you can easily find out why.</p>

### Team Connectedness to the Application Will Make You More Efficient

When your team is on the same page with the application, collaboration can center on solving problems as they arise, rather than on trying to figure out what happened, where it happened or who it happened to.</p>

### Notifications and Channels Can Scale With Your Application

As your application and team grow, so will your monitoring needs. Slack does a great job of giving you all of the permission and notification controls necessary to ensure that the right information gets to the right people.</p>

### Search Is Powerful

By logging a user name in your Slack messages, you can track every error, success message or event that a user has generated while interacting with your application simply by searching for their user name in Slack. Just know that, with a free Slack account, this is limited to the last 10,000 messages.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c5fc4a3-fd07-4dbf-80d6-8bc4683a2cf9/slack-search-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c5fc4a3-fd07-4dbf-80d6-8bc4683a2cf9/slack-search-preview-opt.png" width="780" height="1646" alt="Search Slack by User Name" /></a></figure>

I hope you’ve found this concept to be useful, and I’d love to hear other stories of teams that have implemented similar forms of monitoring, or just other interesting ways to use and build on it.

{{< signature "rb, vf, yk, al, il" >}}

