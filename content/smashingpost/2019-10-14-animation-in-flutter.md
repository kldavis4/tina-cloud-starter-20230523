---
title: 'Animating Apps With Flutter'
slug: animation-apps-flutter
author: shubham-ssj
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ff46b9-aa12-4268-87c7-6907471b0ef1/flutter-animation-hierarchy.png
date: 2019-10-14T13:30:59+02:00
summary: >-
  Flutter provides great animation support for cross-platform apps. This article explores the new unconventional and an easier way to add animations to apps. What exactly are these new “Animation and Motion” widgets and how can we use them to add simple and complex animations?
description: >-
  Flutter provides great animation support for cross-platform apps. This article explores the new unconventional and an easier way to add animations to apps.
categories:
  - Apps
  - Animation
  - Flutter
---
Apps for any platform are praised when they are intuitive, good-looking, and provide pleasant feedback to user interactions. Animation is one of the ways to do just that.

Flutter, a cross-platform framework, has matured in the past two years to include web and desktop support. It has garnered a reputation that apps developed with it are smooth and good-looking. With its rich animation support, declarative way of writing UI, “Hot Reload,” and other features, it is now a complete cross-platform framework.

If you are starting out with Flutter and want to learn an unconventional way of adding animation, then you are at the right place: we will explore the realm of animation and motion widgets, an implicit way of adding animations.

Flutter is based on the concept of widgets. Each visual component of an app is a widget &mdash; think of them as views in Android. Flutter provides animation support using an Animation class, an “AnimationController” object for management, and “Tween” to interpolate the range of data. These three components work together to provide smooth animation. Since this requires manual creation and management of animation, it is known as an explicit way of animating.

Now let me introduce you to animation and motion widgets. Flutter provides numerous widgets which inherently support animation. There’s no need to create an animation object or any controller, as all the animation is handled by this category of widgets. Just choose the appropriate widget for the required animation and pass in the widget’s properties values to animate. This technique is an implicit way of animating.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ff46b9-aa12-4268-87c7-6907471b0ef1/flutter-animation-hierarchy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ff46b9-aa12-4268-87c7-6907471b0ef1/flutter-animation-hierarchy.png" sizes="100vw" caption="Animation hierarchy in Flutter. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ff46b9-aa12-4268-87c7-6907471b0ef1/flutter-animation-hierarchy.png'>Large preview</a>)" alt="" >}}

The chart above roughly sets out the animation hierarchy in Flutter, how both explicit and implicit animation are supported.

Some of the animated widgets covered in this article are:

<ul>
  <li><code>AnimatedOpacity</code></li>
<li><code>AnimatedCrossFade</code></li>
<li><code>AnimatedAlign</code></li>
<li><code>AnimatedPadding</code></li>
<li><code>AnimatedSize</code></li>
<li><code>AnimatedPositioned</code>.</li>
</ul>

Flutter not only provides predefined animated widgets but also a generic widget called <code>AnimatedWidget</code>, which can be used to create custom implicitly animated widgets. As evident from the name, these widgets belong to the animated and motion widgets category, and so they have some common properties which allow us to make animations much smoother and better looking.

Let me explain these common properties now, as they will be used later in all examples.

- `duration`  
The duration over which to animate the parameters.
- `reverseDuration`  
The duration of the reverse animation.
- `curve`  
The curve to apply when animating the parameters. The interpolated values can be taken from a linear distribution or, if and when specified, can be taken from a curve.

Let’s begin the journey by creating a simple app we’ll call “Quoted”. It will display a random quotation every time the app starts. Two things to note: first, all these quotations will be hardcoded in the application; and second, no user data will be saved.

