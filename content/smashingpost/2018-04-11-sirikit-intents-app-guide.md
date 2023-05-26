---
title: 'Will SiriKit’s Intents Fit Your App? If So, Here’s How To Use Them'
slug: sirikit-intents-app-guide
author: lou-franco
date: 2018-04-11T17:00:44+02:00
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d83a8e9-0784-49b4-9644-22eeb548ce07/sirikit-intents09-add-intents-extension-to-project.png
summary: >-
  Since last year, it has been possible to add Siri support to an app if it fits into one of Apple's pre-defined use cases. Find out if SiriKit will work for you and how to use it.
description: >-
  Since last year, it has been possible to add Siri support to an app if it fits into one of Apple's pre-defined use cases. Find out if SiriKit will work for you and how to use it.
categories:
  - Apps
  - iOS
  - Techniques
  - Voice
---
Since iOS 5, Siri has helped iPhone users send messages, set reminders and look up restaurants with Apple’s apps. Starting in iOS 10, we have been able to use Siri in some of our own apps as well.

In order to use this functionality, your app must fit within Apple’s predefined Siri “domains and intents.” In this article, we’ll learn about what those are and see whether our apps can use them. We’ll take a simple app that is a to-do list manager and learn how to add Siri support. We’ll also go through the Apple developer website’s guidelines on configuration and Swift code for a new type of extension that was introduced with SiriKit: the *Intents* extension.

When you get to the coding part of this article, you will need Xcode (at least version 9.x), and it would be good if you are familiar with iOS development in Swift because we’re going to add Siri to a small working app. We’ll go through the steps of setting up a extension on Apple’s developer website and of adding the Siri extension code to the app.

## “Hey Siri, Why Do I Need You?”

Sometimes I use my phone while on my couch, with both hands free, and I can give the screen my full attention. Maybe I’ll text my sister to plan our mom’s birthday or reply to a question in Trello. I can see the app. I can tap the screen. I can type.

But I might be walking around my town, listening to a podcast, when a text comes in on my watch. My phone is in my pocket, and I can’t easily answer while walking.

{{% feature-panel %}}

With Siri, I can hold down my headphone’s control button and say, “Text my sister that I’ll be there by two o’clock.” Siri is great when you are on the go and can’t give full attention to your phone or when the interaction is minor, but it requires several taps and a bunch of typing.

This is fine if I want to use Apple apps for these interactions. But some categories of apps, like messaging, have very popular alternatives. Other activities, such as booking a ride or reserving a table in a restaurant, are not even possible with Apple’s built-in apps but are perfect for Siri.

## Apple’s Approach To Voice Assistants

To enable Siri in third-party apps, Apple had to decide on a mechanism to take the sound from the user’s voice and somehow get it to the app in a way that it could fulfill the request. To make this possible, Apple requires the user to mention the app’s name in the request, but they had several options of what to do with the rest of the request.

- **It could have sent a sound file to the app.**  
The benefit of this approach is that the app could try to handle literally any request the user might have for it. Amazon or Google might have liked this approach because they already have sophisticated voice-recognition services. But most apps would not be able to handle this very easily.
- **It could have turned the speech into text and sent that.**  
Because many apps don’t have sophisticated natural-language implementations, the user would usually have to stick to very particular phrases, and non-English support would be up to the app developer to implement.
- **It could have asked you to provide a list of phrases that you understand.**  
This mechanism is closer to what Amazon does with Alexa (in its “skills” framework), and it enables far more uses of Alexa than SiriKit can currently handle. In an Alexa skill, you provide phrases with placeholder variables that Alexa will fill in for you. For example, “Alexa, remind me at `$TIME$` to `$REMINDER$`” &mdash; Alexa will run this phrase against what the user has said and tell you the values for `TIME` and `REMINDER`. As with the previous mechanism, the developer needs to do all of the translation, and there isn’t a lot of flexibility if the user says something slightly different.
- **It could define a list of requests with parameters and send the app a structured request.**  
This is actually what Apple does, and the benefit is that it can support a variety of languages, and it does all of the work to try to understand all of the ways a user might phrase a request. The big downside is that you can only implement handlers for requests that Apple defines. This is great if you have, for example, a messaging app, but if you have a music-streaming service or a podcast player, you have no way to use SiriKit right now.

Similarly, there are three ways for apps to talk back to the user: with sound, with text that gets converted, or by expressing the kind of thing you want to say and letting the system figure out the exact way to express it. The last solution (which is what Apple does) puts the burden of translation on Apple, but it gives you limited ways to use your own words to describe things.

The kinds of requests you can handle are defined in SiriKit’s domains and intents. An intent is a type of request that a user might make, like texting a contact or finding a photo. Each intent has a list of parameters &mdash; for example, texting requires a contact and a message.

