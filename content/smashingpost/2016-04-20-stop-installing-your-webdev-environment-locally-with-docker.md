---
title: Why You Should Stop Installing Your WebDev Environment Locally
slug: stop-installing-your-webdev-environment-locally-with-docker
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c63ccb04-252f-4284-aa33-5c688db36471/docker.png'
date: 2016-04-20T15:36:20.000Z
author: danieldemmel
description: >-
  Have you heard of Docker but thought that it’s only for system administrators
  and other Linux geeks? Or have you looked into it and felt a bit intimidated
  by the jargon? Or are you **silently suffering with a messy development
  environment** that seems to break all of the time in various mysterious ways?
  Then read on. By the end of this article, you should have a basic
  understanding of Docker and have it working on your computer!

  The first part of this article gives a bit of background to help you
  understand the concepts behind Docker through some metaphors. But if you just
  want to get started with the tutorial, skip to the “Time to Play!” section.
categories:
  - Coding
  - Tools
  - Techniques
---
Have you heard of Docker but thought that it’s only for system administrators and other Linux geeks? Or have you looked into it and felt a bit intimidated by the jargon? Or are you <strong>silently suffering with a messy development environment</strong> that seems to break all of the time in various mysterious ways? Then read on. By the end of this article, you should have a basic understanding of Docker and have it working on your computer!

The first part of this article gives a bit of background to help you understand the concepts behind Docker through some metaphors. But if you just want to get started with the tutorial, skip to the <a href="#time-to-play">“Time to Play!”</a> section.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [The Issue With Global Node Packages](https://www.smashingmagazine.com/2016/01/issue-with-global-node-npm-packages/)
*   [How To Develop An Interactive Command Line Application](https://www.smashingmagazine.com/2017/03/interactive-command-line-application-node-js/)

## A Brief History Of The Shipping Industry

### Break-Bulk Shipping

The loading and unloading of individual goods in barrels, sacks and wooden crates from land transporters to ship, and back again on arrival, used to be slow and cumbersome. Nevertheless, this process, referred to as break-bulk shipping, was the only known way to transport goods via ship up until the second half of the 20th century.

{{% feature-panel %}}

Needless to say, this process was very labor-intensive. A ship could easily spend more time at port than at sea, as dockworkers moved cargo into and out of tight spaces below decks. There was also high risk of accident, loss and theft.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/974b7883-3df4-4b90-b6dd-fa9c9af96c9a/01-port-adelaide-1927-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88bd87d1-aa1d-4779-ae7b-b5593a7471c6/01-port-adelaide-1927-preview-opt.jpg" alt="Queen’s Wharf, Port Adelaide, before 1927." width="500" height="402" /></a><figcaption>Queen’s Wharf, Port Adelaide, before 1927 (Image: <a href="https://collections.slsa.sa.gov.au/resource/B+4433">State Library of South Australia</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/974b7883-3df4-4b90-b6dd-fa9c9af96c9a/01-port-adelaide-1927-opt.jpg">View large version</a>)</figcaption></figure>

### The Introduction of Shipping Containers

Fast-forward to 26 April 1956, when Malcolm McLean’s converted World War II tanker, the Ideal X, made its maiden voyage from Port Newark to Houston. She had a reinforced deck carrying 58 metal container boxes, as well as 15,000 tons of bulk petroleum.

By the time the container ship docked at the port of Houston six days later, the company was already taking orders to ship goods back to Port Newark in containers. McLean’s enterprise later became known as Sea-Land Services, a company that changed the face of shipping forever.

Many famous inland ports (including London’s Docklands) were completely shut down, as ever-larger container ships had to use open (and usually new) seaside ports.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7add6b8-0a4b-4014-9510-9b6955f953c9/02-malcolm-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f23d965-f231-4e0e-bfb4-da68418991fe/02-malcolm-preview-opt.jpg" alt="Malcolm McLean at railing, Port Newark, 1957" width="500" height="499" /></a><figcaption>Malcolm McLean at Port Newark, 1957 (Image: <a href="https://www.flickr.com/photos/maerskline/7312751706/">Maersk Line</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7add6b8-0a4b-4014-9510-9b6955f953c9/02-malcolm-opt.jpg">View large version</a>)</figcaption></figure>

### But Why Would a Developer Care About Shipping Containers?

In the 1950s, Harvard University economist Benjamin Chinitz predicted that containerization would benefit New York by allowing it to ship its industrial goods to the southern United States more cheaply than from other areas, like the midwest. But what actually happened is that importing such goods from abroad became cheaper, wiping out the state’s dominant apparels industry, which was meant to be the beneficiary.

While I obviously can’t foresee the future, it looks like a new wave of containerization is about to transform software, particularly web development, with some potentially major consequences.

But what are the main characteristics of shipping containers?

*   They abstract what’s inside with a tough corrugated steel shell, the private and protected contents of which are known only to the creators.
*   They provide a standardized interface for efficient handling and stacking throughout the delivery chain.
*   They make it easy for anyone to scale their operations quickly using this existing standardized infrastructure.

Hmm, some familiar keywords in there, right?

## What Is The Problem With Local Development Environments?

Even if you install dependencies only for projects that you have to actively work on, after a few new projects, things will start to become a mess — a mess that is difficult to clean up and even harder to restore if you need to work on some old project again.

And if you’re not paying the bills with just a few projects but also want to contribute to open-source libraries — which you totally should, but that means you might need to compile them — then that would get totally out of hand.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/821d950a-fb4e-496b-b685-8a153c261dc0/03-port-adelaide-1927-env-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c96f9c-c2e6-454c-9182-fe3e1cc9e8c9/03-port-adelaide-1927-env-preview-opt.jpg" alt="03-port-adelaide-1927-env-preview-opt" width="500" height="402" /></a><figcaption>Queen’s Wharf, Port Adelaide, before 1927, with runtimes all over the place (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/821d950a-fb4e-496b-b685-8a153c261dc0/03-port-adelaide-1927-env-opt.jpg">View large version</a>)</figcaption></figure>

What if we could have a software Malcolm, locking each project’s mess into the digital equivalent of corrugated steel boxes?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49c9889a-0dbc-4c98-b5bd-a450d6f61fd9/04-malcolm-env-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49c9889a-0dbc-4c98-b5bd-a450d6f61fd9/04-malcolm-env-opt.jpg" alt="Malcolm McLean at railing, Port Newark, 1957, with runtimes neatly in containers" width="500" height="499" /></a><figcaption>Malcolm McLean, Port Newark, 1957, with runtimes neatly in containers (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49c9889a-0dbc-4c98-b5bd-a450d6f61fd9/04-malcolm-env-opt.jpg">View large version</a>)</figcaption></figure>

