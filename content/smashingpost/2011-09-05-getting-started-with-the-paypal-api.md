---
title: 'Getting Started With The PayPal API'
slug: getting-started-with-the-paypal-api
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d8249a-993e-4542-a8c2-b879184cbde3/paypal-logo.jpeg
date: 2011-09-05T11:19:36.000Z
author: eran-galperin
summary: >-
  In this post, Eran Galperin breaks down some of the techniques and approaches to working with the PayPal API, in order to make integration and troubleshooting simpler and easier. Disclaimer: The author says PayPal’s API is among the worst he’s ever had to deal with.
description: >-
  In this post, Eran Galperin breaks down some of the techniques and approaches to working with the PayPal API, in order to make integration and troubleshooting simpler and easier.
categories:
  - Coding
  - PHP
  - API
---

PayPal is the most popular platform for receiving online payments today. The ease of opening a PayPal account and receiving payments compared to opening a merchant account with a traditional payment gateway is probably the number one reason for its popularity, with a close second being the comprehensive API that PayPal provides for its payment services. In this post, I will break down some of the **techniques and approaches to working with the PayPal API**, in order to make integration and troubleshooting simpler and easier.

<figure><a href="https://www.flickr.com/photos/jeanchristophe/4169501247/"><img loading="lazy" decoding="async" class="111563" title="PayPal at LeWeb, Copyright Jean-Christophe Capelli, Some Rights Reserved" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d8249a-993e-4542-a8c2-b879184cbde3/paypal-logo.jpeg" alt="PayPal at LeWeb, Copyright Jean-Christophe Capelli, Some Rights Reserved" width="500" height="201" /></a><figcaption>PayPal at LeWeb. <a href="https://www.flickr.com/photos/jeanchristophe/4169501247">Image credit</a></figcaption></figure>

**Disclaimer:** PayPal’s API is among the worst I’ve ever had to deal with. Inconsistencies, sometimes poor or conflicting documentation, unpredictable failures and account changes, and major differences between the live and sandbox versions all conspire to make the PayPal API quite a pain in the arse to work with. Over the years, I’ve taken my lumps from working quite a bit with the PayPal API, and I’ve published the results of my hard-learned lessons as a commercial *PHP PayPal API component* on the source-code marketplace Binpress.

{{% feature-panel %}}

## The Different Payment Options

PayPal offers a variety of payment options, which might be confusing at first:

*   **Express Checkout**.<br>
The premier PayPal service. Express Checkout allows you to receive payments without having a merchant account and without having to meet special requirements other than verifying your account (either via a bank account or a credit card). Previously, you could receive Express Checkout payments from PayPal users only, but PayPal has since added a credit-card option for non-PayPal users, making this service accessible to practically anyone with a major credit card. Note that the Express Checkout process occurs on PayPal’s platform and thus can never be fully integrated in your website’s experience.
*   **Direct Payment**.<br>
The Direct Payment method allows you to receive credit-card payments directly through an API call. This enables you to host the payment process on your website in full, which might make for a more complete shopping experience for your customers. The Direct Payment method has several variations that enable you to authorize a payment and complete it at a later date: the appropriately named Authorization and Capture methods. These variations are a part of the Website Payments Pro API, which is available only to US, Canadian and UK accounts.
*   **Recurring Payments**.<br>
This allows you to set up a recurring transaction (i.e. a subscription payment).
*   **Mass Payments**.<br>
This allows you to transfer money to multiple accounts at once.
*   **Adaptive Payments**.<br>
Here is another API for sending funds to multiple recipients, with some differences from the Mass Payments API. (Did I mention that the PayPal API is confusing and a bit redundant?)

