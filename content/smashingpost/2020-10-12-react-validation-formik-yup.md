---
title: 'React Form Validation With Formik And Yup'
slug: react-validation-formik-yup
author: nefe-emadamerho-atori
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0911969f-bf77-4329-9dde-677274a95b1f/react-validation-formik-yup.png
date: 2020-10-12T10:30:00.000Z
summary: >-
  Forms are an integral part of how users interact with our websites and web applications. Validating the data the user passes through the form is a critical aspect of our jobs as web developers. However, it doesn’t have to be a pain-staking process. In this article, we’ll learn how Formik handles the state of the form data, validates the data, and handles form submission.
description: >-
  Forms are an integral part of how users interact with our websites and web applications. Validating the data the user passes through the form is a critical aspect of our jobs as web developers. However, it doesn’t have to be a pain-staking process. In this article, we’ll learn how Formik handles the state of the form data, validates the data, and handles form submission.
categories:
  - Forms
  - React
  - Tools
---

As developers, it is our job to ensure that when users interact with the forms we set up, the data they send across is in the form we expect.

In this article, we will learn how to handle form validation and track the state of forms without the aid of a form library. 
Next, we will see how the Formik library works. We’ll learn how it can be used incrementally with HTML input fields and custom validation rules. Then we will set up form validation using Yup and Formik's custom components and understand how Yup works well with Formik in handling Form validation. We will implement these form validation methods to validate a simple sign up form I have set up.

***Note:*** *This article requires a basic understanding of React.*

## Form Validation In React

