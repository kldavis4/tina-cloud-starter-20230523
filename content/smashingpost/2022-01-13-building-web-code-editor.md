---
title: 'Building A Web Code Editor'
slug: building-web-code-editor
author: daniel-don
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7db33e0-a76e-4f4f-959f-be0f8898784f/building-web-code-editor.jpg
date: 2022-01-13T11:30:00.000Z
summary: >-
  If you’re a developer who’s thinking about building a platform that requires a code editor in one form or another, then this article is for you. This article explains how to create a web code editor that displays the result in real time with the help of some HTML, CSS and JavaScript.
description: >-
  If you’re a developer who’s thinking about building a platform that requires a code editor in one form or another, then this article is for you. This article explains how to create a web code editor that displays the result in real time with the help of some HTML, CSS and JavaScript.
categories:
  - React
  - Tools
  - JavaScript
  - Workflow
  - Techniques
---

An online web code editor is most useful when you do not have the opportunity to use a code editor application, or when you want to quickly try out something on the web with your computer or even your mobile phone. This is also an interesting project to work on because having the knowledge of how to build a code editor will give you ideas on how to approach other projects that require you to integrate a code editor to show some functionality.

Here are a few React concepts you’ll need to know in order to follow along in this article:

- Hooks,
- Component structure,
- Functional components,
- Props.

## Using CodeMirror

