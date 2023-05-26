---
title: 'Get Started Developing For Android With Eclipse, Reloaded'
slug: get-started-developing-for-android-with-eclipse-reloaded
image: null
date: 2011-03-28T09:30:07.000Z
author: chris-blunt
description: >-
  To follow this tutorial, you’ll need the code from the previous article. If
  you want to get started right away, grab the code from
  [GitHub](https://github.com/cblunt/BrewClock) and check out the
  _tutorial_part_1_ tag.
categories:
  - Coding
  - Eclipse
  - Android
---
In the <a href="https://www.smashingmagazine.com/2010/10/25/get-started-developing-for-android-with-eclipse/">first part</a> of this tutorial series, we built a simple brew timer application using Android and Eclipse. In this second part, we’ll continue developing the application by adding extra functionality. In doing this, you’ll be introduced to some important and powerful features of the Android SDK, including Persistent data storage, Activities and Intent as well as Shared user preferences.

To follow this tutorial, you’ll need the code from the previous article. If you want to get started right away, grab the code from <a href="https://github.com/cblunt/BrewClock">GitHub</a> and check out the <em>tutorial_part_1</em> tag using this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2870f59e-1e3b-45dd-9f8e-38cc166a0dd4/1-starting-point-full.jpg"><img class="aligncenter size-full wp-image-90587" title="1_starting_point" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5165043b-0126-49de-87b0-3d878bf3a736/1-starting-point.jpg" alt="" width="500" height="356" /></a>

<pre><code class="language-markup tmp-python">$ git clone git://github.com/cblunt/BrewClock.git
$ cd BrewClock
$ git checkout tutorial_part_1</code></pre>

Once you’ve checked out the code on GitHub, you’ll need to import the project into Eclipse:

{{% feature-panel %}}

1.  Launch Eclipse and choose _File → Import…_
2.  In the Import window, select “Existing Projects into Workspace” and click “Next.”
3.  On the next screen, click “Browse,” and select the project folder that you cloned from GitHub.
4.  Click “Finish” to import your project into Eclipse.

After importing the project into Eclipse, you might receive a warning message:

<pre><code class="language-markup tmp-python">Android required .class compatibility set to 5.0.
Please fix project properties.</code></pre>

If this is the case, right-click on the newly imported “BrewClock” project in the “Project Explorer,” choose “Fix Project Properties,” and then restart Eclipse.</p>

## Getting Started With Data Storage

Currently, BrewClock lets users set a specific time for brewing their favorite cups of tea. This is great, but what if they regularly drink a variety of teas, each with their own different brewing times? At the moment, users have to remember brewing times for all their favorite teas! This doesn’t make for a great user experience. So, in this tutorial we’ll develop functionality to let users store brewing times for their favorite teas and then choose from that list of teas when they make a brew.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Get Started Developing For Android With Eclipse](https://www.smashingmagazine.com/2010/10/get-started-developing-for-android-with-eclipse/)
*   [Getting The Best Out Of Eclipse For Android Development](https://www.smashingmagazine.com/2011/11/getting-the-best-out-of-eclipse-for-android-development/)
*   [Guidelines For Mobile Web Development](https://www.smashingmagazine.com/guidelines-for-mobile-web-development/)

To do this, we’ll take advantage of Android’s rich data-storage API. Android offers several ways to store data, two of which we’ll cover in this article. The first, more powerful option, uses the SQLite database engine to store data for our application.

SQLite is a popular and lightweight SQL database engine that saves data in a single file. It is often used in desktop and embedded applications, where running a client-server SQL engine (such as MySQL or PostgreSQL) isn’t feasible.

Every application installed on an Android device can save and use any number of SQLite database files (subject to storage capacity), which the system will manage automatically. An application’s databases are private and so cannot be accessed by any other applications. (Data can be shared through the <code>ContentProvider</code> class, but we won’t cover content providers in this tutorial.) Database files persist when the application is upgraded and are deleted when the application is uninstalled.

We’ll use a simple SQLite database in BrewClock to maintain a list of teas and their appropriate brewing times. Here’s an overview of how our database schema will look:

<pre><code class="language-markup tmp-python">+-------------------------------------+
| Table: teas                         |
+------------+------------------------+
| Column     | Description            |
+------------+------------------------+
| _ID        | integer, autoincrement |
| name       | text, not null         |
| brew_time  | integer, not null      |
+------------+------------------------+</code></pre>

If you’ve worked with SQL before, this should look fairly familiar. The database table has three columns: a unique identifier (<code>_ID</code>), name and brewing time. We’ll use the APIs provided by Android to create the database table in our code. The system will take care of creating the database file in the right location for our application.</p>

### Abstracting the Database

To ensure the database code is easy to maintain, we’ll abstract all the code for handling database creation, inserts and queries into a separate class, <code>TeaData</code>. This should be fairly familiar if you’re used to the model-view-controller approach. All the database code is kept in a separate class from our <code>BrewClockActivity</code>. The Activity can then just instantiate a new <code>TeaData</code> instance (which will connect to the database) and do what it needs to do. Working in this way enables us to easily change the database in one place without having to change anything in any other parts of our application that deal with the database.

Create a new class called <code>TeaData</code> in the BrewClock project by going to File → New → Class. Ensure that <code>TeaData</code> extends the <code>android.database.sqlite.SQLiteOpenHelper</code> class and that you check the box for “Constructors from superclass.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d90fbe40-bbdb-4db7-9410-bf32fe2abd6d/2-create-teadata-class1.jpg"><img class="aligncenter size-full wp-image-94000" title="2_create_teadata_class" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d90fbe40-bbdb-4db7-9410-bf32fe2abd6d/2-create-teadata-class1.jpg" alt="" width="500" height="583" /></a>

The <code>TeaData</code> class will automatically handle the creation and versioning of a SQLite database for your application. We’ll also add methods to give other parts of our code an interface to the database.

Add two constants to <code>TeaData</code> to store the name and version of the database, the table’s name and the names of columns in that table. We’ll use the Android-provided constant <code>BaseColumns._ID</code> for the table’s unique id column:

<pre><code class="language-javascript">// src/com/example/brewclock/TeaData.java
import android.app.Activity;
import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.DatabaseUtils;
import android.provider.BaseColumns;

public class TeaData extends SQLiteOpenHelper {
  private static final String DATABASE_NAME = "teas.db";
  private static final int DATABASE_VERSION = 1;

  public static final String TABLE_NAME = "teas";

  public static final String _ID = BaseColumns._ID;
  public static final String NAME = "name";
  public static final String BREW_TIME = "brew_time";

  // …
}</code></pre>

Add a constructor to <code>TeaData</code> that calls its parent method, supplying our database name and version. Android will automatically handle opening the database (and creating it if it does not exist).

<pre><code class="language-javascript">// src/com/example/brewclock/TeaData.java
public TeaData(Context context) {
  super(context, DATABASE_NAME, null, DATABASE_VERSION);
}</code></pre>

We’ll need to override the <code>onCreate</code> method to execute a string of SQL commands that create the database table for our tea. Android will handle this method for us, calling <code>onCreate</code> when the database file is first created.

On subsequent launches, Android checks the version of the database against the <code>DATABASE_VERSION</code> number we supplied to the constructor. If the version has changed, Android will call the <code>onUpgrade</code> method, which is where you would write any code to modify the database structure. In this tutorial, we’ll just ask Android to drop and recreate the database.

So, add the following code to <code>onCreate</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/TeaData.java
@Override
public void onCreate(SQLiteDatabase db) {
  // CREATE TABLE teas (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT NOT NULL, brew_time INTEGER);
  String sql =
    "CREATE TABLE " + TABLE_NAME + " ("
      + _ID + " INTEGER PRIMARY KEY AUTOINCREMENT, "
      + NAME + " TEXT NOT NULL, "
      + BREW_TIME + " INTEGER"
      + ");";

  db.execSQL(sql);
}

@Override
public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
  db.execSQL("DROP TABLE IF EXISTS " + TABLE_NAME);
  onCreate(db);
}</code></pre>

Next, we’ll add a new method to <code>TeaData</code> that lets us easily add new tea records to the database. We’ll supply the method with a name and brewing time for the tea to be added. Rather than forcing us to write out the raw SQL to do this, Android supplies a set of classes for inserting records into the database. First, we create a set of <code>ContentValues</code>, pushing the relevant values into that set.

With an instance of <code>ContentValues</code>, we simply supply the column name and the value to insert. Android takes care of creating and running the appropriate SQL. Using Android’s database classes ensures that the writes are safe, and if the data storage mechanism changes in a future Android release, our code will still work.

Add a new method, <code>insert()</code>, to the <code>TeaData</code> class:

<pre><code class="language-javascript">// src/com/example/brewclock/TeaData.java
public void insert(String name, int brewTime) {
  SQLiteDatabase db = getWritableDatabase();

  ContentValues values = new ContentValues();
  values.put(NAME, name);
  values.put(BREW_TIME, brewTime);

  db.insertOrThrow(TABLE_NAME, null, values);
}</code></pre>

### Retrieving Data

With the ability to save data into the database, we’ll also need a way to get it back out. Android provides the <code>Cursor</code> interface for doing just this. A <code>Cursor</code> represents the results of running a SQL query against the database, and it maintains a pointer to one row within that result set. This pointer can be moved forwards and backwards through the results, returning the values from each column. It can help to visualize this:

<pre><code class="language-markup tmp-python">SQL Query: SELECT * from teas LIMIT 3;

+-----------------------------------+
|  _ID  |  name       |  brew_time  |
+-----------------------------------+
|    1  |  Earl Grey  |          3  |
|    2  |  Green      |          1  | &lt;= Cursor
|    3  |  Assam      |          5  |
+-------+-------------+-------------+</code></pre>

In this example, the Cursor is pointing at the second row in the result set (Green tea). We could move the Cursor back a row to represent the first row (Earl Grey) by calling <code>cursor.moveToPrevious()</code>, or move forward to the Assam row with <code>moveToNext()</code>. To fetch the name of the tea that the Cursor is pointing out, we would call <code>cursor.getString(1)</code>, where <code>1</code> is the column index of the column we wish to retrieve (note that the index is zero-based, so column 0 is the first column, 1 the second column and so on).

Now that you know about Cursors, add a method that creates a <code>Cursor</code> object that returns all the teas in our database. Add an <code>all</code> method to <code>TeaData</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/TeaData.java
public Cursor all(Activity activity) {
  String[] from = { _ID, NAME, BREW_TIME };
  String order = NAME;

  SQLiteDatabase db = getReadableDatabase();
  Cursor cursor = db.query(TABLE_NAME, from, null, null, null, null, order);
  activity.startManagingCursor(cursor);

  return cursor;
}</code></pre>

Let’s go over this method in detail, because it looks a little strange at first. Again, rather than writing raw SQL to query the database, we make use of Android’s database interface methods.

First, we need to tell Android which columns from our database we’re interested in. To do this, we create an array of strings—each one of the column identifiers that we defined at the top of <code>TeaData</code>. We’ll also set the column that we want to order the results by and store it in the <code>order</code> string.

Next, we create a read-only connection to the database using <code>getReadableDatabase()</code>, and with that connection, we tell Android to run a query using the <code>query()</code> method. The <code>query()</code> method takes a set of parameters that Android internally converts into a SQL query. Again, Android’s abstraction layer ensures that our application code will likely continue to work, even if the underlying data storage changes in a future version of Android.

Because we just want to return every tea in the database, we don’t apply any joins, filters or groups (i.e. <code>WHERE</code>, <code>JOIN</code>, and <code>GROUP BY</code> clauses in SQL) to the method. The <code>from</code> and <code>order</code> variables tell the query what columns to return on the database and the order in which they are retrieved. We use the <code>SQLiteDatabase.query()</code> method as an interface to the database.

Last, we ask the supplied Activity (in this case, our <code>BrewClockActivity</code>) to manage the Cursor. Usually, a Cursor must be manually refreshed to reload any new data, so if we added a new tea to our database, we would have to remember to refresh our Cursor. Instead, Android can take care of this for us, recreating the results whenever the Activity is suspended and resumed, by calling <code>startManagingCursor()</code>.

Finally, we’ll add another utility method to return the number of records in the table. Once again, Android provides a handy utility to do this for us in the <code>DatabaseUtils</code> class:

Add the following method, <code>count</code>, to your <code>TeaData</code> class:

<pre><code class="language-javascript">// src/com/example/brewclock/TeaData.java
  public long count() {
    SQLiteDatabase db = getReadableDatabase();
    return DatabaseUtils.queryNumEntries(db, TABLE_NAME);
  }</code></pre>

Save the <code>TeaData</code> class, and fix any missing imports using Eclipse (Source → Organize Imports). With our data class finished, it’s time to change BrewClock’s interface to make use of the database!

### Modify BrewClock’s Interface to Allow Tea Selection

The purpose of storing preset teas and brew times is to let the user quickly select their favorite tea from the presets. To facilitate this, we’ll add a <code>Spinner</code> (analogous to a pop-up menu in desktop interfaces) to the main BrewClock interface, populated with the list of teas from <code>TeaData</code>.

As in the previous tutorial, use Eclipse’s layout editor to add the Spinner to BrewClock’s main interface layout XML file. Add the following code just below the <code>LinearLayout</code> for the brew count label (around line 24). Remember, you can switch to the “Code View” tab along the bottom of the window if Eclipse opens the visual layout editor.

<pre><code class="language-markup tmp-xml">&lt;!-- /res/layout/main.xml --&gt;

&lt;!-- Tea Selection --&gt;
&lt;LinearLayout
  android:orientation="vertical"
  android:layout_width="fill_parent"
  android:layout_height="wrap_content"&gt;

  &lt;Spinner
    android:id="@+id/tea_spinner"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" /&gt;

&lt;/LinearLayout&gt;</code></pre>

In the <code>BrewClockActivity</code> class, add a member variable to reference the Spinner, and connect it to the interface using <code>findViewById</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
protected Spinner teaSpinner;
protected TeaData teaData;

// …

public void onCreate(Bundle savedInstanceState) {
  // …
  teaData = new TeaData(this);
  teaSpinner = (Spinner) findViewById(R.id.tea_spinner);
}</code></pre>

Try running your application to make sure the new interface works correctly. You should see a blank pop-up menu (or Spinner) just below the brew count. If you tap the spinner, Android handles displaying a pop-up menu so that you can choose an option for the spinner. At the moment, the menu is empty, so we’ll remedy that by binding the Spinner to our tea database.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1f81adb-dece-4db6-9701-ec7dc0193c1f/3-blank-spinner-full.jpg"><img class="aligncenter size-full wp-image-90589" title="Blank Spinner" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb2c257a-c6fa-4c65-934a-ec33a92177a1/3-blank-spinner.jpg" alt="" width="500" height="356" /></a>

### Data Binding

When Android retrieves data from a database, it returns a <code>Cursor</code> object. The Cursor represents a set of results from the database and can be moved through the results to retrieve values. We can easily bind these results to a view (in this case, the Spinner) using a set of classes provided by Android called “Adapters.” Adapters do all the hard work of fetching database results from a <code>Cursor</code> and displaying them in the interface.

Remember that our <code>TeaData.all()</code> method already returns a Cursor populated with the contents of our teas table. Using that Cursor, all we need to do is create a <code>SimpleCursorAdapter</code> to bind its data to our <code>teaSpinner</code>, and Android will take care of populating the spinner’s options.

Connect the Cursor returned by <code>teaData.all()</code> to the Spinner by creating a <code>SimpleCursorAdapter</code>:

<pre><code class="language-javascript">// com/example/brewclock/BrewClockActivity.java

public void onCreate(Bundle savedInstanceState) {
  // …
  Cursor cursor = teaData.all(this);

  SimpleCursorAdapter teaCursorAdapter = new SimpleCursorAdapter(
    this,
    android.R.layout.simple_spinner_item,
    cursor,
    new String[] { TeaData.NAME },
    new int[] { android.R.id.text1 }
  );

  teaSpinner.setAdapter(teaCursorAdapter);
  teaCursorAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
}</code></pre>

Notice that we’ve made use of Android’s built-in <code>android.R</code> object. This provides some generic default resources for your application, such as simple views and layouts. In this case, we’ve used <code>android.R.layout.simple_spinner_item</code>, which is a simple text label layout.

If you run the application again, you’ll see that the spinner is still empty! Even though we’ve connected the spinner to our database, there are no records in the database to display.

Let’s give the user a choice of teas by adding some default records to the database in BrewClock’s constructor. To avoid duplicate entries, we’ll add only the default teas if the database is empty. We can make use of TeaData’s <code>count()</code> method to check if this is the case.

Add code to create a default set of teas if the database is empty. Add this line just above the code to fetch the teas from <code>teaData</code>:

<pre><code class="language-javascript">// com/example/brewclock/BrewClockActivity.java
public void onCreate(Bundle savedInstanceState) {
  // …

  // Add some default tea data! (Adjust to your preference :)
  if(teaData.count() == 0) {
    teaData.insert("Earl Grey", 3);
    teaData.insert("Assam", 3);
    teaData.insert("Jasmine Green", 1);
    teaData.insert("Darjeeling", 2);
  }

  // Code from the previous step:
  Cursor cursor = teaData.all(this);

  // …
}</code></pre>

Now run the application again. You’ll now see that your tea Spinner has the first tea selected. Tapping on the Spinner lets you select one of the teas from your database!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4cac013-55cf-4fac-b201-0509956621fe/4-populated-spinner-full.jpg"><img class="aligncenter size-full wp-image-90590" title="Populated Spinner" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647bd9ad-3de1-49e0-b6b4-ddd4744ee3ce/4-populated-spinner.jpg" alt="" width="500" height="356" /></a>

Congratulations! You’ve successfully connected your interface to a data source. This is one of the most important aspects of any software application. As you’ve seen, Android makes this task fairly easy, but it is extremely powerful. Using cursors and adapters, you can take virtually any data source (from a simple array of strings to a complex relational database query) and bind it to any type of view: a spinner, a list view or even an iTunes-like cover-flow gallery!

Although now would be a good time for a brew, our work isn’t over yet. While you can choose different teas from the Spinner, making a selection doesn’t do anything. We need to find out which tea the user has selected and update the brew time accordingly.</p>

### Read Selected Tea, and Update Brew Time

To determine which tea the user has selected from our database, <code>BrewClockActivity</code> needs to listen for an event. Similar to the <code>OnClickListener</code> event that is triggered by button presses, we’ll implement the <code>OnItemSelectedListener</code>. Events in this listener are triggered when the user makes a selection from a view, such as our Spinner.

Enable the <code>onItemSelectedListener</code> in <code>BrewClockActivity</code> by adding it to the class declaration. Remember to implement the interface methods <code>onItemSelected()</code> and <code>onNothingSelected()</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
public class BrewClockActivity extends Activity implements OnClickListener, OnItemSelectedListener {
  // …
  public void onItemSelected(AdapterView&lt;?&gt; spinner, View view, int position, long id) {
    if(spinner == teaSpinner) {
      // Update the brew time with the selected tea’s brewtime
      Cursor cursor = (Cursor) spinner.getSelectedItem();
      setBrewTime(cursor.getInt(2));
    }
  }

  public void onNothingSelected(AdapterView&lt;?&gt; adapterView) {
    // Do nothing
  }
}</code></pre>

Here we check whether the spinner that triggered the <code>onItemSelected</code> event was BrewClock’s <code>teaSpinner</code>. If so, we retrieve a Cursor object that represents the selected record. This is all handled for us by the <code>SimpleCursorAdapter</code> that connects <code>teaData</code> to the Spinner. Android knows which query populates the Spinner and which item the user has selected. It uses these to return the single row from the database, representing the user’s selected tea.

Cursor’s <code>getInt()</code> method takes the index of the column we want to retrieve. Remember that when we built our Cursor in <code>teaData.all()</code>, the columns we read were <code>_ID</code>, <code>NAME</code> and <code>BREW_TIME</code>. Assuming we chose Jasmine tea in <code>teaSpinner</code>, the Cursor returned by our selection would be pointing at that record in the database.

We then ask the Cursor to retrieve the value from column 2 (using <code>getInt(2)</code>), which in this query is our <code>BREW_TIME</code> column. This value is supplied to our existing <code>setBrewTime()</code> method, which updates the interface to show the selected tea’s brewing time.

Finally, we need to tell the <code>teaSpinner</code> that <code>BrewClockActivity</code> is listening for <code>OnItemSelected</code> events. Add the following line to <code>BrewClockActivity</code>’s <code>onCreate</code> method:

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
public void onCreate() {
  // …
  teaSpinner.setOnItemSelectedListener(this);
}</code></pre>

That should do it! Run your application again, and try selecting different teas from the Spinner. Each time you select a tea, its brew time will be shown on the countdown clock. The rest of our code already handles counting down from the current brew time, so we now have a fully working brew timer, with a list of preset teas.

You can, of course, go back into the code and add more preset teas to the database to suit your tastes. But what if we released BrewClock to the market? Every time someone wanted to add a new tea to the database, we’d need to manually update the database, and republish the application; everyone would need to update, and everybody would have the same list of teas. That sounds pretty inflexible, and a lot of work for us!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f563f32-a1a5-4f6d-8a72-af2d7ff4e5a3/5-default-teas-full.jpg"><img class="aligncenter size-full wp-image-90591" title="Default Teas" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f62cf096-6da2-47b4-a04b-55cf67dd2b30/5-default-teas.jpg" alt="" width="500" height="356" /></a>

It would be much better if the user had some way to add their own teas and preferences to the database. We’ll tackle that next…

## Introducing Activities

Each screen in your application and its associated code is an <code>Activity</code>. Every time you go from one screen to another, Android creates a new Activity. In reality, although an application may comprise any number of screens/activities, Android treats them as separate entities. Activities work together to form a cohesive experience because Android lets you easily pass data between them.

In this final section, you’ll add a new Activity (<code>AddTeaActivity</code>) to your application and register it with the Android system. You’ll then pass data from the original <code>BrewClockActivity</code> to this new Activity.

First, though, we need to give the user a way to switch to the new Activity. We’ll do this using an options menu.</p>

### Options Menus

Options menus are the pop-up menus that appear when the user hits the “Menu” key on their device. Android handles the creation and display of options menus automatically; you just need to tell it what options to display and what to do when an option is chosen by the user.

However, rather than hard-coding our labels into the menu itself, we’ll make use of Android string resources. String resources let you maintain all the human-readable strings and labels for your application in one file, calling them within your code. This means there’s only one place in your code where you need to change strings in the future.

In the project explorer, navigate to “res/values” and you will see that a <em>strings.xml</em> file already exists. This was created by Eclipse when we first created the project, and it is used to store any strings of text that we want to use throughout the application.

Open <em>strings.xml</em> by double clicking on it, and switch to the XML view by clicking the <em>strings.xml</em> tab along the bottom of the window.

Add the following line within the <code>&lt;resources&gt;…&lt;/resources&gt;</code> element:

<pre><code class="language-markup tmp-xml">&lt;!-- res/values/strings.xml --&gt;
  &lt;resources&gt;
    &lt;!-- … --&gt;
    &lt;string name="add_tea_label"&gt;Add Tea&lt;/string&gt;
  &lt;/resources&gt;</code></pre>

Here you’ve defined a string, <code>add_tea_label</code>, and its associated text. We can use <code>add_tea_label</code> to reference the string throughout the application’s code. If the label needs to change for some reason in the future, you’ll need to change it only once in this file.

Next, let’s create a new file to define our options menu. Just like strings and layouts, menus are defined in an XML file, so we’ll start by creating a new XML file in Eclipse:

Create a new Android XML file in Eclipse by choosing File → New → Other, and then select “Android XML File.”

Select a resource type of “Menu,” and save the file as <em>main.xml</em>. Eclipse will automatically create a folder, <em>res/menu</em>, where your menu XML files will be stored.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e7e5add-9f66-40eb-938b-f5783d09a437/7-new-menu-xml-full.jpg"><img class="aligncenter size-full wp-image-90592" title="New Menu XML" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07dd7be5-0cb9-4b6a-aa82-f4a09dbe7129/7-new-menu-xml.jpg" alt="" width="500" height="482" /></a>

Open the <em>res/menus/main.xml</em> file, and switch to XML view by clicking the “main.xml” tab along the bottom of the window.

Add a new menu item, <code>add_tea</code>.

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;menu xmlns:android="https://schemas.android.com/apk/res/android"&gt;
  &lt;item android:id="@+id/add_tea" android:title="@string/add_tea_label" /&gt;
&lt;/menu&gt;</code></pre>

Notice the <code>android:title</code> attribute is set to <code>@string/add_tea_label</code>. This tells Android to look up <code>add_tea_label</code> in our <em>strings.xml</em> file and return the associated label. In this case, our menu item will have a label “Add Tea.”

Next, we’ll tell our Activity to display the options menu when the user hits the “Menu” key on their device.

Back in <em>BrewClockActivity.java</em>, override the <code>onCreateOptionsMenu</code> method to tell Android to load our menu when the user presses the “Menu” button:

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
  MenuInflater inflater = getMenuInflater();
  inflater.inflate(R.menu.main, menu);

  return true;
}</code></pre>

When the user presses the “Menu” button on their device, Android will now call <code>onCreateOptionsMenu</code>. In this method, we create a <code>MenuInflater</code>, which loads a menu resource from your application’s package. Just like the buttons and text fields that make up your application’s layout, the <em>main.xml</em> resource is available via the global <code>R</code> object, so we use that to supply the <code>MenuInflater</code> with our menu resource.

To test the menu, save and run the application in the Android emulator. While it’s running, press the “Menu” button, and you’ll see the options menu pop up with an “Add Tea” option.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dee3653d-699d-4edd-9df4-62eddbbceeeb/8-add-teas-options-menu-full.jpg"><img class="aligncenter size-full wp-image-90593" title="Add Teas Options Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7396522e-b4d2-4e81-8d06-11a575f7dd77/8-add-teas-options-menu.jpg" alt="" width="500" height="356" /></a>

If you tap the “Add Tea” option, Android automatically detects the tap and closes the menu. In the background, Android will notify the application that the option was tapped.</p>

### Handling Menu Taps

When the user taps the “Add Tea” menu option, we want to display a new Activity so that they can enter the details of the tea to be added. Start by creating that new Activity by selecting File → New → Class.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c32cd31-b955-4b11-a81d-3e03f04a1590/9-new-activity-settings-full.jpg"><img class="aligncenter size-full wp-image-90594" title="New Activity Settings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13bde074-ec78-4fea-930e-0180d697bc9b/9-new-activity-settings.jpg" alt="" width="500" height="583" /></a>

Name the new class <code>AddTeaActivity</code>, and make sure it inherits from the <code>android.app.Activity</code> class. It should also be in the <code>com.example.brewclock</code> package:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
package com.example.brewclock;

import android.app.Activity;
import android.os.Bundle;

public class AddTeaActivity extends Activity {
  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
  }
}</code></pre>

