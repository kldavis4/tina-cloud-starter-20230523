---
title: 'Monetize Open-Source Software With Gatsby Functions And Stripe'
slug: monetize-open-source-software-gatsby-functions-stripe
author: paul-scanlon
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73f6525b-6678-4db1-a875-16150bc822cd/monetize-open-source-software-gatsby-functions-stripe.jpg
date: 2021-09-17T09:00:00.000Z
summary: >-
  Gatsby Functions provide front-end developers a way to write and use server-side code without the hassle of maintaining a server. If making money from open-source is of interest to you and your site isn’t built using Gatsby, this approach may well be the answer you were looking for.
description: >-
  Gatsby Functions provide front-end developers a way to write and use server-side code without the hassle of maintaining a server. If making money from open-source is of interest to you and your site isn’t built using Gatsby, this approach may well be the answer you were looking for.
categories:
  - Gatsby
  - JavaScript
  - Serverless
---

In this article, I’ll be explaining how I’ve used [Gatsby Functions](https://www.gatsbyjs.com/docs/reference/functions/) and the [Stripe](https://stripe.com/) API to enable secure “Pay what you want” contributions that help fund my open-source project [MDX Embed](https://www.mdx-embed.com/).

**Note**: *MDX Embed allows you to easily embed popular third-party media content such as YouTube videos, Tweets, Instagram posts, Egghead lessons, Spotify, TikTok and many more straight into your `.mdx` &mdash; no import required.*

## Gatsby Serverless Functions

[Gatsby Functions](https://www.gatsbyjs.com/docs/reference/functions/) open up a whole new world for front-end developers as they provide a way to write and use server-side code without the hassle of maintaining a server. Uses for Serverless Functions range from Newsletter signups with [ConvertKit](https://convertkit.com/), sending an email using [SendGrid](https://sendgrid.com/), saving data in a database like [Fauna](https://fauna.com/), or in this case, accepting secure payments using [Stripe](https://stripe.com/) &mdash; the list is quite frankly endless!

Third-party services like the ones mentioned above will only accept requests that are sent server-side. There’s a number of reasons for this but using secure or private keys is typically one. Using these keys server-side means they’re not exposed to the client (browser) and can’t be abused, and it’s here where Gatsby’s Serverless Functions can help.

[Gatsby](https://www.gatsbyjs.com/) provides the same logical approach to Serverless Functions as they do with pages. For example, website pages are located in `src/pages` and Serverless Functions are located in `src/api`.

Naturally, there’s slightly more to it than that but Gatsby’s developer experience is both logical and consistent, and I for one absolutely love that!

## Same Origin Functions

Nine times out of ten when working with Serverless Functions you’ll be using them the way they were supposed to be used, E.g, your website uses its own functions. I call this usage **Same Origin Functions** or SOF’s for short. In this scenario both the Front-end and the API are deployed to the same origin, E.g [www.my-website.com](www.my-website.com), and [www.my-website.com/api](www.my-website.com/api), and communication between the two is both seamless and, of course, blazing fast!

Here’s a diagram to help illustrate what that looks like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ba8f0a-7d06-4fb0-8664-08d51b8a9f25/1-monetize-open-source-software-gatsby-functions-stripe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ba8f0a-7d06-4fb0-8664-08d51b8a9f25/1-monetize-open-source-software-gatsby-functions-stripe.jpg" width="800" height="450" sizes="100vw" caption="A Gatsby website using its own Serverless Functions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ba8f0a-7d06-4fb0-8664-08d51b8a9f25/1-monetize-open-source-software-gatsby-functions-stripe.jpg'>Large preview</a>)" alt="Diagram of same origin function" >}}

## Cross-Origin Functions

There are, however, at least two scenarios I’ve encountered where I’ve needed what I’ve been calling “Cross-Origin Functions” (or COF’s for short). The two scenarios where I’ve needed COF’s are as follows:

1. I need server-side capabilities but the origin website can’t run Serverless Functions.
2. The Serverless Function is used by more than one origin.

**Note**: *Using Gatsby isn’t the only way to write Serverless Functions but more on that in a moment.*

I first experimented with this approach in November 2020 before the release of Gatsby Functions and used Netlify Functions to provide server-to-server communications with the Twitter API and my Gatsby blog and commercial portfolio. You can read about this approach here: [Use Netlify Functions and the Twitter API v2 as a CMS for your Gatsby blog](https://paulie.dev/posts/2020/11/gatsby-netlify-twitter/).

After the release of Gatsby Functions in June 2021 I refactored the above to work with Gatsby Functions and here’s a little more information about how I went about it and why: [Using Gatsby Functions as an abstracted API](https://paulie.dev/posts/2021/06/gatsby-abstracted-functions/).

Here’s a diagram to better illustrate the general approach.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d07d29-6fe4-4b5e-9040-0e1fea0fd493/2-monetize-open-source-software-gatsby-functions-stripe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d07d29-6fe4-4b5e-9040-0e1fea0fd493/2-monetize-open-source-software-gatsby-functions-stripe.jpg" width="800" height="450" sizes="100vw" caption="Two websites using a Gatsby API’s Serverless Functions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d07d29-6fe4-4b5e-9040-0e1fea0fd493/2-monetize-open-source-software-gatsby-functions-stripe.jpg'>Large preview</a>)" alt="Diagram of cross origin function" >}}

In the above diagram `website-1.com` is built with Gatsby and *could* have used Serverless Functions (but doesn’t) and `website-2.com` is built using something that has no Serverless Function capabilities.

**Note**: *In both cases, they both need to use the same third-party service so it makes sense to abstract this functionality into a standalone API.*

The example standalone API (`my-api.com`) is also a Gatsby site and has Serverless Function capabilities, but more importantly, it allows websites from other origins to use its Serverless Functions.

I know what you’re thinking: CORS! Well, sit tight. I’ll cover this shortly. 

{{% feature-panel %}}

## 💰 Monetizing MDX Embed

This was the situation I found myself in with MDX Embed. The documentation website for this project is built using [Storybook](https://storybook.js.org/). Storybook has no serverless capabilities but I really needed server-to-server communication. My solution? I created a standalone API called [Paulie API](https://paulieapi.gatsbyjs.io/).

### Paulie API

Paulie API (like the example standalone API mentioned above) can accept requests from websites of different origins and can connect to a number of different third-party services, one of which is Stripe.

To enable Stripe payments from MDX Embed, I created an `api/make-stripe-payment` endpoint on Paulie API which can pass the relevant information from MDX Embed through its own Serverless Function and on to the Stripe API to create a “checkout”. You can [see the src code here](https://github.com/PaulieScanlon/paulie-api/blob/main/src/api/make-stripe-payment.js).

Once a checkout has been successfully created, the Stripe API returns a URL. This URL is passed back to MDX Embed which opens a new window in the browser where “customers” can securely enter their payment details on a Stripe webpage... and boom! You get paid!

Here’s a diagram that better illustrates how this works:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76efecc6-ff6b-49d0-b522-b71da1b92f2d/3-monetize-open-source-software-gatsby-functions-stripe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76efecc6-ff6b-49d0-b522-b71da1b92f2d/3-monetize-open-source-software-gatsby-functions-stripe.jpg" width="800" height="450" sizes="100vw" caption="MDX Embed connecting to the Stripe API via Paulie API’s Serverless Functions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76efecc6-ff6b-49d0-b522-b71da1b92f2d/3-monetize-open-source-software-gatsby-functions-stripe.jpg'>Large preview</a>)" alt="Diagram of MDX Embed using Paulie API" >}}

This approach is the same as mentioned above where [https://mdx-embed.com](https://mdx-embed.com) sends requests to [https://paulieapi.gatsbyjs.io](https://paulieapi.gatsbyjs.io) which in turn connects to the Stripe API using server-to-server communication. But before we go too much further, it’s worth explaining why I didn’t use [`react-stripe-js`](https://github.com/stripe/react-stripe-js).

### `react-stripe-js`

[`react-stripe-js`](https://github.com/stripe/react-stripe-js) is a client-side (browser) toolkit that allows you to create Stripe checkouts and elements in your React project. With react-stripe-js you can set up a method for accepting payments securely without the need for server-side communication, but… and there is a but. I wanted to implement “Pay what you want” contributions. Allow me to explain.

Here’s a screenshot of the MDX Embed “product” that I’ve set up in my Stripe dashboard. Notice the price is $1.00.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4c8934-ae67-4127-b616-c6a941eb6829/4-monetize-open-source-software-gatsby-functions-stripe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4c8934-ae67-4127-b616-c6a941eb6829/4-monetize-open-source-software-gatsby-functions-stripe.jpg" width="800" height="450" sizes="100vw" caption="Stripe dashboard product section. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4c8934-ae67-4127-b616-c6a941eb6829/4-monetize-open-source-software-gatsby-functions-stripe.jpg'>Large preview</a>)" alt="Screenshot of Stripe dashboard with a price of $1.00 for the MDX Embed Product" >}}

If I’d used react-stripe-js to enable payments all “customers” would be asked to pay the same amount. In this case, it’s only $1.00 and that’s not gonna pay the bills is it!

To enable “Pay what you want” (e.g. a nominal amount chosen by a “customer”), you have to dive a little deeper and use server-to-server communication and send this amount to the Stripe API using a custom HTTP request. This is where I'm using a Gatsby Function and I pass in a dynamic value which will then be used to create the “checkout” experience and overwrite the price defined in my Stripe dashboard.

On MDX Embed, I’ve added an HTML `<input type="number" />` which allows “customers” to set an amount rather than paying a predefined amount &mdash; if only all e-commerce were like this!

Here’s a little video I made that shows how MDX Embed, Paulie API and the Stripe API all work together:

{{< vimeo id="605497778" caption="How MDX Embed, Paulie API and the Stripe API work together to enable “Pay what you want”." breakout="true" >}}

By passing the input value from MDX Embed to Paulie API which in turn connects to the Stripe API I'm able to create a “dynamic” checkout.

**Note**: *This now means that “customers” can decide what the project is worth to them and set an appropriate amount to contribute.*

I’d like to mention [Benedicte Raae](https://twitter.com/raae) at this point who first showed me this approach during her fabulous *Summer Functions* course. You can find out more by visiting [Queen Raae Codes](https://queen.raae.codes/). (*Thanks Benedicte, you’re the best!*)

{{% ad-panel-leaderboard %}}

## Let’s Talk About CORS

By default, Gatsby Serverless Functions won’t be blocked by CORS since the Front-end and the API are deployed to the same origin. When developing Cross-Origin Functions, however, you’ll need to configure your API so it accepts requests from origins different to that of its own.

Here’s a code snippet to show how I handle CORS in the `api/make-stripe-payment` endpoint:

<pre><code class="language-javascript">// src/api/make-stripe-payment

const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY)
import Cors from 'cors'

const allowedOrigins = [
  'https://www.mdx-embed.com',
  'https://paulie.dev',
]


const cors = Cors({
  origin: (origin, callback) =&gt; {
    if (allowedOrigins.includes(origin)) {
      callback(null, true)
    } else {
      callback(new Error())
    }
  },
})

const runCorsMiddleware = (req, res) =&gt; {
  return new Promise((resolve, reject) =&gt; {
    cors(req, res, (result) =&gt; {
      if (result instanceof Error) {
        return reject(result)
      }
      return resolve(result)
    })
  })
}

export default async function handler(req, res) {
  const { success_url, cancel_url, amount, product } = req.body

  try {
    await runCorsMiddleware(req, res)

    try {
      const session = await stripe.checkout.sessions.create({
        success_url: success_url,
        cancel_url: cancel_url,
        payment_method_types: ['card'],
        line_items: [
          {
            quantity: 1,
            price_data: {
              unit_amount: amount * 100,
              currency: 'usd',
              product: product,
            },
          },
        ],
        mode: 'payment',
      })

      res.status(200).json({ message: '🕺 Stripe checkout created ok', url: session.url })
    } catch (error) {
      res.status(500).json({ message: '🚫 Stripe checkout error' })
    }
  } catch (error) {
    res.status(403).json({ message: '🚫 Request blocked by CORS' })
  }
}</code></pre>

In the above code snippet you should be able to see I’ve defined an array of `allowedOrigins`, these are the only origins allowed to use this endpoint. Requests from any other origin will receive a status code `403` and a message of `🚫 Request blocked by CORS`.

This function also accepts a number of body parameters, one of which is the `amount` the “customer” has decided to pay, this is the value from the HTML input on the MDX Embed site. You’ll also notice the `product` parameter, this is the product id defined in my Stripe dashboard and how the Stripe API creates the correct “checkout” URL. Passing this value as a body parameter rather than hardcoding it in the function allows me to re-use this endpoint for other Stripe products.

{{% ad-panel-leaderboard %}}

## 🍋 Is The Juice Worth The Squeeze?

I’ve mentioned a few things along the way for why I decided to go this route. After all, it may well seem like a more complicated way to use Serverless Functions but I have my reasons, and I think it is worth it. Here’s why. 👇

Paulie API is both a Cross-Origin API and a documentation site. Naturally, if you’re going to write an API it has to be documented right?

This is where it works in my favor to use Gatsby to power my API because along with Serverless capabilities Paulie API is also a Gatsby website, and because it’s actually a website I can fill it with content and make it look pretty, but wait there’s more…

**Note:** *Paulie API is also an interactive API playground!* 😵

Each function has a `▶ Run in browser` link. This takes you to a page on the site where you can interact with the function. It serves as both a useful testing ground while I'm developing the function and an easy way to demonstrate how the function works, docs are good, interactive docs are better!

I also use this API to provide similar server-side functionality for my other websites. Take a look at the [About page](https://paulieapi.gatsbyjs.io/about) where I’ve documented which of my sites use which functions, and here’s a diagram to illustrate how it all currently comes together.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f8b3462-e9b3-447d-a9da-aa0e3aa7af78/5-monetize-open-source-software-gatsby-functions-stripe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f8b3462-e9b3-447d-a9da-aa0e3aa7af78/5-monetize-open-source-software-gatsby-functions-stripe.jpg" width="800" height="450" sizes="100vw" caption="Paulie API cross origin function capabilities. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f8b3462-e9b3-447d-a9da-aa0e3aa7af78/5-monetize-open-source-software-gatsby-functions-stripe.jpg'>Large preview</a>)" alt="Diagram of Paulie API’s cross origin functions" >}}

You should see from the above diagram that [https://paulie.dev](https://paulie.dev) also uses the Stripe endpoint. I’ve used the same approach as with MDX Embed to enable the “Pay what you want” functionality. It’s a small thing, but since the `make-stripe-payment` endpoint is already written and working, I can re-use it and avoid duplicating this functionality.

The [https://paulie.dev](https://paulie.dev) website also has its own Gatsby Serverless Functions which I use to post user reactions to Fauna and capture Newsletter signups. This functionality is unique to this site so I haven’t abstracted this yet. However, if I wanted newsletter sign-ups on [https://www.pauliescanlon.io](https://www.pauliescanlon.io), this would be the point where I migrate the function over to Paulie API.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/235c79d0-b1a4-45a3-9325-6158e479cee1/6-monetize-open-source-software-gatsby-functions-stripe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/235c79d0-b1a4-45a3-9325-6158e479cee1/6-monetize-open-source-software-gatsby-functions-stripe.jpg" width="800" height="450" sizes="100vw" caption="paulie.dev’s “Pay what you want” section. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/235c79d0-b1a4-45a3-9325-6158e479cee1/6-monetize-open-source-software-gatsby-functions-stripe.jpg'>Large preview</a>)" alt="Screenshot of paulie.dev “Pay what you want” user interface" >}}

## Abstraction

This might seem like a step backwards to abstract your Serverless Functions. After all, one of the coolest things about going serverless is that both your front and back-end code are live in the same place. As I’ve shown, there are times where abstracting makes sense &mdash; to me anyway.

I’m certainly benefitting from using this approach and plan to further develop my API to provide more functionality to a number of my own websites, but if making money from open-source is of interest to you and your site isn’t built using Gatsby, this approach may well be the answer you were looking for.

Wanna get started with Gatsby Functions? Check out the [Gatsby Functions docs](https://www.gatsbyjs.com/docs/reference/functions/) to get going!

### Further Reading

If you’re interested in learning more about Serverless Functions I’d recommend:

- [Swizec Teller](https://twitter.com/Swizec)’s book, “[Serverless Handbook For Frontend Engineers](https://serverlesshandbook.dev/)”
- Benedict’s [Summer Functions course](https://www.crowdcast.io/raae)
- ...and, of course, [the Gatsby docs](https://www.gatsbyjs.com/docs/reference/functions)

### FuncJam

From August 17 to September 30, the Gatsby folks are running a community competition with some absolutely mega prizes to be won. If there’s still time, then [pop on over to FuncJam](https://www.gatsbyjs.com/func-jam-21) and join in. Also, [check out the Byte-size section of this blog post](https://www.gatsbyjs.com/blog/the-gatsby-funcjam-challenge); it contains helpful videos and links to a number of example functions.

Thanks for reading, and if you’d like to discuss anything mentioned in this article, leave a comment below or [find me on Twitter](https://twitter.com/PaulieScanlon).

{{< signature "vf, yk, il" >}}
