---
title: Windows Phone Design For Developers
slug: windows-phone-design-developers
image: >-
  https://www.smashingmagazine.com/general/2014/04/10/120835-revision-41/attachment/people-hub/
date: 2012-10-18T22:07:21.000Z
author: reza-alizadeh
description: >-
  There is a prevalent belief amongst developers that design is a skill that
  can't be learned — you either have it or you don't. While much of this can be
  attributed to the perception that heightened creativity is required to produce
  good design, the truth is anyone can create attractive applications and good
  user experience by following common design patterns and applying guidelines
  for the particular platform being targeted.
categories:
  - Mobile
  - Windows Phone
---
There is a prevalent belief amongst developers that design is a skill that can't be learned — you either have it or you don't. While much of this can be attributed to the perception that heightened creativity is required to produce good design, the truth is anyone can create attractive applications and good user experience by following common design patterns and applying guidelines for the particular platform being targeted.

So rejoice, Mr. "Not-a-Designer," this article was written just for you. This article is targeted at the everyday developer looking for practical guidelines and tips to leverage in their Windows Phone application to build compelling Windows Phone UI-compliant apps with solid user experiences. Think of it as a checklist of sorts to ensure that your app avoids the common design problems found in Windows Phone applications.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Testing For And With Windows Phone](https://www.smashingmagazine.com/2015/05/testing-for-windows-phone/)
*   [Introduction To Designing For Windows Phone 7 And Metro](https://www.smashingmagazine.com/2011/12/introduction-designing-windows-phone-7-metro/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)
*   [Building An Online Magazine App For Windows 8](https://www.smashingmagazine.com/2013/09/online-magazine-app-for-windows-8-part1-html5-app/)

Please see the <a href="https://msdn.microsoft.com/en-us/library/hh202915(v=vs.92).aspx">User Experience Design Guidelines for Windows Phone</a> for a complete overview of the platform and user interaction model on Windows Phone.

{{% feature-panel %}}

## Panorama Controls

The aptly named Panorama is one of the innovative controls of the Windows Phone platform. Whereas a traditional mobile application is designed to fit within the boundaries of the screen, the Panorama control allows for a long horizontal canvas, to lay out elements that extend beyond the confines of the screen. The Panorama control is composed of a number of Panorama items, which contain the content. When viewing each Panorama item, the user will see a little piece of the item to the right, indicating that additional content is waiting to be discovered. As the user pans horizontally across the Panorama, the control exhibits a parallax behavior — smoothly moving the background, title and items at different speeds.

When creating your panorama, approach it as if you were designing a magazine cover — it should engage the user and entice them to explore more. It should reveal relevant, fresh and compelling content, and it should serve as the entry point to the rest of the application. Panoramas are great for showing a few pieces of content that you want to highlight in your app — the top news from your social network, the last eight songs played, the top six featured recipes. Consider also adding a background image to your Panorama control to provide a more visually appealing and immersive experience.

Given the popularity of the control, you can find inspiration for designing your Panorama in many apps on Windows Phone. Several of the native apps, or “hubs,” on Windows Phone also use the Panorama control, such as those for People, Pictures, Games and Office.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dfa0ca7-1dff-4748-9c6c-1680fa245774/people-hub.jpg"><img loading="lazy" decoding="async" class="130464" title="People Hub" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dfa0ca7-1dff-4748-9c6c-1680fa245774/people-hub.jpg" alt="People Hub" width="700" height="460" /></a><br>
<em>The native People "hub" Panorama without a background image on Windows Phone.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/593c01d1-d5e2-4576-8ae2-288f1062dd06/pictures-hub.jpg"><img loading="lazy" decoding="async" class="130465" title="Pictures Hub" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/593c01d1-d5e2-4576-8ae2-288f1062dd06/pictures-hub.jpg" alt="Pictures Hub" width="700" height="461" /></a><br>
<em>The native Pictures "hub" Panorama with a background image on Windows Phone.</em>

### Optimized for Up to Five Items

While fitting a lot of content into your main Panorama might be tempting, really think through what content will provide the best launch experience, and limit the number of items to five or fewer. Any more than five items will cause users to get lost in the Panorama control and will also result in a performance hit.</p>

### Don’t Compete With Swipe Gestures

The following controls would compete with swipe gestures in a Panorama:

*   Toggle switches,
*   Sliders,
*   Maps,
*   Web browsers.

The Panorama control provides horizontal scrolling to navigate the various items and vertical scrolling for each item. Using a control that accepts gestures for one of these actions in a Panorama would cause it to compete with the native functionality. For example, if a user wants to explore a Panorama control and swipes left in a Map control, then they will pan across the map, rather than move the panorama. For this reason, use only controls that don’t accept swipe gestures. There is one proviso — you could use a Map or Web Browser control in a Panorama as long as it is locked and doesn’t accept touch input.</p>

### Scrollable Items

The items on your Panorama control should scroll either horizontally or vertically, but not both.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eda4e99-e40a-4fa0-add6-5303d9561255/incorrect-panorama.png"><img loading="lazy" decoding="async" class="131931" title="Incorrect Panorama" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eda4e99-e40a-4fa0-add6-5303d9561255/incorrect-panorama.png" alt="Incorrect Panorama" width="618" height="346" /></a><br>
<em>Incorrect layout of Panorama, with items that scroll both horizontally and vertically.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0eb0cfc-ec62-47a0-b80c-fac7845dc228/correct-panorama.png"><img loading="lazy" decoding="async" class="131930" title="Correct Panorama" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0eb0cfc-ec62-47a0-b80c-fac7845dc228/correct-panorama.png" alt="Correct Panorama" width="618" height="280" /></a><br>
<em>Correctly designed Panorama, with items that distinctly scroll either horizontally or vertically.</em>

### Eliminate (or Limit) Interactive Content

The Panorama control is intended to be digested like a magazine cover — it’s a tool to reveal key content for the user and to serve as an entry point to explore the app. The Panorama should not be the application itself, so limit the use of interactive controls in it (forms, search boxes), and put them instead on pages within the app that are designed for those purposes.</p>

### Use the Application Bar for Actions

Avoid floating buttons (i.e. buttons placed within content) where possible. Ideally, all buttons should be placed in the Application Bar and should be changed or hidden contextually as the user swipes across the items.</p>

## Alignment And Layout

### Left-Align Controls, With a 24-Pixel Margin

All pages should respect the 24-pixel margin on the left, which serves as a perimeter for content. Content should be left-aligned to the 24-pixel margin to continue the balance and flow of existing controls. Elements that creep outside or inside the margin create visual imbalance, drawing attention to the inconsistent margin.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8fdd9e-106f-497f-800a-29ed15e38e86/incorrect-alignment.png"><img loading="lazy" decoding="async" class="130472" title="Incorrect Alignment" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8fdd9e-106f-497f-800a-29ed15e38e86/incorrect-alignment.png" alt="Incorrect Alignment" width="244" height="403" /></a><br>
<em>Improper alignment of elements from top to bottom.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce789b8-a2a0-44f6-84d2-a915b6e11e56/correct-alignment.png"><img loading="lazy" decoding="async" class="130471" title="Correct Alignment" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce789b8-a2a0-44f6-84d2-a915b6e11e56/correct-alignment.png" alt="Correct Alignment" width="244" height="403" /></a><br>
<em>Correct left-alignment of elements</em>

<strong>Tip:</strong> Check out Jeff Wilcox’s <a href="https://www.jeff.wilcox.name/2011/10/metrogridhelper/">MetroGridHelper</a> for a great little tool to help ensure that your controls are properly aligned, while also debugging your application.

The MetroGridHelper places a semi-transparent grid of 25 × 25-pixel red squares on your application when running in debug mode. These squares are contained within a padding of 24 pixels around the page and are offset by 12 pixels between one another — the magic combo for Windows Phone design. The grid enables you to quickly and easily identify any alignment issues on the page.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1845070-b574-466b-9b62-98252816e94c/metrogridhelper.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130478" title="MetroGridHelper" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc7cd17a-93a4-4531-bfcd-ae219966917c/metrogridhelper-180x300.png" alt="MetroGridHelper" width="180" height="300" /></a>

Adding MetroGridHelper to your app is very straightforward:

1.  Use the NuGet package manager to install the MetroGridHelper package, and add a reference in your project.
2.  Open the `App.xaml.cs` file, and add `MetroGridHelper.IsVisible = true;` to the constructor within the block of code that checks whether the debugger is attached. Your complete constructor should look like this:

<pre><code class="language-javascript"> /// Constructor for the Application object. ///
        public App()
        {
            // Global handler for uncaught exceptions.

            UnhandledException += Application_UnhandledException;
            // Standard Silverlight initialization
            InitializeComponent();
            // Phone-specific initialization
            InitializePhoneApplication();
            // Show graphics profiling information while debugging.

            if (System.Diagnostics.Debugger.IsAttached)
            {
                // Display the current frame rate counters.

                Application.Current.Host.Settings.EnableFrameRateCounter = true;
                // Show the MetroGridHelper
                MetroGridHelper.IsVisible = true;
                PhoneApplicationService.Current.UserIdleDetectionMode = IdleDetectionMode.Disabled;
            }
        }</code></pre>

### Lay Out Field/Value Pairs Cleanly

When creating a page with a set of field and value pairs, the textblock elements should be presented either in two columns, both aligned left, or with the titles above the fields.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd4dbc9b-e532-4334-a327-ac651d323891/incorrectnamepair.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130498" title="Incorrect Name Pair" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a79ee4e-e451-4734-b9e4-e7e612074479/incorrectnamepair-182x300.png" alt="Incorrect Name Pair" width="182" height="300" /></a><br>
<em>Incorrect layout makes it difficult to discern where the label ends and the value begins.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9ed4f23-2945-428f-93f2-9d00ee830b8f/goodnamepair.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130497" title="Good Name Pair" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31c14805-67d9-48d1-b659-9812d9170dcb/goodnamepair-180x300.png" alt="Good Name Pair" width="180" height="300" /></a><br>
<em>A two-column layout produces an interface that is cleaner and easier to read.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80718702-f306-41fe-9e74-30a8246dd840/bestnamepair.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130496" title="Best Name Pair" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc436de1-504c-480b-8b80-e8f4d7cc1197/bestnamepair-182x300.png" alt="Best Name Pair" width="182" height="300" /></a><br>
<em>Placing the label above the field is the best approach because it creates visual hierarchy and clearly distinguishes between field/value pairs.</em>

### Space Elements by a Multiple or Subdivision of 12 Pixels

Spacing between elements should be consistent both horizontally and vertically. A multiple or subdivision of 12 pixels is recommended in order to adhere to the design grid.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336c9b49-7e15-4b32-82cc-e4ec93cf429b/incorrectspacing.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130521" title="Incorrect Spacing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14adfc57-8254-4c18-8f43-e1a24b8da7a8/incorrectspacing-180x300.png" alt="Incorrect Spacing" width="180" height="300" /></a><br>
<em>Inconsistent horizontal and vertical spacing.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2c53c-e85f-4bb7-b89d-fa3012d2fe5f/correctspacing.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130520" title="Correct Spacing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcabc657-fd63-4288-9355-0f065d23dc36/correctspacing-180x300.png" alt="" width="180" height="300" /></a><br>
<em>Consistent spacing creates a cleaner layout.</em>

## Animation And Visual Feedback

<strong>Tip:</strong> The <a href="https://silverlight.codeplex.com">Silverlight for Windows Phone Toolkit</a> lets you easily add tilt animations, page transitions and a performance progress bar to your application.</p>

### Visual Feedback via Tilt Animations

Buttons, list items and other controls being used as buttons should have a tilt effect to provide visual feedback to the user. Changes in color should not be used for visual feedback.

Visual feedback has the following benefits:

1.  It helps to distinguish between interactive and static elements,
2.  It allows the application to communicate back to the user and confirm the user’s actions.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e718948-6c5b-4e13-a092-70bab42f8593/correctvisualfeedback.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130522" title="Correct Visual Feedback" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0877dfa1-a924-408f-8f06-ca04be6b9a49/correctvisualfeedback-156x300.png" alt="Correct Visual Feedback" width="156" height="300" /></a><br>
<em>Using color changes to provide visual feedback would be inconsistent with native apps.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42f4aae9-0a4e-4b2a-8a1a-67e67285a5b0/incorrectvisualfeedback.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130523" title="Incorrect Visual Feedback" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81532a77-8543-4c75-968e-b9fa2519fa03/incorrectvisualfeedback-158x300.png" alt="Incorrect Visual Feedback" width="158" height="300" /></a><br>
<em>Tilt animation provides visual feedback and makes the user experience consistent.</em>

Implementing the tilt effect requires only a couple of lines of code in your XAML page:

1.  Add a reference to `Microsoft.Phone.Controls.Toolkit.dll` in your project. This DLL is installed with the Silverlight for Windows Phone Toolkit.
2.  Add a `namespace` to the XAML that references the DLL: `xmlns:toolkit="clr-namespace:Microsoft.Phone.Controls;``assembly=Microsoft.Phone.Controls.Toolkit"`.
3.  Set the `IsTiltEnabled` property of `TiltEffect` to `true` in the `PhoneApplicationPage` tag: `toolkit:TiltEffect.IsTiltEnabled="True"`.

That’s it. The final XAML of your <code>PhoneApplicationPage</code> tag should look something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c95a1fbb-9384-4ff9-ad23-a55f2e2a6c28/xaml-tilt.png"><img loading="lazy" decoding="async" class="130553" title="XAML Tilt" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c95a1fbb-9384-4ff9-ad23-a55f2e2a6c28/xaml-tilt.png" alt="XAML Tilt" width="1003" height="423" /></a>

### Use Page Transitions to Add Polish

Page transition animations can add attractive effects to an application and communicate to the user that they are navigating between pages.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6e722aa-afd0-4a26-8bde-9db97e452699/turnstile1.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130559" title="Turns Tile 1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44fe18bb-61ca-4c2e-a42a-34916262e30b/turnstile1-157x300.png" alt="Turns Tile 1" width="157" height="300" /></a><br>
<em>Turnstile page transition.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13f2c2aa-da36-43cd-b5cc-53a6ce6c9917/turnstile2.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130560" title="Turns Tile 2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29a1ecef-11a7-45f4-9af6-756f24d82de5/turnstile2-156x300.png" alt="Turns Tile 2" width="156" height="300" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57a26c36-6a9d-40dd-96e4-6ad72a4d54b9/turnstile3.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130561" title="Turns Tile 3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba107304-da85-4a79-ab97-3f03ab66f1e0/turnstile3-157x300.png" alt="Turns Tile 3" width="157" height="300" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89de61b3-6cee-4f2b-8f80-79e5e43a66e7/turnstile4.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130562" title="Turns Tile 4" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181317a4-0667-486c-be17-155d84371b13/turnstile4-157x300.png" alt="Turns Tile 4" width="157" height="300" /></a><br>
<em>Turnstile page transition.</em>

Six page transitions are included in the Silverlight for Windows Phone Toolkit:

*   Turnstile,
*   Swivel,
*   Slide,
*   Roll,
*   Rotate.

Adding page transition animations is similar to adding the tilt effect:

1.  Add a reference to `Microsoft.Phone.Controls.Toolkit.dll` in your project. This DLL is installed as part of the Silverlight for Windows Phone Toolkit installation.
2.  Add a namespace to the XAML that references the DLL: `xmlns:toolkit="clr-namespace:Microsoft.Phone.Controls;``assembly=Microsoft.Phone.Controls.Toolkit"`.
3.  Paste the XAML code below into your page:

<pre></pre>

### Use a Bar to Indicate Progress

Just as you use tilt animation to indicate to the user that their tap has taken effect, progress bars enable you to communicate that a process is being executed. This removes doubt for the user about whether the application is functioning properly. Two types of progress bars can be used: determinate and indeterminate.
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14558d23-7903-47f2-a22b-6800ea52558c/determinate.png"><img loading="lazy" decoding="async" class="130570" title="Determinate Progress Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14558d23-7903-47f2-a22b-6800ea52558c/determinate.png" alt="Determinate Progress Bar" width="338" height="77" /></a><br>
<em>Determinate progress bar.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181fc16d-51e7-4deb-9336-c3b654b21cb1/indeterminate.png"><img loading="lazy" decoding="async" class="130571" title="Indeterminate Progress Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181fc16d-51e7-4deb-9336-c3b654b21cb1/indeterminate.png" alt="Indeterminate Progress Bar" width="338" height="77" /></a><br>
<em>Indeterminate progress bar.</em>

A determinate progress bar is used to communicate the percentage of completion, such as the percentage of bytes copied out of the total number of bytes. An indeterminate progress bar is much more common and is particularly useful when you don’t know the length of the process, such as when calling a Web service and waiting for a response.</p>

## Buttons

### Place Buttons in the Application Bar

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c249cb2-dac8-4713-bf7c-87a1f403676a/collapsedappbar.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130575" title="Collapsed Application Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebbc889-1f26-4574-81ca-7c7527ddd196/collapsedappbar-300x176.png" alt="Collapsed Application Bar" width="300" height="176" /></a><br>
<em>Collapsed application bar.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/601c83fa-3e16-45e4-a29c-9f7222ca29c1/expandedappbar.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130576" title="Expanded Application Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768ef679-1eec-4599-9b0a-5dd16a8d2140/expandedappbar-300x294.png" alt="Expanded Application Bar" width="300" height="294" /></a><br>
<em>Expanded application bar.</em>

Avoid floating buttons (i.e. buttons placed within content) where possible. Such buttons usually make the experience inconsistent and confusing. The Application Bar serves as a fixed home for buttons on the page, a design paradigm that is consistent with native apps. Another big benefit is that the Application Bar is always visible, even when the software keyboard is shown. This eliminates the common problem of buttons being hidden behind the keyboard, and it allows for instant access to the buttons. Floating buttons might make sense in a few places, though:

*   "Settings" pages, where more verbose actions are needed,
*   Quick action buttons associated with list entries, such as a “Play” button next to a song item or a “Call” button next to a contact item in a list.</p>

### Avoid “Back” and “Close” Buttons

Every Windows Phone has a physical “Back” button. Windows Phone users are used to using the hard “Back” button to navigate back in an application or to end (or cancel) an action, thus eliminating the need for a soft “Back” button. The result is a more consistent experience and less clutter.</p>

### Avoid “Home” Buttons

“Home” buttons break the Windows Phone’s navigation model and are strongly discouraged. Users know to use the hard “Back” button to navigate back to the home screen. A “Home” button might make sense in a few scenarios, though:

*   Applications with a very deep navigation hierarchy,
*   Pages that launch via a deep-linking “secondary tile.”

If you do end up using a “Home” button in your application, make sure that you completely clear out the back stack upon navigating to the home page. This is critical because without clearing the back stack, the user could get stuck in a near infinite loop and would be unable to exit the application via the hard “Back” button. To clear your back stack, override the <code>OnNavigatedTo</code> method on the page that you are navigating to, and add in the code shown here:

<pre><code class="language-javascript">protected override void OnNavigatedTo(System.Windows.Navigation.NavigationEventArgs e)
{
    while (NavigationService.CanGoBack)
    {
        NavigationService.RemoveBackEntry();
    }
    base.OnNavigatedTo(e);
}</code></pre>

The above code is a simple loop which checks to see if the application can go back and removes the most recent item off the back stack. Once it can no longer go back, your back stack has been cleared.</p>

## Summary

One of the most important factors in delivering the best experience on any mobile platform is to design the app for the platform and its accompanying usage patterns.

The Windows Phone UI represents a fresh approach to the phone experience. The first step in building a compelling Windows Phone UI-compliant application is to spend time using the apps that ship with the OS. This will familiarize you with Windows Phone’s unique set of controls and design paradigms.

A lot of beautifully designed third-party apps can be found in the Windows Phone Marketplace, so plenty of inspiration is available. Some of my favorites have innovated on the Windows Phone design principles to deliver a truly compelling experience, such as the <a href="https://cocktailflow.com/">Cocktail Flow</a> app published by Gergely Orosz.

Once you have the basics down and have begun to piece together the visuals for your application, refer to the guidelines in this article. They will help you avoid some of the most common mistakes that I have seen when reviewing designs for my app partners.

{{< signature "al" >}}

