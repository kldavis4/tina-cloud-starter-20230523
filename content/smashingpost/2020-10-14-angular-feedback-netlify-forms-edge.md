---
title: 'Build And Deploy An Angular Form With Netlify Forms And Edge'
slug: angular-feedback-netlify-forms-edge
author: zara-cooper
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcf65cc1-7671-4953-8650-d81b67a1ae29/angular-feedback-netlify-forms-edge.png
date: 2020-10-14T12:30:00.000Z
summary: >-
  Netlify Forms is a form handling feature that receives submissions from HTML forms automatically. In this article, we’ll cover how to use it with Angular reactive forms and how to deploy the finished app on Netlify’s hosting platform, Netlify Edge. 
description: >-
  Netlify Forms is a form handling feature that receives submissions from HTML forms automatically. In this article, we’ll cover how to use it with Angular reactive forms and how to deploy the finished app on Netlify’s hosting platform, Netlify Edge. 
categories:
  - Forms
  - Tools
  - Angular
---

Creating the frontend, backend, and deployment workflow of an app takes a lot of work. In instances where your app collects only a limited amount of data submissions from its users, building a whole backend may not seem worth the time and effort. An alternative to developing a complete backend is using Netlify Forms. In this tutorial, I’ll explain how you could use an Angular reactive form with Netlify Forms. Since Netlify Forms only work when deployed on Netlify, I’ll also illustrate how to deploy your app on Netlify Edge.

## The Toolkit

An Angular reactive form is a form that has a structured data model created explicitly within a component class using the [ReactiveFormsModule](https://angular.io/api/forms/ReactiveFormsModule) providers. A form model is created for each input element within the form view. This form model is an instance of the [FormControl](https://angular.io/api/forms/FormControl) class and it keeps track of the value of the form element. The form model is immutable because whenever a change is made to the model the FormControl instance returns a new data model instead of updating the old model. Its immutability makes change detection more efficient and allows data alteration with observable operators. Since form input elements are directly connected to their form models, updates between them are synchronous and do not rely on UI rendering. 

Netlify is a platform that allows you to build, deploy, and host sites built with various technologies. Sites built with Angular can be hosted on Netlify. Netlify additionally provides a host of tools that simplify, automate, and augment builds and deployments of these sites. We’re going to use two of its products in this tutorial: Netlify Edge and Netlify Forms. 

As described earlier, Netlify Forms is a form handling feature that receives submissions from HTML forms automatically. It does not require any submission processing configuration, like creating APIs, scripts, etc. This feature only works with forms in sites deployed on Netlify. It is enabled by default, further reducing the configuration needed to set up the form submissions. Submission handling is set up during deployment where a site’s HTML files are parsed by Netlify’s build bots.

Netlify Edge is a global application delivery network on which sites and applications are published. It provides features like A/B testing, rollbacks, staging, and phased rollouts. All deployments on Netlify Edge are atomic, meaning a site is only live when all files have been uploaded/updated and changes to the site are ready. Once a site is deployed, it is assigned a subdomain on **netlify.app** when deployed to production. Netlify Edge also supports preview and branch deployments (staging, development, etc.).

Netlify Forms submission-handling works because build bots parse HTML forms on a site during deployment. Client-side Javascript rendered forms like those in compiled Angular sites won’t be found by these bots. So the normal set up for Netlify Forms won’t work with Angular Forms.

However, there is a work-around to this. To get it to receive submissions, a hidden plain HTML form is added to the `index.html` file. This form works with the build bots. When submitting the Angular Form, a post request is made to this hidden form which is then captured by Netlify Forms. 

In this article, we will create a reactive form. We’ll also develop a service to make a post request to the hidden HTML form. Lastly, we will deploy the app to Netlify Edge.

## Example

To illustrate how to build the app, we will take an example of a feedback form common on many websites. We will use this form to collect comments/complaints, questions, and suggestions from users of the site along with their name and email. We shall also use it to collect their rating of the site. 

### Requirements

To follow along with this tutorial, you will need a Netlify account and the Angular CLI installed. If you do not have the CLI, you can install it using npm.

<pre><code class="language-bash">npm install -g @angular/cli
</code></pre>

If you’ve not signed up for a Netlify account yet, you can create one [here](https://app.netlify.com/signup). Netlify offers sign-up through Github, Gitlab, Bitbucket, or Email. Depending on what deployment method you choose to go with, they may be other requirements. They will be stated under each deployment method. 

{{% feature-panel %}}

## Setting Up The App

To start, we will create the app and call it `feedback`. When creating it, add routing to it when asked in the prompts.

<pre><code class="language-ts">ng new feedback
</code></pre>

Next, we’ll generate three components: a feedback form, a successful submission message page, and a 404 page. Netlify Forms allow you to navigate to a page upon successful form entry submission. That’s what we’ll use the `SuccessComponent` for.

<pre><code class="language-ts">ng g c feedback
ng g c success
ng g c page-not-found
</code></pre>

After generating the components, we’ll add the routes to each page in the `AppRoutingModule` within the `app-routing.module.ts` file.

<pre><code class="language-ts">const routes: Routes = [
  { path:'', component: FeedbackComponent },
  { path: 'success', component: SuccessComponent },
  { path: '**', component: PageNotFoundComponent }
];
</code></pre>

We’ll use the `FormBuilder` service to create our reactive form. This is because it is more convenient and less repetitive than using basic form controls. To have access to it, we’ll need to register the `ReactiveFormsModule` in the `app.module.ts` file.

Since we will be making a post request to the hidden HTML form, we also have to register the `HttpClientModule`. 

<pre><code class="language-javascript">import { ReactiveFormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    // other imports
    ReactiveFormsModule,
    HttpClientModule
  ]
})
export class AppModule { }
</code></pre>

