---
title: What You Need To Know About OAuth2 And Logging In With Facebook
slug: oauth2-logging-in-facebook
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c619cce1-eb0c-4182-804b-b7bfc4713aa3/login2-500w-opt.png
date: 2017-05-02T20:19:55.000Z
author: zack-grossbart
summary: >-
  OAuth2 makes it easy for users to log into your app, to not have to remember a password for every website, and to trust your security. OAuth2 dominates the industry as there is no other security protocol that comes close to the adoption of OAuth2.
description: >-
  OAuth2 makes it easy for users to log into your app, to not have to remember a password for every website, and to trust your security. OAuth2 dominates the industry as there is no other security protocol that comes close to the adoption of OAuth2.
categories:
  - Forms
  - Browsers
  - Apps
  - JSON
---
In case you're wondering what OAuth2 is, it's the protocol that enables anyone to log in with their Facebook account. It powers the “Log in with Facebook” button in apps and on websites everywhere.

This article shows you how “Log in with Facebook” works and explains the protocol behind it all. You’ll learn why you’d want to log in with Facebook, Google, Microsoft or one of the many other companies that support OAuth2.

This article shows you how “Log in with Facebook” works and explains the protocol behind it all. You’ll learn why you’d want to log in with Facebook, Google, Microsoft or one of the many other companies that support OAuth2.

