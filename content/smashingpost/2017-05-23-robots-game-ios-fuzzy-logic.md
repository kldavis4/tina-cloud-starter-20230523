---
title: 'Building Killer Robots: Game Behavior In iOS With Fuzzy Logic Rule Systems'
slug: robots-game-ios-fuzzy-logic
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e54634d6-6726-471b-84d0-76fe8e10ee90/robot-war-start-500w-opt.png
date: 2017-05-23T22:25:32.000Z
author: lou-franco
description: >-
  Imagine that it's a hot day. The sun is out, and the temperature is rising.
  Perhaps, every now and then, there's a cool breeze. A good song is playing on
  the radio. At some point, you get up to get a glass of water, but the exact
  reason why you did that at that particular time isn't easy to explain. It was
  "too hot" and you were "somewhat thirsty," but also maybe "a little bored."
  Each of these qualities **isn't either/or, but instead fall on a spectrum of
  values**.

  In contrast, our software is usually built on Boolean values. We set `isHot`
  to `true` and if `isHot && isThirsty && isBored`, then we call `getWater()`.
  If we use code like this to control our game characters, then they will appear
  jerky and less natural. In this article, we'll learn how to add intelligent
  behavior to the non-player characters of a game using an alternative to
  conventional Boolean logic.
categories:
  - Coding
  - Mobile
  - Games
  - iOS
---
In contrast, our software is usually built on Boolean values. We set <code>isHot</code> to <code>true</code> and if <code>isHot &amp;&amp; isThirsty &amp;&amp; isBored</code>, then we call <code>getWater()</code>. If we use code like this to control our game characters, then they will appear jerky and less natural. In this article, we'll learn how to add intelligent behavior to the non-player characters of a game using an alternative to conventional Boolean logic.

To see why Boolean logic isn't good enough, look at this graph of <code>isHot</code> versus temperature.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b83305-7445-4307-9840-18e8d353d070/ishot-bool-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b83305-7445-4307-9840-18e8d353d070/ishot-bool-preview-opt.png" alt="isHot jumps from FALSE to TRUE" width="686" height="495" /></a><figcaption>isHot jumps from FALSE to TRUE.</figcaption></figure>

It jumps from <code>FALSE</code> to <code>TRUE</code> at 88°F (31°C), and when I combine this with a similar graph for boredom (based on the number of minutes ago a good song was playing), I get something like this:

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176af5d9-abb8-4e9e-9599-0b325ca614ab/ishot-isbored-bool-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f79dfbb9-ca49-43a9-8462-fd55e101d3d0/ishot-isbored-bool-780w-opt.png" alt="The combination also jumps from FALSE to TRUE" width="780" height="377" /></a><figcaption>The combination also jumps from FALSE to TRUE. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176af5d9-abb8-4e9e-9599-0b325ca614ab/ishot-isbored-bool-large-opt.png">View large version</a>)</figcaption></figure>

But if we used decimal numbers to represent <code>hotness</code>, <code>thirstiness</code> and <code>boredom</code>, we might be able to combine them and get more lifelike behavior. Here is the same graph of <code>hotness</code> and <code>boredom</code> using values from 0 to 1.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f35a96ab-b25c-40a1-af1d-15758d07863e/ishot-isbored-fuzzy-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc92ab2c-2461-4f32-ab44-842e4598f362/ishot-isbored-fuzzy-780w-opt.png" alt="" width="780" height="380" /></a><figcaption>The combination is now gradual. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f35a96ab-b25c-40a1-af1d-15758d07863e/ishot-isbored-fuzzy-large-opt.png">View large version</a>)</figcaption></figure>

If we use values from this formula to drive behavior, our characters will gradually move from one state to another.