Proceed to change the contents of `app.component.html` to just have the router outlet. 

<pre><code class="language-html">&lt;router-outlet&gt;&lt;/router-outlet&gt;
</code></pre>

The different pages will share some styling. So add the styling below to *styles.css*. 

<pre><code class="language-css">html, body {
    height: 100%;
    width: 100%;
    display: flex;
    align-items: flex-start;
    justify-content: center;
}

h1 {
    margin: 0;
    text-align: center;
}

h1, p, label {
    font-family: Arial, Helvetica, sans-serif;
}

p {
    max-width: 25rem;
}

#container {
    border: none;
    padding: .4rem;
    border-radius: 0;
    flex-direction: column;
    display: flex;
}

hr {
    width: 80%;
}

button {
    color: white;
    background-color: black;
    font-size: large;
    padding: .5rem;
    border-radius: .5rem;
    margin-top: 1rem;
}

@media screen and (min-height: 700px) {
    html, body {
        align-items: center;
        justify-content: center;
    }
}

@media screen and (min-width: 480px) {
    #container {
        border: .1rem solid lightgray;
        padding: 2rem;
        border-radius: .5rem;
    }

    html, body {
        align-items: center;
        justify-content: center;
    }
}
</code></pre>

## Create The Reactive Form

In our `FeedbackComponent` class, we will begin by importing the `FormBuilder` service which we’ll use to create the form. We’ll also import the `Validators` class for form input validation. 

<pre><code class="language-javascript">import { FormBuilder, Validators } from '@angular/forms';
</code></pre>

We will then inject the `FormBuilder` service by adding it to the `FeedbackComponent` constructor. 

<pre><code class="language-javascript">constructor(private fb: FormBuilder) { }
</code></pre>

Next, we’ll define the form model using the `group` method of the injected `FormBuilder` service. We’ll also add an `errorMsg` property to hold any errors we may encounter when submitting the form input. Also included is a `closeError` method that will close the error alert that displays on the form. 

Each control in the form model will be verified using validators from the <code>[Validators](https://angular.io/api/forms/Validators)</code> class. If any of the inputs fail validation, the form will be invalid and submission will be disabled. You can choose to add multiple validators to a form control like in the case of the <code>email </code>control. 

<pre><code class="language-javascript">export class FeedbackComponent {
  feedbackForm = this.fb.group({
    firstName: ['', Validators.required],
    lastName: ['', Validators.required],
    email: ['', [Validators.email, Validators.required]],
    type: ['', Validators.required],
    description: ['', Validators.required],
    rating: [0, Validators.min(1)]
  });

  errorMsg = '';

  closeError() {
    this.errorMsg = '';
  }

  // ...
}
</code></pre>

In the component’s template (`feedback.component.html`), we shall add this. 

<div class="break-out">

 <pre><code class="language-html">&lt;div id="container"&gt;
  &lt;div class="error" [class.hidden]="errorMsg.length == 0"&gt;
    &lt;p&gt;{{errorMsg}}&lt;/p&gt;
    &lt;span (click)="closeError()" class="close"&gt;✖︎&lt;/span&gt;
  &lt;/div&gt;
  &lt;h1&gt;Feedback Form&lt;/h1&gt;
  &lt;hr&gt;
  &lt;p&gt;We’d like your feedback to improve our website.&lt;/p&gt;
  &lt;form [formGroup]="feedbackForm" name="feedbackForm" (ngSubmit)="onSubmit()"&gt;
    &lt;div id="options"&gt;
      &lt;p class="radioOption"&gt;
        &lt;input formControlName="type" type="radio" id="suggestion" name="type" value="suggestion"&gt;
        &lt;label for="suggestion"&gt;Suggestion&lt;/label&gt;&lt;br&gt;
      &lt;/p&gt;
      &lt;p class="radioOption"&gt;
        &lt;input formControlName="type" type="radio" id="comment" name="type" value="comment"&gt;
        &lt;label for="comment"&gt;Comment&lt;/label&gt;&lt;br&gt;
      &lt;/p&gt;
      &lt;p class="radioOption"&gt;
        &lt;input formControlName="type" type="radio" id="question" name="type" value="question"&gt;
        &lt;label for="question"&gt;Question&lt;/label&gt;&lt;br&gt;
      &lt;/p&gt;
    &lt;/div&gt;
    &lt;div class="inputContainer"&gt;
      &lt;label&gt;Description:&lt;/label&gt;
      &lt;textarea rows="6" formControlName="description"&gt;&lt;/textarea&gt;
    &lt;/div&gt;
    &lt;div class="inputContainer"&gt;
      &lt;div id="ratingLabel"&gt;
        &lt;label&gt;How would you rate our site?&lt;/label&gt;
        &lt;label id="ratingValue"&gt;{{feedbackForm.value?.rating}}&lt;/label&gt;
      &lt;/div&gt;
      &lt;input formControlName="rating" type="range" name="rating" max="5"&gt;
    &lt;/div&gt;
    &lt;div class="inputContainer"&gt;
      &lt;label&gt;Name:&lt;/label&gt;
      &lt;div class="nameInput"&gt;
        &lt;input formControlName="firstName" type="text" name="firstName" placeholder="First"&gt;
        &lt;input formControlName="lastName" type="text" name="lastName" placeholder="Last"&gt;
      &lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="inputContainer"&gt;
      &lt;label&gt;Email:&lt;/label&gt;
      &lt;input formControlName="email" type="email" name="email"&gt;
    &lt;/div&gt;
    &lt;div class="inputContainer"&gt;
      &lt;button type="submit" [disabled]="feedbackForm.invalid"&gt;Submit Feedback&lt;/button&gt;
    &lt;/div&gt;
  &lt;/form&gt;
&lt;/div&gt;
</code></pre>
</div>

Note that the form element should have the `[formGroup]="feedbackForm"` attribute corresponding to the model we just created. Also, each of the input elements should have a `formControlName=""` attribute corresponding to its counterpart form control in the model. 

To style the form, add this to` feedback.component.css`. 

<pre><code class="language-css">#options {
    display: flex;
    flex-direction: column;
}

