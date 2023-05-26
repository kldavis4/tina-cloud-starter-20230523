---
title: 'How To Maintain A Large Next.js Application'
slug: maintain-large-nextjs-application
author: nirmalya-ghosh
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d36d3a50-0f3f-402e-9ceb-8164b41065bc/maintain-large-nextjs-application.jpg
date: 2021-11-26T12:30:00.000Z
summary: >-
  In this article, Nirmalya discusses some of the complex problems that he faced while building and maintaining large Next.js applications. He always explains how these problems can be solved by using various tools.
description: >-
  In this article, Nirmalya discusses some of the complex problems that he faced while building and maintaining large Next.js applications. He always explains how these problems can be solved by using various tools.
categories:
  - Apps
  - Next.js
  - Tools
  - TypeScript
---

Maintaining a large application is always a difficult task. It might have outdated dependencies which can cause maintainability issues. It can also have tests that are flaky and don’t inspire any confidence. There can also be issues with large JavaScript and CSS bundles causing the application to provide a non-optimal user experience for the end-users.

However, there are a few ways in which you can make a large code-base easy to maintain. In this article, we will discuss a few of those techniques as well as some of the things I wish I had known earlier to help manage large Next.js applications.

**Note**: *While this article is specific to Next.js, some of the points will also work for a wide variety of front-end applications.*

## Use TypeScript

