---
title: 'Things I Wish I Had Known About Angular When I Started'
slug: angular-guide
author: william-juan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef27939e-040f-49bc-bd4e-1af6d80a84ac/angular-guide.jpg
date: 2022-09-22T13:00:00.000Z
summary: >-
  If you’re considering learning Angular, this article sums up what William Juan wished he knew when he started, including the mistakes made and lessons learned the hard way.
description: >-
  If you’re considering learning Angular, this article sums up what William Juan wished he knew when he started, including the mistakes made and lessons learned the hard way.
categories:
  - Angular
  - Guides
  - Tools
  - UI
---

I’ve been using Angular since version 2, and it has come a long way since those days to what it is right now. I’ve worked on various Angular projects over the years, yet I keep finding new things. It goes to say how massive the framework is. Here are some things I wish I had known about Angular when I started so you don’t have to learn it the hard way.

## Modularize Your Application

Angular has [detailed documentation](https://angular.io/guide/styleguide) outlining the recommended approach to structure your application. Angular also provides a [CLI](https://angular.io/cli) to help scaffold your application that adheres to their recommendations.

I’ve had my fair share of mistakes when it comes to structuring the application. As you follow tutorials, you’re guided through where you should put your files and which modules the components or services belong to. However, when you venture beyond the tutorial, you sometimes end up with a structure that doesn’t scale well. This could lead to issues down the road.

Below are some mistakes I’ve made that came back and bit me.

### Split Your Components Into Modules

The release of Standalone Components in Angular 14 makes `NgModules` no longer a requirement when creating components. You can choose not to use modules for your components, directives, and pipes. However, you could still follow the folder structure outlined below, omitting the module files.

Initially, I put all the components into the default module you get when creating a new Angular app. As the application grew, I ended up with a lot of components in the same module. They were separate components and didn’t have any need to be in the same module.

Split your components into separate modules, so you can import and load only the required modules. The common approach is to divide your application into the following modules:

- **Core module** for singleton services and components that are used once at the app level (example: navigation bar and footer).
- **[Feature modules](https://angular.io/guide/feature-modules)** for each feature &mdash; code related to the specific functionality of your application. For example, a simple e-commerce application could have a feature module for products, carts, and orders.
- **Shared module** for the module that is referenced across different parts of the application. These can include components, directives, and pipes.

Dividing the application into separate modules helps partition your application into smaller, more focused areas. It creates clear boundaries between the different types of modules and each feature module. This separation helps maintain and scale the application as different teams can work on separate parts with a lower risk of breaking another part of the application.

### Lazy Load Your Routes

This is a result of my first mistake of putting everything in a single module. Because all the components were in the same module, I couldn’t [lazy load the modules](https://angular.io/guide/lazy-loading-ngmodules). All the modules were imported at the root level, eventually affecting the initial load time. After separating your components into modules, lazy load your routes, so the modules only get loaded when you navigate to the route that requires them.

### Single Responsibility

This applies to all types of files in an Angular app. I’ve let my service and component files grow beyond their scope, which made them difficult to work with. The general rule is to keep each component/service/pipe/directive performing a specific set of tasks. If a component is trying to do more than what it was initially made for, it might be worth refactoring and splitting it into several smaller components. This will make testing and maintenance a lot easier.

## Use The Angular CLI

You’ve probably used the `ng serve` command either directly in your command line or through a script in your `package.json` file. This is one of Angular CLI’s commands. However, the CLI comes with more handy commands that can speed up your development especially when it comes to initializing and scaffolding.

Initially, I did most of these manually as I didn’t understand how to use the CLI except for starting and stopping the local server. I would create component files manually, add the boilerplate code, and add them to the right modules. This was okay for smaller projects but became a tedious task as the project grew. That’s when I learned how to use the CLI and use it to automate most of the manual work I do. For example, instead of creating all the boilerplate for a card component, the following command will create them for you:

<pre><code class="language-bash">ng g c card
</code></pre>

You can use the CLI by installing it globally via npm using the command below:

<pre><code class="language-bash">npm install -g @angular/cli
</code></pre>

To view the available commands, execute the code below:

<pre><code class="language-bash">ng help
</code></pre>

Most projects have custom configurations that are project-specific, and you have to do some modifications to the code generated by the CLI. Angular provides an elegant solution for these scenarios, such as [**schematics**](https://angular.io/guide/schematics). A schematic is a template-based code generator &mdash; a set of instructions to generate or modify code for your project. Similar to Angular CLI, your custom schematics are packaged and can be installed via `npm` in whichever project needs it.

{{% feature-panel %}} 

## Path Aliases And Barrel Exports

As I was learning Angular, I tried to keep my project neat by putting all the services into a `services` folder, models in a `models` folder, and so on. However, after some time, I end up with a growing list of `import` statements like this:

<pre><code class="language-javascript">import { UserService } from '../../services/user.service';
import { RolesService } from '../../services/roles.service';
</code></pre>

[Typescript path alias](https://fireship.io/snippets/improving-long-relative-paths-imports/) can help simplify your import statements. To setup path aliases, open your `tsconfig.json` and add the desired path name and its actual path:

<pre><code class="language-javascript">{
 "compilerOptions": {
 "paths": {
 "@services/&#42;": ["src/app/services/*"],
 }
 }
}
</code></pre>

Now the import statements above can be re-written as:

<pre><code class="language-javascript">import { UserService } from '@services/user.service';
import { RolesService } from '@services/roles.service';
</code></pre>

An added benefit of using path aliases is that it allows you to move your files around without having to update your `imports`. You’d have to update them if you were using relative paths.

This can be further simplified by using [barrel `exports`](https://github.com/basarat/typescript-book/blob/master/docs/tips/barrel.md). Barrels are a handy way to export multiple files from a single folder (think of it as a proxy for your files). Add an `index.ts` in the `services` folder with the following contents:

<pre><code class="language-javascript">export &#42; from './user.service';
export &#42; from './roles.service';
</code></pre>

Now, update the `tsconfig.json` to point to the `index.ts` file instead of the asterisk (`*`). 

<pre><code class="language-javascript">{
 "compilerOptions": {
 "paths": {
 "@services": ["src/app/services/index.ts"],
 }
 }
}
</code></pre>

The import statements can now be further simplified into:

<pre><code class="language-javascript">import { UserService, RolesService } from '@services';
</code></pre>

## Embrace Typescript’s Features

I started by learning JavaScript, so I wasn’t used to the type system and the other features that TypeScript offers. My exposure to TypeScript was through Angular, and it was overwhelming to learn both a new language (although it’s a superset of JavaScript, some differences trip me up every time) and a new framework. I often find TypeScript slowing me down instead of helping me with the development. I avoided using TypeScript features and overused the `any` type in my project.

However, as I got more acquainted with the framework, I began to understand the benefits of TypeScript when used correctly. TypeScript offers a lot of useful features that improve the overall developer experience and make the code you write cleaner. One of the benefits of using TypeScript that I’ve grown accustomed to is the IntelliSense or autocomplete it provides in your IDE. Their [type safety and static type checking](https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html#typescript-a-static-type-checker) have also helped catch potential bugs at compile time that could have snuck in.

The nice thing about TypeScript is its [flexible configuration](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html). You can toggle their settings easily via their `tsconfig.json` as per your project’s needs. You can change these settings again if you decide on a different setting. This allows you to set the rules as loose or strict as you’d like.

{{% ad-panel-leaderboard %}}

## Improve Performance By Using `trackBy`

Performance is crucial for applications, and Angular provides various ways to optimize your applications. This is often a problem that you won’t run into at the beginning as you are probably working with small data sets and a limited number of components. However, as your application grows and the number of components being rendered grows and becomes increasingly complex, you’ll start to notice some performance degradation. These performance degradations are usually in the form of slowness in the app: slow to respond, load, or render and stuttering in the UI.

Identifying the source of these problems is an adventure on its own. I’ve found that most of the performance issues I’ve run into in the applications are UI related (this doesn’t mean that other parts of the application don’t affect performance). This is especially prominent when rendering components in a loop and updating an already rendered component. This usually causes a flash in the component when the components are updated.

Under the hood, when a change occurs in these types of components, Angular needs to remove all the DOM elements associated with the data and re-create them with the updated data. That is a lot of DOM manipulations that are expensive.

A solution I’ve found to fix this issue is to use the [`trackBy`](https://angular.io/api/core/TrackByFunction) function whenever you’re rendering components using the `ngFor` directive (especially when you’re frequently updating the rendered components). 

The `ngFor` directive needs to uniquely identify items in the iterable to correctly perform DOM updates when items in the iterable are reordered, new items are added, or existing items are removed. For these scenarios, it is desirable only to update the elements affected by the change to make the updates more efficient. The `trackBy` function lets you pass in a unique identifier to identify each component generated in the loop, allowing Angular to update only the elements affected by the change.

Let’s look at an example of a regular `ngFor` that creates a new `div` for each entry in the `users` array.

<pre><code class="language-javascript">@Component({
 selector: 'my-app',
 template: `
 &lt;div &#42;ngFor="let user of users"&gt;
 {{ user.name }}
 &lt;/div&gt;
 `,
})

export class App {
 users = [
 {id: 1, name: 'Will'},
 {id: 2, name: 'Mike'},
 {id: 3, name: 'John'},
 ]
}
</code></pre>

Keeping most of the code the same, we can help Angular keep track of the items in the template by adding the `trackBy` function and assigning it to a function that returns the unique identifier for each entry in the array (in our case, the user’s `id`).

<pre><code class="language-javascript">@Component({
 selector: 'my-app',
 template: `
 &lt;div &#42;ngFor="let user of users; trackBy: trackByFn"&gt;
 {{ user.name }}
 &lt;/div&gt;
 `,
})

export class App {
 users = [
 {id: 1, name: 'Will'},
 {id: 2, name: 'Mike'},
 {id: 3, name: 'John'},
 ]
 trackByFn(index, item) {
 return item.id;
 }
}
</code></pre>

## Use Pipes For Data Transformations

Data transformations are inevitable as you render data in your templates. My initial approach to this was to:

- Bind the template to a function that accepts the data as the input:

<pre><code class="language-javascript">interface User {
 firstName: string,
 middleName: string,
 lastName: string
}
@Component({
 selector: 'my-app',
 template: `
 &lt;h1&gt;{{ formatDisplayName(user) }}&lt;/h1&gt;
 `,
})

export class App {
 user: User = {
 firstName: 'Nick',
 middleName: 'Piberius',
 lastName: 'Wilde'
 }
 formatDisplayName(user: User): string {
 return `${user.firstName} ${user.middleName.substring(0,1)}. ${user.lastName}`; 
 }
}
</code></pre>

- Create a new variable, assign the formatted data to the variable, and bind the new variable in the template:

<pre><code class="language-javascript">interface User {
 firstName: string,
 middleName: string,
 lastName: string
}
@Component({
 selector: 'my-app',
 template: `
 &lt;h1&gt;{{ displayName }}&lt;/h1&gt;
 `,
})

export class App {
 user: User = {
 firstName: 'Nick',
 middleName: 'Piberius',
 lastName: 'Wilde'
 }
 displayName = `${this.user.firstName} ${this.user.middleName.substring(0,1)}. ${this.user.lastName}`; 
}
</code></pre>

Neither approach was clean nor performant and wasn’t what Angular recommends to perform data transformations. For these scenarios, angular recommends using [**pipes**](https://angular.io/guide/pipes). Pipes are functions specifically designed to be used in templates.

Angular provides built-in pipes for common data transformations such as internationalization, date, currency, decimals, percentage, and upper and lower case strings. In addition, Angular also lets you create custom pipes that can be reused throughout your application.

The data transformation above can be re-written using a pipe as follows:

<pre><code class="language-javascript">@Pipe({name: 'displayName'})
export class DisplayNamePipe implements PipeTransform {
 transform(user: User): string {
 return `${user.firstName} ${user.middleName.substring(0,1)}. ${user.lastName}`; 
 }
}
</code></pre>

The pipe can then be used in the template by using the pipe (`|`) character followed by the pipe name.

<pre><code class="language-javascript">@Component({
 selector: 'my-app',
 template: `
 &lt;h1&gt;{{ user | displayName }}&lt;/h1&gt;
 `,
})

export class App {
 user: User = {
 firstName: 'Nick',
 middleName: 'Piberius',
 lastName: 'Wilde'
 }
}
</code></pre>

{{% ad-panel-leaderboard %}}

## Improve Performance With `OnPush` Change Detection

Angular applications are made up of a tree of components that rely on their change detectors to keep the view and their corresponding models in sync. When Angular detects a change in the model, it immediately updates the view by walking down the tree of change detectors to determine if any of them have changed. If the change detector detects the change, it will re-render the component and update the DOM with the latest changes.

There are two [change detection](https://angular.io/guide/change-detection) strategies provided by Angular:

- **Default**  
The change detection cycle runs on every event that occurs inside the component.
- **OnPush**  
The change detection cycle only runs when a component’s event handler is triggered, an async pipe is used in the template, a new value is emitted, and when any of the component’s input reference changes.

In addition to the reduced number of change detection cycles and its performance boost, the restrictions imposed by using the `OnPush` change detection strategy also make you architect your app better by pushing you to create more modular components that utilize one of the three recommended ways mentioned above to update the DOM. 

## RxJS Is Your Friend

[RxJS](https://rxjs.dev/) is a JavaScript library that uses observables for [reactive programming](https://www.techtarget.com/searchapparchitecture/definition/reactive-programming). While RxJS isn’t exclusively used in Angular, it plays a big role in the Angular ecosystem. Angular’s core features, such as `Routing`, `HttpClient`, and `FormControl`, leverage observables by default. 

RxJS is a part of Angular that has been largely unexplored for me as I was learning the framework. I’ve avoided using it unless I had to. It was a new concept, and I found it quite hard to wrap my head around it. I’ve worked with JavaScript Promises, but observables and streams are a new paradigm for me.

After working for a while with Angular, I eventually took the time to learn and understand RxJS and try to use them in my projects. It wasn’t long before I realized the numerous benefits of RxJS that I’ve been missing out on all this time. RxJS, with its large collection of chainable operators, excels in handling async tasks.

I’ve been using RxJS with Angular for a few years now, and my experience has been nothing less than positive. The [set of operators](https://rxjs.dev/guide/operators) RxJS offers is really handy. They seem to have an operator (or a chain of operators) for every use case. Commonly used operators include:

- `map`: passes each source value through a transformation function to get corresponding output values.
- `tap`: modify the outside state when the observable emits a new value without altering the stream.
- `switchMap`: maps each value to an Observable, then flattens all of these inner Observables.
- `filter`: emits a value from the source if it passes a criterion function.
- `combineLatestWith`: create an observable that combines the latest values from all passed observables and the source into an array and emits them.

## Learn How To Spot And Prevent Memory Leaks

[Memory leaks](https://www.geeksforgeeks.org/what-is-memory-leak-how-can-we-avoid/) are one of the worst types of issues you run into &mdash; hard to find, debug, and often hard to solve. This might not be a concern initially, but it becomes crucial when your application reaches a certain size. Common symptoms of memory leaks are degrading performance the longer the app is being used or the same events being fired multiple times. Two of the most common source of memory leaks I’ve run into are:

### 1. Subscriptions That Are Not Cleaned Up

Unlike the [`async`](https://angular.io/api/common/AsyncPipe) pipe, listening to an observable using the `subscribe` method won’t get cleaned up automatically. You will have to manually clean up the subscriptions by calling `unsubscribe` on the subscription or using the `takeUntil` operator.

The example below shows a memory leak introduced by listening to the route params observable. Every new instance of `MyComponent` creates a new subscription which will continue to run even after the component is destroyed.

<pre><code class="language-javascript">export class MyComponent {
 constructor(private route: ActivatedRoute){
 this.route.params.subscribe((params) =&gt; {
 // Do something
 });
 }
}
</code></pre>

As mentioned above, you can fix the memory leak by either calling `unsubscribe` or using the `takeUntil` operator.

- Fixing the memory leak using the `unsubscribe` method:

<pre><code class="language-javascript">export class MyComponent {
 private routeSubscription;
 constructor(private route: ActivatedRoute){
 this.routeSubscription = this.route.params.subscribe((params) =&gt; {
 // Do something
 });
 
 }
 ngOnDestroy() {
 this.routeSubscription.unsubcribe();
 }
}
</code></pre>

- Fixing the memory leak using the `takeUntil` operator:

<pre><code class="language-javascript">export class MyComponent {
 private componentDestroyed$ = new Subject&lt;boolean&gt;();
 constructor(private route: ActivatedRoute){
 this.route.params.pipe(
 takeUntil(this.componentDestroyed$)
 ).subscribe((params) =&gt; {
 // Do something
 });
 
 }
 ngOnDestroy() {
 this.componentDestroyed$.next(true);
 this.componentDestroyed$.complete();
 }
}
</code></pre>

### 2. Event Listeners That Are Not Cleaned Up

Another common source of memory leaks is event listeners that aren’t unregistered when no longer used. For example, the `scroll` event listener in the code below gets instantiated on every new instance of `MyComponent` and continuously runs even after the component is destroyed unless you unregister it. 

<pre><code class="language-javascript">export class MyComponent {
 constructor(private renderer: Renderer2) {}
 ngOnInit() {
 this.renderer.listen(document.body, 'scroll', () =&gt; {
 // Do something
 });
 }
}
</code></pre>

To fix this and stop listening to the event after the component is destroyed, assign it to a variable and unregister the listener on the `ngOnDestroy` lifecycle method.

<pre><code class="language-javascript">export class MyComponent {
 private listener;
 constructor(private renderer: Renderer2) {}
 ngOnInit() {
 this.listener = this.renderer.listen(
 document.body,
 ‘scroll’,
 () =&gt; {
 // Do something
 });
 
 }
 ngOnDestroy() {
 this.listener();
 }
}
</code></pre>

## Consider Using A State Management Library (If Applicable)

[State management](https://blog.nrwl.io/managing-state-in-angular-applications-22b75ef5625f) is another part of the stack that you don’t usually think about until you need it. Most small and simple applications don’t need any external state management library. However, as the project grows and managing your application’s state gets more complicated, it might be time to re-think if the project could benefit from implementing more robust state management.

There is no correct solution for state management as every project’s requirements are different. Luckily, there are a few state management libraries for Angular that offer different features. These are a few of the commonly used state management libraries in the Angular ecosystem:

- [NgRx](https://ngrx.io/)
- [NGXS](https://www.ngxs.io/)
- [Akita](https://opensource.salesforce.com/akita/)

## Wrapping Up

If you’ve just started to learn Angular and it hasn’t quite clicked yet, be patient! It will eventually start to make sense, and you’ll see what the framework has to offer. I hope my personal experience can help you accelerate your learning and avoid the mistakes I’ve made.

{{< signature "yk, il" >}}
