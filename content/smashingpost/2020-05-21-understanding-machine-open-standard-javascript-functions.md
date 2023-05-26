---
title: 'Understanding Machines: An Open Standard For JavaScript Functions'
slug: understanding-machines-open-standard-javascript-functions
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/351b8a00-832f-42c4-aea4-5cb9ab81f661/understanding-machines-open-standard-js-functions.png
date: 2020-05-21T10:30:00.000Z
summary: >-
  In this article, Kelvin Omereshone introduces you to machines, an open standard for JavaScript functions. At the end of this article, you should be familiar with what machines are and how to implement them.
description: >-
  In this article, Kelvin Omereshone introduces you to machines, an open standard for JavaScript functions. At the end of this article, you should be familiar with what machines are and how to implement them.
categories:
  - JavaScript
  - Frameworks
---

As developers, we always seek ways to do our job better, whether by following patterns, using well-written libraries and frameworks, or what have you. In this article, I’ll share with you a JavaScript specification for easily consumable functions. This article is intended for JavaScript developers, and you’ll learn how to write JavaScript functions with a universal API that makes it easy for those functions to be consumed. This would be particularly helpful for authoring npm packages (as we will see by the end of this article).

There is no special prerequisite for this article. If you can write a JavaScript function, then you’ll be able to follow along. With all that said, let’s dive in.

## What Are Machines?

