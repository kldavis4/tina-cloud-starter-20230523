---
title: 'How To Build An Accessible Front-End Application With Chakra UI And Nuxt.js'
slug: accessible-front-end-application-chakra-ui-nuxtjs
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d843d095-1886-4361-b2c4-4d72f4d8ed00/accessible-front-end-application-chakra-ui-nuxtjs.png
date: 2020-07-20T10:00:00.000Z
summary: >-
  In this article, we are going to be looking at how to use Chakra UI and NuxtJS in building accessible front-end applications. In order to follow along, you should be familiar with using the progressive front-end framework Vue.js with Nuxt. If not, see the [Vue.js](https://vuejs.org/) and [NuxtJS](https://nuxtjs.org/) docs to get started.
description: >-
  In this article, we are going to be looking at how to use Chakra UI and NuxtJS in building accessible front-end applications.
categories:
  - Accessibility
  - UI
  - Vue
  - Nuxt.js
  - JavaScript
---

For many people, the web is an essential part of their daily lives. They use it at work, home, and even on the road. Web accessibility means people with disabilities can use the web equally. So it’s crucial for developers and organizations building on the web to build inclusivity and accessibility into their applications. 

In order to make the web more accessible, there are a couple of best practices and standards that you will have to implement in your applications, such as adhering to the following:

* [Section 508](https://www.section508.gov/);
* [Assistive Technology Act](https://www.afb.org/aw/6/1/14652);
* [Americans with Disabilities Act(ADA)](https://adata.org/learn-about-ada);
* [WCAG 2.0 (A & AA Guidelines)](https://www.w3.org/TR/WCAG20/);
* [BBC Mobile Accessibility Guidelines](https://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile);
* [WAI-ARIA](https://www.w3.org/TR/wai-aria-practices/) (**W**eb **A**ccessibility **I**nitiative&ndash;**A**ccessible **R**ich **I**nternet **A**pplications) practices.

Learning to implement these standards can seem like a daunting task when you factor in project deadlines and other constraints that you have to work with as a developer. In that light, let me introduce you to a UI design system that was built to help you make your web applications accessible.

## Chakra UI

Chakra UI is a [design system](https://uxdesign.cc/everything-you-need-to-know-about-design-systems-54b109851969) and UI framework created by [Segun Adebayo](https://twitter.com/thesegunadebayo). It was created with simplicity, modularity, composability, and accessibility in mind. Chakra UI gives you all the building blocks needed to create accessible front-end applications.

**Note**: *While Chakra UI depends on CSS-in-JS under the hood, you don’t need to know it in order to use the library.*

Though the framework was originally created for React, [Jonathan Bakebwa](https://twitter.com/codebender828) spear-headed the porting to Vue. So Vuejs/NuxtJS developers can now utilize Chakra UI to create accessible web applications.

## Features Of Chakra UI

Chakra UI was created with the following principles in mind:

- **Style props**  
Chakra UI makes it possible to style components or override their styles by using [props](https://vuejs.org/v2/guide/components-props.html). This reduces the need for stylesheet or inline styles. Chakra UI achieves this level of flexibility by using [Styled Systems](https://styled-system.com/) under the hood.
- **Composition**  
Components in Chakra UI have been broken down into smaller parts with minimal props to keep complexity low, and compose them together. This will ensure that the styles and functionality are flexible and extensible. For example, you can use the `CBox` and `CPseudoBox` components to create new components.
- **Accessible**  
Chakra UI components follow the [WAI-ARIA guidelines specifications](https://www.w3.org/TR/wai-aria-practices/) and have the right aria-* attributes. You can also find the accessibility report of each authored component in a file called `accessibility.md`. See the [accessibility report](https://github.com/chakra-ui/chakra-ui-vue/blob/master/packages/chakra-ui-core/src/CAccordion/accessibility.md) for the `CAccordion` component.
- **Themeable**  
Chakra UI affords you the ability to easily reference values from your theme throughout your entire application, on any component.
- **Dark mode support**  
Most components in Chakra UI are dark mode compatible right out of the box.

## How Chakra UI Supports Accessibility

One of the core principles behind the creation of Chakra UI is **accessibility**. With that in mind, all components in Chakra UI comes out of the box with support for accessibility by providing:

- Keyboard Navigation &mdash; useful for users with motor skills disabilities,
- Focus Management,
- aria-* attributes which are needed by screen readers,
- Focus trapping and restoration for modal dialogs.

{{% feature-panel %}}

## Getting Started With Chakra UI And Nuxt 

**Note**: *To use Chakra UI with Vue.js see the [Getting Started guide](https://vue.chakra-ui.com/getting-started).*

For our demo project, we will be building *Chakra-ui explorer* &mdash; an accessible single-page web application to search Chakra UI components.

- [See live project on Netlify&nbsp;&rarr;](https://chakra-ui-explorer.netlify.app/)

### Getting Started With Chakra-ui Explorer

Assuming you already have NPM installed, create a new Nuxt application by running:

<pre><code class="language-bash">$ npx create-nuxt-app chakra-ui-explorer
</code></pre>

Or if you prefer in yarn, then run:

<pre><code class="language-bash">$ yarn create nuxt-app chakra-ui-explorer
</code></pre>

Follow the installation prompt to finish creating your Nuxt application.

## Setting Up Chakra UI

Chakra UI uses [Emotion](https://emotion.sh/docs/introduction) for handling component styles. So to get started with Chakra UI, you will need to install Chakra UI alongside Emotion as a peer dependency. For this project, we will be using the official Nuxt modules for both Chakra UI and Emotion which will reduce the friction in getting started with Chakra UI. Let’s add them to our project by running the following command:

<pre><code class="language-bash">npm i @chakra-ui/nuxt @nuxtjs/emotion
</code></pre>

**Note**: *`@nuxtjs/emotion` allows your component styles to be generated and injected in the server build.*

After installing both modules, you will need to register them in the `nuxt.config.js` file under the modules array option:

<pre><code class="language-javascript">// nuxt.config.js
modules: ['@chakra-ui/nuxt', '@nuxtjs/emotion'],
</code></pre>

<p class="c-pre-sidenote--left">To complete our setup process of Chakra UI, we need to touch our default layout component in <code>layouts/</code> and add <code>CThemeProvider</code>, <code>CColorModeProvider</code>, and <code>CReset</code> components from Chakra UI.<br /><br />It is recommended thatyou use the <code>CReset</code> component to ensure all components provided by Chakra UI work correctly.</p><p class="c-sidenote c-sidenote--right">The <code>CThemeProvider</code> component will make your theme available to every part of your application, while the <code>CColorModeProvider</code> component is responsible for handling our application’s color mode which can be in one of two states: light or dark. Finally, the <code>CReset</code> component will remove all browser default styles.</p>

Let’s add the aforementioned components in `layouts/default.vue`. In our template section, let’s add this:

<pre><code class="language-html">&lt;!-- layouts/default.vue --&gt;
&lt;template&gt;
  &lt;div class="container"&gt;
    &lt;c-theme-provider&gt;
      &lt;c-color-mode-provider&gt;
        &lt;c-box as="section"&gt;
          &lt;c-reset /&gt;
          &lt;nuxt /&gt;
        &lt;/c-box&gt;
      &lt;/c-color-mode-provider&gt;
    &lt;/c-theme-provider&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>

Then in our script section, we will import and register the components like so:

<div class="break-out">

<pre><code class="language-javascript">&lt;script&gt;
import { CThemeProvider, CColorModeProvider, CReset, CBox } from '@chakra-ui/vue'

export default {
  name: 'DefaultLayout',
  components: {
    CThemeProvider,
    CColorModeProvider,
    CReset,
    CBox
  }
}
&lt;/script&gt;
</code></pre>
</div>

Your `default.vue` layout component should look like this:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
   &lt;div class="container"&gt;
    &lt;c-theme-provider&gt;
      &lt;c-color-mode-provider&gt;
        &lt;c-box as="section"&gt;
          &lt;c-reset /&gt;
          &lt;nuxt /&gt;
        &lt;/c-box&gt;
      &lt;/c-color-mode-provider&gt;
    &lt;/c-theme-provider&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import { CThemeProvider, CColorModeProvider, CReset, CBox } from '@chakra-ui/vue'

export default {
  name: 'DefaultLayout',
  components: {
    CThemeProvider,
    CColorModeProvider,
    CReset,
    CBox
  }
}
&lt;/script&gt;
</code></pre>
</div>

**Note**: *Notice I am wrapping both `<c-reset />` and `<nuxt />` components in a `c-box` component.*

{{% ad-panel-leaderboard %}} 

## Setting Your Application Theme

Chakra UI allows you the ability to set a theme for your application. By ‘theme’, I mean the setting of your application’s color palette, type scale, font stacks, breakpoints, border-radius values, and so on. Since colors and contrast are vital components of accessibility, it’s important to use colors that are easily perceived.

Out of the box Chakra UI ships with a [default theme](https://vue.chakra-ui.com/theme) object that affords for most of your application needs in terms of colors, fonts, and so on. The default theme is set up with contrast in mind which allows for the easily toggling of color modes (more on this later).

Chakra UI, however, allows you to extend or completely replaced the default theme. This is possible by accepting a theme object based on the [Styled System Theme Specification](https://system-ui.com/theme/).
 
The values in the theme object are automatically available for use in your application. For example, the colors specified in `theme.colors` can be referenced by the `color`, `borderColor`, `backgroundColor`, `fill`, `stroke`,  and `style` props in your components.

To personalize your application, you can override the default theme provided by Chakra UI or set new values in it. To do that, the Chakra UI Nuxt module exposes a `chakra` object which will take in an `extendTheme` property which takes an object. The object given to `extendTheme` will be recursively merged to the Chakra UI default theme object. Let’s add our brand color palette to Chakra so we can use it in our application.

**Note**: *Chakra UI recommends adding color palette into the colors object of your theme using keys from 50 — 900. You can use web tools like [coolors](https://coolors.co/app) and [palx](https://palx.jxnblk.com/) to generate these palettes.*

For our demo homepage, I will be using a brand color of lime. To make Chakra UI aware of this color, I’ll create a `customeTheme` object in a folder called `chakra`(you can call it whatever you want) in the root of my project’s directory. In this object, I will define our brand color palette. 

Create a file called `theme.js` in the folder you created and then add the following snippet:

<pre><code class="language-javascript">// ./chakra/theme.js

const customTheme = {
  colors: {
    brand: {
      50: '#f6fcee',
      100: '#e2f4c8',
      200: '#cbec9e',
      300: '#b2e26e',
      400: '#94d736',
      500: '#75c800',
      600: '#68b300',
      700: '#599900',
      800: '#477900',
      900: '#294700'
    }
  }
}

module.exports = customTheme
</code></pre>

Now let’s merge our custom theme to Chakra UI. We do that in `nuxt.config.js`. First, we need our custom theme object:

<pre><code class="language-javascript">import customTheme from './chakra/theme'
</code></pre>

Next, we have to specify the `chakra` key provided by the Chakra UI Nuxt module and pass in `customTheme` to the `extendTheme` property:

<pre><code class="language-javascript">chakra: {
  extendTheme: customTheme
},
</code></pre>

Your `nuxt.config.js` file should look like this:

<div class="break-out">

<pre><code class="language-javascript">// nuxt.config.js
import customTheme from './chakra/theme'

export default {
  mode: 'spa',
  /&#42;
   &#42; Headers of the page
   &#42;/
  head: {
    title: process.env.npm_package_name || '',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      {
        hid: 'description',
        name: 'description',
        content: process.env.npm_package_description || ''
      }
    ],
    link: [{ rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }]
  },
  /&#42;
   &#42; Customize the progress-bar color
   &#42;/
  loading: { color: '#fff' },
  /&#42;
   &#42; Global CSS
   &#42;/
  css: [],
  /&#42;
   &#42; Plugins to load before mounting the App
   &#42;/
  plugins: [],
  /&#42;
   &#42; Nuxt.js dev-modules
   &#42;/
  buildModules: [
    // Doc: https://github.com/nuxt-community/eslint-module
    '@nuxtjs/eslint-module'
  ],
  /&#42;
   &#42; Nuxt.js modules
   &#42;/
  modules: [
    '@chakra-ui/nuxt',
    '@nuxtjs/emotion'
  ],

  chakra: {
    extendTheme: customTheme
  },
  /&#42;
   &#42; Build configuration
   &#42;/
  build: {
    /&#42;
     &#42; You can extend webpack config here
     &#42;/
    extend (config, ctx) {}
  }
}
</code></pre>
</div>

When you run your application with `npm run dev`, your homepage should look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab86e120-d73b-45b0-a1c1-0064a0063b55/1-accessible-front-end-application-chakra-ui-nuxtjs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab86e120-d73b-45b0-a1c1-0064a0063b55/1-accessible-front-end-application-chakra-ui-nuxtjs.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab86e120-d73b-45b0-a1c1-0064a0063b55/1-accessible-front-end-application-chakra-ui-nuxtjs.png'>Large preview</a>)" alt="A demo application showing Chakra UI and NuxtJS" >}}

Now that we have successfully installed Chakra UI and added our application’s custom theme, let’s begin building out Chakra-ui explorer.

### Creating Our Main Navigation

We want our navigation to have our brand name, in this case, it will be **Chakra-ui explorer**, 2 navigation links: **Documentation** and **Repo**, and a button which is responsible for toggling our color mode. Let’s create a new component under the `components` directory called `NavBar` in which we’ll create our application’s main navigation using Chakra UI.

Let’s do this. Add the following snippet to `NavBar.vue`:

<pre><code class="language-html">&lt;template&gt;
  &lt;c-box
    as="nav"
    h="60px"
    px="4"
    d="flex"
    align-items="center"
    shadow="sm"
  &gt;
    &lt;c-link
      as="nuxt-link"
      to="/"
      color="brand.700"
      font-weight="bold"
      :_hover="{ color: 'brand.900' }"
    &gt;
      Chakra-ui Explorer
    &lt;/c-link&gt;

    &lt;c-box
      as="ul"
      color="gray.500"
      d="flex"
      align-items="center"
      list-style-type="none"
      ml="auto"
    &gt;
      &lt;c-box as="li" mr="8"&gt;
        &lt;c-link
          color="gray.500"
          :_hover="{ color: 'brand.400' }"
          is-external
          href="https://vue.chakra-ui.com"
        &gt;
          Documentation
        &lt;/c-link&gt;
      &lt;/c-box&gt;
      &lt;c-box as="li" mr="8"&gt;
        &lt;c-link
          color="gray.500"
          :_hover="{ color: 'brand.400' }"
          is-external
          href="https://github.com/chakra-ui/chakra-ui-vue"
        &gt;
          Repo
        &lt;/c-link&gt;
      &lt;/c-box&gt;
      &lt;c-box as="li"&gt;
        &lt;c-icon-button
          variant="ghost"
          variant-color="gray[900]"
          aria-label="Switch to dark mode"
          icon="moon"
        /&gt;
      &lt;/c-box&gt;
    &lt;/c-box&gt;
  &lt;/c-box&gt;
&lt;/template&gt;

&lt;script&gt;
import { CBox, CLink, CIconButton } from '@chakra-ui/vue'
export default {
  name: 'NavBar',
  components: {
    CBox,
    CLink,
    CIconButton
  }
}
&lt;/script&gt;
</code></pre>

Next, we need to import this component in our default layout component &mdash; `default.vue` and add it to our template so overall our default layout should look like this:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="container"&gt;
    &lt;c-theme-provider&gt;
      &lt;c-color-mode-provider&gt;
        &lt;c-box as="section"&gt;
          &lt;c-reset /&gt;
          &lt;nav-bar /&gt;
          &lt;nuxt /&gt;
        &lt;/c-box&gt;
      &lt;/c-color-mode-provider&gt;
    &lt;/c-theme-provider&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
import { CThemeProvider, CColorModeProvider, CReset, CBox } from '@chakra-ui/vue'
import NavBar from '@/components/NavBar'
export default {
  name: 'DefaultLayout',
  components: {
    CThemeProvider,
    CColorModeProvider,
    CReset,
    CBox,
    NavBar
  }
}
&lt;/script&gt;
</code></pre>
</div>

When you run your application now, you’ll get to see this:

{{< vimeo id="433930000" breakout="true" >}}

You can see that the navigation is already accessible without even specifying it. This can only be seen when you hit the <kbd>Tab</kbd> key on your keyboard; Chakra UI handles focus management while you can focus on each link on the navigation menu.

### The `as` Prop

From our `NavBar.vue`’s snippet above, you will notice the `as` prop. This is a feature available to Chakra UI components that allows you to pass an HTML tag or another component to be rendered as the base tag of the component along with all its styles and props. So when we did:

<pre><code class="language-html">&lt;c-box as="li"&gt;
      &lt;c-icon-button
        variant="ghost"
        variant-color="gray[900]"
        aria-label="Switch to dark mode"
        icon="moon"
      /&gt;
&lt;/c-box&gt;
</code></pre>

we are asking Chakra UI to render an `<li>` element and place a button component inside it. You can also see us use that pattern here:

<pre><code class="language-html"> &lt;c-link 
     as="nuxt-link"
     to="/" 
     color="brand.700" 
     font-weight="bold" 
     :_hover="{ color : 'brand.900' }"&gt;
      ChakraMart
 &lt;/c-link&gt;
</code></pre>
 
In the above case, we are asking Chakra UI to render the Nuxt’s &lt;nuxt-link /&gt; component.

The `as` prop gives you the power to use the right(or wrong) element for the context of your markup. What this means, is you can leverage it to build your application template using [semantic markups](https://www.w3schools.com/html/html5_semantic_elements.asp) which will make your application more meaningful to screen readers. So instead of using a generic `div` element for the main content of your application, with the `as` prop you can render a `main` element telling screen readers that this is the main content of your application.

**Note**: *Check out the documentation for all [props](https://vue.chakra-ui.com/style-props) exposed by Chakra UI components. Also, take a closer look at how the brand color in `chakra/theme.js` was specified. You can see from the snippet above that we’re using it as any of the [colors](https://vue.chakra-ui.com/theme) that Chakra UI provides. Another thing to be aware of is the `moon` icon that we used for the [`CIconButton`](https://vue.chakra-ui.com/iconbutton) on our NavBar. The `moon` icon is one of the [default icons](https://vue.chakra-ui.com/icon) that Chakra UI provides out of the box.*

{{% ad-panel-leaderboard %}} 

## Color Mode

One of the features of Chakra UI is color mode support. And you can tell from the use of the `moon` icon in Chakra-ui explorer’s navigation, we plan on integrating dark mode. So instead of leaving it for last, let’s get it over with and wire it up right now. To do this, `CColorModeProvider` using Vue’s [provide/inject](https://vuejs.org/v2/api/#provide-inject), provides,  `$chakraColorMode` and `$toggleColorMode` functions. `$chakraColorMode` returns the current color mode of your application while `$toggleColorMode` toggles the color mode from `light` to `dark` and vice versa. To use these two functions, we’ll need to inject them into the `NavBar.vue` component. Let’s do this below in the `<script />` section:

<pre><code class="language-javascript">&lt;script&gt;
&lt;script&gt;
import { CBox, CLink, CIconButton } from '@chakra-ui/vue'
export default {
  name: 'NavBar',
  inject: ['$chakraColorMode', '$toggleColorMode'],
  components: {
    CBox,
    CLink,
    CIconButton
  },
}
&lt;/script&gt;
</code></pre>

Let’s create a computed property to return the color mode:

<pre><code class="language-javascript">...
 computed: {
    colorMode () {
      return this.$chakraColorMode()
    }
  }
</code></pre>

Now that we have injected both functions in `NavBar.vue` let’s modify the toggle color mode button. We’ll start with the icon so that it shows a different icon depending on the color mode. Our `CIconButton` component now looks like this at this state:

<pre><code class="language-html">&lt;c-icon-button
  variant="ghost"
  variant-color="gray[900]"
  aria-label="Switch to dark mode"
  :icon="colorMode == 'light' ? 'moon' : 'sun'"
/&gt;
</code></pre>

Currently, we are using an `aria-label` attribute to tell screen-readers to Switch to dark mode. Let’s modify this to support both light and dark mode:

<div class="break-out">

<pre><code class="language-html">&lt;c-icon-button
  variant="ghost"
  variant-color="gray[900]"
  :aria-label="`Switch to ${colorMode == 'light' ? 'dark : 'light'} mode`"
   :icon="colorMode == 'light' ? 'moon' : 'sun'"
/&gt;
</code></pre>
</div>

Lastly, we will add a click event handler on the button to toggle the color mode of our application using the `$toggleColorMode` function. Like so:

<div class="break-out">

<pre><code class="language-html">&lt;c-icon-button
   variant="ghost"
   variant-color="gray[900]"
   :aria-label="`Switch to ${colorMode == 'light' ? 'dark' : 'light'} mode`"
   :icon="colorMode == 'light' ? 'moon' : 'sun'"
   @click="$toggleColorMode"
/&gt;
</code></pre>
</div>

To test if our color mode set up is working, I’ll add an interpolation of the color mode and a text next to the `CIconButton` toggling our color mode. Like so:

<div class="break-out">

<pre><code class="language-html">&lt;c-box as="li"&gt;
  &lt;c-icon-button
    variant="ghost"
    variant-color="gray[900]"
    :aria-label="`Switch to ${colorMode == 'light' ? 'dark' : 'light'} mode`"
    :icon="colorMode == 'light' ? 'moon' : 'sun'"
    @click="$toggleColorMode"
  /&gt;
  Current mode: {{ colorMode }}
&lt;/c-box&gt;
</code></pre>
</div>

Here is what our app currently looks like:

{{< vimeo id="433937922" breakout="true" >}}

So we have done the heavy lifting in setting up color mode in Chakra UI. So now we can style our application based on the color mode. Let’s go to `default.vue` and use the color mode slot prop provided by `CColorModeProvider` to style our application. Let’s modify our template first in `default.vue`.

<pre><code class="language-html">&lt;template&gt;
  &lt;div class="container"&gt;
    &lt;c-theme-provider&gt;
      &lt;c-color-mode-provider #default="{ colorMode }"&gt;
        &lt;c-box
          v-bind="mainStyles[colorMode]"
          w="100vw"
          h="100vh"
          as="section"
        &gt;
          &lt;c-reset /&gt;
          &lt;nav-bar /&gt;
          &lt;nuxt /&gt;
        &lt;/c-box&gt;
      &lt;/c-color-mode-provider&gt;
    &lt;/c-theme-provider&gt;
  &lt;/div&gt;
&lt;/template&gt;
</code></pre>

We are [destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) `colorMode` from the slot props property provided by `CColorModeProvider` and then passing it as a dynamic key to a `mainStyle` object which we will create in a bit. The idea is to use a different set of styles based on the `colorMode` value. I am also using the width and height with the shorthand props &mdash; `w` and `h` respectively to set the width and height of our `CBox` component. Let’s define this `mainStyles` object in our script section:

<div class="break-out">

<pre><code class="language-javascript">&lt;script&gt;
import { CThemeProvider, CColorModeProvider, CReset, CBox } from '@chakra-ui/vue'
import NavBar from '@/components/NavBar'
export default {
  name: 'DefaultLayout',
  components: {
    CThemeProvider,
    CColorModeProvider,
    CReset,
    CBox,
    NavBar
  },
  data () {
    return {
      mainStyles: {
        dark: {
          bg: 'gray.900',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'whiteAlpha.900',
          color: 'gray.900'
        }
      }
    }
  }
}
&lt;/script&gt;
</code></pre>
</div>

Chakra-ui explorer now has dark mode support!

{{< vimeo id="433938703" breakout="true" >}}

Now we have our navigation bar and have successfully set up dark mode support for our application, let’s focus on `index.vue` in our `pages/` directory where the meat of our application can be found. We’ll start off with adding a `CBox` component like so:

<pre><code class="language-html">&lt;c-box
  as="main"
  d="flex"
  direction="column"
  align-items="center"
  p="10" 
&gt;
&lt;/c-box&gt;
</code></pre>

Then we’ll add the [`CInput`](https://vue.chakra-ui.com/input) component inside it. Our `index.vue` page component will then look like this:

<div class="break-out">

<pre><code class="language-javascript">&lt;template&gt;
  &lt;c-box
    as="main"
    d="flex"
    align-items="center"
    direction="column"
    w="auto"
    p="16"
  &gt;
    &lt;c-input placeholder="Search components..." size="lg" mb="5" is-full-width /&gt;
  &lt;/c-box&gt;
&lt;/template&gt;

&lt;script&gt;
import { CBox, CInput } from '@chakra-ui/vue'
export default {
  components: {
    CBox,
    CInput
  }
}
&lt;/script&gt;
</code></pre>
</div>

Here is how our application looks like now:

{{< vimeo id="433939833" breakout="true" >}}

You can see from the above screencast how the `CInput` element automatically knows when it’s in dark mode and adjust accordingly even though we didn’t explicitly set that. Also, the user can hit the tab key to focus on that `CInput` component.

## Adding The Components’ List

So the idea of the Chakra-ui explorer (as stated earlier) is to show the user all of the available components in Chakra UI so that we can have a list of those components as well as the links that will take the user to the documentation of the component. To do this, I will create a folder called `data` at the root of our project’s directory then create a file called `index.js`. In `index.js`, I will export an array of objects which will contain the names of the components. Here is how  the file should look like:

<pre><code class="language-javascript">// ./data/index.js

export const components = [
  {
    name: 'Accordion'
  },
  {
    name: 'Alert'
  },
  {
    name: 'AlertDialog'
  },
  {
    name: 'AspectRatioBox'
  },
  {
    name: 'AspectRatioBox'
  },
  {
    name: 'Avatar'
  },
  {
    name: 'Badge'
  },
  {
    name: 'Box'
  },
  {
    name: 'Breadcrumb'
  },
  {
    name: 'Button'
  },
  {
    name: 'Checkbox'
  },
  {
    name: 'CircularProgress'
  },
  {
    name: 'CloseButton'
  },
  {
    name: 'Code'
  },
  {
    name: 'Collapse'
  },
  {
    name: 'ControlBox'
  },
  {
    name: 'Divider'
  },
  {
    name: 'Drawer'
  },
  {
    name: 'Editable'
  },
  {
    name: 'Flex'
  },
  {
    name: 'Grid'
  },
  {
    name: 'Heading'
  },
  {
    name: 'Icon'
  },
  {
    name: 'IconButton'
  },
  {
    name: 'IconButton'
  },
  {
    name: 'Input'
  },
  {
    name: 'Link'
  },
  {
    name: 'List'
  },
  {
    name: 'Menu'
  },
  {
    name: 'Modal'
  },
  {
    name: 'NumberInput'
  },
  {
    name: 'Popover'
  },
  {
    name: 'Progress'
  },
  {
    name: 'PseudoBox'
  },
  {
    name: 'Radio'
  },
  {
    name: 'SimpleGrid'
  },
  {
    name: 'Select'
  },
  {
    name: 'Slider'
  },
  {
    name: 'Spinner'
  },
  {
    name: 'Stat'
  },
  {
    name: 'Stack'
  },
  {
    name: 'Switch'
  },
  {
    name: 'Tabs'
  },
  {
    name: 'Tag'
  },
  {
    name: 'Text'
  },
  {
    name: 'Textarea'
  },
  {
    name: 'Toast'
  },
  {
    name: 'Tooltip'
  }
]
</code></pre>

For our implementation to be complete, I will import the above array into `pages/index.vue` and iterate over it to display all the components. Also, we will give the user the ability to filter the components using the search box. Here is the complete implementation:

<div class="break-out">

<pre><code class="language-javascript">// pages/index.vue
&lt;template&gt;
  &lt;c-box
    as="main"
    d="flex"
    align-items="space-between"
    flex-direction="column"
    w="auto"
    p="16"
  &gt;
    &lt;c-input v-model="search" placeholder="Search components..." size="lg" mb="10" is-full-width /&gt;
    &lt;c-grid template-columns="repeat(4, 1fr)" gap="3" p="5"&gt;
      &lt;c-box v-for="(chakraComponent, index) of filteredComponents" :key="index" h="10"&gt;
        {{ chakraComponent.name }}
  
      &lt;c-badge&gt;
          &lt;c-link
            is-external
            :href="lowercase(`https://vue.chakra-ui.com/${chakraComponent.name}`)"
          &gt;
            &lt;c-icon name="info" size="18px" /&gt;
          &lt;/c-link&gt;
        &lt;/c-badge&gt;
      &lt;/c-box&gt;
    &lt;/c-grid&gt;
  &lt;/c-box&gt;
&lt;/template&gt;

&lt;script&gt;
import { CBox, CInput, CGrid, CLink, CBadge, CIcon } from '@chakra-ui/vue'
import { components as chakraComponents } from '../data'
export default {
  components: {
    CBox,
    CInput,
    CGrid,
    CBadge,
    CIcon,
    CLink
  },
  data () {
    return {
      search: ''
    }
  },
  computed: {
    filteredComponents () {
      return chakraComponents.filter((component) =&gt; {
        return this.lowercase(component.name).includes(this.lowercase(this.search))
      })
    }
  },
  methods: {
    lowercase (value) {
      return value.toLowerCase()
    }
  }
}
&lt;/script&gt;
</code></pre>
</div>

And now our application looks like this:

{{< vimeo id="433940773" breakout="true" >}}

You can now see how dark mode is automatic for the component’s list as well as how the focus management is added for the links (by default) to aid accessibility.

## Putting Chakra UI To The Test

Finally, let’s see how our app scores by running the [Lighthouse accessibility](https://web.dev/accessibility-scoring/) test on it. Mind you, this test is based on the [Axe user impact assessment](https://github.com/dequelabs/axe-core/blob/develop/doc/rule-descriptions.md). Below is a screencast of the test. You can also run the test yourself by [following these steps](https://medium.com/accessibility-a11y/do-an-accessibility-audit-using-google-chrome-lighthouse-30ff7887901c).

{{< vimeo id="439910198" breakout="true" >}}

From the screencast above you can see that our Chakra UI app has a score of **85** on the lighthouse accessibility test.

## Conclusion

In this article, we have touched on the need for building accessible interfaces and we have also seen how to use Chakra UI to build accessible applications from the ground up by building an explorer (Chakra-ui explorer) for the Chakra UI components.

- [See the live application on Netlify&nbsp;&rarr;](https://chakra-ui-explorer.netlify.app/)
- [Link to the repo&nbsp;&rarr;](https://github.com/DominusKelvin/chakra-ui-explorer)

{{< signature "ra, yk, il" >}}
