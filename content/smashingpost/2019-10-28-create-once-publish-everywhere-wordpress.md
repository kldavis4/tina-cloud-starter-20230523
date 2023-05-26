---
title: '“Create Once, Publish Everywhere” With WordPress'
slug: create-once-publish-everywhere-wordpress
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/829ad691-38ee-4683-ae16-0f5fbf8e45b0/create-once-publish-everywhere-wordpress.png
date: 2019-10-28T16:00:59+02:00
summary: >-
  The term COPE (“Create Once, Publish Everywhere”) is a methodology for publishing our content to different outputs (website, AMP site, email, apps, and so on) by having a single source of truth for all of them. Let’s explore how to implement COPE using WordPress.
description: >-
  The term COPE (“Create Once, Publish Everywhere”) is a methodology for publishing our content to different outputs (website, AMP site, email, apps, and so on) by having a single source of truth for all of them. Let’s explore how to implement COPE using WordPress.
categories:
  - WordPress
---
COPE is a strategy for reducing the amount of work needed to publish our content into different mediums, such as website, email, apps, and others. [First pioneered by NPR](https://www.programmableweb.com/news/cope-create-once-publish-everywhere/2009/10/13), it accomplishes its goal by establishing a single source of truth for content which can be used for all of the different mediums.

Having content that works everywhere is not a trivial task since each medium will have its own requirements. For instance, whereas HTML is valid for printing content for the web, this language is not valid for an iOS/Android app. Similarly, we can add classes to our HTML for the web, but these must be converted to styles for email. 

The solution to this conundrum is to separate form from content: The presentation and the meaning of the content must be decoupled, and only the meaning is used as the single source of truth. The presentation can then be added in another layer (specific to the selected medium).

For example, given the following piece of HTML code, the `<p>` is an HTML tag which applies mostly for the web, and attribute `class="align-center"` is presentation (placing an element "on the center" makes sense for a screen-based medium, but not for an audio-based one such as Amazon Alexa):

<pre><code class="language-html">&lt;p class="align-center"&gt;Hello world!&lt;/p&gt;
</code></pre>

Hence, this piece of content cannot be used as a single source of truth, and it must be converted into a format which separates the meaning from the presentation, such as the following piece of JSON code:

<pre><code class="language-json">{
  content: "Hello world!",
  placement: "center",
  type: "paragraph"
}
</code></pre>

This piece of code can be used as a single source of truth for content since from it we can recreate once again the HTML code to use for the web, and procure an appropriate format for other mediums.

{{% feature-panel %}}

## Why WordPress

WordPress is ideal to implement the COPE strategy due of several reasons:

<ul>
  <li><strong>It is versatile.</strong><br />The WordPress database model does not define a fixed, rigid content model; on the contrary, it was created for versatility, enabling to create varied content models through the use of meta field, which allow the storing of additional pieces of data for four different entities: posts and custom post types, users, comments, and taxonomies (tags and categories).</li>
  <li><strong>It is powerful.</strong><br />WordPress shines as a CMS (Content Management System), and its plugin ecosystem enables to easily add new functionalities.</li>
  <li><strong>It is widespread.</strong><br />It is estimated that 1/3rd of websites run on WordPress. Then, a sizable amount of people working on the web know about and are able to use, i.e. WordPress. Not just developers but also bloggers, salesmen, marketing staff, and so on. Then, many different stakeholders, no matter their technical background, will be able to produce the content which acts as the single source of truth.</li>
  <li><strong>It is headless.</strong><br />Headlessness is the ability to decouple the content from the presentation layer, and it is a fundamental feature for implementing COPE (as to be able to feed data to dissimilar mediums).<br /><br />Since incorporating the <a href="https://developer.wordpress.org/rest-api/">WP REST API</a> into core starting from version 4.7, and more markedly since the launch of Gutenberg in version 5.0 (for which plenty of REST API endpoints had to be implemented), WordPress can be considered a headless CMS, since most WordPress content can be accessed through a REST API by any application built on any stack.<br /><br />In addition, the recently-created <a href="https://www.wpgraphql.com/">WPGraphQL</a> integrates WordPress and GraphQL, enabling to feed content from WordPress into any application using this increasingly popular API. Finally, my own project <a href="https://github.com/leoloso/PoP">PoP</a> has recently added an <a href="https://github.com/leoloso/pop-api-wp">implementation of an API for WordPress</a> which allows to export the WordPress data as either REST, GraphQL or PoP native formats.</li>
  <li>It has <strong>Gutenberg</strong>, a block-based editor that greatly aids the implementation of COPE because it is based on the concept of blocks (as explained in the sections below).</li>
</ul>

## Blobs Versus Blocks To Represent Information

A blob is a single unit of information stored all together in the database. For instance, writing the blog post below on a CMS that relies on blobs to store information will store the blog post content on a single database entry &mdash; containing that same content:

<div class="break-out">

 <pre><code class="language-html">&lt;p&gt;Look at this wonderful tango:&lt;/p&gt;
&lt;figure&gt;
  &lt;iframe width="951" height="535" src="https://www.youtube.com/embed/sxm3Xyutc1s" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen&gt;&lt;/iframe&gt;
  &lt;figcaption&gt;An exquisite tango performance&lt;/figcaption&gt;
&lt;/figure&gt;
</code></pre>
</div>

As it can be appreciated, the important bits of information from this blog post (such as the content in the paragraph, and the URL, the dimensions and attributes of the Youtube video) are not easily accessible: If we want to retrieve any of them on their own, we need to parse the HTML code to extract them &mdash; which is far from an ideal solution. 

Blocks act differently. By representing the information as a list of blocks, we can store the content in a more semantic and accessible way. Each block conveys its own content and its own properties which can depend on its type (e.g. is it perhaps a paragraph or a video?).

For example, the HTML code above could be represented as a list of blocks like this:

<div class="break-out">

 <pre><code class="language-json">{
  [
    type: "paragraph",
    content: "Look at this wonderful tango:"
  ],
  [
    type: "embed",
    provider: "Youtube",
    url: "https://www.youtube.com/embed/sxm3Xyutc1s",
    width: 951,
    height: 535,
    frameborder: 0,
    allowfullscreen: true,
    allow: "accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture",
    caption: "An exquisite tango performance"
  ]  
}
</code></pre>
</div>

Through this way of representing information, we can easily use any piece of data on its own, and adapt it for the specific medium where it must be displayed. For instance, if we want to extract all the videos from the blog post to show on a car entertainment system, we can simply iterate all blocks of information, select those with `type="embed"` and `provider="Youtube"`, and extract the URL from them. Similarly, if we want to show the video on an Apple Watch, we need not care about the dimensions of the video, so we can ignore attributes `width` and `height` in a straightforward manner.

{{% ad-panel-leaderboard %}}

## How Gutenberg Implements Blocks

Before WordPress version 5.0, WordPress used blobs to store post content in the database. Starting from version 5.0, WordPress ships with Gutenberg, a block-based editor, enabling the enhanced way to process content mentioned above, which represents a breakthrough towards the implementation of COPE. Unfortunately, Gutenberg has not been designed for this specific use case, and its representation of the information is different to the one just described for blocks, resulting in several inconveniences that we will need to deal with. 

Let’s first have a glimpse on how the blog post described above is saved through Gutenberg:

<div class="break-out">

 <pre><code class="language-html">&lt;!-- wp:paragraph --&gt; 
&lt;p&gt;Look at this wonderful tango:&lt;/p&gt; 
&lt;!-- /wp:paragraph --&gt;  

&lt;!-- wp:core-embed/youtube {"url":"https://www.youtube.com/embed/sxm3Xyutc1s","type":"rich","providerNameSlug":"embed-handler","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} --&gt; 
&lt;figure class="wp-block-embed-youtube wp-block-embed is-type-rich is-provider-embed-handler wp-embed-aspect-16-9 wp-has-aspect-ratio"&gt;
  &lt;div class="wp-block-embed__wrapper"&gt; https://www.youtube.com/embed/sxm3Xyutc1s &lt;/div&gt;
  &lt;figcaption&gt;An exquisite tango performance&lt;/figcaption&gt;
&lt;/figure&gt; 
&lt;!-- /wp:core-embed/youtube --&gt;
</code></pre>
</div>

From this piece of code, we can make the following observations:

### Blocks Are Saved All Together In The Same Database Entry

There are two blocks in the code above:

<pre><code class="language-html">&lt;!-- wp:paragraph --&gt;
&lt;p&gt;Look at this wonderful tango:&lt;/p&gt;
&lt;!-- /wp:paragraph --&gt;
</code></pre>

<div class="break-out">

 <pre><code class="language-html">&lt;!-- wp:core-embed/youtube {"url":"https://www.youtube.com/embed/sxm3Xyutc1s","type":"rich","providerNameSlug":"embed-handler","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} --&gt; 
&lt;figure class="wp-block-embed-youtube wp-block-embed is-type-rich is-provider-embed-handler wp-embed-aspect-16-9 wp-has-aspect-ratio"&gt;
  &lt;div class="wp-block-embed__wrapper"&gt; https://www.youtube.com/embed/sxm3Xyutc1s &lt;/div&gt;
  &lt;figcaption&gt;An exquisite tango performance&lt;/figcaption&gt;
&lt;/figure&gt; 
&lt;!-- /wp:core-embed/youtube --&gt;
</code></pre>
</div>

With the exception of global (also called "reusable") blocks, which have an entry of their own in the database and can be referenced directly through their IDs, all blocks are saved together in the blog post’s entry in table `wp_posts`.

Hence, to retrieve the information for a specific block, we will first need to parse the content and isolate all blocks from each other. Conveniently, WordPress provides function `parse_blocks($content)` to do just this. This function receives a string containing the blog post content (in HTML format), and returns a JSON object containing the data for all contained blocks.

### Block Type And Attributes Are Conveyed Through HTML Comments

Each block is delimited with a starting tag `<!-- wp:{block-type} {block-attributes-encoded-as-JSON} -->` and an ending tag `<!-- /wp:{block-type} -->` which (being HTML comments) ensure that this information will not be visible when displaying it on a website. However, we can’t display the blog post directly on another medium, since the HTML comment may be visible, appearing as garbled content. This is not a big deal though, since after parsing the content through function `parse_blocks($content)`, the HTML comments are removed and we can operate directly with the block data as a JSON object.

### Blocks Contain HTML

The paragraph block has `"<p>Look at this wonderful tango:</p>"` as its content, instead of `"Look at this wonderful tango:"`. Hence, it contains HTML code (tags `<p>` and `</p>`) which is not useful for other mediums, and as such must be removed, for instance through PHP function `strip_tags($content)`. 

When stripping tags, we can keep those HTML tags which explicitly convey semantic information, such as tags `<strong>` and `<em>` (instead of their counterparts `<b>` and `<i>` which apply only to a screen-based medium), and remove all other tags. This is because there is a great chance that semantic tags can be properly interpreted for other mediums too (e.g. Amazon Alexa can recognize tags `<strong>` and `<em>`, and change its voice and intonation accordingly when reading a piece of text). To do this, we invoke the `strip_tags` function with a 2nd parameter containing the allowed tags, and place it within a wrapping function for convenience:

<pre><code class="language-php">function strip_html_tags($content) 
{
  return strip_tags($content, '&lt;strong&gt;&lt;em&gt;');
}
</code></pre>

### The Video’s Caption Is Saved Within The HTML And Not As An Attribute

As can be seen in the Youtube video block, the caption `"An exquisite tango performance"` is stored inside the HTML code (enclosed by tag `<figcaption />`) but not inside the JSON-encoded attributes object. As a consequence, to extract the caption, we will need to parse the block content, for instance through a regular expression: 

<div class="break-out">

 <pre><code class="language-php">function extract_caption($content) 
{
  $matches = [];
  preg_match('/&lt;figcaption>(.*?)&lt;\/figcaption>/', $content, $matches);
  if ($caption = $matches[1]) {
    return strip_html_tags($caption);
  }
  return null;
}
</code></pre>
</div>

This is a hurdle we must overcome in order to extract all metadata from a Gutenberg block. This happens on several blocks; since not all pieces of metadata are saved as attributes, we must then first identify which are these pieces of metadata, and then parse the HTML content to extract them on a block-by-block and piece-by-piece basis. 

Concerning COPE, this represents a wasted chance to have a really optimal solution. It could be argued that the alternative option is not ideal either, since it would duplicate information, storing it both within the HTML and as an attribute, which violates the DRY (**D**on’t **R**epeat **Y**ourself) principle. However, this violation does already take place: For instance, attribute `className` contains value `"wp-embed-aspect-16-9 wp-has-aspect-ratio"`, which is printed inside the content too, under HTML attribute `class`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce35f2a3-a9de-461c-b005-96623d2ca9a6/adding-content-through-gutenberg-post.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce35f2a3-a9de-461c-b005-96623d2ca9a6/adding-content-through-gutenberg-post.jpg" sizes="100vw" caption="Adding content through Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce35f2a3-a9de-461c-b005-96623d2ca9a6/adding-content-through-gutenberg-post.jpg'>Large preview</a>)" alt="Adding content through Gutenberg" >}}

## Implementing COPE

**Note:** *I have released this functionality, including all the code described below, as WordPress plugin [Block Metadata](https://wordpress.org/plugins/block-metadata/). You’re welcome to install it and play with it so you can get a taste of the power of COPE. The source code is available in this [GitHub repo](https://github.com/leoloso/block-metadata).*

Now that we know what the inner representation of a block looks like, let’s proceed to implement COPE through Gutenberg. The procedure will involve the following steps:

1. Because function `parse_blocks($content)` returns a JSON object with nested levels, we must first simplify this structure.
2. We iterate all blocks and, for each, identify their pieces of metadata and extract them, transforming them into a medium-agnostic format in the process. Which attributes are added to the response can vary depending on the block type.
3. We finally make the data available through an API (REST/GraphQL/PoP).

Let’s implement these steps one by one.

{{% ad-panel-leaderboard %}}

## 1. Simplifying The Structure Of The JSON Object

The returned JSON object from function `parse_blocks($content)` has a nested architecture, in which the data for normal blocks appear at the first level, but the data for a referenced reusable block are missing (only data for the referencing block are added), and the data for nested blocks (which are added within other blocks) and for grouped blocks (where several blocks can be grouped together) appear under 1 or more sublevels. This architecture makes it difficult to process the block data from all blocks in the post content, since on one side some data are missing, and on the other we don’t know a priori under how many levels data are located. In addition, there is a block divider placed every pair of blocks, containing no content, which can be safely ignored.

For instance, the response obtained from a post containing a simple block, a global block, a nested block containing a simple block, and a group of simple blocks, in that order, is the following:

<div class="break-out">

 <pre><code class="language-json">[
  // Simple block
  {
    "blockName": "core/image",
    "attrs": {
      "id": 70,
      "sizeSlug": "large"
    },
    "innerBlocks": [],
    "innerHTML": "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/sandwich-1024x614.jpg\" alt=\"\" class=\"wp-image-70\"/&gt;&lt;figcaption&gt;This is a normal block&lt;/figcaption&gt;&lt;/figure&gt;\n",
    "innerContent": [
      "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/sandwich-1024x614.jpg\" alt=\"\" class=\"wp-image-70\"/&gt;&lt;figcaption&gt;This is a normal block&lt;/figcaption&gt;&lt;/figure&gt;\n"
    ]
  },
  // Empty block divider
  {
    "blockName": null,
    "attrs": [],
    "innerBlocks": [],
    "innerHTML": "\n\n",
    "innerContent": [
      "\n\n"
    ]
  },
  // Reference to reusable block
  {
    "blockName": "core/block",
    "attrs": {
      "ref": 218
    },
    "innerBlocks": [],
    "innerHTML": "",
    "innerContent": []
  },
  // Empty block divider
  {
    "blockName": null,
    "attrs": [],
    "innerBlocks": [],
    "innerHTML": "\n\n",
    "innerContent": [
      "\n\n"
    ]
  },
  // Nested block
  {
    "blockName": "core/columns",
    "attrs": [],
    // Contained nested blocks
    "innerBlocks": [
      {
        "blockName": "core/column",
        "attrs": [],
        // Contained nested blocks
        "innerBlocks": [
          {
            "blockName": "core/image",
            "attrs": {
              "id": 69,
              "sizeSlug": "large"
            },
            "innerBlocks": [],
            "innerHTML": "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/espresso-1024x614.jpg\" alt=\"\" class=\"wp-image-69\"/&gt;&lt;/figure&gt;\n",
            "innerContent": [
              "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/espresso-1024x614.jpg\" alt=\"\" class=\"wp-image-69\"/&gt;&lt;/figure&gt;\n"
            ]
          }
        ],
        "innerHTML": "\n&lt;div class=\"wp-block-column\"&gt;&lt;/div&gt;\n",
        "innerContent": [
          "\n&lt;div class=\"wp-block-column\"&gt;",
          null,
          "&lt;/div&gt;\n"
        ]
      },
      {
        "blockName": "core/column",
        "attrs": [],
        // Contained nested blocks
        "innerBlocks": [
          {
            "blockName": "core/paragraph",
            "attrs": [],
            "innerBlocks": [],
            "innerHTML": "\n&lt;p&gt;This is how I wake up every morning&lt;/p&gt;\n",
            "innerContent": [
              "\n&lt;p&gt;This is how I wake up every morning&lt;/p&gt;\n"
            ]
          }
        ],
        "innerHTML": "\n&lt;div class=\"wp-block-column\"&gt;&lt;/div&gt;\n",
        "innerContent": [
          "\n&lt;div class=\"wp-block-column\"&gt;",
          null,
          "&lt;/div&gt;\n"
        ]
      }
    ],
    "innerHTML": "\n&lt;div class=\"wp-block-columns\"&gt;\n\n&lt;/div&gt;\n",
    "innerContent": [
      "\n&lt;div class=\"wp-block-columns\"&gt;",
      null,
      "\n\n",
      null,
      "&lt;/div&gt;\n"
    ]
  },
  // Empty block divider
  {
    "blockName": null,
    "attrs": [],
    "innerBlocks": [],
    "innerHTML": "\n\n",
    "innerContent": [
      "\n\n"
    ]
  },
  // Block group
  {
    "blockName": "core/group",
    "attrs": [],
    // Contained grouped blocks
    "innerBlocks": [
      {
        "blockName": "core/image",
        "attrs": {
          "id": 71,
          "sizeSlug": "large"
        },
        "innerBlocks": [],
        "innerHTML": "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/coffee-1024x614.jpg\" alt=\"\" class=\"wp-image-71\"/&gt;&lt;figcaption&gt;First element of the group&lt;/figcaption&gt;&lt;/figure&gt;\n",
        "innerContent": [
          "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/coffee-1024x614.jpg\" alt=\"\" class=\"wp-image-71\"/&gt;&lt;figcaption&gt;First element of the group&lt;/figcaption&gt;&lt;/figure&gt;\n"
        ]
      },
      {
        "blockName": "core/paragraph",
        "attrs": [],
        "innerBlocks": [],
        "innerHTML": "\n&lt;p&gt;Second element of the group&lt;/p&gt;\n",
        "innerContent": [
          "\n&lt;p&gt;Second element of the group&lt;/p&gt;\n"
        ]
      }
    ],
    "innerHTML": "\n&lt;div class=\"wp-block-group\"&gt;&lt;div class=\"wp-block-group__inner-container\"&gt;\n\n&lt;/div&gt;&lt;/div&gt;\n",
    "innerContent": [
      "\n&lt;div class=\"wp-block-group\"&gt;&lt;div class=\"wp-block-group__inner-container\"&gt;",
      null,
      "\n\n",
      null,
      "&lt;/div&gt;&lt;/div&gt;\n"
    ]
  }
]
</code></pre>
</div>

A better solution is to have all data at the first level, so the logic to iterate through all block data is greatly simplified. Hence, we must fetch the data for these reusable/nested/grouped blocks, and have it added on the first level too. As it can be seen in the JSON code above:

- The empty divider block has attribute `"blockName"` with value `NULL`
- The reference to a reusable block is defined through `$block["attrs"]["ref"]`
- Nested and group blocks define their contained blocks under `$block["innerBlocks"]`

Hence, the following PHP code removes the empty divider blocks, identifies the reusable/nested/grouped blocks and adds their data to the first level, and removes all data from all sublevels:

<div class="break-out">

 <pre><code class="language-php">/&#42;&#42;
 &#42; Export all (Gutenberg) blocks' data from a WordPress post
 &#42;/
function get_block_data($content, $remove_divider_block = true)
{
  // Parse the blocks, and convert them into a single-level array
  $ret = [];
  $blocks = parse_blocks($content);
  recursively_add_blocks($ret, $blocks);

  // Maybe remove blocks without name
  if ($remove_divider_block) {
    $ret = remove_blocks_without_name($ret);
  }

  // Remove 'innerBlocks' property if it exists (since that code was copied to the first level, it is currently duplicated)
  foreach ($ret as &$block) {
    unset($block['innerBlocks']);
  }

  return $ret;
}

/&#42;&#42;
 &#42; Remove the blocks without name, such as the empty block divider
 &#42;/
function remove_blocks_without_name($blocks)
{
  return array_values(array_filter(
    $blocks,
    function($block) {
      return $block['blockName'];
    }
  ));
}

/&#42;&#42;
 &#42; Add block data (including global and nested blocks) into the first level of the array
 &#42;/
function recursively_add_blocks(&$ret, $blocks) 
{  
  foreach ($blocks as $block) {
    // Global block: add the referenced block instead of this one
    if ($block['attrs']['ref']) {
      $ret = array_merge(
        $ret,
        recursively_render_block_core_block($block['attrs'])
      );
    }
    // Normal block: add it directly
    else {
      $ret[] = $block;
    }
    // If it contains nested or grouped blocks, add them too
    if ($block['innerBlocks']) {
      recursively_add_blocks($ret, $block['innerBlocks']);
    }
  }
}

/&#42;&#42;
 &#42; Function based on `render_block_core_block`
 &#42;/
function recursively_render_block_core_block($attributes) 
{
  if (empty($attributes['ref'])) {
    return [];
  }

  $reusable_block = get_post($attributes['ref']);
  if (!$reusable_block || 'wp_block' !== $reusable_block-&gt;post_type) {
    return [];
  }

  if ('publish' !== $reusable_block-&gt;post_status || ! empty($reusable_block-&gt;post_password)) {
    return [];
  }

  return get_block_data($reusable_block-&gt;post_content);
}
</code></pre>
</div>

Calling function `get_block_data($content)` passing the post content (`$post->post_content`) as parameter, we now obtain the following response:

<div class="break-out">

 <pre><code class="language-json">[[
  {
    "blockName": "core/image",
    "attrs": {
      "id": 70,
      "sizeSlug": "large"
    },
    "innerHTML": "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/sandwich-1024x614.jpg\" alt=\"\" class=\"wp-image-70\"/&gt;&lt;figcaption&gt;This is a normal block&lt;/figcaption&gt;&lt;/figure&gt;\n",
    "innerContent": [
      "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/sandwich-1024x614.jpg\" alt=\"\" class=\"wp-image-70\"/&gt;&lt;figcaption&gt;This is a normal block&lt;/figcaption&gt;&lt;/figure&gt;\n"
    ]
  },
  {
    "blockName": "core/paragraph",
    "attrs": [],
    "innerHTML": "\n&lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.&lt;/p&gt;\n",
    "innerContent": [
      "\n&lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.&lt;/p&gt;\n"
    ]
  },
  {
    "blockName": "core/columns",
    "attrs": [],
    "innerHTML": "\n&lt;div class=\"wp-block-columns\"&gt;\n\n&lt;/div&gt;\n",
    "innerContent": [
      "\n&lt;div class=\"wp-block-columns\"&gt;",
      null,
      "\n\n",
      null,
      "&lt;/div&gt;\n"
    ]
  },
  {
    "blockName": "core/column",
    "attrs": [],
    "innerHTML": "\n&lt;div class=\"wp-block-column\"&gt;&lt;/div&gt;\n",
    "innerContent": [
      "\n&lt;div class=\"wp-block-column\"&gt;",
      null,
      "&lt;/div&gt;\n"
    ]
  },
  {
    "blockName": "core/image",
    "attrs": {
      "id": 69,
      "sizeSlug": "large"
    },
    "innerHTML": "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/espresso-1024x614.jpg\" alt=\"\" class=\"wp-image-69\"/&gt;&lt;/figure&gt;\n",
    "innerContent": [
      "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/espresso-1024x614.jpg\" alt=\"\" class=\"wp-image-69\"/&gt;&lt;/figure&gt;\n"
    ]
  },
  {
    "blockName": "core/column",
    "attrs": [],
    "innerHTML": "\n&lt;div class=\"wp-block-column\"&gt;&lt;/div&gt;\n",
    "innerContent": [
      "\n&lt;div class=\"wp-block-column\"&gt;",
      null,
      "&lt;/div&gt;\n"
    ]
  },
  {
    "blockName": "core/paragraph",
    "attrs": [],
    "innerHTML": "\n&lt;p&gt;This is how I wake up every morning&lt;/p&gt;\n",
    "innerContent": [
      "\n&lt;p&gt;This is how I wake up every morning&lt;/p&gt;\n"
    ]
  },
  {
    "blockName": "core/group",
    "attrs": [],
    "innerHTML": "\n&lt;div class=\"wp-block-group\"&gt;&lt;div class=\"wp-block-group__inner-container\"&gt;\n\n&lt;/div&gt;&lt;/div&gt;\n",
    "innerContent": [
      "\n&lt;div class=\"wp-block-group\"&gt;&lt;div class=\"wp-block-group__inner-container\"&gt;",
      null,
      "\n\n",
      null,
      "&lt;/div&gt;&lt;/div&gt;\n"
    ]
  },
  {
    "blockName": "core/image",
    "attrs": {
      "id": 71,
      "sizeSlug": "large"
    },
    "innerHTML": "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/coffee-1024x614.jpg\" alt=\"\" class=\"wp-image-71\"/&gt;&lt;figcaption&gt;First element of the group&lt;/figcaption&gt;&lt;/figure&gt;\n",
    "innerContent": [
      "\n&lt;figure class=\"wp-block-image size-large\"&gt;&lt;img src=\"https://localhost/wp-content/uploads/2017/12/coffee-1024x614.jpg\" alt=\"\" class=\"wp-image-71\"/&gt;&lt;figcaption&gt;First element of the group&lt;/figcaption&gt;&lt;/figure&gt;\n"
    ]
  },
  {
    "blockName": "core/paragraph",
    "attrs": [],
    "innerHTML": "\n&lt;p&gt;Second element of the group&lt;/p&gt;\n",
    "innerContent": [
      "\n&lt;p&gt;Second element of the group&lt;/p&gt;\n"
    ]
  }
]
</code></pre>
</div>

Even though not strictly necessary, it is very helpful to create a REST API endpoint to output the result of our new function `get_block_data($content)`, which will allow us to easily understand what blocks are contained in a specific post, and how they are structured. The code below adds such endpoint under `/wp-json/block-metadata/v1/data/{POST_ID}`: 

<div class="break-out">

 <pre><code class="language-php">/&#42;&#42;
 &#42; Define REST endpoint to visualize a post’s block data
 &#42;/
add_action('rest_api_init', function () {
  register_rest_route('block-metadata/v1', 'data/(?P<post_id>\d+)', [
    'methods'  => 'GET',
    'callback' => 'get_post_blocks'
  ]);
});
function get_post_blocks($request) 
{
  $post = get_post($request['post_id']);
  if (!$post) {
    return new WP_Error('empty_post', 'There is no post with this ID', array('status' => 404));
  }

  $block_data = get_block_data($post->post_content);
  $response = new WP_REST_Response($block_data);
  $response->set_status(200);
  return $response;
}
</code></pre>
</div>

To see it in action, check out [this link](https://nextapi.getpop.org/wp-json/block-metadata/v1/data/1499) which exports the data for [this post](https://nextapi.getpop.org/posts/cope-with-wordpress-post-demo-containing-plenty-of-blocks/).

## 2. Extracting All Block Metadata Into A Medium-Agnostic Format

At this stage, we have block data containing HTML code which is not appropriate for COPE. Hence, we must strip the non-semantic HTML tags for each block as to convert it into a medium-agnostic format.

We can decide which are the attributes that must be extracted on a block type by block type basis (for instance, extract the text alignment property for `"paragraph"` blocks, the video URL property for the `"youtube embed"` block, and so on).

As we saw earlier on, not all attributes are actually saved as block attributes but within the block’s inner content, hence, for these situations, we will need to parse the HTML content using regular expressions in order to extract those pieces of metadata.

After inspecting all blocks shipped through WordPress core, I decided not to extract metadata for the following ones:

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>"core/columns"</code><br /><code>"core/column"</code><br /><code>"core/cover"</code></td>
      <td>These apply only to screen-based mediums and (being nested blocks) are difficult to deal with.</td>
    </tr>
    <tr>
      <td><code>"core/html"</code></td>
      <td>This one only makes sense for web.</td>
    </tr>
    <tr>
      <td><code>"core/table"</code><br /><code>"core/button"</code><br /><code>"core/media-text"</code></td>
      <td>I had no clue how to represent their data on a medium-agnostic fashion or if it even makes sense.</td>
    </tr>
  </tbody>
</table>

This leaves me with the following blocks, for which I’ll proceed to extract their metadata:

<ul>
  <li><a href="#core-paragraph"><code>'core/paragraph'</code></a></li>
  <li><a href="#core-image"><code>'core/image'</code></a></li>
  <li><a href="#core-embed-youtube"><code>'core-embed/youtube'</code></a> (as a representative of all the <code>'core-embed'</code> blocks)</li>
  <li><a href="#core-heading"><code>'core/heading'</code></a></li>
  <li><a href="#core-gallery"><code>'core/gallery'</code></a></li>
  <li><a href="#core-list"><code>'core/list'</code></a></li>
  <li><a href="#core-audio"><code>'core/audio'</code></a></li>
  <li><a href="#core-file"><code>'core/file'</code></a></li>
  <li><a href="#core-video"><code>'core/video'</code></a></li>
  <li><a href="#core-code"><code>'core/code'</code></a></li>
  <li><a href="#core-preformatted"><code>'core/preformatted'</code></a></li>
  <li><a href="#core-quotes"><code>'core/quote'</code> &amp; <code>'core/pullquote'</code></a></li>
  <li><a href="#core-verse"><code>'core/verse'</code></a></li>
</ul>

To extract the metadata, we create function `get_block_metadata($block_data)` which receives an array with the block data for each block (i.e. the output from our previously-implemented function `get_block_data`) and, depending on the block type (provided under property `"blockName"`), decides what attributes are required and how to extract them:

<div class="break-out">

 <pre><code class="language-php">/&#42;&#42;
 &#42; Process all (Gutenberg) blocks' metadata into a medium-agnostic format from a WordPress post
 &#42;/
function get_block_metadata($block_data)
{
  $ret = [];
  foreach ($block_data as $block) {
    $blockMeta = null;
    switch ($block['blockName']) {
      case ...:
        $blockMeta = ...
        break;
      case ...:
        $blockMeta = ...
        break;
      ...
    }

    if ($blockMeta) {
      $ret[] = [
        'blockName' => $block['blockName'],
        'meta' => $blockMeta,
      ];
    }
  }

  return $ret;
}
</code></pre>
</div>

Let’s proceed to extract the metadata for each block type, one by one:

### <code>"core/paragraph"</code>

Simply remove the HTML tags from the content, and remove the trailing breaklines.

<pre><code class="language-php">case 'core/paragraph':
  $blockMeta = [
    'content' => trim(strip_html_tags($block['innerHTML'])),
  ];
  break;
</code></pre>

### <code>'core/image'</code>

  The block either has an ID referring to an uploaded media file or, if not, the image source must be extracted from under `<img   src="...">`. Several attributes (caption, linkDestination, link, alignment) are optional. 

<div class="break-out">

 <pre><code class="language-php">case 'core/image':
  $blockMeta = [];
  // If inserting the image from the Media Manager, it has an ID
  if ($block['attrs']['id'] && $img = wp_get_attachment_image_src($block['attrs']['id'], $block['attrs']['sizeSlug'])) {
    $blockMeta['img'] = [
      'src' => $img[0],
      'width' => $img[1],
      'height' => $img[2],
    ];
  }
  elseif ($src = extract_image_src($block['innerHTML'])) {
    $blockMeta['src'] = $src;
  }
  if ($caption = extract_caption($block['innerHTML'])) {
    $blockMeta['caption'] = $caption;
  }
  if ($linkDestination = $block['attrs']['linkDestination']) {
    $blockMeta['linkDestination'] = $linkDestination;
    if ($link = extract_link($block['innerHTML'])) {
      $blockMeta['link'] = $link;
    }
  }
  if ($align = $block['attrs']['align']) {
    $blockMeta['align'] = $align;
  }
  break;
</code></pre>
</div>

It makes sense to create functions `extract_image_src`, `extract_caption` and `extract_link` since their regular expressions will be used time and again for several blocks. Please notice that a caption in Gutenberg can contain links (`<a href="...">`), however, when calling `strip_html_tags`, these are removed from the caption.

Even though regrettable, I find this practice unavoidable, since we can’t guarantee a link to work in non-web platforms. Hence, even though the content is gaining universality since it can be used for different mediums, it is also losing specificity, so its quality is poorer compared to content that was created and customized for the particular platform.

<div class="break-out">

 <pre><code class="language-php">function extract_caption($innerHTML)
{
  $matches = [];
  preg_match('/&lt;figcaption&gt;(.*?)&lt;\/figcaption&gt;/', $innerHTML, $matches);
  if ($caption = $matches[1]) {
    return strip_html_tags($caption);
  }
  return null;
}

function extract_link($innerHTML)
{
  $matches = [];
  preg_match('/&lt;a href="(.*?)"&gt;(.*?)&lt;\/a>&gt;', $innerHTML, $matches);
  if ($link = $matches[1]) {
    return $link;
  }
  return null;
}

function extract_image_src($innerHTML)
{
  $matches = [];
  preg_match('/&lt;img src="(.&#42;?)"/', $innerHTML, $matches);
  if ($src = $matches[1]) {
    return $src;
  }
  return null;
}
</code></pre>
</div>

### <code>'core-embed/youtube'</code>

Simply retrieve the video URL from the block attributes, and extract its caption from the HTML content, if it exists.

<pre><code class="language-php">case 'core-embed/youtube':
  $blockMeta = [
    'url' => $block['attrs']['url'],
  ];
  if ($caption = extract_caption($block['innerHTML'])) {
    $blockMeta['caption'] = $caption;
  }
  break;
</code></pre>

### <code>'core/heading'</code>

Both the header size (h1, h2, ..., h6) and the heading text are not attributes, so these must be obtained from the HTML content. Please notice that, instead of returning the HTML tag for the header, the `size` attribute is simply an equivalent representation, which is more agnostic and makes better sense for non-web platforms.

<div class="break-out">

 <pre><code class="language-php">case 'core/heading':
  $matches = [];
  preg_match('/&lt;h[1-6])&gt;(.*?)&lt;\/h([1-6])&gt;/', $block['innerHTML'], $matches);
  $sizes = [
    null,
    'xxl',
    'xl',
    'l',
    'm',
    'sm',
    'xs',
  ];
  $blockMeta = [
    'size' => $sizes[$matches[1]],
    'heading' => $matches[2],
  ];
  break;
</code></pre>
</div>

### <code>'core/gallery'</code>

Unfortunately, for the image gallery I have been unable to extract the captions from each image, since these are not attributes, and extracting them through a simple regular expression can fail: If there is a caption for the first and third elements, but none for the second one, then I wouldn’t know which caption corresponds to which image (and I haven’t devoted the time to create a complex regex). Likewise, in the logic below I'm always retrieving the `"full"` image size, however, this doesn’t have to be the case, and I'm unaware of how the more appropriate size can be inferred.

<pre><code class="language-php">case 'core/gallery':
  $imgs = [];
  foreach ($block['attrs']['ids'] as $img_id) {
    $img = wp_get_attachment_image_src($img_id, 'full');
    $imgs[] = [
      'src' => $img[0],
      'width' => $img[1],
      'height' => $img[2],
    ];
  }
  $blockMeta = [
    'imgs' => $imgs,
  ];
  break;
</code></pre>

### <code>'core/list'</code>

Simply transform the `<li>` elements into an array of items.

<pre><code class="language-php">case 'core/list':
  $matches = [];
  preg_match_all('/&lt;li&gt;(.*?)&lt;\/li&gt;/', $block['innerHTML'], $matches);
  if ($items = $matches[1]) {
    $blockMeta = [
      'items' => array_map('strip_html_tags', $items),
    ];
  }
  break;
</code></pre>

### <code>'core/audio'</code>

Obtain the URL of the corresponding uploaded media file.

<pre><code class="language-php">case 'core/audio':
  $blockMeta = [
    'src' => wp_get_attachment_url($block['attrs']['id']),
  ];
  break;
</code></pre>

### <code>'core/file'</code>

Whereas the URL of the file is an attribute, its text must be extracted from the inner content.

<div class="break-out">

 <pre><code class="language-php">case 'core/file':
  $href = $block['attrs']['href'];
  $matches = [];
  preg_match('/&lt;a href="'.str_replace('/', '\/', $href).'"&gt;(.&#42;?)&lt;\/a&gt;/', $block['innerHTML'], $matches);
  $blockMeta = [
    'href' =&gt; $href,
    'text' =&gt; strip_html_tags($matches[1]),
  ];
  break;
</code></pre>
</div>

### <code>'core/video'</code>

Obtain the video URL and all properties to configure how the video is played through a regular expression. If Gutenberg ever changes the order in which these properties are printed in the code, then this regex will stop working, evidencing one of the problems of not adding metadata directly through the block attributes.

<pre><code class="language-php">case 'core/video':
  $matches = [];
  preg_match('/<video (autoplay )?(controls )?(loop )?(muted )?(poster="(.&#42;?)" )?src="(.&#42;?)"( playsinline)?>&lt;\/video&gt;&gt;', $block['innerHTML'], $matches);
  $blockMeta = [
    'src' => $matches[7],
  ];
  if ($poster = $matches[6]) {
    $blockMeta['poster'] = $poster;
  }
  // Video settings
  $settings = [];
  if ($matches[1]) {
    $settings[] = 'autoplay';
  }
  if ($matches[2]) {
    $settings[] = 'controls';
  }
  if ($matches[3]) {
    $settings[] = 'loop';
  }
  if ($matches[4]) {
    $settings[] = 'muted';
  }
  if ($matches[8]) {
    $settings[] = 'playsinline';
  }
  if ($settings) {
    $blockMeta['settings'] = $settings;
  }
  if ($caption = extract_caption($block['innerHTML'])) {
    $blockMeta['caption'] = $caption;
  }
  break;
</code></pre>

### <code>'core/code'</code>

Simply extract the code from within `<code />`.

<pre><code class="language-php">case 'core/code':
  $matches = [];
  preg_match('/&lt;code&gt;(.*?)&lt;\/code>/is', $block['innerHTML'], $matches);
  $blockMeta = [
    'code' => $matches[1],
  ];
  break;
</code></pre>

### <code>'core/preformatted'</code>

Similar to `<code />`, but we must watch out that Gutenberg hardcodes a class too.

<div class="break-out">

 <pre><code class="language-php">case 'core/preformatted':
  $matches = [];
  preg_match('/&lt;pre class="wp-block-preformatted">(.*?)&lt;\/pre&gt;/is', $block['innerHTML'], $matches);
  $blockMeta = [
    'text' => strip_html_tags($matches[1]),
  ];
  break;
</pre></code>
</div>

### <code>'core/quote'</code> and <code>'core/pullquote'</code>

We must convert all inner `<p />` tags to their equivalent generic `"\n"` character.

<div class="break-out">

 <pre><code class="language-php">case 'core/quote':
case 'core/pullquote':
  $matches = [];
  $regexes = [
    'core/quote' =&gt; '/&lt;blockquote class=\"wp-block-quote\"&gt;(.&#42;?)&lt;\/blockquote&gt;/',
    'core/pullquote' =&gt; '/&lt;figure class=\"wp-block-pullquote\"&gt;&lt;blockquote&gt;(.*?)&lt;\/blockquote&gt;&lt;\/figure&gt;/',
  ];
  preg_match($regexes[$block['blockName']], $block['innerHTML'], $matches);
  if ($quoteHTML = $matches[1]) {
    preg_match_all('/&lt;p&gt;(.*?)&lt;\/p&gt;/', $quoteHTML, $matches);
    $blockMeta = [
      'quote' =&gt; strip_html_tags(implode('\n', $matches[1])),
    ];
    preg_match('/&lt;cite&gt;(.*?)&lt;\/cite&gt;/', $quoteHTML, $matches);
    if ($cite = $matches[1]) {
      $blockMeta['cite'] = strip_html_tags($cite);
    }
  }
  break;
</code></pre>
</div>

### <code>'core/verse'</code>

Similar situation to `<pre />`.

<div class="break-out">

 <pre><code class="language-php">case 'core/verse':
  $matches = [];
  preg_match('/&lt;pre class="wp-block-verse"&gt;(.*?)&lt;\/pre&gt;/is', $block['innerHTML'], $matches);
  $blockMeta = [
    'text' => strip_html_tags($matches[1]),
  ];
  break;
</code></pre>
</div>

## 3. Exporting Data Through An API

Now that we have extracted all block metadata, we need to make it available to our different mediums, through an API. WordPress has access to the following APIs:

- REST, through the [WP REST API](https://developer.wordpress.org/rest-api/) (integrated in WordPress core)
- GraphQL, through [WPGraphQL](https://www.wpgraphql.com/)
- PoP, through its [implementation for WordPress](https://github.com/leoloso/pop-api-wp)

Let’s see how to export the data through each of them.

### REST

The following code creates endpoint `/wp-json/block-metadata/v1/metadata/{POST_ID}` which exports all block metadata for a specific post:

<div class="break-out">

 <pre><code class="language-php">/**
 * Define REST endpoints to export the blocks' metadata for a specific post
 */
add_action('rest_api_init', function () {
  register_rest_route('block-metadata/v1', 'metadata/(?P<post_id>\d+)', [
    'methods'  => 'GET',
    'callback' => 'get_post_block_meta'
  ]);
});
function get_post_block_meta($request) 
{
  $post = get_post($request['post_id']);
  if (!$post) {
    return new WP_Error('empty_post', 'There is no post with this ID', array('status' => 404));
  }

  $block_data = get_block_data($post->post_content);
  $block_metadata = get_block_metadata($block_data);
  $response = new WP_REST_Response($block_metadata);
  $response->set_status(200);
  return $response;
}
</code></pre>
</div>

To see it working, [this link](https://nextapi.getpop.org/wp-json/block-metadata/v1/metadata/1499) (corresponding to [this blog post](https://nextapi.getpop.org/posts/cope-with-wordpress-post-demo-containing-plenty-of-blocks/)) displays the metadata for blocks of all the types analyzed earlier on.

### GraphQL (Through WPGraphQL)

GraphQL works by setting-up [schemas and types](https://graphql.org/learn/schema/) which define the structure of the content, from which arises this API’s power to fetch exactly the required data and nothing else. Setting-up schemas works very well when the structure of the object has a unique representation.

In our case, however, the metadata returned by a new field `"block_metadata"` (which calls our newly-created function `get_block_metadata`) depends on the specific block type, so the structure of the response can vary wildly; GraphQL provides a solution to this issue through a [Union type](https://graphql.org/learn/schema/#union-types), allowing to return one among a set of different types. However, its [implementation](https://docs.wpgraphql.com/extending/types) for all different variations of the metadata structure has proved to be a lot of work, and I quit along the way 😢. 

As an alternative (not ideal) solution, I decided to provide the response by simply encoding the JSON object through a new field `"jsonencoded_block_metadata"`:

<div class="break-out">

 <pre><code class="language-php">/**
 * Define WPGraphQL field "jsonencoded_block_metadata"
 */
add_action('graphql_register_types', function() {
  register_graphql_field(
    'Post',
    'jsonencoded_block_metadata',
    [
      'type'        => 'String',
      'description' => __('Post blocks encoded as JSON', 'wp-graphql'),
      'resolve'     => function($post) {
        $post = get_post($post->ID);
        $block_data = get_block_data($post->post_content);
        $block_metadata = get_block_metadata($block_data);
        return json_encode($block_metadata);
      }
    ]
  );
});
</code></pre>
</div>

### PoP

**Note:** This functionality is available on its own [GitHub repo](https://github.com/getpop/block-metadata-for-wp).

The final API is called PoP, which is a [little-known project](https://github.com/leoloso/PoP) I’ve been working on for several years now. I have recently converted it into a full-fledged API, with the capacity to [produce a response compatible with both REST and GraphQL](https://github.com/getpop/api), and which even benefits from the advantages from these 2 APIs, at the same time: no under/over-fetching of data, like in GraphQL, while being cacheable on the server-side and not susceptible to DoS attacks, like REST. It offers a mix between the two of them: REST-like endpoints with GraphQL-like queries.

The block metadata is made available through the API through the following code:

<div class="break-out">

 <pre><code class="language-php">class PostFieldValueResolver extends AbstractDBDataFieldValueResolver
{
  public static function getClassesToAttachTo(): array
  {
    return array(\PoP\Posts\FieldResolver::class);
  }

  public function resolveValue(FieldResolverInterface $fieldResolver, $resultItem, string $fieldName, array $fieldArgs = [])
  {
    $post = $resultItem;
    switch ($fieldName) {
      case 'block-metadata':
        $block_data = \Leoloso\BlockMetadata\Data::get_block_data($post->post_content);
        $block_metadata = \Leoloso\BlockMetadata\Metadata::get_block_metadata($block_data);

        // Filter by blockName
        if ($blockName = $fieldArgs['blockname']) {
          $block_metadata = array_filter(
            $block_metadata,
            function($block) use($blockName) {
              return $block['blockName'] == $blockName;
            }
          );
        }
        return $block_metadata;
    }

    return parent::resolveValue($fieldResolver, $resultItem, $fieldName, $fieldArgs);
  }
}
</code></pre>
</div>

To see it in action, [this link](https://nextapi.getpop.org/posts/api/graphql/?query=block-metadata|id|title|url,author.id|name) displays the block metadata (+ ID, title and URL of the post, and the ID and name of its author, à la GraphQL) for a list of posts.

In addition, similar to [GraphQL arguments](https://graphql.org/learn/queries/#arguments), our query can be customized through field arguments, enabling to obtain only the data that makes sense for a specific platform. For instance, if we desire to extract all Youtube videos added to all posts, we can add modifier `(blockname:core-embed/youtube)` to field `block-metadata` in the endpoint URL, like in [this link](https://nextapi.getpop.org/posts/api/graphql/?query=block-metadata(blockname:core-embed/youtube)|id|title|url). Or if we want to extract all images from a specific post, we can add modifier `(blockname:core/image)` like in [this other link](https://nextapi.getpop.org/markup/markup-image-alignment/api/graphql/?query=block-metadata(blockname:core/image)|id|title)|id|title).

## Conclusion

The COPE ("Create Once, Publish Everywhere") strategy helps us lower the amount of work needed to create several applications which must run on different mediums (web, email, apps, home assistants, virtual reality, etc) by creating a single source of truth for our content. Concerning WordPress, even though it has always shined as a Content Management System, implementing the COPE strategy has historically proved to be a challenge.

However, a couple of recent developments have made it increasingly feasible to implement this strategy for WordPress. On one side, since the integration into core of the WP REST API, and more markedly since the launch of Gutenberg, most WordPress content is accessible through APIs, making it a genuine headless system. On the other side, Gutenberg (which is the new default content editor) is block-based, making all metadata inside a blog post readily accessible to the APIs. 

As a consequence, implementing COPE for WordPress is straightforward. In this article, we have seen how to do it, and all the relevant code has been made available through several repositories. Even though the solution is not optimal (since it involves plenty of parsing HTML code), it still works fairly well, with the consequence that the effort needed to release our applications to multiple platforms can be greatly reduced. Kudos to that!

{{< signature "dm, il" >}}
