---
title: 'Forms And Validation In Ionic React'
slug: forms-validation-ionic-react
author: jerry-navi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/904d0dc8-ba87-4646-892d-d7f04c9c27b0/forms-validation-ionic-react.png
date: 2020-08-20T11:00:00.000Z
summary: >-
  Ionic Framework provides first-class support for building fast and mobile-optimized applications for any platform using React. In this tutorial, you will learn how to build forms when working with Ionic React and how to make these forms interactive by adding validation rules with helpful text hints.
description: >-
  In this tutorial, you will learn how to build forms when working with Ionic React and how to make these forms interactive by adding validation rules with helpful text hints.
categories:
  - UI
  - Apps
  - React
  - Tools
  - Forms
---

Ionic Framework is a UI Toolkit for building cross-platform mobile applications using HTML, CSS, and JavaScript. The release of Ionic 5 in early 2020 came with official support for React, enabling React developers to easily build mobile applications using their favorite tools. There isn’t much support for working with forms, however, and many of the existing libraries available for building forms in the React ecosystem do not play nicely with Ionic Framework’s components.

You will learn how to build forms using Ionic React’s UI input components in this tutorial. You will also learn how to use a library to help with detecting form input changes and responding to validation rules. Finally, you will learn to make your forms accessible to screen readers by adding helpful text to your inputs’ ARIA attributes.

## Ionic’s Form Components

Forms are an important part of most web and mobile applications today. Whether you are enabling access to restricted parts of your application through user registration and login forms or collecting feedback from your users, you have to &mdash; at some point in your application’s lifecycle &mdash; build a form.

Ionic provides prebuilt components for working with forms &mdash; some of which include `IonItem`, `IonLabel`, `IonInput`, `IonCheckbox` and `IonRadio`. We can combine these components to build standard looking forms without adding any styling ourselves.

For example, the following code:

<pre><code class="language-javascript">&lt;form className="ion-padding"&gt;
  &lt;IonItem&gt;
    &lt;IonLabel position="floating"&gt;Username&lt;/IonLabel&gt;
    &lt;IonInput /&gt;
  &lt;/IonItem&gt;
  &lt;IonItem&gt;
    &lt;IonLabel position="floating"&gt;Password&lt;/IonLabel&gt;
    &lt;IonInput type="password" /&gt;
  &lt;/IonItem&gt;
  &lt;IonItem lines="none"&gt;
    &lt;IonLabel&gt;Remember me&lt;/IonLabel&gt;
    &lt;IonCheckbox defaultChecked={true} slot="start" /&gt;
  &lt;/IonItem&gt;
  &lt;IonButton className="ion-margin-top" type="submit" expand="block"&gt;
    Login
  &lt;/IonButton&gt;
&lt;/form&gt;</code></pre>

Will give us a login form which looks like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb0ab23-85ea-47ff-872e-91f01894be0d/fig-01-standard-login-form-ios.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41f3f797-3f25-46ef-b3f6-60864958917d/01-standard-login-form-ios.png" sizes="100vw" caption="Standard login form on iOS (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb0ab23-85ea-47ff-872e-91f01894be0d/fig-01-standard-login-form-ios.png'>Large preview</a>)" alt="" >}}

Out of the box, Ionic's form components look great on iOS or Android, but they can be a bit unwieldy if you are working with React. As with most tools in the React ecosystem, you have to decide how you want to go about building your forms when it comes to functionality and accessibility &mdash; both equally as important as design.

While there are already so many React form helpers available to choose from, most of them do not work with Ionic's form components. I suspect the main reason for this is that the event fired when a field value changes in Ionic is `onIonChange`, whereas most of the existing form libraries listen for `onChange`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d760812-8ca0-4d65-bd06-2199800eb38b/fig-02-change-event-triggered.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d760812-8ca0-4d65-bd06-2199800eb38b/fig-02-change-event-triggered.png" sizes="100vw" caption="Change event triggered when the field changes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d760812-8ca0-4d65-bd06-2199800eb38b/fig-02-change-event-triggered.png'>Large preview</a>)" alt="" >}}

## React Hook Form: Small And Fast React Forms Library

Thankfully, it isn't all doom and gloom. I recently came across React Hook Form (RHF), a library for working with forms in React projects. It provides support for controlled or uncontrolled components and input validation, and the API is hooks-based so it only works with functional components.

The most appealing feature for Ionic React developers &mdash; in my opinion &mdash; is the wrapper `<Controller />` component it provides for working with controlled components. The component has an `onChangeName` prop which can be used to specify the change event name for whatever component instance you pass to it. I’ll show you how this makes working with forms in Ionic really easy in the following sections.

{{% feature-panel %}}

## Building A Signup Form

