---
title: 'Improve Your JavaScript Knowledge By Reading Source Code'
slug: javascript-knowledge-reading-source-code
author: carl-mungazi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3aab2fdd-f8bc-40a0-8045-13b1fbcc8a1d/js-knowledge-source-code-sharing-card.png
date: 2019-07-12T12:30:59+02:00
summary: >-
  When you are still early on in your programming career, digging into the source code of open source libraries and frameworks can be a daunting endeavor. In this article, Carl Mungazi shares how he got over his fear and began using source code to improve his knowledge and skills. He also uses Redux to demonstrate how he approaches breaking down a library.
description: >-
  When you are still early on in your programming career, digging into the source code of open source libraries and frameworks can be a daunting endeavor. In this article, Carl Mungazi shares how he got over his fear and began using source code to improve his knowledge and skills. He also uses Redux to demonstrate how he approaches breaking down a library.
categories:
  - Coding
  - JavaScript
  - Workflow
---
<p>Do you remember the first time you dug deep into the source code of a library or framework you use frequently? For me, that moment came during my first job as a frontend developer three years ago.</p>

<p>We had just finished rewriting an internal legacy framework we used to create e-learning courses. At the beginning of the rewrite, we had spent time investigating a number of different solutions including Mithril, Inferno, Angular, React, Aurelia, Vue, and Polymer. As I was very much a beginner (I had just switched from journalism to web development), I remember feeling intimidated by the complexity of each framework and not understanding how each one worked.</p>

<p>My understanding grew when I began investigating our chosen framework, Mithril, in greater depth. Since then, my knowledge of JavaScript &mdash; and programming in general &mdash; has been greatly helped by the hours I have spent digging deep into the guts of the libraries I use daily either at work or in my own projects. In this post, I will share some of the ways you can take your favorite library or framework and use it as an educational tool.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a94d53ac-c580-4a50-846d-74d997c484d9/2-improve-your-javascript-knowledge-by-reading-source-code.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a94d53ac-c580-4a50-846d-74d997c484d9/2-improve-your-javascript-knowledge-by-reading-source-code.png" sizes="100vw" caption="My first introduction to reading code was via Mithril’s hyperscript function. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a94d53ac-c580-4a50-846d-74d997c484d9/2-improve-your-javascript-knowledge-by-reading-source-code.png'>Large preview</a>)" alt="The source code for Mithril’s hyperscript function" >}}

{{% feature-panel %}}

## The Benefits Of Reading Source Code

<p>One of the major benefits of reading source code is the number of things you can learn. When I first looked into Mithril’s codebase, I had a vague idea of what the virtual DOM was. When I finished, I came away with the knowledge that the virtual DOM is a technique which involves creating a tree of objects that describe what your user interface should look like. That tree is then turned into DOM elements using DOM APIs such as <code>document.createElement</code>. Updates are performed by creating a new tree describing the future state of the user interface and then comparing it with objects from the old tree.</p>

<p>I had read about all of this in various articles and tutorials, and whilst it was helpful, being able to observe it at work in the context of an application we had shipped was very illuminating for me. It also taught me which questions to ask when comparing different frameworks. Instead of looking at GitHub stars, for example, I now knew to ask questions such as, “How does the way each framework performs updates affect performance and the user experience?”</p>

<p>Another benefit is an increase in your appreciation and understanding of good application architecture. Whilst most open-source projects generally follow the same structure with their repositories, each of them contains differences. Mithril’s structure is pretty flat and if you are familiar with its API, you can make educated guesses about the code in folders such as <code>render</code>, <code>router</code> and <code>request</code>. On the other hand, React’s structure reflects its new architecture. The maintainers have separated the module responsible for UI updates (<code>react-reconciler</code>) from the module responsible for rendering DOM elements (<code>react-dom</code>).</p>

<p>One of the benefits of this is that it is now easier for developers to write their own <a href="https://github.com/chentsulin/awesome-react-renderer">custom renderers</a> by hooking into the <code>react-reconciler</code> package. Parcel, a module bundler I have been studying recently, also has a <code>packages</code> folder like React. The key module is named <code>parcel-bundler</code> and it contains the code responsible for creating bundles, spinning up the hot module server and the command-line tool.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6777ea35-ee97-40c4-a0b8-5b4c2455f733/1-improve-your-javascript-knowledge-by-reading-source-code.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6777ea35-ee97-40c4-a0b8-5b4c2455f733/1-improve-your-javascript-knowledge-by-reading-source-code.png" sizes="100vw" caption="It will not be long before the source code you are reading leads you to the JavaScript specification. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6777ea35-ee97-40c4-a0b8-5b4c2455f733/1-improve-your-javascript-knowledge-by-reading-source-code.png'>Large preview</a>)" alt="The section of the JavaScript specification which explains how Object.prototype.toString works" >}}