### Approaches for Multi-Project Development Environments

A few years ago, the best solution around was to use package managers (RubyGems and Bundler, npm, Maven, etc.) with local project-specific dependency bundles, instead of installing libraries on a global operating-system level. Together with runtime version switchers (Ruby Version Manager, rbenv, nvm, JSelect, etc.), these provided temporary relief, but there were still differences between environments on different developer machines, often resulting in broken builds and generally weird behavior. Of course, you were almost guaranteed to have to set up every single project again after every OS update and to remember quirky workarounds for legacy projects (if the dependencies were even still available).

Then, virtualization started becoming more mainstream (and open source) on the desktop, after years of success on servers. So, with help of the likes of Virtualbox and Vagrant, it became possible to run an entire operating system in a virtualized environment, independent of the host system. This way, the environments for all development computers and even production servers could be identical. While this is a powerful and versatile solution, the downside is a big hit on the resources of the host machine.

Taking the sealed-box approach from full-fat virtualization, yet sharing the kernel and some low-level components from the host operating system, containerization offers the best of both worlds. Because no actual virtualization is happening on a container level (just a few fences are drawn up and torn down for isolation), start-up is pretty much instant, and the direct access to the CPU and other hardware components eliminates performance overhead.</p>

## Enter Docker’s Containers

