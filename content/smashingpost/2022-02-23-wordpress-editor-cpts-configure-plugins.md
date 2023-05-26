---
title: 'Using The WordPress Editor And CPTs To Configure Plugins'
slug: wordpress-editor-cpts-configure-plugins
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/854c1fe6-8061-4a9f-bf59-75f81a732114/wordpress-editor-cpts-configure-plugins.jpg
date: 2022-02-23T10:30:00.000Z
summary: >-
  If we want our WordPress plugins to offer a settings page that is fully powered by blocks, how can we do it? Since Full Site Editing doesn’t support this feature yet, we need to code a custom solution. In this article, we will learn how we can do it.
description: >-
  If we want our WordPress plugins to offer a settings page that is fully powered by blocks, how can we do it? Since *Full Site Editing* doesn’t support this feature yet, we need to code a custom solution. In this article, we will learn how we can do it.
categories:
  - WordPress
  - Plugins
  - Tools
---

WordPress 5.9 was released recently shipping with Full Site Editing (FSE), which enables using blocks to create the layout for any page in the website (as was already possible to write posts via the WordPress editor). Slowly but surely, blocks are becoming the main user interface for creating WordPress sites.
 
However, FSE does not fully help us configure WordPress sites. While it already does provide global settings via `theme.json`, that’s mainly for configuring the theme’s visual options, such as fonts, colors and paddings; for a theme or plugin’s invisible settings, usually defined as some entry in the `wp_options` table, FSE offers no support (yet).
 
Providing a settings page for our themes and plugins that is fully powered by blocks would provide a compelling user experience. Through it, we could allow our users to input configuration values using components tailored to that type of value, such as calendars to input dates, interactive maps to input location coordinates, sliders to pick a number from within a range (such as WooCommerce’s slider block to filter prices, displayed below), and so on.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8257b50-f717-4b88-a1f3-c47779746fb0/1-wordpress-editor-cpts-configure-plugins.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8257b50-f717-4b88-a1f3-c47779746fb0/1-wordpress-editor-cpts-configure-plugins.png" width="800" height="571" sizes="100vw" caption="WooCommerce provides a slider block to filter prices. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8257b50-f717-4b88-a1f3-c47779746fb0/1-wordpress-editor-cpts-configure-plugins.png'>Large preview</a>)" alt="WooCommerce provides a slider block to filter prices" >}}
 
If we want to implement custom settings pages powered by blocks, for the time being, we will need to implement a custom solution.
 