Let's see how RHF helps us with form functionality as we build a registration form in Ionic. If you are running the latest version of the Ionic CLI (run `npm i -g @ionic/cli` to confirm), start a new Ionic app with React by running the following command:

<pre><code class="language-bash">ionic start myApp blank --type=react</code></pre> 

I used a blank template here. You should be able to rewrite your existing forms to use the React Hook Form library with ease, especially if your components are written as Functional Components. 

**Note:** *You should remove the `ExploreContainer` component and its import in Home.tsx before proceeding with this tutorial.*

To get started with your form, install the React Hook Form package by running the following command in your project’s root directory:

<pre><code class="language-bash">yarn add react-hook-form</code></pre>

This will make the React Hook Form library available in your project. Let’s create a form input field using the library. Open the **Home.tsx** file and replace its contents with the following:

<div class="break-out">

<pre><code class="language-javascript">import { IonContent, IonPage, IonText, IonItem, IonLabel, IonInput, IonButton } from "@ionic/react";
import React from "react";
import "./Home.css";
import { Controller, useForm } from 'react-hook-form';

const Home: React.FC = () =&gt; {
  const { control, handleSubmit } = useForm();

  const registerUser = (data) =&gt; {
    console.log('creating a new user account with: ', data);
  }

  return (
    &lt;IonPage&gt;
      &lt;IonContent className="ion-padding"&gt;
        &lt;IonText color="muted"&gt;
          &lt;h2&gt;Create Account&lt;/h2&gt;
        &lt;/IonText&gt;
        &lt;form onSubmit={handleSubmit(registerUser)}&gt;
          &lt;IonItem&gt;
            &lt;IonLabel position="floating"&gt;Email&lt;/IonLabel&gt;
            &lt;Controller
              as={&lt;IonInput type="email" /&gt;}
              name="email"
              control={control}
              onChangeName="onIonChange"
            /&gt;
          &lt;/IonItem&gt;
          &lt;IonButton expand="block" type="submit" className="ion-margin-top"&gt;
            Register
          &lt;/IonButton&gt;
        &lt;/form&gt;
      &lt;/IonContent&gt;
    &lt;/IonPage&gt;
  );
};
export default Home;</code></pre>
</div>

This gives you a form with a single field to collect an email address. Let’s break down the important parts (highlighted in the code block).

First, we destructure the return value of the `useForm()` hook from RHF. `handleSubmit` passes your input’s values to the handler function you specify when the form passes validation. `control` is an object containing methods used for registering controlled components into RHF.

Next, we have a standard form item block, but unlike the example for the login form, we pass the `IonInput` component to RHF’s `<Controller />` component, register the change event by setting `<Controller />`'s `onChangeName` prop to Ionic’s change event name, and set the `control` prop to the control object from invoking `useForm()`.

This is good so far, but you might find yourself repeating nearly the same code over and over again. You could try to make a reusable `Input` component that builds an input field with given properties.

Create a file in the **src/components** directory named **Input.tsx** and add the following code to the file:

<div class="break-out">

<pre><code class="language-javascript">import React, { FC } from "react";
import { IonItem, IonLabel, IonInput } from "@ionic/react";
import { Controller, Control } from "react-hook-form";

export interface InputProps {
  name: string;
  control?: Control;
  label?: string;
  component?: JSX.Element;
}

const Input: FC&lt;InputProps&gt; = ({
  name,
  control,
  component,
  label,
}) =&gt; {
  return (
    &lt;&gt;
      &lt;IonItem&gt;
        {label && (
          &lt;IonLabel position="floating"&gt;{label}&lt;/IonLabel&gt;
        )}
        &lt;Controller
          as={component ?? &lt;IonInput /&gt;}
          name={name}
          control={control}
          onChangeName="onIonChange"
        /&gt;
      &lt;/IonItem&gt;
    &lt;/&gt;
  );
};

export default Input;</code></pre>
</div>

This component receives a `name` prop and optional `control`, `component` and `label` props and renders an input field using the Ionic form components introduced earlier. This reduces the amount of code you have to write when creating form input fields. You can finish the rest of your form using this component. Edit the Home.tsx file with the following changes:

<div class="break-out">

<pre><code class="language-javascript">import { IonContent, IonPage, IonText, IonInput, IonButton, IonCheckbox, IonItem, IonLabel } from "@ionic/react";
import React from "react";
import "./Home.css";
import { useForm } from "react-hook-form";
import Input, { InputProps } from "../components/Input";

