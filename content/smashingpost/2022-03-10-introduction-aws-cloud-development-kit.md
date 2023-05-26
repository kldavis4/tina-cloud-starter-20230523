---
title: 'An Introduction To AWS Cloud Development Kit (CDK)'
slug: introduction-aws-cloud-development-kit
author: vivek-maskara
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46a0c491-6562-46ba-a48d-41b4f97b0965/introduction-aws-cloud-development-kit.jpg
date: 2022-03-10T18:00:00.000Z
summary: >-
  In this article, Vivek Maskara introduces Amazon Web Services’ (AWS) Cloud Development Kit (CDK) which is increasingly becoming a popular tool for managing AWS-based infrastructure. We’ll take a closer look into CDK concepts, and then how to use the AWS CDK toolkit to deploy a sample application to an AWS account.
description: >-
  In this article, Vivek Maskara introduces Amazon Web Services’ (AWS) Cloud Development Kit (CDK) which is increasingly becoming a popular tool for managing AWS-based infrastructure. We’ll take a closer look into CDK concepts, and then how to use the AWS CDK toolkit to deploy a sample application to an AWS account.
categories:
  - UI
  - Apps
  - Tools
  - Coding
---

When you start building a cloud-based back-end system for your application, you have a choice, on the one hand, to do it manually using a graphical user interface (GUI) or the command-line interface (CLI) or, on the other hand, to do it programmatically. If your application uses just a handful of cloud resources, you can easily manage it using the GUI console. As the complexity of your system increases, the underlying infrastructure will also grow, and managing it manually will become a nightmare. Moreover, it’s prone to human error &mdash; a small user error could potentially bring the system into a bad state. Managing your infrastructure programmatically is a much better alternative, whether you are an indie developer using just a small bunch of cloud resources or a large organization with very complex infrastructure requirements.

Before jumping into AWS CDK, I’ll provide a brief overview of the workflow for manual infrastructure deployment and discuss a few points to determine whether managing the infrastructure manually is the right choice for your project. Next, we’ll look into ways to programmatically manage your infrastructure and briefly discuss different tools that you can use to do so. Finally, we’ll dive deep into using AWS CDK, an infrastructure-as-code (IaC) tool offered by AWS, and see an example of how to use it to manage your infrastructure.

## Manual Infrastructure Deployment

Manual infrastructure deployment refers to using the GUI or CLI made available by a cloud provider to deploy your cloud resources. Because it involves manual intervention, creating new environments can’t be executed in a repeatable, reliable, or consistent fashion. Moreover, the run books need to be kept up to date, and knowledge transfer is required whenever there is a change in personnel.

