---
title: 'Preparing Your App For iOS 12 Notifications'
slug: preparing-your-app-for-ios-12-notifications
author: kaya-thomas
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cc3d6eb-5da6-4067-b091-1071009a9670/app-ios-12-notifications-hiddenpreviewgroup.png
date: 2018-09-05T13:30:35+02:00
summary: >-
  With the launch of iOS 12, there are several new notification features such as new authorization options, dynamic quick actions, and user interaction within notifications. Learn more about how to implement these features and if they are right for your app.
description: >-
  With the launch of iOS 12, there are several new notification features such as new authorization options, dynamic quick actions and user interaction within notifications. Learn more about how to implement these features and if they are right for your app.
categories:
  - iOS
  - Apps
  - User Interaction
---
In 2016, Apple announced a new extension that will allow developers to better customize their push and local notifications called the `UNNotificationContentExtension`. The extension gets triggered when a user long presses or 3D touches on a notification whenever it is delivered to the phone or from the lock/home screen. In the content extension, developers can use a view controller to structure the UI of their notification, but there was no user interaction enabled within the view controller &mdash; until now. With the release of iOS 12 and XCode 10, **the view controller in the content extension now enables user interaction** which means notifications will become even more powerful and customizable. 

At WWDC 2018, Apple also announced several changes to notification settings and how they appear on the home screen. In an effort to make users more aware of how they are using apps and allowing more user control of their app usage, there is a new notification setting called “Deliver Quietly.” Users can set your app to *Delivery Quietly* from the Notification Center, which means they will not receive banners or sound notifications from your app, but they will appear in the Notification Center. Apple using an in-house algorithm, which presumably tracks often you interact with notifications, will also **ask users if they still want to receive notifications from particular apps** and encourage you to turn on *Deliver Quietly* or turn them off completely. 

Notifications are getting a big refresh in iOS 12, and I've only scratched the surface. In the rest of this article, we’ll go over the rest of the new notification features coming to iOS 12 and how you can implement them in your own app. 

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/06/wwdc-2018-diary-ios-developer/">WWDC 2018 Diary Of An iOS Developer</a></em></p>

## Remote vs Local Notifications

There are two ways to send push notifications to a device: remotely or locally. To send notifications remotely, you need a server that can send JSON payloads to Apple’s Push Notification Service. Along with a payload, you also need to send the device token and any other authentication certificate or tokens that verify your server is allowed to send the push notification through Apple. For this article, we focus on local notifications which do not need a separate server. Local notifications are requested and sent through the `UNUserNotificationCenter`. We’ll go over later how specifically to make the request for a local notification. 

In order to send a notification, you first need to get permission from the user on **whether or not they want you to send them notifications**. With the release of iOS 12, there are a lot of changes to notification settings and permissions so let’s break it down. To test out any of the code yourself, make sure you have the Xcode 10 beta installed.

{{% feature-panel %}}

## Notification Settings And Permissions

### Deliver Quietly 

*Delivery Quietly* is Apple’s attempt to allow users more control over the noise they may receive from notifications. Instead of going into the settings app and looking for the app whose notification settings you want to change, you can now change the setting directly from the notification. This means that a lot more users may turn off notifications for your app or just delivery them quietly which means the app will get badged and notifications only show up in the Notification Center. If your app has its own custom notification settings, Apple is allowing you to link directly to that screen from the settings management view pictured below. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/015ae8de-f1c1-460e-82c4-303f9339246a/deliverquietly.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983fa66d-c378-48b6-a2e1-4aab6c720733/app-ios-12-notifications-deliverquietly.png" sizes="100vw" caption="Delivery quietly feature. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/015ae8de-f1c1-460e-82c4-303f9339246a/deliverquietly.png'>Large preview</a>)" alt="iPhone 8 Plus shown with Manage selected from notification which brings up the Deliver Quietly and Turn Off options." >}}

In order to link to your custom notification setting screen, you must set `providesAppNotificationSettings` as a `UNAuthorizationOption` when you are requesting notification permissions in the app delegate. 