<p>Yet another benefit &mdash; which came as a welcome surprise to me &mdash; is you become more comfortable reading the official JavaScript specification which defines how the language works. The first time I read the spec was when I was investigating the difference between <code>throw Error</code> and <code>throw new Error</code> (spoiler alert &mdash; there is <a href="https://www.ecma-international.org/ecma-262/7.0/#sec-error-constructor">none</a>). I looked into this because I noticed that Mithril used <code>throw Error</code> in the implementation of its <code>m</code> function and I wondered if there was a benefit to using it over <code>throw new Error</code>. Since then, I have also learnt that the logical operators <code>&&</code> and <code>||</code> <a href="https://tc39.es/ecma262/#prod-LogicalORExpression">do not necessarily return booleans</a>, found the <a href="https://www.ecma-international.org/ecma-262/#sec-abstract-equality-comparison">rules</a> which govern how the <code>==</code> equality operator coerces values and the <a href="https://www.ecma-international.org/ecma-262/#sec-object.prototype.tostring">reason</a> <code>Object.prototype.toString.call({})</code> returns <code>'[object Object]'</code>.</p>

{{% ad-panel-leaderboard %}}

## Techniques For Reading Source Code

<p>There are many ways of approaching source code. I have found the easiest way to start is by selecting a method from your chosen library and documenting what happens when you call it. Do not document every single step but try to identify its overall flow and structure.</p>

<p>I did this recently with <code>ReactDOM.render</code> and consequently learned a lot about React Fiber and some of the reasons behind its implementation. Thankfully, as React is a popular framework, I came across a lot of articles written by other developers on the same issue and this sped up the process.</p>

<p>This deep dive also introduced me to the concepts of <a href="https://developer.mozilla.org/en-US/docs/Web/API/Background_Tasks_API">co-operative scheduling</a>, the <code><a href="https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback">window.requestIdleCallback</a></code> method and a <a href="https://github.com/facebook/react/blob/v16.7.0/packages/react-reconciler/src/ReactUpdateQueue.js#L10">real world example of linked lists</a> (React handles updates by putting them in a queue which is a linked list of prioritised updates). When doing this, it is advisable to create a very basic application using the library. This makes it easier when debugging because you do not have to deal with the stack traces caused by other libraries.</p>

<p>If I am not doing an in-depth review, I will open up the <code>/node_modules</code> folder in a project I am working on or I will go to the GitHub repository. This usually happens when I come across a bug or interesting feature. When reading code on GitHub, make sure you are reading from the latest version. You can view the code from commits with the latest version tag by clicking the button used to change branches and select “tags”. Libraries and frameworks are forever undergoing changes so you do not want to learn about something which may be dropped in the next version.</p>

<p>Another less involved way of reading source code is what I like to call the ‘cursory glance’ method. Early on when I started reading code, I installed <em>express.js</em>, opened its <code>/node_modules</code> folder and went through its dependencies. If the <code>README</code> did not provide me with a satisfactory explanation, I read the source. Doing this led me to these interesting findings:</p>

<ul>
  <li>Express depends on two modules which both merge objects but do so in very different ways. <code>merge-descriptors</code> only adds properties directly found directly on the source object and it also merges non-enumerable properties whilst <code>utils-merge</code> only iterates over an object’s enumerable properties as well as those found in its prototype chain. <code>merge-descriptors</code> uses <code>Object.getOwnPropertyNames()</code> and <code>Object.getOwnPropertyDescriptor()</code> whilst <code>utils-merge</code> uses <code>for..in</code>;</li>
  <li>The <code>setprototypeof</code> module provides a cross platform way of setting the prototype of an instantiated object;</li>
  <li><code>escape-html</code> is a 78-line module for escaping a string of content so it can be interpolated in HTML content.</li>
 </ul>

<p>Whilst the findings are not likely to be useful immediately, having a general understanding of the dependencies used by your library or framework is useful.</p>