Docker started out by being built on an implementation called Linux Containers (or LXC) which has been around for quite a while; so, containers aren’t a totally new concept. That being said, Docker’s makers later decided to create a layer that depends less on Linux distribution-specific components, which was first Libcontainer and now RunC. Quite a lot of details are involved in how these container implementations actually work; however, from a user perspective, it’s enough to know that the high-level architecture is to run what’s inside the containers, with a limitation and prioritization of resources, its own networking, a mounted file system and so on, thereby creating practically complete but securely fenced child operating systems inside the host.

Docker itself is open-source and offers a large ecosystem of tools and contributors on top of the basic container technology, addressing several levels of the problem.</p>

### Docker Engine

The Docker Engine, or just Docker, is the core and deals with the containers themselves. It bundles together the barebones Unix-style utilities for handling various aspects of the containers, and it adds several convenience functions around them.

With Docker, a nice REST API is exposed on the containers, which makes it possible for both command-line and GUI tools (locally) and deployment scripts (remotely) to interact with them. It also makes it very simple to define images with a single <code>Dockerfile</code>, which enables one to build layered, incremental images quickly, including downloading and compiling all of the dependencies.

Because Docker is Linux-based, if you want to use it on Windows or Mac, it’ll need virtualization after all, which is typically done with the open-source Virtualbox and the tiny Boot2Docker image (although there are some promising up-and-comers, like <a href="https://www.xhyve.org/">xhyve</a>). Of course, you can have as many containers in one box as you’d like, inside which containers would work the same way as on Linux, sharing the resources of one host machine.</p>

## Time To Play!

### Installing Docker Toolbox

The simplest way to get started is to download the official <a href="https://www.docker.com/docker-toolbox">Docker Toolbox</a>. This is an installer that puts in place all Docker-related tools. It also makes sure Virtualbox is installed (in case you’re not using Linux and don’t already have it) and sets up the Boot2Docker image.

Once the installation process is completed, you should start Kitematic (Docker’s UI interface), an app that will automatically create a Docker host environment (named <code>default</code>) for you. If everything has gone well, you should see a list of downloadable Docker images on the right.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab42e673-7c5c-48f3-b532-90a7c7bef823/05-kitematic-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab42e673-7c5c-48f3-b532-90a7c7bef823/05-kitematic-preview-opt.png" alt="Kitematic screenshot with a cornucopia of Docker images" width="500" height="346" /></a><figcaption>Kitematic screenshot with a cornucopia of Docker images (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab42e673-7c5c-48f3-b532-90a7c7bef823/05-kitematic-preview-opt.png">View large version</a>)</figcaption></figure>

### Cloning the Tutorial Repository

Now we are ready to Dockerize a small React, Sass and Node.js app, compiled with Gulp, which should be just enough to see something beyond “Hello World.”

To get started with this, clone the <a href="https://github.com/daaain/docker-tutorial">tutorial’s repository from GitHub</a>.</p>

<strong>Note:</strong> Make sure your working copy is under <code>/Users/[username]</code> (Mac OS X) or <code>C:\Users\[username]</code> (Windows). Otherwise, mounting source-code folders won’t work later — these folders are automatically mapped by Docker.

If you haven’t done so yet, crack open a terminal shell, and go to the folder where you checked out the repository! All commands below (starting with, but without pasting, <code>&gt;</code>) will have to be executed there.</p>

### Getting the Docker Host Ready

Because we’re going to use the <code>default</code> Docker host, you don’t have to create one. If you want to do it (later), you can use <code>docker-machine create</code>.

However, we need to tell Docker that we want to use this <code>default</code> host. So, go ahead and type this:

<pre><code class="language-bash">&gt; eval "$(docker-machine env default)"
</code></pre>

You’ll need to do this for every new shell session, or else put it in your <code>.profile</code> or <code>.bashrc</code> file. The reason for this is that Docker can work with multiple hosts locally, remote hosts like AWS, and swarms, so it can’t safely assume where you want to work.

To verify that everything has gone well, type the following:

<pre><code class="language-bash">&gt; docker-machine ls
</code></pre>

