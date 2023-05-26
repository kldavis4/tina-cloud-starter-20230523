---
title: 'A CSS Grid Framework For Shopify Collection Pages'
slug: css-grid-framework-shopify-collection-pages
author: liam-griffin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ecb8c45-9aa3-4db6-b234-233ff6a1f5ff/css-grid-framework-webpage.jpg
date: 2020-09-22T10:00:00.000Z
summary: >-
  In this article, we’ll be looking at how to set up a grid layout for products on your collection pages, and how to use Shopify’s section settings to create customizable options in the online store editor.
description: >-
  In this article, we’ll be looking at how to set up a grid layout for products on your collection pages, and how to use Shopify’s section settings to create customizable options in the online store editor.
categories:
  - CSS
  - E-commerce
disable_ads: true
disable_panels: true
disable_newsletterbox: true
canonical: 'https://www.shopify.com/partners/blog/css-grid-framework'
sponsor:
  title: Shopify
  link: https://www.shopify.com/shopifypartnersvap?utm_source=SMplacement&utm_medium=cpm&utm_campaign=become+a+partner+smashingmagazine&utm_term=shopifypartnersvap
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b1dad44-d5ca-480b-b770-c5b3223b0778/shopify-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.shopify.com/shopifypartnersvap?utm_source=SMplacement&utm_medium=cpm&utm_campaign=become+a+partner+smashingmagazine&utm_term=shopifypartnersvap" style="text-shadow: none !important">Shopify</a>, an all-in-one commerce platform to help you start, run, and grow your business. <em>Thank you!</em>
---

<p>CSS Grid has become an increasingly popular technique for applying a layout to pages amongst other CSS frameworks. Developers can take advantage of this system to reduce complexity and define clear style rules. As explained in my Shopify blog post on <a href="https://www.shopify.com/partners/blog/css-grid">getting started with a CSS grid</a> layout, a CSS Grid framework can be easily implemented on Shopify themes to design responsive page layouts based on rows and columns.</p>

<p>All pages of a Shopify online store can adopt CSS Grid, but one obvious touchpoint of any e-commerce site that can benefit from a robust and clean grid layout is the collection page. On collection pages, it feels natural that products are organized in a grid format, with rows and columns. So, if an option for creating a robust grid arrangement with a simple set of rules is possible, it’s worth exploring for your custom theme projects.</p>

<p><strong>Note</strong>: <em>To get an idea of how this could look for your clients and so you can follow along with this CSS Grid tutorial, <a href="https://testing-css-grid.myshopify.com/collections/all" rel="nofollow noopener noreferrer">I’ve set up a test store</a> which you can use to see the approach I’ve outlined in this tutorial.</em></p>

## Creating A Basic Collection Page Layout 

<p>Working with CSS Grid on a Shopify collection page will operate in very much the same way as how Grid works on a custom section—something we explored in the <a href="https://www.shopify.com/partners/blog/css-grid">CSS grid</a> blog article. Thankfully, Shopify has excellent CSS grid support. The biggest difference when implementing a grid system on a collection page is that you won’t need to assign a class to each individual item. Note that if you aren’t extremely advanced with CSS, we recommend you read over our <a href="https://www.shopify.com/partners/blog/intro-to-css">intro to CSS</a> guide before going further.</p>

<p>Now, since products are automatically outputted in a loop as repeatable content items, it’s possible to apply the same class to all products that are associated with a collection. But first, let’s look at an example of a collection page with no styling. </p>

<p>If you start off with a basic collection page setup, you’d likely have markup that looks like the following:</p>

<div class="break-out">

 <pre><code class="language-markup">&lt;h1&gt;{{ collection.title }}&lt;/h1&gt;
  {% for product in collection.products %}
    &lt;a href="{{ product.url | within: collection }}"&gt;
      &lt;img src="{{ product.featured_image.src | img_url: '300x' }}" alt="{{ product.featured_image.alt | escape }}"&gt;
    &lt;/a&gt;
    &lt;a href="{{ product.url | within: collection }}"&gt;{{ product.title }}&lt;/a&gt;
      &lt;p&gt;{{ product.price | money }}&lt;/p&gt;
  {% unless product.available %}&lt;br&gt;&lt;strong&gt;sold out&lt;/strong&gt;{% endunless %}
  {% endfor %}
</code></pre>
</div>

<p>This will output the collection name as a header, and display the collection’s associated products with their image, name, and price. Without any styling, these products will appear in a vertical row by default. The size of the product images will be 300 pixels, as defined by the <a href="https://shopify.dev/docs/liquid/reference/filters/url-filters#img_url" target="_blank" rel="nofollow noopener noreferrer"><code>img_url</code> filter. </a></p>

