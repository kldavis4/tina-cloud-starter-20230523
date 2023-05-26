---
title: 'How To Automate Documentation Workflow For Developers'
slug: automate-documentation-workflow-for-developers
author: portia-burton
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68266575-8f47-415b-9c91-7004a02944ee/action-github-1.png
date: 2021-08-24T13:00:00.000Z
summary: >-
  In this article, you’ll learn how to save hours of tedious work of writing, updating, and correcting technical documentation. In this article, you will learn how to automate your documentation workflow with Vale and GitHub Actions.
description: >-
  In this article, you’ll learn how to save hours of tedious work of writing, updating, and correcting technical documentation. In this article, you will learn how to automate your documentation workflow with Vale and GitHub Actions.
categories:
  - Workflow
  - Tools
  - Techniques
---

To get the most out of this tutorial, you should be familiar with: [Git](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/), [GitHub](https://docs.github.com/en/get-started/quickstart/github-flow) and [Linux and the command line](https://www.smashingmagazine.com/2012/01/introduction-to-linux-commands/).

## Why Should You Care About High-Quality Documentation?

Many teams struggle with **writing documentation**. When you go to check a framework, the documentation will often be out of date or unclear. This can lead to internal frustration when a team member tries to add a feature, but they don’t understand how the current feature works because of poor documentation. This can lead to unproductive hours on the job.

Poor documentation also compromises a good customer experience. According to Jeff Lawson, author of *Ask Your Developer* and founder of Twilio, if you are selling an API as a product, documentation is the **ultimate advertisement for technical stakeholders**. IBM did a study on the importance of documentation, and 90% of respondents admitted that they made their purchasing decisions based on the quality of a product’s documentation.

Writing good documentation is important for the developer and customer experiences.

## If Documentation Is So Important, Then Why Do Engineering Teams Deprioritize It?

Writing documentation can break developers out of the “flow”. Documentation **often lives outside of the main code base**, and it is cumbersome to find and update. Putting it in an Excel spreadsheet or a proprietary CMS is not uncommon.

Automating documentation and improving documentation workflow fixes this.

## Automating Documentation From a High Level

What does *automating* documentation mean? It means adopting common software development practices. When you automate documentation, you are:

- writing your documentation in Markdown;
- using a continuous integration and continuous deployment (CI/CD) pipeline to run tasks such as correcting errors and deploying updates (in this tutorial, we are going to highlight GitHub Actions);
- implementing tools like Vale to enforce a style guide and to correct common grammatical mistakes.

## The Style Guides

Before you use tools such as [Vale](https://docs.errata.ai/vale/about) and GitHub Actions to automate the style guide, let’s take a moment to define what exactly is a style guide.

You know that feeling when you are writing documentation and something seems a little off? Your explanations don’t fit the rest of the documentation, but you can’t quite describe why they’re wrong. The writing explains the concept, but it doesn’t seem to fit.

When you get this feeling, your **voice and tone might be off**. Refining the voice and tone is a way to make writing sound cohesive even if you are developing documentation that has been edited by the QA, engineering, and product teams. Below is an example style guide from the city bus application TAPP, taken from the book [*Strategic Writing for UX*](https://www.oreilly.com/library/view/strategic-writing-for/9781492049388/) by Torrey Podmajersky.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba6be772-ef8f-41dc-a824-96d01ea7c68b/image-000.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba6be772-ef8f-41dc-a824-96d01ea7c68b/image-000.png" width="800" height="456" sizes="100vw" caption="An example style guide from the city bus application TAPP, taken from the book Strategic Writing for UX. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba6be772-ef8f-41dc-a824-96d01ea7c68b/image-000.png'>Large preview</a>)" alt="An example style guide from the city bus application TAPP, taken from the book Strategic Writing for UX" >}}

TAPP is a transit application (for buses and trains). The header of the table announces TAPP’s values as a company, being efficient, trustworthy, and accessible. The left side of the table lists the different parts covered by the style guide: concepts, vocabulary, verbosity, grammar, and punctuation.

Together, these make a **style guide**. The header introduces the values, and the left side of the table shows the different components that you would find in any written material: vocabulary, grammar, and punctuation. The beauty of this style guide is that engineers and copywriters will clearly know what capitalization to use and which punctuation to use in order to promote Tapp’s brand identity.

{{% feature-panel %}}

### Technical Writing Style Guide

Not all style guides come in tables. Microsoft has a [whole website](https://docs.microsoft.com/en-us/style-guide/welcome/) that serves as a comprehensive guide, covering everything from acronyms to bias-free communication to chatbots. Microsoft of course isn’t the only company that has a style guide. [Google has one](https://developers.google.com/style), too.

### The Trouble With Style Guides

Style guides are a great starting point for companies that are serious about documentation. They solve a lot of the confusion that developers might have about how exactly to write about a major feature that they are pushing out.

The problem with style guides is that they add friction to the writing process. Many writers, including me, don’t bother to stop writing and look at the style guide every time they have a question. Sometimes, a style guide is cumbersome and too difficult to reference &mdash; for instance, the [Microsoft Style Guide](https://opdhsblobprod03-secondary.blob.core.windows.net/contents/1b0c5ed94a6a4332b3ded83a8000ec2c/6ca9ae2be2407c744532364a00b292ab?sv=2018-03-28&sr=b&si=ReadPolicy&sig=6sDQt45S3L%2B0BUtizPO83H4uZX7wxbhfVPv3Ea4IyBY%3D&st=2021-07-28T15%3A05%3A16Z&se=2021-07-29T15%3A15%3A16Z) is over a thousand pages long!

## Linters and CI/CD for Documentation

If you are a programmer, then you are probably familiar with linters. Linters are an ideal way to **enforce coding standards** on your team. The same is true with documentation. When you create a linter, you are setting a benchmark of quality for your documentation. In this tutorial, we are going to use the [Vale linter](https://docs.errata.ai/vale/about).

Using some sort of documentation automation alongside a linter is common. When we say automation in this context, we’re referring to the [continuous integration and continuous deployment](https://www.freecodecamp.org/news/the-real-difference-between-ci-and-cd/) (CI/CD) workflow. CI automates the **building and testing of documentation**. CD automates the release of code.

You can use many different types of apps to implement a CI/CD workflow. In this tutorial, we are going to use GitHub Actions to run our documentation linter. GitHub Actions run CI directly in a GitHub repository, so there is no need to use a third-party application, such as CircleCI or Travis.

Finally, GitHub Actions are *event-driven*, which means they are triggered when something happens, such as when someone writes a pull request or an issue. In our example, a GitHub action will occur when someone pushes changes to their main branch.

## GitHub Actions

First, create a [GitHub repository](https://docs.github.com/en/get-started/quickstart/create-a-repo). Then, locally, create a folder and `cd` into it.

<pre><code class="language-bash">mkdir automated-docs
cd automated-docs</code></pre>

Once you are in the folder, initialize the directory for Git.

<pre><code class="language-bash">git init</code></pre>

Once you have initialized the repository, proceed to create a workflow directory to your folder.

<pre><code class="language-bash">mkdir .github/ && cd .github/ && mkdir workflows/ && cd workflows/</code></pre>

Workflows are where we will store all of our GitHub actions. Once you’ve created a `workflows` folder, make a new workflow. We are going to name this workflow `vale.yml`.

<pre><code class="language-bash">touch vale.yml</code></pre>

`Vale.yml` is a YAML file. In this workflow file, we will include actions and jobs.

Now, open `vale.yml` in your favorite text editor.

<pre><code class="language-bash">nano vale.yml</code></pre>

Copy and paste the following into `vale.yml`, and let’s go over the context and syntax.

<pre><code class="language-yaml"># This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      # Runs a single command using the runners shell
      - name: Run a one-line script
        run: echo Hello, world!

      # Runs a set of commands using the runners shell
      - name: Run a multi-line script
        run: |
          echo Add other actions to build,
          echo test, and deploy your project.
        env:
          GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}</code></pre>

- `name`  
This is the name, or what we are calling our workflow. It is a string.
- `on`  
This controls the workflow and the triggers.
- `jobs`  
This is where we set up and control our actions. We select the environment where our actions will run &mdash; it is usually a good bet to go with Ubuntu. And this is where we will add our actions.

GitHub has a guide on all of the other workflow [syntax and variables](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions), in case you’re curious.

In this section, we have:

- learned what GitHub actions are,
- created our first GitHub workflow,
- identified the most important parts of a GitHub workflow YAML file.

Next, we are going to customize our GitHub workflow to use Vale.

{{% ad-panel-leaderboard %}}

## Set Up Vale in GitHub Actions File

Once we’ve copied the base workflow file, it is time to customize it, so that we can start using Vale actions. The first thing to do is change the name of the YAML file to `Docs-Linting`.

<pre><code class="language-bash"># This is a basic workflow to help you get started with Actions.

name: Docs-Linting</code></pre>

Next, we want to run the Vale test once someone **has pushed their changes** to the main branch on GitHub. We don’t want the test to run when someone creates a pull request, so we’ll delete that part of the YAML file.

<pre><code class="language-bash">on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
</code></pre>

The `jobs` section is the main part of the workflow file, and it is responsible for running the GitHub actions.

<pre><code class="language-bash">jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@master</code></pre>

These actions are going to run on the latest version of Ubuntu. The `Checkout` action checks out the repository in order for the [GitHub workflow to access it](https://github.com/marketplace/actions/checkout).

Now it is time to add a Vale action to our GitHub workflow.

<pre><code class="language-bash">  - name: Vale
      uses: errata-ai/vale-action@v1.4.2
      with:
        debug: true
        styles: |
          https://github.com/errata-ai/write-good/releases/latest/download/write-good.zip
          https://github.com/errata-ai/Microsoft/releases/latest/download/Microsoft.zip

      env:
        GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}</code></pre>

We have named our action `Vale`. The `uses` variable shows which version of Vale we’re going to implement &mdash; ideally, we should use the most recent version. In the `with` variable, we set `debug` to `true`.

The `styles` section gives us the option to add a style guide to Vale. In this example, we are going to use `write-good` and Microsoft’s official style guide. Keep in mind that we can use [other style guides](https://github.com/errata-ai/styles#available-styles) as well.

The final part of this GitHub action is `env`. In order to run this GitHub action, we need to include a [secret token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token).

This is what the result should look like:

<pre><code class="language-bash"># This is a basic workflow to help you get started with Actions.

name: Docs-Linting

# Controls when the action will run.
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  prose:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@master

    - name: Vale
      uses: errata-ai/vale-action@v1.4.2
      with:
        debug: true
        styles: |
          https://github.com/errata-ai/write-good/releases/latest/download/write-good.zip
          https://github.com/errata-ai/Microsoft/releases/latest/download/Microsoft.zip

      env:
        GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}</code></pre>

Once you’ve finished making changes, save the file, commit to Git, and push your changes to GitHub.

<pre><code class="language-bash">git add .github/workflows/vale.yml
git commit -m "Added github repo to project"
git push -u origin main</code></pre>

To recap, in this section, we have:

- triggered the action to occur when we push new code to the `main` branch;
- added a Vale action, setting `debug` to `true` and identifying style guides;
- added a GitHub token;
- committed changes and pushed to GitHub.

In the next section, we are going to create a Vale configuration file.

{{% ad-panel-leaderboard %}}

## Setting Up Vale Configuration File

Go to the root of your project’s directory, and then `touch .vale.ini`. Open `.vale.ini` in a text editor. Copy and paste the following into `.vale.ini`:

<pre><code class="language-bash">StylesPath = .github/styles
MinAlertLevel = warning

[formats]
Markdown = markdown

[*.md]
BasedOnStyles = write-good, Microsoft</code></pre>

- `StylesPath = .github/styles`  
The `StylesPath` gives the path of the Vale styles.
- `MinAlertLevel = warning`  
The minimum alert level shows the scale of severity in alerts. The options are `suggestion`, `warning`, and `error`.
- `[formats]`  
`Markdown = markdown` sets the format as Markdown.
- `[*.md]`  
The configuration `BasedOnStyles = write-good, Microsoft` will run write-good and the Microsoft style guide on all Markdown files ending with `.md`.

This set-up is the bare minimum. If you are interested in learning more about configuring Vale, head over to [the documentation](https://errata-ai.github.io/vale-server/docs/ini).

When you are finished making changes, save the file, and commit and push to GitHub.

<pre><code class="language-bash">git add .vale.ini
git commit -m "Added Vale config file"
git push -u origin main</code></pre>

In this part, we’ve learned the internals of a Vale configuration file. Now it’s time to create sample documentation.

## Creating Documentation and Triggering the Vale GitHub Actions

Now it is time to see Vale and GitHub Actions in action! We are going to create a Markdown file and fill it with text. And we are going to get our text from [DeLorean Ipsum](https://satoristudio.net/delorean-ipsum/).

Go to the root of your project, and then `touch getting-started.md`. Once you’ve created the `getting-started` file, go to DeLorean Ipsum and create some dummy text for your documentation. Then, return to your text editor and paste the text in `getting-started-md`.

<pre><code class="language-bash"># Getting Started Guide

I can’t play. It’s my dad. They’re late. My experiment worked. They’re all exactly twenty-five minutes slow. Marty, this may seem a little foreward, but I was wondering if you would ask me to the Enchantment Under The Sea Dance on Saturday. Well, they’re your parents, you must know them. What are their common interests, what do they like to do together?

Okay. Are you okay? Whoa, wait, Doc. What, well you mean like a date? I don’t wanna see you in here again.

No, Biff, you leave her alone. Jesus, George, it’s a wonder I was ever born. Hey, hey, keep rolling, keep rolling there. No, no, no, no, this sucker’s electrical. But I need a nuclear reaction to generate the one point twenty-one gigawatts of electricity that I need. I swiped it from the old lady’s liquor cabinet. You know Marty, you look so familiar, do I know your mother?</code></pre>

Save the file, commit it, and push it to GitHub.

<pre><code class="language-bash">git add getting-started.md
git commit -m "first draft"
git push -u origin main</code></pre>

Once you’ve pushed the changes, head over to GitHub where your repository is located. Go to the `Actions` tab.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc46db45-3e5a-4434-9292-18818d52de8c/2-automate-documentation-workflow-for-developers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68266575-8f47-415b-9c91-7004a02944ee/action-github-1.png" width="800" height="278" sizes="100vw" caption="Locate Actions in the GitHub’s tab bar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68266575-8f47-415b-9c91-7004a02944ee/action-github-1.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

You will see all of your workflows on the left side. We have only one, named `Docs-Linting`, the same name we put in the `vale.yml` file.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856ea8-673a-45ac-aa5b-41c85dca993b/3-automate-documentation-workflow-for-developers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856ea8-673a-45ac-aa5b-41c85dca993b/3-automate-documentation-workflow-for-developers.png" width="800" height="325" sizes="100vw" caption="All workflows are located on the left side. That’s also where your documentation workflow will live. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856ea8-673a-45ac-aa5b-41c85dca993b/3-automate-documentation-workflow-for-developers.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

When we push the documentation to GitHub, we will trigger the action.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f83a888-de1c-4ebd-bad1-82ae70e01768/4-automate-documentation-workflow-for-developers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f83a888-de1c-4ebd-bad1-82ae70e01768/4-automate-documentation-workflow-for-developers.png" width="800" height="157" sizes="100vw" caption="With every push of the documentation to GitHub, we will trigger the action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f83a888-de1c-4ebd-bad1-82ae70e01768/4-automate-documentation-workflow-for-developers.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

If the action has run without any problems, we will get a green checkmark.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbfcbebe-ba94-43d8-8022-b6b489bc0581/5-automate-documentation-workflow-for-developers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbfcbebe-ba94-43d8-8022-b6b489bc0581/5-automate-documentation-workflow-for-developers.png" width="800" height="" sizes="100vw" caption="If everything works as expected, you should see a green checkmark appearing next to the workflow. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbfcbebe-ba94-43d8-8022-b6b489bc0581/5-automate-documentation-workflow-for-developers.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

Click on “Added docs” to get a full report.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a21c8644-a3a1-4aae-a4fe-25fb11a4ed15/weasel-word-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a21c8644-a3a1-4aae-a4fe-25fb11a4ed15/weasel-word-1.png" width="800" height="494" sizes="80vw" caption="Annotations provide insights around things that might need to be adjusted. Take a closer look at the weasel word warning from write-good. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a21c8644-a3a1-4aae-a4fe-25fb11a4ed15/weasel-word-1.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

You will see that we got 11 warnings. Let’s deal with the “[weasel word](https://www.merriam-webster.com/dictionary/weasel%20word)” warning. Go back to the text editor, open `getting-started.md`, and delete the word “exactly”.

<pre><code class="language-markup"># Getting Started Guide

I can’t play. It’s my dad. They’re late. My experiment worked. They’re all twenty-five minutes slow. Marty, this may seem a little foreward, but I was wondering if you would ask me to the Enchantment Under The Sea Dance on Saturday. Well, they’re your parents, you must know them. What are their common interests, what do they like to do together?

Okay. Are you okay? Whoa, wait, Doc. What, well you mean like a date? I don’t wanna see you in here again.

No, Biff, you leave her alone. Jesus, George, it’s a wonder I was ever born. Hey, hey, keep rolling, keep rolling there. No, no, no, no, this sucker’s electrical. But I need a nuclear reaction to generate the one point twenty-one gigawatts of electricity that I need. I swiped it from the old lady’s liquor cabinet. You know Marty, you look so familiar, do I know your mother?</code></pre>

Save the changes, commit it to Git, and push the new version of the file to GitHub. It should **trigger the GitHub action**.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/657f3547-d7a3-4642-b846-6e90fa9d217b/7-automate-documentation-workflow-for-developers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/657f3547-d7a3-4642-b846-6e90fa9d217b/7-automate-documentation-workflow-for-developers.png" width="800" height="204" sizes="100vw" caption="Another workflow run in GitHub. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/657f3547-d7a3-4642-b846-6e90fa9d217b/7-automate-documentation-workflow-for-developers.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

If we click on “Deleted the weasel word”, we will see that we have only 10 warnings now, and the “weasel word” warning is gone. Hooray!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/337c2c6f-8195-42cb-b0c1-ff09b6eaded3/annotations-10-warnings-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/337c2c6f-8195-42cb-b0c1-ff09b6eaded3/annotations-10-warnings-1.png" width="800" height="448" sizes="80vw" caption="One error fixed, 10 more to go. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/337c2c6f-8195-42cb-b0c1-ff09b6eaded3/annotations-10-warnings-1.png'>Large preview</a>)" alt="Screenshot of GitHub website" >}}

We are finished, and we’ve covered a lot of ground. In this section, we have:

- added documentation to our Vale GitHub Actions repository,
- triggered the Vale GitHub action,
- corrected an error produced by Vale and pushed the change back to GitHub.

## Conclusion

In a world that is increasingly going remote, prioritizing **good documentation** and good documentation workflow is important. You first have to define what “good” is by creating a style guide. Once you’ve figured out the rules of your documentation, then it’s time to automate.

Documentation should be treated like your code base: a living body of work that is constantly being iterated and becoming a bit better than the last time you updated it.

{{< signature "yk, al" >}}