**Note**: *All of [the files for these examples](https://github.com/dev4fun007/animated_widgets) can be found on GitHub.*

{{% feature-panel %}}

## Getting Started

Flutter should be installed and you’ll need some familiarity with the basic flow before moving on. A good place to start is, “<a href="https://www.smashingmagazine.com/2018/06/google-flutter-mobile-development/">Using Google’s Flutter For Truly Cross-Platform Mobile Development</a>”.

Create a new Flutter project in Android Studio.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa76395-f624-446c-b71f-d6b6b6a316a7/new-flutter-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa76395-f624-446c-b71f-d6b6b6a316a7/new-flutter-project.png" sizes="100vw" caption="New flutter project menu in Android Studio. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa76395-f624-446c-b71f-d6b6b6a316a7/new-flutter-project.png'>Large preview</a>)" alt="" >}}

This will open a new project wizard, where you can configure the project basics.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d758e94-0f21-4720-807b-80ea9ae4397f/select-flutter-application.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d758e94-0f21-4720-807b-80ea9ae4397f/select-flutter-application.png" sizes="100vw" caption="Flutter project type selection screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d758e94-0f21-4720-807b-80ea9ae4397f/select-flutter-application.png'>Large preview</a>)" alt="" >}}

In the project type selection screen, there are various types of Flutter projects, each catering to a specific scenario.. For this tutorial, choose <strong>Flutter Application</strong> and press <strong>Next</strong>.

You now need to enter some project-specific information: the project name and path, company domain, and so on. Have a look at the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54a602fa-8b0c-4e47-aac1-a68536549497/flutter-app-project-name.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54a602fa-8b0c-4e47-aac1-a68536549497/flutter-app-project-name.png" sizes="100vw" caption="Flutter application configuration screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54a602fa-8b0c-4e47-aac1-a68536549497/flutter-app-project-name.png'>Large preview</a>)" alt="" >}}

Add the project name, the Flutter SDK path, project location, and an optional project description. Press <strong>Next</strong>.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3184587d-3aef-4e29-8fd9-ad30e8a56dce/flutter-app-company-name.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3184587d-3aef-4e29-8fd9-ad30e8a56dce/flutter-app-company-name.png" sizes="100vw" caption="Flutter application package name screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3184587d-3aef-4e29-8fd9-ad30e8a56dce/flutter-app-company-name.png'>Large preview</a>)" alt="" >}}

Each application (be it Android or iOS) requires a unique package name. Typically, you use the reverse of your website domain; for example, com.google or com.yahoo. Press <strong>Finish</strong> to generate a working Flutter application.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa40006-be80-4995-bebd-b1fc4c016e1a/open-main-dart-file.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa40006-be80-4995-bebd-b1fc4c016e1a/open-main-dart-file.png" sizes="100vw" caption="The generated sample project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa40006-be80-4995-bebd-b1fc4c016e1a/open-main-dart-file.png'>Large preview</a>)" alt="" >}}

Once the project is generated, you should see the screen shown above. Open the *main.dart* file (highlighted in the screenshot). This is the main application file. The sample project is complete in itself, and can be run directly on an emulator or a physical device without any modification.

{{% ad-panel-leaderboard %}}

Replace the content of the *main.dart* file with the following code snippet:

<pre><code class="language-css">import 'package:animated_widgets/FirstPage.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
class MyApp extends StatelessWidget {
 @override
 Widget build(BuildContext context) {
   return MaterialApp(
     title: 'Animated Widgets',
     debugShowCheckedModeBanner: false,
     theme: ThemeData(
       primarySwatch: Colors.blue,
       accentColor: Colors.redAccent,
     ),
     home: FirstPage(),
   );
 }
}</code></pre>

This code cleans up the *main.dart* file by just adding simple information relevant to creating a new app. The class MyApp returns an object: a <code>MaterialApp</code> widget, which provides the basic structure for creating apps conforming to <a href="https://material.io/design/">Material Design</a>. To make the code more structured, create two new dart files inside the *lib* folder: *FirstPage.dart* and *Quotes.dart*.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6152a6b4-f5d3-488c-8fd1-eb5fc14139b2/first-page-dart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6152a6b4-f5d3-488c-8fd1-eb5fc14139b2/first-page-dart.png" sizes="100vw" caption="The FirstPage.dart file. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6152a6b4-f5d3-488c-8fd1-eb5fc14139b2/first-page-dart.png'>Large preview</a>)" alt="" >}}

*FirstPage.dart* will contain all the code responsible for all the visual elements (widgets) required for our Quoted app. All the animation is handled in this file.

**Note**: *Later in the article, all of the code snippets for each animated widget are added to this file as children of the Scaffold widget. For more information, <a href="https://github.com/dev4fun007/animated_widgets">This example on GitHub</a> could be useful.*

Start by adding the following code to *FirstPage.dart*. This is the partial code where other stuff will be added later.

<div class="break-out">

<pre><code class="language-javascript">import 'dart:math';

import 'package:animated_widgets/Quotes.dart';
import 'package:flutter/material.dart';


class FirstPage extends StatefulWidget {
 @override
 State<StatefulWidget> createState() {
   return FirstPageState();
 }
}

class FirstPageState extends State<FirstPage> with TickerProviderStateMixin {

 bool showNextButton = false;
 bool showNameLabel = false;
 bool alignTop = false;
 bool increaseLeftPadding = false;
 bool showGreetings = false;
 bool showQuoteCard = false;
 String name = '';


 double screenWidth;
 double screenHeight;
 String quote;


 @override
 void initState() {
   super.initState();
   Random random = new Random();
   int quoteIndex = random.nextInt(Quotes.quotesArray.length);
   quote = Quotes.quotesArray[quoteIndex];
 }

 @override
 Widget build(BuildContext context) {

   screenWidth = MediaQuery.of(context).size.width;
   screenHeight = MediaQuery.of(context).size.height;

   return Scaffold(
     appBar: _getAppBar(),
     body: Stack(
       children: <Widget>[
         // All other children will be added here.
	  // In this article, all the children widgets are contained
	  // in their own separate methods.
	  // Just method calls should be added here for the respective child.
       ],
     ),
   );
 }
}</code></pre>
</div>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b12bf2a-b80f-4cfc-b05b-a907ef130e2e/quotes-file.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b12bf2a-b80f-4cfc-b05b-a907ef130e2e/quotes-file.png" sizes="100vw" caption="The Quotes.dart file. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b12bf2a-b80f-4cfc-b05b-a907ef130e2e/quotes-file.png'>Large preview</a>)" alt="" >}}

The *Quotes.dart* file contains a list of all the hardcoded quotations. One point to note here is that the list is a static object. This means it can be used at other places without creating a new object of the Quotes class. This is chosen by design, as the above list act simply as a utility.

Add the following code to this file:

<div class="break-out">

<pre><code class="language-javascript">class Quotes {
 static const quotesArray = [
   "Good, better, best. Never let it rest. 'Til your good is better and your better is best",
   "It does not matter how slowly you go as long as you do not stop.",
   "Only I can change my life. No one can do it for me."
 ];
}</code></pre>
</div>

The project skeleton is now ready, so let’s flesh out Quoted a bit more.


## <code>AnimatedOpacity</code>

To lend a personal touch to the app, it would be nice to know the user’s name, so let’s ask for it and show a next button. Until the user enters their name, this button is hidden, and it will gracefully show up when a name is given. We need some kind of visibility animation for the button, but is there a widget for that? Yes, there is.

Enter <code>AnimatedOpacity</code>. This widget builds on the Opacity widget by adding implicit animation support. How do we use it? Remember our scenario: we need to show a next button with animated visibility. We wrap the button widget inside the <code>AnimatedOpacity</code> widget, feed in some proper values and add a condition to trigger the animation &mdash; and Flutter can handle the rest.

<pre><code class="language-javascript">_getAnimatedOpacityButton() {
  return AnimatedOpacity(
	duration: Duration(seconds: 1),
	reverseDuration: Duration(seconds: 1),
	curve: Curves.easeInOut,
	opacity: showNextButton ? 1 : 0,
	child: _getButton(),
  );
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/000143f0-0f6f-4f77-9a61-4450568cebcd/animatedopacity.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/607f778f-7968-4330-a565-cd5d9b818b8e/animated-opacity-400w.gif" width="400" height="" alt="" /></a><figcaption>Opacity animation of next button. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/000143f0-0f6f-4f77-9a61-4450568cebcd/animatedopacity.gif">Large preview</a>)</figcaption></figure>

The <code>AnimatedOpacity</code> widget has two mandatory properties:

- `opacity`  
A value of 1 means completely visible; 0 (zero) means hidden. While animating, Flutter interpolates values between these two extremes. You can see how a condition is placed to change the visibility, thus triggering animation.
- `child`  
The child widget that will have its visibility animated.

You should now understand how really simple it is to add visibility animation with the implicit widget. And all such widgets follow the same guidelines and are easy to use. Let’s move on to the next one.

{{% ad-panel-leaderboard %}}

## <code>AnimatedCrossFade</code>

We have the user’s name, but the widget is still waiting for input. In the previous step, as the user enters their name, we display the next button. Now, when the user presses the button, I want to stop accepting input and show the entered name. There are many ways to do it, of course, but perhaps we can hide away the input widget and show an uneditable text widget. Let’s try it out using the <code>AnimatedCrossFade</code> widget.

This widget requires two children, as the widget crossfades between them based on some condition. One important thing to keep in mind while using this widget is that both of the children should be the same width. If the height is different, then the taller widget gets clipped from the bottom. In this scenario, two widgets will be used as children: input and label.

<div class="break-out">

<pre><code class="language-javascript">_getAnimatedCrossfade() {

  return AnimatedCrossFade(

	duration: Duration(seconds: 1),

	alignment: Alignment.center,

	reverseDuration: Duration(seconds: 1),

	firstChild: _getNameInputWidget(),

	firstCurve: Curves.easeInOut,

	secondChild: _getNameLabelWidget(),

	secondCurve: Curves.easeInOut,

	crossFadeState: showNameLabel ? CrossFadeState.showSecond : CrossFadeState.showFirst,

  );

}</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bde61ba-34fe-414f-9905-552e2e96d002/animatedcrossfade.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/376db7c4-6934-4ef3-84b5-bc813a096b1b/animated-crossfade-400w.gif" width="400" height="" alt="" /></a><figcaption>Cross-fading between the input widget and name widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bde61ba-34fe-414f-9905-552e2e96d002/animatedcrossfade.gif">Large preview</a>)</figcaption></figure>

