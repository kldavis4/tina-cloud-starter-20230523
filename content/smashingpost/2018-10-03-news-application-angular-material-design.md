---
title: 'How To Build A News Application With Angular 6 And Material Design'
slug: news-application-with-angular-and-material-design
author: rachid-sakara
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b3f780-c3c5-4a7f-b125-052f6873be99/introduction-800w.png
date: 2018-10-03T12:00:26+02:00
summary: >-
  In this article, we’re going to build a news application using Angular 6 and Google’s material design in combination, which will help you to make your future applications with Angular look great in web browsers and mobile devices.
description: >-
  In this article, we’re going to build a news application using Angular 6 and Google’s material design in combination, which will help you to make your future applications with Angular look great in web browsers and mobile devices.
categories:
  - Apps
  - API
  - Angular
---
<p>Are you looking to combine Google’s <a href="https://material.angular.io">material design</a> with <a href="https://angular.io/">Angular</a> applications? Well, look no further!</p>

<p>In this tutorial, we’re going to build a news application using two of the most powerful and popular resources out there, Angular 6 and material design. You’ll learn how to incorporate Google’s material design components into Angular application templates to change and style your application in a professional way. The tutorial also serves as a reminder of how to make HTTP requests to bring live news articles to an application using the <a href="https://newsapi.org/">News API</a>.</p>

<p>Before we get started building the app, let’s quickly review the resources we’re going to use, Angular and material design, and see why we’ve paired them to build this application?</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7486f5f-7cb1-4a4e-b125-9f7fdeb11146/introduction.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7486f5f-7cb1-4a4e-b125-9f7fdeb11146/introduction.png" sizes="100vw" caption="A news application with Angular 6 and Material Design. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7486f5f-7cb1-4a4e-b125-9f7fdeb11146/introduction.png'>Large preview</a>)" alt="A news application with Angular 6 and Material Design" >}}

## What Is Angular?

<p>Angular &mdash; according to the <a href="https://angular.io/docs#what-is-angular">official documentation</a> &mdash; is described as follows:</p>

<blockquote>“Angular is a platform that makes it easy to build applications with the web. Angular combines declarative templates, dependency injection, end-to-end tooling, and integrated best practices to solve development challenges. Angular empowers developers to build applications that live on the web, mobile, or the desktop.”</blockquote>

<p>In short, it’s the most powerful JavaScript framework for building highly interactive and dynamic web applications.</p>

<blockquote>“As mentioned, Angular is powerful, but also popular, which is why companies such as Upwork, Freelancer, Udemy, YouTube, Paypal, Nike, Google, Telegram, Weather, iStockphoto, AWS, Crunchbase are using it.”</blockquote>

{{% feature-panel %}}

## What Is Google’s Material Design?

<p>Material design is a design language introduced by Google in the summer of 2014 for Android’s new OS. Although its initial focus was touch-based mobile apps, now its functionality has been extended to reach the web design world.</p>

<p>It’s an adaptable system of guidelines, components, and tools that support the best practices of user interface design. It’s also backed by open-source code and supported by a large community of designers and developers who are collaborating together to build beautiful products.</p>

## Why Angular And Google’s Material Design Specifically?

<p>It’s a matter of choice. No JavaScript framework is better than another. It’s all about what your project needs. The same goes for programming languages.</p>

<p>Now, I’m not going to outline the benefits and features of Angular. Instead, I’m going to share with you why I’ve picked Angular specifically to build a news application.</p>

<p>As is always the case with any news application, communicating with back-end services over the HTTP protocol is a crucial part. This is where the newer Angular <strong>HttpClient module</strong>, which is an improved version of the old Http, can help us easily interact with the service API.</p>

<p><strong>The model-view-viewmodel</strong> (MVVM) of Angular will be handy when it comes to binding the remote data that will be stored in objects into our application template, where the component plays the part of the controller/viewmodel and where the template represents the view. This is what we call the Angular template language.</p>

