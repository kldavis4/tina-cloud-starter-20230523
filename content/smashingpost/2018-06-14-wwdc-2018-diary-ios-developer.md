---
title: 'WWDC 2018 Diary Of An iOS Developer'
slug: wwdc-2018-diary-ios-developer
author: lou-franco
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f761b7-ce7f-4e6e-8edc-30d320cbb3fa/wwdc-2018-diary-day-2-copylist-debug.jpeg
date: 2018-06-14T13:45:32+02:00
summary: >-
  Since 1987, the Apple Worldwide Developers Conference (WWDC) has been taking place annually and keeping iOS developers on their toes. Lou Franco watched this year’s event and shares his notes and references in case you missed out. 
description: >-
  Since 1987, the Apple Worldwide Developers Conference (WWDC) has been taking place annually and keeping iOS developers on their toes. Lou Franco watched this year’s event and shares his notes and references in case you missed out.
categories:
  - Events
  - iOS
  - Tools
---
The traditional boundaries of summer in the US are Memorial and Labor Day, but iOS developers mark the summer by WWDC and the iPhone release. Even though the weather is cool and rainy this week in NYC, I’m in a summer mood and looking forward to the renewal that summer and WWDC promise.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f668c12-dd91-4f44-a118-2f9f59c94b5e/wwdc-2018-diary-intro-wwdc.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f668c12-dd91-4f44-a118-2f9f59c94b5e/wwdc-2018-diary-intro-wwdc.jpg" sizes="100vw" caption="WWDC (<a href='https://commons.wikimedia.org/wiki/File:San_Jose_Convention_Center_main_entrance,_WWDC17.jpg'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f668c12-dd91-4f44-a118-2f9f59c94b5e/wwdc-2018-diary-intro-wwdc.jpg'>Large preview</a>)" alt="Photo in front of the San Jose McEnery Convention Center" >}}

It’s the morning of June 4th, and I’m reviewing my notes from [WWDC 2017](https://www.smashingmagazine.com/2017/07/wwdc-2017-highlights/). Last year, I wrote that ARKit and Core ML were two of the big highlights. It was refreshing to see Apple focus on Machine Learning (ML), but there wasn’t much follow up in the rest of 2017. ARKit has spawned some interest, but no killer app (perhaps Pokemon Go, but that was popular before ARKit). Apple did not add to its [initial library of Core ML downloadable models](https://developer.apple.com/machine-learning/) after the Core ML announcement. 

Apple did release [Turi Create](https://github.com/apple/turicreate) and Lobe released a new interesting [Core ML model maker](https://lobe.ai/) last month. In the Apple/ML space, Swift creator, Chris Lattner, is taking a different approach with [Swift for TensorFlow](https://www.tensorflow.org/api_docs/swift/). But from the outside, Core ML seems mostly to have one obvious use: image classification. There doesn’t seem to be a lot of energy around exploring wildly different applications (even though we all know the ML is at the core of self-driving cars and whiz-bang demos like Google Duplex).

{{% feature-panel %}}

Another way Apple uses ML is in Siri, and earlier this year, I wrote about [SiriKit](https://www.smashingmagazine.com/2018/04/sirikit-intents-app-guide/) and mentioned its perceived and real deficiencies when compared to Alexa and Google. One issue I explored was how Siri’s emphasis on pre-defined intents limits its range but hasn’t produced the promised accuracy that you might get from a bounded focus.

The introduction of HomePod last year only highlighted Siri’s woes, and a [widely reported customer satisfaction survey](https://techpinions.com/top-takeaways-from-studying-iphone-x-owners/52639) showed 98% satisfaction with iPhone X but only a 20% satisfaction with Siri.

With all of this in the back of my mind, I personally was hoping to hear that Apple was going to make some major improvements in AR, ML, and Siri. Specifically, as an iOS developer, I wanted to see many more Core ML models, spanning more than just image classification and more help in making models. For Siri, I wanted to see many more intents and possibly some indication that intents would be a thing that would be added year round. It was a long-shot, but for AR, the next step is a device. But in the meantime, I hoped for increased spatial accuracy.

Finally, I love Xcode Playgrounds and iPad Playground books, but they need to to be a lot faster and stable, so I was hoping for something there too. 

On the morning of WWDC, [I tweeted this](https://twitter.com/loufranco/status/1003605685060456448):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75e60355-3514-49ca-b90a-5cd66ba1958c/wwdc-2018-diary-day-1-tweet.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75e60355-3514-49ca-b90a-5cd66ba1958c/wwdc-2018-diary-day-1-tweet.png" sizes="100vw" caption="My tweet describing what I was hoping for from WWDC 2018 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75e60355-3514-49ca-b90a-5cd66ba1958c/wwdc-2018-diary-day-1-tweet.png'>Large preview</a>)" alt="An image of a tweet with my WWDC wishes" >}}

This wasn’t a prediction. It’s just a list of things I wanted to use in 2017 but found them underpowered or too hard for me to get started with, and was hoping Apple would make some improvements.

My plan for the day is to watch the keynote live, and then to watch the Platforms State of the Union. Those give a good overview of what to concentrate on for the rest of the week.

## End Of Day 1: The Keynote And Platforms State Of The Union

The first day of WWDC is the [keynote](https://developer.apple.com/videos/play/wwdc2018/101/), which is meant for public consumption, and the [Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2018/102/), which is an overview of the entire event, with some details for developers so that they can choose which sessions to attend.

### Summary Of Notable, Non-iOS Developer Announcements

WWDC is not entirely about iOS development, so here’s a quick list of other things that happened to the other platforms or that are not very developer focused. 

- To get it out of the way, there were **no hardware announcements at all**. No previews and no updates on the Mac Pro. We’ll have to wait for the iPhone and follow-on events in the fall.
- iOS 12 has a new Shortcuts app that seems to be the result of their acquisition of Workflow. It’s a way to **“script” a series of steps via drag and drop**. You can also assign the shortcut to a Siri keyword, which I’ll be covering below.
- iOS will **automatically group notifications** that are from the same app and let you act on them as a group.
- Animojis can now mimic you sticking out your tongue, and the new **Memojis are highly configurable human faces** that you can customize to look like yourself.
- **FaceTime supports group video chat** of up to 32 people.
- There is a new **Screen Time app that gives you reports on your phone and app usage** (to help you control yourself and be less distracted). It is also the basis of new parental controls.
- Apple TV got a small update: Support for Dolby Atmos and new **screen savers taken from the International Space Station**.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75a1ff08-72f1-41d3-a519-39cd1f3ec655/wwdc-2018-diary-intro-tv-space.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75a1ff08-72f1-41d3-a519-39cd1f3ec655/wwdc-2018-diary-intro-tv-space.jpg" sizes="100vw" caption="Apple TV Space Screen Saver (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75a1ff08-72f1-41d3-a519-39cd1f3ec655/wwdc-2018-diary-intro-tv-space.jpg'>Large preview</a>)" alt="Photo of the new Apple TV Space Screen Saver" >}}

- **The Watch got a competition mode** for challenging others to workout-related challenges. It will also try to **auto-detect the beginning and end of workouts** in case you forget to start or stop them, and it now has Hiking and Yoga workouts.
- The Watch also has a new Walkie-Talkie mode that you can enable for trusted contacts.
- There are **more audio SDKs that are native on the Watch**, and Apple’s Podcasts app is now available. I expect third-party podcast apps will take advantage of these new SDKs as well.
- The Mac got the anchor spot of the event (which is hopefully an indication of renewed attention). It will be called **macOS Mojave and features a  dark mode**.
- There are big updates to the Mac App Store, but notably, it now gets the **same visual and content treatment the iOS App Store** got last year. There are enough changes to the sandbox that **Panic has decided to move Transit back there**.
- **Quick Look in the Finder now has some simple actions** you can do to the file (e.g. rotating an image) and is customizable via Automator.
- **Mojave will be the last version of macOS to support 32-bit** apps and frameworks, which means the Quick Time Framework going away. It has seemingly been replaced with some video capture features in the OS itself.
- Apple announced that they are internally using **a port of UIKit to make Mac apps** and showed ports of Stocks, News, Home, and Voice Memos. The new framework will be released in 2019.

### The iOS Developer Announcements I’m Most Excited About

iOS Developers got some good news as well. They hit on the four major areas I wanted to see improvement on:

- SiriKit now has **custom intents**, which opens up the possibilities quite a bit.
- Create ML is a new way to use Xcode Playgrounds to train models via _transfer learning_, which lets you **augment existing models with your own training data**.
- Xcode playgrounds now allow you to **add code to the bottom of a page and run it without restarting**. It’s hard to know if Playgrounds will be more stable until we get a real release in September, but this will make trying code much faster.
- ARKit 2 was announced along with a **new Augmented Reality file format called USDZ**, which is open and was developed with Adobe and Pixar. Adobe announced some tooling support already. It will allow users and developers to store and share AR assets and experiences. In addition, ARKit 2 allows multiple devices to be in the same AR environment and supports 3D object detection.

We didn’t get an AR device, but it sure feels like we’ll get one soon. And it needs to come from Apple (not third parties) because running ARKit requires an iOS device.

### Setting Up Your Machine

Everything you need is available now in the [developer portal](https://developer.apple.com/download/). To use the code in the article, you need the Xcode 10 Beta. I would not recommend using iOS 12 Betas yet, but if you really want to, go to the portal on your device and download the iOS 12 Beta Configuration Profile.

The only major thing you need a device with the beta for is ARKit 2. Everything else should run well enough in Xcode 10’s simulator. As of the first beta, Siri Shortcut support in the simulator is limited, but there is enough there to think that that will be fixed in future releases.

## End Of Day 2: Playing With Siri Custom Intents

Last year, I wrote how you needed to fit within one of Apple’s pre-defined intents in order to [use SiriKit in your app](https://www.smashingmagazine.com/2018/04/sirikit-intents-app-guide/). This mechanism was introduced in 2016 and added to in 2017 and even between WWDC events. But it was clear that Amazon’s approach of custom intents was superior for getting voice control into more diverse apps, and Apple added that to SiriKit last week.

To be clear, this is a first implementation, so it’s not as extensive as Alexa Skills just yet, but it opens up Siri’s possibilities quite a bit. As I discussed in the previous article, the main limitation of custom intents is that the developer needs to do all of the language translation. SiriKit gets around this a little by asking the user to provide the phrase that they’d like to use, but there is still more translation needed for custom intents than for predefined intents.

And they built in on the same foundation as the predefined intents, so everything I covered still applies. In fact, I will show you how to add a new custom intent to [List-o-Mat](https://github.com/app-o-mat/ListOMat), the app I wrote for the original SiriKit article.

### (Free) Siri Shortcut Support If You Already Support Spotlight

If you use `NSUserActivity` to indicate things in your app that your user can initiate via handoff or search, then it’s trivial to make them available to Siri as well.

All you need to do is add the following line to your activity object:

<pre><code class="language-javascript">activity.isEligibleForPrediction = true
</code></pre>

This will only work for Spotlight-enabled activities (where `isEligibleForSearch` is `true`).

Now, when users do this activity, it is considered *donated* for use in Siri. Siri will recommend very commonly done activities or users can find them in the Shortcuts app. In either case, the user will be able to assign their own spoken phrase in order to start it. Your support for starting the activity via Spotlight is sufficient to support it being started via a shortcut.

In List-o-Mat, we could make the individual lists available to Spotlight and Siri by constructing activity objects and assigning them to the `ListViewController`. Users could open them via Siri with their own phrase. 

It’s redundant in our case because we had a pre-defined intent for opening a list, but most apps are not so lucky and now have this simple mechanism. So, if your app has activities that aren’t supported by Siri’s pre-defined intents (e.g. playing a podcast), you can just make them eligible for prediction and not worry about custom intents.

### Configuring SiriKit To Use Custom Intents

If you do need to use a custom intent, then SiriKit needs to be added to your app, which requires a bit of configuration.

All of the steps for configuring SiriKit for custom intents are the same as for predefined intents, which is covered in detail in my [SiriKit article here on Smashing](https://www.smashingmagazine.com/2018/04/sirikit-intents-app-guide/). To summarize: 

1. You are adding an extension, so you need a new App ID, and provisioning profile and your app’s entitlements needs have Siri added.
2. You probably need an App Group (it’s how the extension and app communicate).
3. You’ll need an Intents Extension in your project
4. There are Siri specific *.plist* keys and project entitlements you need to update.

All of the details can be found in my SiriKit article, so I’ll just cover what you need to support a custom intent in List-o-Mat.

### Adding A Copy List Command To List-o-Mat

Custom intents are meant to be used only where there is no pre-defined intent, and Siri does actually offer a lot of list and task support in its Lists and Notes Siri Domain.

But, one way to use a list is as a template for a repeated routine or process. To do that we’ll want to copy an existing list and uncheck all of its items. The built-in List intents don’t support this action.

First, we need to add a way to do this manually. Here is a demo of this new behavior in List-o-Mat:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b58455d-839c-47f4-a5ff-9cc0f7b41585/wwdc-2018-diary-day-2-copy-list.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b58455d-839c-47f4-a5ff-9cc0f7b41585/wwdc-2018-diary-day-2-copy-list.gif" width="600" alt="An animated GIF with a demo of copying lists" /></a><figcaption>Copying a list in List-o-Mat</figcaption></figure>

To get this behavior to be invokable by Siri, we’ll “donate an intent,” which means we’ll tell iOS every time you do this. Then, it will eventually learn that in the morning, you like to copy this list and offer it as a shortcut. Users can also look for donated intents and assign phrases manually.

### Creating The Custom Intent

The next step is to create the custom intent in Xcode. There is a new file template, so:

<ol>
    <li>Choose File&nbsp;&rarr;&nbsp;New File and pick “SiriKit Intent Definition File”.<br />
        <figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6631332-a3c4-4288-a531-a9f618ad04f4/wwdc-2018-diary-day-2-custom-intent.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6631332-a3c4-4288-a531-a9f618ad04f4/wwdc-2018-diary-day-2-custom-intent.png" alt="A screen shot of the New File dialog" /></a><figcaption>Choose to add an intent definition file (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6631332-a3c4-4288-a531-a9f618ad04f4/wwdc-2018-diary-day-2-custom-intent.png">Large preview</a>)</figcaption></figure>
    </li>
    <li>Name the file <em>ListOMatCustomIntents.intentdefinition</em>, and choose to put the file in both the App and Intent Extension targets. This will automatically generate classes into both targets that implement the intent protocols but have your custom behavior implemented.</li>
    <li>Open the <em>Definition</em> file.</li>
    <li>Use the + button on the bottom left to add an intent and name it “CopyList”.</li>
    <li>Set the Category to “Create” and fill in the title and subtitle to describe the intent:<br />
        <figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/615d8f71-e9ba-4778-bdf2-7da14e036421/wwdc-2018-diary-day-2-custom-intent-form.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/615d8f71-e9ba-4778-bdf2-7da14e036421/wwdc-2018-diary-day-2-custom-intent-form.png" alt="Screenshot of the custom intent description" /></a><figcaption>Add a category, title, and subtitle to the intent (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/615d8f71-e9ba-4778-bdf2-7da14e036421/wwdc-2018-diary-day-2-custom-intent-form.png">Large preview</a>)</figcaption></figure>
    </li>
    <li>Add a String parameter named “list”.<br />
        <figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e65a1c85-4240-4162-b85c-bb09a4b9e523/wwdc-2018-diary-day-2-custom-intent-param.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e65a1c85-4240-4162-b85c-bb09a4b9e523/wwdc-2018-diary-day-2-custom-intent-param.png" alt="Screenshot of the parameter section" /></a><figcaption>Add a String paramter named “list” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e65a1c85-4240-4162-b85c-bb09a4b9e523/wwdc-2018-diary-day-2-custom-intent-param.png">Large preview</a>)</figcaption></figure>
    </li>
    <li>Add a shortcut type with the list parameter and give it a title named “Copy list”.<br />
        <figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf24b9a5-4b3a-4e7d-b456-ec58fbd16985/wwdc-2018-diary-day-2-shortcut-type.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf24b9a5-4b3a-4e7d-b456-ec58fbd16985/wwdc-2018-diary-day-2-shortcut-type.png" alt="Screenshot of the shortcut type section" /></a><figcaption>Add a shortcut type titled “Copy list” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf24b9a5-4b3a-4e7d-b456-ec58fbd16985/wwdc-2018-diary-day-2-shortcut-type.png">Large preview</a>)</figcaption></figure>
    </li>
</ol>

If you look in the Intent plist, you will see that this intent has already been configured for you:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c55b7f6-8058-4d4b-ba9d-f6a87499a383/wwdc-2018-diary-day-2-plist.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c55b7f6-8058-4d4b-ba9d-f6a87499a383/wwdc-2018-diary-day-2-plist.png" sizes="100vw" caption="" alt="" >}}

### Donating The Intent

When we do a user interaction in our app that we want Siri to know about, we donate it to Siri. Siri keeps track of contextual information, like the time, day of the week, and even location, and if it notices a pattern, it will offer the shortcut to the user.

When we tap the Copy menu, add this code:

<div class="break-out">

<pre><code class="language-javascript">@available(iOS 12, *)
func donateCopyListInteraction(listName: String) {
    let copyListInteraction = CopyListIntent()
    copyListInteraction.list = listName
    copyListInteraction.suggestedInvocationPhrase = "Copy \(listName)"
    let interaction = INInteraction(intent: copyListInteraction, response: nil)
    interaction.donate { [weak self] (error) in
        self?.show(error: error)
    }
}
</code></pre></div>

This simply creates an object of the auto-generated `CopyListIntent` class and donates it to Siri. Normally, iOS would collect this info and wait for the appropriate time to show it, but for development, you can open the Settings app, go to the Developer section, and turn on Siri Shortcut debugging settings.

**Note**: *As of this writing, with the first betas, this debug setting only works on devices, and not the simulator. Since the setting is there, I expect it to start working in further betas.*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bc372de-1f4a-49a5-9e07-63443b53625c/wwdc-2018-diary-day-2-dev-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bc372de-1f4a-49a5-9e07-63443b53625c/wwdc-2018-diary-day-2-dev-settings.png" sizes="100vw" caption="Turn on Siri Shortcut debugging" alt="Screenshot of Siri debug settings" >}}

When you do this, your donated shortcut shows up on in Siri Suggestions in Spotlight.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f761b7-ce7f-4e6e-8edc-30d320cbb3fa/wwdc-2018-diary-day-2-copylist-debug.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f761b7-ce7f-4e6e-8edc-30d320cbb3fa/wwdc-2018-diary-day-2-copylist-debug.jpeg" sizes="100vw" caption="You can debug your donated shortcut in search" alt="Screenshot of the donated shortcut in Siri" >}}

Tapping that will call into your Intent extension because we are allowing background execution. We’ll add support for that next.

### Handling The Custom Intent

We already have an Intents extension, and since the custom intent definitions file is already added to the file, it also has the generated intent classes. All we need to do is add a handler.

The first step is to add a new class, named `CopyListIntentHandler` to the extension. Here is its code:

<div class="break-out">

<pre><code class="language-javascript">import Intents

@available(iOS 12, *)
class CopyListIntentHandler: ListOMatIntentsHandler, CopyListIntentHandling {

    func handle(intent: CopyListIntent, completion: @escaping (CopyListIntentResponse) -> Void) {

        // Find the list
        var lists = loadLists()
        guard
            let listName = intent.list?.lowercased(),
            let listIndex = lists.index(where: { $0.name.lowercased() == listName})
        else {
            completion(CopyListIntentResponse(code: .failure, userActivity: nil))
            return
        }

        // Copy the list to the top, and respond with success
        copyList(from: &lists, atIndex: listIndex, toIndex: 0)
        save(lists: lists)
        let response = CopyListIntentResponse(code: .success, userActivity: nil)
        completion(response)
    }

}
</code></pre></div>

Custom intents only have a confirm and handle phase (custom resolution of parameters is not supported). Since the default `confirm()` returns success, we’ll just implement `handle()`, which has to look up the list, copy it, and let Siri know if it was successful or not.

You also need to dispatch to this class from the registered intent handler by adding this code:

<div class="break-out">

<pre><code class="language-javascript">if #available(iOS 12, *) {
    if intent is CopyListIntent {
        return CopyListIntentHandler()
    }
}
</code></pre></div>

Now you can actually tap that Siri suggestion and it will bring this up:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c76ea5f-b38e-4ca0-af5f-28db47658733/wwdc-2018-diary-day-2-copylist-create.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c76ea5f-b38e-4ca0-af5f-28db47658733/wwdc-2018-diary-day-2-copylist-create.jpeg" sizes="100vw" caption="Activate the shortcut (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c76ea5f-b38e-4ca0-af5f-28db47658733/wwdc-2018-diary-day-2-copylist-create.jpeg'>Large preview</a>)" alt="Screenshot of the activated shortcut" >}}

And tapping the Create button will copy the list. The button says “Create” because of the category we chose in the intent definition file.

Phew, that was a lot. These new Siri shortcuts are the main feature in iOS 12 that has a new large developer surface area to explore. Also, since I happened to have a good (and documented) Siri example to work with, it was reasonable to try to add the new features to it this week.

You can see the update [List-o-Mat in GitHub](https://github.com/app-o-mat/ListOMat/tree/xcode-10-custom-siri-intents). Until Xcode 10 and iOS 12 are released it’s in its own branch.

The next few days, I’ll mostly be looking at Apple sample code or making much smaller projects.

## End Of Day 3: Xcode Playgrounds

The entire previous day was spent in Xcode 10 beta, which didn’t crash once and seemed ready for development. So now I wanted to explore the new Playgrounds features.

The main thing I wanted from playgrounds is to make them more stable and much faster. To make them faster, Apple added a big feature — a REPL mode.

Before Xcode 10, when you were in a Playground that had auto-run on (which is the default), every line of code actually rebuilt the entire file and ran it from the beginning. If you had built up any state, it was lost. But, the real issue was that this was way too slow for iterative development. When I use Playgrounds, I set them to manually run, but even that is slow.

In Xcode 10, manual running is more the norm, but after you run it, you can add more lines at the bottom of the page and continue execution. This means you can explore data and draw views iteratively without constantly rebuilding and starting from scratch.

To get started, I created an iOS playground (File&nbsp;&rarr;&nbsp;New&nbsp;&rarr;&nbsp;Playground) with the Single View template.

Turn on manual running by bringing down the menu below the Play button (the triangle in the bottom left corner). This puts a vertical strip to the left that shows the current position of the Play head (kind of like breakpoints).

You can tap any line and then tap the play button to its left. This will run the Playground to this point. Then you can go further by tapping lines lower in the Playground. Critically, you can add more lines to the bottom and type <kbd>Shift</kbd> + <kbd>Enter</kbd> after each one to move the Play head to that point.

Here’s a GIF of me changing the label of a view without needing to restart the Playground. After each line I type, I am pressing <kbd>Shift</kbd> + <kbd>Enter</kbd>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06ff2439-b94f-4f44-97b4-350da17fee51/wwdc-2018-diary-day-3-playgrounds-small.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06ff2439-b94f-4f44-97b4-350da17fee51/wwdc-2018-diary-day-3-playgrounds-small.gif" width="600" alt="GIF of Playground with REPL mode" /></a><figcaption>Add more code and run it without restarting</figcaption></figure>

Playgrounds also support custom rendering of your types now, and Apple is making a big push for every Swift framework to include a Playground to document it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a7770e-c5c7-4a97-ac70-adf61b548e90/wwdc-2018-diary-day-3-playground-all-the-things.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a7770e-c5c7-4a97-ac70-adf61b548e90/wwdc-2018-diary-day-3-playground-all-the-things.png" sizes="100vw" caption="TJ Usiyan asks WWDC attendees to add Playgrounds to their projects. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a7770e-c5c7-4a97-ac70-adf61b548e90/wwdc-2018-diary-day-3-playground-all-the-things.png'>Large preview</a>)" alt="WWDC photo showing slide to encourage more Playgrounds" >}}

## End Of Day 4: Create ML

Last year, Apple made a big leap for programming Machine Learning for their devices. There was a new ML model file format and direct support for it in Xcode. 

The potential was that there would be a large library of these model files, that there would be tools that would create them, and that many more app developers would be able to incorporate ML into their projects without having to know how to create models.

This hasn’t fully materialized. Apple didn’t add to the repository of models after WWDC, and although there are third-party repositories, they mostly have models that are variations on the image classification demos. ML is used for a lot more than image classification, but a broad selection of examples did not appear.

So, it became clear that any real app would need its developers to train new models. Apple released [Turi Create](day-3-playground-all-the-things.png) for this purpose, but its far from simple.

At WWDC 2018, Apple did a few things to Core ML:

1. They **expanded the Natural Language Processing (NLP) part of Core ML** which gives us a new major domain of examples.
2. They added the concept of *Transfer Learning* to Core ML, which allows you to **add training data to an existing model**. This means you can take models from the library, and customize them to your own data (for example, have them recognize new objects in images you provide).
3. **They released Create ML which is implemented inside of Xcode Playgrounds** and lets you drag and drop data for training and generate model extensions (using Transfer Learning).

This is another nice step in democratizing ML. There’s not much code to write here. To extend an image classifier, you just need to gather and label images. Once you have them, you just drag them into Create ML. You can see the demo in this [Create ML WWDC video](https://developer.apple.com/videos/play/wwdc2018/703/).

## End Of The Week: Play With The New AR Demos

ARKit was another big addition last year and it seems even more clear that an AR device is coming.

My [ARKit code from last year’s article](https://www.smashingmagazine.com/2017/07/wwdc-2017-highlights/#augmented-reality) is still a good way to get started. Most of the new features are about making AR more accurate and faster.

After that, if you have installed a beta, you will definitely want to download the new [SwiftShot ARKit demo app](https://developer.apple.com/arkit/). This app takes advantage of the new features of ARKit, especially the multi-player experience. Two or more devices on the same network and in the same place, can communicate with each other and see the same AR experience. 

Of course, to play this, you need two or more devices you are willing to put on the iOS 12 beta. I’m waiting for the public beta to do this because I only have one beta-safe device.

The easier AR app to play with is the new Measure app, which allows you to measure the length of real objects you see in AR camera view. There have been third-party apps that do this, but Apple’s is polished and pre-installed with iOS 12.

## Links To WWDC Videos And Sample Code

So, I’m looking forward to doing more with Xcode 10 and iOS 12 this summer while we wait for the new phones and whatever devices Apple might release at the end of the summer. In the meantime, iOS developers can enjoy the sun, track our hikes with our new beta Watch OS, and watch these WWDC videos when we get a chance.

[You can stream WWDC 2018 videos](https://developer.apple.com/videos/wwdc2018/) from the Apple developer portal. There is also this unofficial [Mac App for viewing WWDC videos](https://wwdc.io/).

Here are the videos referenced in this article:

- [WWDC 2018 Keynote](https://developer.apple.com/videos/play/wwdc2018/101/)
- [WWDC 2018 Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2018/102/)
- [Introduction to Siri Shortcuts](https://developer.apple.com/videos/play/wwdc2018/211/)
- [Getting the Most out of Playgrounds in Xcode](https://developer.apple.com/videos/play/wwdc2018/402/)
- [Introducing Create ML](https://developer.apple.com/videos/play/wwdc2018/703/), and if you want something more advanced, [A Guide to Turi Create](https://developer.apple.com/videos/play/wwdc2018/712/)

To start playing with Xcode 10 and iOS 12:

- [Download the betas](https://developer.apple.com/download/) (visit on a device to get the beta profile)
- [List-o-Mat with Siri Shortcut updates](https://github.com/app-o-mat/ListOMat/tree/xcode-10-custom-siri-intents)
- [Swift Shot](https://developer.apple.com/arkit/) (the multi-player ARKit 2 game)

{{< signature "ra, il" >}}