A domain is just a group of related intents. Reading a text and sending a text are both in the messaging domain. Booking a ride and getting a location are in the ride-booking domain. There are domains for making VoIP calls, starting workouts, searching for photos and a few more things. SiriKit’s documentation contains a [full list of domains and their intents](https://developer.apple.com/documentation/sirikit).

A common criticism of Siri is that it seems unable to handle requests as well as Google and Alexa, and that the third-party voice ecosystem enabled by Apple’s competitors is richer.

I agree with those criticisms. If your app doesn’t fit within the current intents, then you can’t use SiriKit, and there’s nothing you can do. Even if your app does fit, you can’t control all of the words Siri says or understands; so, if you have a particular way of talking about things in your app, you can’t always teach that to Siri.

The hope of iOS developers is both that Apple will greatly expand its list of intents and that its natural language processing becomes much better. If it does that, then we will have a voice assistant that works without developers having to do translation or understand all of the ways of saying the same thing. And implementing support for structured requests is actually fairly simple to do &mdash; a lot easier than building a natural language parser.

Another big benefit of the intents framework is that it is not limited to Siri and voice requests. Even now, the Maps app can generate an intents-based request of your app (for example, a restaurant reservation). It does this programmatically (not from voice or natural language). If Apple allowed apps to discover each other’s exposed intents, we’d have a much better way for apps to work together, (as opposed to [x-callback style URLs](https://x-callback-url.com/)).

Finally, because an intent is a structured request with parameters, there is a simple way for an app to express that parameters are missing or that it needs help distinguishing between some options. Siri can then ask follow-up questions to resolve the parameters without the app needing to conduct the conversation.

## The Ride-Booking Domain

To understand domains and intents, let’s look at the [ride-booking domain](https://developer.apple.com/documentation/sirikit/ride_booking). This is the domain that you would use to ask Siri to get you a Lyft car.

Apple defines how to ask for a ride and how to get information about it, but there is actually no built-in Apple app that can actually handle this request. This is one of the few domains where a SiriKit-enabled app is required.

You can invoke one of the intents via voice or directly from Maps. Some of the intents for this domain are:

- **Request a ride**  
Use this one to book a ride. You’ll need to provide a pick-up and drop-off location, and the app might also need to know your party’s size and what kind of ride you want. A sample phrase might be, “Book me a ride with &lt;appname&gt;.”
- **Get the ride’s status**  
Use this intent to find out whether your request was received and to get information about the vehicle and driver, including their location. The Maps app uses this intent to show an updated image of the car as it is approaching you.
- **Cancel a ride**  
Use this to cancel a ride that you have booked.

For any of this intents, Siri might need to know more information. As you’ll see when we implement an intent handler, your Intents extension can tell Siri that a required parameter is missing, and Siri will prompt the user for it.

The fact that intents can be invoked programmatically by Maps shows how intents might enable inter-app communication in the future.

**Note**: *You can get a [full list of domains and their intents](https://developer.apple.com/documentation/sirikit) on Apple’s developer website. There is also a [sample Apple app with many domains and intents implemented](https://developer.apple.com/library/content/samplecode/IntentHandling/Introduction/Intro.html), including ride-booking.*

## Adding Lists And Notes Domain Support To Your App

OK, now that we understand the basics of SiriKit, let’s look at how you would go about adding support for Siri in an app that involves a lot of configuration and a class for each intent you want to handle.

The rest of this article consists of the detailed steps to add Siri support to an app. There are five high-level things you need to do:

1. Prepare to add a new extension to the app by creating provisioning profiles with new entitlements for it on Apple’s developer website.
2. Configure your app (via its `plist`) to use the entitlements.
3. Use Xcode’s template to get started with some sample code.
4. Add the code to support your Siri intent.
5. Configure Siri’s vocabulary via `plist`s.

Don’t worry: We’ll go through each of these, explaining extensions and entitlements along the way.

To focus on just the Siri parts, I’ve prepared a simple to-do list manager, List-o-Mat.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91fd25ff-fee1-4b6d-83aa-444555336b64/sirikit-intentslist-o-mat.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91fd25ff-fee1-4b6d-83aa-444555336b64/sirikit-intentslist-o-mat.gif" width="552" height="850" alt="An animated GIF showing a demo of List-o-Mat" /></a><figcaption>Making lists in List-o-Mat (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91fd25ff-fee1-4b6d-83aa-444555336b64/sirikit-intentslist-o-mat.gif">Large preview</a>)</figcaption></figure>

*You can find the [full source of the sample, List-o-Mat, on GitHub](https://github.com/app-o-mat/ListOMat).*

To create it, all I did was start with the Xcode Master-Detail app template and make both screens into a `UITableView`. I added a way to add and delete lists and items, and a way to check off items as done. All of the navigation is generated by the template.

To store the data, I used the `Codable` protocol, ([introduced at WWDC 2017](https://www.smashingmagazine.com/2017/07/wwdc-2017-highlights/#swift)), which turns structs into JSON and saves it in a text file in the `documents` folder.

I’ve deliberately kept the code very simple. If you have any experience with Swift and making view controllers, then you should have no problem with it.

Now we can go through the steps of adding SiriKit support. The high-level steps would be the same for any app and whichever domain and intents you plan to implement. We’ll mostly be dealing with Apple’s developer website, editing `plist`s and writing a bit of Swift.

For List-o-Mat, we’ll focus on the [lists and notes domain](https://developer.apple.com/documentation/sirikit/lists_and_notes), which is broadly applicable to things like note-taking apps and to-do lists.

In the lists and notes domain, we have the following intents that would make sense for our app.

- Get a list of tasks.
- Add a new task to a list.

Because the interactions with Siri actually happen outside of your app (maybe even when you app is not running), iOS uses an extension to implement this.

## The Intents Extension

If you have not worked with extensions, you’ll need to know three main things:

1. An extension is a separate process. It is delivered inside of your app’s bundle, but it runs completely on its own, with its own sandbox.
2. Your app and extension can communicate with each other by being in the same app group. The easiest way is via the group’s shared sandbox folders (so, they can read and write to the same files if you put them there).
3. Extensions require their own app IDs, profiles and entitlements.

To add an extension to your app, start by logging into your [developer account](https://developer.apple.com) and going to the “Certificates, Identifiers, & Profiles” section.

### Updating Your Apple Developer App Account Data

In our Apple developer account, the first thing we need to do is create an app group. Go to the “App Groups” section under “Identifiers” and add one.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7eac68f-a44d-4c65-87c9-d6ee29ae148f/sirikit-intents01-create-app-group.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7eac68f-a44d-4c65-87c9-d6ee29ae148f/sirikit-intents01-create-app-group.png" width="1406" height="1126" alt="A screenshot of the Apple developer website dialog for registering an app group" /></a><figcaption>Registering an app group (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7eac68f-a44d-4c65-87c9-d6ee29ae148f/sirikit-intents01-create-app-group.png">Large preview</a>)</figcaption></figure>

It must start with `group`, followed by your usual reverse domain-based identifier. Because it has a prefix, you can use your app’s identifier for the rest.

Then, we need to update our app’s ID to use this group and to enable Siri:

<ol>
	<li>Go to the “App IDs” section and click on your app’s ID;</li>
	<li>Click the “Edit” button;</li>
	<li>Enable app groups (if not enabled for another extension).<br />
		<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2a5ac93-5854-4f6a-8d48-e85de316174c/sirikit-intents02-profile-add-app-groups-siri.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2a5ac93-5854-4f6a-8d48-e85de316174c/sirikit-intents02-profile-add-app-groups-siri.png" width="709" height="252" alt="A screenshot of Apple developer website enabling app groups for an app ID" /></a><figcaption>Enable app groups (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2a5ac93-5854-4f6a-8d48-e85de316174c/sirikit-intents02-profile-add-app-groups-siri.png">Large preview</a>)</figcaption></figure>
	</li>
	<li>Then configure the app group by clicking the “Edit” button. Choose the app group from before.<br />
		<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa7f7d6-f64a-44ce-a3fa-4216052f39d8/sirikit-intents03-configure-app-groups.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa7f7d6-f64a-44ce-a3fa-4216052f39d8/sirikit-intents03-configure-app-groups.png" width="1342" height="280" alt="A screenshot of the Apple developer website dialog to set the app group name" /></a><figcaption>Set the name of the app group (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa7f7d6-f64a-44ce-a3fa-4216052f39d8/sirikit-intents03-configure-app-groups.png">Large preview</a>)</figcaption></figure>
	</li>
	<li>Enable SiriKit.<br />
		<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176bd09f-a32a-47ac-b180-6d3fe3af251e/sirikit-intents04-enable-sirikit.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176bd09f-a32a-47ac-b180-6d3fe3af251e/sirikit-intents04-enable-sirikit.png" width="445" height="72" alt="A screenshot of SiriKit being enabled" /></a><figcaption>Enable SiriKit (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176bd09f-a32a-47ac-b180-6d3fe3af251e/sirikit-intents04-enable-sirikit.png">Large preview</a>)</figcaption></figure>
	</li>
	<li>Click “Done” to save it.</li>
</ol>

Now, we need to create a new app ID for our extension:

<ol>
	<li>In the same “App IDs” section, add a new app ID. This will be your app’s identifier, with a suffix. Do <em>not</em> use just <code>Intents</code> as a suffix because this name will become your module’s name in Swift and would then conflict with the real <code>Intents</code>.<br />
		<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c62157c-c75a-45ce-90ba-65cfdbf76d95/sirikit-intents05-intents-app-id.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c62157c-c75a-45ce-90ba-65cfdbf76d95/sirikit-intents05-intents-app-id.png" width="1332" height="552" alt="A screenshot of the Apple developer screen to create an app ID" /></a><figcaption>Create an app ID for the Intents extension (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c62157c-c75a-45ce-90ba-65cfdbf76d95/sirikit-intents05-intents-app-id.png">Large preview</a>)</figcaption></figure>
	</li>
	<li>Enable this app ID for app groups as well (and set up the group as we did before).</li>
</ol>

Now, create a development provisioning profile for the Intents extension, and regenerate your app’s provisioning profile. Download and install them as you would normally do.

Now that our profiles are installed, we need to go to Xcode and update the app’s entitlements.

### Updating Your App’s Entitlements In Xcode

Back in Xcode, choose your project’s name in the project navigator. Then, choose your app’s main target, and go to the “Capabilities” tab. In there, you will see a switch to turn on Siri support.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74351e5b-9eeb-4680-8961-a30961b1b983/sirikit-intents06-entitlement-add-siri.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74351e5b-9eeb-4680-8961-a30961b1b983/sirikit-intents06-entitlement-add-siri.png" width="1082" height="367" alt="A screenshot of Xcode’s entitlements screen showing SiriKit is enabled" /></a><figcaption>Enable SiriKit in your app's entitlements. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74351e5b-9eeb-4680-8961-a30961b1b983/sirikit-intents06-entitlement-add-siri.png">Large preview</a>)</figcaption></figure>

Further down the list, you can turn on app groups and configure it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7048116b-9078-4094-aade-755582023b23/sirikit-intents07-entitlements-app-group.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7048116b-9078-4094-aade-755582023b23/sirikit-intents07-entitlements-app-group.png" alt="A screenshot of Xcode's entitlements screen showing the app group is enabled and configured" width="464" height="214" /></a><figcaption>Configure the app's app group (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7048116b-9078-4094-aade-755582023b23/sirikit-intents07-entitlements-app-group.png">Large preview</a>)</figcaption></figure>

If you have set it up correctly, you’ll see this in your app’s `.entitlements` file:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d0edc3-6aa6-4202-80a4-5a4c1d44c6d0/sirikit-intents08-entitlements-app-groups.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d0edc3-6aa6-4202-80a4-5a4c1d44c6d0/sirikit-intents08-entitlements-app-groups.png" width="1084" height="222" alt="A screenshot of the App's plist showing that the entitlements are set" /></a><figcaption>The plist shows the entitlements that you set (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d0edc3-6aa6-4202-80a4-5a4c1d44c6d0/sirikit-intents08-entitlements-app-groups.png">Large preview</a>)</figcaption></figure>

Now, we are finally ready to add the Intents extension target to our project.

### Adding The Intents Extension

We’re finally ready to add the extension. In Xcode, choose “File” &rarr; “New Target.” This sheet will pop up:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d83a8e9-0784-49b4-9644-22eeb548ce07/sirikit-intents09-add-intents-extension-to-project.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d83a8e9-0784-49b4-9644-22eeb548ce07/sirikit-intents09-add-intents-extension-to-project.png" width="1462" height="1052" alt="A screenshot showing the Intents extension in the New Target dialog in Xcode" /></a><figcaption>Add the Intents extension to your project (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d83a8e9-0784-49b4-9644-22eeb548ce07/sirikit-intents09-add-intents-extension-to-project.png">Large preview</a>)</figcaption></figure>

Choose “Intents Extension” and click the “Next” button. Fill out the following screen:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50cf572-502c-4d5d-a750-22dee341f756/sirikit-intents10-new-intents-target.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50cf572-502c-4d5d-a750-22dee341f756/sirikit-intents10-new-intents-target.png" width="1078" height="572" alt="A screeenshot from Xcode showing how you configure the Intents extension" /></a><figcaption>Configure the Intents extension (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50cf572-502c-4d5d-a750-22dee341f756/sirikit-intents10-new-intents-target.png">Large preview</a>)</figcaption></figure>

The product name needs to match whatever you made the suffix in the intents app ID on the Apple developer website.

We are choosing not to add an intents UI extension. This isn’t covered in this article, but you could add it later if you need one. Basically, it’s a way to put your own branding and display style into Siri’s visual results.

When you are done, Xcode will create an intents handler class that we can use as a starting part for our Siri implementation.

## The Intents Handler: Resolve, Confirm And Handle

Xcode generated a new target that has a starting point for us.

The first thing you have to do is set up this new target to be in the same app group as the app. As before, go to the “Capabilities” tab of the target, and turn on app groups, and configure it with your group name. Remember, apps in the same group have a sandbox that they can use to share files with each other. We need this in order for Siri requests to get to our app.

List-o-Mat has a function that returns the group document folder. We should use it whenever we want to read or write to a shared file.

<div class="break-out">

<pre><code class="language-javascript">func documentsFolder() -> URL? {
    return FileManager.default.containerURL(forSecurityApplicationGroupIdentifier: "group.com.app-o-mat.ListOMat")
}
</code></pre></div>

For example, when we save the lists, we use this:

<div class="break-out">

<pre><code class="language-javascript">func save(lists: Lists) {
    guard let docsDir = documentsFolder() else {
        fatalError("no docs dir")
    }

    let url = docsDir.appendingPathComponent(fileName, isDirectory: false)

    // Encode lists as JSON and save to url
}
</code></pre></div>

The Intents extension template created a file named `IntentHandler.swift`, with a class named `IntentHandler`. It also configured it to be the intents’ entry point in the extension’s `plist`.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/624e1b19-2fe4-4564-8b8f-80a7ba942319/sirikit-intents11-intent-handler-plist.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/624e1b19-2fe4-4564-8b8f-80a7ba942319/sirikit-intents11-intent-handler-plist.png" width="577" height="29" alt="A screenshot from Xcode showing how the IntentHandler is configured as an entry point" /></a><figcaption>The intent extension plist configures IntentHandler as the entry point</figcaption></figure>

In this same `plist`, you will see a section to declare the intents we support. We’re going to start with the one that allows searching for lists, which is named `INSearchForNotebookItemsIntent`. Add it to the array under `IntentsSupported`.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e07f699b-3dfe-4094-94cc-994be7998113/sirikit-intents12-domain-add-to-intent.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e07f699b-3dfe-4094-94cc-994be7998113/sirikit-intents12-domain-add-to-intent.png" width="1066" height="182" alt="A screenshot in Xcode showing that the extension plist should list the intents it handles" /></a><figcaption>Add the intent’s name to the intents plist (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e07f699b-3dfe-4094-94cc-994be7998113/sirikit-intents12-domain-add-to-intent.png">Large preview</a>)</figcaption></figure>

Now, go to `IntentHandler.swift` and replace its contents with this code:

<div class="break-out">

<pre><code class="language-javascript">import Intents

class IntentHandler: INExtension {
    override func handler(for intent: INIntent) -> Any? {
        switch intent {
        case is INSearchForNotebookItemsIntent:
            return SearchItemsIntentHandler()
        default:
            return nil
        }
    }
}
</code></pre></div>

The `handler` function is called to get an object to handle a specific intent. You can just implement all of the protocols in this class and return `self`, but we’ll put each intent in its own class to keep it better organized.

Because we intend to have a few different classes, let’s give them a common base class for code that we need to share between them:

<pre><code class="language-javascript">class ListOMatIntentsHandler: NSObject {
}
</code></pre>

The intents framework requires us to inherit from `NSObject`. We’ll fill in some methods later.

We start our search implementation with this:

<pre><code class="language-javascript">class SearchItemsIntentHandler: ListOMatIntentsHandler,
                                                       INSearchForNotebookItemsIntentHandling {
}
</code></pre>

To set an intent handler, we need to implement three basic steps

1. **Resolve** the parameters.  
Make sure required parameters are given, and disambiguate any you don’t fully understand.
2. **Confirm** that the request is doable.  
This is often optional, but even if you know that each parameter is good, you might still need access to an outside resource or have other requirements.
3. **Handle** the request.  
Do the thing that is being requested.

`INSearchForNotebookItemsIntent`, the first intent we’ll implement, can be used as a task search. The kinds of requests we can handle with this are, “In List-o-Mat, show the grocery store list” or “In List-o-Mat, show the store list.”

Aside: “List-o-Mat” is actually a bad name for a SiriKit app because Siri has a hard time with hyphens in apps. Luckily, SiriKit allows us to have alternate names and to provide pronunciation. In the app’s `Info.plist`, add this section:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3e83a1-940d-4b65-96fa-dc4b9a50fe90/sirikit-intents13-alternate-app-name.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3e83a1-940d-4b65-96fa-dc4b9a50fe90/sirikit-intents13-alternate-app-name.png" width="566" height="78" alt="A screenshot from Xcode showing that the app plist can add alternate app names and pronunciations" /></a><figcaption>Add alternate app name's and pronunciation guides to the app plist</figcaption></figure>

This allows the user to say “list oh mat” and for that to be understood as a single word (without hyphens). It doesn’t look ideal on the screen, but without it, Siri sometimes thinks “List” and “Mat” are separate words and gets very confused.

### Resolve: Figuring Out The Parameters

For a search for notebook items, there are several parameters:

1. the item type (a task, a task list, or a note),
2. the title of the item,
3. the content of the item,
4. the completion status (whether the task is marked done or not),
3. the location it is associated with,
4. the date it is associated with.

We require only the first two, so we’ll need to write resolve functions for them. `INSearchForNotebookItemsIntent` has methods for us to implement.

Because we only care about showing task lists, we’ll hardcode that into the resolve for item type. In `SearchItemsIntentHandler`, add this:

<div class="break-out">

<pre><code class="language-javascript">func resolveItemType(for intent: INSearchForNotebookItemsIntent,
                         with completion: @escaping (INNotebookItemTypeResolutionResult) -> Void) {

    completion(.success(with: .taskList))
}
</code></pre></div>

So, no matter what the user says, we’ll be searching for task lists. If we wanted to expand our search support, we’d let Siri try to figure this out from the original phrase and then just use `completion(.needsValue())` if the item type was missing. Alternatively, we could try to guess from the title by seeing what matches it. In this case, we would complete with success when Siri knows what it is, and we would use `completion(.notRequired())` when we are going to try multiple possibilities.

Title resolution is a little trickier. What we want is for Siri to use a list if it finds one with an exact match for what you said. If it’s unsure or if there is more than one possibility, then we want Siri to ask us for help in figuring it out. To do this, SiriKit provides a set of resolution enums that let us express what we want to happen next.

So, if you say “Grocery Store,” then Siri would have an exact match. But if you say “Store,” then Siri would present a menu of matching lists.

We’ll start with this function to give the basic structure:

<div class="break-out">

<pre><code class="language-javascript">func resolveTitle(for intent: INSearchForNotebookItemsIntent, with completion: @escaping (INSpeakableStringResolutionResult) -> Void) {
    guard let title = intent.title else {
        completion(.needsValue())
        return
    }

    let possibleLists = getPossibleLists(for: title)
    completeResolveListName(with: possibleLists, for: title, with: completion)
}
</code></pre></div>

We’ll implement `getPossibleLists(for:)` and `completeResolveListName(with:for:with:)` in the `ListOMatIntentsHandler` base class.

`getPossibleLists(for:)` needs to try to fuzzy match the title that Siri passes us with the actual list names.

<div class="break-out">

<pre><code class="language-javascript">public func getPossibleLists(for listName: INSpeakableString) -> [INSpeakableString] {
    var possibleLists = [INSpeakableString]()
    for l in loadLists() {
        if l.name.lowercased() == listName.spokenPhrase.lowercased() {
            return [INSpeakableString(spokenPhrase: l.name)]
        }
        if l.name.lowercased().contains(listName.spokenPhrase.lowercased()) || listName.spokenPhrase.lowercased() == "all" {
            possibleLists.append(INSpeakableString(spokenPhrase: l.name))
        }
    }
    return possibleLists
}
</code></pre></div>

We loop through all of our lists. If we get an exact match, we’ll return it, and if not, we’ll return an array of possibilities. In this function, we’re simply checking to see whether the word the user said is contained in a list name (so, a pretty simple match). This lets “Grocery” match “Grocery Store.” A more advanced algorithm might try to match based on words that sound the same (for example, with the [Soundex algorithm](https://en.wikipedia.org/wiki/Soundex)),

`completeResolveListName(with:for:with:)` is responsible for deciding what to do with this list of possibilities.

<div class="break-out">

<pre><code class="language-javascript">public func completeResolveListName(with possibleLists: [INSpeakableString], for listName: INSpeakableString, with completion: @escaping (INSpeakableStringResolutionResult) -> Void) {
    switch possibleLists.count {
    case 0:
        completion(.unsupported())
    case 1:
        if possibleLists[0].spokenPhrase.lowercased() == listName.spokenPhrase.lowercased() {
            completion(.success(with: possibleLists[0]))
        } else {
            completion(.confirmationRequired(with: possibleLists[0]))
        }
    default:
        completion(.disambiguation(with: possibleLists))
    }
}
</code></pre></div>

If we got an exact match, we tell Siri that we succeeded. If we got one inexact match, we tell Siri to ask the user if we guessed it right.

If we got multiple matches, then we use `completion(.disambiguation(with: possibleLists))` to tell Siri to show a list and let the user pick one.

Now that we know what the request is, we need to look at the whole thing and make sure we can handle it.

### Confirm: Check All Of Your Dependencies

In this case, if we have resolved all of the parameters, we can always handle the request. Typical `confirm()` implementations might check the availability of external services or check authorization levels.

Because `confirm()` is optional, we could just do nothing, and Siri would assume we could handle any request with resolved parameters. To be explicit, we could use this:

<div class="break-out">

<pre><code class="language-javascript">func confirm(intent: INSearchForNotebookItemsIntent, completion: @escaping (INSearchForNotebookItemsIntentResponse) -> Void) {
    completion(INSearchForNotebookItemsIntentResponse(code: .success, userActivity: nil))
}
</code></pre></div>

This means we can handle anything.

### Handle: Do It

The final step is to handle the request.

<div class="break-out">

<pre><code class="language-javascript">func handle(intent: INSearchForNotebookItemsIntent, completion: @escaping (INSearchForNotebookItemsIntentResponse) -> Void) {
    guard
        let title = intent.title,
        let list = loadLists().filter({ $0.name.lowercased() == title.spokenPhrase.lowercased()}).first
    else {
        completion(INSearchForNotebookItemsIntentResponse(code: .failure, userActivity: nil))
        return
    }

    let response = INSearchForNotebookItemsIntentResponse(code: .success, userActivity: nil)
    response.tasks = list.items.map {
        return INTask(title: INSpeakableString(spokenPhrase: $0.name),
                      status: $0.done ? INTaskStatus.completed : INTaskStatus.notCompleted,
                      taskType: INTaskType.notCompletable,
                      spatialEventTrigger: nil,
                      temporalEventTrigger: nil,
                      createdDateComponents: nil,
                      modifiedDateComponents: nil,
                      identifier: "\(list.name)\t\($0.name)")
    }
    completion(response)
}
</code></pre></div>

First, we find the list based on the title. At this point, `resolveTitle` has already made sure that we’ll get an exact match. But if there’s an issue, we can still return a failure.

When we have a failure, we have the option of passing a user activity. If your app uses [Handoff](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/Handoff/HandoffFundamentals/HandoffFundamentals.html) and has a way to handle this exact type of request, then Siri might try deferring to your app to try the request there. It will not do this when we are in a voice-only context (for example, you started with “Hey Siri”), and it doesn’t guarantee that it will do it in other cases, so don’t count on it.

This is now ready to test. Choose the intent extension in the target list in Xcode. But before you run it, edit the scheme.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b0ce00d-7b29-41ed-b668-32d8f3ff2591/sirikit-intents14-edit-intent-scheme.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b0ce00d-7b29-41ed-b668-32d8f3ff2591/sirikit-intents14-edit-intent-scheme.png" width="326" height="116" alt="A screenshot from Xcode showing how to edit a scheme" /></a><figcaption>Edit the scheme of the the intent to add a sample phrase for debugging.</figcaption></figure>

That brings up a way to provide a query directly:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48619fcf-3e87-4ef3-82ed-d12bb57790b6/sirikit-intents15-siri-query.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48619fcf-3e87-4ef3-82ed-d12bb57790b6/sirikit-intents15-siri-query.png" width="710" height="286" alt="A screenshot from Xcode showing the edit scheme dialog" /></a><figcaption>Add the sample phrase to the Run section of the scheme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48619fcf-3e87-4ef3-82ed-d12bb57790b6/sirikit-intents15-siri-query.png">Large preview</a>)</figcaption></figure>

Notice, I am using “ListOMat” because of the hyphens issue mentioned above. Luckily, it’s pronounced the same as my app’s name, so it should not be much of an issue.

Back in the app, I made a “Grocery Store” list and a “Hardware Store” list. If I ask Siri for the “store” list, it will go through the disambiguation path, which looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7752611a-ee4a-43ba-b34f-b1268dae33bb/sirikit-intentslist-o-mat-store.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7752611a-ee4a-43ba-b34f-b1268dae33bb/sirikit-intentslist-o-mat-store.gif" width="602" height="884" alt="An animated GIF showing Siri handling a request to show the Store list" /></a><figcaption>Siri handles the request by asking for clarification. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7752611a-ee4a-43ba-b34f-b1268dae33bb/sirikit-intentslist-o-mat-store.gif">Large preview</a>)</figcaption></figure>

If you say “Grocery Store,” then you’ll get an exact match, which goes right to the results.

## Adding Items Via Siri

Now that we know the basic concepts of resolve, confirm and handle, we can quickly add an intent to add an item to a list.

First, add `INAddTasksIntent` to the extension’s plist:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d938700-2a88-4a68-9e22-d6cc9ca5fa64/sirikit-intents16-all-intents-plist.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d938700-2a88-4a68-9e22-d6cc9ca5fa64/sirikit-intents16-all-intents-plist.png" width="588" height="110" alt="A screenshot in XCode showing the new intent being added to the plist" /></a><figcaption>Add the INAddTasksIntent to the extension plist (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d938700-2a88-4a68-9e22-d6cc9ca5fa64/sirikit-intents16-all-intents-plist.png">Large preview</a>)</figcaption></figure>

