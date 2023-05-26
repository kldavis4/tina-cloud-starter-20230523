---
title: 'Local Testing A Serverless API (API Gateway And Lambda)'
slug: local-testing-serverless-api-gateway-lambda
author: tomhudson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d43ff4a2-4767-4595-9f46-f1ca18f64060/local-testing-serverless-api-gateway-lambda.jpg
date: 2021-10-05T10:00:00.000Z
summary: >-
  Have you ever struggled with testing cloud services locally? Specifically, have you ever struggled with locally testing an API that uses API Gateway and Lambda, with the Serverless framework, on AWS? In this article, Tom Hudson shares a quick overview of how easy it is to quickly set up your project to test locally before deploying to AWS.
description: >-
  Have you ever struggled with testing cloud services locally? Specifically, have you ever struggled with locally testing an API that uses API Gateway and Lambda, with the Serverless framework, on AWS? In this article, Tom Hudson shares a quick overview of how easy it is to quickly set up your project to test locally before deploying to AWS.
categories:
  - Testing
  - API
  - Tools
  - Serverless
---

This article is for anyone struggling with testing cloud services locally, and specifically for people wanting to locally test an API that uses API Gateway and Lambda, with the Serverless framework, on AWS. I was once in desperate need of this knowledge, and my co-worker Joseph Jaffe helped me put this solution into place.

