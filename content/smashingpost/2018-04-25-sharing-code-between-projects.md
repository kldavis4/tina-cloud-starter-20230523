---
title: 'Sharing Code Between Projects: Lessons Learned In The Trenches'
slug: sharing-code-between-projects
author: jonathan-saring
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adc3be2f-343a-4bee-8ee8-2cec63967354/01-sharing-code-between-projects-800w.png
date: 2018-04-25T14:40:51+02:00
summary: >-
  Ever find yourself writing the same code over and over again? In this article, Jonathan Saring shares his and his team's lessons learned from their own journey towards simple and effective code sharing.
description: >-
  Ever find yourself writing the same code over and over again? In this article, Jonathan Saring shares his and his team's lessons learned from their own journey towards simple and effective code sharing.
categories:
  - JavaScript
  - Node.js
---
<p>About a year ago, we came to a crossroad that changed the way we build software today. Like many other teams, we were working on a few things at a time, developing different projects for our web and mobile applications, with shared ingredients in the form of common Node.js code between our back-end repositoriess and microservices, and common React UI components with some slight visual and functional differences between our apps.</p>

<p>As our team grew and code lines multiplied, we began to realize that with every passing day <strong>we were writing the same code over and over again</strong>. Over time, it became harder to maintain our code base and develop new features with the same speed and efficiency.</p>

<p>Finally, we decided to find a solution that would enable us to share and sync common components of code between our projects. Here is what we learned along our journey, which eventually gave birth to <a href="https://bitsrc.io">Bit</a>.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a867ddc-af30-472b-8ef1-fd9a74164e59/01-sharing-code-between-projects.png" sizes="100vw" caption="Code components as building blocks. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a867ddc-af30-472b-8ef1-fd9a74164e59/01-sharing-code-between-projects.png'>Large preview</a>)" alt="Sharing code components between projects" >}}

{{% feature-panel %}}

## Common Code In The Wild

<p>While Git is great for collaborating on a single repository, sharing code between multiple projects can be more challenging than we think.</p>

<p>To get started, we looked into our own code base to learn how many times we duplicated our own integration to our user service. The unbelievable result was no less than 86 instances. After the initial shock, we started thinking that this must also be happening elsewhere.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b66750c6-d86a-48a5-b72d-186c70303b70/05-sharing-code-between-projects.png" sizes="100vw" caption="Using the same code in different places. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b66750c6-d86a-48a5-b72d-186c70303b70/05-sharing-code-between-projects.png'>Large preview</a>)" alt="Code shared in multiple projects" >}}

<p>We asked some friends working in a few different organizations of various sizes to run a simple copy-and-paste detection on their code base, looking for duplicates of code longer than 100 lines. The result blew us away: On average, more than 30% of their code base was duplicated.</p>

<p>Finally, we decided to look deep into the open-source projects on GitHub, checking for both duplications and re-implementations of a simple <code>isString</code> function in the 10,000 most popular JavaScript GitHub projects.</p>

<p>Amazingly, we found <strong>this function was implemented in more than 100 different ways</strong> and duplicated over 1,000 times in only 10,000 repositories. Later studies claim that over 50% of the code on GitHub is actually <a href="https://developers.slashdot.org/story/17/11/23/2352233/more-than-half-of-github-is-duplicate-code-researchers-find">duplicated</a>. We realized we were not the only ones facing this issue.</p>

## Looking For A Solution

<p>Before building <a href="https://bitsrc.io">Bit</a>, we looked for a tool that would help us turn the smaller components that our apps are built from into building blocks that could be shared between our projects and synced across our code base. We also wanted to organize them and make them discoverable for our team. Here’s a short summary of what we learned.</p>

### A Micro-Package Arsenal With NPM

<p>At first, we considered publishing all of our UI components, utility functions and smaller modules as packages to NPM. This seemed like the obvious solution for modularity for our software’s building blocks. However, we quickly learned that this solution came with huge overhead.</p>

<p>Trying to publish a few files from our project to NPM forced us to split our repository and create new ones just to share this code. When dealing with hundreds of components, <strong>this meant having to maintain and make changes across hundreds of repositories</strong>.</p>

<p>We would also have to refactor our code base, removing the newly created packages from their original repositories, boilerplating the packages in the new repositories and so on.</p>

<p>Even then, we had now a simple way to organize these packages and make them easily <a href="https://medium.com/@Rich_Harris/small-modules-it-s-not-quite-that-simple-3ca532d65de4#.88d5anyhv">discoverable</a> to our entire team. Another major problem was the coupling between the packages and the owners of their origin repositories, which made it nearly impossible for other people to quickly make updates to the packages while working on their own projects.</p>

