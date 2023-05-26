---
title: 'Adding A Commenting System To A WYSIWYG Editor'
slug: commenting-system-wysiwyg-editor
author: shalabh-vyas
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec39e154-d3d3-4a12-91fd-f0c068cd5247/commenting-system-wysiwyg-editor.jpg
date: 2021-05-28T11:00:00.000Z
summary: >-
  In this article, we’ll be re-using the foundational WYSIWYG Editor built in the <a href="https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/">first article</a> to build a commenting system for a WYSIWYG Editor that enables users to select text inside a document and share their comments on it. We’ll also be bringing in <a href="https://recoiljs.org/">RecoilJS</a> for state management in the UI application. (The code for the system we build here is available on a Github <a href="https://github.com/shalabhvyas/wysiwyg-editor">repository</a> for reference.)
description: >-
  In this article, we’ll be re-using the foundational WYSIWYG Editor built in the <a href="https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/">first article</a> to build a commenting system for a WYSIWYG Editor that enables users to select text inside a document and share their comments on it. Let’s dig in!
categories:
  - Tools
  - JavaScript
---

In recent years, we’ve seen Collaboration penetrate a lot of digital workflows and use-cases across many professions. Just within the Design and Software Engineering community, we see designers collaborate on design artifacts using tools like [Figma](https://www.figma.com/collaboration/), teams doing Sprint and Project Planning using tools like [Mural](https://www.mural.co/?) and interviews being conducted using [CoderPad](https://coderpad.io/). All these tools are constantly aiming to bridge the gap between an online and a physical world experience of executing these workflows and making the collaboration experience as rich and seamless as possible.

For the majority of the Collaboration Tools like these, the ability to share opinions with one another and have discussions about the same content is a must-have. A Commenting System that enables collaborators to annotate parts of a document and have conversations about them is at the heart of this concept. Along with building one for text in a WYSIWYG Editor, the article tries to engage the readers into how we try to weigh the pros and cons and attempt to find a balance between application complexity and user experience when it comes to building features for WYSIWYG Editors or Word Processors in general.

## Representing Comments In Document Structure

In order to find a way to represent comments in a rich text document’s data structure, let’s look at a few scenarios under which comments could be created inside an editor.

- Comments created over text that has no styles on it (basic scenario);
- Comments created over text that may be bold/italic/underlined, and so on;
- Comments that overlap each other in some way (partial overlap where two comments share only a few words or fully-contained where one comment’s text is fully contained within text of another comment);
- Comments created over text inside a link (special because links are nodes themselves in our document structure);
- Comments that span multiple paragraphs (special because paragraphs are nodes in our document structure and comments are applied to text nodes which are paragraph’s children).

Looking at the above use-cases, it seems like comments in the way they can come up in a rich text document are very similar to character styles (bold, italics etc). They can overlap with each other, go over text in other types of nodes like links and even span multiple parent nodes like paragraphs.

For this reason, we use the same method to represent comments as we do for character styles, i.e. “Marks” (as they are so called in SlateJS terminology). Marks are just regular properties on nodes &mdash; speciality being that Slate’s API around marks (`Editor.addMark` and `Editor.removeMark`) handles changing of the node hierarchy as multiple marks get applied to the same range of text. This is extremely useful to us as we deal with a lot of different combinations of overlapping comments.

### Comment Threads As Marks

Whenever a user selects a range of text and tries to insert a comment, technically, they’re starting a new comment thread for that text range. Because we would allow them to insert a comment and later replies to that comment, we treat this event as a new comment thread insertion in the document.

The way we represent comment threads as marks is that each comment thread is represented by a mark named as `commentThread_threadID` where `threadID` is a unique ID we assign to each comment thread.  So, if the same range of text has two comment threads over it, it would have two properties set to the `true` &mdash; `commentThread_thread1` and `commentThread_thread2`. This is where comment threads are very similar to character styles since if the same text was bold and italic, it would have both the properties set to `true` &mdash; `bold` and `italic`.

Before we dive into actually setting this structure up, it’s worth looking at how the text nodes change as comment threads get applied to them. The way this works (as it does with any mark) is that when a mark property is being set on the selected text, Slate’s [Editor.addMark](https://github.com/ianstormtaylor/slate/blob/228f4fa94f61f42ca41feae2b3029ebb570e0480/packages/slate/src/create-editor.ts#L92) API would split the text node(s) if needed such that in the resulting structure, text nodes are set up in a way that each text node has the exact same value of the mark.

To understand this better, take a look at the following three examples that show the before-and-after state of the text nodes once a comment thread is inserted on the selected text:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca21103b-cd8c-4868-8240-db95ceafb0ff/1-structure-uncommented-textt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca21103b-cd8c-4868-8240-db95ceafb0ff/1-structure-uncommented-textt.png" width="800" height="197" sizes="100vw" caption="A text node getting split into three as a comment thread mark is inserted in the middle of the text. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca21103b-cd8c-4868-8240-db95ceafb0ff/1-structure-uncommented-textt.png'>Large preview</a>)" alt="Illustration showing how text node is split with a basic comment thread insertion" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8be36e26-f239-40a0-8393-f20875bf32b2/2-structure-partial-overlap.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8be36e26-f239-40a0-8393-f20875bf32b2/2-structure-partial-overlap.png" width="800" height="323" sizes="100vw" caption="Adding a comment thread over ‘text has’ creates two new text nodes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8be36e26-f239-40a0-8393-f20875bf32b2/2-structure-partial-overlap.png'>Large preview</a>)" alt="Illustration showing how text node is split in case of a partial overlap of comment threads" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f3d6f6-557b-4b43-80c9-0b2db1e490c7/3-structure-thread-links.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f3d6f6-557b-4b43-80c9-0b2db1e490c7/3-structure-thread-links.png" width="800" height="470" sizes="100vw" caption="Adding a comment thread over ‘has link’ splits the text node inside the link too. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f3d6f6-557b-4b43-80c9-0b2db1e490c7/3-structure-thread-links.png'>Large preview</a>)" alt="Illustration showing how text node is split in case of a partial overlap of comment threads with links" >}}

{{% feature-panel %}}

## Highlighting Commented Text

Now that we know how we are going to represent comments in the document structure, let’s go ahead and add a few to the example document from the [first article](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/) and configure the editor to actually show them as highlighted. Since we will have a lot of utility functions to deal with comments in this article, we create a `EditorCommentUtils` module that will house all these utils. To start with, we create a function that creates a mark for a given comment thread ID. We then use that to insert a few comment threads in our `ExampleDocument`.

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

const COMMENT_THREAD_PREFIX = "commentThread_";

export function getMarkForCommentThreadID(threadID) {
  return `${COMMENT_THREAD_PREFIX}${threadID}`;
}</code></pre>

Below image underlines in red the ranges of text that we have as example comment threads added in the next code snippet. Note that the text ‘Richard McClintock’ has two comment threads that overlap each other. Specifically, this is a case of one comment thread being fully contained inside another.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f785c2a-4d29-4878-8c17-bce30b0cc6ee/highlight-comment-before.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f785c2a-4d29-4878-8c17-bce30b0cc6ee/highlight-comment-before.png" width="800" height="322" sizes="100vw" caption="Text ranges that would be commented upon underlined in red. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f785c2a-4d29-4878-8c17-bce30b0cc6ee/highlight-comment-before.png'>Large preview</a>)" alt="Picture showing which text ranges in the document are going to be commented upon - one of them being fully contained in another." >}}

<div class="break-out">

<pre><code class="language-javascript"># src/utils/ExampleDocument.js
import { getMarkForCommentThreadID } from "../utils/EditorCommentUtils";
import { v4 as uuid } from "uuid";

const exampleOverlappingCommentThreadID = uuid();

const ExampleDocument = [
   ...
   {
        text: "Lorem ipsum",
        [getMarkForCommentThreadID(uuid())]: true,
   },
   ...
   {
        text: "Richard McClintock",
        // note the two comment threads here.
        [getMarkForCommentThreadID(uuid())]: true,
        [getMarkForCommentThreadID(exampleOverlappingCommentThreadID)]: true,
   },
   {
        text: ", a Latin scholar",
        [getMarkForCommentThreadID(exampleOverlappingCommentThreadID)]: true,
   },
   ...
];</code></pre>
</div>

