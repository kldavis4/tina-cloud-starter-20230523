---
title: A Swift Transition From iOS To macOS Development
slug: from-ios-to-macos-development
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ed192c8-03b9-473e-826a-26d3e72e658b/01-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg
date: 2017-10-30T16:15:35.000Z
author: marcvandehey
description: >-
  Today started just like any other day. You sat down at your desk, took a sip
  of coffee and opened up Xcode to start a new project. But wait! The
  similarities stop there. Today, we will try to build for a different platform!
  Don’t be afraid. I know you are comfortable there on your iOS island, knocking
  out iOS applications, but **today begins a brand new adventure**. Today is the
  day we head on over to macOS development, a dark and scary place that you know
  nothing about.

  The good news is that developing for macOS using Swift has a lot more in
  common with iOS development than you realize. To prove this, I will walk you
  through building a simple screen-annotation application. Once we complete it,
  you will realize how easy it is to build applications for macOS.
categories:
  - Mobile
  - iOS
  - Swift
---
The good news is that developing for macOS using Swift has a lot more in common with iOS development than you realize. To prove this, I will walk you through building a simple screen-annotation application. Once we complete it, you will realize how easy it is to build applications for macOS.</p>

## The Concept

The idea comes from two unlikely sources. The first source is my boss, <a href="https://www.thirteen23.com/about/#doug-cook">Doug Cook</a>. He came over and asked if I knew how to make a circular floating app on macOS for prototyping purposes. Having never really done anything on macOS, I started to do some digging. After a little digging, I found Apple’s little gem of <a href="https://developer.apple.com/library/content/samplecode/RoundTransparentWindow/Introduction/Intro.html">RoundTransparentWindow</a>. Sure, it was in Objective-C, and it was pre-ARC to boot, but after reading through the code, I saw that figuring out how to do it in Swift wasn’t very difficult. The second source was pure laziness. I recently picked up a side project making <a href="https://www.youtube.com/channel/UCDkvBXNhfeQwSksBNMutaeA/featured">tutorial videos on YouTube</a>. I wanted to be able to describe what I was saying by drawing directly on the screen, without any post-production.

I decided to build a macOS app to draw on the computer screen:

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070e4777-7d0d-451b-8b97-c8e6d1abb676/08-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b34e1b-f40d-4d1b-8884-3c4c14739c0e/08-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Behold the app in all its glory!" width="800" height="500" /></a><figcaption>Behold the app in all its glory! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070e4777-7d0d-451b-8b97-c8e6d1abb676/08-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

OK, it doesn’t look like much — and, honestly, it shouldn’t because I haven’t drawn anything. If you look closely at the image above, you will see a little pencil icon in the upper-right bar. This area of macOS contains items called “<a href="https://en.wikipedia.org/wiki/Menu_extra">menu extras</a>.” By clicking the pencil icon, you will enable drawing on screen, and then you can draw something like this below!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ab7d1b-cf13-4365-9bfd-93d25df93511/09-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3db7490-e08c-4a5c-8eb8-9e65d0ecb024/09-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Behold the app in all its glory, again!" width="800" height="500" /></a><figcaption>Behold the app in all its glory, again! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ab7d1b-cf13-4365-9bfd-93d25df93511/09-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

I wanted drawing on the screen to be enabled at all times, but not to take over the screen when not in use. I preferred that it not live in the dock, nor change the contents of macOS’ menu bar. I knew that it was possible because I’d seen it in other apps. So, over lunch one day, I decided to take a crack at building this drawing tool, and here we are! This is what we will build in this tutorial.</p>

### The Soapbox

At this point, you might be saying to yourself, “Why build this? It's just a simple drawing app!” But that isn’t the point. If you are anything like me, you are a little intimidated by the thought of making a macOS app. Don't be. If you program for your iPhone on your MacBook, shouldn't you also be able to program for your MacBook on your MacBook? What if Apple actually does merge iOS and macOS? Should you be left behind because you were intimidated by macOS development? ChromeOS already supports Android builds. How long before macOS supports iOS builds? There are differences between Cocoa and UIKit, which will become apparent, but this tutorial will get your feet wet and (hopefully) challenge you to build something bigger and better.</p>

### Caveats and Requirements

There are some caveats to this project that I want to get out of the way before we start. We will be making an app that draws over the entire screen. This will work on only one screen (for now) and will not work as is over full-screen apps. For our purpose, this is enough, and it leaves open room for plenty of enhancements in future iterations of the project. In fact, if you have any ideas for enhancements of your own, please leave them in the comments at the bottom!

For this tutorial, you’ll need a basic understanding of Swift development and familiarity with storyboards. We will also be doing this in Xcode 9 because that is the latest and greatest version at the time of writing.</p>

## 1\. Begin A macOS Project

Open Xcode and create a new macOS project. At this point, you are probably still in the “iOS” style project. We have to update this so that we are building for the correct system. Hit the “macOS” icon at the top, and then make sure that “Cocoa App” is selected. Hit “Next.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ed192c8-03b9-473e-826a-26d3e72e658b/01-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ed192c8-03b9-473e-826a-26d3e72e658b/01-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg" alt="Create a new macOS project" width="731" height="527" /></a><figcaption>Create a new macOS project.</figcaption></figure>

