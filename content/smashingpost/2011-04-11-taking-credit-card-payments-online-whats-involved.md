---
title: 'Taking Credit Card Payments Online: What’s Involved?'
slug: taking-credit-card-payments-online-whats-involved
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08cb5776-31eb-4dde-9e13-c6b8fff97bdc/payment-105.jpg
date: 2011-04-11T15:25:02.000Z
author: leigh-mason
summary: >-
  The prospect of integrating a payment solution on your website can seem unwieldy. Leigh Mason breaks down the entire process for you to understand it much better! 
description: >-
 Leigh Mason breaks down the process of integrating a credit card payment solution onto your website. If at first glance you consider the prospect can seem unwieldy, this article will help you to understand it much better. 
categories:
  - Business
  - Web Design
  - E-Commerce
  - Security
  - Payment
---
If you’re looking to integrate a credit card payment solution onto your website, the following steps are a guide to applying for, enabling and taking payments online. At first glance, the prospect of integrating a payment solution on a website can seem unwieldy, what with the vast array of payment options and technical acronyms. This article breaks down the entire process into bite-sized pieces, helping you understand the process much better.

{{% feature-panel %}}

## Apply For An IMA

When taking any kind of credit card payments connected to a bank account, you must apply for a merchant account with a bank. If the payments will be taken online, you’ll specifically need an Internet Merchant Account (IMA). In addition to banks, in many locations there are dedicated merchant account providers you can use.

Even if you currently take “card-not-present” payments (such as for mail orders) or use in-store payment terminals (such as chip-and-pin), you still have to speak with your bank about taking payments via your website (ask your bank for an additional IMA ID).

As a broad overview, your bank acts as the “acquirer,” which confirms available funds, authorizes transactions and exchanges funds with the issuing bank of the credit card (e.g. Visa, MasterCard), i.e. the card holder’s bank. The funds are then transferred to your account (the merchant), minus the applicable fees. The issuing bank’s charges are called interchange fees, and your bank’s fees are the acquirer’s fees. As the merchant, you should be informed of any fees prior to signing the merchant services agreement with your bank and payment service provider (more about this further down).

Your acquiring bank will expect your website to operate within a strict set of rules in order for them to comply with their own security procedures and government legislation (more on that later, too). Some credit card providers have developed the technology to allow card holders to authenticate themselves online. MasterCard’s is called MasterCard SecureCode, and Visa’s is called Verified by Visa.

It’s worth noting that it is possible to process Internet payments manually, using your regular point of sale system. This isn’t recommended, though, partly due to security reasons, and partly because it can quickly become too much work to manually process payments taken through your website (do you really want to have to key in a thousand individual cards if you suddenly have a huge uptick in sales?). Also, some merchant agreements may specifically prohibit this type of payment processing. Even if you do decide to process payments manually, you’ll still need an Internet Merchant Account, because it’s where the transaction is initiated that counts, not where it’s eventually processed.

## Select A PSP

In addition to an IMA, you will need to use the services of a payment service provider (PSP). Commonly, PSPs handle the pages on a website where customers submit their payment details. PSPs provide a “virtual” cashier, or point-of-sale terminal, that collects card details, screens for fraud and securely passes the details to your acquiring bank for processing. PSPs are sometimes referred to as payment gateways.

The PSPs offer various packages and rates to suit the requirements of different merchants. The main difference between packages comes down to whether you want to host the secure payment pages on the PSP’s servers or on your own server. Some PSPs also provide tailored solutions.

It’s worth noting that some PSPs also provide IMAs, and some acquiring banks provide PSP services.

## Payment-Processing Companies

As is often the case, there are alternatives to the approach outlined above, especially if you want to avoid the challenge of technically implementing one of these solutions. One alternative is to use the services of a payment-processing company. This option eliminates the need to apply for an IMA and PSP separately. The application process of a payment processing service is usually a lot less stringent than that for an IMA, which results in a faster set-up, especially if you have little or no trading history.

