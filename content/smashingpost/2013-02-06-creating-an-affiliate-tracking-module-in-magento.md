---
title: How To Create An Affiliate Tracking Module In Magento
slug: creating-an-affiliate-tracking-module-in-magento
image: null
date: 2013-02-06T11:11:06.000Z
author: joseph-mcdermott
description: >-
  In this tutorial, we will create a Magento module that will capture an affiliate referral from a third-party source (e.g. an external website or newsletter) and include a HTML script on the checkout success page once this referral has been converted.
categories:
  - Coding
  - Frameworks
  - Magento
---
We will be covering the following topics:

*   Capturing URI request data,
*   Saving to and retrieving values from cookies,
*   Adding custom content to the checkout success page,
*   Adding module configuration to the Magento admin panel,
*   Creating a community module with no hard-coded settings.

As always, this module will be written in such a way that no core files are modified, making it portable and Magento-upgrade friendly.</p>

{{% feature-panel %}}

## Before We Start

This tutorial assumes you are already familiar with <a href="/2012/03/01/basics-creating-magento-module/">the basics of creating a Magento module</a>, and builds upon the points covered in <a href="/2012/11/30/introducing-magento-layout/">our previous article on the Magento Layout</a>, so it might be worth brushing up on both if you are not familiar with either.

We will be adding any website-specific settings as configurable options in the Magento admin panel, and as a result, our module is a “community module” whose code belongs in <code>app/code/community</code>, the idea being that we can drop this community module onto any Magento instance, and no code modification will be required to get it working.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/335ca589-1dd4-4f77-a0da-b140bf846e70/creating-an-affiliate-tracking-module-in-magento-opt.png"><img loading="lazy" decoding="async" class="123413" title="Creating-An-Affiliate-Tracking-Module-In-Magento-opt" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/335ca589-1dd4-4f77-a0da-b140bf846e70/creating-an-affiliate-tracking-module-in-magento-opt.png" alt="" width="500" height="400" /></a></figure>

To begin with, create the following file structure with empty files ready to be populated later.

<pre><code class="language-markup tmp-xml">app
  - code
      - community
          - SmashingMagazine
              - Affiliate
                  - Block
                      - Conversion.php
                  - Model
                      - Observer.php
                  - etc
                      - config.xml
  - design
      - frontend
          - base
              - default
                  - layout
                      - smashingmagazine_affiliate.xml
                  - template
                      - smashingmagazine_affiliate
                          - conversion.phtml

  - etc
      - modules
          - SmashingMagazine_Affiliate.xml</code></pre>

We can already complete the content of <code>SmashingMagazine_Affiliate.xml</code>:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Affiliate&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;codePool&gt;community&lt;/codePool&gt;
        &lt;/SmashingMagazine_Affiliate&gt;
    &lt;/modules&gt;
&lt;/config&gt;</code></pre>

## Capturing The Affiliate Referral

The first task of an affiliate-tracking process is to capture the referral, which is generally provided as a <code>$&#95;GET</code> parameter in a URI from a third-party website or newsletter. For example <code>smashingmagazine.com/&amp;quest;utm_source=some_affiliate_id</code> where <code>some_affiliate</code> is the ID of the affiliate we will reward if our customer completes a purchase.</p>

### Defining An Event Observer

We want our affiliates to be able to link to any page of our website, so that our customers can click directly to the product or service of interest. Therefore, we need a method of checking for this <code>$&#95;GET</code> parameter on every page. As always, we don't want to modify any Magento core code since we want our module to be as portable and upgrade-friendly as possible, so we will be using an <code>event observer</code>.

One event that is dispatched on every page is <code>controller_front_init_before</code>, so let's create our <code>config.xml</code> with an <code>observer</code> for this event.

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Affiliate&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_Affiliate&gt;
    &lt;/modules&gt;
    &lt;global&gt;
        &lt;models&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Model&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/models&gt;
        &lt;events&gt;
            &lt;controller_front_init_before&gt;
                &lt;observers&gt;
                    &lt;smashingmagazine_affiliate&gt;
                        &lt;class&gt;smashingmagazine_affiliate/observer&lt;/class&gt;
                        &lt;method&gt;captureReferral&lt;/method&gt;
                        &lt;type&gt;singleton&lt;/type&gt;
                    &lt;/smashingmagazine_affiliate &gt;
                &lt;/observers&gt;
            &lt;/controller_front_init_before&gt;
        &lt;/events&gt;
    &lt;/global&gt;