<p><strong>The two-way binding system</strong>, which means that any changes in the application’s state will be automatically reflected into the view, and vice versa. You’ll notice that when selecting the news resources from the side menu, that will change the state of our news article. </p>

<p>What I like most about Angular is the <strong>SPA technology</strong>. Loading only the part of the page that needs to be changed will definitely help our application load and perform more quickly and smoothly.</p>

<p>Of course, there are many other benefits and features of Angular, which you can look up with a quick online search.</p>

## What About The Visual Aspect?

<p>We’ve chosen material design because its language is a suitable fit for Angular, and it’s easy to implement.</p>

<p>It’s also a very popular visual language; it’s responsive, and most Google apps are built with it. We want our app to look as much like a Google app as possible.</p>

<p>As an introduction, that’s all we need. It’s time to look at the project overview and then jump into the build process.</p>

<ul>
<li><a href="#project-overview">Project Overview</a></li>
<li><a href="#prerequisites">Prerequisites</a></li>
<li><a href="#setting-up-an-angular-project">Setting Up An Angular Project</a></li>
<li><a href="#installing-dependencies">Installing Dependencies</a></li>
<li><a href="#acquiring-free-api-key">Acquiring Free API Key</a></li>
<li><a href="#working-on-components">Working On Components</a></li>
<li><a href="#defining-material-default-style">Defining Material Default Style</a></li>
<li><a href="#define-a-template">Define A Template</a></li>
<li><a href="#conclusion">Conclusion</a></li>
</ul>

## Project Overview

<blockquote>“Getting the latest live news articles from a range of <a href="https://newsapi.org/sources">sources</a>, including BBC News, CNN, TechCrunch, Huffington Post and more, along with different categories, like technology, sports, business, science and entertainment.”</blockquote>

<p>This is how your application will look when you finish it:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb95aed3-3e20-4908-af4d-2897375b4b46/project-overview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb95aed3-3e20-4908-af4d-2897375b4b46/project-overview.png" sizes="100vw" caption="Project overview. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb95aed3-3e20-4908-af4d-2897375b4b46/project-overview.png'>Large preview</a>)" alt="A news application overview" >}}

<p>That should get you excited, shouldn’t it? Let’s start by building the app.</p>

## Prerequisites

<p>This is what you’re going to need in order to follow along with this tutorial:</p>

<ul>
<li><a href="https://nodejs.org/en/">Node.js</a> and npm installed on your machine;</li>
<li><a href="https://cli.angular.io/">Angular CLI</a> installed on your machine;</li>
<li>A basic understanding of <strong>Angular</strong>.</li>
</ul>

<p>Once that stuff is out of the way, we can proceed.</p>

## Setting Up The Angular Project

<p>In this section, we’re going to use the Angular command line interface (CLI) to generate a new Angular project. To do so, head over to the CLI and run this:</p>

<pre><code class="language-html">ng new news-app</code></pre>

<p>Next, point your command line to the project’s root folder by running the following:</p>

<pre><code class="language-html">cd news-app</code></pre>

{{% ad-panel-leaderboard %}}

## Installing Dependencies

<p>To set up our dependencies, we’re going to install, with just one command, all of the dependencies necessary for this tutorial. Don’t worry, I’ll explain this in a second:</p>

<div class="break-out">

<pre><code class="language-html">npm install --save @angular/material @angular/animations @angular/cdk</code></pre></div>

<p>We have three packages being installed with this command.</p>

### @angular/material

<p>This is the official material design package for the Angular framework.</p>

### @angular/animations

<p>Installing the Angular animation package separately from the Angular core library is necessary. Certain material components need access to the animation libraries, which is why we’re installing it here.</p>

### @angular/cdk

<p>The <strong>CDK</strong> part stands for “component dev kit”, which provides us with high-quality predefined behaviors for your components, since modern web development is all about components.</p>

