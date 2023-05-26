---
title: 'Implementing A Reset Password Feature With Next.js Dynamic Routes'
slug: implementing-reset-password-feature-nextjs-dynamic-routes
author: caleb-olojo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59a0f37a-cd1e-4a3c-abaf-bbf803d81034/implementing-reset-password-feature-nextjs-dynamic-routes-sharing-card.jpg
date: 2022-08-19T10:00:00.000Z
summary: >-
  Most users tend to forget their passwords, so create experiences that will always be valuable for people when they use your products. In this article, we’ll discuss how to implement a password-reset feature with Next.js dynamic routes while prioritizing the UX.
description: >-
  Most users tend to forget their passwords, so create experiences that will always be valuable for people when they use your products. In this article, we’ll discuss how to implement a password-reset feature with Next.js dynamic routes while prioritizing the UX.
categories:
  - JavaScript
  - Next.js
  - Performance
  - Security
---

In a general sense, authentication poses itself as a roadblock to many people when they are trying to get started with a particular framework, and Next.js isn’t left behind.

Although, there are lots of resources around building authenticated applications with Next.js. Well, there’s even an [open-source project](https://next-auth.js.org/) that literally handles authentication from the ground up.

But, the scope of this article doesn’t revolve around the whole concept of authentication. We’re only picking a specific pattern of the authentication process: the “reset password” flow and how it can be implemented on the client-side &mdash; frontend &mdash; of a web application.

In this article, you’re going to see how this feature can be implemented by using the common data-fetching tool, Axios &mdash; the built-in dynamic routes feature of Next.js and the `useRouter` hook.

## An Overview Of The Reset-Password Flow

Since the advent of the web, Engineers have always strived to provide solutions to the problems that arose during the early days of the web &mdash; and the security of software on the web is no exception.

There’s this popular saying that goes thus: “Users will always forget their passwords,” and that is the absolute truth. A lot of people even dread the “reset-password” page because, come to think of it, after spending a lot of time trying to guess their passwords &mdash; all to no avail &mdash; they’re either frustrated or angry as they land on this particular page.

As we create user interfaces, we should also try as much as possible to make the experience enjoyable for the users. As much as we’d love to just get over the flow of the reset password process, the UX of that flow should be prioritized too.

The common flow of the password reset process can be seen below.

- The user is frustrated after trying to sign without success. They click on the “password-reset” link, and they’re redirected to the corresponding page. The user interface that they see is the typical web form that’ll take in either their email address or username.
- When they type their email address or username into the input field, they click on the button which has the common “email me a recovery link” text.
- They get a confirmation that a secure link has been sent to their email. Sometimes, this confirmation text can be displayed in a card-like component or a modal that fades out over time.
    
**Note**: *For security purposes and good UX, it is good to use a text that is quite similar to this: “An email has been sent to your inbox. Please click the link when you get it.” You can construct this sentence anyhow you deem fit, as long as it does not reveal that the email or username they entered exists in the database. This approach prevents attackers from knowing if that email exists at all, thus sabotaging any phishing attempt they may want to try with the said email address. As for the UX, the text doesn’t assure the user that the credentials they’ve entered are the correct ones. This, in turn, allows them to double-check whatever credentials they’re submitting.*

- The link that is sent to their email address contains a JWT and their `user_id`, or in this case, their email address.
- Upon clicking on that link, they’re redirected to the route/page where they can input their new password. The route that the user will be on may be of the form below

<pre><code class="language-markup">https://localhost:3000/reset-password/user-email/JWToken</code></pre>

- The last part of the flow is to verify if the JWT that is generated is associated with the user’s account. If not, we throw an error by rendering the error message that is obtained from the backend.

Now that you’ve seen how the “reset password” flow is structured, let’s see how it can be implemented with Next.js.

## Understanding Dynamic Routes

In this section, we’ll go over the concept of dynamic routes by illustrating it with the folder structure of a Next.js project and see how we’ll integrate it into the “reset password” feature. But first, let’s set up a Next.js app.

<pre><code class="language-markup">npx create-next-app app-name</code></pre>

The command above does that for us. The Next.js team has already shipped a new update to the framework, and they’ve also introduced a couple of new folders and features in the default project structure. However, we won’t be covering much on that aspect, as it is out of the scope of this article. You can read more about the updates [here](https://nextjs.org/blog/layouts-rfc) if you want to.

In the snippet below, you’ll see the basic structure of the files we’ll be interacting with in this article.

<pre><code class="language-markup">└── pages /
    ├── forgot-password/
    │   └── [token]/
    │       └── [email].js
    ├── _app.js
    └── index.js
</code></pre>

Above, you’ll see that the files in the folder structure are quite small. That’s because I want to be concise as much as possible in this article.

And since the implementation of the “password reset” flow is our utmost concern, I think it’ll be best if we have less clutter. Now, let’s get a bit of an understanding of this structure.

You’ll notice that we have the `forgot-password` folder in the `pages` directory, which contains some files. But the naming convention of these files is quite different from the way other files are named. The name of the files &mdash; token and email.js &mdash; are wrapped with a pair of square brackets.

Folders and files that are named like this are referred to as dynamic routes, and since they’re in the `pages` directory, they automatically become routes that can be accessed by the browser. They are dynamic because the values that these routes take are not static, which means that they change over time.

This pattern of naming files is commonly seen in action when you decide to build a blog or when you’re interacting with data that changes based on the type of user that is logged into an application. You can take a look at how I utilized this feature of Next.js when I was [building my blog](https://meje.dev/blog/how-i-built-this-blog). You can also learn more about it in the [Next.js docs](https://nextjs.org/docs/routing/dynamic-routes).

In the `forgot-password` folder, the path to where the UI containing the forgot password form can be accessed here. Take a look at it below.

<pre><code class="language-markup">http://localhost:3000/forgot-password/token/email</code></pre>

Since it is a dynamic route, the `token` and `email` URL parameters will always change based on the user that is trying to reset their password. The token and email for user A will be different from that of user B.

{{% feature-panel %}}

## Reading Url Parameters With The Userouter Hook

The `useRouter` hook in Next.js can be used to achieve a lot of practical frontend UI implementations &mdash; from the common idea of implementing an active navbar item with the `.pathname` key, to more complex features.

Let’s see how we can read the URL parameters from dynamic routes with the `useRouter` hook now, shall we? To do that, you’ll have to import the module into your page/component first.

<div class="break-out">

<pre><code class="language-javascript">import { useRouter } from 'next/router'
export default function PageComponent({ children }) {
  const router = useRouter()
  return (
    &lt;React.Fragment&gt;
      {/* page content falls below */}
      &lt;div&gt;{children}&lt;/div&gt;
    &lt;/React.Fragment&gt;
  )
}
</code></pre>
</div>

The snippet above shows the basic usage of the hook. Since we’re interested in the query parameters of the URL, it’ll be best if we destructure the `query` method of the hook instead of doing something like this: `router.query`. We’ll just do something similar below.

<div class="break-out">

<pre><code class="language-javascript">import { useRouter } from 'next/router'
const { query } = useRouter()
</code></pre>
</div>

We can now go ahead to create variables that’ll store the URL parameters that we want. The snippet below shows how you can do that.

<div class="break-out">

<pre><code class="language-javascript">const token = query.token
const email = query.email
</code></pre>
</div>

Note that the `query.token` and `query.email` values are a result of the name of the files. Recall from the folder structure in the `forgot-password` folder where we have the `[email].js` and `[token]` files. If you rename those files to `[userEmail].js` and `[userToken]` respectively, the pattern of assigning these variables will become something like the one below.

<div class="break-out">

<pre><code class="language-javascript">const token = query.userToken
const email = query.userEmail
</code></pre>
</div>

You can always log these variables to the console to see the result. 

Now that you’ve gotten an understanding of how these parameters are obtained from the URL, let’s get started by building the structure of the forms.

## Building The Forms

In this section, we’ll walk through the process of building the form and how you can use Axios to perform data fetching via the arbitrary API endpoint. We won’t be focusing on the styling of these forms and the explanation of the structure. I’m assuming you already know how to structure and style a basic React form. So let’s get started with the form layout on the forget-password route.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import axios from 'axios'
import { ErrModal, SuccessModal } from '../components/Modals'

export const DefaultResetPassword = () =&gt; {
  const [email, setEmail] = React.useState('')
  const [loading, setLoading] = React.useState(false)

  const handleForgot = () =&gt; { } // we’ll see this later

  return (
    &lt;div&gt;
      &lt;form onSubmit={handleForgot} className="reset-password"&gt;
        &lt;h1&gt;Forgot Password&lt;/h1&gt;
        &lt;p&gt;You are not alone. We’ve all been here at some point.&lt;/p&gt;
        &lt;div&gt;
          &lt;label htmlFor="email"&gt;Email address&lt;/label&gt;
          &lt;input
            type="email"
            name="email"
            id="email"
            placeholder= “your email address”
            value={email}
            onChange={(e) =&gt; setEmail(e.target.value)}
            required
          /&gt;
        &lt;/div&gt;
        &lt;button name="reset-pwd-button" className="reset-pwd"&gt;
          {!loading ? ‘Get secure link’: ‘Sending...’}
        &lt;/button&gt;
      &lt;/form&gt;
    &lt;/div&gt;
  )
}
</code></pre>
</div>

The snippet above shows the basic structure of the UI that you’ll see when you get to the forgot-password route. You’ll notice the text in the paragraph tag below the bold “Forgot password” text.

<div class="break-out">

<pre><code class="language-HTML">&lt;p&gt;You are not alone. We’ve all been here at some point&lt;/p&gt;
</code></pre>
</div>

With a type of text like the one above, you are improving the user experience of people who get to the forgot password page of your app. You are assuring them that it is not a big deal that they forgot their password(s), so there’s no need to feel bad about it.

You don’t necessarily need to use the exact text above. You can just make sure that whatever text you are using has a tone of **empathy**.

Now, let’s move on to the important part of this form, which is where we need to declare a function that’ll send the email that the user enters in the input field to the backend.

<div class="break-out">

<pre><code class="language-javascript">import { authEndpoints } from '../endpoints'

export const DefaultResetPassword = () =&gt; {
  const handleForgot = async (e) =&gt; {
    e.preventDefault()
    try {
      setLoading(true)
      const response = await axios({
        method: 'POST',
        url: authEndpoints.recover,
        data: {
          email,
        },
        headers: {
          'Content-Type': 'application/json',
        },
      })
      setResestSuccess(response.data.msg)
      setLoading(false)
      setResetError('')
    } catch (error) {
      setLoading(false)
      const { data } = error.response
      setResetError(data.msg)
      setResestSuccess(null)
    }
  }
  return &lt;div&gt;{/* ...previous form component &#42;/}&lt;/div&gt;
}
</code></pre>
</div>

From the snippet above, you’ll notice that we’re importing the API endpoint that we’ll be sending a POST request to &mdash; and that’s why we’re passing it as a variable to the `url` key in the Axios method.

The POST request receives the user’s email address as payload, which in turn will be validated at the backend, and a JWT will be generated for that email address which will be used to authorize the password reset process of the user.

<div class="break-out">

<pre><code class="language-javascript">setResestSuccess(response.data.msg)
setLoading(false)
setResetError('')
catch (error) {
  setLoading(false)
  const { data } = error.response
  setResetError(data.msg)
  setResestSuccess(null)
}
</code></pre>
</div>

When you take a look at the snippet above, you’ll notice that we’re using some already-declared state callback functions of the state variables.  

An example is the `setLoading` function which has its value set to `true` in the `try` block. Then, its value is set to false when the data has been successfully sent. And if it doesn’t, we have a `catch` block that will “catch” the error and displays the error message that we’ve destructured from the endpoint.  

You’ll also notice that there are a couple of state callback functions in the snippet above, like `setResestSuccess` and `setResetError`. 

The setters are obtained from the declaration of the state variables. See them below.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import { ErrModal, SuccessModal } from '../components/Modals'

export const DefaultResetPassword = () =&gt; {
  const [resetSuccess, setResestSuccess] = React.useState()
  const [resetError, setResetError] = React.useState()
  return (
    &lt;div&gt;
      {resetError ? &lt;ErrModal message={resetError} /&gt; : null}
      {resetSuccess ? &lt;SuccessModal message={resetSuccess} /&gt; : null}
      &lt;form onSubmit={handleForgot} className="reset-password"&gt;
        {/&#42; form content &#42;/}
      &lt;/form&gt;
    &lt;/div&gt;
  )
}
</code></pre>
</div>

The error or success messages gotten from the backend can be rendered in the UI to let the user know the status of their action(s).

You’ll notice that we’re using custom modal components to render the message. These components receive the message as props, and they can be reused across the codebase. Take a look at the structure of the components below.

<div class="break-out">

<pre><code class="language-javascript">export const SuccessModal = ({ message }) =&gt; {
  return (
    &lt;div className="auth-success-msg"&gt;
      &lt;p&gt;{message}&lt;/p&gt;
    &lt;/div&gt;
  )
}
export const ErrModal = ({ message }) =&gt; {
  return (
    &lt;div className="auth-err-msg"&gt;
      &lt;p&gt;{message}&lt;/p&gt;
    &lt;/div&gt;
  )
}
</code></pre>
</div>

You can style these components uniquely so that you can be able to distinguish the “error” modal from the “success” modal. The common convention is to use red color for error messages and green color for success messages. How you choose to style these components is completely up to you.

{{% ad-panel-leaderboard %}}

In addition to all that has been said, we need a way to verify that the correct data type is being passed as a prop to the modal component. This can be achieved with the “prop-type” module in react.

<pre><code class="language-javascript">propTypes.ErrModal = {
  message: propTypes.string.isRequired,
}
propTypes.SuccessModal = {
  message: propTypes.string.isRequired,
}
</code></pre>

The type-checking process in the snippet above ensures that the data the component receives must be a string, and it is required. If the component does not receive a prop with a string value, React will throw an error.

Now that we’ve covered the important aspect of the first form and the building blocks of what we’ll be replicating in the reset-password route. Let’s get started by taking a look at the layout of the form below.

<div class="break-out">

 <pre><code class="language-javascript">import axios from "axios";
import React from “react”;
import Head from “next/head”;
import { useRouter } from "next/router";
import { SuccessModal, ErrModal } from "../components/Modals";

const ResetPassword = () =&gt; {
  const &#91;newPassword, setNewPassword&#93; = React.useState("");
  const &#91;loading, setLoading&#93; = React.useState(false);
  const &#91;resetPasswordSuccess, setResetPasswordSuccess&#93; = React.useState();
  const &#91;resetPasswordError, setResetPasswordError&#93; = React.useState();

  const { query } = useRouter();
  const token = query.token;
  const email = query.email;

  const resetPassword = () =&gt; { } // coming in later...

  return (
    &lt;React.Fragment&gt;
      &lt;Head&gt;
        &lt;title&gt;Reset your password&lt;/title&gt;
      &lt;/Head&gt;
      &lt;div&gt;
        {email && token ? (
          &lt;div className="auth-wrapper"&gt;
            {resetPasswordSuccess ? (
              &lt;SuccessModal message={resetPasswordSuccess} /&gt;
            ) : (
              null
            )}
            {resetPasswordError ? (
              &lt;ErrModal message={resetPasswordError} /&gt;
            ) : (
              null
            )}
            &lt;form onSubmit={resetPassword} className="reset-password"&gt;
              &lt;h1&gt;Reset Password&lt;/h1&gt;
              &lt;p&gt;Please enter your new password&lt;/p&gt;
              &lt;div&gt;
                &lt;label htmlFor="password"&gt;Password&#42;&lt;/label&gt;
                &lt;input
                  name="password"
                  type="password"
                  id="password"
                  placeholder="enter new pasword"
                  value={newPassword}
                  onChange={(e) =&gt; setNewPassword(e.target.value)}
                /&gt;
              &lt;/input&gt;
              &lt;button
                name="reset-pwd-button"
                className="reset-pwd"
              &gt;
                {!loading ? "Reset" : "Processing..."}
              &lt;/button&gt;
            &lt;/form&gt;
          &lt;/div&gt;
        ) : (
          &lt;p&gt;The page you're trying to get to isn't available&lt;/p&gt;
        )}
      &lt;/div&gt;
    &lt;/React.Fragment&gt;
  );
};
</code></pre>
</div>

Since we’ve gone through the rudiments of the first form in the previous section, the snippet above contains almost the same thing in the previous form.

You can see how we’re reading the parameters from the URL and the declarations of the password reset error and success variables too.

<div class="break-out">

<pre><code class="language-javascript">const [resetPasswordSuccess, setResetPasswordSuccess] = React.useState()
const [resetPasswordError, setResetPasswordError] = React.useState()
const { query } = useRouter()
const token = query.token
const email = query.email
</code></pre>
</div>

You’ll also notice the way we’re conditionally rendering the reset password form by checking if the `email` and `token` variables are present in the URL; if these variables are false (i.e., they are not in the URL), we render a text that says that the page they’re looking for isn’t available.

<div class="break-out">

<pre><code class="language-javascript">{
  email && token ? (
    &lt;div className="auth-wrapper"&gt;
      &lt;FormComponentt /&gt;
    &lt;/div&gt;
  ) : (
    &lt;p&gt;The page you’re trying to get to isn’t available&lt;/p&gt;
  )
}
</code></pre>
</div>

Now, let’s take a look at the handler function that we’d use in sending the new password of the user &mdash; coupled with the token and the email for the purpose of verification &mdash; to the backend through the API endpoint.

<div class="break-out">

<pre><code class="language-javascript">import { authEndpoints } from '../endpoints'
const resetPassword = async (e) =&gt; {
  e.preventDefault()
  try {
    setLoading(true)
    const response = await axios({
      method: 'POST',
      url: authEndpoints.resetPassword,
      data: {
        token,
        email,
        password: newPassword,
      },
      headers: {
        'Content-Type': 'application/json',
      },
    })
    setResetPasswordSuccess(response.data.msg)
    setLoading(false)
    setTimeout(() =&gt; {
      router.push('/')
    }, 4000)
    setResetPasswordError('')
  } catch (error) {
    setLoading(false)
    setResetPasswordError(error.response.data.msg)
    setResetPasswordSuccess(null)
  }
}
</code></pre>
</div>

The snippet above is an asynchronous handler function. We’re using it to send a POST request with the user’s new password, the access token, and the email address &mdash; which we grabbed from the query parameters at the URL segment.

<div class="break-out">

<pre><code class="language-javascript">setTimeout(() =&gt; {
  router.push('/')
}, 4000)
</code></pre>
</div>

When you take a look at the snippet above, you’ll see how we’re using the `setTimeout` method in JavaScript and Next.js’ `useRouter` hook to redirect the user to the home page &mdash; which is the login page in this case &mdash; after four seconds (you can reduce this time frame if you want to), so they can log in again.

Doing this also adds to the good user experience metric, as it prevents the user from looking for a link or a button that takes them back to the login page.

{{% ad-panel-leaderboard %}}

## Final Thoughts

There is a lot of information about the best practices and awesome password-reset design patterns out there. This article is just a frontend implementation of a password-reset flow which also factors in the issue of user experience. It is not enough to just create a password reset feature without considering the UX of the people who would use this feature.

Thank you for reading. I hope this article has been helpful!
  
### Further Reading On Smashing Magazine

- “[How To Implement Authentication In Next.js With Auth0](https://www.smashingmagazine.com/2021/05/implement-authentication-nextjs-auth0/),” Facundo Giuliani 
- “[Dynamic Data-Fetching In An Authenticated Next.js App](https://www.smashingmagazine.com/2022/04/dynamic-data-fetching-authenticated-nextjs-app/),” Caleb Olojo
- “[Localizing Your Next.js App](https://www.smashingmagazine.com/2021/11/localizing-your-nextjs-app/),” Átila Fassina
- “[The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/),” Drew Thomas

{{< signature "nl, il" >}}
