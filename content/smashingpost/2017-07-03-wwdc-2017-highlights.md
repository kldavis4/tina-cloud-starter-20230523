---
title: Apple’s WWDC 2017 Highlights For iOS Developers
slug: wwdc-2017-highlights
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0419f378-3cc0-4bcf-9dd6-942edbcfa521/wwdc-sj-keynote-john-knoll-demo-vr-preview-opt.jpg
date: 2017-07-03T19:31:20.000Z
author: lou-franco
description: >-
  Apple's Worldwide Developer Conference (WWDC) has been running for 34 years,
  which is 6 years longer than The Simpsons. Like Netflix, Apple likes to drop a
  whole season at once. When it does, I devote that week and the following
  weekend to binge-watching as many videos as I can and trying out some of the
  new technology, especially as it relates to iOS.

  In the past 10 years, a big portion of these conferences has been devoted to
  iOS. This is where we learned about the first iPhone SDK, notifications, share
  and today widgets, the iOS 7 redesign, iPad multitasking, and other iOS
  milestones. I was genuinely surprised with some of the announcements this
  year.
categories:
  - Mobile
  - Apps
  - iOS
---
In the past 10 years, a big portion of these conferences has been devoted to iOS. This is where we learned about the first iPhone SDK, notifications, share and todvay widgets, the iOS 7 redesign, iPad multitasking, and other iOS milestones. I was genuinely surprised with some of the announcements this year.

