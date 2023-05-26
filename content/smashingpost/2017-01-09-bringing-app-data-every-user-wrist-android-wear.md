---
title: 'Bringing Your App’s Data To Every User’s Wrist With Android Wear'
slug: bringing-app-data-every-user-wrist-android-wear
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c013cff3-c973-4022-84f6-3e0879f2276f/complications-flow-preview-opt.png
date: 2017-01-09T18:46:26.000Z
author: danielebonaldo
summary: >-
  Have you tried experimenting with the Complications API? This article shows how to make your app’s data available directly from a wearable watch face, allowing the user to access it at a glance. You’ll also learn how to sync data between a phone and smartwatch, and how to display it using the new Complications API.
description: >-
  Have you tried experimenting with the Complications API? This article shows how to make your app’s data available directly from a wearable watch face, allowing the user to access it at a glance.
categories:
  - Mobile
  - Apps
  - Android
---
The most popular mobile operating system is known to be [Android](https://www.netmarketshare.com/operating-system-market-share.aspx?qprid=8&qpcustomd=1). One of the main reasons for its popularity is its ability to run on a huge number of devices, not only on phones and tablets. We find Android on TVs, watches, cars, even fridges and [mirrors](https://medium.com/@danybony_/mirror-smart-mirror-on-the-wall-a211a73456f5).

Android Wear is the version of the operating system specifically designed to extend the Android platform to wearables, with particular attention to smartwatches. These devices allow the user to consume information in a completely different way than traditional handheld devices: Data is presented at the right time depending on the user's context, and interaction is less invasive and time-consuming than in a phone app.

Android Wear is the version of the operating system specifically designed to extend the Android platform to wearables, with particular attention to smartwatches. These devices allow the user to consume information in a completely different way than traditional handheld devices: Data is presented at the right time depending on the user's context, and interaction is less invasive and time-consuming than in a phone app.</p>

This article shows <strong>how to make your app's data available</strong> directly from a wearable watch face, allowing the user to access it at a glance. We'll see how to sync data between a phone and smartwatch and how to display it using the new Complications API.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Getting Started With Wearables: How To Plan, Build And Design](https://www.smashingmagazine.com/2015/10/getting-started-wearables-plan-build-design/)
*   [Designing For Smartwatches And Wearables](https://www.smashingmagazine.com/2015/02/designing-for-smartwatches-wearables/)
*   [Intimate And Interruptive: Designing For The Power Of Apple Watch](https://www.smashingmagazine.com/2015/10/intimate-interruptive-designing-power-apple-watch/)
*   [The Wireframe Perfectionist’s Guide](https://www.smashingmagazine.com/2016/11/wireframe-perfectionist-guide/)

{{% feature-panel %}}

## Watch Faces And Complications

What are these complications, to start with? In the context of traditional watchmaking, a complication is, as defined by Wikipedia:
<blockquote>"...any feature in a timepiece beyond the simple display of hours and minutes."</blockquote>

Some of the best-known examples of complications are the date display, a chronometer or a second time indicator.

Complications are certainly nothing new in mechanical watches. We have the first reports of pocket watches including extra complications from back in the 16th century.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c9c7e6-896a-4906-a9fc-8fff8e864d3c/movement-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8442275-ca60-4edc-a9da-8fd678944e01/movement-preview-opt.jpg" alt="A mechanical watch movement" width="780" height="438" /></a><figcaption>The movement of the first mechanical watch that I built (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c9c7e6-896a-4906-a9fc-8fff8e864d3c/movement-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

Smartwatches are the perfect house for these kinds of additional features, thanks to the huge potential provided by digital screens.

The most popular type of app for smartwatches today is the watch face, and for a good reason: It is displayed for most of the time on the watch's display, when no other app is in use. Thousands of watch faces are available in the Play store, each with a different style.

One of the main principles of Android Wear is glanceability: The user should always be able to consume the displayed information in a split second, without any interruption to their activity. Complications are created exactly with this principle in mind: While the main purpose of a watch face is to enable the user to tell the time, <strong>complications can be even more useful</strong>, displaying an array of information without requiring the user to open a different app.

In Android Wear, we already have several examples of watch faces that include complications. They display information such as a step counter, the weather forecast, details about the user's next meeting and much more.

The way these complications have worked so far had a big limitation: Every single watch face app had to implement its own logic to fetch the data. If two watch faces displayed the weather forecast, for example, the developers had to implement two similar mechanisms to fetch the same data. Such a waste of resources!

Android Wear 2.0 aims to solve this problem with the new Complications API.</p>

## Wear's Complications API

Specifically, Android Wear puts two main actors into communication:

*   the **data provider**, which includes the logic to fetch the data;
*   the **watch face**, which displays the information exposed by the data provider.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0dcfb76-a655-4da9-9b0e-ee3ed1e013ae/complications-flow-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c013cff3-c973-4022-84f6-3e0879f2276f/complications-flow-preview-opt.png" alt="The Complication API flow" width="780" height="439" /></a><figcaption>The Complication API's flow (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0dcfb76-a655-4da9-9b0e-ee3ed1e013ae/complications-flow-large-preview-opt.png">View large version</a>)</figcaption></figure>

A watch face <strong>never has direct access to a data provider</strong>. It will instead receive a callback when new data is available for the complications that the user has selected. Meanwhile, the data provider doesn't know how the exposed information will be displayed: That is completely up to the watch face, depending on its style.</p>

{{% ad-panel-leaderboard %}}

### Complication Types

To define some sort of communication protocol between the two actors, the Complications API specifies a set of complication types that can be used by a provider when exposing data.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86754742-bcd0-439b-a456-f3fefe45a8ce/complications-types-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e018aeb0-f6bc-4357-8bdc-881b76fe59f4/complications-types-preview-opt.png" alt="Different complication types" width="780" height="439" /></a><figcaption>Complication types (Image: <a href="https://d.android.com">d.android.com</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86754742-bcd0-439b-a456-f3fefe45a8ce/complications-types-large-preview-opt.png">View large version</a>)</figcaption></figure>

Each type has at least one required field, which is the primary piece of data. The watch face always expects to receive this field, and some optional fields can be used to provide additional information.

In the "Short Text" type, for example, the required field is a short amount of text, which may be accompanied by a short title or an icon to make the main information even more explicit. Icons in general should be a single color with transparency, because they might be tinted by the watch face.

The following table summarizes the required and optional fields for every complication type:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
    <tr>
      <th data-tablesaw-priority="persist">Complication type</th>
      <th>Required fields</th>
      <th>Optional fields</th>
    </tr>
  </thead>  
<tbody>
<tr>
<td>Short Text</td>
<td>Short text</td>
<td>Icon
Short title</td>
</tr>
<tr>
<td>Icon</td>
<td>Icon</td>
<td></td>
</tr>
<tr>
<td>Ranged Value</td>
<td>Value
Minimum value
Maximum value</td>
<td>Icon
Short text
Short title</td>
</tr>
<tr>
<td>Long Text</td>
<td>Long text</td>
<td>Long title
Icon
Small image</td>
</tr>
<tr>
<td>Small Image</td>
<td>Small image</td>
<td></td>
</tr>
<tr>
<td>Large Image</td>
<td>Large image</td>
<td></td>
</tr>
</tbody>
</table>

## Use Case

It became immediately apparent to me that this new API has huge potential. So, I decided to use it with an existing project, in order to expose some already available data from the app using an <em>ad-hoc</em> complication.

The project is an open-source app created by my friend <a href="https://twitter.com/alexstyl">Alexandros</a>, which I've been using for a while now: <a href="https://github.com/alexstyl/Memento-Namedays">Memento Namedays</a>. The purpose of the app is to remind you of birthdays and name days of your contacts, and this looks like a perfect use case for a complication to display information about the next birthday among your contacts.

Let's have a look at how I managed to create the data provider.</p>

### Syncing Data Between Handheld and Wearable

The code for the phone app was included in an Android module named <code>mobile</code>. I created another module named <code>wear</code>, which includes the code for the part of the app to be installed on the smartwatch. I then made the required data from <code>mobile</code> available to the <code>wear</code> module of the app.

The phone app already has a service for checking every day for upcoming birthdays and name days, and that became the perfect access point to fetch the data needed by the complication.

Every time a relevant change happens (for example, when the birthday of one of my contacts arrived), I used the <a href="https://developer.android.com/training/wearables/data-layer/index.html">Wearable Data Layer API</a> to sync this data between the handheld and wearable.</p>

{{% ad-panel-leaderboard %}}

### Exposing the Complication Data

In the <code>wear</code> module, I created the complication data provider, which is a service that extends <code>ComplicationProviderService</code>. This base class gives us a set of callbacks for us to know the status of our complication:

*   `onComplicationActivated` tells us when the provider is selected as the data source for a complication in the current watch face.
*   `onComplicationDeactivated` tells us when the complication is not selected anymore.
*   `onComplicationUpdate` tells us when it is time to provide an updated set of data to populate the complication.

The last method is the most important one, because there we need to load new data and bundle it to be forwarded to the watch face.

Among the callback parameters, the complication type allows the data provider to add the required fields according to the type supported by the watch face.

In the case of a "Short Text" type, I populate <code>ComplicationData</code> with the date of the next event and an optional icon:

<div class="break-out">

<pre><code class="language-javascript">
ComplicationData.Builder(ComplicationData.TYPE_SHORT_TEXT)
    .setShortText(ComplicationText.plainText(formatShortDate(date)))
    .setIcon(Icon.createWithResource(context, R.drawable.ic_event))
    .setTapAction(createContactEventsActivityIntent())
    .build();
</code></pre></div>

In the case of a "Long Text," I add the list of contact names associated with the next event:

<div class="break-out">

<pre><code class="language-javascript">
ComplicationData.Builder(ComplicationData.TYPE_SHORT_TEXT)
    .setLongTitle(ComplicationText.plainText(formatLongDate(date)))
    .setLongText(ComplicationText.plainText(formatList(names))) 
    .setIcon(Icon.createWithResource(context, R.drawable.ic_event))
    .setTapAction(createContactEventsActivityIntent())
    .build();
</code></pre></div>

Note that complications may be made tappable by the user directly from the watch face. To support this, I used the builder method <code>setTapAction</code> to specify a <code>PendingIntent</code>, pointing to an activity displaying all information for the given event. It is then responsibility of the watch face to trigger that <code>PendingIntent</code> on the user's tap.

In the following picture, we see the final result. From left to right, the exposed complication with the "Short Text" and "Long Text" types are displayed on two different watch faces, and the activity displays the event details.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1b88433-26ca-4c24-92f7-d75e9e74828c/screenshots-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b050f7d0-32df-4aa7-89da-9268c060dac7/screenshots-preview-opt-2.png" alt="Screenshots of the complications created" width="780" height="358" /></a><figcaption>The result: "Short Text" and "Long Text" complications and the activity launched upon a tap (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1b88433-26ca-4c24-92f7-d75e9e74828c/screenshots-large-preview-opt.png">View large version</a>)</figcaption></figure>

### Updating the Data

It is possible to specify an update period for the <code>ComplicationProviderService</code> in its manifest entry using the following key:

<div class="break-out">

<pre><code class="language-javascript">android.support.wearable.complications.UPDATE_PERIOD_SECONDS</code></pre></div>

This value should be set as high as possible, in order to minimize the impact on the device's battery from frequent updates. Also, note that this value does not guarantee a constant update frequency: The system will optimize the update calls depending on the status of the device (setting less frequent updates if the device is in ambient mode or is not being worn).

In our case, the complication data doesn't change often, and the phone app already handles that logic of updating the synced data. I decided, then, to be a good citizen and go for a push-style update mechanism.

First, I disabled automatic data refreshing by setting the <code>UPDATE_PERIOD_SECONDS</code> value to <code>0</code> in the manifest.

I then used a <code>WearableListenerService</code> to receive a callback every time some updated data is synced for a given URI. In this case, it's the one I used to sync data between <code>mobile</code> and <code>wear</code>. When this happens, I manually request an update using a <code>ProviderUpdateRequester</code>:

<div class="break-out">

<pre><code class="language-javascript">
public class DataChangedListenerService extends WearableListenerService {

    @Override
    public void onDataChanged(DataEventBuffer dataEventBuffer) {
        super.onDataChanged(dataEventBuffer);
        ComponentName providerComponentName = new ComponentName(
            context, 
            MyComplicationProviderService.class
        );
        ProviderUpdateRequester providerUpdateRequester = new
            ProviderUpdateRequester(context, providerComponentName);
        providerUpdateRequester.requestUpdateAll();
    }

} 
</code></pre></div>

All of the code for this article is <a href="https://github.com/alexstyl/Memento-Namedays/pull/40">available on GitHub</a>.

You will see how easy it is to update an existing app to sync data between a phone and smartwatch, and then to display it on a watch face using the new Complications API.</p>

## Conclusion

Thanks to the Complications API, every Android application can easily export the most important data and make it accessible at a glance directly on the user's wrist, even without requiring a dedicated watch face.

At the time of writing, this API is still in a preview state, so it might change before the final release of Android Wear 2.0, but its potential is already very interesting.

If a lot of apps are updated to use this new API, we will have a prosperous ecosystem of complications for users to choose from, with information-rich watch faces and a great increase in usefulness in our connected devices!

For more information on the Complications API, please have a look at the <a href="https://developer.android.com/wear/preview/features/complications.html">official documentation</a>.

{{< signature "da, yk, al, il" >}}