Then, update our `IntentHandler`’s `handle` function.

<pre><code class="language-javascript">override func handler(for intent: INIntent) -> Any? {
    switch intent {
    case is INSearchForNotebookItemsIntent:
        return SearchItemsIntentHandler()
    case is INAddTasksIntent:
        return AddItemsIntentHandler()
    default:
        return nil
    }
}
</code></pre>

Add a stub for the new class:

<div class="break-out">

<pre><code class="language-javascript">class AddItemsIntentHandler: ListOMatIntentsHandler, INAddTasksIntentHandling {
}
</code></pre></div>

Adding an item needs a similar `resolve` for searching, except with a target task list instead of a title.

<div class="break-out">

<pre><code class="language-javascript">func resolveTargetTaskList(for intent: INAddTasksIntent, with completion: @escaping (INTaskListResolutionResult) -> Void) {

    guard let title = intent.targetTaskList?.title else {
        completion(.needsValue())
        return
    }

    let possibleLists = getPossibleLists(for: title)
    completeResolveTaskList(with: possibleLists, for: title, with: completion)
}
</code></pre></div>

`completeResolveTaskList` is just like `completeResolveListName`, but with slightly different types (a task list instead of the title of a task list).

<div class="break-out">

<pre><code class="language-javascript">public func completeResolveTaskList(with possibleLists: [INSpeakableString], for listName: INSpeakableString, with completion: @escaping (INTaskListResolutionResult) -> Void) {

    let taskLists = possibleLists.map {
        return INTaskList(title: $0, tasks: [], groupName: nil, createdDateComponents: nil, modifiedDateComponents: nil, identifier: nil)
    }

    switch possibleLists.count {
    case 0:
        completion(.unsupported())
    case 1:
        if possibleLists[0].spokenPhrase.lowercased() == listName.spokenPhrase.lowercased() {
            completion(.success(with: taskLists[0]))
        } else {
            completion(.confirmationRequired(with: taskLists[0]))
        }
    default:
        completion(.disambiguation(with: taskLists))
    }
}
</code></pre></div>