We focus on the UI side of things of a Commenting System in this article so we assign them IDs in the example document directly using the npm package [uuid](https://www.npmjs.com/package/uuid). Very likely that in a production version of an editor, these IDs are created by a backend service.

We now focus on tweaking the editor to show these text nodes as highlighted. In order to do that, when rendering text nodes, we need a way to tell if it has comment threads on it. We add a util `getCommentThreadsOnTextNode` for that. We build on the `StyledText` component that we created in the first article to handle the case where it may be trying to render a text node with comments on. Since we have some more functionality coming that would be added to commented text nodes later, we create a component `CommentedText` that renders the commented text. `StyledText` will check if the text node it’s trying to render has any comments on it. If it does, it renders `CommentedText`. It uses a util `getCommentThreadsOnTextNode` to deduce that.

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

export function getCommentThreadsOnTextNode(textNode) {
  return new Set(
     // Because marks are just properties on nodes,
    // we can simply use Object.keys() here.
    Object.keys(textNode)
      .filter(isCommentThreadIDMark)
      .map(getCommentThreadIDFromMark)
  );
}

export function getCommentThreadIDFromMark(mark) {
  if (!isCommentThreadIDMark(mark)) {
    throw new Error("Expected mark to be of a comment thread");
  }
  return mark.replace(COMMENT_THREAD_PREFIX, "");
}

function isCommentThreadIDMark(mayBeCommentThread) {
  return mayBeCommentThread.indexOf(COMMENT_THREAD_PREFIX) === 0;
}</code></pre>

The [first article](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/) built a component `StyledText` that renders text nodes (handling character styles and so on). We extend that component to use the above util and render a `CommentedText` component if the node has comments on it.

<pre><code class="language-javascript"># src/components/StyledText.js

import { getCommentThreadsOnTextNode } from "../utils/EditorCommentUtils";

export default function StyledText({ attributes, children, leaf }) {
  ...

  const commentThreads = getCommentThreadsOnTextNode(leaf);

  if (commentThreads.size &gt; 0) {
    return (
      &lt;CommentedText
      {...attributes}
     // We use commentThreads and textNode props later in the article.
      commentThreads={commentThreads}
      textNode={leaf}
      &gt;
        {children}
      &lt;/CommentedText&gt;
    );
  }

  return &lt;span {...attributes}&gt;{children}&lt;/span&gt;;
}</code></pre>

Below is the implementation of `CommentedText` that renders the text node and attaches the CSS that shows it as highlighted.

<pre><code class="language-javascript"># src/components/CommentedText.js

import "./CommentedText.css";

import classNames from "classnames";

export default function CommentedText(props) {
  const { commentThreads, ...otherProps } = props;
  return (
    &lt;span
      {...otherProps}
      className={classNames({
        comment: true,
      })}
    &gt;
      {props.children}
    &lt;/span&gt;
  );
}

# src/components/CommentedText.css

.comment {
  background-color: #feeab5;
}</code></pre>

With all of the above code coming together, we now see text nodes with comment threads highlighted in the editor.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a54ada8-f9fc-4cd6-b3b0-8dbbd9c11b45/highlight-comment-after.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a54ada8-f9fc-4cd6-b3b0-8dbbd9c11b45/highlight-comment-after.png" width="800" height="336" sizes="100vw" caption="Commented text nodes appear as highlighted after comment threads have been inserted. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a54ada8-f9fc-4cd6-b3b0-8dbbd9c11b45/highlight-comment-after.png'>Large preview</a>)" alt="Commented text nodes appears as highlighted after comment threads have been inserted" >}}

**Note**: *The users currently cannot tell if certain text has overlapping comments on it. The entire highlighted text range looks like a single comment thread. We address that later in the article where we introduce the concept of active comment thread which lets users select a specific comment thread and be able to see its range in the editor.*

## UI Storage For Comments

Before we add the functionality that enables a user to insert new comments, we first setup a UI state to hold our comment threads. In this article, we use [RecoilJS](https://recoiljs.org/) as our state management library to store comment threads, comments contained inside the threads and other metadata like creation time, status, comment author etc. Let’s add Recoil to our application:

<pre><code class="language-bash">&gt; yarn add recoil</code></pre>

We use Recoil [atoms](https://recoiljs.org/docs/basic-tutorial/atoms) to store these two data structures. If you’re not familiar with Recoil, atoms are what hold the application state. For different pieces of application state, you’d usually want to set up different atoms. [Atom Family](https://recoiljs.org/docs/api-reference/utils/atomFamily) is a collection of atoms &mdash; it can be thought to be a `Map` from a unique key identifying the atom to the atoms themselves. It’s worth going through [core concepts](https://recoiljs.org/docs/introduction/core-concepts/) of Recoil at this point and familiarizing ourselves with them.

For our use case, we store comment threads as an Atom family and then wrap our application in a `RecoilRoot` component. [`RecoilRoot`](https://recoiljs.org/docs/api-reference/core/RecoilRoot) is applied to provide the context in which the atom values are going to be used. We create a separate module `CommentState` that holds our Recoil atom definitions as we add more atom definitions later in the article.

<pre><code class="language-javascript"># src/utils/CommentState.js

import { atom, atomFamily } from "recoil";

export const commentThreadsState = atomFamily({
  key: "commentThreads",
  default: [],
});

export const commentThreadIDsState = atom({
  key: "commentThreadIDs",
  default: new Set([]),
});</code></pre>

Worth calling out few things about these atom definitions:

- Each atom/atom family is uniquely identified by a `key` and can be set up with a default value.
- As we build further in this article, we are going to need a way to iterate over all the comment threads which would basically mean needing a way to iterate over `commentThreadsState` atom family. At the time of writing this article, the way to do that with Recoil is to set up another atom that holds all the IDs of the atom family. We do that with `commentThreadIDsState` above. Both these atoms would have to be kept in sync whenever we add/delete comment threads.

We add a `RecoilRoot` wrapper in our root `App` component so we can use these atoms later. Recoil’s documentation also provides a helpful [Debugger](https://recoiljs.org/docs/guides/dev-tools/#observing-all-state-changes) component that we take as it is and drop into our editor. This component will leave `console.debug` logs to our Dev console as Recoil atoms are updated in real-time.

<pre><code class="language-javascript"># src/components/App.js

import { RecoilRoot } from "recoil";

export default function App() {
  ...

  return (
    &lt;RecoilRoot&gt;
      &gt;
         ...
        &lt;Editor document={document} onChange={updateDocument} /&gt;
    
    &lt;/RecoilRoot&gt;
  );
}</code></pre>

<pre><code class="language-javascript"># src/components/Editor.js

export default function Editor({ ... }): JSX.Element {
  .....

  return (
    &lt;&gt;
      &lt;Slate&gt;
         .....
      &lt;/Slate&gt;
      &lt;DebugObserver /&gt;
   &lt;/&gt;
);

function DebugObserver(): React.Node {
   // see API link above for implementation.
}</code></pre>

We also need to need to add code that initializes our atoms with the comment threads that already exist on the document (the ones we added to our example document in the previous section, for instance). We do that at a later point when we build the Comments Sidebar that needs to read all the comment threads in a document.

At this point, we load our application, make sure there are no errors pointing to our Recoil setup and move forward.

{{% ad-panel-leaderboard %}}

## Adding New Comments

In this section, we add a button to the toolbar that lets the user add comments (viz. create a new comment thread) for the selected text range. When the user selects a text range and clicks on this button, we need to do the below:

1. Assign a unique ID to the new comment thread being inserted.
2. Add a new mark to Slate document structure with the ID so the user sees that text highlighted.
3. Add the new comment thread to Recoil atoms we created in the previous section.

Let’s add a util function to `EditorCommentUtils` that does #1 and #2.

<div class="break-out">

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

import { Editor } from "slate";
import { v4 as uuidv4 } from "uuid";

export function insertCommentThread(editor, addCommentThreadToState) {
    const threadID = uuidv4();
    const newCommentThread = {
        // comments as added would be appended to the thread here.
        comments: [],
        creationTime: new Date(),
        // Newly created comment threads are OPEN. We deal with statuses
        // later in the article.
        status: "open",
    };
    addCommentThreadToState(threadID, newCommentThread);
    Editor.addMark(editor, getMarkForCommentThreadID(threadID), true);
    return threadID;
}</code></pre>
</div>

By using the concept of marks to store each comment thread as its own mark, we’re able to simply use the `Editor.addMark` API to add a new comment thread on the text range selected. This call alone handles all the different cases of adding comments &mdash; some of which  we described in the earlier section &mdash; partially overlapping comments, comments inside/overlapping links, comments over bold/italic text, comments spanning paragraphs and so on. This API call adjusts the node hierarchy to create as many new text nodes as needed to handle these cases.

`addCommentThreadToState` is a callback function that handles step #3 &mdash; adding the new comment thread to Recoil atom . We implement that next as a custom callback hook so that it’s re-usable. This callback needs to add the new comment thread to both the atoms &mdash; `commentThreadsState` and `commentThreadIDsState`. To be able to do this, we use the [`useRecoilCallback`](https://recoiljs.org/docs/api-reference/core/useRecoilCallback) hook. This hook can be used to construct a callback which gets a few things that can be used to read/set atom data. The one we’re interested in right now is the `set` function which can be used to update an atom value as `set(atom, newValueOrUpdaterFunction)`.

<div class="break-out">

<pre><code class="language-javascript"># src/hooks/useAddCommentThreadToState.js

import {
  commentThreadIDsState,
  commentThreadsState,
} from "../utils/CommentState";

import { useRecoilCallback } from "recoil";

export default function useAddCommentThreadToState() {
  return useRecoilCallback(
    ({ set }) =&gt; (id, threadData) =&gt; {
      set(commentThreadIDsState, (ids) =&gt; new Set([...Array.from(ids), id]));
      set(commentThreadsState(id), threadData);
    },
    []
  );
}</code></pre>
</div>

The first call to `set` adds the new ID to the existing set of comment thread IDs and returns the new `Set`(which becomes the new value of the atom).

In the second call, we get the atom for the ID from the atom family &mdash; `commentThreadsState` as `commentThreadsState(id)` and then set the `threadData` to be its value. `atomFamilyName(atomID)` is how Recoil lets us access an atom from its atom family using the unique key. Loosely speaking, we could say that if `commentThreadsState` was a javascript Map, this call is basically &mdash; `commentThreadsState.set(id, threadData)`. 

Now that we have all this code setup to handle insertion of a new comment thread to the document and Recoil atoms, lets add a button to our toolbar and wire it up with the call to these functions.

<div class="break-out">

<pre><code class="language-javascript"># src/components/Toolbar.js

import { insertCommentThread } from "../utils/EditorCommentUtils";
import useAddCommentThreadToState from "../hooks/useAddCommentThreadToState";

export default function Toolbar({ selection, previousSelection }) {
  const editor = useEditor();
  ...

  const addCommentThread = useAddCommentThreadToState();

  const onInsertComment = useCallback(() =&gt; {
    const newCommentThreadID = insertCommentThread(editor, addCommentThread);
  }, [editor, addCommentThread]);
 
return (
    &lt;div className="toolbar"&gt;
       ...
      &lt;ToolBarButton
        isActive={false}
        label={&lt;i className={`bi ${getIconForButton("comment")}`} /&gt;}
        onMouseDown={onInsertComment}
      /&gt;
    &lt;/div&gt;
  );
}</code></pre>
</div>

**Note**: *We use `onMouseDown` and not `onClick` which would have made the editor lose focus and selection to become `null`. We’ve discussed that in a little more detail in the link insertion section of the [first article](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/).*

In the below example, we see the insertion in action for a simple comment thread and an overlapping comment thread with links. Notice how we get updates from Recoil Debugger confirming our state is getting updated correctly. We also verify that new text nodes are created as threads are being added to the document.

{{< vimeo id="554464535" caption="Inserting a comment thread splits the text node making the commented text its own node." breakout="true" >}}

{{< vimeo id="554465021" caption="More text nodes get created as we add overlapping comments." breakout="true" >}}

## Overlapping Comments

Before we proceed with adding more features to our commenting system, we need to make some decisions around how we are going to deal with overlapping comments and their different combinations in the editor. To see why we need that, let’s take a sneak peek into how a Comment Popover works &mdash; a functionality we will build later in the article. When a user clicks on a certain text with comment thread(s) on it, we ‘select’ a comment thread and show a popover where the user can add comments to that thread.

{{< vimeo id="554465973" caption="When the user clicks on a text node with overlapping comments, the editor needs to decide which comment thread to select." breakout="true" >}}

As you can tell from the above video, the word ‘designers’ is now part of three comment threads. So we have two comment threads that overlap with each other over a word. And both these comment threads (#1 and #2) are fully contained inside a longer comment thread text range (#3). This raises a few questions:

1. Which comment thread should we select and show when the user clicks on the word ‘designers’?
2. Based on how we decide to tackle the above question, would we ever have a case of overlap where clicking on any word would never activate a certain comment thread and the thread cannot be accessed at all?

This implies in the case of overlapping comments, the most important thing to consider is &mdash; once the user has inserted a comment thread, would there be a way for them to be able to select that comment thread in the future by clicking on some text inside it? If not, we probably don’t want to allow them to insert it in the first place. To ensure this principle is respected **most** of the time in our editor, we introduce two rules regarding overlapping comments and implement them in our editor.

Before we define those rules, it’s worth calling out that different editors and word processors have different approaches when it comes to overlapping comments. To keep things simple, some editors do not allow overlapping comments whatsoever. In our case, we try to find a middle ground by not allowing too complicated cases of overlaps but still allowing overlapping comments so that users could have a richer Collaboration and Review experience.

### Shortest Comment Range Rule

This rule helps us answer the question #1 from above as to which comment thread to select if a user clicks on a text node that has multiple comment threads on it. The rule is:

<blockquote>“If the user clicks on text that has multiple comment threads on it, we find the comment thread of the shortest text range and select that.”</blockquote>

Intuitively, it makes sense to do this so that the user always has a way to get to the innermost comment thread that is fully contained inside another comment thread. For other conditions (partial overlap or no-overlap), there should be some text that has only one comment thread on it so it should be easy to use that text in order to select that comment thread. It’s the case of a full (or a *dense*) overlap of threads and why we need this rule.

Let’s look at a rather complex case of overlap that allows us to use this rule and ‘do the right thing’ when selecting the comment thread.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53fa0167-b5b0-4a19-9857-1e34b556dcf9/shortest-length-rule.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53fa0167-b5b0-4a19-9857-1e34b556dcf9/shortest-length-rule.png" width="800" height="328" sizes="100vw" caption="Following the Shortest Comment Thread Rule, clicking on ‘B’ selects comment thread #1. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53fa0167-b5b0-4a19-9857-1e34b556dcf9/shortest-length-rule.png'>Large preview</a>)" alt="Example showing three comment threads overlapping each other in a way that the only way to select a comment thread is using the shortest length rule." >}}

In the above example, the user inserts the following comment threads in that order:

1. Comment Thread #1 over character ‘B’ (length = 1).
2. Comment Thread #2 over ‘AB’ (length = 2).
3. Comment Thread #3 over ‘BC’ (length = 2).

At the end of these insertions, because of the way Slate splits the text nodes with marks, we will have three text nodes &mdash; one for each character. Now, if the user clicks on ‘B’, going by the shortest length rule, we select thread #1 as it is the shortest of the three in length. If we don’t do that, we wouldn’t have a way to select Comment Thread #1 ever since it is only one-character in length and also a part of two other threads.

Although this rule makes it easy to surface shorter-length comment threads, we could run into situations where longer comment threads become inaccessible since all the characters contained in them are part of some other shorter comment thread. Let’s look at an example for that.

Let’s assume we have 100 characters (say, character ‘A’ typed 100 times that is) and the user inserts comment threads in the following order:

1. Comment Thread # 1 of range 20,80
2. Comment Thread # 2 of range 0,50
3. Comment Thread # 3 of range 51,100

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b0cd9e6-0722-4565-abf6-58a32fcb3f70/shortest-length-rule-exception.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b0cd9e6-0722-4565-abf6-58a32fcb3f70/shortest-length-rule-exception.png" width="800" height="352" sizes="100vw" caption="All text under Comment Thread #1 is also part of some other comment thread shorter than #1. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b0cd9e6-0722-4565-abf6-58a32fcb3f70/shortest-length-rule-exception.png'>Large preview</a>)" alt="Example showing shortest length rule making a comment thread non-selectable as all of its text is covered by shorter comment threads." >}}

As you can see in the above example, if we follow the rule we just described here, clicking on any character between #20 and #80, would always select threads #2 or #3 since they are shorter than #1 and hence #1 would not be selectable. Another scenario where this rule can leave us undecided as to which comment thread to select is when there are more than one comment threads of the same shortest length on a text node.

For such combination of overlapping comments and many other such combinations that one could think of where following this rule makes a certain comment thread inaccessible by clicking on text, we build a Comments Sidebar later in this article which gives user a view of all the comment threads present in the document so they can click on those threads in the sidebar and activate them in the editor to see the range of the comment. We still would want to have this rule and implement it as it should cover a lot of overlap scenarios except for the less-likely examples we cited above. We put in all this effort around this rule primarily because seeing highlighted text in the editor and clicking on it to comment is a more intuitive way of accessing a comment on text than merely using a list of comments in the sidebar.

### Insertion Rule

The rule is:

<blockquote>“If the text user has selected and is trying to comment on is already fully covered by comment thread(s), don’t allow that insertion.”</blockquote>

This is so because if we did allow this insertion, each character in that range would end up having at least two comment threads (one existing and another the new one we just allowed) making it difficult for us to determine which one to select when the user clicks on that character later.

Looking at this rule, one might wonder why we need it in the first place if we already have the Shortest Comment Range Rule that allows us to select the smallest text range. Why not allow all combinations of overlaps if we can use the first rule to deduce the right comment thread to show? As some of the examples we’ve discussed earlier, the first rule works for a lot of scenarios but not all of them. With the Insertion Rule, we try to minimize the number of scenarios where the first rule cannot help us and we have to fallback on the Sidebar as the only way for the user to access that comment thread. Insertion Rule also prevents exact-overlaps of comment threads. This rule is commonly implemented by a lot of popular editors.

Below is an example where if this rule didn’t exist, we would allow the Comment Thread #3 and then as a result of the first rule, #3 would not be accessible since it would become the longest in length.

{{< vimeo id="554477344" caption="Insertion Rule not allowing a third comment thread whose entire text range is covered by two other comment threads." breakout="true" >}}

**Note**: *Having this rule doesn’t mean we would never have fully contained overlapping comments. The tricky thing about overlapping comments is that despite the rules, the order in which comments are inserted can still leave us in a state we didn’t want the overlap to be in. Referring back to our example of the comments on the word ‘designers’ earlier, the longest comment thread inserted there was the last one to be added so the Insertion Rule would allow it and we end up with a fully contained situation &mdash; #1 and #2 contained inside #3. That’s fine because the Shortest Comment Range Rule would help us out there.*

We’ll implement the Shortest Comment Range Rule in the <a href="#implementing-shortest-comment-range-rule">next section</a> where we implement selecting of comment threads. Since we now have a toolbar button to insert comments, we can implement the Insertion Rule right away by checking the rule when the user has some text selected. If the rule is not satisfied, we would disable the Comment button so users cannot insert a new comment thread on the selected text. Let’s get started!

<div class="break-out">

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

export function shouldAllowNewCommentThreadAtSelection(editor, selection) {
  if (selection == null || Range.isCollapsed(selection)) {
    return false;
  }

  const textNodeIterator = Editor.nodes(editor, {
    at: selection,
    mode: "lowest",
  });

  let nextTextNodeEntry = textNodeIterator.next().value;
  const textNodeEntriesInSelection = [];
  while (nextTextNodeEntry != null) {
    textNodeEntriesInSelection.push(nextTextNodeEntry);
    nextTextNodeEntry = textNodeIterator.next().value;
  }

  if (textNodeEntriesInSelection.length === 0) {
    return false;
  }

  return textNodeEntriesInSelection.some(
    ([textNode]) =&gt; getCommentThreadsOnTextNode(textNode).size === 0
  );
}</code></pre>
</div>

The logic in this function is relatively straightforward.

- If the user’s selection is a blinking caret, we don’t allow inserting a comment there as no text has been selected.
- If the user’s selection is not a collapsed one, we find all the text nodes in the selection. Note the use of the `mode: lowest` in the call to `Editor.nodes` (a helper function by SlateJS) that helps us select all the text nodes since text nodes are really the leaves of the document tree.
- If there is at least one text node that has no comment threads on it, we may allow the insertion. We use the util `getCommentThreadsOnTextNode` we wrote earlier here.

We now use this util function inside the toolbar to control the disabled state of the button.

<div class="break-out">

<pre><code class="language-javascript"># src/components/Toolbar.js

export default function Toolbar({ selection, previousSelection }) {
  const editor = useEditor();
  ....

  return (
   &lt;div className="toolbar"&gt;
     ....
    &lt;ToolBarButton
        isActive={false}
        disabled={!shouldAllowNewCommentThreadAtSelection(
          editor,
          selection
        )}
        label={&lt;i className={`bi ${getIconForButton("comment")}`} /&gt;}
        onMouseDown={onInsertComment}
      /&gt;
  &lt;/div&gt;
);</code></pre>
</div>

Let’s test the implementation of the rule by recreating our example above.

{{< vimeo id="554481310" caption="Insertion button in the toolbar disabled as user tries to insert comment over text range already fully covered by other comments." breakout="true" >}}

A fine user experience detail to call out here is that while we disable the toolbar button if the user has selected the entire line of text here, it doesn’t complete the experience for the user. The user may not fully understand why the button is disabled and is likely to get confused that we’re not responding to their intent to insert a comment thread there. We address this later as Comment Popovers are built such that even if the toolbar button is disabled, the popover for one of the comment threads would show up and the user would still be able to leave comments.

Let’s also test a case where there is some uncommented text node and the rule allows inserting a new comment thread.

{{< vimeo id="554481468" caption="Insertion Rule allowing insertion of comment thread when there is some uncommented text within user’s selection." breakout="true" >}}

## Selecting Comment Threads

In this section, we enable the feature where the user clicks on a commented text node and we use the Shortest Comment Range Rule to determine which comment thread should be selected. The steps in the process are:

1. Find the shortest comment thread on the commented text node that user clicks on.
2. Set that comment thread to be the active comment thread. (We create a new Recoil atom which will be the source of truth for this.)
3. The commented text nodes would listen to the Recoil state and if they are part of the active comment thread, they’d highlight themselves differently. That way, when the user clicks on the comment thread, the entire text range stands out as all the text nodes will update their highlight color.

### Step 1: Implementing Shortest Comment Range Rule

Let’s start with Step #1 which is basically implementing the Shortest Comment Range Rule. The goal here is to find the comment thread of the shortest range at the text node on which the user clicked. To find the shortest length thread, we need to compute the length of all the comment threads at that text node. Steps to do this are:

1. Get all the comment threads at the text node in question.
2. Traverse in either direction from that text node and keep updating the thread lengths being tracked.
3. Stop the traversal in a direction when we’ve reached one of the below edges:
  - An uncommented text node (implying we’ve reached furthermost start/end edge of all the comment threads we’re tracking).
  - A text node where all the comment threads we are tracking have reached an edge (start/end).
  - There are no more text nodes to traverse in that direction (implying we’ve either reached the start or the end of the document or a non-text node).

Since the traversals in forward and reverse direction are functionally the same, we’re going to write a helper function `updateCommentThreadLengthMap` that basically takes a text node iterator. It will keep calling the iterator and keep updating the tracking thread lengths. We’ll call this function twice &mdash; once for forward and once for backward direction. Let’s write our main utility function that will use this helper function.

<div class="break-out">

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

export function getSmallestCommentThreadAtTextNode(editor, textNode) {

  const commentThreads = getCommentThreadsOnTextNode(textNode);
  const commentThreadsAsArray = [...commentThreads];

  let shortestCommentThreadID = commentThreadsAsArray[0];

  const reverseTextNodeIterator = (slateEditor, nodePath) =&gt;
    Editor.previous(slateEditor, {
      at: nodePath,
      mode: "lowest",
      match: Text.isText,
    });

  const forwardTextNodeIterator = (slateEditor, nodePath) =&gt;
    Editor.next(slateEditor, {
      at: nodePath,
      mode: "lowest",
      match: Text.isText,
    });

  if (commentThreads.size &gt; 1) {

    // The map here tracks the lengths of the comment threads.
    // We initialize the lengths with length of current text node
    // since all the comment threads span over the current text node
    // at the least.
    const commentThreadsLengthByID = new Map(
      commentThreadsAsArray.map((id) =&gt; [id, textNode.text.length])
    );


    // traverse in the reverse direction and update the map
    updateCommentThreadLengthMap(
      editor,
      commentThreads,
      reverseTextNodeIterator,
      commentThreadsLengthByID
    );

    // traverse in the forward direction and update the map
    updateCommentThreadLengthMap(
      editor,
      commentThreads,
      forwardTextNodeIterator,
      commentThreadsLengthByID
    );

    let minLength = Number.POSITIVE_INFINITY;


    // Find the thread with the shortest length.
    for (let [threadID, length] of commentThreadsLengthByID) {
      if (length &lt; minLength) {
        shortestCommentThreadID = threadID;
        minLength = length;
      }
    }
  }

  return shortestCommentThreadID;
}</code></pre>
</div>

The steps we listed out are all covered in the above code. The comments should help follow how the logic flows there.

One thing worth calling out is how we created the traversal functions. We want to give a traversal function to `updateCommentThreadLengthMap` such that it can call it while it is iterating text node’s path and easily get the previous/next text node. To do that, Slate’s traversal utilities `Editor.previous` and `Editor.next` (defined in the [Editor](https://github.com/ianstormtaylor/slate/blob/0b0328b2d0a595d48905b41c6afcc4f65bc352c6/packages/slate/src/interfaces/editor.ts#L237) interface) are very helpful. Our iterators `reverseTextNodeIterator` and `forwardTextNodeIterator` call these helpers with two options `mode: lowest` and the match function `Text.isText` so we know we’re getting a text node from the traversal, if there is one.

Now we implement `updateCommentThreadLengthMap` which traverses using these iterators and updates the lengths we’re tracking.

<div class="break-out">

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

function updateCommentThreadLengthMap(
  editor,
  commentThreads,
  nodeIterator,
  map
) {
  let nextNodeEntry = nodeIterator(editor);

  while (nextNodeEntry != null) {
    const nextNode = nextNodeEntry[0];
    const commentThreadsOnNextNode = getCommentThreadsOnTextNode(nextNode);

    const intersection = [...commentThreadsOnNextNode].filter((x) =&gt;
      commentThreads.has(x)
    );

     // All comment threads we're looking for have already ended meaning
    // reached an uncommented text node OR a commented text node which
    // has none of the comment threads we care about.
    if (intersection.length === 0) {
      break;
    }


    // update thread lengths for comment threads we did find on this
    // text node.
    for (let i = 0; i &lt; intersection.length; i++) {
      map.set(intersection[i], map.get(intersection[i]) + nextNode.text.length);
    }


    // call the iterator to get the next text node to consider
    nextNodeEntry = nodeIterator(editor, nextNodeEntry[1]);
  }

  return map;
}
</code></pre>
</div>

One might wonder why do we wait until the `intersection` becomes `0` to stop iterating in a certain direction. Why can’t we just stop if we’re reached the edge of at least one comment thread &mdash; that would imply we’ve reached the shortest length in that direction, right? The reason we can’t do that is that we know that a comment thread can span over multiple text nodes and we wouldn’t know which of those text nodes did the user click on and we started our traversal from. We wouldn’t know the range of all comment threads in question without fully traversing to the farthest edges of the union of the text ranges of the comment threads in both the directions.

Check out the below example where we have two comment threads ‘A’ and ‘B’ overlapping each other in some way resulting into three text nodes 1,2 and 3 &mdash; #2 being the text node with the overlap.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4babfb22-4448-4706-8f29-ab11bf43800b/select-comment-thread-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4babfb22-4448-4706-8f29-ab11bf43800b/select-comment-thread-example.png" width="800" height="450" sizes="100vw" caption="Two comment threads overlapping over the word ‘text’. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4babfb22-4448-4706-8f29-ab11bf43800b/select-comment-thread-example.png'>Large preview</a>)" alt="Example of multiple comment threads overlapping on a text node." >}}

In this example, let’s assume we don’t wait for intersection to become 0 and just stop when we reach the edge of a comment thread. Now, if the user clicked on #2 and we start traversal in reverse direction, we’d stop at the start of text node #2 itself since that’s the start of the comment thread A. As a result, we might not compute the comment thread lengths correctly for A & B. With the implementation above traversing the farthest edges (text nodes 1,2, and 3), we should get B as the shortest comment thread as expected.

To see the implementation visually, below is a walkthrough with a slideshow of the iterations. We have two comment threads A and B that overlap each other over text node #3 and the user clicks on the overlapping text node #3.

{{< vimeo id="554484825" caption="Slideshow showing iterations in the implementation of Shortest Comment Thread Rule." breakout="true" >}}

### Steps 2 & 3: Maintaining State Of The Selected Comment Thread And Highlighting It

Now that we have the logic for the rule fully implemented, let’s update the editor code to use it. For that, we first create a Recoil atom that’ll store the active comment thread ID for us. We then update the `CommentedText` component to use our rule’s implementation.

<div class="break-out">

<pre><code class="language-javascript"># src/utils/CommentState.js

import { atom } from "recoil";

export const activeCommentThreadIDAtom = atom({
  key: "activeCommentThreadID",
  default: null,
});


# src/components/CommentedText.js

import { activeCommentThreadIDAtom } from "../utils/CommentState";
import classNames from "classnames";
import { getSmallestCommentThreadAtTextNode } from "../utils/EditorCommentUtils";
import { useRecoilState } from "recoil";

export default function CommentedText(props) {
 ....
const { commentThreads, textNode, ...otherProps } = props;
const [activeCommentThreadID, setActiveCommentThreadID] = useRecoilState(
    activeCommentThreadIDAtom
  );

  const onClick = () =&gt; {
    setActiveCommentThreadID(
      getSmallestCommentThreadAtTextNode(editor, textNode)
    );
  };

  return (
    &lt;span
      {...otherProps}
      className={classNames({
        comment: true,
        // a different background color treatment if this text node's
        // comment threads do contain the comment thread active on the
        // document right now.   
        "is-active": commentThreads.has(activeCommentThreadID),
      })}
      onClick={onClick}
    &gt;
      {props.children}
    &gl;/span&gt;
  );
}</code></pre>
</div>

This component uses `useRecoilState` that allows a component to subscribe to and also be able to set the value of Recoil atom. We need the subscriber to know if this text node is part of the active comment thread so it can style itself differently. Check out the screenshot below where the comment thread in the middle is active and we can see its range clearly.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4375dda-a6f9-40d7-9f88-bc19ffef04d0/select-comment-thread-range.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4375dda-a6f9-40d7-9f88-bc19ffef04d0/select-comment-thread-range.png" width="800" height="364" sizes="100vw" caption="Text node(s) under selected comment thread change in style and jump out. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4375dda-a6f9-40d7-9f88-bc19ffef04d0/select-comment-thread-range.png'>Large preview</a>)" alt="Example showing how text node(s) under selected comment thread jump out." >}}

Now that we have all the code in to make selection of comment threads work, let’s see it in action. To test our traversal code well, we test some straightforward cases of overlap and some edge cases like:

- Clicking on a commented text node at the start/end of the editor.
- Clicking on a commented text node with comment threads spanning multiple paragraphs.
- Clicking on a commented text node right before an image node.
- Clicking on a commented text node overlapping links.

{{< vimeo id="554486191" caption="Selecting shortest comment thread for different overlap combinations." breakout="true" >}}

As we now have a Recoil atom to track the active comment thread ID, one tiny detail to take care of is setting the newly created comment thread to be the active one when the user uses the toolbar button to insert a new comment thread. This enables us, in the next section, to show the comment thread popover immediately on insertion so the user can start adding comments right away.

<div class="break-out">

<pre><code class="language-javascript"># src/components/Toolbar.js

import useAddCommentThreadToState from "../hooks/useAddCommentThreadToState";
import { useSetRecoilState } from "recoil";

export default function Toolbar({ selection, previousSelection }) {
  ...
  const setActiveCommentThreadID = useSetRecoilState(activeCommentThreadIDAtom);
 .....
  const onInsertComment = useCallback(() =&gt; {
    const newCommentThreadID = insertCommentThread(editor, addCommentThread);
    setActiveCommentThreadID(newCommentThreadID);
  }, [editor, addCommentThread, setActiveCommentThreadID]);

 return &lt;div className='toolbar'&gt;
              ....
           &lt;/div&gt;;
};</code></pre>
</div>

**Note:** *The use of [`useSetRecoilState`](https://recoiljs.org/docs/api-reference/core/useSetRecoilState) here (a Recoil hook that exposes a setter for the atom but doesn’t subscribe the component to its value) is what we need for the toolbar in this case.*

## Adding Comment Thread Popovers

In this section, we build a Comment Popover that makes use of the concept of selected/active comment thread and shows a popover that lets the user add comments to that comment thread. Before we build it, let’s take a quick look at how it functions.

{{< vimeo id="554488598" caption="Preview of the Comment Popover Feature." breakout="true" >}}

When trying to render a Comment Popover close to the comment thread that is active, we run into some of the problems that we did in the first article with a Link Editor Menu. At this point, it is encouraged to read through the section in the [first article](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/) that builds a Link Editor and the selection issues we run into with that.

Let’s first work on rendering an empty popover component in the right place based on the what active comment thread is. The way popover would work is:

- **Comment Thread Popover** is rendered only when there is an active comment thread ID. To get that information, we listen to the Recoil atom we created in the previous section.
- When it does render, we find the text node at the editor’s selection and render the popover close to it.
- When the user clicks anywhere outside the popover, we set the active comment thread to be `null` thereby de-activating the comment thread and also making the popover disappear.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentThreadPopover.js

import NodePopover from "./NodePopover";
import { getFirstTextNodeAtSelection } from "../utils/EditorUtils";
import { useEditor } from "slate-react";
import { useSetRecoilState} from "recoil";

import {activeCommentThreadIDAtom} from "../utils/CommentState";

export default function CommentThreadPopover({ editorOffsets, selection, threadID }) {
  const editor = useEditor();
  const textNode = getFirstTextNodeAtSelection(editor, selection);
  const setActiveCommentThreadID = useSetRecoilState(
    activeCommentThreadIDAtom
  );

  const onClickOutside = useCallback(
    () =&gt; {},
    []
  );

  return (
    &lt;NodePopover
      editorOffsets={editorOffsets}
      isBodyFullWidth={true}
      node={textNode}
      className={"comment-thread-popover"}
      onClickOutside={onClickOutside}
    &gt;
      {`Comment Thread Popover for threadID:${threadID}`}
    &lt;/NodePopover&gt;
  );
}</code></pre>
</div>

Couple of things that should be called out for this implementation of the popover component:

- It takes the `editorOffsets` and the `selection` from the `Editor` component where it would be rendered. `editorOffsets` are the bounds of the Editor component so we could compute the position of the popover and `selection` could be current or previous selection in case the user used a toolbar button causing `selection` to become `null`. The section on the Link Editor from the first article linked above goes through these in detail.
- Since the `LinkEditor` from the first article and the `CommentThreadPopover` here, both render a popover around a text node, we’ve moved that common logic into a component `NodePopover` that handles rendering of the component aligned to the text node in question. Its implementation details are what `LinkEditor` component had in the first article.
- `NodePopover` takes a `onClickOutside` method as a prop that is called if the user clicks somewhere outside the popover. We implement this by attaching `mousedown` event listener to the `document` &mdash; as explained in detail in [this](https://www.smashingmagazine.com/2021/03/outside-focus-click-handler-react-component/) Smashing article on this idea.
- `getFirstTextNodeAtSelection` gets the first text node inside the user's selection which we use to render the popover against. The implementation of this function uses Slate’s helpers to find the text node.

<pre><code class="language-javascript"># src/utils/EditorUtils.js

export function getFirstTextNodeAtSelection(editor, selection) {
  const selectionForNode = selection ?? editor.selection;

  if (selectionForNode == null) {
    return null;
  }

  const textNodeEntry = Editor.nodes(editor, {
    at: selectionForNode,
    mode: "lowest",
    match: Text.isText,
  }).next().value;

  return textNodeEntry != null ? textNodeEntry[0] : null;
}</code></pre>

Let’s implement the `onClickOutside` callback that should clear the active comment thread. However, we have to account for the scenario when the comment thread popover is open and a certain thread is active and the user happens to click on another comment thread. In that case, we don’t want the `onClickOutside` to reset the active comment thread since the click event on the other `CommentedText` component should set the other comment thread to become active. We don’t want to interfere with that in the popover.

{{% ad-panel-leaderboard %}}

The way we do that is that is we find the Slate Node closest to the DOM node where the click event happened. If that Slate node is a text node and has comments on it, we skip resetting the active comment thread Recoil atom. Let’s implement it!

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentThreadPopover.js

const setActiveCommentThreadID = useSetRecoilState(activeCommentThreadIDAtom);

const onClickOutside = useCallback(
    (event) =&gt; {
      const slateDOMNode = event.target.hasAttribute("data-slate-node")
        ? event.target
        : event.target.closest('[data-slate-node]');

      // The click event was somewhere outside the Slate hierarchy.
      if (slateDOMNode == null) {
        setActiveCommentThreadID(null);
        return;
      }

      const slateNode = ReactEditor.toSlateNode(editor, slateDOMNode);

      // Click is on another commented text node =&gt; do nothing.
      if (
        Text.isText(slateNode) &&
        getCommentThreadsOnTextNode(slateNode).size &gt; 0
      ) {
        return;
      }

      setActiveCommentThreadID(null);
    },
    [editor, setActiveCommentThreadID]
  );</code></pre>
</div>

Slate has a helper method `toSlateNode` that returns the Slate node that maps to a DOM node or its closest ancestor if itself isn’t a Slate Node. The current [implementation](https://github.com/ianstormtaylor/slate/blob/1a4c67f5fad60b3a8df94c9a29568c02bfa1c18e/packages/slate-react/src/plugin/react-editor.ts#L367) of this helper throws an error if it can’t find a Slate node instead of returning `null`. We handle that above by checking the `null` case ourselves which is a very likely scenario if the user clicks somewhere outside the editor where Slate nodes don’t exist.

We can now update the `Editor` component to listen to the `activeCommentThreadIDAtom` and render the popover only when a comment thread is active.

<div class="break-out">

<pre><code class="language-javascript"># src/components/Editor.js

import { useRecoilValue } from "recoil";
import { activeCommentThreadIDAtom } from "../utils/CommentState";

export default function Editor({ document, onChange }): JSX.Element {

  const activeCommentThreadID = useRecoilValue(activeCommentThreadIDAtom);
  // This hook is described in detail in the first article
  const [previousSelection, selection, setSelection] = useSelection(editor);

  return (
    &lt;&gt;
               ...
              &lt;div className="editor" ref={editorRef}&gt;
                 ...
                {activeCommentThreadID != null ? (
                  &lt;CommentThreadPopover
                    editorOffsets={editorOffsets}
                    selection={selection ?? previousSelection}
                    threadID={activeCommentThreadID}
                  /&gt;
                ) : null}
             &lt;/div&gt;
               ...
    &lt;/&gt;
  );
}</code></pre>
</div>

Let’s verify that the popover loads at the right place for the right comment thread and does clear the active comment thread when we click outside.

{{< vimeo id="554492643" caption="Comment Thread Popover correctly loads for the selected comment thread." breakout="true" >}}

We now move on to enabling users to add comments to a comment thread and seeing all the comments of that thread in the popover. We are going to use the Recoil atom family &mdash; `commentThreadsState` we created earlier in the article for this.

The comments in a comment thread are stored on the `comments` array. To enable adding a new comment, we render a Form input that allows the user to enter a new comment. While the user is typing out the comment, we maintain that in a local state variable &mdash; `commentText`. On the click of the button, we append the comment text as the new comment to the `comments` array.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentThreadPopover.js

import { commentThreadsState } from "../utils/CommentState";
import { useRecoilState } from "recoil";

import Button from "react-bootstrap/Button";
import Form from "react-bootstrap/Form";

export default function CommentThreadPopover({
  editorOffsets,
  selection,
  threadID,
}) {

  const [threadData, setCommentThreadData] = useRecoilState(
    commentThreadsState(threadID)
  );

  const [commentText, setCommentText] = useState("");

  const onClick = useCallback(() =&gt; {
    setCommentThreadData((threadData) =&gt; ({
      ...threadData,
      comments: [
        ...threadData.comments,
        // append comment to the comments on the thread.
        { text: commentText, author: "Jane Doe", creationTime: new Date() },
      ],
    }));
    // clear the input
    setCommentText("");
  }, [commentText, setCommentThreadData]);

  const onCommentTextChange = useCallback(
    (event) =&gt; setCommentText(event.target.value),
    [setCommentText]
  );

  return (
    &lt;NodePopover
      ...
    &gt;
      &lt;div className={"comment-input-wrapper"}&gt;
        &lt;Form.Control
          bsPrefix={"comment-input form-control"}
          placeholder={"Type a comment"}
          type="text"
          value={commentText}
          onChange={onCommentTextChange}
        /&gt;
        &lt;Button
          size="sm"
          variant="primary"
          disabled={commentText.length === 0}
          onClick={onClick}
        &gt;
          Comment
        &lt;/Button&gt;
      &lt;/div&gt;
    &lt;/NodePopover&gt;
  );
}</code></pre>
</div>

**Note**: *Although we render an input for the user to type in comment, we don’t necessarily let it take focus when the popover mounts. This is a User Experience decision that could vary from one editor to another. Some editors do not let users edit the text while the comment thread popover is open. In our case, we want to be able to let the user edit the commented text when they click on it.*

Worth calling out how we access the specific comment thread’s data from the Recoil atom family &mdash; by calling out the atom as &mdash; `commentThreadsState(threadID)`. This gives us the value of the atom and a setter to update just that atom in the family. If the comments are being lazy loaded from the server, Recoil also provides a [`useRecoilStateLoadable`](https://recoiljs.org/docs/api-reference/core/useRecoilStateLoadable) hook that returns a [Loadable](https://recoiljs.org/docs/api-reference/core/Loadable) object which tells us about the loading state of the atom’s data. If it is still loading, we can choose to show a loading state in the popover.

Now, we access the `threadData` and render the list of comments. Each comment is rendered by the `CommentRow` component.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentThreadPopover.js

return (
    &lt;NodePopover
      ...
    &gt;
      &lt;div className={"comment-list"}&gt;
        {threadData.comments.map((comment, index) =&gt; (
          &lt;CommentRow key={`comment_${index}`} comment={comment} /&gt;
        ))}
      &lt;/div&gt;
      ...
    &lt;/NodePopover&gt;
);</code></pre>
</div>

Below is the implementation of `CommentRow` that renders the comment text and other metadata like author name and creation time. We use the `date-fns` module to show a formatted creation time.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentRow.js

import { format } from "date-fns";

export default function CommentRow({
  comment: { author, text, creationTime },
}) {
  return (
    &lt;div className={"comment-row"}&gt;
      &lt;div className="comment-author-photo"&gt;
        &lt;i className="bi bi-person-circle comment-author-photo"&gt;&lt;/i&gt;
      &lt;/div&gt;
      &lt;div&gt;
        &lt;span className="comment-author-name"&gt;{author}&lt;/span&gt;
        &lt;span className="comment-creation-time"&gt;
          {format(creationTime, "eee MM/dd H:mm")}
        &lt;/span&gt;
        &lt;div className="comment-text"&gt;{text}&lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}</code></pre>
</div>

We’ve extracted this to be its own component as we re-use it later when we implement the Comment Sidebar.

At this point, our Comment Popover has all the code it needs to allow inserting new comments and updating the Recoil state for the same. Let’s verify that. On the browser console, using the Recoil Debug Observer we added earlier, we’re able to verify that the Recoil atom for the comment thread is getting updated correctly as we add new comments to the thread.

{{< vimeo id="554497047" caption="Comment Thread Popover loads on selecting a comment thread." breakout="true" >}}

## Adding A Comments Sidebar

Earlier in the article, we’ve called out why occasionally, it may so happen that the rules we implemented prevent a certain comment thread to not be accessible by clicking on its text node(s) alone &mdash; depending upon the combination of overlap. For such cases, we need a Comments Sidebar that lets the user get to any and all comment threads in the document.

A Comments Sidebar is also a good addition that weaves into a Suggestion & Review workflow where a reviewer can navigate through all the comment threads one after the other in a sweep and be able to leave comments/replies wherever they feel the need to. Before we start implementing the sidebar, there is one unfinished task we take care of below.

### Initializing Recoil State Of Comment Threads

When the document is loaded in the editor, we need to scan the document to find all the comment threads and add them to the Recoil atoms we created above as part of the initialization process. Let’s write a utility function in `EditorCommentUtils` that scans the text nodes, finds all the comment threads and adds them to the Recoil atom.

<div class="break-out">

<pre><code class="language-javascript"># src/utils/EditorCommentUtils.js

export async function initializeStateWithAllCommentThreads(
  editor,
  addCommentThread
) {
  const textNodesWithComments = Editor.nodes(editor, {
    at: [],
    mode: "lowest",
    match: (n) =&gt; Text.isText(n) && getCommentThreadsOnTextNode(n).size &gt; 0,
  });

  const commentThreads = new Set();

  let textNodeEntry = textNodesWithComments.next().value;
  while (textNodeEntry != null) {
    [...getCommentThreadsOnTextNode(textNodeEntry[0])].forEach((threadID) =&gt; {
      commentThreads.add(threadID);
    });
    textNodeEntry = textNodesWithComments.next().value;
  }

  Array.from(commentThreads).forEach((id) =&gt;
    addCommentThread(id, {
      comments: [
        {
          author: "Jane Doe",
          text: "Comment Thread Loaded from Server",
          creationTime: new Date(),
        },
      ],
      status: "open",
    })
  );
}</code></pre>
</div>

#### Syncing with Backend Storage and Performance Consideration

For the context of the article, as we’re purely focused on the UI implementation, we just initialize them with some data that lets us confirm the initialization code is working.

In the real-world usage of the Commenting System, comment threads are likely to be stored separately from the document contents themselves. In such a case, the above code would need to be updated to make an API call that fetches all the metadata and comments on all the comment thread IDs in `commentThreads`. Once the comment threads are loaded, they are likely to be updated as multiple users add more comments to them in real time, change their status and so on. The production version of the Commenting System would need to structure the Recoil storage in a way that we can keep syncing it with the server. If you choose to use Recoil for state management, there are some [examples](https://recoiljs.org/docs/guides/atom-effects#state-synchronization-example) on the Atom Effects API (experimental as of writing this article) that do something similar.

If a document is really long and has a lot of users collaborating on it on a lot of comment threads, we might have to optimize the initialization code to only load comment threads for the first few pages of the document. Alternatively, we may choose to only load the light-weight metadata of all the comment threads instead of the entire list of comments which is likely the heavier part of the payload.

Now, let's move on to calling this function when the  `Editor` component mounts with the document so the Recoil state is correctly initialized.

<div class="break-out">

<pre><code class="language-javascript"># src/components/Editor.js

import { initializeStateWithAllCommentThreads } from "../utils/EditorCommentUtils";
import useAddCommentThreadToState from "../hooks/useAddCommentThreadToState";
 
export default function Editor({ document, onChange }): JSX.Element {
   ...
  const addCommentThread = useAddCommentThreadToState();

  useEffect(() =&gt; {
    initializeStateWithAllCommentThreads(editor, addCommentThread);
  }, [editor, addCommentThread]);

  return (
     &lt;&gt;
       ...
     &lt;/&gt;
  );
}</code></pre>
</div>

We use the same custom hook &mdash; `useAddCommentThreadToState` that we used with the Toolbar Comment Button implementation to add new comment threads. Since we have the popover working, we can click on one of pre-existing comment threads in the document and verify that it shows the data we used to initialize the thread above.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18412e7f-4e8c-4725-ac02-ee2819725b60/recoil-initialization.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18412e7f-4e8c-4725-ac02-ee2819725b60/recoil-initialization.png" width="800" height="344" sizes="100vw" caption="Clicking on a pre-existing comment thread loads the popover with their comments correctly. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18412e7f-4e8c-4725-ac02-ee2819725b60/recoil-initialization.png'>Large preview</a>)" alt="Clicking on a pre-existing comment thread loads the popover with their comments correctly." >}}

Now that our state is correctly initialized, we can start implementing the sidebar. All our comment threads in the UI are stored in the Recoil atom family &mdash; `commentThreadsState`. As highlighted earlier, the way we iterate through all the items in a Recoil atom family is by tracking the atom keys/ids in another atom. We’ve been doing that with `commentThreadIDsState`.  Let’s add the `CommentSidebar` component that iterates through the set of ids in this atom and renders a `CommentThread` component for each.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentsSidebar.js

import "./CommentSidebar.css";

import {commentThreadIDsState,} from "../utils/CommentState";
import { useRecoilValue } from "recoil";

export default function CommentsSidebar(params) {
  const allCommentThreadIDs = useRecoilValue(commentThreadIDsState);

  return (
    &lt;Card className={"comments-sidebar"}&gt;
      &lt;Card.Header&gt;Comments&lt;/Card.Header&gt;
      &lt;Card.Body&gt;
        {Array.from(allCommentThreadIDs).map((id) =&gt; (
          &lt;Row key={id}&gt;
            &lt;Col&gt;
              &lt;CommentThread id={id} /&gt;
            &lt;/Col&gt;
          &lt;/Row&gt;
        ))}
      &lt;/Card.Body&gt;
    &lt;/Card&gt;
  );
}</code></pre>
</div>

Now, we implement the `CommentThread` component that listens to the Recoil atom in the family corresponding to the comment thread it is rendering. This way, as the user adds more comments on the thread in the editor or changes any other metadata, we can update the sidebar to reflect that.

As the sidebar could grow to be really big for a document with a lot of comments, we hide all comments but the first one when we render the sidebar. The user can use the ‘Show/Hide Replies’ button to show/hide the entire thread of comments.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentSidebar.js

function CommentThread({ id }) {
  const { comments } = useRecoilValue(commentThreadsState(id));

  const [shouldShowReplies, setShouldShowReplies] = useState(false);
  const onBtnClick = useCallback(() =&gt; {
    setShouldShowReplies(!shouldShowReplies);
  }, [shouldShowReplies, setShouldShowReplies]);

  if (comments.length === 0) {
    return null;
  }

  const [firstComment, ...otherComments] = comments;
  return (
    &lt;Card
      body={true}
      className={classNames({
        "comment-thread-container": true,
      })}
    &gt;
      &lt;CommentRow comment={firstComment} showConnector={false} /&gt;
      {shouldShowReplies
        ? otherComments.map((comment, index) =&gt; (
            &lt;CommentRow key={`comment-${index}`} comment={comment} showConnector={true} /&gt;
          ))
        : null}
      {comments.length &gt; 1 ? (
        &lt;Button
          className={"show-replies-btn"}
          size="sm"
          variant="outline-primary"
          onClick={onBtnClick}
        &gt;
          {shouldShowReplies ? "Hide Replies" : "Show Replies"}
        &lt;/Button&gt;
      ) : null}
    &lt;/Card&gt;
  );
}</code></pre>
</div>

We’ve reused the `CommentRow` component from the popover although we added a design treatment using `showConnector` prop that basically makes all the comments look connected with a thread in the sidebar.

Now, we render the `CommentSidebar` in the `Editor` and verify that it shows all the threads we have in the document and correctly updates as we add new threads or new comments to existing threads.

<pre><code class="language-javascript"># src/components/Editor.js

return (
    &lt;&gt;
      &lt;Slate ... &gt;
       .....
		&lt;div className={"sidebar-wrapper"}&gt;
		  &lt;CommentsSidebar /&gt;
            &lt;/div&gt;
      &lt;/Slate&gt;
    &lt;/&gt;
);</code></pre>

{{< vimeo id="554503454" caption="Comments Sidebar with all the comment threads in the document." breakout="true" >}}

We now move on to implementing a popular Comments Sidebar interaction found in editors:

Clicking on a comment thread in the sidebar should select/activate that comment thread. We also add a differential design treatment to highlight a comment thread in the sidebar if it’s active in the editor. To be able to do so, we use the Recoil atom &mdash; `activeCommentThreadIDAtom`. Let’s update the `CommentThread` component to support this.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentsSidebar.js

function CommentThread({ id }) {
 
const [activeCommentThreadID, setActiveCommentThreadID] = useRecoilState(
    activeCommentThreadIDAtom
  );

const onClick = useCallback(() =&gt; {   
    setActiveCommentThreadID(id);
  }, [id, setActiveCommentThreadID]);

  ...

  return (
    &lt;Card
      body={true}
      className={classNames({
        "comment-thread-container": true,
        "is-active": activeCommentThreadID === id,      
      })}
      onClick={onClick}
    &gt;
    ....
   &lt;/Card&gt;
);</code></pre>
</div>

{{< vimeo id="554504775" caption="Clicking on a comment thread in Comments Sidebar selects it in the editor and highlights its range." breakout="true" >}}

If we look closely, we have a bug in our implementation of sync-ing the active comment thread with the sidebar. As we click on different comment threads in the sidebar, the correct comment thread is indeed highlighted in the editor. However, the Comment Popover doesn’t actually move to the changed active comment thread. It stays where it was first rendered. If we look at the implementation of the Comment Popover, it renders itself against the first text node in the editor’s selection. At that point in the implementation, the only way to select a comment thread was to click on a text node so we could conveniently rely on the editor's selection since it was updated by Slate as a result of the click event. In the above `onClick` event, we don’t update the selection but merely update the Recoil atom value causing Slate’s selection to remain unchanged and hence the Comment Popover doesn’t move.

A solution to this problem is to update the editor’s selection along with updating the Recoil atom when the user clicks on the comment thread in the sidebar. The steps do this are:

1. Find all text nodes that have this comment thread on them that we are going to set as the new active thread.
2. Sort these text nodes in the order in which they appear in the document (We use Slate’s [`Path.compare`](https://github.com/ianstormtaylor/slate/blob/f7b6f438ef5ca504eebef39bfc11850ff2c39c3e/packages/slate/src/interfaces/path.ts#L15) API for this).
3. Compute a selection range that spans from the start of the first text node to the end of the last text node.
4. Set the selection range to be the editor’s new selection (using Slate’s [`Transforms.select`](https://github.com/ianstormtaylor/slate/blob/e4936c3f32711a646ecdb51d4a75462975861660/packages/slate/src/transforms/selection.ts#L20) API).

If we just wanted to fix the bug, we could just find the first text node in Step #1 that has the comment thread and set that to be the editor’s selection. However, it feels like a cleaner approach to select the entire comment range as we really are selecting the comment thread.

Let’s update the `onClick` callback implementation to include the steps above.

<div class="break-out">

<pre><code class="language-javascript">const onClick = useCallback(() =&gt; {

    const textNodesWithThread = Editor.nodes(editor, {
      at: [],
      mode: "lowest",
      match: (n) =&gt; Text.isText(n) && getCommentThreadsOnTextNode(n).has(id),
    });

    let textNodeEntry = textNodesWithThread.next().value;
    const allTextNodePaths = [];

    while (textNodeEntry != null) {
      allTextNodePaths.push(textNodeEntry[1]);
      textNodeEntry = textNodesWithThread.next().value;
    }

    // sort the text nodes
    allTextNodePaths.sort((p1, p2) =&gt; Path.compare(p1, p2));

    // set the selection on the editor
    Transforms.select(editor, {
      anchor: Editor.point(editor, allTextNodePaths[0], { edge: "start" }),
      focus: Editor.point(
        editor,
        allTextNodePaths[allTextNodePaths.length - 1],
        { edge: "end" }
      ),
    });

   // Update the Recoil atom value.
    setActiveCommentThreadID(id);
  }, [editor, id, setActiveCommentThreadID]);</code></pre>
</div>

**Note**: *`allTextNodePaths` contains the path to all the text nodes. We use the [`Editor.point`](https://github.com/ianstormtaylor/slate/blob/f7b6f438ef5ca504eebef39bfc11850ff2c39c3e/packages/slate/src/interfaces/editor.ts#L213) API to get the start and end points at that path. The [first article](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/) goes through Slate’s Location concepts. They’re also well-documented on Slate’s [documentation](https://docs.slatejs.org/concepts/03-locations).*

Let’s verify that this implementation does fix the bug and the Comment Popover moves to the active comment thread correctly. This time, we also test with a case of overlapping threads to make sure it doesn’t break there.

{{< vimeo id="554506474" caption="Clicking on a comment thread in Comments Sidebar selects it and loads Comment Thread Popover." breakout="true" >}}

With the bug fix, we’ve enabled another sidebar interaction that we haven’t discussed yet. If we have a really long document and the user clicks on a comment thread in the sidebar that’s outside the viewport, we’d want to scroll to that part of the document so the user can focus on the comment thread in the editor. By setting the selection above using Slate’s API, we get that for free. Let’s see it in action below.

{{< vimeo id="554506856" caption="Document scrolls to the comment thread correctly when clicked on in the Comments Sidebar." breakout="true" >}}

With that, we wrap our implementation of the sidebar. Towards the end of the article, we list out some nice feature additions and enhancements we can do to the Comments Sidebar that help elevate the Commenting and Review experience on the editor.

## Resolving And Re-Opening Comments

In this section, we focus on enabling users to mark comment threads as ‘Resolved’ or be able to re-open them for discussion if needed. From an implementation detail perspective, this is the `status` metadata on a comment thread that we change as the user performs this action. From a user’s perspective, this is a very useful feature as it gives them a way to affirm that the discussion about something on the document has concluded or needs to be re-opened because there are some updates/new perspectives, and so on.

To enable toggling the status, we add a button to the `CommentPopover` that allows the user to toggle between the two statuses: `open` and `resolved`.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentThreadPopover.js

export default function CommentThreadPopover({
  editorOffsets,
  selection,
  threadID,
}) {
  …
  const [threadData, setCommentThreadData] = useRecoilState(
    commentThreadsState(threadID)
  );

  ...

  const onToggleStatus = useCallback(() =&gt; {
    const currentStatus = threadData.status;
    setCommentThreadData((threadData) =&gt; ({
      ...threadData,
      status: currentStatus === "open" ? "resolved" : "open",
    }));
  }, [setCommentThreadData, threadData.status]);

  return (
    &lt;NodePopover
      ...
      header={
        &lt;Header
          status={threadData.status}
          shouldAllowStatusChange={threadData.comments.length &gt; 0}
          onToggleStatus={onToggleStatus}
        /&gt;
      }
    &gt;
      &lt;div className={"comment-list"}&gt;
          ...
      &lt;/div&gt;
    &lt;/NodePopover&gt;
  );
}

function Header({ onToggleStatus, shouldAllowStatusChange, status }) {
  return (
    &lt;div className={"comment-thread-popover-header"}&gt;
      {shouldAllowStatusChange && status != null ? (
        &lt;Button size="sm" variant="primary" onClick={onToggleStatus}&gt;
          {status === "open" ? "Resolve" : "Re-Open"}
        &lt;/Button&gt;
      ) : null}
    &lt;/div&gt;
  );
}</code></pre>
</div>

Before we test this, let’s also give the Comments Sidebar a differential design treatment for resolved comments so that the user can easily detect which comment threads are un-resolved or open and focus on those if they want to.

<div class="break-out">

<pre><code class="language-javascript"># src/components/CommentsSidebar.js

function CommentThread({ id }) {
  ...
  const { comments, status } = useRecoilValue(commentThreadsState(id));
 
 ...
  return (
    &lt;Card
      body={true}
      className={classNames({
        "comment-thread-container": true,
        "is-resolved": status === "resolved",
        "is-active": activeCommentThreadID === id,
      })}
      onClick={onClick}
    &gt;
       ...  
   &lt;/Card&gt;
  );
}</code></pre>
</div>

{{< vimeo id="554508937" caption="Comment Thread Status being toggled from the popover and reflected in the sidebar." breakout="true" >}}

## Conclusion

In this article, we built the core UI infrastructure for a Commenting System on a Rich Text Editor. The set of functionalities we add here act as a foundation to build a richer Collaboration Experience on an editor where collaborators could annotate parts of the document and have conversations about them. Adding a Comments Sidebar gives us a space to have more conversational or review-based functionalities to be enabled on the product.

Along those lines, here are some of features that a Rich Text Editor could consider adding on top of what we built in this article:

- Support for `@` mentions so collaborators could tag one another in comments;
- Support for media types like images and videos to be added to comment threads;
- Suggestion Mode at the document level that allows reviewers to make edits to the document that appear as suggestions for changes. One could refer to this feature in [Google Docs](https://support.google.com/docs/answer/6033474?co=GENIE.Platform%3DDesktop&hl=en) or [Change Tracking](https://support.microsoft.com/en-us/office/track-changes-in-word-197ba630-0f5f-4a8e-9a77-3712475e806a) in Microsoft Word as examples;
- Enhancements to the sidebar to search conversations by keyword, filter threads by status or comment author(s), and so on.

{{< signature "vf, yk, il" >}}
