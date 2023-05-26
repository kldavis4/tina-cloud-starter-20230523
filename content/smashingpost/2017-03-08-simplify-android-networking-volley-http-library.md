---
title: 'How To Simplify Networking In Android: Introducing The Volley HTTP Library'
slug: simplify-android-networking-volley-http-library
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/916a68ca-d47c-4194-9e84-ec3372028cf7/volley-network-call-500w-opt.png
date: 2017-03-08T23:49:27.000Z
author: chetangiridhar
summary: >-
  Volley is a useful library and can save the day for any developer. It’s an integral part of Chetan’s toolkit, and it’s a huge win for any development team in any project. Let’s review what Volley is and get to know its benefits.
description: >-
  Volley is a useful library and can save the day for any developer. It’s an integral part of Chetan’s toolkit, and it’s a huge win for any development team in any project.
categories:
  - Coding
  - Apps
  - Development
  - Android
---
In a world driven by the Internet, mobile apps need to share and receive information from their products' back end (for example, from databases) as well as from third-party sources such as Facebook and Twitter. These interactions are often made through RESTful APIs. When the number of requests increases, the way these requests are made becomes very critical to development, because the manner in which you fetch data can really affect the user experience of an app.

In this article, I’d like to take you through my experience of using networking libraries in Android, focusing on APIs. I’ll start with the basics of synchronous and asynchronous programming and cover the complexities of Android threads. We’ll then dive into the <a href="https://developer.android.com/reference/android/os/AsyncTask.html"> AsyncTask</a> module, <strong>understand its architectural flows and look at code examples</strong> to learn the implementation. I’ll also cover the limitations of the AsyncTask library and introduce Android <a href="https://developer.android.com/training/volley/index.html">Volley</a> as a better approach to making asynchronous network calls. We will then delve deeper into Volley’s architecture and cover its valuable features with code examples.

Still interested? Conquering Android networking will take you far in your journey toward becoming a skillful app developer.

