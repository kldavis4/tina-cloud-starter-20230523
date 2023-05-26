---
title: 'Performing iOS Animations On Views With UIKit And UIView'
slug: performing-ios-animations-views-uikit-uiview
author: saravanan-v
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f0786fa-1f90-4b49-8ddb-44c1e17deb5a/animations-examples-tutorial.png
date: 2019-11-20T11:00:00.000Z
summary: >-
  This article aims to be a primer on iOS animations exhaustively covering different ways of doing so. We start off by understanding the basics of animations, move to the Core Frameworks building a single example using the different methods offered and finally looking at ways to tune performance.
description: >-
  This article aims to be a primer on iOS animations exhaustively covering different ways of doing so. We start off by understanding the basics of animations, move to the Core Frameworks building a single example using the different methods offered and finally looking at ways to tune performance.
categories:
  - Animation
  - iOS
  - UI
  - Mobile
---
<p>I have been an iOS developer for over a decade now and have rarely seen articles that consolidate all possible ways to perform animations in iOS. This article aims to be a primer on iOS animations with the intent of exhaustively covering the different ways of doing the same.</p>

<p>Given the extensiveness of the topic, we would cover each part succinctly at a fairly high level. The goal is to educate the reader with a set of choices to add animations to his/ her iOS app.</p>

<p>Before we start off with topics related to iOS, let us take a brief look at animation speed.</p>

## Animating At 60FPS

<p>Generally in videos, each frame is represented by an image and the frame rate determines the number of images flipped in the sequence. This is termed as ‘frames per second’ or FPS.</p>

<p>FPS determines the number of still images flipped within a second, which literally means that the more the number of images/ frames, more details/ information are displayed in the video. This holds true for animations as well.</p>

<p>FPS is typically used to determine the quality of animations. There is a popular opinion that any good animation should run at 60fps or higher &mdash; anything less than 60fps would feel a bit off.</p>

<p>Do you want to see the difference between 30FPS and 60FPS? <a href="https://www.30vs60fps.com">Check this</a>!</p>

<p>Did you notice the difference? Human eyes can definitely feel the jitter at lower fps. Hence, it is always a good practice to make sure that any animation you create, adheres to the ground rule of running at 60FPS or higher. This makes it feel more realistic and alive.</p>

<p>Having looked at FPS, let’s now delve into the different core iOS frameworks that provide us a way to perform animations.</p>

{{% feature-panel %}}

## Core Frameworks

<p>In this section, we will touch upon the frameworks in the iOS SDK which can be used for creating view animations. We will do a quick walk through each of them, explaining their feature set with a relevant example.</p>

### UIKit/ UIView Animations

<p>UIView is the base class for any view that displays content in iOS apps.</p>

<p>UIKit, the framework that gives us UIView, already provides us some basic animation functions which make it convenient for developers to achieve more by doing less.</p>

<p>The API, <code>UIView.animate</code>, is the easiest way to animate views since any view’s properties can be easily animated by providing the property values in the block-based syntax.</p>

<p>In UIKit animations, it is recommended to modify only the animatable properties of UIVIew else there will be repercussions where the animations might cause the view to end up in an unexpected state.</p>

#### animation(withDuration: animations: completion)

<p>This method takes in the animation duration, a set of view’s animatable property changes that need to be animated. The completion block gives a callback when the view is done with performing the animation.</p>

<p>Almost any kind of animation like moving, scaling, rotating, fading, etc. on a view can be achieved with this single API.</p>

<p>Now, consider that you want to animate a button size change or you want a particular view to zoom into the screen. This is how we can do it using the <code>UIView.animate</code> API:</p>

<div class="break-out">

<pre><code class="language-javascript">let newButtonWidth: CGFloat = 60

UIView.animate(withDuration: 2.0) { //1
    self.button.frame = CGRect(x: 0, y: 0, width: newButtonWidth, height: newButtonWidth) //2
    self.button.center = self.view.center //3
}</code></pre>
</div>

