---
title: 'How To Create And Deploy Angular Material Application'
slug: angular-8-material-application-netlify
author: shubham-ssj
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1649ea62-4817-4da5-8b1e-e87a8edc6677/history-page.PNG
date: 2020-01-09T12:30:00.000Z
summary: >-
  A walkthrough of creating an Angular 8 web application and a QR Code generator app completely based on Angular while hosted on Netlify.
description: >-
   This article will help you get started with a new Angular project from just a thought to deployment.
categories:
  - API
  - Apps
  - Angular
  - JavaScript
  - Service Workers
---
<p>Angular is one of the popular choices while creating new web applications. Moreover, “Material Design” specs have become a go-to choice for creating minimal and engaging experience today. Thus, any new “Angular” project mostly uses the “Angular Material Design Library” to use the components which follow the material design specifications. From smooth animations to proper interaction feedback, all of this is already available as part of the official material design library for angular.</p>

<p>After the web application is developed, the next step is to deploy it. That is where “Netlify” comes into the picture. With its very easy to use interface, automatic deployment, traffic splitting for A/B testing and various other features, Netlify is surely a great tool.</p>

<p>The article will be a walkthrough of creating an Angular 8 web application using the official Angular Material Design library. We will be creating a QR Code generator web application completely based on Angular while hosted on Netlify.</p>

