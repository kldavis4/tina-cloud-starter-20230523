---
title: 'Improving The CI/CD Flow For Your Application'
slug: improving-ci-cd-flow-application
author: tom-hastjarjanto
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48cfa0d0-3a69-4e42-bc6d-3c07df736343/improving-ci-cd-flow-application.jpg
date: 2022-03-14T12:30:00.000Z
summary: >-
  Looking for ways to create a smooth CI/CD flow for your software? In this article, Tom Hastjarjanto shares a quick list of useful concepts that can be combined with GitHub Actions and NPM packages. To fully benefit from the setup and the release with maximum confidence, it is highly recommended to have a robust test suite that runs on integration.
description: >-
  Looking for ways to create a smooth CI/CD flow for your software? In this article, Tom Hastjarjanto shares some useful concepts that can be combined with GitHub Actions and NPM packages. With this setup, you will be able to release multiple times per hour with a fully documented trace managed by Git.
categories:
  - Git
  - GitHub
  - Techniques
  - Workflow
---

Big tech companies have the ability to make thousands of releases per day. Already back in 2011, Amazon released new software once every [11.6 seconds](https://www.youtube.com/watch?v=dxk8b9rSKOo). These companies typically have entire teams working on improving the delivery speed of their product teams. Luckily, many of the best practices used at these tech companies are well documented and have open-source tools available for every team to achieve the same delivery performance as big tech companies.

In this article, we will go through a few concepts which can be combined to create a modern CI/CD flow for your software. We will use GitHub Actions and NPM packages as a base, but the tools and concepts can be applied to any language. I’ve used them to successfully release Python packages and Docker containers.

## GitHub Flow

[GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow) is a lightweight branching model that is suggested by GitHub. For most companies and teams this is more than sufficient, and it’s very suitable for modularized code and microservices. Teams that have decided on [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), often do not run in the edge cases or situations for which the complete flow offers solutions (e.g. hotfixes, multiple active releases of software). 

The rules are simple:

- `main` is always releasable;
- Branch from `main` to introduce a change (new feature, bug fix, and so on);
- Once a branch is finished, create a Pull Request;
- Once the Pull request is approved, merge it to `main`;
- To create a release, simply tag `main`.

This strategy works well when your team adopts short-living branches and keeps the scope of changes small. If you choose to work on larger features and keep branches around for a longer period, you will have a hard time periodically resolving merge conflicts.

By creating releases often, you **reduce the scope of the changes**, and therefore the risk of issues after a new deployment. This will also reduce the necessity of creating hotfix releases since those can be handled in the regular development flow. Since the scope of changes for releases are small, and your pace of delivery is fast, there is often no need to have separate release branches around for any bug fixes.

## Semantic Version

Semantic versioning is a version numbering strategy to communicate the scope of the change of your new release. 

The release version is specified in the following form: `vX.Y.Z`

- `X`: this version introduces a breaking change.
- `Y`: this version introduces a new feature.
- `Z`: this version introduces a fix or other non-visible change.

By checking the version number, others can quickly estimate the impact of the new release, and decide whether they should automatically update to your new version or schedule some time to handle the breaking changes.

## Conventional Commits

[Conventional commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/) are, as the name implies, a convention on how to structure your commit messages. The pattern of this convention looks like this:

<pre><code class="language-git">&lt;type&gt;[optional scope]: &lt;description&gt;

[optional body]

[optional footer]</code></pre>

A few practical examples:

<pre><code class="language-git">chore: add GitHub actions for merge requests</code></pre>

<pre><code class="language-git">fix: handle empty post bodies</code></pre>

<pre><code class="language-git">feat: add dropdown to specify currency</code></pre>

The specification allows for some flexibility towards the types, but the most important ones are the following:

- `fix`  
This change fixes a bug.
- `feat`  
This change introduces a new feature or resolves a user story.
- `BREAKING CHANGE`  
This change introduces a breaking change and results in required actions for the users of this software.

{{% feature-panel %}}

## Standard Version

What is the point of conventional commits, you may ask. In general, using conventions allows you to build tooling and automation. That is also the case for conventional commits. For example, you can automatically generate release notes and bump your package version. [Standard Version](https://www.npmjs.com/package/standard-version) is a tool that automatically does that for you. 

The Standard version parses your Git log for the following purpose:

- Generating release notes;
- Determining the next version based on Git tags;
- Bumping your `package.json` version;
- Creating a commit that includes your release notes and `package.json` version bump;
- Tagging the commit.

To install the Standard Version, you can use NPM:

<pre><code class="language-bash">npm i -D standard-version</code></pre>

You can then add it to your `package.json` as a script:

<pre><code class="language-json">{
  "scripts": {
    "release": "standard-version"
  }
}</code></pre>

Or, alternatively, use npx:

<pre><code class="language-bash">npx standard-version</code></pre>

When you want to create a release, you can simply run `npm run release`, and Standard Version will take of the rest. Typically, you will configure your CI/CD pipeline to perform these tasks for you. 

If you want to move fast, you can set up your pipeline to **create a release every time a pull request is merged** in your codebase. In this case, you have to be cautious that your pipeline doesn’t create an infinite build loop, since the tool will commit and push changes to itself. In GitHub Actions, you can include a tag `[skip ci]` in your commit messages in order to tell GitHub to not trigger a CI build for a certain commit. You can configure a Standard version to include the `[skip ci]` tag in its configuration in `package.json`:

<pre><code class="language-json">"standard-version": {
    "releaseCommitMessageFormat": "chore(release): {{currentTag}} [skip ci]"
}</code></pre>

{{% ad-panel-leaderboard %}}

## GitHub Actions

If you use GitHub, you can use the integrated work automation feature called [GitHub Actions](https://github.com/features/actions). GitHub Actions can be used as your CI/CD service by including a YAML configuration file in a `.github/workflows` directory in the root of your repository.

For [example](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#create-an-example-workflow), you can create a file `.github/workflows/learn-github-actions.yml` with the following content:

<pre><code class="language-yml">name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
</code></pre>

GitHub Actions can be configured to allow itself to commit and push back changes to your repository. To do so, you only need to run `git config` in your workflow:

<pre><code class="language-git">- name: setup git config
run: |
    git config user.name "GitHub Actions Bot"
    git config user.email "&lt;&gt;"
- run: ...
- run: git push --follow-tags origin main</code></pre>

## Putting It All Together

Combining all of these concepts together will result in **a highly automated release flow** for your repository. The tooling configuration consists primarily of two sources:

1. `package.json`
2. `.github/workflows/<your-workflow.yml>`

This is how the `package.json` file looks like (including `[skip ci]` configuration):

<pre><code class="language-json">{
  "name": "cicd-demo",
  "version": "1.0.4",
  "description": "",
  "main": "hello-world.js",
  "scripts": {
    "release": "standard-version"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/Intellicode/cicd-demo.git"
  },
  "author": "Tom Hastjarjanto",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/Intellicode/cicd-demo/issues"
  },
  "homepage": "https://github.com/Intellicode/cicd-demo#readme",
  "dependencies": {
    "standard-version": "^9.3.2"
  },
  "standard-version": {
    "releaseCommitMessageFormat": "chore(release): {{currentTag}} [skip ci]"
  }
}</code></pre>

And this is the GitHub Actions workflow that runs on a push to `main`:

<pre><code class="language-bash">name: Release on push

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16.x]
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm run build --if-present
    - name: setup git config
      run: |
          git config user.name "GitHub Actions Bot"
          git config user.email "&lt;&gt;"
    - run: npm run release
    - run: git push --follow-tags origin main</code></pre>

This `npm run release` will do the following:

- updating `CHANGELOG.md` with new release notes since the last release;
- determining the next version based on Git tags;
- bumping your `package.json` version;
- creating a commit that includes your release notes and `package.json` version bump;
- tagging the commit.

`git push --follow-tags origin main` will finalize the release:

- It pushes the newly created tag to your repository.
- It updates `main` with the changes performed in `package.json` and `CHANGELOG.md`.

**Note**: *A full example is available in [my example repository](https://github.com/Intellicode/cicd-demo).*

{{% ad-panel-leaderboard %}}

## Conclusion

We have explored a couple of concepts that &mdash; when combined &mdash; can result in an efficient automated setup for your release procedure. With this setup, you will be able to release multiple times per hour with **a fully documented trace managed by Git**. To fully benefit from the setup and the release with maximum confidence, it is highly recommended to have a robust test suite that runs on integration.

If releasing on each merge is a step too far, you can adapt the setup to be performed manually.

### Further Reading On SmashingMag

- “[Powerful Terminal And Command-Line (CLI) Tools For Modern Web Development](https://www.smashingmagazine.com/2021/11/powerful-terminal-commandline-tools-modern-web-development/),” Louis Lazaris
- “[How To Develop An Interactive Command Line Application Using Node.js](https://www.smashingmagazine.com/2017/03/interactive-command-line-application-node-js/),” Nihar Sawant
- “[How Should Designers Learn To Code? The Terminal And Text Editors](https://www.smashingmagazine.com/2020/03/designers-code-terminal-text-editors-part-1/),” Paul Hanaoka
- “[Moving Your JavaScript Development To Bash On Windows](https://www.smashingmagazine.com/2019/09/moving-javascript-development-bash-windows/),” Burke Holland

{{< signature "vf, yk, il" >}}