&lt;/config&gt;</code></pre>

Now, on every page load, our method <code>SmashingMagazine_Affiliate_Model_Observer::captureReferral()</code> will be called, so let's add our <code>Observer.php</code> content:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Model_Observer
{
    public function captureReferral(Varien_Event_Observer $observer)
    {
        // here we add the logic to capture the referring affiliate ID
    }
}</code></pre>

### Capturing the Affiliate ID

The event <code>controller_front_init_before</code> is dispatched from the Magento core method <code>Mage_Core_Controller_Varien_Front::init()</code>, and includes a reference to the same class in the dispatched event, as per the following code snippet from <code>app/code/core/Mage/Core/Controller/Varien/Front.php</code>:

<pre><code class="language-php">Mage::dispatchEvent(
    'controller_front_init_before',
    array('front' =&gt; $this)
);</code></pre>

We can therefore gain access to this instance of <code>Mage_Core_Controller_Varien_Front</code> by including the following code in our <code>event observer</code>:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Model_Observer
{
    public function captureReferral(Varien_Event_Observer $observer)
    {
        $frontController = $observer-&gt;getEvent()-&gt;getFront();
    }
}</code></pre>

Since the <code>controller</code> is responsible for the parsing of URI's, we now have access to the appropriate object we need to determine whether our <code>$&#95;GET</code> parameter exists:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Model_Observer
{
    public function captureReferral(Varien_Event_Observer $observer)
    {
        $frontController = $observer-&gt;getEvent()-&gt;getFront();

        $utmSource = $frontController-&gt;getRequest()
            -&gt;getParam('utm_source', false);

        if ($utmSource) {
            // here we will save the referrer affiliate ID
        }
    }
}</code></pre>

In the above code, we are calling <code>getRequest()</code> to retrieve the <code>Mage_Core_Controller_Request_Http</code> instance from the <code>controller</code>, which will contain all of the information we need about the current URI request, including any <code>$&#95;POST</code> or <code>$&#95;GET</code> parameters. We are interested in the <code>$&#95;GET</code> parameter <code>utm_source</code>, and we can retrieve its value with the <code>getParam()</code> method.

If present in the current URI, the variable <code>$utmSource</code> will now contain our referring affiliate's ID.</p>

### Saving the Affiliate ID

Now we need to save the <code>$utmSource</code> value so that we can reward this affiliate should our customer proceed to make a purchase. There are a number of ways to do this, but for this tutorial we will simply use a <code>$&#95;COOKIE</code>. Magento has core functionality for dealing with <code>cookie</code>s, so this is very straightforward:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Model_Observer
{
    const COOKIE_KEY_SOURCE = 'smashingmagazine_affiliate_source';

    public function captureReferral(Varien_Event_Observer $observer)
    {
        $frontController = $observer-&gt;getEvent()-&gt;getFront();

        $utmSource = $frontController-&gt;getRequest()
            -&gt;getParam('utm_source', false);

        if ($utmSource) {
            Mage::getModel('core/cookie')-&gt;set(
                self::COOKIE_KEY_SOURCE,
                $utmSource,
                $this-&gt;_getCookieLifetime()
            );
        }
    }

    protected function _getCookieLifetime()
    {
        $days = 30;

        // convert to seconds
        return (int)86400 * $days;
    }
}</code></pre>

We have defined a new constant, <code>COOKIE_KEY_SOURCE</code>, because we will be referencing this same value from a different class. When referencing a value like this from multiple locations, it is good practice to use a constant. This way, we keep refactoring work to a minimum should the value ever need to change. We have also defined a new protected method, <code>&#95;getCookieLifetime()</code>, for retrieving the <code>cookie</code> lifetime, which we have hard coded to 30 days from now.</p>