In `didFinishLaunchingWithOptions`, add the following code:

<div class="break-out">

<pre><code class="language-javascript">UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound, .providesAppNotificationSettings]) { ... }
</code></pre></div>

When you do this, you’ll now see your custom notification settings in two places:

- If the user selects `Turn Off` when they go to manage settings directly from the notification;
- In the notification settings within the system’s Settings app. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6fba0db-8684-420c-8d3d-414aaf80ce07/turnoffnotifications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4ee20c1-ca99-419b-bfa4-4f5ebbffabf3/app-ios-12-notifications-turnoffnotifications.png" sizes="100vw" caption="Deep link to to custom notification settings for NotificationTester from notification in the Notification Center. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6fba0db-8684-420c-8d3d-414aaf80ce07/turnoffnotifications.png'>Large preview</a>)" alt="iPhone 8 Plus shown with Turn Off selected from notification which brings up the Turn Off All Notifications and Configure in NotificationTester options." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/658ab8e1-d0f1-46b2-b092-7f8ed643f4e0/systemnotificationsettings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e51038-8365-4064-ab03-feee8cc56eef/app-ios-12-notifications-systemnotificationsettings.png" sizes="100vw" caption="Deep link to custom notification settings for NotificationTester from system’s Settings app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/658ab8e1-d0f1-46b2-b092-7f8ed643f4e0/systemnotificationsettings.png'>Large preview</a>)" alt="iPhone 8 Plus shown with system Settings app open with Notifications screen for NotificationTester app." >}}

You also have to make sure to handle the callback for when the user selects on either way to get to your notification settings. Your app delegate or an extension of your app delegate has to conform to the protocol `UNUserNotificationCenterDelegate` so you can then implement the following callback method:

<div class="break-out">

<pre><code class="language-javascript">func userNotificationCenter(_ center: UNUserNotificationCenter, openSettingsFor notification: UNNotification?) {
    let navController = self.window?.rootViewController as! UINavigationController
    let notificationSettingsVC = NotificationSettingsViewController()
    navController.pushViewController(notificationSettingsVC, animated: true)
}</code></pre></div>

Another new `UNAuthorizationOption` is provisional authorization. If you don't mind your notifications being delivered quietly, you can set add `.provisional` to your authorization options as shown below. This means that you don't have to prompt the user to allow notifications &mdash; the notifications will still show up in the Notification Center. 

<div class="break-out">

<pre><code class="language-javascript">UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .provisional]) { ... }
</code></pre></div>

So now that you've determined how to request permission from the user to deliver notifications and how to navigate users to your own customized settings view, let’s go more into more detail about the actual notifications. 

## Sending Grouped Notifications

Before we get into the customization of the UI of a notification, let’s go over how to make the request for a local notification. First, you have to register any `UNNotificationCategory`, which are like templates for the notifications you want to send. Any notification set to a particular category will inherit any actions or options that were registered with that category. After you've requested permission to send notifications in `didFinishLaunchingWithOptions`, you can register your categories in the same method. 

<div class="break-out">

<pre><code class="language-javascript">let hiddenPreviewsPlaceholder = "%u new podcast episodes available"
let summaryFormat = "%u more episodes of %@"
let podcastCategory = UNNotificationCategory(identifier: "podcast", actions: [], intentIdentifiers: [], hiddenPreviewsBodyPlaceholder: hiddenPreviewsPlaceholder, categorySummaryFormat: summaryFormat, options: [])
UNUserNotificationCenter.current().setNotificationCategories([podcastCategory])
</code></pre></div>

In the above code, I start by initiating two variables: 

- `hiddenPreviewsPlaceholder`  
This placeholder is used in case the user has "Show Previews" off for your app; if we don't have a placeholder there, your notification will show with only "Notification" also the text.
- `summaryFormat`  
This string is new for iOS 12 and coincides with the new feature called “Group Notifications” that will help the Notification Center look a lot cleaner. All notifications will show up in stacks which will be either representing all notifications from the app or specific groups that the developer has set for there app.

The code below shows how we associate a notification with a group. 

<div class="break-out">