The disadvantage is that your customers will be sent to the processing company’s website in order to make their payment. Also, settlement periods can take much longer (up to 60 days), and your overall cost may be slightly higher than if you had gone with an IMA and PSP.

Not all payment-processing companies operate like this, though. Some companies, including PayPal and Google Checkout, remit payment immediately in most cases, directly into your account. In other words, as soon as the payment is made by your customer, the money is deposited into your merchant account.

## A Sample Checkout Process

Here’s a step-by-step example of **a common credit card payment process** for any website:

### Step 1: The Basket

Your customer has added a product to their basket and is ready to proceed to checkout. The basket page on your website should be SSL encrypted to bolster the customer’s confidence (but that’s for another article).

### Step 2: The Checkout

The customer proceeds to the next page of your website: the checkout page. You can have various options here: account log-in page, shipping options, etc. But for the purpose of this example, let’s assume the first stage of checkout is simply a page that requires the customer to submit some personal details, such as contact info and a billing and shipping address.

Once the required fields are submitted and validated, the details are first securely sent to your back-end database, then wrapped up and securely passed to your PSP’s website. The customer is also redirected to the PSP’s website.

Let’s pause for a second and look at what’s happening here. Your customer’s data should be encrypted when sent to the PSP, not stored in plain text. So, you make a function call to your PSP’s API, requesting the transfer of data. The API’s function will usually require a set of parameters that include the merchant’s ID, a unique order reference, the transaction’s total charge and currency, and all of the billing and shipping mentioned above.

The function will then either return an encrypted version of your data, ready to be posted to the PSP’s payment pages, or hold onto the data and return a secure key in receipt that verifies that particular set of data against the transaction. You would store this key along with the order details and then redirect the customer to the PSP’s payment pages.

### Step 3: Payment

Your customer arrives on the PSP’s secure payment pages. Technically, keeping the customer on your website at this stage is possible (if the PSP has this option), but let’s keep this simple. If the PSP’s pages duplicate some of the fields on your own checkout page (like the billing and shipping address), then these fields can be pre-populated.

Once all of the card holder’s data has been submitted and payment has been made, your customer is seamlessly returned to your website.

OK, some stuff is also going on in the background here, too. First, the card holder’s details are authenticated by the PSP using a variety of security procedures. Next, the card holder’s total charge must be authorized and the funds allocated to the merchant. Technically, the merchant should not take payment directly, but rather take a deferred payment until the goods have actually shipped (see the regulations on distance selling below).

Your PSP would then send the status of the transaction’s outcome to your website, along with the unique order reference (to identify the order) and any other pertinent data, including security-related confirmations such as CV2 and postal code checks.

You should make sure that your e-commerce store follows the <a href="https://www.pcicomplianceguide.org/">PCI complance</a> guidelines for storing, accessing and managing sensitive credit card data. This Payment Card Industry Data Security Standard (PCI DSS) is a set of requirements designed to ensure that all companies that process, store or transmit credit card information maintain a secure environment.

It applies to all organizations or merchants, regardless of size or number of transactions, that accepts, transmits or stores any cardholder data. So, if any customer of that organization ever pays the merchant directly using a credit card or debit card, then the PCI DSS requirements apply. This server security standard is required by almost all major credit card providers, or you risk the potential for steep daily fines. (*Thanks to Brian and Rebecca in the comments for pointing it out!*)

### Step 4: Order Confirmation

On returning to your website, the customer is presented with a confirmation page indicating whether the payment has been authorized or declined.

The PSP passes variable data (such as an order reference) back to your website, which you use to look up the order data on your database and present the appropriate content.

{{% ad-panel-leaderboard %}}

## PSP Checklist

Check that your PSP provides the following features:

*   SSL encryption on all payment pages,
*   Authentication procedures,
*   API to securely post data from your website,
*   Call-back API to indicate payment confirmation (which should contain multiple status descriptions),
*   Option to pre-populate fields on payment pages,
*   Feature to customize payment pages to match your layout and branding,
*   Redirection back to your website upon payment completion.

## Gateway Comparison

