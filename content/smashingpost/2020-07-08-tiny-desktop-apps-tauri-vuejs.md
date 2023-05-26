---
title: 'Creating Tiny Desktop Apps With Tauri And Vue.js'
slug: tiny-desktop-apps-tauri-vuejs
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a942f1db-3e36-4839-b284-d87e327da023/tiny-desktop-apps-tauri-vuejs.png
date: 2020-07-08T11:00:00.000Z
summary: >-
  Tauri is a toolchain for creating small, fast, and secure desktop apps from your existing HTML, CSS, and JavaScript. In this article, Kelvin explains how Tauri plays well with the progressive framework Vue.js by integrating both technologies in bundling an example web app called **nota** as a native application.
description: >-
  Tauri is a toolchain for creating small, fast, and secure desktop apps from your existing HTML, CSS, and JavaScript. In this article, Kelvin explains how Tauri plays well with the progressive framework Vue.js by integrating both technologies in bundling an example web app called **nota** as a native application.
categories:
  - Vue
  - JavaScript
  - Tools
---

Technology makes our lives better, not just users, but also creators (developers and designers). In this article, I’ll introduce you to Tauri. This article will be useful to you if:

- you have been building applications on the web with HTML, CSS, and JavaScript, and you want to use the same technologies to create apps targeted at Windows, macOS, or Linux platforms;
- you are already building cross-platform desktop apps with technologies like Electron, and you want to check out alternatives;
- you want to build apps with web technologies for Linux distributions, such as PureOS;
- you are a Rust enthusiast, and you’d like to apply it to build native cross-platform applications.

We will look at how to build a native cross-platform application from an existing web project. Let’s get to it!

**Note**: *This article assumes you are comfortable with HTML, CSS, JavaScript, and Vue.js.*

{{% feature-panel %}}

### What Is Tauri?

