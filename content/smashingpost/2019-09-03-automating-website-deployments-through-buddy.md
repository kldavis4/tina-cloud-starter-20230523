---
title: 'Automating Website Deployments Through Buddy'
slug: automating-website-deployments-through-buddy
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdddfae-6e83-4a5c-89e2-2a9876370d8d/automating-website-deployments-through-buddy.png
date: 2019-09-03T12:30:00+02:00
summary: >-
  The typical website stack has gotten complex, involving many tools and technologies, and requiring automation to handle its deployment adequately. In this article, let’s take a closer look at <a href="https://buddy.works/?utm_source=art_top&utm_medium=cpc&utm_campaign=smashing_art_0819">Buddy</a>, one of the most comprehensive tools for automating website deployments.
description: >-
  In this article, let’s take a closer look at Buddy, one of the most comprehensive tools for automating website deployments.
categories:
  - Performance
  - Tools
disable_ads: true
disable_panels: true
---
<p>(This is a sponsored article.) Managing the deployment of a website used to be easy: It simply involved uploading files to the server through FTP and you were pretty much done. But those days are gone: Websites have gotten very complex, involving many tools and technologies in their stacks.</p>

<p>Nowadays, a typical web project may require to execute build tools to compress assets and generate the deliverable files for production, upload the assets to a CDN and invalidate stale ones, execute a test suite to make sure the code has no errors (for both client and server-side code), do database migrations (and, to be on the safe side, first execute a backup of the database), instantiate the desired number of servers behind a load balancer and deploy the application to them (through an atomic deployment, so that the website is always available), download and install the dependencies, deploy serverless functions, and finally notify the team that everything is ready through Slack or by email.</p>

<p>All this process sounds like a bit too much, right? Well, it actually <em>is</em> too much. How can we avoid getting overwhelmed by the complexity of the task at hand? The solution boils down to a single word: Automation. By automating all the tasks to execute, we will not dread doing the deployment (and having a trembling sweaty finger when pressing the Enter button), indeed we may not be even aware of it.</p>

<p>Automation improves the quality of our work, since we can avoid having to manually execute mind-numbing tasks again and again, which will enable us to use all our time for coding, and reassures us that the deployment will not fail due to human errors (such as overriding the wrong folder as in the old FTP days).</p>

## Introduction To Continuous Integration, Delivery, And Deployment

<p>Managing and automating software deployment involves both tools and processes. In particular, Git as the version control system where to store our source code, and the availability of Git-hosting services (such as GitHub, GitLab and BitBucket) which trigger events when new code is pushed into the repository, enable to benefit from the following processes:</p>

<ul>
  <li><strong>Continuous Integration</strong><br />The strategy of merging changes in the code into the main branch as often as possible, upon which automated tests against a build of the codebase are run to validate that the new code doesn’t introduce errors;</li>
  <li><strong>Continuous Delivery</strong><br />An extension to Continuous Integration which also automates the release process, enabling to deploy the project into production at any moment;</li>
  <li><strong>Continuous Deployment</strong><br />An extension to Continuous Delivery which automatically deploys the new code whenever it passes all required tests (as small a change it may contain), enabling to easily identify the source of any problem that might arise, and removing pressure off the team as it doesn’t need to deal with a "release day" anymore.</li>
</ul>

<p>Adhering to these strategies has several benefits. The most immediate one is that our product can ship new features faster, indeed they can go live as soon as the team has finished coding them. The team can also receive feedback immediately (either from team members on a development environment, from the client on a staging environment, and from the users after it goes live) and be able to react straight away, thus creating a positive feedback loop. And because the whole process is fully automated, the team can save time and focus on the code, thus improving the quality of the product.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/246f14ea-cae9-4860-b89f-7cf04d630cfc/continuous-delivery-flow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/246f14ea-cae9-4860-b89f-7cf04d630cfc/continuous-delivery-flow.png" sizes="100vw" caption="Continuous delivery enables getting feedback as early as possible. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/246f14ea-cae9-4860-b89f-7cf04d630cfc/continuous-delivery-flow.png'>Large preview</a>)" alt="Continuous delivery enables getting feedback as early as possible" >}}

## Introducing Buddy, A Tool For Automating Software Deployment

<p>The popularity of Git has given rise to a new generation of tools to manage the complexity of software deployments. <a href="https://bit.ly/smbuddy">Buddy</a> is one of these new tools, born with the goal of making it easy to implement Continuous Integration/Delivery/Deployment, while broadening the number of features our application can provide, improving its quality, and reducing its costs by allowing to incorporate the offerings of the best or cheapest cloud-based service providers (among them AWS, DigitalOcean, Google Cloud Platform, Cloudflare, Rackspace, Azure, and others) into our stacks. This way, for instance, our application can be hosted on GitHub, be protected from DDoS through Cloudflare, have its static files hosted through DigitalOcean, use serverless functions from AWS Lambda, and authenticate users through Firebase, and everything is handled seamlessly.</p>

<p>Buddy operates through the use of pipelines: Sets of actions defined by the developer in a specific order, executed either manually or automatically when executing a Git push, that deliver the application from a Git repository to wherever needed and transforming it as required. Pipelines are extremely flexible, enabling developers to add only the required actions and have them customized for their specific needs.</p>

