---
title: 'Using CSCS Scripting Language For Cross-Platform Development'
slug: cscs-scripting-language-cross-platform-development
author: vassili-kaplan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86a712fa-07ac-407c-9e28-7f326437f84a/cscs-scripting-language-cross-platform-development.png
date: 2020-01-29T11:00:00.000Z
summary: >-
  In this article, Vassili Kaplan explains how you can use a scripting language to develop cross-platform mobile applications. You’ll find examples in both iOS and Android that include placing widgets on the screen, SQLite, Web Requests and JSON parsing.
description: >-
  In this article, Vassili Kaplan explains how to use a scripting language to develop cross-platform mobile applications.
categories:
  - iOS
  - Apps
  - Android
  - Mobile
---
<blockquote>Our goal is not to build a platform; it’s to be cross all of them.<br /><br />&mdash; Mark Zuckerberg</blockquote>

<p>CSCS (Customized Scripting in C#) is an open-source scripting language implemented in C#. Syntactically it’s very similar to JavaScript, but it also has some similarities with Python. Some of these similarities are the keywords in the well-known <code>if…elif…else</code> construct, and also have the same variable scope definition as in Python (e.g. a variable defined inside of an <code>if</code> block or inside a loop will be also visible outside).</p>

<p>As opposed to JavaScript and Python, variables and functions in CSCS are case-insensitive. <strong>The primary goal of CSCS is to let the developer write as little code as possible</strong>. Also, the same code is used for both iOS and Android development. Additionally, CSCS can be used for Windows, Mac, and Unity development.</p>

<p><strong>Note</strong>: <em>You can read more about how Microsoft uses CSCS in their Maquette product (based on Unity) over <a href="https://www.codemag.com/Article/1903081">here</a>.</em></p>

<p>CSCS can be added to your project by embedding its C# source code into a Visual Studio Xamarin project. Unlike most other languages, you have full ownership of the CSCS source code and can easily add or modify its functionality. I’ll be sharing an example of this later on in the article.</p>

<p>Also, we are going to <strong>learn how to get started with CSCS</strong> and use some more advanced features that have been covered in other articles. Among these features, we are going to access a Web Service via Web Requests with JSON string parsing, and we’ll also be using SQLite on iOS and Android.</p>

<p>The easiest way to get started is to <a href="https://github.com/vassilych/mobile">download a sample of a project using CSCS</a> and start playing with the <em>start.cscs</em> file. This is what we’ll be doing in the next section: creating an iOS/Android app with basic GUI and events.</p>

{{% feature-panel %}}

## "Hello, World!" In CSCS

<p>Let’s start with a relatively simple example of CSCS code that constructs a screen with a few widgets:</p>

<pre><code class="language-javascript">AutoScale();
SetBackgroundColor("light_green");

locLabelText = GetLocation("ROOT", "CENTER", "ROOT", "TOP");
AddLabel(locLabelText, "labelText", "Welcome " +
    _DEVICE_INFO_ + " " + _VERSION_INFO_ + " User!", 600, 100);

locTextEdit = GetLocation("ROOT", "LEFT", labelText,
  "BOTTOM");
AddTextEdit(locTextEdit, "textEdit", "Your name", 320, 80);

locButton = GetLocation(textEdit,"RIGHT",textEdit, "CENTER");
AddButton(locButton, "buttonHi", "Hello", 160, 80);

function buttonHi_click(sender, arg) {
  name = getText(textEdit);
  msg = name != "" ? "Hello, "+ name + "!" : "Hello, World!";
  AlertDialog("My Great App", msg);
}</code></pre>

<p>The image below shows the resulting user interface on an iPhone as well as an Android device after clicking on the “Hello” button and not typing anything in the “Text Edit” field:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de7dcc7f-3f52-473a-bb38-9eb6bc4d920b/1-cscs-scripting-language-for-cross-platform-development.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de7dcc7f-3f52-473a-bb38-9eb6bc4d920b/1-cscs-scripting-language-for-cross-platform-development.png" sizes="100vw" caption="“Hello, World!” on iPhone (left) and Android (right) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de7dcc7f-3f52-473a-bb38-9eb6bc4d920b/1-cscs-scripting-language-for-cross-platform-development.png'>Large preview</a>)" alt="Hello, World!” on iPhone (left) and Android (right)" >}}

<p>Let’s briefly go over the code above. It starts with the <code>AutoScale()</code> function call, and what that does is to tell the parser that the widget sizes are relative to the screen size, i.e. they will be auto-resized (the widget will look bigger on bigger screens and smaller on smaller screens). This setting could be also overridden per widget.</p>

<p>Note that there is no need to create a special handler on a button click. If you define a function with name <code>widgetName_click()</code>, it will be used as a handler when the user clicks on a widget called <code>widgetName</code> (it doesn’t have to be a button, it can actually be any widget). That’s why the function <code>buttonHi_click()</code> will be triggered as soon as the user clicks on the button.</p>

<p>You may have noticed that the GUI is constructed completely in code. This is done by supplying a relative widget location when adding it. The general format of a location command is the following:</p>

<div class="break-out">

<pre><code class="language-javascript">location = GetLocation(WidgetX, HorizontalPlacement, WidgetY, VerticalPlacement,
                       deltaX=0, deltaY=0, autoResize=true);
</code></pre>
</div>

So, you can place a widget relative to other widgets on the screen. A special case of a widget is a “ROOT” widget, meaning the main screen.

After creating a location, you need to provide it as an argument to any of the following functions:

  - `AddLabel`,
  - `AddButton`,
  - `AddCombobox`,
  - `AddStepper`,
  - `AddListView`,
  - `AddTextView`,
  - `AddStepper`,
  - `AddImageView`,
  - `AddSlider`,
  - `AddPickerView`,
  - and so on.

All of the above have the same structure:</p>

<pre><code class="language-javascript">AddButton(location, newWidgetname, initialValue, width, height);
</code></pre>

<p>The widget width and height will be relative to the screen size if the <code>AutoScale()</code> CSCS command was previously run. Also, the initial value (in case of a button) is the text shown on it. This can be changed anytime by invoking <code>SetText(widgetName, newText)</code>.</p>

## Using Visual Studio Code To Debug CSCS

<p>We can also use Visual Studio Code to debug CSCS scripts. If you want to develop apps for both Android and iOS, you need to use a Mac. After installing <a href="https://code.visualstudio.com/download">Visual Studio Code</a>, install the <a href="https://marketplace.visualstudio.com/items?itemName=vassilik.cscs-debugger">CSCS Debugger and REPL extension</a>.</p>

<p>In order to use the extension, add this line of code anywhere in your <code>start.cscs</code> CSCS script:</p>

<pre><code class="language-javascript">StartDebugger();
</code></pre>

<p>The following image below shows how you can use Visual Studio Code to debug and change the functionality of the “Hello, World!” app that we developed in the previous section. In the upcoming example, we’ll be adding a label and a button on the fly to the existing layout.</p>

<p>To do this, we just select the code to be executed by the parser and press <kbd>Ctrl</kbd> + <kbd>8</kbd>. As a result, a label and a button will be added at the center of the screen. We also add a button handler that will update the new label with the current time on each button click.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d18c9b5-31eb-45f0-9e64-ecab08b13bc3/2-cscs-scripting-language-for-cross-platform-development.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d18c9b5-31eb-45f0-9e64-ecab08b13bc3/2-cscs-scripting-language-for-cross-platform-development.png" sizes="100vw" caption="Changing Layout on the fly with Visual Studio Code (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d18c9b5-31eb-45f0-9e64-ecab08b13bc3/2-cscs-scripting-language-for-cross-platform-development.png'>Large preview</a>)" alt="Changing Layout on the fly with Visual Studio Code" >}}

{{% ad-panel-leaderboard %}}

## Using SQLite In CSCS

<p><a href="https://sqlite.org/">SQLite</a> is an ACID (Atomicity, Consistency, Isolation, Durability) type of a relational database, and was developed by Richard Hipp (the first version was released in 2000). In difference to other relational databases, like Microsoft SQL Server or Oracle Database, it’s embedded. (Embedded not only into the device, but also into the end program.) It’s included in the program as a very compact library, which is less than 500 KB in size. But two apps (released by the same developer) can read the same SQLite DB if the DB file path is known to both apps.</p>

<p>The advantage of SQLite is that it can be used without an extra installation on an iOS or an Android device. The disadvantage is that it obviously cannot hold as much data as a “normal” DB and also that it’s weakly typed (i.e. you can insert a string instead of an integer &mdash; it will then be converted to an integer or 0 on failure). On the other hand, the latter can be also seen as an advantage as well.</p>

<p>SQLite can be easily used from CSCS without extra import statements. Here’s a table that will help you get an overview of the main SQLite functions used in CSCS:</p>

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Command</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>SQLInit(DBName)</code></td>
      <td>Initializes a database or sets a database to be used with consequent DB statements.</td>
    </tr>
    <tr>
      <td><code>SQLDBExists(DBName)</code></td>
      <td>Checks whether the DB has been initialized. Also sets the database to be used with consequent DB statements.</td>
    </tr>
    <tr>
      <td><code>SQLQuery(query)</code></td>
      <td>Executes an SQL query (a select statement). Returns a table with records.</td>
    </tr>
    <tr>
      <td><code>SQLNonQuery(nonQuery)</code></td>
      <td>Executes an SQL non-query, e.g. an update, create or delete statement. Returns number of records affected.</td>
    </tr>
    <tr>
      <td><code>SQLInsert(tableName, columnList, data)</code></td>
      <td>Inserts passed table of data of records to the specified DB table. The <code>columnList</code> argument has the following structure: <code>colName1,colName2,…,colNameN</code></td>
    </tr>
</tbody>
</table>
<p><em>Table 1: SQLite commands in CSCS</em></p>

<p>This is how the <code>SQLInit()</code> and <code>SQLDBExists()</code> functions are typically used:</p>

<pre><code class="language-javascript">DBName = "myDB.db1";

if (!SQLDBExists(DBName)) {
  create = "CREATE TABLE [Data] (Symbol ntext, Low real,
    High real, Close real, Volume real,
    Stamp text DEFAULT CURRENT_TIMESTAMP)";
  SQLNonQuery(create);
}


SQLInit(DBName);
</code></pre>

<p>We are going to see more examples of how you can select and insert data into an SQLite database later on. I’ll show you an example of how to write stock data that has been extracted from a Web Service into a local SQLite database.</p>

## Adding Custom Functionality To CSCS

<p>In this section, we are going to see how you can extend the CSCS functionality. As an example, we are going to see the existing implementation of the CSCS Sleep function below.</p>

<p>To add custom functionality, all you need to do is create a new class by deriving from the <code>ParserFunction</code> class, overriding its <code>Evaluate()</code> method, and registering this class with the parser. Here’s a short version (without error checking):</p>

<pre><code class="language-javascript">class SleepFunction : ParserFunction
{
  protected override Variable Evaluate(ParsingScript script)
  {
    List <Variable> args = script.GetFunctionArgs();
    int sleepms = Utils.GetSafeInt(args, 0);
    Thread.Sleep(sleepms);

    return Variable.EmptyInstance;
  }
}</code></pre>

<p>Registration of a class with the parser can be done anywhere in the initialization stage via the following command:</p>

<pre><code class="language-javascript">ParserFunction.RegisterFunction("Sleep", new SleepFunction());</code></pre>

<p>That’s it! Now the <code>Evaluate()</code> method of the <code>SleepFunction</code> class will be invoked as soon as a “Sleep” token is extracted by the parser.</p>

<p>Note that CSCS is case insensitive (except the core control flow statements: <code>if</code>, <code>elif</code>, <code>else</code>, <code>for</code>, <code>while</code>, <code>function</code>, <code>include</code>, <code>new</code>, <code>class</code>, <code>return</code>, <code>try</code>, <code>throw</code>, <code>catch</code>, <code>break</code>, <code>continue</code>). This means that you can type either “sleep(100)” or “Sleep(100)” &mdash; both calls will suspend the executing thread for 100 milliseconds.</p>

{{% ad-panel-leaderboard %}}

## Processing JSON In CSCS

<p><a href="https://json.org/">JSON</a> (JavaScript Object Notation) is a lightweight data interchange format, consisting of attribute-value pairs and array-type pairs. It was developed by Douglas Crockford in the early 2000s (around same time when SQLite appeared as well).</p>

<p>In this section, we are going to learn how to parse JSON using CSCS.</p>

<p>The CSCS function to parse a JSON string is <code>GetVariableFromJSON(jsonText)</code>. This function returns a hash table in which the keys are the attributes from the JSON string.</p>

<p>Consider the following example of a JSON string:</p>

<div class="break-out">

<pre><code class="language-javascript">jsonString = '{ "eins" : 1, "zwei" : "zweiString", "mehr" : { "uno": "dos" },
               "arrayValue" : [ "une", "deux" ] }';</code></pre>