<p>To apply a <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout">CSS Grid framework</a> to this group of products, you’ll first want to wrap the collection <code>for loop</code> in one main grid container, which is considered the parent container. Next, you can wrap the code for each individual product (the children) within its own individual container. </p>

<p>Once these containers are added, the markup would appear as:</p>

<div class="break-out">

 <pre><code class="language-markup">&lt;h1&gt;{{ collection.title }}&lt;/h1&gt;
  &lt;div class="grid-collection"&gt;
    {% for product in collection.products %}
      &lt;div class="grid-product"&gt;
        &lt;a href="{{ product.url }}"&gt;
          &lt;img src="{{ product.featured_image.src | img_url: '300x' }}" alt="{{ product.featured_image.alt | escape }}"&gt;
        &lt;/a&gt;
        &lt;a href="{{ product.url }}"&gt;{{ product.title }}&lt;/a&gt;
          &lt;p&gt;{{ product.price | money }}&lt;/p&gt;
          {% unless product.available %}&lt;br&gt;&lt;strong&gt;sold out&lt;/strong&gt;{% endunless %}
      &lt;/div&gt;
    {% endfor %}
  &lt;/div&gt;
</code></pre>
</div>

## Applying The CSS Grid Framework Styling To The Collection Page 

<p>Now that we have a basic collection page with a hierarchy of containers, you can divide the products into a <a href="https://www.shopify.com/partners/blog/grid-layout">grid layout</a> by applying styles to the classes you’ve created. In the themes stylesheet file, you can add the following:</p>