<p>For instance, the following pipeline performs all required tasks to deploy some Node.js application: execute the build step, upload files to the server through SFTP, upload assets to AWS S3 and purge them from the CDN, restart the server and finally inform the team through Slack (as it can be appreciated in the image below, the pipeline can be self-explanatory):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f411757d-c184-4cdb-bc0d-8fddae6bd21c/pipeline-example.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66bb861f-c475-49c3-95a8-017be853ac3b/pipeline-example-800w.png" width="800" height="" alt="Buddy pipeline example" /></a><figcaption>An example of a pipeline to deploy a Node.js application. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f411757d-c184-4cdb-bc0d-8fddae6bd21c/pipeline-example.png">Large preview</a>)</figcaption></figure>

<p>We can create different pipelines for different environments, and execute special actions when the process fails (such as when a test was not successful when the server to deploy to is down, or others). For instance, the following pipeline (to <a href="https://buddy.works/blog/pipeline-of-the-week-getflow?utm_source=pipeline_of_theweek&utm_medium=cpc&utm_campaign=smashing_art_0819">deploy a Node.js & PHP app that uses DigitalOcean, Fortrabbit & AWS CloudFront for hosting</a>) makes a backup of assets and purges the CDN only when deploying to production, and sends a notification to the team through Slack in case of failure:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/995c2946-9efb-4197-94d9-ecfd6ecc7ae7/pipeline-environments.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/995c2946-9efb-4197-94d9-ecfd6ecc7ae7/pipeline-environments.jpg" width="800" height="" alt="Demonstration of Buddy pipeline" /></a><figcaption>Pipeline configured for different environments. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/995c2946-9efb-4197-94d9-ecfd6ecc7ae7/pipeline-environments.jpg">Large preview</a>)</figcaption></figure>

<p>A noteworthy effect of configuring our pipelines with actions from different cloud-service providers is that we can conveniently switch among them whenever the need arises, making it easy to avoid vendor lock-in (this includes also <a href="https://buddy.works/blog/change-repository-provider?utm_source=change_rep_provider&utm_medium=cpc&utm_campaign=smashing_art_0819">changing the repository provider</a>). Buddy offers slightly over 100 actions out of the box, and also allows developers to create and use their own actions. This image shows all the readily available actions:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e565457-8362-422e-8094-c54a4e8a1299/buddy-actions.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e565457-8362-422e-8094-c54a4e8a1299/buddy-actions.gif" width="750" height="710" alt="Buddy actions" /></a><figcaption>Out of the box actions in Buddy. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e565457-8362-422e-8094-c54a4e8a1299/buddy-actions.gif">Large preview</a>)</figcaption></figure>

## Creating A Pipeline

