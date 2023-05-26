---
title: 'What’s New In Flutter 2?'
slug: flutter2-stable-mobile-web-desktop-development-native-speed-one-codebase
author: carmine-zaccagnino
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/797b3677-8410-4da5-830b-d738215083d8/flutter2-stable-mobile-web-desktop-development-native-speed-one-codebase.jpg
date: 2021-03-17T12:00:00.000Z
summary: >-
  Flutter has been transitioning from a cross-platform mobile development SDK for Android/iOS into a tool that allows you to run the same code natively in a browser on Windows, Linux and macOS. With Flutter 2, non-mobile Flutter development is starting to become more viable.
description: >-
  Flutter has been transitioning from a cross-platform mobile development SDK for Android/iOS into a tool that allows you to run the same code natively in a browser on Windows, Linux and macOS. With Flutter 2, non-mobile Flutter development is starting to become more viable.
categories:
  - Apps
  - Mobile
---

Last year, I wrote two articles here on Smashing Magazine about using [Flutter](https://flutter.dev/) on web and desktop platforms. [The first article](https://www.smashingmagazine.com/2020/04/responsive-web-desktop-development-flutter/) was a general introduction to web and desktop development, and focused on building responsive UI; [the second article](https://www.smashingmagazine.com/2020/06/common-cross-platform-issues-flutter/) was about the challenges you might face when trying to develop a Flutter app that runs on multiple platforms.

Back then, Flutter support for non-mobile platforms wasn’t considered stable and production-ready by the Flutter team, but things have changed now.

## Flutter 2 Is Here

On the 3rd of March, Google held the [Flutter Engage event](https://www.youtube.com/watch?v=yll3SNXvQCw), where Fluter 2.0 was launched. This release is really a proper 2.0 release, with [many changes](https://medium.com/flutter/whats-new-in-flutter-2-0-fe8e95ecc65) promising to make Flutter *really* ready for going beyond mobile app development.

The change that is central to understanding why Flutter 2.0 matters is that *web development* is now officially part of the **stable channel** and desktop support will follow soon on the stable channel as well. In fact, it is currently enabled in release candidate-like form as an early release beta snapshot in the stable channel.

In the announcement, Google didn’t just give a hint of what the future of Flutter will be like. There were also actual examples of how large companies are already working on Flutter apps to replace their existing apps with ones that perform better and allow developers to be more productive. E.g. the world’s biggest car manufacturer, Toyota, will now be building the infotainment system on their cars using Flutter.

Another interesting announcement — this one showing how fast Flutter is improving as a cross-platform SDK — is Canonical’s announcement that, in addition to developing their new Ubuntu installer using Flutter, they will also be using **Flutter as their default option** to build desktop apps.

They also released [a Flutter version of Ubuntu’s Yaru theme](https://github.com/ubuntu/yaru.dart), which we will use later in the article to build a Flutter desktop app that looks perfectly at home in the Ubuntu desktop, also using some more of the new Flutter features. You can take a look at [Google’s Flutter 2 announcement](https://developers.googleblog.com/2021/03/announcing-flutter-2.html) to get a more complete picture.

Let’s look at some of the **technical changes to Flutter** which got onto the stable channel with version 2.0 and build a very simple example desktop app with Flutter before we draw some conclusions on what specific project types we could and couldn’t use Flutter for as of now.

{{% feature-panel %}}

## General Usability Changes For Bigger Devices

According to the announcement, many changes have been made to Flutter to provide better support for devices that aren’t mobile devices.

For example, an obvious example of something that was needed for web and desktop apps and until now had to be done using third-party packages or by implementing it yourself is a **scrollbar**.

Now there is a built-in `Scrollbar` which can fit right into your app, looking exactly how a scrollbar should look in the specific platform: with or without a track, with the possibility of scrolling by clicking on the track, for example, which is huge if you want your users to feel right at home from the start when using your Flutter app. You can also theme it and customize it.

It also looks like at some point Flutter will automatically **show suitable scrollbars** when the content of the app is scrollable.

Meanwhile, you can just wrap any scrollable view with the scrollbar widget of your choice and create a **`ScrollController`** to add as the `controller` for both the scrollbar and the scrollable widget (in case you’ve never used a `ScrollController`, you use exactly like a `TextEditingController` for a `TextField`). You can see an example of the use of a regular Material scrollbar a bit further down this article in the desktop app example.

## Flutter Web Changes

Flutter for the web was already in a quite usable form, but there were performance and usability issues which meant it never felt as polished as mobile Flutter. With the release of Flutter 2.0, there have been many improvements to it, especially when it comes to **performance**.

The compilation target, previously very experimental and tricky to use to render your app (with WebAssembly and Skia) is now called **CanvasKit**. It’s been refined to offer a consistent and performant experience when going from running a Flutter app natively on mobile devices to running it in a browser.

Now, by default, your app will render using CanvasKit for desktop web users and with the default HTML renderer (which has had improvements as well, but is not as good as CanvasKit) for mobile web users.

If you’ve tried to use Flutter to build web apps, you might have noticed it wasn’t particularly intuitive to have something as simple as a hyperlink. Now at least, you can create hyperlinks a bit more like you would when using HTML, using the `Link` class.

This is actually not an addition to Flutter itself, but a recent addition to [Google’s `url_launcher` package](https://pub.dev/packages/url_launcher). You can find a complete description and examples of usage of the `Link` class in [the official API reference](https://pub.dev/documentation/url_launcher/latest/link/Link-class.html).

**Text selection** was improved as now the pivot point corresponds to where the user started selecting text and not the left edge of the `SelectableText` in question. Also, now Copy/Cut/Paste options exist and work properly.

Nevertheless, text selection still isn’t top-notch as it’s not possible to select text across different `SelectableText` widgets and selectable text still isn’t default, but we will talk about this as well as other outstanding Flutter web drawbacks (lack of SEO support, first and foremost) in the conclusion to this article.

## Flutter Desktop Changes

When [I wrote about web and desktop development with Flutter last year](https://www.smashingmagazine.com/2020/04/responsive-web-desktop-development-flutter/), I focused mostly on building web apps with Flutter, given that desktop development was still considered very experimental (not even on the `beta` channel). Now though, Flutter desktop support is soon to follow web support and will be going stable.

**Performance and stability** have been improved quite a lot, and the improvements in general usability for bigger devices operated with a mouse and keyboard that benefit web apps so much also mean that Flutter desktop apps are now more usable.

There is still a lack of tooling for desktop apps and there are still many quite severe outstanding bugs, so don’t try to use it for your next desktop app project meant for public distribution.

{{% ad-panel-leaderboard %}}

## Example Desktop App Built With Flutter

Flutter desktop support is now quite stable and usable though, and it will surely get better in the future just as much as Flutter in its entirety has gotten better until now, so let’s give it a try to **see it in action**! You can [download the entire code example on a GitHub repo](https://github.com/carzacc/flutter_ubuntu_desktop_example).

The app we will build is the following very simple app. We have a sidebar navigation along with some content items for each of the navigation sections.

{{< vimeo id="524994038" caption="This is what the app will look like." breakout="true" >}}

The first thing to do is **figure out your dependencies**.

First of all, you must have Flutter desktop development enabled, using the command

<pre><code class="language-bash">flutter config --enable-${OS_NAME}-desktop
</code></pre>

where you’d replace `${OS_NAME}` with your desktop OS of choice, either `windows`, `linux` or `macos`. For this example, I’ll use Linux given that we’re going to use the Ubuntu theme.

There are also other dependencies needed to build native apps for each platform, for example on Windows you need Visual Studio 2019, on macOS you need Xcode and CocoaPods and you can find an up-to-date list of Linux dependencies [on Flutter’s official website](https://flutter.dev/desktop#requirements).

Then create a Flutter project, running:

<pre><code class="language-bash">flutter create flutter_ubuntu_desktop_example
</code></pre>

Then, we must get the theme itself (our app’s only dependency) by adding `yaru` to the your app’s `dependencies` in `pubspec.yaml` (in the root of the source tree):

<pre><code class="language-yaml">dependencies:
  yaru: ^0.0.0-dev.8
  flutter:
    sdk: flutter
</code></pre>

Then, let’s move over to `lib/main.dart`, where our app’s code resides.

First, we import the stuff we need. In this case, we’re just going to import the regular Flutter Material Design library and the Yaru theme (we are only going to use the light theme for this example so we are going to only `show` that one object in the Yaru package):

<pre><code class="language-dart">import 'package:flutter/material.dart';
import 'package:yaru/yaru.dart' show yaruLightTheme;
</code></pre>

Instead of having a separate app class, we are going to call the `MaterialApp` contructors directly in `main` when calling `runApp`, so that’s where we set the app’s theme, which is going to be the Yaru theme, more specifically the light theme called `yaruLightTheme`:

<pre><code class="language-dart">void main() =>
  runApp(MaterialApp(
    theme: yaruLightTheme,
    home: HomePage(),
  ));
</code></pre>

The `HomePage` is going to be a `StatefulWidget`, holding the data we are going to show given that it’s immutable (remember, widgets are always immutable, mutability is handled in the `State` of a `StatefulWidget`):

<pre><code class="language-dart">class HomePage extends StatefulWidget {
  final dataToShow = {
    "First example data": [
      "First string in first list item",
      "Second in first",
      "Example",
      "One"
    ],
    "Second example": [
      "This is another example",
      "Check",
      "It",
      "Out",
      "Here's other data"
    ],
    "Third example": [
      "Flutter is",
      "really",
      "awesome",
      "and",
      "it",
      "now",
      "works",
      "everywhere,",
      "this",
      "is",
      "incredible",
      "and",
      "everyone",
      "should",
      "know",
      "about",
      "it",
      "because",
      "someone",
      "must",
      "be",
      "missing",
      "out",
      "on",
      "a lot"
    ]
  }.entries.toList();

  @override
  createState() => HomePageState();
}
</code></pre>

The `HomePageState` is where we define app UI and behaviour. First of all, let’s look at the tree of widgets we want to build (list and grid items and spacing widgets excluded):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a9f52d-72ee-4816-a4cc-cb7453c65148/ubuntuapptree.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a9f52d-72ee-4816-a4cc-cb7453c65148/ubuntuapptree.png" width="800" height="" sizes="100vw" caption="Our app’s planned widget tree (without spacing and placement widgets). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a9f52d-72ee-4816-a4cc-cb7453c65148/ubuntuapptree.png'>Large preview</a>)" alt="The app’s widget tree" >}}

We are going to restrict the `Column` on the left (the one showing the controls for the widgets to show on the right side of the app) to a certain width (400 pixels for example) using a `Container`, whereas the `GridView` on the right should be `Expanded` to fill the view.

On the left side of the `Row` (within the `Column`), the `ListView` should expand to **fill the vertical space** below the `Row` of buttons at the top. Within the `Row` at the top, we also need to expand the `TextButton` (the reset button) to fill the space to the right of the left and right chevron `IconButton`s.

The resulting `HomePageState` that does all of that, along with the necessary logic to show the right stuff on the right depending on what the user selects on the left, is the following:

<div class="break-out">

 <pre><code class="language-javascript">class HomePageState extends State&lt;HomePage&gt; {
  int selected = 0;

  ScrollController _gridScrollController = ScrollController();

  incrementSelected() {
    if (selected != widget.dataToShow.length - 1) {
      setState(() {
        selected++;
      });
    }
  }

  decrementSelected() {
    if (selected != 0) {
      setState(() {
        selected--;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Row(
        children: [
          Container(
              color: Colors.black12,
              width: 400.0,
              child: Column(
                children: [
                  Row(
                    children: [
                      IconButton(
                        icon: Icon(Icons.chevron_left),
                        onPressed: decrementSelected,
                      ),
                      IconButton(
                        icon: Icon(Icons.chevron_right),
                        onPressed: incrementSelected,
                      ),
                      Expanded(
                          child: Center(
                        child: TextButton(
                          child: Text("Reset"),
                          onPressed: () => setState(() => selected = 0),
                        ),
                      ))
                    ],
                  ),
                  Expanded(
                    child: ListView.builder(
                      itemCount: widget.dataToShow.length,
                      itemBuilder: (_, i) => ListTile(
                        title: Text(widget.dataToShow[i].key),
                        leading: i == selected
                            ? Icon(Icons.check)
                            : Icon(Icons.not_interested),
                        onTap: () {
                          setState(() {
                            selected = i;
                          });
                        },
                      ),
                    ),
                  ),
                ],
              )),
          Expanded(
            child: Scrollbar(
              isAlwaysShown: true,
              controller: _gridScrollController,
              child: GridView.builder(
                  controller: _gridScrollController,
                  itemCount: widget.dataToShow[selected].value.length,
                  gridDelegate: SliverGridDelegateWithMaxCrossAxisExtent(
                      maxCrossAxisExtent: 200.0),
                  itemBuilder: (_, i) => Container(
                        width: 200.0,
                        height: 200.0,
                        child: Padding(
                          padding: const EdgeInsets.all(8.0),
                          child: Card(
                            child: Center(
                                child:
                                    Text(widget.dataToShow[selected].value[i])),
                          ),
                        ),
                      )),
            ),
          ),
        ],
      ),
    );
  }
}
</code></pre>
</div>

and we’re done!

Then you build your app with

<pre><code class="language-bash">flutter build ${OS_NAME}
</code></pre>

where `${OS_NAME}` is the name of your OS, the same you used earlier to enable Flutter desktop development using `flutter config`.

The compiled binary to run your app will be

<figure class="break-out">
<pre class="language-bash"><code>build/linux/x64/release/bundle/flutter_ubuntu_desktop_example</code></pre></figure>

on Linux and

<figure class="break-out">
<pre class="language-bash"><code>build\windows\runner\Release\flutter_ubuntu_desktop_example.exe</code></pre></figure>

on Windows, you can run that and you’ll get the app that I showed you at the start of this section.

On macOS, you need to open `macos/Runner.xcworkspace` in Xcode and then use Xcode to build and run your app.

## Other Flutter Changes

There have also been a few changes that also affect mobile development with Flutter, and here is just a brief selection of some of them.

A feature that so many of us, Flutter developers, wanted is better **support for Admob ads**, and it’s now finally included in the official [`google_mobile_ads`](https://pub.dev/packages/google_mobile_ads) package. Another one is `autocomplete`; there is an [`Autocomplete` material widget for it](https://api.flutter.dev/flutter/material/Autocomplete-class.html), as well as [a more customizable `RawAutocomplete` widget](https://api.flutter.dev/flutter/widgets/RawAutocomplete-class.html).

The addition of the `Link` that we discussed in the section about web development actually **applies to all platforms**, even though its effects will be felt most by those working on Flutter web projects.

### Recent Dart Language Changes

It is important to be aware of the changes that were made to the Dart language that affect Flutter app development.

In particular, Dart 2.12 brought **C language interoperability support** (described in detail and with instructions for different platforms [on the official Flutter website](https://flutter.dev/docs/development/platform-integration/c-interop)); also, sound `null-safety` was added to the stable Dart release channel.

### <code>null-safety</code>

The biggest change that was made to Dart is the introduction of sound `null-safety` that it’s getting more and more support from third-party packages as well as the Google-developed libraries and packages.

*Null safety* brings **compiler optimizations** and reduces the chance of runtime errors so, even though right now it’s optional to support it, it is important you start at least understanding how to make your app null-safe.

At the moment though, that may not be an option for you as not all Pub packages are fully null-safe and that means that if you need one of those packages for your app you won’t be able to take advantage of the benefits on null-safety.

<h4 id="marker">Making Your App <code>null-safe</code></h3>

If you’ve ever worked with Kotlin, Dart’s approach to null safety will be somewhat familiar to you. Take a look at [Dart’s official guide on it](https://dart.dev/null-safety/understanding-null-safety) for a more complete guide to Dart’s `null-safety`.

All of the types you’re familiar with (`String`, `int`, `Object`, `List`, your own classes, etc.) are now non-nullable: their value can *never* be `null`.

This means that a function that has a non-nullable return type **must always return a value**, or else you’ll get a compilation error and you always have to initialize non-nullable variables, unless it’s a local variable that gets assigned a value before it’s ever used.

If you want a variable to be nullable you need to add a question mark to the end of the type name, e.g. when declaring an integer like this:

<pre><code class="language-javascript">int? a = 1
</code></pre>

At any point, you can set it to `null` and the compiler won’t cry about it.

Now, what if you have a nullable value and use it for something that requires a non-nullable value? To do that, you can simply check it isn’t null:

<pre><code class="language-javascript">void function(int? a) {
    if(a != null) {
        // a is an int here
    }
}
</code></pre>

If you *know* with 100% certainty that a variable exists and isn’t null you can just use the `!` operator, like this:

<pre><code class="language-javascript">String unSafeCode(String? s) => s!;
</code></pre>

{{% ad-panel-leaderboard %}}

## Drawing Conclusions: What Can We Do With Flutter 2?

As Flutter keeps evolving, there are more and more things we can do with it, but it’s still not reasonable to say that Flutter can be used for any app development project of any kind.

On the mobile side, it’s unlikely you’re going to run into something that Flutter isn’t great at because it’s been supported since the start and it’s been polished. Most things you’ll ever need are already there.

On the other hand, web and desktop aren’t quite there yet.

**Desktop is still a bit buggy** and Windows apps (which are an important part of desktop development) still require a lot of work before they look good. The situation is better on Linux and macOS only to an extent.

**The web is in a much better place than desktop**. You can build decent web apps, but you’re still mostly limited to single-page applications and Progressive Web Apps. We still most certainly don’t want to use it for content-centric apps where indexability and SEO are needed.

Content-centric apps probably will not be that great because text selection still isn’t top-notch, as we’ve seen in the section about the current state of Flutter for the web.

If you need the web version of your Flutter app, though, Flutter for the web will probably be just fine, especially as there are a huge amount of **web-compatible packages** around already and the list is always growing.

## Additional Resources

* [Keynote (Flutter Engage)](https://www.youtube.com/watch?v=zSbsIiluixw), YouTube
* [What’s New in Flutter 2](https://medium.com/flutter/whats-new-in-flutter-2-0-fe8e95ecc65), Flutter, Medium
* [Understanding `null safety`](https://dart.dev/null-safety/understanding-null-safety), Dart.dev
* [Responsive Web And Desktop Development With Flutter](https://www.smashingmagazine.com/2020/04/responsive-web-desktop-development-flutter/), Smashing Magazine
* [Solving Common Cross-Platform Issues When Working With Flutter](https://www.smashingmagazine.com/2020/06/common-cross-platform-issues-flutter/), Smashing Magazine

{{< signature "vf, il" >}}
