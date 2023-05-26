---
title: 'An Introduction To Stimulus.js'
slug: introduction-stimulusjs
author: mike-rogers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d032726-1ff0-4e40-90c5-172b70d6ea5a/introduction-stimulusjs.png
date: 2020-07-15T10:30:00.000Z
summary: >-
  In this article, Mike Rogers will introduce you to Stimulus, a modest JavaScript framework that complements your existing HTML. By the end, you’ll have an understanding of the premise of Stimulus and why it’s a useful tool to have in your backpack.
description: >-
  In this article, Mike Rogers will introduce you to Stimulus, a modest JavaScript framework that complements your existing HTML. By the end, you’ll have an understanding of the premise of Stimulus and why it’s a useful tool to have in your backpack.
categories:
  - JavaScript
  - Frameworks
  - Tools
  - Generators
---

The web moves pretty fast and picking an approach for your frontend that will feel sensible in a year’s time is tricky. My biggest fear as a developer is picking up a project that hasn’t been touched for a while, and finding the documentation for whatever approach they used is either non-existent or is not easily found online.

About a year ago, I started using Stimulus and I felt really happy about the code I was shipping. It’s a **~30kb library** which encourages small reusable sprinkles of JavaScript within your app, organized in such a way that it leaves little hints in your accessible HTML as to where to find the JavaScript it’s connected to. It makes understanding how a piece of JavaScript will interact with your page almost like reading pseudocode.

Stimulus was created by the team at Basecamp &mdash; they recently released the *HEY* email service &mdash; to help maintain the JavaScript they write for their web applications. Historically, Basecamp has been quite good around maintaining their open-source projects, so I feel quite confident that Stimulus has been tested thoroughly, and will be maintained for the next few years.

Stimulus has allowed me to build applications in a way that feels reusable and approachable. While I don’t think Stimulus will take over the web like React and Vue have, I think it is a worthwhile tool to learn.

### Terminology

Like all frameworks, Stimulus has preferred terms for describing certain things. Luckily (and one of the main reasons I’ve taken to liking Stimulus), there are only two you’ll need to know about:
 
- **Controller**  
This refers to instances of JavaScript classes which are the building blocks of your application. It’s safe to say that when we talk about Stimulus Controllers, we’re talking about JavaScript classes.
- **Identifier**  
This is the name we’ll use to reference our controller in our HTML using a data attribute that is common to Stimulus codebases.

{{% feature-panel %}}

## Let’s Jump Into Stimulus!