<p>This kind of overhead was too much for us to handle. So, we quickly decided to look for a better way to share our code.</p>

### Lerna Monorepos

<p>The next option we came up with was to use <a href="https://github.com/lerna/lerna">Lerna</a> in order to refactor our code base into a few multi-package repositories, often referred to as “monorepos”.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c2d8af6-10ab-44c5-98c6-bff611315f09/06-sharing-code-between-projects.png" sizes="100vw" caption="Lerna multi-package repository. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c2d8af6-10ab-44c5-98c6-bff611315f09/06-sharing-code-between-projects.png'>Large preview</a>)" alt="The Hydra of Lerna" >}}

<p>The upside of this solution was that it would allow us to maintain and publish all our packages from a single repository. However, this option, too, came with a set of drawbacks, particularly when working with smaller components.</p>

<p>Choosing this option meant we would still have to effectively keep multiple packages with multiple <code>package.json</code> files, multiple build and test environments and a complicated dependency tree to handle between them. Updating these packages must also go through the main repository, still making it hard to modify these package from other projects when working with a few separate monorepos.</p>

<p>For example, take the popular <a href="https://github.com/mui-org/material-ui">Material-UI</a> React UI library. Even though it uses Lerna to publish five different packages from the same repository, you would still have to install the entire library to use each of its components. Making changes would still have to go through that project as well, and discoverability for these component didn’t improve.</p>

<p>Monorepos can be great for some cases (such as testing or building a project as a whole) and can definitely work for some teams. However, refactoring your entire code base just to share common code between projects while still having to struggle with the issues mentioned above made us drop this option as well.</p>

## Shared Libraries

<p>This option was quickly dropped, too. In a lot of way, it resembles using a CD-ROMs instead of an iTunes playlist. First, it made no sense to force an entire library of React components and an entire utility library and so on on each of our projects.</p>

<p>Secondly, every project using it would be tightly coupled to the development of this library, making it impossible to adjust its components for each project. This becomes most painful when sharing common Node.js code between our microservices, which would now be coupled to the library.</p>

<p>Thirdly, discoverability within the library is bound to be poor and would involve a lot of work with its documentation and usage in different edge cases.</p>

<p>Because it makes very little sense to couple and slow down our development, we try to <strong>minimize the use of these libraries as much as possible</strong>. Even popular JavaScript utility libraries such as Lodash are working hard to make their smaller components <a href="https://www.npmjs.com/browse/keyword/lodash-modularized">independently available</a> via NPM.</p>

### Git Submodules

<p>Finally, we turned back time and looked into working with <a href="https://medium.com/@porteneuve/mastering-git-submodules-34c65e940407">Git submodules</a>.</p>

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">You there.  You&#39;re thinking about using a Git submodule.  DON&#39;T.  Just don&#39;t.  It&#39;s not worth it, ever.</p>&mdash; Jeremy Kahn (@jeremyckahn) <a href="https://twitter.com/jeremyckahn/status/280406794583539712?ref_src=twsrc%5Etfw">December 16, 2012</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<p>Git enables you to make one repository a subdirectory of another repository, creating a single working tree for the entire project, so that a repository can utilize code from another repository.</p>

<p>As for many other teams, this solution did not last for us. First, submodules only work on the master branch, which causes problems for rapid development. Secondly, submodules increase coupling between projects, which makes it hard to work on cross-repository assignments. Finally, a submodule repository is oblivious to its own nesting and the existence of dependent repositories.</p>

<p>After trying these different solutions, we realized that it shouldn’t be this complicated. There really should be <strong>a simpler way to organize, share and develop components of code</strong> from different projects.  So, we decided to build it, and called it <a href="https://Bit">Bit</a>.</p>

## Building Bit

<p>Our vision for a solution was simple: turn our components and modules into building blocks that can be easily isolated from any project, organized in the cloud and used in any project.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd15a981-1f30-4b9b-836d-0ae9cb226b6a/04-sharing-code-between-projects.png" sizes="100vw" caption="Isolate, share and organize your reusable code. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd15a981-1f30-4b9b-836d-0ae9cb226b6a/04-sharing-code-between-projects.png'>Large preview</a>)" alt="Bit sharing workflow" >}}
<p>When building it, we set a few guidelines for what we needed from the project.</p>

