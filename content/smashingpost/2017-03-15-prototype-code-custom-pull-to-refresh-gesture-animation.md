---
title: 'Prototype And Code: Creating A Custom Pull-To-Refresh Gesture Animation'
slug: prototype-code-custom-pull-to-refresh-gesture-animation
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59511bd3-6c06-42dd-892e-5bd90c83ea88/pull-to-refresh-500w-opt.png
date: 2017-03-15T18:58:28.000Z
author: ellinabereza
description: >-
  Pull-to-refresh is one of the most popular gestures in mobile applications
  right now. It’s easy to use, natural and so intuitive that it is hard to
  imagine refreshing a page without it. In 2010, Loren Brichter created Tweetie,
  one of numerous Twitter applications. Diving into the pool of similar
  applications, you won’t see much difference among them; but Loren’s Tweetie
  stood out then.
categories:
  - Mobile
  - Apps
  - Animation
  - Prototyping
---
It was one simple animation that changed the game — pull-to-refresh, an absolute innovation for the time. No wonder Twitter didn’t hesitate to buy Tweetie and hire Loren Brichter. Wise choice! As time went on, <strong>more and more developers integrated this gesture</strong> into their applications, and finally, Apple itself brought pull-to-refresh to its system application Mail, to the joy of people who value usability.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9918bb84-746e-4f5c-a662-8d1c7f9688f6/pull-to-refresh-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dba9f6c0-bede-4d24-847c-c9ec90a156cb/pull-to-refresh-large-preview-opt.png" alt="Refresh gesture" width="780" height="390" /></a><figcaption>The refresh gesture we are going to create. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9918bb84-746e-4f5c-a662-8d1c7f9688f6/pull-to-refresh-large-opt.png">View large version</a>)</figcaption></figure>

Today, most clients wish to see this gesture in their apps, and most designers want to create prototypes with integrated pull-to-refresh animation, preferably a custom one. This tutorial explains how to build a prototype in <a href="https://www.flinto.com/mac">Flinto</a>, a tool that makes swipe-gesture animation possible, and obviously you cannot create a pull-to-refresh animation without a pull. However, it would be fair to say that Flinto is not the only tool that gives us the swipe gesture — Facebook Origami and POP are worth mentioning. After we create a prototype, we will code it into our design of an Android application.

This tutorial will help you master Flinto, understand the logic of creating prototypes of this kind, and learn the process of coding these prototypes in your application. To follow the steps, you will need macOS, <a href="https://www.sketchapp.com/">Sketch for Mac</a>, <a href="https://www.flinto.com/mac">Flinto for Mac</a> to create the prototype, and <a href="https://developer.android.com/studio/index.html">Android Studio</a> and <a href="https://docs.oracle.com/javase/7/docs/webnotes/install/">JDK 7+</a> to write the code.

{{% feature-panel %}}

### <span class="rh">Further Reading</span> on SmashingMag:

