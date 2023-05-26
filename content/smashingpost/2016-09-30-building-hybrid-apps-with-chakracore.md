---
title: Building Hybrid Apps With ChakraCore
slug: building-hybrid-apps-with-chakracore
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aac7bdb1-9e76-4a93-a92e-1aaf2c8a676b/hyprid-apps-with-chakracore-preview-opt.png
date: 2016-09-30T14:02:53.000Z
author: ericrozell
description: >-
  There are many reasons why one may want to embed JavaScript capabilities into
  an app. One example may be to take a dependency on a JavaScript library that
  has not yet been ported to the language you’re developing in. Another may be
  that you want to allow users to “eval” small routines or functions in
  JavaScript, e.g., in data processing applications.

  The key reason for our investigation of ChakraCore was to support the React
  Native framework on the Universal Windows Platform, which is a framework for
  declaring applications using JavaScript and the React programming model.
categories:
  - Mobile
  - JavaScript
  - React
---
There are many reasons to embed JavaScript capabilities into an app. One example may be to take a dependency on a JavaScript library that has not yet been ported to the language you’re developing in. Another reason could be your desire to allow users to <code>eval</code> small routines or functions in JavaScript, e.g., in data processing applications.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/062514cd-2abe-4f73-91bc-73f327fedc37/hybrid-apps-chakra-core.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/062514cd-2abe-4f73-91bc-73f327fedc37/hybrid-apps-chakra-core.png" alt="A detailed overview on how Hybrid Apps communicate with Windows, the Browser, and the JRST Hosting API" width="500" height="370" /></a><figcaption>ChakraCore is the core part of the JavaScript engine that powers Microsoft Edge and Windows apps written in HTML/CSS/JS. It supports Just-in-time (JIT) compilation of JavaScript, garbage collection, as well as the JavaScript Runtime (JSRT) APIs, which allows you to easily embed ChakraCore in your applications.</figcaption></figure>