A very popular and quick API solution is using Serverless along with API Gateway and Lambda. If you have never done this before, you can [read more about it here](https://www.serverless.com/blog/node-rest-api-with-serverless-lambda-and-dynamodb). If you already have experience, and are looking for creative ways to locally test, then keep reading. Bonus if you like 🌮🌮!

## The Problem

When setting up an API using the Serverless framework, there are important choices to make. Some are *extremely* important: they can make your life much easier as you build your API, or cause you huge headaches in the future. For instance, when I first started my API, I was setting up each endpoint in its own Serverless project folder. Thus each endpoint had unique URLs. This is bad practice for an API solution that needs one base URL with multiple service points. We changed the solution to have all endpoints in the same Serverless project, and that allowed us to use one extra handy aspect of Lambda &mdash; layers. Lambda layers are a way to share code across API endpoints, reducing the amount of repeated code across the API project. You can read <a href="https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html">more about Lambda Layers here</a>, but I digress. Let’s get back to the problem: local testing!

When you create a new API endpoint, you must deploy the entire API to include the new resource in API Gateway and get the URL for it. Once you have done that, you can deploy individual resources. 

Deploying for Serverless takes time. Lots of time. For instance, see these average deploy times for one of our last projects:

<ul>
<li>Deploying a single endpoint: <strong>~7 seconds</strong> 🙂</li>
<li>Deploying full API (~12 resources): <strong>~24 seconds</strong> 😔</li>
<li>Deploying Layers (2 layers): <strong>~32 seconds</strong> 💀</li>
</ul>

While these times don’t appear too bad at first glance, imagine trying to quickly and iteratively test out changes in your API. Having each deploy over 1 minute long is a huge time-hog and will kill your momentum. Stretch this over weeks of development and you will see why we all need a solution to test Lambda functions locally.

## Our Solution

In order to quickly flush out the obvious errors, we require local testing. In order to test locally, we found that `serverless invoke local` allows us to do this in the simplest manner. This not only allows us to run Lambda scripts locally, but we can also add breakpoints using Debug Mode in Visual Studio Code. If you have never played with it, <a href="https://code.visualstudio.com/docs/editor/debugging">Debug Mode in VSC is really helpful</a>.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135f2786-8e9d-482a-9143-69cce0fcc0bc/1-local-testing-serverless-api-gateway-lambda.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135f2786-8e9d-482a-9143-69cce0fcc0bc/1-local-testing-serverless-api-gateway-lambda.png" width="800" height="471" sizes="100vw" caption="🌮 Debug Mode in Visual Studio Code 🌮  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135f2786-8e9d-482a-9143-69cce0fcc0bc/1-local-testing-serverless-api-gateway-lambda.png'>Large preview</a>)" alt="Debug Mode in Visual Studio Code." >}}


The most important aspect of local testing is instant feedback. No more waiting around for layers, functions or entire APIs to deploy! Tons of time saved during the initial build and your (patience as well as your) Program Director will love you for it!
 
### Data

The last Serverless API project we worked on stored all the data in JSON files hosted on AWS S3 buckets. You may be reading the data from a database, so you need to make sure you can still access the data while running locally. One way would be to set up the database locally on your machine. Ultimately, every project is unique and requires you to think creatively for a solution that meets your needs.

{{% feature-panel %}}

### Environment Variables

In order for us to know if we are running locally or not, we created an environment variable to pass in through our local invocation. The variable is named `LOCAL_DEV` and is used to check if we should be loading the data from S3 or from a local file system folder, like so:

<pre><code class="language-javascript">const data = 
  process.env.LOCAL_DEV === "true"
  ? require(`./data/tacos.json`)
  : //handle loading/setting the data as you regularly would</code></pre>

Note above that the boolean value of true is in quotes. Environment variables always come through as strings, so be ready to handle this fact of life.

We have a snapshot of the data stored on S3 on our local computers, so when we are in local development mode, we use that local data in order to run and test the code locally.

Additionally, if you are using layers in Lambda, you will need to point directly to the code as opposed to referring to it by name, at the top of your Lambda file:

<pre><code class="language-json">const apiCommon = process.env.LOCAL_DEV === "true"
? require("../layers/apicommon/nodejs/node_modules/apicommon/index")
: require("apicommon");</code></pre>

### Local Invocation

Once you have all code in place to allow the Lambda function to run successfully locally, then you can try invoking the function. Here is an example invocation of an endpoint called tacos (🌮🌮) that gets all tacos from a food API. Because I ❤️ 🌮🌮. <a href="https://github.com/thirteen23/tacos-are-the-best">Code for this example can found on Github</a>.

This is copied and pasted from a command shortcut I defined in my `package.json` file. That command requires you to put literal `\` markers in front of all quotes. Here is that command from **`package.json`** in its entirety:

<pre><code class="language-json">"scripts": {
"local-tacos": "serverless invoke local --function tacos --data '{ \"queryStringParameters\": {\"type\": \"breakfast\", \"filling1\": \"egg\", \"filling2\": \"bacon\", \"filling3\": \"cheese\", \"tortilla\": \"flour\", \"salsa\": \"Salsa Doña\"}}' -e LOCAL_DEV=true > output.json"
}</code></pre>

Ok, now let’s look at this command and what each part does. I am removing all of the literal markers for easier readability.

<pre><code class="language-json">serverless invoke local --function tacos --data '{ "queryStringParameters": {"type": "breakfast", "filling1": "egg", "filling2": "bacon", "filling3": "cheese", "tortilla": "flour", "salsa": "Salsa Doña"}}' -e LOCAL_DEV=true &gt; output.json</code></pre>

First, the base part:

<pre><code class="language-json">serverless invoke local --function tacos</code></pre>

The item above says to locally invoke the API endpoint "tacos" (local 🌮🌮 are the best, right?) which gets a set of tacos filtered by whatever query string parameters you send it. Next, let’s look at the second part.

<pre><code class="language-json">--data '{ "queryStringParameters": {"type": "breakfast", "filling1": "egg", "filling2": "bacon", "filling3": "cheese", "tortilla": "flour", "salsa": "Salsa Doña"}}'</code></pre>

Here is where we can define whatever query string parameters we are passing into the API endpoint. For this example, we pass into the API endpoint all the attributes that describe the taco(s) we are looking for. In our case, we are looking for egg, bacon and cheese tacos on a flour tortilla with Salsa Doña.

**Note**: *Any guess as to where the taco described above (with Salsa Doña) can be found in Austin, Texas, USA? If you know, please respond in the comments!* 

{{% ad-panel-leaderboard %}}

If you need to test a bunch of parameters, you could save them out in a testing/query.json file(s) so you could do something like:

<pre><code class="language-bash">yarn local-taco query-success yarn local-taco query-fail</code></pre>

This could be a good start for an <a href="https://www.serverless.com/blog/how-test-serverless-applications">API testing environment</a>!

The third part of the call is for defining any environment variables.

<pre><code class="language-bash">-e LOCAL_DEV=true</code></pre>

This tells our Lambda code very clearly we are running this function locally and to make sure and prepare for that by pulling all resources in locally as well.

Last, I pipe the results into a JSON file.

<pre><code class="language-json">&gt; output.json</code></pre>

From here I can easily verify if the results are correct or if an error was thrown.

{{% ad-panel-leaderboard %}}

## Conclusion

That sums it up! If you didn’t see the link earlier, I have a <a href="https://github.com/thirteen23/tacos-are-the-best">sample project written up</a> that you can try on your own, using the Serverless framework, the AWS services API Gateway, and Lambda.

Also, if you have ideas on how to make this solution better, or other alternative solutions, I would love to hear about your feedback/tips/experiences in the comments below.

### Further Reading On Smashing Magazine

- [Orchestrating Complexity With Web Animations API](https://www.smashingmagazine.com/2021/09/orchestrating-complexity-web-animations-api/), Kirill Myshkin
- [Choosing A New Serverless Database Technology At An Agency (Case Study)](https://www.smashingmagazine.com/2021/03/choosing-new-serverless-database-technology-agency/), Michael Rispoli
- [Gatsby Serverless Functions And The International Space Station](https://www.smashingmagazine.com/2021/07/gatsby-serverless-functions-international-space-station/), Paul Scanlon
- [Flaky Tests: Getting Rid Of A Living Nightmare In Testing](https://www.smashingmagazine.com/2021/04/flaky-tests-living-nightmare/), Ramona Schwering

🎧 **Bonus**: [Smashing Podcast Episode 22 With Chris Coyier: What Is Serverless?](https://www.smashingmagazine.com/2020/08/smashing-podcast-episode-22/) (moderated by Drew McLellan)

{{< signature "vf, yk, il" >}}
