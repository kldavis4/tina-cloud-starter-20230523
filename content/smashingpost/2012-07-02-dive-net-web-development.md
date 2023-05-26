---
title: Diving Into .NET Web Development
slug: dive-net-web-development
image: null
date: 2012-07-02T12:39:02.000Z
author: craig-rowe
description: >-
  Many people think of PHP, Ruby on Rails or Python and Django when choosing a
  language to create a new website or when choosing a language to learn to get
  that exciting new job. .NET, however, seems to occupy a space somewhat apart
  from this playground of cool kids. It's always the last to be picked for team
  sports; it was shouting “Wassup!” at parties well after 2000; and it has been
  just plain left out in the cold.

  I'm not one of these people. In fact, I'm quite a fan of .NET and have found
  it great to develop with since moving away from PHP in the early days of my
  career. With its great tools, large community and broad applicability (mobile,
  Xbox, desktop and Web) it's both powerful and fun.
categories:
  - Coding
  - Essentials
---
Many people think of PHP, Ruby on Rails or Python and Django when choosing a language to create a new website or when choosing a language to learn to get that exciting new job. .NET, however, seems to occupy a space somewhat apart from this playground of cool kids. It's always the last to be picked for team sports; it was shouting “Wassup!” at parties well after 2000; and it has been just plain left out in the cold.