</div>

<p>After invoking:</p>

<pre><code class="language-javascript">a = GetVariableFromJSON();</code></pre>

<p>The variable <code>a</code> will be a hash table with the following values:</p>

<pre><code class="language-javascript">a["eins"] = 1
a["zwei"] = "zweiString"
a["mehr"]["uno"] = "dos"
a["arrayValue"][0] = "une"
a["arrayValue"][1] = "deux"</code></pre>

<p>In the next section, we are going to see another example of parsing a JSON string from a Web Service.</p>

## An Example Of An App With SQLite, Web Requests And JSON

<p>For an app using SQLite, a Web Service and JSON parsing, we are going to use <a href="https://www.alphavantage.co/">Alpha Vantage Web Service</a>. You can <a href="https://www.alphavantage.co/support/#api-key">get an API Key for free</a> but the free version allows accessing their web service no more than 5 times per minute.</p>

<p>Using Alpha Vantage, you can extract various financial data sets &mdash; including stock prices. This is what we are going to do in our sample app.</p>

<p>The image below shows how the Stocks apps looks on an iOS and on an Android device.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4707f6a1-58e4-45e5-9e48-211d32c23acb/3-cscs-scripting-language-for-cross-platform-development.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4707f6a1-58e4-45e5-9e48-211d32c23acb/3-cscs-scripting-language-for-cross-platform-development.png" sizes="70vw" caption="Extracting Stocks from Alpha Vantage Web Service on iOS (left) and Android (right) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4707f6a1-58e4-45e5-9e48-211d32c23acb/3-cscs-scripting-language-for-cross-platform-development.png'>Large preview</a>)" alt="Extracting Stocks from Alpha Vantage Web Service on iOS (left) and Android (right)" >}}

