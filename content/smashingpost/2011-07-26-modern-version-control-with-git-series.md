---
title: 'Modern Version Control With Git'
slug: modern-version-control-with-git-series
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4232e0f7-4bc3-410a-bbfe-08ad79b2cac1/multiple-code-illu.jpg
date: 2011-07-26T11:01:15.000Z
author: tobias-guenther
summary: >-
  The benefits of using a “version control system” are many. It can improve software quality, facilitate collaboration and even help you become a better developer or designer. In this article, Tobias Günther will introduce you to the increasingly popular <a href="https://git-scm.com/">Git</a> version control system. He’ll discuss the main benefits and features of Git and finally demonstrate how to integrate it into your workflow.
description: >-
  In this article, Tobias Günther will introduce you to the increasingly popular Git version control system. Find the main benefits and features of Git and finally discover how to integrate it into your workflow.
categories:
  - Git
  - Tools
  - Techniques
  
---
In this article, we will cover the basic background information for understanding how &mdash; and more importantly, why &mdash; to use Git. Later, we will take a closer look at Git’s features, including branching and merging, and discuss how to use it in your own design and development projects.

{{% feature-panel %}}

## Git: Born Of Necessity

Linus Torvalds was unsatisfied: none of the version control systems (VCS) available in 2005 met his requirements. Once the proprietary version control system BitKeeper changed its license agreement, it couldn’t be used to manage the Linux kernel project anymore. An alternative had to be found, one that was distributed, scalable and &mdash; above all &mdash; fast.

The Linux community took action by starting two new projects: <a title="git-scm.com" href="https://git-scm.com/">Git</a> and Mercurial. Both have their origins in this emergency, and they are among today’s leading distributed version control systems. Git is now used in countless well-known open-source projects: the Linux kernel, jQuery, Ruby on Rails, Symfony, CakePHP, Debian, Fedora, Perl and many more. The large number of tutorials and tools, including desktop clients, shows how important Git has become.

## Centralized Vs. Distributed

<figure><img class="103896 alignnone" title="centralized-vcs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1860f04b-0eac-467a-8b65-3b0c4ee5791b/git1-1-centralized-vcs.gif" alt="screenshot" width="296" height="205" /></figure>

Git (like Mercurial) is a “distributed” version control system (DVCS). The classic systems like Subversion and CVS, in contrast, function as centralized systems (CVCS).

In centralized systems, there is only one “master” repository, which every developer feeds their changes into. Every action must be synchronized with this central repository. And because it usually resides on a central server, each action has to pass through the network &mdash; leaving a developer unable to work if they happen to have no network connection.

<figure><img class="103897 alignnone" title="distributed-vcs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21c5442f-3d7c-484a-889d-13913b7fdd7c/git1-2-distributed-vcs.gif" alt="screenshot" width="345" height="268" /></figure>

In distributed systems, each developer has their own full-fledged repository on their computer. In most set-ups there’s an additional central repository on a server that’s used for sharing. However, this is not a requirement; every developer can perform all important actions in their local repository: committing changes, viewing differences between revisions, switching branches, etc.

### Git’s Advantages

One of Git’s main advantages is its distributed nature. It doesn’t matter whether you’re using a complex set-up with multiple remote repositories or you have just one central server to share code (working “Subversion style”). A DVCS can be used independently of any one person’s workflow. Being able to work offline is an important advantage of DVCS for many developers. You can work without constraints, even if you’re not connected to the network.

<figure><img class="103903 " title="performance" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a95579-ae1c-489f-944e-8f3f7b508df5/status-diff-screenshot.jpg" alt="screenshot" width="313" height="341" /><figcaption>Git saves quite some time in your daily workflow.</figcaption></figure>

Speed is another important factor, and the differences between Git and other DVCS here are evident. In almost any situation, Git is faster than other modern systems, such as Mercurial and Bazaar. One of the reasons for Git’s remarkable speed is that it was written in C. Another reason is that it was designed to work with the Linux kernel and therefore has to perform well even under huge amounts of data.

Another convenience: every local Git repository can serve as a full-fledged back-up, because it contains the project’s complete history. And considering that almost every action in Git only adds data, losing data is pretty hard to do.