<p>It is recommended to include the Angular CDK any time you want to link Google’s material design to an Angular application.</p>

<p>To find out more about Angular CDK, check out this  <a href="https://blog.angular.io/a-component-dev-kit-for-angular-9f06e3b4b3b4">article</a>.</p>

<p>Let’s run our app to see that everything works just fine. You can start a development server by running the following command:</p>

<div class="break-out">

<pre><code class="language-html">ng serve</code></pre></div>

<p>Now, if you visit <a href="https://localhost:4200/">https://localhost:4200/</a> in a browser, you should see the following page:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c232e07e-2f23-4a03-883d-9ecfeca1c638/welcome-to-news-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c232e07e-2f23-4a03-883d-9ecfeca1c638/welcome-to-news-app.png" sizes="100vw" caption="Running the Angular project on development server. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c232e07e-2f23-4a03-883d-9ecfeca1c638/welcome-to-news-app.png'>Large preview</a>)" alt="Welcome to news app" >}}

<p>Now, in your code editor, navigate to the file <code>/src/app/app.module.ts</code>, and add the following packages that we’ve just installed:</p>

<div class="break-out">

<pre><code class="language-javascript">… Other imports …
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatButtonModule, MatCardModule, MatMenuModule, MatToolbarModule, MatIconModule, MatSidenavModule, MatListModule } from '@angular/material';
</code></pre></div>

<p>It is important to understand what’s going on here. First, we’re importing the animations package to animate our application a bit.</p>

<blockquote>The next import is what’s unique to Angular material. Before, we just included a single material module. Now, we have to import each material component that we intend to use.</blockquote>

<p>As you can see, we’ve added seven different modules here for material buttons, cards, menus, lists toolbars, side navigation, and icons.</p>

<p>After adding those packages to your <code>app.module.ts</code> file, make sure that your file matches the following:</p>

<div class="break-out">

<pre><code class="language-css">import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';
import { NewsApiService } from './news-api.service';

import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatButtonModule, MatCardModule, MatMenuModule, MatToolbarModule, MatIconModule, MatSidenavModule, MatListModule } from '@angular/material';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    HttpClientModule,
    MatButtonModule,
    MatMenuModule,
    MatCardModule,
    MatToolbarModule,
    MatIconModule,
    MatSidenavModule,
    MatListModule,
  ],
  providers: [NewsApiService],
  bootstrap: [AppComponent]
})
export class AppModule { }
</code></pre></div>

<p><strong>Note</strong>: <em>The statement</em> <strong>import { HttpClientModule } from @angular/common/http</strong><em> in the file above wasn’t generated automatically, but rather added manually. So, make sure you do that, too. And don’t worry about the <strong>NewsApiService</strong> service provider because we’re going to take care of that later on.</em></p>

<p>You might be wondering, though, how did I know the names of the modules to import? The official <a href="https://material.angular.io/components">Angular material documentation</a> gives you the exact code needed to import each module.</p>

<p>If you click on any of the components in the left menu and then click on the “API” tab, it provides you with the exact import line that you need to use.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b6bcd4d-406c-4859-a6db-aa510f258c2e/api-reference.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b6bcd4d-406c-4859-a6db-aa510f258c2e/api-reference.png" sizes="100vw" caption="API reference for Angular Material Component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b6bcd4d-406c-4859-a6db-aa510f258c2e/api-reference.png'>Large preview</a>)" alt="API reference for Angular Material Components" >}}

<p>In terms of setup, that’s all we need to do before we actually begin using and integrating material components in our templates.</p>

<p>You just have to remember to import each unique component that you plan to use. </p>

## Acquiring Free API Key

<p>We’re going to use the <a href="https://newsapi.org/">News API</a> to feed us some news headlines as JSON data, which we’ll implement in the application template.</p>

<p>What is the News API service?</p>

