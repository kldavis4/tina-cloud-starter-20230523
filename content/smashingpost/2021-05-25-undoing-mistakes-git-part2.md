---
title: 'A Guide To Undoing Mistakes With Git (Part 2)'
slug: undoing-mistakes-git-part2
author: tobias-guenther
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/211042ae-7a72-42ba-804e-9f8132815200/undoing-mistakes-git-part1.jpg
date: 2021-05-25T14:00:00.000Z
summary: >-
  Mistakes. These cruel villains do not even stop at the beautiful world of software development. But although we cannot avoid making mistakes, we can learn to undo them! This article will show the right tools for your daily work with Git. You might want to [check the first article of the series](https://www.smashingmagazine.com/2021/05/undoing-mistakes-git-part1/) as well.
description: >-
  Mistakes. These cruel villains do not even stop at the beautiful world of software development. But although we cannot avoid making mistakes, we can learn to undo them! This post will show the right tools for your daily work with Git.
categories:
  - Git
  - Tools
  - Guides
  - JavaScript
---

In this second part of our series on "Undoing Mistakes with Git", we’ll bravely look danger in the eye again: I’ve prepared four new doomsday scenarios &mdash; including, of course, some clever ways to save our necks! But before we dive in: take a look at the check out [previous articles on Git](https://smashingmagazine.com/category/git/) for even more self-rescue methods that help you undo your mistakes with Git!

Let’s go!

## Recovering a Deleted Branch Using the Reflog

Have you ever deleted a branch and, shortly after, realized that you shouldn’t have? In the unlikely event that you don’t know this feeling, I can tell you that it’s not a good one. A mixture of sadness and anger creeps up on you, while you think of all the hard work that went into that branch’s commits, all the valuable code that you’ve now lost.

Luckily, there’s a way to bring that branch back from the dead &mdash; with the help of a Git tool named "Reflog". We had used this tool in the [first part of our series](https://www.smashingmagazine.com/2021/05/undoing-mistakes-git-part1/), but here’s a little refresher: the Reflog is like a journal where Git notes every movement of the HEAD pointer in your local repository. In other, less nerdy words: any time you checkout, commit, merge, rebase, cherry-pick, and so on, a journal entry is created. This makes the Reflog a perfect safety net when things go wrong!

Let’s take a look at a concrete example:

<pre><code class="language-bash">$ git branch
* feature/login
master
</code></pre>

We can see that we currently have our branch `feature/login` checked out. Let’s say that this is the branch we’re going to delete (inadvertently). Before we can do that, however, we need to switch to a different branch because we cannot delete our current HEAD branch!

<pre><code class="language-bash">$ git checkout master
$ git branch -d feature/login
</code></pre>

Our valuable feature branch is now gone &mdash; and I’ll give you a minute to (a) understand the gravity of our mistake and (b) to mourn a little. After you’ve wiped away the tears, we need to find a way to bring back this branch! Let’s open the Reflog (simply by typing `git reflog`) and see what it has in store for us:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee79e32-1818-4bf4-8aa3-68f194545b54/reflog-deleted-branch-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee79e32-1818-4bf4-8aa3-68f194545b54/reflog-deleted-branch-2x.png" width="800" height="266" sizes="100vw" caption="Git’s Reflog protocols all major actions in our local repository. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee79e32-1818-4bf4-8aa3-68f194545b54/reflog-deleted-branch-2x.png'>Large preview</a>)" alt="Git’s Reflog protocols all major actions in our local repository" >}}

Here are some comments to help you make sense of the output:

- First of all, you need to know that the Reflog sorts its entries chronologically: the newest items are at the top of the list.
- The topmost (and therefore newest) item is the `git checkout` command that we performed before deleting the branch. It’s logged here in the Reflog because it’s one of these "HEAD pointer movements" that the Reflog so dutifully records.
- To undo our grave mistake, we can simply return to the state _before_ that &mdash; which is also cleanly and clearly recorded in the Reflog!

So let’s try this, by creating a new branch (with the name of our "lost" branch) that starts at this "before" state SHA-1 hash:

<pre><code class="language-bash">$ git branch feature/login 776f8ca
</code></pre>

And voila! You’ll be delighted to see that we’ve now restored our seemingly lost branch! 🎉

If you’re using a [Git desktop GUI like "Tower"](https://www.git-tower.com/?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=undoing-mistakes-02), you can take a nice shortcut: simply hit <kbd>CMD</kbd> + <kbd>Z</kbd> on your keyboard to undo the last command &mdash; even if you’ve just violently deleted a branch!

{{< vimeo id="554256230" caption="A desktop GUI like Tower can make the process of undoing mistakes easier." breakout="true" >}}

{{% feature-panel %}}

## Moving a Commit to a Different Branch

In many teams, there’s an agreement to not commit on long-running branches like `main` or `develop`: branches like these **should only receive new commits through integrations** (e.g. merges or rebases). And yet, of course, mistakes are inevitable: we sometimes forget and commit on these branches nonetheless! So how can we clean up the mess we made?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df4871c-b565-48af-8446-2ec35dcb0f86/commit-on-wrong-branch-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df4871c-b565-48af-8446-2ec35dcb0f86/commit-on-wrong-branch-2x.png" width="800" height="343" sizes="100vw" caption="Our commit landed on the wrong branch. How can we move it to its correct destination branch? (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df4871c-b565-48af-8446-2ec35dcb0f86/commit-on-wrong-branch-2x.png'>Large preview</a>)" alt="Moving a commit to its correct destination branch" >}}

Luckily, these types of problems can be easily corrected. Let’s roll up our sleeves and get to work.

The first step is to switch to the correct destination branch and then move the commit overusing the `cherry-pick` command:

<pre><code class="language-bash">$ git checkout feature/login
$ git cherry-pick 776f8caf
</code></pre>

You will now have the commit on the desired branch, where it should have been in the first place. Awesome!

But there’s still one thing left to do: we need to clean up the branch where it _accidentally_ landed at first! The `cherry-pick` command, so to speak, created a copy of the commit &mdash; but the original is still present on our long-running branch:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d362e9cd-0b1a-4a8c-ad97-e03d083b243a/remove-commit-from-branch-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d362e9cd-0b1a-4a8c-ad97-e03d083b243a/remove-commit-from-branch-2x.png" width="800" height="619" sizes="100vw" caption="We’ve successfully created a copy of the commit on the correct branch, but the original is still here &mdash; on the wrong branch. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d362e9cd-0b1a-4a8c-ad97-e03d083b243a/remove-commit-from-branch-2x.png'>Large preview</a>)" alt="A copy of the commit on the correct branch, but the original is still shown to be on the wrong branch" >}}

This means we have to switch back to our long-running branch and use `git reset` to remove it:

<pre><code class="language-bash">$ git checkout main
$ git reset --hard HEAD~1
</code></pre>

As you can see, we’re using the `git reset` command here to erase the faulty commit. The `HEAD~1` parameter tells Git to "go back 1 revision behind HEAD", effectively erasing the topmost (and in our case: unwanted) commit from the history of that branch.

And voila: the commit is now where it should have been in the first place _and_ our long-running branch is clean &mdash; as if our mistake had never happened!

{{% ad-panel-leaderboard %}}

## Editing the Message of an Old Commit

It’s all too easy to smuggle a typo into a commit message &mdash; and only discover it much later. In such a case, the good old `--amend` option of `git commit` cannot be used to fix this problem, because it only works for the very last commit. To correct any commit that is older than that, we have to resort to a Git tool called "Interactive Rebase".

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea8f2b3b-17e4-46e4-bafa-ee428927cc8d/edit-commit-message-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea8f2b3b-17e4-46e4-bafa-ee428927cc8d/edit-commit-message-2x.png" width="800" height="516" sizes="100vw" caption="Here’s a commit message worth changing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea8f2b3b-17e4-46e4-bafa-ee428927cc8d/edit-commit-message-2x.png'>Large preview</a>)" alt="A commit message worth changing" >}}

First, we have to tell Interactive Rebase which part of the commit history we want to edit. This is done by feeding it a commit hash: the _parent_ commit of the one we want to manipulate.

<pre><code class="language-bash">$ git rebase -i 6bcf266b
</code></pre>

An editor window will then open up. It contains a list of all commits _after_ the one we provided as a basis for the Interactive Rebase in the command:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b82e30-28e1-46d9-b526-ec3f17c78286/interactive-rebase-reword-commit-list-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b82e30-28e1-46d9-b526-ec3f17c78286/interactive-rebase-reword-commit-list-2x.png" width="800" height="367" sizes="100vw" caption="The range of commits we selected for editing in our Interactive Rebase session. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b82e30-28e1-46d9-b526-ec3f17c78286/interactive-rebase-reword-commit-list-2x.png'>Large preview</a>)" alt="Showing the range of commits we selected for editing in our Interactive Rebase session" >}}

Here, it’s important that you _don’t_ follow your first impulse: in this step, we do _not_ edit the commit message, yet. Instead, we only tell Git what _kind of manipulation_ we want to do with which commit(s). Quite conveniently, there’s a list of action keywords noted in the comments at the bottom of this window. For our case, we mark up line #1 with `reword` (thereby replacing the standard `pick`).

All that’s left to do in this step is to save and close the editor window. In return, a new editor window will open up that contains the current message of the commit we marked up. And _now_ is finally the time to make our edits!

Here’s the whole process at a glance for you:

{{< vimeo id="554255938" caption="Using Interactive Rebase to edit an old commit’s message, from start to finish." breakout="true" >}}

## Correcting a Broken Commit (in a Very Elegant Way)

Finally, we’re going to take a look at `fixup`, the Swiss Army Knife of undoing tools. Put simply, it allows you to fix a broken/incomplete/incorrect commit after the fact. It’s truly a wonderful tool for two reasons:

1. **It doesn’t matter what the problem is.**  
You might have forgotten to add a file, should have deleted something, made an incorrect change, or simply a typo. `fixup` works in all of these situations!
2. **It is extremely elegant.**  
Our normal, instinctive reaction to a bug in a commit is to produce a _new_ commit that fixes the problem. This way of working, however intuitive it may seem, makes your commit history look very chaotic, very soon. You have "original" commits and then these little "band-aid" commits that fix the things that went wrong in the original commits. Your history is littered with small, meaningless band-aid commits which makes it hard to understand what happened in your codebase.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a362d6e3-489b-4eee-a5c6-c773206f1ee9/fixing-commits-with-bandaids-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a362d6e3-489b-4eee-a5c6-c773206f1ee9/fixing-commits-with-bandaids-2x.png" width="800" height="458" sizes="100vw" caption="Constantly fixing small mistakes with “band-aid commits” makes your commit history very hard to read. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a362d6e3-489b-4eee-a5c6-c773206f1ee9/fixing-commits-with-bandaids-2x.png'>Large preview</a>)" alt="Your commit history can be very hard to read if you constantly fix small mistakes with so-called band-aid commits" >}}

This is where `fixup` comes in. It allows you to still make this correcting band-aid commit. But here comes the magic: it then applies it to the original, broken commit (repairing it that way) and then discards the ugly band-aid commit completely!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6122872-491a-4a24-83ac-2db6331f9956/fixup-workflow-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6122872-491a-4a24-83ac-2db6331f9956/fixup-workflow-2x.png" width="800" height="435" sizes="100vw" caption="Fixup applies your corrections to the original commit and then disposes of the superfluous band-aid commit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6122872-491a-4a24-83ac-2db6331f9956/fixup-workflow-2x.png'>Large preview</a>)" alt="Fixup applies your corrections to the original commit and then disposes of the superfluous band-aid commit" >}}

We can go through a practical example together! Let’s say that the selected commit here is broken.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc43d8cf-8e3b-45c9-8a6d-6a30d1ebfe1c/fixup-broken-commit-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc43d8cf-8e3b-45c9-8a6d-6a30d1ebfe1c/fixup-broken-commit-2x.png" width="800" height="500" sizes="100vw" caption="The selected commit is incorrect &mdash; and we’re going to fix it in an elegant way. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc43d8cf-8e3b-45c9-8a6d-6a30d1ebfe1c/fixup-broken-commit-2x.png'>Large preview</a>)" alt="Fixing the selected incorrect commit in an elegant way" >}}

Let’s _also_ say that I have prepared changes in a file named `error.html` that will solve the problem. Here’s the first step we need to make:

<pre><code class="language-bash">$ git add error.html
$ git commit --fixup 2b504bee
</code></pre>

We’re creating a new commit, but we’re telling Git this is a special one: it’s a fix for an old commit with the specified SHA-1 hash (`2b504bee` in this case).

{{% ad-panel-leaderboard %}}

The second step, now, is to start an Interactive Rebase session &mdash; because `fixup` belongs to the big toolset of Interactive Rebase.

<pre><code class="language-bash">$ git rebase -i --autosquash 0023cddd
</code></pre>

Two things are worth explaining about this command. First, why did I provide `0023cddd` as the revision hash here? Because we need to start our Interactive Rebase session at the parent commit of our broken fellow.

Second, what is the `--autosquash` option for? It takes a lot of work off our shoulders! In the editor window that now opens, everything is already prepared for us:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e78ea1-12dc-4879-807a-7eb5b623ea68/fixup-editor-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e78ea1-12dc-4879-807a-7eb5b623ea68/fixup-editor-2x.png" width="800" height="293" sizes="100vw" caption="The Interactive Rebase session window (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e78ea1-12dc-4879-807a-7eb5b623ea68/fixup-editor-2x.png'>Large preview</a>)" alt="The Interactive Rebase session window" >}}

Thanks to the `--autosquash` option, Git has already done the heavy lifting for us:

1. It marked our little band-aid commit with the `fixup` action keyword. That way, Git will combine it with the commit directly _above_ and then discard it.
2. It also reordered the lines accordingly, moving our band-aid commit directly below the commit we want to fix (again: `fixup` works by combining the marked-up commit with the one _above_!).

In short: There’s nothing to do for us but close the window!

Let’s take a final look at the end result.

- The formerly broken commit is fixed: it now contains the changes we prepared in our band-aid commit.
- The ugly band-aid commit itself has been discarded: the commit history is clean and easy to read &mdash; as if no mistake had occurred at all.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b96df80d-96e0-4a90-ba35-f616eccc8e5c/fixup-end-situation-2x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b96df80d-96e0-4a90-ba35-f616eccc8e5c/fixup-end-situation-2x.png" width="800" height="377" sizes="100vw" caption="The end result after using the fixup tool: a clean commit history! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b96df80d-96e0-4a90-ba35-f616eccc8e5c/fixup-end-situation-2x.png'>Large preview</a>)" alt="An example of how a clean commit history looks like" >}}

## Knowing How to Undo Mistakes is a Superpower

Congratulations! You are now able to save your neck in many difficult situations! We cannot really avoid these situations: no matter how experienced we are as developers, mistakes are simply part of the job. But now that you know how to deal with them, you can face them with a laid-back heart rate. 💚

If you want to learn more about undoing mistakes with Git, I can recommend the free "[First Aid Kit for Git](https://www.git-tower.com/learn/git/first-aid-kit?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=undoing-mistakes-02)", a series of short videos about exactly this topic.

Have fun making mistakes &mdash; and, of course, undoing them with ease!

{{< signature "vf, il" >}}