This widget requires a different set of mandatory parameters:

- `crossFadeState`  
This state works out which child to show.
- `firstChild`  
Specifies the first child for this widget.
- `secondChild`  
Specifies the second child.

## <code>AnimatedAlign</code>

At this point, the name label is positioned at the center of the screen. It will look much better at the top, as we need the center of the screen to show quotes. Simply put, the alignment of the name label widget should be changed from center to top. And wouldn’t it be nice to animate this alignment change along with the previous cross-fade animation? Let’s do it.

As always, several techniques can be used to achieve this. Since the name label widget is already center-aligned, animating its alignment would be much simpler than manipulating the top and left values of the widget. The <code>AnimatedAlign</code> widget is perfect for this job.

To initiate this animation, a trigger is required. The sole purpose of this widget is to animate alignment change, so it has only a few properties: add a child, set its alignment, trigger the alignment change, and that’s it.

<pre><code class="language-javascript">_getAnimatedAlignWidget() {

  return AnimatedAlign(

duration: Duration(seconds: 1),

curve: Curves.easeInOut,

alignment: alignTop ? Alignment.topLeft : Alignment.center,

child: _getAnimatedCrossfade(),

  );

}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95e3d10-e95e-4f2d-9bce-b5dde562c22e/animatedalign.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47d752ba-4ef2-4c69-9d7a-b802948cc22a/animated-align-400w.gif" width="400" height="" alt="" /></a><figcaption> Alignment animation of the name widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95e3d10-e95e-4f2d-9bce-b5dde562c22e/animatedalign.gif">Large preview</a>)</figcaption></figure>

