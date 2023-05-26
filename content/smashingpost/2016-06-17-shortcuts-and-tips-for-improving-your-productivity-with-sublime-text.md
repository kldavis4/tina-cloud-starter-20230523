---
title: Shortcuts And Tips For Improving Your Productivity With Sublime Text
slug: shortcuts-and-tips-for-improving-your-productivity-with-sublime-text
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f4357c9-31f3-4ed2-8d5e-9f95cb97c155/sublime-text-code-example-preview-opt.png
date: 2016-06-17T18:11:04.000Z
author: jaipandya
description: >-
  Sublime Text is, no doubt, one of the most powerful text editors out there.
  The number of satisfied users attests to that. If you explore it, you will
  eventually see how beautifully its powerful features are hidden behind a
  simple and elegant interface.

  If you have been using Sublime Text for some time, now is the time to upgrade
  your arsenal with new ammunition. I’ll be taking you through some of my
  favorite tips and tricks. Knowing them might just unleash your hidden powers
  as a programmer to the world.
categories:
  - Coding
  - Tools
  - Workflow
---
Sublime Text is, no doubt, one of the most powerful text editors out there. The number of satisfied users attests to that. If you explore it, you will eventually see how beautifully its powerful features are hidden behind a simple and elegant interface.

If you have been using Sublime Text for some time, now is the time to upgrade your arsenal with new ammunition. I’ll be taking you through some of my favorite tips and tricks. Knowing them might just unleash your hidden powers as a programmer to the world.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [50 Powerful Time-Savers For Web Designers](https://www.smashingmagazine.com/2010/10/50-powerful-time-savers-for-designers/)
*   [Powerful Workflow Tips, Tools And Tricks For Web Designers](https://www.smashingmagazine.com/2013/10/powerful-workflow-tips-tools-and-tricks-for-web-designers/)
*   [How To Keep Your Coding Workflow Organized](https://www.smashingmagazine.com/2011/01/cleaning-up-the-mess-how-to-keep-your-coding-workflow-organized/)

## Sublime Text Plugins

### Package Control

Package Control is a one-stop solution for downloading and managing Sublime Text-related plugins and themes. The [installation instructions are available](https://packagecontrol.io/installation#st3) on the Package Control website.

{{% feature-panel %}}

Once it is installed, you can access it using the command palette. To install a plugin, press `Cmd ⌘ + Shift ⇧ + P` (Mac) or `Ctrl ⌃ + Shift ⇧ + P` (Windows and Linux), and then enter `Install Package` and press “Return.” The list of plugins in the repository takes a few moments to load, but then you can type the name of the plugin you are interested in and install it from there. Some of my favorite plugins are listed below.</p>

{{< vimeo id="169699061" caption="Package Control." >}}

### Sidebar Enhancements

Sublime Text’s default sidebar can only do some limited tasks. The [Sidebar Enhancements](https://packagecontrol.io/packages/SideBarEnhancements) plugin supercharges Sublime Text with commands for opening the file in a browser, copying, pasting, copying a path, duplicating, deleting and more.</p>

{{< vimeo id="169699086" caption="Sidebar Enhancements." >}}

### Plain Tasks

[Plain Tasks](https://packagecontrol.io/packages/PlainTasks) converts Sublime Text into a powerful to-do list manager. You can install it via Package Control. Create a file with `.todo` as the extension to activate Plain Tasks on top of it. For other tips, you can access the tutorial provided in the plugin, available at “Preferences” → “Package Settings” → “Plain Tasks” → “Tutorial.”

For a new task:

*   `Cmd ⌘ + Return ↵` (Mac)
*   `Ctrl ⌃ + Return ↵` (Windows and Linux)

To mark as done:

*   `Cmd ⌘ + D` (Mac)
*   `Ctrl ⌃ + D` (Windows and Linux)

To mark as cancelled:

*   `Ctrl ⌃ + C` (Mac)
*   `Alt + C` (Windows and Linux)

{{< vimeo id="169698983" caption="Plain Tasks." >}}

### Sublime Linter

Check for errors in your code using [Sublime Linter](https://packagecontrol.io/packages/SublimeLinter). The plugin provides a framework for linting your code. The actual linting is done by various plugins (for [Ruby](https://packagecontrol.io/packages/SublimeLinter-ruby), [Python](https://packagecontrol.io/packages/SublimeLinter-pep8), [JavaScript](https://packagecontrol.io/packages/SublimeLinter-jshint) etc.), which means you need to install Sublime Linter first and then install syntax-specific linters for your code. [Extensive documentation](https://www.sublimelinter.com/en/latest/) is available.</p>

{{< vimeo id="169515344" caption="Sublime Linter." >}}

### Emmet

[Emmet](https://emmet.io/), once known as Zen Coding, is an indispensable tool for any web developer. It is probably the most productive and time-saving plugin you’ll ever find.

Writing code takes time, and HTML grunt work such as writing tags and wrapping classes with quotes can be boring. Emmet takes care of all that. It magically expands abbreviations into a whole HTML or CSS structure. The syntax it uses for these abbreviations is inspired from CSS selectors. Let’s watch it in action.</p>

{{< vimeo id="169702703" caption="Emmet." >}}

### Sublime Tutor

[Sublime Tutor](https://sublimetutor.com/) is an interactive in-editor tutorial for keyboard shortcuts in Sublime Text. If you have just started with Sublime Text, the plugin will instantly boost your productivity by teaching you nifty tips and tricks within the editor itself. The plugin uses the spaced repetition technique to make sure you remember the commands it teaches.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e62b0da-5f2e-4d55-a1e6-0e6edab60b21/sublime-tutor-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d56b7f-0485-4066-85bb-4d53b00f227f/sublime-tutor-opt-preview.png" alt="Sublime plugin: Sublime Tutor" width="500" height="338" /></a><figcaption>Sublime Tutor.</figcaption></figure>

Use [Package Control](https://packagecontrol.io/packages/Sublime%20Tutor) to install the plugin. Once it is installed, you can access the tutor via the “Help” menu or the `Ctrl ⌃ + Alt ⌥ + K` keyboard shortcut.

## Sublime Text Functions

### Go To Anything

This is probably the most powerful and most-used command in Sublime Text. Navigate through files, folders, symbols and lines with ease.

To go to a file:

*   `Cmd ⌘ + P` (Mac)
*   `Ctrl ⌃ + P` (Windows and Linux)

Press the keyboard shortcode, and start typing the name of a file. Sublime Text will perform a fuzzy search and fetch you the desired file instantly.

Go to a symbol:

*   `Cmd ⌘ + R` (Mac)
*   `Ctrl ⌃ + R` (Windows and Linux)

Go to a line:

*   `Ctrl ⌃ + G` (Mac)
*   `Ctrl ⌃ + G` (Windows and Linux)

To go to a specific line in a file, type a colon followed by the line number, or use the keyboard shortcode.</p>

{{< vimeo id="169515256" caption="Go to anything." >}}

### Word Selection

*   `Cmd ⌘ + D` (Mac)
*   `Ctrl ⌃ + D` (Windows and Linux)

Put your cursor on a word, press the keyboard shortcode, and the word will instantly be selected. If you press the same key combination again, Sublime Text will go into multi-selection mode and select other instances of the same word in the document. You can use this method to quickly add or replace text in all instances of a word.</p>

{{< vimeo id="169515348" caption="Word selection." >}}

*   `Ctrl ⌃ + Cmd ⌘ + G` (Mac)
*   `Alt + F3` (Windows and Linux)

This is another way to achieve the same thing. Instead of incrementally searching for a word, it performs a bulk search of the word under the cursor and switches to multi-selection mode.</p>

### Expand Selection to Scope

*   `Cmd ⌘ + Shift ⇧ + Space ␣` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + Space ␣` (Windows and Linux)

This shortcut is extremely useful for JavaScript developers. It selects the current scope. Pressing the same key combination again selects its parent scope. The video makes clear how it works:

{{< vimeo id="169515337" caption="Expand selection to scope." >}}

### Break Selection Into Lines

*   `Cmd ⌘ + Shift ⇧ + L` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + L` (Windows and Linux)

Use this shortcut to break the selected area into multiple lines, putting Sublime Text in multi-selection mode. I use this trick to quickly convert a list of words into an enclosed array of strings.</p>

{{< vimeo id="169515347" caption="Break selection into lines." >}}

### Column Selection

*   `Ctrl ⌃ + Shift ⇧ + Up ↑ / Down ↓` (Mac)
*   `Ctrl ⌃ + Alt + Up ↑ / Down ↓` (Win)
*   `Alt + Shift ⇧ + Up ↑ / Down ↓` (Linux)

Use this shortcut to select a column in Sublime Text. Put your cursor anywhere in the document, and then press the shortcut to select columns upwards or downwards. This also takes you into multi-selection mode, like the two commands above.</p>

{{< vimeo id="169515331" caption="Column selection." >}}

### Sort

*   `F5` (Mac)
*   `F9` (Windows and Linux)

I like to keep my CSS properties sorted alphabetically. This command is extremely useful for that. Select the block that you need to be sorted (pro tip: use `Ctrl ⌃ + Shift ⇧ + J` to select an indentation level), and then press the keyboard shortcode.</p>

{{< vimeo id="169702148" caption="Sort." >}}

### Turn on Spellcheck

*   `F6`

No more getting disappointed by typographical errors after the code has made it to the review stage. Use this key to quickly toggle the spellchecker.</p>

{{< vimeo id="169515342" caption="Turn on spellcheck." >}}

### Comment

*   `Cmd ⌘ + /` (Mac)
*   `Ctrl ⌃ + /` (Windows and Linux)

This is one of my most frequently used shortcut. Marking comments in any programming language is made simple with this shortcut. In an HTML file, it puts in a pair of `<!-- -->` tags, while in JavaScript it puts `//` at the beginning of a line.</p>

{{< vimeo id="169515340" caption="Comment." >}}

### Bubble a Line Up or Down

*   `Cmd ⌘ + Ctrl ⌃ + Up ↑ / Down ↓` (Mac)
*   `Shift ⇧ + Ctrl ⌃ Up ↑ / Down ↓` (Windows and Linux)

Want to move a snippet of code five lines up? Cutting and pasting is really old school. Use this keybinding to take the snippet wherever you’d like. Press the shortcut again to keep moving it further up or down.</p>

{{< vimeo id="169515346" caption="Bubble a line up or down." >}}

### Duplicate Selection

*   `Cmd ⌘ + Shift ⇧ + D` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + D` (Windows and Linux)

By default, this shortcut duplicates the current line and puts it on the next line. If you select a region and press this shortcut, it duplicates the whole region.</p>

{{< vimeo id="169702454" caption="Duplicate selection." >}}

### Join Two Lines

*   `Cmd ⌘ + J` (Mac)
*   `Ctrl ⌃ + J` (Windows and Linux)

This joins the following line to the current line, replacing all white space in between with a single space. Performed on a block of lines, this joins all of the lines together.</p>

{{< vimeo id="169702578" caption="Join two lines." >}}

### Go to Matching Bracket

*   `Ctrl ⌃ + M`

Use this command to move your cursor from one bracket position to another. This is especially useful when you get lost in a long method and want to reach its starting position (or vice versa).</p>

{{< vimeo id="169699077" caption="Go to matching bracket." >}}

### Close HTML Tag

*   `Cmd ⌘ + Opt ⌥ + .` (Mac)
*   `Alt + .` (Windows and Linux)

Use this shortcut to close the currently open HTML tag. It inserts the matching closing tag at the current cursor location.</p>

{{< vimeo id="169515336" caption="Close HTML tag." >}}

### Find in Project

*   `Cmd ⌘ + Shift ⇧ + F` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + F` (Windows and Linux)

This is the `grep` equivalent of Sublime Text. It finds a term within an entire project. The special thing about this command is that it is blazing fast. There are options to make it case-sensitive and to perform a regex match as well.

To search for a particular term in the current document, project-wide, put the cursor on that term and then press `Ctrl ⌃ + E`, which will put that term in the search box. Pressing the shortcode above populates the project-wide search box with this term.</p>

{{< vimeo id="169515332" caption="Find in project." >}}

### Switch Between Tabs

*   `Cmd ⌘ + Shift ⇧ + [` or `]` (Mac)
*   `Ctrl ⌃ + Page Up ⇞` or `Page Down ⇟` (Windows and Linux)

Just like in a web browser, you can open multiple tabs in Sublime Text. To move from one tab to another, you can use the shortcuts noted above, and use `Cmd ⌘ + T` (Mac) or `Ctrl ⌃ + N` (Windows and Linux) to create a new tab.</p>

{{< vimeo id="169515334" caption="Switch between tabs." >}}

### Command Palette

*   `Cmd ⌘ + Shift ⇧ + P` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + P` (Windows and Linux)

As you become proficient with Sublime Text, you’ll want to access the menus less and less and instead be able to do everything with a few taps of the keyboard. With the command palette, you can quickly type a command, and Sublime Text will do a fuzzy match with an existing set of commands, letting you access the commands from a convenient place.

Here are some things you can try in the command palette — set the syntax of a newly created file, sort lines in the current document, and install a plugin using Package Control.</p>

{{< vimeo id="169515343" caption="Command palette." >}}

### Show Console

*   `Ctrl ⌃ + ``

Sublime Text comes with an embedded Python interpreter. It’s a handy tool to execute Python commands or to quickly test Sublime Text’s APIs when you’re developing a plugin for the editor.</p>

{{< vimeo id="169515331" caption="Column selection." >}}

### Sort

*   `F5` (Mac)
*   `F9` (Windows and Linux)

I like to keep my CSS properties sorted alphabetically. This command is extremely useful for that. Select the block that you need to be sorted (pro tip: use `Ctrl ⌃ + Shift ⇧ + J` to select an indentation level), and then press the keyboard shortcode.</p>

{{< vimeo id="169702148" caption="Sort." >}}

### Turn on Spellcheck

*   `F6`

No more getting disappointed by typographical errors after the code has made it to the review stage. Use this key to quickly toggle the spellchecker.</p>

{{< vimeo id="169515342" caption="Turn on spellcheck." >}}

### Comment

*   `Cmd ⌘ + /` (Mac)
*   `Ctrl ⌃ + /` (Windows and Linux)

This is one of my most frequently used shortcut. Marking comments in any programming language is made simple with this shortcut. In an HTML file, it puts in a pair of `<!-- -->` tags, while in JavaScript it puts `//` at the beginning of a line.</p>

{{< vimeo id="169515340" caption="Comment." >}}

### Bubble a Line Up or Down

*   `Cmd ⌘ + Ctrl ⌃ + Up ↑ / Down ↓` (Mac)
*   `Shift ⇧ + Ctrl ⌃ Up ↑ / Down ↓` (Windows and Linux)

Want to move a snippet of code five lines up? Cutting and pasting is really old school. Use this keybinding to take the snippet wherever you’d like. Press the shortcut again to keep moving it further up or down.</p>

{{< vimeo id="169515346" caption="Bubble a line up or down." >}}

### Duplicate Selection

*   `Cmd ⌘ + Shift ⇧ + D` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + D` (Windows and Linux)

By default, this shortcut duplicates the current line and puts it on the next line. If you select a region and press this shortcut, it duplicates the whole region.</p>

{{< vimeo id="169702454" caption="Duplicate selection." >}}

### Join Two Lines

*   `Cmd ⌘ + J` (Mac)
*   `Ctrl ⌃ + J` (Windows and Linux)

This joins the following line to the current line, replacing all white space in between with a single space. Performed on a block of lines, this joins all of the lines together.</p>

{{< vimeo id="169702578" caption="Join two lines." >}}

### Go to Matching Bracket

*   `Ctrl ⌃ + M`

Use this command to move your cursor from one bracket position to another. This is especially useful when you get lost in a long method and want to reach its starting position (or vice versa).</p>

{{< vimeo id="169699077" caption="Go to matching bracket." >}}

### Close HTML Tag

*   `Cmd ⌘ + Opt ⌥ + .` (Mac)
*   `Alt + .` (Windows and Linux)

Use this shortcut to close the currently open HTML tag. It inserts the matching closing tag at the current cursor location.</p>

{{< vimeo id="169515336" caption="Close HTML tag." >}}

### Find in Project

*   `Cmd ⌘ + Shift ⇧ + F` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + F` (Windows and Linux)

This is the `grep` equivalent of Sublime Text. It finds a term within an entire project. The special thing about this command is that it is blazing fast. There are options to make it case-sensitive and to perform a regex match as well.

To search for a particular term in the current document, project-wide, put the cursor on that term and then press `Ctrl ⌃ + E`, which will put that term in the search box. Pressing the shortcode above populates the project-wide search box with this term.</p>

{{< vimeo id="169515332" caption="Find in project." >}}

### Switch Between Tabs

*   `Cmd ⌘ + Shift ⇧ + [` or `]` (Mac)
*   `Ctrl ⌃ + Page Up ⇞` or `Page Down ⇟` (Windows and Linux)

Just like in a web browser, you can open multiple tabs in Sublime Text. To move from one tab to another, you can use the shortcuts noted above, and use `Cmd ⌘ + T` (Mac) or `Ctrl ⌃ + N` (Windows and Linux) to create a new tab.</p>

{{< vimeo id="169515334" caption="Switch between tabs." >}}

### Command Palette

*   `Cmd ⌘ + Shift ⇧ + P` (Mac)
*   `Ctrl ⌃ + Shift ⇧ + P` (Windows and Linux)

As you become proficient with Sublime Text, you’ll want to access the menus less and less and instead be able to do everything with a few taps of the keyboard. With the command palette, you can quickly type a command, and Sublime Text will do a fuzzy match with an existing set of commands, letting you access the commands from a convenient place.

Here are some things you can try in the command palette — set the syntax of a newly created file, sort lines in the current document, and install a plugin using Package Control.</p>

{{< vimeo id="169515343" caption="Command palette." >}}

### Show Console

*   `Ctrl ⌃ + ``

Sublime Text comes with an embedded Python interpreter. It’s a handy tool to execute Python commands or to quickly test Sublime Text’s APIs when you’re developing a plugin for the editor.

Keep in mind that this interpreter comes bundled with Sublime Text, and it is different from your system-installed Python. The purpose of this console is to interact with Sublime Text’s API for plugins. You probably used this console when installing Package Control.</p>

{{< vimeo id="169515333" caption="Show console." >}}

To learn what can be done using Sublime Text’s plugin API, [consult the documentation](https://www.sublimetext.com/docs/3/api_reference.html).</p>

### Distraction-Free Mode

*   `Cmd ⌘ + Ctrl ⌃ + Shift ⇧ + F` (Mac)
*   `Shift ⇧ + F11` (Windows and Linux)

For writers and others who need to be able to concentrate intently, Sublime Text has an even more minimalistic interface. Use the shortcut to toggle distraction-free mode on and off.</p>

{{< vimeo id="169699121" caption="Distraction-free mode." >}}

### Text Command-Line Helper

Sublime Text includes a command-line tool that makes it super-easy to work with files on the command line. To get it working on a Mac, you need to make it available in your shell.

Assuming you’ve placed Sublime Text in the “Applications” folder and that you have a `~/bin` directory in your path, you can run the following:

<pre><code class="language-bash">
ln -s "/Applications/Sublime
Text.app/Contents/SharedSupport/bin/subl" ~/bin/sublime
</code></pre>

{{< vimeo id="171070676" caption="Text command-line helper." >}}

To use it as the default editor for commands that prompt for input (such as `git commit`), set the `editor` environment variable.</p>

<pre><code class="language-bash">
export EDITOR='sublime -w'
</code></pre>

On Windows, you can use `subl.exe` in a similar way.</p>

## Conclusion

Sublime Text is full of such powerful shortcuts and commands. You probably won’t be able to remember these just by skimming this article; rather, you’ll need to practice as you’re going through it. List the most useful shortcuts for yourself, and refer to them regularly as you’re working with Sublime Text. Practice is the key. You are on your way to becoming a Sublime Text ninja.

{{< signature "ms, il, al, ml" >}}

