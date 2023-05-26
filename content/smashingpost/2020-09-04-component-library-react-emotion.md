---
title: 'Building A Component Library With React And Emotion'
slug: component-library-react-emotion
author: ademola-adegbuyi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09a7a19-084a-4252-89f2-ab8b168f778c/component-library-react-emotion.png
date: 2020-09-04T10:30:00.000Z
summary: >-
  A component library helps to keep a design consistent across multiple projects. It ensures consistency because any changes made will propagate across the projects that make use of it. In this tutorial, we’ll learn how to build a component library, using Emotion in React to resolve inconsistencies.
description: >-
  A component library helps to keep a design consistent across multiple projects. It ensures consistency because any changes made will propagate across the projects that make use of it. In this tutorial, we’ll learn how to build a component library, using Emotion in React to resolve inconsistencies.
categories:
  - API
  - React
  - JavaScript
---

According to Clearleft, a component library is:

<blockquote>“A collection of components, organised in a meaningful manner, and often (but not necessarily) providing some way to browse and preview those components and their associated assets.”<br /><br />&mdash; “<a href="https://clearleft.com/posts/on-building-component-libraries">On Building Component Libraries</a>,” Clearleft</blockquote>

We’ll learn how to build a component library by making one that comprises four components:

<ol>
  <li><a href="#button-component"><code>Button</code></a><br />A wrapper around the default HTML button</li>
  <li><a href="#box-component"><code>Box</code></a><br />A container (HTML div) with custom properties</li>
  <li><a href="#columns-component"><code>Columns</code></a><br />A container whose children are spaced evenly across the x-axis</li>
  <li><a href="#stack-component"><code>Stack</code></a><br />A container whose children are spaced evenly across the y-axis</li>
</ol>

These components could then be used in whatever application we are working on. We’ll build the component library using React and Emotion.

At the end of this piece, you should be able to create a component library that fits whatever use case you have in mind. This knowledge will come handy when you’re working with a team that needs to make use of reusable components.

First, let’s get started by establishing what the Emotion library is. The documentation explains:

<blockquote>“Emotion is a library designed for writing CSS styles with JavaScript. It provides powerful and predictable style composition in addition to a great developer experience with features such as source maps, labels, and testing utilities.”<br /><br />&mdash; “<a href="https://emotion.sh/docs/introduction">Introduction</a>,” Emotion Docs</blockquote>

In essence, Emotion is a CSS-in-JavaScript library, and an interesting thing about CSS-in-JavaScript libraries is that they enable you to collocate components with styles. Being able to tie them up together in a scope ensures that some component styles don’t interfere with others, which is crucial to our component library.

Emotion exposes two APIs for React:

- `@emotion/core`
- `@emotion/styled`

Before we dive into how these APIs work, note that they both support the styling of components with template strings and objects.

The **core API** is actually like the regular `style` property we currently use today when building apps with React, with the addition of vendor prefixing, nested selectors, media queries, and more.

Using the object approach with the core API would typically look like this:

<pre><code class="language-javascript">import { jsx } from '@emotion/core'

let Box = props => {
  return (
    &lt;div
      css={{
        backgroundColor: 'grey'
      }}
      {...props}
    /&gt;
  )
}
</code></pre>

This is a rather contrived example that shows how we could style a `Box` component with Emotion. It’s like swapping out the `style` property for a `css` property, and then we’re good to go.

{{% feature-panel %}}

Now, let’s see how we could use the template string approach with the same core API:

<pre><code class="language-javascript">import { jsx, css } from '@emotion/core'

let Box = props =&gt; {
  return (
    &lt;div
      css={css`
        background-color: grey
      `}
      {...props}
    /&gt;
  )
}
</code></pre>

All we did was wrap the template string with the `css` tag function, and Emotion handles the rest.

The **styled API**, which is built on the core API, takes a slightly different approach to styling components. This API is called with a particular HTML element or React component, and that element is called with an object or a template string that contains the styles for that element.

Let’s see how we could use the object approach with the styled API:

<pre><code class="language-javascript">import styled from '@emotion/styled'

const Box = styled.div({
        backgroundColor: 'grey'
});
</code></pre>

Here is one way to use the styled API, which is an alternative to using the core API. The rendered outputs are the same.

Now, let’s see how we could use the template string approach using the styled API:

<pre><code class="language-javascript">import styled from '@emotion/styled'

const Box = styled.div`
        background-color: grey
`
</code></pre>

This achieves the same thing as the object approach, only with a template string this time.

We could use either the core API or the styled API when building components or an application. I prefer the styled approach for a component library for a couple of reasons:

- It achieves a lot with few keystrokes.
- It takes in an `as` prop, which helps with dynamically changing the HTML element from the call site. Let’s say we default to a paragraph element, and we need a header element because of semantics; we can pass the header element as a value to the `as` property.

### Getting Started

To get started, let’s clone the [setup scripts](https://github.com/smashingmagazine/component-library) on GitHub, which we can do on the command line:

<pre><code class="language-bash">git clone git@github.com:smashingmagazine/component-library.git</code></pre>

This command copies the code in that repository to the `component-library`’s folder. It contains the code required to set up a component library, which includes [Rollup](https://rollupjs.org/guide/en/) to help bundle our library.

We currently have a `components` folder with an `index.js` file, which does nothing. We’ll be creating new folders under the `components` folder for each component we build in our library. Each component’s folder will expose the following files:

- `Component.js`  
This is the component we’re building.
- `index.js`  
This exports the component from `Component.js` and makes referencing components from a different location easier.
- `Component.story.js`  
This essentially renders our component in its multiple states using Storybook.

It also ships with a `utils` folder, which defines certain properties that would be used in our components. The folder contains several files:

- `helpers.js`  
This contains helper functions that we are going to be using across our application.
- `units.js`  
This defines spacing and font-size units, which we will use later.
- `theme.js`  
This defines our component library’s palette, shadows, typography, and shape.

Let’s look at what we’ve defined in the `units.js` file:

<pre><code class="language-javascript">export const spacing = {
  none: 0,
  xxsmall: '4px',
  xsmall: '8px',
  small: '12px',
  medium: '20px',
  gutter: '24px',
  large: '32px',
  xlarge: '48px',
  xxlarge: '96px',
};

export const fontSizes = {
  xsmall: '0.79rem',
  small: '0.889rem',
  medium: '1rem',
  large: '1.125rem',
  xlarge: '1.266rem',
  xxlarge: '1.424rem',
};
</code></pre>

This defines the `spacing` and `fontSizes` rules. The spacing rule was inspired by the [Braid design system](https://github.com/seek-oss/braid-design-system), which is based on multiples of four. The `fontSizes` are derived from the major second (1.125) type scale, which is a good scale for product websites. If you’re curious to learn more about type scale, “[Exploring Responsive Type Scales](https://medium.com/sketch-app-sources/exploring-responsive-type-scales-cf1da541be54)” explains the value of knowing the scales appropriate for different websites.

Next, let’s through the `theme.js` file!

<div class="break-out">

 <pre><code class="language-javascript">import { spacing } from './units';

const white = '#fff';
const black = '#111';

const palette = {
  common: {
    black,
    white,
  },
  primary: {
    main: '#0070F3',
    light: '#146DD6',
    contrastText: white,
  },
  error: {
    main: '#A51C30',
    light: '#A7333F',
    contrastText: white,
  },
  grey: {
    100: '#EAEAEA',
    200: '#C9C5C5',
    300: '#888',
    400: '#666',
  },
};

const shadows = {
  0: 'none',
  1: '0px 5px 10px rgba(0, 0, 0, 0.12)',
  2: '0px 8px 30px rgba(0, 0, 0, 0.24)',
};

const typography = {
  fontFamily:
    "Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Ubuntu, 'Helvetica Neue', sans-serif",
};

const shape = {
  borderRadius: spacing['xxsmall'],
};

export const theme = {
  palette,
  shadows,
  typography,
  shape,
};
</code></pre>
</div>

In the theme file, we’ve defined our `palette`, which is essentially the colors we’re going to be using across all components in our library. We also have a `shadows` object, where we define our `box-shadow` values. There’s also the `typography` object, which currently just defines our `fontFamily`. Finally, `shape` is used for properties such as `border-radius`. This theme’s structure is inspired by [Material-UI](https://material-ui.com/).

Next, our `helpers.js` file!

<pre><code class="language-javascript">export const isObjectEmpty = (obj) => {
  return Object.keys(obj).length === 0;
};
</code></pre>

Here, we only expose the `isObjectEmpty` function, which takes in an object and returns `true` if the object is empty. It returns `false` if it has any values. We’re going to make use of this function later.

Now that we’ve gone through all of the files in the `utils` folder, it’s about time to start building our components!

## Buttons

Buttons are one of the most used components on the web. They’re used everywhere and can take different forms, shapes, sizes, and more.

Here are the buttons we’re going to build in [Figma](https://www.figma.com/file/WQIRHS8QV3B7ZPDSW327uT/Minimalist?node-id=0%3A1).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87382448-81c9-4bdf-a844-3243c6ee825a/button-component-library-react-emotion.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87382448-81c9-4bdf-a844-3243c6ee825a/button-component-library-react-emotion.png" sizes="100vw" caption="Button component design from Figma (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87382448-81c9-4bdf-a844-3243c6ee825a/button-component-library-react-emotion.png'>Large preview</a>)" alt="An illustration that shows what the Button component looks like" >}}

These subtle variations are going to be applied as properties to our button. We would like the buttons in our component library to accept properties such as `variant`, `size`, `enableElevation` (i.e. `box-shadow`), and `color`.

Starting with the button component, let’s create a `Button` folder, where we will define everything related to buttons, as discussed earlier.

Let's create our button component:

<pre><code class="language-javascript">import styled from '@emotion/styled';
import isPropValid from '@emotion/is-prop-valid';

const StyledButton = () => {};

const IGNORED_PROPS = ['color'];

const buttonConfig = {
  shouldForwardProp: (prop) =>
    isPropValid(prop) && !IGNORED_PROPS.includes(prop),
};

export const Button = styled('button', buttonConfig)(StyledButton);
</code></pre>

Here, we’ve started off by setting up our button component with a `buttonConfig`. The `buttonConfig` contains `shouldForwardProp`, which is used to control the properties that should be forwarded to the DOM, because properties such as `color` show up on the rendered element by default.

Next, let’s define our button sizes, which we’re going to use in the button component!

<pre><code class="language-javascript">const buttonSizeProps = {
  small: {
    fontSize: fontSizes['xsmall'],
    padding: `${spacing['xsmall']} ${spacing['small']}`,
  },
  medium: {
    fontSize: fontSizes['small'],
    padding: `${spacing['small']} ${spacing['medium']}`,
  },
  large: {
    fontSize: fontSizes['medium'],
    padding: `${spacing['medium']} ${spacing['large']}`,
  },
};
</code></pre>

`buttonSizeProps` is a map of our size values (`small`, `medium`, and `large`), and it returns `fontSize` and `padding` values based on the sizes. For a small button, we’d need a small font with small padding. The same goes for the medium and large sizes to scale them appropriately.

Next, let’s define a function that provides valid CSS properties based on the passed variant:

<pre><code class="language-javascript">const getPropsByVariant = ({ variant, color, theme }) => {

  const colorInPalette = theme.palette[color];

  const variants = {
    outline: colorInPalette
      ? outlineVariantPropsByPalette
      : defaultOutlineVariantProps,
    solid: colorInPalette
      ? solidVariantPropsByPalette
      : defaultSolidVariantProps,
  };

  return variants[variant] || variants.solid;
};
</code></pre>

Here, the `getPropsByVariant` function takes in `variant`, `color`, and `theme` properties and returns the properties of the specified variant; if no variant is specified, it defaults to `solid`.  `colorInPalette` retrieves the palette assigned to the specified color if found, and `undefined` if not found in our `theme` object.

In each variant, we check whether a palette actually exists for the color specified; if we don’t, then we use colors from the `common` and `grey` objects of our theme, which we will apply in `defaultOutlineVariantProps` and `defaultSolidVariantProps`.

Next, let’s define our variant properties!

<pre><code class="language-javascript">const defaultSolidVariantProps = {
  main: {
    border: `1px solid ${theme.palette.grey[100]}`,
    backgroundColor: theme.palette.grey[100],
    color: theme.palette.common.black,
  },
  hover: {
    border: `1px solid ${theme.palette.grey[200]}`,
    backgroundColor: theme.palette.grey[200],
  },
};

const defaultOutlineVariantProps = {
  main: {
    border: `1px solid ${theme.palette.common.black}`,
    backgroundColor: theme.palette.common.white,
    color: theme.palette.common.black,
  },
  hover: {
    border: `1px solid ${theme.palette.common.black}`,
    backgroundColor: theme.palette.common.white,
    color: theme.palette.common.black,
  },
};

const solidVariantPropsByPalette = colorInPalette && {
  main: {
    border: `1px solid ${colorInPalette.main}`,
    backgroundColor: colorInPalette.main,
    color: colorInPalette.contrastText,
  },
  hover: {
    border: `1px solid ${colorInPalette.light}`,
    backgroundColor: colorInPalette.light,
  },
};

const outlineVariantPropsByPalette = colorInPalette && {
  main: {
    border: `1px solid ${colorInPalette.main}`,
    backgroundColor: theme.palette.common.white,
    color: colorInPalette.main,
  },
  hover: {
    border: `1px solid ${colorInPalette.light}`,
    backgroundColor: theme.palette.common.white,
    color: colorInPalette.light,
  },
};
</code></pre>

Here, we define the properties that are going to be applied to our button based on the selected variants. And, as discussed earlier, `defaultSolidVariantProps` and `defaultOutlineVariantProps` use colors from our `common` and `grey` objects as fallbacks for when the color specified isn’t in our palette or when no color is specified for what we put in place.

By the way, the `solidVariantPropsByPalette` and `outlineVariantPropsByPalette` objects use the color from our palette as specified by the button. They both have `main` and `hover` properties that differentiate the button’s default and hover styles, respectively.

The button design we’ve used accounts for two variants, which we can check out in [our component library design](https://www.figma.com/file/WQIRHS8QV3B7ZPDSW327uT/Component-Library?node-id=0%3A1).

Next, let’s create our `StyledButton` function, which combines all we’ve done so far.

<div class="break-out">

 <pre><code class="language-javascript">const StyledButton = ({
  color,
  size,
  variant,
  enableElevation,
  disabled,
  theme,
}) => {
  if (isObjectEmpty(theme)) {
    theme = defaultTheme;
  }

  const fontSizeBySize = buttonSizeProps[size]?.fontSize;
  const paddingBySize = buttonSizeProps[size]?.padding;
  const propsByVariant = getPropsByVariant({ variant, theme, color });

  return {
    fontWeight: 500,
    cursor: 'pointer',
    opacity: disabled && 0.7,
    transition: 'all 0.3s linear',
    padding: buttonSizeProps.medium.padding,
    fontSize: buttonSizeProps.medium.fontSize,
    borderRadius: theme.shape.borderRadius,
    fontFamily: theme.typography.fontFamily,
    boxShadow: enableElevation && theme.shadows[1],
    ...(propsByVariant && propsByVariant.main),
    ...(paddingBySize && { padding: paddingBySize }),
    ...(fontSizeBySize && { fontSize: fontSizeBySize }),
    '&:hover': !disabled && {
      boxShadow: enableElevation && theme.shadows[2],
      ...(propsByVariant && propsByVariant.hover),
    },
  };
};
</code></pre>
</div>

In the `StyledButton` function, we’re assigning `defaultTheme` to the theme if the `theme` object is empty which makes it optional for the consumers of our library to use Emotion’s [ThemeProvider](https://emotion.sh/docs/emotion-theming#themeprovider-reactcomponenttype) in order to make use of the library. We assigned `fontSize` and `padding` based on the `buttonSizeProps` object. We defined several default button properties, such as `fontWeight` and `cursor`, which aren’t tied to any property, and we also derived `color`, `backgroundColor`, and `border` values based on the result of `propsByVariant`.

Now that we’ve created our `Button` component, let’s see how we can use it:

<pre><code class="language-javascript">&lt;Button
    variant="solid"
    color="primary"
    size="small"
    enableElevation
    disabled
&gt;
    Small Outline Elevated Button
&lt;/Button&gt;
</code></pre>

We can check what that looks like [on CodeSandbox](https://codesandbox.io/s/component-lib-button-wp0c9?file=/src/App.js):

<iframe loading="lazy" src="https://codesandbox.io/embed/component-lib-button-wp0c9?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Component-lib-button"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

That’s how to use the `Button` component. We define the following properties:

- We define a variant with a `solid` value. We could have specified `outline` instead. If the `variant` prop isn’t provided, we would also default to `solid`.
- We define `color`, with a value of `primary`. We also support `error` as a color value or a color from a `theme` object. If the `color` property isn’t specified, we would fall back to our default color state.
- We define `size`, with a value of `small`. It could be `medium` (the default) or `large`.
- We define `EnableElevation` because we want some `box-shadow` on our button. We could have chosen not to use it.
- Finally, we define `disabled` because we want our button to be disabled. The additional thing we do to a disabled button is reduce its opacity.

The button doesn’t need to take any property. It defaults to a solid medium-sized button.

## Box Component

A box component is a container that can hold any component or HTML element. It accepts but is not limited to properties such as `padding`, `margin`, `display`, and `width`. It can also be used as a base component for some of the other components we’ll get into later.

Here’s what it looks like on Figma:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7abe7c6-addd-4bd2-b2d4-4b752b132182/box-component-library-react-emotion.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7abe7c6-addd-4bd2-b2d4-4b752b132182/box-component-library-react-emotion.png" sizes="100vw" caption="Box component design from Figma (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7abe7c6-addd-4bd2-b2d4-4b752b132182/box-component-library-react-emotion.png'>Large preview</a>)" alt="An illustration that shows what the Box component looks like" >}}

Before diving into the code, let’s not forget to create a new folder for this component.

Now, let’s create our `Box` component:

<div class="break-out">

 <pre><code class="language-javascript">
import styled from '@emotion/styled';
import isPropValid from '@emotion/is-prop-valid';
import { spacing, theme as defaultTheme } from '../../utils';

const StyledBox = ({
  paddingX,
  paddingY,
  marginX,
  marginY,
  width,
  display,
  theme,
  ...props
}) => {

  if (isObjectEmpty(theme)) {
    theme = defaultTheme;
  }

  const padding = spacing[props.padding];
  let paddingTop = spacing[props.paddingTop];
  let paddingRight = spacing[props.paddingRight];
  let paddingBottom = spacing[props.paddingBottom];
  let paddingLeft = spacing[props.paddingLeft];
  if (paddingX) {
    paddingLeft = spacing[paddingX];
    paddingRight = spacing[paddingX];
  }
  if (paddingY) {
    paddingTop = spacing[paddingY];
    paddingBottom = spacing[paddingY];
  }
  let margin = spacing[props.margin];
  let marginTop = spacing[props.marginTop];
  let marginRight = spacing[props.marginRight];
  let marginBottom = spacing[props.marginBottom];
  let marginLeft = spacing[props.marginLeft];
  if (marginX) {
    marginLeft = spacing[marginX];
    marginRight = spacing[marginX];
  }
  if (marginY) {
    marginTop = spacing[marginY];
    marginBottom = spacing[marginY];
  }
  return {
    padding,
    paddingTop,
    paddingRight,
    paddingBottom,
    paddingLeft,
    margin,
    marginTop,
    marginRight,
    marginBottom,
    marginLeft,
    width,
    display,
    fontFamily: theme.typography.fontFamily,
  };
};

const IGNORED_PROPS = ['display', 'width'];

const boxConfig = {
  shouldForwardProp: (prop) =>
    isPropValid(prop) && !IGNORED_PROPS.includes(prop),
};

export const Box = styled('div', boxConfig)(StyledBox);
</code></pre>
</div>

The `spacing` rule we defined earlier is being applied to both padding and margin, as we can see in the `Box` component. We receive contextual values for padding and margin, and we look up their actual values from the `spacing` object.

We accept `paddingX` and `paddingY` props to update padding across the horizontal and vertical axis, respectively. We do the same for `marginX` and `marginY` as well.

Also, we don’t want the `display` and `width` props to get forwarded to the DOM because we only need them in CSS. So, we add them to our list of props to ignore, and pass that on to our config.

Here’s how we could use the `Box` component:

<pre><code class="language-javascript">&lt;Box
  padding="small"
  paddingTop="medium"
  paddingBottom="medium"
&gt;
  Simple Box Component
&lt;/Box&gt;
</code></pre>

We can see what this looks like on [CodeSandbox](https://codesandbox.io/s/component-lib-box-m71mf?file=/src/App.js).

<iframe loading="lazy" src="https://codesandbox.io/embed/component-lib-box-m71mf?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Component-lib-box"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

In this `Box` component, we’ve assigned `small` as a value to our `padding` property, and `medium` to the `paddingTop` and `paddingBottom` properties. When rendered, the `Box` component will have its `padding-left` and `padding-right` properties set to `12px` each, and its `padding-top` and `padding-bottom` properties set to `20px`. We could have replaced `paddingTop` and `paddingBottom` with `paddingY` and gotten the same result.

## Columns Component

The `Columns` component is a variation of our `Box` component, with a `display` type of `flex` and with children spaced evenly across the x-axis.

Here is a representation of the `Columns` component in Figma:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c708b65a-b35b-4de8-aef1-fc83267e3ccb/columns-component-library-react-emotion.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c708b65a-b35b-4de8-aef1-fc83267e3ccb/columns-component-library-react-emotion.png" sizes="100vw" caption="Columns component design from Figma (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c708b65a-b35b-4de8-aef1-fc83267e3ccb/columns-component-library-react-emotion.png'>Large preview</a>)" alt="An illustration that shows what the Button component looks like" >}}

Let’s build our `Columns` component!

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';
import { Box } from '../Box';

export const Columns = ({ children, space, ...props }) => {
  return (
    &lt;Box display="flex" {...props}&gt;
      {React.Children.map(children, (child, index) => {
        if (child.type !== Box) {
          console.warn(
            'Each child in a Columns component should be a Box component'
          );
        }

        if (index > 0) {
          return React.cloneElement(child, {
            marginLeft: space,
            width: '100%',
          });
        }

        return React.cloneElement(child, { width: '100%' });
      })}
    &lt;/Box&gt;
  );
};
</code></pre>
</div>

We’re using [React.Children](https://reactjs.org/docs/react-api.html#reactchildren) to map over the `Columns` component’s children. And we’re adding `marginLeft` and `width` properties to each of the children, except the first child, which doesn’t need a `marginLeft` property because it’s the leftmost child in the column. We expect each child to be a `Box` element to ensure that the necessary styles are applied to it.

Here’s how we could use the `Columns` component:

<pre><code class="language-javascript">&lt;Columns space="small"&gt;
  &lt;Box&gt; Item 1&lt;/Box&gt;
  &lt;Box&gt; Item 2&lt;/Box&gt;
  &lt;Box&gt; Item 3&lt;/Box&gt;
&lt;/Columns&gt;
</code></pre>

We can see what that looks like on [CodeSandbox](https://codesandbox.io/s/component-lib-columns-x1g0m).

<iframe loading="lazy" src="https://codesandbox.io/embed/component-lib-columns-x1g0m?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Component-lib-columns"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

The `Columns` children here are spaced evenly across the x-axis by 12 pixels because that’s what the value of `small` resolves to, as we’ve defined earlier. Because the `Columns` component is literally a `Box` component, it can take in other `Box` component properties, and we can customize it as much as we want.

## Stack Component

This is also a variation of our `Box` component that takes the full width of the parent element and whose children are spaced evenly across the y-axis.

Here is a representation of the `Stack` component in Figma:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42ff98d5-f414-4de3-a4b7-a7c1e2ce7e4d/stack-component-library-react-emotion.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42ff98d5-f414-4de3-a4b7-a7c1e2ce7e4d/stack-component-library-react-emotion.png" sizes="100vw" caption="Stack component design from Figma (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42ff98d5-f414-4de3-a4b7-a7c1e2ce7e4d/stack-component-library-react-emotion.png'>Large preview</a>)" alt="An illustration that shows what the Stack component looks like" >}}

Let’s build our `Stack` component:

<pre><code class="language-javascript">import React from 'react';
import { Box } from '../Box';
import { Columns } from '../Columns';

const StackChildrenTypes = [Box, Columns];
const UnsupportedChildTypeWarning =
  'Each child in a Stack component should be one of the types: Box, Columns';

export const Stack = ({ children, space, ...props }) =&gt; {
  return (
    &lt;Box {...props}&gt;
      {React.Children.map(children, (child, index) =&gt; {
        if (!StackChildrenTypes.includes(child.type)) {
          console.warn(UnsupportedChildTypeWarning);
        }

        if (index &gt; 0) {
          return React.cloneElement(child, { marginTop: space });
        }

        return child;
      })}
    &lt;/Box&gt;
  );
};
</code></pre>

Here, we map over each child with `React.Children` and apply a `paddingTop` property to it with the value of the `space` argument. As for the first child, we need it to take its original position, so we skip adding a `marginTop` property to it. We also accept each child to be a `Box` so that we can apply the necessary properties to it.

Here’s how we could use the `Stack` component:

<pre><code class="language-javascript">&lt;Stack space="small"&gt;
  &lt;Box marginTop="medium"&gt; Item 1&lt;/Box&gt;
  &lt;Box&gt; Item 2&lt;/Box&gt;
  &lt;Box&gt; Item 3&lt;/Box&gt;
&lt;/Stack&gt;
</code></pre>

We can see what that looks like on [CodeSandbox](https://codesandbox.io/s/component-lib-stack-3kx9m?file=/src/App.js).

<iframe loading="lazy" src="https://codesandbox.io/embed/component-lib-stack-3kx9m?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Component-lib-stack"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Here, the `Box` elements are spaced evenly with the `small` unit, and the first `Box` takes a separate `marginTop` property. This shows that you can customize components however you wish.

### Conclusion

We’ve gone through the basics of using Emotion to create components in React using the APIs that it provides. This is just one of many ways to go about building a component library. There are some nuances to building it for a brand because you might not have to take theming and some other things into consideration. But if you plan to release the library to the public one day, then you’ll have to deal with requests for those missing pieces, so consider that possibility and make the library a little flexible ahead of time.

If you have any questions, feel free to drop them as comments.

The [repository for this article](https://github.com/smashingmagazine/component-library/tree/final) is on GitHub, and the [button designs](https://www.figma.com/file/WQIRHS8QV3B7ZPDSW327uT/Component-Library?node-id=0%3A1) we’ve used are on Figma.

### References

- “[On Building Component Libraries](https://clearleft.com/posts/on-building-component-libraries)”, Mark Perkins, Clearleft
- “[Exploring Responsive Type Scales](https://medium.com/sketch-app-sources/exploring-responsive-type-scales-cf1da541be54)”, Joseph Mueller
- “[Design Systems With React and Storybook](https://frontendmasters.com/courses/design-systems/)”, Emma Bostian, Frontend Masters
- [Emotion official documentation](https://emotion.sh/docs/introduction)

{{% newsletter-panel %}}

{{< signature "ks, ra, al, il" >}}