<pre><code class="language-javascript">@objc func sendPodcastNotification(for podcastName: String) {
let content = UNMutableNotificationContent()
content.body = "Introducing Season 7"
content.title = "New episode of \(podcastName):"
content.threadIdentifier = podcastName.lowercased()
content.summaryArgument = podcastName
content.categoryIdentifier = NotificationCategoryType.podcast.rawValue
sendNotification(with: content)
}
</code></pre></div>

For now, I've hardcoded the text of the notification just for the example. The `threadIdentifier` is what creates the groups that we show as stacks in the Notification Center. In this example, I want the notifications grouped by podcast so each notification you get is separated by what podcast it’s associated with. The `summaryArgument` matches back to our `categorySummaryFormat` we set in the app delegate. In this case, we want the string for the format: `"%u more episodes of %@"` to be the podcast name. Lastly, we have to set the category identifier to ensure the notification has the template we set in the app delegate. 

<div class="break-out">

<pre><code class="language-javascript">func sendNotification(for category: String, with content: UNNotificationContent) {
let uuid = UUID().uuidString
let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 5, repeats: false)
let request = UNNotificationRequest(identifier: uuid, content: content, trigger: trigger)
UNUserNotificationCenter.current().add(request, withCompletionHandler: nil)
}
</code></pre></div>

The above method is how we request the notification to be sent to the device. The identifier for the request is just a random unique string; the content is passed in and we create the content in our `sendPodcastNotification` method, and lastly, the trigger is when you want the notification to send. If you want the notification to send immediately, you can set that parameter to nil.  

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4289cd7-c8c7-4699-be0c-099dfe26963d/groupednotifications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/caa0866c-c0d0-4d65-b121-ef64a001eb3f/app-ios-12-notifications-groupednotifications.png" sizes="100vw" caption="Grouped notifications for NotificationTester. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4289cd7-c8c7-4699-be0c-099dfe26963d/groupednotifications.png'>Large preview</a>)" alt="iPhone 8 Plus lock screen shown with a grouped notification stack from Notification Tester app." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/081cfe45-005b-4c63-8a4d-fcae440b96ad/hiddenpreviewgroup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cc3d6eb-5da6-4067-b091-1071009a9670/app-ios-12-notifications-hiddenpreviewgroup.png" sizes="100vw" caption="Notification grouped with previews turned off. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/081cfe45-005b-4c63-8a4d-fcae440b96ad/hiddenpreviewgroup.png'>Large preview</a>)" alt="iPhone 8 Plus lock screen shown with a grouped notification stack from Notification Tester app that has hidden content." >}}

Using the methods we've described above, here’s the result on the simulator. I have a button that has the `sendPodcastNotification` method as a target. I tapped the button three times to have the notifications sent to the device. In the first photo, I have “Show Previews” set to “Always” so I see the podcast and the name of the new episodes along with the summary that shows I have two more new episodes to check out. When “Show Previews” is set to “Never,” the result is the second image above. The user won't see which podcast it is to respect the “No Preview” setting, but they can still see that I have three new episodes to check out. 

{{% ad-panel-leaderboard %}}

## Notification Content Extension

Now that we understand how to set our notification categories and make the request for them to be sent, we can go over how to customize the look of the notification using the Notification Service and Notification Content extensions. The Notification Service extension allows you to edit the notification content and download any attachments in your notification like images, audio or video files. The Notification Content extension contains a view controller and storyboard that allows you to customize the look of your notification as well as handle any user interaction within the view controller or taps on notification actions.

To add these extensions to your app go File&nbsp;&rarr; &nbsp;New&nbsp;&rarr; &nbsp;Target. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e944c138-1386-4050-99e1-e240d1e1cba9/template-new-target.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e944c138-1386-4050-99e1-e240d1e1cba9/template-new-target.png" sizes="100vw" caption="Adding new target to app for the Notification Content Extension. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e944c138-1386-4050-99e1-e240d1e1cba9/template-new-target.png'>Large preview</a>)" alt="Xcode shown after selecting from menu to add a new target, Notification Content Extension is highlighted." >}}