Enter in the product name as you normally would. We will call this one <code>ScreenAnnotation</code>, and then do the normal dance with “organization name” and “team” that you’d normally do. Make sure to select Swift as the language, and again hit “Next.” After saving it in the directory of your choosing, you will have your very own macOS app. Congratulations!

At first glance, you will see most everything you get in an iOS app. The only differences you might notice right now are the entitlements file, Cocoa in place of UIKit in each of the <code>.swift</code> files, and (naturally) the contents of the storyboard.

## 2\. Clean Up

Our next step is to go into the storyboard and delete anything we don’t need. First, let’s get rid of the menu; because our app will live as a menu extra, instead of as a dock app, it is unnecessary. Beneath where the menu existed is the window. We need to subclass this and use it to determine whether we are drawing within our app or toying with windows beneath it. Looking below the window, we can also see the familiar view controller. We already have a subclass of this, provided by Xcode. It is aptly named <code>ViewController</code> because it is a subclass of <code>NSViewController</code>, but we still need a <code>NSWindow</code> subclass, so that we can decorate it as a clear window. Head over to the left pane, right-click, select “New file,” then select “Swift” file. When prompted, name this <code>ClearWindow</code>. Replace the one line with the following:

<pre><code class="language-markup">import Cocoa

class ClearWindow : NSWindow {
  override init(contentRect: NSRect, styleMask style: NSWindow.StyleMask, backing backingStoreType: NSWindow.BackingStoreType, defer flag: Bool) {
    super.init(contentRect: contentRect, styleMask: StyleMask.borderless, backing: backingStoreType, defer: flag)

    level = NSWindow.Level.statusBar

    backgroundColor = NSColor.blue
  }

  override func mouseDown(with event: NSEvent) {
    print("Mouse down: \(event.locationInWindow)")
  }

  override func mouseDragged(with event: NSEvent) {
    print("Mouse dragged: \(event.locationInWindow)")
  }

  override func mouseUp(with event: NSEvent) {
    print("Mouse up: \(event.locationInWindow)")
  }
}</code></pre>

In this code snippet, we are importing Cocoa, which is to macOS as UIKit is to iOS development. This is the main API we will use to control our app. After importing Cocoa, we subclass NSWindow, and then we update our super-call in the <code>init</code> method. In here, we keep the same <code>contentRect</code> but will modify this later. We change the <code>styleMask</code> to <code>borderless</code>, which removes the standard application options: close, minimize and maximize. It also removes the top bar on the window. You can also do this in the storyboard file, but we are doing it here to show what it would look like to do it programmatically. Next, we pass the other variables right on through to the constructor. Now that we have that out of the way, we need to tell our window where to draw. We will set the window level to <code>NSStatusWindowLevel</code> because it will draw above all other normal windows.</p>

## 3\. Our First Test

We are using <a href="https://developer.apple.com/documentation/appkit/nsresponder#contenttable-section-title">NSResponder methods</a> in the same way that we’d use the <code>UIResponder</code> method to respond to touches on iOS. On macOS, we are interested in mouse events. Later on, we will be using these methods to draw in our <code>ViewController</code>.

Finally, we’ll change the color of our view to blue, just to make sure things are running smoothly; if we went straight to a transparent view, we wouldn’t know where the window was drawn yet! Next, we need to set up the storyboard to use our new <code>ClearWindow</code> class, even though it isn’t living up to its name yet. Go back to the storyboard, click the window, and edit its subclass under the “Custom Class” area in the right pane. Type in <code>ClearWindow</code> here, and we can now run our app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96f68a99-c014-4e6e-a707-4c2c990244a5/02-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96f68a99-c014-4e6e-a707-4c2c990244a5/02-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg" alt="Type in ClearWindow" width="526" height="266" /></a><figcaption>Type in <code>ClearWindow</code></figcaption></figure>

Lo and behold, we have a blue rectangle on our screen! Nothing impressive, yet. We can click and drag around, and we can spam the console. Let’s stop running the app at this point because it will only get in the way.

## 4\. Let’s Start Drawing!

Next, we can update our implementation of <code>ViewController</code>. The bulk of our work will now happen here and in <code>Main.storyboard</code>. Right now, the important part is to piggyback on the methods that we created in <code>ClearWindow</code> to capture mouse gestures. Replace the contents of <code>ViewController</code> with the following code:

<pre><code class="language-markup">import Cocoa

class ViewController: NSViewController {
  override func viewDidLoad() {
    super.viewDidLoad()

    view.frame = CGRect(origin: CGPoint(), size: NSScreen.main!.visibleFrame.size)
  }

  func startDrawing(at point: NSPoint) {
  }

  func continueDrawing(at point: NSPoint) {
  }

  func endDrawing(at point: NSPoint) {
  }
}
</code></pre>

This does not look like much yet, but it is the foundation of our drawing code. In our modified <code>viewDidLoad()</code> method, we’ve resized the view to equal our main screen’s dimension. We do this because we can only draw within our <code>NSViewController</code>. If our view covered everything, then we’d be able to draw over anything! Finally, we’ve created hooks that, for <code>ClearWindow</code>, will call for the <code>ViewController</code> to draw. More on that in a bit.