[Files for this tutorial](https://github.com/dev4fun007/qr) can be found on GitHub and a demo version is deployed [here](https://genqr.netlify.com/).

## Getting Started

<ol>
<li>Install <a href="https://cli.angular.io/">Angular 8</a>,</li>
<li>Create a <a href="https://github.com/">GitHub</a> account,</li>
<li>Install <a href="https://git-scm.com/downloads">Git</a> on your computer,</li>
<li>Create a <a href="https://www.netlify.com/">Netlify</a> account.</li>
</ol>

<p><strong>Note</strong>: <em>I will be using VSCode and Microsoft Windows as the preferred IDE and OS, though the steps would be similar for any other IDE on any other OS.</em></p>

<p>After the above prerequisites are complete, let’s begin!</p>

{{% feature-panel %}}

## Mocks & Planning

<p>Before we begin creating the project, it would be beneficial to plan ahead: What kind of UI would we want in our application? Will there be any reusable pieces? How will the application interact with external services?

<p>First, check the UI mocks.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ceed97-9dc1-4dfb-94c0-620f508746aa/home-page.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ceed97-9dc1-4dfb-94c0-620f508746aa/home-page.PNG" sizes="100vw" caption="Homepage (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ceed97-9dc1-4dfb-94c0-620f508746aa/home-page.PNG'>Large preview</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d40265-1654-40e6-8995-dc72c26556eb/create-qr-page.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d40265-1654-40e6-8995-dc72c26556eb/create-qr-page.PNG" sizes="100vw" caption="Creating a QR Page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d40265-1654-40e6-8995-dc72c26556eb/create-qr-page.PNG'>Large preview</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1649ea62-4817-4da5-8b1e-e87a8edc6677/history-page.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1649ea62-4817-4da5-8b1e-e87a8edc6677/history-page.PNG" sizes="100vw" caption="History page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1649ea62-4817-4da5-8b1e-e87a8edc6677/history-page.PNG'>Large preview</a>)" alt="" >}}

<p>These are the three different pages which will be contained in the application. The homepage will be the starting point of our application. Creating a QR page should deal with the creation of a new QR code. The History page will show all the saved QR codes.</p>

<p>The mockups not only provide an idea of the look and feel of the application, but they also segregate the responsibility of each page.</p>

<p>One observation (from the mocks) is that it seems that the top navigation bar is common across all the pages. Thus, the navigation bar can be created as a reusable component and reused.</p>

<p>Now that we have a fair bit of an idea as to how the application will look and what can be reused, let’s start.</p>

## Creating A New Angular Project

<p>Launch VSCode, then open a terminal window in VSCode to generate a new Angular project.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd03683b-bdae-4673-862b-1c128521747e/open-terminal.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd03683b-bdae-4673-862b-1c128521747e/open-terminal.PNG" sizes="100vw" caption="Terminal in VSCode (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd03683b-bdae-4673-862b-1c128521747e/open-terminal.PNG'>Large preview</a>)" alt="" >}}

<p>The terminal will open with a default path as shown in the prompt. You can change to a preferred directory before proceeding; in the case of Windows, I will use the <code>cd</code> command.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebcd42e-d4f2-47d6-8889-7319b9deae47/navigate-to-preferred-path.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebcd42e-d4f2-47d6-8889-7319b9deae47/navigate-to-preferred-path.PNG" sizes="100vw" caption="Navigating to the preferred path (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebcd42e-d4f2-47d6-8889-7319b9deae47/navigate-to-preferred-path.PNG'>Large preview</a>)" alt="" >}}

<p>Moving forward, angular-cli has a command to generate new projects <code>ng new &lt;project-name&gt;</code>. Just use any fancy project name you like and press enter, e.g. <code>ng new qr</code>.</p>

<p>This will trigger the angular-cli magic; it will provide a few options to configure some aspects of the project, for instance, adding angular routing. Then, based on the selected options, it will generate the whole project skeleton which can be run without any modification.</p>

<p>For this tutorial, enter <strong>Yes</strong> for routing and select <strong>CSS</strong> for styling. This will generate a new Angular project:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d872bd01-0926-4ca7-8790-a4ad691b1520/create-new-angular-project.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d872bd01-0926-4ca7-8790-a4ad691b1520/create-new-angular-project.PNG" sizes="100vw" caption="Creating a new Angular project (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d872bd01-0926-4ca7-8790-a4ad691b1520/create-new-angular-project.PNG'>Large preview</a>)" alt="" >}}

<p>We now have got ourselves a fully working Angular project. In order to make sure everything is working properly, we can run the project by entering this command in the terminal: <code>ng serve</code>. Uh oh, but wait, this results in an error. What could have happened?</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fc36768-ce23-40eb-884d-1b0f29740ce2/ng-serve-error.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fc36768-ce23-40eb-884d-1b0f29740ce2/ng-serve-error.PNG" sizes="100vw" caption="ng serve error (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fc36768-ce23-40eb-884d-1b0f29740ce2/ng-serve-error.PNG'>Large preview</a>)" alt="" >}}

<p>Don’t worry. Whenever you create a new project using angular-cli, it generates the whole skeleton inside a folder named after the project name specified in the command <code>ng new qr</code>. Here, we will have to change the current working directory to the one just created. In Windows, use the command <code>cd qr</code> to change directory.</p>

<p>Now, try running the project again with the help of <code>ng serve</code>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad1c54a-f220-4cbe-bb21-01f181b43c53/project-running.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad1c54a-f220-4cbe-bb21-01f181b43c53/project-running.PNG" sizes="100vw" caption="Project running (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad1c54a-f220-4cbe-bb21-01f181b43c53/project-running.PNG'>Large preview</a>)" alt="" >}}

<p>Open a web browser, go to the URL <a href="https://localhost:4200">https://localhost:4200</a> to see the project running. The command <code>ng serve</code> runs the application on port 4200 by default.</p>

<p><strong>TIP</strong>: <em>To run it on a different port, we use the command</em> <code>ng serve --port &lt;any-port&gt;</code> <em>for instance,</em> <code>ng serve --port 3000</code>.</p>

<p>This ensures that our basic Angular project is up and running. Let’s move on.</p>

<p>We need to add the project folder to VSCode. Go to the “File” menu and select “Open Folder” and select the project folder. The project folder will now be shown in the Explorer view on the left.</p>

## Adding Angular Material Library

<p>To install the Angular material library, use the following command in the terminal window: <code>ng add @angular/material</code>. This will (again) ask some questions such as which theme you want, whether you want default animations, whether touch support is required, among others. We will just select the default <code>Indigo/Pink</code> theme, <code>Yes</code> to adding <code>HammerJS</code> library and browser animations.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851aeaf1-87f9-43ae-9f87-f7c425be4586/adding-angular-material.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851aeaf1-87f9-43ae-9f87-f7c425be4586/adding-angular-material.PNG" sizes="100vw" caption="Adding Angular material (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851aeaf1-87f9-43ae-9f87-f7c425be4586/adding-angular-material.PNG'>Large preview</a>)" alt="" >}}

<p>The above command also configures the whole project to enable support for the material components.</p>

<ol>
  <li>It adds project dependencies to <em>package.json</em>,</li>
  <li>It adds the Roboto font to the <em>index.html</em> file,</li>
  <li>It adds the Material Design icon font to your <em>index.html</em>,</li>
  <li>It also adds a few global CSS styles to:
    <ul>
      <li>Remove margins from the body,</li>
      <li>Set <code>height: 100%</code> into the HTML and body,</li>
      <li>Set Roboto as the default application font.</li>
    </ul></li>
</ol>

<p>Just to be sure that everything is fine you can run the project again at this point, though you will not notice anything new.</p>

## Adding Home Page

<p>Our project skeleton is now ready. Let’s start by adding the homepage.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ceed97-9dc1-4dfb-94c0-620f508746aa/home-page.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ceed97-9dc1-4dfb-94c0-620f508746aa/home-page.PNG" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ceed97-9dc1-4dfb-94c0-620f508746aa/home-page.PNG'>Large preview</a>)" alt="" >}}

<p>We want to keep our homepage simple, just like the above picture. This home page uses a few angular material components. Let’s dissect.</p>

<ol>
<li>The top bar is a simple HTML <code>nav</code> element which contains material style button, <code>mat-button</code>, with an image and a text as its child. The bar color is the same as the primary color which was selected while adding Angular material library;</li>
<li>A centered image;</li>
<li>Another, <code>mat-button</code>, with just a text as its child. This button will allow users to navigate to the history page;</li>
<li>A count badge, <code>matBadge</code>, attached to the above button, showing the number of QR codes saved by the user;</li>
<li>A floating action button, <code>mat-fab</code>, at the bottom right corner having the accent color from the selected theme.</li>
</ol>

<p>Digressing a little, let’s add other required components and services first.</p>

### Adding Header

<p>As planned previously, the navigation bar should be reused, let’s create it as a separate angular component. Open terminal in VSCode and type <code>ng g c header</code> (short for ng generate component header) and press Enter. This will create a new folder named “header” which will contain four files:</p>

<ul>
  <li><em>header.component.css</em>: used to provide styling for this component;</li>
  <li><em>header.component.html</em>: for adding HTML elements;</li>
  <li><em>header.component.spec.ts</em>: for writing test cases;</li>
  <li><em>header.component.ts</em>: to add the Typescript-based logic.</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4bed524-0b8e-4efe-8275-4757679547c6/header-component.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4bed524-0b8e-4efe-8275-4757679547c6/header-component.PNG" sizes="100vw" caption="Header component (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4bed524-0b8e-4efe-8275-4757679547c6/header-component.PNG'>Large preview</a>)" alt="" >}}

<p>To make the header look like as it was in the mocks, add the below HTML in <em>header.component.html</em>:</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav class="navbar" [class.mat-elevation-z8]=true&gt;
   &lt;div&gt;
       &lt;button *ngIf="showBackButton" aria-hidden=false mat-icon-button routerLink="/"&gt;
           &lt;mat-icon style="color: white;"&gt;
               &lt;i class="material-icons md-32"&gt;arrow_back&lt;/i&gt;
           &lt;/mat-icon&gt;
       &lt;/button&gt;
       &lt;span style="padding-left: 8px; color: white;"&gt;{{currentTitle}}&lt;/span&gt;
   &lt;/div&gt;
   &lt;button *ngIf="!showBackButton" aria-hidden=false mat-button class="button"&gt;
       &lt;img src="../../assets/qr-icon-white.png" style="width: 40px;"&gt;
       &lt;span style="padding-left: 8px;"&gt;QR Generator&lt;/span&gt;
   &lt;/button&gt;
   &lt;button *ngIf="showHistoryNav" aria-hidden=false mat-button class="button" routerLink="/history"&gt;
       &lt;span style="padding-left: 8px;">History&lt;/span&gt;
   &lt;/button&gt;
&lt;/nav&gt;</code></pre>
</div>

<p><strong>TIP</strong>: <em>To add elevation for any material component use</em> <code>[class.mat-elevation-z8]=true</code>, <em>the elevation value can be changed by changing</em> <strong>z</strong> <em>value, in this case it is</em> <code>z8</code>. <em>For instance, to change the elevation to 16, use</em> <code>[class.mat-elevation-z16]=true</code>.</p>

<p>In the above HTML snippet, there are two Angular material elements being used: <code>mat-icon</code> and <code>mat-button/mat-icon-button</code>. Their usage is very simple; first, we need to add those two as modules in our <em>app.module.ts</em> as shown below:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed9b641e-d89a-44c2-9d6f-742e276251ef/module-import-for-mat-icon-and-mat-button.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed9b641e-d89a-44c2-9d6f-742e276251ef/module-import-for-mat-icon-and-mat-button.PNG" sizes="100vw" caption="Module import for <code>mat-icon</code> and <code>mat-button</code> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed9b641e-d89a-44c2-9d6f-742e276251ef/module-import-for-mat-icon-and-mat-button.PNG'>Large preview</a>)" alt="" >}}

<p>This will allow us to use these two Angular material elements anywhere in any component.</p>

<p>For adding material buttons, the following HTML snippet is used:</p>

<pre><code class="language-html">&lt;button mat-button&gt;
Material Button
&lt;/button&gt;</code></pre>

<p>There are different <a href="https://material.angular.io/components/button/overview">types</a> of material button elements available in the Angular material library such as <code>mat-raised-button</code>, <code>mat-flat-button</code>, <code>mat-fab</code> and others; just replace the <code>mat-button</code> in the above code snippet with any other type.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98236d1f-6301-4799-9f7c-e247d4533158/types-of-material-buttons.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98236d1f-6301-4799-9f7c-e247d4533158/types-of-material-buttons.PNG" sizes="70vw" caption="Types of material buttons (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98236d1f-6301-4799-9f7c-e247d4533158/types-of-material-buttons.PNG'>Large preview</a>)" alt="" >}}

<p>The other element is <code>mat-icon</code> which is used to show icons available in the material icon library. When the Angular material library was added in the beginning, then a reference to the material icon library was added as well, which enabled us to use icons from the vast array of icons.</p>

<p>The usage is as simple as:</p>

<pre><code class="language-html">&lt;mat-icon style="color: white;"&gt;
&lt;i class="material-icons md-32"&gt;arrow_back&lt;/i&gt;
&lt;/mat-icon&gt;</code></pre>

<p>The nested <code>&lt;i&gt;</code> tag can be used to change the icon size (here it’s <code>md-32</code>) which will make the icon size 32px in height and width. This value can be <code>md-24</code>, <code>md-48</code>, and so on. The value of the nested <code>&lt;i&gt;</code> tag is the name of the icon. (The name can be found <a href="https://material.io/resources/icons/?style=baseline">here</a> for any other icon.)</p>

#### Accessibility

<p>Whenever icons or images are used, it is imperative that they provide sufficient information for accessibility purposes or for a screen-reader user. ARIA (Accessible Rich Internet Applications) defines a way to make web content and web applications more accessible to people with disabilities.</p>

<p>One point to note is that the HTML elements which do have their native semantics (e.g. <code>nav</code>) do not need ARIA attributes; the screenreader would already know that <code>nav</code> is a navigation element and read it as such.</p>

<p>The ARIA specs is split into three categories: roles, states and properties. Let’s say that a <code>div</code> is used to create a progress bar in the HTML code. It does not have any native semantics; ARIA role can describe this widget as a progress bar, ARIA property can denote its characteristic such as it can be dragged. ARIA state will describe its current state such as the current value of the progress bar. See the snippet below:</p>

<div class="break-out">

<pre><code class="language-html">&lt;div id="percent-loaded" role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100"&gt; &lt;/div&gt;</code></pre>
</div>

<p>Similarly, a very commonly used aria attribute: <code>aria-hidden=true/false</code> is used. The value true makes that element invisible to screen-readers.</p>

<p>Since most of the UI elements used in this application have native semantic meaning, the only ARIA attributes used are to specify ARIA visibility states.For detailed information, refer to <a href="https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics">this</a>.</p>

<p>The <em>header.component.html</em> does contain some logic to hide and show back button depending on the current page. Moreover, the Home button also contains an image/logo which should be added to the <code>/assets</code> folder. Download the image from <a href="https://raw.githubusercontent.com/dev4fun007/qr-gen/master/src/assets/qr-icon-white.png">here</a> and save it in the <code>/assets</code> folder.</p>

<p>For styling of the navigation bar, add the below css in <em>header.component.css</em>:</p>

<pre><code class="language-css">.navbar {
   position: fixed;
   top: 0;
   left: 0;
   right: 0;
   z-index: 2;
   background: #3f51b5;
   display: flex;
   flex-wrap: wrap;
   align-items: center;
   padding: 12px 16px;
}
.button {
   color: white;
   margin: 0px 10px;
}</code></pre>

<p>As we want to keep the header component reusable across other components, thus to decide what should be shown, we will require those as parameters from other components. This requires usage of <code>@Input()</code> decorator which will bind to the variables we used in <em>header.component.html</em>.</p>

<p>Add these lines in the <em>header.component.ts</em> file:</p>

<pre><code class="language-css">// Add these three lines above the constructor entry.
 @Input() showBackButton: boolean;
 @Input() currentTitle: string;
 @Input() showHistoryNav: boolean;

 constructor() { }</code></pre>

<p>The above three bindings will be passed as a parameter from other components which the header component will be using. Its usage will be more clear once we move forward.</p>

<p>Moving on, we need to create a homepage that can be represented by an Angular component. So let’s start by creating another component; type <code>ng g c home</code> in the terminal to auto-generate the home component. As previously, a new folder named “home” will be created containing four different files. Before proceeding to modify those files, let’s add some routing information to angular routing module.</p>

{{% ad-panel-leaderboard %}}

#### Adding Routing

<p>Angular provides a way to map URL to a specific component. Whenever some navigation happens, the Angular framework monitors the URL and based on the information present in the <em>app-routing.module.ts</em> file; it initializes the mapped component. This way different components are does not need to shoulder the responsibility of initializing other components. In our case, the application has three pages navigable by clicking on different buttons. We achieve this by leveraging the routing support provided by the Angular framework.</p>

<p>The home component should be the starting point of the application. Let’s add this information to the <em>app-routing.module.ts</em> file.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da49761a-aada-4034-8d6a-6c5494bb4b64/routing-home-component.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da49761a-aada-4034-8d6a-6c5494bb4b64/routing-home-component.PNG" sizes="100vw" caption="Routing Home Component (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da49761a-aada-4034-8d6a-6c5494bb4b64/routing-home-component.PNG'>Large preview</a>)" alt="" >}}

<p>The <code>path</code> property is set as an empty string; this enables us to map the application URL to the homepage component, something like <code>google.com</code> which shows the Google homepage.</p>

<p><strong>TIP</strong>: <em>Path value never starts with a</em> “<code>/</code>”, <em>but instead uses an empty string even though path can be like</em> <code>search/coffee</code>.</p>

<p>Moving back to the homepage component, replace the content of <em>home.component.html</em> with this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;app-header [showBackButton]="false" [currentTitle]=""&gt;&lt;/app-header&gt;
&lt;app-profile&gt;&lt;/app-profile&gt;

&lt;!-- FAB Fixed --&gt;
&lt;button mat-fab class="fab-bottom-right" routerLink="/create"&gt;
   &lt;mat-icon&gt;
       &lt;i class="material-icons md-48"&gt;add&lt;/i&gt;
   &lt;/mat-icon&gt;
&lt;/button&gt;</code></pre>
</div>

<p>There are three parts to the home component:</p>

<ol>
  <li>The reusable header component <code>&lt;app-header&gt;</code>,</li>
  <li>Profile component <code>&lt;app-profile&gt;</code>,</li>
  <li>The floating action button at the bottom right.</li>
</ol>

<p>The above HTML snippet shows how the reusable header component is used in other components; we just use the component selector and pass in the required parameters.</p>

<p>Profile component is created to be used as the body for the homepage &mdash; we will create it soon.</p>

<p>The floating action button with the <code>+</code> icon is a kind of Angular material button of type <code>mat-fab</code> on the bottom right of the screen. It has the <code>routerLink</code> attribute directive which uses the route information provided in the <code>app-routing.module.ts</code> for navigation. In this case, the button has the route value as <strong>/create</strong> which will be mapped to create component.</p>

<p>To make the create button float on bottom right, add the below CSS code in <em>home.component.css</em>:</p>

<pre><code class="language-css">.fab-bottom-right {
   position: fixed;
   left: auto;
   bottom: 5%;
   right: 10%;
}</code></pre>

<p>Since profile component is supposed to manage home page body, we will leave <code>home.component.ts</code> intact.</p>

#### Adding Profile Component

<p>Open terminal, type <code>ng g c profile</code> and press enter to generate profile component. As planned earlier, this component will handle the main body of the home page. Open <code>profile.component.html</code> and replace its content with this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;div class="center profile-child"&gt;
   &lt;img class="avatar" src="../../assets/avatar.png"&gt;
   &lt;div class="profile-actions"&gt;
       &lt;button mat-raised-button matBadge="{{historyCount}}"    matBadgeOverlap="true" matBadgeSize="medium" matBadgeColor="accent"
           color="primary" routerLink="/history"&gt;
           &lt;span>History&lt;/span&gt;
       &lt;/button&gt;
   &lt;/div&gt;
&lt;/div&gt;</code></pre>
</div>

<p>The above HTML snippet shows how to use the <code>matBadge</code> element of the material library. To be able to use it here, we need to follow the usual drill of adding <code>MatBadgeModule</code> to <code>app.module.ts</code> file. Badges are small pictorial status descriptor for UI elements such as buttons or icons or texts. In this case, it is used with a button to show count of QR saved by the user. Angular material library badge has various other properties such as setting the position of the badge with <code>matBadgePosition</code>, <code>matBadgeSize</code> to specify size, and <code>matBadgeColor</code> to set the badge color.</p>

<p>One more image asset needs to be added to the assets folder: <a href="https://raw.githubusercontent.com/dev4fun007/qr-gen/master/src/assets/avatar.png">Download</a>. Save the same to the <code>/assets</code> folder of the project.</p>

<p>Open <em>profile.component.css</em> and add this:</p>

<pre><code class="language-css">.center {
   top: 50%;
   left: 50%;
   position: absolute;
   transform: translate(-50%, -50%);
}


.profile-child {
   display: flex;
   flex-direction: column;
   align-items: center;
}


.profile-actions {
   padding-top: 20px;
}


.avatar {
   border-radius: 50%;
   width: 180px;
   height: 180px;
}</code></pre>

<p>The above CSS will achieve the UI as planned.</p>

<p>Moving on, we need some kind of logic to update the history count value as it will reflect in the <code>matBadge</code> used earlier. Open <em>profile.component.ts</em> and add the following snippet appropriately:</p>

<div class="break-out">

<pre><code class="language-css">export class ProfileComponent implements OnInit {

 historyCount = 0;
 constructor(private storageUtilService: StorageutilService) { }

 ngOnInit() {
   this.updateHistoryCount();
 }

 updateHistoryCount() {
   this.historyCount = this.storageUtilService.getHistoryCount();
 }
}</code></pre>
</div>

<p>We have added <strong>StorageutilService</strong> but we have not created such a service untill now. Ignoring the error, we have completed our profile component which also finishes off our homepage component. We will revisit this profile component after creating our storage utility service. Okay, then let’s do so.</p>

### Local Storage

<p>HTML5 provides web storage feature which can be used to store data locally. This provides much more storage compared to cookies &mdash; at least 5MB vs 4KB. There are two types of web storage with different scope and lifetime: <strong>Local</strong> and <strong>Session</strong>. The former can store data permanently while the latter is temporary and for a single session. The decision to select the type can be based on the use case, in our scenario we want to save across sessions, so we will go with <strong>Local</strong> storage.</p>

<p>Each piece of data is stored in a key/value pair. We will use the text for which the QR is generated as the key and the QR image encoded as a base64 string as the value. Create an entity folder, inside the folder create a new <em>qr-object.ts</em> file and add the code snippet as shown:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e2d8ae3-c704-4d7f-9583-6e859227b509/qr-entity-model.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e2d8ae3-c704-4d7f-9583-6e859227b509/qr-entity-model.PNG" sizes="100vw" caption="QR entity model (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e2d8ae3-c704-4d7f-9583-6e859227b509/qr-entity-model.PNG'>Large preview</a>)" alt="" >}}

<p>The content of the class:</p>

<pre><code class="language-css">export class QR {

   text:           string;
   imageBase64:    string;

   constructor(text: string, imageBase64: string) {
       this.imageBase64 = imageBase64;
       this.text = text;
   }

}</code></pre>

<p>Whenever the user saves the generated QR, we will create an object of the above class and save that object using the storage utility service.</p>

<p>Create a new service folder, we will be creating many services, it’s better to group them together.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1703a040-c680-4aa3-9274-b2c0b019154e/services-folder.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1703a040-c680-4aa3-9274-b2c0b019154e/services-folder.PNG" sizes="100vw" caption="Services Folder (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1703a040-c680-4aa3-9274-b2c0b019154e/services-folder.PNG'>Large preview</a>)" alt="" >}}

<p>Change the current working directory to services, <code>cd services</code>, to create a new service use <code>ng g s &lt;any name&gt;</code>. This is a shorthand to <code>ng generate service &lt;any name&gt;</code>, type <code>ng g s storageutil</code> and press enter

<p>This will create two files:</p>

<ul>
  <li><em>storageutil.service.ts</em></li>
  <li><em>storageutil.service.spec.ts</em></li>
</ul>

<p>The latter is for writing unit tests. Open <em>storageutil.service.ts</em> and add this:</p>

<pre><code class="language-css">private historyCount: number;
 constructor() { }

 saveHistory(key : string, item :string) {
   localStorage.setItem(key, item)
   this.historyCount = this.historyCount + 1;
 }

 readHistory(key : string) : string {
   return localStorage.getItem(key)
 }

 readAllHistory() : Array&lt;QR&gt; {
   const qrList = new Array&lt;QR&gt;();

   for (let i = 0; i < localStorage.length; i++) {
     const key = localStorage.key(i);
     const value = localStorage.getItem(key);
     if (key && value) {
       const qr = new QR(key, value);
       qrList.push(qr);
     }
   }
   this.historyCount = qrList.length;
   return qrList;
 }

 getHistoryCount(): number {
   if (this.historyCount) {
     return this.historyCount;
   }
   this.readAllHistory();
   return this.historyCount;
 }

 deleteHistory(key : string) {
   localStorage.removeItem(key)
   this.historyCount = this.historyCount - 1;
 }</code></pre>

<p>Import the qr-object class to correct any errors. To use the local storage feature, there is no need to import anything new just use the keyword <code>localStorage</code> to save or get value based on a key.</p>

<p>Now open the <em>profile.component.ts</em> file again and import the <code>StorageutilService</code> class to properly finish off the profile component.</p>

<p>Running the project, we can see the homepage is up as planned.</p>

## Adding Create QR Page

<p>We have our homepage ready, though the create/add button does not do anything. Worry not, the actual logic was already written. We used a <code>routerLink</code> directive to change the base path of the URL to <code>/create</code> but there was no mapping added to the <em>app-routing.module.ts</em> file.</p>

<p>Let’s create a component which will deal with the creation of new QR codes, type <code>ng g c create-qr</code> and press enter to generate a new component.</p>

<p>Open the <em>app-routing.module.ts</em> file and add the below entry to the <code>routes</code> array:</p>

<pre><code class="language-css">{ path: 'create', component: CreateQrComponent },</code></pre>

<p>This will map the <code>CreateQRComponent</code> with the URL <code>/create</code>.</p>

<p>Open <em>create-qr.components.html</em> and replace the contents with this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;app-header [showBackButton]="showBackButton" [currentTitle]="title" [showHistoryNav]="showHistoryNav"&gt;&lt;/app-header&gt;


&lt;mat-card class="qrCard" [class.mat-elevation-z12]=true&gt;
   &lt;div class="qrContent"&gt;

       &lt;!--Close button section--&gt;
       &lt;div class="closeBtn"&gt;
           &lt;button mat-icon-button color="accent" routerLink="/" matTooltip="Close"&gt;
               &lt;mat-icon&gt;
                   &lt;i class="material-icons md-48"&gt;close&lt;/i&gt;
               &lt;/mat-icon&gt;
           &lt;/button&gt;
       &lt;/div&gt;

       &lt;!--QR code image section--&gt;
       &lt;div class="qrImgDiv"&gt;
           &lt;img *ngIf="!showProgressSpinner" style="padding: 5px 5px;" src={{qrCodeImage}} width="200px" height="200px"&gt;
           &lt;mat-spinner *ngIf="showProgressSpinner"&gt;&lt;/mat-spinner&gt;
           &lt;div class="actionButtons" *ngIf="!showProgressSpinner"&gt;
               &lt;button mat-icon-button color="accent" matTooltip="Share this QR" style="margin: 0 5px;"&gt;
                   &lt;mat-icon&gt;
                       &lt;i class="material-icons md-48"&gt;share&lt;/i&gt;
                   &lt;/mat-icon&gt;
               &lt;/button&gt;
               &lt;button mat-icon-button color="accent" (click)="saveQR()" matTooltip="Save this QR" style="margin: 0 5px;"&gt;
                   &lt;mat-icon&gt;
                       &lt;i class="material-icons md-48"&gt;save&lt;/i&gt;
                   &lt;/mat-icon&gt;
               &lt;/button&gt;
           &lt;/div&gt;
       &lt;/div&gt;

       &lt;!--Textarea to write any text or link--&gt;
       &lt;div class="qrTextAreaDiv"&gt;
           &lt;mat-form-field style="width: 80%;"&gt;
               &lt;textarea matInput [(ngModel)]="qrText" cdkTextareaAutosize cdkAutosizeMinRows="4" cdkAutosizeMaxRows="4"
                   placeholder="Enter a website link or any text..."&gt;&lt;/textarea&gt;
           &lt;/mat-form-field&gt;
       &lt;/div&gt;

       &lt;!--Create Button--&gt;
       &lt;div class="createBtnDiv"&gt;
           &lt;button class="createBtn" mat-raised-button color="accent" matTooltip="Create new QR code" matTooltipPosition="above"
               (click)="createQrCode()"&gt;Create&lt;/button&gt;
       &lt;/div&gt;
   &lt;/div&gt;
&lt;/mat-card&gt;</code></pre>
</div>

<p>The above snippet uses many of the Angular material library elements. As planned, it has one header component reference wherein the required parameters are passed. Next up is the main body of the create page; it consists of one Angular material card or <code>mat-card</code> centered and elevated up to 12px as <code>[class.mat-elevation-z12]=true</code> is used.</p>

<p>The material card is just another kind of container that can be used as any other <code>div</code> tag. Although the material library provides some properties to lay out well-defined information in a <code>mat-card</code> such as image placement, title, subtitle, description and action as can be seen below.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6b87cf-65e4-48fe-bd3a-acd4a2f11c03/card-example.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6b87cf-65e4-48fe-bd3a-acd4a2f11c03/card-example.PNG" sizes="70vw" caption="Card example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6b87cf-65e4-48fe-bd3a-acd4a2f11c03/card-example.PNG'>Large preview</a>)" alt="" >}}

<p>In the above HTML snippet, we have used <code>mat-card</code> just as any other container. Another material library element used is <code>matTooltip</code>; it is just another tooltip with ease of use, displayed when the user hovers over or longpresses an element. Just use the snippet below to show tooltip:</p>

<pre><code class="language-css">matTooltip="Any text you want to show"</code></pre>

<p>It can be used with icon buttons or any other UI element to convey extra information. In application context, it is displaying information about the close icon button. To change the placement of the tooltip, <code>matTooltipPosition</code> is used:</p>

<div class="break-out">

<pre><code class="language-css">matTooltip="Any text you want to show" matTooltipPosition="above"</code></pre>
</div>

<p>Besides <code>matTooltip</code>, <code>mat-spinner</code> is used to show loading progress. When the user clicks on the “Create” button, a network call is made. This is when the progress spinner is shown. When the network call returns with result, we just hide the spinner. It can be used simply like this:</p>

<pre><code class="language-html">&lt;mat-spinner *ngIf="showProgressSpinner"&gt;&lt;/mat-spinner&gt;</code></pre>

<p><code>showProgressSpinner</code> is a Boolean variable which is used to show/hide the progress spinner. The library also provides some other parameters like <code>[color]='accent'</code> to change color, <code>[mode]='indeterminate'</code> to change the progress spinner type. An indeterminate progress spinner will not show the progress of the task while a determinate one can have different values to reflect task progress. Here, an indeterminate spinner is used as we do not know how long the network call will take.</p>

<p>The material library provides a variant of textarea conforming to the material guideline but it can only be used as a descendent of <code>mat-form-field</code>. Usage of material textarea is just as simple as the default HTML one, like below:</p>

<pre><code class="language-html">&lt;mat-form-field&gt;
   &lt;textarea matInput placeholder="Hint text"&gt;&lt;/textarea&gt;
&lt;/mat-form-field&gt;</code></pre>

<p><code>matInput</code> is a directive which allows native <code>input</code> tag to work with <code>mat-form-field</code>. The <code>placeholder</code> property allows adding any hint text for the user.</p>

<p><strong>TIP</strong>: <em>Use the</em> <code>cdkTextareaAutosize</code> <em>textarea property to make it auto-resizable. Use</em> <code>cdkAutosizeMinRows</code> <em>and</em> <code>cdkAutosizeMaxRows</code> <em>to set rows and columns and all three together to make textarea auto-resize till it reaches the max rows and columns limit set.</em></p>

<p>To use all these material library elements, we need to add them in the <em>app.module.ts</em> file.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/178063a8-7131-4734-ab12-159f689a3bd8/create-qr-module-imports.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/178063a8-7131-4734-ab12-159f689a3bd8/create-qr-module-imports.PNG" sizes="100vw" caption="Creating QR module imports (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/178063a8-7131-4734-ab12-159f689a3bd8/create-qr-module-imports.PNG'>Large preview</a>)" alt="" >}}

<p>There is a placeholder image being used in the HTML. <a href="https://raw.githubusercontent.com/dev4fun007/qr-gen/master/src/assets/download.png">Download</a> and save it to the <code>/assets</code> folder.</p>

<p>The above HTML also requires CSS styling, so open the <em>create-qr.component.ts</em> file and add the following:</p>

<pre><code class="language-css">.qrCard {
   display: flex;
   flex-direction: column;
   align-items: center;
   position: absolute;
   top: 50%;
   left: 50%;
   transform: translate(-50%, -50%);
   width: 20%;
   height: 65%;
   padding: 50px 20px;
}

.qrContent {
   display: flex;
   flex-direction: column;
   align-items: center;
   width: 100%;
}

.qrTextAreaDiv {
   width: 100%;
   display: flex;
   flex-direction: row;
   justify-content: center;
   padding: 0px 0px;
   position: absolute;
   bottom: 10%;
}

.createBtn {
   left: 50%;
   transform: translate(-50%, 0px);
   width: 80%;
}

.createBtnDiv {
   position: absolute;
   bottom: 5%;
   width: 100%;
}


.closeBtn {
   display: flex;
   flex-direction: row-reverse;
   align-items: flex-end;
   width: 100%;
   margin-bottom: 20px;
}

.closeBtnFont {
   font-size: 32px;
   color: rgba(0,0,0,0.75);
}

.qrImgDiv {
   top: 20%;
   position: absolute;
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;
   width: 100%;
}
.actionButtons {
   display: flex;
   flex-direction: row;
   padding-top: 20px;
}</code></pre>

<p>Let’s wire up the UI with logic. Open the <em>create-qr.component.ts</em> file and add the below code, leaving those lines which are already present:</p>

<div class="break-out">

<pre><code class="language-javascript">export class CreateQrComponent implements OnInit {

 qrCodeImage = '../../../assets/download.png';
 showProgressSpinner = false;
 qrText: string;
 currentQR;
 showBackButton = true;
 title = 'Generate New QR Code';
 showHistoryNav = true;

 constructor(private snackBar: MatSnackBar,
     private restutil: RestutilService,
     private storageService: StorageutilService) { }

 ngOnInit() {
 }

 createQrCode() {
   //Check if any value is given for the qr code text
   if (!!this.qrText) {
     //Make the http call to load qr code
     this.loadQRCodeImage(this.qrText);
   } else {
     //Show snackbar
     this.showSnackbar('Enter some text first')
   }
 }

 public loadQRCodeImage(text: string) {
   // Show progress spinner as the request is being made
   this.showProgressSpinner = true;
   // Trigger the API call
   this.restutil.getQRCode(text).subscribe(image =>{
     // Received the result - as an image blob - require parsing
     this.createImageBlob(image);
   }, error => {
     console.log('Cannot fetch QR code from the url', error)
     // Hide the spinner - show a proper error message
     this.showProgressSpinner = false;
   });
 }

 private createImageBlob(image: Blob) {
   // Create a file reader to read the image blob
   const reader = new FileReader();
   // Add event listener for "load" - invoked once the blob reading is complete
   reader.addEventListener('load', () => {
     this.qrCodeImage = reader.result.toString();
     //Hide the progress spinner
     this.showProgressSpinner = false;
     this.currentQR = reader.result.toString();
   }, false);
   // Read image blob if it is not null or undefined
   if (image) {
     reader.readAsDataURL(image);
   }
 }

 saveQR() {
   if (!!this.qrText) {
     this.storageService.saveHistory(this.qrText, this.currentQR);
     this.showSnackbar('QR saved')
   } else {
     //Show snackbar
     this.showSnackbar('Enter some text first')
   }

 }

 showSnackbar(msg: string) {
   //Show snackbar
   this.snackBar.open(msg, '', {
     duration: 2000,
   });
 }
}</code></pre>
</div>

<p>To provide users contextual information, we also use <code>MatSnackBar</code> from the material design library. This shows up as a popup from below the screen and stays for a few seconds before disappearing. This is not an element but rather a service that can be invoked from the Typescript code.</p>

<p>The above snippet with the method name <code>showSnackbar</code> shows how to open up a snackbar, but before it can be used, we need to add the <code>MatSnackBar</code> entry in the <em>app.module.ts</em> file just like we did for other material library elements.</p>

<p><strong>TIP</strong>: <em>In recent Angular material library versions, there is no straightforward way to change the snackbar styling. Instead, one has to make two additions to the code.</em></p>

<p>First, use the below CSS to alter background and foreground colors:</p>

<pre><code class="language-css">::ng-deep snack-bar-container.snackbarColor {
   background-color: rgba(63, 81, 181, 1);
}
::ng-deep .snackbarColor .mat-simple-snackbar {
   color: white;
 }</code></pre>

<p>Second, use a property called <code>panelClass</code> to set the style to the above CSS class:</p>

<pre><code class="language-css">this.snackBar.open(msg, '', {
     duration: 2000,
     panelClass: ['snackbarColor']
   });</code></pre>

<p>The above two combinations will allow custom styling to the material design library snackbar component.</p>

<p>This completes the steps on how to create a QR page, but there is one piece still missing. Checking the <em>create-qr.component.ts</em> file, it will show an error regarding the missing piece. The missing piece to this puzzle is <code>RestutilService</code> which is responsible for fetching the QR code image from the third-party <a href="https://goqr.me/api/">API</a>.</p>

<p>In the terminal, change the current directory to services by typing in <code>ng g s restutil</code> and pressing Enter. This will create the RestUtilService files. Open the <em>restutil.service.ts</em> file and add this snippet:</p>

<div class="break-out">

<pre><code class="language-javascript">private edgeSize = '300';
 private BASE_URL = 'https://api.qrserver.com/v1/create-qr-code/?data={data}!&size={edge}x{edge}';

 constructor(private httpClient: HttpClient) { }

 public getQRCode(text: string): Observable<Blob> {
   // Create the url with the provided data and other options
   let url = this.BASE_URL;
   url = url.replace("{data}", text).replace(/{edge}/g, this.edgeSize);
   // Make the http api call to the url
   return this.httpClient.get(url, {
     responseType: 'blob'
   });
 }</code></pre>
</div>

<p>The above service fetches the QR image from the third-party API and since the response is not of JSON type, but an image, so we specify the <code>responseType</code> as <code>'blob'</code> in the above snippet.</p>

<p>Angular provides <code>HttpClient</code> class to communicate with any HTTP supporting server. It provides many features like filtering the request before it is fired, getting back the response, enabling the processing of the response via callbacks and others. To use the same, add an entry for the <em>HttpClientModule</em> in <em>app.module.ts</em> file.</p>

<p>Finally, import this service into the <em>create-qr.component.ts</em> file to complete creating the QR code.</p>

<p>But wait! There is a problem with the above create QR logic. If the user uses the same text to generate the QR again and again, it will result in a network call. One way to redress this is caching the request based, thus serving the response from the cache if the request text is same.</p>

{{% ad-panel-leaderboard %}}

## Caching Request

<p>Angular provides a simplified way of making HTTP calls, HttpClient, along with HttpInterceptors to inspect and transform HTTP requests or responses to and from servers. It can be used for authentication or caching and many such things, multiple interceptors can be added and chained for further processing. In this case, we are intercepting requests and serving the response from the cache if the QR text is same.</p>

<p>Create an interceptor folder, then create a file <em>cache-interceptor.ts</em>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c55c8a9-f8ca-4d63-ac71-ad7e47870233/cache-interceptor.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c55c8a9-f8ca-4d63-ac71-ad7e47870233/cache-interceptor.PNG" sizes="100vw" caption="Cache interceptor (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c55c8a9-f8ca-4d63-ac71-ad7e47870233/cache-interceptor.PNG'>Large preview</a>)" alt="" >}}

<p>Add the below code snippet to the file:</p>

<div class="break-out">

<pre><code class="language-javascript">import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpResponse, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { tap } from 'rxjs/operators';
import { of, Observable } from 'rxjs';

@Injectable({
 providedIn: 'root'
})
export class RequestCachingService implements HttpInterceptor {
 private cacheMap = new Map&lt;string, HttpResponse&lt;any&gt;&gt;();

 constructor() { }

 intercept(req: HttpRequest<any>, next: HttpHandler): Observable&lt;HttpEvent&lt;any&gt;&gt; {
   const cachedResponse = this.cacheMap.get(req.urlWithParams);

   if (cachedResponse) {
     return of(cachedResponse);
   }

   return next.handle(req).pipe(tap(event => {
     if (event instanceof HttpResponse) {
       this.cacheMap.set(req.urlWithParams, event);
     }
   }))

 }
}</code></pre>
</div>

<p>In the above code snippet, we have a map with the key being the request URL, and the response as the value. We check if the current URL is present in the map; if it is, then return the response (the rest is handled automatically). If the URL is not in the map, we add it.</p>

<p>We are not done yet. An entry to the <em>app.module.ts</em> is required for its proper functioning. Add the below snippet:</p>

<div class="break-out">

<pre><code class="language-javascript">import { HttpClientModule, HTTP_INTERCEPTORS  } from '@angular/common/http';
import { CacheInterceptor } from './interceptor/cache-interceptor';


providers: [
   { provide: HTTP_INTERCEPTORS, useClass: CacheInterceptor, multi: true }
 ],</code></pre>
</div>

<p>This adds the caching feature to our application. Let’s move on to the third page, the History page.</p>

## Adding The History Page

<p>All the saved QR codes will be visible here. To create another component, open terminal type <code>ng g c history</code> and press Enter.</p>

<p>Open <em>history.component.css</em> and add the below code:</p>

<pre><code class="language-css">.main-content {
   padding: 5% 10%;
}
.truncate {
   width: 90%;
   white-space: nowrap;
   overflow: hidden;
   text-overflow: ellipsis;
}
.center-img {
   position: absolute;
   top: 50%;
   left: 50%;
   transform: translate(-50%, -50%);
   display: flex;
   flex-direction: column;
   align-items: center;
}</code></pre>

<p>Open <em>history.component.html</em> and replace the content with this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;app-header [showBackButton]="showBackButton" [currentTitle]="title" [showHistoryNav]="showHistoryNav">&lt;/app-header&gt;

&lt;div class="main-content"&gt;
   &lt;mat-grid-list cols="4" rowHeight="500px" &#42;ngIf="historyList.length &gt; 0"&gt;
       &lt;mat-grid-tile &#42;ngFor="let qr of historyList"&gt;
           &lt;mat-card&gt;
               &lt;img mat-card-image style="margin-top: 5px;" src="{{qr.imageBase64}}"&gt;
               &lt;mat-card-content&gt;
                   &lt;div class="truncate"&gt;
                       {{qr.text}}
                   &lt;/div&gt;
               &lt;/mat-card-content&gt;
               &lt;mat-card-actions&gt;
                       &lt;button mat-button (click)="share(qr.text)">SHARE&lt;/button&gt;
                       &lt;button mat-button color="accent" (click)="delete(qr.text)">DELETE&lt;/button&gt;
               &lt;/mat-card-actions&gt;
           &lt;/mat-card&gt;
       &lt;/mat-grid-tile&gt;
   &lt;/mat-grid-list&gt;
   &lt;div class="center-img" &#42;ngIf="historyList.length == 0"&gt;
       &lt;img src="../../assets/no-see.png" width="256" height="256"&gt;
       &lt;span style="margin-top: 20px;">Nothing to see here&lt;/span&gt;
   &lt;/div&gt;
&lt;/div&gt;</code></pre>
</div>

<p>As usual, we have the header component at the top. Then, the rest of the body is a grid list that will show all the saved QR codes as individual <code>mat-card</code>. For the grid view, we are using <code>mat-grid-list</code> from the Angular material library. As per the drill, before we can use it, we have to first add it to the <em>app.module.ts</em> file.</p>

<p>Mat grid list acts as a container with multiple tile children called <code>mat-grid-tile</code>. In the above HTML snippet, each tile is created using <code>mat-card</code> using some of its properties for generic placement of other UI elements. We can provide the <code>number of columns</code> and <code>rowHeight</code>, which is used to calculate width automatically. In the above snippet, we are providing both the number of columns and the <code>rowHeight</code> value.</p>

<p>We are using a placeholder image when the history is empty, <a href="https://raw.githubusercontent.com/dev4fun007/qr-gen/master/src/assets/no-see.png">download</a> it and add to the assets folder.</p>

<p>To implement the logic for populating all this information, open the <em>history.component.ts</em> file and add the below snippet into the <code>HistoryComponent</code> class:</p>

<div class="break-out">

<pre><code class="language-javascript">showBackButton = true;
 title = 'History';
 showHistoryNav = false;
 historyList;

 constructor(private storageService: StorageutilService,
 private snackbar: MatSnackBar ) { }

 ngOnInit() {
   this.populateHistory();
 }

 private populateHistory() {
   this.historyList = this.storageService.readAllHistory();
 }

 delete(text: string) {
   this.storageService.deleteHistory(text);
   this.populateHistory();
 }

 share(text: string) {
   this.snackbar.open(text, '', {duration: 2000,})
 }</code></pre>
</div>

<p>The above logic just fetches all the saved QR and populates the page with it. Users can delete the saved QR which will delete the entry from the local storage.</p>

<p>So this finishes off our history component... or does it? We still need to add the route mapping for this component. Open <em>app-routing.module.ts</em> and add a mapping for the history page as well:</p>

<pre><code class="language-javascript">{ path: 'history', component: HistoryComponent },</code></pre>

<p>The whole route array should look like this by now:</p>

<pre><code class="language-javascript">const routes: Routes = [
 { path: '', component: HomeComponent },
 { path: 'create', component: CreateQrComponent },
 { path: 'history', component: HistoryComponent },
];</code></pre>

<p>Now is a good time to run the application to check the complete flow, so open terminal and type <code>ng serve</code> and press Enter. Then, go to <code>localhost:4200</code> to verify the working of the application.</p>

## Add To GitHub

<p>Before proceeding to the deployment step, it would be good to add the project to a GitHub repository.</p>

<ol>
    <li>Open <a href="https://github.com/">GitHub</a>.</li>
    <li>Create a new repository.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd1c20f-9736-4afd-ac71-9b53f01838d7/github-new-repository.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd1c20f-9736-4afd-ac71-9b53f01838d7/github-new-repository.PNG" sizes="100vw" caption="GitHub new repository (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd1c20f-9736-4afd-ac71-9b53f01838d7/github-new-repository.PNG'>Large preview</a>)" alt="" >}}

<li>In VS Code, use the terminal and follow the first set of commands mentioned in the quick start guide to push all the project files.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c92d72-aa3b-4c35-a787-9d8e7507cedd/github-add-project.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c92d72-aa3b-4c35-a787-9d8e7507cedd/github-add-project.PNG" sizes="100vw" caption="Adding a project in GitHub (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c92d72-aa3b-4c35-a787-9d8e7507cedd/github-add-project.PNG'>Large preview</a>)" alt="" >}}
</ol>

<p>Just refresh the page to check if all the files are visible. From this point on, any git changes (such as commit, pull/push) will be reflected in this newly created repository.</p>

## Netlify And Deployment

<p>Our application runs in our local machine, but to enable others to access it, we should deploy it on a cloud platform and register it to a domain name. This is where Netlify comes into play. It provides continuous deployment services, integration with GitHub, and many more features to benefit from. Right now, we want to enable global access to our application. Let’s get started.</p>

<ol>
    <li>Sign-up on <a href="https://app.netlify.com/">Netlify</a>.</li>
    <li>From the dashboard, click on the <strong>New site from Git</strong> button.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b53e4e36-646b-4224-813a-a7a8450699dd/netlify-new-site.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b53e4e36-646b-4224-813a-a7a8450699dd/netlify-new-site.PNG" sizes="100vw" caption="Netlify new site (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b53e4e36-646b-4224-813a-a7a8450699dd/netlify-new-site.PNG'>Large preview</a>)" alt="" >}}

<li>Click on GitHub in the next screen.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce5c2e87-c0b0-476c-a0b8-58046114df90/netlify-select-git-provider.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce5c2e87-c0b0-476c-a0b8-58046114df90/netlify-select-git-provider.PNG" sizes="100vw" caption="Netlify select git provider (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce5c2e87-c0b0-476c-a0b8-58046114df90/netlify-select-git-provider.PNG'>Large preview</a>)" alt="" >}}

<li>Authorize Netlify to be able to access your GitHub repositories.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dde80de-fb51-44f1-9f6d-b90058029b81/netlify-github-authorization.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dde80de-fb51-44f1-9f6d-b90058029b81/netlify-github-authorization.jpg" sizes="100vw" caption="Netlify GitHub authorization (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dde80de-fb51-44f1-9f6d-b90058029b81/netlify-github-authorization.jpg'>Large preview</a>)" alt="" >}}

<li>Search for and select the newly created <code>qr</code> repository.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d971dd9d-69e8-468f-9f7e-d147900bac73/netlify-github-repository-selection.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d971dd9d-69e8-468f-9f7e-d147900bac73/netlify-github-repository-selection.PNG" sizes="100vw" caption="Netlify GitHub repository selection (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d971dd9d-69e8-468f-9f7e-d147900bac73/netlify-github-repository-selection.PNG'>Large preview</a>)" alt="" >}}

<li>Netlify, in the next step, allows us to choose the GitHub repository branch for deployments. Normally one uses the <code>master</code> branch but one can also have a separate <code>release</code> branch which contains only release related and stable features.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b55f6d3a-b3cb-4bbe-8cc2-4441c52ddee6/netlify-build-and-deploy.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b55f6d3a-b3cb-4bbe-8cc2-4441c52ddee6/netlify-build-and-deploy.PNG" sizes="100vw" caption="Netlify build and deploy (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b55f6d3a-b3cb-4bbe-8cc2-4441c52ddee6/netlify-build-and-deploy.PNG'>Large preview</a>)" alt="" >}}
</ol>

<p>Since this is an Angular web application, add <code>ng build --prod</code> as the build command. Published directories will be <code>dist/qr</code> as mentioned in the <code>angular.json</code> file.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd7f741c-48ae-4bfa-ae14-d77654cb694c/angular-build-path.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd7f741c-48ae-4bfa-ae14-d77654cb694c/angular-build-path.PNG" sizes="100vw" caption="Angular build path (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd7f741c-48ae-4bfa-ae14-d77654cb694c/angular-build-path.PNG'>Large preview</a>)" alt="" >}}

<p>Now click on the <code>Deploy site</code> button which will trigger a project build with the command <code>ng build --prod</code> and will output the file to <code>dist/qr</code>.</p>

<p>Since we provided the path information to Netlify, it will automatically pick up the correct files for servicing the web application. Netlify adds a random domain to our application by default.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab21ba54-ceb8-48e7-93f8-0c7304c9a153/netlify-site-deployed.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab21ba54-ceb8-48e7-93f8-0c7304c9a153/netlify-site-deployed.PNG" sizes="100vw" caption="Netlify site deployed (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab21ba54-ceb8-48e7-93f8-0c7304c9a153/netlify-site-deployed.PNG'>Large preview</a>)" alt="" >}}

<p>You can now click on the link provided in the above page in order to access the application from anywhere. Finally, the application has been deployed.</p>

### Custom Domain

<p>In the above image, the URL for our application is shown while the sub-domain is randomly generated. Let’s change that.</p>

<p>Click on the <code>Domain settings</code> button then in the Custom Domains section click on the 3-dot menu and select <code>Edit site name</code>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05b90f6-75c9-430a-902b-810d07abf35c/custom-domain.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05b90f6-75c9-430a-902b-810d07abf35c/custom-domain.PNG" sizes="100vw" caption="Custom domain (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05b90f6-75c9-430a-902b-810d07abf35c/custom-domain.PNG'>Large preview</a>)" alt="" >}}

<p>This will open a popup wherein a new site name can be entered; this name should be unique across the Netlify domain. Enter any site name that is available and click <strong>Save</strong>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4afa5eb1-c8b5-4e5f-8c12-1dfb5c4d0d60/site-name.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4afa5eb1-c8b5-4e5f-8c12-1dfb5c4d0d60/site-name.PNG" sizes="100vw" caption="Site name (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4afa5eb1-c8b5-4e5f-8c12-1dfb5c4d0d60/site-name.PNG'>Large preview</a>)" alt="" >}}

<p>Now the link to our application will be updated with the new site name.</p>

### Split Testing

<p>Another cool feature offered by Netlify is split testing. It enables traffic splitting so that different sets of users will interact with different application deployments. We can have new features added to a different branch and split the traffic to this branch deployment, analyze traffic and then merge the feature branch with the main deployment branch. Let’s configure it.</p>

<p>The prerequisite to enabling split testing is a GitHub repository with at least two branches. Head on over to the app repository in GitHub that was created earlier, and create a new branch <code>a</code>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f001d76a-60fb-415c-8388-da9f4161da2c/create-new-branch.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f001d76a-60fb-415c-8388-da9f4161da2c/create-new-branch.PNG" sizes="100vw" caption="Create new branch (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f001d76a-60fb-415c-8388-da9f4161da2c/create-new-branch.PNG'>Large preview</a>)" alt="" >}}

<p>The repository will now have a <code>master</code> branch and <code>a</code> branch. Netlify needs to be configured to do branch deployments, so open the Netlify dashboard and click on <code>Settings</code>. On the left side, click on <code>Build & Deploy</code>, then <code>Continuous Deployment</code>, then on the right side in the <code>Deploy contexts</code> section, click on <code>Edit settings</code>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9215a9-b5dc-4128-a694-ccf83594b5dc/branch-deployments.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9215a9-b5dc-4128-a694-ccf83594b5dc/branch-deployments.PNG" sizes="100vw" caption="Branch deployments (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9215a9-b5dc-4128-a694-ccf83594b5dc/branch-deployments.PNG'>Large preview</a>)" alt="" >}}

<p>In the <code>Branch deploys</code> sub-section, select the option “Let me add individual branches”, and enter the branch names and save it.</p>

<p>Deploying brances is another useful feature provided by Netlify; we can select which GitHub repository branches to deploy, and we can also enable previews for every pull request to the <code>master</code> branch before merging. This is a neat feature enabling developers to actually test their changes out live before adding their code changes to the main deployment branch.</p>

<p>Now, click on <code>Split Testing</code> tab option at the top of the page. The split testing configurations will be presented here.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e89bf79-e299-4e55-ac39-d5e39cf070c6/split-testing.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e89bf79-e299-4e55-ac39-d5e39cf070c6/split-testing.PNG" sizes="100vw" caption="Split testing (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e89bf79-e299-4e55-ac39-d5e39cf070c6/split-testing.PNG'>Large preview</a>)" alt="" >}}

<p>We can select the branch (other than the production branch) &mdash; in this case <code>a</code>. We can also play around with the settings of splitting traffic. Based on the traffic percentage each branch has been allotted, Netlify will re-route some users to the application deployed using the <code>a</code> branch and others to the <code>master</code> branch. After configuring, click on the <code>Start test</code> button to enable traffic splitting.</p>

<p><strong>TIP</strong>: <em>Netlify may not recognize that the connected GitHub repository has more than one branch and may give this error:</em></p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd6cc570-4ad9-46fa-93a1-46d396a79234/split-testing-error.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd6cc570-4ad9-46fa-93a1-46d396a79234/split-testing-error.PNG" sizes="100vw" caption="Split testing error (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd6cc570-4ad9-46fa-93a1-46d396a79234/split-testing-error.PNG'>Large preview</a>)" alt="" >}}

<p>To resolve this, just reconnect to the repository from the <code>Build & Deploy</code> options.</p>

<p>Netlify provides a lot of other features as well. We just went through some of its useful features to demonstrate the ease of configuring different aspects of Netlify.</p>

<p>This brings us to the end of our journey. We have successfully created an Angular Material design based on a web application and deployed it on Netlify.</p>

## Conclusion

<p>Angular is a great and popular framework for web application development. With the official Angular material design library, it is much easier to create applications which adhere to the material design specs for a very natural interaction with the users. Moreover, the application developed with a great framework should use a great platform for deployment, and Netlify is just that. With constant evolution, great support and with a plethora of features, it surely is a great platform to bring web applications or static sites to the masses. Hopefully, this article will provide help in getting started with a new Angular project from just a thought to deployment.</p>

### Further Reading

<ul>
    <li><a href="https://angular.io/guide/architecture">Angular Architecture</a></li>
    <li><a href="https://material.angular.io/components/categories">More Angular Material Components</a></li>
    <li><a href="https://www.netlify.com/products/">More About Netlify Features</a></li>
</ul>

{{< signature "dm, yk, il" >}}
