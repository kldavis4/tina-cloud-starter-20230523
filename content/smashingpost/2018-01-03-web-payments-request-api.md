---
title: 'Introducing Web Payments: Easier Online Purchases With The Payment Request API'
slug: online-purchase-payment-request-api
author: poshaughnessy
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e05109-0959-4bfc-a15f-d020c45a3476/chrome-desktop-payment-request.png
date: 2018-01-02T12:52:21.000Z
summary: >-
  The W3C Working Group has been busy developing new standards to help make
  online payments much easier. In this article, Peter O'Shaughnessy provides you
  with the latest updates and explores the API with a basic example.
description: >-
  The W3C Working Group has been busy developing new standards to help make
  online payments much easier. In this article, Peter O'Shaughnessy provides you
  with the latest updates and explores the API with a basic example.
categories:
  - API
  - Browsers
  - E-Commerce
  - Payment
---
Buying things online can be a frustrating process, especially on mobile. Even if the pages are well designed, there's a lot of information required: Our contact information, shipping and billing addresses, shipping option and card details. If you've ever just given up sometimes, you're in the majority. 

The Baymard Institute took an average across 37 different studies and [found that 69% of shopping carts are abandoned](https://baymard.com/lists/cart-abandonment-rate).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae7a177-d073-4f74-8cfc-ce96e5fc9435/very-long-checkout-form-coinshop.png" sizes="100vw" caption="A typical, long checkout form on mobile. How many times have you been presented with a checkout form like this? (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae7a177-d073-4f74-8cfc-ce96e5fc9435/very-long-checkout-form-coinshop.png'>Large preview</a>)" alt="A typical, long checkout form on mobile" >}}

Unsurprisingly, the figures are worse on mobile, where the smaller screen and lack of a physical keyboard can make input slower. The abandonment rate on mobile can be [as high as 84%](https://econsultancy.com/blog/64343-checkout-abandonment-mobile-ux-examples-to-help-boost-conversions/) or more! With the rise and rise of mobile browsing over recent years, this means the overall problem has been getting worse and worse. For e-commerce sites, these abandoned carts are costing a huge amount of money. [Business Insider estimated](https://uk.businessinsider.com/heres-how-retailers-can-reduce-shopping-cart-abandonment-and-recoup-billions-of-dollars-in-lost-sales-2014-4) $4 trillion worth of merchandise would be abandoned in one year.

Thankfully, the web is fighting back against this problem. The ["Web Payments" W3C Working Group](https://www.w3.org/Payments/WG) has been busy working on *"a revolution in payments on the web"*, developing new standards to help make online payments much easier. As well as being the name of the Working Group, "Web Payments" is essentially an umbrella term covering these new, up-and-coming standards.

{{% feature-panel %}}

## The Payment Request API

The first of these standards, the *Payment Request API*, is a major step forward. It gives us the ability to request payment from a user and have the browser provide the user interface to accept it. It is already supported in Chrome, Edge and Samsung Internet, and it is in development in Firefox and Safari. Many high profile companies are adopting the API, including the New York Times, the Washington Post and Monzo.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b7bd5b-d06a-479a-9b63-de0bd3693455/monzo-payment-request-ui.png" sizes="35vw" caption="Example of the Payment Request UI from monzo.me in Samsung Internet. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b7bd5b-d06a-479a-9b63-de0bd3693455/monzo-payment-request-ui.png'>Large preview</a>)" alt="Example of the Payment Request UI from monzo.me in Samsung Internet" >}}

Requesting this information from the browser provides an immediate, major benefit because *it probably has these details stored already*. As long as we've entered our details on one other website that uses the API and allowed our browser to remember it, the browser will be able to pre-populate the form, letting us check out much faster. 

This is better than standard autofill; allowing the browser to handle the input fields means that it can be totally accurate — avoiding any issues with pre-populating the wrong information in the wrong fields. It also means we have a mobile-optimized, single-page checkout form, without having to write our own HTML and CSS for it.

The benefits might be felt even more on mobile, but the Payment Request API isn't limited to mobile browsers. It is already supported in the desktop versions of Chrome, Edge and Samsung Internet for DeX. We can also expect support to arrive in desktop Firefox and Safari later too (at the time of writing, it has recently been [enabled by default in Safari Technology Preview 44](https://webkit.org/blog/8035/release-notes-for-safari-technology-preview-44/)).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e05109-0959-4bfc-a15f-d020c45a3476/chrome-desktop-payment-request.png" sizes="100vw" caption="An example of the Payment Request UI in Chrome on the desktop. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e05109-0959-4bfc-a15f-d020c45a3476/chrome-desktop-payment-request.png'>Large preview</a>)" alt="An example of the Payment Request UI in Chrome on the desktop" >}}

## Our First Payment Request

Let's start exploring the API with a basic example. We are going to request a card payment from the user and allow them to check out like this:

<figure class="video-container"><iframe loading="lazy" data-
src="https://www.youtube.com/embed/ACWmYJYpAqw"
  width="600" height="480" frameborder="0"
  webkitallowfullscreen mozallowfullscreen allowfullscreen>
  </iframe><figcaption>Example of a ‘basic-card' Payment Request in Samsung Internet</figcaption></figure>

<p class="c-pre-sidenote--left">In the video above, you'll notice that the user confirms the payment with their fingerprint. This is not part of the Payment Request standard itself, but a security feature that the Samsung Internet browser provides (along with iris scanning) on supported devices.</p><p class="c-sidenote c-sidenote--right">If you're interested in further potential for integrating biometric authentication on the web, you might like to keep an eye on the upcoming <a href="https://w3c.github.io/webauthn/">Web Authentication standard</a>.</p>

First, as usual we should adopt Progressive Enhancement and check that this browser has support for the API:

<div class="break-out">

<pre><code class="language-javascript">
if (window.PaymentRequest) {
  // We can continue with the Payment Request API
} else {
  // Here we could fall back to a legacy checkout form
}
</code></pre></div>

Now we can set up the configuration for our PaymentRequest &mdash; the type of payment we will accept and details to display about the purchase:

<pre><code class="language-javascript">
var methodData = [{
  // ‘basic-card' means standard card payments - credit and debit cards
  supportedMethods: 'basic-card'
}];

var details = {
  // If we are buying multiple items, each one can be included
  displayItems: [
        {
          label: ‘Some product that we are buying',
          amount: {currency: 'USD', value: ‘699.99'}
        }
  ],
  total: {
        label: 'Total',
        amount: {currency: 'USD', value: ‘699.99'}
  }
};

var paymentRequest = new PaymentRequest(methodData, details);
</code></pre>

When we want to display the payment UI (e.g. when the user clicks "Buy Now"), we can call <code>show()</code>. Then we handle the data that the user provided when the promise is resolved:

<div class="break-out">

<pre><code class="language-javascript">
// show() makes it actually display the user interface
paymentRequest.show()
  .then(function(paymentResponse) {
        // User has confirmed. paymentResponse contains the data entered.
        // Here we would process it server-side...
        processPaymentDetails(paymentResponse)
          .then(function(paymentResponse) {
            // ...Then when processed successfully, this will make the dialog indicate success & then close:
            paymentResponse.complete('success');
            // We could also update the page here appropriately
          });
  })
  .catch(function(error) {
        // Handle error, e.g. if user clicks the 'cancel' button.
  });
</code></pre></div>

We now have the UI flow set up on the front end. We can also configure it further, to match our requirements. For example, if we wish to request extra details from the customer, we can pass additional `options` into the PaymentRequest constructor. For example, to request the user's name, email address, telephone number and shipping address:

<div class="break-out">

<pre><code class="language-javascript">
var options = {
  requestPayerName: true,
  requestPayerEmail: true,
  requestPayerPhone: true,
  requestShipping: true
};

var paymentRequest = new PaymentRequest(methodData, details, options);
</code></pre></div>

We can also define multiple shipping options and even control which options are presented dynamically, based on the customer's address. You can find an example of this [here on Glitch](https://glitch.com/~web-payments-101-completed).

## User Experience

We are starting to see some impressive statistics for the benefits that Payment Request can bring to companies. [Google recently shared](https://youtu.be/1-g1rvkORQ8?t=6m21s) that J.Crew, a fashion brand, has found that 50% of their users now go through the Payment Request flow and it cuts down their transaction time by 75%!

It's up to you how to integrate Payment Request into your shopping experience, but a common way is to offer something like an "Express Checkout" or "Buy Now" option, without requiring the customer to log in first. If you like, you can collect the user's contact details using the Payment Request UI and once they have made the purchase, offer the opportunity to create an account then, for future use.

If you want to, you can check first if the customer already has a valid payment method set up, before presenting the Payment Request UI. To do this, you can call `canMakePayment`:

<div class="break-out">

<pre><code class="language-javascript">
if (paymentRequest.canMakePayment) {
  paymentRequest.canMakePayment().then(function(result) {
        if (result) {
          // User has an active payment method
        } else {
          // No active payment method yet (but they could add one)
        }
  }).catch(function(error) {
        // Unable to determine
  });
}
</code></pre></div>

## Back-End Integration

We have seen how to set up the user interface for taking payments, but how do we actually process the payments in the back-end?

Most websites will not handle payments themselves (something which would require a lot of care and [PCI DSS compliance](https://pcidsscompliance.net/)) but use a third party Payment Gateway (PG) or Payment Service Provider (PSP). A number of Payment Gateways have already introduced specific support for the Payment Request API. They may initiate the Payment Request via their own script that you include on your page, helping to ensure that the data is sent securely and that you do not have to handle it yourself. They may also offer an iFrame or redirect solution. The best way to proceed is to check with your Payment Gateway how they recommend incorporating Payment Requests.

## Payment App Integration

So far we have discussed card payments. However, the Payment Request API also supports mobile payment apps like Samsung Pay, Pay with Google (incorporating Android Pay) and Apple Pay.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb8fd8e6-2b8d-438b-be12-8ee19deeca14/samsung-pay-and-pay-with-google.png" sizes="100vw" caption="Examples of Payment Request supporting Samsung Pay (left) and Pay with Google (right). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb8fd8e6-2b8d-438b-be12-8ee19deeca14/samsung-pay-and-pay-with-google.png'>Large preview</a>)" alt="Examples of Payment Request supporting Samsung Pay and Pay with Google" >}}

Letting our customers pay with one of these apps means they can use the card they have saved in the app, without having to re-enter the details (even the first time) in the browser. Using these apps can also be quicker because they do not require the customer to re-enter their CVC (Card Verification Code, also known as CVV) from the back of their card. Finally, they can bring additional security benefits because they do not transmit the original card details, only single-use tokens, thereby protecting us from potential interception and replay attacks.

When the customer selects the payment app as their chosen payment method, the browser switches over to a payment sheet provided by the app, to confirm the payment. The third party app will then generally accept the customer's fingerprint or iris scan to confirm the payment if the device supports it.

Each payment app will have their own particular instructions, but the general idea is the same. You can identify them as potential payment methods using their own special URLs and pass the required configuration in the `data` field. For example, to support Samsung Pay, you would include code like this in your `methodData` array:

<div class="break-out">

<pre><code class="language-javascript">
var methodData = [
  {
        supportedMethods: 'https://spay.samsung.com',
        data: {
        // Samsung Pay specific data here
        }
  },
  … // Other payment methods
];
</code></pre></div>

Generally speaking, there are two methods for integrating these apps with your payment gateway: a "Gateway Token" method and a "Network Token" method. If you are using a third-party service that supports it, then you will most likely use the Gateway Token mode, where the payment app service will make a call to your Payment Gateway on your behalf. Alternatively, you can use the Network Token method where you will handle sending the token to your Payment Gateway securely, using their SDK. Your Payment Gateway and/or payment app provider should be able to provide further details.

Google recently announced the [Google Payment API](https://developers.google.com/payments/mobile-web-setup) which incorporates Android Pay as well as cards stored in customers' Google accounts.

Apple Pay currently uses its own JavaScript solution, [Apple Pay JS](https://developer.apple.com/documentation/applepayjs). However, developers at Google have [created a wrapper](https://github.com/GoogleChrome/appr-wrapper) that allows you to use it via the standard Payment Request API.

## What's Next?

The Web Payments Working Group is not stopping at the Payment Request API. Work is also underway on other standards, including the [Payment Handler API](https://www.w3.org/blog/wpwg/2017/05/18/payment-handler-api-first-public-working-draft-published/) which will allow web applications to act as a third-party payment app. Other topics that are being discussed include possible standardization around tokenization and the ability for Payment Requests to support things like gift cards. If you would like to keep up with the developments, here is the [public mailing list](https://lists.w3.org/Archives/Public/public-payments-wg/). I hope that together we can solve the frustrating checkout experiences of the past and achieve the vision of a web payments revolution!

## Further Resources

* "[W3C's Web Payments Wiki](https://github.com/w3c/webpayments/wiki)," GitHub
* "[W3C's Payment Request API Developer Information](https://github.com/w3c/payment-request-info)," GitHub [see also FAQ](https://github.com/w3c/payment-request-info/wiki/FAQ)
* "[Web Payments 101: A Short Payment Request Coding Tutorial](https://glitch.com/~web-payments-101)," Glitch
* "[Deep Dive Into The Payment Request API](https://developers.google.com/web/fundamentals/payments/deep-dive-into-payment-request)," Google Developers
* "[Payment Request API Dev Guide](https://docs.microsoft.com/en-us/microsoft-edge/dev-guide/device/payment-request-api)," Microsoft Edge
* "[How To Accept Samsung Pay On Your Website Using Web Payments](https://medium.com/samsung-internet-dev/how-to-accept-samsung-pay-on-your-website-using-web-payments-c2fcd4d26c02)," Winston Chen, Medium

{{< signature "rb, ra, yk, il" >}}