The biggest advantages, however, lie in Git’s feature set: in how it deals with code and in its tools and workflows. We’ll take a closer look at things like the staging area, the stash and the concept of branching later on.

### The Local Git Repository

In SVN, every directory that’s under version control is assigned a hidden *.svn* folder, which saves all relevant meta data for that directory. Have you ever (inadvertently, of course) deleted or moved this magical folder? If so, then you’ll appreciate that Git has only one of these folders. This means you can move, delete or rename in your favorite editor or file browser as you wish, without any headaches the next morning.

This folder (*.git*) resides in the root directory of your project and makes up your local repository. The actual files you work with comprise your so-called “working directory” (or “working tree”).

In addition to the *.git* repository and the working directory, the third crucial part is the so-called “staging area.” This enables you to precisely define which changes you want to have in your next commit &mdash; even down to individual lines in a file.

Let’s consider this more carefully, because it’s one of Git’s best features. Say you have modified 10 files, and you realize that splitting these changes into two separate commits would be best (because every commit should contain only related changes and not be a hodgepodge). Using the staging area, you can define exactly which changes to commit and which to leave for a later commit.

Technically, the staging area is nothing more than a file named *index* that lies in your local *.git* repository. That’s why it’s sometimes referred to as the index.

### States Of Files

In Git, a file in your working directory can be in one of several states. The most basic distinction is between “tracked” and “untracked.” A file is tracked if it’s already under version control; in this case, Git observes all changes in that file. If it’s not (yet) saved in your Git repository, then it’s treated as untracked.

Tracked files can be in one of the following three states:

*   **Unmodified or committed**. The file is in its last committed state and therefore has no local modifications.
*   **Modified**. The file has been changed since it was last committed.
*   **Staged**. The file was not only changed but also added to the staging area, meaning that the changes will be included in the next commit. Because a file can be staged partially, it’s entirely possible for it to be both staged and modified.

{{% ad-panel-leaderboard %}}

## A Basic Workflow

A typical workflow in Git usually consists of the following steps:

1.  You modify, create or delete files in your working directory. Your favorite editor or file browser is perfectly suited to this job.
2.  You execute the `git status` command in the command line to see an overview of what has been changed. People use this command rather frequently in their workflow to stay on top of things.
3.  You add all changes for the next commit to the staging area using the `git add` command.
4.  Finally, you execute `git commit` to save the staged changes in your local repository.

<figure><img class="103906 " title="git-status" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7929d136-227f-470f-90e1-97fdeecac9d1/git1-4-git-status.gif" alt="screenshot" width="481" height="274" /><figcaption>The <code>git status</code> command gives you an overview of the state of your working directory.</figcaption></figure>

### Hashes Instead Of Revision Numbers

I’ll try to break this to you gently: Git doesn’t understand revision numbers.

In a CVCS such as Subversion, every commit is assigned a consecutive revision number. This doesn’t work in DVCS anymore. Because commits are created locally, the system can’t assign consecutive numbers. Imagine the developers on a team working on their own, producing commits locally, and then publishing their work on a shared remote repository as they go along. When an individual commit is created locally, there’s no way for Git to foresee the eventual order.

<figure><img class="103907 " title="git-log" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ad7f011-2214-4958-8cab-5936761423fa/git1-5-git-log.gif" alt="screenshot" width="300" height="84" /><figcaption>A short summary of a commit in Git.</figcaption></figure>

So, Git uses SHA-1 hashes to identify commits (and all other objects) internally. SHA-1 hashes are 40-character checksums that are unique, like conventional revision numbers, but with the benefit of being compatible with DVCS.

### Installation And Tools

Thanks to graphical installers and package managers, installing Git has become very easy. The steps on all major platforms are explained in detail in Scott Chacon’s free eBook <a title="Pro Git eBook" href="https://progit.org/book/ch1-4.html">Pro Git</a>.

Typically, Git is used from the command line. In many scenarios, however, a desktop client (like <a title="Tower - Git Client for Mac OS X" href="https://www.git-tower.com">Tower</a> on Mac OS [*author’s product*] or <a title="Tortoise Git" href="https://code.google.com/p/tortoisegit/">Tortoise Git</a> on Windows) can make life a lot easier.