<ul>
<li>Make it seamless to isolate and share code components from any project, without having to create new repositories or manually configure build and test environments and dependencies for each component.</li>
<li>Enable two-way development, so that each component could be changed and updated from any project, while changes would be synced across our code base.</li>
<li>Make it simple to organize and share our components, while making them discoverable for our entire team with useful visual information.</li>
</ul>

<p>After hard work and extensive research, in 2017 we released the first version of <a href="https://github.com/teambit/bit">Bit</a> to GitHub.</p>

### How It Works

<p><a href="https://docs.bitsrc.io/">Bit’s workflow</a> is made of three simple steps:</p>

<ol>
	<li>The first is to simply tell Bit which components of code you would like to share from your project, and it will immediately start tracking them in all of the projects you share them in.</li>
	<li>You can then tag a version for these components so that Bit automatically defines and locks their dependency tree for both file and package dependencies, and creates an isolated environment for each component to build and test in isolation.</li>
	<li>Finally, you can share the components to the cloud (or your own remote server), where they will be organized, will be made discoverable and can be installed with NPM or Yarn like any other package.</li>
</ol>

<p>You don’t have to create new repositories, split your code base or refactor a single line of code.</p>

<p>Now comes the really cool part. You can also <strong>use Bit to import the components into other projects</strong> for further development. Because Bit tracks your components between projects, you can simultaneously develop them from different repositories and sync changes across your code base.</p>

<p>This fast and distributed workflow means you won’t be tied by ownership issues, and you can actually develop the shared code and update changes from any of your team’s projects.</p>

<p>Let’s see an example.</p>

### Example: Bit With React UI Components

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/625fcc75-6aed-46c0-b5cd-9ff1f1895397/07-sharing-code-between-projects.png" sizes="100vw" caption="A <a href='https://bitsrc.io/bit/movie-app/components/hero'>React Hero component</a> with Bit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/625fcc75-6aed-46c0-b5cd-9ff1f1895397/07-sharing-code-between-projects.png'>Large preview</a>)" alt="A React Hero component with Bit" >}}

<p>For this example, let’s pick a common use case: syncing React UI components between apps. Although designed to be reusable, achieving such reusability can be <a href="https://medium.com/walmartlabs/how-to-achieve-reusability-with-react-components-81edeb7fb0e0#.brpw2m2yu">challenging</a>.</p>

<p>Let’s take an example <a href="https://github.com/teambit/movie-app">React app</a> on GitHub. It contains eight reusable <a href="https://github.com/teambit/movie-app/tree/master/src/components">React UI components</a> and one global styling component. As you can see, Bit was added to the repository (see the <code>bit.json</code> and <code>.bitmap</code> files) to track these components &mdash; but not a single line of code was changed in the repository. From there, the components were shared to the <a href="https://bitsrc.io/bit/movie-app">corresponding scope</a> on Bit’s free web hub.</p>

<p>As you can see, <strong>each of the components is now available to any developer</strong> to install with NPM or Yarn or to import into their own projects for further development.</p>

<p>All of the components are organized and can be shared with your team and searched for via a search engine. They are presented with visual rendering, build and test results (you can use premade external build and test <a href="https://bitsrc.io/bit/envs">environments</a> or create your own), and come with auto-parsed docs so that you can make an informed decision on which components to use.</p>

<p>Once it’s changed from a different project, you can update the component’s version in the scope (which works as a remote source of truth) and sync changes between different repositories.</p>

<p>A short <a href="https://docs.bitsrc.io/tutorial/react-tutorial.html">tutorial for React</a> is available for the example project.</p>

## Conclusion

<p>Sharing code between projects is vital to building software faster, while making your code base simpler to maintain and develop over time. As more of our applications are built using reusable components such as React and Vue UI components, Node.js modules, simple functions, GraphQL APIs and more, turning them into building blocks for different projects becomes more rewarding.</p>

<p>However, the overhead of splitting repositories, refactoring projects, and modifying components from different projects can make it hard to effectively collaborate and share your code. These are the lessons learned from our own journey towards <strong>simple and effective code sharing</strong>, making it simpler to share, discover and collaborate as a team while building with our common LEGO bricks.</p>

<p>Bit is an open-source project, so feel free to <a href="https://github.com/teambit/bit#contributing">jump in</a>, <a href="https://github.com/teambit/bit/issues">suggest feedback</a> or <a href="https://gitter.im/bit-src/Bit">ask anything</a>. Just remember that, at the end of the day, sharing code is always about people and about growing a collaborative culture where people play together to build great things.</p>

{{< signature "rb, ra, al, yk, il" >}}