#options label {
    margin: 0 0 0 .2rem;
}

.radioOption {
    margin: 0 0 .2rem 0;
}

.inputContainer {
    display: flex;
    flex-direction: column;
    margin: .5rem 0 .5rem 0;
}

label {
    margin: .5rem 0 .5rem 0;
}

.nameInput {
    display: flex;
    flex-direction: column;
}

button:disabled {
    cursor: not-allowed;
    pointer-events: all;
    background-color: slategrey;
}

#ratingLabel {
    display: flex;
    justify-content: space-between;
    margin: .5rem 0 .5rem 0;
}

#ratingValue {
    font-weight: bolder;
    font-size: large;
    border: .1rem solid lightgray;
    padding: .4rem .6rem .1rem .6rem;
    margin: 0;
    vertical-align: middle;
    border-radius: .3rem;
}

.error {
    color: darkred;
    background-color: lightsalmon;
    border: .1rem solid crimson;
    border-radius: .3rem;
    padding: .5rem;
    text-align: center;
    margin: 0 0 1rem 0;
    display: flex;
    width: inherit;
}

.error p {
    margin: 0;
    flex-grow: 1;
}

textarea, input {
    margin: .1rem;
    font-family: Arial, Helvetica, sans-serif;
    padding: 5px;
    font-size: medium;
    font-weight: lighter;
}

.close {
    cursor: default;
}

.hidden {
    display: none;
}

@media screen and (min-width: 480px) {
    #options {
        flex-direction: row;
        justify-content: space-around;
    }

    .nameInput {
        flex-direction: row;
        justify-content: space-between;
    }
}
</code></pre>