## Improve Development Quality

“Complex” is often used to describe the <a title="Git Version Control System Website" href="https://git-scm.com/">Git version control system</a> (VCS). At least compared to classic VCS’ like Subversion, Git does indeed have a steeper learning curve.

When inviting people to learn a “complex” new technology, you’ll hardly get volunteers. But what if the technology could improve software quality and maybe even your own way of developing software? Git is such a technology for which investing time is worth it. Moreover, desktop clients such as <a title="Tower - Git Client for Mac OS X" href="https://www.git-tower.com">Tower</a> for Mac OS (*disclaimer: this is the author’s product*) and <a title="Tortoise Git for Windows" href="https://code.google.com/p/tortoisegit/">Tortoise Git</a> for Windows make a lot of the tasks easier.

### Installation And Help

If a recent version of Git is not installed on your machine, you can quickly and easily catch up by, for example, reading the instructions in Scott Chacon’s free eBook <a title="ProGit eBook" href="https://progit.org/book/ch1-4.html">*Pro Git*</a>. I’ll mention commands only briefly in this article. To get more detailed descriptions and parameter listings, you can use <code>git help &lt;command&gt;</code> in the command line or browse the <a title="GitRef" href="https://gitref.org">GitRef</a> online.

## Creating And Cloning Repositories

Having a repository is the most basic requirement for working in Git. If there is not one for your current project or if you’re starting afresh, then create a new repository in the current location by executing <code>git init</code> in the command line. If a remote repository already exists on a server, then you can get it via <code>git clone</code> on your machine. You can learn more about <code>git clone</code> on the <a href="https://gitref.org/creating/#clone">GitRef website</a>.

## Committing Changes

After working for some time, you’ll have a couple of new, deleted or modified files that you’ll want to save to your local repository as commits. As a first step, we’ll use <code>git status</code> to show us which changes we currently have in our working directory.

To add certain changes to the next commit, you have to explicitly add them to Git’s “staging area.” The command <code>git add</code> is used for this purpose. Let’s look at a concrete scenario:

<figure><img title="git-status" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f73384d-301d-461d-a3ec-d8bb15d0580e/git2-1-git-status.gif" alt="screenshot" width="481" height="274" /></figure>

### git add

The paragraph that begins “Changes to be committed” lists all of the files that will be included in the next commit. The changes had to be added to the staging area via <code>git add</code>.

The paragraph that begins “Changes not staged for commit” lists all of the files that have been changed but that have not been added to the staging area. Therefore, they won’t be included in our next commit but will remain simply as changes in our working directory.

The last paragraph lists “Untracked files,” files that aren’t under version control yet. In other words they are unknown to Git.

You might have spotted a little peculiarity: *error.html* is listed twice! That’s because we staged some of the changes in this file, while leaving other changes in the same file unstaged. This feature &mdash; staging individual files or even parts of a file &mdash; enables us to create extremely granular commits that really only contain related changes.

### git commit

After having composed the commit exactly as we want it to be, we can save it to our local repository via <code>git commit</code>.

## Commit History

<figure><img title="git-log-simple" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1497addc-be1c-4c69-af75-0acbc6e4997f/git2-2-git-log-simple.gif" alt="screenshot" width="305" height="248" /></figure>

Once a repository contains a couple of commits, we should look into its history (or “log”). The <code>git log</code> command gives us an overview of the last few commits. Git log’s default output shows each commit with its SHA-1 hash (which is the equivalent of a revision number in a classic centralized VCS, or CVCS), its author, the date and the message used.

### Customizing git log

You can bend the presentation of <code>git log</code> almost completely to your will. Using the parameter <code>--oneline</code>, for example, reduces the output to a single line per commit. Using <code>-p</code> adds the “diff” (or patch) to every commit, thereby showing you what detailed changes were introduced. Customization can be taken to the point where you have your very own output format:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc579979-af0d-47e1-95ef-12c21d2a0450/git2-3-git-log-format.gif"><img title="git2_3_git-log-format" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc579979-af0d-47e1-95ef-12c21d2a0450/git2-3-git-log-format.gif" alt="" width="410" height="71" /></a></figure>

