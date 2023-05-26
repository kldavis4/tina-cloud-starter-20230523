---
title: 'The Issue With Global Node Packages'
slug: issue-with-global-node-npm-packages
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1c54ef1-cdc6-416e-9d3a-8717db289b3d/excerpt-node-opt.png
date: 2016-01-19T18:23:18.000Z
author: joseph-zimmerman
summary: >-
 Node.js brought about a great revolution for JavaScript developers by allowing us to write code that runs directly on our machines. We started to easily write tools for the command line that automate a lot of things in our development cycles. npm, which is bundled with Node.js, made this even easier by giving us quick and easy access to tools that others have created, which we install on our machines to access from wherever we are in our system. Make the most out of it Installing packages from npm globally.
description: >-
  Node.js runs JavaScript directly on our machines, allowing us to create and share tools, using npm, to automate steps in our development cycles. Make it even better installing npm packages globally.
categories:
  - Coding
  - Workflow
  - JavaScript
  - Node.js
---

**Node.js** brought about a great revolution for JavaScript developers by allowing us to write code that runs directly on our machines; our skills were no longer limited to browsers alone. At first, many of us simply saw this as a way to **write our application servers without needing to learn another language**, but we all quickly caught on to the fact that we could also write tools for the command line that automate a lot of things in our development cycles.

npm, which is bundled with Node.js, made this even easier by giving us quick and easy access to tools that others have created, which we install on our machines to access from wherever we are in our system. JavaScript was finally a “real” programming language. But with these new capabilities came a lot of best practices that needed to be discovered, because there were many new scenarios that wouldn’t be found in the browser. In particular, **I’d like to discuss a practice that has been on my mind** a lot lately that I think much of the community needs to evaluate.

## What’s the Issue?

I’m specifically talking about **installing packages from npm globally** using `npm install -g`. Don’t get me wrong: Installing packages globally is certainly helpful and convenient at times, but we don’t always use it wisely.