<p>The News API is a simple HTTP REST API for searching and retrieving live articles from all over the web.</p>

<p>Now that you know what the News API is, the next step is to get a free <a href="https://newsapi.org/register">API Key</a>, which will help us make some call requests to the server and grab the news articles.</p>

<p>You can sign up for just 30 seconds. You’ll only need to provide your first name, email address, and password. That’s all.</p>

<p>After signing up, you’ll find the API key already generated for you in the dashboard. Just save it in a text file somewhere on your desktop; because we’ll use it in the next chapter.</p>

## Working On The Components

<p>To start working on the components, you need to create a service provider to manage the interaction with the News API service.</p>

### Creating The Service Provider

<p>Enter this command to generate a new service provider:</p>

<pre><code class="language-html">ng generate service NewsApi
</code></pre>

<p>After that, go to the generated <code>/src/app/news-api.service.ts</code> file, and add the following code to it:</p>

<div class="break-out">

<pre><code class="language-css">import { Injectable } from '@angular/core';
import { HttpClient  } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class NewsApiService {

  api_key = 'PUT_YOUR_API_KEY_HERE';

  constructor(private http:HttpClient) { }
  initSources(){
     return this.http.get('https://newsapi.org/v2/sources?language=en&apiKey='+this.api_key);
  }
  initArticles(){
   return this.http.get('https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey='+this.api_key);
  }
  getArticlesByID(source: String){
   return this.http.get('https://newsapi.org/v2/top-headlines?sources='+source+'&apiKey='+this.api_key);
  }
} 
</code></pre></div>

<p>It’s time to use our <strong>API Key</strong>. Just paste it where it says, “Put_YOUR_API_KEY_HERE”.</p>

<p>We’ve imported <code>HttpClient</code>, which will be responsible for making API calls to our endpoints and fetching news headlines for us.</p>

<p>Now, for the <code>initSources</code> function, we simply prepare our left-side menu with some news resources. After that, we’ve created another function, <code>initArticles</code> which retrieves the first articles from <strong>TechCrunch</strong> once the application gets started.</p>

<p>As for the last function, <code>getArticlesByID</code>, it’s going to simply bring some articles for the passing parameter.</p>

### The Main Component

<p>The service provider is done. Let’s move to the <code>/src/app/app.component.ts</code> file and add this code:</p>

<div class="break-out">

<pre><code class="language-css">import { Component } from '@angular/core';
import { NewsApiService } from './news-api.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {

  mArticles:Array&lt;any&gt;;
  mSources:Array&lt;any&gt;;

  constructor(private newsapi:NewsApiService){
    console.log('app component constructor called');         
  }

  ngOnInit() {
        //load articles
      this.newsapi.initArticles().subscribe(data =&gt; this.mArticles = data['articles']);
    //load news sources
    this.newsapi.initSources().subscribe(data=&gt; this.mSources = data['sources']);  
    }

  searchArticles(source){
    console.log("selected source is: "+source);
    this.newsapi.getArticlesByID(source).subscribe(data =&gt; this.mArticles = data['articles']);
  }

}
</code></pre></div>

<p>We’re defining two properties here: <strong>mArticles</strong>, for holding news articles, and <strong>mSources</strong>, for holding news resources. Both are defined as an array.</p>

<p>In the constructor, we’re simply creating a <strong>NewsAPIService</strong> instance.</p>

<p>Next, we’re using that instance on the <strong>ngOnInit()</strong> function to initialize our two properties.</p>

<p>For the <strong>searchArticles</strong> function, it will be triggered whenever the user selects a specific resource from the left-side menu. Then we’re passing this parameter to the <strong>getArticlesByID</strong> service provider function to retrieves articles for it.</p>

{{% ad-panel-leaderboard %}}

## Defining Material’s Default Style

<p>In our <code>/src/styles.css</code> file, which is generated by the Angular CLI, let’s add the following:</p>

<div class="break-out">