We will be using a library named [CodeMirror](https://codemirror.net/index.html) to build our editor. CodeMirror is a versatile text editor implemented in JavaScript for the browser. It is especially for editing code and comes with a number of [language modes](https://codemirror.net/mode/index.html) and [add-ons](https://codemirror.net/doc/manual.html#addons) for more advanced editing functionality.

A rich [programming API](https://codemirror.net/doc/manual.html#api) and a CSS [theming](https://codemirror.net/doc/manual.html#styling) system are available for customizing CodeMirror to fit your application and extending it with new functionality. It gives us the functionality to create a rich code editor that runs on the web and shows us the result of our code in real time.

In the next section, we will set up our new React project and install the libraries we need to build our web app.

## Creating A New React Project

Let’s start by creating a new React project. In your commandline interface, navigate to the directory in which you want to create your project, and let’s create a React application and name it `code_editor`:

<pre><code class="language-bash">npx create-react-app code_editor</code></pre>

Having created our new React application, let’s navigate to that project’s directory in the commandline interface:

<pre><code class="language-bash">cd code_editor</code></pre>

There are two libraries we need to install here: `codemirror` and `react-codemirror2`.

<pre><code class="language-bash">npm install codemirror react-codemirror2</code></pre>

Having installed the libraries we need for this project, let’s create our tabs and enable tab switching between the three tabs that will appear in our editor (for HTML, CSS, and JavaScript).

{{% feature-panel %}}

### Button Component

Instead of creating individual buttons, let’s make the button a component that is reusable. In our project, the button would have three instances, according to the three tabs we need.

Create a folder named `components` in the `src` folder. In this new `components` folder, create a JSX file named `Button.jsx`.

Here is all of the code needed in the `Button` component:

<pre><code class="language-javascript">import React from 'react'
const Button = ({title, onClick}) =&gt; {
  return (
    &lt;div&gt;
      &lt;button
        style={{
          maxWidth: "140px",
          minWidth: "80px",
          height: "30px",
          marginRight: "5px"
        }}
        onClick={onClick}
      &gt;
        {title}
      &lt;/button&gt;
    &lt;/div&gt;
  )
}
export default Button
</code></pre>

Here is a full explanation of what we did above:

- We created a functional component named `Button`, which we then exported.
- We destructured `title` and `onClick` from the props coming into the component. Here, `title` would be a string of text, and `onClick` would be a function that gets called when a button is clicked.
- Next, we used the `button` element to declare our button, and used the `style` attributes to style our button to look presentable.
- We added the `onClick` attribute and passed our destructured `onClick` function props to it.
- The last thing you’ll notice we did in this component is pass in `{title}` as the content of the `button` tag. This allows us to display the title dynamically, based on what prop is being passed to the instance of the button component when it is called.

Now that we have created a reusable button component, let’s move on and bring our component into `App.js.` Go to `App.js` and import the newly created button component:

<pre><code class="language-javascript">import Button from './components/Button';</code></pre>

To track which tab or editor is open, we need a declare state to hold the value of the editor that is open. Using the `useState` React hook, we’ll set up the state that will store the name of the editor tab that is currently open when that tab’s button is clicked.

Here is how we do that:

<pre><code class="language-javascript">import React, { useState } from 'react';
import './App.css';
import Button from './components/Button';

function App() {
  const [openedEditor, setOpenedEditor] = useState('html');
  return (
    &lt;div className="App"&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>

Here, we declared our state. It takes the name of the editor that is currently open. Because the value `html` is passed as the state’s default value, the HTML editor would be the tab open by default.

Let’s move on and write the function that will use `setOpenedEditor` to change the value of the state when a tab button is clicked.

**Note:** Two tabs may not be open at the same time, so we’ll have to consider that when writing our function.

Here is what our function, named `onTabClick`, looks like:

<pre><code class="language-javascript">import React, { useState } from 'react';
import './App.css';
import Button from './components/Button';

function App() {
  ...

  const onTabClick = (editorName) =&gt; {
    setOpenedEditor(editorName);
  };

  return (
    &lt;div className="App"&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>

Here, we passed a single function argument, which is the name of the tab currently selected. This argument would be supplied anywhere the function is called, and the relevant name of that tab would be passed in.

Let’s create three instances of our `Button` for the three tabs we need:

<pre><code class="language-javascript">&lt;div className="App"&gt;
      &lt;p&gt;Welcome to the editor!&lt;/p&gt;
      &lt;div className="tab-button-container"&gt;
        &lt;Button title="HTML" onClick={() =&gt; {
          onTabClick('html')
        }} /&gt;
        &lt;Button title="CSS" onClick={() =&gt; {
          onTabClick('css')
        }} /&gt;
        &lt;Button title="JavaScript" onClick={() =&gt; {
          onTabClick('js')
        }} /&gt;
      &lt;/div&gt;
    &lt;/div&gt;</code></pre>

Here is what we did:

- We started by adding a `p` tag, basically just to give some context to what our application is about.
- We used a `div` tag to wrap our tab buttons. The `div` tag carries a `className` that we will use to style the buttons into a grid display in the CSS file later in this tutorial.
- Next, we declared three instances of the `Button` component. If you recall, the `Button` component takes two props, `title` and `onClick`. In every instance of the `Button` component, these two props are provided.
- The `title` prop takes the title of the tab.
- The `onClick` prop takes a function, `onTabClick`, which we just created and which takes a single argument: the name of the tab selected.

Based on the tab currently selected, we would use the JavaScript ternary operator to display the tab conditionally. This means that if the value of the `openedEditor` state is set to `html` (i.e. `setOpenedEditor('html')`), then the tab for the HTML section would become the currently visible tab. You’ll understand this better as we do it below:

<pre><code class="language-javascript">...
return (
    &lt;div className="App"&gt;
      ...
      &lt;div className="editor-container"&gt;
        {
          openedEditor === 'html' ? (
            &lt;p&gt;The html editor is open&lt;/p&gt;
          ) : openedEditor === 'css' ? (
            &lt;p&gt;The CSS editor is open!!!!!!&lt;/p&gt;
          ) : (
            &lt;p&gt;the JavaScript editor is open&lt;/p&gt;
          )
        }
      &lt;/div&gt;
    &lt;/div&gt;
  );
...</code></pre>

Let’s go over the code above in plain English. If the value of `openedEditor` is `html`, then display the HTML section. Otherwise, if the value of `openedEditor` is `css`, then display the CSS section. Otherwise, if the value is neither `html` nor `css`, then that means the value must be `js`, because we have only three possible values for the `openedEditor` state; so, then we’d display the tab for JavaScript.

We used paragraph tags (`p`) for the different sections in the ternary operator conditions. As we proceed, we will create the editor components and replace the `p` tags with the editor components themselves.

We have come so far already! When a button is clicked, it fires up the action that sets the tab it represents to `true`, making that tab visible. Here’s what our app currently looks like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42818ddc-ef56-4abf-864c-fe38d77eeeb0/2-building-web-code-editor.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54e7e73f-fbbb-4c2a-af2f-d611801222c1/2-building-web-code-editor-800w.gif" width="800" height="360" alt="A GIF showing the tab toggle we currently have." /></a><figcaption>A GIF showing the tab toggle we currently have. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42818ddc-ef56-4abf-864c-fe38d77eeeb0/2-building-web-code-editor.gif">Large preview</a>)</figcaption></figure>

Let’s add a little CSS to the `div` container holding the buttons. We want the buttons to be displayed in a grid, instead of stacked vertically like in the image above. Go to your `App.css` file and add the following code:

<pre><code class="language-css">.tab-button-container{
  display: flex;
}</code></pre>

Recall that we added `className="tab-button-container"` as an attribute in the `div` tag holding the three-tab buttons. Here, we styled that container, using CSS to set its display to `flex`. This is the result:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14bd1cc6-1d43-493b-9940-9850cf50f2f6/4-building-web-code-editor.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49c4a7b6-656a-4e6c-a895-78da9fb7f69c/4-building-web-code-editor-800w.gif" width="800" height="347" alt="We use CSS to set its display to flex" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14bd1cc6-1d43-493b-9940-9850cf50f2f6/4-building-web-code-editor.gif">Large preview</a>)</figcaption></figure>

Be proud of how much you’ve done to get to this point. In the next section, we will create our editors, replacing the `p` tags with them.

{{% ad-panel-leaderboard %}}

## Creating the Editors

Because we have already installed the libraries we are going to be working on within our CodeMirror editor, let’s go ahead and create our `Editor.jsx` file in the `components` folder.

### components > Editor.jsx

Having created our new file, let’s write some initial code in it:

<div class="break-out">

<pre><code class="language-javascript">import React, { useState } from 'react';
import 'codemirror/lib/codemirror.css';
import { Controlled as ControlledEditorComponent } from 'react-codemirror2';


const Editor = ({ language, value, setEditorState }) =&gt; {
  return (
    &lt;div className="editor-container"&gt;
    &lt;/div&gt;
  )
}
export default Editor
</code></pre>
</div>  

Here's what we did:

- We imported React alongside the `useState` hook because we are going to need it.
- We imported the CodeMirror CSS file (which comes from the CodeMirror library that we installed, so you don’t have to install it in any special way).
- We imported `Controlled` from `react-codemirror2`, renaming it to `ControlledEditorComponent` to make it clearer. We will be using this shortly.
- Then, we declared our `Editor` functional component, and we have a return statement with an empty `div`, with a `className` in the return statement for now.

In our functional component, we destructured some values from the props, including `language`, `value`, and `setEditorState`. These three props would be supplied in any instance of the editor when it is called in `App.js`.

Let’s use `ControlledEditorComponent` to write the code for our editor. Here’s what we’ll do:

<div class="break-out">

<pre><code class="language-javascript">import React, { useState } from 'react';
import 'codemirror/lib/codemirror.css';
import 'codemirror/mode/xml/xml';
import 'codemirror/mode/javascript/javascript';
import 'codemirror/mode/css/css';
import { Controlled as ControlledEditorComponent } from 'react-codemirror2';


const Editor = ({ language, value, setEditorState }) =&gt; {
  return (
    &lt;div className="editor-container"&gt;
      &lt;ControlledEditorComponent
        onBeforeChange={handleChange}
        value= {value}
        className="code-mirror-wrapper"
        options={{
          lineWrapping: true,
          lint: true,
          mode: language,
          lineNumbers: true,
        }}
      /&gt;
    &lt;/div&gt;
  )
}
export default Editor</code></pre>
</div>

Let’s walk through what we did here, explaining some CodeMirror terms.

The CodeMirror modes specify which language an editor is meant for. We imported three modes because we have three editors for this project:

1. **XML:** This mode is for HTML. It uses the term XML.
2. **JavaScript:** This (`codemirror/mode/javascript/javascript`) brings in JavaScript mode.
3. **CSS:** This (`codemirror/mode/css/css`) brings in CSS mode.

**Note:** Because the editor is built as a component that is reusable, we cannot put a direct mode in the editor. So, we supply the mode through the `language` prop that we destructured. But this doesn’t change the fact that the modes need to be imported in order to work.

Next, let’s discuss the things in `ControlledEditorComponent`:

- `onBeforeChange`  
This is called anytime you write to or remove from the editor. Think of this like the `onChange` handler you would normally have in an input field to track changes. Using this, we will be able to get the value of our editor anytime there's a new change and save it to our editor’s state. We will write the `{handleChange}` function as we proceed.
- `value = {value}`  
This is just the content of the editor at any given time. We passed a destructured prop named `value` to this attribute. The `value` props is the state holding the value of that editor. This would be supplied from the editor’s instance.
- *`className`*`="code-mirror-wrapper"`  
This class name is not a style we make ourselves. It is supplied from CodeMirror’s CSS file, which we imported above.
- `options`  
This is an object that takes the different functionality we want our editor to have. There are many amazing options in CodeMirror. Let’s look at the ones we used here:
    - `lineWrapping: true`  
This means that code should wrap to the next line when the line is full.
    - `lint: true`  
This allows linting.
    - `mode: language`  
This mode, as discussed above, takes the language that the editor is going to be used for. The language has already been imported above, but the editor is going to apply a language based on the `language` value supplied to the editor via the prop.
    - `lineNumbers: true`  
This specifies that the editor should have line numbers for each line.

Next, we can write the `handleChange` function for the `onBeforeChange` handler:

<pre><code class="language-javascript">const handleChange = (editor, data, value) =&gt; {
    setEditorState(value);
}</code></pre>

The `onBeforeChange` handler gives us access to three things: `editor, data, value`.

We only need the `value` because it is what we want to pass in our `setEditorState` prop. The `setEditorState` prop represents the set value for each state that we declared in `App.js`, holding the value for each editor. As we move on, we will look at how to pass this as a prop to the `Editor` component.

Next, we’ll add a dropdown that allows us to select different themes for the editor. So, let’s look at themes in CodeMirror.

### CodeMirror Themes

CodeMirror has multiple themes we can select from. Visit the [official website](https://codemirror.net/demo/theme.html) to see demos of the different themes available. Let’s make a dropdown with different themes that the user can choose from in our editor. For this tutorial, we’ll be adding five themes, but you can add as many as you like.

First, let’s import our themes in the `Editor.js` component:

<pre><code class="language-javascript">import 'codemirror/theme/dracula.css';
import 'codemirror/theme/material.css';
import 'codemirror/theme/mdn-like.css';
import 'codemirror/theme/the-matrix.css';
import 'codemirror/theme/night.css';</code></pre>

Next, create an array of all of the themes we have imported:

<div class="break-out">

<pre><code class="language-javascript">const themeArray = ['dracula', 'material', 'mdn-like', 'the-matrix', 'night']</code></pre>
</div>

Let’s declare a `useState` hook to hold the value of the selected theme, and set the default theme as `dracula`:

<pre><code class="language-javascript">const [theme, setTheme] = useState("dracula")</code></pre>

Let’s create the dropdown:

<pre><code class="language-javascript">...
return (
    &lt;div className="editor-container"&gt;

      &lt;div style={{marginBottom: "10px"}}&gt;
        &lt;label for="cars"&gt;Choose a theme: &lt;/label&gt;
        &lt;select name="theme" onChange={(el) =&gt; {
          setTheme(el.target.value)
        }}&gt;
          {
            themeArray.map( theme =&gt; (
              &lt;option value={theme}&gt;{theme}&lt;/option&gt;
            ))
          }
        &lt;/select&gt;
      &lt;/div&gt;
    // the rest of the code comes below...
    &lt;/div&gt;
  )
...</code></pre>

In the code above, we used the `label` HTML tag to add a label to our dropdown, and then added the `select` HTML tag to create our dropdown. The `option` tag in the `select` element defines the options available in the dropdown.

Because we needed to fill the dropdown with the theme names in the `themeArray` that we created, we used the `.map` array method to map `themeArray` and display the names individually using the `option` tag.

Hold on &mdash; we’re not done explaining the code above. In the opening `select` tag, we passed the `onChange` attribute to track and update the `theme` state whenever a new value is selected in the dropdown. Whenever a new option is selected in the dropdown, the value is gotten from the object returned to us. Next, we use the `setTheme` from our state hook to set the new value to be the value that the state holds.

At this point, we have created our dropdown, set up our theme’s state, and written our function to set the state with the new value. The final thing we need to do to make CodeMirror use our theme is pass the theme to the `options` object in `ControlledEditorComponent`. In the `options` object, let’s add a value named `theme`, and set its value to the state’s value for the selected theme, also named `theme`.

Here’s what `ControlledEditorComponent` would look like now:

<pre><code class="language-javascript">&lt;ControlledEditorComponent
  onBeforeChange={handleChange}
  value= {value}
  className="code-mirror-wrapper"
  options={{
    lineWrapping: true,
    lint: true,
    mode: language,
    lineNumbers: true,
    theme: theme,
  }}
/&gt;</code></pre>

Now, we have made a dropdown of different themes that can be selected from in the editor.

Here’s what the full code in `Editor.js` looks like at the moment:

<div class="break-out">

<pre><code class="language-javascript">import React, { useState } from 'react';
import 'codemirror/lib/codemirror.css';
import 'codemirror/theme/dracula.css';
import 'codemirror/theme/material.css';
import 'codemirror/theme/mdn-like.css';
import 'codemirror/theme/the-matrix.css';
import 'codemirror/theme/night.css';
import 'codemirror/mode/xml/xml';
import 'codemirror/mode/javascript/javascript';
import 'codemirror/mode/css/css';
import { Controlled as ControlledEditorComponent } from 'react-codemirror2';


const Editor = ({ language, value, setEditorState }) =&gt; {
  const [theme, setTheme] = useState("dracula")
  const handleChange = (editor, data, value) =&gt; {
    setEditorState(value);
  }
  const themeArray = ['dracula', 'material', 'mdn-like', 'the-matrix', 'night']
  return (
    &lt;div className="editor-container"&gt;
      &lt;div style={{marginBottom: "10px"}}&gt;
        &lt;label for="themes"&gt;Choose a theme: &lt;/label&gt;
        &lt;select name="theme" onChange={(el) =&gt; {
          setTheme(el.target.value)
        }}&gt;
          {
            themeArray.map( theme =&gt; (
              &lt;option value={theme}&gt;{theme}&lt;/option&gt;
            ))
          }
        &lt;/select&gt;
      &lt;/div&gt;
      &lt;ControlledEditorComponent
        onBeforeChange={handleChange}
        value= {value}
        className="code-mirror-wrapper"
        options={{
          lineWrapping: true,
          lint: true,
          mode: language,
          lineNumbers: true,
          theme: theme,
        }}
      /&gt;
    &lt;/div&gt;
  )
}
export default Editor
</code></pre>
</div>

There’s only one `className` that we need to style. Go to `App.css` and add the following style:

<pre><code class="language-css">.editor-container{
  padding-top: 0.4%;
}</code></pre>

Now that our editors are ready, let’s go back to `App.js` and use them there.

### src > App.js

The first thing we need to do is import the `Editor.js` component in here:

<pre><code class="language-javascript">import Editor from './components/Editor';</code></pre>

In `App.js`, let’s declare the states that will hold the contents of the HTML, CSS, and JavaScript editors, respectively.

<pre><code class="language-javascript">const [html, setHtml] = useState('');
const [css, setCss] = useState('');
const [js, setJs] = useState('');</code></pre>

If you recall, we will need to use these states to hold and supply the contents of our editors.

Next, let’s replace the paragraph (`p`) tags that we used for the HTML, CSS, and JavaScript in the conditional renderings with the editor components we have just created, and we’ll also pass in the appropriate prop to each instance of the editor component:

<pre><code class="language-javascript">function App() {
  ...
  return (
    &lt;div className="App"&gt;
      &lt;p&gt;Welcome to the edior&lt;/p&gt;

      // This is where the tab buttons container is...

      &lt;div className="editor-container"&gt;
        {
          htmlEditorIsOpen ? (
            &lt;Editor
              language="xml"
              value={html}
              setEditorState={setHtml}
            /&gt;
          ) : cssEditorIsOpen ? (
            &lt;Editor
              language="css"
              value={css}
              setEditorState={setCss}
            /&gt;
          ) : (
            &lt;Editor
              language="javascript"
              value={js}
              setEditorState={setJs}
            /&gt;
          )
        }
      &lt;/div&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>

If you’ve been following along until now, you’ll understand what we did in the code block above.

Here it is in plain English: We replaced the `p` tags (which were there as placeholders) with instances of the editor components. Then, we supplied their `language`, `value`, and `setEditorState` props, respectively, to match their corresponding states.

We've come so far! Here is what our app looks like now:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0fe07c7-bcca-4cb6-a66c-18cc12545854/5-building-web-code-editor.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbbaa0f0-fcd3-404d-baf1-ae0a28bba9f2/5-building-web-code-editor-800w.gif" width="800" height="377" alt="The way our app looks like now" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0fe07c7-bcca-4cb6-a66c-18cc12545854/5-building-web-code-editor.gif">Large preview</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

## Introduction to Iframes

We’ll be making use of inline frames (iframes) to display the result of the code entered in the editor.

According to [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe):

> The HTML Inline Frame element (`<iframe>`) represents a nested [browsing context](https://developer.mozilla.org/en-US/docs/Glossary/browsing_context), embedding another HTML page into the current one.

### How Iframes Work in React

Iframes are normally used with plain HTML. Using Iframes with React doesn’t require many changes, the major one being to convert attribute names to camelcase. An example of this is that `srcdoc` would become `srcDoc`.

### The Future of Iframes on the Web

Iframes continue to be really useful in web development. Something you might want to check out is Portals. As [Daniel Brain explains](https://medium.com/@bluepnume/google-chromes-portals-like-iframes-but-better-and-worse-29e0bbb3f78e):

<blockquote>“Portals introduce a powerful new set of capabilities into this mix. Now it’s possible to build something that feels like an iframe, that can seamlessly animate and morph and take over the full browser window.”</blockquote>

One of the things Portals tries to solve is the URL bar problem. When using iframe, components rendered in the iframe don’t carry a unique URL in the address bar; as such, this might not be great for the user experience, depending on the use case. Portals is worth checking out, and I’d suggest you do that, but because it is not the focus of our article, this is all I’ll say about it here.

## Creating the Iframe to House Our Result

Let’s move ahead with our tutorial by creating an iframe to house the result of our editors.

<pre><code class="language-javascript">return (
    &lt;div className="App"&gt;
      // ...
      &lt;div&gt;
        &lt;iframe
          srcDoc={srcDoc}
          title="output"
          sandbox="allow-scripts"
          frameBorder="1"
          width="100%"
          height="100%"
        /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );</code></pre>

Here, we created the iframe and housed it in a `div` container tag. In the iframe, we passed some attributes that we need:

- `srcDoc`   
The `srcDoc` attribute is written in camelcase because this is how to write iframe attributes in React. When using an iframe, we can either embed an external web page on the page or render specified HTML content. To load and embed an external page, we would use the `src` property instead. In our case, we are not loading an external page; rather, we want to create a new internal HTML document that houses our result; for this, we need the `srcDoc` attribute. This attribute takes the HTML document that we want to embed (we have not created that yet, but we will soon).
- `title`  
The title attribute is used to describe the contents of the inline frame.
- `sandbox`  
This property has [many purposes](https://www.w3schools.com/tags/att_iframe_sandbox.asp#:~:text=The%20sandbox%20attribute%20enables%20an,block%20form%20submission). In our case, we are using it to allow scripts to run in our iframe with the `allow-scripts` value. Because we are working with a JavaScript editor, this would come in handy quickly.
- `frameBorder`   
This merely defines the border thickness of the iframe.
- `width` and `height`   
This defines the width and height of the iframe.

These terms should now make more sense to you. Let’s move on and declare the state that will hold the HTML template document for `srcDoc`. If you look closely at the code block above, you’ll see that we passed a value to the `srcDoc` attribute: *`srcDoc`*`={srcDoc}`. Let’s use our `useState()` React hook to declare the `srcDoc` state. To do this, in the `App.js` file, go to where we defined the other states and add this one:

<pre><code class="language-javascript">const [srcDoc, setSrcDoc] = useState(` `);</code></pre>

Now that we have created the state, the next thing to do is display the result in the state whenever we type in the code editor. But what we don’t want is to re-render the component on every single key press. With that in mind, let’s proceed.

### Configuring the Iframe to Display the Result

Every time there's a change in any of the editors for the HTML, CSS, and JavaScript, respectively, we want `useEffect()` to be triggered, and that will render the updated result in the iframe. Let’s write `useEffect()` to do this in the `App.js` file:

First, import the `useEffect()` hook:

<pre><code class="language-javascript">import React, { useState,  useEffect } from 'react';</code></pre>

Let’s write `useEffect()` like so:

<pre><code class="language-javascript">useEffect(() =&gt; {
    const timeOut = setTimeout(() =&gt; {
      setSrcDoc(
        `
          &lt;html&gt;
            &lt;body&gt;${html}&lt;/body&gt;
            &lt;style&gt;${css}&lt;/style&gt;
            &lt;script&gt;${js}&lt;/script&gt;
          &lt;/html&gt;
        `
      )
    }, 250);
    return () =&gt; clearTimeout(timeOut)
  }, [html, css, js])</code></pre>

Here, we wrote a `useEffect()` hook that will always run whenever the value states that we declared for the HTML, CSS, and JavaScript editors are changed or updated.

Why did we need to use `setTimeout()`? Well, if we wrote this without it, then every time a single key press is made in an editor, our iframe would be updated, and that isn’t great for performance generally. So we use `setTimeout()` to delay the update for 250 milliseconds, giving us enough time to know whether the user is still typing. That is, every time the user presses a key, it restarts the count, so the iframe would only be updated when the user has been idle (not typing) for 250 milliseconds. This is a cool way to avoid having to update the iframe every time a key is pressed.

The next thing we did above was to update `srcDoc` with the new changes. The `srcDoc` component, as we explained above, renders specified HTML content in the iframe. In our code, we passed an HTML template, taking the `html` state that contains the code that the user has typed into the HTML editor and placing it between the `body` tags of our template. We also took the `css` state that contains the styles that the user has typed in the CSS editor, and we passed that between the `style` tags. Finally, we took the `js` state that contains the JavaScript code that the user has typed in the JavaScript editor, and we passed it between the `script` tags.

Notice that in setting `setSrcDoc`, we used backticks (`` ` ` ``) instead of normal quotes (`' '`). This is because backticks allow us to pass in corresponding state values, as we did in the code above.

The `return` statement in the `useEffect()` hook is a cleanup function that clears `setTimeout()` when it is complete, to avoid memory leakage. The [documentation has more](https://reactjs.org/docs/hooks-effect.html) about `useEffect`.

Here’s what our project looks like at the moment:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c00873c4-68a4-427e-8481-c4d25a44649f/3-building-web-code-editor.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ffa79c1-1410-49b5-a145-0c0a5d986b4a/3-building-web-code-editor-800w.gif" width="800" height="380" alt="What our project looks like at the moment" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c00873c4-68a4-427e-8481-c4d25a44649f/3-building-web-code-editor.gif">Large preview</a>)</figcaption></figure>

### CodeMirror Addons

With CodeMirror addons, we can enhance our editor with more of the kind of functionality we would find in other code editors. Let’s walk through an example of closing tags being added automatically when an opening tag is typed, and another example of a bracket automatically closing when the opening bracket is inputted:

The first thing to do is import the addon for this into our `App.js` file:

<pre><code class="language-javascript">import 'codemirror/addon/edit/closetag';
import 'codemirror/addon/edit/closebrackets';</code></pre>

Let’s pass it in the `ControlledEditorComponent` options:

<pre><code class="language-javascript">&lt;ControlledEditorComponent
        ...
        options={{
          ...
          autoCloseTags: true,
          autoCloseBrackets: true,
        }}
      /&gt;</code></pre>

Now here’s what we have:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507dbd6b-c186-4ed6-92cd-4f382f638e97/1-building-web-code-editor.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4239cd95-e529-484c-a79a-e641f64c3367/1-building-web-code-editor-800w.gif" width="800" height="379" alt="The way our project looks" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507dbd6b-c186-4ed6-92cd-4f382f638e97/1-building-web-code-editor.gif">Large preview</a>)</figcaption></figure>

You could add a ton of these addons to your editor to give it richer features. We couldn’t possibly go through [all of them](https://codemirror.net/doc/manual.html#addons) here.

Now that we are done with this, let’s briefly discuss things we could do to improve our app’s accessibility and performance.

## Performance and Accessibility of the Solution

Looking at our web code editor, some things could definitely be improved upon.

Because we’ve paid attention primarily to functionality, we might have neglected design a little bit. For better accessibility, here are some things you could do to improve this solution:

1. You could set an `active` class on the button for the currently open editor. Highlighting the button would improve accessibility by giving users a clear indication of which editor they’re currently working on.
2. You might want the editor to occupy more screen space than what we have here. Another thing you could try is making the iframe pop up with the click of a button that is docked somewhere to the side. Doing so would give the editor more screen space.
3. This sort of editor would be useful for people who want to run a quick exercise on their mobile device, so fully adapting it to mobile would be necessary (not to mention both of the points about mobile above).
4. Currently, we are able to switch the theme of the editor component from among the multiple themes we’ve loaded in, but the general theme of the page remains the same. You could enable the user to switch between a dark and light theme for the entire layout. This would be good for accessibility, relieving the strain on people’s eyes from looking at a bright screen for too long.
5. We didn’t look at security issues with our iframe, mainly because we were loading an internal HTML document in the iframe, rather than an external document. So we don’t need to consider this too carefully because iframes are a good fit for our use case.
6. With iframes, another consideration would be page-loading time, because the content being loaded in the iframe would normally be out of your control. In our app, this isn’t an issue because our iframe content isn’t external.

Performance and accessibility are worth a lot of consideration when you’re building any application because they will determine how useful and usable your application is to its users.

[Shedrack](https://www.smashingmagazine.com/author/shedrack-akintayo/) has done a good job of explaining methods for [improving and optimizing performance in React apps](https://www.smashingmagazine.com/2020/07/methods-performance-react-apps/). It’s worth checking out!

## Conclusion

Working through different projects helps us to learn about a wide range of subjects. Now that you’ve gone through this article, feel free to expand upon your experience by experimenting with more add-ons to make the code editor richer, revamping the UI, and fixing the accessibility and performance concerns outlined above.

- The entire code base for this project is [available on GitHub](https://github.com/smashingmagazine/web_code_editor).

Here’s the demo on Codesandbox:

<iframe src="https://codesandbox.io/embed/suspicious-breeze-hf41m?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="suspicious-breeze-hf41m"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

### Links and Material

- “[Google Chrome’s Portals: Like Iframes, But Better, and Worse](https://bluepnume.medium.com/google-chromes-portals-like-iframes-but-better-and-worse-29e0bbb3f78e)”, Daniel Brain
- “[Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab)”, React documentation
- “[User Manual and Reference Guide](https://codemirror.net/doc/manual.html)”, CodeMirror documentation

{{< signature "ks, vf, yk, il, al" >}}
