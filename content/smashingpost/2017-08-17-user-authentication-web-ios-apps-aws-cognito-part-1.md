---
title: User Authentication For Web And iOS Apps With AWS Cognito (Part 1)
slug: user-authentication-web-ios-apps-aws-cognito-part-1
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c2110c0-7c2e-43a4-a9b2-40e63fc6158b/cognito-diagram-500w-opt.png
date: 2017-08-17T20:29:28.000Z
author: davidtucker
description: >-
  Developers and organizations alike are looking for a way to have more agility
  with mobile solutions. There is a desire to decrease the time from idea to
  test. As a developer, I often run up against one hurdle that can slow down the
  initial build of a mobile hypothesis: user management.
categories:
  - Coding
  - Mobile
  - Tools
  - Workflow
  - Authentication
  - Security
  - iOS
---
Over the years, I have built at least three user management systems from scratch. Much of the approach can be based on a boilerplate, but there are always a few key items that need to be customized for a particular client. This is enough of a concern that an entire category of user management, authentication and authorization services have sprung up to meet this need. Services like [Auth0](https://auth0.com/) have entire solutions based on user and identity management that developers can integrate with.

One service that provides this functionality is Amazon Web Services’ (AWS’) Cognito. Cognito is a tool for **enabling users to sign up for and sign into web and mobile applications** that you create. In addition to this functionality, it also allows for storage of user data offline, and it provides synchronization of this data. As Amazon states, “With Amazon Cognito, you can focus on creating great app experiences instead of worrying about building, securing, and scaling a solution to handle user management, authentication, and sync across devices.”

<div class="c-felix-the-cat">
<h4 class="h3">Underestimating Carousels</h4>
<p>Carousels don't really deserve the bad reputation they’ve gained throughout the years. They can prove to be very effective and come in many shapes and sizes. <a href="https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/" class="btn btn--medium btn--blue">Read a related article&nbsp;→</a></p>
</div>

Last year, Amazon introduced an addition to its Cognito service, custom user pools. This functionality now provides what I and other developers need in order to have a complete, customizable, cross-platform user management system, with the flexibility needed to fit most use cases. To understand why, we need to **take a quick look at what user management is** and what problems it solves.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa381ff1-94e6-4740-bbef-686e2b9087fb/cognito-diagram-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a515b3f-ff35-408a-9e93-7d2a1d47452b/cognito-diagram-800w-opt.jpg" width="800" height="527" alt="AWS Cognito" /></a><figcaption>Cognito custom user pool diagram (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa381ff1-94e6-4740-bbef-686e2b9087fb/cognito-diagram-large-opt.jpg">View large version</a>)</figcaption></figure>

In this article, we will spend a majority of our time walking through the process of configuring a user pool for our needs. Then, we will integrate this user pool with an iOS application and allow a user to log in and fetch the attributes associated with their user account. By the end, we'll have a limited demo application, but one that handles the core of user management. In addition, after this is in place, there will be a follow-up article that takes this quite a bit deeper.</p>

## What Do We Need From User Management?

If you have a mobile or web app, what exactly do you need in terms of user management? While user log-in is probably the first thing you would think of, we cannot stop there. If we want a flexible user management system that would work for most web and mobile app use cases, it would need to have the following functionality:

*   username and password log-in;
*   secure password hashing and storage;
*   password changes;
*   password policy and validation;
*   user lifecycle triggers (welcome email, goodbye email, etc.);
*   user attributes (first name, last name, etc.);
*   required configuration and optional attributes per user;
*   handling of forgotten passwords;
*   phone number validation through SMS;
*   email verification;
*   API access to endpoints based on permissions;
*   secure storage of access token(s) on mobile devices;
*   offline storage of user attributes for mobile devices;
*   synchronization of user attributes for online and offline states;
*   multi-factor authentication.

While user management might at first seem like a log-in system, the functionality must go far beyond that in order for the system to be truly flexible enough to handle most use cases. This clearly goes far beyond just a username and password.

One additional item needs to be called out here: security. One of the requirements of any user management system is that it needs to be continually evaluated for the security of the system as a whole. Many custom user management systems have vulnerabilities that simply haven’t been corrected. Within the last year, there have been security breaches of user management systems of companies such as Dropbox, Dailymotion, Twitter and Yahoo. If you choose to build a custom solution, you are on the hook for securing your system.</p>