In the following few examples, I’m going to use code you can drop into the browser to get started right away via the library distributed via [unpkg.com](https://unpkg.com/). Later on, I’ll cover the webpack approach which is highly encouraged as it allows for improved organization of your code and is the approach used in the Stimulus Handbook.

### The Boilerplate

{{< codepen height="480" theme_id="light" slug_hash="abdjXvP" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [The Boilerplate - Stimulus](https://codepen.io/smashingmag/pen/abdjXvP) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

Once you understand the gist of the above snippet, you’ll have the knowledge to be comfortable picking up a project that uses Stimulus.

Pretty awesome, right? Let’s jump into what everything is doing!

#### `application.start`

This line tells Stimulus to add the listeners to the page. If you call it just once at the top of your page before you add any Stimulus code, it’ll return an instance of the main Stimulus controller which includes the method `register` that is used to tell Stimulus about the classes you’d like to connect to it.

#### Controllers

The `data-controller` attribute connects our HTML element to an instance of our JavaScript class. In this case, we used the identifier “counter” to hook up an instance of the `CounterController` JavaScript class to our `div` element. We told Stimulus about the connection between this identifier and the controller via the `application.register` method.

Stimulus will continuously monitor your page for when elements with this attribute are added and removed. When a new piece of HTML is added to the page with a `data-controller` attribute, it’ll initialize a new instance of the relevant controller class, then connect the HTML element. If you remove that element from the page, it’ll call the `disconnect` method on the controller class.

#### Actions

Stimulus uses a data attribute `data-action` to clearly define which function of the controller will be run. Using the syntax `event->controller#function` anyone reading the HTML will be able to see what it does. This is especially useful as it reduces the risk of unexpected code from other files, making it easier to navigate the codebase. When I first saw the approach Stimulus encourages, it felt almost like reading pseudocode. 

In the above example, when the button fires the “click” event, it will be passed onto the `addOne` function within our “counter” controller.

#### Targets

Targets are a way to explicitly define which elements are going to be available to your controller. Historically I’ve used a mix of ID, CSS class names and data attributes to achieve this, so having a single “This is the way to do it” which is so explicit makes the code a lot more consistent.

This requires defining your target names within your controller class via the `targets` function and adding the name to an element via the `data-target`.

Once you’ve got those two pieces setup, your element will be available in your controller. In this case, I’ve set up the target with the name “output” and it can be accessed by `this.outputTarget` within the functions in our controller.

### Duplicate Targets

{{< codepen height="480" theme_id="light" slug_hash="ExPprPG" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Duplicate Targets - Stimulus](https://codepen.io/smashingmag/pen/ExPprPG) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

If you have multiple targets with the same name, you can access them by using the plural version of the target method, in this case when I call `this.outputTargets`, it’ll return an array containing both my divs with the attribute `data-target="hello.output"`.

### Event Types

You listen for any of the events you’d commonly be able to attach via the JavaScript method [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener). So for example, you could listen for when a button is clicked, a form is submitted or an input is changed.

{{< codepen height="480" theme_id="light" slug_hash="wvMxNGJ" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Event types - Stimulus](https://codepen.io/smashingmag/pen/wvMxNGJ) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

To listen to `window` or `document` events (such as resizing, or the user going offline), you’ll need to append “@window” or “@document” to the `event` type (e.g. `resize@window->console#logEvent` will call the function `logEvent`) on the `console` controller when the window is resized.

There is a [shorthand way to attach common events](https://stimulusjs.org/reference/actions#event-shorthand), where you are able to omit the event type and it has a default action for the element type. However, I strongly discourage using the event shorthand, as it increases the amount of assumptions someone who is less familiar with Stimulus needs to make about your code.

{{% ad-panel-leaderboard %}} 

### Uses Multiple Controllers In The Same Element

Quite often you may want to break out two pieces of logic into separate classes, but have them appear close to each other within the HTML. Stimulus allows you to connect elements to multiple classes by placing references to both within your HTML.

{{< codepen height="480" theme_id="light" slug_hash="XWXBOjy" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Multiple Controllers - Stimulus](https://codepen.io/smashingmag/pen/XWXBOjy) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

In the above example, I’ve set up a `basket` object which only concerns itself with counting the total number of items in the basket, but also added a `child` object that shows the amount of bags per item.

### Passing Data To Your Object

{{< codepen height="480" theme_id="light" slug_hash="mdVjvOP" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Passing Data - Stimulus](https://codepen.io/smashingmag/pen/mdVjvOP) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

Stimulus provides the methods `this.data.get` and `this.data.set` within the controller class, this will allow you to change data attributes which are within the same namespace as the identifier. By this I mean if you want to pass data to your stimulus controller from your HTML, just add an attribute like `data-[identifier]-a-variable` to your HTML element.

When calling `this.data.set`, it will update the value in your HTML so you can see the value change when you inspect the element using your browser development tools.

Using namespaced data attributes is a really nice way to help make it really clear which data attribute is for what piece of code.

### Initialize, Connected, Disconnected

As your application grows, you’ll probably need to hook into 'lifecycle events' to set defaults, fetch data, or handle real-time communication. Stimulus has three build-in methods which are called throughout the lifecycle of a Stimulus class.

{{< codepen height="480" theme_id="light" slug_hash="ZEQjwBj" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Initialize, Connected, Disconnected - Stimulus
](https://codepen.io/smashingmag/pen/ZEQjwBj) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

When Stimulus sees an element with a matching `data-controller` attribute, it will create a new version of your controller and call the `initialize` function. This will often run when you first load the page, but will also be run if you were to append new HTML to your page (e.g. via AJAX) containing a reference to your controller. It will not run when you move an element to a new position within your DOM.

After a class has been initialized, Stimulus will connect it to the HTML element and call the `connect` function. It’ll also call `connect` if you were to move an element within your DOM. So if you were to take an element, remove it from one element, then append it somewhere else, you’d notice only `connect` will be called.

The `disconnect` function will be run when you remove an element from your page, so for example, if you were to replace the body of your HTML, you could tear down any code which might need to be rerun if the element isn’t in the same position. For example, if you had a fancy WYSIWYG editor which adds lots of extra HTML to an element, you could revert it to its original state when `disconnect` was called.

### Inheriting Functionality

On occasion, you may want to share a little common functionality between your Stimulus controllers. The cool thing about Stimulus is that (under the hood) you’re connecting somewhat vanilla JavaScript classes to HTML elements, so sharing functionality should feel familiar.

{{< codepen height="480" theme_id="light" slug_hash="JjGBxbq" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Inheriting functionality - Stimulus](https://codepen.io/smashingmag/pen/JjGBxbq) by <a href="https://codepen.io/mikerogers0">Mike Rogers</a>.{{< /codepen >}}

In this example, I set up a parent class named `ParentController`, which is then extended by a child class named `ChildController`. This let me inherit methods from the `ParentController` so I didn’t have to duplicate code within my `ChildController`.

{{% ad-panel-leaderboard %}} 

## Using It In Production

I demonstrated some fairly stand-alone examples of how to use Stimulus above, which should give you a taste of what you can achieve. I also thought I should touch on how I use it in production and how it has worked out for me.

### Webpack

If you’re using Webpack, you’re in for a treat! Stimulus was totally made to be used with Webpack. Their documentation even has a [lovely starter kit for Webpack](https://github.com/stimulusjs/stimulus-starter). It’ll allow you to break your controllers into separate files and Stimulus will decide on the correct name to use as an identifier.

You don’t have to use webpack if you want to use Stimulus, but it cleans up the experience a bunch. Personally, Stimulus was the library that helped introduce me to Webpack and really feel the value it offered.

### Filename Conventions

I mentioned in the introduction of this article that I enjoyed using Stimulus because it felt organized. This really becomes apparent when you are combining it with Webpack, which enables auto loading and registration of controllers.

Once you’ve set up Stimulus in Webpack, it’ll [encourage you to name your files](https://stimulusjs.org/handbook/installing#controller-filenames-map-to-identifiers) like `[identifier]_controller.js`, where the identifier is what you’ll pass into your HTMLs `data-controller` attribute.

As your project grows, you may also want to move your Stimulus controllers into subfolders. In a magical way, Stimulus will convert underscores into dashes, and folder forward slashes into two dashes, which will then become your identifier. So for example, the filename `chat/conversation_item_controller.js` will have the identifier `chat--conversation-item`.

### Maintaining Less JavaScript

One of my favorite quotes is “The Best Code is No Code At All”, I try to apply this approach to all my projects. 

Web browsers are evolving a lot, I’m pretty convinced that most of the things I need to write JavaScript for today will become standardized and baked into the browser within the next 5 years. A good example of this is the [details element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/details), when I first started in development it was super common to have to manually code that functionality by hand using jQuery.

As a result of this, if I can write accessible HTML with a sprinkling of JavaScript to achieve my needs, with the mindset of “This does the job today, but in 5 years I want to replace this easily” I’ll be a happy developer. This is much more achievable when you’ve written less code to start with, which Stimulus lends itself to.

### HTML First, Then JavaScript

One aspect I really like about the approach Stimulus encourages, is I can focus on sending HTML down the wire to my users, which is then jazzed up a little with JavaScript. 

I’ve always been a fan of using the first few milliseconds of a user’s attention getting what I have to share with them &mdash; in front of them. Then worrying setting up the interaction layer while the user can start processing what they’re seeing.

Furthermore, if the JavaScript were to fail for whatever reason, the user can still see the content and interact with it without JavaScript. For example, instead of a form being submitted via AJAX, it’ll submit via a traditional form request which reloads the page.

## Conclusion

I love building sites that need just small sprinkles of maintainable JavaScript to enhance the user experience, sometimes it’s nice to just build something which feels simpler. Having something lightweight is great, I really love that without too much cognitive load it’s pretty clear how to organize your files, and set up little breadcrumbs that hint about how the JavaScript will run with a piece of HTML.

I’ve really enjoyed working with Stimulus. There isn’t too much to it, so the learning curve is fairly gentle. I feel pretty confident that if I was to pass my code onto someone else they’ll be happy developers. I’d highly recommend giving it a try, even if it’s just out of pure curiosity.

The elephant in the room is how does it stack up compared to the likes of React and Vue, but in my mind, they’re different tools for a different requirement. In my case, I’m often rendering out HTML from my server and I’m adding a little JavaScript to improve the experience. If I was doing something more complex, I’d consider a different approach (or push back on the requirements to help keep my code feeling simple).

### Further Reading

- [Stimulus Homepage](https://stimulusjs.org/)  
They have a fantastic handbook that goes into the concepts I’ve outlined above into a lot more depth.
- [Stimulus GitHub Repository](https://github.com/stimulusjs/stimulus)  
I’ve learned so much about how Stimulus works by exploring their code. 
- [Stimulus Cheatsheet](https://gist.github.com/mrmartineau/a4b7dfc22dc8312f521b42bb3c9a7c1e)  
The handbook summarized on a single page.
- [Stimulus Forum](https://discourse.stimulusjs.org/)  
Seeing other people working with Stimulus has made me really feel like it’s being used in the wild.

{{< signature "sh, ra, yk, il" >}}
