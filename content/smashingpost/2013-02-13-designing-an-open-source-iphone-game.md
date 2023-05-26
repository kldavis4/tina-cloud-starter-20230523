---
title: How To Design An Open-Source iPhone Game
slug: designing-an-open-source-iphone-game
image: >-
  https://www.smashingmagazine.com/wordpress/2012/06/28/create-responsive-mobile-first-wordpress-theme/attachment/responsive-wordpress-themes-splash/attachment/trustworthiness-harris-interactive-truste/attachment/sprite_sheet-500/
date: 2013-02-13T11:54:02.000Z
author: zack-grossbart
description: >-
  I love games and I’m a huge math nerd, so I made a new iPhone game based on a
  famous math problem called [The Seven Bridges of
  Königsberg](https://zgrossbart.github.com/bridges/). I’m selling it in the App
  Store, but I also want to share it with everyone, so I made it [open
  source](https://github.com/zgrossbart/bridges).
categories:
  - Mobile
  - Apps
  - Games
  - iOS
  - iPhone
---
I love games and I’m a huge math nerd, so I made a new iPhone game based on <a href="https://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg">a famous math problem</a> called <a href="https://zgrossbart.github.com/bridges/">The Seven Bridges of Königsberg</a>. I’m <a href="https://itunes.apple.com/us/app/seven-bridges/id586598714?ls=1&amp;mt=8">selling it in the App Store</a>, but I also want to share it with everyone, so I made it <a href="https://github.com/zgrossbart/bridges">open source</a>.

This article is the first in a series that will walk through iOS programming using this game as an example. This first article gives you an overview of the game and of iOS programming in general. We’ll look at a few specific pieces and see how the whole project fits together.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/10/design-your-own-mobile-game/#further-reading-on-smashingmag)

*   [<span class="headline">Creating Realistic iPhone Games With Cocos2D</span>](https://www.smashingmagazine.com/2013/04/realistic-iphone-games-cocos2d/)
*   [How To Build A SpriteKit Game In Swift 3](https://www.smashingmagazine.com/2016/11/how-to-build-a-spritekit-game-in-swift-3-part-1/)
*   [Develop A One-Of-A-Kind CSS / JS-Based Game Portfolio](https://www.smashingmagazine.com/2012/05/develop-a-one-of-a-kind-cssjs-based-game-portfolio/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)

## First Steps

This article uses the real game as the example. You’ll need a couple of things to start using the code:

{{% feature-panel %}}

1.  A Mac,
2.  The Xcode development environment from Apple, which you can [get free from Apple](https://developer.apple.com/xcode/).

After you’ve set up Xcode, go ahead and <a href="https://github.com/zgrossbart/bridges">download the project from GitHub</a>. Open it, and then run it by pressing the big “Run” button in the upper-left corner of Xcode.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0c7c53a-5a20-4e8d-96da-0b32c61a0b08/xcode-run.png"><img loading="lazy" decoding="async" class="134310" title="Running Seven Bridges in Xcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/017dcfc4-cf38-4979-82f3-55ce9f4537f9/xcode-run-500.png" alt="Running Seven Bridges in Xcode" width="500" height="500" /></a>

That will open the game in the simulator so that you can play for free and follow along with the article.</p>

## The Rules Of The Game

Seven Bridges is a puzzle game. The player visits a town of islands surrounded by rivers.

<img loading="lazy" decoding="async" class="132880" title="Hello Bridges level" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bc9a02a-478f-42b4-9493-3f3fce29f410/hello-bridges.png" alt="Hello Bridges level" width="431" height="316" />

The game’s interaction works with a single gesture: tap where you want the player to go. If you hit a bridge, you’ll cross it; if you hit a river, you’ll bounce off it.

<img loading="lazy" decoding="async" class="132881" title="Two Bridges level" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13053616-314e-464b-aade-0d56ddce64a6/two-bridges.png" alt="Two Bridges level" width="431" height="316" />

The game lets you restart the level, undo your last move and go back to the menu. There are also a few other screens to support the game.

<img loading="lazy" decoding="async" class="133203" title="Level set selector" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a9a37e5-ad59-4933-8b51-f5a68519506f/level-set-500.png" alt="Level set selector" width="500" height="333" />

<img loading="lazy" decoding="async" class="133199" title="Levels selector" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc0a43cd-14e9-4a6a-88c2-cbf1cff1b657/levels-500.png" alt="Levels selector" width="500" height="333" />

<img loading="lazy" decoding="async" class="133201" title="You won screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/671af9fd-8ef1-44b4-b504-d21bdf5eb18c/you-won-500.png" alt="You won screen" width="500" height="333" />

Confused? Check out the <a href="https://vimeo.com/55454871">Seven Bridge walkthrough video</a>.

You’ll see similar layouts in popular games such as <a href="https://en.wikipedia.org/wiki/Cut_the_Rope">Cut the Rope</a> and <a href="https://en.wikipedia.org/wiki/Where's_My_Water%3F">Where’s My Water?</a>

## Before We Start

Seven Bridges is a simple game. It doesn’t handle complex physics like <a href="https://en.wikipedia.org/wiki/Angry_birds">Angry Birds</a> does or rich textures like <a href="https://en.wikipedia.org/wiki/Infinity_Blade">Infinity Blade</a> does. Seven Bridges has just a single player who walks over bridges and bumps into rivers. It sounds easy, but a lot goes into even a simple game like this.

Seven Bridges is written in a combination of <a href="https://en.wikipedia.org/wiki/Objective-C">Objective-C</a> and <a href="https://en.wikipedia.org/wiki/Objective-C#Objective-C.2B.2B">Objective-C++</a>. If you’re used to programming in scripting languages such as JavaScript, then Objective-C will come as a shock.</p>

### Programming for iOS

Getting started with JavaScript is easy. You start with a little jQuery behind a button and go from there. Many iPhone programming tutorials make it sound like writing iPhone applications is just as easy. It’s not.

Objective-C has been around for nearly 30 years. Programming with it entails learning a large ecosystem and some fundamental concepts of how it all holds together. All of the Objective-C documentation assumes that you have a strong background in both <a href="https://en.wikipedia.org/wiki/Object-oriented_programming">object-oriented programming</a> and the <a href="https://en.wikipedia.org/wiki/C_(programming_language)">C programming language</a>.

Objective-C is very different from JavaScript, and programming with it requires an understanding of some of the old-school programming fundamentals. Make sure you’ve read a book about object-oriented programming, such as <em><a href="https://www.informit.com/store/product.aspx?isbn=020189551X">Object-Oriented Analysis and Design with Applications</a></em> by Grady Booch, as well as <em><a href="https://en.wikipedia.org/wiki/The_C_Programming_Language_(book)">The C Programming Language</a></em> by Brian Kernighan and Dennis Ritchie. Reading “<a href="https://developer.apple.com/reference/objectivec">The Objective-C Programming Language</a>” guide from Apple is also a good idea.

The news isn’t all bad. Objective-C shows its age in some areas, but the tools are well written and the runtime environment is amazing.</p>

### The Files

You already have the code on your computer, so let’s get a better idea of what we’re looking at. You can tell what each file does by looking at its extension.

*   `.h` These files are class [headers](https://en.wikipedia.org/wiki/Header_file). Each of these files represents the public information available about a single class or object in the project.
*   `.m` These files are Objective-C implementation files.
*   `.mm` These files are Objective-C++ implementation files. Objective-C++ is a hybrid in which you can use parts of Objective-C and [C++](https://en.wikipedia.org/wiki/C%2B%2B) in the same file. Seven Bridges uses Objective-C++ so that it can take advantage of frameworks written in C++.
*   `.xib` These files define visual [views](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaViewsGuide/WhatAreViews/WhatAreViews.html#//apple_ref/doc/uid/TP40002978-CH5-SW1) in the game where you can lay out buttons and other controls.
*   `.png` These files are individual images used in the game.
*   `.pvr.gz` These files contain large sets of images called sprite sheets. The images are combined into a single file so that they load faster and take up less space.
*   `.plist` These are XML properties files. They define the basics of how the application works and the positions of the images in each sprite sheet.
*   `.m4a` These are audio files that provide the sounds for the game.

Xcode projects also include a folder named <code>your project.xcodeproj</code> containing all of the project’s configuration files. Mine is named <code>bridges2</code> because I messed up the project so badly that I had to start over.

## The Frameworks

In addition to the standard Objective-C libraries, Seven Bridges uses three major frameworks.</p>

### UIKit

Every iOS application starts with <a href="https://developer.apple.com/library/ios/#documentation/uikit/reference/UIKit_Framework/_index.html">UIKit</a>. This comprehensive framework from Apple provides all of the basic controls your application uses, such as windows, buttons and text fields. Most of the classes in UIKit start with the prefix <code>UI</code>, like <code>UIWindow</code> and <code>UIButton</code>.

The easiest way to work with UIKit is by using the visual editor provided with Xcode. Xcode makes it easy to drag and drop controls into your application. It works well for business applications, but it wouldn’t know anything about the rivers or bridges in my game. For that, I need a gaming framework and a bit of code.</p>

### Cocos2d

You could draw on the screen directly with <a href="https://en.wikipedia.org/wiki/Opengl">OpenGL</a>, but that signs you up for a lot of work in managing each pixel on the screen. Game libraries provide higher-level support for placing images, creating animations and managing your game. There are a few for iOS.

I chose Cocos2d for iPhone because it’s well supported, has a simple API and comes with a lot of examples. It also has <a href="https://www.raywenderlich.com/">Ray Wenderlich</a>’s excellent tutorials. Ray is a prolific writer about iOS games; every time I searched for a new topic, it led me back to him. His <a href="https://www.raywenderlich.com/606/how-to-use-box2d-for-just-collision-detection-with-cocos2d-iphone">tutorial about collision detection</a> provided the fundamentals for my game, and his <a href="https://www.raywenderlich.com/352/how-to-make-a-simple-iphone-game-with-cocos2d-tutorial">simple iPhone game with a Cocos2D tutorial</a> is a perfect little sample game.

Cocos2d handles all of the animations in my game, as well as the scenes where you’re actually playing; it also handles <a href="https://en.wikipedia.org/wiki/Sprite_(computer_graphics)">sprites</a>, which we’ll get to a little later. It was originally written in Python for desktop applications, so <strong>make sure to search for “Cocos2d iPhone”</strong> when you’re looking for help on the Web. Cocos2d files start with the prefix <code>CC</code>.

Cocos2d handles user interactions, but it can’t handle interactions with objects. I need to know when the player runs into a river, bridge or any other object. That type of collision detection is made much easier with a physics library such as Box2d.</p>

### Box2d

<a href="https://en.wikipedia.org/wiki/Box2d">Box2d</a> is a <a href="https://en.wikipedia.org/wiki/Physics_engine">physics engine</a> written in portable C++. It can handle complex variables like gravity and friction, but we’re only using it for collision detection. Box2d files start with the prefix <code>b2</code>.

My game doesn’t use the complex physics of swinging candy from Cut the Rope or of sloshing liquids from Where’s My Water? It just handles a player walking around the screen and bumping into things. Box2d tells me when those bumps happen, and my code handles the rest.

<img loading="lazy" decoding="async" class="133202" title="Player bump interaction" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e6c973b-26aa-4041-aa52-04558cfa3eb7/bump-500.png" alt="Player bump interaction" width="500" height="352" />

In this article, we’ll see how to use these three frameworks together to build a scene, integrate sprites, respond to user gestures and detect collisions.</p>

## Building A Scene

The playable area of the game is drawn with <code><a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm">LevelLayer</a></code>, which extends the Cocos2d class <code>CCLayerColor</code>. This layer handles all of the drawing in the game and the responses when the user taps on the game screen.

The game is made up of a set of images called sprites. Each item in the game’s scene, such as a bridge or a piece of a river, is made up of a separate image file.

<img loading="lazy" decoding="async" class="132884" title="The 7 Bridges sprite sheet" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39421897-060f-4cd0-b367-21a47d6a0396/sprite-sheet-500.png" alt="The 7 Bridges sprite sheet" width="500" height="298" />

Images used this way, instead of being created programmatically, perform much faster and can include subtleties such as shading and texture without needing a lot of code. The technique also makes delegating artwork easier because the artist doesn’t need to know anything about Objective-C.

The sprites all fit together into a single file called a <strong>sprite sheet</strong>. Cocos2d takes that image and a properties file containing coordinates and creates the individual images from it when the application runs.

The real reason to use a sprite sheet is performance. Ray Wenderlich has written a good <a href="https://www.raywenderlich.com/2361/how-to-create-and-optimize-sprite-sheets-in-cocos2d-with-texture-packer-and-pixel-formats">article comparing sprite sheet performance to individual images</a>. The short story is that sprite sheets are much faster than images loaded individually.

Managing sprite sheets manually is a real pain, so I used <a href="https://www.codeandweb.com/texturepacker">TexturePacker</a>. It costs a little money, but $25 is well worth the hours of adjusting pixel coordinates it saved me. TexturePacker can also convert a sprite sheet to PVR (the internal image format for iOS) and compress it with Gzip so that it loads even faster.

Once we’ve created the sprite sheet, we’re ready to add the sprites to a scene.</p>

### Adding the Sprites

Xcode makes it easy to drag and drop images into a view, but that won’t work for dynamic scenes like our game levels. We’ll need to write some code.

Cocos2d interprets our sprite sheet with the <code>CCSpriteBatchNode</code> class. We initialize the sprite sheet once for the application and then use the individual items when we build our level.

<pre><code class="language-javascript">CCSpriteBatchNode *spriteSheet = [[CCSpriteBatchNode batchNodeWithFile:@"bridgesprites.pvr.gz"
                                 capacity:150] retain];
[[CCSpriteFrameCache sharedSpriteFrameCache]
addSpriteFramesWithFile:@"bridgesprites.plist"];
[self addChild:spriteSheet];</code></pre>

This code creates a new sprite sheet with our sprites file, initializes it with the properties file that defines the images in the sheet, and adds the sheet as a child to our current scene. You can see the full code for this in the <code>init</code> method of <code><a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm">LevelLayer.mm</a></code>.

Now that we have the sheet, we can use it to load individual sprites, like this:

<pre><code class="language-javascript">CCSprite *bridge = [CCSprite spriteWithSpriteFrameName:@"bridge_v.png"];
[spriteSheet addChild:bridge];
bridge.position = ccp(100, 100);</code></pre>

This code snippet creates a new sprite from the sprite sheet, adds that sprite as a child of the sheet, and positions it 100 points from the left side of the screen and 100 points up from the bottom. (We’ll get to what “points” are in the next section.)

Cocos2d manages the sprite sheets with a <strong>caching mechanism</strong> it calls the sprite frame cache. We loaded the frame cache in the previous code snippet when we loaded the <code>bridgesprites.pvr.gz</code> sprite sheet file and the <code>bridgesprites.plist</code> file that describes it. Cocos2d loaded all of those images into the cache, and we can now get them by name.

All positions in Cocos2d are based on a coordinate system in which point <code>0,0</code> is in the bottom-left corner. UIKit puts the point <code>0,0</code> at the top left of the screen. There are a few places where we need to convert back and forth further in the code.

Instead of using points directly, the game uses a tile system to position the sprites.</p>

### Pixels, Points and Tiles

iOS supports five devices:

*   iPhone 3.5 inch
*   iPhone 3.5 inch with Retina display
*   iPhone 4 inch with Retina display
*   iPad
*   iPad with Retina display

<img class="aligncenter size-full wp-image-122539" title="Different iOS device sizes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ca1f7d5-a3ac-4303-997f-a1bcc55a780a/device-sizes-500.png" alt="Different iOS device sizes" width="500" height="375" />

Supporting every device means handling multiple layouts. Cocos2d gives us a lot of help here by supporting points instead of pixels when specifying layout. Pixels represent an exact screen location, whereas points are relative to the device. This makes it easy to support Retina devices whose screens are the same size but pack in twice as many pixels.

Seven Bridges goes farther by defining a tile system. Tiles are a way of <strong>grouping pixels into larger squares</strong> for easier layout. We make the screen 28 tiles tall and at least 42 tiles wide. The tiles make it easy to define where the sprites go on each level. Switch the <code>DEBUG_DRAW</code> constant in <code><a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/BridgeColors.h">Bridgecolors.h</a></code> to <code>true</code> and you’ll be able to see the tile grid in the background of each level.

<img loading="lazy" decoding="async" class="133200" title="Two Bridges debug view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10320fe-f8e1-479b-8736-e1fbd365b30a/two-bridges-debug1-500.png" alt="Two Bridges debug view" width="500" height="371" />

### Touches and Interactions

UIKit handles touches on controls such as buttons and tables, but <strong>for the game scene we’ll need a generic touch handler</strong>. Cocos2d provides that with the <code>ccTouchesEnded</code> method. First, we have to tell Cocos2d that we want touch events, like this:

<pre><code class="language-javascript">self.isTouchEnabled = YES;</code></pre>

Then, we implement the <code>ccTouchesEnded</code> method to get called whenever the user taps the screen.

<pre><code class="language-javascript">-(void)ccTouchesEnded:(NSSet*) touches withEvent:(UIEvent*) event {
   UITouch *touch = [touches anyObject];
   CGPoint location = [touch locationInView:[touch view]];
   location = [[CCDirector sharedDirector] convertToGL:location];

   // Do some stuff with the point that the user touched…
}</code></pre>

<code><a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm">LevelLayer</a></code> handles each screen touch with some simple logic:

*   If the player isn’t on the screen yet, then place the player sprite where the user has touched and return.
*   If the player is on the screen, then move the player from the current location to the place where the user has touched.

That’s all we need to do for the touch. The real logic of the game happens when we handle the collisions.</p>

### Boxes and Collisions

Each object on the screen is a sprite: a little image file that sits at particular coordinates on the screen. Cocos2d can handle the position and animation of those images, but it won’t know if they run into each other. This is where Box2d shines.

The <a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LayerMgr.mm">LayerMgr</a> class adds and removes all of the images from the layers in the game. When it adds an image, it also creates a box around it. <strong>Boxes are the fundamental concept</strong> of Box2d. They outline the position of an object on the screen and detect when it interacts with other objects. Box2d supports complex box shapes, but all of the boxes in this game are rectangles.

Whenever we add an image to the scene, we draw a box around it with Box2d. The box works with a helper class called a <a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/MyContactListener.h">contact listener</a>. This listener sits in a timer and asks the Box2d model if any of the objects have run into each other after each frame of the game.

The contact listener implements two important functions: <code>BeginContact</code> and <code>EndContact</code>. These functions are called when two objects come into contact and when that contact stops. When that happens, we save the data so that we can use it in the layer that renders the level.

<pre><code class="language-javascript">void MyContactListener::BeginContact(b2Contact* contact) {
    MyContact myContact = { contact-&gt;GetFixtureA(), contact-&gt;GetFixtureB() };
    CCSprite *spriteA = (CCSprite *) contact-&gt;GetFixtureA()-&gt;GetBody()-&gt;GetUserData();
    CCSprite *spriteB = (CCSprite *) contact-&gt;GetFixtureB()-&gt;GetBody()-&gt;GetUserData();
    if (spriteA.tag == PLAYER || spriteB.tag == PLAYER) {
        _contacts.push_back(myContact);
    }
}

void MyContactListener::EndContact(b2Contact* contact) {
    MyContact myContact = { contact-&gt;GetFixtureA(), contact-&gt;GetFixtureB() };

    std::vector::iterator pos;
    pos = std::find(_contacts.begin(), _contacts.end(), myContact);
    if (pos != _contacts.end()) {
        _contacts.erase(pos);
    }
}</code></pre>

Once we’ve stored the data about the collisions, we use it every time we draw the level.

<pre><code class="language-javascript">CCSprite *spriteA = (CCSprite *) bodyA-&gt;GetUserData();
    CCSprite *spriteB = (CCSprite *) bodyB-&gt;GetUserData();

    if (spriteA.tag == RIVER &amp;&amp; spriteB.tag == PLAYER) {
        [self bumpObject:spriteB:spriteA];
    } else if (spriteA.tag == BRIDGE &amp;&amp; spriteB.tag == PLAYER) {
        [self crossBridge:spriteB:spriteA];</code></pre>

The contact listener gives us the <strong>two sprites that collided</strong>, and we’ll use the tag of each sprite to determine how to handle it. When two sprites run into each other, we react with some simple logic:

*   If the player contacts a river, then bounce back.
*   If the player contacts a bridge, then check whether the bridge has been crossed.
    *   If the bridge is crossed, then bounce back.
    *   If the bridge isn’t crossed, then cross it and move the player to the other side.

Separating the player’s movement from the collision makes it easy to move the player around the screen. We don’t have to define islands or worry about managing where the player is allowed to move. We just place each sprite in the level and wait for the player to run into it.</p>

## Defining Levels

Each level in the game is defined in a separate JSON document. Separating the level definitions from the code is important so that we can update the levels or add new ones without having to change the code.

Cocos2d manages the sprite sheets with a <strong>caching mechanism</strong> it calls the sprite frame cache. We loaded the frame cache in the previous code snippet when we loaded the <code>bridgesprites.pvr.gz</code> sprite sheet file and the <code>bridgesprites.plist</code> file that describes it. Cocos2d loaded all of those images into the cache, and we can now get them by name.

All positions in Cocos2d are based on a coordinate system in which point <code>0,0</code> is in the bottom-left corner. UIKit puts the point <code>0,0</code> at the top left of the screen. There are a few places where we need to convert back and forth further in the code.

Instead of using points directly, the game uses a tile system to position the sprites.</p>

### Pixels, Points and Tiles

iOS supports five devices:

*   iPhone 3.5 inch
*   iPhone 3.5 inch with Retina display
*   iPhone 4 inch with Retina display
*   iPad
*   iPad with Retina display

<img class="aligncenter size-full wp-image-122539" title="Different iOS device sizes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ca1f7d5-a3ac-4303-997f-a1bcc55a780a/device-sizes-500.png" alt="Different iOS device sizes" width="500" height="375" />

Supporting every device means handling multiple layouts. Cocos2d gives us a lot of help here by supporting points instead of pixels when specifying layout. Pixels represent an exact screen location, whereas points are relative to the device. This makes it easy to support Retina devices whose screens are the same size but pack in twice as many pixels.

Seven Bridges goes farther by defining a tile system. Tiles are a way of <strong>grouping pixels into larger squares</strong> for easier layout. We make the screen 28 tiles tall and at least 42 tiles wide. The tiles make it easy to define where the sprites go on each level. Switch the <code>DEBUG_DRAW</code> constant in <code><a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/BridgeColors.h">Bridgecolors.h</a></code> to <code>true</code> and you’ll be able to see the tile grid in the background of each level.

<img loading="lazy" decoding="async" class="133200" title="Two Bridges debug view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10320fe-f8e1-479b-8736-e1fbd365b30a/two-bridges-debug1-500.png" alt="Two Bridges debug view" width="500" height="371" />

### Touches and Interactions

UIKit handles touches on controls such as buttons and tables, but <strong>for the game scene we’ll need a generic touch handler</strong>. Cocos2d provides that with the <code>ccTouchesEnded</code> method. First, we have to tell Cocos2d that we want touch events, like this:

<pre><code class="language-javascript">self.isTouchEnabled = YES;</code></pre>

Then, we implement the <code>ccTouchesEnded</code> method to get called whenever the user taps the screen.

<pre><code class="language-javascript">-(void)ccTouchesEnded:(NSSet*) touches withEvent:(UIEvent*) event {
   UITouch *touch = [touches anyObject];
   CGPoint location = [touch locationInView:[touch view]];
   location = [[CCDirector sharedDirector] convertToGL:location];

   // Do some stuff with the point that the user touched…
}</code></pre>

<code><a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm">LevelLayer</a></code> handles each screen touch with some simple logic:

*   If the player isn’t on the screen yet, then place the player sprite where the user has touched and return.
*   If the player is on the screen, then move the player from the current location to the place where the user has touched.

That’s all we need to do for the touch. The real logic of the game happens when we handle the collisions.</p>

### Boxes and Collisions

Each object on the screen is a sprite: a little image file that sits at particular coordinates on the screen. Cocos2d can handle the position and animation of those images, but it won’t know if they run into each other. This is where Box2d shines.

The <a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LayerMgr.mm">LayerMgr</a> class adds and removes all of the images from the layers in the game. When it adds an image, it also creates a box around it. <strong>Boxes are the fundamental concept</strong> of Box2d. They outline the position of an object on the screen and detect when it interacts with other objects. Box2d supports complex box shapes, but all of the boxes in this game are rectangles.

Whenever we add an image to the scene, we draw a box around it with Box2d. The box works with a helper class called a <a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/MyContactListener.h">contact listener</a>. This listener sits in a timer and asks the Box2d model if any of the objects have run into each other after each frame of the game.

The contact listener implements two important functions: <code>BeginContact</code> and <code>EndContact</code>. These functions are called when two objects come into contact and when that contact stops. When that happens, we save the data so that we can use it in the layer that renders the level.

<pre><code class="language-javascript">void MyContactListener::BeginContact(b2Contact* contact) {
    MyContact myContact = { contact-&gt;GetFixtureA(), contact-&gt;GetFixtureB() };
    CCSprite *spriteA = (CCSprite *) contact-&gt;GetFixtureA()-&gt;GetBody()-&gt;GetUserData();
    CCSprite *spriteB = (CCSprite *) contact-&gt;GetFixtureB()-&gt;GetBody()-&gt;GetUserData();
    if (spriteA.tag == PLAYER || spriteB.tag == PLAYER) {
        _contacts.push_back(myContact);
    }
}

void MyContactListener::EndContact(b2Contact* contact) {
    MyContact myContact = { contact-&gt;GetFixtureA(), contact-&gt;GetFixtureB() };

    std::vector::iterator pos;
    pos = std::find(_contacts.begin(), _contacts.end(), myContact);
    if (pos != _contacts.end()) {
        _contacts.erase(pos);
    }
}</code></pre>

Once we’ve stored the data about the collisions, we use it every time we draw the level.

<pre><code class="language-javascript">CCSprite *spriteA = (CCSprite *) bodyA-&gt;GetUserData();
    CCSprite *spriteB = (CCSprite *) bodyB-&gt;GetUserData();

    if (spriteA.tag == RIVER &amp;&amp; spriteB.tag == PLAYER) {
        [self bumpObject:spriteB:spriteA];
    } else if (spriteA.tag == BRIDGE &amp;&amp; spriteB.tag == PLAYER) {
        [self crossBridge:spriteB:spriteA];</code></pre>

The contact listener gives us the <strong>two sprites that collided</strong>, and we’ll use the tag of each sprite to determine how to handle it. When two sprites run into each other, we react with some simple logic:

*   If the player contacts a river, then bounce back.
*   If the player contacts a bridge, then check whether the bridge has been crossed.
    *   If the bridge is crossed, then bounce back.
    *   If the bridge isn’t crossed, then cross it and move the player to the other side.

Separating the player’s movement from the collision makes it easy to move the player around the screen. We don’t have to define islands or worry about managing where the player is allowed to move. We just place each sprite in the level and wait for the player to run into it.</p>

## Defining Levels

Each level in the game is defined in a separate JSON document. Separating the level definitions from the code is important so that we can update the levels or add new ones without having to change the code.

Each level defines a name, an ID and a set of objects that go in the level.

<pre><code class="language-javascript">{
    "level": {
        "name": "Hello Bridges!",
        "rivers": [
            {
                "x": "14",
                "y": "b-t",
                "orient": "v"
            }
        ],
        "bridges": [
            {
                "x": "14",
                "y": "m",
                "orient": "h"
            }
        ]
    }
}</code></pre>

Each object has a coordinate in the tile system and a set of properties that define how the object works. For example, a bridge specifies an <code>orient</code> property to determine whether the bridge is horizontal or vertical and a <code>color</code> property to determine whether the bridge has a particular color. A separate <a href="https://github.com/zgrossbart/bridges/wiki/Level-Specification">page defines everything you can put in a level</a>.

Many games define levels in XML, but I chose JSON because it’s faster to parse and <strong>works better with the Web</strong>. One day, I’d like to create a mode in which you can load new levels from a website without having to download a new version of the game.

The <a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/Level.h">Level</a> class defines each level; levels are controlled by a <a href="https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelMgr.h">LevelMgr</a>. The level manager loads the levels, sorts them for the menu and creates the thumbnails of each level on the menu screen.

Seven Bridges does a lot more, but this is a good place to stop for the first article.</p>

## What’s Next

This article has walked us through some of the core parts of games for iOS, but there’s a lot more. You can <a href="https://zgrossbart.github.com/bridges/">get Seven Bridges</a> (not free) or <a href="https://github.com/zgrossbart/bridges">download the source code</a> and run it for free in the simulator.

We’ve reviewed the major frameworks, looked at the anatomy of a game, and learned the basics of user interactions. In the next article, <strong>we’ll delve deeper into the pieces</strong> and see how they all fit together.

{{< signature "al" >}}

