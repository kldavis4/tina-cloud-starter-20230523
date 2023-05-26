---
title: 'Building A Rich Text Editor (WYSIWYG)'
slug: building-wysiwyg-editor-javascript-slatejs
author: shalabh-vyas
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bafdd817-038e-4e70-a830-de0f5da659c4/building-wysiwyg-editor-javascript-slatejs.jpg
date: 2021-05-21T11:30:00.000Z
summary: >-
  In this article, we will learn how to build a WYSIWYG/Rich-Text Editor that supports rich text, images, links and some nuanced features from word processing apps. We will use [SlateJS](https://www.slatejs.org/) to build the shell of the editor and then add a toolbar and custom configurations. The code for the application is [available on GitHub](https://github.com/smashingmagazine/wysiwyg-editor) for reference.
description: >-
  Let’s build a rich text, WYSIWYG-editor that supports rich text, images, links and some nuanced features from word processing apps. We will use SlateJS to build the shell of the editor and then add a toolbar and custom configurations.
categories:
  - Tools
  - JavaScript
---

In recent years, the field of Content Creation and Representation on Digital platforms has seen a massive disruption. The widespread success of products like Quip, Google Docs and Dropbox Paper has shown how companies are racing to build the best experience for content creators in the enterprise domain and trying to find innovative ways of breaking the traditional moulds of how content is shared and consumed. Taking advantage of the massive outreach of social media platforms, there is a new wave of independent content creators using platforms like Medium to create content and share it with their audience. 

As so many people from different professions and backgrounds try to create content on these products, it’s important that these products provide a performant and seamless experience of content creation and have teams of designers and engineers who develop some level of domain expertise over time in this space. With this article, we try to not only lay the foundation of building an editor but also give the readers a glimpse into how little nuggets of functionalities when brought together can create a great user experience for a content creator.

## Understanding The Document Structure

Before we dive into building the editor, let’s look at how a document is structured for a Rich Text Editor and what are the different types of data structures involved.

### Document Nodes

Document nodes are used to represent the contents of the document. The common types of nodes that a rich-text document could contain are paragraphs, headings, images, videos, code-blocks and pull-quotes. Some of these may contain other nodes as children inside them (e.g. Paragraph nodes contain text nodes inside them). Nodes also hold any properties specific to the object they represent that are needed to render those nodes inside the editor. (e.g. Image nodes contain an image `src` property, Code-blocks may contain a `language` property and so on). 

There are largely two types of nodes that represent how they should be rendered -

- **Block Nodes** (analogous to HTML concept of Block-level elements) that are each rendered on a new line and occupy the available width. Block nodes could contain other block nodes or inline nodes inside them. An observation here is that the top-level nodes of a document would always be block nodes.
- **Inline Nodes** (analogous to HTML concept of Inline elements) that start rendering on the same line as the previous node. There are some differences in how inline elements are represented in different editing libraries. SlateJS allows for inline elements to be nodes themselves. DraftJS, another popular Rich Text Editing library, lets you use the concept of Entities to render inline elements. Links and Inline Images are examples of Inline nodes.
- Void Nodes &mdash; SlateJS also allows this third category of nodes that we will use later in this article to render media. 

If you want to learn more about these categories, SlateJS’s documentation on [Nodes](https://docs.slatejs.org/concepts/02-nodes) is a good place to start. 

{{% feature-panel %}}

### Attributes

Similar to HTML’s concept of attributes, attributes in a Rich Text Document are used to represent non-content properties of a node or it’s children. For instance, a text node can have character-style attributes that tell us whether the text is bold/italic/underlined and so on. Although this article represents headings as nodes themselves, another way to represent them could be that nodes have paragraph-styles (`paragraph` & `h1-h6`) as attributes on them. 

Below image gives an example of how a document’s structure (in JSON) is described at a more granular level using nodes and attributes highlighting some of the elements in the structure to the left.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde879ad-0e29-4631-92b0-198cf8730af0/document-structure.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde879ad-0e29-4631-92b0-198cf8730af0/document-structure.png" width="800" height="" sizes="100vw" caption="Example Document and its structural representation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde879ad-0e29-4631-92b0-198cf8730af0/document-structure.png'>Large preview</a>)" alt="Image showing an example document inside the editor with its structure representation on the left" >}}

Some of the things worth calling out here with the structure are:

- Text nodes are represented as `{text: 'text content'}`
- Properties of the nodes are stored directly on the node (e.g. `url` for links and `caption` for images)
- SlateJS-specific representation of text attributes breaks the text nodes to be their own nodes if the character style changes. Hence, the text ‘**Duis aute irure dolor**’ is a text node of it’s own with `bold: true` set on it. Same is the case with the italic, underline and code style text in this document. 

### Locations And Selection

When building a rich text editor, it is crucial to have an understanding of how the most granular part of a document (say a character) can be represented with some sort of coordinates. This helps us navigate the document structure at runtime to understand where in the document hierarchy we are. Most importantly, location objects give us a way to represent user selection which is quite extensively used to tailor the user experience of the editor in real time. We will use selection to build our toolbar later in this article. Examples of these could be:

- Is the user’s cursor currently inside a link, maybe we should show them a menu to edit/remove the link?
- Has the user selected an image? Maybe we give them a menu to resize the image.
- If the user selects certain text and hits the DELETE button, we determine what user’s selected text was and remove that from the document.

SlateJS’s document on [Location](https://docs.slatejs.org/concepts/03-locations) explains these data structures extensively but we go through them here quickly as we use these terms at different instances in the article and show an example in the diagram that follows.

- **Path**  
Represented by an array of numbers, a path is the way to get to a node in the document. For instance, a path `[2,3]` represents the 3rd child node of the 2nd node in the document.
- **Point**  
More granular location of content represented by path + offset. For instance, a point of `{path: [2,3], offset: 14}` represents the 14th character of the 3rd child node inside the 2nd node of the document.
- **Range**  
A pair of points (called `anchor` and `focus`) that represent a range of text inside the document. This concept comes from Web’s [Selection API](https://developer.mozilla.org/en-US/docs/Web/API/Selection) where `anchor` is where user’s selection began and `focus` is where it ended. A collapsed range/selection denotes where anchor and focus points are the same (think of a blinking cursor in a text input for instance).

As an example let’s say that the user’s selection in our above document example is ` ipsum`: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ccf8c84-b447-4b34-a3b4-8ef4959e2125/locations.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ccf8c84-b447-4b34-a3b4-8ef4959e2125/locations.png" width="800" height="" sizes="100vw" caption="User selects the word <code> ipsum</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ccf8c84-b447-4b34-a3b4-8ef4959e2125/locations.png'>Large preview</a>)" alt=" Image with the text ` ipsum` selected in the editor" >}}

The user’s selection can be represented as: 

<div class="break-out">

 <pre><code class="language-javascript">{
  anchor: {path: [2,0], offset: 5}, /*0th text node inside the paragraph node which itself is index 2 in the document*/
  focus: {path: [2,0], offset: 11}, // space + 'ipsum'
}`
</code></pre>
</div>

## Setting Up The Editor

In this section, we are going to set up the application and get a basic rich-text editor going with SlateJS. The boilerplate application would be <code>[`create-react-app`](https://reactjs.org/docs/create-a-new-react-app.html)</code> with SlateJS dependencies added to it. We are building the UI of the application using components from  <code>[`react-bootstrap`](https://react-bootstrap.github.io/)</code>. Let’s get started!

Create a folder called `wysiwyg-editor` and run the below command from inside the directory to set up the react app. We then run a `yarn start` command that should spin up the local web server (port defaulting to 3000) and show you a React welcome screen.

<pre><code class="language-bash">npx create-react-app .
yarn start
</code></pre>

We then move on to add the SlateJS dependencies to the application.

<pre><code class="language-bash">yarn add slate slate-react
</code></pre>

`slate` is SlateJS's core package and `slate-react` includes the set of React components we will use to render Slate editors. SlateJS exposes some more [packages](https://github.com/ianstormtaylor/slate#packages) organized by functionality one might consider adding to their editor.

We first create a `utils` folder that holds any utility modules we create in this application. We start with creating an `ExampleDocument.js` that returns a basic document structure that contains a paragraph with some text. This module looks like below:

<pre><code class="language-javascript">const ExampleDocument = [
  {
    type: "paragraph",
    children: [
      { text: "Hello World! This is my paragraph inside a sample document." },
    ],
  },
];

export default ExampleDocument;
</code></pre>

We now add a folder called `components` that will hold all our React components and do the following:

- Add our first React component `Editor.js` to it. It only returns a `div` for now.
- Update the `App.js` component to hold the document in its state which is initialized to our `ExampleDocument` above. 
- Render the Editor inside the app and pass the document state and an `onChange` handler down to the Editor so our document state is updated as the user updates it. 
- We use React bootstrap’s Nav components to add a navigation bar to the application as well.

`App.js` component now looks like below:

<pre><code class="language-javascript">import Editor from './components/Editor';

function App() {
  const [document, updateDocument] = useState(ExampleDocument);

  return (
    &lt;&gt;
      &lt;Navbar bg="dark" variant="dark"&gt;
        &lt;Navbar.Brand href="#"&gt;
          &lt;img
            alt=""
            src="/app-icon.png"
            width="30"
            height="30"
            className="d-inline-block align-top"
          /&gt;{" "}
          WYSIWYG Editor
        &lt;/Navbar.Brand&gt;
      &lt;/Navbar&gt;
      &lt;div className="App"&gt;
        &lt;Editor document={document} onChange={updateDocument} /&gt;
      &lt;/div&gt;
    &lt;/&gt;
  );
</code></pre>

Inside the Editor component, we then instantiate the SlateJS editor and hold it inside a `useMemo` so that the object doesn’t change in between re-renders. 

<pre><code class="language-javascript">// dependencies imported as below.
import { withReact } from "slate-react";
import { createEditor } from "slate";

const editor = useMemo(() => withReact(createEditor()), []);
</code></pre>

`createEditor` gives us the SlateJS `editor` instance which we use extensively through the application to access selections, run data transformations and so on. [withReact](https://github.com/ianstormtaylor/slate/blob/master/packages/slate-react/src/plugin/with-react.ts) is a SlateJS plugin that adds React and DOM behaviors to the editor object. [SlateJS Plugins](https://docs.slatejs.org/concepts/07-plugins) are Javascript functions that receive the `editor` object and attach some configuration to it. This allows web developers to add configurations to their SlateJS editor instance in a composable way. 

We now import and render `<Slate />` and `<Editable />` components from SlateJS with the document prop we get from App.js. <code>[Slate](https://github.com/ianstormtaylor/slate/blob/master/packages/slate-react/src/components/slate.tsx)</code> exposes a bunch of React contexts we use to access in the application code. <code>[Editable](https://github.com/ianstormtaylor/slate/blob/master/packages/slate-react/src/components/editable.tsx)</code> is the component that renders the document hierarchy for editing. Overall, the <code>`Editor.js`</code> module at this stage looks like below:

<pre><code class="language-javascript">import { Editable, Slate, withReact } from "slate-react";

import { createEditor } from "slate";
import { useMemo } from "react";

export default function Editor({ document, onChange }) {
  const editor = useMemo(() =&gt; withReact(createEditor()), []);
  return (
    &lt;Slate editor={editor} value={document} onChange={onChange}&gt;
      &lt;Editable /&gt;
    &lt;/Slate&gt;
  );
}
</code></pre>

At this point, we have necessary React components added and the editor populated with an example document. Our Editor should be now set up allowing us to type in and change the content in real time &mdash; as in the screencast below.

{{< vimeo id="534643188" caption="Basic Editor Setup in action" breakout="true" >}}

Now, let’s move on to the next section where we configure the editor to render character styles and paragraph nodes.

## CUSTOM TEXT RENDERING AND A TOOLBAR

### Paragraph Style Nodes

Currently, our editor uses SlateJS’s default rendering for any new node types we may add to the document. In this section, we want to be able to render the heading nodes. To be able to do that, we provide a `renderElement` function prop to Slate’s components. This function gets called by Slate at runtime when it is trying to traverse the document tree and render each node. The renderElement function gets three parameters &mdash; 

- `attributes`  
SlateJS specific that must need to be applied to the top-level DOM element being returned from this function.
- `element`  
The node object itself as it exists in the document structure
- `children`  
The children of this node as defined in the document structure.

We add our `renderElement` implementation to a hook called `useEditorConfig` where we will add more editor configurations as we go. We then use the hook on the editor instance inside `Editor.js`.

<pre><code class="language-javascript">import { DefaultElement } from "slate-react";

export default function useEditorConfig(editor) {
  return { renderElement };
}

function renderElement(props) {
  const { element, children, attributes } = props;
  switch (element.type) {
    case "paragraph":
      return &lt;p {...attributes}&gt;{children}&lt;/p&gt;;
    case "h1":
      return &lt;h1 {...attributes}&gt;{children}&lt;/h1&gt;;
    case "h2":
      return &lt;h2 {...attributes}&gt;{children}&lt;/h2&gt;;
    case "h3":
      return &lt;h3 {...attributes}&gt;{children}&lt;/h3&gt;;
    case "h4":
      return &lt;h4 {...attributes}&gt;{children}&lt;/h4&gt;;
    default:
      // For the default case, we delegate to Slate's default rendering. 
      return &lt;DefaultElement {...props} /&gt;;
  }
}
</code></pre>

Since this function gives us access to the `element` (which is the node itself), we can customize `renderElement` to implement a more customized rendering that does more than just checking `element.type`. For instance, you could have an image node that has a `isInline` property that we could use to return a different DOM structure that helps us render inline images as against block images. 

We now update the Editor component to use this hook as below:

<pre><code class="language-javascript">const { renderElement } = useEditorConfig(editor);

return (
    ...
    &lt;Editable renderElement={renderElement} /&gt;
);
</code></pre>

With the custom rendering in place, we update the ExampleDocument to include our new node types and verify that they render correctly inside the editor.

<pre><code class="language-javascript">const ExampleDocument = [
  {
    type: "h1",
    children: [{ text: "Heading 1" }],
  },
  {
    type: "h2",
    children: [{ text: "Heading 2" }],
  },
 // ...more heading nodes
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/444bb608-7f60-40fb-8ed3-d583e9a535b2/paragraph-nodes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/444bb608-7f60-40fb-8ed3-d583e9a535b2/paragraph-nodes.png" width="800" height="" sizes="100vw" caption="Headings and Paragraph nodes in the Editor. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/444bb608-7f60-40fb-8ed3-d583e9a535b2/paragraph-nodes.png'>Large preview</a>)" alt="Image showing different headings and paragraph nodes rendered in the editor" >}}

### Character Styles

Similar to `renderElement`, SlateJS gives out a function prop called renderLeaf that can be used to customize rendering of the text nodes (`Leaf` referring to text nodes which are the leaves/lowest level nodes of the document tree). Following the example of `renderElement`, we write an implementation for `renderLeaf`.

<pre><code class="language-javascript">export default function useEditorConfig(editor) {
  return { renderElement, renderLeaf };
}

// ...
function renderLeaf({ attributes, children, leaf }) {
  let el = &lt;&gt;{children}&lt;/&gt;;

  if (leaf.bold) {
    el = &lt;strong&gt;{el}&lt;/strong&gt;;
  }

  if (leaf.code) {
    el = &lt;code&gt;{el}&lt;/code&gt;;
  }

  if (leaf.italic) {
    el = &lt;em&gt;{el}&lt;/em&gt;;
  }

  if (leaf.underline) {
    el = &lt;u&gt;{el}&lt;/u&gt;;
  }

  return &lt;span {...attributes}&gt;{el}&lt;/span&gt;;
}
</code></pre>

An important observation of the above implementation is that it allows us to respect HTML semantics for character styles. Since renderLeaf gives us access to the text node `leaf` itself, we can customize the function to implement a more customized rendering. For instance, you might have a way to let users choose a `highlightColor` for text and check that leaf property here to attach the respective styles.

We now update the Editor component to use the above, the `ExampleDocument` to have a few text nodes in the paragraph with combinations of these styles and verify that they are rendered as expected in the Editor with the semantic tags we used.

<pre><code class="language-javascript"># src/components/Editor.js

const { renderElement, renderLeaf } = useEditorConfig(editor);

return (
    ...
    &lt;Editable renderElement={renderElement} renderLeaf={renderLeaf} /&gt;
);
</code></pre>

<pre><code class="language-javascript"># src/utils/ExampleDocument.js

{
    type: "paragraph",
    children: [
      { text: "Hello World! This is my paragraph inside a sample document." },
      { text: "Bold text.", bold: true, code: true },
      { text: "Italic text.", italic: true },
      { text: "Bold and underlined text.", bold: true, underline: true },
      { text: "variableFoo", code: true },
    ],
  },
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/617fbdb7-4365-4501-8761-3f6aa1c485bd/character-styles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/617fbdb7-4365-4501-8761-3f6aa1c485bd/character-styles.png" width="800" height="" sizes="100vw" caption="Character styles in UI and how they are rendered in DOM tree. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/617fbdb7-4365-4501-8761-3f6aa1c485bd/character-styles.png'>Large preview</a>)" alt="Character styles in UI and how they are rendered in DOM tree" >}}

## Adding A Toolbar

Let’s begin by adding a new component `Toolbar.js` to which we add a few buttons for character styles and a dropdown for paragraph styles and we wire these up later in the section. 

<div class="break-out">

 <pre><code class="language-javascript">const PARAGRAPH_STYLES = ["h1", "h2", "h3", "h4", "paragraph", "multiple"];
const CHARACTER_STYLES = ["bold", "italic", "underline", "code"];

export default function Toolbar({ selection, previousSelection }) {
  return (
    &lt;div className="toolbar"&gt;
      {/&#42; Dropdown for paragraph styles &#42;/}
      &lt;DropdownButton
        className={"block-style-dropdown"}
        disabled={false}
        id="block-style"
        title={getLabelForBlockStyle("paragraph")}
      &gt;
        {PARAGRAPH_STYLES.map((blockType) =&gt; (
          &lt;Dropdown.Item eventKey={blockType} key={blockType}&gt;
            {getLabelForBlockStyle(blockType)}
          &lt;/Dropdown.Item&gt;
        ))}
      &lt;/DropdownButton&gt;
      {/&#42; Buttons for character styles &#42;/}
      {CHARACTER_STYLES.map((style) =&gt; (
        &lt;ToolBarButton
          key={style}
          icon={&lt;i className={&#96;bi ${getIconForButton(style)}&#96;} /&gt;}
          isActive={false}
        /&gt;
      ))}
    &lt;/div&gt;
  );
}

function ToolBarButton(props) {
  const { icon, isActive, ...otherProps } = props;
  return (
    &lt;Button
      variant="outline-primary"
      className="toolbar-btn"
      active={isActive}
      {...otherProps}
    &gt;
      {icon}
    &lt;/Button&gt;
  );
}
</code></pre>
</div>

We abstract away the buttons to the `ToolbarButton` component that is a wrapper around the React Bootstrap Button component. We then render the toolbar above the `Editable` inside `Editor` component and verify that the toolbar shows up in the application.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd671be-6551-4f13-976e-6ea3ab97c0f6/setup-toolbar.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd671be-6551-4f13-976e-6ea3ab97c0f6/setup-toolbar.png" width="800" height="" sizes="100vw" caption="Toolbar with buttons (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd671be-6551-4f13-976e-6ea3ab97c0f6/setup-toolbar.png'>Large preview</a>)" alt="Image showing toolbar with buttons rendered above the editor" >}}

Here are the three key functionalities we need the toolbar to support:

1. When the user’s cursor is in a certain spot in the document and they click one of the character style buttons, we need to toggle the style for the text they may type next.
2. When the user selects a range of text and click one of the character style buttons, we need to toggle the style for that specific section.
3. When the user selects a range of text, we want to update the paragraph-style dropdown to reflect the paragraph-type of the selection. If they do select a different value from the selection, we want to update the paragraph style of the entire selection to be what they selected.

Let’s look at how these functionalities work on the Editor before we start implementing them.

{{< vimeo id="534645555" caption="Character Styles toggling behavior" breakout="true" >}}

### Listening To Selection

The most important thing the Toolbar needs to be able to perform the above functions is the Selection state of the document. As of writing this article, SlateJS does not expose a `onSelectionChange` method that could give us the latest selection state of the document. However, as selection changes in the editor, SlateJS does call the `onChange` method, even if the document contents haven’t changed. We use this as a way to be notified of selection change and store it in the `Editor` component’s state. We abstract this to a hook `useSelection` where we could do a more optimal update of the selection state. This is important as selection is a property that changes quite often for a WYSIWYG Editor instance.

<pre><code class="language-javascript">import areEqual from "deep-equal";

export default function useSelection(editor) {
  const [selection, setSelection] = useState(editor.selection);
  const setSelectionOptimized = useCallback(
    (newSelection) => {
      // don't update the component state if selection hasn't changed.
      if (areEqual(selection, newSelection)) {
        return;
      }
      setSelection(newSelection);
    },
    [setSelection, selection]
  );

  return [selection, setSelectionOptimized];
}
</code></pre>

We use this hook inside the `Editor` component as below and pass the selection to the Toolbar component.

<pre><code class="language-javascript">const [selection, setSelection] = useSelection(editor);

  const onChangeHandler = useCallback(
    (document) =&gt; {
      onChange(document);
      setSelection(editor.selection);
    },
    [editor.selection, onChange, setSelection]
  );

  return (
    &lt;Slate editor={editor} value={document} onChange={onChangeHandler}&gt;
        &lt;Toolbar selection={selection} /&gt;
        ...
</code></pre>

#### Performance Consideration

In an application where we have a much bigger Editor codebase with a lot more functionalities, it is important to store and listen to selection changes in a performant way (like using some state management library) as components listening to selection changes are likely to render too often. One way to do this is to have optimized selectors on top of the Selection state that hold specific selection information. For instance, an editor might want to render an image resizing menu when an Image is selected. In such a case, it might be helpful to have a selector `isImageSelected` computed from the editor’s selection state and the Image menu would re-render only when this selector’s value changes. Redux’s [Reselect](https://github.com/reduxjs/reselect) is one such library that enables building selectors. 

We don’t use `selection` inside the toolbar until later but passing it down as a prop makes the toolbar re-render each time the selection changes on the Editor. We do this because we cannot rely solely on the document content change to trigger a re-render on the hierarchy (`App -> Editor -> Toolbar`) as users might just keep clicking around the document thereby changing selection but never actually changing the document content itself.

{{% ad-panel-leaderboard %}}

### Toggling Character Styles

We now move to getting what the active character styles are from SlateJS and using those inside the Editor. Let’s add a new JS module `EditorUtils` that will host all the util functions we build going forward to get/do stuff with SlateJS. Our first function in the module is `getActiveStyles` that gives a `Set` of active styles in the editor. We also add a function to toggle a style on the editor function &mdash; `toggleStyle`:

<pre><code class="language-javascript"># src/utils/EditorUtils.js

import { Editor } from "slate";

export function getActiveStyles(editor) {
  return new Set(Object.keys(Editor.marks(editor) ?? {}));
}

export function toggleStyle(editor, style) {
  const activeStyles = getActiveStyles(editor);
  if (activeStyles.has(style)) {
    Editor.removeMark(editor, style);
  } else {
    Editor.addMark(editor, style, true);
  }
}
</code></pre>

Both the functions take the `editor` object which is the Slate instance as a parameter as will a lot of util functions we add later in the article.In Slate terminology, formatting styles are called Marks and we use helper methods on [Editor](https://github.com/ianstormtaylor/slate/blob/master/packages/slate/src/interfaces/editor.ts#L41) interface to get, add and remove these marks.We import these util functions inside the Toolbar and wire them to the buttons we added earlier.

<pre><code class="language-javascript"># src/components/Toolbar.js

import { getActiveStyles, toggleStyle } from "../utils/EditorUtils";
import { useEditor } from "slate-react";

export default function Toolbar({ selection }) {
  const editor = useEditor();

return &lt;div
...
    {CHARACTER_STYLES.map((style) =&gt; (
        &lt;ToolBarButton
          key={style}
          characterStyle={style}
          icon={&lt;i className={`bi ${getIconForButton(style)}`} /&gt;}
          isActive={getActiveStyles(editor).has(style)}
          onMouseDown={(event) =&gt; {
            event.preventDefault();
            toggleStyle(editor, style);
          }}
        /&gt;
      ))}
&lt;/div&gt;
</code></pre>

`useEditor` is a Slate hook that gives us access to the Slate instance from the context where it was attached by the `&lt;Slate>` component higher up in the render hierarchy. 

One might wonder why we use `onMouseDown` here instead of `onClick`? There is an open [Github Issue](https://github.com/ianstormtaylor/slate/issues/3412) about how Slate turns the `selection` to `null` when the editor loses focus in any way. So, if we attach `onClick` handlers to our toolbar buttons, the `selection` becomes `null` and users lose their cursor position trying to toggle a style which is not a great experience. We instead toggle the style by attaching a `onMouseDown` event which prevents the selection from getting reset. Another way to do this is to keep track of the selection ourselves so we know what the last selection was and use that to toggle the styles. We do introduce the concept of `previousSelection` later in the article but to solve a different problem.

SlateJS allows us to configure event handlers on the Editor. We use that to wire up keyboard shortcuts to toggle the character styles. To do that, we add a `KeyBindings` object inside `useEditorConfig` where we expose a `onKeyDown` event handler attached to the `Editable` component. We use the [`is-hotkey`](https://www.npmjs.com/package/is-hotkey) util to determine the key combination and toggle the corresponding style.

<pre><code class="language-javascript"># src/hooks/useEditorConfig.js

export default function useEditorConfig(editor) {
  const onKeyDown = useCallback(
    (event) => KeyBindings.onKeyDown(editor, event),
    [editor]
  );
  return { renderElement, renderLeaf, onKeyDown };
}

const KeyBindings = {
  onKeyDown: (editor, event) => {
    if (isHotkey("mod+b", event)) {
      toggleStyle(editor, "bold");
      return;
    }
    if (isHotkey("mod+i", event)) {
      toggleStyle(editor, "italic");
      return;
    }
    if (isHotkey("mod+c", event)) {
      toggleStyle(editor, "code");
      return;
    }
    if (isHotkey("mod+u", event)) {
      toggleStyle(editor, "underline");
      return;
    }
  },
};

# src/components/Editor.js
...
 &lt;Editable
   renderElement={renderElement}
   renderLeaf={renderLeaf}
   onKeyDown={onKeyDown}
 /&gt;
</code></pre>

{{< vimeo id="534647334" caption="Character styles toggled using keyboard shortcuts." breakout="true" >}}

### Making Paragraph Style Dropdown Work

Let’s move on to making the Paragraph Styles dropdown work. Similar to how paragraph-style dropdowns work in popular Word Processing applications like MS Word or Google Docs, we want styles of the top level blocks in user’s selection to be reflected in the dropdown. If there is a single consistent style across the selection, we update the dropdown value to be that. If there are multiple of those, we set the dropdown value to be ‘Multiple’. This behavior must work for both &mdash; collapsed and expanded selections. 

To implement this behavior, we need to be able to find the top-level blocks spanning the user’s selection. To do so, we use Slate’s [`Editor.nodes`](https://github.com/ianstormtaylor/slate/blob/41cd18b5683fbbdadb570da37a919e24a28e3de1/packages/slate/src/interfaces/editor.ts#L167) &mdash; A helper function commonly used to search for nodes in a tree filtered by different options.

<pre><code class="language-javascript">nodes(
    editor: Editor,
    options?: {
      at?: Location | Span
      match?: NodeMatch&lt;T&gt;
      mode?: 'all' | 'highest' | 'lowest'
      universal?: boolean
      reverse?: boolean
      voids?: boolean
    }
  ) => Generator&lt;NodeEntry&lt;T&gt;, void, undefined&gt;
</code></pre>

The helper function takes an Editor instance and an `options` object that is a way to filter nodes in the tree as it traverses it. The function returns a generator of `NodeEntry`. A `NodeEntry` in Slate terminology is a tuple of  a node and the path to it &mdash; `[node, pathToNode]`. The options found here are available on most of the Slate helper functions. Let’s go through what each of those means:

- `at`  
This can be a Path/Point/Range that the helper function would use to scope down the tree traversal to. This defaults to `editor.selection` if not provided. We also use the default for our use case below as we’re interested in nodes within user’s selection.
- `match`  
This is a matching function one can provide that is called on each node and included if it is a match. We use this parameter in our implementation below to filter to block elements only. 
- `mode`  
Let’s the helper functions know if we’re interested in all, highest-level or lowest level nodes `at` the given location matching `match` function. This parameter (set to `highest`) helps us escape trying to traverse the tree **up** ourselves to find the top-level nodes.
- `universal`  
Flag to choose between full or partial matches of the nodes. ([GitHub Issue](https://github.com/ianstormtaylor/slate/issues/3248) with the proposal for this flag has some examples explaining it)
- `reverse`  
If the node search should be in the reverse direction of the start and end points of the location passed in.
- `voids`   
If the search should filter to void elements only.

SlateJS exposes a lot of helper functions that let you query for nodes in different ways, traverse the tree, update the nodes or selections in complex ways. Worth digging into some of these interfaces (listed towards the end of this article) when building complex editing functionalities on top of Slate. 

With that background on the helper function, below is an implementation of  `getTextBlockStyle`. 

<pre><code class="language-javascript"># src/utils/EditorUtils.js 

export function getTextBlockStyle(editor) {
  const selection = editor.selection;
  if (selection == null) {
    return null;
  }

  const topLevelBlockNodesInSelection = Editor.nodes(editor, {
    at: editor.selection,
    mode: "highest",
    match: (n) => Editor.isBlock(editor, n),
  });

  let blockType = null;
  let nodeEntry = topLevelBlockNodesInSelection.next();
  while (!nodeEntry.done) {
    const [node, _] = nodeEntry.value;
    if (blockType == null) {
      blockType = node.type;
    } else if (blockType !== node.type) {
      return "multiple";
    }

    nodeEntry = topLevelBlockNodesInSelection.next();
  }

  return blockType;
}
</code></pre>

#### Performance Consideration 

The current implementation of `Editor.nodes` finds all the nodes throughout the tree across all levels that are within the range of the `at` param and then runs match filters on it (check `nodeEntries` and the filtering later &mdash; [source](https://github.com/ianstormtaylor/slate/blob/41cd18b5683fbbdadb570da37a919e24a28e3de1/packages/slate/src/interfaces/editor.ts#L878)). This is okay for smaller documents. However, for our use case, if the user selected, say 3 headings and 2 paragraphs  (each paragraph containing say 10 text nodes), it will cycle through at least 25 nodes (3 + 2 + 2&#42;10) and try to run filters on them. Since we already know we’re interested in top-level nodes only, we could find start and end indexes of the top level blocks from the selection and iterate ourselves. Such a logic would loop through only 3 node entries (2 headings and 1 paragraph). Code for that would look something like below:

<pre><code class="language-javascript">export function getTextBlockStyle(editor) {
  const selection = editor.selection;
  if (selection == null) {
    return null;
  }
  // gives the forward-direction points in case the selection was
  // was backwards.
  const [start, end] = Range.edges(selection);

  //path[0] gives us the index of the top-level block.
  let startTopLevelBlockIndex = start.path[0];
  const endTopLevelBlockIndex = end.path[0];

  let blockType = null;
  while (startTopLevelBlockIndex <= endTopLevelBlockIndex) {
    const [node, _] = Editor.node(editor, [startTopLevelBlockIndex]);
    if (blockType == null) {
      blockType = node.type;
    } else if (blockType !== node.type) {
      return "multiple";
    }
    startTopLevelBlockIndex++;
  }

  return blockType;
}
</code></pre>

As we add more functionalities to a WYSIWYG Editor and need to traverse the document tree often, it is important to think about the most performant ways to do so for the use case at hand as the available API or helper methods might not always be the most efficient way to do so.

Once we have `getTextBlockStyle` implemented, toggling of the block style is relatively straightforward. If the current style is not what user selected in the dropdown, we toggle the style to that. If it is already what user selected, we toggle it to be a paragraph. Because we are representing paragraph styles as nodes in our document structure, toggle a paragraph style essentially means changing the `type` property on the node. We use [`Transforms.setNodes`](https://github.com/ianstormtaylor/slate/blob/e4936c3f32711a646ecdb51d4a75462975861660/packages/slate/src/transforms/node.ts#L68) provided by Slate to update properties on nodes.

Our `toggleBlockType`’s implementation is as below:

<pre><code class="language-javascript"># src/utils/EditorUtils.js

export function toggleBlockType(editor, blockType) {
  const currentBlockType = getTextBlockStyle(editor);
  const changeTo = currentBlockType === blockType ? "paragraph" : blockType;
  Transforms.setNodes(
    editor,
    { type: changeTo },
     // Node filtering options supported here too. We use the same
     // we used with Editor.nodes above.
    { at: editor.selection, match: (n) => Editor.isBlock(editor, n) }
  );
}
</code></pre>

Finally, we update our Paragraph-Style dropdown to use these utility functions. 

<pre><code class="language-javascript">#src/components/Toolbar.js

const onBlockTypeChange = useCallback(
    (targetType) =&gt; {
      if (targetType === "multiple") {
        return;
      }
      toggleBlockType(editor, targetType);
    },
    [editor]
  );

  const blockType = getTextBlockStyle(editor);

return (
    &lt;div className="toolbar"&gt;
      &lt;DropdownButton
        .....
        disabled={blockType == null}  
        title={getLabelForBlockStyle(blockType ?? "paragraph")}
        onSelect={onBlockTypeChange}
      &gt;
        {PARAGRAPH_STYLES.map((blockType) =&gt; (
          &lt;Dropdown.Item eventKey={blockType} key={blockType}&gt;
            {getLabelForBlockStyle(blockType)}
          &lt;/Dropdown.Item&gt;
        ))}
      &lt;/DropdownButton&gt;
....
);
</code></pre>

{{< vimeo id="534646808" caption="Selecting multiple block types and changing the type with the dropdown." breakout="true" >}}

## LINKS

In this section, we are going to add support to show, add, remove and change links. We will also add a Link-Detector functionality &mdash; quite similar to how Google Docs or MS Word that scan the text typed by the user and checks if there are links in there. If there are, they are converted into link objects so that the user doesn’t have to use toolbar buttons to do that themselves. 

### Rendering Links

In our editor, we are going to implement links as inline nodes with SlateJS. We update our editor config to flag links as inline nodes for SlateJS and also provide a component to render so Slate knows how to render the link nodes.

<pre><code class="language-javascript"># src/hooks/useEditorConfig.js
export default function useEditorConfig(editor) {
  ...
  editor.isInline = (element) =&gt; ["link"].includes(element.type);
  return {....}
}

function renderElement(props) {
  const { element, children, attributes } = props;
  switch (element.type) {
     ...
    case "link":
      return &lt;Link {...props} url={element.url} /&gt;;
      ...
  }
}
</code></pre>

<pre><code class="language-javascript"># src/components/Link.js
export default function Link({ element, attributes, children }) {
  return (
    &lt;a href={element.url} {...attributes} className={"link"}&gt;
      {children}
    &lt;/a&gt;
  );
}
</code></pre>

We then add a link node to our `ExampleDocument` and verify that it renders correctly (including a case for character styles inside a link) in the Editor.

<pre><code class="language-javascript"># src/utils/ExampleDocument.js
{
    type: "paragraph",
    children: [
      ...
      { text: "Some text before a link." },
      {
        type: "link",
        url: "https://www.google.com",
        children: [
          { text: "Link text" },
          { text: "Bold text inside link", bold: true },
        ],
      },
     ...
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e8910c-1b2f-4ff7-82fe-9d1886e6ad79/render-links.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e8910c-1b2f-4ff7-82fe-9d1886e6ad79/render-links.png" width="800" height="" sizes="100vw" caption="Links rendered in the Editor (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e8910c-1b2f-4ff7-82fe-9d1886e6ad79/render-links.png'>Large preview</a>)" alt="Image showing Links rendered in the Editor and DOM tree of the editor" >}}

### Adding A Link Button To The Toolbar

Let’s add a Link Button to the toolbar that enables the user to do the following:

- Selecting some text and clicking on the button converts that text into a link 
- Having a blinking cursor (collapsed selection) and clicking the button inserts a new link there
- If the user’s selection is inside a link, clicking on the button should toggle the link &mdash; meaning convert the link back to text.

To build these functionalities, we need a way in the toolbar to know if the user’s selection is inside a link node. We add a util function that traverses the levels in upward direction from the user’s selection to find a link node if there is one, using [`Editor.above`](https://github.com/ianstormtaylor/slate/blob/master/packages/slate/src/interfaces/editor.ts#L70) helper function from SlateJS.

<pre><code class="language-javascript"># src/utils/EditorUtils.js

export function isLinkNodeAtSelection(editor, selection) {
  if (selection == null) {
    return false;
  }

  return (
    Editor.above(editor, {
      at: selection,
      match: (n) => n.type === "link",
    }) != null
  );
}
</code></pre>


Now, let’s add a button to the toolbar that is in active state if the user's selection is inside a link node.

<pre><code class="language-javascript"># src/components/Toolbar.js

return (
    &lt;div className="toolbar"&gt;
      ...
      {/* Link Button &#42;/}
      &lt;ToolBarButton
        isActive={isLinkNodeAtSelection(editor, editor.selection)}
        label={&lt;i className={&#96;bi ${getIconForButton("link")}&#96;} /&gt;}
      /&gt;
    &lt;/div&gt;
  );
</code></pre>

{{< vimeo id="534648831" caption="Link button in Toolbar becomes active if selection is inside a link." breakout="true" >}}

To toggle links in the editor, we add a util function `toggleLinkAtSelection`. Let’s first look at how the toggle works when you have some text selected. When the user selects some text and clicks on the button, we want only the selected text to become a link. What this inherently means is that we need to break the text node that contains selected text and extract the selected text into a new link node. The before and after states of these would look something like below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8698a35c-74a3-46d5-994d-b590e622d06b/link-wrap-nodes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8698a35c-74a3-46d5-994d-b590e622d06b/link-wrap-nodes.png" width="800" height="" sizes="100vw" caption="Before and After node structures after a link is inserted. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8698a35c-74a3-46d5-994d-b590e622d06b/link-wrap-nodes.png'>Large preview</a>)" alt="Before and After node structures after a link is inserted" >}}

If we had to do this by ourselves, we’d have to figure out the range of selection and create three new nodes (text, link, text) that replace the original text node. SlateJS has a helper function called [`Transforms.wrapNodes`](https://github.com/ianstormtaylor/slate/blob/e4936c3f32711a646ecdb51d4a75462975861660/packages/slate/src/transforms/node.ts#L858) that does exactly this &mdash; wrap nodes at a location into a new container node. We also have a helper available for the reverse of this process &mdash; `Transforms.unwrapNodes` which we use to remove links from selected text and merge that text back into the text nodes around it. With that, `toggleLinkAtSelection` has the below implementation to insert a new link at an expanded selection.

<pre><code class="language-javascript"># src/utils/EditorUtils.js

export function toggleLinkAtSelection(editor) {
  if (!isLinkNodeAtSelection(editor, editor.selection)) {
    const isSelectionCollapsed =
      Range.isCollapsed(editor.selection);
    if (isSelectionCollapsed) {
      Transforms.insertNodes(
        editor,
        {
          type: "link",
          url: '#',
          children: [{ text: 'link' }],
        },
        { at: editor.selection }
      );
    } else {
      Transforms.wrapNodes(
        editor,
        { type: "link", url: '#', children: [{ text: '' }] },
        { split: true, at: editor.selection }
      );
    }
  } else {
    Transforms.unwrapNodes(editor, {
      match: (n) => Element.isElement(n) && n.type === "link",
    });
  }
}
</code></pre>

If the selection is collapsed, we insert a new node there with <code>[`Transform.insertNodes`](https://github.com/ianstormtaylor/slate/blob/e4936c3f32711a646ecdb51d4a75462975861660/packages/slate/src/transforms/node.ts#L17)</code> that inserts the node at the given location in the document. We wire this function up with the toolbar button and should now have a way to add/remove links from the document with the help of the link button.

<pre><code class="language-javascript"># src/components/Toolbar.js
      &lt;ToolBarButton
        ...
        isActive={isLinkNodeAtSelection(editor, editor.selection)}       
        onMouseDown={() =&gt; toggleLinkAtSelection(editor)}
      /&gt;
</code></pre>

{{< vimeo id="534649627" caption="" breakout="true" >}}

### Link Editor Menu

So far, our editor has a way to add and remove links but we don’t have a way to update the URLs associated with these links. How about we extend the user experience to allow users to edit it easily with a contextual menu? To enable link editing, we will build a link-editing popover that shows up whenever the user selection is inside a link and lets them edit and apply the URL to that link node. Let’s start with building an empty `LinkEditor` component and rendering it whenever the user selection is inside a link.

<pre><code class="language-javascript"># src/components/LinkEditor.js
export default function LinkEditor() {
  return (
    &lt;Card className={"link-editor"}&gt;
      &lt;Card.Body&gt;&lt;/Card.Body&gt;
    &lt;/Card&gt;
  );
}
</code></pre>

<pre><code class="language-javascript"># src/components/Editor.js

&lt;div className="editor"&gt;
    {isLinkNodeAtSelection(editor, selection) ? &lt;LinkEditor /&gt; : null}
    &lt;Editable
       renderElement={renderElement}
       renderLeaf={renderLeaf}
       onKeyDown={onKeyDown}
    /&gt;
&lt;/div&gt;
</code></pre>

Since we are rendering the `LinkEditor` outside the editor, we need a way to tell `LinkEditor` where the link is located in the DOM tree so it could render itself near the editor. The way we do this is use Slate’s React API to find the DOM node corresponding to the link node in selection. And we then use `getBoundingClientRect()` to find the link’s DOM element’s bounds and the editor component’s bounds and compute the `top` and `left` for the link editor. The code updates to `Editor` and `LinkEditor` are as below &mdash; 

<pre><code class="language-javascript"># src/components/Editor.js 

const editorRef = useRef(null)
&lt;div className="editor" ref={editorRef}&gt;
              {isLinkNodeAtSelection(editor, selection) ? (
                &lt;LinkEditor
                  editorOffsets={
                    editorRef.current != null
                      ? {
                          x: editorRef.current.getBoundingClientRect().x,
                          y: editorRef.current.getBoundingClientRect().y,
                        }
                      : null
                  }
                /&gt;
              ) : null}
              &lt;Editable
                renderElement={renderElement}
                ...
</code></pre>

<pre><code class="language-javascript"># src/components/LinkEditor.js

import { ReactEditor } from "slate-react";

export default function LinkEditor({ editorOffsets }) {
  const linkEditorRef = useRef(null);

  const [linkNode, path] = Editor.above(editor, {
    match: (n) => n.type === "link",
  });

  useEffect(() => {
    const linkEditorEl = linkEditorRef.current;
    if (linkEditorEl == null) {
      return;
    }

    const linkDOMNode = ReactEditor.toDOMNode(editor, linkNode);
    const {
      x: nodeX,
      height: nodeHeight,
      y: nodeY,
    } = linkDOMNode.getBoundingClientRect();

    linkEditorEl.style.display = "block";
    linkEditorEl.style.top = `${nodeY + nodeHeight &mdash; editorOffsets.y}px`;
    linkEditorEl.style.left = `${nodeX &mdash; editorOffsets.x}px`;
  }, [editor, editorOffsets.x, editorOffsets.y, node]);

  if (editorOffsets == null) {
    return null;
  }

  return &lt;Card ref={linkEditorRef} className={"link-editor"}&gt;&lt;/Card&gt;;
}
</code></pre>

SlateJS internally maintains maps of nodes to their respective DOM elements. We access that map and find the link’s DOM element using [`ReactEditor.toDOMNode`](https://github.com/ianstormtaylor/slate/blob/41cd18b5683fbbdadb570da37a919e24a28e3de1/packages/slate-react/src/plugin/react-editor.ts#L220). 

{{< vimeo id="534650043" caption="Selection inside a link shows the link editor popover." breakout="true" >}}

As seen in the video above, when a link is inserted and doesn’t have a URL, because the selection is inside the link, it opens the link editor thereby giving the user a way to type in a URL for the newly inserted link and hence closes the loop on the user experience there.

We now add an input element and a button to the `LinkEditor` that let the user type in a URL and apply it to the link node. We use the [`isUrl`](https://www.npmjs.com/package/is-url) package for URL validation.

<pre><code class="language-javascript"># src/components/LinkEditor.js

import isUrl from "is-url";

export default function LinkEditor({ editorOffsets }) {

const [linkURL, setLinkURL] = useState(linkNode.url);

  // update state if `linkNode` changes 
  useEffect(() =&gt; {
    setLinkURL(linkNode.url);
  }, [linkNode]);

  const onLinkURLChange = useCallback(
    (event) =&gt; setLinkURL(event.target.value),
    [setLinkURL]
  );

  const onApply = useCallback(
    (event) =&gt; {
      Transforms.setNodes(editor, { url: linkURL }, { at: path });
    },
    [editor, linkURL, path]
  );

return (
 ...
        &lt;Form.Control
          size="sm"
          type="text"
          value={linkURL}
          onChange={onLinkURLChange}
        /&gt;
        &lt;Button
          className={"link-editor-btn"}
          size="sm"
          variant="primary"
          disabled={!isUrl(linkURL)}
          onClick={onApply}
        &gt;
          Apply
        &lt;/Button&gt;
   ...
 );
</code></pre>

With the form elements wired up, let’s see if the link editor works as expected.

{{< vimeo id="534650772" caption="Editor losing selection on clicking inside link editor" breakout="true" >}}

As we see here in the video, when the user tries to click into the input, the link editor disappears. This is because as we render the link editor outside the `Editable` component, when the user clicks on the input element, SlateJS thinks the editor has lost focus and resets the `selection` to be `null` which removes the `LinkEditor` since `isLinkActiveAtSelection` is not `true` anymore.  There is an open [GitHub Issue](https://github.com/ianstormtaylor/slate/issues/3412) that talks about this Slate behavior. One way to solve this is to track the previous selection of a user as it changes and when the editor does lose focus, we could look at the previous selection and still show a link editor menu if previous selection had a link in it. Let’s update the `useSelection` hook to remember the previous selection and return that to the Editor component.

<pre><code class="language-javascript">
# src/hooks/useSelection.js
export default function useSelection(editor) {
  const [selection, setSelection] = useState(editor.selection);
  const previousSelection = useRef(null);
  const setSelectionOptimized = useCallback(
    (newSelection) => {
      if (areEqual(selection, newSelection)) {
        return;
      }
      previousSelection.current = selection;
      setSelection(newSelection);
    },
    [setSelection, selection]
  );

  return [previousSelection.current, selection, setSelectionOptimized];
}
</code></pre>

We then update the logic in the `Editor` component to show the link menu even if the previous selection had a link in it.

<div class="break-out">

 <pre><code class="language-javascript"># src/components/Editor.js


  const [previousSelection, selection, setSelection] = useSelection(editor);

  let selectionForLink = null;
  if (isLinkNodeAtSelection(editor, selection)) {
    selectionForLink = selection;
  } else if (selection == null && isLinkNodeAtSelection(editor, previousSelection)) {
    selectionForLink = previousSelection;
  }

  return (
    ...
            &lt;div className="editor" ref={editorRef}&gt;
              {selectionForLink != null ? (
                &lt;LinkEditor
                  selectionForLink={selectionForLink}
                  editorOffsets={..}
  ...
);
</code></pre>
</div>

We then update `LinkEditor` to use `selectionForLink` to look up the link node, render below it and update it’s URL.

<pre><code class="language-javascript"># src/components/Link.js
export default function LinkEditor({ editorOffsets, selectionForLink }) {
  ...
  const [node, path] = Editor.above(editor, {
    at: selectionForLink,
    match: (n) => n.type === "link",
  });
  ...
</code></pre>

{{< vimeo id="534651383" caption="Editing link using the LinkEditor component." breakout="true" >}}

### Detecting Links In Text

Most of the word processing applications identify and convert links inside text to link objects. Let’s see how that would work in the editor before we start building it.

{{< vimeo id="534651788" caption="Links being detected as the user types them in." breakout="true" >}}

The steps of the logic to enable this behavior would be:

1. As the document changes with the user typing, find the last character inserted by the user. If that character is a space, we know there must be a word that might have come before it.
2. If the last character was space, we mark that as the end boundary of the word that came before it. We then traverse back character by character inside the text node to find  where that word began. During this traversal, we have to be careful to not go past the edge of the start of the node into the previous node.
3. Once we have found the start and end boundaries of the word before, we check the string of the word and see if that was a URL. If it was, we convert it into a link node.

Our logic lives in a util function `identifyLinksInTextIfAny` that lives in `EditorUtils` and is called inside the `onChange` in `Editor` component.

<pre><code class="language-javascript"># src/components/Editor.js

  const onChangeHandler = useCallback(
    (document) => {
      ...
      identifyLinksInTextIfAny(editor);
    },
    [editor, onChange, setSelection]
  );
</code></pre>

Here is `identifyLinksInTextIfAny` with the logic for Step 1 implemented:

<pre><code class="language-javascript">export function identifyLinksInTextIfAny(editor) {
  // if selection is not collapsed, we do not proceed with the link  
  // detection
  if (editor.selection == null || !Range.isCollapsed(editor.selection)) {
    return;
  }

  const [node, _] = Editor.parent(editor, editor.selection);

  // if we are already inside a link, exit early.
  if (node.type === "link") {
    return;
  }

  const [currentNode, currentNodePath] = Editor.node(editor, editor.selection);

  // if we are not inside a text node, exit early.
  if (!Text.isText(currentNode)) {
    return;
  }

  let [start] = Range.edges(editor.selection);
  const cursorPoint = start;

  const startPointOfLastCharacter = Editor.before(editor, editor.selection, {
    unit: "character",
  });

  const lastCharacter = Editor.string(
    editor,
    Editor.range(editor, startPointOfLastCharacter, cursorPoint)
  );

  if(lastCharacter !== ' ') {
    return;
  }
</code></pre>

There are two SlateJS helper functions which make things easy here.

- [`Editor.before`](https://github.com/ianstormtaylor/slate/blob/41cd18b5683fbbdadb570da37a919e24a28e3de1/packages/slate/src/interfaces/editor.ts#L369) &mdash; Gives us the point before a certain location. It takes `unit` as a parameter so we could ask for the character/word/block etc before the `location` passed in. 
- [`Editor.string`](https://github.com/ianstormtaylor/slate/blob/41cd18b5683fbbdadb570da37a919e24a28e3de1/packages/slate/src/interfaces/editor.ts#L1462) &mdash; Gets the string inside a range.

As an example, the diagram below explains what values of these variables are when the user inserts a character ‘E’ and their cursor is sitting after it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2f588a-71d9-43a2-8236-5fa99f375a48/link-detection-step-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2f588a-71d9-43a2-8236-5fa99f375a48/link-detection-step-1.png" width="800" height="" sizes="100vw" caption="<code>cursorPoint</code> and <code>startPointOfLastCharacter</code> after Step 1 with an example text. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2f588a-71d9-43a2-8236-5fa99f375a48/link-detection-step-1.png'>Large preview</a>)" alt="Diagram explaining where cursorPoint and startPointOfLastCharacter point to after step 1 with an example" >}}

If the text ’ABCDE’ was the first text node of the first paragraph in the document, our point values would be &mdash; 

<pre><code class="language-javascript">cursorPoint = { path: [0,0], offset: 5}
startPointOfLastCharacter = { path: [0,0], offset: 4}
</code></pre>

If the last character was a space, we know where it started &mdash; `startPointOfLastCharacter.`Let’s move to step-2 where we move backwards character-by-character until either we find another space or the start of the text node itself. 

<pre><code class="language-javascript">...
 
  if (lastCharacter !== " ") {
    return;
  }

  let end = startPointOfLastCharacter;
  start = Editor.before(editor, end, {
    unit: "character",
  });

  const startOfTextNode = Editor.point(editor, currentNodePath, {
    edge: "start",
  });

  while (
    Editor.string(editor, Editor.range(editor, start, end)) !== " " &&
    !Point.isBefore(start, startOfTextNode)
  ) {
    end = start;
    start = Editor.before(editor, end, { unit: "character" });
  }

  const lastWordRange = Editor.range(editor, end, startPointOfLastCharacter);
  const lastWord = Editor.string(editor, lastWordRange);
</code></pre>


Here is a diagram that shows where these different points point to once we find the last word entered to be `ABCDE`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7729144-0b85-46b4-9018-46a20325881e/link-detection-step-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7729144-0b85-46b4-9018-46a20325881e/link-detection-step-2.png" width="800" height="" sizes="100vw" caption="Where different points are after step 2 of link detection with an example. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7729144-0b85-46b4-9018-46a20325881e/link-detection-step-2.png'>Large preview</a>)" alt="Diagram explaining where different points are after step 2 of link detection with an example" >}}

Note that `start` and `end` are the points before and after the space there. Similarly, `startPointOfLastCharacter` and `cursorPoint` are the points before and after the space user just inserted. Hence `[end,startPointOfLastCharacter]` gives us the last word inserted.

We log the value of `lastWord` to the console and verify the values as we type.

{{< vimeo id="534652977" caption="Console logs verifying last word as entered by the user after the logic in Step 2." breakout="true" >}}

Now that we have deduced what the last word was that the user typed, we verify that it was a URL indeed and convert that range into a link object.  This conversion looks similar to how the toolbar link button converted a user's selected text into a link.

<pre><code class="language-javascript">if (isUrl(lastWord)) {
    Promise.resolve().then(() => {
      Transforms.wrapNodes(
        editor,
        { type: "link", url: lastWord, children: [{ text: lastWord }] },
        { split: true, at: lastWordRange }
      );
    });
  }
</code></pre>

`identifyLinksInTextIfAny` is called inside Slate’s `onChange` so we wouldn’t want to update the document structure inside the `onChange`. Hence, we put this update on our task queue with a `Promise.resolve().then(..)` call.

Let’s see the logic come together in action! We verify if we insert links at the end, in the middle or the start of a text node.

{{< vimeo id="534653441" caption="Links being detected as user is typing them." breakout="true" >}}

With that, we have wrapped up functionalities for links on the editor and move on to Images.

{{% ad-panel-leaderboard %}}

## Handling Images

In this section, we focus on adding support to render image nodes, add new images and update image captions. Images, in our document structure, would be represented as Void nodes. Void nodes in SlateJS (analogous to [Void elements](https://www.w3.org/TR/2011/WD-html-markup-20110405/syntax.html#void-element) in HTML spec) are such that their contents are not editable text. That allows us to render images as voids. Because of Slate’s flexibility with rendering, we can still render our own editable elements inside Void elements &mdash; which we will for image caption-editing. SlateJS has an [example](https://www.slatejs.org/examples/editable-voids) which demonstrates how you can embed an entire Rich Text Editor inside a Void element.

To render images, we configure the editor to treat images as Void elements and provide a render implementation of how images should be rendered. We add an image to our ExampleDocument and verify that it renders correctly with the caption.

<pre><code class="language-javascript"># src/hooks/useEditorConfig.js

export default function useEditorConfig(editor) {
  const { isVoid } = editor;
  editor.isVoid = (element) =&gt; {
    return ["image"].includes(element.type) || isVoid(element);
  };
  ...
}

function renderElement(props) {
  const { element, children, attributes } = props;
  switch (element.type) {
    case "image":
      return &lt;Image {...props} /&gt;;
...
``



``
# src/components/Image.js
function Image({ attributes, children, element }) {
  return (
    &lt;div contentEditable={false} {...attributes}&gt;
      &lt;div
        className={classNames({
          "image-container": true,
        })}
      &gt;
        &lt;img
          src={String(element.url)}
          alt={element.caption}
          className={"image"}
        /&gt;
        &lt;div className={"image-caption-read-mode"}&gt;{element.caption}&lt;/div&gt;
      &lt;/div&gt;     
      {children}
    &lt;/div&gt;
  );
}
</code></pre>

Two things to remember when trying to render void nodes with SlateJS:

- The root DOM element should have `contentEditable={false}` set on it so that SlateJS treats its contents so. Without this, as you interact with the void element, SlateJS may try to compute selections etc. and break as a result.
- Even if Void nodes don’t have any child nodes (like our image node as an example), we still need to render `children` and provide an empty text node as child (see `ExampleDocument` below) which is treated as a selection point of the Void element by SlateJS

We now update the `ExampleDocument` to add an image and verify that it shows up with the caption in the editor.

<pre><code class="language-javascript"># src/utils/ExampleDocument.js

const ExampleDocument = [
   ...
   {
    type: "image",
    url: "/photos/puppy.jpg",
    caption: "Puppy",
    // empty text node as child for the Void element.
    children: [{ text: "" }],
  },
];
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eafd088d-0fb2-4a28-a063-84f0fa186b71/image-rendering.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eafd088d-0fb2-4a28-a063-84f0fa186b71/image-rendering.png" width="800" height="" sizes="100vw" caption="Image rendered in the Editor. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eafd088d-0fb2-4a28-a063-84f0fa186b71/image-rendering.png'>Large preview</a>)" alt="Image rendered in the Editor" >}}

Now let’s focus on caption-editing. The way we want this to be a seamless experience for the user is that when they click on the caption, we show a text input where they can edit the caption. If they click outside the input or hit the RETURN key, we treat that as a confirmation to apply the caption. We then update the caption on the image node and switch the caption back to read mode. Let’s see it in action so we have an idea of what we’re building.

{{< vimeo id="534654272" caption="Image Caption Editing in action." breakout="true" >}}

Let’s update our Image component to have a state for caption’s read-edit modes. We update the local caption state as the user updates it and when they click out (`onBlur`) or hit RETURN (`onKeyDown`), we apply the caption to the node and switch to read mode again.

<pre><code class="language-javascript">const Image = ({ attributes, children, element }) =&gt; {
  const [isEditingCaption, setEditingCaption] = useState(false);
  const [caption, setCaption] = useState(element.caption);
  ...

  const applyCaptionChange = useCallback(
    (captionInput) =&gt; {
      const imageNodeEntry = Editor.above(editor, {
        match: (n) =&gt; n.type === "image",
      });
      if (imageNodeEntry == null) {
        return;
      }

      if (captionInput != null) {
        setCaption(captionInput);
      }

      Transforms.setNodes(
        editor,
        { caption: captionInput },
        { at: imageNodeEntry[1] }
      );
    },
    [editor, setCaption]
  );

  const onCaptionChange = useCallback(
    (event) =&gt; {
      setCaption(event.target.value);
    },
    [editor.selection, setCaption]
  );

  const onKeyDown = useCallback(
    (event) =&gt; {
      if (!isHotkey("enter", event)) {
        return;
      }

      applyCaptionChange(event.target.value);
      setEditingCaption(false);
    },
    [applyCaptionChange, setEditingCaption]
  );

  const onToggleCaptionEditMode = useCallback(
    (event) =&gt; {
      const wasEditing = isEditingCaption;
      setEditingCaption(!isEditingCaption);
      wasEditing && applyCaptionChange(caption);
    },
    [editor.selection, isEditingCaption, applyCaptionChange, caption]
  );

  return (
        ...
        {isEditingCaption ? (
          &lt;Form.Control
            autoFocus={true}
            className={"image-caption-input"}
            size="sm"
            type="text"
            defaultValue={element.caption}
            onKeyDown={onKeyDown}
            onChange={onCaptionChange}
            onBlur={onToggleCaptionEditMode}
          /&gt;
        ) : (
          &lt;div
            className={"image-caption-read-mode"}
            onClick={onToggleCaptionEditMode}
          &gt;
            {caption}
          &lt;/div&gt;
        )}
      &lt;/div&gt;
      ...
</code></pre>

With that, the caption editing functionality is complete. We now move to adding a way for users to upload images to the editor. Let’s add a toolbar button that lets users select and upload an image.

<pre><code class="language-javascript"># src/components/Toolbar.js

const onImageSelected = useImageUploadHandler(editor, previousSelection);

return (
    &lt;div className="toolbar"&gt;
    ....
   &lt;ToolBarButton
        isActive={false}
        as={"label"}
        htmlFor="image-upload"
        label={
          &lt;&gt;
            &lt;i className={`bi ${getIconForButton("image")}`} /&gt;
            &lt;input
              type="file"
              id="image-upload"
              className="image-upload-input"
              accept="image/png, image/jpeg"
              onChange={onImageSelected}
            /&gt;
          &lt;/&gt;
        }
      /&gt;
    &lt;/div&gt;
</code></pre>



As we work with image uploads, the code could grow quite a bit so we move the image-upload handling to a hook `useImageUploadHandler` that gives out a callback attached to the file-input element. We’ll discuss shortly about why it needs the `previousSelection` state.

Before we implement `useImageUploadHandler`, we’ll set up the server to be able to upload an image to. We setup an Express server and install two other packages &mdash; [`cors`](https://www.npmjs.com/package/cors) and [`multer`](https://www.npmjs.com/package/multer) that handle file uploads for us. 

<pre><code class="language-bash">yarn add express cors multer
</code></pre>

We then add a `src/server.js` script that configures the Express server with cors and multer and exposes an endpoint `/upload` which we will upload the image to.

<pre><code class="language-javascript"># src/server.js

const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, "./public/photos/");
  },
  filename: function (req, file, cb) {
    cb(null, file.originalname);
  },
});

var upload = multer({ storage: storage }).single("photo");

app.post("/upload", function (req, res) {
  upload(req, res, function (err) {
    if (err instanceof multer.MulterError) {
      return res.status(500).json(err);
    } else if (err) {
      return res.status(500).json(err);
    }
    return res.status(200).send(req.file);
  });
});

app.use(cors());
app.listen(port, () =&gt; console.log(`Listening on port ${port}`));
</code></pre>

Now that we have the server setup, we can focus on handling the image upload. When the user uploads an image, it could be a few seconds before the image gets uploaded and we have a URL for it. However, we do what to give the user immediate feedback that the image upload is in progress so that they know the image is being inserted in the editor. Here are the steps we implement to make this behavior work -

1. Once the user selects an image, we insert an image node at the user’s cursor position with a flag `isUploading` set on it so we can show the user a loading state.
2. We send the request to the server to upload the image.
3. Once the request is complete and we have an image URL, we set that on the image and remove the loading state.

Let’s begin with the first step where we insert the image node. Now, the tricky part here is we run into the same issue with selection as with the link button in the toolbar. As soon as the user clicks on the Image button in the toolbar, the editor loses focus and the selection becomes `null`. If we try to insert an image, we don’t know where the user's cursor was. Tracking `previousSelection` gives us that location and we use that to insert the node.

<pre><code class="language-javascript"># src/hooks/useImageUploadHandler.js
import { v4 as uuidv4 } from "uuid";

export default function useImageUploadHandler(editor, previousSelection) {
  return useCallback(
    (event) => {
      event.preventDefault();
      const files = event.target.files;
      if (files.length === 0) {
        return;
      }
      const file = files[0];
      const fileName = file.name;
      const formData = new FormData();
      formData.append("photo", file);

      const id = uuidv4();

      Transforms.insertNodes(
        editor,
        {
          id,
          type: "image",
          caption: fileName,
          url: null,
          isUploading: true,
          children: [{ text: "" }],
        },
        { at: previousSelection, select: true }
      );
    },
    [editor, previousSelection]
  );
}
</code></pre>

As we insert the new image node, we also assign it an identifier `id` using the [uuid](https://www.npmjs.com/package/uuid) package. We’ll discuss in Step (3)’s implementation why we need that. We now update the image component to use the `isUploading` flag to show a loading state.

<pre><code class="language-javascript">{!element.isUploading && element.url != null ? (
   &lt;img src={element.url} alt={caption} className={"image"} /&gt;
) : (
   &lt;div className={"image-upload-placeholder"}&gt;
        &lt;Spinner animation="border" variant="dark" /&gt;
   &lt;/div&gt;
)}
</code></pre>

That completes the implementation of step 1. Let’s verify that we are able to select an image to upload, see the image node getting inserted with a loading indicator where it was inserted in the document.

{{< vimeo id="534655011" caption="Image upload creating an image node with loading state." breakout="true" >}}

Moving to Step (2), we will use [axois](https://www.npmjs.com/package/axios) library to send a request to the server.

<pre><code class="language-javascript">export default function useImageUploadHandler(editor, previousSelection) {
  return useCallback((event) => {
    ....
    Transforms.insertNodes(
     …
     {at: previousSelection, select: true}
    );

    axios
      .post("/upload", formData, {
        headers: {
          "content-type": "multipart/form-data",
        },
      })
      .then((response) => {
           // update the image node.
       })
      .catch((error) => {
        // Fire another Transform.setNodes to set an upload failed state on the image
      });
  }, [...]);
}
</code></pre>

We verify that the image upload works and the image does show up in the `public/photos` folder of the app. Now that the image upload is complete, we move to Step (3) where we want to set the URL on the image in the `resolve()` function of the axios promise. We could update the image with `Transforms.setNodes` but we have a problem &mdash; we do not have the path to the newly inserted image node. Let’s see what our options are to get to that image &mdash; 

- Can’t we use `editor.selection` as the selection must be on the newly inserted image node? We cannot guarantee this since while the image was uploading, the user might have clicked somewhere else and the selection might have changed.
- How about using `previousSelection`  which we used to insert the image node in the first place? For the same reason we can’t use `editor.selection`, we can’t use `previousSelection` since it may have changed too.
- SlateJS has a [History](https://docs.slatejs.org/libraries/slate-history) module that tracks all the changes happening to the document. We could use this module to search the history and find the last inserted image node. This also isn’t completely reliable if it took longer for the image to upload and the user inserted more images in different parts of the document before the first upload completed.
- Currently, `Transform.insertNodes`’s API doesn’t return any information about the inserted nodes. If it could return the paths to the inserted nodes, we could use that to find the precise image node we should update. 

Since none of the above approaches work, we apply an `id` to the inserted image node (in Step (1)) and use the same `id` again to locate it when the image upload is complete. With that, our code for Step (3) looks like below &mdash; 

<pre><code class="language-javascript">axios
        .post("/upload", formData, {
          headers: {
            "content-type": "multipart/form-data",
          },
        })
        .then((response) => {
          const newImageEntry = Editor.nodes(editor, {
            match: (n) => n.id === id,
          });

          if (newImageEntry == null) {
            return;
          }

          Transforms.setNodes(
            editor,
            { isUploading: false, url: `/photos/${fileName}` },
            { at: newImageEntry[1] }
          );
        })
        .catch((error) => {
          // Fire another Transform.setNodes to set an upload failure state
          // on the image.        
        });
</code></pre>

With the implementation of all three steps complete, we are ready to test the image upload end to end.

{{< vimeo id="534655724" caption="Image upload working end-to-end" breakout="true" >}}

With that, we’ve wrapped up Images for our editor. Currently, we show a loading state of the same size irrespective of the image. This could be a jarring experience for the user if the loading state is replaced by a drastically smaller or bigger image when the upload completes. A good follow up to the upload experience is getting the image dimensions before the upload and showing a placeholder of that size so that transition is seamless. The hook we add above could be extended to support other media types like video or documents and render those types of nodes as well.

## Conclusion

In this article, we have built a WYSIWYG Editor that has a basic set of functionalities and some micro user-experiences like link detection, in-place link editing and image caption editing that helped us go deeper with SlateJS and concepts of Rich Text Editing in general. If this problem space surrounding Rich Text Editing or Word Processing interests you, some of the cool problems to go after could be:

- Collaboration
- A richer text editing experience that supports text alignments, inline images, copy-paste, changing font and text colors etc.
- Importing from popular formats like Word documents and Markdown.

If you want to learn more SlateJS, here are some links that might be helpful.

- [SlateJS Examples](https://www.slatejs.org/examples/richtext)  
A lot of examples that go beyond the basics and build functionalities that are usually found in Editors like Search & Highlight, Markdown Preview and Mentions.
- [API Docs](https://docs.slatejs.org/api/transforms)  
Reference to a lot of helper functions exposed by SlateJS that one might want to keep handy when trying to perform complex queries/transformations on SlateJS objects.

Lastly, SlateJS’s [Slack Channel](https://slate-slack.herokuapp.com/) is a very active community of web developers building Rich Text Editing applications using SlateJS and a great place to learn more about the library and get help if needed.

{{< signature "vf, il" >}}
