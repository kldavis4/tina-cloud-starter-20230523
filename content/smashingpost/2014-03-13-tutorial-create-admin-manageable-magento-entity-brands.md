---
title: How To Create An Admin-Manageable Magento Entity For Brands
slug: tutorial-create-admin-manageable-magento-entity-brands
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b823902c-8c67-4d36-beb6-0570a97b0ccd/illu-magento.jpg'
date: 2014-03-13T10:34:25.000Z
author: joseph-mcdermott
description: >-
  In this tutorial, we will create a new “brand” entity in Magento that can be
  managed through the admin panel. Once we are finished, you will be able to
  create, update and delete brands that can be viewed in the front-end
  independently, much in the same way that you can interact with existing
  entities such as “products” and “categories.”
categories:
  - Coding
  - Frameworks
  - PHP
  - Tutorials
  - Magento
---
In this tutorial, we will create a new “brand” entity in Magento that can be managed through the admin panel. Once we are finished, you will be able to create, update and delete brands that can be viewed in the front-end independently, much in the same way that you can interact with existing entities such as “products” and “categories.”

In addition, we will associate our new brand entity with other Magento entities, such as products. The process itself is quite lengthy because I will explain each step in detail, but it really is easy once you know how, and it’s a great example of how powerful the Magento platform can be with minimal effort.

We will cover the following topics:

*   Create a new brand entity in Magento.
*   Browse, filter and sort brands in Magento’s admin panel.
*   Create, update and delete brands in the admin panel.
*   Create a brand list, and view pages in the front-end.
*   Associate brands with products.
*   Display a product-brand association in the front-end.
*   Include images throughout.

This tutorial refers to the Magento Community Edition 1.8.0.0, the latest version available at the time of writing. But the code and principles apply to all recent Magento versions, both Community and Enterprise.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75057439-768f-4cc6-adfd-288513bc6319/1-admin-grid.png" alt="Magento Brand Admin Grid" width="500" />