<pre><code class="language-css">@import '~@angular/material/prebuilt-themes/indigo-pink.css';
body {
    padding: 2em 23em;
    background:lightgray;
}
</code></pre></div>

<p>Based on your preference, you can change <code>indigo-pink.css</code> to:</p>

<ul>
<li>deeppurple-amber.css</li>
<li>indigo-pink.css</li>
<li>pink-bluegrey.css</li>
<li>purple-green.css</li>
</ul>

<p>I'm also adding some CSS to the <code>body</code> tag, only to demonstrate this layout. This helps it look more like an app, even on desktop.</p>

<p>Let’s also add two lines to our <code>/src/index.html</code> file just before the closing <code>head</code> tag:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet"&gt;
&lt;link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700,400italic"&gt;
</code></pre></div>

<p>The first line imports the material design icon font, and the second one is the Roboto font, which is used by the material design team.</p>

## Defining A Template

<p>Let’s start off by adding the following template in the <code>/src/app/app.component.html</code> file:</p>

<div class="break-out">

<pre><code class="language-html">&lt;mat-toolbar color="primary"&gt;
  &lt;button mat-button (click)="sidenav.open ()" &gt;&lt;mat-icon&gt;menu&lt;/mat-icon&gt;&lt;/button&gt;
  &lt;span&gt;News Headlines&lt;/span&gt;  
  &lt;span class="example-spacer"&gt;&lt;/span&gt;
  &lt;button mat-button [matMenuTriggerFor]="appMenu"&gt;&lt;mat-icon&gt;settings&lt;/mat-icon&gt;&lt;/button&gt;
&lt;/mat-toolbar&gt;
&lt;mat-menu #appMenu="matMenu"&gt;
  &lt;button mat-menu-item&gt; Settings &lt;/button&gt;
  &lt;button mat-menu-item&gt; Help &lt;/button&gt;
&lt;/mat-menu&gt;
&lt;mat-sidenav-container class="example-container"&gt;

  &lt;mat-sidenav #sidenav class="example-sidenav"&gt;
    &lt;mat-list class="list-nav"&gt;
        &lt;mat-list-item class="list-item" *ngFor="let source of mSources" (click)="searchArticles(source.id);sidenav.close();"&gt;

          &lt;div mat-card-avatar [ngStyle]="{'background-image': 'url(../assets/images/'+ source.id +'.png)'}" class="example-header-image"&gt;&lt;/div&gt;

          &lt;span class="source-name"&gt; {{source.name}}&lt;/span&gt;

        &lt;/mat-list-item&gt;
    &lt;/mat-list&gt;
  &lt;/mat-sidenav&gt;
  &lt;mat-card class="example-card"  *ngFor="let article of mArticles"&gt;
    &lt;mat-card-header&gt;
      &lt;div mat-card-avatar [ngStyle]="{'background-image': 'url(../assets/images/'+ article.source.id +'.png)'}" class="example-header-image"&gt;&lt;/div&gt;
      &lt;mat-card-title class="title"&gt;{{article.title}}&lt;/mat-card-title&gt;
      &lt;mat-card-subtitle&gt;{{article.source.name}}&lt;/mat-card-subtitle&gt;
    &lt;/mat-card-header&gt;
    &lt;img mat-card-image class="img-article" src={{article.urlToImage}} alt=""&gt;
    &lt;mat-card-content&gt;
      &lt;p&gt;
        {{article.description}}
      &lt;/p&gt;
    &lt;/mat-card-content&gt;
    &lt;mat-card-actions class="action-buttons"&gt;
      &lt;button mat-button color="primary"&gt;&lt;mat-icon&gt;thumb_up_alt&lt;/mat-icon&gt; 12 Likes&lt;/button&gt;
      &lt;button mat-button color="primary"&gt;&lt;mat-icon&gt;comment&lt;/mat-icon&gt; Comments&lt;/button&gt;
      &lt;button mat-button color="primary"&gt;&lt;mat-icon&gt;share&lt;/mat-icon&gt; Share&lt;/button&gt;
      &lt;a mat-button color="primary" href={{article.url}} target="_blank" &gt;&lt;mat-icon&gt;visibility&lt;/mat-icon&gt; More&lt;/a&gt;
    &lt;/mat-card-actions&gt;
  &lt;/mat-card&gt;