## Branching And Merging

Branching is often referred to as Git’s killer feature, and rightly so. If you already know the term from another VCS like Subversion, then take an unbiased, fresh look at the topic. Using branches in Git is extremely easy and fast because they have been a core feature since the very beginning. They’re certainly one of the most important tools in a developer’s daily work. But what are they actually used for?

Branches allow you to cleanly separate variants or features in your code base. “Separation of concerns” is a good term for this.

### When To Use Branching

Take the following scenario. At a certain point, you decide to develop a new feature. To separate it from your other development work, you create a new branch, based on the current status. The <code>git branch</code> command creates the new branch, while <code>git checkout</code> makes it your current working branch.

After having implemented a couple of new features, you commit the current status to this branch (C2 in the sketch below). But you haven’t yet finished developing the new feature when an urgent bug report forces you to continue working on your code’s main line (your production or “live” code).

After having switched back (via <code>git checkout</code>) to your master branch, you commit the fix for the problem (C3). Again, you switch to your feature branch and commit some more changes (C4) to complete the development for this feature. Finally, you use <code>git merge</code> to unite the two branches again (C5).

<figure><img title="branches" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9279f98e-e669-437c-9e1a-d0edb2507af1/git2-4-branches.gif" alt="screenshot" width="366" height="98" /></figure>

Imagine this scenario without branches. Because you already had changes that belonged to an unfinished, not yet releasable feature, you would have been mixing two different concerns (the experimental feature and the bug fix in your production code).

With only one feature, the problem might not have been major. But in larger projects, with numerous parallel features and development stages, such processes quickly become confusing and error-prone without branches.

Of course, Git is not the only VCS that uses the concept of branches, but it does make branching easier, faster and more effortless than any other system. As soon as you discover branching in Git, switching your active branch a dozen times a day or creating a new branch for every bug fix, however small, becomes totally run of the mill. Greater clarity and a clear separation of code is worthwhile in the long run.

### Terms Related To Branching

The currently active branch is called “HEAD” in Git. Switching the HEAD is done with the <code>git checkout</code> command (not related to the <code>checkout</code> command in SVN). Your working directory will then contain the files that belong to this branch (or, more precisely, that belong to the last commit in this branch).

## Sharing Code: Working With Remote Repositories

Remote repositories are used to make your code available to teammates and to integrate code from other developers into your local repository. With <code>git remote add</code>, you can connect any number of remotes to your local repository.

To publish local commits from your current branch to a remote repository, use the <code>git push</code> command.

Integrating remote changes into your local repository, on the other hand, is done via <code>git fetch</code>. This downloads all of the changes from the remote server to your local computer, but it does not modify the files in your working directory in any way!

You can decide for yourself when to integrate the downloaded changes into your current HEAD via <code>git merge</code>. Alternatively, you can use <code>git pull</code> to combine downloading and merging into one step.

<figure><img title="remotes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a1014d-9a2d-41c0-a734-2cc5296b4a18/git2-5-remotes.jpg" alt="screenshot" width="500" /></figure>

As with most things, and as anyone who has worked with Git for a while knows, there’s more than one way to skin a cat. A lot of tasks can be performed with a couple of basic commands. However, a few advanced concepts and tricks will sometimes help you achieve your goals more elegantly.

## Advanced Concepts

### Stash: The Clipboard

The “stash” is one such feature. In some situations, a “clean” working directory is recommended (or even essential). That means there shouldn’t be any local changes (for example, when switching the current branch).

Imagine the following scenario. You’ve been working on a new feature for several hours, when suddenly a critical bug report comes in. Of course, you’ve already changed a couple of files. But now you must switch branches to be able to work on your current production code. You could simply commit your changes &mdash; but they’re only half done (and committing stuff that is only half done is bad karma!).

The stash helps you solve precisely this dilemma. All current changes are saved on this clipboard, and your working directory is left in a clean condition. As soon as you’re done fixing that bug, you can return to working on your feature &mdash; and simply restore all stashed changes.

### Staging Parts Of Files

A large commit that mixes a lot of different topics is hard for other developers to understand, and rolling back problems will be hard if problems should occur. That’s why creating granular commits that contain only related changes is so important in version control.