## Enter Amazon Cognito

Amazon Cognito is a managed service that enables you to integrate a flexible and scalable user management system into your web and mobile applications. Cognito provides two distinct ways to utilize the service: federated identities, which allow for log-in via social networks such as Facebook, and user pools, which give you completely custom user management capabilities for a specific app or suite of applications.

Federated identities are great if you want users to be able to log in with Facebook (or Google, Amazon, etc.), but this means that a portion of the user management process will have been outsourced to Facebook. While this might be acceptable in some cases, users might not want to connect their Facebook account to your application. In addition, you might want to manage more of the user's lifecycle directly, and for this, federated identities aren't as flexible. For the purpose of today’s article, we will focus on user pools because they provide the flexibility needed for a robust user management platform that would fit most any use case. In this manner, you will have an approach that can be used in most any project.

Because this is an AWS service, there are other benefits of using Cognito. Cognito can integrate with API Gateway to provide a painless way to authorize API access based on the tokens that are returned from a Cognito log-in. In addition, if you are already leveraging other AWS services for your mobile application, you can use your user pool as an identity provider for your AWS credentials.

As with any other AWS service, there is a cost involved. Pricing for Cognito is based on monthly active users (MAUs). The great news for most developers is that there is an indefinite free tier that is capped at 50,000 MAUs when using a custom user pool. If you have a large application, this will give you a large number of users to pilot a new approach to user management. However, I suspect that many of you have experiences that will never go beyond 50,000 users. In this case, core user management will be pretty much free. The only exception to this is other AWS services that you will be leveraging as part of the user management process, such as Lambda, SNS and S3.</p>

## Creating A User Pool

The first step in integrating a user pool into your mobile application is to create a Cognito user pool. This will give us the configuration values needed to plug into our example application. To create a new user pool, walk through the wizard provided in [Amazon’s Cognito console](https://console.aws.amazon.com/cognito/home).

Let’s walk through the process of creating a user pool. I must warn you that this is a lengthy process. In many ways, this is a good thing because it shows areas of flexibility. However, you'll want to grab a cup of coffee and buckle in for this one.

### 1. Name

The initial step in creating a user pool involves setting a name for your user pool and selecting the approach you will be taking to create the user pool. You can either review the defaults or “step through” the settings. Because we want to have a good working knowledge of how the user pool is being configured, choose the option “Step through settings.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65d35e8b-2a36-42cc-9515-5f2242f73635/userpool-step1-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fe52ff1-4a22-468d-b78f-ccf5bb568200/userpool-step1-800w-opt.jpg" width="800" height="422" alt="Step 1 in User Pool Creation" /></a><figcaption>The initial step in creating a user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65d35e8b-2a36-42cc-9515-5f2242f73635/userpool-step1-large-opt.jpg">View large version</a>)</figcaption></figure>

### 2. Attributes

Configuring attributes will require a bit of thought. For each user pool, you will need to determine which attributes will be stored in the system and which ones are required. Because the system will enforce required values, you cannot change this down the road. The best approach here is to mark only truly essential values here as required. In addition, if you want users to be able to log in with their email address, be sure to mark that one as an alias.

If you want to include custom values, you will need to do that here as well. Each custom value will have a type, optional validation rules, and an option to be mutable (changeable) or non-mutable (unchangeable). There is a hard limit of 25 custom attributes.

Finally, a point needs to be made here about usernames. The username value for each user is immutable (unchangeable). This means that, in most cases, making this value automatically generated would make sense. This is why the “preferred username” value exists. If you want to users to have a username value that they can edit, just mark the “preferred username” attribute as an alias. If you want users simply to log in with their email address, be sure to mark the “email” attribute as both required and an alias.

For our demo application, I chose to make “email,” “given name” and “family name” required.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13372b00-42ed-46dc-aed8-9fb409450c4d/userpool-step2-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cbbfbbe-0564-4b42-8daf-4438e113c89f/userpool-step2-800w-opt.jpg" width="800" height="443" alt="Step 2 in User Pool Creation" /></a><figcaption>Configuring user attributes for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13372b00-42ed-46dc-aed8-9fb409450c4d/userpool-step2-large-opt.jpg">View large version</a>)</figcaption></figure>