const Home: React.FC = () =&gt; {
  const { control, handleSubmit } = useForm();
  
  const formFields: InputProps[] = [
    {
      name: "email",
      component: &lt;IonInput type="email" /&gt;,
      label: "Email",
    },
    {
      name: "fullName",
      label: "Full Name",
    },
    {
      name: "password",
      component: &lt;IonInput type="password" clearOnEdit={false} /&gt;,
      label: "Password",
    },
  ];

  const registerUser = (data) =&gt; {
    console.log("creating a new user account with: ", data);
  };

  return (
    &lt;IonPage&gt;
      &lt;IonContent&gt;
        &lt;div className="ion-padding"&gt;
          &lt;IonText color="muted"&gt;
            &lt;h2&gt;Create Account&lt;/h2&gt;
          &lt;/IonText&gt;
          &lt;form onSubmit={handleSubmit(registerUser)}&gt;
            {formFields.map((field, index) =&gt; (
              &lt;Input {...field} control={control} key={index} /&gt;
            ))}
            &lt;IonItem&gt;
              &lt;IonLabel&gt;I agree to the terms of service&lt;/IonLabel&gt;
              &lt;IonCheckbox slot="start" /&gt;
            &lt;/IonItem&gt;
            &lt;IonButton expand="block" type="submit" className="ion-margin-top"&gt;
              Register
            &lt;/IonButton&gt;
          &lt;/form&gt;
        &lt;/div&gt;
      &lt;/IonContent&gt;
    &lt;/IonPage&gt;
  );
};

export default Home;</code></pre>
</div>
 
