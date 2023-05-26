---
title: Introducing The Magento Layout
slug: introducing-magento-layout
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e42d3ad-5a33-4562-96f3-20f9f8f8f66f/psych-5.jpg
date: 2012-11-30T09:59:38.000Z
author: joseph-mcdermott
description: >-
  In this tutorial, we introduce the Magento layout by creating a simple module
  that will add some custom HTML content to the bottom of every customer-facing
  page, in a non-intrusive manner. In other words, we will do so without
  actually modifying any Magento templates or core files.
categories:
  - Coding
  - Frameworks
  - PHP
  - Magento
---
In this tutorial, we introduce the Magento layout by creating a simple module that will add some custom HTML content to the bottom of every customer-facing page, in a non-intrusive manner. In other words, we will do so without actually modifying any Magento templates or core files.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Basics Of Creating A Magento Module](https://www.smashingmagazine.com/2012/03/basics-creating-magento-module/)
*   [How To Create Custom Shipping Methods In Magento](https://www.smashingmagazine.com/2014/01/create-custom-shipping-methods-magento/)
*   [How To Create An Admin-Manageable Magento Entity For Brands](https://www.smashingmagazine.com/2014/03/tutorial-create-admin-manageable-magento-entity-brands/)
*   [<span class="headline">How To Create An Affiliate Tracking Module In Magento</span>](https://www.smashingmagazine.com/2013/02/creating-an-affiliate-tracking-module-in-magento/)

This kind of functionality is a common requirement for many things such as affiliate referral programs, customer tracking analytics, adding custom JavaScript functionality, etc.

We will be covering a number of interesting topics, including:

{{% feature-panel %}}

*   Magento layout handles
*   Layout XML files
*   Blocks and templates
*   An alternative to Widgets

Once you have understood this article, you will have all the information you need to integrate popular third-party tools such as:

*   Google Analytics
*   Reinvigorate
*   CrazyEgg

<figure><a href="/wp-content/uploads/2012/11/Introducing-The-Magento-Layout-no-frame1.png"><img loading="lazy" decoding="async" class="123410" title="Third-Party Tools" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7436c59-af07-4381-947e-b4ce56840e42/introducing-the-magento-layout-no-frame.png" alt="Third-Party Tools Google Analytics, Reinvigorate and CrazyEgg" width="500" height="400" /></a></figure>

## Before We Start

This tutorial assumes that you are already familiar with creating your own Magento module, so if you haven't already done so, I recommend reading our previous article on <a href="/2012/03/01/basics-creating-magento-module/">Creating a Magento Module</a>.

Okay, lets get started. The file structure of our new module should look like this:

<pre><code class="language-markup tmp-xml">app
  - code
      - local
          - SmashingMagazine
              - Layout
                  - etc
                      - config.xml

  - etc
      - modules
          - SmashingMagazine_Layout.xml</code></pre>

We can leave <code>config.xml</code> empty for now, as we will be populating it later on in the tutorial, but we can already complete the content of <code>SmashingMagazine_Layout.xml</code>, with:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Layout&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;codePool&gt;local&lt;/codePool&gt;
        &lt;/SmashingMagazine_Layout&gt;
    &lt;/modules&gt;
&lt;/config&gt;</code></pre>

## Introducing The Magento Layout

The content that is displayed on each Magento page is largely determined by the layout XML files, which can be found in <code>app/design/frontend/base/default/layout</code>. In these XML files, you will see a number of snippets of XML enclosed in layout handle parent nodes, which are used to determine the type of page being displayed. For example, the handle <code>catalog_product_view</code> is used to add content to the product detail page, and <code>checkout_cart_index</code> the basket page.

Child nodes are then created inside these layout handles to determine which content should appear on any particular page. These child nodes are called <code>block</code>s, which may in turn contain child <code>block</code>s of their own. For example, in a layout XML file for the product page (see <code>app/design/frontend/base/default/layout/catalog.xml</code>), under the <code>catalog_product_view</code> layout handle, we might find a <code>block</code> for displaying the product wrapper <code>template</code>. Then as children of that <code>block</code>, we would find a <code>block</code> for the product image <code>template</code>, a <code>block</code> for displaying the price <code>template</code> and another for displaying the <code>add to basket</code> <code>template</code>.

Each of these blocks has a template associated with it. In Model–View–Controller (MVC) terms, the block acts as a mini <em>controller</em> and the template acts as the <em>view</em>. All of the logic for displaying dynamic content is found in the <code>block</code>, which is requested by the <code>template</code> and displayed in HTML form.

The Magento layout is quite a complex, yet very powerful, beast, and as a result we will only cover the parts that are relevant to this tutorial. There is a layout handle named <code>default</code> which is included on every page, and since we want our module's HTML content to appear at the bottom of every page, this is the layout handle we will use.</p>

## Adding A New Layout File

We need to define a new layout file to contain our updates, so first we need to modify our module's <code>config.xml</code> to cater to layout updates:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Layout&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_Layout&gt;
    &lt;/modules&gt;

    &lt;!-- we are making changes to the frontend --&gt;
    &lt;frontend&gt;

        &lt;!-- we are making changes to the layout --&gt;
        &lt;layout&gt;

            &lt;!-- we are adding a new update file --&gt;
            &lt;updates&gt;

                &lt;!--
                    this child node name must be
                    unique throughout Magento
                --&gt;
                &lt;smashingmagazine_layout
                         module="SmashingMagazine_Layout"&gt;

                    &lt;!-- the name of the layout file we are adding --&gt;
                    &lt;file&gt;smashingmagazine_layout.xml&lt;/file&gt;

                &lt;/smashingmagazine_layout&gt;

            &lt;/updates&gt;

        &lt;/layout&gt;

    &lt;/frontend&gt;

&lt;/config&gt;</code></pre>

Now let's create this layout XML file here:

<pre><code class="language-markup tmp-xml">app
  - design
      - frontend
          - base
              - default
                  - layout
                      - smashingmagazine_layout.xml</code></pre>

Now those of you who have a little Magento experience, or have read any more noteworthy Magento tutorials, may be gasping at the fact we are making changes in <code>base/default</code> since this is where Magento core files are located. However, we are not modifying any files here, we are creating new ones, and furthermore we are prefixing our file name with “smashingmagazine,” so there is very little chance of this conflicting with other modules or causing any issues with upgrading Magento in the future.

The content of our new layout file will be as follows:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;!-- all layout files begin with this node --&gt;
&lt;layout&gt;

    &lt;!-- this is the layout handle we are interested in --&gt;
    &lt;default&gt;

        &lt;!-- this is the name of the block we want to add to --&gt;
        &lt;reference name="before_body_end"&gt;

            &lt;!--
                here we define our new block and template
                to be added to 'before_body_end'
            --&gt;
            &lt;block type="core/template"
                   name="smashingmagazine_layout_footer"
                   template="smashingmagazine_layout/footer.phtml" /&gt;

        &lt;/reference&gt;

    &lt;/default&gt;

&lt;/layout&gt;</code></pre>

Here we have referenced an existing <code>block</code>, <code>before_body_end</code>, in order to add our own <code>block</code>, <code>smashingmagazine_layout_footer</code>, as its child. <code>before_body_end</code> is the name of a <code>block</code> that has its content output just before the <code>&lt;/body&gt;</code> tag of the page HTML. You can find the definition of this parent <code>block</code> by looking in <code>app/design/frontend/base/default/layout/page.xml</code>, and the content of this block is output in the <code>.phtml</code> <code>template</code>s within <code>app/design/frontend/base/default/template/page</code>.

By using <code>reference</code>, we are able to add content to existing <code>block</code>s without needing to modify core Magento files. For example, we could achieve the same result as the above snippet by modifying <code>app/design/frontend/base/default/layout/page.xml</code> directly and adding our <code>block</code> code, but this is not good practice:

<pre><code class="language-markup tmp-xml">&lt;default translate="label" module="page"&gt;
    &lt;label&gt;All Pages&lt;/label&gt;
    &lt;block type="page/html" name="root" output="toHtml"
           template="page/3columns.phtml"&gt;

        ...

        &lt;block type="core/text_list" name="before_body_end"
               as="before_body_end" translate="label"&gt;

            &lt;label&gt;Page Bottom&lt;/label&gt;

            &lt;block type="core/template"
                   name="smashingmagazine_layout_footer"
                   template="smashingmagazine_layout/footer.phtml" /&gt;

        &lt;/block&gt;

        ...

    &lt;/block&gt;
&lt;/default&gt;</code></pre>

## Adding A New Template File

We have now defined a new <code>block</code>, <code>smashingmagazine_layout_footer</code>, and assigned the <code>template</code> <code>smashingmagazine_layout/footer.phtml</code> to contain our HTML content. Let's create that <code>template</code> file now:

<pre><code class="language-markup tmp-xml">app
  - design
      - frontend
          - base
              - default
                  - template
                      - smashingmagazine_layout
                          - footer.phtml</code></pre>

The content of <code>footer.phtml</code> can be whatever we like, but for this tutorial we will create a very simple <code>template</code> containing an image, functionality which is often required by affiliate tracking integrations:

<pre><code class="language-markup tmp-html">&lt;img
    src="/themes/smashingv4/images/logo.png?date=YYYY-MM-DD"
    width="459"
    height="120"
/&gt;</code></pre>

Now it's time to take a look at the front end. Upon viewing any customer-facing Magento page, you should see an image displayed at the bottom, and upon viewing the source of the page, you will see it has been included just before the <code>&lt;body/&gt;</code> tag.</p>

## Creating A New Custom Block

Now we want to tie in some simple logic to our template. The source of the image in our template includes a parameter “date” which currently contains a static value of “YYYY-MM-DD.” We want to be able to dynamically populate this parameter with the current date, for which we require some logic from our associated block.

At the moment, our <code>template</code> is associated with the default <code>block</code> type <code>core/template</code>, which only allows us some basic abstract <code>block</code> functionality. Therefore we must create our own custom <code>block</code>.

First let's modify the <code>block</code> type definition in <code>smashingmagazine_layout.xml</code>:

<pre><code class="language-markup tmp-xml">...

&lt;block type="smashingmagazine_layout/footer"
       name="smashingmagazine_layout_footer"
       template="smashingmagazine_layout/footer.phtml" /&gt;

...</code></pre>

Next let's update our module's <code>config.xml</code> to cater to custom <code>block</code>s:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_Layout&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_Layout&gt;
    &lt;/modules&gt;
    &lt;global&gt;

        &lt;!-- we are adding a new block definition --&gt;
        &lt;blocks&gt;

            &lt;!-- a unique short name for our block files --&gt;
            &lt;smashingmagazine_layout&gt;

                &lt;!-- the location of our module's blocks --&gt;
                &lt;class&gt;SmashingMagazine_Layout_Block&lt;/class&gt;

            &lt;/smashingmagazine_layout&gt;

        &lt;/blocks&gt;

    &lt;/global&gt;
    &lt;frontend&gt;
        &lt;layout&gt;
            &lt;updates&gt;
                &lt;smashingmagazine_layout
                         module="SmashingMagazine_Layout"&gt;
                    &lt;file&gt;smashingmagazine_layout.xml&lt;/file&gt;
                &lt;/smashingmagazine_layout&gt;
            &lt;/updates&gt;
        &lt;/layout&gt;
    &lt;/frontend&gt;
&lt;/config&gt;</code></pre>

Now let's create this custom <code>block</code> PHP file:

<pre><code class="language-markup tmp-xml">app
  - code
      - local
          - SmashingMagazine
              - Layout
                  - Block
                      - Footer.php</code></pre>

Finally, let's define our <code>block</code> class and add a simple method for retrieving the current date:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_Layout_Block_Footer
    extends Mage_Core_Block_Template
{
    public function getDate()
    {
        $date = date('Y-m-d');
        return urlencode($date);
    }
}</code></pre>

## Retrieving Dynamic Content From A Block

Inside a Magento <code>template</code>, PHP's <code>$this</code> keyword contains a reference to the associated <code>block</code> object, so we can call the method <code>$this-&gt;getDate()</code> directly from our <code>template</code>:

<pre><code class="language-markup tmp-html">&lt;img
    src="/themes/smashingv4/images/logo.png?date=&lt;?php echo $this-&gt;getDate() ?&gt;"
    width="459"
    height="120"
/&gt;</code></pre>

## Other Handles And Parent Blocks

Try experimenting by changing the layout handle from <code>default</code> to <code>catalog_product_view</code> or <code>cms_index_index</code> to see the HTML content appear only on the product page or the homepage respectively.

You can also try changing the location the content appears in our page's HTML by modifying the parent <code>block</code> from <code>body_before_end</code> to <code>after_body_start</code> or <code>content</code>.</p>

## Summary

This is a very simple example aimed at showing you the basics of how to make use of the Magento layout <strong>without needing to modify existing templates</strong>, which would potentially cause you problems when upgrading your Magento instance.

Using the techniques outlined in this tutorial, you could easily add something like Google Analytics tracking to every page, without needing to modify a single line in Magento's core templates. What's more, if you no longer wanted the custom HTML content on your website, you could simply disable the module and hey presto, it's gone!

The Magento layout is quite complex, and new developers might be tempted to simply “hack” the changes into the appropriate templates for the time being. However, the Magento layout is written in such a way that once we are familiar with it, we can unobtrusively add our custom content while not jeopardizing the ability to install community modules or to upgrade Magento without worrying, “will this work on my hacked-up Magento?”

Feel free to <a href="https://github.com/josephmcdermott/SmashingMagazine-MagentoLayout">view or download the source code</a> (Github).</p>

## Try It Yourself

Now that we are all experts on the Magento layout, here are some very simple examples which follow the very same pattern, but demonstrate how easy it is to integrate third party software with Magento.

Since all of the information you need is detailed in the above article, I will provide some pointers on how you should approach each integration.</p>

### Google Analytics

Magento actually ships with Google Analytics, so it is in fact as simple as entering your tracking code in the admin panel; however, this does not make it any less useful as a try-it-yourself example.

The first step is to <strong>visit the Google website to retrieve the snippet of code</strong> that you need to include on your website. You will notice the only dynamic element of the standard tracking code is the account number (e.g. UA-12345678-90), so for the purpose of this example I would suggest making this number the dynamic content to be retrieved from the <code>block</code>. In a future article, we will cover the topic of making this kind of content <em>admin panel configurable</em>, so abstracting it to the <code>block</code> for now makes good sense should you wish to revisit this example.

Now on to creating your module. I would suggest keeping the same namespace for all of these examples, “SmashingMagazine,” and a fitting module name would be “GoogleAnalytics” in this case. You will need all of the elements of the main article above, so make your way through the article once more, adjusting as required. Since you want your code to appear on every page, you should now know the best layout handle to choose.

If you encounter any problems, check and double check that you have followed the main article exactly, as most beginner issues with Magento are typos and syntax-related mistakes.</p>

### Reinvigorate, CrazyEgg and Everything Else…

You should now see a pattern emerging! You can simply follow exactly the same steps again to integrate other popular third-party software with your Magento website, <strong>all without modifying a single core Magento file</strong> or having to copy and paste content directly into the admin panel, where somebody could accidentally delete it one day.

I welcome any questions and would love to hear any feedback in the comments area below.

{{< signature "cp" >}}