Below is a comparison of a small selection of gateways. The list is in no particular order and is in no way a recommendation of any particular one.

### Sage Pay (UK and Ireland)

Here is a summary of Sage Pay Go with Server Integration:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34c16582-67de-4301-8861-6c85b4c7531b/payment-1011.jpg" alt="Screenshot" width="500" height="298" /><figcaption>Sage Pay.</figcaption></figure>

*   **Separate test and live servers**.  A simple yet convenient way to test your integration prior to going live. Once you are happy that everything is working as intended, all that’s required to go live is a change to the server’s URL in your code.
*   **iFrame support**.  Gives the appearance that your payment pages are actually on your website (an SSL certificate is required if you opt for this). Keeping customers on your website rather than sending them to the gateway’s website in order to complete payment could increase your conversion rate.
*   **Extensive payment page customization**.  If you do send users to Sage Pay’s website to complete their payment, you can customize the page so that it looks more like your website. However, the templates are created in XML, which makes them more complicated than the standard HTML templates of some other solutions.
*   **Manual approval process for template changes**.  This part of the integration process is slightly inconvenient. Every time you amend your custom payment page, you have to manually submit it to Sage Pay and then wait (usually no more than 24 hours) for it to update the template.
*   **Initial post done by server, not the browser**.  None of the order details are exposed in the HTML page. The customer’s order data is posted using cURL over SSL. A redirection URL is returned to direct the user to the payment pages. Arguably, this is more secure than posting data in the HTML page. I also like the way that payment page URLs are returned, which saves them from being stored and possibly having to be amended.
*   **Call-back**.  When Sage Pay’s server responds to your server with details of the payment outcome, there’s a function to validate the data by matching secure keys.
*   **Account Parameter Configuration**.  Numerous account parameters are stored in the admin control panel. One in particular is the “Valid IP address,” which specifies several IP entries from where the initial data registration must originate.

### Barclaycard (UK)

It’s a common misconception that you need to bank with Barclays in order to use its <a href="https://www.barclaycardbusiness.co.uk/epdq_cpi/">ePDQ CPI</a> payment solution. If you do not bank with Barclays, you can still apply for its IMA and PSP solution. Cleared funds will be transferred to your chosen bank.

<figure><a href="https://www.barclaycardbusiness.co.uk/epdq_cpi/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112ef1e5-affd-429f-9a9c-64db2e5a647d/payment-102.jpg" alt="Screenshot" width="500" height="341" /></a><figcaption>Barclaycard.</figcaption></figure>

*   **Testing**.  As of this writing, no test server is available with the ePDQ solution. You can post test variables though the ePDQ, which flags a test transaction, but these details are not processed to simulate a successful end-to-end transaction. To get around this, we created a test page that emulates the call-back response, which is basically an HTML form containing an order reference and status field that’s posted to the call-back page.
*   **Data posted via browser**.  There’s a big difference between how data is sent with ePDQ and how it is done with Sage Pay. For example, only a handful of data is initially sent to ePDQ for encryption (via a socket connection). Upon receipt, the encrypted string along with the remaining data is posted via the browser within the form, as opposed to the data being sent via the server.
*   **Call-back** ePDQ’s server posts a call-back response that contains only the transaction status and your unique reference (order ID). While this is sufficient to update your database, there’s no way to check where the call-back is coming from. We can emulate this in our test phase (mentioned above), but ePDQ does require the call-back script to be stored in a password-protected directory.
*   **Account parameter configuration**.  Quite a few account parameters are stored in the ePDQ configuration area, including an “allowed URL” (where the initial call must originate) and a “Post URL” (where the call-back script resides). There are also “POST” user names and passwords for the call-back directory.

### WorldPay (Worldwide)

As with ePDQ, you don’t need an RBS bank account in order to use its <a href="https://www.rbsworldpay.com/products/index.php?page=ecom&amp;sub=business&amp;c=UK">WorldPay Business Gateway</a> (formerly Select Junior).