You can only add them one at a time, so name your extension and repeat the process to add the other. If a pop-up appears asking you to activate your new scheme, click the “Activate” button to set it up for debugging.

For the purpose of this tutorial, we will be focusing on the Notification Content Extension. For local notifications, we can include the attachments in the request, which we’ll go over later.

First, go to the *Info.plist* file in the Notification Content Extension target. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d26c3dca-2733-4e91-941c-b6e4f1bff676/plistfile.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d26c3dca-2733-4e91-941c-b6e4f1bff676/plistfile.png" sizes="100vw" caption="Info.plist for the Notification Content Extension. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d26c3dca-2733-4e91-941c-b6e4f1bff676/plistfile.png'>Large preview</a>)" alt="Info.plist file for Notification Content Extension shown in Xcode." >}}

The following attributes are required:

- `UNNotificationExtensionCategory`  
A string value equal to the notification category which we created and set in the app delegate. This will let the content extension know which notification you want to have custom UI for.
- `UNNotificationExtensionInitialContentSizeRatio`  
A number between 0 and 1 which determines the aspect ratio of your UI. The default value is 1 which will allow your interface to have its total height equal to its width.

I've also set `UNNotificationExtensionDefaultContentHidden` to “YES” so that the default notification does not show when the content extension is running.

You can use the storyboard to set up your view or create the UI programmatically in the view controller. For this example I've set up my storyboard with an image view which will show the podcast logo, two labels for the title and body of the notification content, and a “Like” button which will show a heart image. 

Now, in order to get the image showing for the podcast logo and the button, we need to go back to our notification request: 

<div class="break-out">

<pre><code class="language-javascript">guard let pathUrlForPodcastImg = Bundle.main.url(forResource: "startup", withExtension: "jpg") else { return }
let imgAttachment = try! UNNotificationAttachment(identifier: "image", url: pathUrlForPodcastImg, options: nil)

guard let pathUrlForButtonNormal = Bundle.main.url(forResource: "heart-outline", withExtension: "png") else { return }
let buttonNormalStateImgAtt = try! UNNotificationAttachment(identifier: "button-normal-image", url: pathUrlForButtonNormal, options: nil)

guard let pathUrlForButtonHighlighted = Bundle.main.url(forResource: "heart-filled", withExtension: "png") else { return }
let buttonHighlightStateImgAtt = try! UNNotificationAttachment(identifier: "button-highlight-image", url: pathUrlForButtonHighlighted, options: nil)

content.attachments = [imgAttachment, buttonNormalStateImgAtt, buttonHighlightStateImgAtt]
</code></pre></div>

I added a folder in my project that contains all the images we need for the notification so we can access them through the main bundle. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0cdf5dd-3c0e-4ae1-a963-23d6da6ac464/files.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0cdf5dd-3c0e-4ae1-a963-23d6da6ac464/files.png" sizes="100vw" caption="Xcode project navigator. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0cdf5dd-3c0e-4ae1-a963-23d6da6ac464/files.png'>Large preview</a>)" alt="Project navigator shown in Xcode." >}}

For each image, we get the file path and use that to create a `UNNotificationAttachment`. Added that to our notification content allows us to access the images in the Notification Content Extension in the `didReceive` method shown below. 

<div class="break-out">

<pre><code class="language-javascript">func didReceive(_ notification: UNNotification) {
self.newEpisodeLabel.text = notification.request.content.title
self.episodeNameLabel.text = notification.request.content.body

let imgAttachment = notification.request.content.attachments[0]
let buttonNormalStateAtt = notification.request.content.attachments[1]
let buttonHighlightStateAtt = notification.request.content.attachments[2]

guard let imageData = NSData(contentsOf: imgAttachment.url), let buttonNormalStateImgData = NSData(contentsOf: buttonNormalStateAtt.url), let buttonHighlightStateImgData = NSData(contentsOf: buttonHighlightStateAtt.url) else { return }

let image = UIImage(data: imageData as Data)
let buttonNormalStateImg = UIImage(data: buttonNormalStateImgData as Data)?.withRenderingMode(.alwaysOriginal)
let buttonHighlightStateImg = UIImage(data: buttonHighlightStateImgData as Data)?.withRenderingMode(.alwaysOriginal)

imageView.image = image
likeButton.setImage(buttonNormalStateImg, for: .normal)
likeButton.setImage(buttonHighlightStateImg, for: .selected)
}
</code></pre></div>

