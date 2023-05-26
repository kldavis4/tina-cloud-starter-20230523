---
title: 'How To Make Life Easier When Using Git'
slug: make-life-easier-when-using-git
author: shane-hudson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d29e03-763c-4c74-8568-78a4af7e1bc3/make-life-easier-when-using-git.png
date: 2020-03-27T11:30:00.000Z
summary: >-
  You don’t need to know your trees from your dangling blobs. If you use Git every day and feel like it’s a juggling act, then here are some tricks and tips to help make your life a bit easier.
description: >-
  You don’t need to know your trees from your dangling blobs. If you use Git every day and feel like it’s a juggling act, then here are some tricks and tips to help make your life a bit easier.
categories:
  - Git
  - Tools
  - Techniques
  - Workflow
  - Debugging
evergreen: true
last_updated: 2020-03-27T11:30:00.000Z
updated_by: shane-hudson
---

Git was released almost 15 years ago. In that time it has gone from underdog to unbeaten champion, git init is often the first command run on a new project. It is undoubtedly an important tool that many of us use on a daily basis, and yet it is often seen as magic: brilliant, but scary.

There’s been a lot written about getting started with git, understanding how git works under the hood or techniques for better branching strategies. In this article, we will specifically target the stuff that just makes your life better in a small way.

## Finding Your Old Socks

The whole point of git is to be able to save your work, to switch context and do something else. It could be to backup the code for the future, or to be able to make progress on a few different features asynchronously. It would be awful to have to throw out *v2* just because there was a bug in *v1*, it would be equally a shame to have files named like *v1_final_bug_fixed* which notoriously become an impossible mess.

We know life is easier, to some extent, with our updates neatly compartmentalised into git branches that can be shared with other team members. However, I’m sure you can agree, there are often times when you’ve context switched and when you go back it’s impossible to find the right branch. Was it ever committed? Maybe it was stashed? Maybe it wasn’t committed and now the work is in the wrong branch and everything is going awful and I am awful at my job! We’ve all been there.

{{% feature-panel %}}

### Sort Branches By Date

My first attempt at figuring out how to find lost work, in a short blog post titled "[How to find the branch you lost in git](https://shanehudson.net/2019/09/14/how-to-find-the-branch-you-lost-in-git)" was to sort the branches by date. This outputs every single branch you’ve got locally beginning with the one most recently committed to. It’s not fancy or surprising but it has helped me many times.

<pre><code class="language-bash"># To sort branches by commit date
git branch --sort=-committerdate
</code></pre>

### Previous Branch

What can you do if you didn’t commit, switched branch then wanted to get back to it? You could probably work out frorm the branch list anyway, if you’ve some idea of the branch name. But what if it wasn’t a branch, if it was a "detached HEAD", a specific commit.

It turns out there is a way to do this with ease:

<pre><code class="language-bash"># Checkout previous branch
git checkout -
</code></pre>

The `-` acts as a shorthand for `@{-1}` which is a syntax you can use for going back any given amount of checkouts. So if, for example, you had checked out branch `feature/thing-a` then `feature/thing-b` then `bugfix/thing-c`, you can use `@{-2}` to get back to `feature/thing-a`.

<pre><code class="language-bash"># Checkout branch N number of checkouts ago
git checkout @{-N}
</code></pre>

### Show Information About All Branches

If you are looking for a way to see what the last commit in each branch was, you can use option flags `v` to show a list of all branches with the last commit ID and message from each. If you do it twice (`vv`) then it will also show the upstream remote branch that it is linked to.

<pre><code class="language-bash"># List branches along with commit ID, commit message and remote
git branch -vv
</code></pre>

### That One File

We’ve all done it: Somehow, a single file was left in the wrong branch. Do you need to redo all of your work, or copy and paste between the two branches? Nope, thankfully there’s a way to do it.

It’s a bit odd, especially given `git checkout -` goes back a previous branch; if you use `--` after a branch name on checkout then it will let you specify the specific file you’re looking for. It’s not something you would guess, but really handy once you know it.

<pre><code class="language-bash">git checkout feature/my-other-branch -- thefile.txt
</code></pre>

### Make Status Easier To Read