The next thing we need to do is define how we will draw onto the screen. Add the following code above our <code>viewDidLoad</code> method.</p>

<pre><code class="language-markup">let lineWeight: CGFloat = 10
let strokeColor: NSColor = .red
var currentPath: NSBezierPath?
var currentShape: CAShapeLayer?
</code></pre>

These four variables define our drawing. Currently, our line thickness is 10 points, and we will be drawing in red — nothing revolutionary here, but that needs to be defined. Next, we have a <code>NSBezierPath</code> and a <code>CAShapeLayer</code>. These should look pretty familiar if you have ever played with <a href="https://developer.apple.com/documentation/uikit/uibezierpath">UIBezierPath</a>. Note that these two are optional (they will come up again later).

Now for the fun part: We can start implementing our drawing methods.</p>

### Start Drawing

Update <code>startDrawing</code> with the following code:

<pre><code class="language-markup">func startDrawing(at point: NSPoint) {
  currentPath = NSBezierPath()
  currentShape = CAShapeLayer()

  currentShape?.lineWidth = lineWeight
  currentShape?.strokeColor = strokeColor.cgColor
  currentShape?.fillColor = NSColor.clear.cgColor

  currentShape?.lineJoin = kCALineJoinRound
  currentShape?.lineCap = kCALineCapRound

  currentPath?.move(to: point)
  currentPath?.line(to: point)

  currentShape?.path = currentPath?.cgPath

  view.layer?.addSublayer(currentShape!)
}
</code></pre>

This is the most complicated of the three drawing methods. The reason for this is that we need to set up a new <code>NSBezierPath</code> and <code>CAShapeLayer</code> each time we start drawing. This is important because we don’t want to have one continuous line all over our screen — that wouldn’t do at all. This way, we can have one layer per line, and we will be able to make any kind of drawing we want. Then, we set up the newly created <code>CAShapeLayer</code>’s properties. We send in our <code>lineWeight</code> and then the stroke color to our nice red color. We set the fill color to clear, which means we will only be drawing with lines, instead of solid shapes. Then, we set the <code>lineJoin</code> and <code>lineCap</code> to use rounded edges. I chose this because the rounded edges make the drawing look nicer in my opinion. Feel free to play with these properties to figure out what works best for you.

Then, we move the point where we will start drawing to the <code>NSPoint</code> that will be sent to us. This will not draw anything, but it will give the <code>UIBezierPath</code> a reference point for when we actually give it instructions to draw. Think of it as if you had a pen in your hand and you decided to draw something in the middle of a sheet of paper. You move the pen to the location you want to draw, but you’re not doing anything yet, just hovering over the paper, waiting to put the ink down. Without this, nothing can be drawn because the next line requires two points to work. The next line, aptly named <code>line(to: point)</code>, draws a line from the current position to wherever you specify. Currently, we’re telling our <code>UIBezierPath</code> to stay in the same position and touch down on our sheet of paper.

The last two lines pull the path data out of our <code>UIBezierPath</code> in a usable format for <code>CAShapeLayer</code>. Note that <code>currentPath?.cgPath</code> will be marked as an error at the moment. Don’t fret: We will take care of that after we cover the next two methods. Just know that when it does work, this function will have our <code>CAShapeLayer</code> draw its path, even if it is currently a dot. Then, we add this layer to our view’s sublayer. At this point, the user will be able to see that they are now drawing.</p>

### Continue Drawing

Update <code>continueDrawing</code> with the following code:

<pre><code class="language-markup">func continueDrawing(at point: NSPoint) {
  currentPath?.line(to: point)

  if let shape = currentShape {
    shape.path = currentPath?.cgPath
  }
}
</code></pre>

Not much going on here, but we are adding another line to our <code>currentPath</code>. Because the <code>CAShapeLayer</code> is already in our view’s sublayer, the update will show on screen. Again, note that these are optional values; we are guarding ourselves just in case they are nil.</p>

### End Drawing

Update <code>endDrawing</code> with the following code:

<pre><code class="language-markup">func endDrawing(at point: NSPoint) {
  currentPath?.line(to: point)

  if let shape = currentShape {
    shape.path = currentPath?.cgPath
  }

  currentPath = nil
  currentShape = nil
}
</code></pre>

We update the path again, just the same way as we did in <code>continueDrawing</code>, but then we also nil out our <code>currentPath</code> and <code>currentShape</code>. We do this because we are done drawing and no longer need to talk to this shape and path. The next action we can take is <code>startDrawing</code> again, and we start this process all over again. We nil out these values so that we cannot update them again; the view’s sublayer will still hold a reference to the line, and it will stay on screen until we remove it.