This is called fuzzy logic, and in iOS games we can use GameplayKit's rule system classes to implement behavior based on it. Fuzzy Logic works well for driving complex behavior of the non-playable characters of a game. Let's build a small robot-fighting game in which we pit a fuzzy-logic-based AI against a random one.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [What Web Designers Can Learn From Video Games](https://www.smashingmagazine.com/2011/07/what-web-designers-can-learn-from-video-games/)
*   [Playful UX Design: Building A Better Game](https://www.smashingmagazine.com/2012/07/playful-ux-design-building-better-game/)
*   [How To Design An Open-Source iPhone Game](https://www.smashingmagazine.com/2013/02/designing-an-open-source-iphone-game/)
*   [Designing With Audio: What Is Sound Good For?](https://www.smashingmagazine.com/2012/04/designing-with-audio-what-is-sound-good-for/)

## GameplayKit Rule Systems

<a href="https://www.smashingmagazine.com/2017/04/ios-game-logic-gameplaykit/">In a previous article, we learned a simple way to use GameplayKit's rule systems</a> and how they make it easy to model and reuse conditional logic. We used its features to create a puzzle game in which the rules were black and white and well represented by Boolean values. To do this, we created <code>GKRule</code> objects whose <code>init</code> takes a predicate and a grade. It looked like this:

<pre><code class="language-clike">init(predicate: NSPredicate, assertingFact fact: NSObjectProtocol,
   grade: Float)
</code></pre>

The predicate determines whether the rule applies. If it's true, the rule establishes a fact at a given grade. In our examples, we always used a grade of 1.0, which meant certainty (absolutely trueness). The default value of any fact is 0.0, or absolute falseness. As a reminder, we made a game with five buttons, where you won if you tapped each one once and none of them twice. Our rule system was defined with this:

<pre><code class="language-clike">func predicateRulesForLevel001() -&gt; [GKRule] {
   return [
       GameOutcome.reset.assertIf("ANY $b.tapCount == 2"),
       GameOutcome.win.assertIf("ALL $b.tapCount == 1"),
   ]
}
</code></pre>

The <code>$b</code> in the expression is looked up from the game state passed to our <code>evaluate</code> function and contains an array of buttons. We reset the game if <em>any</em> of them had a tap count of two, and we won the game if <em>all</em> of them were tapped once.

The general idea is that the rules are expressions that set the grade of a fact based on the game state. We used grades of 1.0 and 0.0 to represent <code>TRUE</code> and <code>FALSE</code>.

Once we have rules, we can run them through a rule system, like so:

<pre><code class="language-clike">func evaluate(state: [String: Any], rules: [GKRule]) -&gt; GKRuleSystem {
   let rs = GKRuleSystem()
   rs.state.addEntries(from: state)
   rs.add(rules)
   rs.evaluate()

   return rs
}
</code></pre>

Then, we can look up the facts in the returned rule system (<code>rs</code>). In the previous article, only one fact would be asserted with 1.0 because the outcomes were mutually exclusive. The two possible facts were whether we won or lost the game, and only one could be true at a time.

For very simple games in which everything happens with certainty, Boolean-based conditionals make a lot of sense. However, as we saw in the Boolean graphs, if we used this to drive the behavior of in-game characters that are meant to seem more natural and less deterministic, then we'd want a way to transition from one behavior to another.</p>

### Transitioning to Fuzzy Values

We used 0.0 to represent <code>FALSE</code> and 1.0 to represent <code>TRUE</code>, but we can pass any number from 0.0 to 1.0 as a fact's grade, and doing so says that the fact's trueness isn't certain or has a probability. Values closer to 0.0 are more false, and those closer to 1.0 are more true.

Furthermore, <em>every</em> fact can be asserted with some kind of certainty, not just one we know is true. Doing so means we don't need predicates any more (since we always want to fire all rules). So, we can simplify rule creation with this function:

<pre><code class="language-clike">public func fuzzyRule(action: @escaping (GKRuleSystem, GameState) -&gt; ()) -&gt; GKRule {
    return GKRule(blockPredicate: { _ in true }, action: { (rs) in
        return action(rs, GameState(state: rs.state))
    })
}
</code></pre>

Using fuzzy rules, rather than rules that assert true and false facts, is especially useful for modeling non-player characters in games, so that their <strong>behavior seems to emerge from complex stimuli</strong>.</p>

## Robots Made With Fuzzy Logic

As an example, let's make a game that has two robots that are randomly spawned on a board. The code from this article is available in an <a href="https://github.com/loufranco/FuzzyLogicPlayground">Xcode playground on GitHub</a>.

We are going to use the same <code>GKRule</code> and <code>GKRuleSystem</code> classes from iOS' GameplayKit that we used for the conditional logic game from the previous article. But by using a more sophisticated state and by asserting multiple facts with a range of grades, we'll be able to make a much more complex game.

Here's what the game looks like when it starts.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23e66bfb-02ad-40eb-8d91-69e92387023e/robot-war-start-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/110f9c35-88fd-4625-ade1-9084cf8a2c36/robot-war-start-780w-opt.png" alt="The initial state of Robot War" width="780" height="780" /></a><figcaption>The initial state of Robot War. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23e66bfb-02ad-40eb-8d91-69e92387023e/robot-war-start-large-opt.png">View large version</a>)</figcaption></figure>

Neither robot can see the other, but at each point they can:

*   turn right,
*   turn left,
*   move forward,
*   use a radar to get the position of the other robot,
*   fire a laser.

In our game, we'll represent this as an <code>enum</code>:

<pre><code class="language-clike">public enum RobotAction: NSString {
    case turnRight
    case turnLeft
    case moveForward
    case radar
    case fireLaser

    public static let allValues = [
        turnRight,
        turnLeft,
        moveForward,
        radar,
        fireLaser]
}
</code></pre>

If they use their radar and it's successful, then they will only know their opponent's position at that point in time. Each use of the laser or radar depletes it, and it charges by one cell's worth of range each tick of the clock. Here's what it looks like if we make the robots roll a die and choose behaviors randomly.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/429bea3a-0ce9-47f7-9982-452126457d29/robot-war-random.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/429bea3a-0ce9-47f7-9982-452126457d29/robot-war-random.gif" alt="Robots with random behavior" width="600" height="600" /></a><figcaption>Robots with random behavior</figcaption></figure>

If I let this go on for a while, eventually one of the robots will accidentally win. We can do better than that.

If there were no uncertainty, then an easy strategy would be to turn towards your opponent, march towards them and fire when they are in range.

Given a <code>GameState</code> struct that can tell us our position, direction and the last known position of the opponent, a simple attack strategy would look like this:

<pre><code class="language-clike">// Move towards enemy and fire when facing them
func attackAction(state: GameState) -&gt; RobotAction? {
    // Calculate the distance between us and the opponent ...
    // if we move forward
    let fwdDist = state.enemyDistance(from: state.forwardCell(from: state.myDir))
    // if we turn left and then move forward
    let leftFwdDist = state.enemyDistance(from: state.forwardCell(from: state.myDir.left()))
    // if we turn right and then move forward
    let rightFwdDist = state.enemyDistance(from: state.forwardCell(from: state.myDir.right()))

    if fwdDist &lt;= leftFwdDist &amp;&amp; fwdDist &lt;= rightFwdDist {
        // Only move forward if we are not within laser range
        if fwdDist &gt; CGFloat(state.laserCharge) {
            return .moveForward
        }
    } else {
        return (leftFwdDist &lt;= rightFwdDist) ? .turnLeft : .turnRight
    }
    return nil
}
</code></pre>

When the opponent is right in front of us, we return <code>nil</code> to avoid crashing into them. This also gives us a chance to use our laser from this position.

This function breaks down if our opponent quickly abandons their position, because we'd march towards their old location with certainty.

## Fuzzy Logic Rule Systems

What we want to do is <strong>establish certainty as part of the game state</strong>. One feature of rule systems is that rules can see the facts that other rules have asserted (which creates an order dependency, which we'll describe later).

To build up more complex rules later, we'll first define uncertainty (and certainty), nearness and the percentage of laser and radar we have available. Once we have those as a base, we'll learn about the fuzzy equivalents to Boolean <code>AND</code> and <code>OR</code> that we can use to combine them to express a behavior such as shooting when we have a charged laser <em>and</em> when the enemy is near.

For us, certainty is based on how long ago the radar was used successfully. If we got a position a while ago, then we'd be less sure that it's worth using:

<pre><code class="language-clike">public let posUncertaintyRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let posUncertainty: Float = min(1.0, 0.05 * Float(state.ticksSinceEnemyKnown))
    rs.assertFact(RobotFact.posUncertainty.rawValue, grade: posUncertainty)
}
</code></pre>

The subexpression <code>0.05 * Float(state.ticksSinceEnemyKnown)</code> is <code>0.0</code> when we have had a successful radar hit. Each tick of the game clock makes this 5% more uncertain, until it maxes out at 100% uncertain. If we want the robots to have less trust in each other's position, we could make the uncertainty go up faster by using a larger coefficient, like <code>0.08</code>. This would make them use radar more often in an attempt to increase certainty.

A rule can assert only one fact, but sometimes it's useful to readily have the <code>NOT</code> version of a fuzzy logic variable. In fuzzy logic, the <code>NOT</code> of a <code>fuzzyValue</code> is <code>1.0 - fuzzyValue</code>. Here's the certainty rule based on that:

<pre><code class="language-clike">public let posCertaintyRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let posUncertainty = rs.grade(forFact: RobotFact.posUncertainty.rawValue)
    let posCertainty = 1.0 - posUncertainty
    rs.assertFact(RobotFact.posCertainty.rawValue, grade: posCertainty)
}
</code></pre>

When we implement rules to use the laser or radar, we'll want to know how charged they are. The fuzzy value we'll use is their percentage of the maximum charge:

<pre><code class="language-clike">public let hasLaserRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let hasLaserValue = Float(state.laserCharge) / Float(state.maxLaser)
    rs.assertFact(RobotFact.hasLaser.rawValue, grade: hasLaserValue)
}

public let hasRadarRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let hasRadarValue = Float(state.radarCharge) / Float(state.maxRadar)
    rs.assertFact(RobotFact.hasRadar.rawValue, grade: hasRadarValue)
}
</code></pre>

It's also useful to have a notion of <strong>nearness</strong>. We'll use the opponent's distance over the maximum distance to get us a value from 0.0 to 1.0, and then subtract from 1.0 so that near values are close to 1.0.</p>

<pre><code class="language-clike">public let isNearRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let diff = state.enemyDistance()
    let maxDiff = state.maximumDistance()
    let isNearValue = Float(1.0 - diff / maxDiff)
    rs.assertFact(RobotFact.isNear.rawValue, grade: isNearValue)
}
</code></pre>