This should return all of the Docker hosts you have set up, and you should see <code>default</code> set as active. So, something like this:

<pre><code class="language-bash">NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER    ERRORS
default   *        virtualbox   Running   tcp://192.168.99.100:2376           v1.9.1
</code></pre>

### Writing the Dockerfile

This is where things get really interesting! The <code>Dockerfile</code> is essentially a step-by-step recipe for Docker to compile an image and create a container environment exactly the way you need it to be. For the sake of this tutorial, we’ll need to set up <a href="https://www.smashingmagazine.com/2014/05/detailed-introduction-nodejs-mongodb/">a simple Node.js environment</a> so that we can install libraries using npm and compile everything using Gulp.

So, open <code>Dockerfile</code> in your favorite text editor, and let’s get started!

The first line takes the official Node version 5 image from <a href="https://hub.docker.com/_/node/">Docker Hub</a>, prebuilt on top of Debian Jessie as a starting point:

<pre><code class="language-bash">FROM node:5
</code></pre>

Because Docker images can be pushed to Docker Hub and shared with other people, putting your name and email address in there is always a good practice. So, go ahead and edit the second line:

<pre><code class="language-bash">MAINTAINER You &lt;me@example.com&gt;
</code></pre>

You’re on your own now — good luck!

Just kidding. I left the rest empty so that we can fill it in together step by step.

To tell Node.js that this is a development image, let’s set the <code>NODE_ENV</code> environment variable to <code>development</code>:

<pre><code class="language-bash">ENV NODE_ENV=development
</code></pre>

Then, we need to set the base folder inside the image for Docker to put files in. So, let’s put this:

<pre><code class="language-bash">WORKDIR /usr/local/src
</code></pre>

Now, we’re ready to start copying files from the local file system to the image:

<pre><code class="language-bash">COPY package.json /usr/local/src/package.json
</code></pre>

Having put <code>package.json</code> in there, let’s install the dependencies:

<pre><code class="language-bash">RUN npm install
</code></pre>

Now, we can copy our source files and start compiling with Gulp:

<pre><code class="language-bash">COPY gulpfile.js /usr/local/src/gulpfile.js
COPY .babelrc /usr/local/src/.babelrc
COPY src /usr/local/src/src
RUN npm run compile
</code></pre>

In case you’re wondering why there are two <code>COPY</code> and <code>RUN</code> sections, Docker caches the results as intermediate images after each line. In this case, if we don’t change the contents of <code>package.json</code>, it will just take the image from the previous run, with all of the npm dependencies already installed, making the build incomparably faster than if it had to do it from scratch every time.

By default, Docker containers are completely locked down. So, we need to open a port for the Node.js server:

<pre><code class="language-bash">EXPOSE 8877
</code></pre>

Finally, all Docker images need a default command to be executed automatically when running the container. In our case, let’s start a development Node.js server:

<pre><code class="language-bash">CMD ["babel-node", "src/server"]
</code></pre>

### Building the Image

Before you can use it in a container, you have to build your image. Type the following (making sure to include the <code>.</code> at the end):

<pre><code class="language-bash">&gt; docker build -t node-tutorial .
</code></pre>

Here, the <code>-t</code> parameter gives a name to the image; so, we can refer to it later without having to use the generated UUID hash.

This might take a while because Docker needs to download the Node.js image and all of the npm dependencies. If everything has gone well, something like this should be at the end of the output:

<pre><code class="language-bash">Step 12 : CMD babel-node src/server
 ---&gt; Running in c5fc0a3a5940
 ---&gt; ee02b5ac9bf4
Removing intermediate container c5fc0a3a5940
Successfully built ee02b5ac9bf4
</code></pre>

### Run the Container

At this point, you’re ready to run the container! So, let’s try this mouthful of a command — I’ll explain later what each parameter means:

<pre><code class="language-bash">&gt; docker run -p 8877:8877 -p 3001:3001 --name node-tut -v $(pwd)/src:/usr/local/src/src --sig-proxy=false node-tutorial npm run browsersync
</code></pre>