With your setup so far, you have an array of your form’s input fields (`name` is the only required property), with each field rendered using the `Input` component from earlier. You can take this even further and have your field data in a JSON file, keeping the code within your components with forms clean. At this point, your app (running at https://localhost:8100 with the `ionic serve` command) should look like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd2af0d2-8129-4107-894d-6eda4f26f392/fig-03-registration-form-ios.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0b47e63-0f94-4bec-bbd2-1ca2af58294d/03-registration-form-ios.png" sizes="100vw" caption="Registration form page (iOS) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd2af0d2-8129-4107-894d-6eda4f26f392/fig-03-registration-form-ios.png'>Large preview</a>)" alt="" >}}

{{% ad-panel-leaderboard %}}

## How About Field Validation?

You might have noticed that our form’s input fields do not have any validation logic yet. If this were an app intended for real-world use, that could lead to many undesirable effects unless your API is set up to validate incoming data. By the way, your API must always validate incoming data.

RHF comes with validation which aligns with the HTML standard for form validation built-in. This works great for simple validation like making a field required or setting minimum and maximum field lengths. If you want to use [complex validation logic](https://haacked.com/archive/2007/08/21/i-knew-how-to-validate-an-email-address-until-i.aspx/), I would recommend using [Yup](https://github.com/jquense/yup). While you can use any object schema validation library, RHF supports Yup out of the box.

Run the following command to install the library (and typings):

<pre><code class="language-bash">yarn add yup @types/yup</code></pre>

Next, add this to your component’s imports:

<pre><code class="language-javascript">import { object, string } from 'yup';

const Home: React.FC = () =&gt; { ... }</code></pre>

Then, add the following code at the top of your component:

<pre><code class="language-javascript">const Home: React.FC = () =&gt; {
  const validationSchema = object().shape({
    email: string().required().email(),
    fullName: string().required().min(5).max(32),
    password: string().required().min(8),
  });
  // ...
}</code></pre>

Here, we’ve created an object schema and added validation rules to each property using `yup`. The names in the object must match with names in your form’s input tags otherwise your rules won’t be triggered.

Finally, update your `useForm()` hook to use the schema we’ve defined by setting the `validationSchema` property like this:

<pre><code class="language-javascript">const { control, handleSubmit } = useForm({
  validationSchema,
});</code></pre>
    
Now, when you click on the submit button the `handleSubmit` handler isn’t invoked and the form data isn’t submitted. While this is exactly what we wanted, it looks like there is no way for the user to know what’s happening. Let’s fix this by showing text hints when a field isn’t filled correctly.

First, update the `Input` component to look like the following:

<div class="break-out">

<pre><code class="language-javascript">import React, { FC } from "react";
import { IonItem, IonLabel, IonInput, IonText } from "@ionic/react";
import { Controller, Control, NestDataObject, FieldError } from "react-hook-form";

export interface InputProps {
  name: string;
  control?: Control;
  label?: string;
  component?: JSX.Element;
  errors?: NestDataObject&lt;Record&lt;string, any&gt;, FieldError&gt;;
}

const Input: FC&lt;InputProps&gt; = ({
  name,
  control,
  component,
  label,
  errors,
}) =&gt; {
  return (
    &lt;&gt;
      &lt;IonItem&gt;
        {label && &lt;IonLabel position="floating"&gt;{label}&lt;/IonLabel&gt;}
        &lt;Controller
          as={component ?? &lt;IonInput /&gt;}
          name={name}
          control={control}
          onChangeName="onIonChange"
        /&gt;
      &lt;/IonItem&gt;
      {errors && errors[name] && (
        &lt;IonText color="danger" className="ion-padding-start"&gt;
          &lt;small&gt;{errors[name].message}&lt;/small&gt;
        &lt;/IonText&gt;
      )}
    &lt;/&gt;
  );
};

export default Input;</code></pre>
</div>

Here, we’ve updated our component to receive an extra optional property which is the error object from RHF, and we display an error message in the returned input field whenever there is an error. One last thing, add the errors object to your destructured object and update the component in your loop:

<div class="break-out">

<pre><code class="language-javascript">const { control, handleSubmit, errors } = useForm({
  validationSchema,
});</code></pre>
</div>

<div class="break-out">

<pre><code class="language-javascript">  {formFields.map((field, index) =&gt; (
    &lt;Input {...field} control={control} key={index} errors={errors} /&gt;
  ))}</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c33ad116-4f73-4633-9d0b-648c1dc6e0e7/fig-04-registration-form-with-error-messages-ios.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a325ed62-f12e-43f0-886d-d35899c96f9b/04-registration-form-with-error-messages-ios.png" sizes="100vw" caption="Registration form with error messages (iOS) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c33ad116-4f73-4633-9d0b-648c1dc6e0e7/fig-04-registration-form-with-error-messages-ios.png'>Large preview</a>)" alt="" >}}

Your forms now provide visual cues when a user isn’t doing something right. Yup allows you to change the error message. You can do this by passing a string to the validation method you’re using. For email, as an example, you can do the following:

<pre><code class="language-javascript">{
  email: string()
    .email('Please provide a valid email address')
    .required('This is a required field'),
}</code></pre>

{{% ad-panel-leaderboard %}}

## Improving Accessibility

Ionic’s components are usually wrappers over the corresponding native element, meaning that they accept most &mdash; if not all &mdash; of that element’s existing attributes. You can improve your input fields and make them more accessible to visually impaired users by setting ARIA attributes with relevant text.

To continue with our example registration form, open the Input.tsx file and make the following changes:

<div class="break-out">

<pre><code class="language-javascript">import React, { FC } from "react";
import { IonItem, IonLabel, IonInput, IonText } from "@ionic/react";
import { Controller, Control, NestDataObject, FieldError } from "react-hook-form";

export interface InputProps {
  name: string;
  control?: Control;
  label?: string;
  component?: JSX.Element;
  errors?: NestDataObject&lt;Record&lt;string, any&gt;, FieldError&gt;;
}

const Input: FC&lt;InputProps&gt; = ({
  name,
  control,
  component,
  label,
  errors,
}) =&gt; {
  return (
    &lt;&gt;
      &lt;IonItem&gt;
        {label && &lt;IonLabel position="floating"&gt;{label}&lt;/IonLabel&gt;}
        &lt;Controller
          as={
            component ?? (
              &lt;IonInput
                aria-invalid={errors && errors[name] ? "true" : "false"}
                aria-describedby={`${name}Error`}
              /&gt;
            )
          }
          name={name}
          control={control}
          onChangeName="onIonChange"
        /&gt;
      &lt;/IonItem&gt;
      {errors && errors[name] && (
        &lt;IonText color="danger" className="ion-padding-start"&gt;
          &lt;small&gt;
            &lt;span role="alert" id={`${name}Error`}&gt;
              {errors[name].message}
            &lt;/span&gt;
          &lt;/small&gt;
        &lt;/IonText&gt;
      )}
    &lt;/&gt;
  );
};

export default Input;</code></pre>
</div>

The default `IonInput` component we’re passing to `Controller` now includes an `aria-invalid` attribute to indicate whether the field has an error, and an `aria-describedby` attribute to point to the corresponding error message. The error message is now wrapped with a `span` having an ARIA role set to “error”. Now, when your field has an error, a screen reader will highlight that field and read out the error message.

- You’ll find the GitHub repo over [here](https://github.com/smashingmagazine/ionic-react-forms).

## Conclusion

Congratulations! You have learned how to build and validate forms when building cross-platform apps using Ionic. You’ve also seen how easy it is to make your input fields accessible to users with a visual impairment. Hopefully, this tutorial provides a solid platform that you can use when building forms in your Ionic React apps. There are other components for building forms (such as select and radios) that we didn’t explore in this tutorial, but you can find and read more about them in the official docs.

### References

- [Ionic Framework Docs](https://ionicframework.com/docs/)
- [React Hook Form](https://react-hook-form.com/)
- [Yup Docs](https://github.com/jquense/yup)
- [Phil Haack on Validating Email Addresses](https://haacked.com/archive/2007/08/21/i-knew-how-to-validate-an-email-address-until-i.aspx/)
- [Accessibility on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)

{{< signature "ks, ra, yk, il" >}}