It has the same disambiguation logic and behaves in exactly the same way. Saying “Store” needs to be disambiguated, and saying “Grocery Store” would be an exact match.

We’ll leave `confirm` unimplemented and accept the default. For `handle`, we need to add an item to the list and save it.

<div class="break-out">

<pre><code class="language-javascript">func handle(intent: INAddTasksIntent, completion: @escaping (INAddTasksIntentResponse) -> Void) {
    var lists = loadLists()
    guard
        let taskList = intent.targetTaskList,
        let listIndex = lists.index(where: { $0.name.lowercased() == taskList.title.spokenPhrase.lowercased() }),
        let itemNames = intent.taskTitles, itemNames.count > 0
    else {
            completion(INAddTasksIntentResponse(code: .failure, userActivity: nil))
            return
    }

    // Get the list
    var list = lists[listIndex]

    // Add the items
    var addedTasks = [INTask]()
    for item in itemNames {
        list.addItem(name: item.spokenPhrase, at: list.items.count)
        addedTasks.append(INTask(title: item, status: .notCompleted, taskType: .notCompletable, spatialEventTrigger: nil, temporalEventTrigger: nil, createdDateComponents: nil, modifiedDateComponents: nil, identifier: nil))
    }

    // Save the new list
    lists[listIndex] = list
    save(lists: lists)

    // Respond with the added items
    let response = INAddTasksIntentResponse(code: .success, userActivity: nil)
    response.addedTasks = addedTasks
    completion(response)
}
</code></pre></div>