<p>Let’s see how to create a simple pipeline to test and deploy a Node.js application, and send a notification to the team. The first step is to create a new project, during which you will be asked to select the project’s hosting provider (from among GitHub, GitLab, Bitbucket, Buddy Git Hosting, and your private Git server), and then to select the repository:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3782ff0b-3768-48bb-b3b7-32a2f88b9a39/1-automating-website-deployments-through-buddy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3782ff0b-3768-48bb-b3b7-32a2f88b9a39/1-automating-website-deployments-through-buddy.png" sizes="100vw" caption="Selecting the hosting provider (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3782ff0b-3768-48bb-b3b7-32a2f88b9a39/1-automating-website-deployments-through-buddy.png'>Large preview</a>)" alt="Tutorial step 1: Selecting the hosting provider" >}}

<p>Then we can create the pipeline, specifying when it must run (either manually, automatically after new code is pushed to the repository, or automatically every x amount of time) and from which branch:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b2a3c2-a2d1-4c51-8f82-758d7b6ae248/2-automating-website-deployments-through-buddy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b2a3c2-a2d1-4c51-8f82-758d7b6ae248/2-automating-website-deployments-through-buddy.png" sizes="100vw" caption="Creating a new pipeline (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b2a3c2-a2d1-4c51-8f82-758d7b6ae248/2-automating-website-deployments-through-buddy.png'>Large preview</a>)" alt="Tutorial step 2: Creating a new pipeline" >}}

<p>Then we can add actions to the pipeline. For that, we simply click on the “+” button to add a new action, upon which we must configure it as needed. To build and test a Node.js application we add and configure a “Node.js” action:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c60be318-3a85-4b79-ac76-430cf2318f54/3-automating-website-deployments-through-buddy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c60be318-3a85-4b79-ac76-430cf2318f54/3-automating-website-deployments-through-buddy.png" sizes="100vw" caption="Adding a Node.js action (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c60be318-3a85-4b79-ac76-430cf2318f54/3-automating-website-deployments-through-buddy.png'>Large preview</a>)" alt="Tutorial step 3: Adding a Node.js action" >}}

<p>After testing the application, we can deploy it by uploading it to our production server through SFTP. For this, we add an “SFTP” action, and configure it through custom-defined environment variables <code>${SFTP}</code> and <code>${SFTP_USER}</code>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/732a1cdb-fb77-4479-986a-951993383f2b/4-automating-website-deployments-through-buddy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/732a1cdb-fb77-4479-986a-951993383f2b/4-automating-website-deployments-through-buddy.png" sizes="100vw" caption="Adding an SFTP action (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/732a1cdb-fb77-4479-986a-951993383f2b/4-automating-website-deployments-through-buddy.png'>Large preview</a>)" alt="Tutorial step 4: Adding an SFTP action" >}}

<p>Finally, we send an email to the team with the results of the execution. For this, we add and configure the “Email” action:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67431197-55d3-4df6-a5d3-77f3dc23374a/5-automating-website-deployments-through-buddy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67431197-55d3-4df6-a5d3-77f3dc23374a/5-automating-website-deployments-through-buddy.png" sizes="100vw" caption="Adding an Email action (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67431197-55d3-4df6-a5d3-77f3dc23374a/5-automating-website-deployments-through-buddy.png'>Large preview</a>)" alt="Tutorial step 5: Adding an Email action" >}}

<p>That’s it. Our pipeline will look like this:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff28514-249d-4fd7-9d07-f7ddf7a78c40/6-automating-website-deployments-through-buddy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff28514-249d-4fd7-9d07-f7ddf7a78c40/6-automating-website-deployments-through-buddy.png" sizes="100vw" caption="Pipeline finished (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff28514-249d-4fd7-9d07-f7ddf7a78c40/6-automating-website-deployments-through-buddy.png'>Large preview</a>)" alt="Tutorial step 6: Pipeline finished" >}}

<p>From this moment on, if the pipeline was configured to run when new code is pushed to the repository, doing a git push will trigger the execution of the pipeline.</p>

## Staying Constantly Up To Date

<p>Web development is in a never-ending state of flux, with new tools and services being launched without a break, some of them often becoming a hot trend immediately and the new normal barely a few months later. Technologies seldom heard of a few years ago progressively gain importance and eventually become a must (voice search, machine learning, WebAssembly), new frameworks and libraries offer new ways of building sites (GraphQL, Gatsby, Next.js, Nuxt.js), and our applications need to be accessed from newly-invented devices (Amazon Echo, In-car systems). To keep our applications relevant, we must continuously evaluate the latest offerings and decide if to add them to our technology stack. Hence, it is extremely important that our platforms for developing the application do not restrict what technologies we can use.</p>

<p>Buddy deals with this issue by continuously collecting feedback from its users about what they need (through user polls, <a href="https://forum.buddy.works/?utm_source=forum&utm_medium=cpc&utm_campaign=smashing_art_0819">their forum</a>, communication channels, and <a href="https://twitter.com/BuddyGit?utm_source=twitter&utm_medium=cpc&utm_campaign=smashing_art_0819">tweets</a>), and its team strives to deliver the required features. The <a href="https://buddy.works/blog?utm_source=blog&utm_medium=cpc&utm_campaign=smashing_art_0819">Buddy blog</a> provides a glimpse of the intense pace of development: For instance, in the last few months they implemented features for <a href="https://buddy.works/blog/gatsby-cli?utm_source=gatsby&utm_medium=cpc&utm_campaign=smashing_art_0819
">building static apps and websites with Gatsby</a>, deploying to <a href="https://buddy.works/blog/upcloud-deployment?utm_source=upcloud&utm_medium=cpc&utm_campaign=smashing_art_0819">UpCloud</a> and to <a href="https://buddy.works/blog/google-cloud-functions?utm_source=google_cloud&utm_medium=cpc&utm_campaign=smashing_art_0819">Google Cloud Functions</a>, <a href="https://buddy.works/blog/webhook-pipeline-trigger?utm_source=pipelines_webhooks&utm_medium=cpc&utm_campaign=smashing_art_0819">triggering pipelines with webhooks</a>, <a href="https://buddy.works/blog/firebase-integration?utm_source=firebase_integ&utm_medium=cpc&utm_campaign=smashing_art_0819">integrating with Firebase</a>, <a href="https://buddy.works/blog/aws-ecs?utm_source=aws_ecs&utm_medium=cpc&utm_campaign=smashing_art_0819">building and running Docker containers on AWS ECS</a>, and many others.</p>

## Conclusion

<p>Automation has become a must to avoid being overwhelmed by the complexity of modern website deployment. We can make use of Continuous Integration/Delivery/Deployment (readily feasible by hosting our source code through Git) to shorten the time needed for delivering new features into our applications and getting feedback from the users.</p>

<p>Buddy helps in this task, enabling developers to create pipelines to execute actions concerning a wide array of technologies and cloud-service providers, and combining these actions in any possible way to satisfy the most particular needs.</p>
  
<p><em>You can <a href="https://buddy.works/?utm_source=2weeksfree&utm_medium=cpc&utm_campaign=smashing_art_0819">check out Buddy for free for 2 weeks</a> and, if you need to host your data, you can also <a href="https://buddy.works/on-premises?utm_source=onpremises&utm_medium=cpc&utm_campaign=smashing_art_0819
">install it on your own premises</a>.</em></p>

{{< signature "ms, ra, yk, il" >}}
