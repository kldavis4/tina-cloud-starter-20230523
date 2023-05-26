---
title: Moving A Git Repository To A New Server
slug: moving-git-repository-new-server
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c83cbf03-ff33-4c46-b93d-caeea0a177b1/moving-git-preview-opt.jpg
date: 2014-05-19T18:06:46.000Z
author: niksumeiko
summary: >-
  Suppose your company decides to change its code-hosting provider or you wish to move your own Git repository to a different host. It doesn’t happen often, but it happens.
description: >-
  Suppose your company decides to change its code-hosting provider or you wish to move your own Git repository to a different host. It doesn’t happen often, but it happens.
categories:
  - Git
  - Coding
  - Tools
---

When I had to move a number of Git projects to a new host, it took me quite some time to find an accurate method. Having made many attempts, and a couple of fails, and carefully reading <a href="https://git-scm.com/documentation">Git’s documentation</a>, I found a solid and effective way. I thought, then, that every developer would benefit from knowing how to migrate a Git repository to a new host quickly and easily. The most important thing is to make sure that your branches and tags and your commit history are all moved.

## Let’s Learn How To Do That Properly

First, we have to fetch all of the remote branches and tags from the existing repository to our local index:

<pre><code class="language-bash">git fetch origin
</code></pre>

But even if all branches and tags have been fetched and exist in a local index, we still won’t have a copy of them that is physically local. And a local copy is required to migrate the repository.

We can check for any missing branches that we need to create a local copy of. Let’s list all existing branches (local and remote) to see whether we are missing any copies locally:

<pre><code class="language-bash">git branch -a

* master
  remotes/origin/develop
  remotes/origin/master
  remotes/origin/release/0.1
</code></pre>

We can easily tell from this output whether we have local copies of all remote branches: The remote ones are prefixed with the <code>remotes/origin/</code> path, and the local ones aren’t. So, only our master branch is local, whereas <code>remotes/origin/develop</code> and <code>remotes/origin/release/0.1</code> are not. That’s OK — let’s just create local copies:

<pre><code class="language-bash">git checkout -b develop origin/develop
git checkout -b release/0.1 origin/release/0.1
</code></pre>

{{% feature-panel %}}

After creating local copies of everything, we can verify once again whether all branches with the <code>remotes/origin/</code> prefix have corresponding local copies (shown without the prefix):

<pre><code class="language-bash">git branch -a

  develop
  master
* release/0.1
  remotes/origin/develop
  remotes/origin/master
  remotes/origin/release/0.1
</code></pre>

Now we know for sure that all branches in our repository are stored locally, and we are ready to move the repository to a new host.

At this point, let’s assume we have an SSH-cloned URL of our new repository. If not, create a new repository, and then you will have its SSH-cloned URL.

<a><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90995d24-a078-4288-adfb-3326e964fbaf/github-ssh-clone-url-opt.png" width="500" height="84" /></a>

Let’s use the SSH-cloned URL of our new repository to create a new remote in our existing local repository by executing the following command:

<pre><code class="language-bash">git remote add new-origin git@github.com:manakor/manascope.git
</code></pre>

This will give us two remotes for the existing repository: the original one (named <code>origin</code>, connected to the existing remote host) and a new one (named <code>new-origin</code>, connected to the new host).

(Git has this concept of “remotes,” which are simply URLs to other copies of your repository. The name <code>origin</code> refers to the original remote repository; by convention, it is considered the primary centralized repository.)

Now we are ready to push all local branches and tags to the new remote named <code>new-origin</code>. We could push each local branch separately, but pushing all branches at once would be much faster by executing the following Git command:

<pre><code class="language-bash">git push --all new-origin
</code></pre>

Let’s also push all of the tags to <code>new-origin</code> with this Git command:

<pre><code class="language-bash">git push --tags new-origin
</code></pre>

We’re almost done. Let’s make <code>new-origin</code> the default remote, which will direct all future commits to the new repository that we have just pushed to. To do this, remove the old repository remote:

<pre><code class="language-bash">git remote rm origin
</code></pre>

And rename <code>new-origin</code> to just <code>origin</code>, so that it becomes the default remote:

<pre><code class="language-bash">git remote rename new-origin origin
</code></pre>

(Everyone is used to the default remote being named <code>origin</code>. So, let’s keep it standard by naming our primary centralized repository remote <code>origin</code>, too.)

## Awesome, Done!

Your repository is now connected to the new remote (i.e. the new host), which will store all of your branches and tags and your commit history. Plus, all commits will be pushed to the new remote host from now on.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [Modern Version Control With Git](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/)
*   [Become A Command-Line Power User With Oh-My-ZSH And Z](https://www.smashingmagazine.com/2015/07/become-command-line-power-user-oh-my-zsh-z/)

{{< signature "ds, al, il" >}}