This simple, blank Activity won’t do anything yet, but it gives us enough to finish our options menu.

Add the <code>onOptionsItemSelected</code> override method to <code>BrewClockActivity</code>. This is the method that Android calls when you tap on a <code>MenuItem</code> (notice it receives the tapped <code>MenuItem</code> in the item parameter):

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
  switch(item.getItemId()) {
    case R.id.add_tea:
      Intent intent = new Intent(this, AddTeaActivity.class);
      startActivity(intent);
      return true;

    default:
      return super.onOptionsItemSelected(item);
  }
}</code></pre>

With this code, we’ve told Android that when the “Add Tea” menu item is tapped, we want to start a new Activity; in this case, <code>AddTeaActivity</code>. However, rather than directly creating an instance of <code>AddTeaActivity</code>, notice that we’ve used an <code>Intent</code>. Intents are a powerful feature of the Android framework: they bind Activities together to make up an application and allow data to be passed between them.

Intents even let your application take advantage of any Activities within other applications that the user has installed. For example, when the user asks to display a picture from a gallery, Android automatically displays a dialogue to the user allowing them to pick the application that displays the image. Any applications that are registered to handle image display will be shown in the dialogue.

Intents are a powerful and complex topic, so it’s worth reading about them in detail in the <a href="https://developer.android.com/guide/topics/intents/intents-filters.html">official Android SDK documentation</a>.