<p>The CSCS code to build the GUI is the following:</p>

<pre><code class="language-javascript">locLabel = GetLocation("ROOT","CENTER", "ROOT","TOP", 0,30);
AddLabel(locLabel, "labelRefresh", "", 480, 60);

locSFWidget = GetLocation("ROOT","CENTER",
                          labelRefresh,"BOTTOM");
AddSfDataGrid(locSFWidget,  "DataGrid", "",
              graphWidth, graphHeight);

listCols = {"Symbol","string",  "Low","number", "High",
            "number", "Close","number",  "Volume","number"};
AddWidgetData(DataGrid, listCols, "columns");
colWidth = {17, 19, 19, 19, 26};
AddWidgetData(DataGrid, colWidth, "columnWidth");

locButton = GetLocation("ROOT","CENTER",DataGrid,"BOTTOM");
AddButton(locButton, "buttonRefresh", "Refresh", 160, 80);

locLabelError = GetLocation("ROOT","CENTER","ROOT","BOTTOM");
AddLabel(locLabelError, "labelError", "", 600, 160);
SetFontColor(labelError, "red");
AlignText(labelError, "center");

getDataFromDB();
</code></pre>

<p>The <code>getDataFromDB()</code> method will extract all the data from the SQLite database. It uses the SQL query defined as follows:</p>