### 3. Policies

After configuring the attributes, you will be able to configure the policies for the account. The first policy to configure is the password policy. The policy allows you to configure both the length and whether you require numbers, special characters, uppercase letters or lowercase letters. This policy will be enforced on both passwords that users enter as well as passwords that administrators assign to users.

The next policies relate to user sign-up. For a public application, you will likely want to allow users to sign up themselves. However, depending on the type of application, you might want to restrict sign-up and have the system be invitation-only. In addition, you will have to configure how quickly these invitations will expire if they are not used.

For our demo application, I chose to use just the default values, with the exception that I don’t want users to be able to sign up on their own. With these values in place, we can proceed to verifications.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa41cbb-4e0a-450a-bf4a-0664121936b8/userpool-step3-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11148a63-9e73-418d-b435-fe5296c2624c/userpool-step3-800w-opt.jpg" width="800" height="423" alt="Step 3 in User Pool Creation" /></a><figcaption>Configuring policies for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa41cbb-4e0a-450a-bf4a-0664121936b8/userpool-step3-large-opt.jpg">View large version</a>)</figcaption></figure>

### 4. Verifications

The verifications step allows you to set up multi-factor authentication, as well as email and phone verification. While this functionality is relatively easy to set up in the console, note that you will need to [request a spending increase](https://docs.aws.amazon.com/cognito/latest/developerguide/user-pool-settings-email-phone-verification.html) for AWS SNS if you want to either verify phone numbers or use multi-factor authentication.

For our demo application, I chose to use just the default values.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa9055f6-0394-452c-ab25-c7bf1620ff6d/userpool-step4-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad93adb8-0d8c-465a-bbdf-a415d376c37a/userpool-step4-800w-opt.jpg" width="800" height="425" alt="Step 4 in User Pool Creation" /></a><figcaption>Configuring verifications for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa9055f6-0394-452c-ab25-c7bf1620ff6d/userpool-step4-large-opt.jpg">View large version</a>)</figcaption></figure>

### 5. Message Customizations

This step allows you to customize the email and SMS messages that your user pool will send, as well as the “from” and “reply to” email addresses. For the purpose of our demo application, I will leave the default values here and proceed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278675a2-bcec-4066-9685-6e0272c5a827/userpool-step5-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d377c4-0808-4295-a9cc-5cbcf3a1c6f6/userpool-step5-800w-opt.jpg" width="800" height="426" alt="Step 5 in User Pool Creation" /></a><figcaption>Configuring the lifecycle messages for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278675a2-bcec-4066-9685-6e0272c5a827/userpool-step5-large-opt.jpg">View large version</a>)</figcaption></figure>

### 6. Tags

If you are new to AWS, you might not need to specify any tags. However, in case your organization uses AWS regularly, tags provide a way to analyze spending and assign permissions with IAM. For example, some organizations specify tags per environment (development, staging, production) and by project.

No matter what you enter in this step, it won’t affect our demo application.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1c101a2-37e7-4ef1-b50a-7203bb050b95/userpool-step6-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad4a168d-eff9-4642-83e9-6177f931cf05/userpool-step6-800w-opt.jpg" width="800" height="422" alt="Step 6 in User Pool Creation" /></a><figcaption>Adding tags for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1c101a2-37e7-4ef1-b50a-7203bb050b95/userpool-step6-large-opt.jpg">View large version</a>)</figcaption></figure>

### 7. Devices

The next step allows you to define whether the user pool will remember your user’s devices. This is an additional security step that allows you to see what devices a specific account has been logged into with. This has an extra value when you are leveraging multi-factor authentication (MFA). If the device is remembered, you can elect not to require an MFA token upon each log-in.

For the purpose of the demo application, I have chosen to set the value to “Always.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85e1aff0-aa59-46c4-9717-1debfb24d551/userpool-step7-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff72be7-ee83-4575-89be-f859487838e1/userpool-step7-800w-opt.jpg" width="800" height="422" alt="Step 7 in User Pool Creation" /></a><figcaption>Configuring device handling for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85e1aff0-aa59-46c4-9717-1debfb24d551/userpool-step7-large-opt.jpg">View large version</a>)</figcaption></figure>