<p><strong>Note</strong>: <em>A few more Android libraries with networking capabilities are not covered in this article, including <a href="https://square.github.io/retrofit/">Retrofit</a>, <a href="https://square.github.io/okhttp/">OkHttp</a>. I recommend that you go through them to get a glimpse of those libraries.</em></p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [Mobile Design Practices For Android: Tips And Techniques](https://www.smashingmagazine.com/2012/07/android-design-tips/)
*   [Get Started Developing For Android With Eclipse](https://www.smashingmagazine.com/2010/10/get-started-developing-for-android-with-eclipse/)
*   [How To Design For Android](https://www.smashingmagazine.com/2011/06/designing-for-android/)

{{% feature-panel %}}

## Programming Approaches Simplified: Sync And Async

"Hold on, Mom, I'm coming," said Jason, still on his couch, waiting for a text from his girlfriend, who he had texted an hour back. "You could clean your room while you wait for a reply from your friend," replied Jason’s mother with a hint of sarcasm. Isn’t her suggestion an obvious one? Similar is the case with synchronous and asynchronous <a href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol">HTTP</a> requests. Let’s look at them.

Synchronous requests behave like Jason, staying idle until there is a response from the server. Synchronous requests block the interface, increase computation time and make a mobile app unresponsive. (Not always, though — sometimes it doesn’t make sense to go ahead, such as with banking transactions.) A smarter way to handle requests is suggested by Jason’s mother. In the asynchronous world, when the client makes a request to the server, the server dispatches the request to an event handler, registers for a callback and moves on to the next request. When the response is available, the client is responded to with the results. This is a far better approach, because asynchronous requests let you execute tasks independently.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e4e66b-67f2-4798-970a-726dfa86e865/ansychronous-synchronous-requests-android-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0365bd-44dc-472d-ae4c-bae1ac49608c/ansychronous-synchronous-requests-android-preview-opt.png" alt="Synchronous versus asynchronous requests" /></a><figcaption>Synchronous versus asynchronous requests (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e4e66b-67f2-4798-970a-726dfa86e865/ansychronous-synchronous-requests-android-large-preview-opt.png">View large version</a>)</figcaption></figure>

The diagram above shows how both programming approaches differ from each other in a client-server model. In Android, the UI thread, often known as the main thread, is based on the same philosophy as asynchronous programming.

## Android Threads

### What Are They And How Do They Work?

Threads are sets of instructions that are managed by the operating system. Multiple threads run under a single process (a Linux process in the case of Android) and share resources such as memory. In Android, when the app runs, the system creates a thread of execution for the whole application, called the "main" thread (or UI thread). The main thread works on a single-threaded model. It is in charge of dispatching events to UI widgets (drawing events), interacting with components from the UI toolkit, such as <code>View.OnClickListener()</code>, and responding to system events, such as <code>onKeyLongPress()</code>.

The UI thread runs on an infinite loop and monitors the message queue to check whether the UI needs to be updated. Let’s consider an example. When the user touches a button, the UI thread dispatches the touch event to the widget, which in turn sets its pressed state and posts a request to the message queue. The UI thread dequeues the request from the message queue and notifies the widget to take action — in this case, to redraw itself to indicate the button has been pressed. If you’re interested in delving deeper into the internals of the UI thread, you should read about <a href="https://developer.android.com/reference/android/os/Looper.html">Looper</a>, the <a href="https://developer.android.com/reference/android/os/MessageQueue.html">MessageQueue</a> and the <a href="https://developer.android.com/reference/android/os/Handler.html">Handler</a> classes, which accomplish the tasks discussed in our example. As you’d imagine, the UI thread has a lot of responsibilities, such as:

*   starting an activity,
*   executing a service,
*   responding to system callbacks.

### Why You Shouldn’t Block the UI Thread

When you think about it, your single-threaded UI thread performs all of its work in response to user interactions. Because everything happens on the UI thread, time-consuming operations such as database queries and network calls will block the UI. The UI thread will dispatch events to the UI widget. The app will perform poorly, and the user will feel that the app is unresponsive. If these tasks take time and the UI thread is blocked for 4 to 5 seconds, Android will throw an "<a href="https://developer.android.com/guide/practices/responsiveness.html">Application Not Responding</a>" (ANR) error. Referring to such an Android app as being not user-friendly would be an understatement, not to mention the poor ratings and uninstalls.

Using the main thread for long tasks would hold things up. Your app will always remain responsive to user events if your UI thread is non-blocking. That is why, if your application requires making network calls, the calls need to be performed on the <strong>worker threads</strong> that run in the background, not on the main thread. You could use a Java HTTP client library to send and receive data over the network, but the network call itself should be performed by a worker thread. But wait, there’s another issue with Android: thread safety.

### Thread Safety and Why It’s So Important!

The Android UI toolkit is <strong>not</strong> <a href="https://en.wikipedia.org/wiki/Thread_safety">thread-safe</a>. If the worker thread (which performs the task of making network calls) updates the Android UI toolkit, it could result in undefined and unexpected behavior. This can be difficult and time-consuming to track down. The single-thread model ensures that the UI is not modified by different threads at the same time. So, if we have to update the ImageView with an image from the network, the worker thread will perform the network operation in a separate thread, while the ImageView will be updated by the UI thread. This makes sure that the operations are thread-safe, with the UI thread providing the necessary synchronization. It also helps that the UI thread is always non-blocking, because the actual task happens in the background by the worker thread.

In summary, follow two simple rules in Android development:

*   The UI thread should not be blocked.
*   The UI toolkit should not be directly updated from a non-UI worker thread.

### A Note on Android Services

When you talk about making requests from an "activity," you will come across Android "<a href="https://developer.android.com/guide/components/services.html">services</a>." A service is an app component that can perform long operations in the background without the app being active or even when the user has switched to another app. For example, playing music or downloading content in the background can be done well with services. If you choose to work with a service, it will still run in your application’s main thread by default, so you’ll need to create a new thread within the service to handle blocking operations. If you need to perform work outside of your main thread while the user is interacting with your app, you are better off using a networking library such as AsyncTask or Volley.

Performing tasks in worker threads is great, but as your app starts to perform complex network operations, worker threads can get difficult to maintain.

## Down The Rabbit Hole With AsyncTask

It’s quite clear now that we should use a robust HTTP client library and ensure that the network task is achieved in the background using worker threads — essentially, with non-UI threads.

Android does have a resource to help handle network calls asynchronously. <a href="https://developer.android.com/reference/android/os/AsyncTask.html">AsyncTask</a> is a module that allows us to perform asynchronous work on the user interface.

### What Does AsyncTask Give Us?

AsyncTask performs all of the blocking operations in a worker thread, such as network calls, and publishes the results once it’s done. The UI thread gets these results and updates the user interface accordingly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82d13600-091e-4e55-be73-607b0184df7f/asynctasks-in-android-app-development-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0de2fc23-123e-4bb8-8121-74932b30b13c/asynctasks-in-android-app-development-preview-opt.png" alt="Asynchronous tasks on Android" width="650" height="488" /></a><figcaption>Asynchronous tasks on Android (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82d13600-091e-4e55-be73-607b0184df7f/asynctasks-in-android-app-development-large-preview-opt.png">View large version</a>)</figcaption></figure>

Here is how I implemented an asynchronous worker thread using AsyncTask:

1.  Subclass AsyncTask to implement the `onPreExecute()` method, which will create a toast message suggesting that the network call is about to happen.
2.  Implement the `doInBackground(Params...)` method. As the name suggests, `doInBackground` is the worker thread that makes network calls and keeps the main thread free.
3.  Because the worker thread cannot update the UI directly, I implemented my own `postExecute(Result)` method, which will deliver the results from the network call and run in the UI thread so that the user interface can be safely modified.
4.  The progress of the background task can be published from the worker thread with the `publishProgress()` method and can be updated on the UI thread using the `onProgressUpdate(Progress...)` method. These methods are not implemented in the example code but are fairly straightforward to work with.
5.  Finally, call the asynchronous task using the `execute()` method from the UI thread.

<strong>Note:</strong> <code>execute()</code> and <code>postExecute()</code> both run on the UI thread, whereas <code>doInBackground()</code> is a non-UI worker thread.

In the context of my app, I make a <code>POST</code> request on a REST API to start a calling session for a campaign. I also pass the access token in the request header and the campaign ID in the body. If you look at the code, <code>java.net.HttpURLConnection</code> is used to make a network call, but the actual work is done in the <code>doInBackground()</code> method of AsyncTask. In the example above, we also make use of the application context to pop up toast messages, but AsyncTasks can be defined as inner classes in activities if they are small enough, avoiding the need for the <code>Context</code> property.

### Generic Types in AsyncTask

A generic type is a generic class or interface that is parameterized over types. Just like how we define formal parameters used in method declarations, type parameters help you to reuse the same code with different input types. While inputs to methods are values, inputs to type parameters are types. There are three types used by an asynchronous task:

*   `Params` The type of the parameters sent to the task upon execution.
*   `Progress` The type of the progress units published during the background computation.
*   `Result` The type of the result of the background computation.

This is how I have extended AsyncTask with types:

<pre><code class="language-java">public class MyAsync extends AsyncTask&lt;String, Void, Integer&gt;</code></pre>

So, the <code>Params</code> sent to the task are of type <code>String</code>; <code>Progress</code> is set to <code>Void</code>; and the <code>Result</code> is of type <code>Integer</code>. In our implementation, we’re passing the URL (type <code>String</code>) to the <code>doInBackground(String... params)</code> method; while we don’t set a <code>Progress</code> type, we pass the status code of the response (type <code>Integer</code>) to <code>onPostExecute(Integer integer)</code>. Not all types are used by an asynchronous task; and to mark a type as unused, we use type <code>Void</code>.

The <strong>code is available for downloading</strong> on GitHub:

*   [MyAsync.java](https://gist.github.com/chetangiridhar/64135df970ff33a5025904a48c2bdeff)
*   [MainActivity.java](https://gist.github.com/chetangiridhar/b7d09ada3151ca09a07ffa7614365741)

## Struggles With AsyncTask

Working with AsyncTask is pretty nice until you start doing more complex operations with it. A few instances where AsyncTask would not be useful are highlighted below:

*   If a background task is running using AsyncTask and the user rotates the screen, the entire activity will be destroyed and recreated. As a result, the reference to the activity will be lost, and the result of AsyncTask will update the UI elements that don’t exist anymore. By the way, if we have to handle this in AsyncTask, we have to monitor for activity getting destroyed in the `onPostExecute` method.
*   Cancelling requests with AsyncTask ensures that the `postExecute()` method is not called. Unfortunately, it doesn’t actually make the request every time. This behavior is not implicit, and it’s the job of the developer to explicitly cancel asynchronous tasks.
*   AsyncTask does not provide the facility of caching results, which can be a setback. Often, an image such as a thumbnail is displayed several times. To reduce bandwidth when displaying this image, we can use the help of caching mechanisms.
*   There are limits on how many parallel tasks you can run with AsyncTask. It can handle 128 concurrent tasks, with a queue length of 10\. So, be aware when you’re crossing those limits. These limits are derived from [ThreadPoolExecutor](https://developer.android.com/reference/java/util/concurrent/ThreadPoolExecutor.html).

Even though AsyncTask does a good job of performing asynchronous operations, its utility can be limiting due to the reasons mentioned above. Luckily, we have Volley at our disposal, an Android module for making asynchronous network calls.

## Enter Volley

<a href="https://developer.android.com/training/volley/index.html">Volley</a> is a networking library developed by Google and introduced at Google I/O 2013. In Volley, all network calls are asynchronous by default, so you don’t have to worry about performing tasks in the background anymore. Volley considerably simplifies networking with its cool set of features.

### Volley’s Architecture

Before looking at the code, let’s get ourselves elbow-deep in Volley and understand its architecture. Below is a high-level architectural diagram of Volley’s flow. It works in a very simple way:

1.  Volley runs one cache processing thread and a pool of network dispatch threads.
2.  Network call requests are first triaged by the cache thread. If the response can be served from the cache, then the cached response is parsed by `CacheDispatcher` and delivered back to the main thread, the UI thread.
3.  If the result is not available in the cache, then a network request needs to be made to get the required data, for which the request is placed in the network queue.
4.  The first available network thread (`NetworkDispatcher`) takes the request from the queue. It then performs the HTTP request, parses the response on the worker thread and writes the response to cache. It then delivers the parsed response back to the main thread.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e56725c-4a60-4a0b-a731-7eedff4142ae/volley-architecture-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7635631-785f-4f28-997b-ea386cdcfc5f/volley-architecture-preview-opt.png" alt="" width=""650&quot;" height="488" /></a><figcaption>Volley’s architecture (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e56725c-4a60-4a0b-a731-7eedff4142ae/volley-architecture-large-preview-opt.png">View large version</a>)</figcaption></figure>

If you carefully analyze Volley’s architecture, you’ll see that it solves issues that we face with AsyncTask:

*   With Volley, we don’t have to worry about getting work done in the background (`doInBackground()` from AsyncTask) because the library makes asynchronous network calls and manages it for you in `NetworkDispatcher`.
*   Updating the results back to the UI thread from the worker thread is handled by Volley, even without your noticing it.
*   Volley frees you from having to write boilerplate code and allows you to concentrate on the tasks specific to your app.
*   Volley has nice set of features, too. To name a few:
    *   Volley caches API responses, so if you make the same request twice, the results are fetched from the cache. This is really useful, as in the case of loading the same image multiple times — we can reduce bandwidth usage by getting the image from cache. We’ll address how to implement the cache in Volley soon.
    *   Volley helps you to prioritize requests. If there are multiple network calls, you could prioritize a given network call based on its impact and importance.
    *   You can easily cancel or retry requests. You have the flexibility to cancel a single request or to cancel blocks of requests.
    *   Volley has strong ordering, which makes it easy to populate the UI in sequence while still fetching data asynchronously.
    *   Volley can handle multiple request types, such as string and JSON. In fact, Volley is perfect for API calls such as JSON objects and lists, and it makes working with RESTful applications very easy.
    *   Image loading is one of the more useful features of Volley. You can write a custom ImageLoader and complement it with the LRU bitmap cache to make network calls for images. We’ll talk about that a bit later.
*   Volley is maintained by Google, which takes care of fixing bugs. That definitely doesn’t hurt, does it!

Let’s see how to make asynchronous calls using Volley. Start by including Volley in your Android project.

## Add Volley To Your Project Easily

The easiest way to add Volley to your project is to add the following dependency to your app’s <code>build.gradle</code> file.

### app/build.gradle

<pre><code class="language-java">dependencies {
  compile 'com.android.volley:volley:x.y.z'
}
</code></pre>

Another way to do this is by cloning the Volley repository. Build Volley with Ant, copy the built <code>volley.jar</code> file in the <code>libs</code> folder, and then create an entry in <code>build.gradle</code> to use the <code>jar</code> file. Here’s how:

<pre><code class="language-javascript">git clone https://android.googlesource.com/platform/frameworks/volley
cd volley
android update project -p .
ant jar
</code></pre>

You can find the generated <code>volley.jar</code> in Volley’s bin folder. Copy it to your <code>libs</code> folder in Android Studio, and add the entry below to <code>app/build.gradle</code>:

### app/build.gradle

<pre><code class="language-java">  dependencies {
    compile files('libs/volley.jar')
  }
</code></pre>

And you’re done! You have added Volley to your project without any hassle. To use Volley, you must add the <code>android.permission.INTERNET</code> permission to your app’s manifest. Without this, your app won’t be able to connect to the network.

### manifests/AndroidManifest.xml

<pre><code class="language-xml">&lt;uses-feature android:name="android.hardware.wifi" android:required="true" /&gt;
&lt;uses-permission android:name="android.permission.INTERNET" /&gt;
</code></pre>

## "Hello World" With Volley: Handling Standard String Requests

The code example below shows you how to make a request on <code>https://api.ipify.org/?format=json</code>, get the response and update the text view of your app. We use Volley by creating a <code>RequestQueue</code> and passing it <code>Request</code> objects. The <code>RequestQueue</code> manages the worker threads and makes the network calls in the background. It also takes care of writing to cache and parsing the response. Volley takes the parsed response and delivers it to the main thread. Appropriate code constructs are highlighted with comments in the code snippet below. I haven’t implemented caching yet; I’ll talk about that in the next example.

### MainActivity.java

<div class="break-out">

 <pre><code class="language-java">package com.example.chetan.androidnetworking;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import com.android.volley.Request;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //Set the title of Toolbar
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        //Get the ID of button that will perform the network call
        Button btn =  (Button) findViewById(R.id.button);
        assert btn != null;
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String url = "https://api.ipify.org/?format=json";
                final TextView txtView = (TextView) findViewById(R.id.textView3);
                assert txtView != null;

                //Request a string response from the URL resource
                StringRequest stringRequest = new StringRequest(Request.Method.GET, url,
                        new Response.Listener() {
                            @Override
                            public void onResponse(String response) {
                                // Display the response string.
                                txtView.setText("Response is: " + response.toString());
                            }
                        }, new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        txtView.setText("Oops! That didn’t work!");
                    }
                });

                //Instantiate the RequestQueue and add the request to the queue
                RequestQueue queue = Volley.newRequestQueue(getApplicationContext());
                queue.add(stringRequest);
            }
        });
    }