<div class="break-out">

<pre><code class="language-javascript">query = "SELECT Symbol, Low, High, Close, Volume, DATETIME(Stamp,
               'localtime') as Stamp FROM Data ORDER BY Stamp DESC LIMIT 5;";</code></pre>
</div>

<p>Take a look at the code below for the <code>getDataFromDB()</code> implementation.</p>

<pre><code class="language-javascript">function getDataFromDB() {
  results = SQLQuery(query);
  for (i = 1; i < results.Size; i++) {
    vals       = results[i];
    stock      = vals[0];
    low        = Round(vals[1], 2);
    high       = Round(vals[2], 2);
    close      = Round(vals[3], 2);
    volume     = Round(vals[4], 2);
    refresh    = vals[5];

    stockData  = {stock, low, high, close, volume};
    AddWidgetData(DataGrid, stockData, "item");
  }
  SetText(labelRefresh, "DB Last Refresh: " + refresh);
  lockGui(false);
}</code></pre>

<p>Now let’s see how we get data from the Alpha Vantage Web Service. First, we initialize the data:</p>

<pre><code class="language-javascript">baseURL     = "https://www.alphavantage.co/query? " +
              "function=TIME_SERIES_DAILY&symbol=";
apikey      = "Y12T0TY5EUS6BC5F";
stocks      = {"MSFT", "AAPL", "GOOG", "FB", "AMZN"};
totalStocks = stocks.Size;</code></pre>