If we run the app with what we have, we’ll get errors! Almost forgot about that. One thing you will definitely notice when moving over to macOS development is that not every API between iOS and macOS are equivalent. One such issue here is that <code>NSBezierPath</code> doesn’t have the handy <code>cgPath</code> property that <code>UIBezierPath</code> has. We use this property to easily convert the <code>NSBezierPath</code> path to the <code>CAShapeLayer</code> path. This way, <code>CAShapeLayer</code> will do all the heavy lifting to display our line. We can sit back and reap the reward of a nice-looking line with none of the work! StackOverflow has a <a href="https://stackoverflow.com/questions/1815568/how-can-i-convert-nsbezierpath-to-cgpath/38860552#38860552">handy answer</a> that I’ve used to handle this absence of <code>cgPath</code> by updating it to Swift 4 (see below). This code lets us create an extension to <code>NSBezierPath</code> and returns to us a handy <code>CGPath</code> to play with. Create a file named <code>NSBezierPath+CGPath.swift</code> and add the following code to it.</p>

<pre><code class="language-markup">import Cocoa

extension NSBezierPath {
  public var cgPath: CGPath {
    let path = CGMutablePath()
    var points = [CGPoint](repeating: .zero, count: 3)

    for i in 0 ..&lt; self.elementCount {
      let type = self.element(at: i, associatedPoints: &amp;points)
      switch type {
      case .moveToBezierPathElement:
        path.move(to: points[0])
      case .lineToBezierPathElement:
        path.addLine(to: points[0])
      case .curveToBezierPathElement:
        path.addCurve(to: points[2], control1: points[0], control2: points[1])
      case .closePathBezierPathElement:
        path.closeSubpath()
      }
    }

    return path
  }
}
</code></pre>

At this point, everything will run, but we aren’t drawing anything quite yet. We still need to attach the drawing functions to actual mouse actions. In order to do this, we go back into our <code>ClearWindow</code> and update the <code>NSResponder</code> mouse methods to the following:

<pre><code class="language-markup"> override func mouseDown(with event: NSEvent) {
    (contentViewController as? ViewController)?.startDrawing(at: event.locationInWindow)
  }

  override func mouseDragged(with event: NSEvent) {
    (contentViewController as? ViewController)?.continueDrawing(at: event.locationInWindow)
  }

  override func mouseUp(with event: NSEvent) {
    (contentViewController as? ViewController)?.endDrawing(at: event.locationInWindow)
  }
</code></pre>

