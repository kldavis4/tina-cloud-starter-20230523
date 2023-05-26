---
title: How To Develop An Interactive Command Line Application Using Node.js
slug: interactive-command-line-application-node-js
image: null
date: 2017-03-14T22:05:09.000Z
author: niharsawant
description: >-
  Over the last five years, Node.js has helped to bring uniformity to software
  development. You can do anything in Node.js, whether it be front-end
  development, server-side scripting, cross-platform desktop applications,
  cross-platform mobile applications, Internet of Things, you name it. **Writing
  command line tools has also become easier than ever before because of
  Node.js** — not just any command line tools, but tools that are interactive,
  useful and less time-consuming to develop.

  If you are a front-end developer, then you must have heard of or worked on
  Gulp, Angular CLI, Cordova, Yeoman and others. Have you ever wondered how they
  work?
categories:
  - Angular
  - JavaScript
  - Node.js
  - Workflow
---
If you are a front-end developer, then you must have heard of or worked on <a href="https://gulpjs.com">Gulp</a>, <a href="https://cli.angular.io">Angular CLI</a>, <a href="https://cordova.apache.org">Cordova</a>, <a href="https://yeoman.io">Yeoman</a> and others. Have you ever wondered how they work? For example, in the case of Angular CLI, by running a command like <code>ng new &lt;project-name&gt;</code>, you end up creating an Angular project with basic configuration. Tools such as Yeoman ask for runtime inputs that eventually help you to customize a project’s configuration as well. Some generators in Yeoman help you to deploy a project in your production environment. That is exactly what we are going to learn today.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b579719b-a7a1-467c-9309-d721687ac4f1/nodejs-023.jpg" width="500" height="300" alt="How To Develop An Interactive Command Line Application Using Node.js" /></figure>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [An Introduction To Node.js And MongoDB](https://www.smashingmagazine.com/2014/05/detailed-introduction-nodejs-mongodb/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Useful Node.js Tools, Tutorials And Resources](https://www.smashingmagazine.com/2011/09/useful-node-js-tools-tutorials-and-resources/)

{{% feature-panel %}}

In this tutorial, we will develop a command line application that accepts a CSV file of customer information, and using the <a href="https://github.com/sendgrid/sendgrid-nodejs">SendGrid API</a>, we will send emails to them. Here are the contents of this tutorial:

1.  ["Hello, World"](#hello-world)
2.  [Handling command line arguments](#cli-arguments)
3.  [Runtime user inputs](#runtime-inputs)
4.  [Asynchronous network communication](#async-communication)
5.  [Decorating the CLI output](#chalk)
6.  [Making it a shell command](#shell-command)
7.  [Beyond JavaScript](#beyond-js)

## "Hello, World"

This tutorial assumes you have installed Node.js on your system. In case you have not, please <a href="https://nodejs.org/">install it</a>. Node.js also comes with a package manager named <a href="https://www.npmjs.com">npm</a>. Using npm, you can install many open-source packages. You can get the complete list on <a href="https://www.npmjs.com">npm’s official website</a>. For this project, we will be using many open-source modules (more on that later). Now, let’s create a Node.js project using npm.

<pre><code class="language-bash">$ npm init
name: broadcast
version: 0.0.1
description: CLI utility to broadcast emails
entry point: broadcast.js
</code></pre>

I have created a directory named <code>broadcast</code>, inside of which I have run the <code>npm init</code> command. As you can see, I have provided basic information about the project, such as name, description, version and entry point. The entry point is the main JavaScript file from where the execution of the script will start. By default, Node.js assigns <code>index.js</code> as the entry point; however, in this case, we are changing it to <code>broadcast.js</code>. When you run the <code>npm init</code> command, you will get a few more options, such as the Git repository, license and author. You can either provide values or leave them blank.

Upon successful execution of the <code>npm init</code>, you will find that a <code>package.json</code> file has been created in the same directory. This is our configuration file. At the moment, it holds the information that we provided while creating the project. You can explore more about <code>package.json</code> <a href="https://docs.npmjs.com/files/package.json">in npm’s documentation</a>.

Now that our project is set up, let’s create a "Hello world" program. To start, create a <code>broadcast.js</code> file in your project, which will be your main file, with the following snippet:

<pre><code class="language-javascript">console.log('hello world');
</code></pre>

Now, let’s run this code.

<pre><code class="language-bash">$ node broadcast
hello world
</code></pre>

As you can see, "hello word" is printed to the console. You can run the script with either <code>node broadcast.js</code> or <code>node broadcast</code>; Node.js is smart enough to understand the difference.

According to <code>package.json</code>’s documentation, there is an option named <a href="https://docs.npmjs.com/files/package.json#dependencies"><code>dependencies</code></a> in which you can mention all of the third-party modules that you plan to use in the project, along with their version numbers. As mentioned, we will be using many third-party open-source modules to develop this tool. In our case, <code>package.json</code> looks like this:

<pre><code class="language-javascript">{
  "name": "broadcast",
  "version": "0.0.1",
  "description": "CLI utility to broadcast emails",
  "main": "broadcast.js",
  "license": "MIT",
  "dependencies": {
    "async": "^2.1.4",
    "chalk": "^1.1.3",
    "commander": "^2.9.0",
    "csv": "^1.1.0",
    "inquirer": "^2.0.0",
    "sendgrid": "^4.7.1"
  }
}
</code></pre>

As you must have noticed, we will be using <a href="https://caolan.github.io/async/docs.html">Async</a>, <a href="https://github.com/chalk/chalk">Chalk</a>, <a href="https://www.npmjs.com/package/commander">Commander</a>, <a href="https://www.npmjs.com/package/csv">CSV</a>, <a href="https://github.com/SBoudrias/Inquirer.js/">Inquirer.js</a> and <a href="https://github.com/sendgrid/sendgrid-nodejs">SendGrid</a>. As we progress ahead with the tutorial, usage of these modules will be explained in detail.</p>

## Handling Command Line Arguments

Reading command line arguments is not difficult. You can simply use <a href="https://nodejs.org/docs/latest/api/process.html"><code>process.argv</code></a> to read them. However, parsing their values and options is a cumbersome task. So, instead of reinventing the wheel, we will use the <a href="https://www.npmjs.com/package/commander">Commander</a> module. Commander is an open-source Node.js module that helps you write interactive command line tools. It comes with very interesting features for parsing command line options, and it has Git-like subcommands, but the thing I like best about Commander is the automatic generation of help screens. You don’t have to write extra lines of code — just parse the <code>--help</code> or <code>-h</code> option. As you start defining various command line options, the <code>--help</code> screen will get populated automatically. Let’s dive in:

<pre><code class="language-bash">$ npm install commander --save
</code></pre>

This will install the Commander module in your Node.js project. Running the <code>npm install with --save</code> option will automatically include Commander in the project’s dependencies, defined in <code>package.json</code>. In our case, all of the dependencies have already been mentioned; hence, there is no need to run this command.

<pre><code class="language-javascript">var program = require('commander');

program
  .version('0.0.1')
  .option('-l, --list [list]', 'list of customers in CSV file')
  .parse(process.argv)

console.log(program.list);
</code></pre>

As you can see, handling command line arguments is straightforward. We have defined a <code>--list</code> option. Now, whatever values we provide followed by the <code>--list</code> option will get stored in a variable wrapped in brackets — in this case, <code>list</code>. You can access it from the <code>program</code> variable, which is an instance of Commander. At the moment, this program only accepts a file path for the <code>--list</code> option and prints it in the console.

<pre><code class="language-bash">$ node broadcast --list input/employees.csv
input/employees.csv
</code></pre>

You must have noticed also a chained method that we have invoked, named <code>version</code>. Whenever we run the command providing <code>--version</code> or <code>-V</code> as the option, whatever value is passed in this method will get printed.

<pre><code class="language-bash">$ node broadcast --version
0.0.1
</code></pre>

Similarly, when you run the command with the <code>--help</code> option, it will print all of the options and subcommands defined by you. In this case, it will look like this:

<pre><code class="language-bash">$ node broadcast --help

  Usage: broadcast [options]

  Options:

    -h, --help                 output usage information
    -V, --version              output the version number
    -l, --list &lt;list&gt;          list of customers in CSV file
</code></pre>

Now that we are accepting file paths from command line arguments, we can start reading the CSV file using the <a href="https://www.npmjs.com/package/csv">CSV</a> module. The CSV module is an all-in-one-solution for handling CSV files. From creating a CSV file to parsing it, you can achieve anything with this module.

Because we plan to send emails using the SendGrid API, we are using the following document as a sample CSV file. Using the CSV module, we will read the data and display the name and email address provided in the respective rows.
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>First name</th>
<th>Last name</th>
<th>Email</th>
</tr>
<tr>
<td>Dwight</td>
<td>Schrute</td>
<td>dwight.schrute@dundermifflin.com</td>
</tr>
<tr>
<td>Jim</td>
<td>Halpert</td>
<td>jim.halpert@dundermifflin.com</td>
</tr>
<tr>
<td>Pam</td>
<td>Beesly</td>
<td>pam.beesly@dundermifflin.com</td>
</tr>
<tr>
<td>Ryan</td>
<td>Howard</td>
<td>ryan.howard@dundermifflin.com</td>
</tr>
<tr>
<td>Stanley</td>
<td>Hudson</td>
<td>stanley.hudson@dundermifflin.com</td>
</tr>
</tbody>
</table>

Now, let’s write a program to read this CSV file and print the data to the console.

<pre><code class="language-javascript">const program = require('commander');
const csv = require('csv');
const fs = require('fs');

program
  .version('0.0.1')
  .option('-l, --list [list]', 'List of customers in CSV')
  .parse(process.argv)

let parse = csv.parse;
let stream = fs.createReadStream(program.list)
    .pipe(parse({ delimiter : ',' }));

stream
  .on('data', function (data) {
    let firstname = data[0];
    let lastname = data[1];
    let email = data[2];
    console.log(firstname, lastname, email);
  });
</code></pre>

Using the native <a href="https://nodejs.org/api/fs.html">File System</a> module, we are reading the file provided via command line arguments. The File System module comes with predefined events, one of which is <code>data</code>, which is fired when a chunk of data is being read. The <code>parse</code> method from the CSV module splits the CSV file into individual rows and fires multiple data events. Every data event sends an array of column data. Thus, in this case, it prints the data in the following format:

<pre><code class="language-bash">$ node broadcast --list input/employees.csv
Dwight Schrute dwight.schrute@dundermifflin.com
Jim Halpert jim.halpert@dundermifflin.com
Pam Beesly pam.beesly@dundermifflin.com
Ryan Howard ryan.howard@dundermifflin.com
Stanley Hudson stanley.hudson@dundermifflin.com
</code></pre>

## Runtime User Inputs

Now we know how to accept command line arguments and how to parse them. But what if we want to accept input during runtime? A module named <a href="https://github.com/SBoudrias/Inquirer.js">Inquirer.js</a> enables us to accept various types of input, from plain text to passwords to a multi-selection checklist.

For this demo, we will accept the sender’s email address and name via runtime inputs.

<pre><code class="language-javascript">…
let questions = [
  {
    type : "input",
    name : "sender.email",
    message : "Sender's email address - "
  },
  {
    type : "input",
    name : "sender.name",
    message : "Sender's name - "
  },
  {
    type : "input",
    name : "subject",
    message : "Subject - "
  }
];
let contactList = [];
let parse = csv.parse;
let stream = fs.createReadStream(program.list)
    .pipe(parse({ delimiter : "," }));

stream
  .on("error", function (err) {
    return console.error(err.message);
  })
  .on("data", function (data) {
    let name = data[0] + " " + data[1];
    let email = data[2];
    contactList.push({ name : name, email : email });
  })
  .on("end", function () {
    inquirer.prompt(questions).then(function (answers) {
      console.log(answers);
    });
  });
</code></pre>

First, you’ll notice in the example above that we’ve created an array named <code>contactList</code>, which we’re using to store the data from the CSV file.

Inquirer.js comes with a method named <a href="https://github.com/SBoudrias/Inquirer.js#methods"><code>prompt</code></a>, which accepts an array of questions that we want to ask during runtime. In this case, we want to know the sender’s name and email address and the subject of their email. We have created an array named <code>questions</code> in which we are storing all of these questions. This array accepts objects with properties such as <code>type</code>, which could be anything from an input to a password to a raw list. You can see the list of all available types in the <a href="https://github.com/SBoudrias/Inquirer.js/">official documentation</a>. Here, <code>name</code> holds the name of the key against which user input will be stored. The <code>prompt</code> method returns a promise object that eventually invokes a chain of success and failure callbacks, which are executed when the user has answered all of the questions. The user’s response can be accessed via the <code>answers</code> variable, which is sent as a parameter to the <code>then</code> callback. Here is what happens when you execute the code:

<pre><code class="language-bash">$ node broadcast -l input/employees.csv
? Sender's email address -  michael.scott@dundermifflin.com
? Sender's name -  Micheal Scott
? Subject - Greetings from Dunder Mifflin
{ sender:
   { email: 'michael.scott@dundermifflin.com',
     name: 'Michael Scott' },
  subject: 'Greetings from Dunder Mifflin' }
</code></pre>

## Asynchronous Network Communication

Now that we can read the recipient’s data from the CSV file and accept the sender’s details via the command line prompt, it is time to send the emails. We will be using SendGrid’s API to send email.

<pre><code class="language-javascript">…
let __sendEmail = function (to, from, subject, callback) {
  let template = "Wishing you a Merry Christmas and a " +
    "prosperous year ahead. P.S. Toby, I hate you.";
  let helper = require('sendgrid').mail;
  let fromEmail = new helper.Email(from.email, from.name);
  let toEmail = new helper.Email(to.email, to.name);
  let body = new helper.Content("text/plain", template);
  let mail = new helper.Mail(fromEmail, subject, toEmail, body);

  let sg = require('sendgrid')(process.env.SENDGRID_API_KEY);
  let request = sg.emptyRequest({
    method: 'POST',
    path: '/v3/mail/send',
    body: mail.toJSON(),
  });

  sg.API(request, function(error, response) {
    if (error) { return callback(error); }
    callback();
  });
};

stream
  .on("error", function (err) {
    return console.error(err.response);
  })
  .on("data", function (data) {
    let name = data[0] + " " + data[1];
    let email = data[2];
    contactList.push({ name : name, email : email });
  })
  .on("end", function () {
    inquirer.prompt(questions).then(function (ans) {
      async.each(contactList, function (recipient, fn) {
        __sendEmail(recipient, ans.sender, ans.subject, fn);
      });
    });
  });
</code></pre>

In order to start using the <a href="https://github.com/sendgrid/sendgrid-nodejs">SendGrid</a> module, we need to get an API key. You can generate this API key from <a href="https://app.sendgrid.com/settings/api_keys">SendGrid’s dashboard</a> (you’ll need to create an account). Once the API key is generated, we will store this key in environment variables against a key named <code>SENDGRID_API_KEY</code>. You can access environment variables in Node.js using <a href="https://nodejs.org/api/process.html#process_process_env"><code>process.env</code></a>.

In the code above, we are sending asynchronous email using SendGrid’s API and the <a href="https://caolan.github.io/async/docs.html">Async</a> module. The Async module is one of the most powerful Node.js modules. Handling asynchronous callbacks often leads to <a href="https://stackoverflow.com/a/25098230/757449">callback hell</a>. There comes a point when there are so many asynchronous calls that you end up writing callbacks within a callback, and often there is no end to it. Handling errors gets even more complicated for a JavaScript ninja. The Async module helps you to overcome callback hell, providing handy methods such as <a href="https://caolan.github.io/async/docs.html#each"><code>each</code></a>, <a href="https://caolan.github.io/async/docs.html#series"><code>series</code></a>, <a href="https://caolan.github.io/async/docs.html#map"><code>map</code></a> and many more. These methods help us write code that is more manageable and that, in turn, appears like synchronous behavior.

In this example, rather than sending a synchronous request to SendGrid, we are sending an asynchronous request in order to send an email. Based on the response, we’ll send subsequent requests. Using each method in the Async module, we are iterating over the <code>contactList</code> array and calling a function named <code>__sendEmail</code>. This function accepts the recipient’s details, the sender’s details, the subject line and the callback for the asynchronous call. <code>__sendEmail</code> sends emails using SendGrid’s API; you can explore more about the SendGrid module in the <a href="https://sendgrid.com/docs/API_Reference/Web_API_v3/index.html">official documentation</a>. Once an email is successfully sent, an asynchronous callback is invoked, which passes the next object from the <code>contactList</code> array.

That’s it! Using Node.js, we have created a command line application that accepts CSV input and sends email.</p>

## Decorating The Output

Now that our application is ready to send emails, let’s see how can we decorate the output, such as errors and success messages. To do so, we’ll use the <a href="https://github.com/chalk/chalk">Chalk</a> module, which is used to style command line inputs.

<pre><code class="language-javascript">…
stream
  .on("error", function (err) {
    return console.error(err.response);
  })
  .on("data", function (data) {
    let name = data[0] + " " + data[1];
    let email = data[2];
    contactList.push({ name : name, email : email });
  })
  .on("end", function () {
    inquirer.prompt(questions).then(function (ans) {
      async.each(contactList, function (recipient, fn) {
        __sendEmail(recipient, ans.sender, ans.subject, fn);
      }, function (err) {
        if (err) {
          return console.error(chalk.red(err.message));
        }
        console.log(chalk.green('Success'));
      });
    });
  });
</code></pre>

In the snippet above, we have added a callback function while sending emails, and that function is called when the asynchronous <code>each</code> loop is either completed or broken due to runtime error. Whenever a loop is not completed, it sends an <code>error</code> object, which we print to the console in red. Otherwise, we print a success message in green.

If you go through Chalk’s documentation, you will find many options to style this input, including a range of console colors (magenta, yellow, blue, etc.) underlining and bolded text.</p>

## Making It A Shell Command

Now that our tool is complete, it is time to make it executable like a regular shell command. First, let’s add a <a href="https://unix.stackexchange.com/a/87600">shebang</a> at the top of <code>broadcast.js</code>, which will tell the shell how to execute this script.

<pre><code class="language-javascript">#!/usr/bin/env node

const program = require("commander");
const inquirer = require("inquirer");
…
</code></pre>

Now, let’s configure the <code>package.json</code> to make it executable.

<pre><code class="language-javascript">…
  "description": "CLI utility to broadcast emails",
  "main": "broadcast.js",
  "bin" : {
    "broadcast" : "./broadcast.js"
  }
…
</code></pre>

We have added a new property named <a href="https://docs.npmjs.com/files/package.json#bin"><code>bin</code></a>, in which we have provided the name of the command from which <code>broadcast.js</code> will be executed.

Now for the final step. Let’s install this script at the global level so that we can start executing it like a regular shell command.

<pre><code class="language-bash">$ npm install -g
</code></pre>

Before executing this command, make sure you are in the same project directory. Once the installation is complete, you can test the command.

<pre><code class="language-bash">$ broadcast --help
</code></pre>

This should print all of the available options that we get after executing <code>node broadcast --help</code>. Now you are ready to present your utility to the world.

One thing to keep in mind: During development, any change you make in the project will not be visible if you simply execute the <code>broadcast</code> command with the given options. If you run <code>which broadcast</code>, you will realize that the path of <code>broadcast</code> is not the same as the project path in which you are working. To prevent this, simply run <code>npm link</code> in your project folder. This will automatically establish a symbolic link between the executable command and the project directory. Henceforth, whatever changes you make in the project directory will be reflected in the broadcast command as well.</p>

## Beyond JavaScript

The scope of the implementation of these kinds of CLI tools goes well beyond JavaScript projects. If you have some experience with software development and IT, then <a href="https://en.wikipedia.org/wiki/Bash_(Unix_shell)">Bash tools</a> will have been a part of your development process. From deployment scripts to <a href="https://en.wikipedia.org/wiki/Cron">cron jobs</a> to backups, you could automate anything using Bash scripts. In fact, before <a href="https://www.docker.com">Docker</a>, <a href="https://www.chef.io">Chef</a> and <a href="https://puppet.com">Puppet</a> became the <em>de facto</em> standards for infrastructure management, Bash was the savior. However, Bash scripts always had some issues. They do not easily fit in a development workflow. Usually, we use anything from Python to Java to JavaScript; Bash has rarely been a part of core development. Even writing a simple conditional statement in Bash requires going through endless documentation and debugging.

However, with JavaScript, this whole process becomes simpler and more efficient. All of the tools automatically become cross-platform. If you want to run a native shell command such as <code>git</code>, <code>mongodb</code> or <code>heroku</code>, you could do that easily with the <a href="https://nodejs.org/api/child_process.html">Child Process</a> module in Node.js. This enables you to write software tools with the simplicity of JavaScript.

I hope this tutorial has been helpful to you. If you have any questions, please drop them in the comments section below or <a href="https://twitter.com/nihar_sawant">tweet me</a>.

{{< signature "rb, al, il" >}}

