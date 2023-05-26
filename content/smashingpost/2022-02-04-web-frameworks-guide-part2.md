---
title: 'What Web Frameworks Solve: The Vanilla Alternative (Part 2)'
slug: web-frameworks-guide-part2
author: noam-rosenthal
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3745837-4c65-4b2b-81ab-42e0088633d2/web-frameworks-guide-part2.jpg
date: 2022-02-04T13:30:00.000Z
summary: >-
  In this second part, Noam suggests a few patterns of how to use the web platform directly as an alternative to some of the solutions that are offered by frameworks.
description: >-
  In this second part, Noam suggests a few patterns of how to use the web platform directly as an alternative to some of the solutions that are offered by frameworks.
categories:
  - React
  - Frameworks
  - JavaScript
---

[Last week](https://www.smashingmagazine.com/2022/01/web-frameworks-guide-part1/), we looked at the different benefits and costs of using frameworks, starting from the point of view of which core problems they’re trying to solve, focusing on declarative programming, data-binding, reactivity, lists and conditionals. Today, we’ll see whether an alternative can emerge from the web platform itself.

## Roll Your Own Framework?

An outcome that might seem inevitable from exploring life without one of the frameworks, is to roll your own framework for reactive data-binding. Having tried this before, and seeing how costly it can be, I decided to work with a guideline in this exploration; not to roll my own framework, but instead to see if I can use the web platform directly in a way that makes frameworks less necessary. If you consider rolling your own framework, be aware that there is a set of costs not discussed in this article.

## Vanilla Choices

The web platform already provides a declarative programming mechanism out of the box: HTML and CSS. This mechanism is mature, well tested, popular, widely used, and documented. However, it does not provide clear built-in concepts of data-binding, conditional rendering, and list synchronization, and reactivity is a subtle detail spread across multiple platform features.

When I skim through the documentation of popular frameworks, I find the features [described in Part 1](https://www.smashingmagazine.com/2022/01/web-frameworks-guide-part1/) straight away. When I read the web platform documentation (for example, on [MDN](https://developer.mozilla.org/)), I find many confusing patterns of how to do things, without a conclusive representation of data-binding, list synchronization, or reactivity. I will try to draw some guidelines of how to approach these problems on the web platform, without requiring a framework (in other words, by going vanilla).

### Reactivity With Stable DOM Tree and Cascading

Let’s go back to the error label example. In ReactJS and SolidJS, we create declarative code that translates to imperative code that adds the label to the DOM or removes it. In Svelte, that code is generated.

But what if we didn’t have that code at all, and instead we used CSS to hide and show the error label?

<pre><code class="language-javascript">&lt;style&gt;
    label.error { display: none; }
    .app.has-error label.error {display: block; }
&lt;/style&gt;
&lt;label class="error"&gt;Message&lt;/label&gt;

&lt;script&gt;
   app.classList.toggle('has-error', true);
&lt;/script&gt;
</code></pre>

The reactivity, in this case, is handled in the browser &mdash; the app’s change of class propagates to its descendants until the internal mechanism in the browser decides whether to render the label.

This technique has several advantages:

- The bundle size is zero.
- There are zero build steps.
- Change propagation is optimized and well tested, in native browser code, and avoids unnecessary expensive DOM operations like `append` and `remove`.
- The selectors are stable. In this case, you can count on the label element being there. You can apply animations to it without relying on complicated constructs such as “transition groups”. You can hold a reference to it in JavaScript.
- If the label is shown or hidden, you can see the reason in the style panel of the developer tools, which shows you the entire cascade, the chain of rules that ended up in the label being visible (or hidden).

Even if you read this and choose to keep working with frameworks, the idea of keeping the DOM stable and changing state with CSS is powerful. Consider where this could be useful to you.

{{% ad-panel-leaderboard %}}

### Form-Oriented “Data-Binding”

Before the era of JavaScript-heavy single-page applications (SPAs), forms were the major way to create web applications that include user input. Traditionally, the user would fill in the form and click a “Submit” button, and the server-side code would handle the response. Forms were the multi-page application version of data-binding and interactivity. No wonder that HTML elements with the basic names of `input` and `output` are form elements.

Because of their wide use and long history, the form APIs accumulated several hidden nuggets that make them useful for problems that are not traditionally thought of as being solved by forms.

#### Forms and Form Elements as Stable Selectors

Forms are accessible by name (using [`document.forms`](https://developer.mozilla.org/en-US/docs/Web/API/Document/forms)), and each form element is accessible by its name (using [`form.elements`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/elements)). In addition, the form associated with an element is accessible (using the [`form` attribute](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement)). This includes not only input elements, but also other form elements such as [`output`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/output), [`textarea`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), and [`fieldset`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset), which allows for nested access of elements in a tree.

In the error label example from the previous section, we showed how to reactively show and hide the error message. This is how we update the error message text in React (and similarly in SolidJS):

<pre><code class="language-javascript">const [errorMessage, setErrorMessage] = useState(null);
return &lt;label className="error"&gt;{errorMessage}&lt;/label&gt;
</code></pre>

When we have a stable DOM and stable tree forms and form elements, we can do the following:

<pre><code class="language-javascript">&lt;form name="contactForm"&gt;
  &lt;fieldset name="email"&gt;
     &lt;output name="error"&gt;&lt;/output&gt;
  &lt;/fieldset&gt;
&lt;/form&gt;

&lt;script&gt;
  function setErrorMessage(message) {
  document.forms.contactForm.elements.email.elements.error.value = message;
  }
&lt;/script&gt;
</code></pre>

This looks quite verbose in its raw form, but it’s also very stable, direct, and extremely performant.

#### Forms for Input

Usually, when we build a SPA, we have some kind of JSON-like API that we work with to update our server, or whatever model we use.

This would be a familiar example (written in Typescript for readability):

<pre><code class="language-javascript">interface Contact {
  id: string;
  name: string;
  email: string;
  subscriber: boolean;
}

function updateContact(contact: Contact) { … }
</code></pre>

It’s common in framework code to generate this `Contact` object by selecting input elements and constructing the object piece by piece. With proper use of forms, there is a concise alternative:

<pre><code class="language-javascript">&lt;form name="contactForm"&gt;
  &lt;input name="id" type="hidden" value="136" /&gt;
  &lt;input name="email" type="email"/&gt;
  &lt;input name="name" type="string" /&gt;
  &lt;input name="subscriber" type="checkbox" /&gt;
&lt;/form&gt;

&lt;script&gt;
   updateContact(Object.fromEntries(
       new FormData(document.forms.contactForm));
&lt;/script&gt;
</code></pre>

By using hidden inputs and the useful [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) class, we can seamlessly transform values between DOM input and JavaScript functions.

#### Combining Forms and Reactivity

By combining the high-performance selector stability of forms and CSS reactivity, we can achieve more complex UI logic:

<pre><code class="language-javascript">&lt;form name="contactForm"&gt;
  &lt;input name="showErrors" type="checkbox" hidden /&gt;
  &lt;fieldset name="names"&gt;
     &lt;input name="name" /&gt;
     &lt;output name="error"&gt;&lt;/output&gt;
  &lt;/fieldset&gt;
  &lt;fieldset name="emails"&gt;
     &lt;input name="email" /&gt;
     &lt;output name="error"&gt;&lt;/output&gt;
  &lt;/fieldset&gt;
&lt;/form&gt;

&lt;script&gt;
  function setErrorMessage(section, message) {
  document.forms.contactForm.elements[section].elements.error.value = message;
  }
  function setShowErrors(show) {
  document.forms.contactForm.elements.showErrors.checked = show;
  }
&lt;/script&gt;

&lt;style&gt;
   input[name="showErrors"]:not(:checked) ~ * output[name="error"] {
      display: none;
   }
&lt;/style&gt;
</code></pre>

Note in this example that there is no use of classes &mdash; we develop the behavior of the DOM and style from the data of the forms, rather than by manually changing element classes.

I am not fond of overusing CSS classes as JavaScript selectors. I think they should be used to group together similarly styled elements, not as a catch-all mechanism to change component styles.

#### Advantages of Forms

- As with cascading, forms are built into the web platform, and most of their features are stable. That means much less JavaScript, many fewer framework version mismatches, and no “build”.
- Forms are accessible by default. If your app uses forms properly, there is much less need for ARIA attributes, “accessibility plugins”, and last-minute audits. Forms lend themselves to keyboard navigation, screen readers, and other assistive technologies.
- Forms come with built-in input-validation features: validation by regex pattern, reactivity to invalid and valid forms in CSS, handling of required versus optional, and more. You don’t need something to look like a form in order to enjoy these features.
- The `submit` event of forms is extremely useful. For example, it allows an “Enter” key to be caught even when there is no submit button, and it allows multiple submit buttons to be differentiated by the `submitter` attribute (as we’ll see in the TODO example later).
- Elements are associated with their containing form by default but can be associated with any other form in the document using the `form` attribute. This allows us to play around with form association without creating a dependency on the DOM tree.
- Using the stable selectors helps with UI test automation: We can use the nested API as a stable way to hook into the DOM regardless of its layout and hierarchy. The `form > (fieldsets) > element` hierarchy can serve as the interactive skeleton of your document.

### ChaCha and HTML Template

Frameworks provide their own way of expressing observable lists. Many developers today also rely on non-framework libraries that provide this kind of feature, such as MobX.

The main problem with general-purpose observable lists is that they are general purpose. This adds convenience with the cost of performance, and it also requires special developer tools to debug the complicated actions that those libraries do in the background.

Using those libraries and understanding what they do are OK, and they can be useful regardless of the choice of UI framework, but using the alternative might not be more complicated, and it might prevent some of the pitfalls that happen when you try to roll your own model.

### Channel of Changes (or ChaCha)

The ChaCha &mdash; otherwise also known as *Changes Channel* &mdash; is a bidirectional stream whose purpose is to notify changes in the **intent** direction and the **observe** direction.

- In the **intent** direction, the UI notifies the model of changes intended by the user.
- In the **observe** direction, the model notifies the UI of changes that were made to the model and that need to be displayed to the user.

It’s perhaps a funny name, but it’s not a complicated or novel pattern. Bidirectional streams are used everywhere on the web and in software (for example, [`MessagePort`](https://developer.mozilla.org/en-US/docs/Web/API/MessagePort)). In this case, we are creating a bidirectional stream that has a particular purpose: to report actual model changes to the UI and intentions to the model.

The interface of ChaCha can usually be derived from the specification of the app, without any UI code.

For example, an app that allows you to add and remove contacts and that loads the initial list from a server (with an option to refresh) could have a ChaCha that looks like this:

<pre><code class="language-javascript">interface Contact {
  id: string;
  name: string;
  email: string;
}
// "Observe" Direction
interface ContactListModelObserver {
  onAdd(contact: Contact);
  onRemove(contact: Contact);
  onUpdate(contact: Contact);
}
// "Intent" Direction
interface ContactListModel {
  add(contact: Contact);
  remove(contact: Contact);
  reloadFromServer();  
}
</code></pre>

Note that all of the functions in the two interfaces are void and only receive plain objects. This is intentional. ChaCha is built like a channel with two ports to send messages, which allows it to work in an `EventSource`, an HTML `MessageChannel`, a service worker, or any other protocol.

The nice thing about ChaChas is that they’re easy to test: You send actions and expect specific calls to the observer in return.

### The HTML Template Element for List Items

HTML templates are special elements that are present in the DOM but don’t get displayed. Their purpose is to generate dynamic elements.

When we use a `template` element, we can avoid all of the boilerplate code of creating elements and populating them in JavaScript.

The following will add a name to a list using a `template`:

<pre><code class="language-javascript">&lt;ul id="names"&gt;
  &lt;template&gt;
   &lt;li&gt;&lt;label class="name" /&gt;&lt;/li&gt;
  &lt;/template&gt;
&lt;/ul&gt;
&lt;script&gt;
  function addName(name) {
    const list = document.querySelector('#names');
    const item = list.querySelector('template').content.cloneNode(true).firstElementChild;
    item.querySelector('label').innerText = name;
    list.appendChild(item);
  }
&lt;/script&gt;
</code></pre>

By using the `template` element for list items, we can see the list item in our original HTML &mdash; it’s not “rendered” using JSX or some other language. Your HTML file now contains _all_ of the HTML of the app &mdash; the static parts are part of the rendered DOM, and the dynamic parts are expressed in templates, ready to be cloned and appended to the document when the time comes.

{{% ad-panel-leaderboard %}}

## Putting It All Together: TodoMVC

[TodoMVC](https://todomvc.com/) is an app specification of a TODO list that has been used to showcase the different frameworks. The TodoMVC template comes with ready-made HTML and CSS to help you focus on the framework.

You can play with [the result](https://noamr.github.io/todomvc-app-template/index.html) in the GitHub repository, and the [full source code](https://github.com/noamr/todomvc-app-template) is available.

### Start With a Specification-Derived ChaCha

We’ll start with the [specification](https://github.com/tastejs/todomvc/blob/master/app-spec.md) and use it to build the ChaCha interface:

<pre><code class="language-javascript">interface Task {
   title: string;
   completed: boolean;
}

interface TaskModelObserver {
   onAdd(key: number, value: Task);
   onUpdate(key: number, value: Task);
   onRemove(key: number);
   onCountChange(count: {active: number, completed: number});
}

interface TaskModel {
   constructor(observer: TaskModelObserver);
   createTask(task: Task): void;
   updateTask(key: number, task: Task): void;
   deleteTask(key: number): void;
   clearCompleted(): void;
   markAll(completed: boolean): void;
}
</code></pre>

The functions in the task model are derived directly from the specification and what the user can do (clear completed tasks, mark all as completed or active, get the active and completed counts).

Note that it follows the guidelines of ChaCha:

- There are two interfaces, one acting and one observing.
- All of the parameter types are primitives or plain objects (being easily translated to JSON).
- All of the functions return void.

The implementation of TodoMVC [uses `localStorage` as the back end](https://github.com/noamr/todomvc-app-template/blob/main/js/model.js).

The model is very simple and not very relevant to the discussion about the UI framework. It saves to `localStorage` when needed and fires change callbacks to the observer when something changes, either as a result of user action or when the model is loaded from `localStorage` for the first time.

### Lean, Form-Oriented HTML

Next, I’ll take the TodoMVC template and modify it to be form-oriented &mdash; a hierarchy of forms, with input and output elements representing data that can be changed with JavaScript.

How do I know whether something needs to be a form element? As a rule of thumb, if it binds to data from the model, then it should be a form element.

The [full HTML file](https://github.com/noamr/todomvc-app-template/blob/main/index.html) is available, but here is its main part:

<pre><code class="language-javascript">&lt;section class="todoapp"&gt;
   &lt;header class="header"&gt;
       &lt;h1&gt;todos&lt;/h1&gt;
       &lt;form name="newTask"&gt;
           &lt;input name="title" type="text" placeholder="What needs to be done?" autofocus&gt;
       &lt;/form&gt;
   &lt;/header&gt;

   &lt;main&gt;
       &lt;form id="main"&gt;&lt;/form&gt;
       &lt;input type="hidden" name="filter" form="main" /&gt;
       &lt;input type="hidden" name="completedCount" form="main" /&gt;
       &lt;input type="hidden" name="totalCount" form="main" /&gt;
       &lt;input name="toggleAll" type="checkbox" form="main" /&gt;

       &lt;ul class="todo-list"&gt;
           &lt;template&gt;
               &lt;form class="task"&gt;
                   &lt;li&gt;
                       &lt;input name="completed" type="checkbox" checked&gt;
                       &lt;input name="title" readonly /&gt;
                       &lt;input type="submit" hidden name="save" /&gt;
                       &lt;button name="destroy"&gt;X&lt;/button&gt;
                   &lt;/li&gt;
               &lt;/form&gt;
           &lt;/template&gt;
       &lt;/ul&gt;
   &lt;/main&gt;

   &lt;footer&gt;
       &lt;output form="main" name="activeCount"&gt;0&lt;/output&gt;
       &lt;nav&gt;
           &lt;a name="/" href="#/"&gt;All&lt;/a&gt;
           &lt;a name="/active" href="#/active"&gt;Active&lt;/a&gt;
           &lt;a name="/completed" href="#/completed"&gt;Completed&lt;/a&gt;
       &lt;/nav&gt;
       &lt;input form="main" type="button" name="clearCompleted" value="Clear completed" /&gt;
   &lt;/footer&gt;
&lt;/section&gt;
</code></pre>

This HTML includes the following:

- We have a `main` form, with all of the global inputs and buttons, and a new form for creating a new task. Note that we associate the elements to the form using the [`form` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-form), to avoid nesting the elements in the form.
- The `template` element represents a list item, and its root element is another form that represents the interactive data related to a particular task. This form would be repeated by cloning the template’s contents when tasks are added.
- Hidden inputs represent data that is not directly shown but that is used for styling and selecting.

Note how this DOM is concise. It does not have classes sprinkled across its elements. It includes all of the elements needed for the app, arranged in a sensible hierarchy. Thanks to the hidden input elements, you can already get a good sense of what might change in the document later on.

This HTML does not know how it’s going to be styled or exactly what data it’s bound to. Let the CSS and JavaScript work for your HTML, rather than your HTML work for a particular styling mechanism. This would make it much easier to change designs as you go along.

### Minimal Controller JavaScript

Now that we have most of the reactivity in CSS, and we have list-handling in the model, what’s left is the controller code &mdash; the duct tape that holds everything together. In this small application, the controller JavaScript is [around 40 lines](https://github.com/noamr/todomvc-app-template/blob/main/js/app.js).

Here is a version, with an explanation for each part:

<pre><code class="language-javascript">import TaskListModel from './model.js';

const model = new TaskListModel(new class {
</code></pre>

Above, we create a new model.

<pre><code class="language-javascript">onAdd(key, value) {
   const newItem = document.querySelector('.todo-list template').content.cloneNode(true).firstElementChild;
   newItem.name = `task-${key}`;
   const save = () => model.updateTask(key,  Object.fromEntries(new FormData(newItem)));
   newItem.elements.completed.addEventListener('change', save);
   newItem.addEventListener('submit', save);
   newItem.elements.title.addEventListener('dblclick', ({target}) => target.removeAttribute('readonly'));
   newItem.elements.title.addEventListener('blur', ({target}) => target.setAttribute('readonly', ''));
   newItem.elements.destroy.addEventListener('click', () => model.deleteTask(key));
   this.onUpdate(key, value, newItem);
   document.querySelector('.todo-list').appendChild(newItem);
}
</code></pre>

When an item is added to the model, we create its corresponding list item in the UI.

Above, we clone the contents of the item `template`, assign the event listeners for a particular item, and add the new item to the list.

Note that this function, along with `onUpdate`, `onRemove`, and `onCountChange`, are callbacks that are going to be called from the [model](https://github.com/noamr/todomvc-app-template/blob/main/js/model.js).

<pre><code class="language-javascript">onUpdate(key, {title, completed}, form = document.forms[`task-${key}`]) {
   form.elements.completed.checked = !!completed;
   form.elements.title.value = title;
   form.elements.title.blur();
}
</code></pre>

When an item is updated, we set its `completed` and `title` values, and then `blur` (to exit editing mode).

<pre><code class="language-javascript">onRemove(key) { document.forms[`task-${key}`].remove(); }
</code></pre>

When an item is removed from the model, we remove its corresponding list item from the view.

<pre><code class="language-javascript">onCountChange({active, completed}) {
   document.forms.main.elements.completedCount.value = completed;
   document.forms.main.elements.toggleAll.checked = active === 0;
   document.forms.main.elements.totalCount.value = active + completed;
   document.forms.main.elements.activeCount.innerHTML = `&lt;strong&gt;${active}&lt;/strong&gt; item${active === 1 ? '' : 's'} left`;
}
</code></pre>

In the code above, when the number of completed or active items changes, we set the proper inputs to trigger the CSS reactions, and we format the output that displays the count.

<pre><code class="language-javascript">const updateFilter = () => filter.value = location.hash.substr(2);
window.addEventListener('hashchange', updateFilter);
window.addEventListener('load', updateFilter);
</code></pre>

And we update the filter from the `hash` fragment (and at startup). All we’re doing above is setting the value of a form element &mdash; CSS handles the rest.

<pre><code class="language-javascript">document.querySelector('.todoapp').addEventListener('submit', e => e.preventDefault(), {capture: true});
</code></pre>

Here, we ensure that we don’t reload the page when a form is submitted. This is the line that turns this app into a SPA.

<pre><code class="language-javascript">document.forms.newTask.addEventListener('submit', ({target: {elements: {title}}}) =&gt;   
    model.createTask({title: title.value}));
document.forms.main.elements.toggleAll.addEventListener('change', ({target: {checked}})=&gt;
    model.markAll(checked));
document.forms.main.elements.clearCompleted.addEventListener('click', () =&gt;
    model.clearCompleted());
</code></pre>

And this handles the main actions (creating, marking all, clearing completed).

### Reactivity With CSS

The [full CSS file](https://github.com/noamr/todomvc-app-template/blob/main/css/app.css) is available for you to view.

CSS handles a lot of the requirements of the specification (with some amendments to favor accessibility). Let’s look at some examples.

According to the specification, the “X” (`destroy`) button is shown only on hover. I’ve also added an accessibility bit to make it visible when the task is focused:

<pre><code class="language-javascript">.task:not(:hover, :focus-within) button[name="destroy"] { opacity: 0 }
</code></pre>

The `filter` link gets a red-ish border when it’s the current one:

<pre><code class="language-javascript">.todoapp input[name="filter"][value=""] ~ footer a[href$="#/"],
nav a:target {
   border-color: #CE4646;
}
</code></pre>

Note that we can use the `href` of the link element as a partial attribute selector &mdash; no need for JavaScript that checks the current filter and sets a `selected` class on the proper element.

We also use the `:target` selector, which frees us from having to worry about whether to add filters.

The view and edit style of the `title` input changes based on its read-only mode:

<pre><code class="language-javascript">.task input[name="title"]:read-only {
…
}

.task input[name="title"]:not(:read-only) {
…
}
</code></pre>

Filtering (i.e. showing only active and completed tasks) is done with a selector:

<pre><code class="language-javascript">input[name="filter"][value="active"] ~ * .task
      :is(input[name="completed"]:checked, input[name="completed"]:checked ~ *),
input[name="filter"][value="completed"] ~ * .task
     :is(input[name="completed"]:not(:checked), input[name="completed"]:not(:checked) ~ *) {
   display: none;
}
</code></pre>

The code above might seem a bit verbose, and it is probably easier to read with a CSS preprocessor such as Sass. But what it does is straightforward: If the filter is `active` and the `completed` checkbox is checked, or vice versa, then we hide the checkbox and its siblings.

I chose to implement this simple filter in CSS to show how far this can go, but if it starts to get hairy, then it would totally make sense to move it into the model instead.

## Conclusion and Takeaways

I believe that frameworks provide convenient ways to achieve complicated tasks, and they have benefits beyond technical ones, such as aligning a group of developers to a particular style and pattern. The web platform offers many choices, and adopting a framework gets everyone at least partially on the same page for some of those choices. There’s value in that. Also, there is something to be said for the elegance of declarative programming, and the big feature of componentization is not something I’ve tackled in this article.

But remember that alternative patterns exist, often with less cost and not always needing less developer experience. Allow yourself to be curious with those patterns, even if you decide to pick and choose from them while using a framework.

### Pattern Recap

- Keep the DOM tree stable. It starts a chain reaction of making things easy.
- Rely on CSS for reactivity instead of JavaScript, when you can.
- Use form elements as the main way to represent interactive data.
- Use the HTML `template` element instead of JavaScript-generated templates.
- Use a bidirectional stream of changes as the interface to your model.

*Special thanks to the following individuals for technical reviews: Yehonatan Daniv, Tom Bigelajzen, Benjamin Greenbaum, Nick Ribal, Louis Lazaris*

{{< signature "vf, il, al" >}}