</code></pre>
</div>

## Caching Responses With Volley

To set up the cache, we have to implement a disk-based cache and add the cache object to the <code>RequestQueue</code>. I set up a <a href="https://developer.android.com/reference/java/net/HttpURLConnection.html">HttpURLConnection</a> to make the network requests. Volley’s toolbox provides a standard cache implementation via the <code>DiskBasedCache</code> class, which caches the data directly on the hard disk. So, when the button is clicked for the first time, a network call is made, but in the next occurence of a button click, I get the data from the cache. Nice!

### MainActivity.java

<div class="break-out">

 <pre><code class="language-java">package com.example.chetan.androidnetworking;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import com.android.volley.Request;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.BasicNetwork;
import com.android.volley.toolbox.DiskBasedCache;
import com.android.volley.toolbox.HurlStack;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

         //Set the title of Toolbar
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        //Get the ID of button, which will perform the network call
        Button btn =  (Button) findViewById(R.id.button);
        assert btn != null;

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String url = "https://api.ipify.org/?format=json";
                final TextView txtView = (TextView) findViewById(R.id.textView3);
                assert txtView != null;

                // Setup 1 MB disk-based cache for Volley
                Cache cache = new DiskBasedCache(getCacheDir(), 1024 * 1024);

                // Use HttpURLConnection as the HTTP client
                Network network = new BasicNetwork(new HurlStack());

                StringRequest stringRequest = new StringRequest(Request.Method.GET, url,
                        new Response.Listener() {
                            @Override
                            public void onResponse(String response) {
                                // Display the string response on the UI
                                txtView.setText("Response is: " + response.toString());
                            }
                        }, new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        txtView.setText("Oops! That didn’t work!");
                    }
                });

                // Instantiate the RequestQueue with the cache and network, start the request
                // and add it to the queue
                RequestQueue queue = new RequestQueue(cache, network);
                queue.start();
                queue.add(stringRequest);
            }
        });
    }
