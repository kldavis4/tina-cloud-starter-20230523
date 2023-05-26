---
title: 'Creating Your Own React Validation Library: The Basics (Part 1)'
slug: react-validation-library-basics-part1
author: kristofer-giltvedt-selbekk
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc742d1-a118-405e-abdc-f96870706f72/react-library-article-sharing-card.png
date: 2019-05-16T13:00:59+02:00
summary: >-
  Ever wondered how validation libraries work? This article will tell you how to build your very own validation library for React step by step. The next part will add some more advanced features, and the final part will focus on improving the developer experience.
description: >-
  Ever wondered how validation libraries work? This article will tell you how to build your very own validation library for React step by step. The next part will add some more advanced features, and the final part will focus on improving the developer experience.
categories:
  - React
  - JavaScript
  - Testing
  - Forms
---
I’ve always thought form validation libraries were pretty cool. I know, it’s a niche interest to have &mdash; but we use them so much! At least in my job &mdash; most of what I do is constructing more or less complex forms with validation rules that depend on earlier choices and paths. Understanding how a form validation library would work is paramount.

Last year, I wrote one such form validation library. I named it “[Calidation](https://github.com/selbekk/calidation)”, and you can read the introductory blog post [here](https://medium.com/@selbekk/introducing-calidation-7d9a79453f7). It’s a good library that offers a lot of flexibility and uses a slightly different approach than the other ones on the market. There are tons of other great libraries out there too, though &mdash; mine just worked well for *our* requirements.

Today, I’m going to show you how to write *your very own validation library* for React. We will go through the process step by step, and you’ll find CodeSandbox examples as we go along. By the end of this article, you will know how to write your own validation library, or at the very least have a deeper understanding of how other libraries implement "the magic of validation".

- **Part 1: The Basics**
- Part 2: [The Features](https://www.smashingmagazine.com/2019/05/react-validation-library-features-part2)
- Part 3: [The Experience](https://www.smashingmagazine.com/2019/05/react-validation-library-developer-experience-part3)

{{% feature-panel %}}

## Step 1: Designing The API

The first step of creating any library is designing how it’s going to be used. It lays the foundation for a lot of the work to come, and in my opinion, it’s the single most important decision you’re going to make in your library. 

It’s important to create an API that’s "easy to use", and yet flexible enough to allow for future improvements and advanced use cases. We’ll try to hit both of these goals. 

We’re going to create a [custom hook](https://reactjs.org/docs/hooks-custom.html) that will accept a single configuration object. This will allow for future options to be passed without introducing breaking changes.

### A Note On Hooks

Hooks is a pretty new way of writing React. If you’ve written React in the past, you might not recognize a few of these concepts. In that case, please have a look at [the official documentation](https://reactjs.org/docs/hooks-intro.html). It’s incredibly well written, and takes you through the basics you need to know.

We’re going to call our custom hook `useValidation` for now. Its usage might look something like this:

<div class="break-out">

 <pre><code class="language-javascript">const config = {
  fields: {
    username: {
      isRequired: { message: 'Please fill out a username' },
    },
    password: {
      isRequired: { message: 'Please fill out a password' },
      isMinLength: { value: 6, message: 'Please make it more secure' }
    }
  },
  onSubmit: e => { /* handle submit */ }
};
const { getFieldProps, getFormProps, errors } = useValidation(config);
</code></pre>
</div>

The `config` object accepts a `fields` prop, which sets up the validation rules for each field. In addition, it accepts a callback for when the form submits.

The `fields` object contains a key for each field we want to validate. Each field has its own config, where each key is a validator name, and each value is a configuration property for that validator. Another way of writing the same would be:

<div class="break-out">

 <pre><code class="language-javascript">{
  fields: {
    fieldName: {
      oneValidator: { validatorRule: 'validator value' },
      anotherValidator: { errorMessage: 'something is not as it should' }
    }
  }
}
</code></pre>
</div>

Our `useValidation` hook will return an object with a few properties &mdash; `getFieldProps`, `getFormProps` and `errors`. The two first functions are what [Kent C. Dodds](https://twitter.com/kentcdodds) calls "prop getters" ([see here for a great article on those](https://kentcdodds.com/blog/how-to-give-rendering-control-to-users-with-prop-getters)), and is used to get the relevant props for a given form field or form tag. The `errors` prop is an object with any error messages, keyed per field.

This usage would look like this:

<div class="break-out">

 <pre><code class="language-javascript">const config = { ... }; // like above
const LoginForm = props =&gt; {
  const { getFieldProps, getFormProps, errors } = useValidation(config);
  return (
    &lt;form {...getFormProps()}&gt;
      &lt;label&gt;
        Username&lt;br/&gt;
        &lt;input {...getFieldProps('username')} /&gt;
        {errors.username && &lt;div className="error"&gt;{errors.username}&lt;/div&gt;}
      &lt;/label&gt;
      &lt;label&gt;
        Password&lt;br/&gt;
        &lt;input {...getFieldProps('password')} /&gt;
        {errors.password && &lt;div className="error"&gt;{errors.password}&lt;/div&gt;}
      &lt;/label&gt;
      &lt;button type="submit"&gt;Submit my form&lt;/button&gt;
    &lt;/form&gt;
  );
};
</code></pre>
</div>

Alrighty! So we’ve nailed the API.

- [See CodeSandbox demo](https://codesandbox.io/s/ovm0vyv1lq)

Note that we’ve created a mock implementation of the `useValidation` hook as well. For now, it’s just returning an object with the objects and functions we require to be there, so we don’t break our sample implementation.

{{% ad-panel-leaderboard %}}

## Storing The Form State 💾

The first thing we need to do is storing all of the form state in our custom hook. We need to remember the values of each field, any error messages and whether or not the form has been submitted. We’ll use the [`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer) hook for this since it allows for the most flexibility (and less boilerplate). If you’ve ever used [Redux](https://redux.js.org/introduction/getting-started), you’ll see some familiar concepts &mdash; and if not, we’ll explain as we go along! We’ll start off by writing a reducer, which is passed to the `useReducer` hook:

<div class="break-out">

 <pre><code class="language-javascript">const initialState = {
  values: {},
  errors: {},
  submitted: false,
};

function validationReducer(state, action) {
  switch(action.type) {
    case 'change': 
      const values = { ...state.values, ...action.payload };
      return { 
        ...state, 
        values,
      };
    case 'submit': 
      return { ...state, submitted: true };
    default: 
      throw new Error('Unknown action type');
  }
}
</code></pre>
</div>

## What’s A Reducer? 🤔

A reducer is a function that accepts an object of values and an "action" and returns an augmented version of the values object.

Actions are plain JavaScript objects with a `type` property. We’re using a [`switch` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch) to handle each possible action type.

The "object of values" is often referred to as **state**, and in our case, it’s the state of our validation logic.

Our state consists of three pieces of data &mdash; `values` (the current values of our form fields), `errors` (the current set of error messages) and a flag `isSubmitted` indicating whether or not our form has been submitted at least once.

In order to store our form state, we need to implement a few parts of our `useValidation` hook. When we call our `getFieldProps` method, we need to return an object with the value of that field, a change-handler for when it changes, and a name prop to track which field is which.

<div class="break-out">

 <pre><code class="language-javascript">function validationReducer(state, action) {
  // Like above
}

const initialState = { /&#42; like above &#42;/ };

const useValidation = config => {
  const [state, dispatch] = useReducer(validationReducer, initialState);
  
  return {
    errors: state.errors,
    getFormProps: e => {},
    getFieldProps: fieldName => ({
      onChange: e => {
        if (!config.fields[fieldName]) {
          return;
        }
        dispatch({ 
          type: 'change', 
          payload: { [fieldName]: e.target.value } 
        });
      },
      name: fieldName,
      value: state.values[fieldName],
    }),
  };
};
</code></pre>
</div>

The `getFieldProps` method now returns the props required for each field. When a change event is fired, we ensure that field is in our validation configuration, and then tell our reducer a `change` action took place. The reducer will handle the changes to the validation state.

- [See CodeSandbox demo](https://codesandbox.io/s/6nx2zzo0rn)

{{% ad-panel-leaderboard %}}

## Validating Our Form 📄

Our form validation library is looking good, but isn’t doing much in terms of validating our form values! Let’s fix that. 💪

We’re going to validate all fields on every change event. This might not sound very efficient, but in the real world applications I’ve come across, it isn’t really an issue.

Note, we’re not saying you have to show every error on every change. We’ll revisit how to show errors only when you submit or navigates away from a field, later in this article.

### How To Pick Validator Functions

When it comes to validators, there are tons of libraries out there that implement all the validation methods you'd ever need. You can also write your own if you want. It’s a fun exercise! 

For this project, we’re going to use a set of validators I wrote some time ago &mdash; [`calidators`](https://github.com/selbekk/calidators). These validators have the following API:

<pre><code class="language-javascript">function isRequired(config) {
  return function(value) {
    if (value === '') {
      return config.message;
    } else {
      return null;
    }
  };
}

// or the same, but terser

const isRequired = config => value => 
    value === '' ? config.message : null;
</code></pre>

In other words, each validator accepts a configuration object and returns a fully-configured validator. When _that_ function is called with a value, it returns the `message` prop if the value is invalid, or `null` if it’s valid. You can look at how some of these validators are implemented by looking at [the source code](https://github.com/selbekk/calidators/tree/master/src). 

To access these validators, install the `calidators` package with `npm install calidators`.

### Validate a single field

Remember the config we pass to our `useValidation` object? It looks like this:

<div class="break-out">

 <pre><code class="language-javascript">{ 
  fields: {
    username: {
      isRequired: { message: 'Please fill out a username' },
    },
    password: {
      isRequired: { message: 'Please fill out a password' },
      isMinLength: { value: 6, message: 'Please make it more secure' }
    }
  },
  // more stuff
}
</code></pre>
</div>

To simplify our implementation, let’s assume we only have a single field to validate. We’ll go through each key of the field’s configuration object, and run the validators one by one until we either find an error or are done validating.

<div class="break-out">

 <pre><code class="language-javascript">import * as validators from 'calidators';

function validateField(fieldValue = '', fieldConfig) {
  for (let validatorName in fieldConfig) {
    const validatorConfig = fieldConfig[validatorName];
    const validator = validators[validatorName];
    const configuredValidator = validator(validatorConfig);
    const errorMessage = configuredValidator(fieldValue);

    if (errorMessage) {
      return errorMessage;
    }
  }
  return null;
}
</code></pre>
</div>

Here, we’ve written a function `validateField`, which accepts the value to validate and the validator configs for that field. We loop through all of the validators, pass them the config for that validator, and run it. If we get an error message, we skip the rest of the validators and return. If not, we try the next validator.

## Note: On validator APIs

If you choose different validators with different APIs (like the very popular [`validator.js`](https://www.npmjs.com/package/validator)), this part of your code might look a bit different. For brevity’s sake, however, we let that part be an exercise left to the reader.

## Note: On for...in loops

Never used `for...in` loops before? That’s fine, this was my first time too! Basically, it iterates over the keys in an object. You can read more about them at [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in).

### Validate all the fields

Now that we’ve validated one field, we should be able to validate all fields without too much trouble.

<div class="break-out">

 <pre><code class="language-javascript">function validateField(fieldValue = '', fieldConfig) {
  // as before
}

function validateFields(fieldValues, fieldConfigs) {
  const errors = {};
  for (let fieldName in fieldConfigs) {
    const fieldConfig = fieldConfigs[fieldName];
    const fieldValue = fieldValues[fieldName];

    errors[fieldName] = validateField(fieldValue, fieldConfig);
  }
  return errors;
}
</code></pre>
</div>

We’ve written a function `validateFields` that accepts all field values and the entire field config. We loop through each field name in the config and validate that field with its config object and value.

### Next: Tell our reducer

Alrighty, so now we have this function that validates all of our stuff. Let’s pull it into the rest of our code!

First, we’re going to add a `validate` action handler to our `validationReducer`.

<pre><code class="language-javascript">function validationReducer(state, action) {
  switch (action.type) {
    case 'change':
      // as before
    case 'submit':
      // as before
    case 'validate': 
      return { ...state, errors: action.payload };
    default:
      throw new Error('Unknown action type');
  }
}
</code></pre>

Whenever we trigger the `validate` action, we replace the errors in our state with whatever was passed alongside the action.

Next up, we’re going to trigger our validation logic from a [`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect) hook:

<div class="break-out">

 <pre><code class="language-javascript">const useValidation = config => {
  const [state, dispatch] = useReducer(validationReducer, initialState);

  useEffect(() => {
    const errors = validateFields(state.fields, config.fields);
    dispatch({ type: 'validate', payload: errors });
  }, [state.fields, config.fields]);
  
  return {
    // as before
  };
};
</code></pre>
</div>

This `useEffect` hook runs whenever either our `state.fields` or `config.fields` changes, in addition to on first mount.

#### Beware Of Bug 🐛

There’s a super subtle bug in the code above. We’ve specified that our `useEffect` hook should only re-run whenever the `state.fields` or `config.fields` change. Turns out, "change" doesn’t necessarily mean a change in value! `useEffect` uses `Object.is` to ensure equality between objects, which in turn uses reference equality. That is &mdash; if you pass a new object with the same content, it won’t be the same (since the object itself is new).

The `state.fields` are returned from `useReducer`, which guarantees us this reference equality, but our `config` is specified inline in our function component. That means the object is re-created on every render, which in turn will trigger the `useEffect` above!

To solve this, we need to use for the [`use-deep-compare-effect`](https://github.com/kentcdodds/use-deep-compare-effect) library by Kent C. Dodds. You install it with `npm install use-deep-compare-effect`, and replace your `useEffect` call with this instead. This makes sure we do a deep equality check instead of a reference equality check.

Your code will now look like this:

<div class="break-out">

 <pre><code class="language-javascript">import useDeepCompareEffect from 'use-deep-compare-effect';

const useValidation = config => {
  const [state, dispatch] = useReducer(validationReducer, initialState);

  useDeepCompareEffect(() => {
    const errors = validateFields(state.fields, config.fields);
    dispatch({ type: 'validate', payload: errors });
  }, [state.fields, config.fields]);
  
  return {
    // as before
  };
};
</code></pre>
</div>

#### A Note On useEffect

Turns out, `useEffect` is a pretty interesting function. [Dan Abramov](https://twitter.com/dan_abramov) wrote [a really nice, long article on the intricacies of `useEffect`](https://overreacted.io/a-complete-guide-to-useeffect/) if you’re interested in learning all there is about this hook.

Now things are starting to look like a validation library!

- [See CodeSandbox demo](https://codesandbox.io/s/486p81o644)

## Handling Form Submission

The final piece of our basic form validation library is handling what happens when we submit the form. Right now, it reloads the page, and nothing happens. That’s not optimal. We want to prevent the default browser behavior when it comes to forms, and handle it ourselves instead. We place this logic inside the `getFormProps` prop getter function:

<div class="break-out">

 <pre><code class="language-javascript">const useValidation = config => {
  const [state, dispatch] = useReducer(validationReducer, initialState);
  // as before
  return {
    getFormProps: () => ({
      onSubmit: e => {
        e.preventDefault();
        dispatch({ type: 'submit' });
        if (config.onSubmit) {
          config.onSubmit(state);
        }
      },
    }),
    // as before
  };
};
</code></pre>
</div>

We change our `getFormProps` function to return an `onSubmit` function, that is triggered whenever the `submit` DOM event is triggered. We prevent the default browser behavior, dispatch an action to tell our reducer we submitted, and call the provided `onSubmit` callback with the entire state &mdash; if it’s provided.

## Summary

We’re there! We’ve created a simple, usable and pretty cool validation library. There’s still tons of work to do before we can dominate the interwebs, though.

- **Part 1: The Basics**
- Part 2: [The Features](https://www.smashingmagazine.com/2019/05/react-validation-library-features-part2)
- Part 3: [The Experience](https://www.smashingmagazine.com/2019/05/react-validation-library-developer-experience-part3)

{{< signature "dm, il" >}}