You should see the shell output inside Docker, with the Gulp compilation kicking off. And in a few seconds, the BrowserSync proxy should start up. So, if everything has gone well, things should be settling in, with something like these as the last few lines:

<pre><code class="language-bash">[14:08:59] Finished 'watch' after 70 ms
[14:08:59] [nodemon] child pid: 28
[14:08:59] [nodemon] watching 4 files
[BS] [info] Proxying: https://localhost:8878
[BS] Access URLs:
 -----------------------------------
       Local: https://localhost:8877
    External: https://172.17.0.2:8877
 -----------------------------------
          UI: https://localhost:3001
 UI External: https://172.17.0.2:3001
 -----------------------------------
[BS] Reloading Browsers…
docker-tutorial 1.0.0 up and running on 8878
</code></pre>

If that’s the case, you’ve just passed another big milestone and are ready to see the results in a browser!

Let’s exit Docker’s shell session by pressing <kbd>Ctrl</kbd> + <kbd>C</kbd>. In your own shell, type this:

<pre><code class="language-bash">&gt; docker-machine ip default
</code></pre>

This should return the IP address of the Docker host’s virtual machine. Knowing that, let’s open our favorite development browser and paste in this address, followed by port <code>8877</code>. So, something like <code>192.168.99.100:8877</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16fbbc8e-37e7-4d77-a41f-7ed86f69419c/06-tutorial-running-in-browser-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16fbbc8e-37e7-4d77-a41f-7ed86f69419c/06-tutorial-running-in-browser-preview-opt.png" alt="Application winning in Firefox screenshot" width="500" height="414" /></a><figcaption>Application winning in Firefox screenshot (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16fbbc8e-37e7-4d77-a41f-7ed86f69419c/06-tutorial-running-in-browser-preview-opt.png">View large version</a>)</figcaption></figure>

If you’re particularly adventurous, try editing any application-related file under <code>src</code>; in a moment, you should see the page reload. Congratulations! You have a relatively complex Node.js environment running in Docker!

With this moment of triumph, let’s look back and see what we did with this long <code>docker run</code> command. The basic anatomy looks like this:

<pre><code class="language-bash">docker run [OPTIONS] IMAGE [COMMAND] [ARG…]
</code></pre>

These were our <code>OPTIONS</code>:

*   `-p hostPort:containerPort` This maps the container ports to the host so that you can expose and access the web server ports.
*   `-v hostDir:containerDir` This mounts the local files and folders so that your local edits get pushed to the container without requiring a rebuild.
*   `--name containerName` This assigns a name to your container so that you don’t have to use the UUID hash.
*   `--sig-proxy=false` This lets us exit from Docker’s shell without killing the running process inside (by not proxying the SIGTERM — hence, the name).

Finally, the name of the <code>IMAGE</code> is <code>node-tutorial</code>, and the <code>COMMAND</code> + <code>ARG…</code> are <code>npm</code> + <code>run browsersync</code>.</p>

## I Want More!

While finishing the tutorial above should cover the basics of getting started with Docker for development, there’s much more to it. I’ve gathered some tips and pointers to get you started on the journey. There’s also a good (but rather long) <a href="https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/">guide to best practices</a> in Docker’s documentation.</p>

### Images vs. Containers

Perhaps one of the most important things to understand is the difference between images and containers. Images are read-only and come in layers. In the tutorial above, the layers are: the Debian Jessie base Linux image → the official Node.js 5 image → our customizations in the <code>Dockerfile</code>. These layers can be modified only by rebuilding the images; this way, you’ll always know what you’re getting, and it becomes a manageable process to share images in the Docker hub by building, pushing and pulling them. Containers, then, are the “machines” that run these images and add the layer of a writable file system on top. So, in the tutorial, the container is what enables volumes to be mounted and, with that, is what enables a way to keep on pushing and executing code inside without having to rebuild the entire image every time.

Because of this immutable nature of images, don’t expect files to stick around in a container when you restart it. This is why it’s important to use file system volumes for your code and, once you get to a more advanced level and want to deploy to production, volume containers for databases, logs, etc.</p>

### Docker Machine