### 8. App Clients

For each application for which you want to use the user pool (such as an iOS application, web application, Android application, etc.), you should create an app. However, you can come back and create these after the user pool has been created, so there is no pressing need to add all of these just yet.

Each application has several values that you can configure. For this demo application, we will give the app a name and then leave the default values. Next, you can configure which user attributes each app can read and write.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae1a298a-72a9-422e-a245-bf15ba8c3fce/userpool-step8-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4943b0f-bc68-457f-b85e-4c6b2c5a9ac4/userpool-step8-800w-opt.jpg" width="800" height="421" alt="Step 8 in User Pool Creation" /></a><figcaption>Configuring client applications for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae1a298a-72a9-422e-a245-bf15ba8c3fce/userpool-step8-large-opt.jpg">View large version</a>)</figcaption></figure>

You can set whichever values you like in this step, as long as the email address, family name and given name are all readable and writable by the application. Be sure to click the option to “Create App Client” before proceeding.</p>

### 9. Triggers

With triggers, you can use Lambda functions to completely customize the user lifecycle process. For example, if you only want users with an email address from your company’s domain to be able to sign up, you could add a Lambda function for the “Pre sign-up” trigger to perform this validation and reject any sign-up request that doesn’t pass.

For our demo application, I will not add any triggers.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b69792-982e-496f-b472-22e5b8b154df/userpool-step9-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dd83a10-6fac-400e-9f88-f7ea26dcf2b0/userpool-step9-800w-opt.jpg" width="800" height="426" alt="Step 9 in User Pool Creation" /></a><figcaption>Configuring triggers for the user pool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b69792-982e-496f-b472-22e5b8b154df/userpool-step9-large-opt.jpg">View large version</a>)</figcaption></figure>

### 10. Review

I realize that this might have seemed like a lengthy and arduous process. But bear in mind that each step in creating a user pool has flexibility that allows for the solution to fit more use cases. And now for the news you've been waiting to hear: This is the last step.

Just review the settings to make sure you have configured them correctly for the demo application. From this screen, you can go back and edit any of the previous settings. Once the user pool is created, some configuration values (such as required attributes) cannot be changed.

With your new user pool created, you can now proceed to integrate them in a sample iOS application using the AWS SDK for iOS.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937f7233-d46d-4f0c-bff7-770fa8f86884/userpool-step10-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe56cc49-3845-4059-9c76-19c8ec4f33b7/userpool-step10-800w-opt.jpg" width="800" height="425" alt="Step 10 in User Pool Creation" /></a><figcaption>Final review of the user pool before creation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937f7233-d46d-4f0c-bff7-770fa8f86884/userpool-step10-large-opt.jpg">View large version</a>)</figcaption></figure>

## Setting Up Your iOS Application For Your User Pool

I have created a sample iOS application that integrates with Cognito to allow the user to log in, log out, enter their first and last name, and set a password. For this initial demo, user sign-up is not included, so I’ve used Cognito’s console to add a new user for testing.