<figure><a href="https://www.rbsworldpay.com/products/index.php?page=ecom&amp;sub=business&amp;c=UK"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c8f1476-05f4-4b87-8265-9900f59de2f5/payment-103.jpg" alt="Screenshot" width="500" height="319" /></a><figcaption>WorldPay.</figcaption></figure>

*   **Separate test and live servers**.  As with Sage Pay, WorldPay has separate URLs for the test and live servers.
*   **Data posted via browser**.  Data is also sent via the browser, either as a `POST` or `GET`. I wanted to see if you could send the customer’s data to the gateway without a clunky JavaScript form post, but while it’s technically possible for the `GET` to be intercepted en route, WorldPay has the mandatory key signature field that counters this threat by matching the received values against those contained in the signature.
*   **Call-back**.  Like ePDQ, WorldPay’s server posts a payment response containing the transaction’s status and your unique reference (order ID). While this is sufficient to update your database, there’s no way to check where the call-back is coming from.
*   **Payment page templates**.  The payment page templates are fairly flexible because you can create a Y and C (success and failure) HTML page that closely matches your website. WorldPay has “smart tags” for data such as order ID and merchant name that must be included on your custom page. A slight difference here is that your website’s return URL must be included in the template.
*   **Account parameter configuration**.  Quite a few account parameters are stored in the installation area: a payment response URL for the call-back script and a payment response password for the call-back script’s directory password. However, there doesn’t appear to be a setting for "allowed URLs" or IP addresses to validate the origin of the merchant’s data.

### Authorize.Net (Worldwide)

<a href="https://www.authorize.net/">Authorize.Net</a> is one of the larger payment gateways, with more than 300,000 sites currently using it.

<figure><a href="https://www.authorize.net/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23e109df-0b9d-4f58-aef4-ae180bce3df7/payment-104.jpg" alt="Screenshot" width="500" height="310" /></a><figcaption>Authorize.Net.</figcaption></figure>

*   **Accept a Variety of Payments**. Authorize.Net lets you accept all major credit cards, eChecks, gift cards, and signature debit cards.
*   **Payments Within Days**. Payments are made quickly, generally within days of the original transaction.
*   **Fraud Prevention Tools**. Authorize.Net has tools in place to identify suspicious transactions, both through built-in tools and add-on products.
*   **Free Support**. They have live tech support and account support, plus online user guides and documentation.
*   **Developer Tools and Reseller Accounts**. Authorize.Net also offers developer tools for creating payment solutions, as well as reseller accounts to developers and service providers.

### 2Checkout (Worldwide)

<a href="https://www.2checkout.com/">2Checkout</a> offers a number of payment gateway services, and has been handling e-commerce payments for more than 10 years.

<figure><a href="https://www.2checkout.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08cb5776-31eb-4dde-9e13-c6b8fff97bdc/payment-105.jpg" alt="Screenshot" width="500" height="378" /></a><figcaption>2Checkout.</figcaption></figure>

*   **Hosted Payments**.  2Checkout offers hosted payments, with simple plug-n-play code for integrating their payment gateway into your existing website and shopping cart software. They collect, store, and encrypt the credit card information your customers submit, all in accordance with industry standards.
*   **Recurring Billing**.  They can handle recurring billing options for subscriptions or similar purchases.
*   **Co-Branded Payment Pages**.  Co-branded payment pages are used “so that they customer recognizes the hand-off from your site to ours.” This could be viewed as a good or a bad thing depending on the image the e-commerce site is looking to convey. Some customers are reassured by being redirected to a larger payment processor, while others are sometimes put off by it.
*   **Variety of Payment Methods**.  They accept 15 different payment methods, including Visa, MasterCard, American Express, Diner’s Club, and even PayPal.

### Google Checkout

<a href="https://checkout.google.com/sell/">Google Checkout</a> removes much of the hassle of setting up online payments by removing much of the barrier to entry. If you have a Google account, you can have Google Checkout set up within a few minutes.

<figure><a href="https://checkout.google.com/sell/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/942960a0-d90d-404e-89cc-47a615ad85c3/payment-106.jpg" alt="Screenshot" width="500" height="271" /></a><figcaption>Google Checkout.</figcaption></figure>

