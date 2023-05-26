---
title: Creating Realistic iPhone Games With Cocos2D
slug: realistic-iphone-games-cocos2d
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d474f97-6701-4153-9072-32ce864b84bc/mobile-04.jpg
date: 2013-04-16T10:14:25.000Z
author: zack-grossbart
description: >-
  Animation makes games real. Movement adds excitement to a game and makes the
  characters more realistic. In this article, we’ll look at the Cocos2D library
  and how it supports programmatic animations in iPhone games.
categories:
  - Mobile
  - Games
  - iOS
  - iPhone
---
Animation makes games real. Movement adds excitement to a game and makes the characters more realistic. In this article, we’ll look at the Cocos2D library and how it supports programmatic animations in iPhone games.

This article is part of a series that teaches you **how to create iPhone games** based on the open-source game [Seven Bridges](https://zgrossbart.github.com/bridges/). Make sure to check out the first article in the series, “[Designing an Open-Source iPhone Game](https://www.smashingmagazine.com/2013/02/13/designing-open-source-iphone-game)” and look at the source code in the [Seven Bridges GitHub repository](https://github.com/zgrossbart/bridges).</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/10/design-your-own-mobile-game/#further-reading-on-smashingmag)

*   [How To Build A SpriteKit Game In Swift 3](https://www.smashingmagazine.com/2016/11/how-to-build-a-spritekit-game-in-swift-3-part-1/)
*   [Develop A One-Of-A-Kind CSS / JS-Based Game Portfolio](https://www.smashingmagazine.com/2012/05/develop-a-one-of-a-kind-cssjs-based-game-portfolio/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)

This article walks you through the basics of animation. We’ll look at actions in Cocos2D and see how to combine them to create complex and custom effects.

{{% feature-panel %}}

## Simple Actions

All of the basic building blocks in a Cocos2D game, such as images and layers, derive from `[CCNode](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_node.html)`. Nodes interact with actions, which extend `[CCAction](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_action.html)` to create movement on the screen.

**The basic Cocos2D actions can:**

*   hide and show,
*   flip and rotate,
*   fade and tint,
*   and a lot more.

We’ll start by looking at the simple action `[CCBlink](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_blink.html)`. Seven Bridges doesn’t use the blink action, but it’s one of the easiest actions to understand.

Before we can start to use any action, **we’ll need a node**. We’ll start with `[PlayerNode](https://github.com/zgrossbart/bridges/blob/master/bridges2/PlayerNode.mm)` from Seven Bridges.

The player node is a simple one. It shows the player sprite, ![The player icon](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93afe403-5c6c-4691-82e8-1c2453f4dee7/player.png), and it handles the movement and animation of the player around the screen. `PlayerNode` isn’t actually a `CCNode`, but it contains a `[CCSprite](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_sprite.html)`, which represents a single image and extends `CCNode`. Separating the player object from the actual player image makes the player object a little more flexible.

Our player node needs a color and a `[LayerManager](https://github.com/zgrossbart/bridges/blob/master/bridges2/LayerMgr.mm)`. `LayerManager` is a helper object in Seven Bridges that lets game nodes interact with the world around them. You don’t need to code your objects with a `LayerManager`, but it gives you a simple place to add some standard code.

**Let’s create a new player** and place the player on the screen.</p>

<pre><code class="language-javascript">
PlayerNode* player = [[PlayerNode alloc] initWithColor:cBlack layerMgr:_layerMgr];
player.player.position = ccp(100, 100);
</code></pre>

`PlayerNode` contains the sprite pointer and uses the `LayerManager` to add the sprite to the scene. It makes the sprite available as a property named `player`, which has a property named `position`. The full code for creating `LayerManager` is in `[LevelLayer](https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm)`.

The blink action can run directly on the player sprite, because sprites are also `CCNode` objects that implement the `[runAction](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_node.html#a5d6d868cc1a0ba72820a055b05661aa5)` method. It works like this:

<pre><code class="language-javascript">
CCBlink* blink = [CCBlink actionWithDuration:10 blinks:5];
[player.player runAction:blink];
</code></pre>

Most actions define a static `actionWithDuration` method, which creates a new action object. `CCBlink` takes a duration and the number of times it should blink. We can apply whatever actions we’d like to the node just by passing them to the `runAction` method.</p>

## Running Multiple Actions

The latest version of Seven Bridges introduces teleporters, ![Teleporter icon](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c6cdbd-508f-4db0-b95d-04daa21a2330/teleport.png). **When players run into teleporters, they should look like they’re jumping in.** To create that effect, we’ll combine three actions: rotate, fade and scale. Each of these actions takes a little time to run, but we can make them all run simultaneously. Put them together and we’ll see players spinning and disappearing as they shrink (again, see [LevelLayer.mm](https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm)).</p>

<pre><code class="language-javascript">
[player.player runAction:[CCRotateBy actionWithDuration:0.5 angle:360]];
[player.player runAction:[CCFadeTo actionWithDuration:0.5 opacity:0.0]];
[player.player runAction:[CCScaleTo actionWithDuration:0.5 scale:0.25]];
</code></pre>

`CCRotateBy` rotates the player from the current position by a specified number of degrees. In this case, we want a full circle, so we rotate by 360 degrees.

`CCFadeTo` changes the player’s opacity to the specified value. We want players to disappear completely, so we fade to `0.0`.

`CCScaleTo` grows or shrinks the player according to the specified scaling factor. **We want players to shrink as they enter the teleporter**, so we scale them down to one quarter of the default size.

These actions take a duration, just like `CCBlink`. By specifying the duration as the same for each action, we cause all three of them to run at the same time. Playing them all together looks like this:

{{< vimeo id="60320015" caption="<a href='https://vimeo.com/60320015'>Seven Bridges - Teleport jump</a> from <a href='https://vimeo.com/user1004495'>Zack Grossbart</a> on <a href='https://vimeo.com'>Vimeo</a>." >}}

## Combining Actions In Sequences

Rotating and fading is cool, but let’s take it up a notch by actually changing the dimensions of the sprite, instead of just the size. The “Houses and Colors” map introduces houses, ![House icon](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b5192d4-58a6-4ece-9e1b-2550efc43f95/house.png), that you have to visit. When you visit a house, we turn it gray with a little flourish.

Houses are rendered by an object similar to `PlayerNode`, named `[HouseNode](https://github.com/zgrossbart/bridges/blob/master/bridges2/HouseNode.mm)`. Each is a helper object that contains a sprite and that handles the interactions. `PlayerNode` exposes the player sprite in a property named `player`, and `HouseNode` exposes the house sprite in a property named `house`.

The house-visiting animation flips the house horizontally while turning it gray. **To flip the house back and forth**, we run two actions sequentially. The first action flips the house to the right and leaves it backwards. The second action flips it back to the left.

The spinning, shrinking, fading player used three animations that ran at the same time. The house needs more control. To space them out, we’ll use a new object named `[CCSequence](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_sequence.html)`. Sequences string together actions that run one after another.

We’ll start by creating our two actions ([HouseNode.mm)](https://github.com/zgrossbart/bridges/blob/master/bridges2/HouseNode.mm):

<pre><code class="language-javascript">
float scale = 1.0;
CCEaseExponentialIn* flipHalf = [CCEaseExponentialIn
    actionWithAction:[CCActionTween actionWithDuration:0.25 key:@"scaleX" from:-scale to:0.0]];

CCEaseExponentialOut* flipRemainingHalf = [CCEaseExponentialOut
    actionWithAction:[CCActionTween actionWithDuration:0.25 key:@"scaleX" from:0.0 to:scale]];
</code></pre>

Cocos2D provides a series of special actions that make [easing and tweening](https://en.wikipedia.org/wiki/Inbetweening) possible. They all derive from `[CCEase](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_action_ease.html)`. These actions provide simple access to some of the basic movement animations that make objects bounce and slide into each other with a more natural movement. These same techniques are used on the Web for [JavaScript animations](https://www.smashingmagazine.com/2011/10/04/quick-look-math-animations-javascript/).

`CCEaseExponentialIn` and `CCEaseExponentialOut` provide natural movement in and out of various positions using an exponential curve. This animation combines that with `[CCTween](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_action_tween.html)`, which can apply changes to any property of a node. We change the `scaleX` property to start the rotation.

**Confused yet?**

There’s a lot of math here, but the basic concepts are pretty simple. The first animation causes the house to get smaller horizontally along the x axis. This squishes the house together until it disappears. The second animation pulls the house apart from zero to the full width. When you put them together, the house looks like it’s rotating.

Let’s create our house and run the animations together with a sequence like this ([HouseNode.mm](https://github.com/zgrossbart/bridges/blob/master/bridges2/HouseNode.mm)):

<pre><code class="language-javascript">
HouseNode *houseNode = [[HouseNode alloc] initWithColorAndCoins:cBlack layerMgr:layerMgr coins:0];

CCSequence* seq = [CCSequence actions:flipHalf, flipRemainingHalf, nil];
[house runAction:seq];
</code></pre>

`CCSequence` takes a series of actions and runs them one after another. The last argument is an Objective-C construct called a selector; it defines a method to call when the actions are complete. It is optional, and we don’t need any notification, so we just pass it `nil`.

## Combining Actions With Custom Code

This sequence will flip the house, but we also want to turn it gray: ![Gray house icon](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce244801-f1fc-4544-8ab0-715cd2a643bc/house-gray.png). Cocos2D provides special actions for tinting, but **we want a high-quality image for the gray house**, so we’ll use a PNG file. None of the default actions replace a sprite’s image, so we need a little custom code. Cocos2D provides the ultimate flexibility with the `[CCCallFunc](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_call_func.html)` action, which sits inside a sequence and calls any code you want.

The house turns gray when the visit ends, so we’ll create a new function named `visitEnded` and define it on `HouseNode`, like so ([HouseNode.mm](https://github.com/zgrossbart/bridges/blob/master/bridges2/HouseNode.mm)):

<pre><code class="language-javascript">
-(void)visitEnded {
    CCSpriteFrameCache* cache = [CCSpriteFrameCache sharedSpriteFrameCache];
    CCSpriteFrame* frame;
    frame = [cache spriteFrameByName:@"house_gray.png"];
    [self.house setDisplayFrame:frame];
}
</code></pre>

We already have a gray house icon, so the `visitEnded` function gets that icon from the sprite cache and sets it into our `house` sprite. Now we just need to tweak our sequence to call `visitEnded` in the middle of the animation. This code is getting a little complicated, so we’ll add it to a new method on `HouseNode` and call it `visit`.</p>

<pre><code class="language-javascript">
-(void) visit {
    float scale = 1.0;
    CCEaseExponentialIn* flipHalf = [CCEaseExponentialIn
        actionWithAction:[CCActionTween actionWithDuration:0.25 key:@"scaleX" from:-scale to:0.0]];

    CCEaseExponentialOut* flipRemainingHalf = [CCEaseExponentialOut
        actionWithAction:[CCActionTween actionWithDuration:0.25 key:@"scaleX" from:0.0 to:scale]];

    CCSequence* seq = [CCSequence actions:flipHalf,
                      [CCCallFunc actionWithTarget:self selector:@selector(visitEnded)],
                      flipRemainingHalf, nil];

    [self.house runAction:seq];
}
</code></pre>

**This new sequence will squish the house down**, call the `visitEnded` method with `CCCallFunc` to turn the house gray, and stretch the house back out.</p>

{{< vimeo id="60319771" caption="<a href='https://vimeo.com/60319771'>Seven Bridges - House Visit</a> from <a href='https://vimeo.com/user1004495'>Zack Grossbart</a> on <a href='https://vimeo.com'>Vimeo</a>." >}}

Cocos2D provides a series of actions for calling custom code, such as `[CCCallFuncN](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_call_func_n.html)` and `[CCCallBlock](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_call_block.html)`. Each is a variation of calling custom code during sequences. Combining out-of-the-box animations with custom code creates an ideal environment for complex animations.</p>

## Combining Multiple Animations Into Particle Systems

We’ve looked at simple animations and looked at some more complex interactions. Now let’s get fancy with particles. Cocos2D provides a set of more complex animations, which all start with `[CCParticleSystem](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_particle_system.html)`.

Particle systems aren’t actions. They use actions to create flexible canned animations. They’re awesome, complex and poorly documented. **Particle systems work well for mimicking natural phenomena** such as rain and smoke.

When you beat a level of Seven Bridges, we give you a little reward: star-shaped confetti that spins and floats across the screen. We add whimsy to those stars with some randomness, and pull everything together with a particle system named `[CCParticleRain](https://www.cocos2d-iphone.org/api-ref/2.1.0/interface_c_c_particle_rain.html)`.</p>

{{< vimeo id="60320148" caption="<a href='https://vimeo.com/60320148'>Seven Bridges - Stars</a> from <a href='https://vimeo.com/user1004495'>Zack Grossbart</a> on <a href='https://vimeo.com'>Vimeo</a>." >}}

So… um… there’s no way to ease into this one — here’s a really big chunk of code ([LevelLayer.mm](https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm)):

<pre><code class="language-javascript">
-(void) showConfetti: (float) x y:(float) y {
    self.emitter = [[CCParticleRain alloc] init];
    [self.emitter setScaleX:0.5];
    [self.emitter setScaleY:0.5];

    [self.emitter resetSystem];
    self.emitter.texture = [[CCTextureCache sharedTextureCache] addImage:@"confetti.png"];

    self.emitter.duration = 1.5;

    // Set the gravity effect for the stars to control how
    // fast they fall down.
    self.emitter.gravity = ccp(self.player.player.position.x, 90);

    // Specify the angle of the stars as they extend from the
    // starting point.
    self.emitter.angle = 90;
    self.emitter.angleVar = 360;

    // The speed the particles will use when floating
    self.emitter.speed = 160;
    self.emitter.speedVar = 20;

    // The radial variable
    self.emitter.radialAccel = -120;
    self.emitter.radialAccelVar = 120;

    // The tangential variable
    self.emitter.tangentialAccel = 30;
    self.emitter.tangentialAccelVar = 60;

    // How long each star should last before fading out
    self.emitter.life = 1;
    self.emitter.lifeVar = 4;

    // How much each star should spin
    self.emitter.startSpin = 15;
    self.emitter.startSpinVar = 5;
    self.emitter.endSpin = 360;
    self.emitter.endSpinVar = 180;

    // The color of the stars as RGB values.  Each color uses
    // a variable value for where the stars should start and
    // what color they should use when they're done.
    ccColor4F startColor = {171.0f, 26.0f, 37.0f, 1.0f};
    self.emitter.startColor = startColor;
    ccColor4F startColorVar = {245.0f, 255.f, 72.0f, 1.0f};
    self.emitter.startColorVar = startColorVar;
    ccColor4F endColor = {255.0f, 223.0f, 85.0f, 1.0f};
    self.emitter.endColor = endColor;
    ccColor4F endColorVar = {255.0f, 131.0f, 62.0f, 1.0f};
    self.emitter.endColorVar = endColorVar;

    // The size of each of the stars
    self.emitter.startSize = 50.0f;
    self.emitter.startSizeVar = 20.0f;
    self.emitter.endSize = kParticleStartSizeEqualToEndSize;

    // The rate at which new stars will be created
    self.emitter.totalParticles = 250;
    self.emitter.emissionRate = self.emitter.totalParticles/self.emitter.life;

    // The position to start the stars
    self.emitter.posVar = ccp(x + 20, y - 20);
    self.emitter.position = ccp(x,y);

    // We have a simple white background, so we don't want to
    // do additive blending.
    self.emitter.blendAdditive = NO;

    // Now we're ready to run the particle emitter
    [self addChild: self.emitter z:10];
    self.emitter.autoRemoveOnFinish = YES;

    // We call the doWon function when the particle system completes
    // so that we can take the player to the You Won screen.
    [self scheduleOnce:@selector(doWon) delay:3];
}
</code></pre>

This code comes from `[LevelLayer](https://github.com/zgrossbart/bridges/blob/master/bridges2/LevelLayer.mm)`, which controls the player’s interactions with the play screen. When the player wins the level, we call the `showConfetti` method and pass in the player’s current location.

The particle system starts with a single image, ![Star confetti icon](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643b02fc-cc6d-4de1-ab68-4238bd7b23f8/confetti.png), creates hundreds of instances of that image, and moves those instances across the screen while changing their size, color, rotation and speed.

Most of this code just sets up `CCParticleRain` and tells it how to behave. **Particle systems are very flexible** and support a dizzying array of configuration properties. These properties aren’t well documented; I found most of them by looking in Cocos2D’s source code.

Particle systems achieve a natural look by having random variability added to them. You control the range of the randomness with `var` properties. For example, we want the stars to start out between 20 and 50 times their regular size, so we specify a `startSize` property of `50.0f` and a `startSizeVar` property of `20.0f`. This means that each of the stars will start somewhere between these two values.</p>

## Create Your Own Animations

Now that you’ve seen some of the basic concepts in Cocos2D animations, you can create your own. An easy place to start is by changing Seven Bridges. Just [download the source code](https://github.com/zgrossbart/bridges) and start tweaking it.

Add a blinking animation to make the player character blink while moving. Take a look at `[PlayerNode](https://github.com/zgrossbart/bridges/blob/master/bridges2/PlayerNode.mm)` to see the sequence for moving the player across the screen. Play with the particle emitter to change the way the stars work.

In this article, we’ve reviewed programmatic animations in games, but **Cocos2D also supports sprite-based animations**. These animations play a series of images to create the illusion of movement, somewhat like a [flip book](https://en.wikipedia.org/wiki/Flip_book). Seven Bridges uses that style of animation when moving the player around the screen.

![Player movement animation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d43e5bdd-6004-4b29-8ebd-a16d1f20609b/player-movement.png)

Ray Wenderlich has an awesome tutorial on sprite-based animation, titled “[How to Use Animations and Sprite Sheets in Cocos2D](https://www.raywenderlich.com/1271/how-to-use-animations-and-sprite-sheets-in-cocos2d).” The article is excellent, but it mentions a product called Zwoptex, and I strongly recommend [TexturePacker](https://www.codeandweb.com/texturepacker) instead.

{{< signature "al" >}}

