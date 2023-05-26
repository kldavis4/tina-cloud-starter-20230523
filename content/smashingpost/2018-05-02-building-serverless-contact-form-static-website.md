---
title: 'Building A Serverless Contact Form For Your Static Site'
slug: building-serverless-contact-form-static-website
author: brian-holt
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7527d8-8518-4957-931d-efc1e22e34fe/form-submission.gif
date: 2018-05-02T18:30:17+02:00
summary: >-
  With the help of this article, you will finally be able to learn the basics of Amazon Web Services (AWS) Lambda and Simple Email Service (SES) APIs to help you build your own static site mailer on the Serverless Framework. Let’s get started!
description: >-
  With the help of this article, you will finally be able to learn the basics of Amazon Web Services (AWS) Lambda and Simple Email Service (SES) APIs to help you build your own static site mailer on the Serverless Framework. Let’s get started!
categories:
  - Serverless
  - Forms
  - Generators
---
Static site generators provide a fast and simple alternative to Content Management Systems (CMS) like [WordPress](https://wordpress.com). There’s no server or database setup, just a build process and simple HTML, CSS, and JavaScript. Unfortunately, without a server, it’s easy to hit their limits quickly. For instance, in adding a contact form.

With the rise of [serverless architecture](https://martinfowler.com/articles/serverless.html) adding a contact form to your static site doesn’t need to be the reason to switch to a CMS anymore. It’s possible to get the best of both worlds: a static site with a serverless back-end for the contact form (that you don’t need to maintain). Maybe best of all, in low-traffic sites, like portfolios, the high limits of many serverless providers make these services completely free!

In this article, you’ll learn the basics of Amazon Web Services (AWS) [Lambda](https://aws.amazon.com/lambda/) and [Simple Email Service (SES)](https://aws.amazon.com/ses/) APIs to build your own static site mailer on the [Serverless Framework](https://serverless.com/framework/). The full service will take form data submitted from an AJAX request, hit the Lambda endpoint, parse the data to build the SES parameters, send the email address, and return a response for our users. I’ll guide you through getting Serverless set up for the first time through deployment. It should take under an hour to complete, so let’s get started!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7527d8-8518-4957-931d-efc1e22e34fe/form-submission.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7527d8-8518-4957-931d-efc1e22e34fe/form-submission.gif" width="606" height="532" alt="The static site form, sending the message to the Lambda endpoint and returning a response to the user." /></a><figcaption>The static site form, sending the message to the Lambda endpoint and returning a response to the user.</figcaption></figure>

{{% feature-panel %}}

## Setting Up

There are minimal prerequisites in getting started with Serverless technology. For our purposes, it’s simply a [Node Environment](https://nodejs.org/en/) with [Yarn](https://yarnpkg.com/lang/en/), the [Serverless Framework](https://serverless.com/framework/), and an [AWS account](https://aws.amazon.com/s/dm/optimization/server-side-test/free-tier/free_np/).

### Setting Up The Project

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38189e1a-bf20-464b-8132-bf8f6e005bfe/serverless-framework.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38189e1a-bf20-464b-8132-bf8f6e005bfe/serverless-framework.png" sizes="100vw" caption="The Serverless Framework web site. Useful for installation and documentation." alt="The Serverless Framework web site. Useful for installation and documentation." >}}

We use Yarn to install the Serverless Framework to a local directory.

1. Create a new directory to host the project.
1. Navigate to the directory in your command line interface.
1. Run `yarn init` to create a `package.json` file for this project.
1. Run `yarn add serverless` to install the framework locally.
1. Run `yarn serverless create --template aws-nodejs --name static-site-mailer` to create a Node service template and name it `static-site-mailer`.

Our project is setup but we won’t be able to do anything until we set up our AWS services.

### Setting Up An Amazon Web Services Account, Credentials, And Simple Email Service

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15c1d472-387a-4db1-ac30-236dd30413b8/aws-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15c1d472-387a-4db1-ac30-236dd30413b8/aws-page.png" sizes="100vw" caption="The Amazon Web Services sign up page, which includes a generous free tier, enabling our project to be entirely free." alt="The Amazon Web Services sign up page, which includes a generous free tier, enabling our project to be entirely free." >}}

The Serverless Framework has recorded a [video walk-through](https://www.youtube.com/watch?v=KngM5bfpttA) for setting up AWS credentials, but I've listed the steps here as well.

1. Sign Up for an [AWS account](https://aws.amazon.com/s/dm/optimization/server-side-test/free-tier/free_np/) or log in if you already have one.
1. In the AWS search bar, search for "IAM".
1. On the IAM page, click on "Users" on the sidebar, then the "Add user" button.
1. On the Add user page, give the user a name -- something like "serverless" is appropriate. Check "Programmatic access" under Access type then click next.
1. On the permissions screen, click on the "Attach existing policies directly" tab, search for "AdministratorAccess" in the list, check it, and click next.
1. On the review screen you should see your user name, with "Programmatic access", and "AdministratorAccess", then create the user.
1. The confirmation screen shows the user "Access key ID" and "Secret access key", you’ll need these to provide the Serverless Framework with access. In your CLI, type `yarn sls config credentials --provider aws --key YOUR_ACCESS_KEY_ID --secret YOUR_SECRET_ACCESS_KEY`, replacing `YOUR_ACCESS_KEY_ID` and `YOUR_SECRET_ACCESS_KEY` with the keys on the confirmation screen.

Your credentials are configured now, but while we're in the AWS console let’s set up Simple Email Service.

1. Click Console Home in the top left corner to go home.
1. On the home page, in the AWS search bar, search for "Simple Email Service".
1. On the SES Home page, click on "Email Addresses" in the sidebar.
1. On the Email Addresses listing page, click the "Verify a New Email Address" button.
1. In the dialog window, type your email address then click "Verify This Email Address".
1. You’ll receive an email in moments containing a link to verify the address. Click on the link to complete the process.

Now that our accounts are made, let’s take a peek at the Serverless template files.

### Setting Up The Serverless Framework

Running `serverless create` creates two files: [handler.js](https://smashingmagazine.com/provide/handler.js) which contains the Lambda function, and [serverless.yml](https://smashingmagazine.com/provide/serverless.yml) which is the configuration file for the entire Serverless Architecture. Within the configuration file, you can specify as many handlers as you'd like, and each one will map to a new function that can interact with other functions. In this project, we’ll only create a single handler, but in a full Serverless Architecture, you'd have several of the various functions of the service.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99127c53-2dbd-4b76-b432-7a8ac8003434/sls-file-structure.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99127c53-2dbd-4b76-b432-7a8ac8003434/sls-file-structure.png" sizes="100vw" caption="The default file structure generated from the Serverless Framework containing <a href='https://smashingmagazine.com/provide/handler.js'>handler.js</a> and <a href='https://smashingmagazine.com/provide/serverless.yml'>serverless.yml</a>." alt="The default file structure generated from the Serverless Framework containing handler.js and serverless.yml." >}}

In [handler.js](https://smashingmagazine.com/provide/handler.js), you’ll see a single exported function named `hello`. This is currently the main (and only) function. It, along with all Node handlers, take three parameters:

* `event`  
This can be thought of as the input data for the function.
* [`context object`](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-context.html)  
This contains the runtime information of the Lambda function.
* [`callback`](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html#nodejs-prog-model-handler-callback)  
An optional parameter to return information to the caller.

<div class="break-out">

<pre><code class="language-javascript">// handler.js

'use strict';

module.exports.hello = (event, context, callback) => {
  const response = {
    statusCode: 200,
    body: JSON.stringify({
      message: 'Go Serverless v1.0! Your function executed successfully!',
      input: event,
    }),
  };

  callback(null, response);
};
</code></pre></div>

At the bottom of `hello`, there’s a callback. It’s an optional argument to return a response, but if it’s not _explicitly_ called, it will _implicitly_ return with `null`. The callback takes [two parameters](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html#nodejs-prog-model-handler-callback):

* **Error error**  
For providing error information for when the Lambda itself fails. When the Lambda succeeds, `null` should be passed into this parameter.
* **Object result**  
For providing a response object. It must be `JSON.stringify` compatible. If there’s a parameter in the error field, this field is ignored.

Our static site will send our form data in the event body and the callback will return a response for our user to see.

In [serverless.yml](https://smashingmagazine.com/provide/serverless.yml) you’ll see the name of the service, provider information, and the functions.

<pre><code class="language-yaml"># serverless.yml

service: static-site-mailer

provider:
  name: aws
  runtime: nodejs6.10

functions:
  hello:
    handler: handler.hello
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6677f489-dbd3-4a6a-b7c5-ff6237a57474/mapping.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6677f489-dbd3-4a6a-b7c5-ff6237a57474/mapping.png" sizes="100vw" caption="How the function names in <a href='https://smashingmagazine.com/provide/serverless.yml'>serverless.yml</a> map to <a href='https://smashingmagazine.com/provide/handler.js'>handler.js</a>." alt="How the function names in serverless.yml map to handler.js." >}}

Notice the mapping between the hello function and the handler? We can name our file and function anything and as long as it maps to the configuration it will work. Let’s rename our function to `staticSiteMailer`.

<pre><code class="language-yaml"># serverless.yml

functions:
  staticSiteMailer:
    handler: handler.staticSiteMailer
</code></pre>

<div class="break-out">

<pre><code class="language-javascript">// handler.js

module.exports.staticSiteMailer = (event, context, callback) => {
  ...
};
</code></pre></div>

Lambda functions need permission to interact with other AWS infrastructure. Before we can send an email, we need to allow SES to do so. In [serverless.yml](https://smashingmagazine.com/provide/serverless.yml), under `provider.iamRoleStatements` add the permission.

<pre><code class="language-yaml"># serverless.yml

provider:
  name: aws
  runtime: nodejs6.10
  iamRoleStatements:
    - Effect: "Allow"
      Action:
        - "ses:SendEmail"
      Resource: ["*"]
</code></pre>

Since we need a URL for our form action, we need to add HTTP events to our function. In [serverless.yml](https://smashingmagazine.com/provide/serverless.yml) we create a path, specify the method as `post`, and set CORS to true for security.

<pre><code class="language-yaml">functions:
  staticSiteMailer:
    handler: handler.staticSiteMailer
    events:
      - http:
          method: post
          path: static-site-mailer
          cors: true
</code></pre>

Our updated [serverless.yml](https://smashingmagazine.com/provide/serverless.yml) and [handler.js](https://smashingmagazine.com/provide/handler.js) files should look like:

<pre><code class="language-yaml"># serverless.yml

service: static-site-mailer

provider:
  name: aws
  runtime: nodejs6.10

functions:
  staticSiteMailer:
    handler: handler.staticSiteMailer
    events:
      - http:
          method: post
          path: static-site-mailer
          cors: true

provider:
  name: aws
  runtime: nodejs6.10
  iamRoleStatements:
    - Effect: "Allow"
      Action:
        - "ses:SendEmail"
      Resource: ["*"]
</code></pre>

<div class="break-out">

<pre><code class="language-javascript">// handler.js

'use strict';

module.exports.staticSiteMailer = (event, context, callback) => {
  const response = {
    statusCode: 200,
    body: JSON.stringify({
      message: 'Go Serverless v1.0! Your function executed successfully!',
      input: event,
    }),
  };

  callback(null, response);
};
</code></pre></div>

Our Serverless Architecture is setup, so let’s deploy it and test it. You’ll get a simple JSON response.

<div class="break-out">

<pre><code class="language-bash">yarn sls deploy --verbose
yarn sls invoke --function staticSiteMailer

{
    "statusCode": 200,
    "body": "{\"message\":\"Go Serverless v1.0! Your function executed successfully!\",\"input\":{}}"
}
</code></pre></div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e655ec6-3562-4834-922c-bc1c1004dac5/response.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e655ec6-3562-4834-922c-bc1c1004dac5/response.png" sizes="100vw" caption="The return response from invoking our brand new serverless function." alt="The return response from invoking our brand new serverless function." >}}

## Creating The HTML Form

Our Lambda function input and form output need to match, so before we build the function we’ll build the form and capture its output. We keep it simple with name, email, and message fields. We’ll add the form action once we've deployed our serverless architecture and got our URL, but we know it will be a POST request so we can add that in. At the end of the form, we add a paragraph tag for displaying response messages to the user which we’ll update on the submission callback.

<pre><code class="language-html">&lt;form action="{{ SERVICE URL }}" method="POST"&gt;
  &lt;label&gt;
    Name
    &lt;input type="text" name="name" required&gt;
  &lt;/label&gt;
  &lt;label&gt;
    Email
    &lt;input type="email" name="reply_to" required&gt;
  &lt;/label&gt;
  &lt;label&gt;
    Message:
    &lt;textarea name="message" required&gt;&lt;/textarea&gt;
  &lt;/label&gt;
  &lt;button type="submit"&gt;Send Message&lt;/button&gt;
&lt;/form&gt;
&lt;p id="js-form-response"&gt;&lt;/p&gt;
</code></pre>

To capture the output we add a submit handler to the form, turn our form parameters into an object, and send stringified JSON to our Lambda function. In the Lambda function we use `JSON.parse()` to read our data. Alternatively, you could use [jQuery’s Serialize](https://api.jquery.com/serialize/) or [query-string](https://www.npmjs.com/package/query-string) to send and parse the form parameters as a query string but `JSON.stringify()` and `JSON.parse()` are native.

<div class="break-out">

<pre><code class="language-javascript">(() => {
  const form = document.querySelector('form');
  const formResponse = document.querySelector('js-form-response');

  form.onsubmit = e => {
    e.preventDefault();

    // Prepare data to send
    const data = {};
    const formElements = Array.from(form);
    formElements.map(input => (data[input.name] = input.value));

    // Log what our lambda function will receive
    console.log(JSON.stringify(data));
  };
})();
</code></pre></div>

Go ahead and submit your form then capture the console output. We’ll use it in our Lambda function next.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c14cf58-3540-4ae2-9304-585ffe87991b/form-submission-capture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c14cf58-3540-4ae2-9304-585ffe87991b/form-submission-capture.png" sizes="100vw" caption="Capturing the form data in a console log." alt="Capturing the form data in a console log." >}}

## Invoking Lambda Functions

Especially during development, we need to test our function does what we expect. The Serverless Framework provides the [`invoke`](https://serverless.com/framework/docs/providers/aws/cli-reference/invoke/) and [`invoke local`](https://serverless.com/framework/docs/providers/aws/cli-reference/invoke-local/) command to trigger your function from _live_ and _development_ environments respectively. Both commands require the function name passed through, in our case `staticSiteMailer`.

<pre><code class="language-bash">yarn sls invoke local --function staticSiteMailer
</code></pre>

To pass mock data into our function, create a new file named `data.json` with the captured console output under a `body` key within a JSON object. It should look something like:

<div class="break-out">

<pre><code class="language-javascript">// data.json

{
  "body": "{\"name\": \"Sender Name\",\"reply_to\": \"sender@email.com\",\"message\": \"Sender message\"}"
}
</code></pre></div>

To invoke the function with the local data, pass the `--path` argument along with the path to the file.

<div class="break-out">

<pre><code class="language-bash">yarn sls invoke local --function staticSiteMailer --path data.json
</code></pre></div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d98e0e-fe10-4a81-9837-dbbb45ac198f/response-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d98e0e-fe10-4a81-9837-dbbb45ac198f/response-2.png" sizes="100vw" caption="An updated return response from our serverless function when we pass it JSON data." alt="An updated return response from our serverless function when we pass it JSON data." >}}

You’ll see a similar response to before, but the `input` key will contain the event we mocked. Let’s use our mock data to send an email using Simple Email Service!

## Sending An Email With Simple Email Service

We're going to replace the `staticSiteMailer` function with a call to a private `sendEmail` function. For now you can comment out or remove the template code and replace it with:

<div class="break-out">

<pre><code class="language-javascript">// hander.js

function sendEmail(formData, callback) {
  // Build the SES parameters
  // Send the email
}

module.exports.staticSiteMailer = (event, context, callback) => {
  const formData = JSON.parse(event.body);

  sendEmail(formData, function(err, data) {
    if (err) {
      console.log(err, err.stack);
    } else {
      console.log(data);
    }
  });
};
</code></pre></div>

First, we parse the `event.body` to capture the form data, then we pass it to a private `sendEmail` function. `sendEmail` is responsible for sending the email, and the callback function will return a failure or success response with `err` or `data`. In our case, we can simply log the error or data since we’ll be replacing this with the Lambda callback in a moment.

Amazon provides a convenient SDK, `aws-sdk`, for connecting their services with Lambda functions. Many of their services, including SES, are part of it. We add it to the project with `yarn add aws-sdk` and import it into the top the handler file.

<pre><code class="language-javascript">// handler.js

const AWS = require('aws-sdk');
const SES = new AWS.SES();
</code></pre>

In our private `sendEmail` function, we build the [`SES.sendEmail` parameters](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/SES.html#sendEmail-property) from the parsed form data and use the callback to return a response to the caller. The parameters require the following as an object:

* **Source**  
The email address SES is sending _from_.
* **ReplyToAddresses**  
An array of email addresses added to the reply to the field in the email.
* **Destination**  
An object that must contain at least one **ToAddresses**, **CcAddresses**, or **BccAddresses**. Each field takes an array of email addresses that correspond to the _to_, _cc_, and _bcc_ fields respectively.
* **Message**  
An object which contains the **Body** and **Subject**.

Since `formData` is an object we can call our form fields directly like `formData.message`, build our parameters, and send it. We pass _your_ SES-verified email to `Source` and `Destination.ToAddresses`. As long as the email is verified you can pass anything here, including different email addresses. We pluck our `reply_to`, `message`, and `name` off our `formData` object to fill in the `ReplyToAddresses` and `Message.Body.Text.Data` fields.

<div class="break-out">

<pre><code class="language-javascript">// handler.js
function sendEmail(formData, callback) {
  const emailParams = {
    Source: 'your_email@example.com', // SES SENDING EMAIL
    ReplyToAddresses: [formData.reply_to],
    Destination: {
      ToAddresses: ['your_email@example.com'], // SES RECEIVING EMAIL
    },
    Message: {
      Body: {
        Text: {
          Charset: 'UTF-8',
          Data: `${formData.message}\n\nName: ${formData.name}\nEmail: ${formData.reply_to}`,
        },
      },
      Subject: {
        Charset: 'UTF-8',
        Data: 'New message from your_site.com',
      },
    },
  };

  SES.sendEmail(emailParams, callback);
}
</code></pre></div>

`SES.sendEmail` will send the email and our callback will return a response. Invoking the local function will send an email to your verified address.

<div class="break-out">

<pre><code class="language-bash">yarn sls invoke local --function staticSiteMailer --path data.json
</code></pre></div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cf13126-7715-4e9d-9920-b6264b98e70c/response-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cf13126-7715-4e9d-9920-b6264b98e70c/response-3.png" sizes="100vw" caption="The return response from <code>SES.sendEmail</code> when it succeeds." alt="The return response from SES.sendEmail when it succeeds." >}}

## Returning A Response From The Handler

Our function sends an email using the command line, but that’s not how our users will interact with it. We need to return a response to our AJAX form submission. If it fails, we should return an appropriate `statusCode` as well as the `err.message`. When it succeeds, the `200` `statusCode` is sufficient, but we’ll return the mailer response in the body as well. In `staticSiteMailer` we build our response data and replace our `sendEmail` callback function with the Lambda callback.

<div class="break-out">

<pre><code class="language-javascript">// handler.js

module.exports.staticSiteMailer = (event, context, callback) => {
  const formData = JSON.parse(event.body);

  sendEmail(formData, function(err, data) {
    const response = {
      statusCode: err ? 500 : 200,
      headers: {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': 'https://your-domain.com',
      },
      body: JSON.stringify({
        message: err ? err.message : data,
      }),
    };

    callback(null, response);
  });
};
</code></pre></div>

Our Lambda callback now returns both success and failure messages from `SES.sendEmail`. We build the response with checks if `err` is present so our response is consistent. The Lambda callback function itself passes `null` in the error argument field and the response as the second. We want to pass errors onwards, but if the Lambda itself fails, its [callback will be implicitly called](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html#nodejs-prog-model-handler-callback) with the error response.

In the `headers`, you’ll need to replace `Access-Control-Allow-Origin` with your own domain. This will prevent any other domains from using your service and potentially racking up an AWS bill in your name! And I don’t cover it in this article, but it’s possible to set-up Lambda to use your own domain. You’ll need to have an SSL/TLS certificate uploaded to Amazon. The Serverless Framework team wrote a [fantastic tutorial](https://serverless.com/blog/serverless-api-gateway-domain/) on how to do so.

Invoking the local function will now send an email and return the appropriate response.

<div class="break-out">

<pre><code class="language-bash">yarn sls invoke local --function staticSiteMailer --path data.json
</code></pre></div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8001f309-c77d-4a1d-af59-f6d0bbb958ac/response-4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8001f309-c77d-4a1d-af59-f6d0bbb958ac/response-4.png" sizes="100vw" caption="The return response from our serverless function, containing the SES.sendEmail return response in the body." alt="The return response from our serverless function, containing the SES.sendEmail return response in the body." >}}

## Calling The Lambda Function From The Form

Our service is complete! To deploy it run `yarn sls deploy -v`. Once it’s deployed you’ll get a URL that looks something like `https://r4nd0mh45h.execute-api.us-east-1.amazonaws.com/dev/static-site-mailer` which you can add to the form action. Next, we create the AJAX request and return the response to the user.

<div class="break-out">

<pre><code class="language-javascript">(() => {
  const form = document.querySelector('form');
  const formResponse = document.querySelector('js-form-response');

  form.onsubmit = e => {
    e.preventDefault();

    // Prepare data to send
    const data = {};
    const formElements = Array.from(form);
    formElements.map(input => (data[input.name] = input.value));

    // Log what our lambda function will receive
    console.log(JSON.stringify(data));

    // Construct an HTTP request
    var xhr = new XMLHttpRequest();
    xhr.open(form.method, form.action, true);
    xhr.setRequestHeader('Accept', 'application/json; charset=utf-8');
    xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');

    // Send the collected data as JSON
    xhr.send(JSON.stringify(data));

    // Callback function
    xhr.onloadend = response => {
      if (response.target.status === 200) {
        // The form submission was successful
        form.reset();
        formResponse.innerHTML = 'Thanks for the message. I’ll be in touch shortly.';
      } else {
        // The form submission failed
        formResponse.innerHTML = 'Something went wrong';
        console.error(JSON.parse(response.target.response).message);
      }
    };
  };
})();
</code></pre></div>

In the AJAX callback, we check the status code with `response.target.status`. If it’s anything other than `200` we can show an error message to the user, otherwise let them know the message was sent. Since our Lambda returns stringified JSON we can parse the body message with `JSON.parse(response.target.response).message`. It’s especially useful to log the error.

You should be able to submit your form entirely from your static site!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7527d8-8518-4957-931d-efc1e22e34fe/form-submission.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7527d8-8518-4957-931d-efc1e22e34fe/form-submission.gif" width="606" height="532" alt="The static site form, sending the message to the Lambda endpoint and returning a response to the user." /></a><figcaption>The static site form, sending the message to the Lambda endpoint and returning a response to the user.</figcaption></figure>

## Next Steps

Adding a contact form to your static is easy with the Serverless Framework and AWS. There’s room for improvement in our code, like adding [form validation with a honeypot](https://jennamolby.com/how-to-prevent-form-spam-by-using-the-honeypot-technique/), preventing AJAX calls for invalid forms and improving the UX if the response, but this is enough to get started. You can see some of these improvements within the [static site mailer repo](https://github.com/bholtbholt/static-site-mailer) I’ve created. I hope I've inspired you to try out Serverless yourself!

{{< signature "lf, ra, il" >}}

