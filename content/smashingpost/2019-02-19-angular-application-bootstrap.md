---
title: 'Styling An Angular Application With Bootstrap'
slug: angular-application-bootstrap
author: ahmed-bouchefra
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32d49f6a-7b37-4ceb-99f2-080206c3fb0c/angular-bootstrap-contacts-feature.png
date: 2019-02-19T13:00:19+01:00
summary: >-
  In this tutorial, we’ll use the latest versions of Bootstrap 4 and Angular 7 to build an Angular application and style the interface with Bootstrap.
description: >-
  In this tutorial, we’ll use the latest versions of Bootstrap 4 and Angular 7 to build an Angular application and style the interface with Bootstrap. 
categories:
  - Apps
  - CSS
  - Angular
  - JavaScript
---
In case you’ve already tried building a web application with Angular 7, it’s time to kick it up a notch. Let’s see how we can integrate Bootstrap CSS styles and JavaScript files with an Angular project generated using the Angular CLI, and how to use [form controls and classes](https://getbootstrap.com/docs/4.0/components/forms/) to create beautiful forms and how to style HTML tables using [Table styles](https://getbootstrap.com/docs/4.0/content/tables/).

For the Angular part, we’ll be creating a simple client-side application for creating and listing contacts. Each contact has an ID, name, email, and description, and we’ll be using a simple data service that stores the contacts in a TypeScript array. You can use an advanced in-memory API instead. (Check out  “[A Complete Guide To Routing In Angular](https://www.smashingmagazine.com/2018/11/a-complete-guide-to-routing-in-angular/)”.)

**Note**: *You can get the source code of this tutorial from this [GitHub repository](https://github.com/techiediaries/angular-bootstrap-demo) and see the live example over [here](https://www.techiediaries.com/angular-bootstrap-demo).*

## Requirements

Before we start creating the demo application, let’s see the requirements needed for this tutorial.

Basically, you will need the following:

- Node.js and NPM installed (you can simply head on over to the [official website](https://nodejs.org/en/download/) and download the binaries for your system),
- Familiarity with TypeScript,
- Working experience of Angular,
- Basic knowledge of CSS and HTML.

{{% feature-panel %}}

## Installing Angular CLI

Let’s start by installing the latest version of Angular CLI. In your terminal, run the following command:

<pre><code class="language-bash">$ npm install -g @angular/cli
</code></pre>

At the time writing, **v7.0.3** of Angular CLI is installed. If you have the CLI already installed, you can make sure you have the latest version by using this command:

<pre><code class="language-bash">$ ng --version
</code></pre>

## Creating A Project

Once you have Angular CLI installed, let’s use it to generate an Angular 7 project by running the following command:

<pre><code class="language-bash">$ ng new angular-bootstrap-demo
</code></pre>

The CLI will then ask you:

<blockquote>Would you like to add Angular routing?</blockquote>

Press <kbd>Y</kbd>. Next, it will ask you:

<blockquote>Which stylesheet format would you like to use?</blockquote>

Choose “CSS”.

## Adding Bootstrap 

After creating the project, you need to install Bootstrap 4 and integrate it with your Angular project.

First, navigate inside your project’s root folder:

<pre><code class="language-bash">$ cd angular-bootstrap-demo
</code></pre>

Next, install Bootstrap 4 and jQuery from npm:

<pre><code class="language-bash">$ npm install --save bootstrap jquery
</code></pre>

(In this case, **bootstrap v4.2.1** and **jquery v3.3.1** are installed.)

Finally, open the `angular.json` file and add the file paths of Bootstrap CSS and JS files as well as jQuery to the `styles` and `scripts` arrays under the `build` target:

<div class="break-out">

 <pre><code class="language-json">"architect": {
  "build": {
    [...], 
    "styles": [
      "src/styles.css", 
        "node_modules/bootstrap/dist/css/bootstrap.min.css"
      ],
      "scripts": [
        "node_modules/jquery/dist/jquery.min.js",
        "node_modules/bootstrap/dist/js/bootstrap.min.js"
      ]
    },
</code></pre>
</div>

Check out [how to add Bootstrap to an Angular 6 project](https://stackoverflow.com/questions/50290197/how-to-add-bootstrap-in-angular-6-project) for options on how to integrate Bootstrap with Angular.

## Adding A Data Service

After creating a project and adding Bootstrap 4, we’ll create an Angular service that will be used to provide some demo data to display in our application.

In your terminal, run the following command to generate a service:

<pre><code class="language-bash">$ ng generate service data
</code></pre>

This will create two `src/app/data.service.spec.ts` and `src/app/data.service.ts` files.

Open `src/app/data.service.ts` and replace its contents with the following:

<div class="break-out">

 <pre><code class="language-typescript">import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {

  contacts = [
    {id: 1, name: "Contact 001", description: "Contact 001 des", email: "c001@email.com"},
    {id: 2, name: "Contact 002", description: "Contact 002 des", email: "c002@email.com"},
    {id: 3, name: "Contact 003", description: "Contact 003 des", email: "c003@email.com"},
    {id: 4, name: "Contact 004", description: "Contact 004 des", email: "c004@email.com"}
  ];

  constructor() { }

  public getContacts():Array<{id, name, description, email}>{
    return this.contacts;
  }
  public createContact(contact: {id, name, description, email}){
    this.contacts.push(contact);
  }
}
</code></pre>
</div>

We add a `contacts` array with some demo contacts, a `getContacts()` method which returns the contacts and a `createContact()` which append a new contact to the `contacts` array.

{{% ad-panel-leaderboard %}}

## Adding Components

After creating the data service, next we need to create some components for our application. In your terminal, run:

<pre><code class="language-bash">$ ng generate component home
$ ng generate component contact-create
$ ng generate component contact-list
</code></pre>

Next, we’ll add these components to the routing module to enable navigation in our application. Open the `src/app/app-routing.module.ts` file and replace its contents with the following:

<div class="break-out">

 <pre><code class="language-typescript">import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { ContactListComponent } from './contact-list/contact-list.component';
import { ContactCreateComponent } from './contact-create/contact-create.component';
import { HomeComponent } from './home/home.component';

const routes: Routes = [
  {path:  "", pathMatch:  "full",redirectTo:  "home"},
  {path: "home", component: HomeComponent},
  {path: "contact-create", component: ContactCreateComponent},
  {path: "contact-list", component: ContactListComponent}  
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
</code></pre>
</div>

We use the `redirectTo` property of the router’s path to redirect users to the home page when they visit our application. 

## Adding Header And Footer Components

Next, let’s create the header and footer components:

<pre><code class="language-bash">$ ng generate component header
$ ng generate component footer
</code></pre>

Open the `src/app/header/header.component.html` file and add the following code:

<div class="break-out">

 <pre><code class="language-html">&lt;nav class="navbar navbar-expand-md bg-dark navbar-dark fixed-top"&gt;
  &lt;a class="navbar-brand" href="#"&gt;Angular Bootstrap Demo&lt;/a&gt;
  &lt;button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarCollapse" aria-controls="navbarCollapse"
    aria-expanded="false" aria-label="Toggle navigation"&gt;
    &lt;span class="navbar-toggler-icon"&gt;&lt;/span&gt;
  &lt;/button&gt;
  &lt;div class="collapse navbar-collapse" id="navbarCollapse"&gt;
    &lt;ul class="navbar-nav mr-auto"&gt;

      &lt;li class="nav-item"&gt;
        &lt;a class="nav-link" routerLink="/home"&gt;Home&lt;/a&gt;
      &lt;/li&gt;
      &lt;li class="nav-item"&gt;
        &lt;a class="nav-link" routerLink="/contact-list"&gt;Contacts&lt;/a&gt;
      &lt;/li&gt;
      &lt;li class="nav-item"&gt;
        &lt;a class="nav-link" routerLink="/contact-create"&gt;Create&lt;/a&gt;
      &lt;/li&gt;

    &lt;/ul&gt;
  &lt;/div&gt;
&lt;/nav&gt;
</code></pre>
</div>

A navigation bar will be created with Bootstrap 4, and we’ll use the `routerLink` directive to link to different components.

Use the `.navbar`, `.navbar-expand{-sm|-md|-lg|-xl}` and `.navbar-dark` classes to create Bootstrap navigation bars. (For more information about nav bars, check out Bootstrap’s documentation on “[Navbar](https://getbootstrap.com/docs/4.0/components/navbar/)”.

Next, open the `src/app/header/header.component.css` file and add:

<pre><code class="language-css">
.nav-item{
    padding:2px;
    margin-left: 7px;
}
</code></pre>

Next, open the `src/app/footer/footer.component.html` file and add:

<div class="break-out">

 <pre><code class="language-html">&lt;footer&gt;
  &lt;p  class="text-xs-center"&gt;&copy; Copyright 2019. All rights reserved.&lt;/p&gt;
&lt;/footer&gt;
</code></pre>
</div>

Open the `src/app/footer/footer.component.css` file and add:

<pre><code class="language-css">
footer {
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    padding: 1rem;
    text-align: center;
}
</code></pre>

Next, open the `src/app/app.component.html` file and replace its contents with the following:

<pre><code class="language-html">&lt;app-header&gt;&lt;/app-header&gt;
&lt;router-outlet&gt;&lt;/router-outlet&gt;
&lt;app-footer&gt;&lt;/app-footer&gt;
</code></pre>

We’re creating an application shell by using the header and footer components which means that they will be present on every page of our application. The only part that will be changed is what will be inserted in the router outlet (check out “[The Application Shell](https://angular.io/tutorial/toh-pt0)” on the Angular website for more information).

{{% ad-panel-leaderboard %}}

## Adding A Bootstrap Jumbotron 

According to the [Bootstrap docs](https://getbootstrap.com/docs/4.0/components/jumbotron/):

<blockquote>“A Jumbotron is a lightweight, flexible component that can optionally extend the entire viewport to showcase key marketing messages on your site.”</blockquote>

Let’s add a Jumbotron component to our home page. Open the  `src/app/home/home.component.html` file and add:

<div class="break-out">

 <pre><code class="language-html">&lt;div class="jumbotron" style="background-color: #fff; height: calc(95vh);"&gt;
  &lt;h1&gt;Angular Bootstrap Demo&lt;/h1&gt;
  &lt;p class="lead"&gt;
    This demo shows how to integrate Bootstrap 4 with Angular 7  
  &lt;/p&gt;
  &lt;a class="btn btn-lg btn-primary" href="" role="button"&gt;View tutorial&lt;/a&gt;
&lt;/div&gt;
</code></pre>
</div>

The `.jumbotron` class is used to create a Bootstrap Jumbotron.

## Adding A List Component: Using A Bootstrap Table

Now let’s create a component-to-list data from the data service and use a Bootstrap 4 table to display tabular data.

First, open the `src/app/contact-list/contact-list.component.ts` file and inject the data service then call the `getContacts()` method to get data when the component is initialized:

<pre><code class="language-typescript">import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-contact-list',
  templateUrl: './contact-list.component.html',
  styleUrls: ['./contact-list.component.css']
})
export class ContactListComponent implements OnInit {

  contacts;
  selectedContact;

  constructor(public dataService: DataService) { }

  ngOnInit() {
    this.contacts = this.dataService.getContacts();    
  }
  public selectContact(contact){
    this.selectedContact = contact;
  }
}
</code></pre>

We added two variables `contacts`and `selectedContact` which hold the set of contacts and the selected contact. And a `selectContact()` method which assigns the selected contact to the `selectedContact` variable.

Open the `src/app/contact-list/contact-list.component.html`  file and add:

<div class="break-out">

 <pre><code class="language-html">&lt;div class="container" style="margin-top: 70px;"&gt;
  &lt;table class="table table-hover"&gt;
    &lt;thead&gt;
      &lt;tr&gt;
        &lt;th&gt;#&lt;/th&gt;
        &lt;th&gt;Name&lt;/th&gt;
        &lt;th&gt;Email&lt;/th&gt;
        &lt;th&gt;Actions&lt;/th&gt;
      &lt;/tr&gt;
    &lt;/thead&gt;
    &lt;tbody&gt;
      &lt;tr &#42;ngFor="let contact of contacts"&gt;

        &lt;td&gt;{{ contact.id }}&lt;/td&gt;
        &lt;td&gt; {{ contact.name }}&lt;/td&gt;
        &lt;td&gt; {{ contact.email }}&lt;/td&gt;
        &lt;td&gt;
          &lt;button class="btn btn-primary" (click)="selectContact(contact)"&gt; Show details&lt;/button&gt;
        &lt;/td&gt;
      &lt;/tr&gt;
    &lt;/tbody&gt;
  &lt;/table&gt;
  &lt;div class="card text-center" *ngIf="selectedContact"&gt;
      &lt;div class="card-header"&gt;
        # {{selectedContact.id}}
      &lt;/div&gt;
      &lt;div class="card-block"&gt;
        &lt;h4 class="card-title"&gt;{{selectedContact.name}}&lt;/h4&gt;
        &lt;p class="card-text"&gt;
          {{selectedContact.description}}
        &lt;/p&gt;    
      &lt;/div&gt;

    &lt;/div&gt;
&lt;/div&gt;
</code></pre>
</div>

We simply loop through the `contacts` array and display each contact details and a button to select a contact. If the contact is selected, a Bootstrap 4 Card with more information will be displayed.

This is the definition of a Card from [Bootstrap 4 docs](https://getbootstrap.com/docs/4.0/components/card/):

<blockquote>“A <strong>card</strong> is a flexible and extensible content container. It includes options for headers and footers, a wide variety of content, contextual background colors, and powerful display options. If you’re familiar with Bootstrap 3, cards replace our old panels, wells, and thumbnails. Similar functionality to those components is available as modifier classes for cards.”</blockquote>

We use the `.table` and `.table-hover` classes to create Bootstrap-styled tables, the `.card`, `.card-block`, `.card-title` and `.card-text` classes to create cards. (For more information, check out [Tables](https://getbootstrap.com/docs/4.0/content/tables/) and [Cards](https://getbootstrap.com/docs/4.0/components/card/).)

## Adding A Create Component: Using Bootstrap Form Controls And Classes

Let’s now add a form to our `contact-create` component. First, we need to import the `FormsModule` in our main application module. Open the `src/app/app.module.ts` file, import `FormsModule` from `@angular/forms`, and add it to the `imports` array:

<pre><code class="language-typescript">import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppRoutingModule } from './app-routing.module';
import { FormsModule } from '@angular/forms';

/* ... */

@NgModule({
  declarations: [
  /* ... */
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
</code></pre>

Next, open the `src/app/contact-create/contact-create.component.ts` file and replace its contents with the following:

<div class="break-out">

 <pre><code class="language-typescript">import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-contact-create',
  templateUrl: './contact-create.component.html',
  styleUrls: ['./contact-create.component.css']
})
export class ContactCreateComponent implements OnInit {

  contact : {id, name, description, email} = {id: null, name: "", description: "", email: ""};

  constructor(public dataService: DataService) { }

  ngOnInit() {
  }

  createContact(){
    console.log(this.contact);
    this.dataService.createContact(this.contact);
    this.contact = {id: null, name: "", description: "", email: ""};

  }
}
</code></pre>
</div>

Next, open the `src/app/contact-create/contact-create.component.html` file and add the following code:

<div class="break-out">

 <pre><code class="language-html">&lt;div class="container" style="margin-top: 70px;"&gt;

  &lt;div class="row"&gt;

    &lt;div class="col-sm-8 offset-sm-2"&gt;

      &lt;div&gt;
        &lt;form&gt;
          &lt;div class="form-group"&gt;
            &lt;label for="id"&gt;ID&lt;/label&gt;
            &lt;input [(ngModel)]="contact.id" type="text" name="id" class="form-control" id="id" aria-describedby="idHelp" placeholder="Enter ID"&gt;
            &lt;small id="idHelp" class="form-text text-muted"&gt;Enter your contact’s ID&lt;/small&gt;

            &lt;label for="name"&gt;Contact Name&lt;/label&gt;
            &lt;input [(ngModel)]="contact.name" type="text" name="name" class="form-control" id="name" aria-describedby="nameHelp" placeholder="Enter your name"&gt;
            &lt;small id="nameHelp" class="form-text text-muted"&gt;Enter your contact’s name&lt;/small&gt;

            &lt;label for="email"&gt;Contact Email&lt;/label&gt;
            &lt;input [(ngModel)]="contact.email" type="text" name="email" class="form-control" id="email" aria-describedby="emailHelp"
              placeholder="Enter your email"&gt;
            &lt;small id="nameHelp" class="form-text text-muted"&gt;Enter your contact’s email&lt;/small&gt;

            &lt;label for="description"&gt;Contact Description&lt;/label&gt;
            &lt;textarea [(ngModel)]="contact.description" name="description" class="form-control" id="description" aria-describedby="descHelp"&gt;
                      &lt;/textarea&gt;
            &lt;small id="descHelp" class="form-text text-muted"&gt;Enter your contact’s description&lt;/small&gt;

          &lt;/div&gt;
        &lt;/form&gt;
        &lt;button class="btn btn-primary" (click)="createContact()"&gt;Create contact&lt;/button&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>
</div>

We use the `.form-group`, `.form-control` classes to create a Bootstrap-styled form (check out “[Forms](https://getbootstrap.com/docs/4.0/components/forms/)” for more information).

We use the `ngModel` directive to bind the form fields to the components' variable. For data binding to properly work, you need to give each form field a name. 

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2019/02/image-breakpoints-angular/">Managing Image Breakpoints With Angular</a> by Tamas Piros</em></p>

## Running The Angular Application

At this step, let’s run the application and see if everything works as expected. Head over to your terminal, make sure you are in the root folder of your project then run the following command:

<pre><code class="language-bash">$ ng serve
</code></pre>

A live-reload development server will be running from the `https://localhost:4200` address. Open your web browser and navigate to that address. You should see the following interface:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24438800-f4f0-4a52-a778-31c02d4eac0b/angular-bootstrap-home.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24438800-f4f0-4a52-a778-31c02d4eac0b/angular-bootstrap-home.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24438800-f4f0-4a52-a778-31c02d4eac0b/angular-bootstrap-home.png'>Large preview</a>)" alt="Angular Bootstrap demo: Home page" >}}

If you navigate to the Contacts page, you should see:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d887a6e1-6ef7-4059-a454-797b16b9c3a9/angular-bootstrap-contacts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d887a6e1-6ef7-4059-a454-797b16b9c3a9/angular-bootstrap-contacts.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d887a6e1-6ef7-4059-a454-797b16b9c3a9/angular-bootstrap-contacts.png'>Large preview</a>)" alt="Angular Bootstrap Demo: Contacts Page" >}}

If you navigate to the “Create contact” page, you should see:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9324f7d8-6b58-4884-8383-b222222d69e2/angular-bootstrap-create.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9324f7d8-6b58-4884-8383-b222222d69e2/angular-bootstrap-create.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9324f7d8-6b58-4884-8383-b222222d69e2/angular-bootstrap-create.png'>Large preview</a>)" alt="Angular Bootstrap Demo: Create contact page" >}}

## Conclusion

In this tutorial, we’ve seen how to create a simple Angular application with a Bootstrap interface. You can find the complete source code on [GitHub](https://github.com/techiediaries/angular-bootstrap-demo) and see the [live example here](https://www.techiediaries.com/angular-bootstrap-demo).

{{< signature "dm, il" >}}