These rules are a base that can be combined with each other into further rules. For example, suppose we want to use the radar if we have a fully charged radar <em>or</em> if we are uncertain of the opponent's position. We want to fire a laser if the opponent is near, if we have a charge <em>and</em> if their position is more certain. The <code>AND</code> and <code>OR</code> seem like Boolean operations, but as we'll see, fuzzy logic values require a different way to implement them.</p>

### More Fuzzy Logic Operators

In regular conditional logic, the <code>AND</code> operator is true if all of its operands are true and false otherwise. You can think of this as returning the least true operand. If we had fuzzy values of <code>(isNear: 0.9, hasLaser: 0.5, posCertain: 0.8)</code>, then we could mimic an <code>AND</code> by using the minimum value, or <code>0.5</code> in this case.</p>

<code>GKRuleSystem</code> can do that for us with pre-established facts using its <code>minimumGrade(forFacts:)</code> method. We'll use this in our laser rule like this:

<pre><code class="language-clike">let shouldFireRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    if !state.isFacingWall() {
        let shouldLaser = rs.minimumGrade(forFacts: [
            RobotFact.hasLaser.rawValue,
            RobotFact.posCertainty.rawValue,
            RobotFact.isNear.rawValue]
        )
        rs.assertFact(RobotAction.fireLaser.rawValue, grade: shouldLaser)
    }
}
</code></pre>

