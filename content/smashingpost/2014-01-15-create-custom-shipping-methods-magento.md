---
title: How To Create Custom Shipping Methods In Magento
slug: create-custom-shipping-methods-magento
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b823902c-8c67-4d36-beb6-0570a97b0ccd/illu-magento.jpg'
date: 2014-01-15T11:51:34.000Z
author: matthew-haworth
description: >-
  In this tutorial, we will use Magento’s powerful shipping-method code
  abstraction to create a shipping carrier. We will create two shipping methods
  that provide a fixed shipping price, allow for free shipping promotions,
  define logic based on an item’s weight and, finally, make it all configurable
  in the admin panel.
categories:
  - Coding
  - PHP
  - Techniques
  - Magento
---
In this tutorial, we will use Magento’s powerful shipping-method code abstraction to create a shipping carrier. We will create three shipping methods that provide a fixed shipping price, allow for free shipping promotions, define logic based on an item’s weight and, finally, make it all configurable in the admin panel.

We will cover the following:

*   Extend the abstract shipping class and implement the required methods.
*   Make the shipping method configurable in Magento’s admin panel.
*   Work with promotions to allow for free shipping.
*   Allow tracking codes to be set against an order.</p>

## Before We Start

This tutorial assumes that <strong>you are familiar with how to create a Magento module</strong>. If you are not, please first refer to an earlier tutorial in this series, “<a href="https://www.smashingmagazine.com/2012/03/01/basics-creating-magento-module/">The Basics of Creating a Magento Module</a>.” To begin, you will need a Community or Enterprise installation of Magento, either locally or on a server that you are able to access.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Introducing The Magento Layout</span>](https://www.smashingmagazine.com/2012/11/introducing-magento-layout/)
*   [The Basics Of Creating A Magento Module](https://www.smashingmagazine.com/2012/03/basics-creating-magento-module/)
*   [<span class="headline">How To Create An Affiliate Tracking Module In Magento</span>](https://www.smashingmagazine.com/2013/02/creating-an-affiliate-tracking-module-in-magento/)
*   [35 Free High-Quality E-Commerce Templates](https://www.smashingmagazine.com/2009/01/35-free-high-quality-e-commerce-templates/)

The logic we will implement in this tutorial could be client-specific, so we will implement our module as a “local module” and, therefore, create it in <code>app/code/local</code>. Let’s start by creating the following file structure:

<pre><code class="language-php">
app
  - code
    - local
      - SmashingMagazine
        - MyCarrier
          - Model
            - Carrier.php
          - etc
            - config.xml
            - system.xml
  - etc
    - modules
      - SmashingMagazine_MyCarrier.xml</code></pre>

Now we can create <code>SmashingMagazine_MyCarrier.xml</code>:

<pre><code class="language-markup">
&lt;?xml version="1.0"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_MyCarrier&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;codePool&gt;local&lt;/codePool&gt;
            &lt;depends&gt;
                &lt;Mage_Shipping /&gt;
            &lt;/depends&gt;
        &lt;/SmashingMagazine_MyCarrier&gt;
    &lt;/modules&gt;
&lt;/config&gt;
</code></pre>

Notice the dependency on the shipping module. This ensures that our SmashingMagazine MyCarrier module will load after the Mage Shipping module, and it will throw an error if the Mage Shipping module has been disabled.</p>

## Carriers, Methods, Requests And Results

Before continuing, we should understand the terminology that Magento uses throughout its shipping abstraction. A “carrier” represents a shipping carrier in the sense you would expect (DPD, FedEx, etc.). Each carrier has one or many shipping methods, which contain the carrier code, the carrier title, the method code, the method title, a price to be paid by the customer and a cost of shipping to the retailer (optional).

During [the checkout process](https://www.scnsoft.com/blog/magento-checkout), **Magento creates a shipping-rate “request” object that contains all of the shipping information**. The request can be used to determine which rates apply. For example, an “express” shipping method might not apply to orders under $10. All applicable rates are then “appended” to a shipping-rate “result” object, which generates a list of methods for the customer to choose from.

The following list names these concepts defined above, along with their representation as Magento classes:

*   Request `Mage_Shipping_Model_Rate_Request`
*   Result `Mage_Shipping_Model_Rate_Result`
*   Method `Mage_Shipping_Model_Rate_Result_Method`
*   Carrier Any class that extends the abstract class `Mage_Shipping_Model_Carrier_Abstract` and implements the interface `Mage_Shipping_Model_Carrier_Interface`

## Extending The Shipping Abstract

To create our shipping carrier, we need to extend <code>Mage_Shipping_Model_Carrier_Abstract</code>, implement <code>Mage_Shipping_Model_Carrier_Interface</code> and add the required abstract methods.

The <strong>most important method</strong> is <code>collectRates</code>. This is the method that receives a shipping request, appends applicable shipping methods and returns a shipping result.

Copy the following code into <code>app/code/local/SmashingMagazine/MyCarrier/Model/Carrier.php</code>:

<pre><code class="language-php">
&lt;?php
class SmashingMagazine_MyCarrier_Model_Carrier
    extends Mage_Shipping_Model_Carrier_Abstract
    implements Mage_Shipping_Model_Carrier_Interface
{
    protected $_code = 'smashingmagazine_mycarrier';

    public function collectRates(
        Mage_Shipping_Model_Rate_Request $request
    )
    {
        return Mage::getModel('shipping/rate_result');
    }

    public function getAllowedMethods()
    {
        return array();
    }
}
</code></pre>

This is <strong>the skeleton for a shipping method class</strong>, but it is pretty useless because we have no shipping methods.

Let’s start by hardcoding a method. This method will be called “standard” and have a price of $4.99. For now, we will assume there is no cost to the retailer.

<pre><code class="language-php">
&lt;?php
class SmashingMagazine_MyCarrier_Model_Carrier
    extends Mage_Shipping_Model_Carrier_Abstract
    implements Mage_Shipping_Model_Carrier_Interface
{
    protected $_code = 'smashingmagazine_mycarrier';

    public function collectRates(
        Mage_Shipping_Model_Rate_Request $request
    )
    {
        $result = Mage::getModel('shipping/rate_result');
        /* @var $result Mage_Shipping_Model_Rate_Result */

        $result-&gt;append($this-&gt;_getStandardShippingRate());

        return $result;
    }

    protected function _getStandardShippingRate()
    {
        $rate = Mage::getModel('shipping/rate_result_method');
        /* @var $rate Mage_Shipping_Model_Rate_Result_Method */

        $rate-&gt;setCarrier($this-&gt;_code);
        /**
         * getConfigData(config_key) returns the configuration value for the
         * carriers/[carrier_code]/[config_key]
         */
        $rate-&gt;setCarrierTitle($this-&gt;getConfigData('title'));

        $rate-&gt;setMethod('standand');
        $rate-&gt;setMethodTitle('Standard');

        $rate-&gt;setPrice(4.99);
        $rate-&gt;setCost(0);

        return $rate;
    }

    public function getAllowedMethods()
    {
        return array(
            'standard' =&gt; 'Standard',
        );
    }
}
</code></pre>

Now we are just one step away from a working shipping method — the module configuration file.</p>

### Module Configuration

The module configuration has the standard structure (as detailed in “<a title="The Basics Of Creating A Magento Module" href="https://www.smashingmagazine.com/2012/03/01/basics-creating-magento-module/">The Basics of Creating a Magento Module</a>”). Copy the following into <code>app/code/local/SmashingMagazine/MyCarrier/etc/config.xml</code>:

<pre><code class="language-markup">
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_MyCarrier&gt;
            &lt;module&gt;0.0.1&lt;/module&gt;
        &lt;/SmashingMagazine_MyCarrier&gt;
    &lt;/modules&gt;
    &lt;global&gt;
        &lt;models&gt;
            &lt;smashingmagazine_mycarrier&gt;
                &lt;class&gt;SmashingMagazine_MyCarrier_Model&lt;/class&gt;
            &lt;/smashingmagazine_mycarrier&gt;
        &lt;/models&gt;
    &lt;/global&gt;
    &lt;!-- Default configuration --&gt;
    &lt;default&gt;
        &lt;carriers&gt;
            &lt;smashingmagazine_mycarrier&gt;
                &lt;active&gt;1&lt;/active&gt;
                &lt;!--
                     This configuration should not be made visible
                     to the administrator, because it specifies
                     the model to be used for this carrier.
                --&gt;
                &lt;model&gt;smashingmagazine_mycarrier/carrier&lt;/model&gt;
                &lt;!--
                    The title as referenced in the carrier class
                --&gt;
                &lt;title&gt;Smashing Magazine Carrier&lt;/title&gt;
                &lt;!--
                    The sort order specifies the position that
                    this carrier appears relative to the other
                    carriers available in checkout.
                --&gt;
                &lt;sort_order&gt;10&lt;/sort_order&gt;
                &lt;!--
                    Out of the box, Magento offers shipping
                    carriers the ability to restrict themselves
                    to specific countries. For this configuration
                    option, 0 means allow all countries available,
                    and 1 means allow all countries specified
                    in the country list that we will add later
                    in system.xml
                --&gt;
                &lt;sallowspecific&gt;0&lt;/sallowspecific&gt;
            &lt;/smashingmagazine_mycarrier&gt;
        &lt;/carriers&gt;
    &lt;/default&gt;
&lt;/config&gt;
</code></pre>

This default configuration “registers” the model we have just created as a shipping carrier. As you may know, <strong>Magento merges all of its configuration XML together</strong> and caches the result (if the cache is enabled). When a customer loads the shipping-method list, Magento loops through all of the carriers in the carriers node of the configuration and loads the shipping methods from the models determined by the “active” carriers.

We should now be able to see our shipping method in the checkout.</p>

## Making It Configurable

We have already specified the default configuration for this module. So, let’s make our module configurable in the admin panel by copying the following into <code>app/code/local/SmashingMagazine/etc/system.xml</code>:

<pre><code class="language-markup">
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;sections&gt;
        &lt;carriers translate="label" module="shipping"&gt;
            &lt;groups&gt;
                &lt;smashingmagazine_mycarrier translate="label"&gt;
                    &lt;label&gt;Smashing Magazine Carrier&lt;/label&gt;
                    &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                    &lt;sort_order&gt;2&lt;/sort_order&gt;
                    &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                    &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                    &lt;show_in_store&gt;1&lt;/show_in_store&gt;
                    &lt;fields&gt;
                        &lt;!--
                            The following fields are available
                            to modify in the admin panel.
                            The values are saved in the
                            database.

                            This shipping carrier abstract checks
                            this value to determine whether
                            the carrier should be shown.
                        --&gt;
                        &lt;active translate="label"&gt;
                            &lt;label&gt;Enabled&lt;/label&gt;
                            &lt;frontend_type&gt;select&lt;/frontend_type&gt;
                            &lt;source_model&gt;adminhtml/system_config_source_yesno&lt;/source_model&gt;
                            &lt;sort_order&gt;1&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;0&lt;/show_in_store&gt;
                        &lt;/active&gt;
                        &lt;!--
                            This value can be used to specify a
                            custom title for our method.
                        --&gt;
                        &lt;title translate="label"&gt;
                            &lt;label&gt;Title&lt;/label&gt;
                            &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                            &lt;sort_order&gt;2&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;1&lt;/show_in_store&gt;
                        &lt;/title&gt;
                        &lt;!--
                            The sort order is used in Magento
                            to determine what order the carrier
                            will appear in relative to the
                            other carriers available.
                        --&gt;
                        &lt;sort_order translate="label"&gt;
                            &lt;label&gt;Sort Order&lt;/label&gt;
                            &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                            &lt;sort_order&gt;100&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;0&lt;/show_in_store&gt;
                        &lt;/sort_order&gt;
                        &lt;!--
                            This value is used to specify whether
                            the carrier is available only for
                            specific countries or all countries
                            available in the current Magento
                            installation.
                        --&gt;
                        &lt;sallowspecific translate="label"&gt;
                            &lt;label&gt;Ship to Applicable Countries&lt;/label&gt;
                            &lt;frontend_type&gt;select&lt;/frontend_type&gt;
                            &lt;sort_order&gt;90&lt;/sort_order&gt;
                            &lt;frontend_class&gt;shipping-applicable-country&lt;/frontend_class&gt;
                            &lt;source_model&gt;adminhtml/system_config_source_shipping_allspecificcountries&lt;/source_model&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;0&lt;/show_in_store&gt;
                        &lt;/sallowspecific&gt;
                        &lt;!--
                            If 'specific countries' is chosen
                            in the previous option, then this field
                            allows the administrator to specify
                            which specific countries this carrier
                            should be available for.
                        --&gt;
                        &lt;specificcountry translate="label"&gt;
                            &lt;label&gt;Ship to Specific Countries&lt;/label&gt;
                            &lt;frontend_type&gt;multiselect&lt;/frontend_type&gt;
                            &lt;sort_order&gt;91&lt;/sort_order&gt;
                            &lt;source_model&gt;adminhtml/system_config_source_country&lt;/source_model&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;0&lt;/show_in_store&gt;
                            &lt;can_be_empty&gt;1&lt;/can_be_empty&gt;
                        &lt;/specificcountry&gt;
                    &lt;/fields&gt;
                &lt;/smashingmagazine_mycarrier&gt;
            &lt;/groups&gt;
        &lt;/carriers&gt;
    &lt;/sections&gt;
&lt;/config&gt;
</code></pre>

These fields are visible in the admin panel by navigating to <code>System → Configuration → Shipping Method → Smashing Magazine Carrier</code>.</p>

## Using Multiple Shipping Methods

### Express Shipping

So far, we have added a standard shipping method for the price of $9.99. However, the customer may wish to pay more to receive their order faster. The following code creates a shipping rate with a higher price and different shipping code:

<pre><code class="language-php">
protected function _getExpressShippingRate()
{
    $rate = Mage::getModel('shipping/rate_result_method');
    /* @var $rate Mage_Shipping_Model_Rate_Result_Method */
    $rate-&gt;setCarrier($this-&gt;_code);
    $rate-&gt;setCarrierTitle($this-&gt;getConfigData('title'));
    $rate-&gt;setMethod('express');
    $rate-&gt;setMethodTitle('Express (Next day)');
    $rate-&gt;setPrice(12.99);
    $rate-&gt;setCost(0);
    return $rate;
}
</code></pre>

To make this shipping rate appear next to the standard rate that we created earlier, we will need to modify the code in the <code>collectRates</code> method to append the new rate. Add the following before the return statement:

<pre><code class="language-php">
$result-&gt;append($this-&gt;_getExpressShippingRate());
</code></pre>

Finally, add the shipping method to the allowed methods array in <code>getAllowedMethods</code>:

<pre><code class="language-php">
public function getAllowedMethods()
{
    return array(
        'standard' =&gt; 'Standard',
        'express' =&gt; 'Express',
    );
}
</code></pre>

### Free Shipping

Many websites offer free shipping when a customer spends over a certain amount or satisfies certain conditions. We need to be able to do the same here. In Magento, you can set up a “Shopping Cart Rule.” With it, you can <strong>specify a set of conditions and define actions if those conditions are met</strong>; one of those actions is free shipping.

If free shipping is available for a customer, then the <code>request</code> object will populated with <code>is_free_shipping</code> set to <code>1</code>. We need to check for and handle this possibility in our shipping method. Add the following before the return statement in the <code>collectRates</code> method:

<pre><code class="language-php">
if ($request-&gt;getFreeShipping()) {
    /**
     *  If the request has the free shipping flag,
     *  append a free shipping rate to the result.
     */
    $freeShippingRate = $this-&gt;_getFreeShippingRate();
    $result-&gt;append($freeShippingRate);
}
</code></pre>

Add the following code to <code>app/code/local/SmashingMagazine/MyCarrier/Model/Carrier.php</code>:

<pre><code class="language-php">
protected function _getFreeShippingRate()
{
    $rate = Mage::getModel('shipping/rate_result_method');
    /* @var $rate Mage_Shipping_Model_Rate_Result_Method */
    $rate-&gt;setCarrier($this-&gt;_code);
    $rate-&gt;setCarrierTitle($this-&gt;getConfigData('title'));
    $rate-&gt;setMethod('free_shipping');
    $rate-&gt;setMethodTitle('Free Shipping (3 - 5 days)');
    $rate-&gt;setPrice(0);
    $rate-&gt;setCost(0);
    return $rate;
}
</code></pre>

Remember to add the method to the allowed methods array:

<pre><code class="language-php">
public function getAllowedMethods()
{
    return array(
        'standard' =&gt; 'Standard',
        'express' =&gt; 'Express',
        'free_shipping' =&gt; 'Free Shipping',
    );
}
</code></pre>

## Taking It A Bit Further

### Tracking Deliveries

Tracking numbers may be added to shipments through either the admin panel or an API. But to make our shipping methods visible in the admin panel, we will have to overwrite the <code>isTrackingAvailable</code> method in the abstract to return <code>true</code>.

Add the following method to the end of <code>SmashingMagazine_MyCarrier_Model_Carrier</code>.

<pre><code class="language-php">
public function isTrackingAvailable()
{
    return true;
}
</code></pre>

You should now see the shipping carriers and methods available in the delivery courier drop-down menu when you try to place a shipment in the admin panel.</p>

### Using the Weight

Earlier, we added a more expensive express shipping method. But heavier items that require complex shipping arrangements might not be available for next-day delivery. We can check for this using the weight attribute of the request object by wrapping the code that appends the shipping method to the shipping result:

<pre><code class="language-php">
// ...
$expressWeightThreshold =
    $this-&gt;getConfigData('express_weight_threshold');

$eligibleForExpressDelivery = true;
foreach ($request-&gt;getAllItems() as $_item) {
    if ($_item-&gt;getWeight() &gt; $expressWeightThreshold) {
        $eligibleForExpressDelivery = false;
    }
}

if ($eligibleForExpressDelivery) {
    $result-&gt;append($this-&gt;_getExpressShippingRate());
}
// ...
</code></pre>

Notice that we have added a reference to the configuration. To make this appear in the admin panel, we need to add the following XML to the <code>app/code/local/SmashingMagazine/MyCarrier/etc/system.xml</code> file in the <code>fields</code> node:

<pre><code class="language-markup">
&lt;express_weight_threshold translate="label"&gt;
    &lt;label&gt;Express Weight Threshold&lt;/label&gt;
    &lt;frontend_type&gt;text&lt;/frontend_type&gt;
    &lt;sort_order&gt;100&lt;/sort_order&gt;
    &lt;show_in_default&gt;1&lt;/show_in_default&gt;
    &lt;show_in_website&gt;1&lt;/show_in_website&gt;
    &lt;show_in_store&gt;0&lt;/show_in_store&gt;
&lt;/express_weight_threshold&gt;
</code></pre>

## Summary

With a relatively small amount of code, we have been able to define our own shipping logic that integrates with checkout, the admin panel and even the shopping-cart promotions. You can learn much more about creating shipping modules in Magento by looking at the examples in the core files — namely, <code>Mage_Usa</code> and <code>Mage_Shipping</code>.

The code from this tutorial can be downloaded <a href="https://amp.co/K457V">here</a>.

I welcome any questions and would love to hear your feedback in the comments area below.

{{< signature "al, ea" >}}