<div class="break-out">

 <pre><code class="language-css">.grid-collection {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

.grid-product {
  display: grid;
}
</code></pre>
</div>

<p>Now, when you navigate to the collection page, you should see the products appearing in a grid, fitting into the available space on the screen. </p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ecb8c45-9aa3-4db6-b234-233ff6a1f5ff/css-grid-framework-webpage.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ecb8c45-9aa3-4db6-b234-233ff6a1f5ff/css-grid-framework-webpage.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ecb8c45-9aa3-4db6-b234-233ff6a1f5ff/css-grid-framework-webpage.jpg'>Large preview</a>)" alt="A preview of the collection page" >}}

<p>As well as adding <code>display: grid</code>, you’ll notice we’re also using the <code>grid-template-columns</code> property, which can be used to define how many columns appear within the grid. Instead of defining a fixed value, we can use the repeat notation to create a rule that our products should appear as many times as they can fit inside the Grid.</p>

<p>Within the functional notation, <code>auto-fit</code> is displaying as many items on the line as possible, so on a full screen, we will see as many products appearing as there is space on the buyers screen. Finally, with <code>minmax</code>, we set up a rule that each cell should be a minimum of 300 pixels, and a maximum of one fraction of the grid-container.</p>

<p>When using this property, we need to ensure that the size defined in the <code>minmax</code> function matches, or is larger than, the size defined by the <code>img_url</code> Liquid filter in our markup. If the <code>minmax</code> function contains a smaller pixel size, you’ll see that product images become cut off as they won’t have enough space within the defined cell. </p>

<p>Once our basic grid is appearing as expected, we can add additional CSS to tidy up the layout by adding margin space and positioning the products on the center of the page. If you’d like the gap between your columns and rows to be the same, you can define both with the <code>gap</code> property, rather than defining each separately.</p>

<p>Once this is all set up, your stylesheet will look like this: </p>

<pre><code class="language-css">.grid-collection {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1px;
  margin: 1em;
  background-color: white;
}

.grid-product {
  display: grid;
  justify-content: center;
  padding: 10px;
  color: white;
  line-height: 1;
  border-radius: 5px;
}
</code></pre>

<p>While this is a simple example of how a CSS Grid framework can be applied to a collection page, I’d recommend that you experiment with different parameters to suit your client’s images and existing brand imagery. You can also use this approach to create grids on other pages, like the cart and adjust based on its unique characteristics.</p>

## Adding Customizable Grid Options

<p>The above approach works well for a grid that will display columns of products based on the size of the screen. But, what if you want to give the merchant some control over how the grid is represented?</p>

<p>In some cases your clients may want to customize the product page, and dictate how many products appear.</p>

<p>If your markup is contained in a section file, you can create section settings that will allow clients to customize the grid from the online store editor. A configuration of settings that allows your client to select a number of products on a row could look like this:</p>

<pre><code class="language-javascript">{% schema %}

{
    "name": "Collection",
    "settings": [
  {
    "type": "select",
    "id":  "product_number",
    "label": "Number of products per row",
    "options": [
		{
		"value": "two",
		"label": "two"
		},
		{
		"value": "three",
		"label": "three"
		},
		{
		"value": "four",
		"label": "four"
		}
      ]
    }
  ]
}

{% endschema %}
</code></pre>

<p>You can see here that the setting has a type of <code>select</code> which will output a drop down option on the online store editor. There is also a <code>label</code> property to describe the setting. </p>

<p>The <code>id</code> property will not be visible on the editor, but we can reference this to create a variable. A common use-case for variables created with section objects is to reference them within the markup to change class names based on what settings are selected. </p>

<p>To achieve this effect, we can use Liquid to output the <code>value</code> that is selected on the online store editor, as an attribute of <a href="https://shopify.dev/docs/liquid/reference/objects/section#section-settings" rel="nofollow noopener noreferrer">the section object</a>. This object will be expressed as <code>{{ section.settings.product_number }}</code>, and will output whichever value is the selected option.</p>

<p>One way of looking at it is that the <code>id</code> we assigned in the section setting becomes a "placeholder" for the value in the selected option. </p>

<p>Then, we can take this object and append it to the class name of the collection. This will allow the class name to change based on the selected option, and you can create different CSS rules for each class name. </p>

<p>When we append the variable to the existing collection class name it will look like:</p>

<div class="break-out">

 <pre><code class="html">&lt;div class="grid-collection-{{ section.settings.product_number }}"&gt;
</code></pre>
</div>

<p>Here you can see that the section object references the <code>id</code> of the section setting. The value that is outputted by this section object is determined by the value selected on the online store editor. For example, if "three" is selected on our drop down box, this would cause the markup to output as:</p>

<pre><code class="html">&lt;div class="grid-collection-three"&gt;
</code></pre>

<p>Now we can move back to our stylesheet and set up different CSS rules for <code>grid-collection-two</code>, <code>grid-collection-three</code>, and <code>grid-collection-four</code>. These would look like:</p>

<pre><code class="language-css">.grid-collection-two {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1px;
  margin: 1em;
  background-color: white;
}

.grid-collection-three {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  margin: 1em;
  background-color: white;
}

.grid-collection-four {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  margin: 1em;
  background-color: white;
}
</code></pre>

<p>The <code>grid-template-columns</code> property determines how many columns will appear within the grid, and as a result, how many products will appear in a row on the collection page. So, each class will have a different value for the <code>grid-template-columns</code> property, that corresponds with its unique class name.</p>

<p>Now when a client navigates to the online store editor and selects an option for "Number of products per row", the grid will adjust to reflect this:</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e6d690c-991e-4a60-a2c8-42d75ccef15d/css-grid-framework.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e6d690c-991e-4a60-a2c8-42d75ccef15d/css-grid-framework.gif" alt="Preview of the online store editor" /></a></figure>

<p>Finally, we can add media queries so that there are different CSS Grid rules for smaller screens. This will avoid the grid appearing with too many columns of products on smaller devices, which would result in products appearing off-screen. </p>

<p>Each variation of the <code>collection-grid</code> class can be assigned different rules where the grid will drop to two or one columns. When this is set up on your stylesheet, it could look like this:</p>

<pre><code class="language-css">@media screen and (max-width: 992px) {
  .grid-collection-two {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 600px) {
  .grid-collection-two {
    grid-template-columns: repeat(1, 1fr);
  }
}

@media screen and (max-width: 992px) {
  .grid-collection-three {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 600px) {
  .grid-collection-three {
    grid-template-columns: repeat(1, 1fr);
  }
}

@media screen and (max-width: 992px) {
  .grid-collection-four {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 600px) {
  .grid-collection-four {
    grid-template-columns: repeat(1, 1fr);
  }
}
</code></pre>

<p>It’s likely that you’ll need to adjust the pixel sizes and values for the <code>img_url</code> filter based on the specific requirements of your client and the images they’re using. However, this method will show you how to get started using a CSS Grid system for collection pages on your own custom theme builds. </p>

## Expanding The Grid

<p>Once you’ve applied a CSS Grid to your collection pages, you can start to consider other areas on your Shopify themes where robust <a href="https://www.shopify.com/partners/blog/website-layouts">website layouts</a> may apply. As an example, it’s possible to create image gallery sections in a grid, and add irregular shaped cells for variety. </p>

<p>There are a range of opportunities when using CSS Grid on Shopify, and each one potentially adds further value to your theme projects. With the help of this article, you can expand the CSS Grid framework to all of your theme projects.</p>

{{< signature "ra, il" >}}