This basically checks to see whether the current view controller is our instance of <code>ViewController</code>, where we will handle the drawing logic. If you run the app now, you should see something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444b1be-1efd-4f45-ac64-158802b17598/03-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46062087-ce95-4281-aaf9-7a38783623c9/03-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="The app as it is now" width="800" height="450" /></a><figcaption>The app as it is now (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444b1be-1efd-4f45-ac64-158802b17598/03-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

This is not completely ideal, but we are currently able to draw on the blue portion of our screen. This means that our drawing logic is correct, but our layout is not. Before correcting our layout, let’s create a good way to quit, or disable, drawing on our app. If we make it full screen right now, we would either have to “force quit” or switch to another space to quit our app.</p>

## 5\. Create A Menu

Head back over to our <code>Main.storyboard</code> file, where we can add a new menu to our <code>ViewController</code>. In the right pane, drag “Menu” under the “View Controller Scene” in our storyboard’s hierarchy.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e4bb2d7-a77b-4592-aed8-01074d5e83d0/04-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a56967-e93a-4eb4-b73c-6536229bc3a6/04-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Setting up the menu" width="800" height="358" /></a><figcaption>Setting up the menu (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e4bb2d7-a77b-4592-aed8-01074d5e83d0/04-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

Edit these menu items to say “Clear,” “Toggle” and “Quit.” For extra panache, we can add a line separator above our “Exit” item, to deter accidental clicks:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d591c14f-421e-41e3-a950-eed57f6ccf00/05-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57709447-8093-49e3-8bc8-2a0dc7d86f7f/05-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Creating menu options" width="800" height="422" /></a><figcaption>Creating menu options (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d591c14f-421e-41e3-a950-eed57f6ccf00/05-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

Next, open up the “Assistant Editor” (the Venn diagram-looking button near the top right of Xcode), so that we can start hooking up our menu items. For both “Clear” and “Toggle,” we want to create a “Referencing Outlet” so that we can modify them. After this, we want to hook up “Sent Action” so that we can get a callback when the menu item is selected.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b573f81-be7b-4d14-804d-27704a68f792/06-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44f45f11-a5d7-4c77-8301-6cad73d01c8f/06-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Hooking up the code to the buttons" width="800" height="379" /></a><figcaption>Hooking up the code to the buttons (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b573f81-be7b-4d14-804d-27704a68f792/06-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

For “Exit,” we will drag our “Sent Action” to the first responder, and select “Terminate.” “Terminate” is a canned action that will quit the application. Finally, we need a reference to the menu itself; so, right-click on the menu under “View Controller Scene,” and create a reference named <code>optionsMenu</code>. The newly added code in <code>ViewController</code> should look like this:

<pre><code class="language-markup">@IBOutlet weak var clearButton: NSMenuItem!
@IBOutlet weak var toggleButton: NSMenuItem!
@IBOutlet var optionsMenu: NSMenu!

@IBAction func clearButtonClicked(_ sender: Any) {
}

@IBAction func toggleButtonClicked(_ sender: Any) {
}
</code></pre>

We have the building blocks for the menu extras for our app; now we need to finish the process. Close out of “Assistant Editor” mode and head over to <code>ViewController</code> so that we can make use of these menu buttons. First, we will add the following strings to drive the text of the toggle button. Add the following two lines near the top of the file.</p>

<pre><code class="language-markup">private let offText = "Disable Drawing"
private let onText = "Enable Drawing"</code></pre>

We need to update what happens when the clear and toggle buttons are clicked. Add the following line to clear the drawing in <code>clearButtonClicked(_ sender)</code>:

<pre><code class="language-markup">view.window!.ignoresMouseEvents = !view.window!.ignoresMouseEvents
toggleButton.title = view.window!.ignoresMouseEvents ? onText : offText</code></pre>

This toggles the flag on our window to ignore mouse events, so that we will click “through” our window, in order to use our computer as intended. We’ll also update the <code>toggleButton</code>’s text to let the user know that drawing is either enabled or disabled.

Now we need to finally put our menu to use. Let’s start by adding an icon to our project. You can find that <a href="https://github.com/thirteen23/ScreenAnnotation/blob/master/pencil.zip">in the repository</a>. Then, we can override the <code>awakeFromNib()</code> method because, at this point, our view will be inflated from the storyboard. Add the following code to <code>ViewController</code>.</p>

<pre><code class="language-markup">let statusItem = NSStatusBar.system.statusItem(withLength: NSStatusItem.variableLength)

override func awakeFromNib() {
  statusItem.menu = optionsMenu
  let icon = NSImage(named: NSImage.Name(rawValue: "pencil"))
  icon?.isTemplate = true // best for dark mode
  statusItem.image = icon

  toggleButton.title = offText
}</code></pre>

Make sure to put the <code>statusItem</code> near the top, next to the rest of the variables. <code>statusItem</code> grabs a spot for our app to use menu extras in the top toolbar. Then, in <code>awakeFromNib</code>, we set the menu as our <code>optionsMenu</code>, and, finally, we give it an icon, so that it is easily identifiable and clickable. If we run our app now, the “menu extra” icon will appear at the top! We aren’t quite finished yet. We need to ensure that the drawing space is placed correctly on screen; otherwise, it will be only partially useful.</p>

## 6\. Positioning The Drawing App

To get our view to draw where we want it, we must venture back into <code>Main.storyboard</code>. Click on the window itself, and then select the attributes inspector, the icon fourth from the left in the right-hand pane. Uncheck everything under the “Appearance,” “Controls” and “Behavior” headings, like so:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7912fcc1-ddd8-4136-8483-fc6c070ad2a3/07-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7912fcc1-ddd8-4136-8483-fc6c070ad2a3/07-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg" alt="Attributes inspector" width="249" height="380" /></a><figcaption>Attributes inspector</figcaption></figure>

We do this to remove all extra behaviors and appearances. We want a clear screen, with no bells and whistles. If we run the app again, we will be greeted by a familiar blue screen, only larger. To make things useful, we need to change the color from blue to transparent. Head back over to <code>ClearWindow</code> and update the blue color to this:

<pre><code class="language-markup">backgroundColor = NSColor(calibratedRed: 1, green: 1, blue: 1, alpha: 0.001)</code></pre>

This is pretty much the same as <code>NSColor.clear</code>. The reason why we are not using <code>NSColor.clear</code> is that if our entire app is transparent, then macOS won’t think our app is visible, and no clicks will be captured in the app. We’ll go with a mostly transparent app — something that, at least to me, is not noticeable, yet our clicks will be recorded correctly.

The final thing to do is remove it from our dock. To do this, head over to <code>Info.plist</code> and add a new row, named “Application is agent (UIElement)” and set it to “Yes.” Once this is done, rerun the app, and it will no longer appear in the dock!

## Conclusion

This app is pretty short and sweet, but we did learn a few things. First, we figured out some of the similarities and differences between UIKit and Cocoa. We also took a tour around what Cocoa has in store for us iOS developers. We also (hopefully) know that creating a Cocoa-based app is not difficult, nor should it be intimidating. We now have a small app that is presented in an atypical fashion, and it lives up in the menu bar, next to the menu extras. Finally, we can use all of this stuff to build bigger and better Cocoa apps! You started this article as an iOS developer and grew beyond that, becoming an <em>Apple</em> developer. Congratulations!

I will be updating the <a href="https://github.com/thirteen23/ScreenAnnotation">public repository</a> for this example to add extra options. Keep an eye on the repository, and feel free to add code, issues and comments.

Good luck and happy programming!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cff6f87-7454-4198-b518-5257d368a9f7/thank-you.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cff6f87-7454-4198-b518-5257d368a9f7/thank-you.gif" alt="Attributes inspector" width="500" height="312" /></a><figcaption>Thank you!</figcaption></figure>

This does not look like much yet, but it is the foundation of our drawing code. In our modified <code>viewDidLoad()</code> method, we’ve resized the view to equal our main screen’s dimension. We do this because we can only draw within our <code>NSViewController</code>. If our view covered everything, then we’d be able to draw over anything! Finally, we’ve created hooks that, for <code>ClearWindow</code>, will call for the <code>ViewController</code> to draw. More on that in a bit.

The next thing we need to do is define how we will draw onto the screen. Add the following code above our <code>viewDidLoad</code> method.</p>

<pre><code class="language-markup">let lineWeight: CGFloat = 10
let strokeColor: NSColor = .red
var currentPath: NSBezierPath?
var currentShape: CAShapeLayer?
</code></pre>

These four variables define our drawing. Currently, our line thickness is 10 points, and we will be drawing in red — nothing revolutionary here, but that needs to be defined. Next, we have a <code>NSBezierPath</code> and a <code>CAShapeLayer</code>. These should look pretty familiar if you have ever played with <a href="https://developer.apple.com/documentation/uikit/uibezierpath">UIBezierPath</a>. Note that these two are optional (they will come up again later).

Now for the fun part: We can start implementing our drawing methods.</p>

### Start Drawing

Update <code>startDrawing</code> with the following code:

<pre><code class="language-markup">func startDrawing(at point: NSPoint) {
  currentPath = NSBezierPath()
  currentShape = CAShapeLayer()

  currentShape?.lineWidth = lineWeight
  currentShape?.strokeColor = strokeColor.cgColor
  currentShape?.fillColor = NSColor.clear.cgColor

  currentShape?.lineJoin = kCALineJoinRound
  currentShape?.lineCap = kCALineCapRound

  currentPath?.move(to: point)
  currentPath?.line(to: point)

  currentShape?.path = currentPath?.cgPath

  view.layer?.addSublayer(currentShape!)
}
</code></pre>

This is the most complicated of the three drawing methods. The reason for this is that we need to set up a new <code>NSBezierPath</code> and <code>CAShapeLayer</code> each time we start drawing. This is important because we don’t want to have one continuous line all over our screen — that wouldn’t do at all. This way, we can have one layer per line, and we will be able to make any kind of drawing we want. Then, we set up the newly created <code>CAShapeLayer</code>’s properties. We send in our <code>lineWeight</code> and then the stroke color to our nice red color. We set the fill color to clear, which means we will only be drawing with lines, instead of solid shapes. Then, we set the <code>lineJoin</code> and <code>lineCap</code> to use rounded edges. I chose this because the rounded edges make the drawing look nicer in my opinion. Feel free to play with these properties to figure out what works best for you.

Then, we move the point where we will start drawing to the <code>NSPoint</code> that will be sent to us. This will not draw anything, but it will give the <code>UIBezierPath</code> a reference point for when we actually give it instructions to draw. Think of it as if you had a pen in your hand and you decided to draw something in the middle of a sheet of paper. You move the pen to the location you want to draw, but you’re not doing anything yet, just hovering over the paper, waiting to put the ink down. Without this, nothing can be drawn because the next line requires two points to work. The next line, aptly named <code>line(to: point)</code>, draws a line from the current position to wherever you specify. Currently, we’re telling our <code>UIBezierPath</code> to stay in the same position and touch down on our sheet of paper.

The last two lines pull the path data out of our <code>UIBezierPath</code> in a usable format for <code>CAShapeLayer</code>. Note that <code>currentPath?.cgPath</code> will be marked as an error at the moment. Don’t fret: We will take care of that after we cover the next two methods. Just know that when it does work, this function will have our <code>CAShapeLayer</code> draw its path, even if it is currently a dot. Then, we add this layer to our view’s sublayer. At this point, the user will be able to see that they are now drawing.</p>

### Continue Drawing

Update <code>continueDrawing</code> with the following code:

<pre><code class="language-markup">func continueDrawing(at point: NSPoint) {
  currentPath?.line(to: point)

  if let shape = currentShape {
    shape.path = currentPath?.cgPath
  }
}
</code></pre>

Not much going on here, but we are adding another line to our <code>currentPath</code>. Because the <code>CAShapeLayer</code> is already in our view’s sublayer, the update will show on screen. Again, note that these are optional values; we are guarding ourselves just in case they are nil.</p>

### End Drawing

Update <code>endDrawing</code> with the following code:

<pre><code class="language-markup">func endDrawing(at point: NSPoint) {
  currentPath?.line(to: point)

  if let shape = currentShape {
    shape.path = currentPath?.cgPath
  }

  currentPath = nil
  currentShape = nil
}
</code></pre>

We update the path again, just the same way as we did in <code>continueDrawing</code>, but then we also nil out our <code>currentPath</code> and <code>currentShape</code>. We do this because we are done drawing and no longer need to talk to this shape and path. The next action we can take is <code>startDrawing</code> again, and we start this process all over again. We nil out these values so that we cannot update them again; the view’s sublayer will still hold a reference to the line, and it will stay on screen until we remove it.

If we run the app with what we have, we’ll get errors! Almost forgot about that. One thing you will definitely notice when moving over to macOS development is that not every API between iOS and macOS are equivalent. One such issue here is that <code>NSBezierPath</code> doesn’t have the handy <code>cgPath</code> property that <code>UIBezierPath</code> has. We use this property to easily convert the <code>NSBezierPath</code> path to the <code>CAShapeLayer</code> path. This way, <code>CAShapeLayer</code> will do all the heavy lifting to display our line. We can sit back and reap the reward of a nice-looking line with none of the work! StackOverflow has a <a href="https://stackoverflow.com/questions/1815568/how-can-i-convert-nsbezierpath-to-cgpath/38860552#38860552">handy answer</a> that I’ve used to handle this absence of <code>cgPath</code> by updating it to Swift 4 (see below). This code lets us create an extension to <code>NSBezierPath</code> and returns to us a handy <code>CGPath</code> to play with. Create a file named <code>NSBezierPath+CGPath.swift</code> and add the following code to it.</p>

<pre><code class="language-markup">import Cocoa

extension NSBezierPath {
  public var cgPath: CGPath {
    let path = CGMutablePath()
    var points = [CGPoint](repeating: .zero, count: 3)

    for i in 0 ..&lt; self.elementCount {
      let type = self.element(at: i, associatedPoints: &amp;points)
      switch type {
      case .moveToBezierPathElement:
        path.move(to: points[0])
      case .lineToBezierPathElement:
        path.addLine(to: points[0])
      case .curveToBezierPathElement:
        path.addCurve(to: points[2], control1: points[0], control2: points[1])
      case .closePathBezierPathElement:
        path.closeSubpath()
      }
    }

    return path
  }
}
</code></pre>

At this point, everything will run, but we aren’t drawing anything quite yet. We still need to attach the drawing functions to actual mouse actions. In order to do this, we go back into our <code>ClearWindow</code> and update the <code>NSResponder</code> mouse methods to the following:

<pre><code class="language-markup"> override func mouseDown(with event: NSEvent) {
    (contentViewController as? ViewController)?.startDrawing(at: event.locationInWindow)
  }

  override func mouseDragged(with event: NSEvent) {
    (contentViewController as? ViewController)?.continueDrawing(at: event.locationInWindow)
  }

  override func mouseUp(with event: NSEvent) {
    (contentViewController as? ViewController)?.endDrawing(at: event.locationInWindow)
  }
</code></pre>

This basically checks to see whether the current view controller is our instance of <code>ViewController</code>, where we will handle the drawing logic. If you run the app now, you should see something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444b1be-1efd-4f45-ac64-158802b17598/03-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46062087-ce95-4281-aaf9-7a38783623c9/03-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="The app as it is now" width="800" height="450" /></a><figcaption>The app as it is now (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444b1be-1efd-4f45-ac64-158802b17598/03-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

This is not completely ideal, but we are currently able to draw on the blue portion of our screen. This means that our drawing logic is correct, but our layout is not. Before correcting our layout, let’s create a good way to quit, or disable, drawing on our app. If we make it full screen right now, we would either have to “force quit” or switch to another space to quit our app.</p>

## 5\. Create A Menu

Head back over to our <code>Main.storyboard</code> file, where we can add a new menu to our <code>ViewController</code>. In the right pane, drag “Menu” under the “View Controller Scene” in our storyboard’s hierarchy.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e4bb2d7-a77b-4592-aed8-01074d5e83d0/04-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a56967-e93a-4eb4-b73c-6536229bc3a6/04-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Setting up the menu" width="800" height="358" /></a><figcaption>Setting up the menu (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e4bb2d7-a77b-4592-aed8-01074d5e83d0/04-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

Edit these menu items to say “Clear,” “Toggle” and “Quit.” For extra panache, we can add a line separator above our “Exit” item, to deter accidental clicks:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d591c14f-421e-41e3-a950-eed57f6ccf00/05-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57709447-8093-49e3-8bc8-2a0dc7d86f7f/05-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Creating menu options" width="800" height="422" /></a><figcaption>Creating menu options (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d591c14f-421e-41e3-a950-eed57f6ccf00/05-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

Next, open up the “Assistant Editor” (the Venn diagram-looking button near the top right of Xcode), so that we can start hooking up our menu items. For both “Clear” and “Toggle,” we want to create a “Referencing Outlet” so that we can modify them. After this, we want to hook up “Sent Action” so that we can get a callback when the menu item is selected.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b573f81-be7b-4d14-804d-27704a68f792/06-a-swift-transition-from-ios-to-macos-development-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44f45f11-a5d7-4c77-8301-6cad73d01c8f/06-a-swift-transition-from-ios-to-macos-development-800w-opt.jpg" alt="Hooking up the code to the buttons" width="800" height="379" /></a><figcaption>Hooking up the code to the buttons (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b573f81-be7b-4d14-804d-27704a68f792/06-a-swift-transition-from-ios-to-macos-development-large-opt.jpg">View large version</a>)</figcaption></figure>

For “Exit,” we will drag our “Sent Action” to the first responder, and select “Terminate.” “Terminate” is a canned action that will quit the application. Finally, we need a reference to the menu itself; so, right-click on the menu under “View Controller Scene,” and create a reference named <code>optionsMenu</code>. The newly added code in <code>ViewController</code> should look like this:

<pre><code class="language-markup">@IBOutlet weak var clearButton: NSMenuItem!
@IBOutlet weak var toggleButton: NSMenuItem!
@IBOutlet var optionsMenu: NSMenu!

@IBAction func clearButtonClicked(_ sender: Any) {
}

@IBAction func toggleButtonClicked(_ sender: Any) {
}
</code></pre>

We have the building blocks for the menu extras for our app; now we need to finish the process. Close out of “Assistant Editor” mode and head over to <code>ViewController</code> so that we can make use of these menu buttons. First, we will add the following strings to drive the text of the toggle button. Add the following two lines near the top of the file.</p>

<pre><code class="language-markup">private let offText = "Disable Drawing"
private let onText = "Enable Drawing"</code></pre>

We need to update what happens when the clear and toggle buttons are clicked. Add the following line to clear the drawing in <code>clearButtonClicked(_ sender)</code>:

<pre><code class="language-markup">view.window!.ignoresMouseEvents = !view.window!.ignoresMouseEvents
toggleButton.title = view.window!.ignoresMouseEvents ? onText : offText</code></pre>

This toggles the flag on our window to ignore mouse events, so that we will click “through” our window, in order to use our computer as intended. We’ll also update the <code>toggleButton</code>’s text to let the user know that drawing is either enabled or disabled.

Now we need to finally put our menu to use. Let’s start by adding an icon to our project. You can find that <a href="https://github.com/thirteen23/ScreenAnnotation/blob/master/pencil.zip">in the repository</a>. Then, we can override the <code>awakeFromNib()</code> method because, at this point, our view will be inflated from the storyboard. Add the following code to <code>ViewController</code>.</p>

<pre><code class="language-markup">let statusItem = NSStatusBar.system.statusItem(withLength: NSStatusItem.variableLength)

override func awakeFromNib() {
  statusItem.menu = optionsMenu
  let icon = NSImage(named: NSImage.Name(rawValue: "pencil"))
  icon?.isTemplate = true // best for dark mode
  statusItem.image = icon

  toggleButton.title = offText
}</code></pre>

Make sure to put the <code>statusItem</code> near the top, next to the rest of the variables. <code>statusItem</code> grabs a spot for our app to use menu extras in the top toolbar. Then, in <code>awakeFromNib</code>, we set the menu as our <code>optionsMenu</code>, and, finally, we give it an icon, so that it is easily identifiable and clickable. If we run our app now, the “menu extra” icon will appear at the top! We aren’t quite finished yet. We need to ensure that the drawing space is placed correctly on screen; otherwise, it will be only partially useful.</p>

## 6\. Positioning The Drawing App

To get our view to draw where we want it, we must venture back into <code>Main.storyboard</code>. Click on the window itself, and then select the attributes inspector, the icon fourth from the left in the right-hand pane. Uncheck everything under the “Appearance,” “Controls” and “Behavior” headings, like so:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7912fcc1-ddd8-4136-8483-fc6c070ad2a3/07-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7912fcc1-ddd8-4136-8483-fc6c070ad2a3/07-a-swift-transition-from-ios-to-macos-development-preview-opt.jpg" alt="Attributes inspector" width="249" height="380" /></a><figcaption>Attributes inspector</figcaption></figure>

We do this to remove all extra behaviors and appearances. We want a clear screen, with no bells and whistles. If we run the app again, we will be greeted by a familiar blue screen, only larger. To make things useful, we need to change the color from blue to transparent. Head back over to <code>ClearWindow</code> and update the blue color to this:

<pre><code class="language-markup">backgroundColor = NSColor(calibratedRed: 1, green: 1, blue: 1, alpha: 0.001)</code></pre>

This is pretty much the same as <code>NSColor.clear</code>. The reason why we are not using <code>NSColor.clear</code> is that if our entire app is transparent, then macOS won’t think our app is visible, and no clicks will be captured in the app. We’ll go with a mostly transparent app — something that, at least to me, is not noticeable, yet our clicks will be recorded correctly.

The final thing to do is remove it from our dock. To do this, head over to <code>Info.plist</code> and add a new row, named “Application is agent (UIElement)” and set it to “Yes.” Once this is done, rerun the app, and it will no longer appear in the dock!

## Conclusion

This app is pretty short and sweet, but we did learn a few things. First, we figured out some of the similarities and differences between UIKit and Cocoa. We also took a tour around what Cocoa has in store for us iOS developers. We also (hopefully) know that creating a Cocoa-based app is not difficult, nor should it be intimidating. We now have a small app that is presented in an atypical fashion, and it lives up in the menu bar, next to the menu extras. Finally, we can use all of this stuff to build bigger and better Cocoa apps! You started this article as an iOS developer and grew beyond that, becoming an <em>Apple</em> developer. Congratulations!

I will be updating the <a href="https://github.com/thirteen23/ScreenAnnotation">public repository</a> for this example to add extra options. Keep an eye on the repository, and feel free to add code, issues and comments.

Good luck and happy programming!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cff6f87-7454-4198-b518-5257d368a9f7/thank-you.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cff6f87-7454-4198-b518-5257d368a9f7/thank-you.gif" alt="Attributes inspector" width="500" height="312" /></a><figcaption>Thank you!</figcaption></figure>

{{< signature "al" >}}