</code></pre>
</div>

## Setting Up Singleton Class For RequestQueue

If you have to fire network requests in multiple Android activities, you should avoid using <code>Volley.newRequestQueue.add()</code>, as we did in the first example. You can develop a <a href="https://en.wikipedia.org/wiki/Singleton_pattern">singleton</a> class for the <code>RequestQueue</code> and use it across your project. Creating a <code>RequestQueue</code> as a singleton is recommended, so that the <code>RequestQueue</code> lasts for the lifetime of your app. It also ensures that the same <code>RequestQueue</code> is utilized even when the activity is recreated, as in case of a screen rotation.

### VolleyController.java

<div class="break-out">

 <pre><code class="language-java">package com.example.chetan.androidnetworking;

import android.content.Context;
import com.android.volley.Request;
import com.android.volley.RequestQueue;
import com.android.volley.toolbox.ImageLoader;
import com.android.volley.toolbox.Volley;

public class VolleyController    {
    private static VolleyController mInstance;
    private RequestQueue mRequestQueue;
    private static Context mCtx;

    private VolleyController(Context context) {
        mCtx = context;
        mRequestQueue = getRequestQueue();
    }

    public static synchronized VolleyController getInstance(Context context) {
        // If instance is not available, create it. If available, reuse and return the object.
        if (mInstance == null) {
            mInstance = new VolleyController(context);
        }
        return mInstance;
    }

