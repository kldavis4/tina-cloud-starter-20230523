---
title: 'How To Create A Card Matching Game Using Angular And RxJS'
slug: card-matching-game-angular-rxjs
author: anna-prenzel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ad8d7ad-9d35-4923-b6cf-4a34b27b9cf2/card-matching-game-angular-rxjs.png
date: 2020-01-30T13:00:00.000Z
summary: >-
  This article is dedicated to Angular developers who want to harness the concept of reactive programming. This is a programming style that &mdash; simply put &mdash; deals with the processing of asynchronous data streams.
description: >-
  This article is dedicated to Angular developers, who want to harness the concept of reactive programming. This is a programming style that &mdash; simply put &mdash; deals with the processing of asynchronous data streams.
categories:
  - UI
  - Angular
  - JavaScript
  - User Interaction
---

Today, I’d like to focus on data streams resulting from click events on the user interface. The processing of such clickstreams is particularly useful for applications with an intensive user interaction where many events have to be processed. I’d also like to introduce you to RxJS a bit more; it’s a JavaScript library that can be used to express event handling routines compactly and concisely in a reactive style.

## What Are We Building?

Learning games and knowledge quizzes are popular both for younger and older users. An example is the game “pair matching”, where the user has to find related pairs in a mixture of images and/or text snippets.

The animation below shows a simple version of the game: The user selects two elements on the left and right side of the playing field one after the other, and in any order. Correctly matched pairs are moved to a separate area of the playing field, while any wrong assignments are immediately dissolved so that the user has to make a new selection. 

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38120a52-1daa-43a3-8694-261adc67d915/card-matching-game-angular-rxjs-game.gif" alt="Screen capture of the learningl game “matching pairs”" /><figcaption>A sneak peek of the game we’ll be creating today</figcaption></figure>

In this tutorial, we will build such a learning game step by step. In the <a href="#angular-component-learning-game">first part</a>, we will build an Angular component that is just showing the playing field of the game. Our aim is that the component can be configured for different use cases and target groups &mdash; from an animal quiz up to a vocabulary trainer in a language learning app. For this purpose, Angular offers the concept of content projection with customizable templates, which we will make use of. To illustrate the principle, I will build two versions of the game (“game1” and “game2”) with different layouts.

In the <a href="#control-user-interaction-rxjs">second part</a> of the tutorial, we will focus on reactive programming. Whenever a pair is matched, the user needs to get some sort of feedback from the app; it is this event handling that is realized with the help of the library RxJS.