*   [In-App Gestures And Mobile App User Experience](https://www.smashingmagazine.com/2016/10/in-app-gestures-and-mobile-app-user-experience/)
*   [How Functional Animation Helps Improve UX](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/)
*   [The Thumb Zone: Designing For Mobile Users](https://www.smashingmagazine.com/2016/09/the-thumb-zone-designing-for-mobile-users/)
*   [Creating Advanced Animations In Photoshop](https://www.smashingmagazine.com/2015/06/creating-advanced-animations-in-photoshop/)

## Prototype In Flinto

For the prototype, I am using screens of <a href="https://play.google.com/store/apps/details?id=com.erminesoft.chatboard">ChatBoard</a>, an Android chat application by <a href="https://www.erminesoft.com">Erminesoft</a>. The list of user chat rooms would be a perfect place to integrate a refresh animation to check new messages. Let’s begin!

### Step 1

We’ll make all of the designs in <a href="https://www.sketchapp.com/">Sketch</a>. For the first step, we’ll need to create one screen with any list of items the user will be able to refresh. Now we need to export the screen to Flinto. We have two options here:

*   Export as separate PNG files.
*   Use the plugin [Send to Flinto](https://www.flinto.com/mac_sketch_plugin).</p>

### Step 2

Let’s move to Flinto for Mac, which you can buy for $99, or you can download a free trial on <a href="https://www.flinto.com/mac">the website</a>. To make a simple pull-to-refresh animation, we need five screens. At this point, we can add a custom image or use standard Flinto forms (a rectangle or circle) to create the animated element. For this project, I am using three standard circles. Stop right there: Don’t search for a circle form. Use a rectangle (R), make a square out of it, and set a maximum corner radius. There you go — you’ve got a circle!

### Step 3

The first animation frame requires a separate layer with the list of content. Behind it, we’ll place the animated element in the starting position; in our case, there will be three circles placed on the same X and Y coordinates. That’s screen 1.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ec0a9d0-f38f-433b-8686-5a96e9adeda7/3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ebec55b-0ee2-4440-bc5d-8e26b391547f/3-large-preview-opt.png" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ec0a9d0-f38f-433b-8686-5a96e9adeda7/3-large-opt.png">View large version</a>)</figcaption></figure>

### Step 4

On screen 2, we need to move the content down the Y-axis, revealing the animated element hidden behind the list of content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f10e07b6-70e2-44f2-bab0-c426f6a86aa7/4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe33a368-3b5d-48ea-8243-d3daeebefdd1/4-large-preview-opt.png" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f10e07b6-70e2-44f2-bab0-c426f6a86aa7/4-large-opt.png">View large version</a>)</figcaption></figure>

Additionally at this step (and all following steps), the transition timer (“Timer Link”) should be turned on and set to 0 milliseconds, to eliminate any lag in transition to the next animation screen. Just click on an artboard title to see the timer transition settings.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b34df86-bd95-475a-a329-c67e8c466201/5-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/741e69fc-8a6e-434d-b413-bfd947edf58a/5-large-preview-opt.png" alt="Timer Link" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b34df86-bd95-475a-a329-c67e8c466201/5-large-opt.png">View large version</a>)</figcaption></figure>

### Step 5

The previous screen (screen 2) shows only one circle, but remember that three circles are placed at the same X and Y coordinates. At this point (screen 3), our task is to move one of the circles 30 pixels left along the X-axis, and another circle 30 pixels right along the X-axis. Don’t forget to set the transition timer to 0 milliseconds.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b64bf2e0-d448-45e3-a97d-a08b2992fb39/6-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c63cee2-1c99-48f9-b24c-8833dfb5845d/6-large-preview-opt.png" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b64bf2e0-d448-45e3-a97d-a08b2992fb39/6-large-opt.png">View large version</a>)</figcaption></figure>

### Step 6

Let’s move on to screen 4. Repeat step 5 doing the same thing but moving the circles along the Y-axis instead of the X-axis for the same 30 pixels. The X coordinates of all of the elements should be the same and center-aligned. Don’t forget about the transition timer.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b456aeaa-af16-4f63-a9c0-f3e35b8695b6/7-large-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9df5c5ce-3606-4781-a413-25d0da0b16de/7-large-preview-opt.png" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b456aeaa-af16-4f63-a9c0-f3e35b8695b6/7-large-opt-1.png">View large version</a>)</figcaption></figure>

### Step 7

Copy screen 2 for the new screen 5. At this step, all we need to do is change the timer link’s target not to screen 3 but to our home screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c718e00-b031-4648-9fcf-249e90a93e2d/8-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5221180-ce0a-4d44-b456-c921de3c7fe9/8-large-preview-opt.png" alt="All Screens" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c718e00-b031-4648-9fcf-249e90a93e2d/8-large-opt.png">View large version</a>)</figcaption></figure>

### Step 8

All of the preparations are done, and we can now move to the animations. Create a new transition. Select the layer of content on the home screen, press <code>F</code>, and link it to screen 2.

(By the way, the key <code>F</code> refers to the name of the program itself, “Flinto.” It is its signature key.)

Apply the following transition settings:

*   Gesture: down swipe
*   Target: “Screen 2”
*   Transition: “New transition”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09f72a29-6ae4-4dbc-aa75-88b9cc7c4186/9-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/807aed11-154d-4e69-9e7c-6ed995290bb9/9-large-preview-opt.png" alt="New Transition" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09f72a29-6ae4-4dbc-aa75-88b9cc7c4186/9-large-opt.png">View large version</a>)</figcaption></figure>

### Step 9

Now we get to the custom transition animation section. The first thing to do here is to lay one screen above the other. This creates the impression that it is one animated screen, instead of two screens, because it technically is.</p>

### Step 10

At this point, we need to set the connections between elements throughout the screens in order for the program to associate them. For example, the element named “Circle-1” on the home screen is the same object on all of the screens. We just need to select two identical elements and click “Connect Layers.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fd59d85-74ec-41c5-a02d-f9e675583c2d/10-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cb7d300-1ff0-4f2c-bd03-2ec0c0ff2c72/10-large-preview-opt.png" alt="Connect Layers" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fd59d85-74ec-41c5-a02d-f9e675583c2d/10-large-opt.png">View large version</a>)</figcaption></figure>

