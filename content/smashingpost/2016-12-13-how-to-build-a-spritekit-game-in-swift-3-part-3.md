---
title: How To Build A SpriteKit Game In Swift 3 (Part 3)
slug: how-to-build-a-spritekit-game-in-swift-3-part-3
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d05ba205-2a0b-4062-840a-9670cf3dcf60/raincat-header-sm-preview-opt-1.png
date: 2016-12-13T20:11:12.000Z
author: marcvandehey
description: >-
  Have you ever wondered what it takes to create a
  [SpriteKit](https://developer.apple.com/spritekit/) game? Do buttons seem like
  a bigger task than they should be? Ever wonder how to persist settings in a
  game? Game-making has never been easier on iOS since the introduction of
  SpriteKit. In part three of this three-part series, we will finish up our
  RainCat game and complete our introduction to SpriteKit.

  If you missed out on the [previous
  lesson](https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-2/),
  you can catch up by getting the code [on
  GitHub](https://github.com/thirteen23/RainCat/releases/tag/smashing-magazine-lesson-two).
  Remember that this tutorial requires Xcode 8 and Swift 3.
categories:
  - Mobile
  - Apps
  - Games
  - iOS
  - Swift
---
Have you ever wondered what it takes to create a <a href="https://developer.apple.com/spritekit/">SpriteKit</a> game? Do buttons seem like a bigger task than they should be? Ever wonder how to persist settings in a game? Game-making has never been easier on iOS since the introduction of SpriteKit. In part three of this three-part series, we will finish up our RainCat game and complete our introduction to SpriteKit.

If you missed out on the <a href="https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-2/">previous lesson</a>, you can catch up by getting the code <a href="https://github.com/thirteen23/RainCat/releases/tag/smashing-magazine-lesson-two">on GitHub</a>. Remember that this tutorial requires Xcode 8 and Swift 3.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2016/11/building-shaders-with-babylon-js/#further-reading-on-smashingmag)

*   [Gamification And UX: Where Users Win Or Lose](https://www.smashingmagazine.com/2012/04/gamification-ux-users-win-lose/)
*   [Playful UX Design: Building A Better Game](https://www.smashingmagazine.com/2012/07/playful-ux-design-building-better-game/)
*   [Combining UX Design And Psychology To Change User Behavior](https://www.smashingmagazine.com/2016/01/combining-ux-design-and-psychology-to-change-user-behavior/)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d05ba205-2a0b-4062-840a-9670cf3dcf60/raincat-header-sm-preview-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d05ba205-2a0b-4062-840a-9670cf3dcf60/raincat-header-sm-preview-opt-1.png" alt="Raincat, lesson 3" width="500" height="300" /></a><figcaption>RainCat, lesson 3</figcaption></figure>

{{% feature-panel %}}

This is lesson three in our RainCat journey. In the <a href="https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-2/">previous lesson</a>, we had a long day going though some simple animations, cat behaviors, quick sound effects and background music.

Today we will focus on the following:

*   heads-up display (HUD) for scoring;
*   main menu — with buttons;
*   options for muting sounds;
*   game-quitting option.</p>

### Even More Assets

The assets for the final lesson are <a href="https://github.com/thirteen23/RainCat/blob/smashing-day-3/dayThreeAssets.zip">available on GitHub</a>. Drag the images into <code>Assets.xcassets</code> again, just as we did in the previous lessons.</p>

## Heads Up!

We need a way to keep score. To do this, we can create a heads-up display (HUD). This will be pretty simple; it will be an <code>SKNode</code> that contains the score and a button to quit the game. For now, we will just focus on the score. The font we will be using is Pixel Digivolve, which you can <a href="https://www.dafont.com/pixel-digivolve.font">get at Dafont.com</a>. As with using images or sounds that are not yours, read the font's license before using it. This one states that it is free for personal use, but if you really like the font, you can donate to the author from the page. You can't always make everything yourself, so giving back to those who have helped you along the way is nice.

Next, we need to add the custom font to the project. This process can be tricky the first time.

Download and move the font into the project folder, under a "Fonts" folder. We've done this a few times in the previous lessons, so we'll go through this process a little more quickly. Add a group named <code>Fonts</code> to the project, and add the <code>Pixel digivolve.otf</code> file.

Now comes the tricky part. If you miss this part, you probably won't be able to use the font. We need to add it to our <code>Info.plist</code> file. This file is in the left pane of Xcode. Click it and you will see the property list (or <code>plist</code>). Right-click on the list, and click "Add Row."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efd0d228-80f8-469f-8aa3-da716652f685/settings-infoplist-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efd0d228-80f8-469f-8aa3-da716652f685/settings-infoplist-preview-opt.png" alt="Add Row" width="500" height="" /></a><figcaption>Add a row to the <code>plist</code>.</figcaption></figure>

When the new row comes up, enter in the following:

<pre><code class="language-c">Fonts provided by application</code></pre>

Then, under <code>Item 0</code>, we need to add our font's name. The <code>plist</code> should look like the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd931589-d376-461f-a3db-6fb610f1340b/settings-plistfont-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd931589-d376-461f-a3db-6fb610f1340b/settings-plistfont-preview-opt.png" alt="Pixel digivolve.otf" width="448" height="63" /></a><figcaption>Font added to <code>plist</code> successfully!</figcaption></figure>

The font should be ready to use! We should do a quick test to make sure it works as intended. Move to <code>GameScene.swift</code>, and in <code>sceneDidLoad</code> add the following code at the top of the function:

<pre><code class="language-c">let label = SKLabelNode(fontNamed: "PixelDigivolve")
label.text = "Hello World!"
label.position = CGPoint(x: size.width / 2, y: size.height / 2)
label.zPosition = 1000

addChild(label)</code></pre>

Does it work?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2cec232-20a0-42d0-8dc8-8234f1840907/screen-withtext-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2cec232-20a0-42d0-8dc8-8234f1840907/screen-withtext-preview-opt.png" alt="Hello world!" width="500" height="375" /></a><figcaption>Testing our <code>SKLabelNode</code>. Oh no! The "Hello World" label is back.</figcaption></figure>

If it works, then you've done everything correctly. If not, then something is wrong. Code With Chris has a more in-depth <a href="https://codewithchris.com/common-mistakes-with-adding-custom-fonts-to-your-ios-app/">troubleshooting guide</a>, but note that it is for an older version of Swift, so you will have to make minor tweaks to bring it up to Swift 3.

Now that we can load in custom fonts, we can start on our HUD. Delete the "Hello World" label, because we only used it to make sure our font loads. The HUD will be an <code>SKNode</code>, acting like a container for our HUD elements. This is the same process we followed when creating the background node in lesson one.

Create the <code>HudNode.swift</code> file using the usual methods, and enter the following code:

<pre><code class="language-c">import SpriteKit

class HudNode : SKNode {
  private let scoreKey = "RAINCAT_HIGHSCORE"
  private let scoreNode = SKLabelNode(fontNamed: "PixelDigivolve")
  private(set) var score : Int = 0
  private var highScore : Int = 0
  private var showingHighScore = false

  /// Set up HUD here.
  public func setup(size: CGSize) {
    let defaults = UserDefaults.standard

    highScore = defaults.integer(forKey: scoreKey)

    scoreNode.text = "\(score)"
    scoreNode.fontSize = 70
    scoreNode.position = CGPoint(x: size.width / 2, y: size.height - 100)
    scoreNode.zPosition = 1

    addChild(scoreNode)
  }

  /// Add point.
  /// - Increments the score.
  /// - Saves to user defaults.
  /// - If a high score is achieved, then enlarge the scoreNode and update the color.
  public func addPoint() {
    score += 1

    updateScoreboard()

    if score &gt; highScore {

      let defaults = UserDefaults.standard

      defaults.set(score, forKey: scoreKey)

      if !showingHighScore {
        showingHighScore = true

        scoreNode.run(SKAction.scale(to: 1.5, duration: 0.25))
        scoreNode.fontColor = SKColor(red:0.99, green:0.92, blue:0.55, alpha:1.0)
      }
    }
  }

  /// Reset points.
  /// - Sets score to zero.
  /// - Updates score label.
  /// - Resets color and size to default values.
  public func resetPoints() {
    score = 0

    updateScoreboard()

    if showingHighScore {
      showingHighScore = false

      scoreNode.run(SKAction.scale(to: 1.0, duration: 0.25))
      scoreNode.fontColor = SKColor.white
    }
  }

  /// Updates the score label to show the current score.
  private func updateScoreboard() {
    scoreNode.text = "\(score)"
  }
}</code></pre>

Before we do anything else, open up <code>Constants.swift</code> and add the following line to the bottom of the file — we will be using it to retrieve and persist the high score:

<pre><code class="language-c">let ScoreKey = "RAINCAT_HIGHSCORE"</code></pre>

In the code, we have five variables that pertain to the scoreboard. The first variable is the actual <code>SKLabelNode</code>, which we use to present the label. Next is our variable to hold the current score; then the variable that holds the best score. The last variable is a boolean that tells us whether we are currently presenting the high score (we use this to establish whether we need to run an <code>SKAction</code> to increase the scale of the scoreboard and to colorize it to the yellow of the floor).

The first function, <code>setup(size:)</code>, is there just to set everything up. We set up the <code>SKLabelNode</code> the same way we did earlier. The <code>SKNode</code> class does not have any size properties by default, so we need to create a way to set a size to position our <code>scoreNode</code> label. We're also fetching the current high score from <a href="https://developer.apple.com/reference/foundation/userdefaults"><code>UserDefaults</code></a>. This is a quick and easy way to save small chunks of data, but it isn't secure. Because we're not worried about security for this example, <code>UserDefaults</code> is perfectly fine.

In our <code>addPoint()</code>, we're incrementing the current <code>score</code> variable and checking whether the user has gotten a high score. If they have a high score, then we save that score to <code>UserDefaults</code> and check whether we are currently showing the best score. If the user has achieved a high score, we can animate the size and color of <code>scoreNode</code>.

In the <code>resetPoints()</code> function, we set the current score to <code>0</code>. We then need to check whether we were showing the high score, and reset the size and color to the default values if needed.

Finally, we have a small function named <code>updateScoreboard</code>. This is an internal function to set the score to <code>scoreNode</code>'s text. This is called in both <code>addPoint()</code> and <code>resetPoints()</code>.

## Hooking Up The HUD

We need to test whether our HUD is working correctly. Move over to <code>GameScene.swift</code>, and add the following line below the <code>foodNode</code> variable at the top of the file:

<pre><code class="language-c">private let hudNode = HudNode()</code></pre>

Add the following two lines in the <code>sceneDidLoad()</code> function, near the top:

<pre><code class="language-c">hudNode.setup(size: size)
addChild(hudNode)</code></pre>

Then, in the <code>spawnCat()</code> function, reset the points in case the cat has fallen off the screen. Add the following line after adding the cat sprite to the scene:

<pre><code class="language-c">hudNode.resetPoints()</code></pre>

Next, in the <code>handleCatCollision(contact:)</code> function, we need to reset the score again when the cat is hit by rain. In the <code>switch</code> statement at the end of the function — when the other body is a <code>RainDropCategory</code> — add the following line:

<pre><code class="language-c">hudNode.resetPoints()</code></pre>

Finally, we need to tell the scoreboard when the user has earned points. At the end of the file in <code>handleFoodHit(contact:)</code>, find the following lines up to here:

<pre><code class="language-c">//TODO increment points
print("fed cat")</code></pre>

And replace them with this:

<pre><code class="language-c">hudNode.addPoint()</code></pre>

Voilà!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939cdd88-829c-459a-b7e5-23c4db19f952/raincat-scoring-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939cdd88-829c-459a-b7e5-23c4db19f952/raincat-scoring-preview-opt.png" alt="HUD unlocked!" width="500" height="375" /></a><figcaption>HUD unlocked!</figcaption></figure>

You should see the HUD in action. Run around and collect some food. The first time you collect food, you should see the score turn yellow and grow in scale. When you see this happen, let the cat get hit. If the score resets, then you'll know you are on the right track!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f64069-fb6a-4284-a537-6da5753ddf42/raincat-scoreincrease-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f64069-fb6a-4284-a537-6da5753ddf42/raincat-scoreincrease-preview-opt.png" alt="High Score!" width="500" height="375" /></a><figcaption>Highest score ever (… at the time of writing)!</figcaption></figure>

## The Next Scene

That's right, we are moving to another scene! In fact, when completed, this will be the first screen of our app. Before you do anything else, open up <code>Constants.swift</code> and add the following line to the bottom of the file — we will be using it to retrieve and persist the high score:

<pre><code class="language-c">let ScoreKey = "RAINCAT_HIGHSCORE"</code></pre>

Create the new scene, place it under the "Scenes" folder, and call it <code>MenuScene.swift</code>. Enter the following code in the <code>MenuScene.swift</code> file:

<pre><code class="language-c">import SpriteKit

class MenuScene : SKScene {
  let startButtonTexture = SKTexture(imageNamed: "button_start")
  let startButtonPressedTexture = SKTexture(imageNamed: "button_start_pressed")
  let soundButtonTexture = SKTexture(imageNamed: "speaker_on")
  let soundButtonTextureOff = SKTexture(imageNamed: "speaker_off")

  let logoSprite = SKSpriteNode(imageNamed: "logo")
  var startButton : SKSpriteNode! = nil
  var soundButton : SKSpriteNode! = nil

  let highScoreNode = SKLabelNode(fontNamed: "PixelDigivolve")

  var selectedButton : SKSpriteNode?

  override func sceneDidLoad() {
    backgroundColor = SKColor(red:0.30, green:0.81, blue:0.89, alpha:1.0)

    //Set up logo - sprite initialized earlier
    logoSprite.position = CGPoint(x: size.width / 2, y: size.height / 2 + 100)

    addChild(logoSprite)

    //Set up start button
    startButton = SKSpriteNode(texture: startButtonTexture)
    startButton.position = CGPoint(x: size.width / 2, y: size.height / 2 - startButton.size.height / 2)

    addChild(startButton)

    let edgeMargin : CGFloat = 25

    //Set up sound button
    soundButton = SKSpriteNode(texture: soundButtonTexture)
    soundButton.position = CGPoint(x: size.width - soundButton.size.width / 2 - edgeMargin, y: soundButton.size.height / 2 + edgeMargin)

    addChild(soundButton)

    //Set up high-score node
    let defaults = UserDefaults.standard

    let highScore = defaults.integer(forKey: ScoreKey)

    highScoreNode.text = "\(highScore)"
    highScoreNode.fontSize = 90
    highScoreNode.verticalAlignmentMode = .top
    highScoreNode.position = CGPoint(x: size.width / 2, y: startButton.position.y - startButton.size.height / 2 - 50)
    highScoreNode.zPosition = 1

    addChild(highScoreNode)
  }
}</code></pre>

Because this scene is relatively simple, we won't be creating any special classes. Our scene will consist of two buttons. These could be (and possibly deserve to be) their own class of <code>SKSpriteNodes</code>, but because they are different enough, we will not need to create new classes for them. This is an important tip for when you build your own game: You need to be able to determine where to stop and refactor code when things get complex. Once you've added more than three or four buttons to a game, it might be time to stop and refactor the menu button's code into its own class.

The code above isn't doing anything special; it is setting the positions of four sprites. We are also setting the scene's background color, so that the whole background is the correct value. A nice tool to generate color codes from HEX strings for Xcode is <a href="https://uicolor.xyz/">UI Color</a>. The code above is also setting the textures for our button states. The button to start the game has a normal state and a pressed state, whereas the sound button is a toggle. To simplify things for the toggle, we will be changing the alpha value of the sound button upon the user's press. We are also pulling and setting the high-score <code>SKLabelNode</code>.

Our <code>MenuScene</code> is looking pretty good. Now we need to show the scene when the app loads. Move to <code>GameViewController.swift</code> and find the following line:

<pre><code class="language-c">let sceneNode = GameScene(size: view.frame.size)</code></pre>

Replace it with this:

<pre><code class="language-c">let sceneNode = MenuScene(size: view.frame.size)</code></pre>

This small change will load <code>MenuScene</code> by default, instead of <code>GameScene</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a705357-de9f-4b17-a5dc-11fde6214a4f/raincat-newscene-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a705357-de9f-4b17-a5dc-11fde6214a4f/raincat-newscene-preview-opt.png" alt="Our new scene!" width="500" height="375" /></a><figcaption>Our new scene! Note the 1.0 frames per second: Nothing is moving, so no need to update anything.</figcaption></figure>

## Button States

Buttons can be tricky in SpriteKit. Plenty of third-party options are available (I even made one myself), but in theory you only need to know the three touch methods:

*   `touchesBegan(_ touches: with event:)`
*   `touchesMoved(_ touches: with event:)`
*   `touchesEnded(_ touches: with event:)`

We covered this briefly when updating the umbrella, but now we need to know the following: which button was touched, whether the user released their tap or clicked that button, and whether the user is still touching it. This is where our <code>selectedButton</code> variable comes into play. When a touch begin, we can capture the button that the user started clicking with that variable. If they drag outside the button, we can handle this and give the appropriate texture to it. When they release the touch, we can then see whether they are still touching inside the button. If they are, then we can apply the associated action to it. Add the following lines to the bottom of <code>MenuScene.swift</code>:

<pre><code class="language-c">override func touchesBegan(_ touches: Set, with event: UIEvent?) {
  if let touch = touches.first {
    if selectedButton != nil {
      handleStartButtonHover(isHovering: false)
      handleSoundButtonHover(isHovering: false)
    }

    // Check which button was clicked (if any)
    if startButton.contains(touch.location(in: self)) {
      selectedButton = startButton
      handleStartButtonHover(isHovering: true)
    } else if soundButton.contains(touch.location(in: self)) {
      selectedButton = soundButton
      handleSoundButtonHover(isHovering: true)
    }
  }
}

override func touchesMoved(_ touches: Set, with event: UIEvent?) {
  if let touch = touches.first {

    // Check which button was clicked (if any)
    if selectedButton == startButton {
      handleStartButtonHover(isHovering: (startButton.contains(touch.location(in: self))))
    } else if selectedButton == soundButton {
      handleSoundButtonHover(isHovering: (soundButton.contains(touch.location(in: self))))
    }
  }
}

override func touchesEnded(_ touches: Set, with event: UIEvent?) {
  if let touch = touches.first {

    if selectedButton == startButton {
      // Start button clicked
      handleStartButtonHover(isHovering: false)

      if (startButton.contains(touch.location(in: self))) {
        handleStartButtonClick()
      }

    } else if selectedButton == soundButton {
      // Sound button clicked
      handleSoundButtonHover(isHovering: false)

      if (soundButton.contains(touch.location(in: self))) {
        handleSoundButtonClick()
      }
    }
  }

  selectedButton = nil
}

/// Handles start button hover behavior
func handleStartButtonHover(isHovering : Bool) {
  if isHovering {
    startButton.texture = startButtonPressedTexture
  } else {
    startButton.texture = startButtonTexture
  }
}

/// Handles sound button hover behavior
func handleSoundButtonHover(isHovering : Bool) {
  if isHovering {
    soundButton.alpha = 0.5
  } else {
    soundButton.alpha = 1.0
  }
}

/// Stubbed out start button on click method
func handleStartButtonClick() {
  print("start clicked")
}

/// Stubbed out sound button on click method
func handleSoundButtonClick() {
  print("sound clicked")
}</code></pre>

This is simple button-handling for our two buttons. In <code>touchesBegan(_ touches: with events:)</code>, we start off by checking whether we have any currently selected buttons. If we do, we need to reset the state of the button to unpressed. Then, we need to check whether any button is pressed. If one is pressed, it will show the highlighted state for the button. Then, we set <code>selectedButton</code> to the button for use in the other two methods.

In <code>touchesMoved(_ touches: with events:)</code>, we check which button was originally touched. Then, we check whether the current touch is still within the bounds of <code>selectedButton</code>, and we update the highlighted state from there. The <code>startButton</code>'s highlighted state changes the texture to the pressed-state's texture, where the <code>soundButton</code>'s highlighted state has the alpha value of the sprite set to 50%.

Finally, in <code>touchesEnded(_ touches: with event:)</code>, we check again which button is selected, if any, and then whether the touch is still within the bounds of the button. If all cases are satisfied, we call <code>handleStartButtonClick()</code> or <code>handleSoundButtonClick()</code> for the correct button.</p>

## A Time For Action

Now that we have the basic button behavior down, we need an event to trigger when they are clicked. The easier button to implement is <code>startButton</code>. On click, we only need to present the <code>GameScene</code>. Update <code>handleStartButtonClick()</code> in the <code>MenuScene.swift</code> function to the following code:

<pre><code class="language-c">func handleStartButtonClick() {
  let transition = SKTransition.reveal(with: .down, duration: 0.75)
  let gameScene = GameScene(size: size)
  gameScene.scaleMode = scaleMode
  view?.presentScene(gameScene, transition: transition)
}</code></pre>

If you run the app now and press the button, the game will start!

Now we need to implement the mute toggle. We already have a sound manager, but we need to be able to tell it whether muting is on or off. In <code>Constants.swift</code>, we need to add a key to persist when muting is on. Add the following line:

<pre><code class="language-c">let MuteKey = "RAINCAT_MUTED"</code></pre>

We will use this to save a boolean value to <code>UserDefaults</code>. Now that this is set up, we can move into <code>SoundManager.swift</code>. This is where we will check and set <code>UserDefaults</code> to see whether muting is on or off. At the top of the file, under the <code>trackPosition</code> variable, add the following line:

<pre><code class="language-c">private(set) var isMuted = false</code></pre>

This is the variable that the main menu (and anything else that will play sound) checks to determine whether sound is allowed. We initialize it as <code>false</code>, but now we need to check <code>UserDefaults</code> to see what the user wants. Replace the <code>init()</code> function with the following:

<pre><code class="language-c">private override init() {
  //This is private, so you can only have one Sound Manager ever.
  trackPosition = Int(arc4random_uniform(UInt32(SoundManager.tracks.count)))

  let defaults = UserDefaults.standard

  isMuted = defaults.bool(forKey: MuteKey)
}
</code></pre>

Now that we have a default value for <code>isMuted</code>, we need the ability to change it. Add the following code to the bottom of <code>SoundManager.swift</code>:

<pre><code class="language-c">func toggleMute() -&gt; Bool {
  isMuted = !isMuted

  let defaults = UserDefaults.standard
  defaults.set(isMuted, forKey: MuteKey)
  defaults.synchronize()

  if isMuted {
    audioPlayer?.stop()
  } else {
    startPlaying()
  }

  return isMuted
}</code></pre>

This method will toggle our muted variable, as well as update <code>UserDefaults</code>. If the new value is not muted, playback of the music will begin; if the new value is muted, playback will not begin. Otherwise, we will stop the current track from playing. After this, we need to edit the <code>if</code> statement in <code>startPlaying()</code>.

Find the following line:

<pre><code class="language-c">if audioPlayer == nil || audioPlayer?.isPlaying == false {</code></pre>

And replace it with this:

<pre><code class="language-c">if !isMuted &amp;&amp; (audioPlayer == nil || audioPlayer?.isPlaying == false) {</code></pre>

Now, if muting is off and either the audio player is not set or the current audio player is no longer playing, we will play the next track.

From here, we can move back into <code>MenuScene.swift</code> to finish up our mute button. Replace <code>handleSoundbuttonClick()</code> with the following code:

<pre><code class="language-c">func handleSoundButtonClick() {
  if SoundManager.sharedInstance.toggleMute() {
    //Is muted
    soundButton.texture = soundButtonTextureOff
  } else {
    //Is not muted
    soundButton.texture = soundButtonTexture
  }
}</code></pre>

This toggles the sound in <code>SoundManager</code>, checks the result and then appropriately sets the texture to show the user whether the sound is muted or not. We are almost done! We only need to set the initial texture of the button on launch. In <code>sceneDidLoad()</code>, find the following line:

<pre><code class="language-c">soundButton = SKSpriteNode(texture: soundButtonTexture)</code></pre>

And replace it with this:

<pre><code class="language-c">soundButton = SKSpriteNode(texture: SoundManager.sharedInstance.isMuted ?
  soundButtonTextureOff : soundButtonTexture)</code></pre>

The example above uses a <a href="https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/BasicOperators.html#//apple_ref/doc/uid/TP40014097-CH6-ID60">ternary operator</a> to set the correct texture.

Now that the music is hooked up, we can move to <code>CatSprite.swift</code> to disable the cat meowing when muting is on. In the <code>hitByRain()</code>, we can add the following <code>if</code> statement after removing the walking action:

<pre><code class="language-c">if SoundManager.sharedInstance.isMuted {
  return
}</code></pre>

This statement will return whether the user has muted the app. Because of this, we will completely ignore our <code>currentRainHits</code>, <code>maxRainHits</code> and meowing sound effects.

After all of that, now it is time to try out our mute button. Run the app and verify whether it is playing and muting sounds appropriately. Mute the sound, close the app, and reopen it. Make sure that the mute setting persists. Note that if you just mute and rerun the app from Xcode, you might not have given enough time for <code>UserDefaults</code> to save. Play the game, and make sure the cat never meows when you are muted.</p>

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/189700402" width="640" height="481" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<figcaption>Testing out the button functionality.</figcaption></figure>

## Exiting The Game

Now that we have the first type of button for the main menu, we can get into some tricky business by adding the quit button to our game scene. Some interesting interactions can come up with our style of game; currently, the umbrella will move to wherever the user touches or moves their touch. Obviously, the umbrella moving to the quit button when the user is attempting to exit the game is a pretty poor user experience, so we will attempt to stop this from happening.

The quit button we are implementing will mimic the start game button that we added earlier, with much of the process staying the same. The change will be in how we handle touches. Get your <code>quit_button</code> and <code>quit_button_pressed</code> assets into the <code>Assets.xcassets</code> file, and add the following code to the <code>HudNode.swift</code> file:

<pre><code class="language-c">private var quitButton : SKSpriteNode!
private let quitButtonTexture = SKTexture(imageNamed: "quit_button")
private let quitButtonPressedTexture = SKTexture(imageNamed: "quit_button_pressed")</code></pre>

This will handle our <code>quitButton</code> reference, along with the textures that we will set for the button states. To ensure that we don't inadvertently update the umbrella while trying to quit, we need a variable that tells the HUD (and the game scene) that we are interacting with the quit button and not the umbrella. Add the following code below the <code>showingHighScore</code> boolean variable:

<pre><code class="language-c">private(set) var quitButtonPressed = false</code></pre>

Again, this is a variable that only the <code>HudNode</code> can set but that other classes can check. Now that our variables are set up, we can add in the button to the HUD. Add the following code to the <code>setup(size:)</code> function:

<pre><code class="language-c">quitButton = SKSpriteNode(texture: quitButtonTexture)
let margin : CGFloat = 15
quitButton.position = CGPoint(x: size.width - quitButton.size.width - margin, y: size.height - quitButton.size.height - margin)
quitButton.zPosition = 1000

addChild(quitButton)</code></pre>

The code above will set the quit button with the texture of our non-pressed state. We're also setting the position to the upper-right corner and setting the <code>zPosition</code> to a high number in order to force it to always draw on top. If you run the game now, it will show up in <code>GameScene</code>, but it will not be clickable yet.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/956d9556-bab0-4c3e-b723-ce32ed201a0d/raincat-quit-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/956d9556-bab0-4c3e-b723-ce32ed201a0d/raincat-quit-preview-opt.png" alt="Quit button" width="500" height="375" /></a><figcaption>Note the new quit button in our HUD.</figcaption></figure>

Now that the button has been positioned, we need to be able to interact with it. Right now, the only place where we have interaction in <code>GameScene</code> is when we are interacting with <code>umbrellaSprite</code>. In our example, the HUD will have priority over the umbrella, so that users don't have to move the umbrella out of the way in order to exit. We can create the same functions in <code>HudNode.swift</code> to mimic the touch functionality in <code>GameScene.swift</code>. Add the following code to <code>HudNode.swift</code>:

<pre><code class="language-c">func touchBeganAtPoint(point: CGPoint) {
  let containsPoint = quitButton.contains(point)

  if quitButtonPressed &amp;&amp; !containsPoint {
    //Cancel the last click
    quitButtonPressed = false
    quitButton.texture = quitButtonTexture
  } else if containsPoint {
    quitButton.texture = quitButtonPressedTexture
    quitButtonPressed = true
  }
}

func touchMovedToPoint(point: CGPoint) {
  if quitButtonPressed {
    if quitButton.contains(point) {
      quitButton.texture = quitButtonPressedTexture
    } else {
      quitButton.texture = quitButtonTexture
    }
  }
}

func touchEndedAtPoint(point: CGPoint) {
  if quitButton.contains(point) {
    //TODO tell the gamescene to quit the game
  }

  quitButton.texture = quitButtonTexture
}</code></pre>

The code above is a lot like the code that we created for <code>MenuScene</code>. The difference is that there is only one button to keep track of, so we can handle everything within these touch methods. Also, because we will know the location of the touch in <code>GameScene</code>, we can just check whether our button contains the touch point.

Move over to <code>GameScene.swift</code>, and replace the <code>touchesBegan(_ touches with event:)</code> and <code>touchesMoved(_ touches: with event:)</code> methods with the following code:

<pre><code class="language-c">override func touchesBegan(_ touches: Set, with event: UIEvent?) {
  let touchPoint = touches.first?.location(in: self)

  if let point = touchPoint {
    hudNode.touchBeganAtPoint(point: point)

    if !hudNode.quitButtonPressed {
      umbrellaNode.setDestination(destination: point)
    }
  }
}

override func touchesMoved(_ touches: Set, with event: UIEvent?) {
  let touchPoint = touches.first?.location(in: self)

  if let point = touchPoint {
    hudNode.touchMovedToPoint(point: point)

    if !hudNode.quitButtonPressed {
      umbrellaNode.setDestination(destination: point)
    }
  }
}

override func touchesEnded(_ touches: Set, with event: UIEvent?) {
  let touchPoint = touches.first?.location(in: self)

  if let point = touchPoint {
    hudNode.touchEndedAtPoint(point: point)
  }
}
</code></pre>

Here, each method handles everything in pretty much the same way. We're telling the HUD that the user has interacted with the scene. Then, we check whether the quit button is currently capturing the touches. If it is not, then we move the umbrella. We've also added the <code>touchesEnded(_ touches: with event:)</code> function to handle the end of the click for the quit button, but we are still not using it for <code>umbrellaSprite</code>.</p>

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/189701318" width="640" height="482" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<figcaption>Clicking the quit button will not move the umbrella, but clicking elsewhere will.</figcaption></figure>

</figure>

Now that we have a button, we need a way to have it affect <code>GameScene</code>. Add the following line to the top of <code>HudeNode.swift</code>:

<pre><code class="language-c">var quitButtonAction : (() -&gt; ())?</code></pre>

This is a generic <a href="https://www.weheartswift.com/closures/">closure</a> that has no input and no output. We will set this with code in the <code>GameScene.swift</code> file and call it when we click the button in <code>HudNode.swift</code>. Then, we can replace the <code>TODO</code> in the code we created earlier in the <code>touchEndedAtPoint(point:)</code> function with this:

<pre><code class="language-c">if quitButton.contains(point) &amp;&amp; quitButtonAction != nil {
  quitButtonAction!()
}</code></pre>

Now, if we set the <code>quitButtonAction</code> closure, it will be called from this point.

To set up the <code>quitButtonAction</code> closure, we need to move over to <code>GameScene.swift</code>. In <code>sceneDidLoad()</code>, we can replace our HUD setup with the following code:

<pre><code class="language-c">hudNode.setup(size: size)

hudNode.quitButtonAction = {
  let transition = SKTransition.reveal(with: .up, duration: 0.75)

  let gameScene = MenuScene(size: self.size)
  gameScene.scaleMode = self.scaleMode

  self.view?.presentScene(gameScene, transition: transition)

  self.hudNode.quitButtonAction = nil
}

addChild(hudNode)
</code></pre>

Run the app, press play, and then press quit. If you are back at the main menu, then your quit button is working as intended. In the closure that we created, we initialized a transition to the <code>MenuScene</code>. And we set this closure to the <code>HUD</code> node to run when the quit button is clicked. Another important line here is when we set the <code>quitButtonAction</code> to <code>nil</code>. The reason for this is that a retain cycle is occurring. The scene is holding a reference to the HUD where the HUD is holding a reference to the scene. Because there is a reference to both objects, neither will be disposed of when it comes time for garbage collection. In this case, every time we enter and leave <code>GameScene</code>, another instance of it will be created and never released. This is bad for performance, and the app will eventually run out of memory. There are a number of ways to avoid this, but in our case we can just remove the reference to <code>GameScene</code> from the HUD, and the scene and HUD will be terminated once we go back to the <code>MenuScene</code>. <a href="https://krakendev.io/blog/weak-and-unowned-references-in-swift">Krakendev has a deeper explanation</a> of reference types and how to avoid these cycles.

Now, move to <code>GameViewController.swift</code>, and remove or comment out the following three lines of code:

<pre><code class="language-c">view.showsPhysics = true
view.showsFPS = true
view.showsNodeCount = true</code></pre>

With the debugging data out of the way, the game is looking really good! Congratulations: We are currently into beta! Check out the final code from today <a href="https://github.com/thirteen23/RainCat/releases/tag/smashing-magazine-lesson-three">on GitHub</a>.</p>

## Final Thoughts

This is the final lesson of a three-part tutorial, and if you made it this far, you just did a lot of work on your game. In this tutorial, you went from a scene that had absolutely nothing in it, to a completed game. Congrats! In <a href="https://www.smashingmagazine.com/2016/11/how-to-build-a-spritekit-game-in-swift-3-part-1/">lesson one</a>, we added the floor, raindrops, background and umbrella sprites. We also played around with physics and made sure that our raindrops don't pile up. We started out with collision detection and worked on culling nodes so that we would not run out of memory. We also added some user interaction by allowing the umbrella to move around towards where the user touches on the screen.

In <a href="https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-2/">lesson two</a>, we added the cat and food, along with custom spawning methods for each of them. We updated our collision detection to allow for the cat and food sprites. We also worked on the movement of the cat. The cat gained a purpose: Eat every bit of food available. We added simple animation for the cat and added custom interactions between the cat and the rain. Finally, we added sound effects and music to make it feel like a complete game.

In this last lesson, we created a heads-up display to hold our score label, as well as our quit button. We handled actions across nodes and enabled the user to quit with a callback from the HUD node. We also added another scene that the user can launch into and can get back to after clicking the quit button. We handled the process for starting the game and for controlling sound in the game.</p>

### Where To Go From Here

We put in a lot of time to get this far, but there is still a lot of work that can go into this game. RainCat continues development still, and it is <a href="https://itunes.apple.com/us/app/raincat/id1152624676?ls=1&amp;mt=8">available in the App Store</a>. Below is a list of wants and needs to be added. Some of the items have been added, while others are still pending:

*   Add in icons and a splash screen.
*   Finalize the main menu (simplified for the tutorial).
*   Fix bugs, including rogue raindrops and multiple food spawning.
*   Refactor and optimize the code.
*   Change the color palette of the game based on the score.
*   Update the difficulty based on the score.
*   Animate the cat when food is right above it.
*   Integrate Game Center.
*   Give credit (including proper credit for music tracks).</p>

<a href="https://github.com/thirteen23/RainCat">Keep track on GitHub</a> because these changes will be made in future. If you have any questions about the code, feel free to drop us a line at <a href="mailto:hello@thirteen23.com">hello@thirteen23.com</a> and we can discuss it. If certain topics get enough attention, maybe we can write another article discussing the topic.</p>

### Thank You!

I want to thank all of the people who helped in the process of creating the game and developing the articles that go along with it.

*   [Cathryn Rowe](https://www.thirteen23.com/about/#cathryn-rowe) For the initial art, design and editing, and for publishing the articles in our [Garage](https://www.thirteen23.com/garage/).
*   [Morgan Wheaton](https://www.thirteen23.com/about/#morgan-wheaton) For the final menu design and color palettes (which will look awesome once I actually implement these features — stay tuned).
*   [Nikki Clark](https://www.thirteen23.com/about/#nikki-clark) For the awesome headers and dividers in the articles and for help with editing the articles.
*   [Laura Levisay](https://www.thirteen23.com/about/#laura-levisay) For all of the awesome GIFs in the articles and for sending me cute cat GIFs for moral support.
*   [Tom Hudson](https://www.thirteen23.com/about/#tom-hudson) For help with editing the articles and without whom this series would not have been made at all.
*   [Lani DeGuire](https://www.thirteen23.com/about/#lani-deguire) For help with editing the articles, which was a ton of work.
*   [Jeff Moon](https://www.thirteen23.com/about/#jeffrey-moon) For help editing lesson three and the ping-pong. Lots of ping-pong.
*   [Tom Nelson](https://www.thirteen23.com/about/#tom-nelson) For helping to make sure that the tutorial works as it should.

Seriously, it took a ton of people to get everything ready for this article and to release it to the store.

Thank you to everyone who reads this sentence, too.

{{< signature "da, il, al" >}}