- **Requirements**  
To follow this tutorial, the [Angular CLI must be installed](https://cli.angular.io/).
- **Source Code**  
The source code of this tutorial can be found [here](https://smashingmagazine.com/provide/card-matching-game-angular-rxjs-learning-app.zip) (14KB).

{{% feature-panel %}}

## 1. Building An Angular Component For The Learning Game

### How To Create The Basic Framework

First, let’s create a new project named “learning-app”. With the Angular CLI, you can do this with the command `ng new learning-app`. In the file *app.component.html*, I replace the pre-generated source code as follows:

<pre><code class="language-html">&lt;div style="text-align:center"&gt; 
  &lt;h1&gt;Learning is fun!&lt;/h1&gt;
&lt;/div&gt;
</code></pre>

In the next step, the component for the learning game is created. I’ve named it “matching-game” and used the command `ng generate component matching-game`. This will create a separate subfolder for the game component with the required HTML, CSS and Typescript files. 

As already mentioned, the educational game must be configurable for different purposes. To demonstrate this, I create two additional components (`game1` and `game2`) by using the same command. I add the game component as a child component by replacing the pre-generated code in the file *game1.component.html* or *game2.component.html* with the following tag:

<pre><code class="language-html">&lt;app-matching-game&gt;&lt;/app-matching-game&gt;
</code></pre>

At first, I only use the component `game1`. In order to make sure that game 1 is displayed immediately after starting the application, I add this tag to the *app.component.html* file:

<pre><code class="language-html">&lt;app-game1&gt;&lt;/app-game1&gt;
</code></pre>

When starting the application with `ng serve --open`, the browser will display the message “matching-game works”. (This is currently the only content of *matching-game.component.html*.)

Now, we need to test the data. In the `/app` folder, I create a file named *pair.ts* where I define the class `Pair`:

<pre><code class="language-ts">export class Pair {
  leftpart: string;
  rightpart: string;
  id: number;
}
</code></pre>

A pair object comprises two related texts (`leftpart` and `rightpart`) and an ID.

The first game is supposed to be a species quiz in which species (e.g. `dog`) have to be assigned to the appropriate animal class (i.e. `mammal`).

In the file *animals.ts*, I define an array with test data:

<pre><code class="language-ts">import { Pair } from './pair';
export const ANIMALS: Pair[] = [
  { id: 1, leftpart: 'dog', rightpart: 'mammal'},
  { id: 2, leftpart: 'blickbird', rightpart: 'bird'},
  { id: 3, leftpart: 'spider', rightpart: 'insect'},
  { id: 4, leftpart: 'turtle', rightpart: 'reptile' },
  { id: 5, leftpart: 'guppy', rightpart: 'fish'},
];
</code></pre>

The component `game1` needs access to our test data. They are stored in the property `animals`. The file *game1.component.ts* now has the following content:

<pre><code class="language-ts">import { Component, OnInit } from '@angular/core';
import { ANIMALS } from '../animals';
@Component({
  selector: 'app-game1',
  templateUrl: './game1.component.html',
  styleUrls: ['./game1.component.css']
})
export class Game1Component implements OnInit {
  animals = ANIMALS;
  constructor() { }
  ngOnInit() {
  }
}
</code></pre>

### The First Version Of The Game Component

Our next goal: The game component `matching-game` has to accept the game data from the parent component (e.g. `game1`) as input. The input is an array of "pair" objects. The user interface of the game should be initialized with the passed objects when starting the application.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38120a52-1daa-43a3-8694-261adc67d915/card-matching-game-angular-rxjs-game.gif" alt="Screen capture of the learningl game “matching pairs”" /></figure>

For this purpose, we need to proceed as follows:

1. Add the property `pairs` to the game component using the `@Input` decorator.
2. Add the arrays `solvedPairs` and `unsolvedPairs` as additional private properties of the component. (It is necessary to distinguish between already "solved" and "not yet solved" pairs.)
3. When the application is started (see function `ngOnInit`) all pairs are still "unsolved" and are therefore moved to the array `unsolvedPairs`.

<pre><code class="language-ts">import { Component, OnInit, Input } from '@angular/core';
import { Pair } from '../pair';
@Component({
  selector: 'app-matching-game',
  templateUrl: './matching-game.component.html',
  styleUrls: ['./matching-game.component.css']
})

export class MatchingGameComponent implements OnInit {
  @Input() pairs: Pair[];
  private solvedPairs: Pair[] = [];
  private unsolvedPairs: Pair[] = [];
  constructor() { }
  ngOnInit() {      
    for(let i=0; i&lt;this.pairs.length; i++){    
        this.unsolvedPairs.push(this.pairs[i]);
    }
  }
}
</code></pre>

Furthermore, I define the HTML template of the `matching-game` component. There are containers for the unsolved and solved pairs. The `ngIf` directive ensures that the respective container is only displayed if at least one unsolved or solved pair exists.

In the container for the unsolved pairs (class `container unsolved`), first all `left` (see the left frame in the GIF above) and then all `right` (see the right frame in the GIF) components of the pairs are listed. (I use the `ngFor` directive to list the pairs.) At the moment, a simple button is sufficient as a template.

With the template expression `{{{pair.leftpart}}` and {`{{pair.rightpart}}}`, the values of the properties `leftpart` and `rightpart` of the individual pair objects are queried when iterating the `pair` array. They are used as labels for the generated buttons.

The assigned pairs are listed in the second container (class `container solved`). A green bar (class `connector`) indicates that they belong together.

The corresponding CSS code of the file *matching-game.component.css* can be found in the source code at the beginning of the article.

<div class="break-out">

 <pre><code class="language-css">&lt;div id="game"&gt;
   &lt;div class="container unsolved" &#42;ngIf="unsolvedPairs.length&gt;0"&gt;
      &lt;div class="pair_items left"&gt;
         &lt;button &#42;ngFor="let pair of unsolvedPairs" class="item"&gt;  
             {{pair.leftpart}}
         &lt;/button&gt;        
      &lt;/div&gt;
    &lt;div class="pair_items right"&gt;
      &lt;button &#42;ngFor="let pair of unsolvedPairs" class="item"&gt; 
            {{pair.rightpart}}
         &lt;/button&gt;  
    &lt;/div&gt;
   &lt;/div&gt;
   &lt;div class="container solved" &#42;ngIf="solvedPairs.length&gt;0"&gt;
       &lt;div &#42;ngFor="let pair of solvedPairs" class="pair"&gt;
          &lt;button&gt;{{pair.leftpart}}&lt;/button&gt;
          &lt;div class="connector"&gt;&lt;/div&gt;
          &lt;button&gt;{{pair.rightpart}}&lt;/button&gt;
       &lt;/div&gt;
   &lt;/div&gt;
&lt;/div&gt;
</code></pre>
</div>

In the component `game1`, the array `animals` is now bound to the `pairs` property of the component `matching-game` (one-way data binding).

<pre><code class="language-html">&lt;app-matching-game [pairs]="animals"&gt;&lt;/app-matching-game&gt;
</code></pre>

The result is shown in the image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb84db0f-f394-467e-a682-553aa5cfd89c/card-matching-game-angular-rxjs-figure2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb84db0f-f394-467e-a682-553aa5cfd89c/card-matching-game-angular-rxjs-figure2.png" sizes="100vw" caption="Current state of the user interface" alt="Current state of the user interface" >}}

Obviously, our matching game is not too difficult yet, because the left and right parts of the pairs are directly opposite each other. So that the pairing is not too trivial, the right parts should be mixed. I solve the problem with a self-defined pipe `shuffle`, which I apply to the array `unsolvedPairs` on the right side (the parameter `test` is needed later to force the pipe to be updated):

<div class="break-out">

 <pre><code class="language-ts">...
&lt;div class="pair_items right"&gt;
  &lt;button &#42;ngFor="let pair of unsolvedPairs | shuffle:test" class="item"&gt; 
        {{pair.rightpart}}
  &lt;/button&gt;  
&lt;/div&gt;
...
</code></pre>
</div>

The source code of the pipe is stored in the file *shuffle.pipe.ts* in the app folder (see source code at the beginning of the article). Also note the file *app.module.ts*, where the pipe must be imported and listed in the module declarations. Now the desired view appears in the browser.

### Extended Version: Using Customizable Templates To Allow An Individual Design Of The Game

Instead of a button, it should be possible to specify arbitrary template snippets to customize the game. In the file *matching-game.component.html* I replace the button template for the left and right side of the game with an `ng-template` tag. I then assign the name of a template reference to the property `ngTemplateOutlet`. This gives me two placeholders, which are replaced by the content of the respective template reference when rendering the view. 

We are here dealing with the concept of **content projection**: certain parts of the component template are given from outside and are "projected" into the template at the marked positions. 

When generating the view, Angular must insert the game data into the template. With the parameter `ngTemplateOutletContext` I tell Angular that a variable `contextPair` is used within the template, which should be assigned the current value of the `pair` variable from the `ngFor` directive.

The following listing shows the replacement for the container `unsolved`. In the container `solved`, the buttons have to be replaced by the `ng-template` tags as well.

<div class="break-out">

 <pre><code class="language-ts">&lt;div class="container unsolved" &#42;ngIf="unsolvedPairs.length&gt;0"&gt;
&lt;div class="pair_items left"&gt;        
    &lt;div &#42;ngFor="let pair of unsolvedPairs" class="item"&gt;
         &lt;ng-template [ngTemplateOutlet]="leftpart_temp" 
             [ngTemplateOutletContext]="{contextPair: pair}"&gt;
       &lt;/ng-template&gt;
    &lt;/div&gt;    
&lt;/div&gt;    
&lt;div class="pair_items right"&gt;
    &lt;div &#42;ngFor="let pair of unsolvedPairs | shuffle:test" class="item"&gt;           
         &lt;ng-template [ngTemplateOutlet]="leftpart_temp"
           [ngTemplateOutletContext]="{contextPair: pair}"&gt;
       &lt;/ng-template&gt;
    &lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;
...
</code></pre>
</div>

In the file *matching-game.component.ts*, the variables of both template references (`leftpart_temp` and `rightpart_temp`) must be declared. The decorator `@ContentChild` indicates that this is a content projection, i.e. Angular now expects that the two template snippets with the respective selector (`leftpart` or `rightpart`) are provided in the parent component between the tags `<app-matching-game></app-matching-game>` of the host element (see `@ViewChild`).

<div class="break-out">

 <pre><code class="language-ts">@ContentChild('leftpart', {static: false}) leftpart_temp: TemplateRef&lt;any&gt;;
@ContentChild('rightpart', {static: false}) rightpart_temp: TemplateRef&lt;any&gt;;
</code></pre>
</div>

Don’t forget: The types `ContentChild` and `TemplateRef` must be imported from the core package.

In the parent component `game1`, the two required template snippets with the selectors `leftpart` and `rightpart` are now inserted.

For the sake of simplicity, I will reuse the buttons here again:

<pre><code class="language-ts">&lt;app-matching-game [pairs]="animals"&gt;
    &lt;ng-template #leftpart let-animalPair="contextPair"&gt;
          &lt;button&gt;{{animalPair.leftpart}}&lt;/button&gt;       
       &lt;/ng-template&gt;
    &lt;ng-template #rightpart let-animalPair="contextPair"&gt;
          &lt;button&gt;{{animalPair.rightpart}}&lt;/button&gt;
       &lt;/ng-template&gt;
&lt;/app-matching-game&gt;
</code></pre>

The attribute `let-animalPair="contextPair"` is used to specify that the context variable `contextPair` is used in the template snippet with the name `animalPair`.

The template snippets can now be changed to your own taste. To demonstrate this I use the component `game2`. The file *game2.component.ts* gets the same content as *game1.component.ts*. In *game2.component.html* I use an individually designed `div` element instead of a button. The CSS classes are stored in the file *game2.component.css*.

<div class="break-out">

 <pre><code class="language-ts">&lt;app-matching-game [pairs]="animals"&gt;
    &lt;ng-template #leftpart let-animalPair="contextPair"&gt;
          &lt;div class="myAnimal left"&gt;{{animalPair.leftpart}}&lt;/div&gt;        
       &lt;/ng-template&gt;
    &lt;ng-template #rightpart let-animalPair="contextPair"&gt;
          &lt;div class="myAnimal right"&gt;{{animalPair.rightpart}}&lt;/div&gt;
       &lt;/ng-template&gt;
&lt;/app-matching-game&gt;
</code></pre>
</div>

After adding the tags `<app-game2></app-game2>` on the homepage *app.component.html*, the second version of the game appears when I start the application:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c10a27ac-75a0-47ea-bf76-0cade86ad868/card-matching-game-angular-rxjs-figure3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c10a27ac-75a0-47ea-bf76-0cade86ad868/card-matching-game-angular-rxjs-figure3.png" sizes="100vw" caption="An alternative view of the game in the component <code>game2</code>" alt="An alternative view of the game in the component game2" >}}

The design possibilities are now almost unlimited. It would be possible, for example, to define a subclass of `Pair` that contains additional properties. For example, image addresses could be stored for the left and/or right parts. The images could be displayed in the template along with the text or instead of the text.

{{% ad-panel-leaderboard %}}

## 2. Control Of User Interaction With RxJS

### Advantages Of Reactive Programming With RxJS

To turn the application into an interactive game, the events (e.g. mouse click events) that are triggered at the user interface must be processed.  In reactive programming, continuous sequences of events, so-called "streams", are considered. A stream can be observed (it is an "observable"), i.e. there can be one or more "observers" or "subscribers" subscribing to the stream. They are notified (usually asynchronously) about every new value in the stream and can react to it in a certain way.

With this approach, a low level of coupling between the parts of an application can be achieved. The existing observers and observables are independent of each other and their coupling can be varied at runtime.

The JavaScript library RxJS provides a mature implementation of the Observer design pattern. Furthermore, RxJS contains numerous operators to convert streams (e.g. filter, map) or to combine them into new streams (e.g. merge, concat). The operators are "pure functions" in the sense of functional programming: They do not produce side effects and are independent of the state outside the function. A program logic composed only of calls to pure functions does not need global or local auxiliary variables to store intermediate states. This, in turn, promotes the creation of stateless and loosely coupled code blocks. It is therefore desirable to realize a large part of the event handling by a clever combination of stream operators. Examples of this are given in the section after next, based on our matching game.

### Integrating RxJS Into The Event Handling Of An Angular Component

The Angular framework works with the classes of the RxJS library. RxJS is therefore automatically installed when Angular is installed. 

The image below shows the main classes and functions that play a role in our considerations:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac04acf-910e-488b-a3f1-a165573c18f4/card-matching-game-angular-rxjs-image4.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac04acf-910e-488b-a3f1-a165573c18f4/card-matching-game-angular-rxjs-image4.jpg" sizes="100vw" caption="A model of the essential classes for event handling in Angular/RxJS" alt="A model of the essential classes for event handling in Angular/RxJS" >}}


<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Class Name</th>
      <th>Function</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Observable (RxJS)</td>
      <td>Base class that represents a stream; in other words, a continuous sequence of data. An observable can be subscribed to. The <code>pipe</code> function is used to apply one or more operator functions to the observable instance. </td>
    </tr>
    <tr>
      <td>Subject (RxJS)</td>
      <td>The subclass of observable provides the next function to publish new data in the stream.</td>
    </tr>
    <tr>
      <td>EventEmitter (Angular)</td>
      <td>This is an angular-specific subclass that is usually only used in conjunction with the <code>@Output</code> decorator to define a component output. Like the next function, the <code>emit</code> function is used to send data to the subscribers.</td>
    </tr>
    <tr>
      <td>Subscription (RxJS)</td>
      <td>The <code>subscribe</code> function of an observable returns a subscription instance. It is required to cancel the subscription after using the component.</td>
  </tbody>
</table>

With the help of these classes, we want to implement the user interaction in our game. The first step is to make sure that an element that is selected by the user on the left or right side is visually highlighted.

The visual representation of the elements is controlled by the two template snippets in the parent component. The decision how they are displayed in the selected state should therefore also be left to the parent component. It should receive appropriate signals as soon as a selection is made on the left or right side or as soon as a selection is to be undone.

For this purpose, I define four output values of type `EventEmitter` in the *matching-game.component.ts* file. The types `Output` and `EventEmitter` have to be imported from the core package.

<pre><code class="language-ts">@Output() leftpartSelected = new EventEmitter&lt;number&gt;();
@Output() rightpartSelected = new EventEmitter&lt;number&gt;();
@Output() leftpartUnselected = new EventEmitter();
@Output() rightpartUnselected = new EventEmitter();
</code></pre>

In the template *matching-game.component.html*, I react to the `mousedown` event on the left and right side, and then send the ID of the selected item to all receivers.

<div class="break-out">

 <pre><code class="language-html">&lt;div &#42;ngFor="let pair of unsolvedPairs" class="item" (mousedown)="leftpartSelected.emit(pair.id)"&gt;
...
&lt;div &#42;ngFor="let pair of unsolvedPairs | shuffle:test" class="item" (mousedown)="rightpartSelected.emit(pair.id)"&gt;
</code></pre>
</div>

In our case, the receivers are the components `game1` and `game2`. There you can now define the event handling for the events `leftpartSelected`, `rightpartSelected`, `leftpartUnselected` and `rightpartUnselected`. The variable `$event` represents the emitted output value, in our case the ID. In the following you can see the listing for *game1.component.html*, for *game2.component.html* the same changes apply.

<div class="break-out">

 <pre><code class="language-html">&lt;app-matching-game [pairs]="animals" (leftpartSelected)="onLeftpartSelected($event)" (rightpartSelected)="onRightpartSelected($event)" (leftpartUnselected)="onLeftpartUnselected()" (rightpartUnselected)="onRightpartUnselected()"&gt;

      &lt;ng-template #leftpart let-animalPair="contextPair"&gt;
           &lt;button [class.selected]="leftpartSelectedId==animalPair.id"&gt; 
           {{animalPair.leftpart}}
           &lt;/button&gt;       
      &lt;/ng-template&gt;    
    &lt;ng-template #rightpart let-animalPair="contextPair"&gt;
        &lt;button [class.selected]="rightpartSelectedId==animalPair.id"&gt; 
        {{animalPair.rightpart}}
        &lt;/button&gt; 
     &lt;/ng-template&gt;
&lt;/app-matching-game&gt;
</code></pre>
</div>

In *game1.component.ts* (and similarly in *game2.component.ts*), the `event` handler functions are now implemented. I store the IDs of the selected elements. In the HTML template (see above), these elements are assigned the class `selected`. The CSS file *game1.component.css* defines which visual changes this class will bring about (e.g. color or font changes). Resetting the selection (unselect) is based on the assumption that the pair objects always have positive IDs.

<pre><code class="language-css">onLeftpartSelected(id:number):void{
    this.leftpartSelectedId = id;
}
onRightpartSelected(id:number):void{
    this.rightpartSelectedId = id;
}
onLeftpartUnselected():void{
    this.leftpartSelectedId = -1;
}
onRightpartUnselected():void{
    this.rightpartSelectedId = -1;
}
</code></pre>


In the next step, event handling is required in the matching game component. It must be determined if an assignment is correct, that is, if the left selected element matches the right selected element. In this case, the assigned pair can be moved into the container for the resolved pairs.

I would like to formulate the evaluation logic using RxJS operators (see the next section). For preparation, I create a subject `assignmentStream` in *matching-game.component.ts*. It should emit the elements selected by the user on the left or right side. The goal is to use RxJS operators to modify and split the stream in such a way that I get two new streams: one stream `solvedStream` which provides the correctly assigned pairs and a second stream `failedStream` which provides the wrong assignments. I would like to subscribe to these two streams with `subscribe` in order to be able to perform appropriate event handling in each case.

I also need a reference to the created subscription objects, so that I can cancel the subscriptions with "unsubscribe" when leaving the game (see `ngOnDestroy`). The classes `Subject` and `Subscription` must be imported from the package "rxjs".

<pre><code class="language-javascript">private assignmentStream = new Subject<{pair:Pair, side:string}>();

private solvedStream = new Observable&lt;Pair&gt;();
private failedStream = new Observable&lt;string&gt;();

private s_Subscription: Subscription;
private f_Subscription: Subscription;

ngOnInit(){

  ...
  //TODO: apply stream-operators on 
  //assignmentStream
  this.s_Subscription = this.solvedStream.subscribe(pair =>   
  handleSolvedAssignment(pair));
  this.f_Subscription = this.failedStream.subscribe(() =>    
  handleFailedAssignment());
}

ngOnDestroy() {
   this.s_Subscription.unsubscribe();
   this.f_Subscription.unsubscribe();
}
</code></pre>

If the assignment is correct, the following steps are done:

- The assigned pair is moved to the container for the solved pairs. 
- The events `leftpartUnselected` and `rightpartUnselected` are sent to the parent component.

No pair is moved if the assignment is incorrect. If the wrong assignment was executed from left to right (`side1` has the value `left`), the selection should be undone for the element on the left side (see the GIF at the beginning of the article). If an assignment is made from right to left, the selection is undone for the element on the right side. This means that the last element that was clicked on remains in a selected state.

For both cases, I prepare the corresponding handler functions `handleSolvedAssignment` and `handleFailedAssignment` (remove function: see source code at the end of this article):

<pre><code class="language-javascript">private handleSolvedAssignment(pair: Pair):void{
   this.solvedPairs.push(pair);
   this.remove(this.unsolvedPairs, pair);    
   this.leftpartUnselected.emit();
   this.rightpartUnselected.emit();
   //workaround to force update of the shuffle pipe
   this.test = Math.random() * 10;
}
private handleFailedAssignment(side1: string):void{

   if(side1=="left"){        
        this.leftpartUnselected.emit();        
   }else{            
        this.rightpartUnselected.emit();
   }  

}
</code></pre>

Now we have to change the viewpoint from the consumer who subscribes to the data to the producer who generates the data. In the file *matching-game.component.html*, I make sure that when clicking on an element, the associated pair object is pushed into the stream `assignmentStream`. It makes sense to use a common stream for the left and right side because the order of the assignment is not important for us.

<div class="break-out">

 <pre><code class="language-html">&lt;div &#42;ngFor="let pair of unsolvedPairs" class="item" (mousedown)="leftpartSelected.emit(pair.id)"
(click)="assignmentStream.next({pair: pair, side: 'left'})"&gt;
...
&lt;div &#42;ngFor="let pair of unsolvedPairs | shuffle:test" class="item" (mousedown)="rightpartSelected.emit(pair.id)" 
(click)="assignmentStream.next({pair: pair, side: 'right'})"&gt;
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Design Of The Game Interaction With RxJS Operators

All that remains is to convert the stream `assignmentStream` into the streams `solvedStream` and `failedStream`. I apply the following operators in sequence:

### `pairwise`

There are always two pairs in an assignment. The `pairwise` operator picks the data in pairs from the stream. The current value and the previous value are combined into a pair. 

From the following stream...

<div class="break-out">

 <pre><code class="language-markup">„{pair1, left},  {pair3, right},  {pair2, left},  {pair2, right},  {pair1, left},  {pair1, right}“
</code></pre>
</div>

...results this new stream:

<div class="break-out">

 <pre><code class="language-markup">„({pair1, left}, {pair3, right}),   ({pair3, right}, {pair2, left}),   ({pair2, left}, {pair2, right}),   ({pair2, right}, {pair1, left}),   ({pair1, left}, {pair1, right})“
 </code></pre>
</div>

For example, we get the combination `({pair1, left}, {pair3, right})` when the user selects `dog` (id=1) on the left side and `insect` (id=3) on the right side (see array `ANIMALS` at the beginning of the article). These and the other combinations result from the game sequence shown in the GIF above.

### `filter`

You have to remove all combinations from the stream that were made on the same side of the playing field like `({pair1, left}, {pair1, left})` or `({pair1, left}, {pair4, left})`.

The filter condition for a combination `comb` is therefore `comb[0].side != comb[1].side`.

### `partition`

This operator takes a stream and a condition and creates two streams from this. The first stream contains the data that meets the condition and the second stream contains the remaining data. In our case, the streams should contain correct or incorrect assignments. So the condition for a combination `comb` is `comb[0].pair===comb[1].pair`.

The example results in a „correct” stream with

<div class="break-out">

 <pre><code class="language-markup">({pair2, left}, {pair2, right}),   ({pair1, left}, {pair1, right})
 </code></pre>
</div>

and a “wrong” stream with

<div class="break-out">

 <pre><code class="language-markup">({pair1, left}, {pair3, right}), ({pair3, right}, {pair2, left}),  ({pair2, right}, {pair1, left})
 </code></pre>
</div>

### `map`

Only the individual pair object is required for further processing of a correct assignment, such as `pair2`. The map operator can be used to express that the combination `comb` should be mapped to `comb[0].pair`. If the assignment is incorrect, the combination `comb` is mapped to the string `comb[0].side` because the selection should be reset on the side specified by `side`. 

The `pipe` function is used to concatenate the above operators. The operators `pairwise`, `filter`, `partition`, `map` must be imported from the package `rxjs/operators`.

<div class="break-out">

 <pre><code class="language-javascript">ngOnInit() {    
   ...  
   const stream = this.assignmentStream.pipe(
                   pairwise(),
                   filter(comb => comb[0].side != comb[1].side)                    
                  );
   //pipe notation leads to an error message (Angular 8.2.2, RxJS 6.4.0)      
   const [stream1, stream2] = partition(comb => 
                                        comb[0].pair === comb[1].pair)(stream);
   this.solvedStream = stream1.pipe( 
                         map(comb => comb[0].pair)
                       );
   this.failedStream = stream2.pipe(
                         map(comb => comb[0].side)
                       );
   this.s_Subscription = this.solvedStream.subscribe(pair => 
                             this.handleSolvedAssignment(pair));
   this.f_Subscription = this.failedStream.subscribe(side => 
                             this.handleFailedAssignment(side));
}
</code></pre>
</div>

Now the game already works!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38120a52-1daa-43a3-8694-261adc67d915/card-matching-game-angular-rxjs-game.gif" alt="Screen capture of the learningl game “matching pairs”" /><figcaption>Final result</figcaption></figure>

By using the operators, the game logic could be described declaratively. We only described the properties of our two target streams (combined into pairs, filtered, partitioned, remapped) and did not have to worry about the implementation of these operations. If we had implemented them ourselves, we would also have had to store intermediate states in the component (e.g. references to the last clicked items on the left and right side). Instead, the RxJS operators encapsulate the implementation logic and the required states for us and thus raise the programming to a higher level of abstraction.

## Conclusion

Using a simple learning game as an example, we tested the use of RxJS in an Angular component. The reactive approach is well suited to process events that occur on the user interface. With RxJS, the data needed for event handling can be conveniently arranged as streams. Numerous operators, such as `filter`, `map` or `partition` are available for transforming the streams. The resulting streams contain data that is prepared in its final form and can be subscribed to directly. It requires a little skill and experience to select the appropriate operators for the respective case and to link them efficiently. This article should provide an introduction to this.

### Further Resources

- “[The Introduction To Reactive Programming You’ve Been Missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754),” *written by André Staltz*

### <span class="rh">Related Reading</span> on SmashingMag:

<ul>
  <li><a title="Read 'Managing Image Breakpoints With Angular'" href="https://www.smashingmagazine.com/2019/02/image-breakpoints-angular/" rel="bookmark">Managing Image Breakpoints With Angular</a></li>
  <li><a title="Read 'Styling An Angular Application With Bootstrap'" href="https://www.smashingmagazine.com/2019/02/angular-application-bootstrap/" rel="bookmark">Styling An Angular Application With Bootstrap</a></li>
  <li><a title="Read 'How To Create And Deploy Angular Material Application'" href="https://www.smashingmagazine.com/2020/01/angular-8-material-application-netlify/" rel="bookmark">How To Create And Deploy Angular Material Application</a></li>
</ul>

{{< signature "ra, il" >}}