*   **Variety of Integration Options**.  Google Checkout has some of the most versatile integration options out there. Sure, you can just set up a "Buy Now" button or two, but they also offer integration with custom shopping carts, pre-integration with existing shopping cart systems, a store gadget (that you can set up with a Google Spreadsheet), email invoices, and their own shopping cart solution.
*   **Google is a Recognized Brand**.  Google is recognizable all over the world, and is a trusted brand for the most part. This can be especially valuable to smaller, unknown businesses who might not have their own good reputation to ride on.
*   **API Developer’s Guide** Developer’s can have a field day with the developer API for Google Checkout. It means you can customize the Google Checkout experience to your heart’s content.
*   **Protection from Chargebacks**.  Chargebacks can be a big problem for some businesses, especially those in higher-risk industries. Google Checkout offers a Payment Guarantee that protects an average of 98% of all Google Checkout transactions. If your transaction falls under their guarantee, and there’s a chargeback, you won’t lose money.

### PayPal

<a href="https://paypal.com">PayPal</a> started as a solution for eBay sellers to accept credit card payments but has turned into a major player in the online payment gateway industry.

<figure><a href="https://paypal.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31a3b1ea-f09a-4c45-a662-76bba5d2c7a1/payment-107.jpg" alt="Screenshot" width="500" height="326" /></a><figcaption>PayPal.</figcaption></figure>

*   **Recognizable Name**.  PayPal has become almost as big a household name as Google. Some consumers have gone so far as refusing to do business with online retailers who don’t accept PayPal.
*   **Solutions for Every Kind of Business**.  PayPal now provides a range of solutions for businesses, including fully-featured merchant accounts like those you’d find at a bank (Payflow Payment Gateway). Their Website Payments accounts provide most of what a gateway provides, including the ability to keep customers on your site through the entire transaction (with the Pro account). And of course PayPal also offers simple "Buy Now" buttons if that’s all you need.
*   **Immediate Payment**.  PayPal pays immediately for most transactions, which means that your payments go directly into your PayPal account when they’re made. (This is not always the case for certain businesses, or for accounts with a history of high returns.) In some countries, PayPal offers signature debit cards that can be used like a credit card and give you immediate access to your PayPal funds from any ATM.
*   **Easy Integration**.  PayPal offers a number of developer tools, both for facilitating payments and for accessing account information and reporting. Various PayPal payment processing products have different levels of difficulty when it comes to integration, but at the easiest end of the spectrum it involves just inserting a bit of code.

{{% ad-panel-leaderboard %}}

## Summary

Taking credit card payments online is a fairly straightforward process, but you should understand *what* your options are and *how* each option suits your business objectives. The **solutions available range** from simple pieces of JavaScript for "Buy now" buttons (PayPal and Google Checkout do this) to self-hosted secure payment pages. Some solutions are attractive for their ease of integration, some for their price and others for their flexibility. Hopefully, this article has helped you choose a payment solution for your website.

*Note: Thanks to Cameron Chapman for her much appreciated improvements and research for this article. You might want to take a look at the article Web apps, credit cards, merchant accounts and PayPal for a related case study for the issue covered in this article.*

### Further Reading

*   [Getting Started With E-Commerce: Your Options](https://www.smashingmagazine.com/2010/06/getting-started-with-e-commerce-your-options-when-selling-online/)
*   [Testing Credit-Card Numbers In Checkouts (Cheat Sheet)](https://www.smashingmagazine.com/2016/07/testing-credit-card-numbers-in-e-commerce-checkouts-cheat-sheet/)
*   [Getting Started With The PayPal API](https://www.smashingmagazine.com/2011/09/getting-started-with-the-paypal-api/)
*   [Free PNG Credit Card, Debit Card and Payment Icons Set](https://www.smashingmagazine.com/2010/10/free-png-credit-card-debit-card-and-payment-icons-set-18-icons/)

{{< signature "al, ik, vf, mrn" >}}