It has only two mandatory properties:

<ul>
  <li><strong>child:</strong><br />The child whose alignment will be modified.</li>
  <li><strong>alignment:</strong><br />Required alignment value.</li>
</ul>

This widget is really simple but the results are elegant. Moreover, we saw how easily we can use two different animated widgets to create a more complex animation. This is the beauty of animated widgets.


## <code>AnimatedPadding</code>

Now we have the user’s name at the top, smoothly animated without much effort, using different kinds of animated widgets. Let’s add a greeting, “Hi,” before the name. Adding a text widget with value “Hi,” at the top will make it overlap the greeting text widget, looking like the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487115cd-a1fc-4e31-9bb7-3738f9487c89/name-greetings-overlap.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487115cd-a1fc-4e31-9bb7-3738f9487c89/name-greetings-overlap.png" sizes="100vw" caption="The greeting and name widgets overlap. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487115cd-a1fc-4e31-9bb7-3738f9487c89/name-greetings-overlap.png'>Large preview</a>)" alt="" >}}

What if the name text widget had some padding on the left? Increasing the left padding will definitely work, but wait: can we increase the padding with some animation? Yes, and that is what <code>AnimatedPadding</code> does. To make all this much better looking, let’s have the greetings text widget fade in and the name text widget’s padding increase at the same time.