Let’s try running our application to test out the new “Add Tea” screen.

Run your project, tap the “Menu” button and then tap “Add Tea.”

Instead of seeing your “Add Tea” Activity as expected, you’ll be presented with a dialogue that is all too common for Android developers:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0031ac67-1bec-4390-bb9c-547af6180a89/10-crash-full.jpg"><img class="aligncenter size-full wp-image-90595" title="Crash" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/554c70a1-1573-40eb-a055-828dc9183faf/10-crash.jpg" alt="" width="500" height="356" /></a>

Although we created the <code>Intent</code> and told it to start our <code>AddTeaActivity</code> Activity, the application crashed because we haven’t yet registered it within Android. The system doesn’t know where to find the Activity we’re trying to run (remember that Intents can start Activities from any application installed on the device). Let’s remedy this by registering our Activity within the application manifest file.

Open your application’s manifest file, <em>AndroidManifest.xml</em> in Eclipse, and switch to the code view by selecting the “AndroidManifest.xml” tab along the bottom of the window.

The application’s manifest file is where you define global settings and information about your application. You’ll see that it already declares <code>.BrewClockActivity</code> as the Activity to run when the application is launched.

Within <code>&lt;application&gt;</code>, add a new <code>&lt;activity&gt;</code> node to describe the “Add Tea” Activity. Use the same <code>add_tea_label</code> string that we declared earlier in <em>strings.xml</em> for the Activity’s title:

<pre><code class="language-markup tmp-xml">&lt;!-- AndroidManifest.xml --&gt;
&lt;application …&gt;
  …
  &lt;activity android:name=".AddTeaActivity" android:label="@string/add_tea_label" /&gt;
&lt;/application&gt;</code></pre>

Save the manifest file before running BrewClock again. This time, when you open the menu and tap “Add Tea,” Android will start the <code>AddTeaActivity</code>. Hit the “Back” button to go back to the main screen.

With the Activities hooked together, it’s time to build an interface for adding tea!

## Building The Tea Editor Interface

Building the interface to add a tea is very similar to how we built the main BrewClock interface in the previous tutorial. Start by creating a new layout file, and then add the appropriate XML, as below.

Alternatively, you could use Android’s recently improved layout editor in Eclipse to build a suitable interface. Create a new XML file in which to define the layout. Go to File → New, then select “Android XML File,” and select a “Layout” type. Name the file <em>add_tea.xml</em>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1066cf7c-3984-4921-933c-b066729d28dd/11-new-layout-xml-full.jpg"><img class="aligncenter size-full wp-image-90596" title="New Layout XML" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3119248-b95e-4919-a982-5743cf93f560/11-new-layout-xml.jpg" alt="" width="500" height="482" /></a>

Replace the contents of <em>add_tea.xml</em> with the following layout:

<pre><code class="language-markup tmp-xml">&lt;!-- res/layouts/add_tea.xml --&gt;
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout
  xmlns:android="https://schemas.android.com/apk/res/android"
  android:layout_width="fill_parent"
  android:layout_height="fill_parent"
  android:orientation="vertical"
  android:padding="10dip"&gt;

  &lt;TextView
    android:text="@string/tea_name_label"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" /&gt;

  &lt;EditText
    android:id="@+id/tea_name"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"/&gt;

  &lt;TextView
    android:text="@string/brew_time_label"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/&gt;

  &lt;SeekBar
    android:id="@+id/brew_time_seekbar"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:progress="2"
    android:max="9" /&gt;

  &lt;TextView
    android:id="@+id/brew_time_value"
    android:text="3 m"
    android:textSize="20dip"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:gravity="center_horizontal" /&gt;
&lt;/LinearLayout&gt;</code></pre>

We’ll also need to add some new strings to <em>strings.xml</em> for the labels used in this interface:

<pre><code class="language-markup tmp-xml">&lt;!-- res/values/strings.xml --&gt;
&lt;resources&gt;
  &lt;!-- … --&gt;
  &lt;string name="tea_name_label"&gt;Tea Name&lt;/string&gt;

  &lt;string name="brew_time_label"&gt;Brew Time&lt;/string&gt;