<p>Next, we load stocks one by one as soon as the user clicks on the “Refresh” button:</p>

<pre><code class="language-javascript">function buttonRefresh_click(object, arg) {
  lockGui();

  SetText(labelRefresh, "Loading ...");
  SetText(labelError, "");
  ClearWidget(DataGrid);
  loadedStocks = 0;
  getData(stocks[loadedStocks]);
}

function getData(symbol) {
  stockUrl  = baseURL + symbol + "&apikey=" + apikey;
  WebRequest("GET", stockUrl, "", symbol, "OnSuccess", "OnFailure");
}</code></pre>

<p>Here’s the main CSCS function to use in order to get data from a Web Service:</p>

<pre><code class="language-javascript">WebRequest("GET", stockUrl, "", symbol, "OnSuccess", "OnFailure");</code></pre>

<p>The last two parameters are functions to invoke on completion of the web request. For example, in case of a failure, the following CSCS function will be called:</p>

<pre><code class="language-javascript">function OnFailure(object, errorCode, text)
{
  SetText(labelError, text);
  lockGui(false);
}</code></pre>

<p>As a result, the user will get an error message as shown below:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad97b6aa-b094-45cf-bf3f-07a3f0179bd3/4-cscs-scripting-language-for-cross-platform-development.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad97b6aa-b094-45cf-bf3f-07a3f0179bd3/4-cscs-scripting-language-for-cross-platform-development.png" sizes="70vw" caption="An error when requesting web data (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad97b6aa-b094-45cf-bf3f-07a3f0179bd3/4-cscs-scripting-language-for-cross-platform-development.png'>Large preview</a>)" alt="An error when requesting web data" >}}

<p>But, if all is good, we are going to parse the JSON string and insert its contents into the SQLite DB.</p>

<pre><code class="language-javascript">function OnSuccess(object, errorCode, text)
{
  jsonFromText  = GetVariableFromJSON(text);
  metaData      = jsonFromText[0];
  result        = jsonFromText[1];

  symbol        = metaData["2. Symbol"];
  lastRefreshed = metaData["3. Last Refreshed"];
  allDates      = result.keys;

  dateData   = result[allDates[0]];
  high       = Round(dateData["2. high"],  2);
  low        = Round(dateData["3. low"],   2);
  close      = Round(dateData["4. close"], 2);
  volume     = dateData["5. volume"];
  stockData  = {symbol, low, high, close, volume};
  SQLInsert("Data","Symbol,Low,High,Close,Volume",stockData);

  if (++loadedStocks >= totalStocks) {
    getDataFromDB();
  } else {
    getData(stocks[loadedStocks]);
  }
}</code></pre>

<p>In order to understand how we access different fields in the hash table above, let’s take a look at the actual string received from the Alpha Vantage web request:</p>

<div class="break-out">

<pre><code class="language-javascript">{   "Meta Data": {
        "1. Information": "Daily Prices (open, high, low, close) and Volumes",
        "2. Symbol": "MSFT",
        "3. Last Refreshed": "2019-10-02 14:23:20",
        "4. Output Size": "Compact",
        "5. Time Zone": "US/Eastern"
    },
    "Time Series (Daily)": {
        "2019-10-02": {
            "1. open": "136.3400",
            "2. high": "136.3700",
            "3. low": "133.5799",
            "4. close": "134.4100",
            "5. volume": "11213086"
        },
   …
    }
}</code></pre>
</div>

<p>As you can see, we get the latest date as the first element of the <code>allDates</code> array that consists all of the extracted dates.</p>

## Conclusion

<p>Adding CSCS to your project is easy. All you need to do is simply embed the source code of CSCS as a module to your project &mdash; just like it’s done in a <a href="https://github.com/vassilych/mobile">sample Xamarin project</a>.</p>

<p>Do you use and extend CSCS scripting language in your projects? Leave a comment below &mdash; I’d be happy to hear from you!</p>

### Further Reading

<p>If you want to explore the CSCS language a bit more, here are some of the articles I’ve written about on the topic:</p>

<ul>
  <li>“<a href="https://msdn.microsoft.com/en-us/magazine/mt573716.aspx">A Split-and-Merge Expression Parser in C#</a>,” MSDN Magazine (Oct. 2015)</li>
  <li>“<a href="https://msdn.microsoft.com/en-us/magazine/mt632273.aspx">Customizable Scripting in C#</a>,” MSDN Magazine (Feb. 2016)</li>
  <li>“<a href="https://msdn.microsoft.com/en-us/magazine/mt829272">Writing Native Mobile Apps Using a Customizable Scripting Language</a>,” MSDN Magazine (Feb. 2018)</li>
  <li>“<a href="https://github.com/vassilych/cscs">CSCS: Customized Scripting in C#</a>,” GitHub</li>
  <li>“<a href="https://www.codemag.com/Article/1711081">Developing Cross-Platform Native Apps with a Functional Scripting Language</a>,” CODE Magazine</li>
  <li>“<a href="https://www.syncfusion.com/resources/techportal/details/ebooks/implementing-a-custom-language">Implementing A Custom Language Succinctly</a>” (eBook)</li>
  <li>“<a href="https://www.syncfusion.com/ebooks/writing_native_mobile_apps_in_a_functional_language_succinctly">Writing Native Mobile Apps in a Functional Language Succinctly</a>” (eBook)</li>
</ul>

<p><em>As an additional resource, I also recommend reading how you can improve CSCS performance by <a href="https://www.codemag.com/Article/2001071">precompiling</a> its functions.</em></p>

{{< signature "ra, yk, il" >}}