<div class="break-out">

<pre><code class="language-javascript">_getAnimatedPaddingWidget() {

  return AnimatedPadding(

	duration: Duration(seconds: 1),

	curve: Curves.fastOutSlowIn,

	padding: increaseLeftPadding ? EdgeInsets.only(left: 28.0) : EdgeInsets.only(left: 0),

	child: _getAnimatedCrossfade(),

  );

}</code></pre>
</div>

Since the animation above should occur only after the previous animated alignment is complete, we need to delay triggering this animation. Digressing from the topic briefly, this is a good moment to talk about a popular mechanism to add delay. Flutter provides several such techniques, but the Future.delayed constructor is one of the simpler, cleaner and more readable approaches. For instance, to execute a piece of code after 1 second:

<div class="break-out">

<pre><code class="language-javascript">Future.delayed(Duration(seconds: 1), (){
	sum = a + b;	// This sum will be calculated after 1 second.
	print(sum);
});</code></pre>
</div>

Since the delay duration is already known (calculated from previous animation durations), the animation can be triggered after this interval.

<div class="break-out">

<pre><code class="language-javascript">// Showing “Hi” after 1 second - greetings visibility trigger.
_showGreetings() {
  Future.delayed(Duration(seconds: 1), () {
	setState(() {
  		showGreetings = true;
	});
  });
}

// Increasing the padding for name label widget after 1 second - increase padding trigger.
_increaseLeftPadding() {
  Future.delayed(Duration(seconds: 1), () {
	setState(() {
  	increaseLeftPadding = true;
	});
  });
}</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/309333bd-518f-4802-b4bb-20d61bc143b3/animatedpadding.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eab3737-3249-4906-bfbb-d43214014082/animated-padding-400w.gif" width="400" height="" alt="" /></a><figcaption>Padding animation of the name widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/309333bd-518f-4802-b4bb-20d61bc143b3/animatedpadding.gif">Large preview</a>)</figcaption></figure>

This widget has only two mandatory properties:

- `child`  
The child inside this widget, which padding will be applied to.
- `padding`  
The amount of space to add.

## <code>AnimatedSize</code>

Today, any app having some kind of animation will include zooming in to or out of visual components to grab user attention (commonly called scaling animation). Why not use the same technique here? We can show the user a motivational quote that zooms in from the center of the screen. Let me introduce you to the <code>AnimatedSize</code> widget, which enables the zoom-in and zoom-out effects, controlled by changing the size of its child.

This widget is a bit different from the others when it comes to the required parameters. We need what Flutter calls a “Ticker.” Flutter has a method to let objects know whenever a new frame event is triggered. It can be thought of as something that sends a signal saying, “Do it now! … Do it now! … Do it now! …”

The <code>AnimatedSize</code> widget requires a property &mdash; <strong>vsync</strong> &mdash; which accepts a ticker provider. The easiest way to get a ticker provider is to add a <strong>Mixin</strong> to the class. There are two basic ticker provider implementations: <code>SingleTickerProviderStateMixin</code>, which provides a single ticker; and <code>TickerProviderStateMixin</code>, which provides several.

The default implementation of a Ticker is used to mark the frames of an animation. In this case, the latter is employed. More about <a href="https://dart.dev/guides/language/language-tour#adding-features-to-a-class-mixins">mixins</a>.

<div class="break-out">