This list is not comprehensive, but it covers the main payment options (<a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/howto_api_reference">see the API documentation for more</a>).

### Making API Requests

PayPal supports two main formats over HTTP: NVP and SOAP. NVP is short for Name-Value Pair, and SOAP stands for Simple Object Access Protocol. I will cover the NVP approach, which I prefer to SOAP’s relatively verbose and complex syntax.

Each of the API methods has different parameters, but they all share <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_NVPAPIOverview#id09C2F0G0C7U">some basic parameters</a>, which are used to identify the API account and sign the transaction. These include:

*   `USER`<br>
Your PayPal API user name.
*   `PWD`<br>
Your PayPal API password.
*   `VERSION`<br>
The version number of the NVP API service, such as [74.0](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&content_ID=developer/e_howto_api_nvp_PayPalAPIWhatsNewNVP) (the most recent as of this writing).
*   `SIGNATURE`<br>
Your PayPal API signature string. This parameter is optional if you use a certificate to authenticate.

The last required parameter is <code>METHOD</code>, which declares which API method we are calling.

Requests are made over HTTPS. We’ll use cURL to build our basic request, and then encapsulate the process in a class:

<pre><code class="language-php">class Paypal {
   /**
    * Last error message(s)
    * @var array
    */
   protected $_errors = array();

   /**
    * API Credentials
    * Use the correct credentials for the environment in use (Live / Sandbox)
    * @var array
    */
   protected $_credentials = array(
      'USER' =&gt; 'seller_1297608781_biz_api1.lionite.com',
      'PWD' =&gt; '1297608792',
      'SIGNATURE' =&gt; 'A3g66.FS3NAf4mkHn3BDQdpo6JD.ACcPc4wMrInvUEqO3Uapovity47p',
   );

   /**
    * API endpoint
    * Live - https://api-3t.paypal.com/nvp
    * Sandbox - https://api-3t.sandbox.paypal.com/nvp
    * @var string
    */
   protected $_endPoint = 'https://api-3t.sandbox.paypal.com/nvp';

   /**
    * API Version
    * @var string
    */
   protected $_version = '74.0';

   /**
    * Make API request
    *
    * @param string $method string API method to request
    * @param array $params Additional request parameters
    * @return array / boolean Response array / boolean false on failure
    */
   public function request($method,$params = array()) {
      $this -&gt; _errors = array();
      if( empty($method) ) { //Check if API method is not empty
         $this -&gt; _errors = array('API method is missing');
         return false;
      }

      //Our request parameters
      $requestParams = array(
         'METHOD' =&gt; $method,
         'VERSION' =&gt; $this -&gt; _version
      ) + $this -&gt; _credentials;

      //Building our NVP string
      $request = http_build_query($requestParams + $params);

      //cURL settings
      $curlOptions = array (
         CURLOPT_URL =&gt; $this -&gt; _endPoint,
         CURLOPT_VERBOSE =&gt; 1,
         CURLOPT_SSL_VERIFYPEER =&gt; true,
         CURLOPT_SSL_VERIFYHOST =&gt; 2,
         CURLOPT_CAINFO =&gt; dirname(__FILE__) . '/cacert.pem', //CA cert file
         CURLOPT_RETURNTRANSFER =&gt; 1,
         CURLOPT_POST =&gt; 1,
         CURLOPT_POSTFIELDS =&gt; $request
      );

      $ch = curl_init();
      curl_setopt_array($ch,$curlOptions);

      //Sending our request - $response will hold the API response
      $response = curl_exec($ch);

      //Checking for cURL errors
      if (curl_errno($ch)) {
         $this -&gt; _errors = curl_error($ch);
         curl_close($ch);
         return false;
         //Handle errors
      } else  {
         curl_close($ch);
         $responseArray = array();
         parse_str($response,$responseArray); // Break the NVP string to an array
         return $responseArray;
      }
   }
}</code></pre>

Note that I use a CA certificate file for SSL certificate validation. You can obtain the file from the <a href="https://curl.haxx.se/docs/caextract.html">cURL website</a> or any trusted source. Update the path to the certificate file according to where you’ve placed it.

The response returned will be in NVP format as well, and I reformat it into an array before returning it. A parameter named <code>ACK</code> signifies the status of the request: <code>Success</code> or <code>SuccessWithWarning</code> when the request succeeds, and <code>Error</code> or <code>Warning</code> when the request fails.

A request could fail for many reasons, and there are different reasons for each API method, which are <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_errorcodes">covered in detail in the manual</a>. We’ll go over some further down in this article and look at ways to handle them. Keep in mind that the parameter values are case-sensitive, so code against them accordingly.

## Express Checkout

One of the most popular APIs is the Express Checkout API, which enables you to receive payments without opening a Website Payments Pro account (which is available only to verified US accounts) or hosting the actual transaction yourself (which requires additional security).

The Express Checkout process works as follows:

1.  We request a checkout token from PayPal using the transaction details;
2.  If successful, we redirect the user to the PayPal endpoint using the received token;
3.  The user completes or cancels the payment on the PayPal platform and is redirected back to our website;
4.  We complete the payment either when the user is redirected back or via an [Instant Payment Notification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&content_ID=developer/e_howto_admin_IPNIntro) (IPN).

<figure><img loading="lazy" decoding="async" class="111667" title="Express Checkout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d74906-6e70-4bd8-ae8c-e299a956528c/scr-ukexpresscheckout-cut.gif" alt="Express Checkout flow" width="531" height="301" /></figure>

{{% ad-panel-leaderboard %}}

### 1. Getting the Checkout Token: SetExpressCheckout

We initiate the Express Checkout process by passing the order details to the PayPal API, and we receive a token string that identifies it. This token would be used in the next step to redirect to PayPal.

Here are the required parameters:

*   `METHOD`<br>
This is the API method that we’re using (i.e. `SetExpressCheckout`).
*   `RETURNURL`<br>
The URL that the user will be redirected to after the payment process is completed.
*   `CANCELURL`<br>
The URL that the user will be redirected to after having cancelled the payment process.
*   `PAYMENTREQUEST_0_AMT`<br>
The transaction’s total amount. This must have two decimal places, with the decimal separator being a period (`.`). The optional thousands separator must be a comma (`,`).
*   `PAYMENTREQUEST_0_ITEMAMT`<br>
The total cost of the items in the order, excluding shipping, taxes and other costs. If there are no extra costs, then it should be the same value as `PAYMENTREQUEST_0_AMT`.

We can pass additional parameters to add more information about the order, some of which have default values:

*   `PAYMENTREQUEST_0_CURRENCYCODE`<br>
The payment’s currency, as a three-letter code. The default is USD.
*   `PAYMENTREQUEST_0_SHIPPINGAMT`<br>
The total shipping costs for this order.
*   `PAYMENTREQUEST_0_TAXAMT`<br>
The total tax amount for this order. This is required if per-item tax is specified (see below).
*   `PAYMENTREQUEST_0_DESC`<br>
The order’s description.

We can also add details about individual items in the order:

*   `L_PAYMENTREQUEST_0_NAMEm`<br>
The item’s name.
*   `L_PAYMENTREQUEST_0_DESCm`<br>
The item’s description.
*   `L_PAYMENTREQUEST_0_AMTm`<br>
The item’s cost.
*   `L_PAYMENTREQUEST_0_QTYm`<br>
The quantity of an item.

The variable index <code>m</code> identifies the item. (Use the same variable for all details of the same item.)

There are many other optional parameters, which can be found in the <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout">API documentation</a>.

We’ll use the function that we wrote above to build the <code>SetExpressCheckout</code> request:

<pre><code class="language-php">//Our request parameters
$requestParams = array(
   'RETURNURL' =&gt; 'https://www.yourdomain.com/payment/success',
   'CANCELURL' =&gt; 'https://www.yourdomain.com/payment/cancelled'
);

$orderParams = array(
   'PAYMENTREQUEST_0_AMT' =&gt; '500',
   'PAYMENTREQUEST_0_SHIPPINGAMT' =&gt; '4',
   'PAYMENTREQUEST_0_CURRENCYCODE' =&gt; 'GBP',
   'PAYMENTREQUEST_0_ITEMAMT' =&gt; '496'
);

$item = array(
   'L_PAYMENTREQUEST_0_NAME0' =&gt; 'iPhone',
   'L_PAYMENTREQUEST_0_DESC0' =&gt; 'White iPhone, 16GB',
   'L_PAYMENTREQUEST_0_AMT0' =&gt; '496',
   'L_PAYMENTREQUEST_0_QTY0' =&gt; '1'
);

$paypal = new Paypal();
$response = $paypal -&gt; request('SetExpressCheckout',$requestParams + $orderParams + $item);</code></pre>

### 2. Redirecting To PayPal Using The Checkout Express Token

If the request is successful, we’ll receive a checkout token in the <code>TOKEN</code> parameter of the response.

<pre><code class="language-php">if(is_array($response) &amp;&amp; $response['ACK'] == 'Success') { //Request successful
      $token = $response['TOKEN'];
      header( 'Location: https://www.paypal.com/webscr?cmd=_express-checkout&amp;token=' . urlencode($token) );
}</code></pre>

The user now goes through the purchase process on PayPal’s website. When they confirm or cancel it, they will return to one of the URLs that we’ve specified in the request.

### 3. Completing The Transaction

Assuming the user confirms the transaction, they will be redirected to our website by PayPal. At this point, we should use two relevant API methods: <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_DoExpressCheckoutPayment"><code>DoExpressCheckoutPayment</code></a> will complete the transaction, but before that we might want to get additional information on the buyer using <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_GetExpressCheckoutDetails"><code>GetExpressCheckoutDetails</code></a>.

PayPal will redirect the user back from the purchase with the checkout token, which we will use to call those methods. The token will be available in the URL query parameters via the <code>token</code> parameter. We will check for its existence in the confirmation URL and then send our API requests if we find it.

The <code>GetExpressCheckoutDetails</code> method requires only the checkout token. <code>DoExpressCheckoutPayment</code> requires a couple of additional parameters:

*   `PAYMENTREQUEST_0_PAYMENTACTION`<br>
This is the payment action. It should be set to `Sale` unless we’ve specified a different action in the `SetExpressCheckout` method (possible values include `Authorization` and `Capture`).
*   `PAYERID`<br>
This is the unique identification for the PayPal account. This, too, is returned in the URL query parameters (in the `PayerID` parameter) and can also be retrieved from the details returned by `GetExpressCheckoutDetails`.

<pre><code class="language-php">if( isset($_GET['token']) &amp;&amp; !empty($_GET['token']) ) { // Token parameter exists
   // Get checkout details, including buyer information.
   // We can save it for future reference or cross-check with the data we have
   $paypal = new Paypal();
   $checkoutDetails = $paypal -&gt; request('GetExpressCheckoutDetails', array('TOKEN' =&gt; $_GET['token']));

   // Complete the checkout transaction
   $requestParams = array(
       'TOKEN' =&gt; $_GET['token'],
       'PAYMENTACTION' =&gt; 'Sale',
       'PAYERID' =&gt; $_GET['PayerID'],
       'PAYMENTREQUEST_0_AMT' =&gt; '500', // Same amount as in the original request
       'PAYMENTREQUEST_0_CURRENCYCODE' =&gt; 'GBP' // Same currency as the original request
   );

   $response = $paypal -&gt; request('DoExpressCheckoutPayment',$requestParams);
   if( is_array($response) &amp;&amp; $response['ACK'] == 'Success') { // Payment successful
       // We'll fetch the transaction ID for internal bookkeeping
       $transactionId = $response['PAYMENTINFO_0_TRANSACTIONID'];
   }
}</code></pre>

## Direct Payment

The Direct Payment API allows you to receive payments directly on your website or application, giving you complete control over the checkout process. PayPal tends to push users to register and use a PayPal account, which is understandable, but this conflicts somewhat with our interest to make the payment process as simple and clear as possible for our customers. For this reason, full control over the checkout process is preferred and gives us more options to optimize sales and generate more sales.

<img loading="lazy" decoding="async" class="111668" title="Direct Payment" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f8df71-c779-453a-ba7b-3e242b4635f9/scr-ukdirectpayment-cut.gif" alt="Direct Payment flow" width="529" height="206" />

The process is a bit simpler than that of Express Checkout, because the entire interaction occurs on our website, and we need to perform just one API call to process a normal payment: <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_DoDirectPayment"><code>DoDirectPayment</code></a>.

A couple of more API requests are required if you want to perform a transaction that is billed at a later date (for example, when you ship the product or confirm availability). These would be the <a href="https://www.paypalobjects.com/en_US/ebook/PP_APIReference/authcapture.html">Authorization &amp; Capture API</a> methods, which I will not cover in this post, but be aware that this option exists.

### DirectPayment Parameters

DirectPayment requires different parameters than Express Checkout, as to be expected. While the transaction details parameters are similar (with different key names, to make it more interesting), the method also requires credit-card and address information.

**DirectPayment’s basic parameters:**

*   `METHOD`<br>
This is `DoDirectPayment`.
*   `IPADDRESS`<br>
This is the IP address of the payer. In PHP, we can retrieve it using the superglobal `$_SERVER['REMOTE_ADDR']`. You’ll have to do a bit more work to get the IP when dealing with set-ups that have a proxy between the PHP process and the outside network (such as nginx).
*   `PAYMENTACTION`<br>
This is the type of action that we want to perform. A value of `Sale` indicates an immediate transaction. A value of `Authorization` indicates that this transaction will not be performed immediately, but rather will be captured later using the Authorization & Capture API mentioned earlier.

**Credit-card details:**

*   `CREDITCARDTYPE`<br>
The credit-card type (Visa, MasterCard, etc.). See the API documentation for the full list.
*   `ACCT`<br>
The credit-card number. (Don’t you love these abbreviated key names?) This must conform to the particular format of the card’s type.
*   `EXPDATE`<br>
The expiration date, in MMYYYY format (i.e. a two-digit month and a four-digit year, as one string).
*   `CVV2`<br>
The “card verification value,” or security code, as it’s sometimes known.

**Payer information and address parameters:**

*   `FIRSTNAME, LASTNAME`<br>
The payer’s first name and last name, respectively (in separate fields). You can also provide an email address in an `EMAIL` parameter, but it’s not required.
*   `CITY, STATE, COUNTRYCODE, ZIP`<br>
The city, state, country code (as a two-letter code) and zip code parts of the address, all required.
*   `STREET, STREET2`<br>
Two lines for the address (only the first is required).

This address will be used in the <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_AVSResponseCodes">address verification system</a> (AVS). You’ll receive a specific error code if a transaction has failed due to an address verification failure.

The payment details parameters are the same as the ones for Express Checkout, but with slightly different names (<code>AMT</code>, <code>ITEMAMT</code>, <code>CURRENCYCODE</code>, <code>SHIPPINGAMT</code>, <code>TAXAMT</code> and <code>DESC</code>) and without the <code>PAYMENTREQUEST_0_</code> prefix. Refer to the previous section or the API documentation for specific details on those.

Similarly, the item details parameters are similar to those of Express Checkout. These include <code>L_NAMEm</code>, <code>L_DESCm</code>, <code>L_AMTm</code> and <code>L_QTYm</code>, giving you granular control of item details in the order summary. The <code>m</code> integer variable is used to account for multiple items (replace with <code>0</code>, <code>1</code> and so on for numbered items in the order). See the API documentation for a <a href="https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_DoDirectPayment">comprehensive list of item details</a>.

### Performing The Transaction

Sending the request using our function is very similar to <code>GetExpressCheckoutToken</code>. We pass all of the parameters into the request function as before, with the method set to <code>DoDirectPayment</code>.

<pre><code class="language-php">$requestParams = array(
   'IPADDRESS' =&gt; $_SERVER['REMOTE_ADDR'],
   'PAYMENTACTION' =&gt; 'Sale'
);

$creditCardDetails = array(
   'CREDITCARDTYPE' =&gt; 'Visa',
   'ACCT' =&gt; '4929802607281663',
   'EXPDATE' =&gt; '062012',
   'CVV2' =&gt; '984'
);

$payerDetails = array(
   'FIRSTNAME' =&gt; 'John',
   'LASTNAME' =&gt; 'Doe',
   'COUNTRYCODE' =&gt; 'US',
   'STATE' =&gt; 'NY',
   'CITY' =&gt; 'New York',
   'STREET' =&gt; '14 Argyle Rd.',
   'ZIP' =&gt; '10010'
);

$orderParams = array(
   'AMT' =&gt; '500',
   'ITEMAMT' =&gt; '496',
   'SHIPPINGAMT' =&gt; '4',
   'CURRENCYCODE' =&gt; 'GBP'
);

$item = array(
   'L_NAME0' =&gt; 'iPhone',
   'L_DESC0' =&gt; 'White iPhone, 16GB',
   'L_AMT0' =&gt; '496',
   'L_QTY0' =&gt; '1'
);

$paypal = new Paypal();
$response = $paypal -&gt; request('DoDirectPayment',
   $requestParams + $creditCardDetails + $payerDetails + $orderParams + $item
);

if( is_array($response) &amp;&amp; $response['ACK'] == 'Success') { // Payment successful
   // We'll fetch the transaction ID for internal bookkeeping
   $transactionId = $response['TRANSACTIONID'];
}</code></pre>

There are plenty of parameters, but all relatively simple.

## Error Handling

In a perfect world, this section would not exist. In reality, you will be referring to it quite a lot. PayPal can fail a transaction for a multitude of reasons, not all of which you can control.

The <code>$response</code> variable we returned from our <code>paypalApiRequest()</code> function could contain a different value than <code>Success</code> for the <code>ACK</code> parameter. That value could be:

*   `Success`<br>
Indicates a successful operation.
*   `SuccessWithWarning`<br>
Indicates a successful operation, and that messages were returned in the response that you should examine.
*   `Failure`<br>
Indicates a failed operation, and that the response contains one or more error messages explaining the failure.
*   `FailureWithWarning`<br>
Indicates a failed operation, and that messages were returned in the response that you should examine.

This gives us two success statuses and two failure statuses. The mock code above tests for the <code>Success</code> value only, but we could change it to check for <code>SuccessWithWarning</code> as well; and keep in mind that we need to find out what the warning is. A common scenario is that a Direct Payment charge will have been performed successfully, but the credit-card company responds that the <a href="https://drupal.org/node/466236">transaction has failed, for whatever reason</a>.

Errors from PayPal are returned in four parameters in the response:

*   `L_ERRORCODE0`<br>
A numeric error code, which can referenced against PayPal’s [error code list](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&content_ID=developer/e_howto_api_nvp_errorcodes) (there are quite a few).
*   `L_SHORTMESSAGE0`<br>
A short error message describing the problem.
*   `L_LONGMESSAGE0`<br>
A longer error message describing the problem.
*   `L_SEVERITYCODE0`<br>
The severity code. (I couldn’t find any useful documentation on this, and it doesn’t really matter, so let’s put it aside.)

The <code>0</code> part of these parameters is an incrementing integer for multiple error message (<code>1</code>, <code>2</code>, etc.).

Here are some common errors you’ll run into:

*   `10002`<br>
**Authentication or authorization failed.** This usually indicates invalid API credentials, or credentials that do not match the type of environment you are working in (such as a live or sandbox environment).
*   `81***`<br>
**Missing parameter.** There are quite a few of these, all starting with `81`. Each refers to a specific required parameter that is missing from the request.
*   `104**`<br>
**Invalid argument.** This indicates that one of the supplied parameters has an invalid value. Each argument has specific errors, all starting with `104`. A common one is `10413`, which means that the total cost of the cart items does not match the order’s amount (i.e. the total amount parameter, `AMT`, does not equal the items’ total plus shipping, handling, taxes and other charges).

### How Do We Handle These Errors in Practice?

PayPal error messages vary and could contain private information that you do not want your users to see (such as an invalid merchant configuration). That being the case, showing PayPal error messages directly to users is not advisable, even though some of them might be useful.

In most cases, I would do the following:

1.  Set up a white-list array of errors that can be shown safely (such as a missing credit-card number and expiration date);
2.  Check the response code against that array;
3.  If the error message is not white-listed, then display a generic message, such as “An error has occurred while processing your payment. Please try again in a few minutes, or contact us if this is a recurring issue.”

If an error falls outside of the white-listed array, I will also log it to a file on the server and send an email to the administrator, with the full details so that someone is up to speed on payment failures. In fact, logging PayPal requests and responses is good practice regardless of errors, so that you can monitor and troubleshoot payment failures (I provide this option in the commercial component that I mentioned at the beginning of this article).

## Ready To Get Started With The PayPal API?

In this post, I’ve covered two of the most widely used API methods, as well as error handling with the PayPal API. This should be enough for you to get started using the most popular payment platform online.

The PayPal API has many more methods and processes, more than can be covered in any one post. Once you get up to speed on the basic methods, learning the others should be relatively straightforward (even if somewhat exhausting). I hope this guide has given you a good head start on using the API. If you have questions or comments, I would love to hear from you in the comments!

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Taking Credit Card Payments Online: What’s Involved?](https://www.smashingmagazine.com/2011/04/taking-credit-card-payments-online-whats-involved/)
*   [Testing Credit-Card Numbers In E-Commerce Checkouts](https://www.smashingmagazine.com/2016/07/testing-credit-card-numbers-in-e-commerce-checkouts-cheat-sheet/)
*   [Getting Started With E-Commerce: Your Options](https://www.smashingmagazine.com/2010/06/getting-started-with-e-commerce-your-options-when-selling-online/)

{{< signature "al, mrn" >}}
