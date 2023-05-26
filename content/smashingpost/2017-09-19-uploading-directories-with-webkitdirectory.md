---
title: Uploading Directories At Once With webkitdirectory
slug: uploading-directories-with-webkitdirectory
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c26dea8-3e2a-4ccc-865c-488dc709990e/webkitdirectory-demo-opt.png
date: 2017-09-19T15:22:08.000Z
author: vitaly-friedman
description: >-
  If you've ever tried to implement a [bulletproof, good-looking file
  uploader](https://www.smashingmagazine.com/2013/10/so-we-wanted-to-build-a-file-uploader-a-case-study/),
  you might have encountered an issue: uploading an entire folder or folders of
  files is usually quite a hassle, as files in each folder have to be selected
  manually. And then some folders might contain sub-folders as well.

  Well, we can use `webkitdirectory`, a non-standard attribute that allows users
  to pick a directory via a file input. Currently supported in Chrome, Firefox
  and Edge.
categories:
  - Forms
  - CSS
  - File Upload
---
Well, we can use `webkitdirectory`, a non-standard attribute that allows users to pick a directory via a file input. Currently [supported in Chrome, Firefox and Edge](https://www.caniuse.com/#search=webkitdirectory).</p>

<figure><a title="input webkitdirectory" href="https://codepen.io/simevidas/pen/ZJjmWG?editors=0010"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e5a60e8-3177-46ca-bb06-ecffc2b9f794/webkit-directory.gif" width="448" height="422" alt="input webkitdirectory" /></a><figcaption>We can upload file directories, including sub-folders, at once. A <a href="https://codepen.io/simevidas/pen/ZJjmWG?editors=0010">demo by Šime Vidas</a>.</figcaption></figure>

For example, users could just pick a directory, and all files in that directory and its sub-folders would be listed below, represented by their relative path — a [demo by Šime Vidas](https://codepen.io/simevidas/pen/ZJjmWG?editors=0010) shows how it works. One click to choose them all is enough.

It's important to note that the [attribute is non-standard](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/webkitdirectory), so it will not work for everybody. However, it doesn't break anything as browsers that don't support it will just ignore it, so you can easily progressively enhance your file upload without relying on the feature being supported everywhere. Being useful in various scenarios, hopefully the attribute will be picked up by and standardized soon, landing in browsers as a `directory` attribute.

{{% feature-panel %}}

Ah, and if you want to design a slightly better drag'n'drop-experience, Alex Reardon has a few tips on [rethinking drag'n'drop altogether](https://medium.com/@alexandereardon/rethinking-drag-and-drop-d9f5770b4e6b). Worth reading!

### Further Resources:

*   [FileAPI](https://github.com/mailru/FileAPI)  
    A set of JavaScript libraries for working with files. Multiupload, drag'n'drop and chunked file upload. Images: crop, resize and auto orientation by EXIF.
*   [Drag and Drop Interaction Ideas](https://tympanus.net/Development/DragDropInteractions/)
*   [HTMLInputElement.webkitdirectory](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/webkitdirectory)
*   [File and Directory Entries API](https://wicg.github.io/entries-api/#dom-htmlinputelement-webkitdirectory)

_We send out this and other useful tips and tricks for designers and developers in our [Smashing Email Newsletter](https://smashingmagazine.us1.list-manage1.com/subscribe?u=16b832d9ad4b28edf261f34df&id=a1666656e0) — once every two weeks. (Once subscribed, you get a free eBook, too.)_