&lt;/mat-sidenav-container&gt;
</code></pre></div>

<p>So, what have we done here?</p>

<p>First, we define a toolbar with a left-side menu, along with the application’s main title and the settings’ right menu.</p>

<p>Next, we’re using <code>*ngFor</code> for both sources and articles, and in doing so, our left-side menu will hold the news resources, and the main contents will hold the news articles.</p>

<p>One thing to notice is that on the <code>click</code> event of our list items, we’ve added two functions because that event executes any JavaScript code. The first function is <code>searchArticles</code>, which we’ve already explain, and the second one is <code>sidenav.close()</code> which will automatically close our left-side menu once the user has selected a resource.</p>

### Styling Our Component

<p>The last thing to do with the components is to visit the <code>/src/app.component.css</code> file and paste the following code in it:</p>

<pre><code class="language-css">.example-spacer {
  flex: 1 1 auto;
}

.example-card{
    margin-top: 4px;
}

.example-header-image { 
  background-size: cover;
}

.title{
    font-weight: bold;
}

.img-article{
    height: 350px;
}

.action-buttons{
    text-align: center;
}

.example-container {
    width: 100%;
    height: auto;
    border: 1px solid rgba(111, 111, 111, 0.50);
}

.example-sidenav-content {
    display: flex;
    height: 75%;
    align-items: center;
    justify-content: center;
}

.example-sidenav {
    padding: 20px;
}

.source-name {
    margin-left:5px; 
}

.list-item:hover{
    cursor: pointer;
    background-color: #3f51b5;
    color: white;
}
</code></pre>

### Set Up Images For News Resources

<p>Move to the <code>/src/assets</code> directory, and create a new folder named <code>images</code>. Then, download these images either from a <a href="https://drive.google.com/open?id=1tst2G_pVlpo41A3XmmrnGOP1PzaNJJOi">Google Drive link</a> or the <a href="https://github.com/rachidsakara/angular-news-application-with-material/tree/master/src/assets/images">GitHub repository</a>.</p>

<p>They are the logos of our news resources. Once you download them, copy and paste all of the image files into the <code>images</code> folder that you just created.</p>

<p>Once everything is complete, run this:</p>

<div class="break-out">

<pre><code class="language-html">ng serve</code></pre></div>

<p>Now, your app should look like the screenshot below. Pretty awesome, huh!</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a7751f7-236b-4723-b00f-316c11cfca05/angular-material-design-final-product.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a7751f7-236b-4723-b00f-316c11cfca05/angular-material-design-final-product.png" sizes="100vw" caption="Launching the app after everything is complete. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a7751f7-236b-4723-b00f-316c11cfca05/angular-material-design-final-product.png'>Large preview</a>)" alt="the news application final product" >}}

<p>Note that when the news snippets are loaded on the main page, a “More” button (as you can see in the picture above) takes the user to read the whole story.</p>

## Conclusion

<p>There you have it! I hope this tutorial was useful and that you’ve enjoyed building this application. If so, feel free to leave your feedback and comments below. In the meantime, the <a href="https://material.angular.io/">Angular Material</a> documentation is pretty cool. It provides you with an overview of each component, an API and an example.</p>

<p>The entire source code of this app is available on <a href="https://github.com/rachidsakara/angular-news-application-with-material">GitHub</a>. You can also check out this <a href="https://world-headlines.herokuapp.com">website</a>, which already implements the service API used in this tutorial.</p>

{{< signature "ra, al, yk, il" >}}