## Notifying The Affiliate Upon Conversion

At this point, we now have an affiliate ID stored in a <code>cookie</code>, and let's assume our referred customer has added some products to their basket, completed the checkout process and is now on the checkout success page. This is where most affiliate schemes will require some notification that a referral has been converted to an order, usually by way of including a snippet of JavaScript or a tiny image at the bottom of the page.

Recommended reading: [Fundamental Guidelines Of E-Commerce Checkout Design](https://www.smashingmagazine.com/2011/04/fundamental-guidelines-of-e-commerce-checkout-design/)

There are, of course, other methods of updating affiliates, for example via server-side API calls which can be achieved with further <code>event observers</code>, but for this tutorial we will utilize the <a href="https://www.smashingmagazine.com/2012/11/introducing-magento-layout/">Magento layout</a> to introduce some custom HTML at the bottom of the order success page.

We need to update our <code>config.xml</code> to cater to <code>blocks</code> and layout updates:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Affiliate&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_Affiliate&gt;
    &lt;/modules&gt;
    &lt;global&gt;
        &lt;blocks&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Block&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/blocks&gt;
        &lt;models&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Model&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/models&gt;
        &lt;events&gt;
            &lt;controller_front_init_before&gt;
                &lt;observers&gt;
                    &lt;smashingmagazine_affiliate&gt;
                        &lt;class&gt;smashingmagazine_affiliate/observer&lt;/class&gt;
                        &lt;method&gt;captureReferral&lt;/method&gt;
                        &lt;type&gt;singleton&lt;/type&gt;
                    &lt;/smashingmagazine_affiliate &gt;
                &lt;/observers&gt;
            &lt;/controller_front_init_before&gt;
        &lt;/events&gt;
    &lt;/global&gt;
    &lt;frontend&gt;
        &lt;layout&gt;
            &lt;updates&gt;
                &lt;smashingmagazine_affiliate
                         module="SmashingMagazine_Affiliate"&gt;
                    &lt;file&gt;smashingmagazine_affiliate.xml&lt;/file&gt;
                &lt;/smashingmagazine_affiliate&gt;
            &lt;/updates&gt;
        &lt;/layout&gt;
    &lt;/frontend&gt;
&lt;/config&gt;</code></pre>

### Adding a New Layout File

The layout handle we are interested in is <code>onepage_checkout_success</code>, since this is the handle for the checkout success page that our customer has arrived at. Let's update our layout file, <code>smashingmagazine_affiliate.xml</code>:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;layout&gt;
    &lt;checkout_onepage_success&gt;
        &lt;reference name="before_body_end"&gt;
            &lt;block type="smashingmagazine_affiliate/conversion"
              name="smashingmagazine_affiliate_conversion"
              template="smashingmagazine_affiliate/conversion.phtml" /&gt;
        &lt;/reference&gt;
    &lt;/checkout_onepage_success&gt;
&lt;/layout&gt;</code></pre>

### Adding A New Template File

The content of <code>conversion.phtml</code> will depend on the requirements of the specific affiliate we are building the module for, so for now we will use a generic format that includes a one pixel image with a dynamic merchant and affiliate ID:

<pre><code class="language-markup tmp-html">&lt;img
    src="/themes/smashingv4/images/logo.png
      &amp;quest;merchant_id=&lt;&amp;quest;php echo $this-&gt;getMerchantId() &amp;quest;&gt;
      &amp;affiliate_id=&lt;&amp;quest;php echo $this-&gt;getAffiliateId() &amp;quest;&gt;"
    width="1"
    height="1"
/&gt;</code></pre>

### Creating a Custom Block

Now we need to create a new <code>block</code> for populating the dynamic data in our template:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Block_Conversion
    extends Mage_Core_Block_Template
{
    public function getMerchantId()
    {
        return '12345';
    }

    public function getAffiliateId()
    {
        return Mage::getModel('core/cookie')-&gt;get(
            SmashingMagazine_Affiliate_Model_Observer::COOKIE_KEY_SOURCE
        );
    }
}</code></pre>

## Adding Items To The Magento Admin Panel

At this point, we have a working module. All of our functionality is in place, and our hard-coded values will work for a single instance of Magento. We have the equivalent of a <em>local module</em>. The next step is to move these hard-coded values into the Magento admin panel, so they can be configured on multiple Magento instances without any code modification required.

It is quite straightforward to add items to the Magento admin panel system configuration, and it's ideal for saving website-specific credentials or settings, like in our case the merchant ID and <code>cookie</code> timeout value.

Now, let's log in to the Magento admin panel and navigate to <code>System</code> → <code>Configuration</code> using the main menu. We can see a number of tabs on the left-hand side for configuring the various elements of our Magento instance, such as “General,” “Web,” “Design,” etc. We are now going to add a new tab for our module's configuration items.</p>

### Adding New System Configuration Tab

Let's create a new XML file called <code>app/code/community/SmashingMagazine/Affiliate/etc/system.xml</code> and add to it the following content:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;

    &lt;!-- we are defining a new tab --&gt;
    &lt;tabs&gt;

        &lt;!-- our tab unique short name --&gt;
        &lt;smashingmagazine&gt;

            &lt;!-- the title of our tab in the admin panel sidebar --&gt;
            &lt;label&gt;Smashing Magazine&lt;/label&gt;

            &lt;!-- the order our tab should appear on the sidebar --&gt;
            &lt;sort_order&gt;100&lt;/sort_order&gt;

        &lt;/smashingmagazine&gt;

    &lt;/tabs&gt;

&lt;/config&gt;</code></pre>

### Configuring ACL Settings

Since we have added a new tab, we need to add a new entry to the Magento ACL (Access Control List) to allow access to this tab. Let's create a new file called <code>app/code/community/SmashingMagazine/Affiliate/etc/adminhtml.xml</code>, with the following content:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;adminhtml&gt;
    &lt;acl&gt;
        &lt;resources&gt;
            &lt;admin&gt;
                &lt;children&gt;
                    &lt;system&gt;
                        &lt;children&gt;
                            &lt;config&gt;
                                &lt;children&gt;
                                    &lt;smashingmagazine_affiliate&gt;
                                        &lt;title&gt;Smashing Magazine
                                               Affiliate&lt;/title&gt;
                                    &lt;/smashingmagazine_affiliate&gt;
                                &lt;/children&gt;
                            &lt;/config&gt;
                        &lt;/children&gt;
                    &lt;/system&gt;
                &lt;/children&gt;
            &lt;/admin&gt;
        &lt;/resources&gt;
    &lt;/acl&gt;
&lt;/adminhtml&gt;</code></pre>

Note: When making changes to the ACL, if you are already logged in to Magento you will have to log out and back in again for the new permissions to take effect. You may find you get a “404 page not found” when you try to access a newly-added tab that you do not have ACL access to.</p>

### Adding New System Configuration Items

Next we will update our <code>system.xml</code> to add the items that we want to be configurable:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;
    &lt;tabs&gt;
        &lt;smashingmagazine&gt;
            &lt;label&gt;Smashing Magazine&lt;/label&gt;
            &lt;sort_order&gt;100&lt;/sort_order&gt;
        &lt;/smashingmagazine&gt;
    &lt;/tabs&gt;

    &lt;!-- we are adding a new section to our tab --&gt;
    &lt;sections&gt;

        &lt;!-- unique shortname for our section --&gt;
        &lt;smashingmagazine_affiliate&gt;

            &lt;!-- the title of our section in the sidebar --&gt;
            &lt;label&gt;Affiliate Tracking&lt;/label&gt;

            &lt;!-- the tab under which we want our section to appear --&gt;
            &lt;tab&gt;smashingmagazine&lt;/tab&gt;

            &lt;!-- order of section relative to our tab --&gt;
            &lt;sort_order&gt;10&lt;/sort_order&gt;

            &lt;!-- visibility of our section --&gt;
            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
            &lt;show_in_store&gt;1&lt;/show_in_store&gt;

            &lt;!-- we are adding some new groups to our section --&gt;
            &lt;groups&gt;

                &lt;!-- the unique short code for our group --&gt;
                &lt;general&gt;

                    &lt;!-- the title of our group --&gt;
                    &lt;label&gt;General Settings&lt;/label&gt;

                    &lt;!-- order of group relative to the section --&gt;
                    &lt;sort_order&gt;10&lt;/sort_order&gt;

                    &lt;!-- visibility of our group --&gt;
                    &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                    &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                    &lt;show_in_store&gt;1&lt;/show_in_store&gt;

                    &lt;!-- we are adding some new fields to our group --&gt;
                    &lt;fields&gt;

                        &lt;!-- the unique short code for our field --&gt;
                        &lt;status&gt;

                            &lt;!-- the label of our field --&gt;
                            &lt;label&gt;Enabled&lt;/label&gt;

                            &lt;!-- the type of our field --&gt;
                            &lt;frontend_type&gt;select&lt;/frontend_type&gt;

                            &lt;!-- the source of our 'select' type --&gt;
                            &lt;source_model&gt;
                                adminhtml/system_config_source_enabledisable
                            &lt;/source_model&gt;

                            &lt;!-- order relative to the group --&gt;
                            &lt;sort_order&gt;10&lt;/sort_order&gt;

                            &lt;!-- visibility of our field --&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;0&lt;/show_in_store&gt;
                        &lt;/status&gt;
                        &lt;merchant_id&gt;
                            &lt;label&gt;Merchant ID&lt;/label&gt;
                            &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                            &lt;sort_order&gt;20&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;1&lt;/show_in_store&gt;
                        &lt;/merchant_id&gt;
                    &lt;/fields&gt;
                &lt;/general&gt;
                &lt;cookie&gt;
                    &lt;label&gt;Cookie Settings&lt;/label&gt;
                    &lt;sort_order&gt;20&lt;/sort_order&gt;
                    &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                    &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                    &lt;show_in_store&gt;1&lt;/show_in_store&gt;
                    &lt;fields&gt;
                        &lt;timeout&gt;
                            &lt;label&gt;Cookie Timeout&lt;/label&gt;
                            &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                            &lt;sort_order&gt;10&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;1&lt;/show_in_store&gt;

                            &lt;!--
                                we can add a comment that
                                will appear below the field
                            --&gt;
                            &lt;comment&gt;&lt;![CDATA[
                                This is the amount of time
                                an affiliate cookie will last, in days
                            ]]&gt;&lt;/comment&gt;
                        &lt;/timeout&gt;
                    &lt;/fields&gt;
                &lt;/cookie&gt;
            &lt;/groups&gt;
        &lt;/smashingmagazine_affiliate&gt;
    &lt;/sections&gt;
&lt;/config&gt;</code></pre>

### Defining Default Admin Panel Settings

Sometimes it is convenient to provide default values for your admin panel configuration settings. For example, it would be a good idea to provide a default value for the <code>cookie</code> timeout value. However, there may be no benefit in providing a default value for <code>merchant_id</code>, since it will always be different. Let's update our <code>config.xml</code> with a default <code>cookie</code> timeout value:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Affiliate&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_Affiliate&gt;
    &lt;/modules&gt;
    &lt;global&gt;
        &lt;blocks&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Block&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/blocks&gt;
        &lt;models&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Model&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/models&gt;
        &lt;events&gt;
            &lt;controller_front_init_before&gt;
                &lt;observers&gt;
                    &lt;smashingmagazine_affiliate&gt;
                        &lt;class&gt;smashingmagazine_affiliate/observer&lt;/class&gt;
                        &lt;method&gt;captureReferral&lt;/method&gt;
                        &lt;type&gt;singleton&lt;/type&gt;
                    &lt;/smashingmagazine_affiliate &gt;
                &lt;/observers&gt;
            &lt;/controller_front_init_before&gt;
        &lt;/events&gt;
    &lt;/global&gt;
    &lt;frontend&gt;
        &lt;layout&gt;
            &lt;updates&gt;
                &lt;smashingmagazine_affiliate
                         module="SmashingMagazine_Affiliate"&gt;
                    &lt;file&gt;smashingmagazine_affiliate.xml&lt;/file&gt;
                &lt;/smashingmagazine_affiliate&gt;
            &lt;/updates&gt;
        &lt;/layout&gt;
    &lt;/frontend&gt;

    &lt;!-- we are setting the default value --&gt;
    &lt;default&gt;

        &lt;!-- this is the section short name --&gt;
        &lt;smashingmagazine_affiliate&gt;

            &lt;!-- this is the group short name --&gt;
            &lt;cookie&gt;

                &lt;!-- this is the field short name --&gt;
                &lt;timeout&gt;30&lt;/timeout&gt;

            &lt;/cookie&gt;

        &lt;/smashingmagazine_affiliate&gt;

    &lt;/default&gt;

&lt;/config&gt;</code></pre>

## Accessing The System Configuration Values

Once all of the above is configured, and we have our default values in place, or have saved our settings through the admin panel, we can easily access these values with the following snippet:

<pre><code class="language-php">&lt;&amp;quest;php $value = Mage::getStoreConfig('system/config/path'); &amp;quest;&gt;</code></pre>

The <code>system/config/path</code> should be replaced with the configuration path to the particular setting you are interested in. For example, the path to our <code>merchant_id</code> setting would be <code>smashingmagazine_affiliate/general/merchant_id</code>.</p>

### Retrieving Our Cookie Timeout From Admin Panel

We previously had the <code>cookie</code> lifetime hard-coded to 30 days, which we can now replace with our Magento admin panel system configuration value:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Model_Observer
{
    const COOKIE_KEY_SOURCE = 'smashingmagazine_affiliate_source';

    public function captureReferral(Varien_Event_Observer $observer)
    {
        $frontController = $observer-&gt;getEvent()-&gt;getFront();

        &lt;!-- unique shortname for our section --&gt;
        &lt;smashingmagazine_affiliate&gt;

            &lt;!-- the title of our section in the sidebar --&gt;
            &lt;label&gt;Affiliate Tracking&lt;/label&gt;

            &lt;!-- the tab under which we want our section to appear --&gt;
            &lt;tab&gt;smashingmagazine&lt;/tab&gt;

            &lt;!-- order of section relative to our tab --&gt;
            &lt;sort_order&gt;10&lt;/sort_order&gt;

            &lt;!-- visibility of our section --&gt;
            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
            &lt;show_in_store&gt;1&lt;/show_in_store&gt;

            &lt;!-- we are adding some new groups to our section --&gt;
            &lt;groups&gt;

                &lt;!-- the unique short code for our group --&gt;
                &lt;general&gt;

                    &lt;!-- the title of our group --&gt;
                    &lt;label&gt;General Settings&lt;/label&gt;

                    &lt;!-- order of group relative to the section --&gt;
                    &lt;sort_order&gt;10&lt;/sort_order&gt;

                    &lt;!-- visibility of our group --&gt;
                    &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                    &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                    &lt;show_in_store&gt;1&lt;/show_in_store&gt;

                    &lt;!-- we are adding some new fields to our group --&gt;
                    &lt;fields&gt;

                        &lt;!-- the unique short code for our field --&gt;
                        &lt;status&gt;

                            &lt;!-- the label of our field --&gt;
                            &lt;label&gt;Enabled&lt;/label&gt;

                            &lt;!-- the type of our field --&gt;
                            &lt;frontend_type&gt;select&lt;/frontend_type&gt;

                            &lt;!-- the source of our 'select' type --&gt;
                            &lt;source_model&gt;
                                adminhtml/system_config_source_enabledisable
                            &lt;/source_model&gt;

                            &lt;!-- order relative to the group --&gt;
                            &lt;sort_order&gt;10&lt;/sort_order&gt;

                            &lt;!-- visibility of our field --&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;0&lt;/show_in_store&gt;
                        &lt;/status&gt;
                        &lt;merchant_id&gt;
                            &lt;label&gt;Merchant ID&lt;/label&gt;
                            &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                            &lt;sort_order&gt;20&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;1&lt;/show_in_store&gt;
                        &lt;/merchant_id&gt;
                    &lt;/fields&gt;
                &lt;/general&gt;
                &lt;cookie&gt;
                    &lt;label&gt;Cookie Settings&lt;/label&gt;
                    &lt;sort_order&gt;20&lt;/sort_order&gt;
                    &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                    &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                    &lt;show_in_store&gt;1&lt;/show_in_store&gt;
                    &lt;fields&gt;
                        &lt;timeout&gt;
                            &lt;label&gt;Cookie Timeout&lt;/label&gt;
                            &lt;frontend_type&gt;text&lt;/frontend_type&gt;
                            &lt;sort_order&gt;10&lt;/sort_order&gt;
                            &lt;show_in_default&gt;1&lt;/show_in_default&gt;
                            &lt;show_in_website&gt;1&lt;/show_in_website&gt;
                            &lt;show_in_store&gt;1&lt;/show_in_store&gt;

                            &lt;!--
                                we can add a comment that
                                will appear below the field
                            --&gt;
                            &lt;comment&gt;&lt;![CDATA[
                                This is the amount of time
                                an affiliate cookie will last, in days
                            ]]&gt;&lt;/comment&gt;
                        &lt;/timeout&gt;
                    &lt;/fields&gt;
                &lt;/cookie&gt;
            &lt;/groups&gt;
        &lt;/smashingmagazine_affiliate&gt;
    &lt;/sections&gt;
&lt;/config&gt;</code></pre>

### Defining Default Admin Panel Settings

Sometimes it is convenient to provide default values for your admin panel configuration settings. For example, it would be a good idea to provide a default value for the <code>cookie</code> timeout value. However, there may be no benefit in providing a default value for <code>merchant_id</code>, since it will always be different. Let's update our <code>config.xml</code> with a default <code>cookie</code> timeout value:

<pre><code class="language-markup tmp-xml">&lt;&amp;quest;xml version="1.0" encoding="UTF-8"&amp;quest;&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Affiliate&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_Affiliate&gt;
    &lt;/modules&gt;
    &lt;global&gt;
        &lt;blocks&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Block&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/blocks&gt;
        &lt;models&gt;
            &lt;smashingmagazine_affiliate&gt;
                &lt;class&gt;SmashingMagazine_Affiliate_Model&lt;/class&gt;
            &lt;/smashingmagazine_affiliate&gt;
        &lt;/models&gt;
        &lt;events&gt;
            &lt;controller_front_init_before&gt;
                &lt;observers&gt;
                    &lt;smashingmagazine_affiliate&gt;
                        &lt;class&gt;smashingmagazine_affiliate/observer&lt;/class&gt;
                        &lt;method&gt;captureReferral&lt;/method&gt;
                        &lt;type&gt;singleton&lt;/type&gt;
                    &lt;/smashingmagazine_affiliate &gt;
                &lt;/observers&gt;
            &lt;/controller_front_init_before&gt;
        &lt;/events&gt;
    &lt;/global&gt;
    &lt;frontend&gt;
        &lt;layout&gt;
            &lt;updates&gt;
                &lt;smashingmagazine_affiliate
                         module="SmashingMagazine_Affiliate"&gt;
                    &lt;file&gt;smashingmagazine_affiliate.xml&lt;/file&gt;
                &lt;/smashingmagazine_affiliate&gt;
            &lt;/updates&gt;
        &lt;/layout&gt;
    &lt;/frontend&gt;

    &lt;!-- we are setting the default value --&gt;
    &lt;default&gt;

        &lt;!-- this is the section short name --&gt;
        &lt;smashingmagazine_affiliate&gt;

            &lt;!-- this is the group short name --&gt;
            &lt;cookie&gt;

                &lt;!-- this is the field short name --&gt;
                &lt;timeout&gt;30&lt;/timeout&gt;

            &lt;/cookie&gt;

        &lt;/smashingmagazine_affiliate&gt;

    &lt;/default&gt;

&lt;/config&gt;</code></pre>

## Accessing The System Configuration Values

Once all of the above is configured, and we have our default values in place, or have saved our settings through the admin panel, we can easily access these values with the following snippet:

<pre><code class="language-php">&lt;&amp;quest;php $value = Mage::getStoreConfig('system/config/path'); &amp;quest;&gt;</code></pre>

The <code>system/config/path</code> should be replaced with the configuration path to the particular setting you are interested in. For example, the path to our <code>merchant_id</code> setting would be <code>smashingmagazine_affiliate/general/merchant_id</code>.</p>

### Retrieving Our Cookie Timeout From Admin Panel

We previously had the <code>cookie</code> lifetime hard-coded to 30 days, which we can now replace with our Magento admin panel system configuration value:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Model_Observer
{
    const COOKIE_KEY_SOURCE = 'smashingmagazine_affiliate_source';

    public function captureReferral(Varien_Event_Observer $observer)
    {
        $frontController = $observer-&gt;getEvent()-&gt;getFront();

        $utmSource = $frontController-&gt;getRequest()
            -&gt;getParam('utm_source', false);

        if ($utmSource) {
            Mage::getModel('core/cookie')-&gt;set(
                self::COOKIE_KEY_SOURCE,
                $utmSource,
                $this-&gt;_getCookieLifetime()
            );
        }
    }

    protected function _getCookieLifetime()
    {
        $days = Mage::getStoreConfig(
            'smashingmagazine_affiliate/cookie/timeout'
        );

        // convert to seconds
        return (int)86400 * $days;
    }
}</code></pre>

### Retrieving Our Merchant ID From Admin Panel

We can now complete our <code>block</code> by replacing the hard-coded values with calls to the Magento admin panel system configuration. We will also add a new method for retrieving whether the module should be “active” or not:

<pre><code class="language-php">&lt;&amp;quest;php
class SmashingMagazine_Affiliate_Block_Conversion
    extends Mage_Core_Block_Template
{
    public function getIsActive()
    {
        return Mage::getStoreConfig(
            'smashingmagazine_affiliate/general/status'
        ) &amp;quest; true : false;
    }

    public function getMerchantId()
    {
        return Mage::getStoreConfig(
            'smashingmagazine_affiliate/general/merchant_id'
        );
    }

    public function getAffiliateId()
    {
        return Mage::getModel('core/cookie')-&gt;get(
            SmashingMagazine_Affiliate_Model_Observer::COOKIE_KEY_SOURCE
        );
    }
}</code></pre>

### Enabling Or Disabling Our Module Through The Admin Panel

With this simple modification to our template, <code>conversion.phtml</code>, we can prevent the image from appearing on the checkout success page if the module status is disabled in the Magento admin panel.

<pre><code class="language-php">&lt;&amp;quest;php if ($this-&gt;getIsActive()): &amp;quest;&gt;
&lt;img
    src="/themes/smashingv4/images/logo.png
             &amp;quest;merchant_id=&lt;&amp;quest;php echo $this-&gt;getMerchantId() &amp;quest;&gt;
             &amp;affiliate_id=&lt;&amp;quest;php echo $this-&gt;getAffiliateId() &amp;quest;&gt;"
    width="1"
    height="1"
/&gt;
&lt;&amp;quest;php endif; &amp;quest;&gt;</code></pre>

Similar <code>if</code> statements can be added in <code>Observer.php</code> to prevent the affiliate <code>cookie</code> being checked for and saved.</p>

## Summary

By carefully considering the way we structure our code, and utilizing the Magento admin panel, we can create community modules that are portable enough to simply drop on to any Magento website and they will work out of the box. They can then be customized and fine tuned as required to suit the needs of each website.

Feel free to <a href="https://github.com/josephmcdermott/SmashingMagazine-MagentoAffiliateTracking">view or download the source code</a> (Github), and, as always, I welcome any questions and would love to hear any feedback in the comments area below.

{{< signature "cp" >}}

