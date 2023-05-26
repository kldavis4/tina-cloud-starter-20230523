---
title: 'Getting Started With The GetX Package In Flutter Applications'
slug: getx-package-flutter-applications
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bef85f3a-8e4e-43f7-b959-4e85276e5380/getx-package-flutter-applications.png
date: 2021-01-08T12:00:13.000Z
summary: >-
  GetX is an extra lightweight solution for state, navigation, and dependencies management for Flutter applications. In this article, we will be looking at its benefits, features, and how to start using it in Flutter applications.
description: >-
  GetX is an extra lightweight solution for state, navigation, and dependencies management for Flutter applications. In this article, we will be looking at its benefits, features, and how to start using it in Flutter applications.
categories:
  - Apps
  - Mobile
  - JavaScript
---

Flutter is one of the fastest ways to build truly cross-platform native applications. It provides features allowing the developer to build a truly beautiful UI experience for their users.

However, most times to achieve things like navigating to screens, state management, and show alerts, a lot of boilerplates are needed. These boilerplates tend to slow down the development efficiency of developers trying to go about building features and meeting their deadlines.

Take for example the boilerplate needed to navigate to a screen in a Flutter application. Let’s say you want to navigate to a screen called `AboutScreen`. you will have to write:

<pre><code class="language-javascript">Navigator.push(
    context,
    MaterialPageRoute(builder: (context) =&gt; AboutScreen()),
  );</code></pre>
  
It would be more efficient and developer-friendly to do something like:

<pre><code class="language-javascript">Get.to(AboutScreen());</code></pre>

When you need to navigate back to the previous page in Flutter you will have to write:

<pre><code class="language-javascript">Navigator.pop(context);</code></pre>