On its own, React is powerful enough for us to be able to set up custom validation for our forms. Let’s see how to do that. We’ll start by creating our form component with initial state values. The following [sandbox](https://codesandbox.io/s/custom-validation-no-library-83fz6?fontsize=14&hidenavigation=1&theme=dark) holds the code for our form:

<iframe loading="lazy" src="https://codesandbox.io/embed/custom-validation-no-library-83fz6?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="custom-validation-no-library"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

*Form validation without the use of a library*

<pre><code class="language-javascript">const Form = () =&gt; {
  const intialValues = { email: "", password: "" };
  const [formValues, setFormValues] = useState(intialValues);
  const [formErrors, setFormErrors] = useState({});
  const [isSubmitting, setIsSubmitting] = useState(false);
}</code></pre>
    
With the `useState` hook, we set state variables for the `formValues`, `formErrors` and `isSubmitting`. 

- The `formValues` variable holds the data the user puts into the input fields.
- The `formErrors` variable holds the errors for each input field.
- The `isSubmitting` variable is a boolean that tracks if the form is being submitted or not. This will be `true` only when there are no errors in the form.  

<pre><code class="language-javascript">const submitForm = () =&gt; {
    console.log(formValues);
  };

 const handleChange = (e) =&gt; {
    const { name, value } = e.target;
    setFormValues({ ...formValues, [name]: value });
  };

const handleSubmit = (e) =&gt; {
    e.preventDefault();
    setFormErrors(validate(formValues));
    setIsSubmitting(true);
  };

const validate = (values) =&gt; {
    let errors = {};
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/i;
    if (!values.email) {
      errors.email = "Cannot be blank";
    } else if (!regex.test(values.email)) {
      errors.email = "Invalid email format";
    }
    if (!values.password) {
      errors.password = "Cannot be blank";
    } else if (values.password.length &lt; 4) {
      errors.password = "Password must be more than 4 characters";
    }
    return errors;
  };

useEffect(() =&gt; {
    if (Object.keys(formErrors).length === 0 && isSubmitting) {
      submitForm();
    }
  }, [formErrors]);</code></pre>

Here, we have 4 form handlers and a `useEffect` set up to handle the functionality of our form.

- `handleChange`  
This keeps the inputs in sync with the `formValues` state and updates the state as the user types.
- `validate`  
We pass in the `formValues` object as a argument to this function, then based on the `email` and `password` meeting the validation tests, the `errors` object is populated and returned.
- `handleSubmit`  
Whenever the form is submitted, the `formErrors` state variable is populated with whatever errors may exist using the `setFormErrors(validate(formValues))` method.
- `useEffect`  
Here, we check if the `formErrors` object is empty, *and* if `isSubmitting` is `true`. If this check holds true, then the `submitForm()` helper is called. It has single dependency, which is the `formErrors` object. This means it only runs when the `formErrors` object changes.
- `submitForm`: this handles the submission of the form data.

<pre><code class="language-javascript">return (
    &lt;div className="container"&gt;
      &lt;h1&gt;Sign in to continue&lt;/h1&gt;
      {Object.keys(formErrors).length === 0 && isSubmitting && (
        &lt;span className="success-msg"&gt;Signed in successfully&lt;/span&gt;
      )}
      &lt;form onSubmit={handleSubmit} noValidate&gt;
        &lt;div className="form-row"&gt;
          &lt;label htmlFor="email">Email&lt;/label&gt;
          &lt;input
            type="email"
            name="email"
            id="email"
            value={formValues.email}
            onChange={handleChange}
            className={formErrors.email && "input-error"}
          /&gt;
          {formErrors.email && (
            &lt;span className="error"&gt;{formErrors.email}&lt;/span&gt;
          )}
        &lt;/div&gt;
        &lt;div className="form-row"&gt;
          &lt;label htmlFor="password">Password&lt;/label&gt;
          &lt;input
            type="password"
            name="password"
            id="password"
            value={formValues.password}
            onChange={handleChange}
            className={formErrors.password && "input-error"}
          /&gt;
          {formErrors.password && (
            &lt;span className="error"&gt;{formErrors.password}&lt;/span&gt;
          )}
        &lt;/div&gt;
        &lt;button type="submit"&gt;Sign In&lt;/button&gt;
      &lt;/form&gt;
    &lt;/div&gt;
  );</code></pre>

Here, we pass in the `handleChange` helper functions to the inputs’ `onChange` attribute. We link the value of the inputs to the `formValues` object, making them controlled inputs. [From the React docs](https://reactjs.org/docs/forms.html#controlled-components), *controlled inputs are inputs whose values are controlled by React*. An input-error style is applied if there are any errors related to that specific input field. An error message is conditionally displayed beneath each input if there are any errors related to that specific input field. Finally, we check if there are any errors in the errors object *and* if `isSubmitting` is true. If these conditions hold true, then we display a message notifying the user that they signed in successfully.

With this, we have a fully functional and validated form set up without the aid of a library. However, a form library like Formik with the aid of Yup can simplify the complexities of handling forms for us.

{{% feature-panel %}}

## What Are Formik And Yup?

[Right from the docs](https://formik.org/docs/overview):

<blockquote>“Formik is a small library that helps you with the 3 most annoying parts in handling forms:<br /><ol><li>Getting values in and out of form state.</li><li>Validation and error messages</li><li>Handling form submission.</li></ol></blockquote>

Formik is a flexible library. It allows you to decide when and how much you want to use it. We can control how much functionality of the Formik library we use. It can be used with HTML input fields and custom validation rules, or Yup and the custom components it provides. Formik makes form validation easy! When paired with Yup, they abstract all the complexities that surround handling forms in React. 

[Yup](https://github.com/jquense/yup) is a JavaScript object schema validator. While it has many powerful features, we’ll focus on how it helps us create custom validation rules so we don’t have to. This is a sample Yup object schema for a sign-up form. We’ll go into Yup and how it works in depth later in the article.

<pre><code class="language-javascript">const SignUpSchema = Yup.object().shape({
  firstName: Yup.string()
    .min(2, "Too Short!")
    .max(50, "Too Long!")
    .required("Firstname is required"),

  lastName: Yup.string()
    .min(2, "Too Short!")
    .max(50, "Too Long!")
    .required("Lastname is required"),

  phoneNumber: Yup.string()
    .required("Phone number is required")
    .matches(
/^([0]{1}|\+?[234]{3})([7-9]{1})([0|1]{1})([\d]{1})([\d]{7})$/g,
      "Invalid phone number"
    ),

  email: Yup.string().email().required("Email is required"),

  password: Yup.string()
    .required("Password is required")
    .min(6, "Password is too short - should be 6 chars minimum"),
});</code></pre>
    
## Formik, HTML Input Fields And Custom Validation Rules

The following [sandbox](https://codesandbox.io/s/formik-html-input-fields-and-custom-validation-rules-nw48z) holds the code for this form set up:

<iframe loading="lazy" src="https://codesandbox.io/embed/formik-html-input-fields-and-custom-validation-rules-nw48z?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Formik, HTML Input Fields and Custom Validation Rules"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

The first thing we have to do is [install Formik](https://formik.org/docs/overview#installation).

<pre><code class="language-bash">npm i formik</code></pre>
   
Then we can go ahead to import it in the file where we’ll make use of it.

<pre><code class="language-javascript">import { Formik } from "formik";</code></pre>

Before creating the component, we need to create an `initialValues` and `validate` object which we’ll pass as props to the Formik component when we set it up. `initialValues` and `validate` are code snippets, not normal words.

The decision to do this outside the component is not a technical one, but rather for readability of our code.

<pre><code class="language-javascript">const initialValues = {
  email: "",
  password: ""
};</code></pre>

`initialValues`: is an object that describes the initial values of the respective form fields. The name given to each key in the `initialValues` must correspond with the value of the name of the input field we want Formik to watch.

<pre><code class="language-javascript">const validate = (values) =&gt; {
  let errors = {};
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/i;
  if (!values.email) {
    errors.email = "Email is required";
  } else if (!regex.test(values.email)) {
    errors.email = "Invalid Email";
  }
  if (!values.password) {
    errors.password = "Password is required";
  } else if (values.password.length &lt; 4) {
    errors.password = "Password too short";
  }
  return errors;
};</code></pre>

`validate`: this accepts a function that handles the form validation. The function accepts an object in the form of data values as an argument and validates each property in the object based on the rules defined. Each key in the values object must correspond with the name of the input field.

<pre><code class="language-javascript">const submitForm = (values) =&gt; {
  console.log(values);
};</code></pre>

`onSubmit`: This handles what happens after the user submits. The onSubmit prop takes a callback function that will only run when there are no errors, meaning the user inputs are valid.

<div class="break-out">

<pre><code class="language-javascript">const SignInForm = () =&gt; {
  return (
    &lt;Formik
      initialValues={initialValues}
      validate={validate}
      onSubmit={submitForm}
    &gt;
      {(formik) =&gt; {
        const {
          values,
          handleChange,
          handleSubmit,
          errors,
          touched,
          handleBlur,
          isValid,
          dirty
        } = formik;
        return (
            &lt;div className="container"&gt;
              &lt;h1&gt;Sign in to continue&lt;/h1&gt;
              &lt;form onSubmit={handleSubmit}&gt;
                &lt;div className="form-row"&gt;
                  &lt;label htmlFor="email"&gt;Email&lt;/label&gt;
                  &lt;input
                    type="email"
                    name="email"
                    id="email"
                    value={values.email}
                    onChange={handleChange}
                    onBlur={handleBlur}
                    className={errors.email && touched.email ? 
                    "input-error" : null}
                  /&gt;
                  {errors.email && touched.email && (
                    &lt;span className="error"&gt;{errors.email}&lt;/span&gt;
                  )}
                &lt;/div&gt;

                &lt;div className="form-row"&gt;
                  &lt;label htmlFor="password"&gt;Password&lt;/label&gt;
                  &lt;input
                    type="password"
                    name="password"
                    id="password"
                    value={values.password}
                    onChange={handleChange}
                    onBlur={handleBlur}
                    className={errors.password && touched.password ? 
                     "input-error" : null}
                  /&gt;
                  {errors.password && touched.password && (
                    &lt;span className="error"&gt;{errors.password}&lt;/span&gt;
                  )}
                &lt;/div&gt;

                &lt;button
                  type="submit"
                  className={dirty && isValid ? "" : "disabled-btn"}
                  disabled={!(dirty && isValid)}&gt;
                  Sign In
                &lt;/button&gt;
              &lt;/form&gt;
            &lt;/div&gt;
        );
      }}
    &lt;/Formik&gt;
  );
};</code></pre>
</div>

We pass in the `initialValues` object, and the `submitForm` and `validate` functions we defined earlier into Formik’s `initialValues`, `onSubmit` and `validate` props respectively.

{{% ad-panel-leaderboard %}}

Using the render props pattern, we have access to even more props the Formik API provides.

1. `values`  
This holds the values of the user inputs.
2. `handleChange`  
This is the input change event handler. It is passed to the input field `<input onChange={handleChange}>`. It handles the changes of the user inputs.
3. `handleSubmit`  
The form submission handler. It is passed into the form `<form onSubmit={props.handleSubmit}>`. This fires the function passed into the `onSubmit` prop whenever the form is submitted.
4. `errors`  
This object holds the validation errors that correspond to each input field, and is populated with the definitions we passed into the Yup object schema.
5. `touched`  
This is an object that watches if a form field has been touched. Each key corresponds to the name of the input elements and has a boolean value.
6. `handleBlur`  
This is the `onBlur` event handler, and it is passed to the input field `<input onBlur={handleBlur} />`. When the user removes focus from an input, this function is called. Without it, if there are any errors in the input when it loses focus, the errors will only display when the user tries to submit.
7. `isValid`  
Returns `true` if there are no errors (i.e. the `errors` object is empty) and `false` otherwise.
8. `dirty`  
This prop checks if our form has been touched or not. We can use this to disable our submit button when the form loads initially. 

When the form is submitted, Formik checks if there are any errors in the `errors` object. If there are, it aborts the submission and displays the errors. To display the span using HTML inputs, we conditionally render and style the error message of each respective input field if the field has been touched and there are errors for that field.

<pre><code class="language-javascript">&lt;button
  type="submit"
  className={!(dirty && isValid) ? "disabled-btn" : ""}
  disabled={!(dirty && isValid)}&gt;
      Sign In
&lt;/button&gt;</code></pre>
    
Also, we can add a visual cue to the button. The button is conditionally styled and disable it if there are errors in the `errors` object using the `isValid` and the `dirty` props. 

{{% ad-panel-leaderboard %}}

## Validation Using Formik’s Components And Yup

[This sandbox](https://codesandbox.io/s/formik-formik-elements-84tf0) holds the final code for this setup.

<pre><code class="language-javascript">npm i yup
import { Formik, Form, Field, ErrorMessage } from "formik";
import * as Yup from "yup";</code></pre>    

We install Yup, import the `Field`, `Form`, and the `ErrorMessage` components from Formik.

Formik makes form validation easy! When paired with Yup, they abstract all the complexities that surround handling forms in React. With that we can then go ahead to create the schema we’ll be using for the sign in form using Yup. Instead of creating custom validations for each possible input field, which can be tedious, depending on the number of fields there are, we can leave that to Yup to handle. 

<pre><code class="language-javascript">const SignInSchema = Yup.object().shape({
  email: Yup.string().email().required("Email is required"),

  password: Yup.string()
    .required("Password is required")
    .min(4, "Password is too short - should be 4 chars minimum"),
});</code></pre>

Yup works similarly to how we define `propTypes` in React. We created an object schema with Yup’s `object` function. We define the shape of the validation object schema and pass it into Yup’s `shape()` method. The `required()` method. This method takes a string as an argument, and this string will be the error message. that displays whenever a required field is left blank. 

This schema has two properties:

- An `email` property that is a string type and is required.
- A `password` property that is of number type but is not required.

We can chain validation is Yup as seen above. The properties of  the schema object match the name of the input fields. [The docs](https://github.com/jquense/yup#string) go into the different validation methods available in Yup.

<div class="break-out">

<pre><code class="language-javascript">const SignInForm = () =&gt; {
  return (
    &lt;Formik
      initialValues={initialValues}
      validationSchema={signInSchema}
      onSubmit={(values) =&gt; {
        console.log(values);
      }}
    &gt;
      {(formik) =&gt; {
        const { errors, touched, isValid, dirty } = formik;
        return (
          &lt;div className="container"&gt;
            &lt;h1&gt;Sign in to continue&lt;/h1&gt;
            &lt;Form&gt;
              &lt;div className="form-row"&gt;
                &lt;label htmlFor="email"&gt;Email&lt;/label&gt;
                &lt;Field
                  type="email"
                  name="email"
                  id="email"
                  className={errors.email && touched.email ? 
                  "input-error" : null}
                /&gt;
                &lt;ErrorMessage name="email" component="span" className="error" /&gt;
              &lt;/div&gt;

              &lt;div className="form-row"&gt;
                &lt;label htmlFor="password"&gt;Password&lt;/label&gt;
                &lt;Field
                  type="password"
                  name="password"
                  id="password"
                  className={errors.password && touched.password ? 
                  "input-error" : null}
                /&gt;
                &lt;ErrorMessage
                  name="password"
                  component="span"
                  className="error"
                /&gt;
              &lt;/div&gt;

              &lt;button
                type="submit"
                className={!(dirty && isValid) ? "disabled-btn" : ""}
                disabled={!(dirty && isValid)}
              &gt;
                Sign In
              &lt;/button&gt;
            &lt;/Form&gt;
          &lt;/div&gt;
        );
      }}
    &lt;/Formik&gt;
  );
};</code></pre>
</div>

While using HTML input fields get the job done, Formik’s custom components make things even easier for us, and reduce the amount of code we have to write! What are these custom components Formik provides us?

1. `Formik`  
We’ve been using this for a while now. This is required for the other components to be usable.
2. `Form`  
A wrapper that wraps the HTML `<form/>` element. It automatically links the `onSubmit` method to the form’s submit event.
3. `Field`  
In the background, this automatically links the form input’s `onChange`, `onBlur` and `value` attributes to Formik’s `handleChange`, `handleBlur`, and `values` object respectively. It uses the name prop to match up with the state and automatically keeps the state in sync with the input value. With this component, we can decide to display it as an input field we want using it’s `as` property. For example, will render a `textarea`. By default, it renders an HTML input field.
4. `ErrorMessage`  
It handles rendering the error message for its respective field based on the value given to the name prop, which corresponds to the `<Field />`’s name prop. It displays the error message if the field has been visited and the error exists. By default, it renders a string is the `component` prop is not specified.

We pass the `signInSchema` into Formik using the `validationSchema` prop. The Formik team loves the Yup validation library so they created a specific prop for Yup called `validationSchema` which transforms errors into objects and matches against their values and touched functions.

## Conclusion

Users do not know or care how you handle form validation. However, for you the developer, it should be as painless a process as possible, and I believe Formik stands out as a solid choice in that regard.

We have successfully looked at some of the options available to us when validating forms in React. We have seen how Formik can be used incrementally, and how it pairs well with Yup in handling form validation. 

### Resources

- [Formik Docs](https://formik.org/docs/overview)
- [Yup Docs](https://github.com/jquense/yup#usage)
- [Validation with Yup](https://www.techzaion.com/validation-with-yup)

{{< signature "ks, ra, yk, il" >}}
