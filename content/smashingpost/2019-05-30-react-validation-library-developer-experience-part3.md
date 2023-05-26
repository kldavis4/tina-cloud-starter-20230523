---
title: 'Creating Your Own React Validation Library: The Developer Experience (Part 3)'
slug: react-validation-library-developer-experience-part3
author: kristofer-giltvedt-selbekk
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc742d1-a118-405e-abdc-f96870706f72/react-library-article-sharing-card.png
date: 2019-05-30T13:00:59+02:00
summary: >-
  So we’ve already seen how we can [implement the basic parts](https://www.smashingmagazine.com/2019/05/react-validation-library-basics-part1/) of our validation library, and [how to add all the nice-to-have features](https://www.smashingmagazine.com/2019/05/react-validation-library-features-part2/) we needed. This final part of this series will focus on improving the user experience for the people that will use our validation library: the developers.
description: >-
  This final part of the series will focus on improving the user experience for the people that will use our validation library: the developers.
categories:
  - React
  - JavaScript
  - Forms
---
If you’ve been following along this little article series, you’ve now learned how to put together your very own validation library. It can handle almost any challenge you can throw at it, and it even helps out with accessibility concerns! Its only downfall is that it sucks to work with.

Yep, that’s right. The user experience from a developer point of view is seriously lacking. We don’t get any helpful warnings when we misspell words, misuse APIs or, well, anything, really!

This article will guide you through how you can improve the developer experience of your validation library &mdash; or any library for that sake.

- [Part 1: The Basics](https://www.smashingmagazine.com/2019/05/react-validation-library-basics-part1/)
- [Part 2: The Features](https://www.smashingmagazine.com/2019/05/react-validation-library-features-part2/)
- **Part 3: The Experience**

## Starting Out

Since the last part of this article, we’ve pulled out all library code into its own files. Take a look at the [CodeSandbox demo](https://codesandbox.io/embed/1v12lj234j?fontsize=14) to see what we’re starting out with.

{{% feature-panel %}}

## Convenience Functions

We want our library to be as simple as possible to use for the most common cases. A way to move towards that goal is to add convenient utility functions for certain functionality.

One such feature could be to check if our form is valid &mdash; that is, if all error messages are `null`. This is something you typically check in your `onSubmit` handler, but it could be useful in your render-method too. Let’s implement it!

<pre><code class="language-javascript">const isFormValid = useMemo(
  () => Object.values(errors).every(error => error === null), 
  [errors]
);
</code></pre>

We’ll provide this flag in our `onSubmit` form handler, as well as in our render method.

- [See CodeSandbox demo](https://codesandbox.io/embed/qq19vyp0q6?fontsize=14)

There are plenty more of these that could be written, but I’ll let that be an exercise for the reader.

## Development Warnings And Invariants

One of React’s greatest features is its many helpful console warnings while developing. We should provide the same sort of quality to our users as well.

To get started, we’ll create two functions &mdash; `warning` for logging warnings to the console, and `invariant` for throwing an error &mdash; both if a given condition is not met.

<pre><code class="language-javascript">function warning(condition, message) {
  if (process.env.NODE_ENV === 'production' || condition) {
    return;
  }

  console.warn('useValidation: ' + message);
}
function invariant(condition, message) {
  if (process.env.NODE_ENV === 'production' || condition) {
    return;
  }

  throw new Error('useValidation: ' + message);
}
</code></pre>

You want to use `invariant` if the error is going to crash your library (or render it useless), and `warning` for bad practices or other advice.

### When To Warn

Deciding when to warn is pretty important. Too many, and you’re just annoying. Too few, and you let critical bugs ship to production. Therefore, we need to be smart with our warnings.

Since our library accepts a pretty large configuration object, it makes sense to validate this somehow &mdash; at least while developing. We could solve it by using a type system like TypeScript or Flow, but that excludes all regular ol' JavaScript users.

Instead, let’s create a runtime schema checker, where we validate that the config contains the correct fields, and print relevant warnings.

<div class="break-out">

<pre><code class="language-javascript">function validateConfigSchema(config) {
  if (process.env.NODE_ENV === 'production') {
    return;
  }
  if (typeof config === 'function') {
    config = config({});
  }

  invariant(
    typeof config === 'object',
    `useValidation should be called with an object or a function returning an object. You passed a ${typeof config}.`,
  );

  invariant(
    typeof config.fields === 'object',
    'useValidation requires a `field` prop with an object containing the fields and their validators. Please refer to the documentation on usage: https://link.to/docs'
  );

  
  invariant(
    Object.values(config.fields).every(field => typeof field === 'object'),
    'useValidation requires that the `field` object only contains objects. It looks like yours isn\'t. Please refer to the documentation on usage: https://link.to/docs'
  );

  warning(
    ['always', 'blur', 'submit', undefined].includes(config.showError),
    'useValidation received an unsupported value in the `showError` prop. Valid values are "always", "blur" or "submit".'
  )

  // And so on
}
</code></pre>
</div>

We could probably go on doing this for a while if we wanted to spend the time. And you should! It’s a great way to improve the developer experience of your app.

You don’t have to be writing these by hand, however. There’s a browser-port of the popular object schema validation library [`joi`](https://github.com/jeffbski/joi-browser) that could help out with creating a really nice runtime validation check. Also, as previously mentioned, a type system would help catch configuration errors at compile time for the users that use that type system.

{{% ad-panel-leaderboard %}}

## Allow For Flexibility

A good developer experience is in large part not getting in the way of the developers. Let’s look at a few ways we can improve that experience.

### Compose Conflicting Props

First, our prop getters apply some props to our inputs and forms that can be accidentally overridden by our consumers. Instead, let’s add a prop override object to our prop getters, which will compose any conflicting props together.

Here’s how we can implement this in our `getFieldProps`:

<pre><code class="language-javascript">
getFieldProps: (fieldName, overrides = {}) => ({
  onChange: e => {
    const { value } = e.target;
    if (!config.fields[fieldName]) {
      return;
    }
    dispatch({
      type: 'change',
      payload: { [fieldName]: value },
    });
    if (overrides.onChange) {
      overrides.onChange(e);
    }
  },
  onBlur: e => {
    dispatch({ type: 'blur', payload: fieldName });
    if (overrides.onBlur) {
      overrides.onBlur(e)
    }
  },
  name: overrides.name || fieldName,
  value: state.values[fieldName] || '',
}),
</code></pre>

A similar approach can be followed in `getFormProps`.

### Help Avoid Prop Drilling

Some forms might be large and split up into several components. Instead of making our consumers' drill props down the tree, we should provide a context. This way, they can access all the stuff we return from our custom hook anywhere in the tree below.

First, let’s create a ValidationContext with React’s `createContext` method:

<pre><code class="language-javascript">export const ValidationContext = React.createContext({});
</code></pre>

Next, let’s create a component `ValidationProvider`, that provides all the values from the `useValidation` hook in context instead:

<pre><code class="language-javascript">export const ValidationProvider = props => {
  const context = useValidation(props.config);
  return (
    <ValidationContext.Provider value={context}>
      {props.children}
    </ValidationContext.Provider>
  );
};
</code></pre>

Now, instead of calling `useValidation` directly, we'd wrap our form in a `ValidationProvider` component, and get access to the validation props (`getFormProps`, `errors` etc) by use of the [`useContext` hook](https://reactjs.org/docs/hooks-reference.html#usecontext). You'd use it like this:

<pre><code class="language-javascript">Import React, { useContext } from 'react';
import { ValidationContext } from './useValidation';

function UsernameForm(props) {
  const { getFieldProps, errors } = useContext(ValidationContext);
  return (
    &lt;&gt;
      &lt;input {...getFieldProps('username')} /&gt;
      {errors.username && <span className="error">{errors.username}>&lt;/span&gt;}
    &lt;/&gt;
  );
}
</code></pre>

This way, you get the best of both worlds! You get a simple hook for those simple scenarios, and you get the flexibility you need for those complex parts. 

{{% ad-panel-leaderboard %}}

## Documentation Is Key 🔑

Whenever I’m using a library I didn’t write myself, I love great documentation. But what should you focus on, and where should you document?


A first step should be to put together a simple to understand README, with the most basic usage examples readily available. [Andrew Healey](https://dev.to/healeycodes) wrote an amazing piece on [how to write a good README](https://dev.to/healeycodes/how-to-write-an-awesome-github-readme-2ldc), which I highly recommend you read.

When you’ve created a good README to get people going, a documentation website might be a good idea. Here, you can put a more in-depth API documentation, recipes for typical use cases and a good ol’ FAQ. 

There are great tools out there for generating documentation websites. My favorite is [`docusaurus` from Facebook](https://docusaurus.io/) (humble brag: we used it when creating the `create-react-app` website), but there are several good alternatives out there.

We’re not going to go through how to write good documentation in this article. There are several good articles out there &mdash; even a community called "[Write the Docs](https://www.writethedocs.org)". They have written a great guide to [how you can get started with writing great documentation](https://www.writethedocs.org/guide/writing/beginners-guide-to-docs/).

## Summary

Through this article series, we’ve created a pretty decent validation library. It has a pretty simple API, flexibility for when you need it, a good developer experience, and a lot of pretty dank features.

We’ve gone through how we implemented things step by step, and I hope you got a deeper understanding of how you can make your own library, and how you make it something people would love to use.

Please let me know in the comments what you think, and if there were some parts you got stuck on or had a hard time understanding. I’ll try my best to update the article as feedback trickles in.

To end this article off &mdash; here’s the final version:

- [See CodeSandbox demo](https://codesandbox.io/embed/749z4p21j?fontsize=14)

Thanks for reading!

{{< signature "dm, yk, il" >}}