    public RequestQueue getRequestQueue() {
        if (mRequestQueue == null) {
            // getApplicationContext() is key. It should not be activity context,
            // or else RequestQueue won’t last for the lifetime of your app
            mRequestQueue = Volley.newRequestQueue(mCtx.getApplicationContext());
        }
        return mRequestQueue;
    }

    public  void addToRequestQueue(Request req) {
        getRequestQueue().add(req);
    }

}
</code></pre>
</div>

You can now use the <code>VolleyController</code> in your <code>MainActivity</code> like this: <code>VolleyController.getInstance(getApplicationContext()).addToRequestQueue(stringRequest);</code>. Or you can create a queue in this way: <code>RequestQueue queue = VolleyController.getInstance(this.getApplicationContext()).getRequestQueue();</code>. Note the use of <code>ApplicationContext</code> in these examples.

## Volley: Working With JSON Requests

In Volley, you can set up up a custom JSON request by extending the <code>Request</code> class. This will help you to parse and deliver network responses. You can also do more things such as set request priorities and set up cookies with this custom class. Below is the code for creating a custom <code>JSONObject Request</code> in Volley. You can handle <code>ImageRequest</code> types in the same manner.

### CustomJSONObjectRequest.java

<div class="break-out">

 <pre><code class="language-java">package com.example.chetan.androidnetworking;