<pre><code class="language-javascript">// Helper method to create quotes card widget.
_getQuoteCardWidget() {
  return Card(
	color: Colors.green,
	elevation: 8.0,
	child: _getAnimatedSizeWidget(),
  );
}
// Helper method to create animated size widget and set its properties.
_getAnimatedSizeWidget() {
  return AnimatedSize(
	duration: Duration(seconds: 1),
	curve: Curves.easeInOut,
	vsync: this,
	child: _getQuoteContainer(),
  );
}
// Helper method to create the quotes container widget with different sizes.
_getQuoteContainer() {
  return Container(
	height: showQuoteCard ? 100 : 0,
	width: showQuoteCard ? screenWidth - 32 : 0,
	child: Center(
  	child: Padding(
    	padding: EdgeInsets.symmetric(horizontal: 16),
    	child: Text(quote, style: TextStyle(color: Colors.white, fontWeight: FontWeight.w400, fontSize: 14),),
  	),
	),
  );
}
// Trigger used to show the quote card widget.
_showQuote() {
  Future.delayed(Duration(seconds: 2), () {
	setState(() {
  		showQuoteCard = true;
	});
  });
}</code></pre>
</div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25d65198-cee7-4b75-827d-662241452484/animatedsize.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adda1c12-f5e1-4968-bc2f-b119f4a79c2d/animated-size-400w.gif" width="400" height="" alt="" /></a><figcaption>Scaling animation of the quotes widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25d65198-cee7-4b75-827d-662241452484/animatedsize.gif">Large preview</a>)</figcaption></figure>

Mandatory properties for this widget:

- `vsync`  
The required ticker provider to coordinate animation and frame changes.<
- `child`  
The child whose size changes will be animated.

The zoom in and zoom out animation is now easily tamed.

## <code>AnimatedPositioned</code>

Great! The quotes zoom in from the center to grab the user’s attention. What if it slid up from the bottom while zooming in? Let’s try it. This motion involves playing with the position of the quote widget and animating the changes in position properties. <code>AnimatedPositioned</code> is the perfect candidate.

This widget automatically transitions the child’s position over a given duration whenever the specified position changes. One point to note: it works only if its parent widget is a “Stack.” This widget is pretty simple and straightforward to use. Let’s see.

<pre><code class="language-javascript">// Helper method to create the animated positioned widget.
// With position changes based on “showQuoteCard” flag.
_getAnimatedPositionWidget() {
  return AnimatedPositioned(
	duration: Duration(seconds: 1),
	curve: Curves.easeInOut,
	child: _getQuoteCardWidget(),
	top: showQuoteCard ? screenHeight/2 - 100 : screenHeight,
	left: !showQuoteCard ? screenWidth/2 : 12,
  );
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48786ddc-3cc6-4178-9605-a1bd4b24da9f/animatedpositioned.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/727fddfe-79bd-4812-aaed-28d39fee5993/animated-positioned-400w.gif" width="400" height="" alt="" /></a><figcaption>Position with scaling animation of quotes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48786ddc-3cc6-4178-9605-a1bd4b24da9f/animatedpositioned.gif">Large preview</a>)</figcaption></figure>

This widget has only one mandatory property:

- `child`  
The widget whose position will be changed.

If the size of the child is not expected to change along with its position, a more performative alternative to this widget would be <code>SlideTransition</code>.

Here is our complete animation:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f62bf735-f74f-4b58-8900-03ef3d23e108/fullvideo-flutter-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d74c1abe-0123-4f0f-a597-4d4b5ff3d6a6/full-video-flutter-animation-400w.gif" width="400" height="" alt="" /></a><figcaption>All the animated widgets together. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f62bf735-f74f-4b58-8900-03ef3d23e108/fullvideo-flutter-animation.gif">Large preview</a>)</figcaption></figure>

## Conclusion

Animations are an integral part of user experience. Static apps or apps with janky animation not only lower user retention but also a developer’s reputation to deliver results.

Today, most popular apps have some kind of subtle animation to delight users. Animated feedback to user requests can also engage them to explore more. Flutter offers a lot of features for cross-platform development, including rich support for smooth and responsive animations.

Flutter has great plug-in support which allows us to use animations from other developers. Now that it has matured to version 1.9, with so much love from the community, Flutter is bound to get better in the future. I’d say now is a great time to learn Flutter!

### Further Resources

<ul>
  <li>“<a href="https://flutter.dev/docs/development/ui/widgets/animation">Animation And Motion Widgets</a>,” Flutter Docs</li>
  <li>“<a href="https://flutter.dev/docs/development/ui/animations">Introduction To Animations</a>,” Flutter Docs</li>
  <li><a href="https://flutter.dev/docs/codelabs">Flutter Codelabs</a></li>
</ul>

**Editor’s Note**: *A huge Thank You to [Ahmad Awais](https://twitter.com/MrAhmadAwais) for his help in reviewing this article.*

{{< signature "dm, og, yk, il" >}}