<p>Here’s what we are doing here:</p>

<ol>
<li>We call the <code>UIView.animate</code> method with a duration value passed to it that represents how long the animation, described inside the block, should run.</li>
<li>We set the new frame of the button that should represent the final state of the animation.</li>
<li>We set the button <code>center</code> with its superview’s center so that it remains at the center of the screen.</li>
</ol>

<p>The above block of animation code should trigger the animation of the button’s frame changing from current frame:

<p><blockquote><code>Width = 0, Height = 0</code></blockquote></p>

<p>To the final frame:</p>

<p><blockquote><code>Width = Height = newButtonWidth</code></blockquote></p>

<p>And here’s what the animation would look like:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97852ff0-90f8-4ab4-847b-2c5b435c5670/1-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97852ff0-90f8-4ab4-847b-2c5b435c5670/1-performing-ios-animations-on-views-with-uikit-uiview.gif" width="220" height="" alt="" /></a></figure>

#### animateWithDuration

<p>This method is like an extension of the animate method where you can do everything that you can perform in the prior API with some physics behaviors added to the view animations.</p>

<p>For example, if you want to achieve spring damping effects in the animation that we have done above, then this is how the code would look like:</p>

<div class="break-out">

<pre><code class="language-javascript">let newButtonWidth: CGFloat = 60
UIView.animate(withDuration: 1.0, //1
    delay: 0.0, //2
    usingSpringWithDamping: 0.3, //3
    initialSpringVelocity: 1, //4
    options: UIView.AnimationOptions.curveEaseInOut, //5
    animations: ({ //6
        self.button.frame = CGRect(x: 0, y: 0, width: newButtonWidth, height: newButtonWidth)
        self.button.center = self.view.center
}), completion: nil)</code></pre>
</div>

<p>Here’s the set of parameters we use:</p>

<ol>
<li><code>duration</code><br />Represents the duration of the animation determining how long the block of code should run.</li>
<li><code>delay</code><br />Represents the initial delay that we want to have before the start of the animation.</li>
<li><code>SpringWithDamping</code><br />Represents the value of the springy effect that we want the view to behave. The value must be between 0 to 1. The lower the value, the higher the spring oscillation.</li>
<li><code>velocity</code><br />Represents the speed at which the animation should start.</li>
<li><code>options</code><br />Type of animation curve that you want to apply to your view animation.</li>
<li>Finally, the block of code where we set the frame of the button that needs to be animated. It is the same as the previous animation.</li>
</ol>

<p>And here’s what the animation would look like with the above animation configuration:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/342d390a-114d-41b9-9123-401f4c8504c8/2-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/342d390a-114d-41b9-9123-401f4c8504c8/2-performing-ios-animations-on-views-with-uikit-uiview.gif" width="352" height="" alt="" /></a></figure>

#### UIViewPropertyAnimator

<p>For a bit more control over animations, <code>UIViewPropertyAnimator</code> comes handy where it provides us a way to pause and resume animations. You can have custom timing and have your animation to be interactive and interruptible. This is very much helpful when performing animations that are also interactable with user actions.</p>

<p>The classic ‘Slide to Unlock’ gesture and the player view dismiss/ expand animation (in the Music app) are examples of interactive and interruptible animations. You can start moving a view with your finger, then release it and the view will go back to its original position. Alternatively, you can catch the view during the animation and continue dragging it with your finger.</p>

<p>Following is a simple example of how we could achieve the animation using <code>UIViewPropertyAnimator</code>:</p>

<div class="break-out">

<pre><code class="language-javascript">let newButtonWidth: CGFloat = 60
let animator = UIViewPropertyAnimator(duration:0.3, curve: .linear) { //1
    self.button.frame = CGRect(x: 0, y: 0, width: newButtonWidth, height: newButtonWidth)
    self.button.center = self.view.center
}
animator.startAnimation() //2</code></pre>
</div>

