---
title: 'Testing The CLI The Way People Use It'
slug: testing-cli-way-people-use-it
author: georgy-marchuk
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6d3ba7a-2c86-4e64-b8e8-6d58adaafdba/testing-cli-way-people-use-it.jpg
date: 2022-04-22T09:30:00.000Z
summary: >-
  Have you ever wondered, why do people write CLI tools? When is a good time to think about yours? Today we’ll touch on these questions, along with some tips to remember when creating one. However, all of this serves as a prelude to the real topic: end-to-end testing of CLI tools.
description: >-
  Have you ever wondered, why do people write CLI tools? When is a good time to think about yours? Today we’ll touch on these questions, along with some tips to remember when creating one. However, all of this serves as a prelude to the real topic: end-to-end testing of CLI tools.
categories:
  - Apps
  - Tools
  - Coding
  - Testing
---

Thousands of tools for the command-line interface (CLI) are out there, without exaggeration. They serve all kinds of purposes. Yarn is one of the most used CLIs in the world, bringing ease to the package management of millions of projects. Others are narrower in scope, serving as a way to communicate with a particular tool such as Webpack (`webpack-cli`) or TypeScript (`tsc`).

Every CLI serves its purpose, but they all have one thing in common: the *interface* part of the name. While it might seem odd or mystifying to the less technical people out there, it is one of the most common ways in which people communicate with and control programs. It’s especially odd when we remember that it’s the oldest way that people have interacted with a computer that didn’t involve plastic punch cards or uploading a program into the computer through some other means.

While people have come up with all kinds of ways to test web and other applications, CLI tools have been overlooked in this area for the most part. Today, we’ll touch on end-to-end testing of these tools, go through patterns to follow, and introduce a library to solve some of the issues we encounter along the way.

## CLI Tools And Why You Need One

Before digging in, we should talk about creating a CLI tool in the first place. After all, to test a CLI, we would usually need to create one first. Forget for a moment about all of the tools used by millions of people, and focus instead on the use case of creating your own CLI. A couple of questions would need to be answered: Why would you do that, and how would you do that?

I spend most of my work-time at Pipedrive, a healthy-paced growing company with a little under a thousand employees as of the time of writing. Putting this into perspective is important.

Even a single person or a small team can suffer tremendously from a suboptimal repetitive process. Losing an hour a day is tremendously wasteful and often leads people to hating the task and everything connected to it. However, what makes the problem worse is scale. The more a task is repeated or the higher the number of people repeating the task, the bigger the problem becomes.

With a thousand people and several hundreds of engineers involved, any repetitive task could grow into ridiculous proportions. It would leak development resources, always a scarce commodity, no matter the position of your company.

That’s one of the main problems Pipedrive has been focusing on a lot lately, having grown to the decent size it is. We’ve been optimizing reusable things, cutting out repetitive work, and ideally getting rid of the need to reinvent the wheel between teams altogether.

That’s where the CLIs come in. It’s a powerful tool for optimizing repetitive work: It’s cheap to create, and it can access or run pretty much anything you need, from reading and writing to the file system to directly accessing remote databases. Your imagination truly is the limit. I’ve been involved in creating several CLI tools in the past year or two, but not only in this time period, nor the biggest of them at Pipedrive.

