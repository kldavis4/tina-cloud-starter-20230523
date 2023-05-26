---
title: The Basics Of Creating A Magento Module
slug: basics-creating-magento-module
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f7a1b16-80b4-4d85-b8ad-cf7b8473e84a/megento-illu.png
date: 2012-03-01T08:00:24.000Z
author: joseph-mcdermott
description: >-
  A lot of community extensions (or modules) are available for the feature-rich
  open-source e-commerce solution Magento but what if they don’t quite work as
  you want them to? What if you could understand the structure of a Magento
  module a little better, to the point that you could modify it to suit your
  needs or, better yet, write your own module from scratch?
categories:
  - Coding
  - Frameworks
  - Magento
---
A lot of community extensions (or modules) are available for the feature-rich open-source e-commerce solution <a title="What is Magento?" href="https://ampersandcommerce.com/what-is-magento/">Magento</a>, but what if they don't quite work as you want them to? What if you could understand the structure of a Magento module a little better, to the point that you could modify it to suit your needs or, better yet, write your own module from scratch?

<img loading="lazy" decoding="async" class="118803" style="border: 1px solid #CCC" title="Magento Admin Screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad60c28b-36ea-4639-a793-6950f59c30dd/magento-admin.png" alt="" width="500" height="319" />

In this tutorial, we will introduce the coding of Magento in the form of a “Hello World”-style module. The goal of the module will be simply to write some information to a log file every time a product is saved. This very basic module will allow us to cover a number of interesting topics, including:

*   The `app/code` directories,
*   The structure and creation of a Magento module,
*   Event observers,
*   Logging.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Creating Custom Shipping Methods In Magento](https://www.smashingmagazine.com/2014/01/create-custom-shipping-methods-magento/)
*   [<span class="headline">Introducing The Magento Layout</span>](https://www.smashingmagazine.com/2012/11/introducing-magento-layout/)
*   [15 Common Mistakes in E-Commerce Design](https://www.smashingmagazine.com/2009/10/15-common-mistakes-in-e-commerce-design-and-how-to-avoid-them/)
*   [Fundamental Guidelines Of E-Commerce Checkout Design](https://www.smashingmagazine.com/2011/04/fundamental-guidelines-of-e-commerce-checkout-design/)

{{% feature-panel %}}

## Before We Begin

This tutorial assumes that you already have an installation of Magento up and running, either locally or on a development server, that you can add new files to. The version of Magento that you use doesn't really matter, because we will be covering fundamental aspects that exist across all versions and editions: Community, Professional and Enterprise.</p>

### Disable the Cache

This is one of the first lessons a Magento developer should learn: disable the cache! You can do this by going to <code>Admin Panel &gt; System &gt; Cache Management &gt; Select All &gt; Actions: Disable &gt; Submit</code>.

While very good at boosting performance in a production environment, the cache is a developer's enemy. Leave it enabled at your peril! Every Magento developer I have met has on more than one occasion spent an hour or so wondering why their latest update is not showing up, only to find that Magento is still displaying the version of the website that it conveniently cached earlier that day.</p>

## The app/code Directory

The brains of Magento can be found in individual modules inside the <code>app/code</code> directory, which is split in to three areas: core, community and local.</p>

### Core

The <code>app/code/core</code> directory contains all of the functionality for products, categories, customers, payments, etc. Until you know what you are doing (and even afterwards), keep <code>app/code/core</code> off limits because these files <strong>should not be modified</strong>.

Magento is structured in such a way that you can alter the functionality of any of these core files without modifying them directly, which ensures that your application remains upgrade-proof. By all means, look in order to better understand how Magento works, but do not touch.</p>

### Community

As the name suggests, <code>app/code/community</code> is where you will find modules that have been provided by third parties (i.e. not Magento's core team). Hundreds of modules are available through Magento Connect, and when you install them through the built-in “Package Manager,” this is where they end up.

### Local

Magento ships with an empty <code>app/code/local</code> directory, ready for you to add bespoke modules for your own Magento installation. This is where we will be working for the duration of this tutorial.</p>

## Structuring Our Directory

Open your favorite editor, and navigate to <code>app/code/local</code> to add some new directories and files.</p>

### Module Namespace

The first directory we will create is a “namespace.” This can be called anything you like, but the convention is some form of the name of the company or module's author. Magento uses “Mage” as its namespace. Here at Ampersand Commerce, we use “Ampersand.” For this tutorial, we will use “SmashingMagazine” as our namespace. So, create the directory <code>app/code/local/SmashingMagazine</code>.</p>

### Module Name

For the next directory, we will give our module a descriptive name. The module we are creating will write log entries each time a product is saved, so a logical name would be <code>LogProductUpdate</code>. Create the directory <code>app/code/local/SmashingMagazine/LogProductUpdate</code>.

We should now have the following directory structure for our module. These directory and file names are <strong>case-sensitive</strong>, so capitalize where appropriate.

<pre><code class="language-markup tmp-html">app
  - code
      - local
          - SmashingMagazine
              - LogProductUpdate</code></pre>

## Configuring Our Module

Next, we will begin to configure our module. The configuration files belong inside our module in a directory named <code>etc</code>, so let's create that along with a new XML file: <code>app/code/local/SmashingMagazine/LogProductUpdate/etc/config.xml</code>. This XML file will inform Magento of the location of the files in our module, as well as many other things, such as version number and events to observe. For now, we will create a simple <code>config.xml</code> file, which contains comments that explain the meaning of each section.

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;!-- The root node for Magento module configuration --&gt;
&lt;config&gt;

    &lt;!--
        The module's node contains basic
        information about each Magento module
    --&gt;
    &lt;modules&gt;

        &lt;!--
            This must exactly match the namespace and module's folder
            names, with directory separators replaced by underscores
        --&gt;
        &lt;SmashingMagazine_LogProductUpdate&gt;

            &lt;!-- The version of our module, starting at 0.0.1 --&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;

        &lt;/SmashingMagazine_LogProductUpdate&gt;

    &lt;/modules&gt;

&lt;/config&gt;</code></pre>

## Activating Our Module

The next step is to inform our Magento installation that our module exists, which we do by creating a new XML file in <code>app/etc/modules</code>. The name of this XML file can be anything you like, since Magento will read all XML files in this directory and will be interested only in the content. However, by convention we should give the file and module the same name. Let's create <code>app/etc/modules/SmashingMagazine_LogProductUpdate.xml</code> with the following content:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_LogProductUpdate&gt;

            &lt;!-- Whether our module is active: true or false --&gt;
            &lt;active&gt;true&lt;/active&gt;

            &lt;!-- Which code pool to use: core, community or local --&gt;
            &lt;codePool&gt;local&lt;/codePool&gt;

        &lt;/SmashingMagazine_LogProductUpdate&gt;
    &lt;/modules&gt;
&lt;/config&gt;</code></pre>

## Sanity Check: Is The Module Enabled?

We now have a fully functional module that is enabled in Magento. It doesn't do anything, but it is a valid module. This is our first opportunity to see whether we have correctly configured everything so far. If we log into the Magento admin panel and navigate to <code>System &gt; Configuration &gt; Advanced &gt; Advanced</code> and view the “Disable Modules Output” listing, we should see our <code>SmashingMagazine_LogProductUpdate</code> module listed as enabled. If it is not listed, then something has gone wrong, so carefully run through the steps up to this point again. This is usually when new Magento developers discover the cache!

Our module's structure now looks like this:

<pre><code class="language-markup tmp-html">app
  - code
      - local
          - SmashingMagazine
              - LogProductUpdate
                  - etc
                      - config.xml

  - etc
      - modules
          - SmashingMagazine_LogProductUpdate.xml</code></pre>

## Defining An Event Observer

Event observers are extremely powerful and are one of the cleanest ways to extend Magento's functionality without having to rewrite or override any core methods or classes. We want to <strong>observe the event that Magento dispatches just after a product is saved</strong>, so the code for the event we are interested in is <code>catalog_product_save_after</code>. Determining which event code to use when defining a new observer requires a basic understanding of Magento's model layer, which is beyond the scope of this tutorial. Don't worry, though: we'll cover it another time!

We now need to modify our <code>config.xml</code> to include the event observer definition:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_LogProductUpdate&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_LogProductUpdate&gt;
    &lt;/modules&gt;

    &lt;!-- Configure our module's behavior in the global scope --&gt;
    &lt;global&gt;

        &lt;!-- Defining an event observer --&gt;
        &lt;events&gt;

            &lt;!-- The code of the event we want to observe --&gt;
            &lt;catalog_product_save_after&gt;

                &lt;!-- Defining an observer for this event --&gt;
                &lt;observers&gt;

                    &lt;!--
                        Unique identifier within the
                        catalog_product_save_after node.
                        By convention, we write the module's
                        name in lowercase.
                    --&gt;
                    &lt;smashingmagazine_logproductupdate&gt;

                        &lt;!-- The model to be instantiated --&gt;
                        &lt;class&gt;smashingmagazine_logproductupdate/observer&lt;/class&gt;

                        &lt;!-- The method of the class to be called --&gt;
                        &lt;method&gt;logUpdate&lt;/method&gt;

                        &lt;!-- The type of class to instantiate --&gt;
                        &lt;type&gt;singleton&lt;/type&gt;

                    &lt;/smashingmagazine_logproductupdate&gt;

                &lt;/observers&gt;

            &lt;/catalog_product_save_after&gt;

        &lt;/events&gt;

    &lt;/global&gt;

&lt;/config&gt;</code></pre>

## Configuring Our Model's Directory

In the event observer defined above, we made reference to a model that we have not yet created. We need to inform Magento where to find models in our module by updating <code>config.xml</code> with the following:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_LogProductUpdate&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_LogProductUpdate&gt;
    &lt;/modules&gt;

    &lt;!-- Configure our module's behavior in the global scope --&gt;
    &lt;global&gt;

        &lt;!-- Defining models --&gt;
        &lt;models&gt;

            &lt;!--
                Unique identifier in the model's node.
                By convention, we put the module's name in lowercase.
            --&gt;
            &lt;smashingmagazine_logproductupdate&gt;

                &lt;!--
                    The path to our models directory, with directory
                    separators replaced by underscores
                --&gt;
                &lt;class&gt;SmashingMagazine_LogProductUpdate_Model&lt;/class&gt;

            &lt;/smashingmagazine_logproductupdate&gt;

        &lt;/models&gt;

        &lt;events&gt;
            &lt;catalog_product_save_after&gt;
                &lt;observers&gt;
                    &lt;smashingmagazine_logproductupdate&gt;
                        &lt;class&gt;smashingmagazine_logproductupdate/observer&lt;/class&gt;
                        &lt;method&gt;logUpdate&lt;/method&gt;
                        &lt;type&gt;singleton&lt;/type&gt;
                    &lt;/smashingmagazine_logproductupdate&gt;
                &lt;/observers&gt;
            &lt;/catalog_product_save_after&gt;
        &lt;/events&gt;

    &lt;/global&gt;

&lt;/config&gt;</code></pre>

## Creating An Observer Model

We will now create the model to be instantiated when the event is dispatched. Create a new PHP file in <code>app/code/local/SmashingMagazine/LogProductUpdate/Model/Observer.php</code> with the following content:

<pre><code class="language-php">&lt;?php
/**
 * Our class name should follow the directory structure of
 * our Observer.php model, starting from the namespace,
 * replacing directory separators with underscores.
 * i.e. app/code/local/SmashingMagazine/
 *                     LogProductUpdate/Model/Observer.php
 */
class SmashingMagazine_LogProductUpdate_Model_Observer
{
    /**
     * Magento passes a Varien_Event_Observer object as
     * the first parameter of dispatched events.
     */
    public function logUpdate(Varien_Event_Observer $observer)
    {
        // Retrieve the product being updated from the event observer
        $product = $observer-&gt;getEvent()-&gt;getProduct();

        // Write a new line to var/log/product-updates.log
        $name = $product-&gt;getName();
        $sku = $product-&gt;getSku();
        Mage::log(
            "{$name} ({$sku}) updated",
            null,
            'product-updates.log'
        );
    }
}</code></pre>

## We're done! Try it out.

The directory structure for our completed module should now look like this:

<pre><code class="language-markup tmp-html">app
  - code
      - local
          - SmashingMagazine
              - LogProductUpdate
                  - Model
                      - Observer.php

                  - etc
                      - config.xml

  - etc
      - modules
          - SmashingMagazine_LogProductUpdate.xml</code></pre>

Now that our module is complete, it's time to try it out! Log into the Magento admin panel, create or update a product in your catalog, and then check the <code>var/log</code> folder to see your <code>product-updates.log</code> file populated.

If nothing appears or the directory does not exist, ensure that the correct permissions are set to allow Magento to write to this directory, and that logging is enabled in <code>Admin Panel &gt; System &gt; Configuration &gt; Developer &gt; Log Settings &gt; Enabled</code>.

This basic tutorial is meant to give you an overall understanding of how Magento modules work. After completing this tutorial, spend some time exploring the Magento modules in <code>app/code/core</code> and see if you now have a better idea of how it all works.

Feel free to <a href="https://github.com/josephmcdermott/SmashingMagazine-MagentoFirstModule">view or download the source code</a> (Github).

We welcome any questions and would love to hear any feedback in the comments area below.

