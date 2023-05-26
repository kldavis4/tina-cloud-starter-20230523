---
title: 6 Version Control Systems Reviewed
slug: the-top-7-open-source-version-control-systems
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecc50ee5-c090-4d0d-92e9-7224f234ccac/cvs.jpg
date: 2008-09-18T16:42:41.000Z
author: glenstansberry
description: >-
  If you’ve ever collaborated with other people on a project, you know the
  frustration of constantly swapping files. Some do it by email, some through
  file upload services and some by other methods. It’s a pain in the neck, and
  every designer and developer knows it. **Revision control** is an excellent
  way to combat the problem of sharing files between workers.
categories:
  - Coding
  - Tools
  - Open Source
  - Reviews
  - Linux
---
If you’ve ever collaborated with other people on a project, you know the frustration of constantly swapping files. Some do it by email, some through file upload services and some by other methods. It’s a pain in the neck, and every designer and developer knows it. <strong>Revision control</strong> is an excellent way to combat the problem of sharing files between workers.

[![6 Version Control](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab3c40f4-0f41-4837-bdbe-8e22f305e263/cvs.gif "6 Version Control Systems Reviewed")](https://www.smashingmagazine.com/2008/09/18/the-top-7-open-source-version-control-systems/)

Most web-developers have probably worked with some sort of revision control system, but designers may find it a foreign concept. The most obvious benefit of using revision control is the <em>ability to have an unlimited number of people working on the same code base</em>, without having to constantly send files back and forth.

You might be interested in the following related posts:

*   [Ultimate Round-Up For Version Control with Subversion](https://www.smashingmagazine.com/2009/03/ultimate-round-up-for-version-control-with-subversion/)
*   [Modern Version Control With Git](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/)
*   [Moving A Git Repository To A New Server](https://www.smashingmagazine.com/2014/05/moving-git-repository-new-server/)

{{% feature-panel %}}

But designers and developers can both benefit from using revision control systems to keep copies of their files and designs. You can instantly browse previous “commits” to your repository and revert to earlier versions if something happens.

This article <strong>reviews some of the top open-source version control systems</strong> and tools that make setting up a version control system easy.</p>

## CVS

<a href="https://www.nongnu.org/cvs/" rel="nofollow"><img loading="lazy" decoding="async" class="1125" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab3c40f4-0f41-4837-bdbe-8e22f305e263/cvs.gif" alt="" width="495" height="433" /></a>

<a href="https://www.nongnu.org/cvs/" rel="nofollow">CVS</a> is the grandfather of revision control systems. It was first released in 1986, and Google Code still hosts the original Usenet post announcing CVS. CVS is the <strong>de facto standard</strong> and is installed virtually everywhere. However, the code base isn’t as fully featured as SVN or other solutions.

The learning curve isn’t too steep for CVS, and it’s a very simple system for making sure files and revisions are kept up to date. While CVS may be an older technology, it’s still quite useful for any designer or developer for backing up and sharing files.

<a href="https://www.tortoisecvs.org/" rel="nofollow">Tortoise CVS</a> is a great client for CVS on Windows, and there are many different IDEs, such as Xcode (Mac), <a href="https://eclipse.org" rel="nofollow">Eclipse</a>, <a href="https://netbeans.org" rel="nofollow">NetBeans</a> and <a href="https://www.gnu.org/software/emacs/" rel="nofollow">Emacs</a>, that use CVS.</p>

### CVS Resources

*   [Introduction to CVS](https://www.linuxdevcenter.com/pub/a/linux/2002/01/03/cvs_intro.html)
*   [CVS Best Practices](https://tldp.org/REF/CVS-BestPractices/html/index.html)
*   [SVN and CVS Quick Comparison](https://www.pushok.com/soft_svn_vscvs.php)

## SVN

<figure><a href="https://subversion.tigris.org/" rel="nofollow"><img loading="lazy" decoding="async" class="1124" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ec031b2-6113-4092-b55f-d0c80aa30097/svn-homepage.jpg" alt="" width="500" height="282" /></a></figure>

<a href="https://subversion.tigris.org/" rel="nofollow">Subversion</a> is probably the version control system with the widest adoption. Most open-source projects use Subversion as a repository because other larger projects, such as SourceForge, Apache, Python, Ruby and <em>many</em> others, use it as well. <a href="https://code.google.com" rel="nofollow">Google Code</a> uses Subversion exclusively to distribute code.

Because of Subversion’s popularity, many different Subversion clients are available. If you’re a Windows user, <a href="https://tortoisesvn.tigris.org/" rel="nofollow">Tortoise SVN</a> is a great file browser for viewing, editing and modifying your Subversion code base. If you’re on a Mac, <a href="https://www.versionsapp.com/" rel="nofollow">Versions</a> is an elegant client that provides a “pleasant way to work with Subversion.” Xcode is Apple’s developer environment and Subversion client that ships with Leopard on a Mac.</p>

### SVN Resources

*   [Ultimate Round-Up For Version Control with Subversion](https://www.smashingmagazine.com/2009/03/ultimate-round-up-for-version-control-with-subversion/)
*   [Subversion home page](https://subversion.tigris.org/)
*   [Getting Started with Subversion - Mac](https://www.rubyrobot.org/tutorial/subversion-with-mac-os-x)
*   [Getting Started with Subversion - Windows](https://codebetter.com/blogs/peter.van.ooijen/archive/2008/05/22/getting-started-with-subversion.aspx)
*   [Subversion for Designers](https://www.thinkvitamin.com/features/design/subversion-for-designers "Subversion for Designers")
*   [Beanstalk](https://www.beanstalkapp.com/) - A hosted Subversion system
*   [Comparison of Subversion Clients](https://en.wikipedia.org/wiki/Comparison_of_Subversion_clients)
*   [Subversion for Java](https://svnkit.com/)

## Git

<figure><a href="https://github.com" rel="nofollow"><img loading="lazy" decoding="async" class="1126" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/460e0024-d0d6-42ea-a9a4-58a36ba39e02/git.jpg" alt="" width="500" height="358" /></a></figure>

<a href="https://git-scm.com/" rel="nofollow">Git</a> is the new fast-rising star of version control systems. Initially developed by Linux kernel creator Linus Torvalds, Git has recently taken the Web development community by storm. Git offers a much different type of version control in that it’s a <strong>distributed version control system</strong>. With a distributed version control system, there isn’t one centralized code base to pull the code from. Different branches hold different parts of the code. Other version control systems, such as SVN and CVS, use centralized version control, meaning that only one master copy of the software is used.

Git prides itself on being a fast and efficient system, and many major open-source projects use Git to power their repositories; projects like:

*   [Linux Kernel](https://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=summary)
*   and [many others](https://git.or.cz/gitwiki/GitProjects).

<a href="https://github.com" rel="nofollow">GitHub</a> has recently helped establish Git as a great version control system, providing a beautiful front end for many large projects, such as <a title="Rails on Github" href="https://github.com/rails">Rails</a> and <a href="https://github.com/sstephenson/prototype/tree/master" rel="nofollow">Prototype</a>. However, Git isn’t as easy to pick up as CVS or SVN, so it’s much harder to use for a beginner.

<figure><a href="https://github.com" rel="nofollow"><img loading="lazy" decoding="async" class="1127" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deb46486-e963-4ce3-ac9f-0ba9fc9f23c6/github.jpg" alt="" width="500" height="324" /></a></figure>

### Git Resources

*   [Modern Version Control With Git](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/)
*   [Modern Version Control With Git, Part 2](https://www.smashingmagazine.com/2011/08/modern-version-control-with-git-part-2/)
*   [Git on Wikipedia](https://en.wikipedia.org/wiki/Git_(software))
*   [Git SVN Comparison](https://git.or.cz/gitwiki/GitSvnComparsion)
*   [git-gui](https://www.kernel.org/pub/software/scm/git/docs/git-gui.html) - a multi-platform user interface for Git

## Mercurial

<figure><img loading="lazy" decoding="async" class="1128" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3d1901-09b1-4b7c-86e6-0f080b6c47f8/mercurial.jpg" alt="" width="500" height="301" /></figure>

<a href="https://www.mercurial-scm.org/">Mercurial</a> is another <strong>open-source distributed version control system</strong>, like Git. Mercurial was designed for larger projects, most likely outside the scope of designers and independent Web developers. That doesn’t mean that small development teams can’t or shouldn’t use it. Mercurial is extremely fast, and the creators built the software with performance as the most important feature. The name “mercurial” is an adjective that means “Relating to or having characteristics (eloquence, swiftness, cleverness) attributed to the god Mercury.”

Aside from being very fast and scalable, Mercurial is a <strong>much simpler</strong> system than Git, which is why it appeals to some developers. There aren’t as many functions to learn, and the functions are similar to those in other CVS systems. It also comes equipped with a stand-alone Web interface and extensive documentation on understanding Mercurial if you have been using another system.

## Bazaar

<figure><a href="https://bazaar-vcs.org/" rel="nofollow"><img loading="lazy" decoding="async" class="1129" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c30bb06-a23b-4161-8054-101b9ac0d15b/bazaar.jpg" alt="" width="500" height="286" /></a></figure>

<a href="https://bazaar-vcs.org/" rel="nofollow">Bazaar</a> is yet another distributed version control system, like Mercurial and Git, that offers a very friendly user experience. It calls itself “<strong>Version control for human beings</strong>.” It supports many different types of <a href="https://www.smashingmagazine.com/2011/01/cleaning-up-the-mess-how-to-keep-your-coding-workflow-organized/">workflows</a>, from solo to centralized to decentralized, with many variations in between.

One of the main features of Bazaar is the fine-grained control you’ll have over the setup. As shown with the workflows, you can use it to fit almost any scenario of users and setups. This is a great revision control system for nearly any project because it’s so easy to modify. It’s also embeddable, so you can add it to existing projects.

Bazaar also has a <a href="https://bazaar-vcs.org/BzrSupport" rel="nofollow">strong community</a> that maintains things like <a href="https://bazaar-vcs.org/BzrPlugins" rel="nofollow">plug-ins</a> and lots of <a href="https://bazaar-vcs.org/3rdPartyTools" rel="nofollow">third-party tools</a>, such as GUI software to add a graphical interface to the system.

<figure><a href="https://bazaar-vcs.org/" rel="nofollow"><img loading="lazy" decoding="async" class="1134" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b74b7972-84c9-4021-9327-b1587c01cfc3/workflows-gatekeeper.jpg" alt="" width="500" height="353" /></a></figure>

### Bazaar resources:

*   [Bazaar in 5 minutes](https://doc.bazaar-vcs.org/bzr.dev/en/mini-tutorial/index.html) - How to set up Bazaar quickly.
*   [Bazaar migration guides](https://bazaar-vcs.org/BzrMigration) - Guides on migrating to Bazaar from CVS, Subversion, Darcs, Mercurial and other systems.
*   [Bazaar vs. Git](https://bazaar-vcs.org/BzrVsGit) - Showcases the differences between the two decentralized systems.</p>

## Monotone

<a href="https://monotone.ca/" rel="nofollow">Monotone</a> is the baby of the distributed revision control bunch. While many of Monotone’s peers focus on performance, <strong>Monotone places higher value on integrity than performance</strong>. In fact, it can take quite a bit of time for a new user of Monotone to simply download the initial repository due to the extensive validation and authentication required.

Monotone is fairly easy to learn if you’re familiar with CVS systems, and it can import previous CVS projects. However, it’s not quite as popular as other version control systems.</p>

## Version Control Tools

*   [QCT GUI commit tool](https://qct.sourceforge.net/) A version control commit tool that supports Mercurial, Bazaar, Cogito (Git), Subversion, Monotone, and CVS.
*   [Meld](https://meld.sourceforge.net/) is a merge and diff tool that allows you to compare two or three files and edit them in place, while updating automatically. It works with CVS, Subversion, Bazaar and Mercurial.</p>

## Version Control Resources

*   [Distributed Revision Control Systems: Git vs. Mercurial vs. SVN](https://www.russellbeattie.com/blog/distributed-revision-control-systems-git-vs-mercurial-vs-svn) A quick look at the major differences between the three types of revision control systems.
*   [Revision Control Systems](https://en.wikipedia.org/wiki/Revision_control) The Wikipedia article on revision control.
*   [Choosing a Distributed Version Control System](https://www.dribin.org/dave/blog/archives/2007/12/28/dvcs/) Article showing the pros and cons of each version control system. _(al)_