Git helps you do this by enabling you to add parts of a changed file to the staging area. If you execute <code>git add</code> with the <code>-p</code> parameter, Git lets you choose for every part of the file whether you want to stage it or not. This way, you can control very precisely which changes should go into your next commit &mdash; and which should remain for a later commit.

### Tracking Branches

If you’ve already glanced at the configuration file of one of your local Git repositories (*.git/config*), you might have spotted one of these sections:

<figure><img title="git-config" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe8d34cb-df88-4660-aa79-d66b1c8f3ed0/git3-1-git-config.gif" alt="screenshot" width="216" height="53" /></figure>

Git saves some meta data about the relationship between two branches; in this case, our local “master” branch tracks the same-named branch on the remote “origin.” This meta data is used by a couple of commands in Git, such as <code>push</code>, <code>pull</code> and <code>status</code>.

<figure><img title="git-status" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f561636-d870-4c0b-8f7b-ac0dce8c1f8c/git3-2-git-status.gif" alt="screenshot" width="350" height="40" /></figure>

In general, though, you don’t have to worry about managing all of this meta data. If you create a new local branch based on a remote branch, Git will set up the tracking relationship for you.

### Undoing Things

Most mistakes that you make in Git can be corrected pretty easily.

Let’s take a simple case. You have mistyped your last commit message and now want to correct this typo. Git offers an <code>--amend</code> parameter for its <code>commit</code> command. This will overwrite the last commit and make it look as if your little mistake never happened. Amending also allows you to change the set of committed files by adding and removing items to and from the commit. But remember one golden rule: don’t amend commits that you’ve already pushed to a remote!

The <code>revert</code> command lets you “take back” a commit (and this time it doesn’t have to be your most recent commit). Reverting, however, will not delete any commits. Quite the opposite: a new commit will be created that reverses the effects of the corresponding commit.

The <code>reset</code> command is useful if you truly regret your most recent commit(s). It takes advantage of the fact that branches are really nothing more than pointers to a certain commit. This command rolls the pointer back to an older commit. In fact, <code>reset</code> will not even delete any commits; but your project’s history will look like it has done exactly that.

### Integrating Selected Commits

Usually, you would integrate changes into a branch by merging with another one. In those rare cases where a merge is undesired, Git offers an alternative with the <code>cherry-pick</code> command. Instead of integrating a complete branch (when merging), <code>cherry-pick</code> allows you to integrate any desired commit. You can even integrate multiple selected commits in one go &mdash; but remember to start with the oldest one to avoid problems.

GUI applications like <a title="Tower - Git client for Mac OS X" href="https://www.git-tower.com">Tower</a> make tasks like these a lot easier by allowing you to simply drag and drop the desired commits.

{{% ad-panel-leaderboard %}}

## Rebase Instead Of Merge

The most common method to integrate one branch into another is to perform a “merge.” For an ordinary three-way merge, Git takes the endpoints of the branches to be merged and the common parent commit as the basis for the integration. This results in a so-called “merge commit” that connects both branches like a knot.

<figure><img title="branch1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d4f9567-91b9-400a-b8be-8c4f6fdd655a/git3-3-branch1.gif" alt="screenshot" width="430" height="122" /></figure>

A “rebase” is an alternative to an ordinary merge. A rebase does not result in a separate merge commit and therefore produces no “bumps” in your project’s history. It will look as if the history has run linearly and all commits have happened on the same branch.

Let’s look at a concrete scenario to better understand what a rebase does:

<figure><img title="branch 2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/275f6369-9ecc-4be2-8ee3-401a7c0e5e5a/git3-4-branch2.gif" alt="screenshot" width="430" height="128" /></figure>

Here, branch_B is our current HEAD branch. If we execute <code>git rebase branch_A</code>, the following things will happen. First, all new commits (C2 and C4) that originated after the last common commit (C1) will be temporarily removed. Now, branch_A’s new commits will be applied on branch_B. This means that both branches are now on the same position: on branch_A’s position.

<figure><img title="branch3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6cffa0c-11a4-4111-b608-bd5822cfa6e6/git3-5-branch3.gif" alt="screenshot" width="430" height="160" /></figure>