import com.android.volley.NetworkResponse;
import com.android.volley.ParseError;
import com.android.volley.Request;
import com.android.volley.Response;
import com.android.volley.Response.ErrorListener;
import com.android.volley.Response.Listener;
import com.android.volley.toolbox.HttpHeaderParser;

import org.json.JSONException;
import org.json.JSONObject;

import java.io.UnsupportedEncodingException;
import java.util.Map;

public class CustomJSONObjectRequest extends Request {

    private Listener listener;
    private Map&lt;String, String&gt; params;
    Priority mPriority;

    public CustomJSONObjectRequest(int method, String url, Map&lt;String, String&gt; params,
                                   Listener responseListener, ErrorListener errorListener) {
        super(method, url, errorListener);
        this.listener = responseListener;
        this.params = params;
    }

    protected Map&lt;String, String&gt; getParams()
            throws com.android.volley.AuthFailureError {
        return params;
    };

    @Override
    protected Response parseNetworkResponse(NetworkResponse response) {
        try {
            String jsonString = new String(response.data,
                    HttpHeaderParser.parseCharset(response.headers));
            return Response.success(new JSONObject(jsonString),
                    HttpHeaderParser.parseCacheHeaders(response));
        } catch (UnsupportedEncodingException e) {
            return Response.error(new ParseError(e));
        } catch (JSONException je) {
            return Response.error(new ParseError(je));
        }
    }

    @Override
    protected void deliverResponse(JSONObject response) {
        listener.onResponse(response);
    }

}
</code></pre>
</div>

With asynchronous tasks, you can’t know when the response will arrive from your API. You need to execute a Volley request and wait for the response in order to parse and return it. You can do this with the help of a callback. Callbacks can be easily implemented with Java interfaces. The code below shows how to build your callback with the help of the <code>VolleyCallback</code> interface.

### VolleyCallback.java

<pre><code class="language-java">package com.example.chetan.androidnetworking;

import org.json.JSONException;
import org.json.JSONObject;

public interface VolleyCallback {
    void onSuccess(JSONObject result) throws JSONException;
    void onError(String result) throws Exception;
}
</code></pre>

Now, let’s make a network call using the custom JSON request class and update the UI with the response.

### MainActivity.java

