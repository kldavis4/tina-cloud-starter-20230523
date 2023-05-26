---
title: 'Getting The Most Out Of Git'
slug: getting-the-most-out-of-git
author: tobias-guenther
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9126ec6d-7bd2-424f-ae9b-077c16dd36e2/getting-the-most-out-of-git.jpg
date: 2021-02-09T12:00:00.000Z
summary: >-
  In this article, Tobias explores some of the less known but very useful features in Git. You’ll learn how to recover deleted commits, clean up your commit history, use submodules to manage third-party code and compose commits with precision &mdash; along with a <a href='https://www.git-tower.com/blog/git-cheat-sheet/?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=TOM'>friendly Git cheat sheet</a>.
description: >-
  In this article, Tobias explores some of the less known but very useful features in Git. You’ll learn how to recover deleted commits, clean up your commit history, use submodules to manage third-party code and compose commits with precision &mdash; along with a friendly Git cheat sheet.
categories:
  - Tools
  - Coding
  - Workflow
  - Git
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Fournova
  link: https://srv.buysellads.com/ads/long/x/T6IVIABXTTTTTT3CZGBMOTTTTTTQFUUMZATTTTTTETRXCUYTTTTTTBDW5JYFC5JGHRSU5R75KRWUVZZW2RSNPAJ5K2UNBZ7X5MBCBUSI2RBU6YSHFM7NBYZI23WNA7S2KHIN4OIQ27LLKRZW2MGNB7Z62HBNBGZF5MLUCRDE2R7UVQIM5JNMOYS32MYC4BZF2YOMVIB2
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2963410-591a-431d-b805-3cc431aa3c2e/tower-app-icon.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.fournova.com/">Tower</a> who have created the popular Git desktop GUI that helps so many folks work more easily and productively with Git. <em>Thank you!</em>
---

Not a single project today will get away without some sort of version control with Git under the hood. Knowing Git *well* helps you become a better developer, boost your developer’s workflow and truly improve the quality of your code base. However, that requires going a little bit outside of the comfort zone that we are all familiar with. As it turns out, there is a bit more to Git than just commit, push and pull.

Some developers stay true to the main principles in Git, and often that’s absolutely understandable. In the front-end world of ours, there are just so many sophisticated things to understand and get better at, that frankly Git is often not a high priority. As a side effect, many of the valuable techniques that can boost a developer’s workflow remain **unnoticed and rarely discovered**.

In this article, we'll explore four advanced Git tools, and hopefully, whet your appetite to learn even more about Git!

## Recovering Deleted Commits

You’re convinced that you’ve programmed yourself into a dead end because your last two commits lead nowhere! Understandably, you might want to undo them and start over.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21b0b502-6394-4002-93c7-03011e4fdd8d/1-reset-last-good-state.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21b0b502-6394-4002-93c7-03011e4fdd8d/1-reset-last-good-state.png" width="845" height="463" sizes="100vw" caption="What if you wanted to recover a deleted commit? That’s where Reflog comes in handy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21b0b502-6394-4002-93c7-03011e4fdd8d/1-reset-last-good-state.png'>Large preview</a>)" alt="Recovering deleted commits with reflog" >}}

Here’s one way to do this:

<pre><code class="language-bash">$ git reset --hard 2b504be
</code></pre>

But let’s also say that, moments later, you notice that you made a mistake: actually, the commits contained important data and you just lost valuable work! 😱

Your heart starts pumping, the sweat starts running &mdash; you know the drill. 🤯

Now, the million-dollar question is: How can we **get those seemingly deleted commits back**? Luckily, there is an answer: the "Reflog"!

### Using the Reflog to Recover Lost States

You can think of the Reflog as Git’s "diary": it’s the place where Git protocols every movement of the HEAD pointer. Or, in other words: all of the more interesting actions like when you commit, merge, checkout, rebase, cherry-pick and others. This, of course, makes it a perfect tool for those inevitable situations when things go wrong.

Let’s open the Reflog for our example scenario and see how it can help us:

<pre><code class="language-bash">$ git reflog
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc737a22-94da-4210-b397-7787de6d1723/2-reflog-cli.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc737a22-94da-4210-b397-7787de6d1723/2-reflog-cli.png" width="845" height="420" sizes="100vw" caption="Reflog in action, with a full diary of all commits, before and after the mistake. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc737a22-94da-4210-b397-7787de6d1723/2-reflog-cli.png'>Large preview</a>)" alt="Overview of commits listed via reflog" >}}

The first and most important thing to know about the Reflog is that it’s **ordered chronologically**. And indeed: the topmost (in other words: newest) item is our mishap when we had hastily used `git reset` and lost some commits.

The solution to fix our problem is pretty easy: we can simply return to *the state before* the mistake. And that state is clearly protocoled in the Reflog, right below our fatal `reset` command. To undo our mistake, we can simply use `git reset` once more to recover this seemingly lost state:

<pre><code class="language-bash">$ git reset e5b19e4
</code></pre>