<p>Here’s what we are doing:</p>

<ol>
<li>We call the <code>UIViewProperty</code> API by passing the duration and the animation curve.</li>
<li>Unlike both the above UIView.animate API’s, the animation won’t start unless you specify it by yourself i.e. you’re in full control of the complete animation process/ flow.</li>
</ol>

<p>Now, let’s say that you want even more control over the animations. For example, you want to design and control each and every frame in the animation. There’s another API for that, <code>animateKeyframes</code>. But before we delve into it, let’s quickly look at what a frame is, in an animation.</p>

{{% ad-panel-leaderboard %}}

### What Is A <code>frame</code>?

<p>A collection of the view’s frame changes/ transitions, from the start state to the final state, is defined as <code>animation</code> and each position of the view during the animation is called as a <code>frame</code>.</p>

#### animateKeyframes

<p>This API provides a way to design the animation in such a way that you can define multiple animations with different timings and transitions. Post this, the API simply integrates all the animations into one seamless experience.</p>

<p>Let’s say that we want to move our button on the screen in a random fashion. Let’s see how we can use the keyframe animation API to do so.</p>

<div class="break-out">

<pre><code class="language-javascript">UIView.animateKeyframes(withDuration: 5, //1
  delay: 0, //2
  options: .calculationModeLinear, //3
  animations: { //4
    UIView.addKeyframe( //5
      withRelativeStartTime: 0.25, //6
      relativeDuration: 0.25) { //7
        self.button.center = CGPoint(x: self.view.bounds.midX, y: self.view.bounds.maxY) //8
    }

    UIView.addKeyframe(withRelativeStartTime: 0.5, relativeDuration: 0.25) {
        self.button.center = CGPoint(x: self.view.bounds.width, y: start.y)
    }

    UIView.addKeyframe(withRelativeStartTime: 0.75, relativeDuration: 0.25) {
        self.button.center = start
    }
})</code></pre>
</div>

<p>Here’s the breakdown:</p>

<ol>
<li><code>duration</code><br />Call the API by passing in the duration of the animation.</li>
<li><code>delay</code><br />Initial delay duration of the animation.</li>
<li><code>options</code><br />The type of animation curve that you want to apply to your view animation.</li>
<li><code>animations</code><br />Block that takes all keyframe animations designed by the developer/ user.</li>
<li><code>addKeyFrame</code><br />Call the API to design each and every animation. In our case, we have defined each move of the button. We can have as many such animations as we need, added to the block.</li>
<li><code>relativeStartTime</code><br />Defines the start time of the animation in the collection of the animation block.</li>
<li><code>relativeDuration</code><br />Defines the overall duration of this specific animation.</li>
<li><code>center</code><br />In our case, we simply change the center property of the button to move the button around the screen.</li>
</ol>

<p>And this is how the final animations looks like:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd184486-4b76-423c-b52b-0bf2ee99e121/3-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd184486-4b76-423c-b52b-0bf2ee99e121/3-performing-ios-animations-on-views-with-uikit-uiview.gif" width="600" height="" alt="" /></a></figure>

### CoreAnimation

<p>Any UIKit based animation is internally translated into core animations. Thus, the Core Animation framework acts as a backing layer or backbone for any UIKit animation. Hence, all UIKit animation APIs are nothing but encapsulated layers of the core animation APIs in an easily consumable or convenient fashion.</p>

<p>UIKit animation APIs don’t provide much control over animations that have been performed over a view since they are used mostly for animatable properties of the view. Hence in such cases, where you intend to have control over every frame of the animation, it is better to use the underlying core animation APIs directly. Alternatively, both the UIView animations and core animations can be used in conjunction as well.</p>

#### UIView + Core Animation

<p>Let’s see how we can recreate the same button change animation along with specifying the timing curve using the UIView and Core Animation APIs.</p>

<p>We can use <code>CATransaction</code>’s timing functions, which lets you specify and control the animation curve.</p>

