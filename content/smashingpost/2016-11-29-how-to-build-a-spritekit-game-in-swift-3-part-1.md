---
title: How To Build A SpriteKit Game In Swift 3 (Part 1)
slug: how-to-build-a-spritekit-game-in-swift-3-part-1
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb3210b-4d9f-43f6-8817-9d5af678722a/raincat-header-preview-opt.png
date: 2016-11-29T22:05:59.000Z
author: marcvandehey
description: >-
  Have you ever wondered what it takes to create a SpriteKit game from beginning
  to beta? Does developing a physics-based game seem daunting? Game-making has
  never been easier on iOS since the introduction of SpriteKit.

  In this three-part series, we will explore the basics of SpriteKit. We will
  touch on SKPhysics, collisions, texture management, interactions, sound
  effects, music, buttons and `SKScene`s. What might seem difficult is actually
  pretty easy to grasp. Stick with us while we make RainCat.
categories:
  - Mobile
  - Apps
  - Games
  - iOS
  - Swift
---
Have you ever wondered what it takes to create a SpriteKit game from beginning to beta? Does developing a physics-based game seem daunting? Game-making has never been easier on iOS since the introduction of [SpriteKit](https://developer.apple.com/spritekit/).

In this three-part series, we will explore the basics of SpriteKit. We will touch on SKPhysics, collisions, texture management, interactions, sound effects, music, buttons and `SKScene`s. What might seem difficult is actually pretty easy to grasp. Stick with us while we make RainCat.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2016/11/building-shaders-with-babylon-js/#further-reading-on-smashingmag)

*   [Gamification And UX: Where Users Win Or Lose](https://www.smashingmagazine.com/2012/04/gamification-ux-users-win-lose/)
*   [Playful UX Design: Building A Better Game](https://www.smashingmagazine.com/2012/07/playful-ux-design-building-better-game/)
*   [Combining UX Design And Psychology To Change User Behavior](https://www.smashingmagazine.com/2016/01/combining-ux-design-and-psychology-to-change-user-behavior/)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb3210b-4d9f-43f6-8817-9d5af678722a/raincat-header-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb3210b-4d9f-43f6-8817-9d5af678722a/raincat-header-preview-opt.png" width="500" height="300" alt="Raincat: Lesson 1" /></a><figcaption>RainCat, lesson 1</figcaption></figure>

{{% feature-panel %}}

The game we will build has a simple premise: We want to feed a hungry cat, but it is outside in the rain. Ironically, RainCat does not like the rain all that much, and it gets sad when it’s wet. To fix this, we must hold an umbrella above the cat so that it can eat without getting rained on. To get a taste of what we will be creating, check out the [completed project](https://itunes.apple.com/us/app/raincat/id1152624676?ls=1&mt=8). It has some more bells and whistles than what we will cover here, but you can look at those additions later on GitHub. The aim of this series is to get a good understanding of what goes into making a simple game. You can check in with us later on and use the code as a reference for future projects. I will keep updating the code base with interesting additions and refactoring.

We will do the following in this article:

*   check out the initial code for the RainCat game;
*   add a floor;
*   add raindrops;
*   prepare the initial physics;
*   add in the umbrella object to keep our cat dry from the rain;
*   begin collision detection with `categoryBitMask` and `contactTestBitMask`;
*   create a world boundary to remove nodes that fall off screen.</p>

## Getting Started

You will need to follow along with a few things. To make it easier to start, I’ve provided a base project. This base project removes all of the boilerplate code that Xcode 8 provides when creating a new SpriteKit project.

*   Get the base code for the RainCat game by downloading the [custom Xcode project](https://github.com/thirteen23/RainCat/releases/tag/smashing-magazine-initial-code).
*   Install Xcode 8.
*   Get something to test on! In this case, it should be an iPad, which will remove some of the complexity of developing for multiple screen sizes. The simulator is functional, but it will always lag and run at a lower frame rate than a proper iOS device.</p>

## Check Out The Project

I've given you a head start by creating the project for the RainCat game and completing some initial steps. Open up the Xcode project. It will look fairly barebones at the moment. Here is an overview of what has happened up to this point: We’ve created a project, targeted iOS 10, set the devices to iPad, and set the orientation to landscape only. We can get away with targeting previous versions of iOS, back to version 8 with Swift 3, if we need to test on an older device. Also, a best practice is to support at least one version of iOS older than the current version. Just note that this tutorial targets iOS 10, and issues may arise if you target a previous version.

Side note on the usage of Swift 3 for this game: The iOS development community has been eagerly anticipating the release of Swift 3, which brings with it many changes in coding styles and improvements across the board. As new iOS versions are quickly and widely adopted by Apple’s consumer base, we decided it would be best to present the lessons in this article according to this latest release of Swift.

In `GameViewController.swift`, which is a standard [`UIViewController`](https://developer.apple.com/library/content/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Lesson4.html), we reworked how we load the initial [SKScene](https://developer.apple.com/reference/spritekit/skscene) named `GameScene.swift`. Before this change, the code would load the `GameScene` class through a SpriteKit scene editor (SKS) file. For this tutorial, we will load the scene directly, instead of inflating it using the SKS file. If you wish to learn more about the SKS file, Ray Wenderlich has a [great example](https://www.raywenderlich.com/118225/introduction-sprite-kit-scene-editor).</p>

## Get Your Assets

Before we can start coding, we need to get the assets for the project. Today we will have an umbrella sprite, along with raindrops. You will [find the textures on GitHub](https://github.com/thirteen23/RainCat/tree/smashing-day-1/dayOneAssets.zip). Add them to your `Assets.xcassets` folder in the left pane of Xcode. Once you click on the `Assets.xcassets` file, you will be greeted with a white screen with a placeholder for the `AppIcon`. Select all of the files in a Finder window, and drag them below the `AppIcon` placeholder. If that is done correctly, your “Assets” file will look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a08bbfd-cec8-4610-8883-65bf3b0c3829/app-assets-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a08bbfd-cec8-4610-8883-65bf3b0c3829/app-assets-preview-opt.png" width="500" height="212" alt="App assets" /></a><figcaption>The umbrella’s top won’t show up due to being white on white, but I promise it is there.</figcaption></figure>

## Time To Start Coding

Now that we have a lot of the initial configuration out of the way, we can get started making the game.

The first thing we need is a floor, since we need a surface for the cat to walk and feed on. Because the floor and the background will be extremely simple, we can handle those sprites with a custom background node. Under the “Sprites” group in the left pane of Xcode, create a new Swift file named `BackgroundNode.swift`, and insert the following code:

<pre><code class="language-c">import SpriteKit

public class BackgroundNode : SKNode {

  public func setup(size : CGSize) {
    let yPos : CGFloat = size.height * 0.10
    let startPoint = CGPoint(x: 0, y: yPos)
    let endPoint = CGPoint(x: size.width, y: yPos)
    physicsBody = SKPhysicsBody(edgeFrom: startPoint, to: endPoint)
    physicsBody?.restitution = 0.3
  }
}
</code></pre>

The code above imports our SpriteKit framework. This is Apple's library for developing games. We will be using this in pretty much every file we create from now on. This object that we are creating is an [`SKNode`](https://developer.apple.com/reference/spritekit/sknode). We will be using it as a container for our background. Currently, we just add an [`SKPhysicsBody`](https://developer.apple.com/reference/spritekit/skphysicsbody) to it when we call the `setup(size:)` function. The physics body will tell our scene that we want this defined area, currently a line, to interact with other physics bodies, as well as with the [physics world](https://developer.apple.com/reference/spritekit/skphysicsworld). We also snuck in a change to `restitution`. This property determines how bouncy the floor will be. To have it show up for us to use, we need to add it to `GameScene`. Move to the `GameScene.swift` file, and near the top of the file, underneath our group of `TimeInterval` variables, we can add this:

<pre><code class="language-c">private let backgroundNode = BackgroundNode()</code></pre>

Then, inside the `sceneDidLoad()` function, we can set up and add the background to the scene with the following lines:

<pre><code class="language-c">backgroundNode.setup(size: size)
addChild(backgroundNode)</code></pre>

Now, if we run the app, we will be greeted with this game scene:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cbae860-8466-4864-9ce9-a8649980971f/empty-scene-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cbae860-8466-4864-9ce9-a8649980971f/empty-scene-preview-opt.png" width="500" height="375" alt="Empty scene" /></a><figcaption>Our slightly less empty scene</figcaption></figure>

If you don’t see this line, then something went wrong when you added the node to the scene, or else the scene is not showing the physics bodies. To turn these options on and off, go to `GameViewController.swift` and modify these values:

<pre><code class="language-c">if let view = self.view as! SKView? {
	view.presentScene(sceneNode)
	view.ignoresSiblingOrder = true
	view.showsPhysics = true
	view.showsFPS = true
	view.showsNodeCount = true
}
</code></pre>

Make sure that `showsPhysics` is set to `true` for now. This will help us to debug our physics bodies. Right now, this isn’t anything special to look at, but this will act as our floor for our raindrops to bounce off of, as well as the boundary within which the cat will walk back and forth.

Next, let’s add some raindrops.

If we think before we just start adding them to the scene, we’ll see that we’ll want a reusable function to add one raindrop to the scene at a time. The raindrop will be made up of an `SKSpriteNode` and another physics body. An `SKSpriteNode` can be initialized by an image or a texture. Knowing this, and also knowing that we will likely spawn a lot of raindrops, we need to do some recycling. With this in mind, we can recycle the texture so that we aren’t creating a new texture every time we create a raindrop.

At the top of the `GameScene.swift` file, above where we initialized `backgroundNode`, we can add the following line to the file:

<pre><code class="language-c">let raindropTexture = SKTexture(imageNamed: "rain_drop")</code></pre>

We can now reuse this texture every time we create a raindrop, so that we aren’t wasting memory by creating a new one every time we want a raindrop.

Now, add in the following function near the bottom of `GameScene.swift`, so that we can constantly create raindrops:

<pre><code class="language-c">private func spawnRaindrop() {
    let raindrop = SKSpriteNode(texture: raindropTexture)
    raindrop.physicsBody = SKPhysicsBody(texture: raindropTexture, size: raindrop.size)
    raindrop.position = CGPoint(x: size.width / 2, y: size.height / 2)

    addChild(raindrop)
  }
</code></pre>

This function, when called, will create a raindrop using the `raindropTexture` that we just initialized. Then, we’ll create an `SKPhysicsBody` from the shape of the texture, position the raindrop node at the center of the scene and, finally, add it to the scene. Because we added an `SKPhysicsBody` to the raindrop, it will be automatically affected by the default gravity and fall to the floor. To test things out, we can call this function in `touchesBegan(_ touches:, with event:)`, and we will see this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8063278-7d6a-4dff-9002-e620fbb04854/first-rain-fall.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8063278-7d6a-4dff-9002-e620fbb04854/first-rain-fall.gif" width="500" height="375" alt="Making it rain" /></a><figcaption>Making it rain</figcaption></figure>

Now, as long as we keep tapping the screen, more raindrops will appear. This is for testing purposes only; later on, we will want to control the umbrella, not the rate of rainfall. Now that we’ve had our fun, we should remove the line that we added to `touchesBegan(_ touches:, with event:)` and tie in the rainfall to our `update` loop. We have a function named `update(_ currentTime:)`, and this is where we will want to spawn our raindrops. Some boilerplate code is here already; currently, we are measuring our delta time, and we will use this to update some of our other sprites later on. Near the bottom of that function, before we update our `self.lastUpdateTime` variable, we will add the following code:

<pre><code class="language-c">// Update the spawn timer
currentRainDropSpawnTime += dt

if currentRainDropSpawnTime > rainDropSpawnRate {
  currentRainDropSpawnTime = 0
  spawnRaindrop()
}
</code></pre>

This will spawn a raindrop every time the accumulated delta time is greater than `rainDropSpawnRate`. Currently, the `rainDropSpawnRate` is 0.5 seconds; so, every half a second, a new raindrop will be created and fall to the floor. Test and run the app. It will act exactly as it did before, but instead of our having to touch the screen, a new raindrop will be created every half a second.

But this is not good enough. We don’t want one location from which to release the raindrops, and we certainly don’t want it to fall from the center of the screen. We can update the `spawnRaindrop()` function to position each new drop at a random `x` location at the top of the screen.

Find the following line in `spawnRaindrop()`:

<pre><code class="language-c">raindrop.position = CGPoint(x: size.width / 2, y: size.height / 2)</code></pre>

Replace it with this:

<pre><code class="language-c">let xPosition =
	CGFloat(arc4random()).truncatingRemainder(dividingBy: size.width)
let yPosition = size.height + raindrop.size.height

raindrop.position = CGPoint(x: xPosition, y: yPosition)</code></pre>

After creating the raindrop, we randomize the `x` position on screen with `arc4Random()`, and we make sure it is on screen with our `truncatingRemainder` method. Run the app, and you should see the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77909a06-20a1-4695-a468-4cbd4bb09c4a/raindrops-for-days-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77909a06-20a1-4695-a468-4cbd4bb09c4a/raindrops-for-days-preview-opt.png" width="500" height="375" alt="Raindrops for days!" /></a><figcaption>Raindrops for days!</figcaption></figure>

We can play with the spawn rate, and we can spawn raindrops faster or slower depending on what value we enter. Update `rainDropSpawnRate` to be `0`, and you will see many pretty raindrops. If you do this, you will notice that we have a big problem now. We are currently spawning unlimited objects and never getting rid of them. We will eventually be crawling at four frames per second and, soon after that, we’ll be out of memory.

## Detect Our Collision

Right now, there are only two types of collision. We have one collision between raindrops and one between raindrops and the floor. We need to detect when the raindrops hit something, so that we can tell it to be removed. We will add in another physics body that will act as the world frame. Anything that touches this frame will be deleted, and our memory will thank us for recycling. We need some way to tell the physics bodies apart. Luckily, `SKPhysicsBody` has a field named `categoryBitMask`. This will help us to differentiate between the items that have come into contact with each other.

To accomplish this, we should create another Swift file named `Constants.swift`. Create the file under the “Support” group in the left pane of Xcode. The “Constants” file enables us to hardcode values that will be used in many places across the app, all in one place. We won't need many of these types of variables, but keeping them in one location is a good practice, so that we don't have to search everywhere for these variables. After you create the file, add the following code to it:

<pre><code class="language-c">let WorldCategory    : UInt32 = 0x1 << 1
let RainDropCategory : UInt32 = 0x1 << 2
let FloorCategory    : UInt32 = 0x1 << 3
</code></pre>

The code above uses a [shift operator](https://www-numi.fnal.gov/offline_software/srt_public_context/WebDocs/Companion/cxx_crib/shift.html) to set a unique value for each of the [`categoryBitMasks`](https://developer.apple.com/reference/spritekit/skphysicsbody/1519869-categorybitmask) in our physics bodies. `0x1 << 1` is the hex value of 1, and `0x1 << 2` is the value of 2\. `0x1 << 3` equals 4, and each value after that is doubled. Now that our unique categories are set up, navigate to our `BackgroundNode.swift` file, where we can update the physics body to the new `FloorCategory`. Then, we need to tell the floor physics body what we want to touch it. To do this, update the floor’s `contactTestBitMask` to contain the `RainDropCategory`. This way, when we have everything hooked up in our `GameScene.swift`, we will get callbacks when the two touch each other. `BackgroundNode` should now look like this:

<pre><code class="language-c">import SpriteKit

public class BackgroundNode : SKNode {

  public func setup(size : CGSize) {

    let yPos : CGFloat = size.height * 0.10
    let startPoint = CGPoint(x: 0, y: yPos)
    let endPoint = CGPoint(x: size.width, y: yPos)

    physicsBody = SKPhysicsBody(edgeFrom: startPoint, to: endPoint)
    physicsBody?.restitution = 0.3
    physicsBody?.categoryBitMask = FloorCategory
    physicsBody?.contactTestBitMask = RainDropCategory
  }
}
</code></pre>

The next step is to update the raindrops to the correct category, as well as update what it should come into contact with. Going back to `GameScene.swift`, in `spawnRaindrop()` we can add the following code after we initialize the raindrop’s physics body:

<pre><code class="language-c">raindrop.physicsBody?.categoryBitMask = RainDropCategory
raindrop.physicsBody?.contactTestBitMask = FloorCategory | WorldCategory
</code></pre>

Notice that we’ve added in the `WorldCategory` here, too. Because we are working with a [bitmask](https://en.wikipedia.org/wiki/Mask_%28computing%29), we can add in any category here that we want with [bitwise operations](https://en.wikipedia.org/wiki/Bitwise_operation). In this instance for `raindrop`, we want to listen for contact when the raindrop hits either the `FloorCategory` or `WorldCategory`. Now, in our `sceneDidLoad()` function, we can finally add in our world frame:

<pre><code class="language-c">var worldFrame = frame
worldFrame.origin.x -= 100
worldFrame.origin.y -= 100
worldFrame.size.height += 200
worldFrame.size.width += 200

self.physicsBody = SKPhysicsBody(edgeLoopFrom: worldFrame)
self.physicsBody?.categoryBitMask = WorldCategory
</code></pre>

In the code above, we’ve create a frame that is the same as the scenes, but we’ve increased the size so that it extends 100 points on either side. This way, we will have a buffer so that items aren’t deleted on screen. Note that we’ve used `edgeLoopFrom`, which creates an empty rectangle that allows for collisions at the edge of the frame.

Now that we have everything in place for detection, we need to start listening to it. Update the game scene to inherit from `SKPhysicsContactDelegate`. Near the top of the file, find this line:

<pre><code class="language-c">class GameScene: SKScene {</code></pre>

And change it to this:

<pre><code class="language-c">class GameScene: SKScene, SKPhysicsContactDelegate {</code></pre>

We now need to tell our scene’s [`physicsWorld`](https://developer.apple.com/reference/spritekit/skphysicsworld) that we want to listen for collisions. Add in the following line in `sceneDidLoad()`, below where we set up the world frame:

<pre><code class="language-c">
	self.physicsWorld.contactDelegate = self
</code></pre>

Then, we need to implement one of the `SKPhysicsContactDelegate` functions, `didBegin(_ contact:)`. This will be called every time there is a collision that matches any of the `contactTestBitMasks` that we set up earlier. Add this code to the bottom of `GameScene.swift`:

<pre><code class="language-c">func didBegin(_ contact: SKPhysicsContact) {
    if (contact.bodyA.categoryBitMask == RainDropCategory) {
      contact.bodyA.node?.physicsBody?.collisionBitMask = 0
      contact.bodyA.node?.physicsBody?.categoryBitMask = 0
    } else if (contact.bodyB.categoryBitMask == RainDropCategory) {
      contact.bodyB.node?.physicsBody?.collisionBitMask = 0
      contact.bodyB.node?.physicsBody?.categoryBitMask = 0
    }
}
</code></pre>

Now, when a raindrop collides with the edge of any object, we’ll remove the collision bitmask of the raindrop. This prevents the raindrop from colliding with anything after the initial impact, which finally puts an end to our Tetris-like nightmare!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab8cb39-7832-4abc-babf-fc3ad2768d56/happy-bouncing-raindrops.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab8cb39-7832-4abc-babf-fc3ad2768d56/happy-bouncing-raindrops.gif" width="500" height="375" alt="Bouncing raindrops" /></a><figcaption>Happy little bouncing raindrops</figcaption></figure>

If there is a problem and the raindrops are not acting like in the GIF above, double-check that every `categoryBitMask` and `contactTestBitMasks` is set up correctly. Also, note that the nodes count in the bottom-right corner of the scene will keep increasing. The raindrops are not piling up on the floor anymore, but they are not being removed from the game scene. We will continue running into memory issues if we don’t start culling.

In the `didBegin(_ contact:)` function, we need to add the delete behavior to cull the nodes. This function should be updated to the following:

<pre><code class="language-c">func didBegin(_ contact: SKPhysicsContact) {
     if (contact.bodyA.categoryBitMask == RainDropCategory) {
      contact.bodyA.node?.physicsBody?.collisionBitMask = 0
      contact.bodyA.node?.physicsBody?.categoryBitMask = 0
    } else if (contact.bodyB.categoryBitMask == RainDropCategory) {
      contact.bodyB.node?.physicsBody?.collisionBitMask = 0
      contact.bodyB.node?.physicsBody?.categoryBitMask = 0
    }

    if contact.bodyA.categoryBitMask == WorldCategory {
      contact.bodyB.node?.removeFromParent()
      contact.bodyB.node?.physicsBody = nil
      contact.bodyB.node?.removeAllActions()
    } else if contact.bodyB.categoryBitMask == WorldCategory {
      contact.bodyA.node?.removeFromParent()
      contact.bodyA.node?.physicsBody = nil
      contact.bodyA.node?.removeAllActions()
    }
}
</code></pre>

Now, if we run our code, we will notice that the node counter will increase to about six nodes and will remain at that count. If this is true, then we are successfully culling off-screen nodes!

## Updating The Background Node

The background node has been very simple until now. It is just an `SKPhysicsBody`, which is one line. We need to upgrade it to make the app look a lot nicer. Initially, we would have used an `SKSpriteNode`, but that would have been a huge texture for such a simple background. Because the background will consist of exactly two colors, we can create two `SKShapeNodes` to act as the sky and the ground.

Navigate to `BackgroundNode.swift` and add the following code in the `setup(size)` function, below where we initialized the `SKPhysicsBody`.</p>

<pre><code class="language-c">let skyNode = SKShapeNode(rect: CGRect(origin: CGPoint(), size: size))
skyNode.fillColor = SKColor(red:0.38, green:0.60, blue:0.65, alpha:1.0)
skyNode.strokeColor = SKColor.clear
skyNode.zPosition = 0

let groundSize = CGSize(width: size.width, height: size.height * 0.35)
let groundNode = SKShapeNode(rect: CGRect(origin: CGPoint(), size: groundSize))
groundNode.fillColor = SKColor(red:0.99, green:0.92, blue:0.55, alpha:1.0)
groundNode.strokeColor = SKColor.clear
groundNode.zPosition = 1

addChild(skyNode)
addChild(groundNode)
</code></pre>

In the code above, we’ve created two `SKShapeNodes` that are basic rectangles. But a new problem arises from `zPosition`. Note in the code above that `skyNode`’s `zPosition` is `0`, and the ground’s is `1`. This way, the ground will always render in front of the sky. If you run the app now, you will see the rain draw in front of the sky but behind the ground. This is not the behavior we want. If we move back to `GameScene.swift`, we can update the `spawnRaindrop()` function and set the `zPosition` of the raindrops to render in front of the ground. In the `spawnRaindrop()` function, below where we set the spawn position, add the following line:

<pre><code class="language-c">
raindrop.zPosition = 2
</code></pre>

Run the code again, and the background should be drawn correctly.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90db4c58-9691-431c-b172-93f288e5da17/background-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90db4c58-9691-431c-b172-93f288e5da17/background-preview-opt.png" width="500" height="375" alt="Background" /></a><figcaption>That’s better.</figcaption></figure>

## Adding Interaction

Now that the rain is falling the way we want and the background is set up nicely, we can start adding some interaction. Create another file under the “Sprites” group, named `UmbrellaSprite.swift`. Add the following code for the initial version of the umbrella.</p>

<pre><code class="language-c">import SpriteKit

public class UmbrellaSprite : SKSpriteNode {
  public static func newInstance() -> UmbrellaSprite {
    let umbrella = UmbrellaSprite(imageNamed: "umbrella")

    return umbrella
  }
}
</code></pre>

The umbrella will be a pretty basic object. Currently, we have a static function to create a new sprite node, but we will soon add a custom physics body to it. For the physics body, we could use the function `init(texture: size:)`, as we did with the raindrop, to create a physics body from the texture itself. This would work just fine, but then we would have a physics body that wraps around the handle of the umbrella. If we have a body around the handle, the cat would get hung up on the umbrella, which would not make for a fun game. Instead, we will add a `SKPhysicsBody` from the `CGPath` that we created in the static `newInstance()` function. Add the code below in `UmbrellaSprite.swift`, before we return the umbrella sprite’s `newInstance()` function.</p>

<pre><code class="language-c">let path = UIBezierPath()
path.move(to: CGPoint())
path.addLine(to: CGPoint(x: -umbrella.size.width / 2 - 30, y: 0))
path.addLine(to: CGPoint(x: 0, y: umbrella.size.height / 2))
path.addLine(to: CGPoint(x: umbrella.size.width / 2 + 30, y: 0))

umbrella.physicsBody = SKPhysicsBody(polygonFrom: path.cgPath)
umbrella.physicsBody?.isDynamic = false
umbrella.physicsBody?.restitution = 0.9
</code></pre>

We are creating a custom path for the umbrella’s `SKPhysicsBody` for two reasons. First, as mentioned, we only want the top part of the umbrella to have any collision. The second reason is so that we can be a little forgiving with the umbrella’s collision size.

The easy way to create a `CGPath` is to first create a `UIBezierPath` and append lines and points to create our basic shape. In the code above, we’ve created this `UIBezierPath` and moved the start point to the center of the sprite. The `umbrellaSprite`’s center point is `0,0` because our [`anchorPoint`](https://developer.apple.com/reference/spritekit/skspritenode#//apple_ref/occ/instp/SKSpriteNode/anchorPoint) of the object is `0.5,0.5`. Then, we add a line to the far-left side of the sprite and extend the line 30 points past the left edge.

Side note on usage of the word “point” in this context: A “point,” not to be confused with `CGPoint` or our `anchorPoint,` is a unit of measurement. A point may be 1 pixel on a non-Retina device, 2 pixels on a Retina device, and more depending on the pixel density of the device. Learn more about [pixels and points on Fluid’s blog](https://blog.fluidui.com/designing-for-mobile-101-pixels-points-and-resolutions/).

Next, go to the top-center point of the sprite for the top edge, followed by the far-right side, and extend them the same 30 points out. We’re extending the edge of the physics body past the texture to give us more room to block raindrops, while maintaining the look of the sprite. When we add the polygon to `SKPhysicsBody`, it will close the path for us and give us a complete triangle. Then, set the umbrella’s physics to not be dynamic, so that it won’t be affected by gravity. The physics body that we drew will look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0229a068-fdd0-45fd-9d78-8b109e725842/umbrella-close-up-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b410939-ff85-43c6-8277-472ccc725a79/umbrella-close-up-preview-opt.png" width="500" height="375" alt="Umbrella Close up" /></a><figcaption>A closeup of the umbrella's physics body (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0229a068-fdd0-45fd-9d78-8b109e725842/umbrella-close-up-large-opt.png">View large version</a>)</figcaption></figure>

Now make your way over to `GameScene.swift` to initialize the umbrella object and add it to the scene. At the top of the file and below our other class variables, add in this line:

<pre><code class="language-c">private let umbrellaNode = UmbrellaSprite.newInstance()</code></pre>

Then, in `sceneDidLoad()`, beneath where we added `backgroundNode` to the scene, insert the following lines to add the umbrella to the center of the screen:

<pre><code class="language-c">umbrellaNode.position = CGPoint(x: frame.midX, y: frame.midY)
umbrellaNode.zPosition = 4
addChild(umbrellaNode)
</code></pre>

Once this is added, run the app to see the umbrella. You will see the raindrops bouncing off it!

## Creating Movement

We will update the umbrella to respond to touch. In `GameScene.swift`, look at the empty functions `touchesBegan(_ touches:, with event:)` and `touchesMoved(_ touches:, with event:)`. This is where we will tell the umbrella where we’ve interacted with the game. If we set the position of the umbrella node in both of these functions based on one of the current touches, it will snap into place and teleport from one side of the screen to the other.

Another approach would be to set a destination in the `UmbrellaSprite` object, and when `update(dt:)` is called, we can move toward that location.

Yet a third approach would be to set `SKActions` to move the `UmbrellaSprite` on `touchesBegan(_ touches:, with event:)` or `touchesMoved(_ touches:, with event:)`, but I would not recommend this. This would cause us to create and destroy these `SKActions` frequently and likely would not be performant.

We will choose the second option. Update the code in `UmbrellaSprite` to look like this:

<pre><code class="language-c">import SpriteKit

public class UmbrellaSprite : SKSpriteNode {
  private var destination : CGPoint!
  private let easing : CGFloat = 0.1

  public static func newInstance() -> UmbrellaSprite {
    let umbrella = UmbrellaSprite(imageNamed: "umbrella")

    let path = UIBezierPath()
    path.move(to: CGPoint())
    path.addLine(to: CGPoint(x: -umbrella.size.width / 2 - 30, y: 0))
    path.addLine(to: CGPoint(x: 0, y: umbrella.size.height / 2))
    path.addLine(to: CGPoint(x: umbrella.size.width / 2 + 30, y: 0))

    umbrella.physicsBody = SKPhysicsBody(polygonFrom: path.cgPath)
    umbrella.physicsBody?.isDynamic = false
    umbrella.physicsBody?.restitution = 0.9

    return umbrella
  }

  public func updatePosition(point : CGPoint) {
    position = point
    destination = point
  }

  public func setDestination(destination : CGPoint) {
    self.destination = destination
  }

  public func update(deltaTime : TimeInterval) {
    let distance = sqrt(pow((destination.x - position.x), 2) + pow((destination.y - position.y), 2))

    if(distance > 1) {
      let directionX = (destination.x - position.x)
      let directionY = (destination.y - position.y)

      position.x += directionX * easing
      position.y += directionY * easing
    } else {
      position = destination;
    }
  }
}
</code></pre>

A few things are happening here. The `newInstance()` function has been left untouched, but we’ve added two variables above it. We’ve added a destination variable (the point that we want to be moving towards); we’ve added a `setDestination(destination:)` function, to where we will ease the umbrella sprite; and we’ve added an `updatePosition(point:)` function.

The `updatePosition(point:)` will act exactly as though the `position` property was being updated directly before we made this update. Now we can update the position and the destination at the same time. This way, the `umbrellaSprite` will be positioned at this point and will stay where it is, because it will already be at its destination, instead of moving towards it immediately after setup.

The `setDestination(destination:)` function will only update the destination property; we will perform our calculations off of this property later. Finally, we added `update(dt:)` to compute how far we need to travel towards the destination point from our current position. We computed the distance between the two points, and if it is greater than one point, we compute how far we want to travel using the `easing` function. The `easing` function just finds the direction that the umbrella needs to travel in, and then moves the umbrella's position 10% of the distance to the destination for each axis. This way, we won't snap to the new location, but rather will move faster if we are further from the point, and slow down as the umbrella approaches its destination. If it is less than or equal to 1 pixel, then we will just jump to the final position. We do this because the easing function will approach the destination very slowly. Instead of constantly updating, computing and moving the umbrella an extremely short distance, we just set the position and forget about it.

Moving back to `GameScene.swift`, we should update our `touchesBegan(_ touches: with event:)` and `touchesMoved(_ touches: with event:)` functions to the following:

<pre><code class="language-c">override func touchesBegan(_ touches: Set&#60;UITouch&#62;, with event: UIEvent?) {
    let touchPoint = touches.first?.location(in: self)

    if let point = touchPoint {
      umbrellaNode.setDestination(destination: point)
    }
  }

override func touchesMoved(_ touches: Set&#60;UITouch&#62;, with event: UIEvent?) {
    let touchPoint = touches.first?.location(in: self)

    if let point = touchPoint {
      umbrellaNode.setDestination(destination: point)
    }
  }
</code></pre>

Now our umbrella will respond to touch. In each function, we check to see whether the touch is valid. If it is, then we tell the umbrella to update its destination to the touch’s location. Now we need to modify the line in `sceneDidLoad()`:

<pre><code class="language-c">umbrella.position = CGPoint(x: frame.midX, y: frame.midY)</code></pre>

Change it to this:

<pre><code class="language-c">umbrellaNode.updatePosition(point: CGPoint(x: frame.midX, y: frame.midY))</code></pre>

Thus, our initial position and destination will be set correctly. When we start the scene, we won’t see the umbrella move without us interacting with the app. Lastly, we need to tell the umbrella to update in our own `update(currentTime:)` function.

Add the following code near the end of our `update(currentTime:)` function:

<pre><code class="language-c">umbrellaNode.update(deltaTime: dt)</code></pre>

When we run the code, we should be able to tap and drag around the screen, and the umbrella will follow our touching and dragging.</p>

<figure><div class="aspect-ratio">{{< vimeo 188124914 >}}></div></figure>

So, that’s lesson one! We’ve covered a ton of concepts today, jumping into the code base to get our feet wet, and then adding in a container node to hold our background and ground `SKPhysicsBody`. We also worked on spawning our raindrops at a constant interval, and had some interaction with the umbrella sprite. The source code for today is [available on GitHub](https://github.com/thirteen23/RainCat/releases/tag/smashing-magazine-lesson-one).

How did you do? Does your code look almost exactly like mine? What changed? Did you update the code for the better? Was I not clear in explaining what to do? Let me know in the comments below.

Thank you for making it this far. Stay tuned for lesson two of RainCat!

{{< signature "da, yk, al, il" >}}