Here's my overview of what happened this WWDC season, with code samples. But before we begin, there are some things you need to keep in mind. If you want to try out any of the sample projects, you are going to have to update your Mac to macOS Sierra 10.12.5 (the latest point release), and have Xcode 9 installed. If you are super-brave, or just irresponsible, you'll need at least one device on iOS 11 for some of the samples to work. I fall under the irresponsible category here, but I also needed iOS 11 for my day job and to write this article, which seemed like a good excuse, but it's not. Everything is working fine for me so far, but this is a huge risk. Don't do it with an unbacked-up device you care about.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [How We Designed And Built Our First Apple Watch App](https://www.smashingmagazine.com/2015/08/how-we-designed-and-built-our-first-apple-watch-app/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)
*   [A Better iOS Architecture: A Deep Look At The Model-View-Controller Pattern](https://www.smashingmagazine.com/2016/05/better-architecture-for-ios-apps-model-view-controller-pattern/)

{{% feature-panel %}}

## Prepare Your Mac and Devices (to Run Code Samples Below)

1.  Update macOS in the Mac App Store if you haven't already. You don't need the beta of the next version, just the most up-to-date release.
2.  [Download Xcode 9](https://developer.apple.com/download/) (which requires a free developer account)
3.  Go to the same website on your device, and [install the iOS 11 Beta Configuration Profile](https://developer.apple.com/download/). This will let you get iOS 11 Beta and updates through the normal iOS update mechanism. (A free developer account is required.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf08c471-3c43-4e08-9b03-b8642b3b5c12/xcode-download-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4008e5a-adbe-4505-a2c2-733a92672b7d/xcode-download-800-opt.png" width="800" height="574" alt="Download Xcode 9 and install the iOS 11 Beta Configuration Profile" /></a><figcaption>Download Xcode 9 and install the iOS 11 Beta Configuration Profile. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf08c471-3c43-4e08-9b03-b8642b3b5c12/xcode-download-large-opt.png">View large version</a>)</figcaption></figure>

While you are waiting for Xcode 9 to download, go watch the [WWDC Keynote](https://www.youtube.com/watch?v=oaqHdULqet0) if you haven't seen it. If you have, watch the "[Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2017/102/)." All WWDC session videos have to viewed in Safari or in the WWDC app on any iOS or tvOS device. Another great option is the [unofficial WWDC app for macOS](https://wwdc.io/).</p>

## WWDC Keynote: TL;DW And Spoilers

This article is about the WWDC updates that matter most to iOS developers, so I'll skim through some of the big news on other fronts.</p>

<ul>
  <li>There were <strong>updates across the MacBook and iMac lines</strong>, including a tease for a new <a href="https://www.apple.com/imac-pro/">iMac Pro</a> with very high-end components (up to 18 cores) and a new space-gray finish, to be released in December.</li>
  <li>These new iMacs (and MacBooks with an external GPU) can be used to <strong>create <a href="https://www.smashingmagazine.com/2017/02/getting-started-with-vr-interface-design/">virtual reality</a> (VR) content</strong>, and this was demoed, with ILM showing off a VR Darth Vader. Steam, Unity and Unreal VR engines will release Mac versions later this year.</li>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e01968f4-c2c6-4f9c-aff6-98615a5f932a/wwdc-sj-keynote-john-knoll-demo-vr-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd870b2c-3739-49c6-921d-179cc581fbae/wwdc-sj-keynote-john-knoll-demo-vr-800-opt.jpg" height="486" width="800" alt="WWDC VR Demo" /></a><figcaption>WWDC VR demo (Image: <a href="https://www.apple.com/newsroom/2017/06/highlights-from-wwdc-2017/">Apple Newsroom</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e01968f4-c2c6-4f9c-aff6-98615a5f932a/wwdc-sj-keynote-john-knoll-demo-vr-large-opt.jpg">View large version</a>)</figcaption></figure>

  <li>The new macOS will be called High Sierra, and, as the name indicates, this release is meant to be a <strong>refinement of Sierra</strong>. Apple File System will make its Mac debut in this release.</li>
  <li>The iPad Pro also got component bumps, and the <strong>smaller size has been increased to 10.5 inches</strong>. The video refresh rate on both is variable and up to 120 Hz (twice the previous speed).</li>
  <li><strong>iOS system apps got updates</strong>, including handwriting recognition and document scanning in Notes, live photo effects, and a new Files app that lets you get to the files inside of apps directly.</li>
  <li>Apple announced a <strong>new smart speaker named <a href="https://www.apple.com/homepod/">HomePod</a></strong>. It describes it as a cross between a high-end speaker like Sonos and a smart speaker like Amazon Echo. It's also scheduled for December, but I'd expect this to be available to buy for the holidays.</li>
  <li>Apple Watch has a new Siri watch face that gives you <strong>information that it thinks you want</strong> (using machine learning). This is a lot like Google Now, but it does it all on the device, so your privacy is protected.</li>
  <li>Apple Pay supports <strong>peer-to-peer payment</strong> through iMessage, so you can split up a restaurant bill with just a text message.</li>
  <li>The <strong>App Store has been totally redesigned</strong>. It looks a lot like the Music app and puts Games into its own area. Developers can now roll out releases over time, among other features.</li>
  <li>Amazon Prime Video will be available on Apple TV later this year.</li>
</ul>

That's a lot, and we haven't even gotten to the new developer capabilities in iOS 11.</p>

## iOS Cocoa Touch And System Updates

Every year, iOS developers can expect some refinements to the overall system experience, and this year we got a big one: **drag and drop**. A lot of app developers try to do this themselves, but now iOS provides built-in support for it that supports multi-select, default animations and standardized interactions. On iPad, it even works between apps. You could say it was overdue, and perhaps it was, but we didn't even get copy-and-paste until iPhone OS 3.

Another big addition to the system is that files are now more of a first-class concept. You can browse your device's documents in the Files app (which includes cloud-based documents from iCloud Drive and third-party services), but, also, any app can bring up a file browser for the user to pick files from.

You can see these and more in the "[What's New in Cocoa Touch](https://developer.apple.com/videos/play/wwdc2017/201/)" session.

### Drag and Drop

The new drag-and-drop system interaction is implemented so that any view can participate by having a `UIDragInteraction` attached to it and then implementing the appropriate delegates. Similarly, the drop target just needs to implement the drop delegates to accept the dragged data. On iPad, items can be dragged from one app to another, but on iPhone, drag and drop only works inside the same app.

One nice thing is that if a view already knows how to accept pasted data, then it automatically will accept drops of the same kind. So, `UITextView` can automatically have text dropped onto it without your needing to add anything to your app. You can get the basics by watching the "[Introducing Drag and Drop](https://developer.apple.com/videos/play/wwdc2017/203/)" video or downloading the [demo app](https://developer.apple.com/sample-code/wwdc/2017/Drag-and-Drop-Demo-App.zip).

If you want to add drag or drop behaviors to a `UITableView` or `UICollectionView`, then a lot of the work is done for you already, and you just need to implement the drag or drop delegates specific to those views. The details can be found in the "[Drag and Drop With Collection and Table View](https://developer.apple.com/videos/play/wwdc2017/223/)" video and [demo app](https://developer.apple.com/sample-code/wwdc/2017/Drag-and-Drop-in-UICollectionView-and-UITableView.zip).

The UICollectionView/UITableView Drag and Drop Demo app implements a photo album that supports using drag and drop to:

*   reorder photos in an album,
*   move photos from one album to another,
*   move all of an album's photos to another album,
*   copy images between this app and other ones.

The main points to look at are in `PhotoCollectionViewController.swift` in the sample app ([which you can download](https://developer.apple.com/sample-code/wwdc/2017/Drag-and-Drop-in-UICollectionView-and-UITableView.zip)):

A `UIViewController` with a collection view should implement the `UICollectionViewDragDelegate` to allow drags and the `UICollectionViewDropDelegate` to allow drops.</p>

<pre><code class="language-css">class PhotoCollectionViewController: UICollectionViewController, UICollectionViewDelegateFlowLayout, UICollectionViewDragDelegate, UICollectionViewDropDelegate {
</code></pre>

As with other delegates, you should assign the collection view's drag and drop delegates to `self` in `viewDidLoad`.</p>

<pre><code class="language-css">collectionView?.dragDelegate = self
collectionView?.dropDelegate = self
</code></pre>

The only required drag delegate protocol method is called to create a `UIDragItem` array when dragging starts. A drag item holds any object that represents the drag data.</p>

<pre><code class="language-css">func collectionView(_ collectionView: UICollectionView, itemsForBeginning
              session: UIDragSession, at indexPath: IndexPath) -&gt; [UIDragItem] {
    let dragItem = self.dragItem(forPhotoAt: indexPath)
    return [dragItem]
}
</code></pre>

On the drop side, you need to say whether you can accept the data being dragged over you:

<pre><code class="language-css">func collectionView(_ collectionView: UICollectionView, canHandle session: UIDropSession) -&gt; Bool {
    guard album != nil else { return false }
    return session.hasItemsConforming(
        toTypeIdentifiers: UIImage.readableTypeIdentifiersForItemProvider)
}
</code></pre>

In this case, we return `true` if the dragged item can be turned into an image.

Once the drop actually happens, we need to copy or move the photos into the collection view.</p>

<pre><code class="language-css">func collectionView(_ collectionView: UICollectionView, performDropWith coordinator: UICollectionViewDropCoordinator) {
   guard album != nil else { return }

   let destinationIndexPath = coordinator.destinationIndexPath ?? IndexPath(item: 0, section: 0)

   switch coordinator.proposal.operation {
   case .copy:
       // Receiving items from another app.
       loadAndInsertItems(at: destinationIndexPath, with: coordinator)
   case .move:
       move(items: coordinator.items, with: coordinator)
   default: return
   }
}
</code></pre>

There are entry points for customizing the lift and drop animations, and for moving items out of the way, and a lot of other possibilities. Many of the optional features are implemented in the sample app, and more details were covered in the "[Mastering Drag and Drop](https://developer.apple.com/videos/play/wwdc2017/213/)" session. You could also read the "[Drag and Drop](https://developer.apple.com/ios/drag-and-drop/)" documentation.</p>

### Other Cocoa Touch Updates

If your iOS app is also available as a mobile web app, then you can get access to the user's website credentials to let them log into your app automatically.

To support pre-iOS 11 features (such as [universal links](https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html)), you probably already have an `apple-app-site-association` file to connect your website and app (if not, you should do that). All you need to do in addition is set the content type of your username and password `UITextField`s to `.username` and `.password`, respectively.</p>

<pre><code class="language-css">self.userNameField.textContentType = .username
self.passwordField.textContentType = .password
</code></pre>

Then, when you show a log-in screen, iOS will offer to fill it in with the user's saved credentials.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bfc8995-53fd-4d51-85f7-4349d2fe4baf/password-autofill-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bfc8995-53fd-4d51-85f7-4349d2fe4baf/password-autofill-preview-opt.png" width="798" height="766" alt="Password Autofill" /></a><figcaption>Password autofill</figcaption></figure>

More details can be found in the "[Introducing Password AutoFill for Apps](https://developer.apple.com/videos/play/wwdc2017/206/)" session.

The new Files app lets users browse files directly, but if your app needs files from other apps, you can bring up a document-picker view, similar to how you would have used an image picker to get a photo from the Photos app.</p>

<pre><code class="language-css">let docs =
  UIDocumentBrowserViewController(forOpeningFilesWithContentTypes: [kUTTypePDF])
docs.delegate = self // implement UIDocumentBrowserViewControllerDelegate
self.present(docs, animated: true)
</code></pre>

To process the chosen document, implement this `UIDocumentBrowserViewControllerDelegate` protocol method:

<pre><code class="language-css">func documentBrowser(_ controller: UIDocumentBrowserViewController, didPickDocumentURLs documentURLs: [URL]) {
   // process document here
}
</code></pre>

The session "[File Provider Enhancements](https://developer.apple.com/videos/play/wwdc2017/243/)" covers this in more detail.</p>

## Swift

Swift 4 is open-source, so most of what's happening in it can be seen in the mailing list and GitHub repository. One thing that was shown at WWDC is the new `Codable` protocol, which allows structs to be encoded via the `NSCoding` classes. All you need to do is declare conformance to the `Codable` protocol, and Swift will give you a default implementation, like so:

<pre><code class="language-css">struct WWDCVideo : Codable {
   let title: String
   let presenters: [String]
   let videoURL: URL
}
</code></pre>

This gets you automatic JSON support. You encode a struct like this:

<pre><code class="language-css">let swiftVideo = WWDCVideo(
      title: &quot;What&#039;s New in Swift&quot;,
      presenters: [
          &quot;Doug Gregor&quot;,
          &quot;Bob Wilson&quot;,
          &quot;Ben Cohen&quot;,
          &quot;John McCall&quot;,
      ],
      videoURL: URL(string: &quot;https://developer.apple.com/videos/play/wwdc2017/402/&quot;)!
)
let jsonData = try JSONEncoder().encode(swiftVideo)
</code></pre>

And you decode with this:

<pre><code class="language-css">let vid = try JSONDecoder().decode(WWDCVideo.self, from: jsonData)
</code></pre>

Also, `Codable` supports custom encoding and decoding if you need it, and it supports an easy way to make simple alterations, like alternate key names (see `CodingKeys`).

For more on what's happening in Swift, see "[What's New in Swift](https://developer.apple.com/videos/play/wwdc2017/402/)."

## Core ML

One big theme of WWDC was how Apple is using machine learning (ML) to add features across the system and apps. The Siri watchface at the top of the keynote was the first example, but Apple announced so many ML-based features that it was not a surprise when it introduced CoreML, a new Apple framework that implements the run phase of ML models, such as neural networks.

At a very high level, machine learning is used to implement functions that map arbitrary inputs to arbitrary outputs. Instead of the mapping being coded directly, it's learned from sample data. In iOS, machine learning has been used to implement facial recognition, OCR, handwriting recognition, typed-text prediction, Siri and a lot of other features.

The first thing that CoreML does is define a machine-learning-model file specification. This file is something you create ahead of time by using training software to describe your model and feeding it a lot of examples of inputs and the expected outputs. Over time, the software will be able to predict the outputs for new inputs. This understanding can be exported to model files to be used in other programs that can run models.

Once you drag a model file into your Xcode project, a Swift class is created for you that exposes a simple function that you can use to run the model on your input.

A common form of ML input is an image (from the camera, for example), and a common output is a rectangle of a recognized region in the photo. It might look something like this:

<pre><code class="language-css">let kittenFinder = KittenFinder()
let r: CGRect = kittenFinder.findKitten(image: imageView.image)
</code></pre>

The exact interface is generated from your model file. When you call it, all kinds of things are taken care of for you. For example, models based on images usually need a specific size and pixel format (color or grayscale). CoreML will automatically convert whatever image you send it to whatever the model actually needs (and supports all of the ways an image can be represented in iOS).

Using the model is extremely simple. Making these models is left as a exercise to the developer, but there are actually a lot of open-source ones, and Apple has [made some available](https://developer.apple.com/machine-learning/) for you to use in your apps. The model format's specification is open, and there's an open-source [Python library to help you convert](https://pypi.python.org/pypi/coremltools) other formats to it. It's likely that the ML community will make more models available in this format in the coming months.

There's a lot more in the "[Introducing Core ML](https://developer.apple.com/videos/play/wwdc2017/703/)" session and in the [CoreML developer documentation](https://developer.apple.com/documentation/coreml).

But Apple didn't stop there. On top of CoreML, It wrote two more frameworks that make some common tasks even easier. The Vision framework assumes that you want to recognize objects in a live camera stream, and it can read `AVCaptureSession` images automatically. It also builds in some models, such as a more accurate face detector that can also give you the location of "face landmarks" (for example, eyes, nose, mouth).

There is no sample app or documentation for detecting faces yet, but I was able to piece something together from what Apple showed in the Vision session ([get it on GitHub](https://github.com/loufranco/FaceDetector)).

In a typical `AVCaptureSession`-based app, add the Vision import to your View Controller

<pre><code class="language-css">import Vision
</code></pre>

And add this property to make detection requests:

<pre><code class="language-css">var requests: [VNDetectFaceRectanglesRequest] = []
</code></pre>

Initialize it in this function, which you should call in `viewDidLoad`:

<pre><code class="language-css">func setupVision() {
   let faceDetectionRequest = VNDetectFaceRectanglesRequest(completionHandler: self.handleFaces)
   self.requests = [faceDetectionRequest];
}
</code></pre>

In your `captureOutput` implementation, add this code:

<pre><code class="language-css">guard let imageBuffer = CMSampleBufferGetImageBuffer(sampleBuffer) else { return }

// Make the Face Detection Request
var requestOptions: [VNImageOption: Any] = [:]
if let cameraIntrinsicData = CMGetAttachment(sampleBuffer, kCMSampleBufferAttachmentKey_CameraIntrinsicMatrix, nil) {
    requestOptions = [.cameraIntrinsics: cameraIntrinsicData]
}

// The orientation should be determined from the phone position, but assume portrait (1) for now
let imageRequestHandler =
    VNImageRequestHandler(cvPixelBuffer:imageBuffer, orientation: 1, options: requestOptions)

do {
    try imageRequestHandler.perform(self.requests)
} catch {
    // handle this
}
</code></pre>

When a face is detected, this function will be called:

<pre><code class="language-css">func handleFaces(request: VNRequest, error: Error?) {
        DispatchQueue.main.async {
            self.hideFaceBox()
            guard let result = (request.results as? [VNFaceObservation])?.first else { return }
            let bb = result.boundingBox
            if let imgFrame = self.imageView?.frame {
                // Bounding Box is a 0..&lt;1.0 normlized to the size of the input image and
                // the origin is at the bottom left of the image (so Y needs to be flipped)
                let faceSize = CGSize(width: bb.width * imgFrame.width, height: bb.height * imgFrame.height)
                self.drawFaceBox(frame:
                    CGRect(x: imgFrame.origin.x + bb.origin.x * imgFrame.width,
                           y: imgFrame.origin.y + imgFrame.height - (bb.origin.y * imgFrame.height) - faceSize.height,
                           width: faceSize.width,
                           height: faceSize.height)
                )
            }
        }
}
</code></pre>

The request passed in has a results array. We grab the first element and turn its bounding box into a frame for a semi-transparent view to show over the captured image. The main thing to note is that the coordinate system of the bounding box puts the origin in the bottom-left, whereas the iPhone puts the origin in the top-left, so we need to flip the Y coordinate.

The full app is [available on GitHub](https://github.com/loufranco/FaceDetector).

Here is me running the device pointing at my laptop showing a picture of Tim Cook:

See the "[Vision Framework: Building on CoreML](https://developer.apple.com/videos/play/wwdc2017/506/)" session for details, or read the [Vision documentation](https://developer.apple.com/documentation/vision).

There's also a natural language processing (NLP) library, which didn't seem as useful to me, but it can detect languages and label parts of speech in a text input. The core parts could be used to implement something like a predictive text engine in a keyboard, but that's not built into the framework.

See all of the details in "[Natural Language Processing and Your Apps](https://developer.apple.com/videos/play/wwdc2017/208/)."

All CoreML frameworks are on device, which means:

*   data is kept private,
*   the functionality is always available,
*   usage does not incur data fees.

The similar features from cloud services tout much higher accuracy and training based on enormous data sets, which continue to grow. Your CoreML model is baked in at compile time. If you get more data, then you'll need to retrain your model, import it and rebuild.</p>

## Augmented Reality

The final big announcement was ARKit, a new framework for adding augmented reality to your app. If you have been building any content using SceneKit (for 3D games) or SpriteKit (for 2D), then you are in a good position to take advantage of ARKit, because it integrates with their drawing surfaces. Incorporating your existing code into an AR version of your app doesn't take much.

To get you started quickly, Xcode now has an augmented-reality app template:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1d5395f-ec38-4084-9ec3-c6fb7047ad7a/ar-template-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebc4b0b5-bc0e-4ca0-bfd4-73b807c20f3a/ar-template-800-opt.png" height="575" width="800" alt="AR Template in Xcode" /></a><figcaption>AR template in Xcode (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1d5395f-ec38-4084-9ec3-c6fb7047ad7a/ar-template-large-opt.png">View large version</a>)</figcaption></figure>

If you choose this, then on the next screen, you are given a choice of content technology (SceneKit, SpriteKit or Metal). Choose SceneKit, and the app will be ready to run.

The default code places a spaceship floating in front of you. You can walk around and examine it. Because this is all built on SceneKit, adding in your 3D models is simple if you have them. Just import one and update this line:

<pre><code class="language-css">let scene = SCNScene(named: &quot;art.scnassets/ship.scn&quot;)!
sceneView.scene = scene
</code></pre>

But to play around, you can generate 3D geometry with SceneKit's various geometry nodes. For example, replace the above two lines with this:

<pre><code class="language-css">self.sceneView.autoenablesDefaultLighting = true
let scene = SCNScene()
let sphereNodes = SCNNode()
scene.rootNode.addChildNode(sphereNodes)

addSphere(to: sphereNodes, pos: SCNVector3Make(0, 0, -2.0))
addSphere(to: sphereNodes, pos: SCNVector3Make(-0.3, 0.2, -2.4))
addSphere(to: sphereNodes, pos: SCNVector3Make(0.3, 0.2, -2.8))
</code></pre>

The AR template turns off default lighting in the storyboard, but we want our spheres to appear to be lit by the light that ARKit detects in the scene. All of the coordinates are in real-space coordinates of 1 meter, and the negative z-axis is in front of us, so this places 3 spheres about 2 meters or so in front of our starting position.

Then, add this function to create and add a sphere to the scene:

<pre><code class="language-css">func addSphere(to node: SCNNode, pos: SCNVector3) {
   let sphere = SCNSphere(radius: 0.1)
   let sphereNode = SCNNode(geometry: sphere)
   sphereNode.position = pos
   node.addChildNode(sphereNode)
}
</code></pre>

When you run it, it will look like this:

ARKit can also detect surfaces and lets your nodes interact with them. Check out the "[Introducing ARKit: Augmented Reality for iOS](https://developer.apple.com/videos/play/wwdc2017/602/)" session for details. Apple's Developer website also has [documentation for ARKit](https://developer.apple.com/arkit/).</p>

## And So Much More

Even with all of this, there was so much more. Xcode 9 is a big upgrade, with a fully rewritten editor and (finally) support for refactoring in Swift. You can run multiple simulators and even debug wirelessly (much needed for AR debugging).

There's more support for right-to-left languages and easier ways to deal with dynamic type sizes.

Swift Playgrounds got two updates. One you can download now, but the beta for [version 2.0 is also available through TestFlight](https://developer.apple.com/download/). This new version lets you play with all of iOS 11's features, such as ARKit and Swift 4.

Normally, we expect the real release of all of this sometime in September, along with new iPhones, so go watch those videos and get your apps ready for iOS 11.</p>

## Final Notes

### Essential Viewing

*   "[WWDC 2017 Keynote](https://www.youtube.com/watch?v=oaqHdULqet0)"
*   "[Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2017/102/)"
*   "[What's New in Cocoa Touch](https://developer.apple.com/videos/play/wwdc2017/201/)"

### Download

*   [Xcode 9 and iOS 11](https://developer.apple.com/download/)

### Apple Documentation

*   [ARKit](https://developer.apple.com/arkit/)
*   [CoreML](https://developer.apple.com/documentation/coreml)
*   [Swift 4](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/#//apple_ref/doc/uid/TP40014097-CH3-ID0)
*   [Vision](https://developer.apple.com/documentation/vision)
*   [Drag and Drop](https://developer.apple.com/ios/drag-and-drop/)
*   [iOS 11](https://developer.apple.com/ios/) (overview for developers)

{{< signature "da, vf, al, il" >}}