<p>Let’s look at an example of a button size change animation with its corner radius utilizing the <code>CATransaction</code>’s timing function and a combination of UIView animations:</p>

<div class="break-out">

<pre><code class="language-javascript">let oldValue = button.frame.width/2
let newButtonWidth: CGFloat = 60

/&#42; Do Animations &#42;/
CATransaction.begin() //1
CATransaction.setAnimationDuration(2.0) //2
CATransaction.setAnimationTimingFunction(CAMediaTimingFunction(name: CAMediaTimingFunctionName.easeInEaseOut)) //3

// View animations //4
UIView.animate(withDuration: 1.0) {
    self.button.frame = CGRect(x: 0, y: 0, width: newButtonWidth, height: newButtonWidth)
    self.button.center = self.view.center
}

// Layer animations
let cornerAnimation = CABasicAnimation(keyPath: #keyPath(CALayer.cornerRadius)) //5
cornerAnimation.fromValue = oldValue //6
cornerAnimation.toValue = newButtonWidth/2 //7

button.layer.cornerRadius = newButtonWidth/2 //8
button.layer.add(cornerAnimation, forKey: #keyPath(CALayer.cornerRadius)) //9

CATransaction.commit() //10</code></pre>
</div>

<p>Here’s the breakdown:</p>

<ol>
<li><code>begin</code><br />Represents the start of the animation code block.</li>
<li><code>duration</code><br />Overall animation duration.</li>
<li><code>curve</code><br />Represents the timing curve that needs to be applied to the animation.</li>
<li><code>UIView.animate</code><br />Our first animation to change the frame of the button.</li>
<li><code>CABasicAnimation</code><br />We create the <code>CABasicAnimation</code> object by referring the <code>cornerRadius</code> of the button as the keypath since that’s what we want to animate. Similarly, if you want to have granular level control over the keyframe animations, then you can use the <code>CAKeyframeAnimation</code> class.</li>
<li><code>fromValue</code><br />Represents the starting value of the animation, i.e. the initial <code>cornerRadius</code> value of the button from where the animation must start off.</li>
<li><code>toValue</code><br />Represents the final value of the animation, i.e. the final <code>cornerRadius</code> value of the button where the animation must end.</li>
<li><code>cornerRadius</code><br />We must set the <code>cornerRadius</code> property of the button with the final value of the animation else the button’s cornerRadius value will get auto-reverted to its initial value after the animation completes.</li>
<li><code>addAnimation</code><br />We attach the animation object that contains the configuration of the entire animation process to the layer by representing the Keypath for which the animation needs to be performed.</li>
<li><code>commit</code><br />Represents the end of the animation code block and starts off the animation.</li>
</ol>

<p>This is how the final animation would look like:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2d35e91-8098-484f-9a97-2d645285ada8/4-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2d35e91-8098-484f-9a97-2d645285ada8/4-performing-ios-animations-on-views-with-uikit-uiview.gif" width="444" height="" alt="" /></a></figure>

<p><a href="https://academy.realm.io/posts/tryswift-tim-oliver-advanced-graphics-with-core-animation/">This blog</a> is a great read to help create more advanced animations as it neatly walks you through most of the Core Animation framework APIs with instructions guiding you through every step of the way.</p>

{{% ad-panel-leaderboard %}}

### UIKitDynamics

<p>UIKit Dynamics is the physics engine for UIKit which enables you to add any physics behaviors like collision, gravity, push, snap, etc, to the UIKit controls.</p>

#### UIKitDynamicAnimator

<p>This is the admin class of the UIKit Dynamics framework that regulates all animations triggered by any given UI control.</p>

#### UIKitDynamicBehavior

<p>It enables you to add any physics behavior to an animator which then enables it to perform on the view attached to it.</p>

<p>Different kinds of behaviors for UIKitDynamics include:</p>

<ul>
<li><code>UIAttachmentBehavior</code></li>
<li><code>UICollisionBehavior</code></li>
<li><code>UIFieldBehavior</code></li>
<li><code>UIGravityBehavior</code></li>
<li><code>UIPushBehavior</code></li>
<li><code>UISnapBehavior</code></li>
</ul>

<p>The architecture of UIKitDynamics looks something like <a href="https://www.techotopia.com/index.php/File:Uikit_dynamics_architecture.png">this</a>. Note that Items 1 to 5 can be replaced with a single view.</p>

<p>Let us apply some physics behavior to our button. We will see how to apply gravity to the button so that it gives us a feeling of dealing with a real object.</p>

<pre><code class="language-javascript">var dynamicAnimator   : UIDynamicAnimator!
var gravityBehavior   : UIGravityBehavior!

dynamicAnimator = UIDynamicAnimator(referenceView: self.view) //1

gravityBehavior = UIGravityBehavior(items: [button]) //2
dynamicAnimator.addBehavior(gravityBehavior) //3</code></pre>

<p>Here’s the breakdown:</p>

<ol>
<li><code>UIKitDynamicAnimator</code><br />We have created a <code>UIKitDynamicAnimator</code> object which acts as an orchestrator for performing animations. We have also passed the superview of our button as the reference view.</li>
<li><code>UIGravityBehavior</code><br />We have created a <code>UIGravityBehavior</code> object and pass our button into the array elements on which this behavior is injected.</li>
<li><code>addBehavior</code><br />We have added the gravity object to the animator.<br /><br />This should create an animation as shown below:<br />

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2bbd018-a7b2-4791-9df8-a27b35beb30a/5-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2bbd018-a7b2-4791-9df8-a27b35beb30a/5-performing-ios-animations-on-views-with-uikit-uiview.gif" width="600" height="" alt="" /></a><figcaption>Notice how the button falls off from the center (its original position) of the screen to the bottom and beyond.</figcaption></figure>

We should tell the animator to consider the bottom of the screen to be the ground. This is where <code>UICollisionBehavior</code> comes into picture.<br /><br />

<pre><code class="language-javascript">var dynamicAnimator   : UIDynamicAnimator!
var gravityBehavior   : UIGravityBehavior!
var collisionBehavior : UICollisionBehavior!

dynamicAnimator = UIDynamicAnimator(referenceView: self.view) //1

gravityBehavior = UIGravityBehavior(items: [button]) //2
dynamicAnimator.addBehavior(gravityBehavior) //3

collisionBehavior = UICollisionBehavior(items: [button]) //4
collisionBehavior.translatesReferenceBoundsIntoBoundary = true //5
dynamicAnimator.addBehavior(collisionBehavior) //6</code></pre>

</li>
  <li><code>UICollisionBehavior</code><br />We have created a <code>UICollisionBehavior</code> object and passed along the button so that the behavior is added to the element.</li>
  <li><code>translatesReferenceBoundsIntoBoundary</code><br />Enabling this property tells the animator to take the reference views boundary as the end, which is the bottom of the screen in our case.</li>
  <li><code>addBehavior</code><br />We have added collision behavior to the animator here.<br /><br />Now, our button should hit the ground and stand still as shown below:<br />

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0cb54de-33e1-4384-b3e8-c889e9603625/6-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0cb54de-33e1-4384-b3e8-c889e9603625/6-performing-ios-animations-on-views-with-uikit-uiview.gif" width="600" height="" alt="" /></a></figure>

<br />That’s pretty neat, isn’t it?<br /><br />Now, let us try adding a bouncing effect so that our object feels more real. To do that, we will use the <code>UIDynamicItemBehavior</code> class.<br />

<pre><code class="language-javascript">var dynamicAnimator   : UIDynamicAnimator!
var gravityBehavior   : UIGravityBehavior!
var collisionBehavior : UICollisionBehavior!
var bouncingBehavior  : UIDynamicItemBehavior!

dynamicAnimator = UIDynamicAnimator(referenceView: self.view) //1

gravityBehavior = UIGravityBehavior(items: [button]) //2
dynamicAnimator.addBehavior(gravityBehavior) //3

collisionBehavior = UICollisionBehavior(items: [button]) //4
collisionBehavior.translatesReferenceBoundsIntoBoundary = true //5
dynamicAnimator.addBehavior(collisionBehavior) //6

//Adding the bounce effect
bouncingBehavior = UIDynamicItemBehavior(items: [button]) //7
bouncingBehavior.elasticity = 0.75 //8
dynamicAnimator.addBehavior(bouncingBehavior) //9</code></pre>
</li>
  <li><code>UIDynamicItemBehavior</code><br />We have created a <code>UIDynamicItemBehavior</code> object and pass along the button so that the behavior is added to the element.</li>
  <li><code>elasticity</code><br />Value must be between 0-1, it represents the elasticity i.e. the number of times the object must bounce on and off the ground when it is hit. This is where the magic happens &mdash; by tweaking this property, you can differentiate between different kinds of objects like balls, bottles, hard-objects and so on.</li>
  <li><code>addBehavior</code><br />We have added collision behavior to the animator here.</li>
</ol>

<p>Now, our button should bounce when it hits the ground as shown below:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38dbb242-3a55-4592-8ce3-60a27657224f/7-performing-ios-animations-on-views-with-uikit-uiview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38dbb242-3a55-4592-8ce3-60a27657224f/7-performing-ios-animations-on-views-with-uikit-uiview.gif" width="600" height="" alt="" /></a></figure>

<p><a href="https://github.com/yudiz-solutions/UIKit-Dynamics">This repo</a> is quite helpful and shows all UIKitDynamics behaviors in action. It also provides source code to play around with each behavior. That, in my opinion, should serve as an extensive list of ways to perform iOS animations on views!</p>

<p>In the next section, we will take a brief look into the tools that will aid us in measuring the performance of animations. I would also recommend you to look at <a href="https://blog.flexiple.com/xcode-build-optimization-a-definitive-guide/">ways to optimize your Xcode build</a> since it will save a huge amount of your development time.</p>

## Performance Tuning

<p>In this section, we will look at ways to measure and tune the performance of iOS animations. As an iOS developer, you might have already used Xcode Instruments like Memory Leaks and Allocations for measuring the performance of the overall app. Similarly, there are instruments that can be used to measure the performance of animations.</p>

### <code>Core Animation</code> Instrument

<p>Try the <code>Core Animation</code> instrument and you should be able to see the FPS that your app screen delivers. This is a great way to measure the performance/ speed of any animation rendered in your iOS app.</p>

### Drawing

<p>FPS is vastly lowered in the app that displays heavy content like images with effects like shadows. In such cases, instead of assigning the Image directly to the <code>UIImageView</code>’s image property, try to draw the image separately in a context using Core Graphics APIs. This overly reduces the image display time by performing the image decompression logic asynchronously when done in a separate thread instead of the main thread.</p>

### Rasterization

<p>Rasterization is a process used to cache complex layer information so that these views aren’t redrawn whenever they’re rendered. Redrawing of views is the major cause of the reduction in FPS and hence, it is best to apply rasterization on views that are going to be reused several times.</p>

## Wrapping Up

<p>To conclude, I have also summed up a <a href="https://blog.flexiple.com/the-ultimate-list-of-resources-for-ios-animations/">list of useful resources for iOS animations</a>. You may find this very handy when working on iOS animations. Additionally, you may also find <a href="https://www.remote.tools/category/Design-Collaboration">this set of design tools</a> helpful as a (design) step before delving into animations.</p>

<p>I hope I have been able to cover as many topics as possible surrounding iOS animations. If there is anything I may have missed out in this article, please let me know in the comments section below and I would be glad to make the addition!</p>

{{< signature "dm, yk, il" >}}