Apart from helping with some basic management of the Docker container host (picking the virtual machine or starting and stopping it), once you have several containers between and maybe even within projects or you want to deploy and manage them on a cloud provider, Docker Machine will give you some simple commands to help with these.</p>

### Docker Hub and Registry

<a href="https://hub.docker.com">Docker Hub</a> is the place to go for community-maintained containers. These containers range from simple base Linux distribution flavors with the bare minimum (<a href="https://hub.docker.com/_/alpine/">Alpine</a> is a great lean image, for example) all the way up to complete application stacks (for <a href="https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/">WordPress</a>, Minecraft, etc.), ready to be started up and used.

As well as the automatic builds, you also get web hooks. So, integrating your continuous integration or deployment system shouldn’t be a problem.</p>

### Kitematic

While I’m reasonably comfortable with the terminal shell, I’m also the first to admit that, for example, unless I need to do something really complex with Git (like fixing a messed-up commit history), I won’t bother doing it manually and will happily do my commits, diffs and interactive rebases in the SourceTree app.

If you want to avoid the command line, that’s totally fine. Docker recently bought the similarly open-source Kitematic, which is a simple but decent UI to drive Docker. It’s still in its infancy but already lets you monitor logs; start, stop and restart containers; and view settings such as volumes, ports, etc.</p>

### Docker in Production or Not?

It is worth making clear that you don’t need to commit to using Docker in production in order to use it to manage your development environment. You can stick to whatever way you’re doing it now. In fact, in this case, even on the same team, people can use Docker or a local environment. It doesn’t matter because the application code and repository will be the same except for the added <code>Dockerfile</code>.

That being said, if you do want to go to production, one important principle of containers is that they should run only one process and do one thing. Linking multiple containers to a network is not that difficult, but it is definitely a different approach and concept from working with virtual machines. If you want to see a working example of a few containers working in tandem, we have open-sourced our <a href="https://github.com/ustwo/ustwo.com-frontend">website code behind ustwo.com</a>.</p>

### More Than Just Servers and Daemons

Just to give you an idea of how versatile a tools container can be, you can even use them instead of locally installed desktop tools. For example, you can convert an image with ImageMagick without having to worry about installing it with all of its dependencies. So, if you have <code>open.png</code> in the current folder and you want a <code>.jpg</code> version, you can just do this:

<pre><code class="language-bash">&gt; docker run --rm -v $(pwd):$(pwd) jess/imagemagick convert $(pwd)/open.png $(pwd)/open.jpg
</code></pre>

This will pull the tiny ImageMagick image, mount the current folder under the same path inside the container, do the conversion, sync the file back, exit, and remove itself when finished.

For more inspiration, check out the blog post “<a href="https://blog.jessfraz.com/post/docker-containers-on-the-desktop/">Docker Containers on the Desktop</a>” on the brilliant Jessie Frazelle’s blog.</p>

### Beyond Docker

While the Linux-based Docker is the current star in the space, the <a href="https://www.opencontainers.org/">Open Container Initiative</a> is taking the containerization idea forward with a cross-platform standard. It’s backed by a big industry alliance, including Microsoft, which is promising to make it work natively on Windows. Apple is notably absent at this point, but let’s hope it is just taking its time.</p>

## The Future

Containerization will start a revolution in open source similar to what Git did, by making it much simpler to take any code and start compiling it right away.

You can quote me on that. I’m fairly confident that we’ll see more and more open-source projects — especially complex ones — embrace containerization for dependency management. All it takes is for someone to add a <code>Dockerfile</code>, after all. And in most cases, people may still choose not to use it and go with their existing local setup instead.

This will dramatically lower the barrier to entry for newcomers to a project, enabling potentially an order of magnitude more people to get involved, just like Git and GitHub did.</p>

## Takeaways

*   Containerize any non-trivial development environment, especially legacy ones.
*   Containerize your open-source projects to remove the barrier to entry for new contributors.
*   Containerize other people’s open-source projects, instead of setting up the environment on your local machine, so that you solve it for all.

{{< signature "rb, ml, al, il" >}}

