---
title: Understanding Mobile Back End As A Service
slug: understanding-mobile-back-end-as-a-service
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1093c34e-8aa7-4346-86c0-5e55431edeb7/project-occupied-opt-small.jpg
date: 2014-12-15T22:52:58.000Z
author: davidtucker
description: >-
  What if you could create an entire back end for your mobile applications that
  was feature-complete in data synchronization, push-notification support, user
  management and file-handling before you even started building the mobile
  experience? What if it was architected in such a way that you could easily
  **create new cross-platform native and web applications seamlessly** on this
  back end?

  While this might sound like a fairy tale, it is exactly what providers of
  mobile back end as a service (MBaaS) are aiming to give app developers. It is
  up to you to determine whether that is true for the experiences you are
  creating.
categories:
  - Mobile
  - Apps
  - Web Development
---
What if you could create an entire back end for your mobile applications that was feature-complete in data synchronization, push-notification support, user management and file-handling before you even started building the mobile experience? What if it was architected in such a way that you could easily <strong>create new cross-platform native and web applications seamlessly</strong> on this back end?

While this might sound like a fairy tale, it is exactly what providers of mobile back end as a service (MBaaS) are aiming to give app developers. It is up to you to determine whether that is true for the experiences you are creating.</p>

### <span class="rh">Further Reading</span> on SmashingMag