Rule of thumb: If your project depends on a package, it should be listed in your `package.json` file as a dependency and installed locally in your project, rather than globally. Tools that your projects do not depend on can certainly be installed globally. For example, I use [UglifyJS](https://www.npmjs.com/package/uglify-js) as a globally installed package to do one&ndash;off JavaScript file minification when the file isn’t part of a larger project or when I just want to share one file. Another good example would be the [http-server](https://www.npmjs.com/package/http-server) package, which allows me to start up a simple file server in whatever directory I need with a simple command.

You might also be able to get away with using global packages if you’re working on an internal project, because many tools (like Docker) can use automation to neutralize some of the issues with global packages. If you’re working on a public and/or open&ndash;source project, though, please pay close attention because you are the primary audience of this post!

{{% feature-panel %}}

## Why Shouldn’t I Install Dependencies Globally?

The obvious short answer is that your project depends on them. If your project depends on a package, it should be documented in `package.json` so that you can guarantee that it is installed when someone types `npm install`. Otherwise, you’ll need to add extra steps in your README file to inform anyone else who clones your project that they need to install each of your global dependencies as well.

For example, if your project relies on [Browserify](https://www.npmjs.com/package/browserify) (we’ll be using Browserify in our examples from here on out), then you may have written a few steps in your README that look like this to help people get started with your project:

To use this project, follow these steps:

1.  `git clone` the repo.
2.  Run `npm install`.
3.  Run `npm install -g browserify`.
4.  Run `browserify main.js > bundle.js` to build.

**Why force the user to add the extra step of installing Browserify globally?** Besides making it simpler to guarantee that Browserify gets installed, adding it to your dependency list in `package.json` also guarantees that the correct version of Browserify will be installed. Having the wrong version of a dependency is often just as bad as not having the dependency installed at all. This means you should include the version of Browserify, and any other global packages you’re using, in your README file (I’m not sure I’ve ever seen anyone do this). This also means that if you update to a newer version of any of those packages, you’ll need to update the README with the new version as well.

Finally, even if someone installs the correct version of Browserify for your project, they may be working on a different project that requires a different version of that same tool, which **would cause conflicts**. Several of your own projects might even use different versions of Browserify because you updated it when you started a new project and didn’t go back to make sure that earlier projects were updated to work with the new version. These conflicts can be avoided.

{{% ad-panel-leaderboard %}}

## What Can I Do About It?

The obvious answer is that you need to avoid using that `-g` flag when you install your packages and start using `-S` or `--save` to save them to your dependencies or `-D` or `--save-dev` to save them to your development dependencies. This, of course, isn’t the whole answer because it doesn’t explain how you can run packages like Browserify from the command line, which was the point of installing it globally in the first place. It wouldn’t be much of a solution if it couldn’t solve the original use case, would it?

Well, don’t worry. As I said, this isn’t the whole answer. So far, we’ve **solved the issue of version collisions** and eliminated a step and some maintenance from our README files. Before arriving at the best solution, we need to know an important fact: When you locally install a package that has “binary” files (i.e. it’s executable from the command line), then the binaries that are necessary for executing that tool will be stored in `./node_modules/.bin`. This means you can use `./node_modules/.bin/browserify` to execute a locally installed version of Browserify. Of course, nobody really wants to type all of that nonsense out, but it’s a start.

A quick fix would be to add `./node_modules/.bin` to your PATH environment variable so that you can just run `browserify` to get it to work. At first, I was floored when I was informed that you could use relative paths like that in your PATH (thanks to a [comment on another post I wrote](https://www.joezimjs.com/javascript/no-more-global-npm-packages/#comment-1952307113)), but since then my emotions have leveled off because I realized that this only works when you are in the root directory of your project. The best workaround I could find is to **throw a few more entries in your PATH** so that you can do this from subdirectories as well (`../node_modules/.bin/` and `../../node_modules/.bin/` and so on, for as many levels deep as you deem necessary); then, it should always be able to find the bin you’re looking for. Note that using relative PATHs has security risks, so use this only on your development machines.

Changing your PATH on your own machine is great because it saves you keystrokes, but I don’t think telling people who use your project that they need to alter their PATH is a great idea. One final solution takes a bit of configuration for each project but can be very helpful later on, especially for other users of your project: [npm scripts](https://docs.npmjs.com/cli/run-script). In your `package.json` file, you can specify a `scripts` property that essentially creates aliases for your commands that npm can run. Let’s say your `package.json` looks like this:

<pre><code class="language-javascript">{
    …
    "scripts": {
        "browserify": "browserify"
    }
    …
}</code></pre>

You could run `npm run browserify`, and it would run the Browserify version that you have installed locally to this project. The key for the property is the alias that you’re creating to use with `npm run` (for example, `npm run $KEY`), and the value is the command that will actually be executed. When you do this, npm will look for the `browserify` binary in the `./node_modules/.bin/` folder first before checking the rest of the folders in your PATH for it.

Of course, having to type `npm run browserify` instead of just `browserify` isn’t nearly as efficient, but I usually don’t use npm scripts like that. Instead, I set it up so that no one needs to know that I use Browserify, by creating a generic alias and letting it envelope a much larger command. For example:

<pre><code class="language-javascript">{
    …
    "scripts": {
        "build": "browserify main.js &gt; bundle.js"
    }
    …
}</code></pre>

Now, I can run `npm run build`, which lets everyone know that they are building the project, without telling them the nitty&ndash;gritty details of how it’s built, and I’m actually saving keystrokes. The encapsulation allows you to completely change the tooling and configuration of your build (making the change to [webpack](https://webpack.github.io/), for example), without having to tell anyone about it or having to update the documentation.

npm scripts also allow you to pass other options to the command you are executing by first passing `--` to tell npm that the rest of the parameters are to be passed to the command that’s being executed, rather than to be passed directly to `npm run`. For example, using the `build` script that I just created, we can run `npm run build -- --debug`, which would be the equivalent of running `browserify main.js &gt; bundle.js --debug`.

npm scripts are very helpful tools for making common tasks easy to find and run and for giving other users really simple access to them. You could even go all out and learn [how to use npm as your “build tool”](https://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/), which is becoming more popular. I put “build tool” in quotation marks because, technically, all it is doing is aliasing commands for your project, but people still tend to call it their build tool.

**Augmenting your PATH and/or utilizing npm scripts** might require a bit more work up front than just installing the tool globally, but I truly believe it is a better practice and will save us from some maintenance and compatibility issues in the long run, which is definitely a good thing. And you can’t go wrong by making things easier for consumers of your projects.

{{% ad-panel-leaderboard %}}

## Can Or Should We Take This Further?

When you get right down to it, you come to realize that Node.js and npm are also dependencies of your project that can cause version conflicts. So, we _should_ begin to list those as dependencies as well, somehow, to ensure that everyone can work with our projects with no fear of conflicts at all.

To do this, it is possible to **install portable or local copies of Node.js and npm** in your project. This has its own caveats. because you don’t want to store an installation of Node.js in your version control, and even if you did, that installation of Node.js likely wouldn’t work on a different computer because it would be specific to the operating system.

Also, this would require you to adjust your PATH to use the local Node.js and npm, and your users would be required to do so as well. These don’t seem like very good tradeoffs to me, so in my opinion, we haven’t reached the point where this is simple enough to do. Maybe some tools will emerge in the future to allow this, but we’ll just have to shove this idea to the wayside for now.

## Conclusion

That’s all I have for you today. I hope you see the importance of keeping _all_ of your dependencies listed and versioned in your project. If you agree with me, please help promote this idea by pointing it out whenever you see a project that doesn’t follow this principle. But remember to be nice! In fact, you could even consider adding a pull request to make the change for the project in question.

_Excerpt image: [npmjs.com](https://www.npmjs.com/package/http-server)_

### Further Reading on Smashing Magazine:

- “[A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/),” Joseph Zimmerman
- “[Preload With Webpack](https://www.smashingmagazine.com/2017/02/web-development-reading-list-168/),” Anselm Hannemann
- “[How To Harness The Machines: Being Productive With Task Runners](https://www.smashingmagazine.com/2016/06/harness-machines-productive-task-runners/),” Adam Simpson
- “[React Native For Web: A Glimpse Into The Future](https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/),” Clayton Anderson

{{< signature "rb, al, ml, jb, nl" >}}