<a href="https://github.com/microsoft/ChakraCore">ChakraCore</a> provides a high performance JavaScript engine that powers the <a href="https://www.microsoft.com/en-us/windows/microsoft-edge#0ucTUyKhi5gAggww.97">Microsft Edge browser</a> and Windows applications written with <a href="https://developer.microsoft.com/en-us/windows/develop/winjs">WinJS</a>. The key reason for our investigation of ChakraCore was to support the React Native framework on the Universal Windows Platform, a framework for declaring applications using JavaScript and the <a href="https://facebook.github.io/react/">React</a> programming model.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Learning JavaScript: Essentials And Guidelines](https://www.smashingmagazine.com/learning-javascript-essentials-guidelines-tutorials/)
*   [Inside Microsoft’s New Rendering Engine For The “Project Spartan”](https://www.smashingmagazine.com/2015/01/inside-microsofts-new-rendering-engine-project-spartan/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [A Beginner’s Guide To jQuery-Based JSON API Clients](https://www.smashingmagazine.com/2012/02/beginners-guide-jquery-based-json-api-clients/)

{{% feature-panel %}}

## Hello, ChakraCore

Embedding ChakraCore in a C# application is quite easy. To start, grab a copy of the JavaScript runtime wrapper from <a href="https://github.com/Microsoft/Chakra-Samples/tree/master/ChakraCore%20Samples/JSRT%20Hosting%20Samples/C%23/ChakraCoreHost/Hosting">GitHub</a>. Include this code directly in your project or build your own library dependency out of it, whichever better suits your needs. There is also a very simple <a href="https://github.com/Microsoft/Chakra-Samples/blob/master/ChakraCore%20Samples/Hello%20World/Windows/C%23/HelloWorld/HelloWorld.cs">console application</a> that shows how to evaluate JavaScript source code and convert values from the JavaScript runtime into C# strings.</p>

## Building Apps With ChakraCore

There are a few extra steps involved when building C# applications with ChakraCore embedded. As of the time of writing, there are no public binaries for ChakraCore. But don't fret. Building ChakraCore is as easy as this:

1.  Clone the [ChakraCore Git repository](https://github.com/microsoft/ChakraCore).
2.  Open the [solution](https://github.com/microsoft/ChakraCore/blob/master/Build/Chakra.Core.sln) in Visual Studio (VS 2015 and the Windows 10 SDK are required if you wish to build for ARM).
3.  Build the solution from Visual Studio.
4.  The build output will be placed in `Build\VcBuild\bin` relative to your Git root folder.

If you wish to build from the command line, open up a Developer Command Prompt for Visual Studio, navigate to the Git root folder for ChakraCore, and run:

<pre><code class="language-js">msbuild Build\Chakra.Core.sln /p:Configuration=Debug /p:Platform=x86</code></pre>

You’ll want to replace the Configuration and Platform parameters with the proper settings for your build.

Now that you have a version of ChakraCore.dll, you have some options for how to ship it with your application. The simplest way is to just copy and paste the binary into your build output folder. For convenience, I drafted a simple MSBuild target to include in your .csproj to automatically copy these binaries for you each time you build:

<pre><code class="language-markup">&lt;Target Name="AfterBuild"&gt;
  &lt;ItemGroup&gt;
    &lt;ChakraDependencies Include="$(ReferencesPath)\ChakraCore.*" /&gt;
  &lt;/ItemGroup&gt;
  &lt;Copy SourceFiles="@(ChakraDependencies)" DestinationFolder="$(OutputPath) " /&gt;
&lt;/Target&gt;</code></pre>

For those who don’t speak MSBuild, one of the MSBuild conventions is to run targets in your project named <code>AfterBuild</code> after the build is complete. The above bit of XML roughly translates to “after the build is complete, search the references path for files that match the pattern ChakraCore.* and copy those files to the output directory.” You’ll need to set the <code>$(ReferencesPath)</code> property in your .csproj as well.

If you are building your application for multiple platforms, it helps to drop the ChakraCore.dll dependencies in folder names based off of your build configuration and platform. E.g., consider the following structure:

<pre><code>├── References
    ├── x86
        ├── Debug
            ├── ChakraCore.dll
            ├── ChakraCore.pdb
        ├── Release
            ├── ...
    ├── x64
        ├── ...
    ├── ARM
        ├── ...</code></pre>

That way you can declare the MSBuild property <code>$(ReferencesPath)</code> based on your build properties, e.g.

<pre><code class="language-js">References\$(Configuration)\$(Platform)\</code></pre>

## JavaScript Value Types In ChakraCore

The first step to building more complex applications with ChakraCore is understanding the data model. JavaScript is a dynamic, untyped language that supports first-class functions. The data model for JavaScript values in ChakraCore supports these designs. Here are the value types supported in Chakra:

*   `Undefined`,
*   `Null`,
*   `Number`,
*   `String`,
*   `Boolean`,
*   `Object`,
*   `Function`,
*   `Error`,
*   `Array`.</p>

### String Conversion With Serialization and Parsing

There are a number of ways of marshalling data from the CLR to the JavaScript runtime. A simple way is to parse and serialize the data as a JSON string once it enters the runtime, as follows:

<pre><code class="language-js">var jsonObject = JavaScriptValue.GlobalObject.GetProperty(
    JavaScriptPropertyId.FromString("JSON"));
    var stringify = jsonObject.GetProperty(
    JavaScriptPropertyId.FromString("stringify"))
    var parse = jsonObject.GetProperty(
    JavaScriptPropertyId.FromString("parse"));

    var jsonInput = @"{""foo"":42}";
    var stringInput = JavaScriptValue.FromString(jsonInput);
    var parsedInput = parse.CallFunction(JavaScriptValue.GlobalObject, stringInput);
    var stringOutput = stringify.CallFunction(JavaScriptValue.GlobalObject, parsedInput);
    var jsonOutput = stringOutput.ToString();

Debug.Assert(jsonInput == jsonOutput);</code></pre>

In the above code, we marshal the JSON data, <code>{"foo":42}</code> into the runtime as a string and, parse the data using the <code>JSON.parse</code> function. The result is a JavaScript object, which we use as input to the <code>JSON.stringify</code> function, then use the <code>ToString()</code> method on the result value to put the result back into a .NET string. Obviously, the idea would be to use the <code>parsedInput</code> object as an input to your logic running in Chakra, and apply the stringify function only when you need to marshal data back out.</p>

### Direct Object Model Conversion (With Json.NET)

An alternative approach to the string-based approach in the previous section would be to use the Chakra native APIs to construct the objects directly in the JavaScript runtime. While you can choose whatever JSON data model you desire for your C# application, we chose <a>Json.NET</a> due to its popularity and performance characteristics. The basic outcome we are looking for is a function from JavaScriptValue (the Chakra data model) to JToken (the Json.NET data model) and the inverse function from JToken to JavaScriptValue. Since JSON is a tree data structure, a recursive visitor is a good approach for implementing the converters.

Here is the logic for the visitor class that converts values from JavaScriptValue to JToken:

<pre><code class="language-js">public sealed class JavaScriptValueToJTokenConverter
{
    private static readonly JToken s_true = new JValue(true);
    private static readonly JToken s_false = new JValue(false);
    private static readonly JToken s_null = JValue.CreateNull();
    private static readonly JToken s_undefined = JValue.CreateUndefined();

    private static readonly JavaScriptValueToJTokenConverter s_instance =
        new JavaScriptValueToJTokenConverter();

    private JavaScriptValueToJTokenConverter() { }

    public static JToken Convert(JavaScriptValue value)
    {
        return s_instance.Visit(value);
    }

    private JToken Visit(JavaScriptValue value)
    {
        switch (value.ValueType)
        {
            case JavaScriptValueType.Array:
                return VisitArray(value);
            case JavaScriptValueType.Boolean:
                return VisitBoolean(value);
            case JavaScriptValueType.Null:
                return VisitNull(value);
            case JavaScriptValueType.Number:
                return VisitNumber(value);
            case JavaScriptValueType.Object:
                return VisitObject(value);
            case JavaScriptValueType.String:
                return VisitString(value);
            case JavaScriptValueType.Undefined:
                return VisitUndefined(value);
            case JavaScriptValueType.Function:
            case JavaScriptValueType.Error:
            default:
                throw new NotSupportedException();
        }
    }

    private JToken VisitArray(JavaScriptValue value)
    {
        var array = new JArray();
        var propertyId = JavaScriptPropertyId.FromString("length");
        var length = (int)value.GetProperty(propertyId).ToDouble();
        for (var i = 0; i &lt; length; ++i)
        {
            var index = JavaScriptValue.FromInt32(i);
            var element = value.GetIndexedProperty(index);
            array.Add(Visit(element));
        }

        return array;
    }

    private JToken VisitBoolean(JavaScriptValue value)
    {
        return value.ToBoolean() ? s_true : s_false;
    }

    private JToken VisitNull(JavaScriptValue value)
    {
        return s_null;
    }

    private JToken VisitNumber(JavaScriptValue value)
    {
        var number = value.ToDouble();

        return number % 1 == 0
            ? new JValue((long)number)
            : new JValue(number);
    }

    private JToken VisitObject(JavaScriptValue value)
    {
        var jsonObject = new JObject();
        var properties = Visit(value.GetOwnPropertyNames()).ToObject();
        foreach (var property in properties)
        {
            var propertyId = JavaScriptPropertyId.FromString(property);
            var propertyValue = value.GetProperty(propertyId);
            jsonObject.Add(property, Visit(propertyValue));
        }

        return jsonObject;
    }

    private JToken VisitString(JavaScriptValue value)
    {
        return JValue.CreateString(value.ToString());
    }

    private JToken VisitUndefined(JavaScriptValue value)
    {
        return s_undefined;
    }
}</code></pre>

And here is the inverse logic from JToken to JavaScript value:

<pre><code class="language-js">public sealed class JTokenToJavaScriptValueConverter
{
    private static readonly JTokenToJavaScriptValueConverter s_instance =
        new JTokenToJavaScriptValueConverter();

    private JTokenToJavaScriptValueConverter() { }

    public static JavaScriptValue Convert(JToken token)
    {
        return s_instance.Visit(token);
    }

    private JavaScriptValue Visit(JToken token)
    {
        if (token == null)
            throw new ArgumentNullException(nameof(token));

        switch (token.Type)
        {
            case JTokenType.Array:
                return VisitArray((JArray)token);
            case JTokenType.Boolean:
                return VisitBoolean((JValue)token);
            case JTokenType.Float:
                return VisitFloat((JValue)token);
            case JTokenType.Integer:
                return VisitInteger((JValue)token);
            case JTokenType.Null:
                return VisitNull(token);
            case JTokenType.Object:
                return VisitObject((JObject)token);
            case JTokenType.String:
                return VisitString((JValue)token);
            case JTokenType.Undefined:
                return VisitUndefined(token);
            default:
                throw new NotSupportedException();
        }
    }

    private JavaScriptValue VisitArray(JArray token)
    {
        var n = token.Count;
        var array = AddRef(JavaScriptValue.CreateArray((uint)n));
        for (var i = 0; i &lt; n; ++i)
        {
            var value = Visit(token[i]);
            array.SetIndexedProperty(JavaScriptValue.FromInt32(i), value);
            value.Release();
        }

        return array;
    }

    private JavaScriptValue VisitBoolean(JValue token)
    {
        return token.Value()
            ? JavaScriptValue.True
            : JavaScriptValue.False;
    }

    private JavaScriptValue VisitFloat(JValue token)
    {
        return AddRef(JavaScriptValue.FromDouble(token.Value()));
    }

    private JavaScriptValue VisitInteger(JValue token)
    {
        return AddRef(JavaScriptValue.FromDouble(token.Value()));
    }

    private JavaScriptValue VisitNull(JToken token)
    {
        return JavaScriptValue.Null;
    }

    private JavaScriptValue VisitObject(JObject token)
    {
        var jsonObject = AddRef(JavaScriptValue.CreateObject());
        foreach (var entry in token)
        {
            var value = Visit(entry.Value);
            var propertyId = JavaScriptPropertyId.FromString(entry.Key);
            jsonObject.SetProperty(propertyId, value, true);
            value.Release();
        }

        return jsonObject;
    }

    private JavaScriptValue VisitString(JValue token)
    {
        return AddRef(JavaScriptValue.FromString(token.Value()));
    }

    private JavaScriptValue VisitUndefined(JToken token)
    {
        return JavaScriptValue.Undefined;
    }

    private JavaScriptValue AddRef(JavaScriptValue value)
    {
        value.AddRef();
        return value;
    }
}</code></pre>

As with any recursive algorithm, there are base cases and recursion steps. In this case, the base cases are the “leaf nodes” of the JSON tree (i.e., undefined, null, numbers, Booleans, strings) and the recursive steps occur when we encounter arrays and objects.

The goal of direct object model conversion is to lessen pressure on the garbage collector as serialization and parsing will generate a lot of intermediate strings. Bear in mind that your choice of .NET object model for JSON (Json.NET in the examples above) may also have an impact on your decision to use the direct object model conversion method outlined in this section or the string serialization / parsing method outlined in the previous section. If your decision is based purely on throughput, and your application is not GC-bound, the string-marshaling approach will outperform the direct object model conversion (especially with the back-and-forth overhead from native to managed code for large JSON trees).

You should evaluate the performance impact of either approach on your scenario before choosing one or the other. To assist in that investigation, I’ve published a simple tool for calculating throughput and garbage collection impact for both the CLR and Chakra on <a href="https://github.com/rozele/ChakraDataMarshaling">GitHub</a>.

## ChakraCore Threading Requirements

The ChakraCore runtime is single-threaded in the sense that only one thread may have access to it at a time. This does not mean, however, that you must designate a thread to do all the work on the JavaScriptRuntime (although it may be easier to do so).

Setting up the JavaScript runtime is relatively straightforward:

<pre><code class="language-js">var runtime = JavaScriptRuntime.Create();</code></pre>

Before you can use this runtime on any thread, you must first set the context for a particular thread:

<pre><code class="language-js">var context = runtime.CreateContext();
    JavaScriptContext.Current = context;</code></pre>

When you are done using that thread for JavaScript work for the time being, be sure to reset the JavaScript context to an invalid value:

<pre><code class="language-js">JavaScriptContext.Current = JavaScriptContext.Invalid;</code></pre>

At some later point, on any other thread, simply recreate or reassign the context as above. If you attempt to assign the context simultaneously on two different threads for the same runtime, ChakraCore will throw an exception like this:

<pre><code class="language-js">var t1 = Task.Run(() =&gt;
{
    JavaScriptContext.Current = runtime.CreateContext();
    Task.Delay(1000).Wait();
    JavaScriptContext.Current = JavaScriptContext.Invalid;
});

    var t2 = Task.Run(() =&gt;
{
    JavaScriptContext.Current = runtime.CreateContext();
    Task.Delay(1000).Wait();
    JavaScriptContext.Current = JavaScriptContext.Invalid;
});

    Task.WaitAll(t1, t2);</code></pre>

While it is appropriate to throw an exception, nothing should prevent you from using multiple threads concurrently for two different runtimes. Similarly, if you attempt to dispose the runtime without first resetting the context to an invalid value, ChakraCore will throw an exception notifying that the runtime is in use:

<pre><code class="language-js">using (var runtime = JavaScriptRuntime.Create())
{
    var context = runtime.CreateContext();
    JavaScriptContext.Current = context;
}</code></pre>

If you encounter the “runtime is in use” exception that stems from disposing the runtime before unsetting the context, double check your JavaScript thread activity for any asynchronous behavior. The way async/await works in C# generally allows for any thread from the thread pool to carry out a continuation after the completion of an asynchronous operation. For ChakraCore to function properly, the context must be unset by the exact same physical thread (not logical thread) that set it initially. For more information, consult the Microsoft Developer Network site on <a href="https://msdn.microsoft.com/en-us/library/dd537609.aspx">Task Parallelism</a>.</p>

### Thread Queue Options

In our implementation of the React Native on Windows, we considered a few different approaches to ensuring all JavaScript operations were single threaded. React Native has three main threads of activity, the UI thread, the background native module thread, and the JavaScript thread. Since JavaScript work can originate from either the native module thread or the UI thread, and generally speaking each thread does not block waiting for completion of activity on any other thread, we also have the requirement of implementing a FIFO queue for the JavaScript work.</p>

### ThreadPool Thread Capture

One of the options we considered was to block a thread pool thread permanently for evaluating JavaScript operations. Here’s the sample code for that:

<pre><code class="language-js">// Initializes the thread queue
var queue = new BlockingCollection();
var asyncAction = ThreadPool.RunAsync(
    _ =&gt;
    {
        JavaScriptContext.Current = context;

        while (true)
        {
            var action = queue.Take();
            if (... /* Check disposal */) break;

            try { action(); }
            catch (Exception ex) { ... /* Handle exceptions */ }
        }

        JavaScriptContext.Current = JavaScriptContext.Invalid;
    },
    WorkItemPriority.Normal);

// Enqueues work
queue.Add(() =&gt; JavaScriptContext.RunScript(... /* JavaScript */);</code></pre>

The benefit to this approach is its simplicity in that we know a single thread is running all of the JavaScript operations. The detriment is that we’re permanently blocking a thread pool thread, so it cannot be used for other work.</p>

### Task Scheduler

Another approach we considered uses the .NET framework’s <a href="https://msdn.microsoft.com/en-us/library/system.threading.tasks.taskscheduler.aspx">TaskScheduler</a>. There are a few ways to create a task scheduler that limits concurrency and guarantees FIFO, but for simplicity, we use <a href="https://msdn.microsoft.com/en-us/library/ee789351.aspx">this one from MSDN</a>.</p>

<pre><code class="language-js">// Initializes the thread queue
    var taskScheduler =
     new LimitedConcurrencyLevelTaskScheduler(1);
    var taskFactory = new TaskFactory(taskScheduler);

// Enqueues work
    taskFactory.StartNew(() =&gt;
{
    if (... /* Check disposed */) return;
    try { JavaScriptContext.RunScript(... /* JavaScript */); }
    catch (Exception ex) { ... /* Handle exception */}
});</code></pre>

The benefit to this approach is that it does not require any blocking operations.</p>

## ChakraCore Runtime Considerations

    private JToken Visit(JavaScriptValue value)
    {
        switch (value.ValueType)
        {
            case JavaScriptValueType.Array:
                return VisitArray(value);
            case JavaScriptValueType.Boolean:
                return VisitBoolean(value);
            case JavaScriptValueType.Null:
                return VisitNull(value);
            case JavaScriptValueType.Number:
                return VisitNumber(value);
            case JavaScriptValueType.Object:
                return VisitObject(value);
            case JavaScriptValueType.String:
                return VisitString(value);
            case JavaScriptValueType.Undefined:
                return VisitUndefined(value);
            case JavaScriptValueType.Function:
            case JavaScriptValueType.Error:
            default:
                throw new NotSupportedException();
        }
    }

    private JToken VisitArray(JavaScriptValue value)
    {
        var array = new JArray();
        var propertyId = JavaScriptPropertyId.FromString("length");
        var length = (int)value.GetProperty(propertyId).ToDouble();
        for (var i = 0; i &lt; length; ++i)
        {
            var index = JavaScriptValue.FromInt32(i);
            var element = value.GetIndexedProperty(index);
            array.Add(Visit(element));
        }

        return array;
    }

    private JToken VisitBoolean(JavaScriptValue value)
    {
        return value.ToBoolean() ? s_true : s_false;
    }

    private JToken VisitNull(JavaScriptValue value)
    {
        return s_null;
    }

    private JToken VisitNumber(JavaScriptValue value)
    {
        var number = value.ToDouble();

        return number % 1 == 0
            ? new JValue((long)number)
            : new JValue(number);
    }

    private JToken VisitObject(JavaScriptValue value)
    {
        var jsonObject = new JObject();
        var properties = Visit(value.GetOwnPropertyNames()).ToObject();
        foreach (var property in properties)
        {
            var propertyId = JavaScriptPropertyId.FromString(property);
            var propertyValue = value.GetProperty(propertyId);
            jsonObject.Add(property, Visit(propertyValue));
        }

        return jsonObject;
    }

    private JToken VisitString(JavaScriptValue value)
    {
        return JValue.CreateString(value.ToString());
    }

    private JToken VisitUndefined(JavaScriptValue value)
    {
        return s_undefined;
    }
}</code></pre>

And here is the inverse logic from JToken to JavaScript value:

<pre><code class="language-js">public sealed class JTokenToJavaScriptValueConverter
{
    private static readonly JTokenToJavaScriptValueConverter s_instance =
        new JTokenToJavaScriptValueConverter();

    private JTokenToJavaScriptValueConverter() { }

    public static JavaScriptValue Convert(JToken token)
    {
        return s_instance.Visit(token);
    }

    private JavaScriptValue Visit(JToken token)
    {
        if (token == null)
            throw new ArgumentNullException(nameof(token));

        switch (token.Type)
        {
            case JTokenType.Array:
                return VisitArray((JArray)token);
            case JTokenType.Boolean:
                return VisitBoolean((JValue)token);
            case JTokenType.Float:
                return VisitFloat((JValue)token);
            case JTokenType.Integer:
                return VisitInteger((JValue)token);
            case JTokenType.Null:
                return VisitNull(token);
            case JTokenType.Object:
                return VisitObject((JObject)token);
            case JTokenType.String:
                return VisitString((JValue)token);
            case JTokenType.Undefined:
                return VisitUndefined(token);
            default:
                throw new NotSupportedException();
        }
    }

    private JavaScriptValue VisitArray(JArray token)
    {
        var n = token.Count;
        var array = AddRef(JavaScriptValue.CreateArray((uint)n));
        for (var i = 0; i &lt; n; ++i)
        {
            var value = Visit(token[i]);
            array.SetIndexedProperty(JavaScriptValue.FromInt32(i), value);
            value.Release();
        }

        return array;
    }

    private JavaScriptValue VisitBoolean(JValue token)
    {
        return token.Value()
            ? JavaScriptValue.True
            : JavaScriptValue.False;
    }

    private JavaScriptValue VisitFloat(JValue token)
    {
        return AddRef(JavaScriptValue.FromDouble(token.Value()));
    }

    private JavaScriptValue VisitInteger(JValue token)
    {
        return AddRef(JavaScriptValue.FromDouble(token.Value()));
    }

    private JavaScriptValue VisitNull(JToken token)
    {
        return JavaScriptValue.Null;
    }

    private JavaScriptValue VisitObject(JObject token)
    {
        var jsonObject = AddRef(JavaScriptValue.CreateObject());
        foreach (var entry in token)
        {
            var value = Visit(entry.Value);
            var propertyId = JavaScriptPropertyId.FromString(entry.Key);
            jsonObject.SetProperty(propertyId, value, true);
            value.Release();
        }

        return jsonObject;
    }

    private JavaScriptValue VisitString(JValue token)
    {
        return AddRef(JavaScriptValue.FromString(token.Value()));
    }

    private JavaScriptValue VisitUndefined(JToken token)
    {
        return JavaScriptValue.Undefined;
    }

    private JavaScriptValue AddRef(JavaScriptValue value)
    {
        value.AddRef();
        return value;
    }
}</code></pre>

As with any recursive algorithm, there are base cases and recursion steps. In this case, the base cases are the “leaf nodes” of the JSON tree (i.e., undefined, null, numbers, Booleans, strings) and the recursive steps occur when we encounter arrays and objects.

The goal of direct object model conversion is to lessen pressure on the garbage collector as serialization and parsing will generate a lot of intermediate strings. Bear in mind that your choice of .NET object model for JSON (Json.NET in the examples above) may also have an impact on your decision to use the direct object model conversion method outlined in this section or the string serialization / parsing method outlined in the previous section. If your decision is based purely on throughput, and your application is not GC-bound, the string-marshaling approach will outperform the direct object model conversion (especially with the back-and-forth overhead from native to managed code for large JSON trees).

You should evaluate the performance impact of either approach on your scenario before choosing one or the other. To assist in that investigation, I’ve published a simple tool for calculating throughput and garbage collection impact for both the CLR and Chakra on <a href="https://github.com/rozele/ChakraDataMarshaling">GitHub</a>.</p>

## ChakraCore Threading Requirements

The ChakraCore runtime is single-threaded in the sense that only one thread may have access to it at a time. This does not mean, however, that you must designate a thread to do all the work on the JavaScriptRuntime (although it may be easier to do so).

Setting up the JavaScript runtime is relatively straightforward:

<pre><code class="language-js">var runtime = JavaScriptRuntime.Create();</code></pre>

Before you can use this runtime on any thread, you must first set the context for a particular thread:

<pre><code class="language-js">var context = runtime.CreateContext();
    JavaScriptContext.Current = context;</code></pre>

When you are done using that thread for JavaScript work for the time being, be sure to reset the JavaScript context to an invalid value:

<pre><code class="language-js">JavaScriptContext.Current = JavaScriptContext.Invalid;</code></pre>

At some later point, on any other thread, simply recreate or reassign the context as above. If you attempt to assign the context simultaneously on two different threads for the same runtime, ChakraCore will throw an exception like this:

<pre><code class="language-js">var t1 = Task.Run(() =&gt;
{
    JavaScriptContext.Current = runtime.CreateContext();
    Task.Delay(1000).Wait();
    JavaScriptContext.Current = JavaScriptContext.Invalid;
});

    var t2 = Task.Run(() =&gt;
{
    JavaScriptContext.Current = runtime.CreateContext();
    Task.Delay(1000).Wait();
    JavaScriptContext.Current = JavaScriptContext.Invalid;
});

    Task.WaitAll(t1, t2);</code></pre>

While it is appropriate to throw an exception, nothing should prevent you from using multiple threads concurrently for two different runtimes. Similarly, if you attempt to dispose the runtime without first resetting the context to an invalid value, ChakraCore will throw an exception notifying that the runtime is in use:

<pre><code class="language-js">using (var runtime = JavaScriptRuntime.Create())
{
    var context = runtime.CreateContext();
    JavaScriptContext.Current = context;
}</code></pre>

If you encounter the “runtime is in use” exception that stems from disposing the runtime before unsetting the context, double check your JavaScript thread activity for any asynchronous behavior. The way async/await works in C# generally allows for any thread from the thread pool to carry out a continuation after the completion of an asynchronous operation. For ChakraCore to function properly, the context must be unset by the exact same physical thread (not logical thread) that set it initially. For more information, consult the Microsoft Developer Network site on <a href="https://msdn.microsoft.com/en-us/library/dd537609.aspx">Task Parallelism</a>.</p>

### Thread Queue Options

In our implementation of the React Native on Windows, we considered a few different approaches to ensuring all JavaScript operations were single threaded. React Native has three main threads of activity, the UI thread, the background native module thread, and the JavaScript thread. Since JavaScript work can originate from either the native module thread or the UI thread, and generally speaking each thread does not block waiting for completion of activity on any other thread, we also have the requirement of implementing a FIFO queue for the JavaScript work.</p>

### ThreadPool Thread Capture

One of the options we considered was to block a thread pool thread permanently for evaluating JavaScript operations. Here’s the sample code for that:

<pre><code class="language-js">// Initializes the thread queue
var queue = new BlockingCollection();
var asyncAction = ThreadPool.RunAsync(
    _ =&gt;
    {
        JavaScriptContext.Current = context;

        while (true)
        {
            var action = queue.Take();
            if (... /* Check disposal */) break;

            try { action(); }
            catch (Exception ex) { ... /* Handle exceptions */ }
        }

        JavaScriptContext.Current = JavaScriptContext.Invalid;
    },
    WorkItemPriority.Normal);

// Enqueues work
queue.Add(() =&gt; JavaScriptContext.RunScript(... /* JavaScript */);</code></pre>

The benefit to this approach is its simplicity in that we know a single thread is running all of the JavaScript operations. The detriment is that we’re permanently blocking a thread pool thread, so it cannot be used for other work.</p>

### Task Scheduler

Another approach we considered uses the .NET framework’s <a href="https://msdn.microsoft.com/en-us/library/system.threading.tasks.taskscheduler.aspx">TaskScheduler</a>. There are a few ways to create a task scheduler that limits concurrency and guarantees FIFO, but for simplicity, we use <a href="https://msdn.microsoft.com/en-us/library/ee789351.aspx">this one from MSDN</a>.</p>

<pre><code class="language-js">// Initializes the thread queue
    var taskScheduler =
     new LimitedConcurrencyLevelTaskScheduler(1);
    var taskFactory = new TaskFactory(taskScheduler);

// Enqueues work
    taskFactory.StartNew(() =&gt;
{
    if (... /* Check disposed */) return;
    try { JavaScriptContext.RunScript(... /* JavaScript */); }
    catch (Exception ex) { ... /* Handle exception */}
});</code></pre>

The benefit to this approach is that it does not require any blocking operations.</p>

## ChakraCore Runtime Considerations

### Garbage Collection

One of the main deterrents from using ChakraCore in conjunction with another managed language like C# is the complexity of competing garbage collectors. ChakraCore has a few hooks to give you more control over how garbage collection in the JavaScript runtime is managed. For more information, check out the documentation on <a href="https://github.com/microsoft/ChakraCore/wiki/JavaScript-Runtime-%28JSRT%29-Overview#runtime-resource-usage">runtime resource usage</a>.</p>

### Conclusion: To JIT or not to JIT?

Depending on your application, you may want to weigh the overhead of the JIT compiler against the frequency at which you run certain functions. In case you do decide that the overhead of the JIT compiler is not worth the trade-off, here’s how you can disable it:

<pre><code class="language-js">var runtime = 
    JavaScriptRuntime.Create(JavaScriptRuntimeAttributes.DisableNativeCodeGeneration);</code></pre>

The option to run the just-in-time (JIT) compiler in ChakraCore is also optional — all the JavaScript code will be fully interpreted even without the JIT compiler.</p>

### More Hands on with Web and Mobile Apps

Check out these helpful resources on building web and mobile apps:

*   [Guide to Universal Windows Platform (UWP) apps](https://msdn.microsoft.com/windows/uwp/get-started/universal-application-platform-guide/?wt.mc_id=873566&HybridAppsAppsatSM)
*   [Bring your existing code to Windows with Windows Bridges](https://developer.microsoft.com/en-us/windows/bridges/?wt.mc_id=873566&HybridAppsAppsatSM)
*   [App Development Courses and Tutorials](https://mva.microsoft.com/training-topics/app-development/?wt.mc_id=873566&HybridAppsAppsatSM#!lang=1049)
*   [C# / XAML Courses and tutorials](https://mva.microsoft.com/training-topics/c-app-development#!index=2&jobf=Developer&lang=1033/?wt.mc_id=873566&HybridAppsAppsatSM)
*   [Azure App Services](https://www.visualstudio.com/vs/mobile-app-development?wt.mc_id=873566&HybridAppsAppsatSM)

For further updates on the topic and new features, please view the original <a href="https://www.microsoft.com/developerblog/real-life-code/2016/06/03/Hybrid-Apps-Using-C-and-JavaScript-with-ChakraCore.html?wt.mc_id=873566&amp;HybridAppsAppsatSM">documentation</a>.

{{< signature "ms, at, il" >}}