<div class="break-out">

 <pre><code class="language-java">public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        Button btn = (Button) findViewById(R.id.button);
        assert btn != null;
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String url = "https://api.ipify.org/?format=json";

                final TextView txtView = (TextView) findViewById(R.id.textView3);
                assert txtView != null;
                makeRequest(url, new VolleyCallback() {
                    @Override
                    public void onSuccess(JSONObject result) throws JSONException {
                        Toast.makeText(getApplicationContext(), "Hurray!!",
                                Toast.LENGTH_LONG).show();
                        txtView.setText(String.format("My IP is: %s", result.getString("ip")));
                        txtView.setTextColor(Color.BLUE);
                    }

                    @Override
                    public void onError(String result) throws Exception {}
                });
            }
        });

    }
    // Custom JSON Request Handler
    public void makeRequest( final String url, final VolleyCallback callback) {
        CustomJSONObjectRequest rq = new CustomJSONObjectRequest(Request.Method.GET,
                url, null,
                new Response.Listener() {
                    //Pass response to success callback
                    @Override
                    public void onResponse(JSONObject response) {

                        Log.v("Response", response.toString());
                        try {
                            String ip = response.getString("ip");
                            if (ip != "null") {
                                callback.onSuccess(response);
                            }
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                },
                new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {}
                }) {

            @Override
            public Map&lt;String, String&gt; getHeaders() throws AuthFailureError {
                HashMap&lt;String, String&gt; headers = new HashMap&lt;String, String&gt;();
                return headers;
            }

            @Override
            protected Map&lt;String, String&gt; getParams() {
                Map&lt;String, String&gt; params = new HashMap&lt;String, String&gt;();
                return params;
            }

        };

	// Request added to the RequestQueue
	VolleyController.getInstance(getApplicationContext()).addToRequestQueue(rq);
}
</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d69fbb05-eca1-4c6d-a0ee-cf200928a722/volley-network-call-without-blocking-ui-thread-screenshot-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d69fbb05-eca1-4c6d-a0ee-cf200928a722/volley-network-call-without-blocking-ui-thread-screenshot-preview-opt.png" alt="Make a network call to get my IP using Volley without blocking the UI thread" width="570" height="543" /></a><figcaption>Using Volley to make a network call without blocking the UI thread.</figcaption></figure>

## Request An Image With Volley

Volley offers the following classes for requesting images:

*   `ImageRequest` This is used to get an image at the given URL. It also helps with resizing images to the size you need, and all of this happens in the worker thread.
*   `ImageLoader` This class handles the loading and caching of images from remote URLs.
*   `NetworkImageView` This replaces `ImageView` when the image is being fetched from a URL via the network call. It also cancels pending requests if the `ImageView` detaches and is no longer available.

For caching images, you should use the in-memory <code>LruBitmapCache</code> class, which extends <a href="https://developer.android.com/reference/android/util/LruCache.html">LruCache</a>. LRU stands for "least recently used"; this type of caching makes sure that the least used objects are removed first from the cache when it gets full. So, when loading a bitmap into an <code>ImageView</code>, the <code>LruCache</code> is checked first. If an entry is found, it is used immediately to update the <code>ImageView</code>; otherwise, a background thread is spawned to process the image. Just what we want!

## Retry Mechanism In Volley

Volley does retry network calls if you have set the retry policy for your requests. We can change the retry values for each request using <code>setRetryPolicy()</code>. This is implemented in the <a href="https://android.googlesource.com/platform/frameworks/volley/+/idea133/src/com/android/volley/DefaultRetryPolicy.java"><code>DefaultRetryPolicy</code> class</a> of Android. You can set the retry policy for a request in this manner:

<div class="break-out">

 <pre><code class="language-java">rq.setRetryPolicy(new DefaultRetryPolicy(DefaultRetryPolicy.TIMEOUT_MS, DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
                DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
</code></pre>
</div>

<code>DEFAULT_TIMEOUT_MS</code> is the default socket timeout in milliseconds. <code>DEFAULT_MAX_RETRIES</code> is the maximum number of request retries you want to perform. And <code>DEFAULT_BACKOFF_MULT</code> is the default backoff multiplier, which determines the exponential time set to the socket for every retry attempt.

## Volley: Error-Handling

Volley can catch network errors very easily, and you don’t have to bother much with cases in which there is a loss of network connectivity. In my app, I’ve chosen to handle network errors with the error message "No Internet access."

The code below shows how to handle <code>NoConnection</code> errors.

### MainActivity.java

<div class="break-out">

 <pre><code class="language-java">public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        Button btn =  (Button) findViewById(R.id.button);
        assert btn != null;
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String url = "https://api.ipify.org/?format=json";
                final TextView txtView = (TextView) findViewById(R.id.textView3);
                assert txtView != null;

                makeRequest(url, new VolleyCallback() {
                    @Override
                    public void onSuccess(JSONObject result) throws JSONException {
                        Toast.makeText(getApplicationContext(), "Hurray!!",
                                Toast.LENGTH_LONG).show();
                        txtView.setText(String.format("My IP is: %s", result.getString("ip")));
                        txtView.setTextColor(Color.BLUE);
                    }

                    @Override
                    public void onError(String result) throws Exception {
                        Toast.makeText(getApplicationContext(), "Oops!!",
                                Toast.LENGTH_LONG).show();
                        txtView.setText(result);
                        txtView.setTextColor(Color.RED);
                    }
                });
            }
        });
    }
    public void makeRequest( final String url, final VolleyCallback callback) {

        CustomJSONObjectRequest rq = new CustomJSONObjectRequest(Request.Method.GET,
                url, null,
                new Response.Listener() {
                    @Override
                    public void onResponse(JSONObject response) {
                        Log.v("Response", response.toString());
                        try {
                            String ip = response.getString("ip");
                            if (ip != "null") {
                                callback.onSuccess(response);
                            }
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                },
                new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        Log.v("Response", error.toString());
                        String err = null;
                        if (error instanceof com.android.volley.NoConnectionError){
                            err = "No internet Access!";
                        }
                        try {
                            if(err != "null") {
                                callback.onError(err);
                            }
                            else {
                                callback.onError(error.toString());
                            }
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                }) {

            @Override
            public Map&lt;String, String&gt; getHeaders() throws AuthFailureError {
                HashMap&lt;String, String&gt; headers = new HashMap&lt;String, String&gt;();
                headers.put("Content-Type", "application/json");
                return headers;
            }

            @Override
            protected Map&lt;String, String&gt; getParams() {
                Map&lt;String, String&gt; params = new HashMap&lt;String, String&gt;();
                return params;
            }

        };
        rq.setPriority(Request.Priority.HIGH);
        VolleyController.getInstance(getApplicationContext()).addToRequestQueue(rq);

    }
}
</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c67c3044-b32e-4006-bdd2-4e905ff5ff7e/volley-error-msg-on-network-failure-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c67c3044-b32e-4006-bdd2-4e905ff5ff7e/volley-error-msg-on-network-failure-preview-opt.png" alt="Pass a predefined error message about a network failure on the UI thread" width="570" height="534" /></a><figcaption>Pass a predefined error message about a network failure on the UI thread.</figcaption></figure>

## Volley: Adding Request Headers

To make API calls to third-party REST APIs, you need to pass API access tokens or have support for different authorization types. Volley lets you do that easily. Add the headers to the HTTP GET call using the <code>headers.put(key,value)</code> method call:

### MainActivity.java

<pre><code class="language-java">@Override
public Map&lt;String, String&gt; getHeaders() throws AuthFailureError {
    HashMap&lt;String, String&gt; headers = new HashMap&lt;String, String&gt;();
    headers.put("Content-Type", "application/json");
    return headers;
}
</code></pre>

## Volley: Prioritizing Requests

Setting priorities for your network calls is required in order to differentiate between critical operations, such as fetching the status of a resource and pulling its meta data. You don’t want to compromise a critical operation, which is why you should implement priorities. Below is an example that demonstrates how you can use Volley to set priorities. Here, we are using the <code>CustomJSONObjectRequest</code> class, which we defined earlier, to implement the <code>setPriority()</code> and <code>getPriority()</code> methods, and then in the <code>MainActivity</code> class, we are setting the appropriate priority for our request. As a rule of thumb, you can use these priorities for the relevant operations:

*   `Priority.LOW` // images, thumbnails
*   `Priority.NORMAL` // standard queries
*   `Priority.HIGH` // descriptions, lists
*   `Priority.IMMEDIATE` // login, logout

### CustomJSONObjectResponse.java

<pre><code class="language-java">public void setPriority(Priority priority) {
   mPriority = priority;
}

@Override
public Priority getPriority() {
   // Priority is set to NORMAL by default
   return mPriority != null ? mPriority : Priority.NORMAL;
}
</code></pre>

### MainActivity.java

<pre><code class="language-java">// set priority to HIGH
rq.setPriority(Request.Priority.HIGH);
</code></pre>

## Advantages Of Volley

Volley is a useful library and can save the day for a developer. It’s an integral part of my toolkit, and it would be a huge win for a development team in any project. Let’s review Volley’s benefits:

*   It is responsive to user interactions, because all network processes happen asynchronously. The UI thread always remain free to handle any user interaction.
*   It handles networking tasks asynchronously. Whenever a network request is made, a background thread is created to process network calls.
*   Volley improves the lag time between requests because it can make multiple requests without the overhead of thread management.
*   Google has made considerable efforts to improve the performance of the Volley library by improving memory usage patterns and by passing callbacks to the main thread in a batch. This reduces context switching and will make your app faster.

## Summary

*   The UI thread, or the main thread, in Android does the work of dispatching events to the UI toolkit and is responsible for dequeueing the request from message queue to notify the widget to take action. That’s why it’s important that the UI thread always be non-blocking.
*   Android has its own HTTP client libraries, such as `HttpURLConnection`, which help you to perform synchronous network calls. To keep the main thread non-blocking, the network calls need to be performed in worker threads that run in the background.
*   Android’s AsyncTask library helps you run tasks in the background and ensures that your main thread is non-blocking. It also ensures that a background task doesn’t directly update the UI. Instead, it returns the result to the UI thread.
*   AsyncTask has its limitations, such as not being able to cache responses and not being able to handle parallel requests. It also doesn’t gracefully handle scenarios such as screen rotation when background tasks are running.
*   Making asynchronous network calls using Volley is a cleaner solution to developing Android apps. Volley has an awesome set of features, such as caching, request cancellation and prioritization.
*   Volley can handle multiple request types, such as JSON, images and text, and it performs better than AsyncTask.

I hope you’ve enjoyed the article. All of the code examples are available for downloading. The complete app is <a href="https://github.com/callhub/AndroidNetworking">hosted on GitHub</a>.

{{< signature "da, al, il" >}}