Right at the beginning, branch_B’s new commits were removed temporarily. Now is the time to reapply them: one after the other, and in their original order.

<figure><img title="branch 4" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/010cbfd9-5f66-4a30-a59c-38c69cacdd4b/git3-6-branch4.gif" alt="screenshot" width="430" height="76" /></figure>

In the end, by rebasing the branches, no merge commit was necessary, and the history has remained linear.

### Rewriting History

A handful of commands in Git will change a project’s history. In addition to amending a commit, <code>rebase</code> also falls into this category.

Note that the reapplied commits in our sample scenario aren’t completely identical to the original commits (which is why they’re named C2’ and C4’). The commit SHA-1 has changed because we rewrote history with the <code>rebase</code>.

Always follow this golden rule when using commands that change your history: local commits that haven’t been published can safely be changed by using <code>rebase</code> or <code>amend</code>. However, if they’ve already been pushed to a remote repository, you should not use these tools anymore. Your teammates will thank you for it.

## Housekeeping In Git

A Git repository can accumulate quite a number of objects over its lifetime, be they commits, files or file trees. Organizing these objects optimally is crucial to keeping Git fast. The <code>git gc</code> command (where <code>gc</code> stands for “garbage collect”) was made for just this purpose. Although it’s executed automatically in the background when running certain commands, running <code>gc</code> from time to time is still a good idea (preferably with the <code>--aggressive</code> parameter, to ensure the best result).

## Desktop Tools And External Code Hosting

### Tools

If you spend a lot of time in the command line, you can spice things up by using plug-ins. Nice little helpers include Tab auto-completion for branch names, and directly displaying the current branch in your shell’s prompt. Plug-ins are available for <a title="Plugin for the Bash Shell" href="https://github.com/revans/bash-it">Bash</a> and <a title="Plugin for Zsh" href="https://github.com/robbyrussell/oh-my-zsh">zsh</a>.

As alternatives to the command line, various desktop clients might be worth a look. A lot of tasks can be performed more easily and comfortably using a graphical user interface &mdash; if not only to not have to memorize all of the commands and parameters. Windows users might want to look at <a title="Tortoise Git for Windows" href="https://code.google.com/p/tortoisegit/">Tortoise Git</a>, while Mac OS users can try <a title="Tower - Git client for Mac OS X" href="https://www.git-tower.com">Tower</a> (*disclaimer: this is the author’s product*).

### Repository Hosting

More and more companies and individual developers are opting not to host their own code anymore. Providing and maintaining expensive server infrastructure is not everyone’s cup of tea: special know-how is necessary, ressources are tied up, and a high degree of security and availability must be guaranteed.

Meanwhile, some companies are already offering code hosting as “software as a service.” Some of the most popular ones currently are <a title="GitHub Code Hosting" href="https://www.github.com">GitHub</a>, <a title="Beanstalk Code Hosting" href="https://www.beanstalkapp.com">Beanstalk</a> and <a title="Codebase Code Hosting" href="https://www.codebasehq.com/">Codebase</a>. If hosting your code externally is an option, then check out one of these services.

## Conclusion

Git is an extremely versatile tool. In its early days, it consisted of more than 140 binaries that could be combined flexibly with one another. While using Git has become much easier with recent versions, it has managed to maintain this flexibility. As a result, Git can be viewed as a toolset for creating your very own version control workflow.

But the advanced tools are not all that make Git interesting. Its extraordinary speed and unique branching concept, for example, are great to have, too.

### Further Reading

*   [Moving A Git Repository To A New Server](https://www.smashingmagazine.com/2014/05/moving-git-repository-new-server/)
*   [S(GH)PA: The Single-Page App Hack For GitHub Pages](https://www.smashingmagazine.com/2016/08/sghpa-single-page-app-hack-github-pages/)
*   [How To Deploy WordPress Plugins With GitHub Using Transients](https://www.smashingmagazine.com/2015/08/deploy-wordpress-plugins-with-github-using-transients/)
*   [Ultimate Round-Up For Version Control with Subversion](https://www.smashingmagazine.com/2009/03/ultimate-round-up-for-version-control-with-subversion/)

{{< signature "kw, al, il, mrn" >}}