I'm not one of these people. In fact, I'm quite a fan of .NET and have found it great to develop with since moving away from PHP in the early days of my career. With its great tools, large community and broad applicability (mobile, Xbox, desktop and Web) it's both powerful and fun.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Upcoming Web Design Conferences](https://www.smashingmagazine.com/web-tech-front-end-ux-conferences/)
*   [Women In Web Design: Group Interview](https://www.smashingmagazine.com/2010/05/women-in-web-design-group-interview/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)

Let's be honest, though. I'm probably already playing devil's advocate. So, let's see if I can convince you, a seasoned non-.NET developer, to try it out.

{{% feature-panel %}}

If you're already a .NET developer, you might still find something new in the code sample, so I urge you to take a look.</p>

## .NET?

Let's be clear on what we mean by .NET, as opposed to IIS (which is a Windows Web server), C# (one of the .NET languages) and <abbr title="Active Server Pages">ASP Classic</abbr> (the previous interpreted ASP from back in the day). First, the decision to become a .NET developer is not necessarily a choice of language. Although the majority of developers out there work with C# and most jobs are for C#, you can also code using the .NET framework in Visual Basic (VB), F#, <a href="https://ironruby.net/">IronRuby</a>, <a href="https://ironpython.net/">IronPython</a> and others, taking advantage of the same base libraries. Admittedly, paid work for ASP.NET is mainly done with C# and VB. For fun, though, and to show how many options you have when developing on the .NET platform, the code sample below will include some of the more obscure methods of rendering a Web page using .NET.

So by “.NET,” we really mean the <strong>Common Language Runtime</strong> (CLR) (and/or the Dynamic Language Runtime for Iron* languages), which is essentially the virtual machine that the various languages accompanied by the base class libraries can run on. Frameworks are then built on top of that for Windows, Xbox, mobile and Web.</p>

### What Does This Mean?

Knowing that .NET is a runtime, we can infer that it is not inherently tied to a particular platform. Of course, the Microsoft CLR is the most common, but <a href="https://www.mono-project.com/Main_Page">Mono</a> is an open-source implementation that runs on Mac and Linux. The mono project also provides us with <a href="https://www.mono-project.com/Mod_mono">mod_mono</a> (Apache), <a href="https://ios.xamarin.com/">monotouch</a> (iPhone) and <a href="https://android.xamarin.com/">monodroid</a> (Android) as alternate platforms on which to run our C# code.

To differentiate it further, unlike scripting, interpreted per request languages such as classic ASP and PHP, C# is <a href="https://en.wikipedia.org/wiki/Compiled_language">compiled</a>. This means you don't have to worry about including files or following naming conventions and folder structures to ensure auto class loading, nor do you have to rely on modules or add-ons to provide such things as RAM-based caching. In fact, the integration goes deeper, allowing you to write modules for IIS (which is the Web server itself) in C#.

So, if you take the time to get to grips with .NET, you can <strong>take advantage of these ancillary benefits</strong>. Maybe make a game for Windows or Xbox using XNA, or make a app for Windows Phone 7 or Surface. Not to say that every .NET developer is doing these things, but by knowing C# and the wider .NET world, you can very easily jump around the ecosystem trying them out, all using the same tools and core languages and all rounding you out well as a developer.

To see examples of .NET in the wild, take a look at <a href="https://stackoverflow.com/">Stack Overflow</a>, <a href="https://www.wired.co.uk/">Wired.co.uk</a>, <a href="https://www.godaddy.com/">GoDaddy</a>, aspects of the Sims and <a href="https://unity3d.com/">Unity 3</a>. It's not just for big enterprise B2Bs or people who are still running IE 6. And you can work with commercial products beyond just EPiServer and Kentico. The mono projects mentioned above are open source; and so, too, are a plethora of apps (e.g. <a href="https://umbraco.com">Umbraco</a>) and libraries (often found via the <a href="https://nuget.org/">NuGet</a> package manager).

Before we get too much into advertising territory, let's be realistic. Plenty of negative opinions about .NET are out there. Some of these are myths, some are problems that have been addressed, and some are genuine problems that you'll have to balance against the pros.</p>

## Tools

Most people have heard of Visual Studio. It's pretty awesome. Yes, you do have to pay for it, but you can also get a <a href="https://www.microsoft.com/visualstudio/en-us/products/2010-editions/visual-web-developer-express">free version</a>. In fact, you can get it pretty easily using the <a href="https://www.microsoft.com/web/downloads/platform.aspx">Web Platform Installer</a>, which will also install the IIS Express Web server and a SQL Server Express database if needed. (“Express” means “small-scale” and “free” in the world of Microsoft.)

If you want the full versions but don't want to pay, then consider applying to <a href="https://www.microsoft.com/bizspark/About/Default.aspx">Microsoft BizSpark</a> (or, if you're a student, <a href="https://www.dreamspark.com/">DreamSpark</a>). You’ll get access to the Microsoft stack for free for three years (after which, your business will be thriving and you can pay for it, or else it's not and you’ll <del>pay a $100 exit fee</del> <a href="https://www.microsoft.com/bizspark/about/Graduation.aspx">graduate</a>). But to be honest, you probably won't need it, particularly in the early days or if you're a hobbyist.

Of course, these are all Windows tools. If you're not on Windows, then you might opt for <a href="https://monodevelop.com/">Mono Develop</a>.

You could even go half and half: running VS as your IDE, coding in C#, but connecting to a MySQL or Postgres database. Nothing stops you, and support is available. This will even save you from having to consider the cost of production SQL server licenses.</p>

## Servers And Hosting

The Microsoft tax comes back to bite us here. But it doesn't amount to a huge difference in cost. For example, for a <a href="https://www.memset.com/dedicated-servers/virtual.php">VPS with the UK hosting provider Memset</a>, a Windows box is £4 per month more than a Linux one. And the Microsoft website lists <a href="https://www.microsoft.com/web/hosting/home">other hosts</a>. Of course, you could go with Linux hosting, get yourself a VPS and configure mod_mono for your website.

What will hurt your wallet is licensing standard editions of SQL server. With this, you'll have to <strong>balance the pros and cons</strong> of tight integration with the rest of the Microsoft ecosystem. You may, for example, go with the half-and-half approach to save on costs if you aren't eligible for licensing discounts or if you are not happy with the restrictions put on SQL Express (such as the number of processors, RAM, etc).</p>

## A Brief Interlude

### Is Mono Really an Option?

Mono has been around for a long time, but Microsoft doesn't support it in the same way that it supports its own platform. Additionally it is usually slightly behind the C# developments coming out of Microsoft because the team has to catch up. The Mono website lists the areas of <a href="https://www.mono-project.com/Compatibility">compatibility</a> between the two. As you can see, the amount of coverage is large.

Finding shared hosts that provide for Mono might be hard, so you could find yourself configuring it on a VPS manually.</p>

## Actual Coding?

This is where we really get into some of the myths surrounding .NET. In my experience, many Web developers have a very negative perception it:

*   Bloated markup,
*   Lack of control over element IDs,
*   Large base 64-encoded form elements,
*   One form to rule them all,
*   An odd paradigm that mirrors Windows development.

However, many of these issues actually apply to <a href="https://www.asp.net/web-forms">ASP.NET Web forms</a>, which, although joined only recently by ASP.NET MVC (and even more recently by the <a href="https://www.asp.net/web-api">Web API</a> in MVC4), was never the only platform for serving Web pages using the ASP.NET base libraries. Not only are there mini frameworks out there, but you could use “Web forms” and just implement some of your HTML output and templates in another way; for example, with XSLT. Or you could even stick with Web forms but use libraries, such as the CSS control adapters, or restrict yourself to repeaters as opposed to grid views, etc. In fact, with the relatively recent <a href="https://weblogs.asp.net/scottgu/archive/2010/03/30/cleaner-html-markup-with-asp-net-4-web-forms-client-ids-vs-2010-and-net-4-0-series.aspx">additions to WebForms</a>, we are seeing efforts to address these markup concerns.

This may not mean a lot to you if you haven't used those systems, and I don't want to get into it too much. The bloated markup was <strong>a sign of over-reliance on “controls”</strong>, where the final HTML was effectively hidden from the developer, and extras such as <code>viewstate</code> were added to mask the stateless nature of the Web. The paradigm itself was quite different from “normal Web development,” with a very desktop-style event-based approach: server-side <code>button_click</code> events, etc. This was useful for Windows developers who were migrating, but it often made Web developers, including me, balk.

The demo below uses an ASP.NET MVC project, but be aware that some of those old prejudices against using the Microsoft stack could be a more narrow dislike of old Web forms, rather than of C# or .NET generally.

## Finally, The Example

Rather than patronize you with a step-by-step guide to installing tools using a GUI (the Web platform installer), I've created a sample project that you can access via GitHub. There is no data access (that topic could cover a whole series of articles). The aim is to give you a taste of ASP.NET pages, to show your range of options, and to provide a look at the code layout and tools so that you can try things out for yourself.</p>

### Tooling Up Your Development Machine

The easiest way is to get your hands on the following:

*   Windows
*   The [Web platform installer](https://www.microsoft.com/web/downloads/platform.aspx)
    *   Install “Visual Web Developer 2010 Express” or a Visual Studio 2010 trial (note that there are different Expresses, such as an [Express for Phone](https://www.microsoft.com/visualstudio/en-us/products/2010-editions/windows-phone-developer-tools)).
    *   Install “ASP.NET MVC 3 (Visual Studio 2010).”
*   If you want to run the IronPython demo, then you will also need to install [IronPython](https://ironpython.net/)
*   If you want to play with the F# examples (and you are using Express, rather than a trial or standard edition Visual Studio), then you will need these:
    *   Visual Studio 2010 Shell
    *   [The most recent F# CTP](https://www.microsoft.com/download/en/details.aspx?id=11100)

Pull the project from the <a href="https://github.com/cargowire/dotnetdev">demo page</a> and open it in your newly installed Visual Studio IDE. You should see something like this:

<img class="115578" title="DotNetDev in Visual Web Developer Express" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b33e6e-ae91-4563-bf5f-b3ac3bb5adac/dotnetdevsolutionexpress.png" alt="Screenshot of the demo project open in Visual Studio Web Developer Express" width="334" height="220" /><br>
<em>The DotNetDev project in Visual Web Developer Express</em>

<img class="115579" title="DotNetDev open in Visual Studio Standard" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d002c28d-fd14-48fb-aabf-963682243f03/dotnetdevsolution.png" alt="Screenshot of the demo project open in Visual Studio Standard" width="368" height="381" /><br>
<em>The DotNetDev project open in Visual Studio Standard</em>

The only difference between the two is that I've used a feature of the paid for Visual Studio to add “Solution” folders for readability.

If you want to see the demo code running, I've put a copy of it on my server. As you'll see, the demo pages include additional notes and highlighted code sections to explain the inner workings.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/021ef775-14f9-4671-adaf-f33b4cb1a9e3/dotnetdev-screenshot.png"><img class="119053" title="Screenshot of DotNetDev running in Chrome" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/021ef775-14f9-4671-adaf-f33b4cb1a9e3/dotnetdev-screenshot.png" alt="" width="400" height="324" /></a><br>
<em>DotNetDev C# MVC example running in Chrome</em>

Although the code looks like a lot here, the examples are extremely simple. In fact, each Web project simply outputs a classic “Hello world” phrase. However, each project uses either a different language or framework for the task. Hopefully, this should give you some insight into the options available to you.

If you want to immediately run any of the examples, simply right-click on the project that you want to run and choose <code>Debug → Start new instance</code>. Visual Studio will launch the website in your default browser, powering the code with the built-in Web server that comes bundled with Visual Studio (you will also see this little server running in your system tray).</p>

## Notes On The Examples

### ASP.NET MVC C# and VB (Two Separate Projects)

These two projects show the most well-known and most used methods of website creation in the .NET framework.

The following are the two key areas in the non-database-driven ASP.NET MVC (C# code shown):

<strong>1. Routes</strong> (<a href="https://github.com/cargowire/DotNetDev/blob/master/src/DotNetDev.Mvc.CSharp.Web/Global.asax.cs">Global.asax</a>)

<pre><code class="language-javascript">routes.MapRoute(
    "Default", // Route name
    "{controller}/{action}/{id}", // URL with parameters
    new { controller = "Message", action = "Index", id = UrlParameter.Optional } // Parameter defaults
  );</code></pre>

This is the initial entry point of the website. With some simple pattern matching of URL strings, we can transpose a request to an instance of a controller and an action method upon that controller. Additional parameters relate directly to those required by the method. For example, <code>{controller}/{action}/{id}</code> will work for <code>/messages/edit/1</code> (i.e. message controller → edit action → sending 1 as the ID parameter to the method) or <code>products/index</code> (i.e. products controller → index action).

<strong>2. Controllers</strong> (<a href="https://github.com/cargowire/dotnetdev/blob/master/src/DotNetDev.Mvc.CSharp.Web/Controllers/MessageController.cs">MessageController.cs</a>)

<pre><code class="language-javascript">public class MessageController : Controller
    {
        public ActionResult Index()
        {
            return View(new Message { Text = "Hello C# ASP.NET MVC World!" });
        }
    }</code></pre>

The MessageController is an IController class instantiated by the ASP.NET engine per request when the above route is matched. A method matching the action name will be called.

<strong>3. View Models</strong> (<a href="https://github.com/cargowire/dotnetdev/blob/master/src/DotNetDev.Mvc.CSharp.Web/ViewModels/Message.cs">Message.cs</a>)

<pre><code class="language-javascript">public class Message
    {
        public string Text { get; set; }
    }</code></pre>

Although passing data to a view via a dictionary (the ViewBag) is possible, it is generally considered a better practice to package up the data that is required by a particular view into a “View Model,” used as a transfer object between the model and template.

<strong>4. Views</strong> (<a href="https://github.com/cargowire/DotNetDev/blob/master/src/DotNetDev.Mvc.CSharp.Web/Views/Message/Index.cshtml">index.cshtml</a>)

<pre><code class="language-markup tmp-xml">@model Message

&lt;h2&gt;Dot Net Dev&lt;/h2&gt;

@Model.Text</code></pre>

The templating engine used in these examples is known as <a href="https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx">Razor</a>. The approach of Razor is to have minimal impact on the code. The <code>@</code> symbol is used to denote the beginning of code. If followed by a view model variable, it will be outputted to the HTML.</p>

### F#

<pre><code class="language-javascript">open System
open System.Web.Mvc

open DotNetDev.Mvc.FSharp.ViewModels

[&lt;HandleError&gt;]
type MessageController() =
  inherit Controller()

  member x.Index() =
    x.ViewData.Model &lt;- new Message "Hello F# ASP.NET MVC World!"
    x.View()</code></pre>

The <a href="https://github.com/cargowire/DotNetDev/tree/master/src/DotNetDev.Mvc.FSharp.Web/">F# example</a> shows a slightly different take on the .NET framework. In this case, the functional F# language (often used in the financial sector) is used to define the routes, controllers and models in a <a href="https://github.com/cargowire/DotNetDev/tree/master/src/DotNetDev.Mvc.FSharp.Web/">class library project</a>. To be fair, the example used here is simple enough (as is my knowledge of F#) that the code is still reasonably imperative.

Also, note that the F# example shows how F# and C# can be used together, allowing you to, if appropriate and useful, use libraries of each in the other.

One point to note if you are trying to run this example via Web Developer Express is that F# library projects are not supported. However, you can use the also free VS2010 Shell and F# CTP to view the source, compile it and then run the Web project (DotNetDev.Mvc.FSharp.Web) from Express itself using that compiled library.</p>

### IronPython

<pre><code class="language-markup tmp-python">class MessageController(Controller) :
    def __init__(self):
        self.ActionInvoker = DynamicActionInvoker(self)
    def Index(self):
        return self.View("index", Message("Hello IronPython ASP.NET MVC World!"))</code></pre>

The IronPython example shows how the DLR can be used to execute Python code from within a .NET application. The <a href="https://github.com/cargowire/DotNetDev/blob/master/src/DotNetDev.Mvc.IronPython.Web/Controllers/PythonControllers.py">PythonControllers.py</a> file contains all of the Python code needed to do this. Again, as with F#, multiple languages can work together in a .NET project.

Experienced .NET developers might be interested to look at the implementation of the DynamicActionInvoker that I'm using, which allows the use of dynamic controllers to serve the request (where traditional reflection to find the controller method would fail).</p>

### C# Using the Nancy Framework

The final example shows that we don't need to use Microsoft's framework(s) to render a website using C#. Here, I'm using the minimalist <a href="https://github.com/NancyFx/Nancy">Nancy framework</a> (inspired by Ruby's Sinatra), one of a number of open-source .NET Web frameworks.

Almost all of the Nancy example is contained within the following <a href="https://github.com/cargowire/DotNetDev/blob/master/src/DotNetDev.Nancy.CSharp.Web/MessageModule.cs">code snippet</a>:

<pre><code class="language-javascript">public MessageModule()
  : base("/")
{
  Get["/"] = x =&gt;
  {
    dynamic model = new Message { Text = "Hello Nancy World!" };
    return View["message_index.cshtml", model];
  };
}</code></pre>

Here, we can see the route pattern being defined and matched to a method in the same line, using a C# <a href="https://secure.wikimedia.org/wikipedia/en/wiki/Lambda_%28programming%29">lambda</a> (or inline anonymous function) assigned to a dictionary in the message module. This means that when a <code>GET</code> request comes in for <code>/</code>, the function body gets executed, and all it does is create a Message model, assign it to a dynamic variable and return it with the view’s name.

#### An Aside

The Nancy example also shows another useful feature of .NET. If you are used to tools such as PEAR, then you will be aware of the concept of package management. Essentially, using <code>[project] right click → Manage NuGet Packages</code> from Visual Studio, you will be able to search online through a myriad of open-source and free libraries to use in your projects. In this case, I've used Andreas Hakansson et al's Nancy Web framework.</p>

## Some Context (Headscape)

This article has been a bit of a whistle stop tour through the .NET ecosystem. The intention was to ground experienced developers in what .NET is about, at least from my perspective, enticing you to make small changes to the sample code to see how you fare. Although I'm not suggesting that you make your controllers in IronPython or F#, hopefully I've shown how easily these languages can be used in a .NET project, whether it be to reuse some existing logic or to take a more dynamic or functional approach to an aspect of your work. It should also now be clear that .NET is embracing open source. Not only do some of <a href="https://weblogs.asp.net/scottgu/archive/2012/03/27/asp-net-mvc-web-api-razor-and-open-source.aspx">its own offerings carry open-source licenses</a>, but the default MVC project includes jQuery and Modernizr, and people are contributing frameworks and applications.

To give some context to all of this, I work as the lead back-end developer at <a href="https://www.headscape.co.uk">Headscape</a>, a design and development agency in the south of England. Although I wouldn't identify ourselves as a “.NET house,” we do use it extensively, having grown from using ASP Classic to using the technologies that Microsoft grew it into. We even started out using the free Express editions of the tools. Our projects over time have been created in Web forms, VB and C#, but we do not shy away from using other technologies. We also use WordPress, Magento and other non-.NET projects. Playing around in the .NET ecosystem, however, has enabled me to have a go at XNA game development, to play with Python in a framework that I already know, and to look into mobile development in my downtime.

Please do run the code, play with it, check out the full demo (with additional notes on how this stuff all works), and let me know what you think.</p>

### Resources

*   DotNetDev The running demo
*   [DotNetDev on GitHub](https://github.com/cargowire/dotnetdev) The source code
*   [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) The tools
*   [Microsoft BizSpark](https://www.microsoft.com/bizspark/About/Default.aspx) The licenses
*   [IronPython](https://ironpython.net/)
*   [The Mono Project](https://www.mono-project.com/)

<em>(al) (km) (jc)</em>