This is what the form will look like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9832f51-1890-4546-a74f-0a9566c7445c/angular-netlify-edge-forms-feedback-form.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9832f51-1890-4546-a74f-0a9566c7445c/angular-netlify-edge-forms-feedback-form.png" sizes="100vw" caption="Screenshot of Feedback Form (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9832f51-1890-4546-a74f-0a9566c7445c/angular-netlify-edge-forms-feedback-form.png'>Large preview</a>)" alt="Feedback Form" >}}

## Adding A Hidden HTML Form

As stated earlier, we need to add a hidden HTML form that the Netlify Forms build bots can parse. Submissions will then be sent from our reactive form to the hidden HTML form. The HTML form is put in the *index.html* file. 

This form should have the same name as the reactive form. Additionally, it should contain three other attributes: `netlify`, `netlify-honeypot`, and `hidden`. The bots look for any forms that have the `netlify` attribute so that Netlify can process inputs from them. The `netlify-honeypot` attribute is added to prevent captchas from being shown when a submission is made and enables extra spam protection.

<div class="break-out">

 <pre><code class="language-html">&lt;!doctype html&gt;
&lt;html lang="en"&gt;
&lt;!-- Head --&gt;
 &lt;body&gt;
  &lt;form name="feedbackForm" netlify netlify-honeypot="bot-field" hidden&gt;
    &lt;input type="text" name="firstName"/&gt;
    &lt;input type="text" name="lastName"/&gt;
    &lt;input type="text" name="email"/&gt;
    &lt;input type="text" name="feedbackType"/&gt;
    &lt;input type="text" name="description"/&gt;
    &lt;input type="text" name="rating"/&gt;
  &lt;/form&gt;
  &lt;app-root&gt;&lt;/app-root&gt;
 &lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

It’s important to note that since you can’t set the value of `file` input elements, you can’t upload a file using this method. 

## Making A Post Request To The Hidden Form 

To send a submission from the reactive form to the HTML form, we’ll make a post request containing the submission to `index.html`. The operation will be performed in the `onSubmit` method of the `FeedbackComponent`.

However, before we can do that, we need to create two things: a `Feedback` interface and a `NetlifyFormsService`. Let’s start with the interface. 

<pre><code class="language-ts">touch src/app/feedback/feedback.ts
</code></pre>

The contents of this file will be:

<pre><code class="language-ts">export interface Feedback {
   firstName: string;
   lastName: string;
   email: string;
   type: string;
   description: string;
   rating: number;
}
</code></pre>

The `NetlifyFormsService` will contain a public method to submit a feedback entry, a private method to submit a generic entry, and another private one to handle any errors. You could add other public methods for additional forms.

To generate it, run the following:

<pre><code class="language-bash">ng g s netlify-forms/netlify-forms
</code></pre>

The `submitEntry` method returns an `Observable<string>` because Netlify sends a HTML page with a success alert once we post data to the form. This is the service:

<div class="break-out">

 <pre><code class="language-javascript">import { Injectable } from '@angular/core';
import { HttpClient, HttpErrorResponse, HttpParams } from '@angular/common/http';
import { Feedback } from '../feedback/feedback';
import { Observable, throwError } from 'rxjs';
import { catchError } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class NetlifyFormsService {

  constructor(private http: HttpClient) { }

  submitFeedback(fbEntry: Feedback): Observable<string> {
    const entry = new HttpParams({ fromObject: {
      'form-name': 'feedbackForm',
      ...fbEntry,
      'rating': fbEntry.rating.toString(),
    }});

    return this.submitEntry(entry);
  }

  private submitEntry(entry: HttpParams): Observable<string> {
    return this.http.post(
      '/',
      entry.toString(),
      {
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        responseType: 'text'
      }
    ).pipe(catchError(this.handleError));
  }

  private handleError(err: HttpErrorResponse) {
    let errMsg = '';

    if (err.error instanceof ErrorEvent) {
      errMsg = `A client-side error occurred: ${err.error.message}`;
    } else {
      errMsg = `A server-side error occurred. Code: ${err.status}. Message: ${err.message}`;
    }

    return throwError(errMsg);
  }
}
</code></pre>
</div>

We’ll send the form submission as `HttpParams`. A header for the `ContentType` should be included with the value `application/x-www-form-urlencoded`. The `responseType` option is specified as `text` because if successful, posting to the hidden form will return an HTML page containing a generic success message from Netlify. If you do not include this option, you will get an error because the response will be parsed as `JSON`. Below is a screenshot of the generic Netlify success message. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6c12c5-544c-46ef-bce1-8ce3a9faa491/netlify-generic-success-message.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6c12c5-544c-46ef-bce1-8ce3a9faa491/netlify-generic-success-message.png" sizes="100vw" caption="Screenshot of Netlify Generic Success Message (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6c12c5-544c-46ef-bce1-8ce3a9faa491/netlify-generic-success-message.png'>Large preview</a>)" alt="forms/Netlify Generic Success Message" >}}

In the `FeedbackComponent` class, we shall import the `NetlifyFormsService` and `Router`. We’ll submit the form entry using the `NetlifyFormsService.submitEntry` method. If the submission is successful, we will redirect to the successful submission page and reset the form. We’ll use the `Router` service for the redirection. If unsuccessful, the `errorMsg` property will be assigned the error message and be displayed on the form. 

<div class="break-out">

 <pre><code class="language-javascript">import { Router } from '@angular/router';
import { NetlifyFormsService } from '../netlify-forms/netlify-forms.service';
</code></pre>
</div>

After that, inject both the `NetlifyFormsService` and `Router` in the constructor.

<pre><code class="language-javascript">constructor(
   private fb: FormBuilder,
   private router: Router,
   private netlifyForms: NetlifyFormsService
) {}
</code></pre>

Lastly, call the `NetlifyFormsService.submitEntry` method in `FeedbackComponent.onSubmit`. 

<pre><code class="language-javascript">onSubmit() {
this.netlifyForms.submitFeedbackEntry(this.feedbackForm.value).subscribe(
   () => {
     this.feedbackForm.reset();
     this.router.navigateByUrl('/success');
   },
   err => {
     this.errorMsg = err;
   }
 );
}
</code></pre>

{{% ad-panel-leaderboard %}}

## Create A Successful Submission Page

When a user completes a submission, Netlify returns a generic success message shown in the last screenshot of the previous section. However, you can link back to your own custom success message page. You do this by adding the `action` attribute to the hidden HTML form. Its value is the relative path to your custom success page. This path must start with `/` and be relative to your root site. 

Setting a custom success page, however, does not seem to work when using a hidden HTML form. If the post request to the hidden HTML form is successful, it returns the generic Netlify success message as an HTML page. It does not redirect even when an `action` attribute is specified. So instead we shall navigate to the success message page after a submission using the `Router` service. 

First, let’s add content to the `SuccessComponent` we generated earlier. In `success.component.html`, add: 

<pre><code class="language-html">&lt;div id="container"&gt;
    &lt;h1&gt;Thank you!&lt;/h1&gt;
    &lt;hr&gt;
    &lt;p&gt;Your feedback submission was successful.&lt;/p&gt;
    &lt;p&gt;Thank you for sharing your thoughts with us!&lt;/p&gt;
    &lt;button routerLink="/"&gt;Give More Feedback&lt;/button&gt;
&lt;/div&gt;
</code></pre>

To style the page, add this to `success.component.css`: 

<pre><code class="language-css">p {
    margin: .2rem 0 0 0;
    text-align: center;
}
</code></pre>

This is what the page looks like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/592662be-674f-4b98-8feb-525e96fcc299/angular-netlify-edge-successful-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/592662be-674f-4b98-8feb-525e96fcc299/angular-netlify-edge-successful-page.png" sizes="100vw" caption="Screenshot of Successful Submission Page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/592662be-674f-4b98-8feb-525e96fcc299/angular-netlify-edge-successful-page.png'>Large preview</a>)" alt="Successful Submission Page" >}}

In the `FeedbackComponent` class, we already added the `Router `service as an import and injected it into the constructor. In its `onSubmit `method, after the request is successful and the form has reset, we navigate to the successful submission page, `/success`. We use the `navigateByUrl` method of the router to do that.

## Creating The 404 Page

The 404 page may not be necessary but is a nice to have. The contents of `page-not-found.component.html` would be: 

<pre><code class="language-html">&lt;div id="container"&gt;
    &lt;h1&gt;Page Not Found!&lt;/h1&gt;
    &lt;hr&gt;
    &lt;p&gt;Sorry! The page does not exist.&lt;/p&gt;
    &lt;button routerLink="/"&gt;Go to Home&lt;/button&gt;
&lt;/div&gt;
</code></pre>

To style it, add this to `page-not-found.component.css`:

<pre><code class="language-css">p {
    text-align: center;
}
</code></pre>

This is what the 404 page will look like.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2555fd08-9d4f-4f61-854e-cd1f5f15fb27/angular-netlify-edge-404-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2555fd08-9d4f-4f61-854e-cd1f5f15fb27/angular-netlify-edge-404-page.png" sizes="100vw" caption="Screenshot of 404 Page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2555fd08-9d4f-4f61-854e-cd1f5f15fb27/angular-netlify-edge-404-page.png'>Large preview</a>)" alt="404 Page" >}}

## Fix Routing Before Deployment

Since we’re using the `Router` service, all our routing is done on the client. If a link to a page in our app is pasted in the address bar (deep link) or there is a page refresh, that request we’ll be sent to our server. The server does not contain any of our routes because they were configured in the frontend, in our app. We’ll receive a 404 status in these instances. 

To fix this, we need to tell the Netlify server to redirect all requests to our <code>index.html</code></strong> page. This way our Angular router can handle them. If you’re interested, you can read more about this phenomenon [here](https://angular.io/guide/visual-studio-2015#for-apps-that-use-routing) and [here](https://angular.io/guide/deployment#fallback). 

We’ll start by creating a `_redirects` file in our *src* folder. The `_redirects` file is a plain text file that specifies redirect and rewrite rules for the Netlify site. It should reside in the site publish site directory (`dist/<app_name>`). We’ll place it in the `src` folder and specify it as an asset in the `angular.json` file. When the app is compiled, it will be placed in `dist/<app_name>`.

<pre><code class="language-javascript">touch src/_redirects
</code></pre>

This file will contain the rule below. It indicates that all requests to the server should be redirected to `index.html`. We also add a HTTP status code option at the end to indicate that these redirects should return a `200` status. By default, a `301` status is returned.

<pre><code class="language-bash">/*  /index.html 200
</code></pre>

The last thing we have to do is add the below option in our `angular.json` und `er projects > {your_project_name} > architect > options > assets`. Include it in the `assets` array:

<pre><code class="language-css">{
  "glob": "_redirects",
  "input": "src",
  "output": "/"
}
</code></pre>

## Preview Your App Locally

Before you can deploy the feedback app, it’s best to preview it. This allows you to make sure your site works as you had intended it. You may unearth issues resulting from the build process like broken paths to resources among other things. First, you’ll have to build your app. We’ll then serve the compiled version using a server. We’ll use [lite-server](https://github.com/johnpapa/lite-server) which is a lightweight live-reload server for web apps. 

**Note**: *Since the app is not deployed on Netlify just yet, you’ll get a 404 error when you attempt to make the post request. This is because Netlify Forms only work on deployed apps. You’ll see an error on the form as shown in the screenshot below, however, it will work once you’ve deployed it.*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48dc131-dbbd-4513-9573-27a601e2f711/error-on-feedback-form.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48dc131-dbbd-4513-9573-27a601e2f711/error-on-feedback-form.png" sizes="100vw" caption="Screenshot of Error on Feedback Form (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48dc131-dbbd-4513-9573-27a601e2f711/error-on-feedback-form.png'>Large preview</a>)" alt="Error on Feedback Form" >}}

<ol>
  <li>To begin, install <a href="https://github.com/johnpapa/lite-server">lite-server</a>:<br /> 

<pre><code class="language-bash">npm install lite-server --save-dev
</code></pre>
</li>
<li>Next, within your app’s workspace directory, build your app. To make sure builds are run every time your files change, pass the <code>--watch</code> flag to it. Once the app is compiled, the results are written to the <code>dist/&lt;app name&gt;</code> output directory. If you are using a version control system, make sure to not check in the <code>dist</code> folder because it is generated and is only for preview purposes.<br />

<pre><code class="language-bash">ng build --watch
</code></pre>
</li>
<li>To serve the compiled site, run the <code>lite-server</code> against the build output directory.<br />

<pre><code class="language-bash">lite-server --baseDir="dist/&lt;app name&gt;"
</code></pre>
</li>
</ol>

<p>The site is now served at <code>localhost:3000</code>. Check it out on your browser and make sure it works as expected before you begin its deployment.</p>

{{% ad-panel-leaderboard %}}

## Deployment 

There are multiple ways you can deploy your Angular project onto Netlify Edge. We shall cover three here:

<ol>
  <li><a href="#using-netlify-builder">Using <code>netlify-builder</code></a>,</li>
  <li><a href="#using-git-and-netlify-web-ui">Using Git and the Netlify web UI</a>,</li>
  <li><a href="#using-netlify-cli-tool">Using the Netlify CLI tool</a>.</li>
</ol>

### 1. Using <code>netlify-builder</code>

[netlify-builder](https://github.com/ngx-builders/netlify-builder) facilitates the deployment of Angular apps through the Angular CLI. To use this method, your app needs to have been created using [Angular CLI v8.3.0 or higher.](https://cli.angular.io/)

<ol>
  <li>From the <strong>Sites</strong> tab of your Netlify dashboard, create a new project. Since we won't be using Git to create a project, drag any empty folder to the dotted-border area marked <strong>"Drag and drop your site folder here"</strong>. This will automatically create a project with a random name. You can change this name under the site’s domain settings later if you wish.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c84b28-a2e5-45af-a649-226f408d0866/1-builder-create-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c84b28-a2e5-45af-a649-226f408d0866/1-builder-create-project.png" sizes="100vw" caption="Screenshot of the dashboard to create a project (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c84b28-a2e5-45af-a649-226f408d0866/1-builder-create-project.png'>Large preview</a>)" alt="Screenshot of the dashboard to create a project" >}}
<br />
This is what you should see once your project has been created.<br />
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f45f9f1d-1d8d-4e8d-ad91-e9255b1c6b1c/2-sample-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f45f9f1d-1d8d-4e8d-ad91-e9255b1c6b1c/2-sample-project.png" sizes="100vw" caption="Screenshot of a project page for a sample project (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f45f9f1d-1d8d-4e8d-ad91-e9255b1c6b1c/2-sample-project.png'>Large preview</a>)" alt="Screenshot of a project page for a sample project" >}}
</li>
<li>Before you can deploy using this method, you will need to get the Netlify project’s <strong>API ID</strong> and a Netlify <strong>personal access token</strong> from your account. You can get the project API ID from the site settings. Under <em>Site Settings > General > Site Details > Site Information</em> you will find your project’s API ID.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66957839-55f8-4219-8e0a-2680e435e135/3-site-settings-button.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66957839-55f8-4219-8e0a-2680e435e135/3-site-settings-button.png" sizes="100vw" caption="Screenshot showing where the Site settings Button is (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66957839-55f8-4219-8e0a-2680e435e135/3-site-settings-button.png'>Large preview</a>)" alt="Screenshot showing where the Site settings Button is" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7bf0346-c4ce-4e13-a707-914131235007/4-api-id.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7bf0346-c4ce-4e13-a707-914131235007/4-api-id.png" sizes="100vw" caption="Screenshot showing where the site’s API ID is in its settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7bf0346-c4ce-4e13-a707-914131235007/4-api-id.png'>Large preview</a>)" alt="Screenshot showing where the site’s API ID is in its settings" >}}
<br />
You can get a personal access token in your user settings. At <em>User Settings > Applications > Personal access tokens</em>, click the <strong>New Access Token</strong> button. When prompted, enter the description of your token, then click the <strong>Generate Token</strong> button. Copy your token. For persistence’s sake, you can store these values in a <code>.env</code> file within your project but do not check this file in if you are using a version control system.<br />
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abeff112-fca1-4779-b37e-ef7be61b7445/5-user-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abeff112-fca1-4779-b37e-ef7be61b7445/5-user-settings.png" sizes="100vw" caption="Screenshot showing where the User Settings button is (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abeff112-fca1-4779-b37e-ef7be61b7445/5-user-settings.png'>Large preview</a>)" alt="Screenshot showing where the User Settings button is" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd98f5ef-295c-4a94-a977-1553b2e83bcc/6-personal-access-tokens-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd98f5ef-295c-4a94-a977-1553b2e83bcc/6-personal-access-tokens-settings.png" sizes="100vw" caption="Screenshot showing where to create a personal access token (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd98f5ef-295c-4a94-a977-1553b2e83bcc/6-personal-access-tokens-settings.png'>Large preview</a>)" alt="Screenshot showing where to create a personal access token" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8a05ad-fd7e-4a8b-b6b0-b67e3be07b33/7-token-description.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8a05ad-fd7e-4a8b-b6b0-b67e3be07b33/7-token-description.png" sizes="100vw" caption="Screenshot showing where to enter the token description (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8a05ad-fd7e-4a8b-b6b0-b67e3be07b33/7-token-description.png'>Large preview</a>)" alt="Screenshot showing where to enter the token description" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/905fa599-d099-46f2-86e8-d9d29fab8fd1/8-token-value.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/905fa599-d099-46f2-86e8-d9d29fab8fd1/8-token-value.png" sizes="100vw" caption="Screenshot showing the token value (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/905fa599-d099-46f2-86e8-d9d29fab8fd1/8-token-value.png'>Large preview</a>)" alt="Screenshot showing the token value" >}}
</li>
<li>Next, add <code>netlify-builder</code> to your project using <code>ng add</code>.<br />

<pre><code class="language-bash">ng add @netlify-builder/deploy
</code></pre>

Once it’s done installing, you will be prompted to add the API ID and personal access token.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4559294d-b515-4751-befd-e0259f8ba1fd/9-add-builder.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4559294d-b515-4751-befd-e0259f8ba1fd/9-add-builder.png" sizes="100vw" caption="Screenshot showing the prompts from adding the netlify builder (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4559294d-b515-4751-befd-e0259f8ba1fd/9-add-builder.png'>Large preview</a>)" alt="Screenshot showing the prompts from adding the netlify builder" >}}
<br />
It’s optional to add these here. You could ignore this prompt because they will be added to your <code>angular.json</code> file which is usually checked in if you use a version control system. It’s not safe to store this kind of sensitive information on code repos. If you are not checking this file in, you could just input your API ID and personal access token. The entry below will be modified in your <code>angular.json</code> file under the <code>architect</code> settings.<br />

<pre><code class="language-json">"deploy": {
    "builder": "@netlify-builder/deploy:deploy",
    "options": {
    "outputPath": "dist/&lt;app name&gt;",
    "netlifyToken": "",
    "siteId": ""
    }
}
</code></pre>
</li>
<li>All that’s left is to deploy your application by running:<br />

<pre><code class="language-bash">NETLIFY_TOKEN=&lt;access token&gt; NETLIFY_API_ID=&lt;api id&gt; ng deploy
</code></pre>

Alternatively, you could put this in a script and run it when you need to deploy your app.<br />

<div class="break-out">

 <pre><code class="language-bash"># To create the script
touch deploy.sh && echo "NETLIFY_TOKEN=&lt;access token&gt; NETLIFY_API_ID=&lt;api id&gt; ng deploy" &gt;&gt; deploy.sh && chmod +x deploy.sh

# To deploy
./deploy.sh
</code></pre>
</div>

This is the output you should see once you run this command:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f55ca156-b8ee-48f1-85f9-6e4a5dbd176a/10-deployment-results.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f55ca156-b8ee-48f1-85f9-6e4a5dbd176a/10-deployment-results.png" sizes="100vw" caption="Screenshot showing the results of the deployment (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f55ca156-b8ee-48f1-85f9-6e4a5dbd176a/10-deployment-results.png'>Large preview</a>)" alt="Screenshot showing the results of the deployment" >}}
</li>
</ol>

### 2. Using Git And The Netlify Web UI

If your Angular app’s code is hosted on either Github, Bitbucket, or Gitlab, you can host the project using Netlify’s web UI. 

<ol>
  <li>From the <strong>Sites</strong> tab on your Netlify dashboard, click the “<ystrong>New site from Git”</strong> button.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7e56612-49ba-4953-9607-68b391500d8c/1-create-site.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7e56612-49ba-4953-9607-68b391500d8c/1-create-site.png" sizes="100vw" caption="Screenshot showing the button to create a new site (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7e56612-49ba-4953-9607-68b391500d8c/1-create-site.png'>Large preview</a>)" alt="Screenshot showing the button to create a new site" >}}
</li>
<li>Connect to a code repository service. Pick the service where your app code is hosted. You’ll be prompted to authorize Netlify to view your repositories. This will differ from service to service.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0605d8-864f-45e3-93b6-2f09847ee428/2-connect-to-provider.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0605d8-864f-45e3-93b6-2f09847ee428/2-connect-to-provider.png" sizes="100vw" caption="Screenshot showing options for connecting to a Git provider(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0605d8-864f-45e3-93b6-2f09847ee428/2-connect-to-provider.png'>Large preview</a>)" alt="Screenshot showing options for connecting to a Git provider" >}}
</li>
<li>Pick your code repository.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181fa802-6d24-4040-acb4-a5cb1161be43/3-pick-a-repository.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181fa802-6d24-4040-acb4-a5cb1161be43/3-pick-a-repository.png" sizes="100vw" caption="Screenshot showing list of available repositories (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181fa802-6d24-4040-acb4-a5cb1161be43/3-pick-a-repository.png'>Large preview</a>)" alt="Screenshot showing list of available repositories" >}}
</li>
<li>Next, you’ll specify the deployments and build settings. In this case, select the branch you’d like to deploy from, specify the build command as <code>ng deploy --prod</code> and the publish directory as <code>dist/&lt;your app name></code>.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee775f6-dd05-4648-8101-fca03f1ad6eb/4-build-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee775f6-dd05-4648-8101-fca03f1ad6eb/4-build-settings.png" sizes="100vw" caption="Screenshot showing build and deployment settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee775f6-dd05-4648-8101-fca03f1ad6eb/4-build-settings.png'>Large preview</a>)" alt="Screenshot showing build and deployment settings" >}}
</li>
<li>Click the <strong>Deploy Site</strong> button and you’re done.</li>
</ol>

### 3. Using The Netlify CLI Tool

<ol>
  <li>To start, install the Netlify CLI tool as follows:<br />

<pre><code class="language-bash">npm install netlify-cli -g
</code></pre>

If the installation is successful, you should see these results on your terminal:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf20a225-e30f-4e7f-863d-57e358ba4ddc/1-cli-installation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf20a225-e30f-4e7f-863d-57e358ba4ddc/1-cli-installation.png" sizes="100vw" caption="Screenshot showing results of a successful Netlify CLI installation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf20a225-e30f-4e7f-863d-57e358ba4ddc/1-cli-installation.png'>Large preview</a>)" alt="Screenshot showing results of a successful Netlify CLI installation" >}}
</li>
<li>Next, log in to Netlify by running:<br />

<pre><code class="language-bash">netlify login
</code></pre>

When you run this command, it will navigate to a browser window where you will be prompted to authorize the Netlify CLI. Click the <code>Authorize</code> button. You can then proceed to close the tab once authorization is granted. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6a3ca41-86a6-4fc0-903c-6c8cb7b4d553/2-grant-netlify.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6a3ca41-86a6-4fc0-903c-6c8cb7b4d553/2-grant-netlify.png" sizes="100vw" caption="Screenshot showing a dialog requesting authorization of Netlify CLI (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6a3ca41-86a6-4fc0-903c-6c8cb7b4d553/2-grant-netlify.png'>Large preview</a>)" alt="Screenshot showing a dialog requesting authorization of Netlify CLI" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd06c43-1c83-49c9-a779-a455df30c91d/3-authorization-granted.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd06c43-1c83-49c9-a779-a455df30c91d/3-authorization-granted.png" sizes="100vw" caption="Screenshot showing authorization granted dialog (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd06c43-1c83-49c9-a779-a455df30c91d/3-authorization-granted.png'>Large preview</a>)" alt="Screenshot showing authorization granted dialog" >}}
</li>
<li>To create a new Netlify project, run the following on your terminal:<br />

<pre><code class="language-bash">netlify init
</code></pre>

You will be prompted to either connect your Angular app to an existing Netlify project or create a new one. Choose the <strong>Create & configure a new site</strong> option. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d73597-9292-4cda-aaa8-3f7950b94f6b/4-new-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d73597-9292-4cda-aaa8-3f7950b94f6b/4-new-project.png" sizes="100vw" caption="Screenshot showing options for creating or connecting a project (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d73597-9292-4cda-aaa8-3f7950b94f6b/4-new-project.png'>Large preview</a>)" alt="Screenshot showing options for creating or connecting a project" >}}

Next, select your team and a name for the site you would like to deploy. Once the project has been created, the CLI tool will list site details for your project.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77c96ea4-6873-4b58-8a2c-1cb310131d56/5-new-site-details.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77c96ea4-6873-4b58-8a2c-1cb310131d56/5-new-site-details.png" sizes="100vw" caption="Screenshot showing the details for the new site (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77c96ea4-6873-4b58-8a2c-1cb310131d56/5-new-site-details.png'>Large preview</a>)" alt="Screenshot showing the details for the new site" >}}

After which the CLI tool will prompt you to connect your Netlify account to a Git hosting provider to configure webhooks and deploy keys. You cannot opt-out of this. Pick an option to login in then authorize Netlify.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54011631-eec4-40fb-bbf1-c38366a1324c/6-git-provider.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54011631-eec4-40fb-bbf1-c38366a1324c/6-git-provider.png" sizes="100vw" caption="Screenshot showing prompt to connect to a Git provider (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54011631-eec4-40fb-bbf1-c38366a1324c/6-git-provider.png'>Large preview</a>)" alt="Screenshot showing prompt to connect to a Git provider" >}}

Next, you’ll be asked to enter a build command. Use:<br />

<pre><code class="language-bash">ng build --prod
</code></pre>

Afterward, you’ll be asked to provide a directory to deploy. Enter <code>dist/&lt;app name&gt;</code> with your app’s name.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3d3a115-cc67-4fd0-9c1e-3c78dddedecf/7-build-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3d3a115-cc67-4fd0-9c1e-3c78dddedecf/7-build-settings.png" sizes="100vw" caption="Screenshot showing a build-settings prompt (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3d3a115-cc67-4fd0-9c1e-3c78dddedecf/7-build-settings.png'>Large preview</a>)" alt="Screenshot showing a build-settings prompt" >}}

At the end of that, the command will complete and display this output.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bedc383-8f22-4500-9810-55c136307bc6/8-init-results.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bedc383-8f22-4500-9810-55c136307bc6/8-init-results.png" sizes="100vw" caption="Screenshot showing results of a successful project initialization (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bedc383-8f22-4500-9810-55c136307bc6/8-init-results.png'>Large preview</a>)" alt="Screenshot showing results of a successful project initialization" >}}
</li>
<li>To deploy the app, run:<br />

<pre><code class="language-bash">netlify deploy --prod
</code></pre>

Using the <code>--prod</code> flag ensures that the build is deployed to production. If you omit this flag, the <code>netlify deploy</code> command will deploy your build to a unique draft URL that is used for testing and previewing. Once the deployment is complete, you should see this output:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec2ecac6-7fd6-445f-b1c5-ea8d0ed4d4c0/9-deploy-results.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec2ecac6-7fd6-445f-b1c5-ea8d0ed4d4c0/9-deploy-results.png" sizes="100vw" caption="Screenshot showing results of a successful deployment (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec2ecac6-7fd6-445f-b1c5-ea8d0ed4d4c0/9-deploy-results.png'>Large preview</a>)" alt="Screenshot showing results of a successful deployment" >}}
</li>
</ol>

## Viewing Form Submissions

Form submissions can be viewed on the Netlify dashboard under the **Forms** tab of your site. You can find it at `app.netlify.com/sites/<your_site_name>/forms`. On this page, all your active forms will be listed. The name attribute that you put down in the hidden form element is the name of the form on the dashboard. 

Once you select a form, all the submissions for that form will be listed. You can choose to download all the entries as a CSV file, mark them as spam, or delete them. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1a4910-c1fa-48a2-88e8-fb7f963d78f1/active-forms-list.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1a4910-c1fa-48a2-88e8-fb7f963d78f1/active-forms-list.png" sizes="100vw" caption="Screenshot of active forms listed on the site dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1a4910-c1fa-48a2-88e8-fb7f963d78f1/active-forms-list.png'>Large preview</a>)" alt="Active forms list" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef8c84ec-edbb-4829-9087-4d25525f2ee4/form-entries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef8c84ec-edbb-4829-9087-4d25525f2ee4/form-entries.png" sizes="100vw" caption="Screenshot of forms entries listed on the form dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef8c84ec-edbb-4829-9087-4d25525f2ee4/form-entries.png'>Large preview</a>)" alt="Form Entries" >}}

## Conclusion

Netlify Forms allow you to collect form submission from your app without having to create or configure a backend to do it. This can be useful especially in apps that only need to collect a limited amount of data like contact information, customer feedback, event sign-ups, and so on.

Pairing Angular reactive forms with Netlify forms allow you to structure your data model. Angular reactive forms have the added benefit of having their data model and form elements being in sync with each other. They do not rely on UI rendering.

Although Netlify Forms only work when deployed on Netlify Edge, the hosting platform is pretty robust, provides useful features like A/B testing, and automates app builds and deployments.

- [See the source code for this project&nbsp;&rarr;](https://github.com/smashingmagazine/feedback)

*You can continue reading more about using Netlify with your forms over [here](https://www.netlify.com/products/edge/).*

{{< signature "ra, il" >}}