<p>When it comes to debugging front-end code, your browser’s debugging tools are your best friend. Among other things, they allow you to stop the program at any time and inspect its state, skip a function’s execution or step into or out of it. Sometimes this will not be immediately possible because the code has been minified. I tend to unminify it and copy the unminified code into the relevant file in the <code>/node_modules</code> folder.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/798703fd-8689-40d9-9159-701f1a00f837/3-improve-your-javascript-knowledge-by-reading-source-code.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/798703fd-8689-40d9-9159-701f1a00f837/3-improve-your-javascript-knowledge-by-reading-source-code.png" sizes="100vw" caption="Approach debugging as you would any other application. Form a hypothesis and then test it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/798703fd-8689-40d9-9159-701f1a00f837/3-improve-your-javascript-knowledge-by-reading-source-code.png'>Large preview</a>)" alt="The source code for the ReactDOM.render function" >}}

## Case Study: Redux’s Connect Function

<p>React-Redux is a library used to manage the state of React applications. When dealing with popular libraries such as these, I start by searching for articles that have been written about its implementation. In doing so for this case study, I came across this <a href="https://blog.isquaredsoftware.com/2018/11/react-redux-history-implementation">article</a>. This is another good thing about reading source code. The research phase usually leads you to informative articles such as this which only improve your own thinking and understanding.</p>

<p><code>connect</code> is a React-Redux function which connects React components to an application’s Redux store. How? Well, according to the <a href="https://react-redux.js.org/api/connect">docs</a>, it does the following:</p>

<blockquote>“...returns a new, connected component class that wraps the component you passed in.”</blockquote>

<p>After reading this, I would ask the following questions:</p>

<ul>
  <li>Do I know any patterns or concepts in which functions take an input and then return that same input wrapped with additional functionality?</li>
<li>If I know of any such patterns, how would I implement this based on the explanation given in the docs?</li>
  </ul>


<p>Usually, the next step would be to create a very basic example app which uses <code>connect</code>. However, on this occasion I opted to use the new React app we are building at <a href="https://limejump.com/">Limejump</a> because I wanted to understand <code>connect</code> within the context of an application which will eventually be going into a production environment.</p>

<p>The component I am focusing on looks like this:</p>

<div class="break-out">

<pre><code class="language-javascript">class MarketContainer extends Component {
 // code omitted for brevity
}

const mapDispatchToProps = dispatch => {
 return {
   updateSummary: (summary, start, today) => dispatch(updateSummary(summary, start, today))
 }
}

export default connect(null, mapDispatchToProps)(MarketContainer);
</code></pre>
</div>

<p>It is a container component which wraps four smaller connected components. One of the first things you come across in the <a href="https://github.com/reduxjs/react-redux/blob/v7.1.0/src/connect/connect.js">file</a> which exports <code>connect</code> method is this comment: <em>connect is a facade over connectAdvanced</em>. Without going far we have our first learning moment: <strong>an opportunity to observe the <a href="https://jargon.js.org/_glossary/FACADE_PATTERN.md">facade</a> design pattern in action</strong>. At the end of the file we see that <code>connect</code> exports an invocation of a function called <code>createConnect</code>. Its parameters are a bunch of default values which have been destructured like this:</p>

<div class="break-out">

<pre><code class="language-javascript">export function createConnect({
 connectHOC = connectAdvanced,
 mapStateToPropsFactories = defaultMapStateToPropsFactories,
 mapDispatchToPropsFactories = defaultMapDispatchToPropsFactories,
 mergePropsFactories = defaultMergePropsFactories,
 selectorFactory = defaultSelectorFactory
} = {})
</code></pre>
</div>

<p>Again, we come across another learning moment: <strong>exporting invoked functions</strong> and <strong>destructuring default function arguments</strong>. The destructuring part is a learning moment because had the code been written like this:</p>

<div class="break-out">

<pre><code class="language-javascript">export function createConnect({
 connectHOC = connectAdvanced,
 mapStateToPropsFactories = defaultMapStateToPropsFactories,
 mapDispatchToPropsFactories = defaultMapDispatchToPropsFactories,
 mergePropsFactories = defaultMergePropsFactories,
 selectorFactory = defaultSelectorFactory
})
</code></pre>
</div>