Machines are self-documenting and predictable JavaScript functions that follow the [machine specification](https://node-machine.org/), written by Mike McNeil. A machine is characterized by the following:

- It must have one clear purpose, whether it’s to send an email, issue a [JSON Web Token](https://jwt.io/), make a fetch request, etc.
- It must follow the specification, which makes machines predictable for consumption via npm installations.

As an example, [here](https://node-machine.org/machinepack-cloudinary) is a collection of machines that provides simple and consistent APIs for working with Cloudinary. This collection exposes functions (machines) for uploading images, deleting images, and more. That’s all that machines are really: They just expose a simple and consistent API for working with JavaScript and Node.js functions.

{{% feature-panel %}}

## Features of Machines

- Machines are self-documenting. This means you can just look at a machine and knows what it’s doing and what it will run (the parameters). This feature really sold me on them. All machines are self-documenting, making them predictable. 
- Machines are quick to implement, as we will see. Using the [machinepack](https://github.com/node-machine/machinepack) tool for the command-line interface (CLI), we can quickly scaffold a machine and publish it to npm.
- Machines are easy to debug. This is also because every machine has a standardized API. We can easily debug machines because they are predictable.

## Are There Machines Out There?

You might be thinking, “If machines are so good, then why haven’t I heard about them until now?” In fact, they are already widely used. If you’ve used the Node.js MVC framework [Sails.js](https://sailsjs.com/), then you have either written a machine or interfaced with a couple. The author of Sails.js is also the author of the machine specification.

In addition to the Sails.js framework, you could browse available machines on npm by searching for machinepack, or head over to [https://node-machine.org/machinepacks](https://node-machine.org/machinepacks), which is machinepack’s registry daemon; it syncs with npm and updates every 10 minutes.

Machines are universal. As a package consumer, you will know what to expect. So, no more trying to guess the API of a particular package you’ve installed. If it’s a machine, then you can expect it to follow the same easy-to-use interface.

Now that we have a handle on what machines are, let’s look into the specification by analyzing a sample machine.

## The Machine Specification

<div class="break-out">

 <pre><code class="language-javascript">    module.exports = {
  friendlyName: 'Do something',
  description: 'Do something with the provided inputs that results in one of the exit scenarios.',
  extendedDescription: 'This optional extended description can be used to communicate caveats, technical notes, or any other sort of additional information which might be helpful for users of this machine.',
  moreInfoUrl: 'https://stripe.com/docs/api#list_cards',
  sideEffects: 'cacheable',
  sync: true,

  inputs: {
    brand: {
      friendlyName: 'Some input',
      description: 'The brand of gummy worms.',
      extendedDescription: 'The provided value will be matched against all known gummy worm brands. The match is case-insensitive, and tolerant of typos within Levenstein edit distance <= 2 (if ambiguous, prefers whichever brand comes first alphabetically).',
      moreInfoUrl: 'https://gummy-worms.org/common-brands?countries=all',
      required: true,
      example: 'haribo',
      whereToGet: {
        url: 'https://gummy-worms.org/how-to-check-your-brand',
        description: 'Look at the giant branding on the front of the package. Copy and paste with your brain.',
        extendedDescription: 'If you don\'t have a package of gummy worms handy, this probably isn\'t the machine for you. Check out the `order()` machine in this pack.'
      }
    }
  },

  exits: {
    success: {
      outputFriendlyName: 'Protein (g)',
      outputDescription: 'The grams of gelatin-based protein in a 1kg serving.',
    },
    unrecognizedFlavors: {
      description: 'Could not recognize one or more of the provided `flavorStrings`.',
      extendedDescription: 'Some **markdown**.',
      moreInfoUrl: 'https://gummyworms.com/flavors',
    }
  },

  fn: function(inputs, exits) {
    // ...
    // your code here
    var result = 'foo';
    // ...
    // ...and when you're done:
    return exits.success(result);
  };
}
</code></pre>
</div>

The snippet above is taken from the [interactive example](https://node-machine.org/spec/machine) on the official website. Let’s dissect this machine.

From looking at the snippet above, we can see that a machine is an exported object containing certain standardized properties and a single function. Let’s first see what those properties are and why they are that way.

- `friendlyName`  
This is a display name for the machine, and it follows these rules:
    - is sentence-case (like a normal sentence),
    - must not have ending punctuation,
    - must be fewer than 50 characters.
- `description`  
This should be a clear one-sentence description in the imperative mood (i.e. the authoritative voice) of what the machine does. An example would be “Issue a JSON Web Token”, rather than “Issues a JSON Web Token”. Its only constraint is:
    - It should be fewer than 80 characters.
- `extendedDescription` (optional)  
This property provides optional supplemental information, extending what was already said in the description property. In this field, you may use punctuation and complete sentences.
    - It should be fewer than 2000 characters.
- `moreInfoUrl` (optional)  
This field contains a URL in which additional information about the inner workings or functionality of the machine can be found. This is particularly helpful for machines that communicate with third-party APIs such as GitHub and Auth0.
    - Be sure to use a fully qualified URL, like https://xyz.abc/qwerty
- `sideEffects` (optional)  
This is an optional field that you can either omit or set as `cacheable` or `idempotent`. If set to `cacheable`, then `.cache()` can be used with this machine. Note that only machines that do not have `sideEffects` should be set to `cacheable`.
- `sync` (optional)  
Machines are asynchronous by default. Setting the `sync` option to `true` turns off async for that machine, and you can then use it as a regular function (without `async`/`await`, or `then()`).

### inputs

This is the specification or declaration of the values that the machine function expects. Let’s look at the different fields of a machine’s input.

- `brand`  
Using the machine snippet above as our guide, the brand field is called the input key. It is normally camel-cased, and it must be an alphanumeric string starting with a lowercase letter.
    - No special characters are allowed in an input key identifier or field.
- `friendlyName`  
This is a human-readable display name for the input. It should:
    - be sentence-case,
    - have no ending punctuation,
    - be fewer than 50 characters.
- `description`  
This is a short description describing the input’s use.
- `extendedDescription`  
Just like the `extendedDescription` field on the machine itself, this field provides supplemental information about this particular input.
- `moreInfoUrl`  
This is an optional URL that provides more information about the input, if needed.
- `required`  
By default, every input is optional. What that means is that if, by runtime, no value is provided for an input, then the `fn` would be undefined. If your inputs are not optional, then it’s best to set this field as true because this would make the machine throw an error.
- `example`  
This field is used to determined the expected data type of the input.
- `whereToGet`  
This is an optional documentation object that provides additional information on how to locate adequate values for this input. This is particularly useful for things like API keys, tokens, and so on.
- `whereToGet.description`  
This is a clear one-sentence description, also in the imperative mood, that describes how to find the right value for this input.
- `extendedDescription`  
This provides additional information on where to get a suitable input value for this machine.

### exits

This is the specification for all possible exit callbacks that this machine’s `fn` implementation can trigger. This implies that each exit represents one possible outcome of the machine’s execution.

- `success`  
This is the standardized exit key in the machine specification that signifies that everything went well and the machine worked without any errors. Let’s look at the properties it could expose:
    - `outputFriendlyName`  
This is simply a display name for the exit output.
    - `outputDescription`  
This short noun phrase describes the output of an exit.

Other exits signify that something went wrong and that the machine encountered an error. The naming convention for such exits should follow the naming convention for the input’s key. Let’s see the fields under such exits:

- `description`  
This is a short description describing when the exit would be called.
- `extendedDescription`  
This provides additional information about when this exit would be called. It’s optional. You may use full Markdown syntax in this field, and as usual, it should be fewer than 2000 characters.

## You Made It!

That was a lot to take in. But don't worry: When you start authoring machines, these conventions will stick, especially after your first machine, which we will write together shortly. But first…

## Machinepacks

When authoring machines, machinepacks are what you publish on npm. They are simply **sets of related utilities for performing common, repetitive development tasks with Node.js**. So let’s say you have a machinepack that works with arrays; it would be a bundle of machines that works on arrays, like `concat()`, `map()`, etc. See the [Arrays machinepack](https://node-machine.org/machinepack-arrays) in the registry to get a full view.

## Machinepacks Naming Convention

All machinepacks must follow the standard of having “machinepack-” as a prefix, followed by the name of the machine. For example, machinepack-array, machinepack-sessionauth.

## Our First Machinepack

To better understand machines, we will write and publish a machinepack that is a wrapper for the [file-contributors](https://www.npmjs.com/package/file-contributors) npm package.

{{% ad-panel-leaderboard %}}

## Getting Started

We require the following to craft our machinepack: 

<ol>
  <li><strong>Machinepack CLI tool</strong><br />You can get it by running:<br />

<pre><code class="language-bash">npm install -g machinepack
</code></pre>
</li>
<li><strong><a href="https://yeoman.io/">Yeoman scaffolding tool</a></strong><br />Install it globally by running:<br />

<pre><code class="language-bash"> npm install -g yo
</code></pre>
</li>
<li><strong>Machinepack Yeomen generator</strong><br />Install it like so:<br />

<pre><code class="language-bash">npm install -g generator-machinepack
</code></pre>
</li>
</ol>

**Note**: *I am assuming that Node.js and npm are already installed on your machine.*

## Generating Your First Machinepack

Using the CLI tools that we installed above, let’s generate a new machinepack using the machinepack generator. Do this by first going into the directory that you want the generator to generate the files in, and then run the following:

<pre><code class="language-bash">yo machinepack
</code></pre>

The command above will start an interactive process of generating a barebones machinepack for you. It will ask you a couple of questions; be sure to say yes to it creating an example machine.

**Note:** *I noticed that the Yeoman generator has some issues when using Node.js 12 or 13. So, I recommend using [nvm](https://github.com/nvm-sh/nvm), and install Node.js 10.x, which is the environment that worked for me.*

If everything has gone as planned, then we would have generated the base layer of our machinepack. Let’s take a peek:

<pre><code class="language-bash">DELETE_THIS_FILE.md
machines/
package.json
package.lock.json
README.md
index.js
node_modules/
</code></pre>

The above are the files generated for you. Let’s play with our example machine, found inside the `machines` directory. Because we have the machinepack CLI tool installed, we could run the following:

<pre><code class="language-bash">machinepack ls
</code></pre>

This would list the available machines in our `machines` directory. Currently, there is one, the say-hello machine. Let’s find out what say-hello does by running this:

<pre><code class="language-bash">machinepack exec say-hello
</code></pre>

This will prompt you for a name to enter, and it will print the output of the say-hello machine.

As you’ll notice, the CLI tool is leveraging the standardization of machines to get the machine’s description and functionality. Pretty neat!

{{% ad-panel-leaderboard %}}

## Let’s Make A Machine

Let’s add our own machine, which will wrap the file-contributors and node-fetch packages (we will also need to install those with npm). So, run this:

<pre><code class="language-bash">npm install file-contributors node-fetch --save
</code></pre>

Then, add a new machine by running:

<pre><code class="language-bash">machinepack add
</code></pre>

You will be prompted to fill in the friendly name, the description (optional), and the extended description (also optional) for the machine. After that, you will have successfully generated your machine.

Now, let’s flesh out the functionality of this machine. Open the new machine that you generated in your editor. Then, require the file-contributors package, like so:

<div class="break-out">

 <pre><code class="language-javascript">const fetch = require('node-fetch');
const getFileContributors = require('file-contributors').default;

global.fetch = fetch; // workaround since file-contributors uses windows.fetch() internally
</code></pre>
</div>

**Note:** *We are using node-fetch package and the `global.fetch = fetch` workaround because the file-contributors package uses `windows.fetch()` internally, which is not available in Node.js.*

The file-contributors’ `getFileContributors` requires three parameters to work: `owner` (the owner of the repository), `repo` (the repository), and `path` (the path to the file). So, if you’ve been following along, then you’ll know that these would go in our `inputs` key. Let’s add these now:

<pre><code class="language-javascript">...
 inputs: {
    owner: {
      friendlyName: 'Owner',
      description: 'The owner of the repository',
      required: true,
      example: 'DominusKelvin'
    },
    repo: {
      friendlyName: 'Repository',
      description: 'The Github repository',
      required: true,
      example: 'machinepack-filecontributors'
    },
    path: {
      friendlyName: 'Path',
      description: 'The relative path to the file',
      required: true,
      example: 'README.md'
    }
  },
...
</code></pre>

Now, let’s add the exits. Originally, the CLI added a `success` exit for us. We would modify this and then add another exit in case things don’t go as planned.

<div class="break-out">

 <pre><code class="language-javascript">exits: {

    success: {
      outputFriendlyName: 'File Contributors',
      outputDescription: 'An array of the contributors on a particular file',
      variableName: 'fileContributors',
      description: 'Done.',
    },

    error: {
      description: 'An error occurred trying to get file contributors'
    }

  },
</code></pre>
</div>

Finally let's craft the meat of the machine, which is the `fn`:

<div class="break-out">

 <pre><code class="language-javascript"> fn: function(inputs, exits) {
    const contributors = getFileContributors(inputs.owner, inputs.repo, inputs.path)
    .then(contributors => {
      return exits.success(contributors)
    }).catch((error) => {
      return exits.error(error)
    })
  },
</code></pre>
</div>

And voilà! We have crafted our first machine. Let’s try it out using the CLI by running the following:

<pre><code class="language-bash">machinepack exec get-file-contributors
</code></pre>

A prompt would appear asking for `owner`, `repo`, and `path`, successively. If everything has gone as planned, then our machine will exit with success, and we will see an array of the contributors for the repository file we’ve specified.

### Usage In Code

I know we won’t be using the CLI for consuming the machinepack in our code base. So, below is a snippet of how we’d consume machines from a machinepack:

<pre><code class="language-javascript">    var FileContributors = require('machinepack-filecontributors');

// Fetch metadata about a repository on GitHub.
FileContributors.getFileContributors({
  owner: 'DominusKelvin',
  repo: 'vue-cli-plugin-chakra-ui',
   path: 'README.md' 
}).exec({
  // An unexpected error occurred.
  error: function (){
  },
  // OK.
  success: function (contributors){
    console.log('Got:\n', contributors);
  },
});
</code></pre>

### Conclusion

Congratulations! You’ve just become familiar with the machine specification, created your own machine, and seen how to consume machines. I’ll be glad to see the machines you create.

### Resources

- “[Getting Started](https://node-machine.org/implementing/Getting-Started)”, node machine
- [file contributors](https://www.npmjs.com/package/file-contributors), npm

*Check out the [repository](https://github.com/DominusKelvin/machinepack-filecontributors) for this article. The npm package we created is also [available on npm](https://www.npmjs.com/package/machinepack-filecontributors).*

{{< signature "ra, il, al" >}}
