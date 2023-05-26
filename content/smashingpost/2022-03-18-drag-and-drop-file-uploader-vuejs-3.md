---
title: 'How To Make A Drag-and-Drop File Uploader With Vue.js 3'
slug: drag-drop-file-uploader-vuejs-3
author: joseph-zimmerman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a9a0777-fd16-459e-b50d-20d5119f220d/drag-drop-file-uploader-vuejs-3.jpg
date: 2022-03-18T10:30:00.000Z
summary: >-
  Building on a previous article on <a href="https://www.smashingmagazine.com/2018/01/drag-drop-file-uploader-vanilla-js/">How to Build a Drag-and-Drop File Uploader</a>, we’ll be adding some new features, but more importantly (maybe), we’ll be learning how to build it in Vue 3 and learn some best practices for Vue along the waxy.
description: >-
  Building on a previous article on <a href="https://www.smashingmagazine.com/2018/01/drag-drop-file-uploader-vanilla-js/">How to Build a Drag-and-Drop File Uploader</a>, we’ll be adding some new features, but more importantly (maybe), we’ll be learning how to build it in Vue 3 and learn some best practices for Vue along the way.
categories:
  - Vue
  - Tools
  - Browsers
  - JavaScript
---

What’s different about the file uploader we’re building in this article versus the previous one? The previous drag-and-drop file uploader was built with Vanilla JS and really focused on how to make file uploading and drag-and-drop file selection work, so its feature set was limited. It uploaded the files immediately after you chose them with a simple progress bar and an image thumbnail preview. You can see all of this at [this demo](https://codepen.io/joezimjs/pen/yPWQbd).

In addition to using Vue, we’ll be changing the features up: after an image is added, it will not upload immediately. Instead, a thumbnail preview will show up. There will be a button on the top right of the thumbnail that will remove the file from the list in case you didn’t mean to select an image or change your mind about uploading it.

You’ll then click on the “Upload” button to send the image data to the server and each image will display its upload status. To top it all off, I crafted some snazzy styles (I’m no designer, though, so don’t judge too harshly). We won’t be digging into those styles in this tutorial, but they’ll be available for you to copy or sift through yourself in the [GitHub Repository](https://github.com/joezimjs/vue-dd-uploader) &mdash; though, if you’re going to copy them, make sure you set up your project to be able to use Stylus styles (or you can set it up to use Sass and change `lang` to `scss` for the style blocks and it will work that way). You can also see what we’re building today on [the demo page](https://vue-dd-uploader.pages.dev/).

**Note**: *I will assume that readers have strong JavaScript knowledge and a good grasp of the Vue features and APIs, especially Vue 3’s composition API, but not necessarily the best ways to use them. This article is to learn how to create a drag-and-drop uploader in the context of a Vue app while discussing good patterns and practices and will not go deep into how to use Vue itself.*

## Setup

There are a lot of ways to set up a Vue project: [Vue CLI](https://cli.vuejs.org/guide/), [Vite](https://vitejs.dev/guide/#scaffolding-your-first-vite-project), [Nuxt](https://v3.nuxtjs.org/getting-started/installation), and [Quasar](https://quasar.dev/start/pick-quasar-flavour) all have their own project scaffolding tools, and I’m sure there are more. I’m not all that familiar with most of them, and I’m not going to prescribe any one tool as of right for this project, so I recommend reading the documentation for whichever you choose to figure out how to set up the way we need it for this little project.

We need to be set up with Vue 3 with the [script setup](https://v3.vuejs.org/api/sfc-script-setup.html) syntax, and if you’re snatching my styles from the [Github repo](https://github.com/joezimjs/vue-dd-uploader), you’ll need to make sure you’re set up to have your Vue styles compiled from Stylus (or you can set it up to use Sass and change `lang` to “scss” for the style blocks and it will work that way).

## Drop Zone

Now that we have the project set up, let’s dive into the code. We’ll start with a component that handles the drag-and-drop functionality. This will be a simple wrapper `div` element with a bunch of event listeners and emitters for the most part. This sort of element is a great candidate for a reusable component (despite it only being used once in this particular project): it has a very specific job to do and that job is generic enough to be used in a lot of different ways/places without the need of a ton of customization options or complexity.

This is one of those things good developers are always keeping an eye out for. Cramming a ton of functionality into a single component would be a bad idea for this project or any other because then 1) it can’t be reused if you find a similar situation later and 2) it’s more difficult to sort through the code and figure out how each piece relates to each other. So, we’re going to do what we can to follow this principle and it starts here with the `DropZone` component. We’ll start with a simple version of the component and then spruce it up a bit to help you grok what’s going on a bit easier, so let’s create a `DropZone.vue` file in the `src/components` folder:

<pre><code class="language-html">&lt;template&gt;
    &lt;div @drop.prevent="onDrop"&gt;
        &lt;slot&gt;&lt;/slot&gt;
    &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
import { onMounted, onUnmounted } from 'vue'
const emit = defineEmits(['files-dropped'])

function onDrop(e) {
    emit('files-dropped', [...e.dataTransfer.files])
}

function preventDefaults(e) {
    e.preventDefault()
}

const events = ['dragenter', 'dragover', 'dragleave', 'drop']

onMounted(() =&gt; {
    events.forEach((eventName) =&gt; {
        document.body.addEventListener(eventName, preventDefaults)
    })
})

onUnmounted(() =&gt; {
    events.forEach((eventName) =&gt; {
        document.body.removeEventListener(eventName, preventDefaults)
    })
})
&lt;/script&gt;</code></pre>

First, looking at the template, you’ll see a `div` with a `drop` event handler (with a `prevent` modifier to prevent default actions) calling a function that we’ll get to in a moment. Inside that `div` is a `slot`, so we can reuse this component with custom content inside it. Then we get to the JavaScript code, which is inside a `script` tag with the `setup` attribute.

**Note**: *If you’re unfamiliar with what benefits we get from this attribute and you didn’t read the link we added above, head over to the [&lt;script setup&gt; documentation for single file components](https://v3.vuejs.org/api/sfc-script-setup.html).*

Inside the script, we define an event that we’ll emit called ‘files-dropped’ that other components can use to do something with the files that get dropped here. Then we define the function `onDrop` to handle the drop event. Right now, all it does is emit the event we just defined and add an array of the files that were just dropped as the payload. Note, we’re using a trick with the spread operator to convert the list of files from the `FileList` that `e.dataTransfer.files` gives us to an array of `File`s so all the array methods can be called on it by the part of the system that takes the files.

Finally, we come to the place where we handle the other drag/drop events that happen on the body, preventing the default behavior during the drag and drop (namely that it’ll open one of the files in the browser. We create a function that simply calls `preventDefault` on the event object. Then, in the `onMounted` lifecycle hook we iterate over the list of events and prevent default behavior for that even on the document body. In the `onUnmounted` hook, we remove those listeners.

{{% feature-panel %}}

### Active State

So, what extra functionality can we add? The one thing I decided to add was some state indicating whether the drop zone was “active”, meaning that a file is currently hovering over the drop zone. That’s simple enough; create a `ref` called `active`, set it to true on the events when the files are dragged over the drop zone and false when they leave the zone or are dropped.

We’ll also want to expose this state to the components using `DropZone`, so we’ll turn our `slot` into a scoped slot and expose that state there. Instead of the scoped slot (or in addition to it for added flexibility), we could emit an event to inform the outside of the value of `active` as it changes. The advantage of this is that the entire component that is using `DropZone` can have access to the state, rather than it being limited to the components/elements within the slot in the template. We’re going to stick with the scoped slot for this article though.

Finally, for good measure, we’ll add a `data-active` attribute that reflects `active`'s value so we can key off it for styling. You could also use a class if you prefer, but I tend to like data attributes for state modifiers.

Let’s write it out:

<div class="break-out">

<pre><code class="language-html">&lt;template&gt;
    &lt;!-- add `data-active` and the event listeners --&gt;
    &lt;div :data-active="active" @dragenter.prevent="setActive" @dragover.prevent="setActive" @dragleave.prevent="setInactive" @drop.prevent="onDrop"&gt;
        &lt;!-- share state with the scoped slot --&gt;
        &lt;slot :dropZoneActive="active"&gt;&lt;/slot&gt;
    &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
// make sure to import `ref` from Vue
import { ref, onMounted, onUnmounted } from 'vue'
const emit = defineEmits(['files-dropped'])

// Create `active` state and manage it with functions
let active = ref(false)

function setActive() {
    active.value = true
}
function setInactive() {
    active.value = false
}

function onDrop(e) {
    setInactive() // add this line too
    emit('files-dropped', [...e.dataTransfer.files])
}

// ... nothing changed below this
&lt;/script&gt;
</code></pre>
</div>

I threw some comments in the code to note where the changes were, so I won’t dive too deep into it, but I have some notes. We’re using the `prevent` modifiers on all the event listeners again to make sure that default behavior doesn’t activate. Also, you’ll notice that the `setActive` and `setInactive` functions seem like a bit of overkill since you could just set `active` directly, and you could make that argument for sure, but just wait a bit; there will be another change that truly justifies the creation of functions.

You see, there’s an issue with what we’ve done. As you can see in the video below, using this code for the drop zone means that it can flicker between active and inactive states while you drag something around inside the drop zone.

{{< youtube id="nqAxR3GcMI8" breakout="true" caption="Flickery Drag Interaction" >}}

Why is it doing that? When you drag something over a child element, it will “enter” that element and “leave” the drop zone, which causes it to go inactive. The `dragenter` event will bubble up to the drop zone, but it happens before the `dragleave` event, so that doesn’t help. Then a `dragover` event will fire again on the drop zone which will flip it back to active but not before flickering to the inactive state.

To fix this, we’ll add a short timeout to the `setInactive` function to prevent it from going inactive immediately. Then `setActive` will clear that timeout so that if it is called before we actually set it as inactive, it won’t actually become inactive. Let’s make those changes:

<pre><code class="language-javascript">// Nothing changed above

let active = ref(false)
let inActiveTimeout = null // add a variable to hold the timeout key

function setActive() {
    active.value = true
    clearTimeout(inActiveTimeout) // clear the timeout
}
function setInactive() {
    // wrap it in a `setTimeout`
    inActiveTimeout = setTimeout(() =&gt; {
        active.value = false
    }, 50)
}

// Nothing below this changes</code></pre>

You’ll note a timeout of 50 milliseconds. Why this number? Because I’ve tested several different timeouts and this feels the best.

I know that’s subjective but hear me out. I’ve tested much smaller timeouts and 15ms was about as low as I went where I never saw a flicker, but who knows how that’ll work on other hardware? It has too small a margin of error in my mind. You also probably don’t want to go over 100ms because that can cause perceived lag when a user intentionally does something that *should* cause it to go inactive. In the end, I settled somewhere in the middle that is long enough to pretty much guarantee there won’t be any flickering on any hardware and there should be no perceived lag.

That’s all we need for the `DropZone` component, so let’s move on to the next piece of the puzzle: a file list manager.

## File List Manager

I guess the first thing that needs to be done is an explanation of what I mean by the file list manager. This will be a composition function that returns several methods for managing the state of the files the user is attempting to upload. This could also be implemented as a [Vuex](https://vuex.vuejs.org/)/[Pinia](https://pinia.vuejs.org/)/[alternative](https://awesome-vue.js.org/components-and-libraries/utilities.html#state-management) store as well, but to keep things simple and prevent needing to install a dependency if we don’t need to, it makes a lot of sense to keep it as a composition function, especially since the data isn’t likely to be needed widely across the application, which is where the stores are the most useful.

You could also just build the functionality directly into the component that will be using our `DropZone` component, but this functionality seems like something that could very easily be reused; pulling it out of the component makes the component easier to understand the intent of what is going on (assuming good function and variable names) without needing to wade through the entire implementation.

Now that we’ve made it clear this is going to be a composition function and why, here’s what the file list manager will do:

1. Keep a list of files that have been selected by the user;
2. Prevent duplicate files;
3. Allow us to remove files from the list;
4. Augment the files with useful metadata: an ID, a URL that can be used to show a preview of the file, and the file’s upload status.

So, let’s build it in `src/compositions/file-list.js`:

<pre><code class="language-javascript">import { ref } from 'vue'

export default function () {
    const files = ref([])

    function addFiles(newFiles) {
        let newUploadableFiles = [...newFiles]
            .map((file) =&gt; new UploadableFile(file))
            .filter((file) =&gt; !fileExists(file.id))
        files.value = files.value.concat(newUploadableFiles)
    }

    function fileExists(otherId) {
        return files.value.some(({ id }) =&gt; id === otherId)
    }

    function removeFile(file) {
        const index = files.value.indexOf(file)

        if (index &gt; -1) files.value.splice(index, 1)
    }

    return { files, addFiles, removeFile }
}

class UploadableFile {
    constructor(file) {
        this.file = file
        this.id = `${file.name}-${file.size}-${file.lastModified}-${file.type}`
        this.url = URL.createObjectURL(file)
        this.status = null
    }
}</code></pre>

We’re exporting a function by default that returns the file list (as a `ref`) and a couple of methods that are used to add and remove files from the list. It would be nice to make the file list returned as read-only to force you to use the methods for manipulating the list, which you can do pretty easily using the `readonly` function imported from Vue, but that would cause issues with the uploader that we’ll build later.

Note that `files` is scoped to the composition function and set inside it, so each time you call the function, you’ll receive a new file list. If you want to share the state across multiple components/calls, then you’ll need to pull that declaration out of the function so it’s scoped and set once in the module, but in our case we’re only using it once, so it doesn’t really matter, and I was working under the thought that each instance of the file list would be used by a separate uploader and any state can be passed down to child components rather than shared via the composition function.

The most complex piece of this file list manager is adding new files to the list. First, we’re making sure that if a `FileList` object was passed instead of an array of `File` objects, then we convert it to an array (as we did in the `DropZone` when we emitted the files. This means we could probably skip that transformation, but better safe than sorry). Then we convert the file to an `UploadableFile`, which is a class we’re defining that wraps the file and gives us a few extra properties. We’re generating an `id` based on several aspects of the file so we can detect duplicates, a `blob://` URL of the image so we can show preview thumbnails and a status for tracking uploads.

Now that we have the IDs on the files, we filter out any files that already exist in the file list before concatenating them to the end of the file list.

### Possible Improvements

While this file list manager works well for what it does, there are a number of upgrades that can be done. For one thing, instead of wrapping the file in a new class and then having to call `.file` on it to access the original file object, we could wrap the file in a proxy that specifies our new properties, but then will forward any other property requests on to the original object, so it is more seamless.

As an alternative to wrapping each file in an `UploadableFile`, we could have provided utility functions that could return the ID or URL given a file, but that’s slightly less convenient and would mean that you’re potentially calculating these properties multiple times (for each render, and so on), but that shouldn’t really matter unless you’re dealing with people dropping thousands of images at once, in which case you can try memorizing it.

As for the status, that isn’t pulled straight from the `File`, so a simple utility function like the others wouldn’t be possible, but you could store the status of each file with the uploader (we’ll be building that later) rather than directly with the files. This might be a better way of handling it in a large app so we don’t end up filling the `UploadableFile` class with a bunch of properties that just facilitate a single area of the app and are useless elsewhere.

**Note**: *For our purposes, having the properties available directly on our file object is by far the most convenient, but it can definitely be argued that it isn’t the most appropriate.*

Another possible improvement is allowing you to specify a filter so that it only allows certain file types to be added to the list. This would also require `addFiles` to return errors when some files don’t match the filter in order to let the user know they made a mistake. This is definitely something that should be done in production-ready applications.

{{% ad-panel-leaderboard %}}

## Better Together

We’re far from a finished product, but let’s put the pieces we have together to verify everything is working so far. We’re going to be editing the `/src/App.vue` file, to put these pieces in, but you can add them to whatever page/section component you want. If you’re putting it inside an alternate component, though, ignore anything (like an ID of “app”) that would only be seen on the main app component.

<div class="break-out">

<pre><code class="language-html">&lt;template&gt;
    &lt;div id="app"&gt;
        &lt;DropZone class="drop-area" @files-dropped="addFiles" #default="{ dropZoneActive }"&gt;
            &lt;div v-if="dropZoneActive"&gt;
                &lt;div&gt;Drop Them&lt;/div&gt;
            &lt;/div&gt;
            &lt;div v-else&gt;
                &lt;div&gt;Drag Your Files Here&lt;/div&gt;
            &lt;/div&gt;
        &lt;/DropZone&gt;
    &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
import useFileList from './compositions/file-list'
import DropZone from './components/DropZone.vue'

const { files, addFiles, removeFile } = useFileList()
&lt;/script&gt;</code></pre>
</div>

If you start with the `script` section, you’ll see we’re not doing a whole lot. We’re importing the two files we just finished writing and we’re initializing the file list. Note, we’re not using `files` or `removeFile` yet, but we will later, so I’m just keeping them there for now. Sorry if ESLint is complaining about unused variables. We’ll want `files` at the very least so we can see if it’s working later.

Moving on to the template, you can see we’re using the `DropZone` component right away. We’re giving it a class so we can style it, passing the `addFiles` function for the “files-dropped” event handler, and grabbing the scoped slot variable so our content can be dynamic based on whether or not the drop zone is active. Then, inside the drop zone’s slot, we create a `div` showing a message to drag files over if it’s inactive and a message to drop them when it is active.

Now, you’ll probably want some styles to at least make the drop zone larger and easier to find. I won’t be pasting any here, but you can find the styles I used for [`App.vue` in the repo](https://github.com/joezimjs/vue-dd-uploader/blob/main/src/App.vue).

Now, before we can test the current state of the app, we’ll need the beta version of Vue DevTools installed in our browser (stable version doesn’t support Vue 3 quite yet). You can get [Vue DevTools from Chrome web store](https://chrome.google.com/webstore/detail/vuejs-devtools/ljjemllljcmogpfapbkkighbhhppjdbg) for most Chromium-based browsers or [download Vue DevTools here for Firefox](https://github.com/vuejs/vue-devtools/releases/download/v6.0.0-beta.8/vuejs_devtools_beta-6.0.0.8-an+fx.xpi).

After you’ve installed that, run your app with `npm run serve` (Vue CLI), `npm run dev` (Vite), or whatever script you use in your app, then open it in your browser via the URL given in the command line. Open up the Vue DevTools, then drag and drop some images onto the drop zone. If it worked, you should see an array of however many files you added when you view the component we just wrote (see screenshot below).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a0917c-20b3-475c-9a0f-05a31a61cb94/1-drag-and-drop-file-uploader-vuejs-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a0917c-20b3-475c-9a0f-05a31a61cb94/1-drag-and-drop-file-uploader-vuejs-3.png" width="800" height="273" sizes="100vw" caption="Vue DevTools showing the files we added. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a0917c-20b3-475c-9a0f-05a31a61cb94/1-drag-and-drop-file-uploader-vuejs-3.png'>Large preview</a>)" alt="A screenshot with Vue Devtools showing the files we added" >}}

Nice! Now Let’s make this a bit more accessible for users who can’t (or don’t want to) drag and drop, by adding a hidden file input (that becomes visible when focused via keyboard for those that need it, assuming you’re using my styles) and wrapping a big label around everything to allow us to use it despite its invisibility. Finally, we’ll need to add an event listener to the file input so that when a user selects a file, we can add it to our file list.

Let’s start with the changes to the `script` section. We’re just going to add a function to the end of it:

<pre><code class="language-javascript">function onInputChange(e) {
    addFiles(e.target.files)
    e.target.value = null
}</code></pre>

This function handles the “change” event fired from the input and adds the files from the input to the file list. Note the last line in the function resetting the value of the input. If a user adds a file via the input, decides to remove it from our file list, then changes their mind and decides to use the input to add that file again, then the file input will not fire the “change” event because the file input has not changed. By resetting the value like this, we ensure the event will always be fired.

Now, let’s make our changes to the template. Change all of the code inside the `DropZone` slot to the following:

<pre><code class="language-javascript">&lt;label for="file-input"&gt;
    &lt;span v-if="dropZoneActive"&gt;
        &lt;span&gt;Drop Them Here&lt;/span&gt;
        &lt;span class="smaller"&gt;to add them&lt;/span&gt;
    &lt;/span&gt;
    &lt;span v-else&gt;
        &lt;span&gt;Drag Your Files Here&lt;/span&gt;
        &lt;span class="smaller"&gt;
            or &lt;strong&gt;&lt;em&gt;click here&lt;/em&gt;&lt;/strong&gt; to select files
        &lt;/span&gt;
    &lt;/span&gt;

    &lt;input type="file" id="file-input" multiple @change="onInputChange" /&gt;
&lt;/label&gt;</code></pre>

We wrap the entire thing in a label that is linked to the file input, then we add our dynamic messages back in, though I’ve added a bit more messages to inform users they can click to select files. I also added a bit for the “drop them” message so that they have the same number of lines of text so the drop zone won’t change size when active. Finally, we add the file input, set the `multiple` attribute to allow users to select multiple files at a time, then wire up the “change” event listener to the function we just wrote.

Run the app again, if you stopped it, we should see the same result in the Vue DevTools whether we drag and drop files or click the box to use the file selector.

## Previewing Selected Images

Great, but users aren’t going to be using Vue DevTools to see if the files they dropped are actually added, so let’s start showing the users those files. We’ll start just by editing `App.vue` (or whatever component file you added the `DropZone` to) and showing a simple text list with the file names.

Let’s add the following bit of code to the template immediately following the `label` we just added in the previous step:

<pre><code class="language-javascript">&lt;ul v-show="files.length"&gt;
    &lt;li v-for="file of files" :key="file.id"&gt;{{ file.file.name }}&lt;/li&gt;
&lt;/ul&gt;</code></pre>

Now, with the app running, if you add some files to the list, you should see a bulleted list of the file names. If you copied my styles, it might look a bit odd, but that’s alright because we’re changing it soon. Make note that thanks to adding the file’s ID in the file list manager, we now have a key in the loop. The only thing that annoys me personally is that since we wrapped the files, we need to write `file.file` to access the original file object to get its name. In the end, though, it’s a small sacrifice to make.

Now, let’s start showing the images instead of just listing their names, but it’s time to move this functionality out of this main component. We certainly could, keep putting the file preview functionality here, but there are two good reasons to pull it out:

1. The functionality is potentially reusable in other cases.
2. As this functionality expands, separating it out prevents the main component from getting too bloated.

So, let’s create `/src/FilePreview.vue` to put this functionality in and we’ll start with just showing the image in a wrapper.

<pre><code class="language-html">&lt;template&gt;
    &lt;component :is="tag" class="file-preview"&gt;
        &lt;img :src="file.url" :alt="file.file.name" :title="file.file.name" /&gt;
    &lt;/component&gt;
&lt;/template&gt;

&lt;script setup&gt;
defineProps({
    file: { type: Object, required: true },
    tag: { type: String, default: 'li' },
})
&lt;/script&gt;</code></pre>

Once again, the styles aren’t included here, but you can find them [on GitHub](https://github.com/joezimjs/vue-dd-uploader/blob/main/src/components/FilePreview.vue). First thing to note about the code we have, though, is that we’re wrapping this in a `component` tag and setting what type of tag it is with a `tag` prop. This can be a good way to make a component more generic and reusable. We’re currently using this inside an unordered list, so `li` is the obvious choice, but if we want to use this component somewhere else at some point, it might not be in a list, so we would want a different tag.

For the image, we’re using the URL created by the file list manager, and we’re using the file name as the alt text and as the `title` attribute so we get that free functionality of users being able to hover over the image and see the file name as a tooltip. Of course, you can always create your own file preview where the file name is written out where it’s always visible for the user. There’s certainly a lot of freedom in how this can be handled.

Moving on to the JavaScript, we see props defined so we can pass in the file that we’re previewing and a tag name to customize the wrapper in order to make this usable in more situations. 

Of course, if you try to run this, it doesn’t seem to do anything because we currently aren’t using the `FilePreview` components. Let’s remedy that now. In the template, replace the current list with this:

<pre><code class="language-javascript">&lt;ul class="image-list" v-show="files.length"&gt;
    &lt;FilePreview v-for="file of files" :key="file.id" :file="file" tag="li" /&gt;
&lt;/ul&gt;</code></pre>

Also, we need to import our new component in the `script` section:

<pre><code class="language-javascript">import  FilePreview  from  './components/FilePreview.vue'</code></pre>

Now if you run this, you’ll see some nice thumbnails of each image you drop or select.

### Remove Files From the List

Let’s augment this with the ability to remove a file from the list. We’ll add a button with an “X” in the corner of the image that people can click/tap on to remove the image. To do this, we’ll need to add 2 lines of code to `FilePreview.vue`. In the template, just above the `img` tag add the following:

<pre><code class="language-javascript">&lt;button @click="$emit('remove', file)" class="close-icon" aria-label="Remove"&gt;&times;&lt;/button&gt;</code></pre>

Then add this line somewhere in the `script` section:

<pre><code class="language-javascript">defineEmits(['remove'])</code></pre>

Now, clicking that button will fire a `remove` event, passing the file along as the payload. Now we need to head back to the main app component to handle that event. All we need to do is to add the event listener to the `FilePreview` tag:

<pre><code class="language-javascript">&lt;FilePreview  v-for="file  of  files" :key="file.id" :file="file"  tag="li" @remove="removeFile" /&gt;</code></pre>

Thanks to `removeFile` already being defined by the file list manager and taking the same arguments that we’re passing from the event, we’re done in seconds. Now if you run the app and select some images, you can click on the little “X” and the corresponding image will disappear from the list.

### Possible Improvements

As usual, there are improvements that could be made to this if you’re so inclined and your application is able to reuse this component elsewhere if it is more generic or customizable.

First of all, you could manage the styles better. I know that I didn’t post the styles here, but if you copied them from GitHub and you’re a person that cares a lot about which components control which styles, then you may be thinking that it’d be wiser to have some specific files moved out of this component. As with most of these possible improvements, this is mostly to do with making the component more useful in more situations. Some of the styles are very specific to how I wanted to display the previews for this one little app, but to make it more reusable, we either need to make styles customizable via props or pull them out and let an outer component define the styles.

Another possible change would be to add props that allow you to hide certain elements such as the button that fires the “remove” event. There are more elements coming later in the article that might be good to hide via props as well.

And finally, it might be wise to separate the `file` prop into multiple props such as `url`, `name`, and &mdash; as we’ll see later &mdash; `status`. This would allow this component to be used in situations where you just have an image URL and name rather than an `UploadableFile` instance, so it’s more useful in more situations.

{{% ad-panel-leaderboard %}}

## Uploading Files

Alright, we have the drag and drop and a preview of the files selected, so now we need to upload those files and keep the user informed of the status of those uploads. We’ll start with creating a new file: `/compositions/file-uploader.js`. In this file, we’ll export some functions that allow our component to upload the files.

<pre><code class="language-javascript">export async function uploadFile(file, url) {
    // set up the request data
    let formData = new FormData()
    formData.append('file', file.file)

    // track status and upload file
    file.status = 'loading'
    let response = await fetch(url, { method: 'POST', body: formData })

    // change status to indicate the success of the upload request
    file.status = response.ok

    return response
}

export function uploadFiles(files, url) {
    return Promise.all(files.map((file) =&gt; uploadFile(file, url)))
}

export default function createUploader(url) {
    return {
        uploadFile: function (file) {
            return uploadFile(file, url)
        },
        uploadFiles: function (files) {
            return uploadFiles(files, url)
        },
    }
}</code></pre>

Before looking into specific functions, note that every function in this file is exported separately so it can be used on its own, but you’ll see that we’ll only be using one of them in our application. This gives some flexibility in how this module is used without actually making the code any more complicated since all we do is add an `export` statement to enable it.

Now, starting at the top, we have an asynchronous function for uploading a single file. This is constructed in a very similar manner to how it was done in the previous article, but we are using an `async` function instead (for that wonderful `await` keyword) and we’re updating the `status` property on the provided `file` to keep track of the upload’s progress. This `status` can have 4 possible values:

- `null`: initial value; indicates that it has not started uploading;
- `"loading"`: indicates that the upload is in progress;
- `true`: indicates the upload was successful;
- `false`: indicates the upload failed.

So, when we start the upload, we mark the status as `"loading"`. Once it’s finished, we mark it as `true` or `false` depending on the result’s `ok` property. Soon we’ll be using these values to show different messages in the `FilePreview` component. Finally, we return the response in case the caller can use that information.

**Note**: *Depending on which service you upload your files to, you may need some additional headers for authorization or something, but you can get those from the documentation for those services since I can’t write an example for every service out there.*

The next function, `uploadFiles`, is there to allow you to easily upload an array of files. The final function, `createUploader`, is a function that grants you the ability to use the other functions without having to specify the URL that you’re uploading to every time you call it. It “caches” the URL via a closure and returns versions of each of the two previous functions that don’t require the URL parameter to be passed in.

### Using the Uploader

Now that we have these functions defined, we need to use them, so go back to our main app component. Somewhere in the `script` section, we’ll need to add the following two lines:

<pre><code class="language-javascript">import  createUploader  from  './compositions/file-uploader'
const { uploadFiles } = createUploader('YOUR URL HERE')</code></pre>

Of course, you’ll need to change the URL to match whatever your upload server uses. Now we just need to call `uploadFiles` from somewhere, so let’s add a button that calls it in its click handler. Add the following at the end of the template:

<pre><code class="language-javascript">&lt;button @click.prevent="uploadFiles(files)"  class="upload-button"&gt;Upload&lt;/button&gt;</code></pre>

There you go. Now if you run the app, add some images, and smash that button, they should be headed for the server. But… we can’t tell if it worked or not &mdash; at least not without checking the server or the network panel in the dev tools. Let’s fix that.

### Showing The Status

Open up `FilePreview.vue`. In the template after the `img` tag but still within `component`, let’s add the following:

<pre><code class="language-javascript">&lt;span class="status-indicator loading-indicator" v-show="file.status == 'loading'"&gt;In Progress&lt;/span&gt;
&lt;span class="status-indicator success-indicator" v-show="file.status == true"&gt;Uploaded&lt;/span&gt;
&lt;span class="status-indicator failure-indicator" v-show="file.status == false"&gt;Error&lt;/span&gt;</code></pre>

All the styles are already included to control how these look if you copied the styles from GitHub earlier. These all sit in the bottom right corner of the images displaying the current status. Only one of them is shown at a time based on `file.status`.

I used `v-show` here, but it also makes a lot of sense to use `v-if`, so you can use either one. By using `v-show`, it always has the elements in the DOM but hides them. This means we can inspect the elements and cause them to show up even if they aren’t in the correct state, so we can test if they look right without trying to do it by putting the app into a certain state. Alternatively, you could go into the Vue DevTools, make sure you’re in the “Inspector” screen, click the three dots menu button in the top right and toggle “Editable props” to true, then edit the props or state in the component(s) to bring about the states needed to test each indicator.

**Note**: *Just be aware that once you edit the `file` state/prop, it is no longer the same object as the one that was passed in, so clicking the button to remove the image will not work (can’t remove a file that isn’t in the array) and clicking “Upload” won’t show any state changes for that image (because the one in the array that is being uploaded isn’t the same file object as the one being displayed by the preview).*

### Possible Improvements

As with other parts of this app, there are a few things we could do to make this better, but that we won’t actually be changing. First of all, the status values are pretty ambiguous. It would be a good idea to implement the values as constants or an enum (TypeScript supports enums). This would ensure that you don’t misspell a value such as “loading” or try to set the status to “error” instead of false and run into a bug. The status could also be implemented as a state machine since there is a very defined set of rules for how the state changes.

In addition to better statuses, there should be better error handling. We inform the users that there was an issue with the upload, but they have no idea what the error is. Is it a problem with their internet? Was the file too big? Is the server down? Who knows? Users need to know what the problem is so they know what they can do about it &mdash; if anything.

We could also keep the users better apprised of the upload. By using XHR instead of `fetch` (which I discussed in the previous drag-and-drop uploader article), we can track “progress” events to know the percentage of the upload that was completed, which is very useful for large files and slow internet connections because it can prove to the user that progress is actually being made and that it didn’t get stuck.

The one change that can increase the reusability of the code is opening up the file uploader to additional options (such as request headers) to be able to be passed in. In addition, we could check the status of a file to prevent us from uploading a file that’s already in progress or is already uploaded. To further help with this, we could disable the “Upload” button during the upload, and it should probably also be disabled when there are no files selected.

And last, but most certainly not least, we should add some accessibility improvements. In particular, when adding files, removing them, and uploading them (with all those status changes), we should audibly inform screen reader users that things have changed using [Live Regions](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions). I’m no expert on this, and they fall a bit outside the scope of this article, so I will not be going into any kind of detail, but it’s definitely something everyone should look into.

## Job’s Done

Well, that’s it. The Vue Drag-and-Drop Image Uploader is done! As mentioned at the beginning, you can see [the finished product here](https://vue-dd-uploader.pages.dev/) and look at the final code in the [GitHub Repository](https://github.com/joezimjs/vue-dd-uploader).

I hope you spend some time trying to implement the possible improvements that I’ve laid out in the previous sections to help you deepen your understanding of this app and keep sharpening your skills by thinking things through on your own. Do you have any other improvements that could be made to this uploader? Leave some suggestions in the comments and if you implemented any of the suggestions from above, you can share your work in the comments, too.

God bless and happy coding!

{{< signature "vf, yk, il" >}}