We get a list of items and a target list. We look up the list and add the items. We also need to prepare a response for Siri to show with the added items and send it to the completion function.

This function can handle a phrase like, “In ListOMat, add apples to the grocery list.” It can also handle a list of items like, “rice, onions and olives.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4007cc94-d909-4357-af25-2d9fc7c9738e/sirikit-intents17-list-o-mat-add-items.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4007cc94-d909-4357-af25-2d9fc7c9738e/sirikit-intents17-list-o-mat-add-items.png" width="559" height="981" alt="A screenshot of the simulator showing Siri adding items to the grocery store list" /></a><figcaption>Siri adds a few items to the grocery store list</figcaption></figure>

## Almost Done, Just A Few More Settings

All of this will work in your simulator or local device, but if you want to submit this, you’ll need to add a `NSSiriUsageDescription` key to your app’s `plist`, with a string that describes what you are using Siri for. Something like “Your requests about lists will be sent to Siri” is fine.

You should also add a call to:

<pre><code class="language-javascript">INPreferences.requestSiriAuthorization { (status) in }
</code></pre>

Put this in your main view controller’s `viewDidLoad` to ask the user for Siri access. This will show the message you configured above and also let the user know that they could be using Siri for this app.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/985615fb-8ee0-40d2-800c-1f51711f0eff/sirikit-intents18-ask-for-siri.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/985615fb-8ee0-40d2-800c-1f51711f0eff/sirikit-intents18-ask-for-siri.png" width="277" height="234" alt="A screenshot of the dialog that a device pops up when you ask for Siri permission" /></a><figcaption>The device will ask for permission if you try to use Siri in the app.</figcaption></figure>