You can also accomplish the same result a little bit faster. As a group of friendly and passionate developers on ["Tower" Git desktop GUI](https://www.git-tower.com/?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=TOM), we’ve been aiming to resolve common pain points around Git heads-on. So in our little tool, you can achieve the same results by simply hitting <kbd>CMD</kbd> + <kbd>Z</kbd> &mdash; as if you wanted to correct a simple typo in your text editor. In fact, the same hotkey is available for a family of different actions, e.g. when you’ve wrongfully deleted a branch, made a mistake with a merge operation, or committed something on the wrong branch.

{{< vimeo id="509917005" breakout="true" >}}

## Cleaning Up Your Commit History

While working on a new feature, the "beauty" of your commit history might not be your top priority &mdash; and understandably so: there are many other things to worry about. But once you’re finished and just before you merge your work into a team branch, it’s probably a good idea to hold on for a moment and just take a breath. Look at the **commit history** you’ve produced along the way and see if it could be improved: is it easily understandable? Are there commits that should actually *not* be included? Two commits that should be combined into one? Or a huge monster of a commit that should be broken up into smaller, more readable commits?

Cleaning up your commits before you integrate them into a team branch is important when we want to maintain a healthy code base. And Git’s **"Interactive Rebase"** tool is the perfect way to get there.

Interactive Rebase allows you to delete commits, rearrange them, combine multiple commits into one, or split up a big commit into multiple smaller ones. In this post, as an example, we’ll just take a look at how to **delete an old commit** that you don’t need anymore.

Let’s say that we don’t want the following commit anymore (e.g. because it contains sensitive data that shouldn’t have been committed in the first place):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e63f5832-a021-43c6-8a72-4d56501e5344/4-interactive-rebase-starting-situation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e63f5832-a021-43c6-8a72-4d56501e5344/4-interactive-rebase-starting-situation.png" width="845" height="415" sizes="100vw" caption="Picking a commit to delete from commit history &mdash; e.g. if it contains sensitive data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e63f5832-a021-43c6-8a72-4d56501e5344/4-interactive-rebase-starting-situation.png'>Large preview</a>)" alt="Picking a commit to delete from commit history" >}}

to correct this mistake, we’ll initiate an Interactive Rebase session, starting at the faulty commit’s *parent revision*:

<pre><code class="language-bash">git rebase -i 2b504be
</code></pre>

An editor window will then open and allow us to manipulate the selected part of our commit history:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43bcd74c-b45c-4c6c-8ad2-fa016436ea0a/5-interactive-rebase-mark-commit-with-drop.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43bcd74c-b45c-4c6c-8ad2-fa016436ea0a/5-interactive-rebase-mark-commit-with-drop.png" width="846" height="520" sizes="100vw" caption="Marking the commit with <code>drop</code> will delete it from the history. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43bcd74c-b45c-4c6c-8ad2-fa016436ea0a/5-interactive-rebase-mark-commit-with-drop.png'>Large preview</a>)" alt="Marking the commit with drop will delete it from the commit history" >}}

In our case, since we want to delete a commit, we simply mark up the respective line in the editor with the <code>drop</code> action keyword. Once we hit "Save" in our editor and close the window, the Interactive Rebase is completed &mdash; and the unwanted commit will have disappeared!

(Just a quick note: again, if you’re using a desktop GUI like [Tower](https://www.git-tower.com/?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=TOM), you can take a shortcut: simply right-click the unwanted commit and select the "Delete..." option from the contextual menu.)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b242831-24b1-4ace-a9c8-28fb9ce1f70c/6-interactive-rebase-delete-with-tower.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b242831-24b1-4ace-a9c8-28fb9ce1f70c/6-interactive-rebase-delete-with-tower.png" width="845" height="736" sizes="100vw" caption="Deleting a commit will not affect the code base, but delete it from the history. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b242831-24b1-4ace-a9c8-28fb9ce1f70c/6-interactive-rebase-delete-with-tower.png'>Large preview</a>)" alt="Deleting a commit in a GUI" >}}

As mentioned above, Interactive Rebase has a lot more use cases to offer! If you’d like to learn more about Interactive Rebase and what it can do, take a look at the free “[First Aid Kit for Git](https://www.git-tower.com/learn/git/first-aid-kit?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=TOM)”: a collection of short, helpful, and free videos, all around undoing mistakes with Git.

## Using Submodules To Manage Third-Party Code

In today’s complex software world, there’s hardly a project that *doesn't* include code from other sources: a module or library from a third party or even from your own team. Managing these modules in an elegant, pragmatic way greatly helps to reduce headaches!

In theory, you could simply copy and paste the necessary code files into your project and then commit them to your code base. But this comes with a couple of downsides. Most importantly, you’ll have a very hard time **updating third-party code** when new versions become available. You’d have to download the code again and copy-paste it &mdash; again and again.

Additionally, it’s considered bad practice if you squeeze multiple projects (your actual project and all the third-party libraries you might need) into a single Git repository. This mixes external code with our own, unique project files.

A much better way to do this is to use Git’s **"Submodule" structure**: this allows you to include third-party code simply as a Git repository inside your actual project’s Git repository. This means that all code bases remain neatly separated.

Including a third-party module / library is as easy as executing the following Git command:

<pre><code class="language-bash">$ git submodule add https://github.com/djyde/ToProgress
</code></pre>

This command will download a clone of the specified Git repository into your project. You’ll be left with a fully-functional, nicely separated Git repository of your third-party code. Tidy, clean and flexible.

Submodules, admittedly, are quite a complex topic when it comes to handling them in practice. If you want to understand them a bit more thoroughly, check out the “[Submodules](https://www.git-tower.com/learn/git/ebook/en/desktop-gui/advanced-topics/submodules/)” chapter of the free "Learn Version Control with Git" online book.

## Composing Commits With Precision

There’s a golden rule in version control: **a commit should only contain changes from a single issue!** When you stick to this rule, you will create commits that are easy to understand. When you don’t &mdash; when multiple issues and topics get crammed into the same commit &mdash; you will inflict chaos on your code base in almost no time.

In practice, this means that you **create separate commits for each and every topic**. Even if it’s just a small bug fix where you’re changing only a semicolon: it’s a topic of its own, so it gets a commit of its own!

But in the messy real world, we often don’t *work* at only one topic at a time. Or we think we do, and only later discover that our code from the last three hours actually involves three different topics. This trickles down to individual files: often, the changes in a single file belong to multiple topics.

That’s when adding a *complete* file to the next commit isn’t the best strategy anymore.

### Staging Selected Parts of Your Changed Files

In the example case below, you can see that we currently have **two chunks** (= parts or areas) of modifications in our file <code>imprint.html</code>:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/114035d0-1fc5-472c-b92e-563fa4f5b3f2/7-staging-parts-of-changes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/114035d0-1fc5-472c-b92e-563fa4f5b3f2/7-staging-parts-of-changes.png" width="845" height="822" sizes="100vw" caption="Staging selected parts of your changed files. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/114035d0-1fc5-472c-b92e-563fa4f5b3f2/7-staging-parts-of-changes.png'>Large preview</a>)" alt="Staging selected parts of your changed files. " >}}

Let’s say that the first chunk belongs to one topic (maybe we’re in the process of unifying and cleaning up all page titles in our project). And let’s also say that the second chunk belongs to another, completely unrelated topic.

A simple `git add imprint.html`, i.e. adding the whole file to Staging, would cram all of its changes into the same commit. Our colleagues, then, would have a hard time understanding what this particular commit was really about. Seeing some titles being changed, they might think it was only about the “title clean-up project”, but they might very well overlook the other changes.

Luckily, Git allows us to **precisely select the chunks** we want to put into the next commit! All we have to do is add the `-p` flag to our `git add` command:

<pre><code class="language-bash">$ git add -p imprint.html
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd1057bc-fbe7-41ee-9596-4b1e061f21f8/8-git-add-p.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd1057bc-fbe7-41ee-9596-4b1e061f21f8/8-git-add-p.png" width="845" height="689" sizes="100vw" caption="Precisely selecting chunks we want to put into the next commit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd1057bc-fbe7-41ee-9596-4b1e061f21f8/8-git-add-p.png'>Large preview</a>)" alt="Precisely selecting chunks we want to put into the next commit" >}}

Git now takes us by the hand and walks us through each and every chunk of changes in that file. And for each one, it asks us a simple question: “Stage this chunk?”

Let’s type <kbd>Y</kbd> (for “Yes”) for the first one and <kbd>N</kbd> for the second one. When we then actually make our commit, only the first chunk of changes will be included. The second one remains as an uncommitted local change in our working copy for a later, separate commit.

If you’re using Git in a desktop GUI, you might be able to do this right through the interface:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88713005-7483-45ec-ad61-9481f9d077b7/9-staging-chunks-in-gui.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88713005-7483-45ec-ad61-9481f9d077b7/9-staging-chunks-in-gui.png" width="845" height="642" sizes="100vw" caption="Staging and discarding chunks is also possible in a desktop GUI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88713005-7483-45ec-ad61-9481f9d077b7/9-staging-chunks-in-gui.png'>Large preview</a>)" alt="Staging and sciard chunk buttons for separate pieces of the commit" >}}

## Becoming More Productive with Git

This short article was just a short glimpse into some of the advanced features in Git. But I sincerely hope it shows that Git has so many powerful features under the hood! From Interactive Rebase to Submodules and from the Reflog to File History, it pays to learn these advanced features because they help you become more productive and make fewer mistakes.

If you want to dive deeper, here are some helpful (and free) resources:

- **Git Cheat Sheet**<br />If you want to keep the most important commands at hand, the [“Git Cheat Sheet"](https://www.git-tower.com/blog/git-cheat-sheet/?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=TOM) might be for you. Available in English, German, Spanish, Portuguese, Arabic and Chinese.
- **Undoing Mistakes**<br />Git is a perfect safety net for when things go wrong. Learning about the different “undo” features in Git is time well spent for any developer. The ["First Aid Kit for Git"](https://www.git-tower.com/learn/git/first-aid-kit/?utm_source=smashingmagazine&utm_medium=guestpost&utm_campaign=TOM), a collection of short videos, provides a great introduction.

Have fun becoming a better developer!

{{< signature "vf, il" >}}