While I have tried to be as thorough as possible in my explanations, <strong>documenting the code is sometimes the best way to explain certain things</strong>, so you will find a lot of comments in the code snippets. The code snippet linked to at the end contains more usages and items than are covered in this tutorial, to show you how to extend the things that you will learn about here.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">How To Create An Affiliate Tracking Module In Magento</span>](https://www.smashingmagazine.com/2013/02/creating-an-affiliate-tracking-module-in-magento/)
*   [The Basics Of Creating A Magento Module](https://www.smashingmagazine.com/2012/03/basics-creating-magento-module/)
*   [How To Create Custom Shipping Methods In Magento](https://www.smashingmagazine.com/2014/01/create-custom-shipping-methods-magento/)

## Creating Our Module

Start by creating the following folder and file structure. For the time being, all files will be empty. Normally, these files and folders would be created one at a time as needed, but for the sake of this tutorial, we will put everything in place up front.

As usual, I assume you already know the <a title="The Basics Of Creating A Magento Module" href="https://www.smashingmagazine.com/2012/03/01/basics-creating-magento-module/">basics of creating a Magento module</a> and are comfortable with this step, with no explanation required.

<pre><code class="language-markup">app
  - code
      - community
          - SmashingMagazine
              - BrandDirectory
                  - Block
                      - Adminhtml
                          - Brand
                              - Edit
                                  - Form.php
                              - Edit.php
                              - Grid.php
                          - Brand.php
                  - Helper
                      - Data.php
                  - Model
                      - Resource
                          - Brand
                              - Collection.php
                          - Brand.php
                      - Brand.php
                  - controllers
                      - Adminhtml
                          - BrandController.php
                  - etc
                      - adminhtml.xml
                      - config.xml
                  - sql
                      - smashingmagazine_branddirectory_setup
                          - install-0.0.1.php
  - etc
      - modules
          - SmashingMagazine_BrandDirectory.xml
</code></pre>

## Module Setup Scripts

For our module to be of any use, we need somewhere to store our data. Therefore, we need to write a module setup script to create a database table to hold information about our brand entity. Setup scripts are stored in two places within the module, <code>/sql</code> and <code>/data</code>. The former is for physical changes to your Magento instance, such as database schema updates, and the latter is for populating or removing entries from the existing schema.

In our case, we are adding a new table. So, edit the file at <code>sql/smashingmagazine_branddirectory_setup/install-0.0.1.php</code> with the following code:

<pre><code class="language-php">&lt;?php
$this-&gt;startSetup();

/**
 * Note: there are many ways in Magento to achieve the same result of
 * creating a database table. For this tutorial, we have gone with the
 * Varien_Db_Ddl_Table method, but feel free to explore what Magento
 * does in CE 1.8.0.0 and earlier versions.
 */
$table = new Varien_Db_Ddl_Table();

/**
 * This is an alias of the real name of our database table, which is
 * configured in config.xml. By using an alias, we can refer to the same
 * table throughout our code if we wish, and if the table name ever has
 * to change, we can simply update a single location, config.xml
 * - smashingmagazine_branddirectory is the model alias
 * - brand is the table reference
 */
$table-&gt;setName($this-&gt;getTable('smashingmagazine_branddirectory/brand'));

/**
 * Add the columns we need for now. If you need more later, you can
 * always create a new setup script as an upgrade. We will introduce
 * that later in this tutorial.
 */
$table-&gt;addColumn(
    'entity_id',
    Varien_Db_Ddl_Table::TYPE_INTEGER,
    10,
    array(
        'auto_increment' =&gt; true,
        'unsigned' =&gt; true,
        'nullable'=&gt; false,
        'primary' =&gt; true
    )
);
$table-&gt;addColumn(
    'created_at',
    Varien_Db_Ddl_Table::TYPE_DATETIME,
    null,
    array(
        'nullable' =&gt; false,
    )
);
$table-&gt;addColumn(
    'updated_at',
    Varien_Db_Ddl_Table::TYPE_DATETIME,
    null,
    array(
        'nullable' =&gt; false,
    )
);
$table-&gt;addColumn(
    'name',
    Varien_Db_Ddl_Table::TYPE_VARCHAR,
    255,
    array(
        'nullable' =&gt; false,
    )
);
$table-&gt;addColumn(
    'url_key',
    Varien_Db_Ddl_Table::TYPE_VARCHAR,
    255,
    array(
        'nullable' =&gt; false,
    )
);
$table-&gt;addColumn(
    'description',
    Varien_Db_Ddl_Table::TYPE_TEXT,
    null,
    array(
        'nullable' =&gt; false,
    )
);
$table-&gt;addColumn(
    'visibility',
    Varien_Db_Ddl_Table::TYPE_BOOLEAN,
    null,
    array(
        'nullable' =&gt; false,
    )
);

/**
 * These two important lines are often missed.
 */
$table-&gt;setOption('type', 'InnoDB');
$table-&gt;setOption('charset', 'utf8');

/**
 * Create the table!
 */
$this-&gt;getConnection()-&gt;createTable($table);

$this-&gt;endSetup();</code></pre>

## Initializing Our Module

At this point, we still do not have an active Magento module; we just have a number of folders and empty files and an installation setup script that does not do anything yet. This is on purpose. In the next steps, we will populate the <code>app/etc/modules</code> XML file and configure <code>config.xml</code> so that Magento knows where to look for our setup script, after which the next visit to the website will trigger the content of our setup script to run.

If we had performed these tasks the other way round (that is, configured the module first and then populated the setup script), then there is a chance Magento would think that our module was on version 0.0.1 and that our setup script was still empty and, as a result, that the script would effectively have to be skipped. So, to limit face-palm moments for you guys, I’ve tried to keep the order of steps as safe as possible.</p>

### Configuring Our Module

Edit the file at <code>app/etc/modules/SmashingMagazine_BrandDirectory.xml</code>, and add the following to enable our module:

<pre><code class="language-markup">&lt;?xml version="1.0"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_BrandDirectory&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;codePool&gt;community&lt;/codePool&gt;
        &lt;/SmashingMagazine_BrandDirectory&gt;
    &lt;/modules&gt;
&lt;/config&gt;</code></pre>

You will notice we are using the community codepool. This BrandDirectory module will not contain any client-specific code or customizations. Instead, it will contain the building blocks for our new entity, which can be used in other modules, depending on the use case. Therefore, this community module may be dropped into any Magento instance and used as is, without any code needing to be changed. If code changes were required for each use, then this would be more suitable to the local code pool.

Now, we tell Magento that we have a module with a version number, which in fact will determine which setup scripts are run and where to find the setup scripts. Edit <code>etc/config.xml</code> with the following:

<pre><code class="language-markup">&lt;?xml version="1.0"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_BrandDirectory&gt;
            &lt;!--
            This is the version number that our module is currently at. In
            order for setup scripts to run, their version number must be less
            than or equal to this value.

            As we add upgrade scripts, we increment this value. The next time
            your Magento instance is accessed, Magento will compare values in
            the DB table 'core_resource' against this value. If the DB is
            lower, it will attempt to run any setup scripts for the module
            and then update the database table to match this value.
            --&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_BrandDirectory&gt;
    &lt;/modules&gt;
    &lt;global&gt;
        &lt;models&gt;

            &lt;!--
            This is the Model alias referred to in install-0.0.1.php.
            --&gt;
            &lt;smashingmagazine_branddirectory&gt;

                &lt;!--
                This tells Magento where to find
                resource materials for this module.
                --&gt;
      &lt;resourceModel&gt;smashingmagazine_branddirectory_resource&lt;/resourceModel&gt;

            &lt;/smashingmagazine_branddirectory&gt;

            &lt;!--
            This alias must match the above &lt;resourceModel/&gt; value.
            --&gt;
            &lt;smashingmagazine_branddirectory_resource&gt;

                &lt;entities&gt;

                    &lt;!--
                    This is the table alias referred to in install-0.0.1.php.
                    --&gt;
                    &lt;brand&gt;

                        &lt;!--
                        This is the actual name of the database table.
                        --&gt;
                        &lt;table&gt;smashingmagazine_branddirectory_brand&lt;/table&gt;

                    &lt;/brand&gt;

                &lt;/entities&gt;

            &lt;/smashingmagazine_branddirectory_resource&gt;

        &lt;/models&gt;

        &lt;resources&gt;

            &lt;!--
            This must match our folder name in the module sql folder.
            --&gt;
            &lt;smashingmagazine_branddirectory_setup&gt;

                &lt;setup&gt;

                    &lt;!--
                    This defines which module the setup
                    scripts in this location belong to.
                    --&gt;
                    &lt;module&gt;SmashingMagazine_BrandDirectory&lt;/module&gt;

                    &lt;!--
                    In each setup script, this
                    value determines the class of $this.
                    --&gt;
                    &lt;class&gt;Mage_Core_Model_Resource_Setup&lt;/class&gt;

                &lt;/setup&gt;

                &lt;!--
                This is only relevant if you have
        multiple database connections.
                --&gt;
                &lt;connection&gt;
                    &lt;use&gt;core_setup&lt;/use&gt;
                &lt;/connection&gt;

            &lt;/smashingmagazine_branddirectory_setup&gt;

        &lt;/resources&gt;

    &lt;/global&gt;
&lt;/config&gt;</code></pre>

## Is Everything Working So Far?

Go ahead and access any page of your website — the home page will do. Magento will find that it has a new module at version 0.0.1, yet it has no record of this module in the <code>core_resource</code> database table. This missing entry will trigger Magento to look for an installation setup script and execute its contents.</p>

### If All Goes Well…

If all goes well, then it will seem like nothing has happened. The Magento page might take a few moments longer to load while the contents of our setup script is run (i.e. while the new database table is created), and then the page will continue to load as normal. You now have two tasks to perform to check that everything has gone as expected:

1.  Ensure that Magento knows about your module and that the module is enabled by going to `System → Configuration → Advanced → Advanced`.
2.  Access your database via either the terminal or something like PHPMyAdmin to see whether Magento has created a new table, `smashingmagazine_branddirectory_brand`.</p>

### If All Does Not Go Well…

If all does not go well, then it might also seem like nothing has happened, only this time nothing really has happened! The reason for this could be typos in <code>config.xml</code>, badly named folders or files (take care with case-sensitivity) or something else. Go through the previous steps and double-check that everything is as it should be.

On the other hand, you might see an error message — perhaps a “PHP Fatal Error” or a report page, depending on the severity of the error. Use your debugging skills to identify the problem and correct it, again double-checking all previous steps in this tutorial.</p>

### “It Went Wrong. How Do I Try Again?”

To try again from scratch, you can perform the following actions — not all may be required, depending on how far Magento got before things went wrong. You will need to access your database directly because this cannot be performed through Magento:

1.  In the `core_resource` table, delete the single row `smashingmagazine_branddirectory_setup`.
2.  Delete the `smashingmagazine_branddirectory_brand` table.</p>

## Creating Our Helper

We don’t actually need to define any custom functionality in a helper for this tutorial. But we will be adding menu items to the admin panel that use a helper for translation purposes, so we can simply create one in <code>Helper/Data.php</code> and forget about it.

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Helper_Data
    extends Mage_Core_Helper_Abstract
{

}</code></pre>

## Creating Our Models

Next, we need to create models and resource models so that we can persist brand data to the database upon creating and saving, display information about our brands in the Magento admin panel grids, and display our brands to the customer in the front-end.</p>

### Brand Model

We need to define a model to enable developers to interact with our brand entities. I won’t go into any more detail than that because people smarter than me have no doubt already explained what a model does, so feel free to search out some articles. For now, I will stick to getting our model to do the job we need in order to continue our tutorial. So, edit <code>Model/Brand.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Model_Brand
    extends Mage_Core_Model_Abstract
{
    const VISIBILITY_HIDDEN = '0';
    const VISIBILITY_DIRECTORY = '1';

    protected function _construct()
    {
        /**
         * This tells Magento where the related resource model can be found.
         *
         * For a resource model, Magento will use the standard model alias -
         * in this case 'smashingmagazine_branddirectory' - and look in
         * config.xml for a child node &lt;resourceModel/&gt;. This will be the
         * location that Magento will look for a model when
         * Mage::getResourceModel() is called - in our case,
         * SmashingMagazine_BrandDirectory_Model_Resource.
         */
        $this-&gt;_init('smashingmagazine_branddirectory/brand');
    }

    /**
     * This method is used in the grid and form for populating the dropdown.
     */
    public function getAvailableVisibilies()
    {
        return array(
            self::VISIBILITY_HIDDEN
                =&gt; Mage::helper('smashingmagazine_branddirectory')
                       -&gt;__('Hidden'),
            self::VISIBILITY_DIRECTORY
                =&gt; Mage::helper('smashingmagazine_branddirectory')
                       -&gt;__('Visible in Directory'),
        );
    }

    protected function _beforeSave()
    {
        parent::_beforeSave();

        /**
         * Perform some actions just before a brand is saved.
         */
        $this-&gt;_updateTimestamps();
        $this-&gt;_prepareUrlKey();

        return $this;
    }

    protected function _updateTimestamps()
    {
        $timestamp = now();

        /**
         * Set the last updated timestamp.
         */
        $this-&gt;setUpdatedAt($timestamp);

        /**
         * If we have a brand new object, set the created timestamp.
         */
        if ($this-&gt;isObjectNew()) {
            $this-&gt;setCreatedAt($timestamp);
        }

        return $this;
    }

    protected function _prepareUrlKey()
    {
        /**
         * In this method, you might consider ensuring
         * that the URL Key entered is unique and
         * contains only alphanumeric characters.
         */

        return $this;
    }
}</code></pre>

### Brand Resource Model

As in my introduction to the model above, I won’t go into any more detail than to say that the job of the resource model is to persist and retrieve data from the database. So edit <code>Model/Resource/Brand.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Model_Resource_Brand
    extends Mage_Core_Model_Resource_Db_Abstract
{
    protected function _construct()
    {
        /**
         * Tell Magento the database name and primary key field to persist
         * data to. Similar to the _construct() of our model, Magento finds
         * this data from config.xml by finding the &lt;resourceModel/&gt; node
         * and locating children of &lt;entities/&gt;.
         *
         * In this example:
         * - smashingmagazine_branddirectory is the model alias
         * - brand is the entity referenced in config.xml
         * - entity_id is the name of the primary key column
         *
         * As a result, Magento will write data to the table
         * 'smashingmagazine_branddirectory_brand' and any calls
         * to $model-&gt;getId() will retrieve the data from the
         * column named 'entity_id'.
         */
        $this-&gt;_init('smashingmagazine_branddirectory/brand', 'entity_id');
    }
}</code></pre>

### Brand Resource Collection

Finally, we need a resource collection to allow iteration through our brands for things like admin panel grids and front-end listing pages. Edit <code>Model/Resource/Brand/Collection.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Model_Resource_Brand_Collection
    extends Mage_Core_Model_Resource_Db_Collection_Abstract
{
    protected function _construct()
    {
        parent::_construct();

        /**
         * Tell Magento the model and resource model to use for
         * this collection. Because both aliases are the same,
         * we can omit the second paramater if we wish.
         */
        $this-&gt;_init(
            'smashingmagazine_branddirectory/brand',
            'smashingmagazine_branddirectory/brand'
        );
    }
}</code></pre>

## Creating Our Admin Blocks

Most of the grunt work is now done. A database is ready to be populated, and models and resource models are ready to populate them. We just need to create the interface to do so. We’ll start by creating and configuring admin blocks to display our brands as grids in the admin panel and allowing them to be created and updated.</p>

### Grid Container Block

The job of the grid container is to house the individual rows of brand entries to be displayed in Magento’s admin panel. The grid container is like a wrapper and includes the buttons in the top right (for example, “Add”). Edit <code>Block/Adminhtml/Brand.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Block_Adminhtml_Brand
    extends Mage_Adminhtml_Block_Widget_Grid_Container
{
    protected function _construct()
    {
        parent::_construct();

        /**
         * The $_blockGroup property tells Magento which alias to use to
         * locate the blocks to be displayed in this grid container.
         * In our example, this corresponds to BrandDirectory/Block/Adminhtml.
         */
        $this-&gt;_blockGroup = 'smashingmagazine_branddirectory_adminhtml';

        /**
         * $_controller is a slightly confusing name for this property.
         * This value, in fact, refers to the folder containing our
         * Grid.php and Edit.php - in our example,
         * BrandDirectory/Block/Adminhtml/Brand. So, we'll use 'brand'.
         */
        $this-&gt;_controller = 'brand';

        /**
         * The title of the page in the admin panel.
         */
        $this-&gt;_headerText = Mage::helper('smashingmagazine_branddirectory')
            -&gt;__('Brand Directory');
    }

    public function getCreateUrl()
    {
        /**
         * When the "Add" button is clicked, this is where the user should
         * be redirected to - in our example, the method editAction of
         * BrandController.php in BrandDirectory module.
         */
        return $this-&gt;getUrl(
            'smashingmagazine_branddirectory_admin/brand/edit'
        );
    }
}</code></pre>

### Grid Block

When rendering the grid, Magento will expect to find a grid block in the <code>_controller</code> location defined in the grid container above, so we will create this now. Here, we can define which fields to retrieve from the database and show in the admin panel grid, and Magento will automatically allow these columns to be searched and filtered. Edit <code>Block/Adminhtml/Brand/Grid.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Block_Adminhtml_Brand_Grid
    extends Mage_Adminhtml_Block_Widget_Grid
{
    protected function _prepareCollection()
    {
        /**
         * Tell Magento which collection to use to display in the grid.
         */
        $collection = Mage::getResourceModel(
            'smashingmagazine_branddirectory/brand_collection'
        );
        $this-&gt;setCollection($collection);

        return parent::_prepareCollection();
    }

    public function getRowUrl($row)
    {
        /**
         * When a grid row is clicked, this is where the user should
         * be redirected to - in our example, the method editAction of
         * BrandController.php in BrandDirectory module.
         */
        return $this-&gt;getUrl(
            'smashingmagazine_branddirectory_admin/brand/edit',
            array(
                'id' =&gt; $row-&gt;getId()
            )
        );
    }

    protected function _prepareColumns()
    {
        /**
         * Here, we'll define which columns to display in the grid.
         */
        $this-&gt;addColumn('entity_id', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('ID'),
            'type' =&gt; 'number',
            'index' =&gt; 'entity_id',
        ));

        $this-&gt;addColumn('created_at', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('Created'),
            'type' =&gt; 'datetime',
            'index' =&gt; 'created_at',
        ));

        $this-&gt;addColumn('updated_at', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('Updated'),
            'type' =&gt; 'datetime',
            'index' =&gt; 'updated_at',
        ));

        $this-&gt;addColumn('name', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('Name'),
            'type' =&gt; 'text',
            'index' =&gt; 'name',
        ));

        $this-&gt;addColumn('lastname', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('Url Key'),
            'type' =&gt; 'text',
            'index' =&gt; 'url_key',
        ));

        $brandSingleton = Mage::getSingleton(
            'smashingmagazine_branddirectory/brand'
        );
        $this-&gt;addColumn('visibility', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('Visibility'),
            'type' =&gt; 'options',
            'index' =&gt; 'visibility',
            'options' =&gt; $brandSingleton-&gt;getAvailableVisibilies()
        ));

        /**
         * Finally, we'll add an action column with an edit link.
         */
        $this-&gt;addColumn('action', array(
            'header' =&gt; $this-&gt;_getHelper()-&gt;__('Action'),
            'width' =&gt; '50px',
            'type' =&gt; 'action',
            'actions' =&gt; array(
                array(
                    'caption' =&gt; $this-&gt;_getHelper()-&gt;__('Edit'),
                    'url' =&gt; array(
                        'base' =&gt; 'smashingmagazine_branddirectory_admin'
                                  . '/brand/edit',
                    ),
                    'field' =&gt; 'id'
                ),
            ),
            'filter' =&gt; false,
            'sortable' =&gt; false,
            'index' =&gt; 'entity_id',
        ));

        return parent::_prepareColumns();
    }

    protected function _getHelper()
    {
        return Mage::helper('smashingmagazine_branddirectory');
    }
}</code></pre>

