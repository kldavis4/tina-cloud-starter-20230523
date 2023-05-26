---
title: 'Principles Of HTML5 Game Design'
slug: principles-of-html5-game-design
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/593f93d6-9729-42c0-90c4-3e53240bb783/12-procedural-curved-line-opt-small.png
date: 2015-09-04T05:07:34.000Z
author: stolarskigrajewski
summary: >-
  Do you want to implement different visual effects in `<canvas>`-based HTML5 games but you’re not sure how to start? In this article, we’ll look at patterns that are commonly used to make games and game effects and also explore the theory and some code examples supporting these patterns.
description: >-
  Do you want to implement different visual effects in `<canvas>`-based HTML5 games but you’re not sure how and where to start? In this article, let’s look at patterns that are commonly used to make games and game effects.
categories:
  - Coding
  - Games
  - HTML5
---
Visual effects in games define their overall look and feel, and gameplay. Players are attracted to high visual quality, which generate more traffic and reach. It’s key for creating successful games and providing a lot of fun for players.

In this article, we'd like to present a few **ideas of how to implement different visual effects** in `<canvas>`-based HTML5 games. These examples will be based on effects we made in our game, [Skytte](https://www.merixstudio.com/skytte/). We will explain the basic ideas supporting them and provide the effects used in our work.</p>

## What You Will Learn

Before we get going, let's set out the things we hope you'll learn from this article:

*   **Basic game design**
    We'll look at patterns that are commonly used to make games and game effects like: game loops, sprites, collisions, and particle systems.
