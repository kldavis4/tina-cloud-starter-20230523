---
title: Putting Mobile Back End As A Service Into Practice (Part 1)
slug: mobile-backend-service-practice-part1
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba61909-67fd-4022-b267-9a7adaedbf45/01-watercooler-demo-app-opt-small.jpg
date: 2015-03-30T20:53:19.000Z
author: davidtucker
description: >-
  In a [previous
  article](https://www.smashingmagazine.com/2014/12/15/understanding-mobile-back-end-as-a-service/)
  I introduced mobile back end as a service (MBaaS) which aims at giving app
  developers the ability to create seamlessly new feature-complete
  cross-platform native and web applications.

  The next step is implementing a complete demo application using those ideas.
  Through this real working application, you will be able to see **the areas in
  which MBaaS provides value**. This first part will walk you through a
  messaging application demo powered by the Kinvey application and explore how
  to leverage user management, file storage and the data store.
categories:
  - Mobile
  - Techniques
  - Apps
  - Web Development
  - Swift
---
In a <a href="https://www.smashingmagazine.com/2014/12/15/understanding-mobile-back-end-as-a-service/">previous article</a> I introduced mobile back end as a service (MBaaS) which aims at giving app developers the ability to create seamlessly new feature-complete cross-platform native and web applications.

The next step is implementing a complete demo application using those ideas. Through this real working application, you will be able to see the areas in which MBaaS provides value. This first part will walk you through a messaging application demo powered by the Kinvey application and explore how to leverage user management, file storage and the data store.</p>

## <span class="rh">Further Reading</span> on SmashingMag

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)

The second part will complete the demo and demonstrate how to leverage two key pieces of Kinvey functionality: the permissions provided by the data store, and push notifications, which are enabled through the business logic functionality.

{{% feature-panel %}}

## Setting Up

Before jumping into the demo application, I want to highlight a few points. First, because I am using a real app to discuss MBaaS, knowledge of the development platform would be extremely helpful. I am leveraging iOS with Swift. In addition, knowing how to integrate with back-end services would certainly be helpful, in order to understand more about what Kinvey is doing under the hood. While all of this is helpful, the application’s full source is included; feel free to analyze the code at your own pace.

Secondly, because the demo application has more of an enterprise focus (as opposed to a consumer focus), I chose <a href="https://www.kinvey.com/">Kinvey</a> for the MBaaS platform. In the <a href="https://www.smashingmagazine.com/2014/12/15/understanding-mobile-back-end-as-a-service/">last article</a> I walked through the process of evaluating MBaaS providers. Note that Kinvey is not a free service, and licensing terms are attached to its SDKs (as one would expect). Licensing terms are included with each SDK download. You can get more information at the following links:

*   [Kinvey pricing for individuals and startups](https://www.kinvey.com/pricing-starter)
*   [Kinvey pricing for businesses](https://www.kinvey.com/pricing)

## A Demo Application

In the past three years, several clients have approached me about developing an internal messaging platform for their organization. This need has led to the success of such companies as <a href="https://slack.com/">Slack</a> (which we use internally at <a href="https://www.universalmind.com/">Universal Mind</a>) and others like it. Because this was a common request, I wanted to see what it would take to implement a basic one-to-one messaging solution for an organization over top of an MBaaS solution.

To help you understand these concepts in a real application, I have provided the application’s entire source code. You can check it out on Github, “<a href="https://github.com/davidtucker/WaterCooler-Demo">WaterCooler Demo</a>.”

Note: For more information on how to choose between the available MBaaS options, please see the initial article in this series, “<a href="https://www.smashingmagazine.com/2014/12/15/understanding-mobile-back-end-as-a-service/">Understanding Mobile Back End as a Service</a>.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddfb66e9-607d-4031-ae80-2f435be7691b/01-watercooler-demo-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba61909-67fd-4022-b267-9a7adaedbf45/01-watercooler-demo-app-opt-small.jpg" alt="Screenshots of WaterCooler app" /></a><figcaption>WaterCooler demo messaging app. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddfb66e9-607d-4031-ae80-2f435be7691b/01-watercooler-demo-app-opt.jpg">View large version</a>)</figcaption></figure>

### Summary of Requirements

To illustrate how an MBaaS solution can power an app like this one, we need to meet a few key requirements. Users should be able to do the following with the app:

*   create an account and set up their profile (including name, title, profile picture, email address and password);
*   log in (and be required to log in only once — at least until they log out);
*   exchange one-to-one messages with other members (visible only to the sender and recipient and inaccessible to other users);
*   browse a directory of members who currently have an account on the platform;
*   log out;
*   manage and update their profile information;
*   be alerted through a push notification that they’ve received a new message.

The following sections detail how I used Kinvey to meet these requirements. While I won't go into detail on how every part of the application was created, I will give full context of the areas where Kinvey was leveraged.</p>

### Technical Details

The demo application is an iOS app targeting iOS 8+. It utilizes Swift (Xcode 6.1.1 and iOS 8.1.3).

The user interface was created following standard UI principles for iOS. It leverages <a href="https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/Introduction/Introduction.html">Auto Layout</a> (both within the storyboard and programmatically). The creation of this interface is beyond the scope of the article, but hopefully the example code will be helpful for your iOS applications.</p>

## Getting Started With Kinvey

If you’re following along, you’ll probably want to build the source code and run the application yourself. To do this, you will need both to create a Kinvey app and to include the credentials for the app in your code.</p>

### Creating a Kinvey App and Environment

To create a Kinvey app and environment, you will need to <a href="https://www.kinvey.com/">create a Kinvey account</a>. After signing up, select “Get Started with Your First App.” From this page, give your app a name, select iOS and the platform, and then click “Create App.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1547052b-1080-4169-b358-c2486da439a3/02-new-app-kinvey-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a785bf9b-0b4f-4489-a558-fe99d9614bc9/02-new-app-kinvey-opt-small.jpg" alt="Screenshot of creating an app in Kinvey" /></a><figcaption>A view of the process of creating an app in Kinvey. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1547052b-1080-4169-b358-c2486da439a3/02-new-app-kinvey-opt.jpg">View large version</a>)</figcaption></figure>

From here, you will have an app created with a single development environment. Clicking on the “Development” environment will take you to the console. In the console, you will see both your <code>appKey</code> and <code>appSecret</code> in the top right. Copy these pieces of information because you'll need to include them in the iOS app.</p>

### Configuring the iOS Application

Once you have created your Kinvey app and gathered your credentials, grab the code from the repository. Next, open the <code>AppDelegate.swift</code> file and update these values in the <code>application:DidFinishLaunchingWithOptions:</code> method.</p>

<pre><code class="language-clike">// Extracted from AppDelegate.swift (https://tuck.cc/1w7wkyI)

func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -&gt; Bool {

 // --------------------------------------------------------------------
 // INCLUDE YOUR KINVEY CREDENTIALS HERE
 // --------------------------------------------------------------------
 let appKey = ""
 let appSecret = ""

 //---------------------------------------------------------------------
 …
}</code></pre>

Once this is in place, you should be able to run the application as expected. If you want to run the application on a device, you will have to update the code signing as provisioning profiles (as with any iOS application).

*   For more information on setting up an iOS application with Kinvey, check out the “[Getting Started](https://devcenter.kinvey.com/ios/guides/getting-started)” tutorial.

## User Management

One foundational element of any MBaaS is user management. This application will leverage user management to control individual user accounts and their respective profile information, as well as provide a directory of all users in the system. Just as with the rest of the functionality we will cover, this integration is provided through Kinvey’s <a href="https://devcenter.kinvey.com/ios/guides/getting-started">iOS SDK</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1dacb8-080c-413c-99b6-2d0308d4056c/03-user-management-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1ceb20d-efb5-4729-978d-77b661c61972/03-user-management-opt-small.jpg" alt="Sign-up, log-in and profile views" /></a><figcaption>A view of the sign-up, log-in and profile views in the application. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1dacb8-080c-413c-99b6-2d0308d4056c/03-user-management-opt.jpg">View large version</a>)</figcaption></figure>

### Creating a User