We have to connect all identical elements in this way for our “New Transition.” You can try out various kinds of animations in the “Effects” section, but in this particular case, I advise you to use “Spring,” to make our circles bounce.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9864b342-8fec-453f-ba5b-59feaa921a70/11-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e15271-44b6-422a-9472-7dd6959bb4e3/11-large-preview-opt.png" alt="Spring" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9864b342-8fec-453f-ba5b-59feaa921a70/11-large-opt.png">View large version</a>)</figcaption></figure>

### Step 11

Click “Save &amp; Exit.” Now we need to select this transition type for all of the transitions in our project, including our timers.

(An interesting fact: In Principle, the prototyping tool, layers are connected automatically when the program finds two elements with identical names. I find the automatic connection more convenient for those who keep Sketch’s layers’ names in order. Flinto is a better choice for the lazy ones who prefer to connect all animated elements while creating a prototype.)

Additionally, to achieve a more realistic effect, you can make the refreshed screen show an update or an additional item.</p>

{{< vimeo id="196645336" caption="The 'Spring' animation" >}}

In case things don’t go as expected when you follow this tutorial, simply [download the related Flinto template](https://drive.google.com/file/d/0B5mFiaC5f_0gMHk0OFBKZU0zLWc/view?usp=sharing).

Despite the simplicity of this animation, it delivers surprising dynamics and responsiveness to the prototype. It also gives a feeling of product completeness, and it is necessary to making a prototype feel as product-like as possible.

Prototyping is a crucial stage in application development, not only impressing the client and verifying the design concept, but also helping to establish a hand-off process between the designers (who create the animations) and the developers (who implement them). Prototypes can become a valuable asset of communication between team members because they ensure that coders understand the project’s specifications and can implement the designer’s custom animations.

Now, let’s proceed to code our prototype in a Java application for Android mobile devices.</p>

## Code

The whole process of creating a custom <code>PullToRefreshListView</code> for Android involves only three steps:

1.  Create the animated element.
2.  Code a custom `ListView`.
3.  Integrate the element into the application’s code.</p>

### 1. The Animated Element

Take the <code>drawable</code> folder in our project, and create a file named <code>point.xml</code> with the following content:

<pre><code class="language-java">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;shape xmlns:android="https://schemas.android.com/apk/res/android"
    android:dither="true"
    android:shape="oval"&gt;

    &lt;gradient
        android:endColor="#ffff6600"
        android:gradientRadius="10dp"
        android:startColor="#ffffcc00"
        android:type="radial"
        android:useLevel="false" /&gt;

    &lt;size
        android:height="10dp"
        android:width="10dp" /&gt;

&lt;/shape&gt;
</code></pre>

The element has now been formed. The next step is to build the animated movement of these elements. Let’s jump to the <code>anim</code> folder (or create it if it’s absent), and add two files, named <code>left_step_anim.xml</code> and <code>right_step_anim.xml</code>.

The following code listing is for <code>left_step_anim.xml</code>:

<pre><code class="language-java">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;set xmlns:android="https://schemas.android.com/apk/res/android"
    android:duration="800"
    android:repeatMode="restart"&gt;

    &lt;translate
        android:fromXDelta="0%"
        android:toXDelta="-50" /&gt;

    &lt;translate
        android:startOffset="800"
        android:toYDelta="50"
        android:toXDelta="50" /&gt;

    &lt;translate
        android:startOffset="1600"
        android:toYDelta="-50" /&gt;

&lt;/set&gt;
</code></pre>

The following code should be placed in <code>right_step_anim.xml</code>:

<pre><code class="language-java">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;set xmlns:android="https://schemas.android.com/apk/res/android"
    android:duration="800"&gt;

    &lt;translate
        android:fromXDelta="0%p"
        android:toXDelta="50" /&gt;

    &lt;translate
        android:startOffset="800"
        android:toYDelta="-50"
        android:toXDelta="-50" /&gt;

    &lt;translate
        android:startOffset="1600"
        android:toYDelta="50" /&gt;

&lt;/set&gt;
</code></pre>

Now we need to add our animation to the markdown. Browse to the <code>layout</code> folder, and create a file named <code>ptr_header.xml</code>, with the following code:

<pre><code class="language-java">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout xmlns:android="https://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal"&gt;
    &lt;RelativeLayout android:id="@+id/ptr_id_header"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:gravity="center_vertical"
        android:padding="5dp"&gt;

        &lt;ImageView
            android:id="@+id/point"
            android:paddingTop="30dp"
            android:paddingBottom="30dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerHorizontal="true"
            android:contentDescription="point"
            android:scaleType="fitCenter"
            android:src="@drawable/point" /&gt;

        &lt;ImageView
            android:id="@+id/point2"
            android:paddingTop="30dp"
            android:paddingBottom="30dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerHorizontal="true"
            android:contentDescription="point"
            android:scaleType="fitCenter"
            android:src="@drawable/point" /&gt;

        &lt;ImageView
            android:id="@+id/point3"
            android:paddingTop="30dp"
            android:paddingBottom="30dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:contentDescription="point"
           android:scaleType="fitCenter"
            android:src="@drawable/point"
            android:layout_alignTop="@+id/point"
            android:layout_alignLeft="@+id/point"
            android:layout_alignStart="@+id/point" /&gt;

    &lt;/RelativeLayout&gt;
&lt;/LinearLayout&gt;
</code></pre>

The file we’ve created will serve as the animated element. Let’s proceed to the second step.</p>

### 2. Custom ListView

We need to create an item to use in our custom <code>ListView</code>. To do this, navigate to the <code>layout</code> folder and create a file named <code>list_item.xml</code>, containing one <code>TextView</code> element. This is what it should look like:

<pre><code class="language-java">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout xmlns:android="https://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" &gt;

    &lt;TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="fill_parent"
        android:padding="5dp"
        android:singleLine="true"
        android:textColor="@android:color/black"
        android:textSize="10pt" /&gt;

&lt;/LinearLayout&gt;
</code></pre>

Now, let’s add a file with our <code>ListView</code> to the layout folder. In our case, it is a file named <code>main.xml</code> in a folder named <code>layout</code>. It should read as follows:

<pre><code class="language-java">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout xmlns:android="https://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical"&gt;

    &lt;erminesoft.com.listreload.PullToRefreshListView
        android:id="@+id/pull_to_refresh_listview"
        android:layout_height="fill_parent"
        android:layout_width="fill_parent"

        android:background="@android:color/white"
        android:cacheColorHint="@android:color/white" /&gt;

&lt;/LinearLayout&gt;
</code></pre>

The custom <code>ListView</code> has now been created.</p>

### 3. Integrating The Elements

The last step of this process involves binding together all of the elements above. We need to create two classes. The first class is named <code>PullToRefreshListViewSampleActivity</code> and is used when launching the application. The second class, <code>PullToRefreshListView</code>, will contain our element.

In the <code>PullToRefreshListViewSampleActivity</code> class, our attention is on the <code>onRefresh()</code> method of the <code>onCreate()</code> method. This method is exactly where all of the <code>ListView</code> refreshing magic will happen. Because this is an example, we’ve added our own test data with the <code>loadData()</code> method of the internal class <code>PullToRfreshListSampleAdapter</code>. The remaining code of the <code>PullToRefreshListViewSampleActivity</code> class is relatively simple.

Let’s move on to the <code>PullToRefreshListView</code> class. Because the main functionality is built on the standard <code>ListView</code>, we’ll add <code>extends ListView</code> to its name. The class is quite simple, yet animation involves a few constants that are defined by experimentation. Besides that, the interface implements the <code>onRefresh()</code> method.

Now let’s add a file with our <code>ListView</code> to the layout folder. In our case, it is a file named <code>main.xml</code> in a folder named <code>layout</code>. It should read as follows:

<pre><code class="language-java">public interface OnRefreshListener{
    void onRefresh();
}
</code></pre>

This method will be used to refresh the <code>ListView</code>. Our class also contains several constructors to create the <code>View</code> element.</p>

<pre><code class="language-java">public PullToRefreshListView(Context context){
    super(context);
    init(context);
}

public PullToRefreshListView(Context context, AttributeSet attrs){
    super(context, attrs);
    init(context);
}

public PullToRefreshListView(Context context, AttributeSet attrs, int defStyle){
    super(context, attrs, defStyle);
    init(context);
}
</code></pre>

The class also includes the <code>onTouchEvent</code> and <code>onScrollChanged</code> event handlers. These are standard solutions that have to be implemented. You will also need the private class <code>HeaderAnimationListener</code>, which handles animation in the <code>ListView</code>.</p>

<pre><code class="language-java">private class HeaderAnimationListener implements AnimationListener{
...
}
</code></pre>

There you go! The code is <a href="https://github.com/erminesoft-com/pull-to-refresh">available on GitHub</a>.

This tutorial is intended to encourage designers and developers to work together to integrate a custom pull-to-refresh animation and to make it a small yet nice surprise for users. It adds a certain uniqueness to an application and shows that the developers are dedicated to creating an engaging experience for the user above all else. It is also the foundation for making more complex animation, limited only by your imagination. We believe it’s important to experiment with custom animations, adding a touch of creativity to every project you build!

{{< signature "da, al, il" >}}