&lt;/resources&gt;</code></pre>

In this layout, we’ve added a new type of interface widget, the SeekBar. This lets the user easily specify a brew time by dragging a thumb from left to right. The range of values that the SeekBar produces always runs from zero (0) to the value of <code>android:max</code>.

In this interface, we’ve used a scale of 0 to 9, which we will map to brew times of 1 to 10 minutes (brewing for 0 minutes would be a waste of good tea!). First, though, we need to make sure that <code>AddTeaActivity</code> loads our new interface:

Add the following line of code to the Activity’s <code>onCreate()</code> method that loads and displays the <code>add_tea</code> layout file:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.add_tea);
}</code></pre>

Now test your application by running it, pressing the “Menu” button and tapping “Add Tea” from the menu.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a15b816f-25c7-4239-ae8e-6691b5e16977/12-add-tea-interface-full.jpg"><img class="aligncenter size-full wp-image-90597" title="Add Tea Interface" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da9c8111-28eb-4f97-9863-41dde7de4113/12-add-tea-interface.jpg" alt="" width="500" height="356" /></a>

You’ll see your new interface on the “Add Tea” screen. You can enter text and slide the SeekBar left and right. But as you’d expect, nothing works yet because we haven’t hooked up any code.

Declare some properties in <code>AddTeaActivity</code> to reference our interface elements:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
public class AddTeaActivity { 
  // …

  /** Properties **/
  protected EditText teaName;
  protected SeekBar brewTimeSeekBar;
  protected TextView brewTimeLabel;

  // …</code></pre>

Next, connect those properties to your interface:

<pre><code class="language-javascript">public void onCreate(Bundle savedInstanceState) {
  // …
  // Connect interface elements to properties
  teaName = (EditText) findViewById(R.id.tea_name);
  brewTimeSeekBar = (SeekBar) findViewById(R.id.brew_time_seekbar);
  brewTimeLabel = (TextView) findViewById(R.id.brew_time_value);
}</code></pre>

The interface is fairly simple, and the only events we need to listen for are changes to the SeekBar. When the user moves the SeekBar thumb left or right, our application will need to read the new value and update the label below with the selected brew time. We’ll use a <code>Listener</code> to detect when the SeekBar is changed:

Add an <code>onSeekBarChangedListener</code> interface to the <code>AddTeaActivity</code> class declaration, and add the required methods:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
public class AddTeaActivity
extends Activity
implements OnSeekBarChangeListener {
  // …

  public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
    // TODO Detect change in progress
  }

  public void onStartTrackingTouch(SeekBar seekBar) {}

  public void onStopTrackingTouch(SeekBar seekBar) {}
}</code></pre>

The only event we’re interested in is <code>onProgressChanged</code>, so we need to add the code below to that method to update the brew time label with the selected value. Remember that our SeekBar values range from 0 to 9, so we’ll add 1 to the supplied value so that it makes more sense to the user:

Add the following code to <code>onProgressChanged()</code> in <em>AddTeaActivity.java</em>:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
  if(seekBar == brewTimeSeekBar) {
    // Update the brew time label with the chosen value.
    brewTimeLabel.setText((progress + 1) + " m");
  }
}</code></pre>

Set the SeekBar’s listener to be our <code>AddTeaActivity</code> in <code>onCreate</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
public void onCreate(Bundle savedInstanceState) {
  // …

  // Setup Listeners
  brewTimeSeekBar.setOnSeekBarChangeListener(this);
}</code></pre>

Now when run the application and slide the SeekBar left to right, the brew time label will be updated with the correct value:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b71d705-1868-42e0-a60f-cb6e3cfd954b/13-seekbar-full.jpg"><img class="aligncenter size-full wp-image-90598" title="Seekbar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a54431e9-1bdc-4eab-90d2-ac0ce0d7a5b6/13-seekbar.jpg" alt="" width="500" height="356" /></a>

### Saving Tea

With a working interface for adding teas, all that’s left is to give the user the option to save their new tea to the database. We’ll also add a little validation to the interface so that the user cannot save an empty tea to the database!

Start by opening <em>strings.xml</em> in the editor and adding some new labels for our application:

<pre><code class="language-markup tmp-xml">&lt;!-- res/values/strings.xml --&gt; 
&lt;string name="save_tea_label"&gt;Save Tea&lt;/string&gt;
&lt;string name="invalid_tea_title"&gt;Tea could not be saved.&lt;/string&gt;

&lt;string name="invalid_tea_no_name"&gt;Enter a name for your tea.&lt;/string&gt;</code></pre>

Just like before, we’ll need to create a new options menu for <code>AddTeaActivity</code> so that the user can save their favorite tea:

Create a new XML file, <em>add_tea.xml</em>, in the <em>res/menus</em> folder by choosing File → New and then Other → Android XML File. Remember to select “Menu” as the resource type.

Add an item to the new menu for saving the tea:

<pre><code class="language-markup tmp-xml">&lt;!-- res/menus/add_tea.xml --&gt; 
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;menu xmlns:android="https://schemas.android.com/apk/res/android"&gt;
  &lt;item android:title="@string/save_tea_label" android:id="@+id/save_tea" /&gt;
&lt;/menu&gt;</code></pre>

Back in <code>AddTeaActivity</code>, add the override methods for <code>onCreateOptionsMenu</code> and <code>onOptionsItemSelected</code>, just like you did in <code>BrewClockActivity</code>. However, this time, you’ll supply the <em>add_tea.xml</em> resource file to the <code>MenuInflater</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
  MenuInflater inflater = getMenuInflater();
  inflater.inflate(R.menu.add_tea, menu);

  return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
  switch(item.getItemId()) {
    case R.id.save_tea:
      saveTea();

    default:
      return super.onOptionsItemSelected(item);
  }
}</code></pre>

Next, we’ll add a new method, <code>saveTea()</code>, to handle saving the tea. The <code>saveTea</code> method first reads the name and brew time values chosen by the user, validates them and (if all is well) saves them to the database:

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
public boolean saveTea() {
  // Read values from the interface
  String teaNameText = teaName.getText().toString();
  int brewTimeValue = brewTimeSeekBar.getProgress() + 1;

  // Validate a name has been entered for the tea
  if(teaNameText.length() &lt; 2) {
    AlertDialog.Builder dialog = new AlertDialog.Builder(this);
    dialog.setTitle(R.string.invalid_tea_title);
    dialog.setMessage(R.string.invalid_tea_no_name);
    dialog.show();

    return false;
  }

  // The tea is valid, so connect to the tea database and insert the tea
  TeaData teaData = new TeaData(this);
  teaData.insert(teaNameText, brewTimeValue);
  teaData.close();

  return true;
}</code></pre>

This is quite a hefty chunk of code, so let’s go over the logic.

First, we read the values of the EditText <code>teaName</code> and the SeekBar <code>brewTimeSeekBar</code> (remembering to add 1 to the value to ensure a brew time of between 1 and 10 minutes). Next, we validate that a name has been entered that is two or more characters (this is really simple validation; you might want to experiment doing something more elaborate, such as using regular expressions).

If the tea name is not valid, we need to let the user know. We make use of one of Android’s helper classes, <code>AlertDialog.Builder</code>, which gives us a handy shortcut for creating and displaying a modal dialog window. After setting the title and error message (using our string resources), the dialogue is displayed by calling its <code>show()</code> method. This dialogue is modal, so the user will have to dismiss it by pressing the “Back” key. At this point, we don’t want to save any data, so just return <code>false</code> out of the method.

If the tea is valid, we create a new temporary connection to our tea database using the <code>TeaData</code> class. This demonstrates the advantage of abstracting your database access to a separate class: you can access it from anywhere in the application!

After calling <code>teaData.insert()</code> to add our tea to the database, we no longer need this database connection, so we close it before returning <code>true</code> to indicate that the save was successful.

Try this out by running the application in the emulator, pressing “Menu” and tapping “Add Tea.” Once on the “Add Tea” screen, try saving an empty tea by pressing “Menu” again and tapping “Save Tea.” With your validation in place, you’ll be presented with an error message:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfee9741-e7c6-4c1e-ba1d-77084642b918/14-invalid-tea-full.jpg"><img class="aligncenter size-full wp-image-90599" title="Invalid Tea" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1650ba94-6a30-4cc4-b0eb-a703274291e1/14-invalid-tea.jpg" alt="" width="500" height="356" /></a>

Next, try entering a name for your tea, choosing a suitable brew time, and choosing “Save Tea” from the menu again. This time, you won’t see an error message. In fact, you’ll see nothing at all.</p>

### Improving the User Experience

While functional, this isn’t a great user experience. The user doesn’t know that their tea has been successfully saved. In fact, the only way to check is to go back from the “Add Tea” Activity and check the list of teas. Not great. Letting the user know that their tea was successfully saved would be much better. Let’s show a message on the screen when a tea has been added successfully.

We want the message to be passive, or non-modal, so using an <code>AlertDialog</code> like before won’t help. Instead, we’ll make use of another popular Android feature, the <code>Toast</code>.

Toasts display a short message near the bottom of the screen but do not interrupt the user. They’re often used for non-critical notifications and status updates.

Start by adding a new string to the <em>strings.xml</em> resource file. Notice the <code>%s</code> in the string? We’ll use this in the next step to interpolate the name of the saved tea into the message!

<pre><code class="language-markup tmp-xml">&lt;!-- res/values/strings.xml --&gt;
&lt;string name="save_tea_success"&gt;%s tea has been saved.&lt;/string&gt;</code></pre>

Modify the code in <code>onOptionsItemSelected</code> to create and show a <code>Toast</code> pop-up if the result of <code>saveTea()</code> is <code>true</code>. The second parameter uses of <code>getString()</code> interpolate the name of our tea into the <code>Toast</code> message. Finally, we clear the “Tea Name” text so that the user can quickly add more teas!