You will notice we are always depending on [context property](https://api.flutter.dev/flutter/widgets/State/context.html) for something as commonplace as navigating between screens. What if instead, we can do something like this:

<pre><code class="language-javascript">Get.back();</code></pre>

The above examples are some of the ways where application development in Flutter can be improved to be more intuitive and efficient with less boilerplate. If you favor simplicity and being efficient in building out features and ideas, in Flutter then the Get package will interest you.

{{% feature-panel %}}

## What Is GetX

[Get or GetX](https://pub.dev/packages/get) is a fast, stable, extra-light framework for building Flutter applications. 

GetX ships out of the box with high-performance state management, intelligent dependency injection, and route management in a simplistic and practical way.

GetX aims to minimize boilerplates while also providing simple and intuitive syntax for developers to use while building their applications. At the core of GetX are these 3 principles:

- **Performance**  
GetX focuses on the performance of your application by implementing its features to consume as little resources as possible.
- **Productivity**  
GetX wants developers to use its features to be productive as quickly as possible. It does so by employing easy to remember syntax and practices. For example, generally, the developer should be concerned to remove controllers from memory but GetX out of the box provides smart management that monitors controllers in your application and remove them when they are not being used by default.
- **Organization**  
GetX allows the decoupling of the View, presentation logic, business logic, dependency injection, and navigation in your Flutter application. You do not need context to navigate between routes, so you are not dependent on the widget tree for navigation. You don’t need context to access your controllers/blocs through an [`inheritedWidget`](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html), so you can completely decouple your presentation logic and business logic from your view layer. You do not need to inject your Controllers/Models/Blocs classes into your widget tree through multiproviders, for this GetX uses its own dependency injection feature, decoupling the DI from its view completely.

## Features Of GetX

GetX comes with a couple of features you will need in your daily app development in Flutter. Let’s look at them:

### State Management

One of the flagship features of GetX is its intuitive state management feature. State management in GetX can be achieved with little or no boilerplate.

### Route Management

GetX provides API for navigating within the Flutter application. This API is simple and with less code needed.

### Dependency Management

GetX provides a smart way to manage dependencies in your Flutter application like the view controllers. GetX will remove any controller not being used at the moment from memory. This was a task you as the developer will have to do manually but GetX does that for you automatically out of the box.

### Internationalization

GetX provides i18n out of the box allowing you to write applications with various language support.

### Validation

GetX provides validation methods for performing input validation in your Flutter applications. This is quite convenient as you wouldn’t need to install a separate validation package.

### Storage

GetX provides a fast, extra light, and synchronous key-value in memory, which backs up data to disk at each operation. It is written entirely in Dart and easily integrates with the core GetX package.

## Getting Started With GetX

Now that you have seen what GetX is and the features and benefits it provides, let’s see how to set it up in your application. We will build a demo app to see most of the features we have mentioned in action. Let’s get started.

### Create A Brand New Flutter Application

We will get started by creating a brand new Flutter application through the Flutter CLI. I am assuming your machine is already set up for application development with Flutter. So we run:

<pre><code class="language-javascript">flutter create getx_demo</code></pre>

This will generate the basic code needed for a Flutter application. Next, open up the project you just created in your editor of choice (We will be using VS Code for this article). We will then run the project to make sure it’s working alright (Make sure you have either a device connected or an emulator/simulator running).

When the application runs, you will see the default counter application that Flutter scaffold for you when you create a new Flutter application. What we are going to do is to implement the very same counter application but with GetX to manage the state of the app (which is the count variable).

We will start with clearing `main.dart` and leaving only this snippet of code:

<pre><code class="language-javascript"># main.dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
</code></pre>

By now our application would have been broken since there is no `MyHomePage` widget anymore. Let’s fix that. With GetX, we don’t need stateful widgets and also our UI can be clearly separated from our business logic. So we will create two directories inside `lib/`. These directories are:

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>views/</code></td>
      <td>To hold the screens in our application.</td>
    </tr>
    <tr>
      <td><code>controllers/</code></td>
      <td>To hold all controllers for the screens in our application.</td>
    </tr>
  </tbody>
</table>

Let’s create `MyHomePage` widget inside `views/`. The name of the file will be `my_home_page.dart`. After you create it, add the following code snippet to it:

<pre><code class="language-javascript">import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
  final String title;

  MyHomePage({this.title});
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: &lt;Widget&gt;[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '0',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: null,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}
</code></pre>

Now we have the `MyHomePage` widget, let’s import it in `main.dart`. Add the import statement to the top of main.dart below `import 'package:flutter/material.dart';`

<pre><code class="language-javascript">import './views/my_home_page.dart';</code></pre>    

Now your `main.dart` file should look like this:

<pre><code class="language-javascript">import 'package:flutter/material.dart';
import './views/my_home_page.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
</code></pre>

When you save your application now, all errors should have been fixed and the app will run. But you will notice when you click the button again, the counter won’t be updated. If you look at the `views/my_home_page.dart` code, you will see we are just hard coding `0` as the value of the Text widget and passing `null` to the `onPressed` handler of the button. Let’s bring in GetX to the mix to get the application functional again.

{{% ad-panel-leaderboard %}}

### Installing GetX

Head over to the [install page](https://pub.dev/packages/get/install) for GetX on pub.dev and you will see the line of code to copy to place in your `pubspec.yml` file to install GetX. As of the time of writing this article, the current version of GetX is 3.23.1. So we will copy the line:

<pre><code class="language-javascript">get: ^3.23.1</code></pre>

And then paste it under the `dependencies` section of our `pubspec.yml` file. When you save the file, get should be automatically installed for you. Or you can run manually in your terminal.

<pre><code class="language-javascript">flutter pub get</code></pre>

The dependencies section of your `pubspec.yml` file should look like this:

<pre><code class="language-javascript">dependencies:
  flutter:
    sdk: flutter
  get: ^3.23.1</code></pre>

### `GetxController`

We have mentioned that GetX allows you to separate the UI of your application from the logic. It does this by providing a `GetxController` class which you can inherit to create controller classes for the views of your application. For our current app, we have one view so we will create a controller for that view. Head over to the `controllers/` directory and create a file called `my_home_page_controller.dart`. This will hold the controller for the `MyHomePage` view.

After you’ve created the file, first import the GetX package by adding this to the top of the file:

<pre><code class="language-javascript">import 'package:get/get.dart';</code></pre>

Then you will create a class called `MyHomePageController` inside it and extend the `GetxController` class. This is how the file should look like:

<pre><code class="language-javascript">import 'package:get/get.dart';

class MyHomePageController extends GetxController {}
</code></pre>

let’s add the count state to the class we’ve created.

<pre><code class="language-javascript">final count = 0;</code></pre>

In GetX, to make a variable observable &mdash; this means that when it changes, other parts of our application depending on it will be notified. To do this we simply need to add `.obs` to the variable initialization. So for our above `count` variable, we will add `.obs` to `0`. So the above declaration will now look like this:

<pre><code class="language-javascript">final count = 0.obs;</code></pre>

This is how our controller file looks like at the moment:

<pre><code class="language-javascript">import 'package:get/get.dart';

class MyHomePageController extends GetxController {
  final count = 0.obs;
}
</code></pre>

To wrap things up with the `MyHomePageController` we will implement the `increment` method. This is the snippet to do that:

<pre><code class="language-javascript">increment() =&gt; count.value++;</code></pre>

You will notice we needed to add `.value` to the count variable to increment it. We did this because adding `.obs` to a variable makes it an observable variable and to get the value of an observable variable, you do so from the `value` property.

So we are done with the controller. Now when the value of count changes, any part of our application using it will be updated automatically.

We will now head over to our view and let it know about the controller we just created. We will do so by instantiating the controller class using GetX dependency management feature. This will ensure that our controller won’t be in memory when it is no longer needed.

In `views/my_home_page.dart` import the Get package and also the controller you created like so:

<pre><code class="language-javascript">import 'package:get/get.dart';
import '../controllers/my_home_page_controller.dart';</code></pre>

Then inside the `MyHomePage` class we will instantiate the `MyHomePageController`:

<div class="break-out">

<pre><code class="language-javascript">final MyHomePageController controller = Get.put(MyHomePageController());</code></pre>
</div>

Now we have an instance of the `MyHomePageController`, we can use the state variable as well as the method. So starting with the state, in GetX to mark a part of your UI to be rebuilt when a state variable changes, you will wrap that part with the `Obx` widget. GetX provides other ways of doing this, but this method is much simpler and cleaner. 

For our count application we want the Text widget to be updated with the current count. So we will wrap the Text widget with `Obx` widget like so:

<pre><code class="language-javascript">Obx(() =&gt; Text('0',style: Theme.of(context).textTheme.headline4,),)</code></pre>

Next, we will replace the static string `0` with the count variable from the `MyHomePageController` like so:

<pre><code class="language-javascript">Obx(() =&gt; Text('${controller.count.value}',
,style: Theme.of(context).textTheme.headline4,),)</code></pre>

Lastly, we will call the increment method when the `floatingActionButton` is pressed like so:

<pre><code class="language-javascript">floatingActionButton: FloatingActionButton(
        onPressed: controller.increment,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),</code></pre>
      
So overall, our `MyHomePage` view file should now look like this:

<div class="break-out">

<pre><code class="language-javascript">import 'package:flutter/material.dart';
import 'package:get/get.dart';
import '../controllers/my_home_page_controller.dart';

class MyHomePage extends StatelessWidget {
  final String title;
  final MyHomePageController controller = Get.put(MyHomePageController());
  MyHomePage({this.title});
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: &lt;Widget&gt;[
            Text(
              'You have pushed the button this many times:',
            ),
            Obx(
              () =&gt; Text(
                '${controller.count.value}',
                style: Theme.of(context).textTheme.headline4,
              ),
            )
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: controller.increment,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}
</code></pre>
</div>

When you save your application or you rerun it, the counter app should be working as it did when we first created the application.

I believe you have seen how intuitive state management is with GetX, we didn’t have to write a lot of boilerplate and this simplicity will be more obvious as your application get complex. You will also notice our view doesn’t hold or maintain any state so it can be a stateless widget. The brain of the view in turn is now a controller class that will hold the state for the view and methods.

## Navigation In GetX

We have seen state management in GetX. Let’s now look at how GetX supports Navigation within your application. To activate the Navigation feature of GetX, you only need to make one change in `main.dart` which is to turn the `MaterialApp` widget to a `GetMaterialApp` widget. Let’s do that by first importing Get in the top of `main.dart`

<pre><code class="language-javascript">import 'package:get/get.dart';</code></pre>

Then we make the change to `MaterialApp` so our `main.dart` file now look like this:

<pre><code class="language-javascript">import 'package:flutter/material.dart';
import 'package:get/get.dart';
import './views/my_home_page.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
</code></pre>

Now our app has been set up to support GetX navigation. To test this out we will create another view in `views/` directory. We will call this on `about_page.dart` and it will contain the following code:

<div class="break-out">

<pre><code class="language-javascript">import 'package:flutter/material.dart';
import 'package:get/get.dart';
import '../controllers/my_home_page_controller.dart';

class AboutPage extends StatelessWidget {
  final MyHomePageController controller = Get.put(MyHomePageController());
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('About GetX'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: &lt;Widget&gt;[
            Padding(
              padding: const EdgeInsets.all(16.0),
              child: Text(
                'GetX is an extra-light and powerful solution for Flutter. It combines high performance state management, intelligent dependency injection, and route management in a quick and practical way.',
              ),
            ),
          ],
        ),
      ),
    );
  }
}
</code></pre>
</div>

We will then go over to `MyHomePage` and add a button that when pressed will navigate us to the `AboutPage`. Like so. The button should be below the Obx widget. Here it is:

<pre><code class="language-javascript"> FlatButton(onPressed: () {}, child: Text('About GetX'))</code></pre>

We will also need to import the `AboutPage` on top of the `MyHomePage` file:

<pre><code class="language-javascript">import './about_page.dart';</code></pre>

To tell GetX to navigate to the `AboutPage` all we need is one line of code which is:

<pre><code class="language-javascript">Get.to(AboutPage());</code></pre>

Let’s add that to the `onPressed` callback of the `FlatButton` widget like so:

<pre><code class="language-javascript"> FlatButton(

    onPressed: () {
       Get.to(AboutPage());
              },
  child: Text('About GetX'))</code></pre>

When you save your application now, you will now be able to navigate to the `AboutPage`.

You can also choose to replace the `MyHomePage` view with the `AboutPage` so the user won’t be able to navigate back to the previous page by hitting the device back button. This is useful for screens like login screens. To do this, replace the content of the `onPressed` handler with the below code:

<pre><code class="language-javascript">  Get.off(AboutPage());</code></pre>

This will pop the `MyHomePage` view and replace it with `AboutPage`.

Now that we can navigate to the `AboutPage`, I think it won’t be so bad to be able to go back to `MyHomePage` to do this we will add a button in `AboutPage` after the Padding widget and in it’s `onPressed` handler we will make a call to `Get.back()` to navigate back to the `MyHomePage`:

<pre><code class="language-javascript"> FlatButton(
    onPressed: () {
        Get.back();
    },
    child: Text('Go Home')
)</code></pre>

{{% ad-panel-leaderboard %}}

## Snackbar

In Flutter conventionally to show a Snackbar, you will need to write something like this:

<pre><code class="language-javascript">final snackBar = SnackBar(content: Text('Yay! A SnackBar!'));
// Find the Scaffold in the widget tree and use it to show a SnackBar.
Scaffold.of(context).showSnackBar(snackBar);</code></pre>

You can observe we are still depending on the `context` property. Let’s see how we can achieve this in GetX. Go into the `MyHomePage` view and add another `FlatButton` widget below the last button we added. Here is the snippet for the button:

<pre><code class="language-javascript"> FlatButton(
      onPressed: () {
         // TODO: Implement Snackbar
       },
      child: Text('Show Snackbar'))</code></pre>
      
Let’s display the message ‘Yay! Awesome GetX Snackbar’. Inside the onPressed handler function add the below line of code:

<pre><code class="language-javascript"> Get.snackbar('GetX Snackbar', 'Yay! Awesome GetX Snackbar');</code></pre>

Run your application and when you click on the “Show Snackbar button” you will see a snackbar on top of your application!

See how we reduced the number of lines needed to show a snackbar in a Flutter application? Let’s do some more customization on the Snackbar; Let’s make it appear at the bottom of the app. Change the code to this:

<div class="break-out">

<pre><code class="language-javascript">Get.snackbar('GetX Snackbar', 'Yay! Awesome GetX Snackbar',snackPosition:SnackPosition.BOTTOM,
);</code></pre>
</div>

Save and run your application and the Snackbar will now appear at the bottom of the application. How about we change the background color of the Snackbar as it is at the moment transparent. We will change it to an `amberAccent` color from the `Colors` class in Flutter. Update the code to this:

<div class="break-out">

<pre><code class="language-javascript">Get.snackbar('GetX Snackbar', 'Yay! Awesome GetX Snackbar',snackPosition:SnackPosition.BOTTOM, backgroundColor: Colors.amberAccent
);</code></pre>
</div>

Overall, the button code should look like this:

<div class="break-out">

<pre><code class="language-javascript"> FlatButton(
                onPressed: () {
                  Get.snackbar('GetX Snackbar', 'Yay! Awesome GetX Snackbar',
                      snackPosition: SnackPosition.BOTTOM,
                      backgroundColor: Colors.amberAccent);
                },
                child: Text('Show Snackbar'))</code></pre>
</div>

## Dialog

GetX provides a simple method for creating AlertDialog in Flutter. Let’s see it in action. Create another button below the previous one:

<pre><code class="language-javascript"> FlatButton(
                onPressed: () {
                 // TODO: Show alert dialog
                },
                child: Text('Show AlertDialog'))</code></pre>

Let’s call GetX to display an alert Dialog:

<pre><code class="language-javascript">Get.defaultDialog();</code></pre>

That will show a default Alert Dialog that is dismissable by tapping outside the Dialog. You can see how in one line of code we have a working alert dialog. Let’s customize it a bit. Let’s change the title and the message:

<div class="break-out">

<pre><code class="language-javascript"> Get.defaultDialog(
                      title: 'GetX Alert', middleText: 'Simple GetX alert');</code></pre>
</div>

Save and run your app and you will see the changes when you hit the “Show AlertDialog” button. We can add confirm and Cancel buttons like so:

<pre><code class="language-javascript">Get.defaultDialog(
                      title: 'GetX Alert',
                      middleText: 'Simple GetX alert',
                      textConfirm: 'Okay',
                      confirmTextColor: Colors.amberAccent,
                      textCancel: 'Cancel');</code></pre>

There are a lot of ways to customize the GetX dialog and the API is quite intuitive and simple.

## Conclusion

GetX was created to improve the productivity of Flutter developers as they build out features. Instead of having to search for boilerplate needed to do things like state management, navigation management, and more, GetX provides a simple intuitive API to achieve these activities without sacrificing performance. This article introduces you to GetX and how to get started using it in your Flutter applications.

- You can find the demo [here&nbsp;&rarr;](https://github.com/DominusKelvin/getx_demo)

{{< signature "ra, yk, il" >}}
