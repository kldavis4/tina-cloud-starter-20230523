---
title: 'Testable Frontend: The Good, The Bad And The Flaky'
slug: testable-frontend-architecture
author: noam-rosenthal
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63e8d419-abd0-4630-b0de-16991a961f26/testable-frontend-architecture.jpg
date: 2022-07-28T12:00:00.000Z
summary: >-
  Testing is not just about tools and processes. It’s about architecture. In this article, Noam Rosenthal will share his experience on how to organize testing and find the right balance between front-end and subsystems and between different strategies.
description: >-
  Testing is not just about tools and processes. It’s about architecture. In this article, Noam Rosenthal will share his experience on how to organize testing and find the right balance between front-end and subsystems and between different strategies.
categories:
  - UI
  - API
  - Apps
  - Tools
  - React
  - Testing
---

I often come across front-end developers, managers, and teams facing a repeating and legitimately difficult dilemma: how to organize their testing between unit, integration, and E2E testing and how to test their UI components.

Unit tests often seem not to catch the “interesting” things happening to users and systems, and E2E tests usually take a long time to run or require a messy configuration. In addition to that, there are so many tools around (JEST, Cypress, Playwright, and so on). How does one make sense of it all?

**Note:** *This article uses React for examples and semantics, but some of the values apply to any UI development paradigm.*

## Why Is Testing Front-end Difficult? 

We don’t tend to author our front-end as a system but rather as a bunch of components and functions that make up the user-interface stories. With component code mainly living in JavaScript or JSX, rather than separating between HTML, JS, and CSS, it’s also more tempting than ever to mix view code and business-logic code. When I say “we,” I mean almost every web project I encountered as a developer or consultant.

When we come around to test this code, we often start from something like the [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) which renders React components and tests the result, or we faff about with configuring Cypress to work nicely with our project and many times end up with a misconfiguration or give up.

When we talk with managers about the time required to set up the front-end testing system, neither they nor we know exactly what it entails and whether our efforts there would bear fruit, and how whatever we build would be valuable to the quality of the final product and the velocity of building it.

{{% feature-panel %}}

## Tools And Processes

It gets worse if we have some sort of a **“mandatory TDD”** (test-driven development) process in the team, or even worse, a code-coverage gate where you have to have X% of your code covered by tests. We finish the day as a front-end developer, fix a bug by fixing a few lines sprinkled across several React components, custom hooks, and Redux reducers, and then we need to come up with a “TDD” test to “cover” what we did.

Of course, this is not TDD; in TDD, we would have written a failing test first. But in most front-end systems I’ve encountered, there is no infrastructure to do something like that, and the request to write a failing test first while trying to fix a critical bug is often unrealistic.