The code for this application can be found in [my GitHub repository](https://github.com/davidtucker/CognitoSampleApplication/tree/article1).</p>

### Configuring Dependencies

This application uses [CocoaPods](https://cocoapods.org/) for managing dependencies. At this point, the only dependencies are the specific pieces of the AWS iOS SDK that relate to Cognito user pools.

(A full description of CocoaPods is beyond the scope of this article, however, a [resource](https://cocoapods.org) on CocoaPods’ website will help you get up and running, in case this concept is new to you.)

The contents of the Podfile for this application can be seen below:

<pre><code class="language-bash">source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '10.0'
use_frameworks!

target 'CognitoApplication' do
    pod 'AWSCore', '~&gt; 2.5.5'
    pod 'AWSCognitoIdentityProvider', '~&gt; 2.5.5'
end
</code></pre>

Assuming that CocoaPods is installed on your machine, you can just run `pod install`, and the necessary dependencies will be installed for you.</p>

### User Pool Configuration

The next step is to include the values for your user pool and client application. The demo application is configured to use a file, `CognitoApplication/CognitoConfig.plist`, from which to pull this information. Four values need to be defined:

*   `region` (string)  
    This is the region in which you created your user pool. This needs to be the standard region identifier, such as `us-east-1` or `ap-southeast-1`.
*   `poolId` (string)  
    This is the ID of the user pool that you created.
*   `clientId` (string)  
    This is the `clientId` configured as a part of the app that you attached to the user pool.
*   `clientSecret` (string)  
    This is the `clientSecret` that is configured as a part of the app that you attached to the user pool.

With that file and the proper values in place, the demo application can be launched. If any exceptions occur during launch, be sure that you have included each of the four values shown below and that the file is placed in the correct directory.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3c075b0-0c6a-4e3a-a74e-bfe58cc8758b/xcode-plist-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647a1b2f-5907-4df8-aeef-25f4686838b1/xcode-plist-800w-opt.jpg" width="800" height="305" alt="plist Configuration in Xcode" /></a><figcaption>User pool configuration in Xcode with the <code>plist</code> file (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3c075b0-0c6a-4e3a-a74e-bfe58cc8758b/xcode-plist-large-opt.jpg">View large version</a>)</figcaption></figure>

### App Delegate Integration

The core of the integration with Amazon Cognito happens within the application’s `AppDelegate`. Our first step is to ensure that we have set up logging and have connected to our user pool. As a part of that process, we will assign our `AppDelegate` as the delegate of the user pool. For this basic example, we can keep this logic within the `AppDelegate`. For larger projects, it might make sense to handle this elsewhere.</p>

<pre><code class="language-c">func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -&gt; Bool {
    // set up logging for AWS and Cognito
    AWSDDLog.sharedInstance.logLevel = .verbose
    AWSDDLog.add(AWSDDTTYLogger.sharedInstance)

    // set up Cognito config
    self.cognitoConfig = CognitoConfig()

    // set up Cognito
    setupCognitoUserPool()

    return true
}

func setupCognitoUserPool() {
    // we pull the needed values from the CognitoConfig object
    // this just pulls the values in from the plist
    let clientId:String = self.cognitoConfig!.getClientId()
    let poolId:String = self.cognitoConfig!.getPoolId()
    let clientSecret:String = self.cognitoConfig!.getClientSecret()
    let region:AWSRegionType = self.cognitoConfig!.getRegion()

    // we need to let Cognito know which region we plan to connect to
    let serviceConfiguration:AWSServiceConfiguration = AWSServiceConfiguration(region: region, credentialsProvider: nil)
    // we need to pass it the clientId and clientSecret from the app and the poolId for the user pool
    let cognitoConfiguration:AWSCognitoIdentityUserPoolConfiguration = AWSCognitoIdentityUserPoolConfiguration(clientId: clientId, clientSecret: clientSecret, poolId: poolId)
    AWSCognitoIdentityUserPool.register(with: serviceConfiguration, userPoolConfiguration: cognitoConfiguration, forKey: userPoolID)
    let pool:AWSCognitoIdentityUserPool = AppDelegate.defaultUserPool()
    // we need to set the AppDelegate as the user pool's delegate, which will get called when events occur
    pool.delegate = self
}
</code></pre>

After this configuration is in place, we need to configure the delegate methods for the user pool. The protocol that we are implementing is `AWSCognitoIdentityInteractiveAuthenticationDelegate`. This delegate will get called any time the user needs to log in, reset their password or provide a multi-factor authentication code or if we need to query the user about whether they would like their device to be remembered. For our example, we only need to implement the `startPasswordAuthentication` and the `startNewPasswordRequired` methods:

<pre><code class="language-c">extension AppDelegate: AWSCognitoIdentityInteractiveAuthenticationDelegate {

    // This method is called when we need to log into the application.
    // It will grab the view controller from the storyboard and present it.
    func startPasswordAuthentication() -&gt; AWSCognitoIdentityPasswordAuthentication {
        if(self.navigationController == nil) {
            self.navigationController = self.window?.rootViewController as? UINavigationController
        }

        if(self.loginViewController == nil) {
            self.loginViewController = self.storyboard?.instantiateViewController(withIdentifier: "LoginViewController") as? LoginViewController
        }

        DispatchQueue.main.async {
            if(self.loginViewController!.isViewLoaded || self.loginViewController!.view.window == nil) {
                self.navigationController?.present(self.loginViewController!, animated: true, completion: nil)
            }
        }

        return self.loginViewController!
    }

    // This method is called when we need to reset a password.
    // It will grab the view controller from the storyboard and present it.
    func startNewPasswordRequired() -&gt; AWSCognitoIdentityNewPasswordRequired {
        if (self.resetPasswordViewController == nil) {
            self.resetPasswordViewController = self.storyboard?.instantiateViewController(withIdentifier: "ResetPasswordController") as? ResetPasswordViewController
        }

        DispatchQueue.main.async {
            if(self.resetPasswordViewController!.isViewLoaded || self.resetPasswordViewController!.view.window == nil) {
                self.navigationController?.present(self.resetPasswordViewController!, animated: true, completion: nil)
            }
        }

        return self.resetPasswordViewController!
    }

}
</code></pre>

One key thing to note is that both of these methods return a view controller that implements a specific protocol. For example, the `LoginViewController` implements `AWSCognitoIdentityPasswordAuthentication`, which has a single method that gets called with the parameters needed to enable the user to complete the log-in process.</p>

### Authentication Flow

With all of these pieces in place in the demo application, you can now see the log-in process work from beginning to end. The main view of the application shows the username and the first name and last name of the user. To make this happen, the following steps occur:

1.  In the `AppViewController`, we call the `fetchUserAttributes` method in the `viewDidLoad` method. If the user isn’t logged in, this will trigger the log-in process.
2.  The `startPasswordAuthentication` method in the `AppDelegate` will be triggered. This method loads the `LoginViewController` and presents it.
3.  The `getDetails` method of `LoginViewController` is called by the AWS SDK. This includes an object that is an instance of `AWSTaskCompletionSource`, which we can use to allow the user to attempt to log in.
4.  When the user presses the “Log in” button, we pass the log-in credentials to that object. This will then call the `didCompleteStepWithError` method, and we can handle the result accordingly. If there is no error, we can dismiss the view controller.
5.  If we created the user in the console, we will have another step to handle here. Because we gave the user a temporary password, they will need to set a more permanent one. In addition, because we set the given name and family name as required parameters, we need to allow the user to enter those, too. The AWS SDK will detect this and call the `startNewPasswordRequired` method in the `AppDelegate`. This will present the `ResetPasswordViewController` and set its instance of `AWSTaskCompletionSource`.
6.  The `ResetPasswordViewController` works almost identically to the `LoginViewController`. We simply need to ask the user for the correct values and then submit those values. Once this process is completed successfully, we dismiss the view controller.
7.  Once the entire log-in process has completed, the SDK will securely store the tokens returned by Cognito. Then, we will finally retrieve the user details, and we can use those to populate the `AppViewController` with the user’s username, given name and family name.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a81d5a5-4306-4876-b54d-97147c98727c/app-working-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a81d5a5-4306-4876-b54d-97147c98727c/app-working-preview-opt.jpg" width="617" height="1098" alt="The working application with authentication working" /></a><figcaption>The working sample application, showing username and meta data</figcaption></figure>

## Conclusion

While the user pool set-up process might have several steps, those steps are easy to navigate. In addition, the amount of configuration possible should give you confidence that it can support a majority of use cases. In my day job at Universal Mind, I’ve worked with several clients who are moving their existing applications over to leverage the capabilities that Cognito provides for user management.

Regardless of whether you need to implement a user management system regularly, this is **a tool that every mobile and web developer should have in their toolbox**. In the next article in this series, we will begin to explore the capabilities of Cognito a bit more by implementing a more full-featured demo application that implements more of the common user management use cases.

With a bit of practice, you can go and impress all of your friends by setting up a new application that satisfies all of these user management use cases within a day. That's pretty good for a day's work.</p>

### Links and Resources

*   [Amazon Cognito](https://aws.amazon.com/cognito/)
*   “[Developer Resources](https://aws.amazon.com/cognito/dev-resources/),” Amazon Cognito
*   [AWS Mobile SDK](https://aws.amazon.com/mobile/sdk/)
*   “[CocoaPods Tutorial for Swift: Getting Started](https://www.raywenderlich.com/156971/cocoapods-tutorial-swift-getting-started),” Joshua Greene, raywenderlich.com

{{< signature "da, vf, yk, al, il" >}}