For example, if you need cloud storage for your application and you decide to use AWS for your cloud requirements, then you can simply browse to the [AWS cloud console](https://console.aws.amazon.com/), log in to it, click on “Create a new bucket”, and fill out the web form to provision an AWS S3 bucket. The diagram below shows an example of the form that you need to fill out in order to create the bucket.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59c6c263-ecc0-4857-9e63-f3f0944de07e/1-introduction-aws-cloud-development-kit.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59c6c263-ecc0-4857-9e63-f3f0944de07e/1-introduction-aws-cloud-development-kit.png" width="800" height="515" sizes="100vw" caption="Create an S3 bucket using AWS console. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59c6c263-ecc0-4857-9e63-f3f0944de07e/1-introduction-aws-cloud-development-kit.png'>Large preview</a>)" alt="An example of the form you need to fill to create an AWS S3 bucket" >}}

If you prefer to use the CLI instead, open your terminal and run the `create-bucket` command.

<div class="break-out">

<pre><code class="language-bash">aws s3api create-bucket --bucket my-bucket --region us-east-1
</code></pre>
</div>

Similarly, if your application uses multiple cloud resources, you would need to repeat these steps for each of the services involved. In addition to provisioning the resources, you will need to ensure that the inter-service permissions are set correctly. And if you are using a different cloud provider, then you would have to perform a similar set of steps in their console. All of the major cloud providers have a GUI and a CLI interface that can be used to create, modify, or delete any cloud resources.

If your process is more formalized, then any infrastructure change might require a new service request. The diagram below shows a general workflow for manually processing any service request. A development and IT operations (DevOps) engineer might be responsible for processing this request and would need to perform a series of steps to make the changes. The DevOps engineer would first determine the list of affected cloud services, and then log in to the corresponding service account to create, modify, or delete resources. Moreover, the engineer would also update the access-control policies for inter-service communication. Finally, the engineer might need to set up any event triggers. For example, let’s say that a function needs to be triggered whenever a new object is uploaded to the cloud storage. In such a scenario, and assuming that the function already exists, the engineer would need to create a new event trigger that invokes the function every time the cloud storage emits a `PUT` object event.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f736798b-a353-497d-93d9-fbe82f806182/2-introduction-aws-cloud-development-kit.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f736798b-a353-497d-93d9-fbe82f806182/2-introduction-aws-cloud-development-kit.jpg" width="800" height="386" sizes="100vw" caption="Deployment workflow without IaC. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f736798b-a353-497d-93d9-fbe82f806182/2-introduction-aws-cloud-development-kit.jpg'>Large preview</a>)" alt="Deployment workflow without IaC" >}}

From the examples above, we get a sense that manually managing infrastructure isn’t a viable option for large projects with complex cloud requirements. For smaller projects, where you need to use just a few cloud resources that do not change often, you could very well manage it manually, because managing another code base for your infrastructure would be too much overhead. When you start working on a new prototype, you could start with manual deployment and switch to IaC once you see a need for frequent changes.

{{% feature-panel %}}

## Programmatic Infrastructure Deployment

Programmatic infrastructure management refers to managing infrastructure in a descriptive model, using the same versioning as the DevOps team uses for source code. Most major cloud providers offer some way for you to manage infrastructure using code or templates.

AWS infrastructure can be managed programmatically using either [AWS CloudFormation](https://aws.amazon.com/cloudformation/) templates or [AWS CDK](https://aws.amazon.com/cdk/). AWS CloudFormation templates comprise a YAML- or JSON-based configuration file that describes the desired resources and their dependencies, so you can launch and configure them together as a stack. Google Cloud recommends the use of its [Deployment Manager](https://cloud.google.com/deployment-manager/docs) to manage your infrastructure. Similar to AWS CloudFormation, Google Cloud’s Deployment Manager templates are YAML templates that can be used to describe your resources. Microsoft Azure offers [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview) (ARM) templates to deploy and manage Azure services. ARM templates are JSON templates that can be used to define resources and their relationships. Moreover, [Terraform](https://www.terraform.io/intro) is an open-source IaC tool that supports hundreds of cloud providers, including AWS, Google Cloud, and Microsoft Azure, and can be used to manage your infrastructure. Terraform configurations are maintained in `.tf` files and are based on the HashiCorp configuration language (HCL) syntax.

Whether AWS CloudFormation, Google Cloud Deployment Manager, Microsoft ARM, or Hashicorp Terraform &mdash; all of them require the use of YAML-, JSON-, or TF-based templates, which might not be intuitive to developers. As the complexity increases, working with YAML, JSON, Terraform files becomes a bit difficult because the configuration cannot be modularized. If you are working with AWS, you have an option to use AWS CDK, which we will discuss in detail in the coming sections. If you are using some other cloud provider, Terraform is currently the best IaC solution, because it supports the use of a declarative language (HCL) to define your infrastructure.

In the coming sections, I will provide a brief overview of AWS CDK and its benefits, and I’ll dive deep into CDK constructs, apps, stacks, and the deployment process.

## Introduction To AWS CDK

AWS CDK is an open-source framework that lets you model and provision AWS cloud resources using the programming language of your choice. It enables you to model application infrastructure using TypeScript, Python, Java, or .NET. Behind the scenes, it uses AWS CloudFormation to provision resources in a safe and repeatable manner.

The diagram below shows the infrastructure management workflow with AWS CDK.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb039808-12e8-4799-a64d-8e32587fd909/3-introduction-aws-cloud-development-kit.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb039808-12e8-4799-a64d-8e32587fd909/3-introduction-aws-cloud-development-kit.png" width="800" height="207" sizes="100vw" caption="Infrastructure management workflow using AWS CDK (Source). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb039808-12e8-4799-a64d-8e32587fd909/3-introduction-aws-cloud-development-kit.png'>Large preview</a>)" alt="Infrastructure management workflow using AWS CDK (Source)" >}}

### Benefits Of AWS CDK

CDK offers multiple advantages, making it one of the preferred choices for programmatically managing infrastructure.

- **Easier cloud onboarding**  
CDK lets you leverage your existing skills and tools to build a cloud infrastructure. Developers can use their language of choice and continue using their preferred integrated development environment (IDE) to write a CDK app. CDK also provides various high-level components that can be used to preconfigure cloud resources with proven defaults, helping you build on AWS without needing to be an expert.
- **Faster development process**  
The expressive power of programming languages and features, such as objects, loops, and conditions, can significantly accelerate the development process. Moreover, writing unit test cases for infrastructure components is also possible. Being able to unit test infrastructure code is of immense value, and it bolsters the developer’s confidence whenever they make any changes.
- **Customizable and shareable**  
CDK allows you to extend existing components to create custom components that meet your organization’s security, compliance, and governance requirements. These components can be easily shared around your organization, enabling you to bootstrap new projects with best practices by default rapidly.
- **No context switching**  
You can write your runtime code and define your AWS resources with the same programming language, and you can continue using the same IDE for runtime code and infrastructure development. Moreover, you can visualize your CDK application stacks and resources with the [AWS Toolkit for Visual Studio Code](https://aws.amazon.com/visualstudiocode/). The toolkit provides an integrated experience for developing serverless applications, including a getting-started guide, step-through debugging, and deployment from the IDE.

In the next few sections, I will provide a brief overview of CDK concepts, and then we will use the AWS CDK toolkit to deploy a sample application to an AWS account.

{{% ad-panel-leaderboard %}}

## CDK Constructs

AWS CDK constructs are cloud components that encapsulate configuration detail and glue logic for one or more AWS services. CDK provides a [library](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-construct-library.html) of constructs covering most of the commonly used AWS services and features. You can customize these constructs based on your needs and create reusable components for your organization. You can easily change any of the parameters or encode your own custom construct. In addition to the constructs made available through these libraries, CDK provides one-to-one mapping with base-level AWS CloudFormation resources, providing a way to define it with a programming language. These resources provide complete coverage and make it possible to provision any AWS resource using CDK.

AWS CDK supports TypeScript, JavaScript, Python, Java, C# and .NET, and (in developer preview) Go. A construct represents a cloud component and encapsulates everything that AWS CloudFormation needs to create the component. When CDK objects are initialized in your CDK application, they are compiled into a YAML template that is deployed as an AWS CloudFormation stack.

The CDK constructs library includes all of the resources available on AWS. For example, `s3.Bucket` represents an Amazon S3 bucket, and `sqs.Queue` represents an Amazon SQS queue. The library contains three different levels of constructs: L1, L2, and L3.

### L1 Constructs

The low-level constructs, L1, are comprised of CloudFormation resources. These constructs directly represent all of the resources available in AWS CloudFormation. For example, the `s3.Bucket` class represents an Amazon S3 bucket, and the `dynamodb.Table` class represents an Amazon DynamoDB table. Let’s take a few examples of L1 constructs to understand how they can be defined in a CDK application.

#### S3 Bucket Construct

The following code snippet can be used to create an S3 bucket and attach a policy to it that grants `GetObject` permission to the AWS account’s root user. In this example, we are using the `addToResourcePolicy` method to attach an IAM `PolicyStatement` to the bucket in order to provide fine-grained permissions:

<pre><code class="language-javascript">import * as s3 from "@aws-cdk/aws-s3";
import &#42; as iam from "@aws-cdk/aws-iam";

const bucket = new s3.Bucket(this, "CdkPlayBucket");
const result = bucket.addToResourcePolicy(
  new iam.PolicyStatement({
    actions: ["s3:GetObject"],
    resources: ["&#42;"],
    principals: [new iam.AccountRootPrincipal()],
  })
);
</code></pre>

#### DynamoDB Construct

The following code snippet can be used to create a DynamoDB table and attach autoscaling rules to it:

<pre><code class="language-javascript">import &#42; as dynamodb from "@aws-cdk/aws-dynamodb";

const table = new dynamodb.Table(this, "CdkPlayTable", {
  partitionKey: { name: "id", type: dynamodb.AttributeType.STRING },
  billingMode: dynamodb.BillingMode.PAY_PER_REQUEST,
});

const readScaling = table.autoScaleReadCapacity({
  minCapacity: 1,
  maxCapacity: 50,
});

readScaling.scaleOnUtilization({
  targetUtilizationPercent: 50,
});
</code></pre>

The examples above demonstrate the power of L1 constructs and how they can be used to string together resources and configurations for your application.

### L2 Constructs

The next level of constructs, L2, represent AWS resources with a higher-level intent-based API. They provide some defaults, boilerplate code, and glue logic, along with the low-level L1 constructs. For example, `bucket.addLifeCycleRule()` represents an S3 bucket with a lifecycle rule added to it. The code snippet below shows how it can be done:

<pre><code class="language-javascript">bucket.addLifecycleRule({
  abortIncompleteMultipartUploadAfter: Duration.days(7),
  enabled: true,
  id: 'BucketLifecycleRule'
})
</code></pre>

Additionally, you can add a [CORS rule](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) to the bucket by using the `addCorsRule` construct. These rules are useful when you need to access the objects in a bucket from a third-party domain.

<pre><code class="language-javascript">bucket.addCorsRule({
  allowedMethods: [
    s3.HttpMethods.GET,
    s3.HttpMethods.POST,
    s3.HttpMethods.PUT,
  ],
  allowedOrigins: ["https://smashingmagazine.com"],
  allowedHeaders: ["*"],
});
</code></pre>

### L3 Constructs

The highest level of constructs, L3, is also called *patterns*. These constructs are designed to help you complete common tasks in AWS, often involving multiple kinds of resources. For instance, `aws-apigateway.LambdaRestApi` represents an AWS API Gateway API that is backed by an AWS Lambda function. The code snippet below shows how it can be used.

**Note:** We are creating a `lambda.Function` with inline code that is being passed to the `LambdaRestApi` method in order to connect it with the API Gateway.

<div class="break-out">

<pre><code class="language-javascript">const backend = new lambda.Function(this, "CDKPlayLambda", {
  code: lambda.Code.fromInline(
    'exports.handler = function(event, ctx, cb) { return cb(null, "success"); }'
  ),
  handler: "index.handler",
  runtime: lambda.Runtime.NODEJS_14_X,
});
const api = new apigateway.LambdaRestApi(this, "CDKPlayAPI", {
  handler: backend,
  proxy: false,
});

const items = api.root.addResource("items");
items.addMethod("GET"); // GET /items
items.addMethod("POST"); // POST /items
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## CDK Stacks And Apps

AWS CDK apps are composed of building blocks known as constructs, which are combined together to form stacks and apps.

### CDK Stacks

A stack is the smallest deployable unit in AWS CDK. All of the resources defined in a stack are provisioned as a single unit. A CDK stack has the same [limitations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html) as AWS CloudFormation. You can define any number of stacks in your AWS CDK app. The code snippet below shows the scaffolding for a sample stack:

<pre><code class="language-javascript">import &#42; as cdk from "@aws-cdk/core";
export class CdkPlayStack extends cdk.Stack {
  constructor(scope: cdk.App, id: string, props?: cdk.StackProps) {
    super(scope, id, props);
    // resources
  }
}
</code></pre>

### CDK Apps

As discussed above, all constructs that represent AWS resources must be defined within the scope of a stack construct. We need to initialize the stack and define it in some scope to deploy it. To define the stack within the scope of an application, we can use the `App` construct. The code snippet below instantiates `CdkPlayStack` and produces the AWS CloudFormation template that the stack defined.

<pre><code class="language-javascript">import { App } from "@aws-cdk/core";
import { CdkPlayStack } from "./cdk-play-stack";

const app = new App();
new CdkPlayStack(app, "hello-cdk");
app.synth();
</code></pre>

## Using the CDK Toolkit

AWS provides a CLI tool, which is the primary way to interact with your AWS CDK application. It builds, synthesizes, and deploys the resources defined in your CDK application.  

### Create the App

The `cdk init` command can be used to initialize a new application in the language of your choice. Each CDK app maintains its own set of module dependencies and should be created in its own directory. For example, we can create a TypeScript CDK application with the `sample-app` template by using the following command:

<pre><code class="language-javascript">cdk init sample-app --language=typescript
</code></pre>

Executing this command will generate several files, but the file that interests us the most is `lib/cdk-init-stack.ts`, which contains a single stack with a few constructs initialized in it. The code snippet below shows the stack that was generated for us:

<pre><code class="language-javascript">import * as sns from '@aws-cdk/aws-sns';
import * as subs from '@aws-cdk/aws-sns-subscriptions';
import * as sqs from '@aws-cdk/aws-sqs';
import * as cdk from '@aws-cdk/core';

export class CdkInitStack extends cdk.Stack {
  constructor(scope: cdk.App, id: string, props?: cdk.StackProps) {
    super(scope, id, props);
    const queue = new sqs.Queue(this, 'CdkInitQueue', {
      visibilityTimeout: cdk.Duration.seconds(300)
    });
    const topic = new sns.Topic(this, 'CdkInitTopic');
    topic.addSubscription(new subs.SqsSubscription(queue));
  }
}
</code></pre>

The `cdk init` command also initializes the project as a Git repository, along with the `.gitignore` file. Apart from that, it generates a `package.json` file for managing project dependencies and a `tsconfig.json` file for TypeScript configuration.

Once you have initialized the project, you can run the `build` command to manually compile the app. This step isn’t mandatory, because the `cdk` toolkit does it for you before you deploy the changes, but a manual build can sometimes help in catching syntax errors. Here’s how it can be done:

<pre><code class="language-bash">npm run build
</code></pre>

Moreover, we saw earlier that the project was initialized with a single stack. We can verify the same by executing the following command:

<pre><code class="language-bash">cdk ls
</code></pre>

The `ls` command should return the name of our app’s directory as the name of the stack. Moreover, we can check the changes made since the last deployment by using the `cdk diff` command.

### Synthesize An AWS CloudFormation Template

Once we are done making changes to our stack, we can use the `synth` command to synthesize the stack to an AWS CloudFormation template. If our application contains multiple stacks, we will need to specify the name of the stack when executing the `synth` command. Here’s how we synthesize the stack:

<pre><code class="language-bash">cdk synth
</code></pre>

This generates a `cdk.out` file, containing a YAML-formatted template, with the resources defined in the stack converted to the equivalent AWS CloudFormation template. The beginning of the YAML output is shown below:

<pre><code class="language-javascript">Resources:
  CdkPlayQueue78BDD396:
    Type: AWS::SQS::Queue
    Properties:
      VisibilityTimeout: 300
    UpdateReplacePolicy: Delete
    DeletionPolicy: Delete
    Metadata:
      aws:cdk:path: CdkPlayStack/CdkPlayQueue/Resource
    </code></pre>

The YAML template generated by `cdk synth` is a perfectly valid AWS CloudFormation template, and it can be deployed either manually via the console or by using any other tool. CDK toolkit also supports the deployment of the template, and the next section describes how it can be done.

### Deploy The Stack

Before trying to deploy the stack, make sure that you have the AWS CLI installed and that your AWS credentials are configured on your device. Refer to the [quick-start document](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html) for more details on how to set up your credentials.

Finally, in order to deploy the stack using AWS CloudFormation, we will have to execute the following command:

<pre><code class="language-bash">cdk deploy
</code></pre>

Similar to the `synth` command, we don’t need to specify the name of the stack if our application contains a single stack. If our stack results in any sensitive policy changes in our account, then the toolkit will confirm those changes before proceeding with the deployment. The screenshot below shows the confirmation prompt when we try to deploy the stack:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7a2b3f7-bfb5-461c-9dec-17f3e399e1e6/4-introduction-aws-cloud-development-kit.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7a2b3f7-bfb5-461c-9dec-17f3e399e1e6/4-introduction-aws-cloud-development-kit.png" width="800" height="215" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7a2b3f7-bfb5-461c-9dec-17f3e399e1e6/4-introduction-aws-cloud-development-kit.png'>Large preview</a>)" alt="The screenshot shows the confirmation prompt when we try to deploy the stack." >}}

The toolkit displays the progress of deployment, and once the deployment succeeds, we can visit the AWS CloudFormation console to see how it lists our stack. Also, if you check the SNS and SQS consoles, you will find the respective resources created for you.

**Note:** If you don’t see the resources or the stack, make sure that the region selected in the AWS console matches the region that you configured using the CLI.

The commands described above are some of the most commonly used toolkit commands. For a detailed overview of other commands, refer to the [official documentation](https://docs.aws.amazon.com/cdk/latest/guide/cli.html).

## Conclusion

This article provided a quick overview of manual and programmatic deployment processes. Also, we talked about the different IaC options available, based on the cloud provider you are using, and then we went into detail on using AWS CDK to programmatically manage your AWS infrastructure. As we’ve seen, CDK offers multiple advantages over traditional techniques. It allows you to use logical statements and object-oriented techniques when modeling a system. You can define high-level abstractions, share them, and publish them to your team, company, or community. Moreover, the infrastructure project can be organized into logical modules and reused as a library. In addition to these benefits, CDK also makes the infrastructure code testable by using industry-standard protocols. It lets you leverage the existing code-review workflow for your infrastructure project.

Also, we saw how you can use the AWS CDK toolkit to interact with the CDK app. The toolkit allows you to synthesize the stacks to the AWS CloudFormation template and to deploy it to an AWS account. The complete source code of the sample CDK application that was used in this article can be found [on GitHub](https://github.com/maskaravivek/CdkPlay). Moreover, you can refer to the [cdk-samples repository](https://github.com/maskaravivek/cdk-samples) for more examples of CDK-based stacks.

We also saw a few examples of the AWS Construct Library and how you can use L1, L2, and L3 constructs to glue together the system architecture. The AWS Construct Library reduces the complexity involved in integrating various AWS services for your application.

{{< signature "vf, yk, il, al" >}}