Now we can use the file path URLs we set in the request to grab the data for the URL and turn them into images. Notice that I have two different images for the different button states which will allow us to update the UI for user interaction. When I run the app and send the request, here’s what the notification looks like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bd578f0-2a67-4b47-96ce-d2091ce585dc/customizednotification.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/038aa952-9159-4d4f-af52-b007190a918f/app-ios-12-notifications-customizednotification.png" sizes="100vw" caption="Content extension loaded for NotificationTester app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bd578f0-2a67-4b47-96ce-d2091ce585dc/customizednotification.png'>Large preview</a>)" alt="iPhone 8 Plus shown with custom notification loaded after force touching the notification." >}}

Everything I've mentioned so far in relation to the content extension isn't new in iOS 12, so let’s dig into the two new features: **User Interaction** and **Dynamic Actions**. When the content extension was first added in iOS 10, there was no ability to capture user touch within a notification, but now we can register UIControl events and respond when the user interacts with a UI element.

For this example, we want to show the user that the “Like” button has been selected or unselected. We already set the images for the `.normal` and `.selected` states, so now we just need to add a target for the UIButton so we can update the selected state. 

<div class="break-out">

<pre><code class="language-javascript">override func viewDidLoad() {
super.viewDidLoad()
// Do any required interface initialization here.
likeButton.addTarget(self, action: #selector(likeButtonTapped(sender:)), for: .touchUpInside)
}</code></pre></div>

<div class="break-out">

<pre><code class="language-javascript">@objc func likeButtonTapped(sender: UIButton) {
likeButton.isSelected = !sender.isSelected
}</code></pre></div>

Now with the above code we get the following behavior:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a37400-3087-4433-a835-f3fcc9457e15/userinteraction.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0310354-e7e0-4fc8-b643-b5cef4a5c75c/userinteraction-800w.gif" width=“800" height="800" alt="GIF of iPhone 8 Plus with custom notification loaded and like button being selected and unselected." /></a><figcaption>Selecting like button within notification. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a37400-3087-4433-a835-f3fcc9457e15/userinteraction.gif">Large preview</a>)</figcaption></figure>

In the selector method `likeButtonTapped`, we could also add any logic for saving the liked state in User Defaults or the Keychain, so we have access to it in our main application. 

Notification actions have existed since iOS 10, but once you click on them, usually the user will be rerouted to the main application or the content extension is dismissed. Now in iOS 12, we can update the list of notification actions that are shown in response to which action the user selects.

First, let’s go back to our app delegate where we create our notification categories so we can add some actions to our podcast category. 

<div class="break-out">

<pre><code class="language-javascript">let playAction = UNNotificationAction(identifier: "play-action", title: "Play", options: [])
let queueAction = UNNotificationAction(identifier: "queue-action", title: "Queue Next", options: [])
let podcastCategory = UNNotificationCategory(identifier: "podcast", actions: [playAction, queueAction], intentIdentifiers: [], hiddenPreviewsBodyPlaceholder: hiddenPreviewsPlaceholder, categorySummaryFormat: summaryFormat, options: [])
</code></pre></div>

Now when we run the app and send a notification, we see the following actions shown below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf7a6884-20f0-4a22-b934-56bf2bb4d3cf/quickactions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf7a6884-20f0-4a22-b934-56bf2bb4d3cf/quickactions.png" sizes="100vw" caption="Notification quick actions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf7a6884-20f0-4a22-b934-56bf2bb4d3cf/quickactions.png'>Large preview</a>)" alt="iPhone 8 Plus with custom notification loaded with an options to Play or Add to Queue." >}}

When the user selects “Play,” we want the action to be updated to “Pause.” If they select “Queue Next,” we want that action to be updated to “Remove from Queue.” We can do this in our `didReceive` method in the Notification Content Extension’s view controller. 

<div class="break-out">

<pre><code class="language-javascript">func didReceive(_ response: UNNotificationResponse, completionHandler completion:
(UNNotificationContentExtensionResponseOption) -> Void) {
guard let currentActions = extensionContext?.notificationActions else { return }

if response.actionIdentifier == "play-action" {
let pauseAction = UNNotificationAction(identifier: "pause-action", title: "Pause", options: [])
let otherAction = currentActions[1]
let newActions = [pauseAction, otherAction]
extensionContext?.notificationActions = newActions

} else if response.actionIdentifier == "queue-action" {
let removeAction = UNNotificationAction(identifier: "remove-action", title: "Remove from Queue", options: [])
let otherAction = currentActions[0]
let newActions = [otherAction, removeAction]
extensionContext?.notificationActions = newActions

}  else if response.actionIdentifier == "pause-action" {
let playAction = UNNotificationAction(identifier: "play-action", title: "Play", options: [])
let otherAction = currentActions[1]
let newActions = [playAction, otherAction]
extensionContext?.notificationActions = newActions

} else if response.actionIdentifier == "remove-action" {
let queueAction = UNNotificationAction(identifier: "queue-action", title: "Queue Next", options: [])
let otherAction = currentActions[0]
let newActions = [otherAction, queueAction]
extensionContext?.notificationActions = newActions
}
completion(.doNotDismiss)
}</code></pre></div>

By resetting the `extensionContext?.notificationActions` list to contain the updated actions, it allows us to change the actions every time the user selects one. The behavior is shown below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e235af4-d403-4dbc-aefd-ad17da4558cc/dynamicactions.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a84f5abd-1223-47fb-978e-80486331e21b/dynamicactions-800w.gif" width=“800" height="800" alt="GIF of iPhone 8 Plus with custom notification loaded and the quick actions being changed from Play to Pause and Add to Queue to Remove from Queue." /></a><figcaption>Dynamic notification quick actions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e235af4-d403-4dbc-aefd-ad17da4558cc/dynamicactions.gif">Large preview</a>)</figcaption></figure>

## Summary

There’s a lot to do before iOS 12 launches to make sure your notifications are ready. The steps vary in complexity and you don't have to implement them all. Make sure to first download XCode 10 beta so you can try out the features we've gone over. If you want to play around with the demo app I've referenced throughout the article, check it out on [Github](https://github.com/kmt901/Notifications-iOS12).

### For Your Notification Permissions Request And Settings, You’ll Need To:

- Determine whether or not you want to enable provisional authorization and add it to your authorization options.
- If you have already have a customized notification settings view in your app, add `providesAppNotificationSettings` to your authorization options as well as implement the call back in your app delegate or whichever class conforms to `UNUserNotificationCenterDelegate`.

### For Notification Grouping:

- Add a thread identifier to your remote and local notifications so your notifications are correctly grouped in the Notification Center.
- When registering your notification categories, add the category summary parameter if you want your grouped notification to be more descriptive than “more notifications.”
- If you want to customize the summary text even more, then add a summary identifier to match whichever formatting you added for the category summary. 

### For Customized Rich Notifications:

- Add the Notification Content extension target to your app to create rich notifications.
- Design and implement the view controller to contain whichever elements you want in your notification.
- Consider which interactive elements would be useful to you, i.e. buttons, table view, switches, etc. 
- Update the `didReceive` method in the view controller to respond to selected actions and update the list of actions if necessary.

## Further Reading

- “[Notifications](https://developer.apple.com/notifications/),” Apple’s list of various documentation regarding user notifications
- “[What’s New in User Notifications](https://developer.apple.com/videos/play/wwdc2018/710),” WWDC 2018 Apple
- “[Customizing the Appearance of Notifications](https://developer.apple.com/documentation/usernotificationsui/customizing_the_appearance_of_notifications),” Apple’s documentation on the Notification Content Extension

{{< signature "ra, yk, il" >}}