<pre><code class="language-javascript">// src/com/example/brewclock/AddTeaActivity.java
// …
switch(item.getItemId()) {
 case R.id.save_tea:
   if(saveTea()) {
     Toast.makeText(this, getString(R.string.save_tea_success, teaName.getText().toString()), Toast.LENGTH_SHORT).show();
     teaName.setText("");
   }
// …</code></pre>

Now re-run your application and try adding and saving a new tea. You’ll see a nice <code>Toast</code> pop up to let you know the tea has been saved. The <code>getString()</code> method interpolates the name of the tea that was saved into the XML string, where we placed the <code>%s</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bbf9235-81ca-47df-99b2-2325bf2a1af3/16-valid-save-full.jpg"><img class="aligncenter size-full wp-image-90601" title="Valid Save" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3852b42-2173-4ffd-8644-8e0916f013fd/16-valid-save.jpg" alt="" width="500" height="356" /></a>

Click the “Back” button to return to the application’s main screen, and tap the tea spinner. The new teas you added in the database now show up as options in the spinner!

## User Preferences

BrewClock is now fully functional. Users can add their favorite teas and the respective brewing times to the database, and they can quickly select them to start a new brew. Any teas added to BrewClock are saved in the database, so even if we quit the application and come back to it later, our list of teas is still available.

One thing you might notice when restarting BrewClock, though, is that the brew counter is reset to 0. This makes keeping track of our daily tea intake (a vital statistic!) difficult. As a final exercise, let’s save the total brew count to the device.

Rather than adding another table to our teas database, we’ll make use of Android’s “Shared Preferences,” a simple database that Android provides to your application for storing simple data (strings, numbers, etc.), such as high scores in games and user preferences.

Start by adding a couple of constants to the top of <em>BrewClockActivity.java</em>. These will store the name of your shared preferences file and the name of the key we’ll use to access the brew count. Android takes care of saving and persisting our shared preferences file.

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
protected static final String SHARED_PREFS_NAME = "brew_count_preferences";
protected static final String BREW_COUNT_SHARED_PREF = "brew_count";</code></pre>

Next, we’ll need to make some changes to the code so that we can read and write the brew count to the user preferences, rather than relying on an initial value in our code. In <code>BrewClockActivity</code>’s <code>onCreate</code> method, change the lines around <code>setBrewCount(0)</code> to the following:

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
public void onCreate() {
  // … 

  // Set the initial brew values
  SharedPreferences sharedPreferences = getSharedPreferences(SHARED_PREFS_NAME, MODE_PRIVATE);
  brewCount = sharedPreferences.getInt(BREW_COUNT_SHARED_PREF, 0);
  setBrewCount(brewCount);

  // …
}</code></pre>

Here we’re retrieving an instance of the application’s shared preferences using <code>SharedPreferences</code>, and asking for the value of the <code>brew_count</code> key (identified by the <code>BREW_COUNT_SHARED_PREF</code> constant that was declared earlier). If a value is found, it will be returned; if not, we’ll use the default value in the second parameter of <code>getInt</code> (in this case, 0).

Now that we can retrieve the stored value of brew count, we need to ensure its value is saved to <code>SharedPreferences</code> whenever the count is updated.

Add the following code to <code>setBrewCount</code> in <code>BrewClockActivity</code>:

<pre><code class="language-javascript">// src/com/example/brewclock/BrewClockActivity.java
 public void setBrewCount(int count) {
   brewCount = count;
   brewCountLabel.setText(String.valueOf(brewCount));

   // Update the brewCount and write the value to the shared preferences.
   SharedPreferences.Editor editor = getSharedPreferences(SHARED_PREFS_NAME, MODE_PRIVATE).edit();
   editor.putInt(BREW_COUNT_SHARED_PREF, brewCount);
   editor.commit();
 }</code></pre>

Shared preferences are never saved directly. Instead, we make use of Android’s <code>SharedPreferences.Editor</code> class. Calling <code>edit()</code> on <code>SharedPreferences</code> returns an <code>editor</code> instance, which can then be used to set values in our preferences. When the values are ready to be saved to the shared preferences file, we just call <code>commit()</code>.

With our application’s code all wrapped up, it’s time to test everything!

Run the application on the emulator, and time a few brews (this is the perfect excuse to go and make a well-deserved tea or two!), and then quit the application. Try running another application that is installed on the emulator to ensure BrewClock is terminated. Remember that Android doesn’t terminate an Activity until it starts to run out of memory.

When you next run the application, you’ll see that your previous brew count is maintained, and all your existing teas are saved!

## Summary

Congratulations! You’ve built a fully working Android application that makes use of a number of core components of the Android SDK. In this tutorial, you have seen how to:

*   Create a simple SQLite database to store your application’s data;
*   Make use of Android’s database classes and write a custom class to abstract the data access;
*   Add option menus to your application;
*   Create and register new Activities within your application and bind them together into a coherent interface using Intents;
*   Store and retrieve simple user data and settings using the built-in “Shared Preferences” database.

Data storage and persistence is an important topic, no matter what type of application you’re building. From utilities and business tools to 3-D games, nearly every application will need to make use of the data tools provided by Android.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35c5587f-15f6-4072-a943-fc091440b6ed/17-brew-up-full.jpg"><img class="aligncenter size-full wp-image-90602" title="Brew Up" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6760a5eb-53a5-4085-8c62-abe3d1c4350b/17-brew-up.jpg" alt="" width="500" height="356" /></a>

### Activities

BrewClock is now on its way to being a fully functional application. However, we could still implement a few more features to improve the user experience. For example, you might like to develop your skills by trying any of the following:

*   Checking for duplicate tea name entries before saving a tea,
*   Adding a menu option to reset the brew counter to 0,
*   Storing the last-chosen brew time in a shared preference so that the application defaults to that value when restarted,
*   Adding an option for the user to delete teas from the database.

Solutions for the Activities will be included in a future branch on the <a href="https://github.com/cblunt/BrewClock">GitHub repository</a>, where you’ll find the full source-code listings. You can download the working tutorial code by switching your copy of the code to the <code>tutorial_2</code> branch:

<pre><code class="language-markup tmp-python"># If you’ve not already cloned the repository,
# you’ll need to do that first:
# $ git clone git://github.com/cblunt/BrewClock.git
# $ cd BrewClock
$ git checkout tutorial_2</code></pre>

I hope you’ve enjoyed working through this tutorial and that it helps you in designing and building your great Android applications. Please let me know how you get on in the comments below, or feel free to drop me an email.

<em>Thanks to <a href="https://blog.anselmbradford.com/">Anselm</a> for his suggestions and feedback!</em>

{{< signature "al" >}}