<p>It would have resulted in this error <code>Uncaught TypeError: Cannot destructure property 'connectHOC' of 'undefined' or 'null'.</code> This is because the function has no default argument to fall back on.</p>

<p><strong>Note</strong>: <em>For more on this, you can read David Walsh’s <a href="https://davidwalsh.name/destructuring-function-arguments">article</a>. Some learning moments may seem trivial, depending on your knowledge of the language, and so it might be better to focus on things you have not seen before or need to learn more about.</em></p>

<p><code>createConnect</code> itself does nothing in its function body. It returns a function called <code>connect</code>, the one I used here:</p>

<pre><code class="language-javascript">export default connect(null, mapDispatchToProps)(MarketContainer)
</code></pre>

<p>It takes four arguments, all optional, and the first three arguments each go through a <code><a href="https://github.com/reduxjs/react-redux/blob/v7.1.0/src/connect/connect.js#L25">match</a></code> function which helps define their behaviour according to whether the arguments are present and their value type. Now, because the second argument provided to <code>match</code> is one of three functions imported into <code>connect</code>, I have to decide which thread to follow.</p>

<p>There are learning moments with the <a href="https://github.com/reduxjs/react-redux/blob/v7.1.0/src/connect/wrapMapToProps.js#L29">proxy function</a> used to wrap the first argument to <code>connect</code> if those arguments are functions, the <code><a href="https://github.com/reduxjs/react-redux/blob/v7.1.0/src/utils/isPlainObject.js">isPlainObject</a></code> utility used to check for plain objects or the <code><a href="https://github.com/reduxjs/react-redux/blob/v7.1.0/src/utils/warning.js">warning</a></code> module which reveals how you can set your debugger to <a href="https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints#exceptions">break on all exceptions</a>. After the match functions, we come to <code>connectHOC</code>, the function which takes our React component and connects it to Redux. It is another function invocation which returns <code><a href="https://github.com/reduxjs/react-redux/blob/v7.1.0/src/components/connectAdvanced.js#L123">wrapWithConnect</a></code>, the function which actually handles connecting the component to the store.</p>

<p>Looking at <code>connectHOC</code>’s implementation, I can appreciate why it needs <code>connect</code> to hide its implementation details. It is the heart of React-Redux and contains logic which does not need to be exposed via <code>connect</code>. Even though I will end the deep dive here, had I continued, this would have been the perfect time to consult the reference material I found earlier as it contains an incredibly detailed explanation of the codebase.</p>

{{% ad-panel-leaderboard %}}

## Summary

<p>Reading source code is difficult at first but as with anything, it becomes easier with time. The goal is not to understand everything but to come away with a different perspective and new knowledge. The key is to be deliberate about the entire process and intensely curious about everything.</p>

<p>For example, I found the <code>isPlainObject</code> function interesting because it uses this <code>if (typeof obj !== 'object' || obj === null) return false</code> to make sure the given argument is a plain object. When I first read its implementation, I wondered why it did not use <code>Object.prototype.toString.call(opts) !== '[object Object]'</code>, which is less code and distinguishes between objects and object sub types such as the Date object. However, reading the next line revealed that in the extremely unlikely event that a developer using <code>connect</code> returns a Date object, for example, this will be handled by the <code>Object.getPrototypeOf(obj) === null</code> check.</p>

<p>Another bit of intrigue in <code>isPlainObject</code> is this code:</p>

<pre><code class="language-javascript">while (Object.getPrototypeOf(baseProto) !== null) {
 baseProto = Object.getPrototypeOf(baseProto)
}
</code></pre>

<p>Some Google searching led me to <a href="https://stackoverflow.com/questions/51722354/the-implementation-of-isplainobject-function-in-redux/51726564#51726564">this</a> StackOverflow thread and the Redux <a href="https://github.com/reduxjs/redux/pull/2599#issuecomment-342849867">issue</a> explaining how that code handles cases such as checking against objects which originate from an iFrame.</p>

### Useful Links On Reading Source Code

<ul>
  <li>“<a href="https://blog.angularindepth.com/level-up-your-reverse-engineering-skills-8f910ae10630">How To Reverse Engineer Frameworks</a>,” Max Koretskyi, Medium</li>
<li>“<a href="https://github.com/aredridel/how-to-read-code/blob/master/how-to-read-code.md">How To Read Code</a>,” Aria Stewart, GitHub</li>
</ul>

{{< signature "dm, yk, il" >}}