The [official website](https://tauri.studio) sums up Tauri well:

- Tauri is a polyglot toolchain for building more secure native apps with both tiny and fast binaries. By “polyglot”, I mean that Tauri uses multiple programming languages. At the moment, Rust, JavaScript, and TypeScript are used. But there are plans to let you use Go, C++, Python, and more.
- It lets you use any HTML and JavaScript-based front-end framework, such as Vue.js, React, or Angular, to build a native desktop app, and it can be integrated into any pipeline.
- It helps you build and bundle binaries for major desktop platforms (mobile and WebAssembly coming soon).

So, basically, Tauri allows you to use web technologies to create tiny and secure native desktop apps.

On its [GitHub page](https://github.com/tauri-apps/tauri), Tauri is described as a framework-agnostic toolchain for building highly secure native apps that have tiny binaries (i.e. file size) and that are very fast (i.e. minimal RAM usage).

## Why Not Electron?

A popular tool for using web technologies to build desktop applications is Electron.

However, Electron apps have a rather large bundle size, and they tend to take up a lot of memory when running. Here is how Tauri compares to Electron:

- **Bundle**  
The size of a Tauri app can be less than 600 KB.
- **Memory**  
The footprint of a Tauri app is less than half the size of an Electron app.
- **Licence**  
Relicensing is possible with Tauri, but not with Electron. Electron ships with Chromium right out of the box. However, Chromium includes a digital rights-management system named [Widevine](https://en.wikipedia.org/wiki/Widevine). The inclusion of Widevine in Chromium makes apps created with Electron frowned upon by users of platforms such as PureOS for the sole reason that it is not free/libre open-source software (FLOSS). Platforms like PureOS are verified by the Free Software Foundation (FSF). This means that they can only publish free and open-source software in their app stores.

In a nutshell, if your app is built with Electron, it will never be shipped officially in the PureOS store. This should be a concern for developers targeting such [distributions](https://en.wikipedia.org/wiki/Linux_distribution).

## More Features Of Tauri

- Security is really important to the Tauri team. Apps created with Tauri are meant to be secure from the get-go.
- Tauri is compatible with any front-end framework, so you don’t have to change your stack.
- It has many design patterns to help you choose important features with simple configurations.

## Pros Of Tauri

- Tauri enables you to take the code base you’ve built for the web and turn it into a native desktop app, without changing a thing.
- Although you could use Rust in a Tauri-based project, it is completely optional. If you did, you wouldn’t need to change anything in your original code base targeted for the web.

## Real-World Tauri

If you have been part of the Vue.js community for a while, then you’ll have heard of [Guillaume Chau](https://twitter.com/Akryum), a member of the core team of Vue.js. He is responsible for the Vue.js command-line interface (CLI), as well as other awesome Vue.js libraries. He recently created [guijs](https://guijs.dev/), which stands for “graphical user interface for JavaScript projects”. It is a Tauri-powered native desktop app to visually manage your JavaScript projects.

Guijs is an example of what is possible with Tauri, and the fact that a core member of the Vue.js team works on the app tells us that Tauri plays nicely with Vue.js (amongst other front-end frameworks). Check out the [guijs repository](https://github.com/Akryum/guijs/) on GitHub if you are interested. And, yes, it is open-source.

## How Tauri Works

At a high level, Tauri uses [Node.js](https://nodejs.org) to scaffold an HTML, CSS, and JavaScript rendering window as a user interface (UI), managed and bootstrapped by [Rust](https://www.rust-lang.org/). The product is a monolithic binary that can be distributed as common file types for Linux (deb/appimage), macOS (app/dmg), and Windows (exe/msi).

## How Tauri Apps Are Made

A Tauri app is created via the following steps:

1. First, make an interface in your GUI framework, and prepare the HTML, CSS, and JavaScript for consumption.
2. The Tauri Node.js CLI takes it and rigs the Rust runner according to your configuration.
3. In development mode, it creates a WebView window, with **debugging** and **Hot Module Reloading**.
4. In build mode, it rigs the bundler and creates a final application according to your settings.

{{% ad-panel-leaderboard %}}

## Setting Up Your Environment

Now that you know what Tauri is and how it works, let me walk you through setting up your machine for development with Tauri.

**Note**: *The setup here is for Linux machines, but guides [for macOS](https://github.com/tauri-apps/tauri/wiki/03.-MacOS-Setup) and [for Windows](https://github.com/tauri-apps/tauri/wiki/04.-MS-Windows-Setup) are also available.*

### Linux Setup

The polyglot nature of Tauri means that it requires a number of tool dependencies. Let’s kick it off by installing some of the dependencies. Run the following:

<div class="break-out">

 <pre><code class="language-bash">$ sudo apt update && sudo apt install libwebkit2gtk-4.0-dev build-essential curl libssl-dev appmenu-gtk3-module
</code></pre>
</div>

Once the above is successful, proceed to install Node.js (if you don’t already have it), because Tauri requires its runtime. You can do so by running this:

<div class="break-out">

 <pre><code class="language-bash">curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
</code></pre>
</div>

This will install nvm (Node.js version manager), which allows you to easily manage the Node.js runtime and easily switch between versions of Node.js. After it is installed, run this to see a list of Node.js versions:

<pre><code class="language-bash">nvm ls-remote
</code></pre>

At the time of writing, the most recent version is 14.1.0. Install it like so:

<pre><code class="language-bash">nvm install v14.1.0
</code></pre>

Once Node.js is fully set up, you would need to install the Rust compiler and the Rust package manager: Cargo. The command below would install both:

<pre><code class="language-bash">$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
</code></pre>

After running this command, make sure that Cargo and Rust are in your `$PATH` by running the following:

<pre><code class="language-bash">rust --version
</code></pre>

If everything has gone well, this should return a version number.

According to the Tauri documentation, make sure you are on the latest version by running the following command:

<pre><code class="language-bash">$ rustup update stable
</code></pre>

Voilà! You are one step closer to getting your machine 100% ready for Tauri. All that’s left now is to install the `tauri-bundler` crate. It’s best to quit your CLI, and run the command below in a new CLI window:

<pre><code class="language-bash">$ cargo install tauri-bundler --force
</code></pre>

Eureka! If everything went all right, your machine is now ready for Tauri. Next up, we will get started integrating Tauri with Vue.js. Let’s get to it!

## Yarn

The Tauri team recommends installing the [Yarn package manager](https://yarnpkg.com/). So let’s install it this way:

<pre><code class="language-bash">npm install -g yarn
</code></pre>

Then run the following:

<pre><code class="language-bash">yarn --version
</code></pre>

If everything worked, a version number should have been returned.

{{% ad-panel-leaderboard %}}

## Integrating Tauri With Vue.js

Now that we have Tauri installed, let’s bundle an existing web project. You can find the live demo of the project [on Netlify](https://tauri-nota.netlify.app/). Go ahead and fork [the repository](https://github.com/DominusKelvin/nota-web), which will serve as a shell. After forking it, make sure to clone the fork by running this:

<pre><code class="language-bash">git clone https://github.com/[yourUserName]/nota-web
</code></pre>

After cloning the project, run the following to install the dependencies:

<pre><code class="language-bash">yarn
</code></pre>

Then, run this:

<pre><code class="language-bash">yarn serve
</code></pre>

Your application should be running on `localhost:8080`. Kill the running server, and let’s install the Vue.js CLI plugin for Tauri.

### vue-cli-plugin-tauri

The Tauri team created a [Vue.js CLI plugin](https://github.com/tauri-apps/vue-cli-plugin-tauri) that quickly rigs and turns your Vue.js single-page application (SPA) into a tiny cross-platform desktop app that is both fast and secure. Let’s install that plugin:

<pre><code class="language-bash">vue add tauri
</code></pre>

After the plugin is installed, which might take a while, it will ask you for a window title. Just type in `nota` and press “Enter”.

Let’s examine the changes introduced by the Tauri plugin.

## package.json

The Tauri plugin added two scripts in the scripts section of our `package.json` file. They are:

<pre><code class="language-json">"tauri:build": "vue-cli-service tauri:build",
"tauri:serve": "vue-cli-service tauri:serve"
</code></pre>

The `tauri:serve` script should be used during development. So let’s run it:

<pre><code class="language-json">yarn tauri:serve
</code></pre>

The above would download the Rust crates needed to start our app. After that, it will launch our app in **development mode**, where it will create a WebView window, with **debugging** and **Hot Module Reloading**!

### src-tauri

You will also notice that the plugin added a `src-tauri` directory to the root of your app directory. Inside this directory are files and folders used by Tauri to configure your desktop app. Let’s check out the contents:

<pre><code class="language-json">icons/
src/
    build.rs
    cmd.rs
    main.rs
Cargo.lock
Cargo.toml
rustfmt.toml
tauri.conf.json
tauri.js
</code></pre>

The only change we would need to make is in `src-tauri/Cargo.toml`. `Cargo.toml` is like the `package.json` file for Rust. Find the line below in `Cargo.toml`:

<pre><code class="language-toml">name = "app"
</code></pre>

Change it to this:

<pre><code class="language-toml">name = "nota"
</code></pre>

That’s all we need to change for this example!

## Bundling

To bundle `nota` for your current platform, simply run this:

<pre><code class="language-bash">yarn tauri:build
</code></pre>

**Note**: *As with the development window, the first time you run this, it will take some time to collect the Rust crates and build everything. On subsequent runs, it will only need to rebuild the Tauri crates themselves.*

When the above is completed, you should have a binary of `nota` for your current OS. For me, I have a `.deb` binary created in the `src-tauri/target/release/bundle/deb/` directory.*

## Going Cross-Platform

You probably noticed that the `yarn tauri:build` command just generated a binary for your operating system. So, let’s generate the binaries for other operating systems. To achieve this, we will set up a workflow on GitHub. We are using GitHub here to serve as a distribution medium for our cross-platform app. So, your users could just download the binaries in the “Release” tab of the project.
The workflow we would implement would automatically build our binaries for us via the power of [GitHub actions](https://github.com/features/actions). Let’s get to it.

## Creating The Tauri Workflow

Thanks to [Jacob Bolda](https://github.com/jbolda), we have a workflow to automatically create and release cross-platform apps with Tauri on GitHub. Apart from building the binary for the various platforms (Linux, Mac, and Windows), the action would also upload the binary for you as a release on GitHub. It also uses the [Create a Release](https://github.com/jbolda/create-release) action made by Jacob to achieve this.

To use this workflow, create a `.github` directory in the root of `nota-web`. In this directory, create another directory named `workflows`. We would then create a workflow file in `.github/workflows/`, and name it `release-tauri-app.yml`.

In `release-tauri-app.yml`, we would add a workflow that builds the binaries for Linux, macOS, and Windows. This workflow would also upload the binaries as a draft release on GitHub. The workflow would be triggered whenever we push to the master.

Open `release-tauri-app.yml`, and add the snippet below:

<div class="break-out">

 <pre><code class="language-yml">name: release-tauri-app

on:
  push:
    branches:
      - master
    paths:
      - '&#42;&#42;/package.json'

jobs:
  check-build:
    runs-on: ubuntu-latest
    timeout-minutes: 30

    steps:
      &mdash; uses: actions/checkout@v2
      &mdash; name: setup node
        uses: actions/setup-node@v1
        with:
          node-version: 12
      &mdash; name: install rust stable
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          profile: minimal
      &mdash; name: install webkit2gtk
        run: |
          sudo apt-get update
          sudo apt-get install -y webkit2gtk-4.0
      &mdash; run: yarn
      &mdash; name: build nota for tauri app
        run: yarn build
      &mdash; run: cargo install tauri-bundler --force
      &mdash; name: build tauri app
        run: yarn tauri:build

  create-release:
    needs: check-build
    runs-on: ubuntu-latest
    outputs:
      RELEASE_UPLOAD_URL: ${{ steps.create_tauri_release.outputs.upload_url }}

    steps:
      &mdash; uses: actions/checkout@v2
      &mdash; name: setup node
        uses: actions/setup-node@v1
        with:
          node-version: 12
      &mdash; name: get version
        run: echo ::set-env name=PACKAGE_VERSION::$(node -p "require('./package.json').version")
      &mdash; name: create release
        id: create_tauri_release
        uses: jbolda/create-release@v1.1.0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ matrix.package.name }}-v${{ env.PACKAGE_VERSION }}
          release_name: 'Release nota app v${{ env.PACKAGE_VERSION }}'
          body: 'See the assets to download this version and install.'
          draft: true
          prerelease: false

  create-and-upload-assets:
    needs: create-release
    runs-on: ${{ matrix.platform }}
    timeout-minutes: 30

    strategy:
      fail-fast: false
      matrix:
        platform: [ubuntu-latest, macos-latest, windows-latest]
        include:
          &mdash; platform: ubuntu-latest
            buildFolder: bundle/deb
            ext: \_0.1.0_amd64.deb
            compressed: ''
          &mdash; platform: macos-latest
            buildFolder: bundle/osx
            ext: .app
            compressed: .tgz
          &mdash; platform: windows-latest
            buildFolder: ''
            ext: .x64.msi
            compressed: ''

    steps:
      &mdash; uses: actions/checkout@v2
      &mdash; name: setup node
        uses: actions/setup-node@v1
        with:
          node-version: 12
      &mdash; name: install rust stable
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          profile: minimal
      &mdash; name: install webkit2gtk (ubuntu only)
        if: matrix.platform == 'ubuntu-latest'
        run: |
          sudo apt-get update
          sudo apt-get install -y webkit2gtk-4.0
      &mdash; run: yarn
      &mdash; name: build nota for tauri app
        run: yarn build
      &mdash; run: cargo install tauri-bundler --force
      &mdash; name: build tauri app
        run: yarn tauri:build
      &mdash; name: compress (macos only)
        if: matrix.platform == 'macos-latest'
        working-directory: ${{ format('./src-tauri/target/release/{0}', matrix.buildFolder ) }}
        run: tar -czf ${{ format('nota{0}{1}', matrix.ext, matrix.compressed ) }} ${{ format('nota{0}', matrix.ext ) }}
      &mdash; name: upload release asset
        id: upload-release-asset
        uses: actions/upload-release-asset@v1.0.2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ needs.create-release.outputs.RELEASE_UPLOAD_URL }}
          asset_path: ${{ format('./src-tauri/target/release/{0}/nota{1}{2}', matrix.buildFolder, matrix.ext, matrix.compressed ) }}
          asset_name: ${{ format('nota{0}{1}', matrix.ext, matrix.compressed ) }}
          asset_content_type: application/zip
      &mdash; name: build tauri app in debug mode
        run: yarn tauri:build --debug
      &mdash; name: compress (macos only)
        if: matrix.platform == 'macos-latest'
        working-directory: ${{ format('./src-tauri/target/debug/{0}', matrix.buildFolder ) }}
        run: tar -czf ${{ format('nota{0}{1}', matrix.ext, matrix.compressed ) }} ${{ format('nota{0}', matrix.ext ) }}
      &mdash; name: upload release asset with debug mode on
        id: upload-release-asset-debug-mode
        uses: actions/upload-release-asset@v1.0.2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ needs.create-release.outputs.RELEASE_UPLOAD_URL }}
          asset_path: ${{ format('./src-tauri/target/debug/{0}/nota{1}{2}', matrix.buildFolder, matrix.ext, matrix.compressed ) }}
          asset_name: ${{ format('nota-debug{0}{1}', matrix.ext, matrix.compressed ) }}
          asset_content_type: application/zip
</code></pre>
</div>

To test the workflow, commit and push your changes to your fork’s `master` branch. After successfully pushing to GitHub, you can then click on the “Actions” tab in GitHub, then click on the “Check build” link to see the progress of the workflow.

Upon successful execution of the action, you can see the draft release in “Releases” on the repository page on GitHub. You can then go on to publish your release!

## Conclusion

This article has introduced a polyglot toolchain for building secure, cross-platform, and tiny native applications. We’ve seen what Tauri is and how to incorporate it with Vue.js. Lastly, we bundled our first Tauri app by running `yarn tauri:build`, and we also used a GitHub action to create binaries for Linux, macOS, and Windows.

Let me know what you think of Tauri &mdash; I’d be excited to see what you build with it. You can [join the Discord server](https://discord.gg/SpmNs4S) if you have any questions.

*The [repository for this article](https://github.com/DominusKelvin/nota) is on GitHub. Also, see the [binaries generated by the GitHub workflow](https://github.com/DominusKelvin/nota/releases/tag/v0.1.0).*

{{< signature "ra, il, al" >}}