TypeScript is a strongly typed programming language which means that it enforces certain strictness while intermixing different types of data. According to [StackOverflow Developer Survey 2021](https://insights.stackoverflow.com/survey/2021), [TypeScript](https://www.typescriptlang.org/) is one of the languages that developers want to work with the most. 

Using a strongly typed language like TypeScript will help a lot when working with a large codebase. It will help you understand if there is a possibility that your application will break when there is a change. It is not guaranteed that TypeScript will always complain when there is a chance of breakage. However, most of the time, TypeScript will help you **eliminate bugs even before you build your application**. In certain cases, the build will fail if there are type mismatches in your code as Next.js checks for type definition during build time.

From [the Next.js docs](https://nextjs.org/docs/basic-features/typescript):

<blockquote>“By default, Next.js will do type checking as part of the next build. We recommend using code editor type checking during development.”</blockquote>

Note that `next build` is the script that creates an optimized production build of your Next.js application. From my personal experience, it helped me a lot when I was trying to [update Next.js to version 11](https://nextjs.org/blog/next-11#upgrade-guide) for one of my applications. As a part of that update, I also decided to update a few other packages. Because of TypeScript and VSCode, I was able to figure out when those breaking changes even before I had built the application.

{{% feature-panel %}}

## Use A Mono-Repo Structure Using Lerna Or Nx

Imagine that you are building a component library along with your main Next.js application. You might want to keep the library in a separate repository to add new components, build and release them as a package. This seems clean and works fine when you want to work in the library. But when you want to integrate the library in your Next.js application, **the development experience will suffer**.

This is because when you integrate the component library with your Next.js application, you might have to go back into the library’s repository, make changes, release the updates and then install the new version in your Next.js application. Only after that, the new changes from the component library will start reflecting in the Next.js application. Imagine your whole team doing this multiple times. The amount of time spent on building and releasing the component library separately will add up to a huge chunk.

This problem can be resolved if you **use a mono-repo structure where your component library resides with your Next.js application**. In this case, you can simply update your component library and it will immediately reflect in your Next.js application. There is no need for a separate build and release of your component library.

You can use a package like [next-transpile-modules](https://www.npmjs.com/package/next-transpile-modules) so that you don’t even need to build your component library before your Next.js application can consume it. However, if you are planning to release your component library as an npm package, you might need to have a build step.

For managing a mono-repo, you can use tools like [Lerna](https://lerna.js.org/), [Nx](https://nx.dev/), [Rush](https://rushjs.io/), [Turborepo](https://turborepo.com/), [yarn workspaces](https://classic.yarnpkg.com/en/docs/workspaces/), or [npm workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces). I liked using Lerna together with yarn workspaces when I needed to configure my build pipeline. If you prefer something which will automate a bunch of things via CLI, you can take a look at Nx. I feel that all of them are good but solve slightly different problems.

## Use Code Generators Like Hygen To Generate Boilerplate Code

When a lot of developers start contributing to a large code-base, there is a good chance that there will be a lot of duplicate code. This happens mainly because there is a need to build a page, component, or utility function which is similar to an already existing one with slight modifications.

You can think of **writing unit test cases** for your components or utility functions. You might want to copy the boilerplate code as much as possible and do certain modifications as per the new file. However, this adds a lot of code consisting of bad variable naming in your code-base. This can be reduced by a proper code-review process. However, there is a better way to reduce this by automating the generation of the boilerplate code.

Unless you are using [Nx](https://nx.dev/latest/react/getting-started/nx-cli), you will need to have a way in which you can automate a lot of code generation. I have used [Hygen](https://www.hygen.io/) to generate the boilerplate code for Redux, React components, and utility functions. You can check out the [documentation](https://www.hygen.io/docs/quick-start) to get started with Hygen. They also have [a dedicated section](https://www.hygen.io/docs/redux) for generating Redux boilerplate. You can also use [Redux Toolkit](https://redux-toolkit.js.org/) to reduce the boilerplate code necessary for your Redux applications. We will discuss this package next.

## Use A Well-Established Pattern Like Redux With Lesser Boilerplate Via Redux Toolkit

Many developers will argue that [Redux](https://redux.js.org/) increases the complexity of the code-base or [React Context](https://reactjs.org/docs/context.html) is much easier to maintain. I think that it depends mostly on the type of application that you are building as well as the expertise of the whole development team. You can choose whatever state management solution your team is most comfortable with, but try to choose one that doesn’t need to have a lot of boilerplate.

In this article, I’m mentioning Redux because it is still [the most popular state management solution](https://www.npmtrends.com/mobx-vs-redux-vs-zustand-vs-xstate) out there according to npm trends. In the case of Redux, you can reduce a lot of boilerplate code by using [Redux Toolkit](https://redux-toolkit.js.org/). This is a very opinionated and powerful library that you can use to **simplify your state management**. Check out their [documentation](https://redux-toolkit.js.org/introduction/getting-started) regarding how to get started with Redux Toolkit.

I have used Redux, [Zustand](https://zustand.surge.sh/), and Redux Toolkit while building Next.js applications. I feel that Zustand is very simple and easy to understand. However, I still use Redux in case I need to build something complex. I haven’t used [XState](https://xstate.js.org/) but it is also a popular choice.

## Use React Query Or SWR For Fetching Async Data

Most front-end applications will fetch data from a back-end server and render it on the page. In a Next.js application or any JavaScript application, you can fetch data using [the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), [Axios](https://www.npmjs.com/package/axios), or similar libraries. However, as the application grows, it becomes very difficult to manage this async state of your data. You might create your abstractions using utility functions or wrappers around Fetch or Axios but when multiple developers are working on the same application, these utility functions or wrappers will soon become difficult to manage. Your application might also suffer from caching, and performance issues.

To resolve these kinds of issues, it is better to use packages like [React Query](https://react-query.tanstack.com/) or [SWR](https://swr.vercel.app/). These packages provide **a default set of configurations out of the box**. They handle a lot of things like caching and performance which are difficult to manage on your own. Both of these packages provide some [default configuration](https://react-query.tanstack.com/guides/important-defaults) and [options](https://swr.vercel.app/docs/options) which you can use to customize their behaviors according to the requirements of your application. These packages will fetch and cache async data from your back-end API endpoints and make your application state much more maintainable.

I have used both React Query and SWR in my projects and I like both of them. You can take a look at [their comparison](https://react-query.tanstack.com/comparison#_top) and features to decide which one you should use.

{{% ad-panel-leaderboard %}}

## Use Commitizen And Semantic Release With Husky

If you deploy and release your application often, then you might have encountered issues with versioning. When you are working on a big application and multiple developers are contributing to it, managing releases becomes even more difficult. It becomes very difficult to keep track of the changelog. Manually updating the changelog becomes very difficult and slowly your changelog becomes out of date.

You can combine packages like [Commitizen](https://www.npmjs.com/package/commitizen) and [Semantic Release](https://www.npmjs.com/package/semantic-release) to help you with versioning and maintaining a changelog. These tools help you in **automating part of your release process by keeping the changelog in sync** with what changes were deployed in a particular release. You can use a tool like [Husky](https://www.npmjs.com/package/husky) to ensure that all the contributors are following the established pattern for writing commit messages and helping you in managing your changelog.

## Use Storybook For Visualizing UI Components

In a large code-base, your application will most likely consist of a lot of components. Some of these components will be outdated, buggy, or not necessary anymore. However, it is very difficult to keep track of this kind of thing in a large application. Developers might create new components whose behavior might be similar to an already existing component because they don’t know that the previous component exists. This happens often because there is no way to keep track of what components the application currently has and how they interact with each other.

Tools like [Storybook](https://storybook.js.org/) will help you **keep track of all the components that your code-base currently consists of**. [Setting up Storybook](https://storybook.js.org/docs/react/get-started/examples) is easy and can integrate with your existing Next.js application. Next.js has [an example](https://github.com/vercel/next.js/tree/canary/examples/with-storybook) that shows how to set up Storybook with your application.

I have always liked using Storybook because it helps my team of developers understand how each component behaves and what APIs it exposes. It serves as a source of documentation for every developer. Storybook also helps designers understand the behavior of all the components and interactions. You can also use [Chromatic](https://www.chromatic.com/) along with Storybook for visual testing and catching regression issues during each release.

**Recommended Reading**: *“[Building React Apps With Storybook](https://www.smashingmagazine.com/2020/09/building-react-apps-storybook/)” by Abdulazeez Adeshina*

## Write Maintainable Tests From The Start

Writing tests consumes time. As a result, many companies tend not to invest time in writing any sort of test. Because of this, the application might suffer in the long run. As the application grows, the complexity of the application also increases. In a complex application, refactoring becomes difficult because it is very hard to understand which files might break because of the changes.

One solution to this problem would be to **write as many tests** as possible from the start. You can follow [Test Driven Development (or TDD)](https://en.wikipedia.org/wiki/Test-driven_development#:~:text=Test%2Ddriven%20development%20(TDD),software%20against%20all%20test%20cases.) or any other similar concept that works for you. There is an excellent article [*The Testing Trophy and Testing Classifications*](https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications) by Kent C. Dodds which talks about different types of tests that you can write.

Although writing maintainable tests take time. But I think that tests are very essential for large applications as it gives developers the confidence to refactor files. Generally, I use [Jest](https://jestjs.io/), [React Testing Library](https://testing-library.com/docs/react-testing-library/intro), and [Cypress](https://www.cypress.io/) for writing tests in my application.

## Use Dependabot To Update Packages Automatically

When multiple feature teams contribute to the same application, there is a good chance that the packages used in it will become outdated. This happens because if there are any breaking changes while updating packages, there is a possibility that a considerable amount of time needs to be invested in doing that update. This might result in missing deadlines for shipping features. However, this practice might hurt in the long run. Working with outdated packages can cause a lot of issues like security vulnerabilities, performance issues, and so on.

Fortunately, tools like [Dependabot](https://dependabot.com/) can **help your team by automating the update process**. Dependabot can be [configured](https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/configuration-options-for-dependency-updates#about-the-dependabotyml-file) to check for outdated packages and send updated pull requests as often as you need. Using tools like Dependabot has helped me a lot in keeping the dependencies of my applications updated.

{{% ad-panel-leaderboard %}}

## Things I Wish I Had Known Earlier

There are many things that I wish I had known earlier while building the Next.js application. However, the most important is the going to the [Production section of the Next.js documentation](https://nextjs.org/docs/going-to-production). This section outlines some of the most important things that one should implement **before deploying a Next.js application to production**. Before I read this section, I used to arbitrarily guess about what to do before deploying any application to production.

Always check what browsers you need to support before deploying your application to production and shipping them to your customers. [Next.js supports a wide range of browsers](https://nextjs.org/docs/basic-features/supported-browsers-features). But it is essential to understand what type of users you are shipping your application to and what type of browsers they use.

## Conclusion

These are some of the things that I learned while building and maintaining a large Next.js application. Most of these points will apply to any front-end application. For any front-end application, the main priority should always be shipping a product that has a very good user experience, is fast, and feels smooth to use.

I try to keep all these points in mind whenever I develop any application. I hope that they’ll prove to be useful to you, too!

{{< signature "vf, yk, il" >}}