Because <code>minimumGrade(forFacts:)</code> returns the smallest value of the passed-in facts, it acts like a Boolean <code>AND</code> but for fuzzy values. You could read this as:

<pre><code class="language-clike">let shouldFire = hasLaser &amp;&amp; posIsCertain &amp;&amp; isNear
</code></pre>

Similarly, an <code>OR</code> is true if any of its operands are true. So, it returns the operand that is most true. We can use <code>maximumGrade(forFacts:)</code> in the radar rule to implement that.</p>

<pre><code class="language-clike">let shouldRadarRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let shouldRadar = rs.maximumGrade(forFacts: [
        RobotFact.hasRadar.rawValue,
        RobotFact.posUncertainty.rawValue]
    )
    rs.assertFact(RobotAction.radar.rawValue, grade:shouldRadar)
}
</code></pre>

The equivalent Boolean expression would be:

<pre><code class="language-clike">let shouldRadar = hasRadar || posIsUncertain
</code></pre>

This makes more sense with fuzzy values because it might be worth firing the radar when the robot is confused, even if the radar charge is low. With Boolean values, it would never make sense to use the radar if it is uncharged.

To finish off the simulation, we just need to reincorporate our attack function and introduce a wander rule. When we are sure of the opponent's position, we want to attack:

<pre><code class="language-clike">let attackRule = fuzzyRule { (rs: GKRuleSystem, state: GameState) in
    let posCertainty = rs.grade(forFact: RobotFact.posCertainty.rawValue)

    if let action = attackAction(state: state) {
        rs.assertFact(action.rawValue, grade: posCertainty)
    }
}
</code></pre>

As the radar hit becomes a distant memory, this rule will have less of an effect. If we did nothing, the robot would stand still and use its radar repeatedly, just hoping that its opponent moves within range. To make it more interesting, we'll have the robot wander around when it has nothing else to do.