The first step in the process is to enable a user to create an account. When a user launches the application, they will land on the view that allows them to either log in or sign up. If the user selects “Sign Up,” they will be taken to the “Sign Up” page, which will guide them through the process of entering their profile information. When this process is complete, the code below is executed, which creates an account and logs the user into the application.

In this example, you will see the <code>KCSUser</code> class. This class handles the representation of a user and is also the gateway for all operations related to user management:

<pre><code class="language-clike">// Extracted from SignupViewController.swift (https://tuck.cc/1vsaWcr)

// Set the parameters of the user
var userParams = [
 KCSUserAttributeGivenname : firstNameField.text,
 KCSUserAttributeSurname : lastNameField.text,
 KCSUserAttributeEmail : emailField.text,
 kWaterCoolerUserTitleValue : titleField.text
];

// Save the user to Kinvey
KCSUser.userWithUsername(emailField.text, password: passwordField.text, fieldsAndValues: userParams) { (user:KCSUser!, error:NSError!, result:KCSUserActionResult) in
 if(error != nil) {
 println("USER NOT CREATED - ERROR: " + error.description)
 } else {
 // User created successfully
 // Do other tasks, such as uploading profile picture to the file store
 }
}</code></pre>

In this case, the fields for first name, last name and email address are include in the <code>KCSUser</code> object. However, Kinvey allows us to save other pieces of data in this object as well. The user's title will be saved in one of these additional fields. An extension to the <code>KCSUser</code> object is also included (as seen below) to make it easier to access this value for a user within the application:

<pre><code class="language-clike">// Extracted from KinveyExtensions.swift (https://tuck.cc/1vsb5N7)

// Create a constant for accessing the title key from the user object
let kWaterCoolerUserTitleValue = "title"

extension KCSUser {
 var title:String {
 return self.getValueForAttribute(kWaterCoolerUserTitleValue) as String!
 }
}</code></pre>

### Logging In

If the user selects the option to log in from the landing page, they will be able to enter their email address and password (which they entered in the sign-up process). They are presented with an alert if their attempt is unsuccessful, and if they log in correctly, they are redirected to the main view of the application.</p>

<pre><code class="language-clike">// Extracted from LandingPageViewController.swift (https://tuck.cc/1vsbeAe)

func attemptLogin() {
 // Get the values from the form
 let username = loginEmailField.text
 let password = loginPasswordField.text

 // Attempt to log in to the application
 KCSUser.loginWithUsername(username, password: password) { (user, error, actionResult) -&gt; Void in
 if(error == nil) {
 self.successfulLogin()
 } else {
 self.incorrectLoginWithError(error)
 }
 }
}

func incorrectLoginWithError(error:NSError) {
 // Let the user know an error occurred in login. In this case
 // we just present an alert using the UIAlertController.
 let alert = UIAlertController(title: "Failed Login", message: error.localizedDescription, preferredStyle: UIAlertControllerStyle.Alert)
 alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.Cancel, handler: { (alertAction) -&gt; Void in
 self.dismissViewControllerAnimated(true, completion:nil)
 }))

 // Present the alert
 presentViewController(alert, animated: true, completion: nil)
}

func successfulLogin() {
 // There is already a segue defined to the main threads view.
 // We need to perform this segue if we have a successful login.
 performSegueWithIdentifier(WaterCoolerConstants.Segue.Login, sender: self)
}</code></pre>

### Logging Out

From the profile management page, the user can log out of the application. Upon doing this, Kinvey’s iOS SDK also does some additional work in the background, including clearing out any cached values. In this example, after logging out, the user is redirected back to the landing page.</p>

<pre><code class="language-clike">// Perform the log-out and send the user to landing page
@IBAction func logout() {
 KCSUser.activeUser().logout()
 performSegueWithIdentifier(WaterCoolerConstants.Segue.Logout, sender: self)
}</code></pre>

### User Directory

To fulfill all of our requirements, the application also needs to provide a list of all users. A special collection, <code>KCSCollection.userCollection()</code>, provides access to the collection of users for an application. Once you have created a store from this collection, you can query it as you would any other data collection. The following example illustrates how to fetch all users for the application:

<pre><code class="language-clike">// Extracted from KinveyDataManager.swift (https://tuck.cc/1vsd0Bp)

