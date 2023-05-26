---
title: 'Creating Your Own React Validation Library: The Features (Part 2)'
slug: react-validation-library-features-part2
author: kristofer-giltvedt-selbekk
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc742d1-a118-405e-abdc-f96870706f72/react-library-article-sharing-card.png
date: 2019-05-23T13:00:16+02:00
summary: >-
  In Kristofer’s previous article, he explained how the basic parts of a validation library can be implemented. While the next part will focus on improving the developer experience, today’s article will focus on adding more features to what was created in [Part 1](https://www.smashingmagazine.com/2019/05/react-validation-library-basics-part1/).
description: >-
  In Kristofer’s previous article, he explained how the basic parts of a validation library can be implemented. This article will focus on adding even more features to what had previously been created.
categories:
  - React
  - JavaScript
  - Testing
  - Forms
---
Implementing a validation library isn’t all that hard. Neither is adding all of those extra features that make *your* validation library much better than the rest.

This article will continue implementing the validation library we started implementing in the [previous part](https://www.smashingmagazine.com/2019/05/react-validation-library-basics-part1/) of this article series. These are the features that are going to take us from a simple proof of concept to an actual usable library!

- Part 1: [The Basics](https://www.smashingmagazine.com/2019/05/react-validation-library-basics-part1/)
- **Part 2: The Features**
- Part 3: [The Experience](https://www.smashingmagazine.com/2019/05/react-validation-library-developer-experience-part3)

## Only Show Validation On Submit

Since we’re validating on all change events, we’re showing the user error messages way too early for a good user experience. There are a few ways we can mitigate this.

The first solution is simply providing the `submitted` flag as a returned property of the `useValidation` hook. This way, we can check whether or not the form is submitted before showing an error message. The downside here is that our "show error code" gets a bit longer:

<pre><code class="language-javascript">&lt;label&gt;
  Username
  &lt;br /&gt;
  &lt;input {...getFieldProps('username')} /&gt;
  {submitted && errors.username && (
    &lt;div className="error"&gt;{errors.username}&lt;/div&gt;
  )}
&lt;/label&gt;
</code></pre>

Another approach is to provide a second set of errors (let’s call them `submittedErrors`), which is an empty object if `submitted` is false, and the `errors` object if it’s true. We can implement it like this:

<pre><code class="language-javascript">const useValidation = config => {
  // as before
  return {
    errors: state.errors,
    submittedErrors: state.submitted ? state.errors : {},
  };
}
</code></pre>

This way, we can simply destructure out the type of errors that we want to show. We could, of course, do this at the call site as well &mdash; but by providing it here, we’re implementing it once instead of inside all consumers.

- [See CodeSandbox demo](https://codesandbox.io/embed/k951np8915?fontsize=14) showing how `submittedErrors` can be used.

{{% feature-panel %}}

## Show Error Messages On-Blur

A lot of people want to be shown an error once they leave a certain field. We can add support for this, by tracking which fields have been "blurred" (navigated away from), and returning an object `blurredErrors`, similar to the `submittedErrors` above.

The implementation requires us to handle a new action type &mdash; `blur`, which will be updating a new state object called `blurred`:

<pre><code class="language-javascript">const initialState = {
  values: {},
  errors: {},
  blurred: {},
  submitted: false,
};

function validationReducer(state, action) {
  switch (action.type) {
    // as before
    case 'blur':
      const blurred = { 
        ...state.blurred, 
        [action.payload]: true 
      }; 
      return { ...state, blurred };
    default:
      throw new Error('Unknown action type');
  }
}
</code></pre>


When we dispatch the `blur` action, we create a new property in the `blurred` state object with the field name as a key, indicating that <em>that</em> field has been blurred.

The next step is adding an `onBlur` prop to our `getFieldProps` function, that dispatches this action when applicable:

<pre><code class="language-javascript">getFieldProps: fieldName => ({
  // as before
  onBlur: () => {
    dispatch({ type: 'blur', payload: fieldName });
  },
}),
</code></pre>

Finally, we need to provide the `blurredErrors` from our `useValidation` hook so that we can show the errors only when needed.

<div class="break-out">

<pre><code class="language-javascript">const blurredErrors = useMemo(() => {
    const returnValue = {};
    for (let fieldName in state.errors) {
      returnValue[fieldName] = state.blurred[fieldName]
        ? state.errors[fieldName]
        : null;
    }
    return returnValue;
  }, [state.errors, state.blurred]);
return {
  // as before
  blurredErrors,
};
</code></pre>
</div>

Here, we create a <a href="https://en.wikipedia.org/wiki/Memoization">memoized function</a> that figures out which errors to show based on whether or not the field has been blurred. We recalculate this set of errors whenever the errors or blurred objects change. You can read more about the `useMemo` hook in the <a href="https://reactjs.org/docs/hooks-reference.html#usememo">documentation</a>.

- [See CodeSandbox demo](https://codesandbox.io/embed/6zm3zj9qlk?fontsize=14)

## Time For A Tiny Refactor

Our `useValidation` component is now returning three sets of errors &mdash; most of which will look the same at some point in time. Instead of going down this route, we’re going to let the user specify in the config when they want the errors in their form to show up.

Our new option &mdash; `showErrors` &mdash; will accept either "submit" (the default), "always" or "blur". We can add more options later, if we need to.

<div class="break-out">

<pre><code class="language-javascript">function getErrors(state, config) {
  if (config.showErrors === 'always') {
    return state.errors;
  }
  if (config.showErrors === 'blur') {
    return Object.entries(state.blurred)
      .filter(([, blurred]) => blurred)
      .reduce((acc, [name]) => ({ ...acc, [name]: state.errors[name] }), {});
  }
  return state.submitted ? state.errors : {};
}
const useValidation = config => {
  // as before
  const errors = useMemo(
    () => getErrors(state, config), 
    [state, config]
  );

  return {
    errors,
    // as before
  };
};
</code></pre>
</div>

Since the error handling code started to take most of our space, we’re refactoring it out into its own function. If you don’t follow the `Object.entries` and `.reduce` stuff &mdash; that’s fine &mdash; it’s a rewrite of the `for...in` code in the last section.

If we required onBlur or instant validation, we could specify the `showError` prop in our `useValidation` configuration object.

<div class="break-out">

<pre><code class="language-javascript">const config = {
  // as before
  showErrors: 'blur',
};
const { getFormProps, getFieldProps, errors } = useValidation(config);
// errors would now only include the ones that have been blurred
</code></pre>
</div>

- [See CodeSandbox demo](https://codesandbox.io/embed/w216oz1x2w?fontsize=14)

#### Note On Assumptions

<blockquote>“Note that I'm now assuming that each form will want to show errors the same way (always on submit, always on blur, etc). That might be true for most applications, but probably not for all. Being aware of your assumptions is a <strong>huge</strong> part of creating your API.”</blockquote>

{{% ad-panel-leaderboard %}}

## Allow For Cross-Validation

A really powerful feature of a validation library is to allow for cross-validation &mdash; that is, to base one field’s validation on another field’s value.


To allow this, we need to make our custom hook accept a function instead of an object. This function will be called with the current field values. Implementing it is actually only three lines of code!

<pre><code class="language-javascript">function useValidation(config) {
  const [state, dispatch] = useReducer(...);
  if (typeof config === 'function') {
    config = config(state.values);
  }
}
</code></pre>

To use this feature, we can simply pass a function that returns the configuration object to `useValidation`:

<div class="break-out">

<pre><code class="language-javascript">const { getFieldProps } = useValidation(fields => ({ 
  password: {
    isRequired: { message: 'Please fill out the password' },
  },
  repeatPassword: {
    isRequired: { message: 'Please fill out the password one more time' },
    isEqual: { value: fields.password, message: 'Your passwords don\’t match' }
  }
}));
</code></pre>
</div>

Here, we use the value of `fields.password` to make sure two password fields contain the same input (which is terrible user experience, but that’s for another blog post).

- [See CodeSandbox demo](https://codesandbox.io/embed/0x5pomny3n?fontsize=14) that doesn’t let the username and the password be the same value.

## Add Some Accessibility Wins

A neat thing to do when you’re in charge of the props of a field is to add the correct aria-tags by default. This will help screen readers with explaining your form.

A very simple improvement is to add `aria-invalid="true"` if the field has an error. Let’s implement that:

<pre><code class="language-javascript">const useValidation = config => {
  // as before
  return {
    // as before
    getFieldProps: fieldName => ({
      // as before
      'aria-invalid': String(!!errors[fieldName]),
    }),
  }
};
</code></pre>

That’s <em>one</em> added line of code, and a <strong>much</strong> better user experience for screen reader users.

You might wonder about why we write `String(!!state.errors[fieldName])`? `state.errors[fieldName]` is a string, and the double negation operator gives us a boolean (and not just a truthy or falsy value). However, the `aria-invalid` property should be a string (it can also read "grammar" or "spelling", in addition to "true" or "false"), so we need to coerce that boolean into its string equivalent.

There are still a few more tweaks we could do to improve accessibility, but this seems like a fair start.

{{% ad-panel-leaderboard %}}

### Shorthand Validation Message Syntax

Most of the validators in the `calidators` package (and most other validators, I assume) only require an error message. Wouldn’t it be nice if we could just pass that string instead of an object with a `message` property containing that string?

Let’s implement that in our `validateField` function:

<div class="break-out">

<pre><code class="language-javascript">function validateField(fieldValue = '', fieldConfig, allFieldValues) {
  for (let validatorName in fieldConfig) {
    let validatorConfig = fieldConfig[validatorName];
    if (typeof validatorConfig === ’string') {
      validatorConfig = { message: validatorConfig };
    }
    const configuredValidator = validators[validatorName](validatorConfig);
    const errorMessage = configuredValidator(fieldValue);

    if (errorMessage) {
      return errorMessage;
    }
  }
  return null;
}
</code></pre>
</div>

This way, we can rewrite our validation config like so:

<pre><code class="language-javascript">const config = {
  username: {
    isRequired: 'The username is required',
    isEmail: 'The username should be a valid email address',
  },
};
</code></pre>

Much cleaner!

## Initial Field Values

Sometimes, we need to validate a form that’s already filled out. Our custom hook doesn’t support that yet &mdash; so let’s get to it!

Initial field values will be specified in the config for each field, in the property `initialValue`. If it’s not specified, it defaults to an empty string.

We’re going to create a function `getInitialState`, which will create the initial state of our reducer for us.

<div class="break-out">

<pre><code class="language-javascript">function getInitialState(config) {
  if (typeof config === 'function') {
    config = config({});
  }
  const initialValues = {};
  const initialBlurred = {};
  for (let fieldName in config.fields) {
    initialValues[fieldName] = config.fields[fieldName].initialValue || '';
    initialBlurred[fieldName] = false;
  }
  const initialErrors = validateFields(initialValues, config.fields);
  return {
    values: initialValues,
    errors: initialErrors,
    blurred: initialBlurred,
    submitted: false,
  };
}
</code></pre>
</div>

We go through all fields, check if they have an `initialValue` property, and set the initial value accordingly. Then we run those initial values through the validators and calculate the initial errors as well. We return the initial state object, which can then be passed to our `useReducer` hook.

Since we’re introducing a non-validator prop into the fields config, we need to skip it when we validate our fields. To do that, we change our `validateField` function:

<pre><code class="language-javascript">function validateField(fieldValue = '', fieldConfig) {
  const specialProps = ['initialValue'];
  for (let validatorName in fieldConfig) {
    if (specialProps.includes(validatorName)) {
      continue;
    }
    // as before
  }
}
</code></pre>

As we keep on adding more features like this, we can add them to our `specialProps` array.

- [See CodeSandbox demo](https://codesandbox.io/embed/kor9r1v7yv?fontsize=14)

## Summing Up

We’re well on our way to create an amazing validation library. We’ve added tons of features, and we’re pretty much-thought leaders by now.

In the [next part](https://www.smashingmagazine.com/2019/05/react-validation-library-developer-experience-part3) of this series, we’re going to add all of those extras that make our validation library even trend on LinkedIn.

{{< signature "dm, yk, il" >}}