This function has it circle around an inner loop, three cells away from the wall:

<pre><code class="language-clike">let wanderRule = fuzzyRule { (rs: GKRuleSystem, state:GameState) in
    let posUncertainty = rs.grade(forFact: RobotFact.posUncertainty.rawValue)

    if (state.isInBounds(pos: state.forwardCell(from: state.myDir, steps: 3))) {
        rs.assertFact(RobotAction.moveForward.rawValue, grade: posUncertainty)
    } else {
        rs.assertFact(RobotAction.turnLeft.rawValue, grade: posUncertainty)
    }
}
</code></pre>

The expression <code>state.isInBounds(pos: state.forwardCell(from: state.myDir, steps: 3))</code> returns <code>TRUE</code> if the robot could move forward and still be three cells away from a wall. If this is <code>FALSE</code>, it turns left. The effect is that the robot wanders around the middle of the board when the uncertainty of the other robot's position is high. At the same time, the radar will be charging, so the radar rule will supersede this one at times, and with the combination of wandering around and using the radar, this robot will eventually find the other one.

With all of these rules created, we can run the rule system. Remember that some rules depend on others, which we can express by the order in which we add them to the system.</p>

<pre><code class="language-clike">func nextAction(state: [String: Any]) -&gt; RobotAction {
    let ruleSystem = GKRuleSystem()
    ruleSystem.state.addEntries(from: state)

   // Add the rules such that dependent ones come later in the array
    ruleSystem.add([
        posUncertaintyRule,
        posCertaintyRule,

        isNearRule,
        hasLaserRule,
        hasRadarRule,

        attackRule,
        shouldFireRule,
        shouldRadarRule,
        wanderRule,
    ])
    ruleSystem.evaluate()

    // Find the action facts that have the highest grade
    let maxGrade = ruleSystem.maximumGrade(forFacts: RobotAction.allValues.map { $0.rawValue } )
    let maxFacts = RobotAction.allValues.flatMap { ruleSystem.grade(forFact: $0.rawValue) == maxGrade ? $0 : nil }

    // Choose randomly from the highest graded facts if there is a tie.
    return maxFacts[GKRandomDistribution(lowestValue:0, highestValue: maxFacts.count - 1).nextInt()]
}
</code></pre>

Because it's possible that the rule system will assert multiple facts of the same grade, on the last line of the function, we'll randomly choose from among them.

With these rules, the red robot is now much better at fighting and almost always wins:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29b6115f-0017-4e6b-a8bc-6beaf8d7b4fd/robot-war-win.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29b6115f-0017-4e6b-a8bc-6beaf8d7b4fd/robot-war-win.gif" alt="Red Robot is smart now" width="600" height="600" /></a><figcaption>Red Robot is smart now.</figcaption></figure>

A big advantage of writing our game logic in this way is that we can have many different notions of when to attack, wander or fire, and we can mix and match them to create different styles of fighting. We can also have rules that increase or decrease the certainty of any grade. For example, squaring a grade lowers its certainty, and taking the square root raises it (this works because grades are always between 0.0 and 1.0).

See the full implementation in my <a href="https://github.com/loufranco/FuzzyLogicPlayground">Xcode playground</a>. You can set an action function for each robot, so you can try to implement your own rules to beat the one we created here.

If you want to see another example of how to use fuzzy values and combine them to drive behavior, see the "<a href="https://developer.apple.com/videos/play/wwdc2015/608/?time=2587">Introducing GameplayKit</a>" video from WWDC 2015 (Safari only), in which a traffic simulator is built with fuzzy ideas of closeness and speed. If you <a href="https://developer.apple.com/videos/play/wwdc2015/608/?time=2924">jump right to the demo of the simulator</a>, you will see the cars keeping a natural distance from each other and obeying traffic laws at intersections and on the freeway.</p>

### Final Notes

*   The playground associated with this article has the entire game, using SpriteKit's `SKScene` and `SKSpriteNode` to implement the visuals of the game. You can learn about those classes in the Smashing Magazine series on them: [part 1](https://www.smashingmagazine.com/2016/11/how-to-build-a-spritekit-game-in-swift-3-part-1/), [part 2](https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-2/), [part 3](https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-3/).
*   Look on Apple's developer website for the full documentation for [GKRuleSystem](https://developer.apple.com/reference/gameplaykit/gkrulesystem) and [GKRule](https://developer.apple.com/reference/gameplaykit/gkrule).

{{< signature "da, vf, yk, al, il" >}}