// Create the app data store corresponding to the users collection
lazy var userStore:KCSAppdataStore = {
 let userCollection:KCSCollection = KCSCollection.userCollection()
 let store = KCSAppdataStore(collection: userCollection, options: nil)
 return store
}()

// Fetch the users from the user store
func fetchUsers(completion: ([KCSUser]!, NSError!) -&gt; ()) {
 userStore.queryWithQuery(KCSQuery(), withCompletionBlock: { (results, error) -&gt; Void in
 if(error == nil) {
 self.users = results as [KCSUser]
 completion(results as [KCSUser]!, nil)
 } else {
 completion(nil, error)
 }
 }, withProgressBlock: nil)
}</code></pre>

Note: For more information on managing users with Kinvey’s iOS SDK, be sure to check out the “<a href="https://devcenter.kinvey.com/ios/guides/users">Users</a>” guide.</p>

## File Management

One powerful feature of many MBaaS solutions is file storage. In our WaterCooler application, this comes into play when a user creates an account and adds a profile picture. We could also leverage this heavily to extend the app to support the uploading of images within messages. In this process, the file is uploaded to a content delivery network (CDN) and, like any other piece of data, has a full configuration of permissions.</p>

<pre><code class="language-clike">// Extracted from SignupViewController.swift (https://tuck.cc/1vsaWcr)

// Upload the profile picture to the Kinvey file store
func uploadProfilePicture(completion:(file:KCSFile!) -&gt; ()) {
 if((self.photo.image) != nil) {
 let photoData = UIImageJPEGRepresentation(self.photo.image, 1.0)

 KCSFileStore.uploadData(photoData, options: fileParams, completionBlock: { (file:KCSFile!, error:NSError!) -&gt; Void in
 completion(file: file);
 }, progressBlock: nil);

 } else {
 completion(file: nil);
 }
}

// Once we have completed the file upload, assign the file ID to the user
// using a custom attribute
func assignProfilePictureIdToUser(user:KCSUser, picture:KCSFile, completion: () -&gt; Void) {
 user.setValue(picture.kinveyObjectId(), forAttribute: kWaterCoolerUserProfilePicFileId);
 user.saveWithCompletionBlock { (user:[AnyObject]!, error:NSError!) -&gt; Void in
 completion();
 }
}</code></pre>

In the code above, two distinct steps are occurring. First, we are uploading the profile picture to the file store. Once this process is completed, we are updating the user with the ID that the file store has returned. In this manner, we are leveraging yet another custom property on the user to store an identifying piece of information. Now, anywhere we display a list of users, we can also display their profile picture.

Note: For more information on working with files in Kinvey’s iOS SDK, see the “<a href="https://devcenter.kinvey.com/ios/guides/files">Files</a>” guide.</p>

## Data Model

One of the benefits of Kinvey’s iOS SDK is that it allows you to map your Swift (or Objective-C) objects to Kinvey collection objects. The <code>KCSUser</code> class is a special class that is already defined and mapped to the user object, but in our case we will create two additional data classes that map to conversations and the messages within them.</p>

### WaterCooler Data Model

The WaterCooler data model will have two main entities, <code>Message</code> and <code>MessageThread</code>.

The <code>MessageThread</code> class will be responsible for representing a conversation between two users. It will contain information about the users involved in the conversation, as well as a reference to the last message sent in the conversation.

Within Kinvey, the <code>entityId</code> is a special field. If you do not assign a value to it, the system will assign one when the object is saved to the data store. In our case, we will go ahead and define a special value that maps to the two users who are in a conversation for the <code>MessageThread</code> class. The method that calculates this value can be seen below:

<pre><code class="language-clike">// Extracted from MessageThread.swift (https://tuck.cc/1w7jdOd)

// This method simply takes a user and the current user and creates
// an ID based on the alphabetized array of user IDs between these
// two users. In this way, we don't have to fetch additional information
// when displaying the message thread view.
class func threadIdentifierForUser(user:KCSUser) -&gt; String {
 let userAIdentifier:String = KCSUser.activeUser().userId
 let userBIdentifier:String = user.userId
 let identifiers:[String] = [ userAIdentifier, userBIdentifier ]
 let sortedIdentifiers = identifiers.sorted {
 $0.localizedCaseInsensitiveCompare($1) == NSComparisonResult.OrderedAscending
 }
 return ":".join(sortedIdentifiers)
}</code></pre>