I’ve worked on my own open-source CLI tool in the past. The tool might not be the most used, but it does save a lot of time by testing the implementation of the [Swup library](https://swup.js.org/) on a website, which is an incredibly time-consuming task when done manually. The point is that **you don’t have to be a thousand-person company to benefit** from your own CLI tool.

## Designing The CLI For Testing

Now that we’ve established why one would need an own CLI tool, let’s get into the *how*. Plenty of guides exist around the internet on how to build your own CLI. That’s mainly the reason why we’ll skip this topic altogether. Instead, let’s focus on something more specific: designing the CLI so that it can be easily tested.

Ideally, each part of the CLI would be a standalone task that you can run and evaluate without running the CLI program. Most libraries, or templates of the sort, that are meant for building CLIs are designed that way already. That might be a conscious design of the creators, but it might just be an accidental byproduct of the purpose of the CLI in running specific, often small tasks.

Enough talking. Let’s throw some code examples into the mix. One of the most popular libraries, if not the most, for building CLI tools is [Commander](https://github.com/tj/commander.js). It’s also one of the simplest tools, meaning that it doesn’t add much abstraction on top, and it mainly simplifies the definition and reading of possible options. A contrived example of a CLI would look something like the following:

<pre><code class="language-javascript">const { Command } = require('commander');
const program = new Command();

const print = (string) =&gt; {
  console.log(string);
}
    
program
  .name('my-cli')
  .description('CLI to show off some cool stuff')
  .version('1.0.0');
    
program.command('print')
  .description('Print a string')
  .argument('&lt;string&gt;', 'string to print')
  .action(print);
    
program.parse();</code></pre>

The example nicely shows how Commander simplifies the management of what the CLI should run at all. For us, the important thing to notice is the line containing the definition of the action called for the print `print` command &mdash; in other words, the function called when the CLI is executed by running `my-cli print hello!`.

This is important because the actual handler of this command is a standalone function &mdash; that is, a function that can be imported, executed, mocked, or anything in between, without touching any other part of the program. In fact, this particular handler is something we could call a pure function, because it doesn’t have any side effects and it always returns the same output for the same input. However, even for non-pure functions, any side effects that could touch the file system, an external API, or whatnot can be mocked, making the testing powerful and replicable for more complex functions, too.

## Make It About The User

We went through how separate parts of a CLI can be tested. Now let’s consider a different approach. Just as unit tests are usually accompanied by other more complex tests for your typical apps, the same approach and arguments can be used for the CLI. While testing separate parts of a program is always advisable, bringing automated tests much closer to the user’s use cases does have its charm.

It is not-so-coincidentally the same philosophy is followed by the [Testing Library](https://testing-library.com/). It brings the flows that we use for testing a step closer to the way the code is used by its users. Thanks to this popular library, many people are so used to the idea that it might even seem obvious, although the same pattern with CLIs is not that common.

<blockquote>The more your tests resemble the way your software is used, the more confidence they can give you.</blockquote>

That’s a short but representative line from Testing Library’s documentation. Let’s unpack this idea. There are simply so many moving pieces in even the smallest programs. Every piece has the potential to break. These moving pieces could be anything. Let’s consider external dependencies as an example. They are usually trusted to follow semantic versioning, but there is always room for mistakes and accidental breaking by maintainers. This probability is significantly higher these days considering that a typical JavaScript project has hundreds of dependencies. These dependencies are not tested in our tests, and they are often mocked up altogether when unit testing.

The same applies to code that might be partially untested or to a scenario that just wasn’t considered.

That’s a technical perspective, but an even better description would be more fundamental. I, as developer of the program, don’t care whether some subpart gets called once or twice or that the values are different. My main concern is the business logic &mdash; that the program does for the user what I intend it to do.

If the program is supposed to create a file on disk, then that’s what we need to make sure works as expected. If the program does some other operation based on user input, then &mdash; you guessed it &mdash; that is what we need to make sure works.

In a sense, it’s a shift away from programming logic altogether, moving closer to the business use cases, because those are what matter at the end of the day.

## From Idea To Implementation

As is usual with projects, now that we’ve established our reasoning, we can move to the practical part of the implementation. The goal is clear by now: allow testing of a CLI tool, resembling the way users use it as closely as possible.

In this section, let’s focus on the most interesting part of the task, which is how we would like the tests to look like. We’ll skip the implementation of the API for the most part, because that consists of technical problems that we can solve anytime.

Conveniently, all of the below-mentioned functionality is provided by a library that we’ve put together for today’s purpose. It’s named [CLI Testing Library](https://github.com/gmrchk/cli-testing-library), which is not exactly creative, but given the similarities in philosophy to Testing Library, it aptly describes what it provides. The library is certainly in the early stages, but it’s been used to test code in production so far without issues. As mentioned, the implementation is not something we will dig into, but it can be reviewed [on GitHub](https://github.com/gmrchk/cli-testing-library/tree/master/src), and it is a fairly small code base.

### Basic Execution

Thanks to the nature of the program we are testing, it’s quite simple to assume what we would like to do in the test: run a shell command that would run the program in a separate process, just as the CLI would be executed by the user in the terminal. For a moment, we can assume that the program is simple and does not require any further input from the user other than the initial options. Considering all of that, we can imagine that the ideal API might look something like this:

<pre><code class="language-javascript">await execute('node my-cli.js my-first-command');</code></pre>

This looks sufficient for the basic use of executing a program and waiting for it to finish. The most obvious thing we would like to know is whether the program has finished successfully. CLI tools use exit codes for that, whereby the general convention is that anything above 0 represents an unsuccessful run of some sort. It’s similar to HTTP codes, with 200 being the equivalent of ultimate success. Such a code could definitely be captured and returned from our API execution, to later be compared:

<pre><code class="language-javascript">const { exitCode } = await execute('node my-cli.js my-first-command');</code></pre>

That will surely do for a convenient basic API to run an end-to-end CLI test. Before moving on to the other points, let’s spice it up a little with some additional useful information, like the `stdout` and `stderr` of the program. In case you’re not familiar with these terms, they’re outputs you’d see in the console as a user, and these differ only in the purpose of the outputted text: default or error.

It would certainly be helpful to check whether the program printed what it was meant to, having finished successfully. Perhaps that’s what our program was meant to do after all, just print something. A simple extension of our existing API would suffice for that.

<div class="break-out">

<pre><code class="language-javascript">const { exitCode, stdout, stderr } = await execute('node my-cli.js my-first-command');

console.log(exitCode); // 0
console.log(stdout); // ["Hello worlds!"]
console.log(stderr); // []</code></pre>
</div>

With that, let’s call this our first iteration of the CLI Testing Library. We can execute a program, give it parameters, wait for it to finish, and evaluate some basic outcomes.

### User Input

While executing a program and waiting for it to finish is sufficient for a basic program, a little more thought needs to be put into the implementation of a program with which the user can interact. A classic scenario would be asking the user to input text or select an option.

We can certainly get inspired by the [Node.js API](https://nodejs.org/api/child_process.html#asynchronous-process-creation), which provides an `exec` function, fairly comparable to our own [`execute`](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L66-L85) function described above, but it also provides a [`spawn`](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L86-L126) method, which creates a process but in this case also allows for further interaction with the process after its creation. Not only will we have to use most of the same logic under the hood for our testing library, but because CLIs are always creating a process, we can also get inspired by Node.js for our own library’s API.

Let’s consider a basic scenario of the CLI asking only for text input from the user. For this trivial program alone, we’ll require several utilities. First, we need to wait for the actual input trigger (in other words, an instruction from the CLI to write some text). This instruction will be printed out in the `stdout`, mentioned earlier, so we would likely want to wait for a specific text question. Let’s call that `waitForText`, which would accept a string, and we’ll search for it any time the CLI program outputs a new line.

Next, it’s time to input the text that the program is asking for. In this case, we’ll have to interact with `stdin` under the hood, which is the input equivalent of `stdout`. Let’s call this utility [`writeText`](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L147-L155). Just like the previous utility function, it will accept a string.

Once the text is inputted into the process “console”, we would usually have to confirm it by pressing a key, such as “Enter”. That’s yet another interaction utility we can introduce, for pressing specific keys. Under the hood, we would also use `stdin`, of course, but let’s not concern ourselves with that. Let’s call it [`pressKey`](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L156-L167), which will accept the name of the key.

Now that the task is done, there is just one thing left to do: wait for the program to finish before we can evaluate whether it was executed successfully, and so on. [`waitForFinish`](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L132-L146) is the obvious name for this. With all that in mind, we can imagine something like the following:

<div class="break-out">

<pre><code class="language-javascript">const { waitForText, writeText, pressKey, waitForFinish } = await spawn(
    'node my-cli ask-for-name'
);

await waitForText('What is your name?');
await writeText('Georgy');
await pressKey('Enter');
await waitForFinish();</code></pre>
</div>

With the code above, we can simulate the whole interaction of the user with the program. We can also accompany the `spawn` helper with some more information such as exit code, `stdout`, or `stderr`, just like we did for `execute`. For `spawn`, the ideal format might be a bit different &mdash; perhaps `get`’ers would be best because the values will be dynamic throughout the program’s execution, and these `get`’ers could technically be called any time. `getStdout`, `getStderr`, or `getExitCode` will do the trick.

<div class="break-out">

<pre><code class="language-javascript">const { getExitCode, getStdout, getStderr, waitForText, writeText, pressKey, waitForFinish } = await spawn(
    'node my-cli ask-for-name'
);

await waitForText('What is your name?');
await writeText('Georgy');
await pressKey('Enter');
await waitForFinish();

console.log(getExitCode());  // 0
console.log(getStdout());  // ["What is your name?", "Georgy", "Your name is Georgy"]
console.log(getStderr());  // []</code></pre>
</div>

With that, we’ve covered the main idea of testing more complex interactive CLI programs.

### Enclosed And Independent Environment

Now that we’re deep into testing the CLI program by actually running the CLI, we should cover an important part of any test: its independence of other tests and test runs. Test frameworks usually support tests being run in parallel, in band, or the like, but that doesn’t mean we should limit ourselves to one of those. Each and every run, unless built otherwise, should be completely independent of everything else.

With your usual code, this is simple in most cases, but with the CLI and end-to-end tests, things can get tricky really quickly. The main problem is that the CLI often works with its surroundings. It might read some configuration files, generate other files, or manipulate the file system in some way. This means that each test needs to have its own temporary space on disk where the test use case can be prepared, with any files that might be needed for the test run. The same file-system space also needs to be cleaned up later so that nothing is left behind after each test run.

Creating a folder on disk is essential for any engine, and so it is for Node.js, one of the more mature engines. It even provides functionality for [creating temporary](https://nodejs.org/docs/latest-v15.x/api/fs.html#fs_fspromises_mkdtemp_prefix_options) folders somewhere on disk, wherever appropriate for the given operating system. The same functionality also gives us the path of the folder on disk so that it can be cleaned up when needed. Fortunately, we can easily use this cross-platform temporary-folder functionality for our test runs.

Let’s get back to our library API. It’s clear that each test should have some sort of [prepare](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L39) and [cleanup](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L49-L63) stages. Something like the following would cover that, allowing for completely independent test runs:

<pre><code class="language-javascript">const { execute, cleanup } = await prepareEnvironment();

const { exitCode } = await execute('node my-cli.js my-first-command');

await cleanup();</code></pre>

Now that we have a dedicated test-run root folder, we can create all kinds of helpers to manipulate this enclosed disk environment. [Reading files](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L49-L63), [creating files and folders](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L206-L212), making sure a [file exists](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L194-L202), [listing a folder’s contents](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/index.ts#L222-L224) &mdash; all of these and many more helpers related to disk manipulation are already provided by the Node.js process itself. All we have to do is wrap them so that the root directory used is the temporary one we have created.

<pre><code class="language-javascript">const {
  makeDir,
  writeFile,
  readFile,
  removeFile,
  removeDir,
  exists,
  ls,
} = await prepareEnvironment();

await makeDir('./subfolder');
await writeFile('./subfolder/file.txt', 'this will be file content');

const folderContent = await ls('./');
console.log(folderContent); // ["subfolder"]

const doesFileExists = await exists('./subfolder/file.txt');
console.log(doesFileExists); // true

const content = await readFile('./subfolder/file.txt');
console.log(content); // this will be file content

await removeFile('./subfolder/file.txt');
await removeDir('./subfolder'); // removes folder with any content</code></pre>

We should consider another thing related to cleanup. From the perspective of test execution, it’s completely unclear what are the contents of the CLI program itself. With end-to-end tests, we’re only concerned with what it does, not with the implementation. That means we cannot be sure what the subprocess contains or does, meaning that it can leave things hanging when executed. When the `cleanup` function is called in our test runs, we know that we’re done with testing. This means that part of the cleanup function could be a forceful teardown of anything that remains open or running.

### Systems Differences

More caveats arise when it comes to differences in systems and shells. The library already makes several normalization steps, described below.

It might be surprising, but even on a single system, different runs can produce a different `stdout` array of outputted lines. In some cases, lines might be missing, and in others, they might be there. Combined with the fact that the array will likely be used in combination with snapshots, this is unacceptable and needs to be normalized. In our case, always [getting rid of empty lines](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/Output.ts#L62) would be a sufficient solution.

A similar thing needs to be done with all of those special symbols used by the shell &mdash; for example, the ones used to make the output in the correct color. These symbols can differ across shell engines with the same program; so, [removing them from the output](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/createExecute.ts#L25-L26) will simplify things.

There is another small but real use case with a system’s special symbols. For whatever reason, in one type of system, they might be clearly visible as a special character in the output, and in another, they might be completely invisible. Two identical strings not being considered the same would lead to an insanely annoying debugging situation. Again, [deleting these](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/createExecute.ts#L27) is the way to go.

Last but not least, in the previous section we talked about creating a separate file-system space. The full path of the current execution folder will often be used in the CLI output. The same goes for the home directory of the system’s current user. Both paths could be part of the output and would cause a test failure in different environments. These need to be normalized so that they are not different in the CLI output in different systems and runs. We can [replace these with something more generic](https://github.com/gmrchk/cli-testing-library/blob/b51e9b683ad56808274fc798ba0823af167d4bcb/src/createExecute.ts#L22-L24), such as `{base}` and `{home}`, making it easily identifiable that a path is one of those special folders on disk.

### Mocking

Let’s be honest: Whatever we want to test and however close we want to get to the use case that the user sees, from time to time there will simply be a use case where we’ll need to make some compromise.

A good example is the CLI running with some dependency on an external web API. Each run would be affected by an external force. Moreover, it would depend not only on the API itself, but also on the internet connection and possibly some other factors, such as a VPN connection. That would compromise the requirement of reproducible runs, which is crucial for testing. So, we would need to sacrifice the integrity of the CLI program in such a case.

There is no library-integrated way to solve that. Remember that the library concerns itself with executing a process and the things around it. It doesn’t touch or understand the underlying CLI in any way. That’s why the following is more of a technique that can be used to mock parts of the executed CLI.

For the mocks to take effect on any part of the CLI program’s code, they need to be a part of the program itself &mdash; that is, be a part of one process. There is only one reasonable solution to this: make the mock a part of the CLI. Any other solution would have to be specific and invasive with regard to how the child processes are being executed in the system. That’s not something we could simply implement in a library and cover all possible use cases. It would also make the test run inconsistent with the production run in a way that is not easily controlled by the CLI’s author.

Instead, let’s focus on the program extension that was mentioned. After all, the CLI being tested will usually also be the CLI being developed, so making another entry point with the mocks included should be fairly doable. The example below mocks a response received from [Axios](https://axios-http.com/), assuming that the CLI uses Axios for this request.

<pre><code class="language-javascript">// mock-and-run.js
import axios from 'axios';
import MockAdapter from 'axios-mock-adapter';

const mock = new MockAdapter(axios);

mock.onGet('http://example.com/').reply(200, 'mocked response');

require('./index');  // include the CLI entry</code></pre>

Once we have that, we can just run the CLI the same way we would without the mocks, except that the CLI won’t be making any actual external requests, and it will always get a reproducible mocked response for the request code.

<pre><code class="language-javascript">const { exitCode } = await execute('node mock-and-run.js my-first-command');</code></pre>

## Conclusion

Many would argue that testing is the core of quality software and long-term sustainability. Different kinds of testing bring different kinds of benefits. Remember that, as with any other testing, end-to-end testing is an additional kind of testing at our disposal, not a replacement. The same surely applies to CLI testing.

With end-to-end tests, we can be even more confident that the program we're testing will do exactly what we want it to do, and won't be broken by some mistakes only affecting runtime, like the ones that can pop up after updating dependencies. 

The power of CLI testing lies in its flexible nature. Whenever we’re testing a program with the JavaScript library, we are certainly not restricted to Node.js programs. After all, we are executing a shell command; so, as long as the environment is able to execute the program as a process, any language will do.

**Recommended Reading**: *[Powerful Terminal And Command-Line (CLI) Tools For Modern Web Development](https://www.smashingmagazine.com/2021/11/powerful-terminal-commandline-tools-modern-web-development/) written by Louis Lazaris*

{{< signature "vf, il, al, yk" >}}