**Coverage tools and mandatory unit tests are a symptom of our industry being obsessed with specific tools and processes.** “What is your testing strategy?” is often answered by “We use TDD and [Cypress](https://www.cypress.io/)” or “we mock things with [MSW](https://mswjs.io/),” or “we use [Jest](https://jestjs.io/) with React Testing Library.” 

Some companies with separate QA/testing organizations do try to create something that looks more like a test plan. Still, those often reach a different problem, where it’s hard to author the tests together with development.

Tools like Jest, [Cypress](https://www.cypress.io/) and [Playwright](https://playwright.dev/) are great, code coverage has its place, and TDD is a crucial practice for maintaining code quality. But too often, they replace architecture: a good plan of interfaces, good function signatures between units, a clear API for a system, and a clear UI definition of the product &mdash; a good-old separation of concerns. **A process is not architecture.**

## The Bad

To respect our organization’s process, like the mandatory testing rule or some code-coverage gate in CI, we use Jest or whatever tool we have at hand, mock everything around the parts of the codebase we’ve changed, and add one or more “unit” tests that verify that it now gives the “correct” result.

The problem with it, apart from the test being difficult to write, is that we’ve now created a de-facto **contract**. We’re not only verifying that a function gives some set of expected results, but we’re also verifying that this function has the signature the test expects and uses the environment in the same way our mocks simulate. If we ever want to refactor that function signature or how it uses the environment, the test will become dead weight, a contract we don’t intend to keep. It might fail even though the feature works, and it might succeed because we changed something internal, and the simulated environment doesn’t match the real environment anymore.

If you’re writing tests like this, **please stop**. You’re wasting time and making the quality and velocity of your product worse. 

{{% pull-quote %}}
It’s better to not have auto-tests at all than to have tests that create fantasy worlds of unspecified simulated environments and rely on internal function signatures and internal environment states.
{{% /pull-quote %}}

## Contracts

A good way to understand if a test is good or bad is to write its contract in plain English (or in your native language). The contract needs to represent not just the test but also the **assumptions about the environment**. For example, “Given the username U and password Y, this login function should return OK.” A contract is usually a state and an expectation. The above is a good contract; the expectations and the state are clear. For companies with transparent testing practices, this is not news.

It gets worse when the contract becomes muddied with implementation detail: “Given an environment where this useState hook currently holds the value 14 and the Redux store holds an array called userCache with three users, the login function should…”. 

This contract is highly specific to implementation choices, which makes it very brittle. Keep contracts stable, change them when there is a business requirement, and let implementations be flexible. Make sure the things you rely on from the environment are sturdy and well-defined.

{{% ad-panel-leaderboard %}}

## The Flaky

When separation of concerns is missing, our systems don’t have a clear API between them, and we lack functions with a clear signature and expectation, we end up with E2E as the only way to test features or regressions. This is not bad as E2E tests run the whole system and ensure that a particular story that’s close to the user works as expected.

**The problem with E2E tests is that their scope is very wide.** By testing a whole user journey, the environment usually needs to be set up from scratch by authenticating, going through the entire process of finding the right spot where the new feature lives or regression occurred, and then running the test case.

Because of the nature of E2E, each of these steps might incur **unpredictable delays** as it relies on many systems, any of which could be down or laggy at the time the CI run, as well as on careful crafting of “selectors” (how to programmatically mimic what the user is doing). Some bigger teams have systems in place for root-cause analysis to do this, and there are solutions like [testim.io](https://www.testim.io/) that address this problem. However, this is not an easy problem to solve.

Often a bug is in a function or system, and running the whole product to get there tests too much. New code changes might show regressions in unrelated user journey paths because of some failure in the environment.

E2E tests definitely have their place in the overall blend of tests and are valuable in finding issues that are not specific to a subsystem. However, relying too much on them is an indication that perhaps the separation of concerns and API barriers between the different systems is not defined well enough.

## The Good

Since unit-testing is limited or relies on a heavily-mocked environment, and E2E tests tend to be costly and flaky, **integration tests** often supply a good middle ground. With UI integration tests, our whole system runs in isolation from other systems, which can be mocked, but the system itself is running without modification. 

When testing the front-end, it means running the whole front-end as a system and simulating the other systems/”backends” it relies on to avoid flakiness and downtimes unrelated to your system.

If the front-end system gets too complicated, also consider porting some of the logic code to subsystems and define a clear API for these subsystems. 

## Strike A Balance

Separating code into subsystems is not **always** the right choice. If you find yourself updating both the subsystem and the front-end for every change, the separation may become unhelpful overhead.

Separate UI logic to subsystems when the **contract** between them can make them somewhat autonomous. This is also where I would be careful with micro-frontends as they are **sometimes** the right approach, but they focus on the solution rather than on understanding your particular problem. 

## Testing UI Components: Divide And Conquer

The difficulty in testing UI components is a special case of the general difficulty in testing. The main issue with UI components is that their API and environments are often not properly defined. In the React world, components have some set of dependencies; some are “props,” and some are hooks (e.g., context or Redux). Components outside the React world often rely on globals instead, which is a different version of the same thing. When looking at the common React component code, the strategy of how to test it can be confusing.

Some of this is inescapable as UI testing is hard. But by dividing the problem in the following ways, we reduce it substantially.

### Separate UI From Logic

The main thing that makes testing component code easier is having less of it. Look at your component code and ask, does this part actually need to be connected to the document in any way? Or is it a separate unit/system that can be tested in isolation?

The more code you have as plain JavaScript “logic,” agnostic to a framework and unaware that it’s used by the UI, the less code you need to test in confusing, flaky, or costly ways. Also, this code is more portable and can be moved into a worker or to the server, and your UI code is more portable across frameworks because there is less of it.

### Separate UI Building Blocks From App Widgets

The other thing that makes UI code difficult to test is that components are very different from each other. For example, your app can have a “TheAppDashboard” component, which contains all the specifics of your app’s dashboard, and a “DatePicker” component, which is a general-purpose reusable widget that appears in many places throughout your app.

DatePicker is a **UI building block**, something that can be composed into the UI in multiple situations but doesn’t require a lot from the environment. It is not specific to the data of your own app.

TheAppDashboard, on the other hand, is an **app widget**. It probably doesn’t get re-used a lot throughout the application; perhaps it appears only once. So, it doesn’t require many parameters, but it does require a lot of information from the environment, such as data related to the purpose of the app.

### Testing UI Building Blocks

UI building blocks should, as much as possible, be **parametric** (or “prop-based” in React). They shouldn’t draw too much from the context (global, Redux, useContext), so they also should not require a lot in terms of per-component environment setup.

A sensible way to test parametric UI building blocks is to set up an environment once (e.g., a browser, plus whatever else they need from the environment) and run multiple tests without resetting the environment.

A good example for a project that does this is the [Web Platform Tests](https://github.com/web-platform-tests/wpt/) &mdash; a comprehensive set of tests used by the browser vendors to test interoperability. In many cases, the browser and the test server are set up once, and the tests can re-use them rather than have to set up a new environment with each test.

### Testing App Widgets

App widgets are **contextual** rather than **parametric.** They usually require a lot from the environment and need to operate in multiple scenarios, but what makes those scenarios different is usually something in the data or user interaction.

It’s tempting to test app widgets the same way we test UI building blocks: create some fake environment for them that satisfies all the different hooks, and see what they produce. However, those environments tend to be brittle, constantly changing as the app evolves, and those tests end up being stale and give an inaccurate view of what the widget is supposed to do.

The most reliable way to test contextual components is within their true context &mdash; the app, as seen by the user. Test those app widgets with UI integration tests and sometimes with e2e tests, but don’t bother unit-testing them by mocking the other parts of the UI or utils.

{{% ad-panel-leaderboard %}}

## Testable UI Cheat Sheet

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b92619-7eb0-4e1c-99f0-3715db758a58/1-frontend-testing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b92619-7eb0-4e1c-99f0-3715db758a58/1-frontend-testing.jpg" width="800" height="600" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b92619-7eb0-4e1c-99f0-3715db758a58/1-frontend-testing.jpg'>Large preview</a>)" alt="Testable UI Cheat Sheet" >}}

## Summary

Front-end testing is complex because often UI code is lacking in terms of separation of concerns. Business logic state-machines are entangled with framework-specific view code, and context-aware app widgets are entangled with isolated, parametric UI building blocks. When everything is entangled, the only reliable way to test is to test “everything” in a flaky and costly e2e test.

To manage this problem, rely on architecture rather than specific processes and tools:

- Convert some of your business-logic flows into **view-agnostic code** (e.g., state machines).
- **Separate building blocks from app widgets** and test them differently. 
- **Mock your backends and subsystems**, not other parts of your front-end. 
- Think and think again about your **system signatures and contracts**. 
- **Treat your testing code with respect.** It’s an important piece of your code, not an afterthought.

Striking the right balance between front-end and subsystems and between different strategies is a software architecture craft. Getting it right is difficult and requires experience. The best way to gain this kind of experience is by trying and learning. I hope this article helps a bit with learning!

*My gratitude to Benjamin Greenbaum and Yehonatan Daniv for reviewing this from the technical side.*

{{< signature "vf, yk, il" >}}