Finally, you’ll need to tell Siri what to tell the user if the user asks what your app can do, by providing some [sample phrases](https://developer.apple.com/documentation/sirikit/registering_custom_vocabulary_with_sirikit/global_vocabulary_reference/intent_phrases):

1. Create a `plist` file in your app (not the extension), named `AppIntentVocabulary.plist`.
2. Fill out the intents and phrases that you support.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc24c80b-798e-4dfa-9780-b8fee734d0ad/sirikit-intents19-example-phrases.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc24c80b-798e-4dfa-9780-b8fee734d0ad/sirikit-intents19-example-phrases.png" width="717" height="244" alt="A screenshot of the AppIntentVocabulary.plist showing sample phrases" /></a><figcaption>Add an <code>AppIntentVocabulary.plist</code> to list the sample phrases that will invoke the intent you handle. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc24c80b-798e-4dfa-9780-b8fee734d0ad/sirikit-intents19-example-phrases.png">Large preview</a>)</figcaption></figure>

There is no way to really know all of the phrases that Siri will use for an intent, but Apple does provide a few samples for each intent in its documentation. The [sample phrases for task-list searching](https://developer.apple.com/documentation/sirikit/insearchfornotebookitemsintent) show us that Siri can understand “Show me all my notes on \<appName\>,” but I found other phrases by trial and error (for example, Siri understands what “lists” are too, not just notes).

## Summary

As you can see, adding Siri support to an app has a lot of steps, with a lot of configuration. But the code needed to handle the requests was fairly simple.

There are a lot of steps, but each one is small, and you might be familiar with a few of them if you have used extensions before.

Here is what you’ll need to prepare for a new extension on Apple’s developer website:

1. Make an app ID for an Intents extension.
1. Make an app group if you don’t already have one.
1. Use the app group in the app ID for the app and extension.
1. Add Siri support to the app’s ID.
1. Regenerate the profiles and download them.

And here are the steps in Xcode for creating Siri’s Intents extension:

1. Add an Intents extension using the Xcode template.
1. Update the entitlements of the app and extension to match the profiles (groups and Siri support).
1. Add your intents to the extension’s `plist`.

And you’ll need to add code to do the following things:

1. Use the app group sandbox to communicate between the app and extension.
1. Add classes to support each intent with resolve, confirm and handle functions.
1. Update the generated `IntentHandler` to use those classes.
1. Ask for Siri access somewhere in your app.

Finally, there are some Siri-specific configuration settings:

1. Add the Siri support security string to your app’s `plist`.
1. Add sample phrases to an `AppIntentVocabulary.plist` file in your app.
1. Run the intent target to test; edit the scheme to provide the phrase.

OK, that is a lot, but if your app fits one of Siri’s domains, then users will expect that they can interact with it via voice. And because the competition for voice assistants is so good, we can only expect that WWDC 2018 will bring a bunch more domains and, hopefully, much better Siri.

### Further Reading

- “[SiriKit](https://developer.apple.com/documentation/sirikit),” Apple  
The technical documentation contains the full list of domains and intents.
- “[Guides and Sample Code](https://developer.apple.com/library/content/samplecode/IntentHandling/Introduction/Intro.html),” Apple  
Includes code for many domains.
- “[Introducing SiriKit](https://developer.apple.com/videos/play/wwdc2016/217/)” (video, Safari only), WWDC 2016 Apple
- “[What’s New in SiriKit](https://developer.apple.com/videos/play/wwdc2017/214/)” (video, Safari only), WWDC 2017, Apple  
Apple introduces lists and notes
- “[Lists and Notes](https://developer.apple.com/documentation/sirikit/lists_and_notes),” Apple  
The full list of lists and notes intents.

{{< signature "da, ra, al, il" >}}