*   **Basic implementation of visual effects**
    We will also explore the theory and some code examples supporting these patterns.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Rebuilding An HTML5 Game In Unity](https://www.smashingmagazine.com/2014/04/rebuilding-an-html5-game-in-unity/)
*   [What Web Designers Can Learn From Video Games](https://www.smashingmagazine.com/2011/07/what-web-designers-can-learn-from-video-games/)
*   [Email Marketing For Mobile App Creators](https://www.smashingmagazine.com/2013/08/email-marketing-for-mobile-app-creators/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)

{{% feature-panel %}}

## Common Patterns

Let's start with some common patterns and elements used in game development.</p>

### Sprites

These are simply 2-D images that represent an object in the game. Sprites can be used for static objects, but also animated objects, when each sprite represents a frame of sequential animation. They can also be used for making user interface elements.

Usually games contain between dozens and hundreds of sprites. To reduce memory usage and the processing power needed to handle these images, many games use **sprite sheets**.</p>

### Sprite Sheets

These are used to group a set of single sprites in one image. This reduces the amount of files in the game, resulting in reduced memory and processing power usage. Sprite sheets contain many single sprites stacked next to each other in rows and columns, and like the sprites they contain can be used statically or for animation.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5090407-6237-4818-9638-6ff95e7a4625/01-sprite-example-opt.gif" alt="Spritesheet example" /><figcaption>Sprite sheet example. (Image credit: <a href="https://commons.wikimedia.org/wiki/File:Sprite-example.gif#/media/File:Sprite-example.gif">Kriplozoik</a>)</figcaption></figure>

Here’s [an article from Code + Web](https://www.codeandweb.com/what-is-a-sprite-sheet/) to help you better understand the benefits of using sprite sheets.</p>

### Game Loops

It's important to realize that game objects don't really move on screen. An illusion of movement is achieved by rendering a snapshot of a game world to the screen, advancing the game time a small amount (usually 1/60th of a second), and then rendering things again. This is literally a stop-motion effect and is used in both 2-D and 3-D games. A game loop is a **mechanism that implements this stop-motion**. It’s the main component needed to run a game. It runs continuously over time, performing various tasks. On each iteration it processes user input, moves entities, checks for collisions, and renders the game (preferably in this order). It also controls game time that’s elapsed between frames.

Below is a very basic game loop in JavaScript:

<div class="break-out">

<pre><code class="language-javascript">var lastUpdate;

function tick() {
  var now = window.Date.now();

  if (lastUpdate) {
    var elapsed = (now-lastUpdate) / 1000;
    lastUpdate = now;

    // Update all game objects here.
    update(elapsed);
    // ...and render them somehow.
    render();
  } else {
    // Skip first frame, so elapsed is not 0.
    lastUpdate = now;
  }

  // This makes the `tick` function run 60 frames per second (or slower, depends on monitor's refresh rate).
  window.requestAnimationFrame(tick);
};
</code></pre></div>

Note that the above example is very simplistic. It uses variable delta time (the `elapsed` variable) and it's recommended to upgrade this code to use fixed delta time. See [this article for more details](https://gafferongames.com/game-physics/fix-your-timestep/).</p>

### Collision Detection

Collision detection refers to finding the intersections between objects. This is essential for many games because it’s used to detect if a player hits a wall or a bullet hits an enemy, and so on. When a collision is detected it can be used for game logic; for example, when a bullet hits the player, the health score is reduced by 10 points.

There are a lot of collision detection algorithms, and because it’s a performance-heavy operation, it’s important to choose the best method wisely. To read more about collision detection, algorithms and how they can be implemented, here’s [an article from MDN](https://developer.mozilla.org/en-US/docs/Games/Techniques/2D_collision_detection).</p>

### Particles And Particle Systems

Particles are basically sprites used by a particle system. In game development, a particle system is a component that consists of a particle emitter and particles assigned to that emitter. It’s used to simulate various effects, like fire, explosions, smoke, and rain effects. Particles are emitted over time and each emitter has its own parameters to define various variables used for the simulated effect, such as velocity, color, a particle's lifetime or duration, gravity, friction, and wind speed.</p>

### Euler Integration

Euler integration is a method for numerically integrating the equations of motion. Each object's position is calculated based on its velocity, mass and force, and needs to be recalculated for each tick in the game loop. The Euler method is the most basic and useful for games like side-scrolling shooters, but there are also other methods like Verlet integration and RK4 integration which are better for other tasks. Below I’ll show a simple implementation of the idea.

You need a basic structure to hold an object's position, velocity and other movement-related data. We propose two identical structures, but each with different meaning in the world's space: point and vector. Usually game engines use some kind of vector class, but the distinction between points and vectors is very important and greatly improves code readability (for example, you calculate distance not between two vectors, but two points, which is more natural).

#### Point

Simply, it represents an element in two-dimmensional space with _x_ and _y_ coordinates which define where the point is located in that space.</p>

<pre><code class="language-javascript">function point2(x, y) {
  return {'x': x || 0, 'y': y || 0};
}</code></pre>

#### Vector

A vector is a geometric object that has length (or magnitude) and direction. In 2-D games vectors are used mostly to describe forces (e.g. gravity, air resistance and wind) and velocities, as well as proscribing movements or how light reflects off an object. Vectors have many uses.</p>

<pre><code class="language-javascript">function vector2(x, y) {
  return {'x': x || 0, 'y': y || 0};
}</code></pre>

The above functions create new two-dimensional vectors and points. Internally we don't use the `new` operator in this case in JavaScript to gain a lot of performance. Also note that there are some third-party libraries available that you could use to manipulate vectors ([glMatrix](https://github.com/toji/gl-matrix/tree/master/src/gl-matrix) is a good candidate for this).

What follows are some very common functions used on the two-dimensional structures defined above. First, calculating the distance between two points:

<div class="break-out">

<pre><code class="language-javascript">point2.distance = function(a, b) {
  // The x and y variables hold a vector pointing from point b to point a.
  var x = a.x - b.x;
  var y = a.y - b.y;
  // Now, distance between the points is just length (magnitude) of this vector, calculated like this:
  return Math.sqrt(x*x + y*y);
};
</code></pre></div>

The magnitude (length) of a vector can be calculated directly from the last line of the above function like this:

<pre><code class="language-javascript">vector2.length = function(vector) {
  return Math.sqrt(vector.x*vector.x + vector.y*vector.y);
};
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21e127e6-adc3-450b-9f20-ca99ae518110/02-vector-length-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bdde184-1ffc-45a2-9b67-dc0d5d51b64d/02-vector-length-opt-small.png" alt="Vector length" /></a><figcaption>Vector length. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21e127e6-adc3-450b-9f20-ca99ae518110/02-vector-length-opt.png">View large version</a>)</figcaption></figure>

Normalization of vectors is also very handy. The function below resizes a vector so it becomes a unit vector; that is, its length is 1, but its direction is maintained.</p>

<div class="break-out">

<pre><code class="language-javascript">
vector2.normalize = function(vector) {
  var length = vector2.length(vector);

  if (length &gt; 0) {
    return vector2(vector.x / length, vector.y / length);
  } else {
    // zero-length vectors cannot be normalized, as they do not have direction.
    return vector2();
  }
};
</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11431d9d-7cdf-4ec1-8912-3900fbe1b814/03-vector-normalization-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b2e0f02-36ab-4f0c-9da6-4bcb2686eec7/03-vector-normalization-opt-small.png" alt="Vector normalization" /></a><figcaption>Vector normalization. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11431d9d-7cdf-4ec1-8912-3900fbe1b814/03-vector-normalization-opt.png">View large version</a>)</figcaption></figure>

Another useful case is to have a unit vector whose direction is pointing from one location to another:

<div class="break-out">

<pre><code class="language-javascript">// Note that this function is different from `vector2.direction`.
// Please don't confuse them.
point2.direction = function(from, to) {
  var x = to.x - from.x;
  var y = to.y - from.y;
  var length = Math.sqrt(x*x + y*y);

  if (length &gt; 0) {
    return vector2(x / length, y / length);
  } else {
    // `from` and `to` are identical
    return vector2();
  }
};
</code></pre></div>

The _dot product_ is an operation on two vectors (usually unit vectors), which returns a scalar number representing the relation between angles of those vectors.</p>

<pre><code class="language-javascript">vector2.dot = function(a, b) {
  return a.x*b.x + a.y*b.y;
};
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a977aa03-326a-4402-b890-14de0020d1ed/04-vector-dot-product-opt.png" alt="Vector dot product" /><figcaption>Vector dot product.</figcaption></figure>

The dot product is a length of a vector _a_ projected on a vector _b_. A returned value of 1 means that both vectors point in the same direction. A value of -1 means that vector _a_ points in the opposite direction of vector _b_. A value of 0 means that vector _a_ is perpendicular to vector _b_.

Here's an example of an entity class, so other objects can inherit from it. Only basic properties related to movement are described.</p>

<div class="break-out">

<pre><code class="language-javascript">function Entity() {
  ...
  // Center of mass usually.
  this.position = point2();
  // Linear velocity.
  // There is also something like angular velocity, not described here.
  this.velocity = vector2();
  // Acceleration could also be named `force`, like in the Box2D engine.
  this.acceleration = vector2();
  this.mass = 1;
  ...
}
</code></pre></div>

You can use pixels or meters as the unit in your game. We encourage you to use meters, as it's easier to balance things out during development. Velocity, then, should be meters per second, and acceleration should be meters per second squared.

{{% ad-panel-leaderboard %}}

When using a third-party physics engine, you just store a reference to a physical body (or set of bodies) in your entity class. Then, the physics engine stores the mentioned properties, like position and velocity, inside each body for you.

Basic Euler integration looks like this:

<pre><code class="language-javascript">acceleration = force / mass
velocity += acceleration
position += velocity
</code></pre>

The code above must be executed in each frame for each object in the game. Here is a basic implementation of the above in JavaScript:

<div class="break-out">

<pre><code class="language-javascript">Entity.prototype.update = function(elapsed) {
  // Acceleration is usually 0 and is set from the outside.
  // Velocity is an amount of movement (meters or pixels) per second.
  this.velocity.x += this.acceleration.x * elapsed;
  this.velocity.y += this.acceleration.y * elapsed;

  this.position.x += this.velocity.x * elapsed;
  this.position.y += this.velocity.y * elapsed;

  ...

  this.acceleration.x = this.acceleration.y = 0;
}
</code></pre></div>

`elapsed` is the amount of time in seconds that has passed since the last frame (since the last call to this method). For games running at 60 frames per second, the `elapsed` value is usually 1/60 of a second, which is 0.016(6)s.

The article on delta time mentioned earlier also covers [this problem](https://gafferongames.com/game-physics/fix-your-timestep/).

To move objects, you can change their acceleration or velocity. Two functions shown below should be used for this purpose:

<pre><code class="language-javascript">Entity.prototype.applyForce = function(force, scale) {
  if (typeof scale === 'undefined') {
    scale = 1;
  }
  this.acceleration.x += force.x * scale / this.mass;
  this.acceleration.y += force.y * scale / this.mass;
};

Entity.prototype.applyImpulse = function(impulse, scale) {
  if (typeof scale === 'undefined') {
    scale = 1;
  }
  this.velocity.x += impulse.x * scale / this.mass;
  this.velocity.y += impulse.y * scale / this.mass;
};
</code></pre>

To move an object to the right you could do this:

<div class="break-out">

<pre><code class="language-javascript">// 10 meters per second in the right direction (x=10, y=0).
var right = vector2(10, 0);

if (keys.left.isDown)
  // The -1 inverts a vector, i.e. the vector will point in the opposite direction,
  // but maintain magnitude (length).
  spaceShip.applyImpulse(right, -1);
if (keys.right.isDown)
  spaceShip.applyImpulse(right, 1);
</code></pre></div>

**Note that objects set in motion stay in motion.** You need to implement some kind of deceleration to stop a moving object (air drag or friction, maybe).</p>

## Weapon Effects

Now I'll explain how certain weapon effects are made in our HTML5 game, [Skytte](https://www.merixstudio.com/skytte).</p>

### Plasma

{{< vimeo id="135389044" >}}

This is the most basic weapon in our game, just one shot each time. There are no special algorithms used for this weapon. When a plasma bullet is fired the game simply draws a single sprite that’s rotated over time.

A simple plasma bullet can be spawned like this:

<pre><code class="language-javascript">// PlasmaProjectile inherits from Entity class
var plasma = new PlasmaProjectile();

// Move right (assuming that X axis is pointing right).
var direction = vector2(1, 0);

// 20 meters per second.
plasma.applyImpulse(direction, 20);
</code></pre>

### Blaster

{{< vimeo id="135389040" >}}

This weapon is a little more complex. It also draws simple sprites as bullets but there’s some code that spreads them out a little and applies a random speed. This gives a more devastating feeling to this weapon, so players feel they can inflict more damage than with the plasma weapon and have better crowd control when among enemies.<p>

<p>The code works similarly to the plasma weapon code, but it spawns three bullets and each has a slightly different direction.</p>

<div class="break-out">

<pre><code class="language-javascript">// BlaserProjectile inherits from Entity class
var topBullet = new BlasterProjectile();  // This bullet will move slightly up.
var middleBullet = new BlasterProjectile();  // This bullet will move horizontally.
var bottomBullet = new BlasterProjectile();  // This bullet will move slightly down.
var direction;

// Angle 0 is pointing directly to the right.
// We start with the bullet moving slightly upwards.
direction = vector2.direction(radians(-5));  // Convert angle to an unit vector
topBullet.applyImpulse(direction, 30);

direction = vector2.direction(radians(0));
middleBullet.applyImpulse(direction, 30);

direction = vector2.direction(radians(5));
middleBullet.applyImpulse(direction, 30);
</code></pre></div>

<p>Some math functions are needed for the above code to work:</p>

<div class="break-out">

<pre><code class="language-javascript">function radians(angle) {
  return angle * Math.PI / 180;
}

// Note that this function is different from `point2.direction`.
// Please don't confuse them.
vector2.direction = function(angle) {
  /*
   * Converts an angle in radians to a unit vector. Angle of 0 gives vector x=1, y=0.
   */
  var x = Math.cos(angle);
  var y = Math.sin(angle);
  return vector2(x, y);
};
</code></pre></div>

### Ray

{{< vimeo id="135389042" >}}

This one's interesting. The weapon shoots a laser ray but it’s procedurally generated in each frame (this will be explained later). To detect hits, it creates a rectangular collider that deals damage every second for as long as it collides with the enemy.</p>

### Rockets

{{< vimeo id="135389043" >}}

This weapon shoots guided missiles. The rocket is a sprite with a particle emitter attached to its end. There’s also some more sophisticated logic, like searching for the nearest enemy or limiting the turn value for a rocket to give it less maneuverability. Also, rockets don’t start to seek for enemy targets immediately – they fly straight for a time to avoid unrealistic behavior.</p>

<p>Rockets in Skytte move toward their nearest neighbor. This is achieved by calculating the proper force needed for the projectile to move in any given direction. To avoid moving only in straight lines the force calculated shouldn't be too big.</p>

<p>Assuming that <code>Rocket</code> is a class inheriting from the <code>Entity</code> class described earlier.</p>

<div class="break-out">

<pre><code class="language-javascript">Rocket.prototype.update = function(elapsed) {
  var direction;

  if (this.target) {
    // Assuming that `this.target` points to the nearest enemy ship.
    direction = point2.direction(this.position, this.target.position);
  } else {
    // No target, so fly ahead.
    // This will fail for objects that are still, so remember to apply some initial velocity when spawning rockets.
    direction = vector2.normalize(this.velocity);
  }

  // You can use any number here, depends on the speed of the rocket, target and units used.
  this.applyForce(direction, 10);

  // Simple inheritance here, calling parent's `update()`, so rocket actually moves.
  Entity.prototype.update.apply(this, arguments);
};
</code></pre></div>

### Flak

{{< vimeo id="135389047" >}}

Flak was designed to shoot many small bullets (something like a shotgun), which are little dot sprites. It has some specific logic to randomly generate the position of these dots within a cone-shaped area.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371b89d9-e266-4fc3-8231-2651ade58f13/10-flak-weapon-bullet-opt.jpg" alt="Flak weapon bullets cone area" /><figcaption>Flak weapon bullets cone area.</figcaption></figure>

To generate random points in a cone-shaped area:</p>

<div class="break-out">

<pre><code class="language-javascript">// Firstly get random angle in degrees in the allowed span. Note that the span below always points to the right.
var angle = radians(random.uniform(-40, 40));

// Now get how far from the barrel the projectile should spawn.
var distance = random.uniform(5, 150);

// Join angle and distance to create an offset from the gun's barrel.
var direction = vector2.direction(angle);
var offset = vector2(direction.x * distance, direction.y * distance);

// Now calculate absolute position in the game world (you need a position of the barrel for this purpose):
var position = point2.move(barrel, offset);
</code></pre></div>

<p>The <code>random.uniform()</code> function returns a random floating point number between two values. A simple implementation could look like this:</p>

<pre><code class="language-javascript">random.uniform = function(min, max) {
  return min + (max-min) * Math.random();
};
</code></pre>

### Electro

{{< vimeo id="135389046" >}}

Electro is fancy weapon that shoots lightning at enemies within a particular radius. It has a limited range but can shoot at several enemies at once and always hits successfully. It uses the same algorithm to draw curved lines to simulate lightning as the ray weapon but with a higher curve factor.</p>

## Techniques Used

### Procedural Curved Line

<p>To create the laser beam effect and electro weapon we've developed an algorithm to count and transform the linear distance between the player's ship and the enemy. In other words, we measured the distance between two objects, found the middle point and moved it randomly alongside the section. We repeat this action for every new section created.</p>

<p>To draw these sections we use HTML5 <code>&lt;canvas&gt;</code> draw function <code>lineTo()</code>. To achieve the glowing color we used multiple lines drawn over one another with more opaque color and a higher stroke width.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/108563b0-2848-462d-a187-2bbe51746a96/12-procedural-curved-line-opt.png"><img property="image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/593f93d6-9729-42c0-90c4-3e53240bb783/12-procedural-curved-line-opt-small.png" alt="Procedural curved line" /></a><figcaption>Procedural curved line. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/108563b0-2848-462d-a187-2bbe51746a96/12-procedural-curved-line-opt.png">View large version</a>)</figcaption></figure>

To find and offset a point between two other points:</p>

<div class="break-out">

<pre><code class="language-javascript">var offset, midpoint;

midpoint = point2.midpoint(A, B);

// Calculate an unit-length vector pointing from A to B.
offset = point2.direction(A, B);

// Rotate this vector 90 degrees clockwise.
offset = vector2.perpendicular(offset);

// We want our offset to work in two directions perpendicular to the segment AB: up and down.
if (random.sign() === -1) {
  // Rotate offset by 180 degrees.
  offset.x = -offset.x;
  offset.y = -offset.y;
}

// Move the midpoint by an offset.
var offsetLength = Math.random() * 10;  // Offset by 10 pixels for example.
midpoint.x += offset.x * offsetLength;
midpoint.y += offset.y * offsetLength;

Below are functions used in the above code:
point2.midpoint = function(a, b) {
  var x = (a.x+b.x) / 2;
  var y = (a.y+b.y) / 2;
  return point2(x, y);
};

vector2.perpendicular = function(v) {
  /*
   * Rotates a vector by 90 degrees clockwise.
   */
  return vector2(-v.y, v.x);
};

random.sign = function() {
  return Math.random() &lt; 0.5 ? -1 : 1;
};
</code></pre></div>

### Finding Nearest Neighbor

<p>To find the nearest enemy for a rocket and the electro weapon, we iterate over an array of active enemies and compare their positions with the position of a rocket, or the shooting point in the case of the electro weapon. When a rocket locks on its target, it flies toward it until it hits or flies off the screen. For the electro weapon, it waits for a target to be in range.</p>

<p>A basic implementation may look like this:</p>

<div class="break-out">

<pre><code class="language-javascript">function nearest(position, entities) {
  /*
   * Given position and an array of entites, this function finds which entity is closest
   * to `position` and distance.
   */
  var distance, nearest = null, nearestDistance = Infinity;

  for (var i = 0; i &lt; entities.length; i++) {
    // Allow list of entities to contain the compared entity and ignore it silently.
    if (position !== entities[i].position) {
      // Calculate distance between two points, usually centers of mass of each entity.
      distance = point2.distance(position, entities[i].position);

      if (distance &lt; nearestDistance) {
        nearestDistance = distance;
        nearest = entities[i];
      }
    }
  }

  // Return the closest entity and distance to it, as it may come handy in some situations.
  return {&#039;entity&#039;: nearest, &#039;distance&#039;: nearestDistance};
}
</code></pre></div>

## Conclusion

<p>These topics cover only the basic ideas that support them. We hope after reading the article you now have a better idea of how to start developing such things. Check out the resources below and try doing something similar yourself.</p>

### Resources

<ul>
<li><a href="https://gamemechanicexplorer.com/">Game Mechanic Explorer</a>: A collection of concrete examples for various game mechanics, algorithms and effects. All examples are written in JavaScript.</li>
<li><a href="https://gafferongames.com/game-physics/integration-basics/">Integration Basics</a>: Discusses implementing some basic intergation methods.</li>
<li><a href="https://www-cs-students.stanford.edu/~amitp/gameprog.html">Amit’s Game Programming Information</a>: A list of bookmarks compiled by Amit Patel, with a lot of information about various game programming patterns and methods.</li>
<li><a href="https://gamedevelopment.tutsplus.com/">Tuts+ Game Development</a>: Collection of game development tutorials</li>
<li><a href="https://www.gamedev.net/page/index.html">Gamedev</a>: Largest and most popular game development portal and forums.</li>
<li><a href="https://gafferongames.com/game-physics/fix-your-timestep/">gafferongames.com</a>: Glenn Fiedler's game development articles.</li>
<li>“<a href="https://www.codeandweb.com/what-is-a-sprite-sheet/">What is a sprite sheet?</a>”: Information and video about sprite sheets and how they work.</li>
<li>“<a href="https://developer.mozilla.org/en-US/docs/Games/Techniques/2D_collision_detection">2D collision detection</a>”: From MDN's game development pages.</li>
</ul>

{{< signature "rb, ml, og" >}}