*   [Putting Mobile Back End As A Service Into Practice (Part 1)](https://www.smashingmagazine.com/2015/03/mobile-backend-service-practice-part1/)
*   [Putting Mobile Back End As A Service Into Practice (Part 2)](https://www.smashingmagazine.com/2015/04/mobile-backend-service-practice-part2/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)

Through this article, I hope you gain four key pieces of information: the way MBaaS providers fit into modern mobile application development, the process of evaluating MBaaS providers, the core functionality provided by MBaaS providers and the downsides of leveraging this type of solution. With this information, you will have the pieces to determine whether an MBaaS provider fits in your digital strategy.

{{% feature-panel %}}

## Framing The Discussion

Normalizing the discussion around MBaaS is extremely challenging. While MBaaS is an accepted term, everyone defines it differently. Kinvey recently mapped providers of back-end-as-a-service enterprise solutions. This map illustrates an extensive ecosystem, and defining different solution groups can be extremely challenging.

With the landscape changing by the minute, nailing down all of the players at any given point in time is hard. However, some key providers have proven themselves in the marketplace. Providers such as <a href="https://parse.com/">Parse</a>, <a href="https://www.kinvey.com/">Kinvey</a> and <a href="https://www.salesforce.com/salesforce1/">Salesforce.com</a> have built mature platforms that are currently relied on by many of the applications you use daily. Other more nascent solutions, such as Amazon Web Services’ (AWS) <a href="https://aws.amazon.com/cognito/">Cognito</a>, Microsoft Azure’s <a href="https://azure.microsoft.com/en-us/documentation/services/mobile-services/">Mobile Services</a>, Apple’s <a href="https://developer.apple.com/icloud/documentation/cloudkit-storage/">CloudKit</a>, <a href="https://www.kony.com/products/mbaas">Kony MobileFabric</a> and <a href="https://www.pivotal.io/platform-as-a-service/pivotal-cf">Pivotal CF</a> still need time to be evaluated. Another key challenge in comparing MBaaS providers is that not all providers have feature parity.

<strong>Note:</strong> For this article, I will spend my time focusing on <a href="https://parse.com/">Parse</a> and <a href="https://www.kinvey.com/">Kinvey</a> because of their maturity and breadth of functionality. These two solutions could work for most uses cases, from an independent developer’s app to an enterprise solution across multiple digital properties.</p>

## MBaaS In Real Life

To help explain the purpose of MBaaS, I’ll use an example that we recently created out of our research and development group at <a href="https://www.universalmind.com/">Universal Mind</a>. All of our offices at Universal Mind have flexible work spaces. We wanted to examine how to track available work spaces using <a href="https://en.wikipedia.org/wiki/IBeacon">iBeacons</a>.

iBeacons are a class of sensors that follow Apple’s iBeacon specification. They utilize Bluetooth 4 low energy for communication, which allows an application to continually search for them without draining the user’s battery. They are ideal sensors for determining a user’s proximity (how close the user is to an object), which in certain settings (such as indoors) is more desirable than using GPS.

As a proof of concept, we wanted to create a quick cross-platform application prototype that illustrates how this idea could be leveraged on a large scale. The app itself was fairly basic. Here is a simplistic outline of the data relationships that describe how the application would function:

*   Users have accounts.
*   A user can be assigned to a workspace if they are close enough to the iBeacon that is at a given station.
*   The work space can be occupied or vacant.
*   A workspace exists at an office that has a specific location.
*   A user can get a list of vacant workspaces near them at that point.

In this application example, I’ll walk you through two different scenarios. First, we’ll see how we would have built this without an MBaaS solution. Then, I’ll contrast that with how we actually built it using an MBaaS solution. Through this, you will clearly see that the level of effort required to get something working is drastically different.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d256cff4-c27e-4d89-9775-7e6598f2cf54/project-occupied-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1093c34e-8aa7-4346-86c0-5e55431edeb7/project-occupied-opt-small.jpg" alt="This is a view of the mobile application prototype that was developed by the research and development team at Universal Mind." width="500" height="281" /></a><figcaption>This is a view of the mobile application prototype that was developed by the research and development team at Universal Mind. (<a>View large version</a>)</figcaption></figure>

### Without MBaaS

To create this cross-platform application, we need to put some core components in place:

*   **Server**.  I could probably fire up an AWS [Elastic Compute Cloud](https://aws.amazon.com/ec2/) (EC2) instance and run a Node.js server. I could even leverage Elastic Beanstalk or OpsWorks to handle some of the common deployment processes.
*   **Database**.  Because I am looking at AWS, I could leverage the Relational Database Service (RDS) or DynamoDB for the data store. There is also the option to deploy another solution on AWS, such as MongoLab.
*   **Services**.  I could create the entire integration with the database and then expose REST-based services to make it easy to perform CRUD operations on the data.
*   **User management and security**.  I need to include a user entity as part of the data, and then tie permissions within the services to data that a particular user and/or group owns. In addition, I need to give users the ability to sign up, reset their password, delete their account and so on.
*   **Push notifications**.  Within this Node.js application deployed on an EC2 server, I would need to integrate one of a handful of modules that allow for cross-platform notifications for both iOS and Android. While most of the heavy lifting would happen within these open-source modules, I would still need to integrate the application logic with the notifications.
*   **iOS service integration**.  Because iOS is a target operating system, I would need to integrate with this server on iOS in either Swift or Objective-C. In addition, I would need to determine how to handle service caching, data storage, offline handling, push-notification handling, etc.
*   **Android service integration**.  Because Android is a completely different platform, I would need to create the same server integration on that platform as well. I would need to handle all of the same concerns that I tackled on iOS as well.

With these items in place, I could begin actually building the views of the application and connecting them with the data. I could also begin handling iBeacon integrations and setting a workstation as “occupied” based on the user’s proximity. However, getting to that point and getting the infrastructure in place would take me a good deal of time and configuration. This is where the benefit of MBaaS is realized.</p>

### With MBaaS

The beauty here is that the biggest items are taken care of for me: I never have to deal with configuring the server, setting up and configuring the database, setting up the service, managing users, securing data, setting up push notifications or integrating native services. All of that is provided as a part of MBaaS. My steps now look a bit different:

1.  Create an app with the MBaaS provider.
2.  Include the native SDK in each application.

With these items in place, I can tackle the two main service interactions with minimal code: fetching nearby work spaces and changing the state of a work space from vacant to occupied (and vice versa). Below, I have detailed some sample iOS Objective-C code with these samples, using Parse as the MBaaS provider:

<pre><code class="language-clike">
// In header file or class extension
@property (nonatomic,strong) NSArray *workstations;

// Within the implementation
/*
  After the view loads, we can asynchronously grab the user's location
  and then use that to query for a list of nearby workstations.
*/
- (void)viewDidLoad
{
  [super viewDidLoad];
  // Get the user's location as a Parse PFGeoPoint
  [PFGeoPoint geoPointForCurrentLocationInBackground:^(PFGeoPoint *geoPoint, NSError *error) {
    if (!error) {
      [self fetchWorkstationsNearPoint:geoPoint];
    }
  }];
}

/*
  This method asychronously fetches an array of the workstations
  that are within two miles of the user's current location.
*/
- (void)fetchWorkstationsNearPoint:(PFGeoPoint *)geoPoint
{
  PFQuery *query = [PFQuery queryWithClassName:@"Workstations"];
  [query whereKey:@"location" nearGeoPoint:userLocation withinMiles:2];
  [query findObjectsInBackgroundWithBlock:^(NSArray *objects, NSError *error) {
    if (!error)
    {
      self.workstations = objects;
    }
  }];
}
</code></pre>

&nbsp;

In the code above, I’ve tackled the first challenge: fetching the data for workstations within two miles of the user’s current location. This starts with a call to grab the user’s current location after the application has finished loading. Parse provides a helper that gets this data, so that we don’t have to rely on <code>CLLocationManager</code> directly. Next, the <code>fetchWorkstationsNearPoint</code> method is called, which asynchronously queries Parse’ data store. Behind the scenes, the SDK is making REST calls to grab the data from Parse’s data store.

<pre><code class="language-clike">
/*
  This method fetches a workstation data object given the iBeacon
  identifier. Then, it sets the occupied property and saves the
  object asynchronously.
*/
- (void)setWorkstationState:(BOOL)isOccupied
withBeaconIdentifier:(NSString *)beacon
completionHandler:^(NSError *error)completion
{
  PFQuery *query = [PFQuery queryWithClassName:@"Workstations"];
  [query whereKey:@"beaconIdentifier" equalTo:beaconIdentifier];
    [query findObjectsInBackgroundWithBlock:^(NSArray *objects, NSError *error) {
    if (!error)
    {
      POWorkstation *workstation = [objects firstObject];
      workstation[@"occupied"] = [NSNumber numberWithBool:isOccupied];
      [workstation saveInBackgroundWithBlock:^(BOOL succeeded, NSError *error) {
        completion(error);
      }];
    }
  }];
}</code></pre>

In the code above, I’ve tackled the second challenge: setting the occupied state for a given workstation. This code is as terse as the first snippet. While you don’t see the iBeacon code that triggers this interaction, I wanted to capture all of the interactions with Parse. First, the specific workstation is fetched based on a beacon identifier. This string value is a property of the workstations in the data store. Next, I set the occupied property of the object and then save that value back to the data store in the background.

Very little code is needed to accomplish these tasks because a majority of the logic is happening within Parse’s iOS SDK. This handles things such as the service delegates, data translation and cached data storage, greatly reducing the code that a developer would have to write and maintain over time. While this isn’t a panacea, it provides a solid solution for the most common mobile use cases.

## The Core Premise

Through this example, you can see that the core promise of MBaaS is that it solves the difficult challenge of supporting your mobile back end one time in such a way that it can be leveraged consistently across multiple projects. Instead of firing up a cloud-based database, push-notification server and user-management system, which you would have to manage, you can leverage an MBaaS vendor, which will provide all of this out of the box. In addition, you no longer have to be responsible for uptime and scalability of the back end, instead relying on the vendor for that.

While MBaaS certainly has its skeptics (which I will address later in this article), the focus on MBaaS over the last year has been undeniable. Early MBaaS provider Parse was acquired by Facebook; since then, Apple, Microsoft, Amazon and Google have emerged with their own cloud platforms. In addition, existing providers have thrived and are seeing a sharp uptake in adoption as their platforms have matured.</p>

## Distinguishing Between The Options

No two MBaaS solutions are the same, so knowing how to compare them is crucial. The key differences between providers lie in three areas: platform support, deployment methodology and feature focus.</p>

### Cross-Platform Support

A core benefit of MBaaS is the ability to support an application across multiple platforms. Some solutions, such as iCloud and CloudKit, do a great job of providing a deeply integrated data store (one component of MBaaS) on a single platform. While this works well for a single platform, it greatly limits the ability of an application to become cross-platform at a future time. However, if an application will only ever be on a single platform, this could be a good solution.

Some providers focus on native mobile platforms, while others support mobile web experiences and even desktop applications. At their core, most MBaaS experiences provide REST services, which allow for use on most any platform, but the technology-specific SDKs are a key benefit to developers. Picking an MBaaS provider that provides an SDK for all of the platforms you would like to support would be ideal.

*   Parse currently provides SDKs for iOS, Android, Windows Phone 8, Windows 8, PHP, JavaScript, Mac OS X and Unity.
*   Kinvey currently provides SDKs for iOS, Android, JavaScript, AngularJS, Backbone.js, Ember.js, Node.js, PhoneGap and Titanium.</p>

### Deployment Methodology

In addition to cross-platform support, MBaaS solutions differentiate according to how they are deployed. Determining which options make sense for an organization will depend on several factors, including existing infrastructure, regulations on data storage (for sensitive data) and cost threshold.

Here are the most popular deployment methods for MBaaS solutions:

*   **managed, multi-tenant**.  With a managed multi-tenant MBaaS solution, you don’t have to worry about deploying the environment on your infrastructure. In most cases, the provider will leverage an existing cloud provider, such as AWS, to deploy your application to a scalable environment. In this environment, your back end will run on servers alongside other applications for other users of the platform.
*   **managed, dedicated**.  With a managed dedicated solution, the provider will still leverage a public cloud, such as AWS, but you will ensure that the MBaaS environment is deployed to servers that are dedicated for your use.
*   **managed, on-premise**.  With an on-premise solution, the provider will deploy the MBaaS environment onto servers that you own. In most cases, this requires that you use a specific virtualization platform, such as VMware vCloud Air. For some organizations that deal with sensitive regulated data, this might be a requirement. In most cases, the provider will work together with an organization’s internal IT team to manage the platform.
*   **open source**.  With open-source MBaaS solutions (such as OpenKit and Helios), you will deploy and manage the solution yourself on any infrastructure you choose. This could be an on-premise or cloud-based solution. However, you will have to maintain and update the system yourself. While these solutions give you total control, they also negate many of the benefits of an MBaaS solution.

For most small organizations, the managed multi-tenant options will work perfectly. Larger enterprises could be facing privacy concerns, state and federal regulations and corporate mandates that dictate one solution over another. For example, financial organizations generally have tight restrictions on where account data may be stored. In such cases, a managed on-premise solution might be the only possibility.

Parse currently offers a managed multi-tenant option. Kinvey currently offers managed multi-tenant, managed dedicated and managed on-premise options.</p>

### Feature Focus

Most every MBaaS solution has an area of focus. Some primarily target independent app developers, while other providers focus on the enterprise. Knowing where your effort lies will also help you determine which MBaaS solution is worth the investment of your time and money.

One good example of this is the focus that Kinvey has placed on the enterprise. Kinvey provides a data-connector specification that allows enterprises to hook outside data sources into the existing MBaaS data store, as well as an AuthLink to integrate with enterprise authentication and authorization. These features are fairly insignificant for most independent app developers, but they are absolutely essential for enterprises looking to integrate an MBaaS solution into their existing systems.

Parse has a different focus. It hasn’t focused as much on the enterprise since its acquisition by Facebook, but due to its integration by Facebook, it now provides a good deal of integration with the social juggernaut. Parse’s SDK now provide several utilities specifically geared to making it easier to access particular pieces of Facebook data.</p>

## Core MBaaS Functionality

Most core services offered through MBaaS solutions address the core needs of a mobile application. The main MBaaS providers share four key functions: user management, synchronized data with security, push notifications and file handling. Understanding these key areas of functionality will help you understand how a MBaaS provider could be a part of your digital strategy.</p>

### User Management

Most providers offer user management as a core feature. With this feature, you can give each user an account to which you can attach meta data. Some services take this a step further by allowing you to easily integrate email verification, password resetting, social login and support for anonymous users. This is a central facet of MBaaS functionality because it ties directly to the entire platform’s security.

For enterprise-focused MBaaS, this solution goes a step further. Vendors such as Kinvey offer integration with existing LDAP providers and even enable users to authenticate with Salesforce.com credentials. The key here is that very few enterprise customers want to reinvent user management and rather just want to integrate with existing solutions. Some enterprise-level MBaaS vendors fit this need nicely.</p>

### Synchronized Data With Security

In today’s digital landscape, a user will rarely interact with only one device or even one platform. While a solution such as iCloud enables developers to persist data for users with multiple devices on the same platform, it does nothing to address situations in which a user needs to access the same data from a website as they do from a mobile application. Synchronized cross-platform data is essential for any application that aims to expose itself to users in all areas of their lives. Because of this, synchronized data is the center of most every MBaaS solution.</p>

### Push Notifications

Real-time push notifications are an essential element of many mobile applications. However, integrating with Apple Push Notification service (APNs) or Google Cloud Messaging often requires a dedicated server application. Many organizations have set up their own cross-platform notification server to manage these interactions.

Both Parse and Kinvey provide a basic level of push-notification integration for both Android and iOS.</p>

### File Storage and Delivery

From the uploading of user-generated content to the global delivery of remote application content, applications need to interact with files. Many applications work with existing services such as Amazon CloudFront to leverage a global content delivery network (CDN) for their remote content. Most MBaaS providers offer an abstraction of CDN solutions to enable application developers to work a network of edge servers in order to ensure that their content is delivered in a consistent and performant manner worldwide.</p>

### Additional Features

After this core set of functionality, MBaaS providers branch off into many different feature sets. For example, Kinvey has iBeacon integration, while Parse has third-party integration for functionality such as sending SMS messages. If you are looking to leverage particular functionality, finding a platform that fits the road map of your application is crucial. Evaluating solutions side by side here becomes difficult because the available options do not have full feature parity.</p>

## Downsides And Skeptics

While this functionality might seem like a dream for organizations that are looking to reduce the overall time to market for their apps and provide back-end consistency across their digital properties, consider a few things:

*   In most cases, MBaaS solutions are designed to provide a very low barrier to entry in regards to cost. However, as app usage grows, there is usually a fairly steep slope in the cost curve as well.
*   Because MBaaS solutions do not all correspond to a standard specification and because mass data migration is not always simple, applications are locked into the MBaaS solution that is initially chosen. This isn’t to say that it can’t be changed, but the cost and effort to do so is extensive in many cases.
*   MBaaS providers are hot commodities. You need look no further than Facebook’s aquisition of Parse to see that an MBaaS provider can certainly get acquired. Thoroughly review the terms of every MBaaS provider you are considering to understand how this could affect your application.

Nevertheless, the advantages in many cases outweigh the downsides. Because of the downsides, investigate potential MBaaS solutions extensively before incorporating one in the development plan for your application.

MBaaS certainly has its share of skeptics. I counted myself among that group in the early days of MBaaS. The main question among skeptics is, How can a single solution provide the flexibility needed for every application? The truth is that no solution has the flexiblity to meet every need. It is up to an experience’s owner to choose the solution that most closely maps to the functionality desired alongside the platforms that will be used to present the experience. In some cases, no match will be found and a custom back end would be the best approach.

In the particular use case that I mentioned earlier, this approach has probably saved me a few weeks of development. In addition, it has saved me from having to monitor and administer server instances as part of the overall solution. For me, the benefit was a reduced time to market for this prototype. However, as we’ll discuss in the next section, this isn’t the only benefit.</p>

## MBaaS And Digital Standards

I am a big fan of establishing digital standards within an organization (no matter the size of the organization). Digital standards do require foresight, but when done properly they yield a great degree of efficiency and consistency across an organization’s digital properties. Most organizations, however, focus on user interface standards only. In many cases, an organization using MBaaS across multiple digital projects could lead to a similar standardization of back-end interaction as well.

Adopting MBaaS across a single project obviously holds some benefit for organizations, but the shared learning and consistency derived from using it across multiple projects is where the most value lies.</p>

## Who Should Consider This Approach

MBaaS holds value for organizations of almost any size, but the advantages are different:

*   **enterprise**.  For a large organization, an enterprise-level solution (such as Kinvey) will set back-end standards for how the organization’s mobile applications perform common tasks. In addition, it standardizes how mobile applications access data outside of the MBaaS cloud (with solutions like Kinvey’s data connectors).
*   **small and medium-sized organizations**.  For small organizations, MBaaS provides a completely unmanaged scalable infrastructure. Organizations can deploy experiences without needing a dedicated team to monitor the infrastructure 24/7\. In addition, it can greatly reduce both the time to market and the amount of code to be maintained over time.

Many companies today are taking advantage of this approach. Cadillac, The Travel Channel and The Food Network are just a few of the companies leveraging MBaaS. Experiences like <a href="https://govtribe.com/">GovTribe</a>, <a href="https://www.hipmunk.com/">Hipmunk</a> and Timbre are all powered by MBaaS providers.

Both <a href="https://parse.com/customers">Parse</a> and <a href="https://www.kinvey.com/customers">Kinvey</a> provide several case studies that will help you evaluate successful experiences.</p>

## Final Thoughts And Next Steps

In my next article, I’ll walk you through the creation of a cross-platform MBaaS application. The article will highlight key areas where efficiencies are gained by leveraging an MBaaS provider instead of developing a custom solution.

If you are ready to jump into MBaaS now, then your next step is to check out some of the samples from the providers and examine the functionality and pricing of each platform. The following resources will assist you in your effort to determine the best solution for your experience.</p>

### Kinvey Resources

*   [Dev Center](https://devcenter.kinvey.com/)
*   “[Kinvey’s App Cost Estimator](https://www.kinvey.com/app-cost-estimator)”
*   “[Platform](https://www.kinvey.com/platform)” (overview)

### Parse Resources

*   [Documentation](https://parse.com/docs)
*   “[Pricing](https://parse.com/plans)”
*   [Parse Core](https://parse.com/products/core)

{{< signature "ml, al" >}}

