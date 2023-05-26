---
title: Simplifying iOS Game Logic With Apple’s GameplayKit’s Rule Systems
slug: ios-game-logic-gameplaykit
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19dd8696-d965-4046-b2ef-e1cdcd204bcf/puzzle-games-500w-opt.jpg
date: 2017-04-25T19:13:21.000Z
author: lou-franco
description: >-
  When you develop a game, you need to sprinkle conditionals everywhere. If
  Pac-Man eats a power pill, then ghosts should run away. If the player has low
  health, then enemies attack more aggressively. If the space invader hits the
  left edge, then it should start moving right.

  Usually, these bits of code are strewn around, embedded in larger functions,
  and **the overall logic of the game** is difficult to see or reuse to build up
  new levels.
categories:
  - Mobile
  - Apps
  - Games
  - iOS
---
Apple’s GameplayKit has several algorithms and data structures that make it easier to follow game development best practices. One of them, <code>GKRuleSystem</code>, lets you build up complex conditional logic from smaller pieces. By structuring your code around it, you’ll create rules that are easier to change or reuse for new levels. In this article, we’re going to take typical game logic code and learn how to represent it as a rule system.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Using The Gamepad API In Web Games](https://www.smashingmagazine.com/2015/11/gamepad-api-in-web-games/)
*   [The Making Of "Melody Jams"](https://www.smashingmagazine.com/2016/05/the-making-of-melody-jams/)
*   [The Thumb Zone: Designing For Mobile Users](https://www.smashingmagazine.com/2016/09/the-thumb-zone-designing-for-mobile-users/)
*   [JavaScript AI For An HTML Sliding Tiles Puzzle](https://www.smashingmagazine.com/2016/02/javascript-ai-html-sliding-tiles-puzzle/)

## Puzzle Games Are Made Of Lots Of Similar Levels

I love puzzle games. The good ones start by teaching you how the game world works. Then, along the way, you discover new capabilities and apply them to harder challenges. The developer needs to balance each level to make sure that you never get bored or want to give up. Two of my favorites are <a href="https://itunes.apple.com/us/app/monument-valley/id728293409?mt=8"><em>Monument Valley</em></a> and <a href="https://itunes.apple.com/us/app/hundreds/id493536432?mt=8"><em>Hundreds</em></a>. A newer iOS game, <a href="https://itunes.apple.com/us/app/mini-metro/id837860959?mt=8"><em>Mini Metro</em></a>, is a subway simulation game and looks perfect for me. The developers say players need to “constantly redesign their line layout to meet the needs of a rapidly-growing city,” which is a good description of the progressive challenges I’m looking for.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bef6e7c0-b62e-4205-8066-bfe0b2a22621/puzzle-games-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bef6e7c0-b62e-4205-8066-bfe0b2a22621/puzzle-games-preview-opt.png" alt="Screenshots of Hundreds, Monument Valley, and Mini Metro." width="“600&quot;" height="394" /></a><figcaption>Screenshots of Hundreds, Monument Valley, and Mini Metro (Image credit: <a href="https://finji.co/about/sheet.php?p=hundreds">Finji</a>, <a href="https://www.monumentvalleygame.com/">ustwo</a>, and <a href="https://dinopoloclub.com/press/sheet.php?p=mini_metro">Dinosaur Polo Club</a>)</figcaption></figure>

These games have lots of levels, each one a little harder or with a new twist. <strong>You’d think that it would be easy to build up the code for successive levels from previous ones, but as you’ll see, it can be harder than it looks.</strong>

I recently started to make a game like this called <em>Puz-o-Mat</em>. The <em>Puz-o-Mat</em> is a box with five colored buttons on it. The goal of each level is to get all of the buttons to light up by discovering the pattern that satisfies the rules of the level. Puz-o-Mat will give you feedback if you are on the right track and buzz and flash its lights to reset the level if you make a mistake.</p>

{{< vimeo id="204541570" caption="A level being reset in <em>Puz-o-Mat</em>" >}}

## A Simple Game Gets Out Of Hand Quickly

To see why we might need a rule system, it’s useful to try to implement the game levels as a set of evaluation functions first. You can follow the code below in a <a href="https://github.com/loufranco/PuzOMatPlayground">Playground on GitHub</a>.

The goal of the first level of Puz-o-Mat is to press each button once. When you press a button, it lights up to let you know that you are on the right track. If you press one that is lit up already, the game will <strong><em>reset</em></strong> and the lights will turn off. When you tap each button once, you <strong><em>win</em></strong> the level.

Since we have a finite and defined set of game outcomes, we can just list them in an enum called <code>GameOutcome</code>:

<pre><code class="language-clike">enum GameOutcome: String {
   case win
   case reset
}
</code></pre>

And then, define an evaluation function that returns a <code>GameOutcome</code> given the buttons. If there is no outcome yet, it returns <code>nil</code>.

<pre><code class="language-clike">func evaluateLevel001(buttons: [Button]) -&gt; GameOutcome? {
   var foundUntappedButton = false

   for button in buttons {
       if button.tapCount &gt;= 2 {
           return .reset
       }
       else if button.tapCount == 0 {
           foundUntappedButton = true
       }
   }

   if !foundUntappedButton {
       return .win
   }

   return nil
}
</code></pre>

It’s not <em>too</em> hard to understand, <strong>but it’s concerning that we need a loop and three conditionals to describe the easiest level</strong>.

The second level of the game is a little harder to complete. Instead of pressing any button you want, you have to press them in order. Here’s how to do that:

<pre><code class="language-clike">func evaluateLevel002(buttons: [Button]) -&gt; GameOutcome? {
   var foundUntappedButton = false

   for button in buttons {
       if button.tapCount &gt;= 2 {
           return .reset
       }
       else if button.tapCount == 0 {
           foundUntappedButton = true
       }
       else if button.tapCount == 1 &amp;&amp; foundUntappedButton {
           return .reset
       }
   }

   if !foundUntappedButton {
       return .win
   }

   return nil
}
</code></pre>

This code has just one extra <code>else if</code> statement. It would be nice to share some code with the previous evaluator.

As we go on from level to level, you’ll find that a line here or there may be duplicated, but it’s hard to come up with a function that handles all levels. You could do it by taking another parameter, but this game is going to have 100’s of levels; we can’t keep adding parameters and extra conditionals for each of the variations.

Moving on, the next level needs you to tap the buttons in reverse order. The function looks exactly like the last one, except the loop looks like this:

<pre><code class="language-clike">for button in buttons.reversed()
</code></pre>

{{< vimeo id="204542578" caption="The reverse level being won in <em>Puz-o-Mat</em>" >}}

Again, a lot of code is the same, but it’s awkward to reuse.

There are some patterns, though.

1.  Each evaluator starts with some game state.
2.  Most of the work is checking conditionals against the game state to see what we should do next. There are many different conditions across the whole game, and each level seems to mix and match them.
3.  The main point of the evaluator is to decide if we need to reset or win.

Even though there is a pattern to the level game logic, all of the parts are mixed together and aren’t easily separated for reuse.</p>

### Refactoring around the conditionals

Using this insight we could try to restructure the code. A promising place to start is by pulling out the conditionals into separate functions. As we’ll see later, this is the design of GameplayKit’s rule system, but we can get part of the way there by playing with this code first. Then, we’ll convert our result to GameplayKit.

First, let’s use a type alias to define what a rule is:

<pre><code class="language-clike">typealias Rule = (_: [Button]) -&gt; GameOutcome?
</code></pre>

A rule is a function that takes the array of buttons and responds with an outcome if it knows what to do or, <code>nil</code> if not.

Many levels may limit the number of taps on a button, so we’ll make a function to return a rule that checks buttons against a tap limit:

<pre><code class="language-clike">func makeTapLimitRule(maxTaps: Int) -&gt; Rule {
   return { buttons in
       if (buttons.first { $0.tapCount &gt;= maxTaps }) != nil {
           return .reset
       }
       return nil
    }
}
</code></pre>

<code>makeTapLimitRule</code> takes a parameter, which is the number of taps to check for, and returns a closure that tells you if the game should reset or not.

Here’s one that can check if all buttons have been tapped once.</p>

<pre><code class="language-clike">func makeAllTappedRule() -&gt; Rule {
   return { buttons in
       if (buttons.first { $0.tapCount != 1 }) == nil {
           return .win
       }
       return nil
   }
}
</code></pre>

To use these buttons in our first level, we return an array of rules:

<pre><code class="language-clike">func rulesForLevel001() -&gt; [Rule] {
   return [
       makeTapLimitRule(maxTaps: 2),
       makeAllTappedRule(),
   ]
}
</code></pre>

Then, we need loop through all of the rules and run them so that they can check their conditional against the button state. If any of the rule functions return a <code>GameOutcome</code>, we’ll return it from the evaluator. If none are true, we’ll return <code>nil</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886637e1-cb72-4a8e-885c-1e1abd259c52/rules-diagram-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886637e1-cb72-4a8e-885c-1e1abd259c52/rules-diagram-preview-opt.png" alt="Diagram of rule evaluation." width="“&quot;" height="" /></a><figcaption>Diagram of rule evaluation</figcaption></figure>

The code is:

<pre><code class="language-clike">func evaluate(buttons: [Button], rules: [Rule]) -&gt; GameOutcome? {
   for rule in rules {
       if let outcome = rule(buttons) {
           return outcome
       }
   }
   return nil
}
</code></pre>

Our first level is simply:

<pre><code class="language-clike">func evaluateLevel001WithRules(buttons: [Button]) -&gt; GameOutcome? {
   return evaluate(buttons: buttons, rules: rulesForLevel001())
}
</code></pre>

Following this train of thought, you could expand the rules to take in more parameters or check more states. Each level is expressed as a list of rules that produce some outcome. Rules are separately encapsulated and easily reused.

This is such a common way of structuring algorithms in game logic, that Apple provides a set of classes in GameplayKit that we can use to build games in this style. They are collectively known as the Rule System classes and are primarily implemented in <a href="https://developer.apple.com/reference/gameplaykit/gkrulesystem"><code>GKRuleSystem</code></a> and <a href="https://developer.apple.com/reference/gameplaykit/gkrule"><code>GKRule</code></a>.

Using these Rule System classes hides all of the complexity of the evaluator, but more importantly, delivers much more power than our simple one.</p>

## GameplayKit’s Rules Systems

In the <code>GameplayKit</code> rule system, you need to define three things:

1.  **The game state** A dictionary that will represent your game state. It can have any keys and structure that you wish.
2.  **A set of _fact_ objects** The possible results of evaluating the rules. Facts can be any object, but in Swift it makes sense for them to be an enum. We could use the `GameOutcome` enum we used in our examples above.
3.  **A list of rules** The `GKRule` objects to evaluate. They each provide a conditional to check against the state and an action to perform if the conditional is true.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb801a6a-acf2-4afc-96c5-95a6087583ea/rulesystem-diagram-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb801a6a-acf2-4afc-96c5-95a6087583ea/rulesystem-diagram-preview-opt.png" alt="Diagram of GKRuleSystem objects." width="“&quot;" height="" /></a><figcaption>GKRuleSystem object relations</figcaption></figure>

To run the algorithm, we need to:

1.  Construct a `GKRuleSystem` object.
2.  Copy all of the game state dictionary entries into the object.
3.  Add the rules array to the rule system.
4.  Call the rule system object’s `evaluate` function.
5.  After evaluating, check to see if any facts were created.
    *   If any were, return the first fact as a game outcome.
    *   If not, return nil.

This diagram shows how the individual objects interact over time:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55471731-c199-444f-a6a4-0e28b3f024be/evaluate-diagram-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55471731-c199-444f-a6a4-0e28b3f024be/evaluate-diagram-preview-opt.png" alt="Diagram of GKRuleSystem evaluation." width="“&quot;" height="" /></a><figcaption>Diagram of GKRuleSystem evaluation</figcaption></figure>

The code to complete this interaction is straightforward:

<pre><code class="language-clike">func evaluate(state: [String: Any], rules: [GKRule]) -&gt; GameOutcome? {
   let rs = GKRuleSystem()
   rs.state.addEntries(from: state)
   rs.add(rules)
   rs.evaluate()

   if rs.facts.count &gt; 0, let fact = rs.facts[0] as? NSString {
       return  GameOutcome(rawValue: fact)
   }
   return nil
}
</code></pre>

Note: GameplayKit classes were designed for Objective-C, which is why I had to derive <code>GameOutcome</code> from <code>String</code> and use the enums as <code>rawValues</code>.

This is a very simple use of <code>GKRuleSystem</code>, and it’s fine if you don’t need to do this in the context of an action game (and need to keep up with a high frame rate). In that case, you can use the fact that the rule system <code>state</code> property is a mutable dictionary that you can alter directly rather than recreate. You could also reuse rule system objects with rules set up.

This is similar to our evaluator from the last section, but this one can operate over a more complex state object. Also, <code>GKRuleSystem.evaluate()</code> is more sophisticated than a loop over the rules. You can provide rule precedence, fact retraction (rules that reverse fact assertions), and find out which exact rules were invoked, among other features.</p>

### Converting our code to GKRules

The last step is converting our <code>Rule</code> functions to <code>GKRule</code>. You could derive <code>GKRule</code> subclasses for each rule, but for most applications, the <code>GKRule</code> constructors will be good enough.</p>

<a href="https://developer.apple.com/reference/gameplaykit/gkrule/1501102-init">One of the constructors</a> takes two blocks:

<pre><code class="language-clike">init(blockPredicate predicate: @escaping (GKRuleSystem) -&gt; Bool,
   action: @escaping (GKRuleSystem) -&gt; Void)
</code></pre>

The first block is a conditional that looks at the state, while the second block is called to assert a fact if the first block returns true.

It’s a little cumbersome to use, but here’s our two tap reset rule:

<pre><code class="language-clike">GKRule(
   blockPredicate: { rs in
       guard let buttons = rs.state["b"] as? [Button] else {
           return false
       }
       return (buttons.first { $0.tapCount &gt;= 2 }) != nil
   },
   action: { rs in
       rs.assertFact(GameOutcome.reset.rawValue)
   })
</code></pre>

During the <code>GKRuleSystem</code> evaluation, this object will have its first block called to see if the rule should be applied. The block could refer to external sources, but the most common thing is to look at the passed in rule system’s <code>state</code> property and check it for a condition. If the first block returns true, then the second one is called. It could also do <em>anything</em>, but it’s expected that it would assert or retract facts.

This is a good constructor to use if you have complex state and conditionals, or if you are using information outside of the rule system to implement rules. <strong>Since the expectation and normal case is to use the state and make facts, there is a more direct constructor to use.</strong>

If you can express your conditional as an <code>NSPredicate</code> against the state dictionary, <code>GKRule</code> <a href="https://developer.apple.com/reference/gameplaykit/gkrule/1501122-init">has a constructor to assert facts directly</a> based on them. It’s:

<pre><code class="language-clike">init(predicate: NSPredicate, assertingFact fact: NSObjectProtocol,
   grade: Float)
</code></pre>

Let’s extend <code>GameOutcome</code> with a function that creates <code>GKRule</code> objects for us.</p>

<pre><code class="language-clike">extension GameOutcome {
   func assertIf(_ predicateFormat: String) -&gt; GKRule {
       let pred = NSPredicate(format: predicateFormat)
       return GKRule(
           predicate: pred, assertingFact: self.rawValue, grade: 1.0)
    }
}
</code></pre>

Our rules function is just:

<pre><code class="language-clike">func predicateRulesForLevel001() -&gt; [GKRule] {
   return [
       GameOutcome.reset.assertIf("ANY $b.tapCount == 2"),
       GameOutcome.win.assertIf("ALL $b.tapCount == 1"),
   ]
}
</code></pre>

And the level evaluator becomes a one-liner:

<pre><code class="language-clike">func evaluateLevel001WithPredicateRules(buttons: [Button]) -&gt; GameOutcome? {
   return evaluate(state: ["b": buttons],
          rules: predicateRulesForLevel001())
}
</code></pre>

The only thing you need for a new level is a new list of <code>GKRules</code>. We have gone from an <em>imperative</em> level description where we need to give every step to a <em>declarative</em> one where we provide queries and outcomes.

Another benefit of this approach is that the predicates are serializable, so they can be stored in external files or sent over the network. With just a few more lines of code, we could move the predicate and enum to a .plist file and load them instead of hard-coding them. Then, a game designer on your team could make or tweak levels without editing code. The main coding work would be to add more state and outcomes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a5c67b8-c019-4b02-ae41-0c3ff7f0e4a3/rules-plist-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c05f5a-b07d-481e-8542-795f22ab4af9/rules-plist-preview-opt.png" alt="Level definitions in a .plist." width="“780&quot;" height="348" /></a><figcaption>Level definitions in a .plist (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a5c67b8-c019-4b02-ae41-0c3ff7f0e4a3/rules-plist-large-opt.png">Large preview</a>)</figcaption></figure>

In this example, facts are mutually exclusive; you can either win or reset, but not both. But, this is not a restriction of rule systems. If it makes sense for multiple facts to be asserted, then you may do so, and the code that checks the facts will need to reconcile them. One example is that we could treat each button’s light as a fact (on or off) and there would be a fact asserted for each button as the game was played. In that case, there could certainly be many facts asserted at the same time.

Finally, you may have noticed that facts are asserted with a grade. This grade is a number from 0 to 1 that you can think of as a probability that this fact is correct. We used 1 to indicate certainty, but you could use lower numbers to indicate that the fact only has a probability of being true. These probabilities can be combined and, using random numbers, we could pick among the asserted facts and have emergent, rather than deterministic, game behavior. This is known as <em>Fuzzy Logic</em>, and I’ll cover that in a future article.

All of the code in this article is available in a <a href="https://github.com/loufranco/PuzOMatPlayground">three-page Playground on GitHub</a>.</p>

### Final Notes

*   This article concentrated on just the game logic aspect of developing a game for iOS, but if you want to see how to construct the visual aspect of a game using SpriteKit, check out this series right here on Smashing: [Part I](https://www.smashingmagazine.com/2016/11/how-to-build-a-spritekit-game-in-swift-3-part-1/), [Part II](https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-2/), [Part III](https://www.smashingmagazine.com/2016/12/how-to-build-a-spritekit-game-in-swift-3-part-3/).
*   This [WWDC video](https://developer.apple.com/videos/play/wwdc2015/608/?time=2587) (Safari required) covers GameplayKit. Go to 43:10 in the video to hear about Rule Systems.

{{< signature "da, yk, aa, il" >}}