### Form Container Block

The form container block has a function similar to that of the grid container but is used to create or edit an entity. Edit <code>Block/Adminhtml/Brand/Edit.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Block_Adminhtml_Brand_Edit
    extends Mage_Adminhtml_Block_Widget_Form_Container
{
    protected function _construct()
    {
        $this-&gt;_blockGroup = 'smashingmagazine_branddirectory_adminhtml';
        $this-&gt;_controller = 'brand';

        /**
         * The $_mode property tells Magento which folder to use
         * to locate the related form blocks to be displayed in
         * this form container. In our example, this corresponds
         * to BrandDirectory/Block/Adminhtml/Brand/Edit/.
         */
        $this-&gt;_mode = 'edit';

        $newOrEdit = $this-&gt;getRequest()-&gt;getParam('id')
            ? $this-&gt;__('Edit')
            : $this-&gt;__('New');
        $this-&gt;_headerText =  $newOrEdit . ' ' . $this-&gt;__('Brand');
    }
}</code></pre>

### Form Block

In the form block, we define which fields may be managed when creating or editing an entity. Edit <code>Block/Adminhtml/Brand/Edit/Form.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Block_Adminhtml_Brand_Edit_Form
    extends Mage_Adminhtml_Block_Widget_Form
{
    protected function _prepareForm()
    {
        // Instantiate a new form to display our brand for editing.
        $form = new Varien_Data_Form(array(
            'id' =&gt; 'edit_form',
            'action' =&gt; $this-&gt;getUrl(
                'smashingmagazine_branddirectory_admin/brand/edit',
                array(
                    '_current' =&gt; true,
                    'continue' =&gt; 0,
                )
            ),
            'method' =&gt; 'post',
        ));
        $form-&gt;setUseContainer(true);
        $this-&gt;setForm($form);

        // Define a new fieldset. We need only one for our simple entity.
        $fieldset = $form-&gt;addFieldset(
            'general',
            array(
                'legend' =&gt; $this-&gt;__('Brand Details')
            )
        );

        $brandSingleton = Mage::getSingleton(
            'smashingmagazine_branddirectory/brand'
        );

        // Add the fields that we want to be editable.
        $this-&gt;_addFieldsToFieldset($fieldset, array(
            'name' =&gt; array(
                'label' =&gt; $this-&gt;__('Name'),
                'input' =&gt; 'text',
                'required' =&gt; true,
            ),
            'url_key' =&gt; array(
                'label' =&gt; $this-&gt;__('URL Key'),
                'input' =&gt; 'text',
                'required' =&gt; true,
            ),
            'description' =&gt; array(
                'label' =&gt; $this-&gt;__('Description'),
                'input' =&gt; 'textarea',
                'required' =&gt; true,
            ),
            'visibility' =&gt; array(
                'label' =&gt; $this-&gt;__('Visibility'),
                'input' =&gt; 'select',
                'required' =&gt; true,
                'options' =&gt; $brandSingleton-&gt;getAvailableVisibilies(),
            ),

            /**
             * Note: we have not included created_at or updated_at.
             * We will handle those fields ourself in the model
       * before saving.
             */
        ));

        return $this;
    }

    /**
     * This method makes life a little easier for us by pre-populating
     * fields with $_POST data where applicable and wrapping our post data
     * in 'brandData' so that we can easily separate all relevant information
     * in the controller. You could of course omit this method entirely
     * and call the $fieldset-&gt;addField() method directly.
     */
    protected function _addFieldsToFieldset(
        Varien_Data_Form_Element_Fieldset $fieldset, $fields)
    {
        $requestData = new Varien_Object($this-&gt;getRequest()
            -&gt;getPost('brandData'));

        foreach ($fields as $name =&gt; $_data) {
            if ($requestValue = $requestData-&gt;getData($name)) {
                $_data['value'] = $requestValue;
            }

            // Wrap all fields with brandData group.
            $_data['name'] = "brandData[$name]";

            // Generally, label and title are always the same.
            $_data['title'] = $_data['label'];

            // If no new value exists, use the existing brand data.
            if (!array_key_exists('value', $_data)) {
                $_data['value'] = $this-&gt;_getBrand()-&gt;getData($name);
            }

            // Finally, call vanilla functionality to add field.
            $fieldset-&gt;addField($name, $_data['input'], $_data);
        }

        return $this;
    }

    /**
     * Retrieve the existing brand for pre-populating the form fields.
     * For a new brand entry, this will return an empty brand object.
     */
    protected function _getBrand()
    {
        if (!$this-&gt;hasData('brand')) {
            // This will have been set in the controller.
            $brand = Mage::registry('current_brand');

            // Just in case the controller does not register the brand.
            if (!$brand instanceof
                    SmashingMagazine_BrandDirectory_Model_Brand) {
                $brand = Mage::getModel(
                    'smashingmagazine_branddirectory/brand'
                );
            }

            $this-&gt;setData('brand', $brand);
        }

        return $this-&gt;getData('brand');
    }
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4af04d9a-7814-4094-bdbf-5dafcae98811/2-admin-form.png" alt="Magento Brand Admin Form" width="500" height="" />

## Creating Our Admin Controller

Now, we need a controller to accept requests and render the container blocks from above. The controller will also handle <code>POST</code> requests to create, update and delete brands as required. Edit <code>controllers/Adminhtml/BrandController.php</code> with this:

<pre><code class="language-php">&lt;?php
class SmashingMagazine_BrandDirectory_Adminhtml_BrandController
    extends Mage_Adminhtml_Controller_Action
{
    /**
     * Instantiate our grid container block and add to the page content.
     * When accessing this admin index page, we will see a grid of all
     * brands currently available in our Magento instance, along with
     * a button to add a new one if we wish.
     */
    public function indexAction()
    {
        // instantiate the grid container
        $brandBlock = $this-&gt;getLayout()
            -&gt;createBlock('smashingmagazine_branddirectory_adminhtml/brand');

        // Add the grid container as the only item on this page
        $this-&gt;loadLayout()
            -&gt;_addContent($brandBlock)
            -&gt;renderLayout();
    }

    /**
     * This action handles both viewing and editing existing brands.
     */
    public function editAction()
    {
        /**
         * Retrieve existing brand data if an ID was specified.
         * If not, we will have an empty brand entity ready to be populated.
         */
        $brand = Mage::getModel('smashingmagazine_branddirectory/brand');
        if ($brandId = $this-&gt;getRequest()-&gt;getParam('id', false)) {
            $brand-&gt;load($brandId);

            if ($brand-&gt;getId() _getSession()-&gt;addError(
                    $this-&gt;__('This brand no longer exists.')
                );
                return $this-&gt;_redirect(
                    'smashingmagazine_branddirectory_admin/brand/index'
                );
            }
        }

        // process $_POST data if the form was submitted
        if ($postData = $this-&gt;getRequest()-&gt;getPost('brandData')) {
            try {
                $brand-&gt;addData($postData);
                $brand-&gt;save();

                $this-&gt;_getSession()-&gt;addSuccess(
                    $this-&gt;__('The brand has been saved.')
                );

                // redirect to remove $_POST data from the request
                return $this-&gt;_redirect(
                    'smashingmagazine_branddirectory_admin/brand/edit',
                    array('id' =&gt; $brand-&gt;getId())
                );
            } catch (Exception $e) {
                Mage::logException($e);
                $this-&gt;_getSession()-&gt;addError($e-&gt;getMessage());
            }

            /**
             * If we get to here, then something went wrong. Continue to
             * render the page as before, the difference this time being
             * that the submitted $_POST data is available.
             */
        }

        // Make the current brand object available to blocks.
        Mage::register('current_brand', $brand);

        // Instantiate the form container.
        $brandEditBlock = $this-&gt;getLayout()-&gt;createBlock(
            'smashingmagazine_branddirectory_adminhtml/brand_edit'
        );

        // Add the form container as the only item on this page.
        $this-&gt;loadLayout()
            -&gt;_addContent($brandEditBlock)
            -&gt;renderLayout();
    }

    public function deleteAction()
    {
        $brand = Mage::getModel('smashingmagazine_branddirectory/brand');

        if ($brandId = $this-&gt;getRequest()-&gt;getParam('id', false)) {
            $brand-&gt;load($brandId);
        }

        if ($brand-&gt;getId() _getSession()-&gt;addError(
                $this-&gt;__('This brand no longer exists.')
            );
            return $this-&gt;_redirect(
                'smashingmagazine_branddirectory_admin/brand/index'
            );
        }

        try {
            $brand-&gt;delete();

            $this-&gt;_getSession()-&gt;addSuccess(
                $this-&gt;__('The brand has been deleted.')
            );
        } catch (Exception $e) {
            Mage::logException($e);
            $this-&gt;_getSession()-&gt;addError($e-&gt;getMessage());
        }

        return $this-&gt;_redirect(
            'smashingmagazine_branddirectory_admin/brand/index'
        );
    }

    /**
     * Thanks to Ben for pointing out this method was missing. Without
     * this method the ACL rules configured in adminhtml.xml are ignored.
     */
    protected function _isAllowed()
    {
        /**
         * we include this switch to demonstrate that you can add action
         * level restrictions in your ACL rules. The isAllowed() method will
         * use the ACL rule we have configured in our adminhtml.xml file:
         * - acl
         * - - resources
         * - - - admin
         * - - - - children
         * - - - - - smashingmagazine_branddirectory
         * - - - - - - children
         * - - - - - - - brand
         *
         * eg. you could add more rules inside brand for edit and delete.
         */
        $actionName = $this-&gt;getRequest()-&gt;getActionName();
        switch ($actionName) {
            case 'index':
            case 'edit':
            case 'delete':
                // intentionally no break
            default:
                $adminSession = Mage::getSingleton('admin/session');
                $isAllowed = $adminSession
                    -&gt;isAllowed('smashingmagazine_branddirectory/brand');
                break;
        }

        return $isAllowed;
    }
}</code></pre>

## Completing The Configuration

That’s all the code we need for the back end. We just need to make a few changes to <code>config.xml</code> to tell Magento where to find our controller, blocks, models and helper. We also have to add a menu item to the admin panel for easy access to manage our brand entity.</p>

### config.xml

We need to add block, helper and model definitions to our module configuration so that Magento knows where to locate these files, as well as an admin router so that Magento knows where to locate our controller for the menu items that we are about to add in the next step. The final version of our <code>etc/config.xml</code> file will look as follows:

<pre><code class="language-markup">&lt;?xml version="1.0"?&gt;
&lt;config&gt;
    &lt;modules&gt;
        &lt;SmashingMagazine_BrandDirectory&gt;
            &lt;!--
            This is the version number that our module is currently at.
            In order for setup scripts to run, their version number must
            be less than or equal to this value.

            As we add upgrade scripts, we increment this value. The next time
            your Magento instance is accessed, Magento will compare values in
            the database table 'core_resource' against this value. If the
            database is lower, it will attempt to run any setup scripts for
            the module and then update the database table to match this value.
            --&gt;
            &lt;version&gt;0.0.1&lt;/version&gt;
        &lt;/SmashingMagazine_BrandDirectory&gt;
    &lt;/modules&gt;
    &lt;global&gt;

        &lt;!--
        add an adminhtml block definition
        --&gt;
        &lt;blocks&gt;
            &lt;smashingmagazine_branddirectory_adminhtml&gt;
               &lt;class&gt;SmashingMagazine_BrandDirectory_Block_Adminhtml&lt;/class&gt;
            &lt;/smashingmagazine_branddirectory_adminhtml&gt;
        &lt;/blocks&gt;

        &lt;!--
        Add a helper definition for use in adminhtml.xml menu translation.
        --&gt;
        &lt;helpers&gt;
            &lt;smashingmagazine_branddirectory&gt;
                &lt;class&gt;SmashingMagazine_BrandDirectory_Helper&lt;/class&gt;
            &lt;/smashingmagazine_branddirectory&gt;
        &lt;/helpers&gt;

        &lt;models&gt;

            &lt;!--
            This is the model alias referred to in install-0.0.1.php.
            --&gt;
            &lt;smashingmagazine_branddirectory&gt;
                &lt;!--
                This tells Magento where to find models for this module.
                --&gt;
                &lt;class&gt;SmashingMagazine_BrandDirectory_Model&lt;/class&gt;

                &lt;!--
                This tells Magento where to find resource
                materials for this module.
                --&gt;
      &lt;resourceModel&gt;smashingmagazine_branddirectory_resource&lt;/resourceModel&gt;

            &lt;/smashingmagazine_branddirectory&gt;

            &lt;!--
            This alias must match the &lt;resourceModel/&gt; value above.
            --&gt;
            &lt;smashingmagazine_branddirectory_resource&gt;
                &lt;!--
                This tells Magento where to find resource
                models for this module.
                --&gt;
                &lt;class&gt;SmashingMagazine_BrandDirectory_Model_Resource&lt;/class&gt;

                &lt;entities&gt;

                    &lt;!--
                    This is the table alias referred to in install-0.0.1.php.
                    --&gt;
                    &lt;brand&gt;

                        &lt;!--
                            This is the name of the database table itself.
                        --&gt;
                        &lt;table&gt;smashingmagazine_branddirectory_brand&lt;/table&gt;

                    &lt;/brand&gt;

                &lt;/entities&gt;

            &lt;/smashingmagazine_branddirectory_resource&gt;

        &lt;/models&gt;

        &lt;resources&gt;

            &lt;!--
            This must match our folder name in the module sql folder.
            --&gt;
            &lt;smashingmagazine_branddirectory_setup&gt;

                &lt;setup&gt;

                    &lt;!--
                    This defines which module the setup
                    scripts in this location belong to.
                    --&gt;
                    &lt;module&gt;SmashingMagazine_BrandDirectory&lt;/module&gt;

                    &lt;!--
                    In each setup script, this
                    value determines the class of $this.
                    --&gt;
                    &lt;class&gt;Mage_Core_Model_Resource_Setup&lt;/class&gt;

                &lt;/setup&gt;

                &lt;!--
                This is relevant only if you have multiple database connections.
                --&gt;
                &lt;connection&gt;
                    &lt;use&gt;core_setup&lt;/use&gt;
                &lt;/connection&gt;

            &lt;/smashingmagazine_branddirectory_setup&gt;

        &lt;/resources&gt;

    &lt;/global&gt;

    &lt;!-- Add a router for access to our admin panel controller. --&gt;
    &lt;admin&gt;
        &lt;routers&gt;

            &lt;!-- This is the alias for this router. --&gt;
            &lt;smashingmagazine_branddirectory_admin&gt;

                &lt;!--
                This basically informs Magento to use the
                admin scope for requests to this router.
                --&gt;
                &lt;use&gt;admin&lt;/use&gt;

                &lt;args&gt;
                    &lt;!--
                    This tells Magento where to find
                    adminhtml controllers for this module.
                    --&gt;
                   &lt;module&gt;SmashingMagazine_BrandDirectory_Adminhtml&lt;/module&gt;

                    &lt;!-- This is the term used in the actual URL. --&gt;
                    &lt;frontName&gt;brand-directory-admin&lt;/frontName&gt;
                &lt;/args&gt;

            &lt;/smashingmagazine_branddirectory_admin&gt;

        &lt;/routers&gt;
    &lt;/admin&gt;

&lt;/config&gt;</code></pre>

### adminhtml.xml

Adding menu items to Magento’s admin panel is straightforward. We simply have to create an <code>adminhtml.xml</code> file, define which items should appear and where they should lead to when clicked. Edit <code>etc/adminhtml.xml</code> with this:

<pre><code class="language-markup">&lt;?xml version="1.0"?&gt;
&lt;config&gt;
    &lt;!-- We are defining a new menu item for the admin panel. --&gt;
    &lt;menu&gt;

        &lt;!--
        First, create a top-level menu item, which will appear alongside CMS
        --&gt;
        &lt;smashingmagazine_branddirectory translate="title"
                module="smashingmagazine_branddirectory"&gt;
            &lt;title&gt;Brand Directory&lt;/title&gt;
            &lt;sort_order&gt;75&lt;/sort_order&gt;
            &lt;depends&gt;
                &lt;module&gt;SmashingMagazine_BrandDirectory&lt;/module&gt;
            &lt;/depends&gt;

            &lt;!-- Under this top-level menu, create a child menu item. --&gt;
            &lt;children&gt;
                &lt;brand translate="title"
                        module="smashingmagazine_branddirectory"&gt;
                    &lt;title&gt;Manage Brands&lt;/title&gt;
                    &lt;sort_order&gt;10&lt;/sort_order&gt;

                    &lt;!--
                    When the menu is clicked, take the user here.
                    --&gt;
                 &lt;action&gt;smashingmagazine_branddirectory_admin/brand&lt;/action&gt;

                &lt;/brand&gt;
            &lt;/children&gt;
        &lt;/smashingmagazine_branddirectory&gt;
    &lt;/menu&gt;

    &lt;!-- Define ACL for access to these menu items. --&gt;
    &lt;acl&gt;
        &lt;resources&gt;
            &lt;admin&gt;
                &lt;children&gt;
                    &lt;smashingmagazine_branddirectory translate="title"
                            module="smashingmagazine_branddirectory"&gt;
                        &lt;title&gt;Brand Directory&lt;/title&gt;
                        &lt;sort_order&gt;75&lt;/sort_order&gt;
                        &lt;children&gt;
                            &lt;brand translate="title"
                                    module="smashingmagazine_branddirectory"&gt;
                                &lt;title&gt;Manage Brands&lt;/title&gt;
                            &lt;/brand&gt;
                        &lt;/children&gt;
                    &lt;/smashingmagazine_branddirectory&gt;
                &lt;/children&gt;
            &lt;/admin&gt;
        &lt;/resources&gt;
    &lt;/acl&gt;
&lt;/config&gt;</code></pre>

## Displaying Brands In The Front-End

We have reached the end of this tutorial on how to create an entity that is manageable from the admin panel. By now, you should be able to create, update and delete brands and to have those changes reflected in the database. You have a fully functioning brand entity, but it doesn’t actually do anything. The next step is to integrate this new entity in the rest of your Magento code.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a74125ee-fcb4-4b83-a88a-2956a08affce/3-product-view.png" alt="Magento Brand Product View" width="500" height="" />

Rather than continue to ramble about how to do this, I have included in the attached source code an additional local module, named “BrandExample,” which contains examples of how to achieve this.

Upon inspecting the attachment, you will notice I have kept this supplemental front-end example as a separate local module, in order for it not to be confused with the admin panel management sections covered above. Once you are more familiar, then by all means, bundle both modules into one if you wish.

I won’t go into much detail with the example usages, but feel free to ask any questions in the comments section below.

<img loading="lazy" decoding="async" class="size-medium wp-image-130472" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9226b1a2-ff83-4117-96f9-b90cde7d5476/4-brand-list.png" alt="Magento Brand List" width="500" height="" />

<img loading="lazy" decoding="async" class="size-medium wp-image-130473" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9907e3cd-9768-4e7b-a08d-48d0234ff596/5-brand-view.png" alt="Magento Brand View" width="500" height="" />

Feel free to <a href="https://github.com/josephmcdermott/SmashingMagazine-MagentoBrandEntity">view or download the source code</a> (Github), which contains the following additional content:

*   the completed tutorial from above;
*   a new product attribute to associate products with brands;
*   inclusion of brands on the product view page, once associated;
*   a brands listing and brands landing page, including related products;
*   data setup scripts to create dummy products and brands.

{{< signature "al, il" >}}