We may eventually be able to create a page in the `wp-admin` that directly renders &mdash; and allows to interact with &mdash; the needed blocks, as I recently described in my recent article, “[Implications Of WordPress Joining The Block Protocol](https://www.smashingmagazine.com/2022/02/implications-wordpress-joining-block-protocol/),” but that's currently only under consideration &mdash; nowhere near of it becoming a reality (if it ever does).

A related approach that is doable already today, is to create a standard page in the `wp-admin` that loads React and reuses the components powering our blocks (that is, the components making up the blocks, but not the blocks themselves). However, we would then be reinventing the wheel, to produce a GUI of lower quality than the one from the WordPress editor.
 
A better approach is to still use the WordPress editor, but altering its objective: instead of creating content for a blog post, we can produce the configuration required for our plugin. This is not difficult: because the WordPress editor can power custom post types (CPTs), we can then create a specific CPT that models the required configuration, and have the plugin retrieve the stored data from within the custom post content.
 
In this scenario, we must limit which blocks are available when editing the CPT and, quite likely, lock them using a predefined template. We must also be careful: the CPT content is of private use to the plugin, not intended for public consumption, so we must make sure it cannot be loaded on the public-facing website.
 
This is the strategy I employed for my WordPress plugin. In this write-up, I will describe my implementation (fully available in the [the `leoloso/PoP` repo](https://github.com/leoloso/PoP)), which aims to leverage the WordPress editor to provide a great user experience for configuring our themes and plugins.

{{% feature-panel %}} 

## Overview Of The Results

I’ll first give an overview of what’s the objective: what functionality I’ve planned for my plugin to support.
 
My plugin installs a GraphQL server that supports [persisted queries](https://graphql-api.com/features/#heading-persisted-queries). To retrieve data for a persisted query in the WordPress site, I decided to create a new CPT called `persisted-query`, and retrieve its data simply by requesting its permalink.
 
The CPT uses the standard WordPress editor, powered by blocks:
 
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e967c17-eb46-49d2-b9bb-c016074bcec3/2-wordpress-editor-cpts-configure-plugins.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e967c17-eb46-49d2-b9bb-c016074bcec3/2-wordpress-editor-cpts-configure-plugins.png" width="800" height="504" sizes="100vw" caption="Persisted query CPT. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e967c17-eb46-49d2-b9bb-c016074bcec3/2-wordpress-editor-cpts-configure-plugins.png'>Large preview</a>)" alt="Persisted query CPT" >}}
 
Persisted queries can be configured according to rules, involving access control and HTTP caching. Selecting what rules must be applied could be done within the persisted-query CPT itself, via some custom block. However, different persisted queries will usually require the same set of rules, and if the set changes, then all persisted queries would need to be updated. That is something I’d rather avoid.
 
So, I decided to create a new CPT containing the selected rules, which could then be applied across different persisted queries. This CPT, called `schema-config`, contains custom blocks to allow users to select which Access Control Lists and Cache-Control Lists must be applied:
 
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9700dc02-46ed-4938-9379-1146f2f8cbd2/3-wordpress-editor-cpts-configure-plugins.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9700dc02-46ed-4938-9379-1146f2f8cbd2/3-wordpress-editor-cpts-configure-plugins.png" width="800" height="502" sizes="100vw" caption="Schema configuration CPT. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9700dc02-46ed-4938-9379-1146f2f8cbd2/3-wordpress-editor-cpts-configure-plugins.png'>Large preview</a>)" alt="Schema configuration CPT" >}}
 
The relationship between a persisted query and its schema configuration must be provided by the user. If the user had the Advanced Custom Fields plugin installed, then providing the interface to create this relationship would be very easy. However, I cannot make such an assumption, or I’d be excluding many potential users.
 
So, I had to code my own solution, for which I created a custom block that displays the list of all the schema configurations, and had it embedded in the editor of the persisted query CPT:
 
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dd9f9fe-36d3-4e9e-9fc9-ba4e3abbcc22/4-wordpress-editor-cpts-configure-plugins.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dd9f9fe-36d3-4e9e-9fc9-ba4e3abbcc22/4-wordpress-editor-cpts-configure-plugins.png" width="800" height="501" sizes="100vw" caption="Selecting the schema configuration within the persisted query CPT. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dd9f9fe-36d3-4e9e-9fc9-ba4e3abbcc22/4-wordpress-editor-cpts-configure-plugins.png'>Large preview</a>)" alt="Selecting the schema configuration within the persisted query CPT" >}}

In this solution, both CPTs are created using the WordPress editor, and I can create custom blocks for each of them. The `persisted-query` CPT is public since users must be able to load it as to retrieve the response from the query. The `schema-config` CPT, though, is private; it must be accessed only by the plugin, to retrieve configuration data used to render the persisted query.
 
Let’s explore next how to implement it.

## Creating The CPTs

To create a custom post type we use the [`register_post_type` method](https://developer.wordpress.org/reference/functions/register_post_type/):

<pre><code class="language-javascript">function create_persisted_query_cpt(): void
{
  $labels = [
    'name'               =&gt; 'Persisted queries',
    'singular_name'      =&gt; 'Persisted query',
    'menu_name'          =&gt; 'Persisted queries',
    'name_admin_bar'     =&gt; 'Persisted query',
    'add_new'            =&gt; 'Add New',
    'add_new_item'       =&gt; 'Add New Persisted query',
    'new_item'           =&gt; 'New Persisted query',
    'edit_item'          =&gt; 'Edit Persisted query',
    'view_item'          =&gt; 'View Persisted query',
    'all_items'          =&gt; 'All Persisted queries',
    'search_items'       =&gt; 'Search Persisted queries',
    'parent_item_colon'  =&gt; 'Parent Persisted query',
    'not_found'          =&gt; 'No Persisted queries found',
    'not_found_in_trash' =&gt; 'No Persisted queries found in Trash'
  ];
  $args = [
    'labels'              =&gt; $labels,
    'public'              =&gt; true,
    'show_in_rest'        =&gt; true,
    'rewrite'             =&gt; ['slug' =&gt; 'persisted-query'],
  ];

  register_post_type('persisted-query', $args);
}
add_action('init', 'create_persisted_query_cpt');</code></pre>
 
The code above applies to creating the public CPT. To create a private CPT, we need only switch the `public` argument to `false`; argument `show_in_rest` must still be `true`, as to be able to retrieve its data via the WP REST API (which powers the blocks in the WordPress editor):
 

<pre><code class="language-javascript">function create_schema_config_cpt(): void
{
  $labels = [
    'name'               =&gt; 'Schema configurations',
    'singular_name'      =&gt; 'Schema configuration',
    // All the rest...
  ];
  $args = [
    'public'              =&gt; false,
    'show_in_rest'        =&gt; true,
    // ...
  ];
}
add_action('init', 'create_schema_config_cpt');</code></pre>
 
For finer control, we can also set the value of [the other arguments](https://developer.wordpress.org/reference/functions/register_post_type/#parameters), including: `exclude_from_search`, `publicly_queryable`, `show_ui`, `show_in_nav_menus`, `show_in_menu` and `show_in_admin_bar`.

As a side note, please notice how, due to the effort to avoid introducing breaking changes in each new release of WordPress (mostly on the PHP side; the JS side powering the WordPress editor has undergone some instability), old guides on the topic, such as [this Smashing article from 2015](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/#registering-the-post-type), will still be mostly up to date. The `show_in_rest` argument (and also `template`, used later on) is not explained there but, otherwise, everything else still works. And the CPT will by default use the new WordPress editor, instead of the “Classic” editor.

{{% ad-panel-leaderboard %}}

## Creating The Custom Block
 
By now, I have created my public and private CPTs. The next step is to link them up, by embedding a custom block that lists all entries from the private CPT `schema-config` in the editor for the public CPT `persisted-query`.
 
The easiest way to set up a new block is through [`@wordpress/create-block`](https://www.npmjs.com/package/@wordpress/create-block), which by default generates a new WordPress plugin containing a single block. If we already have the plugin, after running command `npx @wordpress/create-block my-block`, we can copy the PHP code for registering the block, and the JS/CSS files for the block, copy them to our plugin and discard everything else.
 
I did this to create my custom block, of type `graphql-api/schema-configuration`:
 
<div class="break-out">

<pre><code class="language-javascript">import { registerBlockType } from '@wordpress/blocks';
import { &#95;&#95; } from '@wordpress/i18n';

registerBlockType( 'graphql-api/schema-configuration', {
  title: &#95;&#95;( 'Schema Configuration', 'graphql-api' ),
  description: &#95;&#95;( 'Select the Schema Configuration for the GraphQL persisted query', 'graphql-api' ),
  icon: 'admin-users',

  // ...
} );</code></pre>
</div>

The custom block must be given the following behavior.
 
**First**: It must store the ID of the selected `schema-config` CPT entry, for which I register an attribute `schemaConfiguration` of type `integer`:
 

<pre><code class="language-javascript">registerBlockType( 'graphql-api/schema-configuration', {
  // ...

  /&#42;&#42;
   &#42; 1. Store the ID of the selected schema configuration entry
   &#42;/
  attributes: {
    schemaConfiguration: {
      type: 'integer',
      default: 0,
    },
  },
} );</code></pre>
 
**Second**: It must only be available to the `persisted-query` CPT, and nowhere else.
 
For this, I define the `inserter` attribute to `false`, making the block unavailable in the editor, and it must be explicitly set via a template (more on this later on).

<pre><code class="language-javascript">registerBlockType( 'graphql-api/schema-configuration', {
  // ...

  /&#42;&#42;
   &#42; 2. The block can only be accessible to the "persisted-query" CPT
   &#42;/
  supports: {
    inserter: false,
  },
} );</code></pre>
 
**Third**: Don’t render the configuration.
 
This option shouldn’t matter much, because the block should not be printed on screen. Its only purpose is to store configuration to power some other functionality, such as rendering a persisted query.
 
However, just to be on the safe side and avoid unintended leaks, we’d rather not print the configuration data. More since the WordPress editor stores block data within an HTML comment, like this:

<div class="break-out">

<pre><code class="language-javascript">&lt;!-- wp:graphql-api/schema-config {"key1": "value1", "key2": "value2"} /--&gt;</code></pre>
</div>

This comment may be printed on the page without us being aware of it. While displaying the chosen schema configuration ID is not dangerous, we may as well store sensitive configuration data, such as API keys.
 
Then, for peace of mind, let’s produce some safe content in the block’s `save` method:
 

<pre><code class="language-javascript">registerBlockType( 'graphql-api/schema-configuration', {
  // ...

  /&#42;&#42;
   &#42; 3. Don't render the configuration
   &#42;/
  save() {
    return &lt;p&gt;You should not be reading this! 😈&lt;/p&gt;;
  },
} );</code></pre>
 
**Last**: The block must retrieve the list of the schema configuration entries, allow the user to select one by displaying them on suitable input control, and persist the selected entry in the DB.
 
This item will require a couple of steps:

1. Retrieving the schema configuration entries from the server.
2. Creating components to render the block.
 
To retrieve the list of entries from the `schema-config` CPT, the block [uses a store](https://github.com/leoloso/PoP/blob/ce6a059377f16c74239074a09aea02f3e76c850e/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/blocks/schema-configuration/src/store/resolvers.js) which works by executing a GraphQL query against the server:
 
<div class="break-out">

<pre><code class="language-javascript">import {
  receiveSchemaConfigurations,
  setSchemaConfigurations,
} from './action-creators';

export const FETCH_SCHEMA_CONFIGURATIONS_GRAPHQL_QUERY = `
  query GetSchemaConfigurations {
    schemaConfigurations {
      id
      title
    }
  }
`

export default {
  &#42; getSchemaConfigurations() {

    const response = yield receiveSchemaConfigurations( FETCH_SCHEMA_CONFIGURATIONS_GRAPHQL_QUERY );
    const schemaConfigurations = response.data?.schemaConfigurations || [];
    return setSchemaConfigurations( schemaConfigurations );
  },
};</code></pre>
</div>

To create components to render the block, we can conveniently use any React component to power our blocks, including those freely available in [npm](https://www.npmjs.com). I took advantage of this and imported the wonderful `Select` component offered by the [`react-select`](https://www.npmjs.com/package/react-select) package, as to allow the user to pick the schema configuration entry through a good-looking select input.
 
I created the hierarchy of components composing each other as to make the code reusable. At the bottom-most layer there is `<Select />`, which is wrapped by a custom [`SelectCard` component](https://github.com/leoloso/PoP/blob/380f16c46a91bb3d40fff53c6770a31c30d6d457/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/packages/components/src/components/select-card/select-card.js), which is itself wrapped by a top-level [`SchemaConfigurationSelectCard` component](https://github.com/leoloso/PoP/blob/73ebd08203d61693889553161d7be9b99e915d61/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/blocks/schema-configuration/src/schema-configuration.js). This latter component displays a select input with all the schema configuration entries, and `onChange` will persist the value of the selected entry to the DB:

<div class="break-out">

<pre><code class="language-javascript">import { withSelect } from '@wordpress/data';
import { compose, withState } from '@wordpress/compose';
import { &#95;&#95; } from '@wordpress/i18n';
import { SelectCard } from '@graphqlapi/components';

const SchemaConfigurationSelectCard = ( props ) =&gt; {
  const {
    schemaConfigurations,
    attributes: {
      schemaConfiguration
    }
  } = props;
  
  const schemaConfigurationOptions = schemaConfigurations.map( schemaConfiguration =&gt; (
    {
      label: schemaConfiguration.title,
      value: schemaConfiguration.id,
    }
  ) );
  const metaOptions = [
    {
      label: `🟡 ${ &#95;&#95;('Default', 'graphql-api') }`,
      value: 0,
    },
    {
      label: `❌ ${ &#95;&#95;('None', 'graphql-api') }`,
      value: -1,
    },
  ];
  const groupedOptions = [
    {
    label: '',
    options: metaOptions,
    },
    {
    label: '',
    options: schemaConfigurationOptions,
    },
  ];
  const selectedOptions = schemaConfigurationOptions.filter( option =&gt; option.value == schemaConfiguration );
  const defaultValue = selectedOptions[0];

  return (
    &lt;SelectCard
      { ...props }
      isMulti={ false }
      options={ groupedOptions }
      defaultValue={ defaultValue }
      onChange={ selected =&gt; setAttributes( {
        ['schemaConfiguration']: selected.value
      } ) }
    /&gt;
  );
}

export default compose( [
  withState( {
    label: &#95;&#95;('Schema configuration', 'graphql-api'),
  } ),
  withSelect( ( select ) =&gt; {
    const {
      getSchemaConfigurations,
    } = select ( 'graphql-api/schema-configuration' );
    return {
      schemaConfigurations: getSchemaConfigurations(),
    };
  } ),
] )( SchemaConfigurationSelectCard );</code></pre>
</div>
 
Finally, I embedded `<SchemaConfigurationSelectCard />` within the block's `edit` method:

<div class="break-out">

<pre><code class="language-javascript">import SchemaConfigurationSelectCard from './schema-configuration';

registerBlockType( 'graphql-api/schema-configuration', {
  // ...

  /&#42;&#42;
   &#42; 4. Display all schema configuration entries, and persist the selected entry to DB
   &#42;/
  edit(props) {
    const { className } = props;
    return (
      &lt;div class={ className }&gt;
        &lt;SchemaConfigurationSelectCard
          { ...props }
        /&gt;
      &lt;/div&gt;
    )
  },
} );</code></pre>
</div>

The resulting `index.js` file is [this one](https://github.com/leoloso/PoP/blob/6de7034b50fe69c1f93dc840d2adabfed34be3f3/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/blocks/schema-configuration/src/index.js):
 
<div class="break-out">

<pre><code class="language-javascript">import { registerBlockType } from '@wordpress/blocks';
import { &#95;&#95; } from '@wordpress/i18n';
import SchemaConfigurationSelectCard from './schema-configuration';

registerBlockType( 'graphql-api/schema-configuration', {
  title: &#95;&#95;( 'Schema Configuration', 'graphql-api' ),
  description: &#95;&#95;( 'Select the Schema Configuration for the GraphQL query', 'graphql-api' ),
  icon: 'admin-users',

  /&#42;&#42;
   &#42; 1. Store the ID of the selected schema configuration entry
   &#42;/
  attributes: {
    schemaConfiguration: {
      type: 'integer',
      default: 0,
    },
  },

  /&#42;&#42;
   &#42; 2. The block can only be accessible to the "persisted-query" CPT
   &#42;/
  supports: {
    inserter: false,
  },

  /&#42;&#42;
   &#42; 3. Don't render the configuration
   &#42;/
  save() {
    return &lt;p&gt;You should not be reading this! 🤔&lt;/p&gt;;
  },

  /&#42;&#42;
   &#42; 4. Display all schema configuration entries, and persisted the selected entry to DB
   &#42;/
  edit(props) {
    const { className } = props;
    return (
      &lt;div class={ className }&gt;
        &lt;SchemaConfigurationSelectCard
          { ...props }
        /&gt;
      &lt;/div&gt;
    )
  },
} );</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Embedding The Custom Block Within The Public CPT

By now, we have created the public and private CPTs, and the custom block that links them together. Next, we need to embed the custom block within the public CPT.
 
The schema configuration is mandatory, and it must be set only once. Hence, it makes no sense for the block to be added via the inserter in the editor, which would allow the user to not insert the block, or insert it multiple times. For that reason, earlier on we defined attribute `inserter` as `false` when registering the block.
 
Instead, we will “lock” a predefined template in the editor for the CPT, which specifies which blocks are to be used. For the persisted query, there will be two blocks:

1. The GraphiQL client (implemented [here](https://github.com/leoloso/PoP/blob/7677ddb44a8dd62b81377999ccd666b23d6b9eee/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/blocks/graphiql)),
2. The “schema configuration” block.
 
To do this, we can [define the template already when registering the post type](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-templates/#custom-post-types), or by setting properties [`template` and `template_lock` from the CPT object](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-templates/#locking):
 

<pre><code class="language-javascript">function register_persisted_query_template(): void
{
  $post_type_object = get_post_type_object( 'persisted-query' );
  $post_type_object-&gt;template = [
    ['graphql-api/graphiql'],
    ['graphql-api/schema-configuration'],
  ];
  $post_type_object-&gt;template_lock = 'all';
}
add_action( 'init', 'register_persisted_query_template' );</code></pre>

Now, when editing a persisted query, the predefined blocks will appear in the order and quantity specified, and be ready to be filled by the user.

## Retrieving The CPT Configuration Data

By now, the system is mostly in place: we have created our public and private CPTs and linked them both together via a custom block. By this stage, our plugin users can create schema configuration entries, and select the required one when creating a persisted query. As a result, we will have all this data stored in the database, under the corresponding custom post entry.
 
Finally, we need to render the persisted query dynamically, making use of the schema configuration. Let’s see how to read the configuration data in our PHP code.
 
We can access the schema configuration ID in the template `persisted-query.php` (or anywhere the CPT will be rendered). First, we parse the content of the persisted query via [`parse_blocks`](https://developer.wordpress.org/reference/functions/parse_blocks/), as to have access to the block data:
 
<div class="break-out">

<pre><code class="language-javascript">$persistedQueryObject = \get_post($persistedQueryID);
$persistedQueryBlocks = \parse_blocks($persistedQueryObject-&gt;post_content);</code></pre>
</div>

To retrieve the “schema-configuration” block, we must filter it by its name:

<pre><code class="language-javascript">$schemaConfigurationBlock = null;
foreach ($persistedQueryBlocks as $block) {
  if ($block['blockName'] === 'graphql-api/schema-configuration') {
    // We found the block
    $schemaConfigurationBlock = $block;
    break;
  }
}</code></pre>
 
Once we have the block, we can access its data under `attrs` and the name of the attribute we chose to store the data when registering the block, which was `"schemaConfiguration"`:
 
<div class="break-out">

<pre><code class="language-javascript">$schemaConfigurationID = $schemaConfigurationBlock['attrs']['schemaConfiguration'];</code></pre>
</div>

We have now retrieved the selected schema configuration ID. Repeating the same sequence, we can retrieve the block data saved in this custom post entry, which is our private configuration data.
 
The schema configuration CPT stores the selected access control entries under block [`schema-config-access-control-lists`](https://github.com/leoloso/PoP/blob/82f64fc5e761163642e4acd1e6acb07913a86233/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/blocks/schema-config-access-control-lists), and the selected cache control entries under block [`schema-config-cache-control-lists`](https://github.com/leoloso/PoP/blob/82f64fc5e761163642e4acd1e6acb07913a86233/layers/GraphQLAPIForWP/plugins/graphql-api-for-wp/blocks/schema-config-cache-control-lists):
 
<div class="break-out">

<pre><code class="language-javascript">$schemaConfigurationObject = \get_post($schemaConfigurationID);
$schemaConfigurationBlocks = \parse_blocks($schemaConfigurationObject-&gt;post_content);
$accessControlBlock = $cacheControlBlock = null;
foreach ($schemaConfigurationBlocks as $block) {
  if ($block['blockName'] === 'graphql-api/schema-config-access-control-lists') {
    $accessControlBlock = $block;
  } elseif ($block['blockName'] === 'graphql-api/schema-config-cache-control-lists') {
    $cacheControlBlock = $block;
  }
}

// Retrieve the stored configuration from the private CPT
$accessControlLists = $accessControlBlock['attrs']['accessControlLists'];;
$cacheControlLists = $cacheControlBlock['attrs']['cacheControlLists'];</code></pre>
</div>
 
Finally, we have retrieved the private configuration data, which we can use to decide how to render the persisted query (how my plugin then goes on to render this response is not important to the topic of this article):

<pre><code class="language-javascript">// Do something with the configuration data
// ... 

/&#42;&#42;
                                               
    ffffffffffffffff    iiii                   
   f::::::::::::::::f  i::::i                  
  f::::::::::::::::::f  iiii                   
  f::::::fffffff:::::f                         
  f:::::f       ffffffiiiiiiinnnn  nnnnnnnn    
  f:::::f             i:::::in:::nn::::::::nn  
 f:::::::ffffff        i::::in::::::::::::::nn 
 f::::::::::::f        i::::inn:::::::::::::::n
 f::::::::::::f        i::::i  n:::::nnnn:::::n
 f:::::::ffffff        i::::i  n::::n    n::::n
  f:::::f              i::::i  n::::n    n::::n
  f:::::f              i::::i  n::::n    n::::n
 f:::::::f            i::::::i n::::n    n::::n
 f:::::::f            i::::::i n::::n    n::::n
 f:::::::f            i::::::i n::::n    n::::n
 fffffffff            iiiiiiii nnnnnn    nnnnnn

&#42;/</code></pre>
 
Tadaaaaa! We have created a public custom post type that retrieves configuration data from a private custom post type, and both CPTs are powered by blocks. Success! 🙏

## Wrapping Up

If we want to configure our plugins using blocks, since the recently-released *Full Site Editing* feature cannot yet be used to create settings pages, we must then implement a custom solution.
 
In this article, I described one solution, based on creating a private custom post type to store the configuration data, and using the WordPress editor as the interface to fill this data.
 
As a result, we can provide a compelling experience for our users, thanks to the editor’s WYSIWYG, and the ability of blocks to provide controls that suit the type of content that must be provided, such as calendars, sliders, maps, or any other format.

### Further Resources

- “[WordPress 5.9 “Josephine”](https://wordpress.org/news/2022/01/josephine/)”, Matt Mullenweg
- [Introducing WordPress 5.9](https://www.youtube.com/watch?v=XvEG9XWD4JI), YouTube video by WordPress
- “[What’s New in WordPress 5.9](https://kinsta.com/blog/wordpress-5-9/)”, Carlo Daniele
- [Block Editor Handbook](https://developer.wordpress.org/block-editor/), wordpress.org
- “[The (Upcoming) WordPress Renaissance](https://www.smashingmagazine.com/2019/08/upcoming-wordpress-renaissance/)”, Leonardo Losoviz
- “[Implications Of Thinking In Blocks Instead Of Blobs](https://www.smashingmagazine.com/2018/11/implications-blocks-blobs/)”, Leonardo Losoviz

{{< signature "vf, yk, il" >}}
