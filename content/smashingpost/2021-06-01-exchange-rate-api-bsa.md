---
title: 'Setting Up A Currency Convertor With ExchangeRatesApi.io'
slug: currency-convertor-exchangeratesapi
author: leonardolosoviz
image: >-
 https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ce4b3b1-3ae6-4371-8aaf-d72da3b69fc5/4-exchange-rate-api-bsa.png
date: 2021-06-01T09:00:00.000Z
summary: >-
 Amazon allows visitors to display prices in their own currency. Thanks to [ExchangeRatesApi.io](https://exchangeratesapi.io/?utm_source=SmashingMagazine&utm_medium=ThirdParties&utm_content=Article-exchangerateapi), we can do the same for our online shops, providing a better experience to our customers. Let’s find out how.
description: >-
 Amazon allows visitors to display prices in their own currency. Thanks to *ExchangeRatesApi.io*, we can do the same for our online shops, providing a better experience to our customers. Let’s find out how.
categories:
 - API
 - Tutorials
 - Coding
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: ExchangeRatesApi.io
  link: https://exchangeratesapi.io/?utm_source=SmashingMagazine&utm_medium=ThirdParties&utm_content=Article-exchangerateapi
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d18ad67-3ded-40d7-81b7-751b42f72d1a/exchangeratesapi-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://exchangeratesapi.io/?utm_source=SmashingMagazine&utm_medium=ThirdParties&utm_content=Article-exchangerateapi">ExchangeRatesApi.io</a> who provide developers with powerful data and conversion APIs for current and historical exchange rates. <em>Thank you!</em>
---

Products and services are increasingly accessed and bought online. As we live in a global village, if we have an online shop, many of our visitors will quite likely be based on a different country than our own, and use a different currency than our own.

If we want to provide a great user experience for them, to increase the chances of them buying our product, and coming back to the site, there is something very simple we can do: Display the price of the shopping items in their own currency. To achieve that, we can convert the price of the item from a base currency (say, EUR) to the visitor’s currency (say, CNY) using the exchange rate between the two currencies at that specific time.

Currency exchange rates change constantly, on an hourly basis (and even faster). This means that we can’t have a pre-defined list of exchange rates stored in our application; these must be gathered in real-time. However, this is not a problem nowadays. Thanks to APIs providing currency exchange data, we can add a currency convertor to our online shops rather effortlessly.

In this article, we will introduce [ExchangeRatesApi.io](https://exchangeratesapi.io/?utm_source=SmashingMagazine&utm_medium=ThirdParties&utm_content=Article-exchangerateapi), a popular API solution providing data for current and historical exchange rates for 168 currencies.

## What We Want To Achieve

Simply said, we want to do what Amazon is doing: Give the option to the user in our online shop to display the prices in a currency of their own choosing.

When visiting a product page in [amazon.co.uk](https://www.amazon.co.uk), we are presented the price in British pounds:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f0d5aa-70a0-4070-8bfc-f5442250e344/1-exchange-rate-api-bsa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f0d5aa-70a0-4070-8bfc-f5442250e344/1-exchange-rate-api-bsa.png" width="800" height="601" sizes="100vw" caption="Product page in <a href='amazon.co.uk'>amazon.co.uk</a>, with price shown in pounds. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f0d5aa-70a0-4070-8bfc-f5442250e344/1-exchange-rate-api-bsa.png'>Large preview</a>)" alt="Product page in amazon.co.uk, with price shown in pounds" >}}

But we can also see the price in a different currency, if we wish to. In the country/region settings, there is the option to change the currency:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ca0824-5fd4-419e-b61f-7f6c592bc47e/2-exchange-rate-api-bsa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ca0824-5fd4-419e-b61f-7f6c592bc47e/2-exchange-rate-api-bsa.png" width="800" height="601" sizes="100vw" caption="Dropdown with region settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ca0824-5fd4-419e-b61f-7f6c592bc47e/2-exchange-rate-api-bsa.png'>Large preview</a>)" alt="Dropdown with region settings" >}}

After clicking on "Change", we are presented a select input, containing several pre-defined currencies. From among them, I’ve chosen the Euro:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8b5a6b3-7d64-4407-8020-d7d333579141/3-exchange-rate-api-bsa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8b5a6b3-7d64-4407-8020-d7d333579141/3-exchange-rate-api-bsa.png" width="800" height="601" sizes="100vw" caption="Dropdown with region settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8b5a6b3-7d64-4407-8020-d7d333579141/3-exchange-rate-api-bsa.png'>Large preview</a>)" alt="Dropdown with region settings" >}}

Finally, back on the product page, the price is displayed in euros:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ce4b3b1-3ae6-4371-8aaf-d72da3b69fc5/4-exchange-rate-api-bsa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ce4b3b1-3ae6-4371-8aaf-d72da3b69fc5/4-exchange-rate-api-bsa.png" width="800" height="601" sizes="100vw" caption="Product page in amazon.co.uk, with price shown in euros. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ce4b3b1-3ae6-4371-8aaf-d72da3b69fc5/4-exchange-rate-api-bsa.png'>Large preview</a>)" alt="Product page in amazon.co.uk, with price shown in euros." >}}

Having access to exchange rate data via an API, we can implement this same functionality for our own online shops.

## How Do We Do It

ExchangeRatesApi.io provides a REST API, offering the latest forex data for 168 currencies. It is always up-to-date, compiling the data from a broad base of commercial sources and banks around the world.

After [signing up on their service](https://exchangeratesapi.io/pricing/) (**tip:** they have a [free tier](https://manage.exchangeratesapi.io/signup/free)), we will be assigned an API access key:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a322f1d-d9d2-40ec-8916-469c7da7b8f9/5-exchange-rate-api-bsa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a322f1d-d9d2-40ec-8916-469c7da7b8f9/5-exchange-rate-api-bsa.png" width="800" height="424" sizes="100vw" caption="Dashboard in <a href='ExchangeRatesApi.io'>ExchangeRatesApi.io</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a322f1d-d9d2-40ec-8916-469c7da7b8f9/5-exchange-rate-api-bsa.png'>Large preview</a>)" alt="Dashboard in ExchangeRatesApi.io" >}}

We grab our API access key, and [append it to the endpoint](https://exchangeratesapi.io/documentation/#apikey):

<pre><code class="language-javascript">https://api.exchangeratesapi.io/v1/latest
 ?access_key=YOUR_API_KEY
</code></pre>

To visualize the response, copy/paste the endpoint in your browser:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19fddcd5-4ea2-4d69-9ff5-5e0d8b5e436e/6-exchange-rate-api-bsa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19fddcd5-4ea2-4d69-9ff5-5e0d8b5e436e/6-exchange-rate-api-bsa.png" width="800" height="694" sizes="100vw" caption="Viewing the response to the REST API on the browser. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19fddcd5-4ea2-4d69-9ff5-5e0d8b5e436e/6-exchange-rate-api-bsa.png'>Large preview</a>)" alt="Viewing the response to the REST API on the browser" >}}

As can be possibly appreciated in the image above, the data for all 168 currencies has been retrieved. To narrow down the results to just a few of them, we [indicate the currency codes via param](https://exchangeratesapi.io/documentation/#specifysymbols) [`symbols`](https://exchangeratesapi.io/documentation/#specifysymbols).

For instance, to retrieve data for the USD, British pound, Australian dollar, Japanese Yen and Chinese Yuan (compared against the Euro, which is the base currency by default), we execute this endpoint:

<pre><code class="language-javascript">https://api.exchangeratesapi.io/v1/latest
 ?access_key=YOUR_API_KEY
 &symbols=USD,GBP,AUD,JPY,CNY
</code></pre>

The response is the following:

<pre><code class="language-javascript">{
 "success": true,
 "timestamp": 1620904263,
 "base": "EUR",
 "date": "2021-05-13",
 "rates": {
   "USD": 1.207197,
   "GBP": 0.860689,
   "AUD": 1.568196,
   "JPY": 132.334216,
   "CNY": 7.793428
 }
}
</code></pre>



## What Data Can We Retrieve

ExchangeRatesApi.io provides several REST endpoints, to fetch different sets of data. Depending on the subscribed plan, endpoints may or may not be available (their [pricing page](https://exchangeratesapi.io/pricing/) explains what features are covered by each tier).

The endpoints indicated below must be attached to `https://api.exchangeratesapi.io/v1/` (eg: `latest` becomes `https://api.exchangeratesapi.io/v1/latest`), and added the `access_key` param with your API access key.

#### Latest rates

The [`latest`](https://exchangeratesapi.io/documentation/#latestrates) [endpoint](https://exchangeratesapi.io/documentation/#latestrates) returns exchange rate data in real-time for all available currencies or for a specific set.

#### Currency Conversion

The [`convert`](https://exchangeratesapi.io/documentation/#convertcurrency) [endpoint](https://exchangeratesapi.io/documentation/#convertcurrency) enables to convert an amount, from any currency to any other one within the supported 168 currencies.

#### Historical Rates

This endpoint [has the shape](https://exchangeratesapi.io/documentation/#historicalrates) [`YYYY-MM-DD`](https://exchangeratesapi.io/documentation/#historicalrates) (such as `2021-03-20`), corresponding to the date for which we want to retrieve historical exchange rate information.

#### Time-Series Data

The [`timeseries`](https://exchangeratesapi.io/documentation/#timeseries) [endpoint](https://exchangeratesapi.io/documentation/#timeseries) returns the daily historical data for exchange rates between two specified dates, for a maximum timeframe of 365 days.

#### Fluctuation Data

The [`fluctuation`](https://exchangeratesapi.io/documentation/#fluctuation) [endpoint](https://exchangeratesapi.io/documentation/#fluctuation) returns the fluctuation data between specified dates, for a maximum timeframe of 365 days.

## Fetching Data From The API

In order to implement the currency convertor, we can use the `convert` endpoint (for which we need be subscribed to the Basic tier):

<pre><code class="language-javascript">https://api.exchangeratesapi.io/v1/convert
 ?access_key=YOUR_API_KEY
 &from=GBP
 &to=JPY
 &amount=25
</code></pre>

The response we will obtain looks like this:

<pre><code class="language-javascript">{
 "success": true,
 "query": {
   "from": "GBP",
   "to": "JPY",
   "amount": 25
 },
 "info": {
   "timestamp": 1620904845,
   "rate": 154.245331
 },
 "historical": "",
 "date": "2021-05-14",
 "result": 3856.079212
}
</code></pre>

Because the data is exposed via a REST API, we can conveniently retrieve it for any application based on any stack, whether it runs on the client-side or server-side, without having to install any additional library.

### Client-Side

The following JavaScript code connects to the API, and prints the converted amount and exchange rate in the console:

<div class="break-out">

<pre><code class="language-javascript">// Set endpoint and your access key
const access_key = 'YOUR_API_KEY';
const from = 'GPB';
const to = 'JPY';
const amount = 25;
const url = `https://api.exchangeratesapi.io/v1/convert?access_key=${ access_key }&from=${ from }&to=${ to }&amount=${ amount }`;

// Get the most recent exchange rates via the "latest" endpoint:
fetch(url)
 .then(response =&gt; response.json())
 .then(data =&gt; {
   // If our tier does not support the requested endpoint, we will get an error
   if (data.error) {
     console.log('Error:', data.error);
     return;
   }

   // We got the data
   console.log('Success:', data);
   console.log('Converted amount: ' + data.result);
   console.log('(Exchange rate: ' + data.info.rate + ')');
 })
 .catch((error) =&gt; {
   console.error('Error:', error);
 });
</code></pre>
</div>

### Server-Side

The following code demonstrates how to connect to the REST API, and print the converted result, [within a PHP application](https://exchangeratesapi.io/documentation/#phpcurl).

The same procedure can be implemented for other languages:

- Define the endpoint URL, attach your API access key.
- Connect to the endpoint, retrieve its response in JSON format.
- Decode the JSON data into an object/array.
- Obtain the converted amount from under the `result` property.

<div class="break-out">

<pre><code class="language-javascript">// Set endpoint and your access key
$access_key = 'YOUR_API_KEY';
$from = 'GBP';
$to = 'JPY';
$amount = 25;

// Initialize CURL:
$ch = curl_init("https://api.exchangeratesapi.io/v1/convert?access_key=${access_key}&from=${from}&to=${to}&amount=${amount}");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

// Get the JSON data:
$json = curl_exec($ch);
curl_close($ch);

// Decode JSON response:
$conversionResult = json_decode($json, true);

// Access the converted amount
echo $conversionResult['result'];
</code></pre>
</div>

## Conclusion

[ExchangeRatesApi.io](https://exchangeratesapi.io/?utm_source=SmashingMagazine&utm_medium=ThirdParties&utm_content=Article-exchangerateapi) was born as an [open-source project](https://github.com/exchangeratesapi/exchangeratesapi), with the intention to provide current and historical foreign exchange rates published by the European Central Bank, and written in Python.

If you’d like to incorporate currency conversion for your online shop, to emulate Amazon and provide a compelling user experience for your visitors, then you can download and install the open-source project.

And you can also make it much easier: If you’d like to have your currency convertor working in no time, for any programming language, accessing always up-to-date data which includes a wide array of commercial sources, and from a super-fast API with uptime of nearly 100% (99.9% in the last 12 months), then check out [ExchangeRatesApi.io](https://exchangeratesapi.io/?utm_source=SmashingMagazine&utm_medium=ThirdParties&utm_content=Article-exchangerateapi).

{{< signature "vf, yk, il" >}}