The <code>Message</code> class will be responsible for tracking an individual message within an overall conversation. This class contains information about the message, including its time, contents, sender and related message thread. To get all of the messages for a particular conversation, we simply query based on the <code>threadId</code> of the conversation. The following code fetches all of the messages for a predefined message thread:

<pre><code class="language-clike">// Extracted from KinveyDataManager.swift (https://tuck.cc/1vsd0Bp)

func messagesForThread(thread:MessageThread, completion:([Message]) -&gt; ()) {
 let query = KCSQuery(onField: "threadId", withExactMatchForValue: thread.entityId)
 messagesStore.queryWithQuery(query, withCompletionBlock: { (results, error) -&gt; Void in
 completion(results as [Message])
 }, withProgressBlock: nil)
}</code></pre>

### Data Model Relationships

Kinvey supports data model relationships within both the core data store as well as the iOS SDK. In our situation, the <code>lastMessage</code> property on the <code>MessageThread</code> class is one such instance. When we fetch a thread, it looks at specific methods in our class to determine how it should handle references to other collection objects. In our case, the following methods allow it to treat this reference as a <code>Message</code> instance:

<pre><code class="language-clike">// Extracted from MessageThread.swift (https://tuck.cc/1w7jdOd)

// This method tells Kinvey to save the message in the lastMessage property
// when the thread is saved. If this method were not included, the message
// itself would not be saved when the thread is saved.
override func referenceKinveyPropertiesOfObjectsToSave() -&gt; [AnyObject]! {
 return [
 "lastMessage"
 ]
}

// This maps the properties in the class to specific values in the Kinvey
// data store.
override func hostToKinveyPropertyMapping() -&gt; [NSObject : AnyObject]! {
 return [
 "entityId" : KCSEntityKeyId,
 "lastMessage" : "lastMessage",
 "metadata" : KCSEntityKeyMetadata
 ]
}

// This method tells Kinvey that the lastMessage property is a member of
// the Messages collection. (You need to put the name of the Kinvey collection
// here and not the name of the class.)
override class func kinveyPropertyToCollectionMapping() -&gt; [NSObject : AnyObject]! {
 return [
 "lastMessage" : "Messages"
 ]
}

// Here you tell Kinvey which class to map the lastMessage property to. This
// is how it knows how to build the object when it fetches it from the server.
override class func kinveyObjectBuilderOptions() -&gt; [NSObject : AnyObject]! {
 let referenceMap:[NSObject : AnyObject] = [
 "lastMessage" : Message.self
 ]
 return [
 KCS_REFERENCE_MAP_KEY : referenceMap
 ]
}</code></pre>

### Data Model Classes in Swift

For data model classes to work properly in Swift, they need to be able to leverage the default initializer. This means you need to have a default value for each property within the class. You can still leverage convenience initializers, as we have done here with the <code>Message</code> class:

<pre><code class="language-clike">// Extracted from Message.swift (https://tuck.cc/1w7kkgB)

// This initializer creates a Message instance based on the message text
// and the recipient ID. This is the initializer that is used when a
// user creates a new message in a conversation.
init(messageText:String, recipientId:String) {
 senderId = KCSUser.activeUser().userId
 self.messageText = messageText
 entityId = NSUUID().UUIDString
 metadata = KCSMetadata(userIds: [recipientId], includeActiveUser:true)
}</code></pre>

Note: For more information on the data store and data modeling in Kinvey, see the “<a href="https://devcenter.kinvey.com/ios/guides/datastore">Data Store</a>” guide.</p>

## Conclusion

Through this process, we have completed the core of Kinvey interactions for the application. However, with all of this in place, two key requirements still have not been met: data permissions and push notifications. In the next article, we will explore the permissions model in Kinvey, as well as the business logic functionality provided by the platform.

{{< signature "da, al, ml" >}}