In a [tweet](https://twitter.com/tlakomy/status/1236278685336055808), Tomasz Łakomy mentioned about reducing the output of git status using `-sb` flags and said, “I’ve been using git for YEARS and nobody told me about this.” This isn’t strictly about finding lost files, but there’s cases where simplifying the output could make it easier to see what’s been changed.

*Most git commands have flags like this so it’s always worth looking into how you can use them to customise your workflow!*

<div class="break-out">

 <pre><code class="language-bash"># Usually we would use git status to check what files have changed
git status

# Outputs:
On branch master
Changes not staged for commit:
  (use "git add &lt;file&gt;..." to update what will be committed)
  (use "git checkout -- &lt;file&gt;..." to discard changes in working directory)

	modified:   README.md

Untracked files:
  (use "git add &lt;file&gt;..." to include in what will be committed)

	another-file
	my-new-file

# Using the flags -sb we can shorten the output
git status -sb

# Outputs:
## master
 M README.md
?? another-file
?? my-new-file
</code></pre>
</div>

### See Everything That Has Happened

There are times when something goes completely wrong &mdash; such as accidentally discarding staged changes before commiting them. When git log isn’t enough to get back to what you were last doing and none of the above tips are helpful, then there’s **git reflog**.

Everything you do in git that changes where `HEAD@{}` points to (such as `push/pull/branch/checkout/commit`) will update the reference log so it essentially acts as a history of everything you’ve done no matter which branch you’re on. This contrasts with git log which is everything that has changed over time for the particular branch.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b79bc60d-9845-4031-9de5-09d376817967/overview-code-all-in-one.png" sizes="100vw" caption="" alt="Overview all in one place" >}}

With the commit ID, you are able to do git show to see the change and if it’s definitely the one you want you can use git checkout or even select a specific file as shown above.

<pre><code class="language-bash"># See the reference log of your activity
git reflog --all

# Look at the HEAD at given point from reflog
git show HEAD@{2}

# Checkout the HEAD, to get back to that point
git checkout HEAD@{2}
</code></pre>

### Staged Files That Were Never Commited

In the extreme case that git reflog is unable to help you get your files back (e.g. if you ran a hard reset with staged files), there’s one more trick up your sleeve. Every change is stored in `.git/objects` which on an active project would be full of files and impossible to decipher. There is, however, a git command called `git fsck` which is used to verify integrity (check for corrupt files) within a repository. We are able to use this command with the `--lost-found` flag to find all files that are not related to a commit; these files are called a “dangling blob”.

It will also find “dangling trees” and “dangling commits” &mdash; you can use `--dangling` if you want but `--lost-found` has the advantage that it extracts all of the appropriate files into a folder `.git/lost-found`. On an active project, it’s likely you will have a lot of these dangling files without even knowing about it; git has a garbage cleanup command that runs regularly to get rid of them.

So, by using `--lost-found`, you’re then able to list the files and see the time/date they were made which makes it a lot easier to see the files you’re looking for. Note that each individual file will still be an individual file (you cannot use checkout) and all files will have unrecognisable names (a hash) so you will need to copy the files you want.

<div class="break-out">

 <pre><code class="language-bash"># This will find any change that was staged but is not attached to the git tree
git fsck --lost-found

# See the dates of the files
ls -lah .git/lost-found/other/

# Copy the relevant files to where you want them, for example:
cp .git/lost-found/other/73f60804ac20d5e417783a324517eba600976d30 index.html
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Git As A Team

Using Git as a single user is one thing but when you’re on a team of people &mdash; usually with a mix of backgrounds and technologies &mdash; Git can become both a blessing and a curse. It can be powerful for sharing the same codebase, getting code reviews, and seeing progress of the whole team. But at the same time, everyone needs to have a shared understanding of how the team intends to use it. Whether it is branch naming conventions, how you structure a commit message or exactly which files are committed, **it’s essential to have good communication and talk about how you will all use the tool**.

It’s always important to consider how easy it is to on-board a new developer, what would happen if they began committing without knowing some of the agreed principles and conventions? It wouldn’t be the end of the world, but it would likely cause some confusion and take time to get things back to the agreed approach.

This section has some tips and tricks for getting the repository itself to know the conventions, to automate and declare as much as possible. In the ideal case, any new contributor would almost straight away be working the same way as the rest of the team.

### Same Line Endings

By default, Windows uses DOS line endings `\r\n` (CRLF) while Mac and Linux both use UNIX line endings `\n` (LF) and really old versions of Mac used to use `\r` (CR). So as a team grows, it becomes more likely that mismatched line endings will become a problem. Usually, these are an inconvenience; they (probably) won’t break your code but will make commits and pull requests show all kinds of irrelevant changes. Quite often people will just ignore them &mdash; it’s quite a hassle to go through and change.

There is a solution to this: You can get everyone on the team to set their local configs to automatic line endings.

<div class="break-out">

 <pre><code class="language-bash"># This will let you configure line-endings on an individual basis
git config core.eol lf
git config core.autocrlf input
</code></pre>
</div>

Of course, that would mean making sure the new contributor does that and it’s so easy to forget to tell them. So how would we do it for the whole team? Well the way Git works is it checks for a config file in the repository at .git/config, then it checks the user’s system-wide config at `~/.git/config` then checks the global config at `/etc/gitconfig`. These are all useful at times but it turns out that none of those can be set through the repository itself. You can add repository-specific configurations but that will not carry over to other members of the team.

There is, however, a file that does get committed to the repository. It’s called *.gitattributes*. You won’t have one by default, so make a new file and save it as “*.gitattributes*”. This file is used for setting attributes per file; for example, you could make git diff use exif data for image files instead of trying to diff a binary file. In this case, we can use a wildcard to make the setting work for all files, essentially acting as a team-wide config file.

<div class="break-out">

 <pre><code class="language-bash"># Adding this to your .gitattributes file will make it so all files
# are checked in using UNIX line endings while letting anyone on the team
# edit files using their local operating system’s default line endings. 
* text=auto
</code></pre>
</div>

### Auto-Collapse

It’s a well-known solution to add package-managed files (such as `node_modules/`) to the `.gitignore` file in order to keep compiled files locally and not add them to the repository. However, sometimes there are files that you do want to check in but don’t want to see each time in the pull request.

For this situation (at least on GitHub), you can add paths annotated with linguist-generated to your *.gitattributes* file and check that file in at the root of the repository. This will collapse the files in the pull request, so you can still see they were changed without the full contents of the change.

{{% pull-quote %}}
 Anything to reduce stress and cognitive load of code reviewing is going to help improve the quality of the code reviews and reduce the time it takes.
{{% /pull-quote %}}

For example, if you have a Unity project, you would want to check-in your asset files but not actually care about them so you can add it to the attributes file like so:

<pre><code class="language-bash">*.asset linguist-generated
</code></pre>

### Use Git Blame More Often

This is a tip that Harry Roberts suggested in his post about Git, “[Little Things I Like To Do With Git](https://csswizardry.com/2017/05/little-things-i-like-to-do-with-git/).” He says to alias `git blame` to `git praise` so it feels like a positive action. This seems like semantics — renaming something doesn't change what it does at all. But whenever I've seen any team speak about using Git's blame feature, everyone tenses up, and I certainly do, too. It's a natural reaction to think it's a negative thing… it really shouldn't be!


It’s a powerful feature knowing who last touched the code you’re looking at. Not to blame them or even to praise them, but simply to ask the right person questions and to save time figuring out who to talk to.

Not only should you think of git blame as a good thing (call it ‘praise’ if you want to), but you should think of it as a communication tool that will help the entire team reduce confusion and prevent wasting time figuring out who knows about what. Some IDEs such as Visual Studio include this feature as annotations (without any negative connotation at all) of each function so you can instantly see who last modified it (and therefore who to talk to about it).

### Git Blame For A Missing File

Recently, I saw a developer on the team trying to figure out who removed a file, when it was, and why it was removed. This seems like a useful time for git blame but that works based on lines in a file; it doesn’t help with stuff that isn’t there any more. There is, however, a solution. The old trusty git log. If you look at the log with no arguments, then you will see a long list of all the changes on the current branch. You can add a commit ID to see the log for that specific commit, but if you use `--` (which we’ve used before to target a specific file), then you can get the log for a file &mdash; even one that no longer exists.

<div class="break-out">

 <pre><code class="language-bash"># By using -- for a specific file,
# git log can find logs for files that were deleted in past commits
git log -- missing_file.txt
</code></pre>
</div>

### Commit Message Template

One thing that eventually gets mentioned within teams is that commit messages could be improved. Maybe they could reference a project management tool’s ID for the bug the commit fixes or maybe you want to encourage some text instead of an empty message.

This one needs to be run manually each time someone clones the repository (as git config files are not committed to the repository), but it is handy because you can have a shared file in the repository (named anything you want) that can act as the commit message template.

<div class="break-out">

 <pre><code class="language-bash"># This sets the commit template to the file given,
# this needs to be run for each contributor to the repository.
git config commit.template ./template-file
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Git As Automation

Git is powerful for automation. This is not immediately obvious but if you consider that it knows all of your past activity within the repository &mdash; plus that of other contributors &mdash; it has a lot of information that can be very useful.

### Git Hooks

Quite often you will find that within a team you all want to be doing repeated tasks while you work. This could be ensuring tests and code linters pass before it lets you push using the pre-push hook, or to [enforce a branch naming strategy](https://itnext.io/using-git-hooks-to-enforce-branch-naming-policy-ffd81fa01e5e) using the pre-commit hook. Here on Smashing Magazine, Konstantinos Leimonis wrote an article titled "[How To Ease Your Team’s Development Workflow With Git Hooks](https://www.smashingmagazine.com/2019/12/git-hooks-team-development-workflow/)" which is all about improving workflow using Git Hooks.

### Manual Automation

One of the key automation features that Git has is **git bisect**. This is something that many people have heard of but probably not used. The purpose of it is to work through the git tree (the history of commits) and work out where a bug was introduced. The simplest way to do this is manually; you run `git bisect start`, give it the good and bad commit IDs, then `git bisect good `or `git bisect bad` for each commit.

This is more powerful than it seems at first because it doesn’t iterate linearly through the git log, which you could do manually and it would be a repetitive process. It, instead, uses a binary search so it’s an efficient way to go through the commits with the least amount of steps.

<div class="break-out">

 <pre><code class="language-bash"># Begin the bisect
git bisect start

# Tell git which commit does not have the bug
git bisect good c5ba734

# Tell git which commit does have the bug
git bisect bad 6c093f4

# Here, do your test for the bug.
# This could be running a script, doing a journey on a website, unit test etc.

# If the current commit has bug:
git bisect bad

# If the current commit does not have the bug
git bisect good

# This will repeat until it finds the first commit with the bug
# To exit the bisect, either:

# Go back to original branch:
git bisect reset

# Or stick with current HEAD
git bisect reset HEAD

# Or you can exit the bisect at a specific commit
git bisect reset &lt;commit ID&gt;
</code></pre>
</div>

### Taking It Further: Automating The Scientific Method

In his talk “[Debugging With The Scientific Method](https://www.youtube.com/watch?v=FihU5JxmnBg),” Stuart Halloway explained how Git’s bisect functionality could be used to automate debugging. It focuses on Clojure but you don’t need to know that language to find the talk interesting and useful.

<blockquote>“Git bisect is actually partial automation of the scientific method. You write a little program that will test something and git will bounce back and fourth cutting the world in half each time until it finds the boundary at which your test changes.”<br /><br />&mdash; Stuart Halloway</blockquote>

At first, git bisect can feel interesting and quite cool but in the end not very useful. Stuart’s talk goes a long way to showing how it’s actually counterproductive to debug in the way most of us usually do. If you, instead, focus on the empirical facts whether or not a test passes, you can run it against all commits since a working version and reduce the "feeling around in the dark" kind of debugging that we are used to.

So how do we automate git bisect? We pass it a script to run for each appropriate commit. Previously, I said we can manually run a script at each step of the bisect but if we pass it a command to run then it will automatically run the script at each step. This could be a script you write specifically to debug this one particular issue, or it could be a test (unit, functional, integration, any type of test could be used). So you could write a test to ensure the regression doesn’t happen again and use that test on previous commits.

<pre><code class="language-bash"># Begin the bisect
git bisect start

# Tell git which commit does not have the bug
git bisect good c5ba734

# Tell git which commit does have the bug
git bisect bad 6c093f4

# Tell git to run a specific script on each commit
# For example you could run a specific script:
git bisect run ./test-bug

# Or use a test runner
git bisect run jest
</code></pre>

### On Every Commit In The Past

One of the strengths of git bisect is the efficient use of binary searches to iterate through history in a non-linear way. However, sometimes a linear crawl through history is exactly what you need. You could write a script that reads git log and loops through each commit executing code, but there’s a familiar command that can do this for you git rebase.

Kamran Ahmed wrote a [tweet](https://twitter.com/kamranahmedse/status/1224069798692343808) about using rebase to run a test suite on every commit to see which commit fails the test:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Find the commit that broke the tests<br><br>$ git rebase -i --exec &quot;yarn test&quot; d294ae9<br><br>This will run &quot;yarn test&quot; on all the commits between d294ae9 and HEAD and stop on the commit where the tests fail</p>&mdash; Kamran Ahmed (@kamranahmedse) <a href="https://twitter.com/kamranahmedse/status/1224069798692343808?ref_src=twsrc%5Etfw">February 2, 2020</a></blockquote>

We’ve already looked at using git bisect to do this efficiently so that’s generally more useful for this use-case, but what if we could have all of the other use-cases running a script for a given set of commits?

There’s room to be creative here. Maybe you want a way to generate a report of how your code has changed over time (or maybe show history of tests) and parsing the git log is not enough. This is perhaps the least directly useful trick in this article, but it’s interesting and raises the possibility of doing things that maybe we wouldn’t realise is possible.

<div class="break-out">

 <pre><code class="language-bash"># This will run for every commit between current and the given commit ID
git rebase -i --exec ./my-script <commit ID>
</code></pre>
</div>

## Further Reading

It’s impossible to more than scratch the surface of git in an article &mdash; it would end up being a book! In this article, I have chosen little tricks that could be new to even someone that’s been using git for years.

There’s so much more to Git from the foundations through to complex scripting, precise configurations and integrating into the terminal, so here are some resources to look at if this has piqued your interest:

*   [Git Explorer](https://gitexplorer.com/)  
This interactive website makes it easy to figure out how to achieve what you are trying to do.
*   [Dang it Git!](https://dangitgit.com/)  
Everyone at some point gets lost in git and doesn’t know how to solve an issue. This gives solutions to a lot of the most common issues people have.
*   [Pro Git](https://git-scm.com/book/en/v2)  
It’s a book and yet it is available online for free too, so Pro Git is an invaluable resource for understanding git.
*   [Git Docs](https://git-scm.com/docs)  
It’s become a meme to tell developers to read the manual, but seriously both the git docs website and man git (for example man git-commit) go into detail about the internals of git and can be really useful.
*   [Thoughtbot](https://thoughtbot.com/blog/tags/git)  
The git category on Thoughtbot has some very useful tips for using git.
*   [Git Hooks](https://githooks.com/)  
The git hooks website has resources and ideas for all the available git hooks.
*   [Demystifying Git Internals](https://medium.com/@pawan_rawal/demystifying-git-internals-a004f0425a70)  
Trees, blobs... these terms can seem a bit odd. This article explains some of the fundamentals of how Git works internally which can be useful (as shown already) to use Git to it’s full potential.
*   [Git From Beginner To Advanced](https://www.madebymike.com.au/writing/how-to-git/)  
Mike Riethmuller wrote this useful article that is ideal for beginners to Git.
*   [Little Things I Like To Do With Git](https://csswizardry.com/2017/05/little-things-i-like-to-do-with-git/)  
It was this article by Harry Roberts that made me realise how much more there is to Git after you’ve learned enough to move code around.
*   [Atlassian’s Advanced Git Tutorials](https://www.atlassian.com/git/tutorials/advanced-overview)  
These tutorials go into detail about many of the topics mentioned in this article. 
*   [Github Git Cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)  
It’s always handy to have a good cheatsheet for tools like Git.
*   [Git Shortcuts](https://blog.praveen.science/git-shortcuts/)  
This article goes into depth about the various flags git commands have and recommends lots of aliases to use.

{{< signature "ra, il" >}}

<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 
