---
title: 'Billing Management For Your Next SaaS Idea Using Stripe And Azure Functions'
slug: billing-management-saas-stripe-azure-functions
author: nwani-victory
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/346f3641-b7be-486d-8ac9-327ffe00e232/billing-management-saas-stripe-azure-functions.jpg
date: 2021-12-17T13:30:00.000Z
summary: >-
  In every software-as-a-service solution, user billing and payments are key aspects in the sale of services rendered. Let’s learn about Stripe and how the REST API can be programmatically used in serverless functions to manage the billing for an application.
description: >-
  In every software-as-a-service solution, user billing and payments are key aspects in the sale of services rendered. Let’s learn about Stripe and how the REST API can be programmatically used in serverless functions to manage the billing for an application.
categories:
  - API
  - Apps
  - Auth0
  - React
  - Tutorials
  - Serverless
---

To follow the steps in this tutorial, you should have the following:

- a Stripe account (you can [create](https://dashboard.stripe.com/register) one for free and use the test mode to avoid incurring any charges while following the steps in this article);
- a basic understanding of JavaScript and React;
- an Auth0 account (you can [sign up](https://auth0.com/signup?place=header&type=button&text=sign%20up) for a free one).

## Introduction

Delivering a solution to users through [software as a service](https://www.salesforce.com/in/saas/) (Saas) often entails making use of cloud providers to host and deliver your entire infrastructure, usually comprising a back end and a front-end client. To offset the charges incurred from your cloud providers, a proper billing model for your users is needed in certain cases. In other scenarios, you might have products or services that you want to sell.

The two applications in the aforementioned scenarios share a functional requirement, which is the **ability to process the user’s payment**. To achieve this, the developer could leverage an external payment infrastructure, such as [Stripe](https://stripe.com/), [Square](https://squareup.com/us/en), or [Amazon Pay](https://pay.amazon.com/), among many others.

In this article, we’ll look at Stripe and use its [REST API](https://stripe.com/docs/api) through Stripe’s [Node.js package](https://www.npmjs.com/package/stripe) to build an API layer comprising Azure Functions apps that can be executed by an HTTP trigger from a web, mobile, or desktop client. The API layer and the endpoints accessible through each of the functions are depicted in the diagram below.

**Note**: An Azure Functions app is an individual serverless function deployed and managed using the Azure Functions service. As depicted in the diagram below, a single project can comprise several Azure Functions apps.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f767369a-7560-4333-a849-5b035e151c0a/azure-functions-api-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f767369a-7560-4333-a849-5b035e151c0a/azure-functions-api-architecture.png" width="800" height="211" sizes="100vw" caption="High-level diagram of the API comprising Azure Functions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f767369a-7560-4333-a849-5b035e151c0a/azure-functions-api-architecture.png'>Large preview</a>)" alt="High-level diagram of the API comprising Azure Functions" >}}

After building the API, we will clone an existing web application, built using React to display art paintings for sale. The APIs above will be used to retrieve the paintings as individual products, and the other endpoints will be used to handle payments.

**Note**: While this article makes use of [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/) as a provider of serverless functions, you can reuse the logic in your preferred provider, such as AWS’ [Lambda](https://aws.amazon.com/lambda/) or Google’s [Cloud Functions](https://cloud.google.com/functions).

## Stripe Objects

Before going further, we should understand the Stripe objects that we’ll be creating in this article and what they represent. Below is a list of the five objects we will be working with:

1. [subscription](https://stripe.com/docs/api/subscriptions)  
A `subscription` object is created to charge users at intervals specified by the `billing_period` in the `price` object attached to the product. In this tutorial, we will have a product with a recurring price type, and we will subscribe users to it using the `subscription` object.

2. [product](https://stripe.com/docs/api/products)  
A `product` object is used to represent a single item or service being sold, and the price of the product is stored in the `price` object. In this article, we will create a product using Stripe’s admin dashboard, then retrieve it through the Stripe API.

3. [price](https://stripe.com/docs/api/prices)  
The `price` object is used to hold the price-related details of a product, such as currency, price, and billing cycle. In this article, we will again create the `price` object using Stripe’s admin dashboard, then retrieve it through the Stripe API.

4. [payment method](https://stripe.com/docs/api/payment_methods)  
A `payment_method` object on Stripe is used to hold a customer’s payment details. In this tutorial, we will create a payment method on each transaction and use it together with a `payment_intent` object.

5. [payment intent](https://stripe.com/docs/api/payment_intents/object)  
A `payment_intent` object is created to track the payment for a product from when it was created to when the payment is finally received. Each `payment_intent` object contains a `status` field to record the stage at which the payment is. In this article, we will use a `payment_intent` when a user purchases a product with a one-time pricing type.

{{% feature-panel %}}

## Creating a Stripe Profile for Your Business Idea

The first step to using Stripe is to create an account with your email address and a password, using Stripe’s online dashboard.

Creating a Stripe account will launch the new business in test mode. We can liken test mode to your local development mode, because it allows you to create Stripe objects and test them using test credit cards provided by Stripe, without incurring charges.

As shown in the Stripe dashboard for the sample application below, you can fill in an account name and other details to customize your service.  

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60334aa4-eec9-4348-a2fe-7be921b3b687/stripe-business-dashboard.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60334aa4-eec9-4348-a2fe-7be921b3b687/stripe-business-dashboard.png" width="800" height="384" sizes="100vw" caption="Stripe business admin dashboard for a new account. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60334aa4-eec9-4348-a2fe-7be921b3b687/stripe-business-dashboard.png'>Large preview</a>)" alt="Stripe business admin dashboard" >}}

The image above shows the dashboard for our newly created account. Note the highlighted box in the image above, because the section contains the keys that you would use when programmatically working with the Stripe account either through the API or a supported client library.

**Note**: Store the secret key in a secure notepad, because we will be using them when working with Stripe through a Node.js package from an Azure function in the next section.

## Creating Sample Products on Stripe

To create a `product` object in Stripe, we can either use the REST API or Stripe’s web admin dashboard. In our case, the application’s owner is the sole manager of the products being sold; hence, we will use Stripe’s admin dashboard to create some sample products to be displayed in the demo application.

**Note:** When using [Stripe’s Node.js package](https://stripe.com/docs/api), the [`product` method](https://stripe.com/docs/api/products/object) is used to perform CRUD operations on a `product` object.

Using the top navigation bar in the Stripe dashboard’s home page, click the “Products” tab to navigate to the “Products” page. On the “Products” page, click the “Create Product” button at the top to create your first product in this Stripe business account.

On the page for creating a product, write “Gallery Subscription” in the “Name” input field. Write some brief text in the “Description” input field, to be used as the product information. And put “150” in the “Price” input field, to be used as the price of the new product, as shown below.

**Note:** You can also click the “Image” box on the “Create Product” page to pick an image from your device to use as the image of the product.

The image below shows the input fields on the “Create Product” page for the sample product we’re creating.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6936f070-35c8-4753-968c-3a5318aa478c/stripe-create-recurring-product.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6936f070-35c8-4753-968c-3a5318aa478c/stripe-create-recurring-product.png" width="800" height="450" sizes="100vw" caption="Stripe will create a product with a recurring price type. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6936f070-35c8-4753-968c-3a5318aa478c/stripe-create-recurring-product.png'>Large preview</a>)" alt="Stripe will create a product with a recurring price type" >}}

From the image above, we can see that the “Recurring” option in the “Pricing details” is selected. This means that when a user is subscribed to this product, Stripe will automatically attempt to renew the subscription for the product at the end of the “billing period” specified in the “Pricing details” secton shown above. Click the “[Save Product](https://stripe.com/docs/issuing/testing)” button to save and continue.

After saving the product, you will be redirected back to the “Products” page. Click the “Create Product” button again to create a product, specifying different information for the “Name”, “Description”, and “Pricing details”. This time, select the “One time” box in the “Pricing details” to enable a user to purchase this item once without being charged again for it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b75d37f-f6c3-41de-9773-823a2a20d7ba/stripe-create-onetime-product.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b75d37f-f6c3-41de-9773-823a2a20d7ba/stripe-create-onetime-product.png" width="800" height="" sizes="100vw" caption="Stripe will create a product with a one-time price type. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b75d37f-f6c3-41de-9773-823a2a20d7ba/stripe-create-onetime-product.png'>Large preview</a>)" alt="Stripe will create a product with a one-time price type" >}}

The image above shows a new product being created with a “one-time” price type. Notice that the “Billing period” dropdown menu is removed when the “One time” option is selected, unlike the first product that we created with a “Recurring” pricing type.

**Note**: You can continue to create more products with different names, descriptions, and pricing details, to populate the products in your Stripe business account.

## Creating Azure Functions

[Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/) are functions provided by [Azure](https://azure.microsoft.com/en-us/) for managing serverless event-driven code that can be executed through a defined [event trigger](https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=csharp). All Azure functions that we’ll create in this article will use the [HTTP trigger](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook), which enables a function to be triggered by making an HTTP request to the function’s URL endpoint.

All programmatic operations with Stripe in this article will be done using Stripe’s [npm library](https://www.npmjs.com/package/stripe) for a Node.js environment. Serverless functions are used in this article to cover use cases for small applications, using a [JAMstack](https://jamstack.org/) architecture without a back-end service.

Azure functions can be developed either through the [Azure portal](https://azure.microsoft.com/en-us/features/azure-portal/) or locally on your computer. All Azure functions in this article will be developed and executed locally using Azure’s [Core Tools](https://github.com/Azure/azure-functions-core-tools#linux) command-line interface (CLI). Execute the command below to install Azure’s Core Tools globally on your computer using npm.

<pre><code class="language-bash">npm i -g azure-functions-core-tools@3 --unsafe-perm true</code></pre>

Next, run the commands below to create a new project directory to store the Azure Functions files and to bootstrap the Azure Functions project using the Core Tools CLI.

<pre><code class="language-bash">
# Create a new directory
mkdir stripe-serverless-api

# Change into new directory
cd stripe-serverless-api

# Bootstrap Azure Functions project
func new --language='javascript' --worker-runtime='node' --template="HTTP trigger"
--name="products"
</code></pre>

The commands above will create a `stripe-serverless-api` project directory on your computer. Also, using the parameters passed to the Core Tools CLI, we created an Azure Functions app with an HTTP trigger template using a Node.js runtime with JavaScript.

We can start our new Azure function from the CLI to listen to HTTP requests through localhost on port `5050`.

**Note**: When using the HTTP trigger for an Azure Functions app, the function can be invoked via the function app’s name appended to the endpoint. An example of the products function app created above is `<FUNCTIONS_ENDPOINT>/products`.

<pre><code class="language-bash">func start -p 5050</code></pre>

Before we begin implementing the Azure functions, let’s install the two dependencies below, to be used within the Azure functions.

<pre><code class="language-bash">yarn add stripe dotenv</code></pre>

Stripe’s Node.js package, installed above, will be used to interact with the Stripe API. And [dotenv](https://www.npmjs.com/package/dotenv) will be used to load Stripe’s secret credentials, used in the Azure functions that will be created next.

Create a `.env` file to store the Stripe credentials copied from the Stripe dashboard in the format below, replacing the placeholder in angled brackets with the appropriate value.

<pre><code class="language-bash">// .env

STRIPE_SECRET_KEY=&lt;STRIPE_SECRET_KEY&gt;
</code></pre>

The Stripe credentials stored above will be used to authenticate the Stripe package with the Stripe API. These credentials are sensitive and should be privately stored. To prevent them from getting pushed when the entire project is pushed to a GitHub repository, create a `.gitignore` file and add the `.env` file name.

<pre><code class="language-bash">// .gitignore
.env</code></pre>

At this point, the Azure Functions project is fully set up, and we can now proceed to build the individual apps within the project. We will proceed with implementing the logic in the Azure Functions apps, starting with the products function app.

### Products Function

The purpose of this Azure function is to accept a `GET` HTTP request, and then respond with JSON data containing all products in the Stripe account.

Using your code editor, open the `index.js` file in the `products` directory that was made when you created the Azure Functions project. Add the code block below to the `index.js` file to retrieve all products created in Stripe.

<pre><code class="language-javascript">require("dotenv").config();

const stripe = require("stripe")(process.env.STRIPE_SECRET_KEY);
const headers = {
  "Access-Control-Allow-Methods": "*",
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers": "Content-Type",
  "Content-Type": "application/json",
};

module.exports = async function (context, req) {
  try {
    const { data } = await stripe.products.list({});
    context.res = {
      headers,
      body: {
        data,
      },
    };
  } catch (e) {
    context.res = {
      headers,
      body: e,
    };
  }
};
</code></pre>

The exported function in the code block above uses the [`list`](https://stripe.com/docs/api/products/list) method to list all products created in the account belonging to the `STRIPE_SECRET_KEY` variable being used.

Once the promise from the asynchronous `list` method is resolved, the data array is destructured and sent back (alongside some request headers) as the response to the request, by setting the body within the [`context`](https://stripe.com/docs/api/products/list) object.

To test the function implemented above, open a new CLI and execute the command below, which makes a `GET` HTTP request, using [cURL](https://curl.se), to the Azure functions running in a separate terminal.

<pre><code class="language-bash">curl http://localhost:4040/api/customer</code></pre>

After executing the command above, a JSON response will be returned to your console containing the previously created products.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9684cd28-874a-4905-b9e7-058c35dd73dd/1-product-function-response.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9684cd28-874a-4905-b9e7-058c35dd73dd/1-product-function-response.png" width="800" height="450" sizes="100vw" caption="JSON data response prints out the console from an HTTP request to the products function. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9684cd28-874a-4905-b9e7-058c35dd73dd/1-product-function-response.png'>Large preview</a>)" alt="JSON data response prints out the console from an HTTP request to the products function" >}}

### Price Function

As shown in the fields returned from the products function above, the price details of a product are not included in the `product` object. To get the price details of a product, we need to fetch the `price` object associated with the product. This will be the job of the price function, because each time it is executed, it will return the `price` object associated with a product.

To create a new Azure Functions app, copy the the existing `products` folder, and paste it in the same directory as a duplicate. Then, rename the duplicated folder to `price`.

Using your code editor, open the `index.js` file in the new `price` directory, and replace the existing function with the contents of the code block below, which implements the price function:

<pre><code class="language-javascript">require("dotenv").config();

const stripe = require("stripe")(process.env.STRIPE_SECRET_KEY);
const headers = {
  "Access-Control-Allow-Methods": "*",
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers": "Content-Type",
  "Content-Type": "application/json",
};

module.exports = async function (context, req) {
  const { product } = req.query;

  try {
    const { data } = await stripe.prices.list({
      product,
    });
    context.res = {
      headers,
      body: {
        data : data[0],
      },
    };
  } catch (e) {
    context.res = {
      headers,
      body: e,
    };
  }
};
</code></pre>

The `price` function app above accepts a `GET` HTTP request that contains a product in the `query` parameter with the value of a product’s ID. The [`list`](https://stripe.com/docs/api/prices/list) method on the `price` object is used to retrieve prices within a Stripe account. The `product` parameter passed to the `list` method restricts the prices retrieved to the ones associated with the `product` object whose ID has been passed to the `list` method.

Once the promise from the `list` method is resolved, the data array from the `list` method is destructured, and only the first object within the data array is sent back as the request response.

**Note:** Only the first object from the data array is sent back because we want to display only one price entity. A product may have several `price` objects attached it, but for this application, we will use only one.

To test the function implemented above, execute the command below, which sends a `GET` HTTP request containing a product ID in a `request` parameter to the Azure functions running in a separate terminal.

**Note:** You can find the ID of a product in the Stripe dashboard. Navigate to the “Products” page, and click a product to view its details. In the details displayed, you will find the ID of the product.

<pre><code class="language-bash">curl http://localhost:4040/api/price?product="prod_JudY3VFuma4zj7"</code></pre>  

Once you execute the command above, a JSON response will be returned to your console with an object containing the `price` object of a product.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ca10bc6-dc5c-401b-b757-a8867150f162/price-function-response.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ca10bc6-dc5c-401b-b757-a8867150f162/price-function-response.png" width="800" height="450" sizes="100vw" caption="JSON data response prints out the console from an HTTP request to the price function. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ca10bc6-dc5c-401b-b757-a8867150f162/price-function-response.png'>Large preview</a>)" alt="JSON data response prints out the console from an HTTP request to the price function" >}}

From the response shown in the sample above, we can see the price details of the product, including the currency, type, and recurring data.

### Purchase Function

The purchase function app will be used either to make a one-time purchase of a product or to subscribe a user to a product. Either of these two operations involves charging a user via their bank card.

To create a new function app within the Azure Functions project, copy either the existing products or the `price` folder, and paste it in the same directory as a duplicate. Then, rename the duplicated folder to `purchase`.

In your code editor, add the contents of the code block below in the `index.js` file, which will handle a `POST` request to create either a subscription or a one-time purchase for a user.

<pre><code class="language-javascript">// ./purchase/index.js
require("dotenv").config();

const stripe = require("stripe")(process.env.STRIPE_SECRET_KEY);
const headers = {
  "Access-Control-Allow-Methods": "*",
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers": "Content-Type",
  "Content-Type": "application/json",
};

module.exports = async function (context, req) {
  const {
    number,
    purchaseCurrency,
    cvc,
    exp_month,
    exp_year,
    purchaseAmount,
    email,
    purchaseType,
    priceEntityId,
  } = req.body;

  try {
    // Create a payment method for user using the card details
    const { id: paymentID } = await stripe.paymentMethods.create({
      type: "card",
      card: {
        number,
        cvc,
        exp_year,
        exp_month,
      },
    });

    const { id: customerID } = await stripe.customers.create({
      email,
      description: "Artwork gallery customer",
      payment_method: paymentID,
    });

    await stripe.paymentMethods.attach(paymentID, { customer: customerID });
    if (purchaseType === "recurring") {
      const subscriptionData = await stripe.subscriptions.create({
        customer: customerID,
        default_payment_method: paymentID,
        items: [
          {
            price: priceEntityId,
          },
        ],
      });
      context.res = {
        headers,
        body: {
          message: "SUBSCRIPTION CREATED",
          userStripeId: customerID,
          userSubscriptionId: subscriptionData.id,
        },
      };
    } else {
      const { id: paymentIntentId } = await stripe.paymentIntents.create({
        amount: purchaseAmount,
        currency: purchaseCurrency || "usd",
        customer: customerID,
        payment_method: paymentID,
      });
      const { amount_received } = await stripe.paymentIntents.confirm(
        paymentIntentId,
        {
          payment_method: paymentID,
        }
      );
      context.res = {
        headers,
        body: {
          message: `PAYMENT OF ${amount_received} RECIEVED`,
        },
      };
    }
  } catch (e) {
    context.res = {
      status: 500,
      body: e,
    };
  }
};
</code></pre>

The function app in the code block above uses the Stripe package to create either a one-time payment or a subscription for a user based on the `purchaseType` value gotten from the request body. Here is a run down of what happened above:

- First, a `payment_method` entity is created using the credit card number, name, CVC, and expiration details, destructured from the data sent in the function’s request body.
- Next, a customer is created in Stripe using the `email` value sent in the request body, a description, and the payment method previously created. The `customer` object is also attached to the `payment_method` entity by using the `attach` method and specifying the `payment_method` ID string that was returned when the payment method was created, and specifying a `customer` option with the customer ID that was returned when the `customer` entity was created.
- The last part of the function handler has an `if` condition that evaluates the `purchaseType` value sent in the request body. If the `purchaseType` value is recurring, then the `subscription` entity would contain the customer ID returned from the `customer` entity, a `default_payment_method` with the value of the `payment_method` ID returned from the `payment` entity, and an `items` array with a single `item` object containing the ID of a `price` entity.

{{% ad-panel-leaderboard %}}

## Expanding the Demo Web Application

A web application built using [React](https://reactjs.org/) will serve as the web client that directly accesses the Azure Functions apps that we’ve built up to now. As explained earlier, the interface has already been built, and the data has been retrieved from a mock JSON file. We will only make some minimal changes and add the HTTP requests to use the Azure Functions endpoint.

Clone the web application from the [GitHub repository](https://github.com/vickywane/stripe-art-app.git) by executing the Git command below from your local CLI:

<pre><code class="language-bash">git clone https://github.com/vickywane/stripe-art-app.git</code></pre>

Next, move into the cloned application’s directory and install the dependencies listed in the `package.json` file.

<pre><code class="language-bash"># change directory
cd stripe-art-app

# install dependencies
yarn install</code></pre>

Once the dependencies have been installed, run the `yarn start` command from your CLI to view the home page of the web application from your web browser at `http://localhost:3000`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9469cf13-1a2d-413f-9a79-1f6fa17399cf/gallery-application-home-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9469cf13-1a2d-413f-9a79-1f6fa17399cf/gallery-application-home-page.png" width="800" height="450" sizes="100vw" caption="Home page of the gallery application displaying artwork from local mock.json file. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9469cf13-1a2d-413f-9a79-1f6fa17399cf/gallery-application-home-page.png'>Large preview</a>)" alt="Home page of the gallery application displaying artwork from local mock.json file." >}}

Before diving into the code base of the web application, let’s note a few things about the existing structure of the application.

First, user management, including authentication and the storing of a user’s personal data from the application, was implemented using [Auth0](https://auth0.com/) through the use of the [auth0-react](https://www.npmjs.com/package/@auth0/auth0-react) SDK for React applications.

To use Auth0 in the cloned application, we need to supply the credentials from an Auth0 [single-page application](https://auth0.com/docs/quickstart/spa) type in the `.env` file within the web application folder in the format shown below.

**Note**: See the [Auth0 quickstart guide](https://auth0.com/docs/quickstart/spa/react) for more details on how to get started with a single-page application.

<pre><code class="language-bash"># ./env

REACT_APP_AUTHO_DOMAIN=&lt;AUTH0_DOMAIN&gt;
REACT_APP_AUTHO_SECRET_KEY=&lt;AUTH0_SECRET&gt;
REACT_APP_FUNCTION_ENDPOINT="http://localhost:5050/api"</code></pre>

The `REACT_APP_FUNCTION_ENDPOINT` defined in the `.env` file above will be accessed with the application components to make HTTP requests to the running function apps. Currently, the Azure Functions apps are being served locally on your computer’s localhost, but this will change to a live URL when the function apps are deployed to Azure Functions.

The second thing to note is that the data of art products displayed on the home page are static, retrieved from a JSON file in the `data` directory.

In this part of this article, we will extend the functionalities above as follows:

- **Home page**  
We will refactor the home page to fetch and display products created in Stripe using the `GET` products Azure function created previously, and we will discard the `mock.json` file containing the prototype art products.
- **Checkout page**  
We will build a new checkout page for users who want to purchase either an art print or a subscription with their credit card.

## Home Page

The home page is displayed for all users, whether authenticated or unauthenticated, and it displays a list of all available artwork products, using a child `artworkCard` component exported from the `artworkCard.js` file.

We need to make a few changes to this component, because we want the button in the `artworkCard` component to prompt the user to purchase an artwork. Modify the existing `artworkCard.js` file in the `components` directory with the highlighted portions of the code block below.

<div class="break-out">
 <pre data-line="7-19,36-54"><code class="language-javascript">// ./src/components/artworkCard.js

import { navigate } from "@reach/router";
import React, { useState, useEffect } from "react";

const ArtworkCard = ({ name, description, img_uri, productId }) =&gt; {
  const [priceData, setPriceData] = useState({});

  useEffect(() =&gt; {
    (async () =&gt; await fetchPrice())();
  }, []);

  const fetchPrice = async () =&gt; {
    const res = await fetch(
      '${process.env.REACT_APP_FUNCTION_ENDPOINT}/price?product=${productId}'
    );
    const { data } = await res.json();
    setPriceData(data);
  };

  return (
    &lt;div className="artwork-card"&gt;
      &lt;div
        className="card-top"
        style={{
          backgroundImage: 'url(${img_uri})',
        }}
      &gt;&lt;/div&gt;
      &lt;div className="artwork-details"&gt;
        &lt;div className={"align-center"}&gt;
          &lt;h5&gt; {name} &lt;/h5&gt;
        &lt;/div&gt;
        &lt;hr /&gt;
        &lt;div style={{ justifyContent: "space-between" }} className="flex"&gt;
          &lt;div className="align-center"&gt;
          &lt;p&gt; {'$${priceData.unit_amount}'} &lt;/p&gt;
          &lt;/div&gt;
          &lt;div&gt;
            &lt;button
              className="btn"
              onClick={() =&gt;
                navigate('/checkout/${productId}', {
                  state: {
                    name,
                    productId,
                    priceEntityId: priceData.id,
                    price: priceData.unit_amount,
                    purchaseType: priceData.type,
                  },
                })
              }
            &gt;
              Purchase
            &lt;/button&gt;
            &lt;/div&gt;
        &lt;/div&gt;
        &lt;br /&gt;
        &lt;p&gt; {description} &lt;/p&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default ArtworkCard;</code></pre>
</div>

In the highlighted parts of the file above, we introduced a [`useEffect`](https://reactjs.org/docs/hooks-effect.html) hook to make an HTTP request to the price function app to retrieve the `price` object attached to the product being displayed in the card. Once the promise from the `fetch` method is resolved, the data stream is further converted to JSON and stored in the component’s local state.

A button labelled `Purchase` was also added to the `artworkCard` component. When clicked, it navigates the user to the checkout page, where the user can input their bank card details to purchase the product.

In your code editor, open the `Home.js` file in the `pages` directory, and modify it with the highlighted portions of the code block below, which will fetch all available products in Stripe through the products function app and then display them.

<div class="break-out">
 <pre data-line="11-20,43-52"><code class="language-javascript"># ./src/pages/home.js

import React, { useState, useEffect } from "react";
import Header from "../components/header";
import "../App.css";
import Banner from "../components/banner";
import ArtworkCard from "../components/artworkCard";

const Home = () =&gt; {

  const [artworks, setArtworks] = useState([]);
  useEffect(() =&gt; {
    (async () =&gt; await fetchArtworks())();
  }, []);

  const fetchArtworks = async () =&gt; {
    const res = await fetch(`${process.env.REACT_APP_FUNCTION_ENDPOINT}/products`);
    const { data } = await res.json();
    setArtworks(data);
  };

  return (
    &lt;div style={{ backgroundColor: "#F3F6FC", height: "100vh" }}&gt;
      &lt;Header /&gt;
      &lt;Banner /&gt;
      &lt;br /&gt;
      &lt;br /&gt;
      &lt;div className="page-padding"&gt;
        &lt;div style={{}}&gt;
          &lt;div className="flex"&gt;
            &lt;div className="align-center"&gt;
              &lt;h4&gt; My Rated Art Paints &lt;/h4&gt;
            &lt;/div&gt;
          &lt;/div&gt;
          &lt;p&gt;
            Every artist dips his brush in his own soul, &lt;br /&gt;
            and paints his own nature into his pictures.
          &lt;/p&gt;
        &lt;/div&gt;
        &lt;br /&gt;
        &lt;div&gt;
          &lt;ul className="artwork-list"&gt;
            {artworks.map(({ id, name, img_uri, images, description }) =&gt; (
              &lt;li key={id}&gt;
                &lt;ArtworkCard
                  productId={id}
                  description={description}
                  img_uri={images[0]}
                  name={name}
                /&gt;
              &lt;/li&gt;
            ))}
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default Home;
</code></pre>
</div>

In the code block above, a `GET` request is made as soon as the component is loaded in a `useEffect` hook using the browser’s fetch API. The stream response from the request made is further converted into JSON format, and the data is stored in the local component state for further use.

With this change, the `data.json` file is no longer being used. Also, when you view the web application in your browser, you will find the products created in Stripe displayed in a grid, as shown below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09d59b9f-4892-41f4-9900-3d244e442456/store-app-home-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09d59b9f-4892-41f4-9900-3d244e442456/store-app-home-page.png" width="800" height="450" sizes="100vw" caption="Home page in gallery application displaying all products fetched from Stripe. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09d59b9f-4892-41f4-9900-3d244e442456/store-app-home-page.png'>Large preview</a>)" alt="Home page in gallery application displaying all products fetched from Stripe." >}}

From the details shown in the image above, you will notice that the products displayed on the home page were the ones created at the beginning of this article.

{{% ad-panel-leaderboard %}}

## Checkout Page

Create a `checkout.js` file in the `pages` directory. This new file will contain the component that will be displayed to collect the user’s credit card details, after they are routed to `/checkout` upon clicking the “Purchase” button to purchase an art print.

Add the contents of the code block below to create the checkout component that contains the form elements to collect the credit card details:

<pre><code class="language-javascript"># ./src/pages/checkout.js

import React, { useState } from "react";
import { useAuth0 } from "@auth0/auth0-react";
import Header from "../components/header";
import "../App.css";

const Checkout = (props) =&gt; {
  const { purchaseType, productId, priceEntityId, name, price } =
    props.location.state;

  const [cardNumber, setCardNumber] = useState("");
  const [cardName, setCardName] = useState("");
  const [cvc, setcvc] = useState("");
  const [cardExpiryMonth, setCardExpiryMonth] = useState("");
  const [cardExpiryYear, setCardExpiryYear] = useState("");
  const [loading, setLoading] = useState(false);
  const [paymentSuccess, setPaymentSuccess] = useState(false);
  const { user } = useAuth0();

  const makePayment = async () =&gt; {
    setLoading(true);
    try {
      const res = await fetch(
        `${process.env.REACT_APP_FUNCTION_ENDPOINT}/purchase`,
        {
          method: "POST",
          body: JSON.stringify({
            number: cardNumber,
            exp_month: cardExpiryMonth,
            exp_year: cardExpiryYear,
            purchaseAmount: price,
            purchaseType,
            priceEntityId,
            cvc,
            email: user.email,
          }),
        }
      );

      if (res.status === 200) {
        const { paymentId } = await res.json();
        await fetch(`${process.env.REACT_APP_FUNCTION_ENDPOINT}/billing-data`, {
          method: "POST",
          body: JSON.stringify({
            productId,
            userId: user.sub,
            paymentId,
          }),
        });
        setPaymentSuccess(true);
      }
    } catch (e) {
      console.log(e);
    } finally {
      setLoading(false);
    }
  };

  return (
    &lt;div
      style={{
        height: "100vh",
        background: "#F3F6FC",
      }}
    &gt;
      &lt;Header /&gt;
      &lt;div
        className="product-page-padding"
        style={{
          height: window.innerHeight,
          display: "flex",
          justifyContent: "center",
          alignItems: "center",
        }}
      &gt;
        &lt;div className="align-center"&gt;
          &lt;div className="payment-card"&gt;
            &lt;h5 className="align-center"&gt;
              &lt;b&gt;{name} Checkout &lt;/b&gt;
            &lt;/h5&gt;
            &lt;p&gt;
              &lt;b&gt;Total Price:&lt;/b&gt; {`$${price}`}
            &lt;/p&gt;
            &lt;p&gt;
              &lt;b&gt; Payment Type: &lt;/b&gt; {purchaseType.toUpperCase()}
            &lt;/p&gt;
            &lt;hr /&gt;
            {!paymentSuccess ? (
              &lt;form
                onSubmit={(e) =&gt; {
                  e.preventDefault();
                  makePayment();
                }}
              &gt;
                &lt;h5&gt; Payment Details &lt;/h5&gt;
                &lt;br /&gt;
                &lt;div className="input-container"&gt;
                  &lt;label id="name"&gt; Cardholder Name &lt;/label&gt;
                  &lt;input
                    value={cardName}
                    onChange={(e) =&gt; setCardName(e.target.value)}
                    className="payment-input"
                    placeholder="Bank Cardholder Name"
                    type="text"
                  /&gt;
                &lt;/div&gt;
                &lt;br /&gt;
                &lt;div className="input-container"&gt;
                  &lt;label id="name"&gt; Card Number &lt;/label&gt;
                  &lt;input
                    value={cardNumber}
                    onChange={(e) =&gt; setCardNumber(e.target.value)}
                    className="payment-input"
                    placeholder="Bank Card Numbers"
                    type="number"
                  /&gt;
                &lt;/div&gt;
                &lt;br /&gt;
                &lt;div className="input-container"&gt;
                  &lt;label id="name"&gt; Card CVC &lt;/label&gt;
                  &lt;input
                    value={cvc}
                    onChange={(e) =&gt; setcvc(e.target.value)}
                    className="payment-input"
                    placeholder="Bank Card CVC"
                    type="text"
                  /&gt;
                &lt;/div&gt;
                &lt;br /&gt;
                &lt;div className="input-container"&gt;
                  &lt;label id="name"&gt; Card Expiry Month &lt;/label&gt;
                  &lt;input
                    value={cardExpiryMonth}
                    onChange={(e) =&gt; setCardExpiryMonth(e.target.value)}
                    className="payment-input"
                    placeholder="Bank Card Expiry Month"
                    type="text"
                  /&gt;
                &lt;/div&gt;
                &lt;br /&gt;
                &lt;div className="input-container"&gt;
                  &lt;label id="name"&gt; Card Expiry Year &lt;/label&gt;
                  &lt;input
                    value={cardExpiryYear}
                    onChange={(e) =&gt; setCardExpiryYear(e.target.value)}
                    className="payment-input"
                    placeholder="Bank Card Expiry Year"
                    type="text"
                  /&gt;
                &lt;/div&gt;
                &lt;br /&gt;
                &lt;button
                  disabled={loading}
                  style={{ width: "100%" }}
                  onClick={(e) =&gt; {
                    e.preventDefault();
                    makePayment();
                  }}
                  className="btn"
                &gt;
                  {!loading ? "Confirm" : "Confirming"} My Payment
                &lt;/button&gt;
              &lt;/form&gt;
            ) : (
              &lt;div&gt;
                &lt;br /&gt;
                &lt;h5 className="align-center"&gt;
                  Your {`$${price}`} purchase of {name} was successfull{" "}
                &lt;/h5&gt;
                &lt;br /&gt;
              &lt;/div&gt;
            )}
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default Checkout;
</code></pre>

As described earlier, the form component above contains four input fields for the user to type in their name, number, expiration and CVC details. These details are further stored in the component’s local state, and, upon a click of the “Confirm my payment” button, the stored credit card details are used to purchase the product.

Of particular interest in the checkout component above is the `makePayment` function, because it handles the functionality of the checkout page. When executed, the `makePayment` function sends a `POST` request containing the credit card details in its request body using fetch to the `/purchase` cloud function. Once the first `POST` request is resolved successfully, with a `200` status code indicating a successful payment, a new `POST` request is made to the `/billing-data` cloud function to store the details of the purchased product.

**Note:** As explained when we were designing the `productCard` component, the purchased product details stored in Auth0 will be used to identify products purchased by the user from the home page.

To test this component, we will fill the input fields with the details of one of the [basic test cards](https://stripe.com/docs/testing#cards) provided by Stripe for applications still in test mode, and then click the “Confirm payment” button, as shown below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9db6345e-71ac-4f14-a04b-5c3982f940a1/checkout-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9db6345e-71ac-4f14-a04b-5c3982f940a1/checkout-page.png" width="800" height="450" sizes="100vw" caption="Checkout page in the gallery application displaying fields for inputting a credit card to purchase the selected product. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9db6345e-71ac-4f14-a04b-5c3982f940a1/checkout-page.png'>Large preview</a>)" alt="Checkout page in the gallery application displaying fields for inputting a credit card to purchase the selected product." >}}

**Note:** The credit card used in the image above is one of the [basic test cards](https://stripe.com/docs/testing#cards) provided by Stripe and not a real credit card. Stripe accounts in test mode must use one of the basic test cards.

Once the “Confirm my payment” button in the checkout card is clicked, a payment for the product is made from the credit card provided, and the checkout card interface is changed to reflect the successful response.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb7ad85-7bc1-4b43-85e7-679e1fe13322/payment-successful-response.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb7ad85-7bc1-4b43-85e7-679e1fe13322/payment-successful-response.png" width="800" height="450" sizes="100vw" caption="Checkout page in the gallery application displaying a successful payment response. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb7ad85-7bc1-4b43-85e7-679e1fe13322/payment-successful-response.png'>Large preview</a>)" alt="Checkout page in the gallery application displaying a successful payment response." >}}

Going to the “Reports” section of your Stripe admin dashboard, you will see a reflection of the last payment made when the gallery subscription was created on the checkout page above.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/069f5c27-d12b-40a2-80b2-886249640ac4/stripe-dashboard-statistics.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/069f5c27-d12b-40a2-80b2-886249640ac4/stripe-dashboard-statistics.png" width="800" height="450" sizes="100vw" caption="Home page in Stripe admin dashboard displays $150 as gross volume for the day from last transaction. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/069f5c27-d12b-40a2-80b2-886249640ac4/stripe-dashboard-statistics.png'>Large preview</a>)" alt="Home page in Stripe admin dashboard displays $150 as gross volume for the day from last transaction." >}}

From the charts shown in the image above, taken from the test Stripe card used in this tutorial, you will see that a gross volume of $150.00 was attained once the gallery subscription was created.  

**Note**: The image also shows statistics from test operations that were made on the Stripe account while this article was being developed.

At this point, we have fully set up the entire payment flow. You can repeat the process of creating a product through the Stripe dashboard and purchasing it using the React application or any other client that consumes Azure Functions.

## Summary

Congratulations on completing this hands-on tutorial.

By going through the steps in this tutorial, we have worked with Stripe, Azure Functions, and React. We started by building an API layer that uses the Stripe API through a Node.js package. Then, we moved on to consuming the Azure Functions app endpoints from a web application, using the function app to retrieve products and make payments for the products.

### References

- [Documentation](https://stripe.com/docs), Stripe
- [auth0-react](https://www.npmjs.com/package/@auth0/auth0-react) (SDK for React single-page applications)
- [Auth0](https://auth0.com)

{{< signature "ks, vf, yk, al, il" >}}