We’ll look at two examples: why Spotify uses Facebook to let you log into the Spotify mobile app, and why Quora uses Google and Facebook to let you log into its website.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Four Ways To Build A Mobile Application](https://www.smashingmagazine.com/2013/11/four-ways-to-build-a-mobile-app-part1-native-ios/)
*   [How To Build Honest UIs And Help Users Make Better Decisions](https://www.smashingmagazine.com/2016/10/how-to-build-honest-uis-and-help-users-make-better-decisions/)
*   [Keeping Your Android App Popular After Launch](https://www.smashingmagazine.com/2015/10/keep-your-android-app-popular-after-launch/)
*   [Spotify Playlists To Fuel Your Coding And Design Sessions](https://www.smashingmagazine.com/2016/11/playlists-fuel-coding-design-sessions/)

{{% feature-panel %}}

## Before OAuth2

OAuth2 won a standards battle a few years ago. It’s the only authentication protocol supported by the major vendors. Google recommends OAuth2 for all of its APIs, and Facebook’s Graph API only supports OAuth2.

The best way to understand OAuth2 is to look at what came before it and why we needed something different. It all started with Basic Auth.</p>

### Basic Auth

Authentication schemes focus on two key questions: Who are you? And can you prove it?

The most common way to ask these two questions is with a username and password. The username says who you are, and the password proves it.

Basic Auth was the first web authentication scheme. It sounds funny but “Basic authentication” was its actual name in the specification first published in 1999.

Basic Auth allows web servers to ask for these credentials in a way that browsers understand. The server returns an HTTP response code of <code>401</code> (which means that authentication is required) and adds a special header to the response, named <code>WWW-Authenticate</code>, with a special value of <code>Basic</code>.

When the browser sees this response code and this header, it shows a popup log-in dialog:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dea41e0-a85a-4f10-8f16-d74611566313/1-basic-auth-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dea41e0-a85a-4f10-8f16-d74611566313/1-basic-auth-preview-opt.png" alt="The Basic Auth log-in dialog" width="453" height="" /></a><figcaption>The Basic Auth log-in dialog</figcaption></figure>

The great part about Basic Auth is its simplicity. You don’t have to write a log-in screen. The browser handles all of that and just sends the username and password to the server. It also gives the browser a chance to specially handle the password, whether by remembering it for the user, getting it from a third-party plugin or taking the user’s credentials from their operating system.

The downside is that you don’t get any control over the look and feel of the log-in screen. That means you can’t style it or add new functionality, such as a “Forgot password?” link or an option to create a new account. If you want more customization, you’d have to write a custom log-in form.</p>

### Custom Log-In Forms

Custom log-in forms give you all the control you could want. You write an HTML form and prompt for the credentials. You then submit the form and handle the log-in any way you want. You get total control: You can style it, ask for more details or add more links.

Some websites, such as WordPress, use a simple form for the log-in screen:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/667634d8-7cfa-4460-b380-1bccb22873c6/7-wordpress-login-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/667634d8-7cfa-4460-b380-1bccb22873c6/7-wordpress-login-preview-opt.png" alt="WordPress log-in screen" width="385" height="" /></a><figcaption>WordPress log-in screen</figcaption></figure>

LinkedIn lets users log in or create an account on the same page, without having to go to another part of the website:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72ed6a80-fcea-421f-b75e-41c7c34b92f9/2-linkedin-login-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfa28ef5-d5e9-4f83-8c1e-a981c1705c77/2-linkedin-login-780w-opt.png" alt="LinkedIn log-in screen" width="780" height="508" /></a><figcaption>LinkedIn log-in screen (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72ed6a80-fcea-421f-b75e-41c7c34b92f9/2-linkedin-login-large-opt.png">View large version</a>)</figcaption></figure>

Form-based log-in is very popular, but it has a major fundamental problem: Users have to tell the website their password.</p>

### Keeping Secrets Secret

In security circles, we call a password a secret. It’s a piece of information that only you have and proves that you’re you. The secret can also be more than just a password; we’ll talk more about that a little later.

A website can take all the security measures in the world, but if the user shares their password, then that security is gone. Hackers breached the Gawker website in 2010, exposing many users’ passwords. While this was a problem for Gawker, the problem didn’t stop there. Most people reuse passwords, so hackers took the leaked data from Gawker and tried to log into more critical websites, such as Gmail, Facebook and eBay. Anyone who used a Gawker password for more important things lost a lot more than the latest gossip about Hulk Hogan’s sex tape.

{{% ad-panel-leaderboard %}}

Making sure your users don’t reuse a password for multiple accounts is the first half of the problem — and it’s impossible. As long as people have to create different accounts all over the Internet, they will reuse their passwords.

The second half of the problem is storing the passwords securely.

When someone logs into your app, you need to verify their password, and that means you need a copy to verify it against. You could store all usernames and passwords in a database somewhere, but now you risk losing those passwords or getting hacked. The best practice is to use a <a href="https://en.wikipedia.org/wiki/Cryptographic_hash_function">hash function</a>, such as one of the <a href="https://en.wikipedia.org/wiki/SHA-2">SHA-2</a> functions. This function encrypts data in a way that you can never get it back, but you can replicate the encryption: “my password” will hash to something like <code>bb14292d91c6d0920a5536bb41f3a50f66351b7b9d94c804dfce8a96ca1051f2</code> every time.

And now we’re off in the tall grass: I’m telling you how to implement cryptographic protocols. Next, I’ll have to explain how to add a <a href="https://en.wikipedia.org/wiki/Salt_(cryptography)">salt</a> to your data and which textbooks to read on man-in-the-middle attacks. All you wanted to do is write an app, and now you have to become a security expert. We need to step back.</p>

## OAuth2

You probably aren’t a security expert. Even if you are, I still wouldn’t trust you with my password. OAuth2 gives you a better way.

As an example, I use Spotify on my iPad. I pay the company $10 a month to listen to music. Spotify gives me access on only three devices, so I need a password to make sure that nobody else uses my account. My Spotify account isn’t a big security concern. Getting hacked wouldn’t be the end of the world, but the company does have my credit card, so I want to make sure that I’m secure.

I hardly ever log into Spotify, so I don’t want to create another account and have to remember another password. Spotify gives me a better option:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b60d700-2c50-4bb2-a7f6-35211e94b3a4/3-login1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fece086-bfba-4b9b-aeef-4271cf7dc362/3-login1-780w-opt.png" alt="Spotify log-in screen with _Log in with Facebook_ option" width="780" height="1040" /></a><figcaption>Spotify log-in screen with “Log in with Facebook” option (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b60d700-2c50-4bb2-a7f6-35211e94b3a4/3-login1-large-opt.png">View large version</a>)</figcaption></figure>

I can use my Facebook account to log in. When I tap that button, Spotify sends me over to facebook.com, and I log in there. This might seem like a small detail, but it’s the most important step of the whole process.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec3ab2f9-ca41-4352-8905-e432725f6b45/4-login2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e617f73-1fde-4b3a-8066-1ab2206efaf4/4-login2-780w-opt.png" alt="Facebook log-in screen for Spotify" width="780" height="1040" /></a><figcaption>Facebook log-in screen for Spotify (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec3ab2f9-ca41-4352-8905-e432725f6b45/4-login2-large-opt.png">View large version</a>)</figcaption></figure>

Spotify’s programmers could have written a log-in form themselves and then sent my username and password to Facebook with a back-end API, but there are two big reasons why I don’t want them to do that:

*   **I don’t trust Spotify with my Facebook password.** I use Facebook to connect with friends and I don’t want to get hacked. I don’t trust that Spotify will handle the password correctly. I also don’t trust that it’ll avoid the temptation to do something funny with it. Maybe it would try to store it so that it can use it later. Maybe it has a bug that writes it to a file somewhere before sending it off to Facebook, so a hacker could grab it. I’m sorry, Spotify; I’m just not the trusting sort.
*   **I don’t want to let Spotify do everything.** I want Spotify to play music. I don’t want it to post to my friends’ walls when I listen to the Spice Girls. I also don’t want to let it download my list of friends and bug them to join Spotify. If I gave Spotify my Facebook password, then it could log in as me on Facebook; it could do anything I could do.

There are also two big reasons why Spotify doesn’t want to do that:

*   **Facebook has multiple options for me to log in.**.  I can either log in with my username and password or I can log in with the Facebook app. I can also retrieve my password from Facebook or get help that Spotify can’t give me. If I just gave Spotify my password, I wouldn’t get any of those options.
*   **My secret might not be a password.**.  A password is enough security for my $10-per-month Spotify account, but it might not be enough for my bank or something even more important. There are a lot of other secrets I could provide: I might have a smart card, or I might be living in a Mission Impossible movie and use a retinal scanner.

I’m not in a Mission Impossible movie, but in the real world, many companies use two-factor authentication, such as a password plus something else. The most common method is to use your phone. When you want to log in, the company sends you a text with a special code that lasts for a few minutes; you then type in the code or use an app to input it.

{{% ad-panel-leaderboard %}}

Now the company is sure that nobody can log into your account without your phone. If someone steals your password, they still can’t log in. As long as you don’t lose your phone, everything is secure.

Facebook isn’t the only OAuth2 provider. When I log into Quora with my Google account, Google tells me what Quora would like to do and asks if that’s OK:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f51e0026-51da-4347-bd7a-8931262eb112/6-quora-auth-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f51e0026-51da-4347-bd7a-8931262eb112/6-quora-auth-preview-opt.png" alt="The step-2 dialog for the Google Quora OAuth2 process" width="438" height="" /></a><figcaption>The step-2 dialog for the Google and Quora OAuth2 process</figcaption></figure>

I might be fine with allowing Quora to view my email address and my basic profile data, but I don’t want it to manage my contacts. OAuth2 shows me all of the access that Quora wants, allowing me to pick and choose what I grant access to.

So, those are the advantages of OAuth2. Let’s see how it works.

## How OAuth2 Works

Facebook, Google and most of the other OAuth2 providers treat native clients differently from web clients. Native clients are considered more secure, and they get tokens and refresh tokens that can last for months. Web clients get much shorter tokens, which typically time out when the user closes the browser or hasn’t clicked on the website for a while.

In both cases, the log-in process is the same. The difference is in how often the user needs to go through it.

OAuth2 log-in follows these general steps:

1.  **The user tries to do something that requires authentication.** This could be as simple as opening an app or clicking a “Log in” button.
2.  **The app or website determines that the user hasn’t logged in yet and starts the log-in process.** It does this by opening a web page and sending it to a special URL at Facebook, Google or whatever other website is providing your OAuth2.

Opening a new browser window for the OAuth2 provider is a crucial step. That’s what allows providers to show their own log-in forms and to ask each user for whatever log-in information they need. Most apps do this with an embedded web view.

Along with the provider’s log-in URL, you need to send some URL parameters that tell the provider who you are and what you want to do:

*   `client_id` This tells the OAuth2 provider what your app is. You’ll need to register your app ahead of time to get a client ID.
*   `redirect_uri` This tells the provider where you want to go when you’re done. For a website, this could be back to the main page; a native app could go to a page that closes the web view.
*   `response_type` This tells the provider what you want back. Normally, this value is either `token`, to indicate that you want an access token, or `code`, to indicate that you want an access code. Providers may also extend this value to provide other types of data.
*   `scope` This tells the provider what your app wants to access. This is how Google knows that Quora is asking for access to manage your contacts. Each provider has a different set of scopes.

There are additional fields that can add more security or help with caching. Certain providers also get to add more fields, but these four are the important ones.

Once your app opens the web view, the provider takes over. They might just ask for a simple username and password, or they might present multiple screens requesting anything from the name of your favorite teacher to your mother’s maiden name. That’s all up to them. The important part is that, when the provider is done, they will redirect back to you and give you a token.</p>

### It’s All About The Tokens

When the process completes, the provider will give you a token and a token type. There are two types of tokens: access tokens and refresh tokens. The type of client you have will determine which types of tokens you’re allowed to ask for.

When I log into my Spotify app, I can stay logged in for months, because the assumption is that my phone is used only by me. Facebook trusts the Spotify app to manage the tokens, and I trust the Spotify app not to lose the tokens.

When the access token times out (typically, in one to two hours), Spotify can use the refresh token to get a new one.

The refresh token lasts for months. That way, I only have to log in on my phone a few times a year. The downside is that if I lose that refresh token, someone else could use my account for months. The refresh token is so important that iOS provides a keychain for tokens, where it makes sure to encrypt and store them safely.

Using OAuth2 in a web application works the same way. Instead of using a web view, you can open up the OAuth2 log-in request in a frame, an iframe or a separate window. You can also open it on the current page, but this would cause you to lose all JavaScript application state whenever someone needs to log in.

When I log into Quora with my web browser, I don’t get a refresh token. They want the token to time out and prompt me to log in again when I quit my browser or even just go away for lunch. Untrusted clients can’t refresh the token because they can’t be trusted to hold on to the important refresh token. It’s more secure but less convenient, because they will prompt you to log in again much more frequently.</p>

## Using OAuth2 In Your App

Now you know how OAuth2 works, but you probably don’t want to implement your own OAuth2 client. You could go read the whole 75-page <a href="https://tools.ietf.org/html/rfc6749">OAuth 2.0 specification</a> if you’re having trouble sleeping, but you don’t need to. Some great libraries are out there for you to use.

iOS has built-in support for OAuth2. Corrina Krych has a very helpful tutorial on <a href="https://www.raywenderlich.com/99431/oauth-2-with-swift-tutorial">using OAuth 2.0 with Swift</a>. It walks you through how to get a token, how to integrate the views in your app and where to store your tokens.

Android also has built-in support for OAuth2. I must admit that I’m not as familiar with it because I focus on iOS, but there are some good <a href="https://developer.android.com/training/id-auth/authenticate.html">sections in the documentation</a> to show you examples and some open-source libraries to make it even easier.

JavaScript doesn’t have built-in support for OAuth2, but there are clients for all of the major JavaScript libraries. React fully supports OAuth2. AngularJS has third-party support for OAuth2.0 for many projects. I even wrote <a href="https://github.com/gromit-soft">one of them</a>.

Once you have an OAuth2 client, you’ll need to choose a provider.</p>

## Who Do You Trust?

The big assumption here is that I trust Facebook more than Spotify. I have no good reason for that. Facebook doesn’t make its internal security public, and there’s no good way for me to audit it. Neither does Spotify. There’s no Consumer Reports for OAuth2 security. I’m basically trusting Facebook because it’s bigger. I trust Facebook because other people do.

I’m also trusting Facebook more every time I click the “Log in with Facebook” button. If Facebook loses my password, then hackers will get access not just to my Facebook account, but also to my Spotify account and to any other service I’ve logged into with my Facebook account. The upside is that there is only one place I have to reset my password in order to fix the problem.

I don’t have to trust Facebook, but I have to trust someone. Somebody has to authenticate me. I need to choose the provider I trust.</p>

### Choosing an OAuth2 Provider

Wikipedia maintains a <a href="https://en.wikipedia.org/wiki/List_of_OAuth_providers">list of OAuth providers</a>, but you wouldn’t care about most of them. The big ones are Facebook and Google. You might also want to look at Amazon or Microsoft.

All four of them are big and easy to integrate with. Facebook provides <a href="https://developers.facebook.com/docs/apps/register">instructions for registering an app</a>. Google has <a href="https://developers.google.com/identity/protocols/OAuth2">similar steps</a>. The basic idea is that you create a developer account and then create an app ID. The provider then gives you a client ID that you can use to make requests.

You can also choose multiple providers. Quora allows you to log in with Facebook or Google; because they both use OAuth2, you may use the same code for both.</p>

## What’s Missing From OAuth2

OAuth2 does a very good job of solving a complex problem, but it is missing a couple of things:

*   **The standard isn’t completely standard.** I’ve never been able to write a single OAuth2 client that can log into both Facebook and Google without a few `if` statements. Each interprets the specification differently, and there are little dissimilar details for each one. They also always have different ideas on what scopes to provide. Using a library to integrate with OAuth2 helps a lot with this problem, but it will never be 100% transparent in your app’s code.
*   **Logging out is tricky.**.  Every app or website that uses OAuth2 has a log-out button, but most will just forget the tokens without invalidating them. The app will forget about all of your current tokens and allow someone else to log in, but your tokens are still valid. If a hacker stole your token, they could still use it and log in as you.

There is a separate specification for <a href="https://tools.ietf.org/html/rfc7009">invalidating OAuth2 tokens</a>, but it wasn’t picked up by many of the major providers. OAuth2 doesn’t provide a way to recover if a hacker gets your refresh token; even though you can delete your local copy of the token, the hacker will still have it. Many providers give you a way to suspend your account, but there’s no standard way to do it.

In defence of OAuth2, this is a difficult problem, because many providers use <a href="https://www.smashingmagazine.com/2012/05/backpack-algorithms-and-public-key-cryptography-made-easy/">public-key cryptography</a> to create stateless tokens. This means that the server doesn’t remember the tokens it has created, so it can’t forget them later.

The other major problem with OAuth2 is that you are dependent on your provider. When Facebook goes down, so does the “Log in with Facebook” button in your app. If Google decides to start charging you to support OAuth2 or demands that you share your profit with it, there’s nothing you can do. This is the double-edged sword of trusting a provider: They are doing a lot for you, but they have control over your users.</p>

## OAuth2 Runs The World

Even with a couple of missing features and a big dependency, OAuth2 is still an excellent choice. It makes it easy for users to log into your app, to not have to remember a password for every website, and to trust your security. OAuth2 is a very popular choice. It dominates the industry. No other security protocol comes close to the adoption of OAuth2.

Now you know where OAuth2 comes from and how it works. Go make smart choices about who to trust, stop reading articles about safely storing encrypted passwords, and spend more of your time writing your amazing app.

{{< signature "da, il, al" >}}

