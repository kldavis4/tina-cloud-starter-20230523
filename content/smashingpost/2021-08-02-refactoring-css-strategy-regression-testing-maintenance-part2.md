---
title: 'Refactoring CSS: Strategy, Regression Testing And Maintenance (Part 2)'
slug: refactoring-css-strategy-regression-testing-maintenance-part2
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1005065b-5daf-4b21-8ac6-89b91effa5b9/refactoring-css-strategy-regression-testing-maintenance-part2.jpg
date: 2021-08-02T11:00:00.000Z
summary: >-
  After analyzing CSS and its weaknesses, and management giving a green light to the refactoring project, it’s time to get to work. A team needs to agree on the internal code standards and best practices, plan out the refactoring strategy, and outline individual tasks. We need to set up a visual regression testing suite, and a maintenance plan to enforce the new standards and best practices in the future.
description: >-
  In this article, we’ll take a deep dive into the refactoring process itself, and cover incremental refactoring strategy, visual regression testing, and maintaining the refactored codebase.
categories:
  - CSS
  - Testing
  - Techniques
  - Refactoring
---

In [Part 1](https://www.smashingmagazine.com/2021/07/refactoring-css-introduction-part1/), we’ve covered the side effects of low-quality CSS codebase on end-users, development teams, and management. Maintaining, extending, and working with the low-quality codebase is difficult and often requires additional time and resources. Before bringing up the refactoring proposal to the management and stakeholders, it can be useful to back up the suggestion with some hard data about the **codebase health** &mdash; not only to convince the management department, but also have a measurable goal for the refactoring process.

Let’s assume that management has approved the CSS refactoring project. The development team has analyzed and pinpointed the weaknesses in the CSS codebase and has set target goals for the refactor (file size, specificity, color definitions, and so on). In this article, we’ll take a deep dive into the refactoring process itself, and cover incremental refactoring strategy, visual regression testing, and maintaining the refactored codebase.


<div class="c-felix-the-cat">
<h4 class="h3">Part Of: <a href="/category/refactoring/">CSS Refactoring</a></h4>
<ul>
<li>Part 1: <a href="/2021/07/refactoring-css-introduction-part1/">CSS Refactoring: Introduction</a></li>
<li>Part 2: <strong>CSS Refactoring: Strategy, Regression Testing And Maintenance</strong></li>
<li>Part 3: <a href="/2021/08/refactoring-css-optimizing-size-performance-part3/">CSS Refactoring: Optimizing Size And Performance</a></li>
<li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next ones.</li>
</ul>
</div>

## Preparation And Planning

Before starting the refactoring process, the team needs to go over the codebase issues [and](https://www.smashingmagazine.com/2021/07/refactoring-css-introduction-part1/#auditing-css-codebase-health) [CSS health audit data](https://www.smashingmagazine.com/2021/07/refactoring-css-introduction-part1/#auditing-css-codebase-health) (CSS file size, selector complexity, duplicated properties, and declarations, etc.) and discuss individual issues about how to approach them and what challenges to expect. These issues and challenges are specific to the codebase and can make the refactoring process or testing difficult. As concluded in the [previous article](https://www.smashingmagazine.com/2021/07/refactoring-css-introduction-part1/), it’s important to establish internal rules and codebase standards and keep them documented to make sure that the team is on the same page and has a more **unified and standardized approach to refactoring**.

The team also needs to outline the individual refactoring tasks and set the deadlines for completing the refactoring project, taking into account current tasks and making sure that refactoring project doesn’t prevent the team from addressing urgent tasks or working on planned features. Before estimating the time duration and workload of the refactoring project, the team needs to consult with the management about the short-term plans and adjust their estimates and workload based on the planned features and regular maintenance procedures.

Unlike regular features and bug fixes, the refactoring process yields little to no visible and measurable changes on the front end, and management cannot keep track of the progress on their own. It’s important to establish **transparent communication** to keep the management and other project stakeholders updated on the refactoring progress and results. Online collaborative workspace tools like [Miro](https://miro.com/) or [MURAL](https://www.mural.co/) can also be used for effective communication and collaboration between the team members and management, as well as a quick and simple task management tool.

Christoph Reinartz pointed out the importance of transparency and clear communication while the [team at trivago](https://tech.trivago.com/2016/02/02/large-scale-css-refactoring-at-trivago/) was working on the CSS refactoring project.

<blockquote>“Communication and clearly making the progress and any upcoming issues visible to the whole company were our only weapon. We decided to build up a very simple Kanban board, established a project stand-up and a project Slack channel, and kept management and the company up-to-date via our internal social cast network.”</blockquote>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cd05d84-1be6-4da6-9115-692cbcbadddc/1-refactoring-css-strategy-regression-testing-maintenance-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cd05d84-1be6-4da6-9115-692cbcbadddc/1-refactoring-css-strategy-regression-testing-maintenance-part2.png" width="800" height="450" sizes="100vw" caption="Simple, clear and effective Kanban board used for large scale CSS refactoring at trivago. (Image by <a href='https://tech.trivago.com/2016/02/02/large-scale-css-refactoring-at-trivago/'>trivago</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cd05d84-1be6-4da6-9115-692cbcbadddc/1-refactoring-css-strategy-regression-testing-maintenance-part2.png'>Large preview</a>)" alt="Simple, clear and effective Kanban board used for large scale CSS refactoring at trivago. (Image by trivago)" >}}

The most crucial element of planning the refactoring process is to keep the CSS refactoring task scope as small as possible. This makes the tasks more manageable, and easier to test and integrate.

Harry Roberts refers to these tasks as “[refactoring tunnels](https://csswizardry.com/2017/06/refactoring-tunnels/)”. For example, refactoring the entire codebase to follow the BEM methodology all at once can yield a massive improvement to the codebase and the development process. This might seem like a simple search-and-replace task at first. However, this task affects all elements on every page (high scope) and the team cannot “see the light at the end of the tunnel” right away; a lot of things can break in the process and unexpected issues can slow down the progress and **no one can tell when the task is going to be finished**. The team can spend days or weeks working on it and risk hitting a wall, accumulate additional technical debt, or making the codebase even less healthy. The team ends up either giving up on the task of starting over, wasting time and resources in the process.

By contrast, improving just the navigation component CSS is a smaller scope task and is much more manageable and doable. It is also easier to test and verify. This task can be done in a few days. Even with potential issues and challenges that slow down the task, there is a high chance of success. The team can always “see the end of the tunnel” while they’re working on the task because they know the task will be completed once the component has been refactored and all issues related to the component have been fixed.
 
Finally, the team needs to agree on the refactoring strategy and regression testing method. This is where the refactoring process gets challenging &mdash; refactoring should be as streamlined as possible and shouldn’t introduce any regressions or bugs. 

Let’s dive into one of the **most effective CSS refactoring strategies** and see how we can use it to improve the codebase quickly and effectively.

{{% feature-panel %}}

## Incremental Refactoring Strategy

Refactoring is a challenging process that is much more complex than simply deleting the legacy code and replacing it with the refactored code. There is also the matter of integrating the refactored codebase with the legacy codebase and avoiding regressions, accidental code deletions, preventing stylesheet conflicts, etc. To avoid these issues, I would recommend using an incremental (or granular) refactoring strategy.

In my opinion, this is one of the safest, most logical, and most recommended CSS refactoring strategies I’ve come across so far. Harry Roberts has [outlined this strategy](https://www.youtube.com/watch?v=fvTryZjGyg8) in 2017. and it has been my personal go-to CSS refactoring strategy since I first heard about it.

Let’s go over this strategy step by step.

### Step 1: Pick A Component And Develop It In Isolation

This strategy relies on individual tasks having low scope, meaning that we should refactor the project component by component. It’s recommended to start with low-scope tasks (individual components) and then move onto higher-scoped tasks (global styles).

Depending on the project structure and CSS selectors, individual component styles consist of a combination of component (class) styles and global (wide-ranging element) styles. Both component styles and global styles can be the source of the codebase issues and might need to be refactored. 

Let’s take a look at the **more common CSS codebase issues** which can affect a single component. Component (class) selectors might be too complex, difficult to reuse, or can have high specificity and enforce the specific markup or structure. Global (element) selectors might be greedy and leak unwanted styles into multiple components which need to be undone with high-specificity component selectors.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5a165e-537a-4554-819e-6b9e47ae134d/3-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5a165e-537a-4554-819e-6b9e47ae134d/3-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="281" sizes="100vw" caption="Starting state of the CSS and HTML codebase that we want to refactor. Card component markup consists of multiple HTML elements. Card component styles consist of a combination of class selector styles and global element selector styles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5a165e-537a-4554-819e-6b9e47ae134d/3-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Starting state of the CSS and HTML codebase that we want to refactor. Card component markup consists of multiple HTML elements. Card component styles consist of a combination of class selector styles and global element selector styles." >}}

After choosing a component to refactor (a lower-scoped task), we need to develop it in an isolated environment away from the legacy code, its weaknesses, and conflicting selectors. This is also a good opportunity to improve the HTML markup, remove unnecessary nestings, use better CSS class names, use ARIA attributes, etc. 

You don’t have to go out of your way to set up a whole build system for this, you can even use [CodePen](https://codepen.io/) to rebuild the individual components. To avoid conflicts with the legacy class names and to separate the refactored code from the legacy code more clearly, we’ll use an `rf-` prefix on CSS class name selectors.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af7ed03e-4d73-47ec-91a4-95294d593239/4-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af7ed03e-4d73-47ec-91a4-95294d593239/4-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="204" sizes="100vw" caption="Building refactored Card component CSS and Markup in isolation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af7ed03e-4d73-47ec-91a4-95294d593239/4-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Building refactored Card component CSS and Markup in isolation." >}}

### Step 2: Merge With The Legacy Codebase And Fix Bugs

Once we’ve finished rebuilding the component in an isolated environment, we need to replace the legacy HTML markup with refactored markup (new HTML structure, class names, attributes, etc.) and add the refactored component CSS alongside the legacy CSS.

We don’t want to act too hastily and remove legacy styles right away. By making too many changes simultaneously, we’ll lose track of the issues that might happen due to the conflicting codebases and multiple changes. For now, let’s replace the markup and add refactored CSS to the existing codebase and see what happens. Keep in mind that refactored CSS should have the `.rf-` prefix in their class names to prevent conflicts with the legacy codebase.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8896e361-f959-4004-b007-cec12612efaf/5-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8896e361-f959-4004-b007-cec12612efaf/5-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="407" sizes="100vw" caption="Replacing the legacy Card markup with refactored markup and adding refactored Card CSS alongside legacy styles. Legacy component and global styles apply unwanted side-effects due to the wide-reaching global or element selectors. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8896e361-f959-4004-b007-cec12612efaf/5-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Replacing the legacy Card markup with refactored markup and adding refactored Card CSS alongside legacy styles. Legacy component and global styles apply unwanted side-effects due to the wide-reaching global or element selectors." >}}

Legacy component CSS and global styles can cause unexpected side-effects and leak unwanted styles into the refactored component. Refactored codebase might be missing the faulty CSS which was required to undo these side-effects. Due to those styles having a wider reach and possibly affecting other components, we cannot simply edit the problematic code directly. We need to use a different approach to tackle these conflicts.

We need to create a separate CSS file, which we can name `overrides.css` or `defend.css` which will contain hacky, high-specificity code that combats the unwanted leaked styles from the legacy codebase.

`overrides.css` which will contain high-specificity selectors which make sure that the refactored codebase works with the legacy codebase. This is only a temporary file and it will be removed once the legacy code is deleted. For now, add the high-specificity style overrides to unset the styles applied by legacy styles and test if everything is working as expected.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d821412-5eea-4ccd-a969-84b91b99d5bf/6-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d821412-5eea-4ccd-a969-84b91b99d5bf/6-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="559" sizes="100vw" caption="We are adding <code>overrides.css</code> to combat the unwanted side-effects. This file contains high-specificity code that overrides the legacy styles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d821412-5eea-4ccd-a969-84b91b99d5bf/6-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="We are adding overrides.css to combat the unwanted side-effects. This file contains high-specificity code that overrides the legacy styles." >}}

If you notice any issues, check if the refactored component is missing any styles by going back to the isolated environment or if any other styles are leaking into the component and need to be overridden. If the component looks and works as expected after adding these overrides, remove the legacy code for the refactored component and check if any issues happen. Remove related hacky code from `overrides.css` and test again. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce07ddae-979c-4d8d-9e00-7825cb52613f/7-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce07ddae-979c-4d8d-9e00-7825cb52613f/7-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="384" sizes="100vw" caption="Legacy Card component styles can now be safely removed, alongside with (some) styles from <code>overrrides.css</code> which helped combat the side-effects from those selectors. However, global CSS selectors may still apply unwanted side-effects so we cannot completely remove this file until we’ve refactored global styles also. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce07ddae-979c-4d8d-9e00-7825cb52613f/7-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Legacy Card component styles can now be safely removed, alongside with (some) styles from overrrides.css which helped combat the side-effects from those selectors. However, global CSS selectors may still apply unwanted side-effects so we cannot completely remove this file until we’ve refactored global styles also." >}}

Depending on the case, you probably won’t be able to remove every override right away. For example, if the issue lies within a global element selector which leaks styles into other components that also need to be refactored. For those cases, we won’t risk expanding the scope of the task and the pull request but rather **wait until all components have been refactored** and tackle the high-scope tasks after we’ve removed the same style dependency from all other components.

In a way, you can treat the `overrides.css` file as your makeshift TODO list for refactoring greedy and wide-reaching element selectors. You should also consider updating the task board to include the newly uncovered issues. Make sure to add useful comments in the `overrides.css` file so other team members are on the same page and instantly know why the override has been applied and in response to which selector.

<pre><code class="language-css">/* overrides.css */
/* Resets dimensions enforced by ".sidebar > div" in "sidebar.css" */
.sidebar > .card {
  min-width: 0;
}

/* Resets font size enforced by ".hero-container" in "hero.css"*/
.card {
  font-size: 18px;
}
</code></pre>

### Step 3: Test, Merge And Repeat

Once the refactored component has been successfully integrated with the legacy codebase, create a Pull Request and run an automated visual regression test to catch any issues that might have gone unnoticed and fix them before merging them into one of the main git branches. Visual regression testing can be treated as the last line of defense before merging the individual pull requests. We’ll cover visual regression testing in more detail in one of the upcoming sections of this article.

Now rinse and repeat these three steps until the codebase has been refactored and `overrides.css` is empty and can be safely removed.

### Step 4: Moving From Components To Global Styles

Let’s assume that we have refactored all individual low-scoped components and all that is left in the `overrides.css` file are related to global wide-reaching element selectors. This is a very realistic case, speaking from the experience, as many CSS issues are caused by wide-reaching element selectors leaking styles into multiple components.

By tackling the individual components first and shielding them from the global CSS side-effects using `overrides.css` file, we’ve made these higher-scoped tasks much more manageable and less risky to do. We can move onto refactoring global CSS styles more safely than before and remove duplicated styles from the individual components and replacing them with general element styles and utilities &mdash; buttons, links, images, containers, inputs, grids, and so on. By doing so, we’re going to incrementally remove the code from our makeshift TODO `overrides.css` file and duplicated code repeated in multiple components.

Let’s apply the same three steps of the incremental refactoring strategy, starting by developing and testing the styles in isolation.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ef08ea8-4d4c-4238-be9b-e21b2fe5a70e/8-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ef08ea8-4d4c-4238-be9b-e21b2fe5a70e/8-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="182" sizes="100vw" caption="Refactoring global styles in isolation. If these global styles are using element selectors without any special markup or class name applied, then markup won’t change and only the refactored CSS needs to be moved to the codebase. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ef08ea8-4d4c-4238-be9b-e21b2fe5a70e/8-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Refactoring global styles in isolation. If these global styles are using element selectors without any special markup or class name applied, then markup won’t change and only the refactored CSS needs to be moved to the codebase." >}}

Next, we need to add the refactored global styles to the codebase. We might encounter the same issues when merging the two codebases and we can add the necessary overrides in the `overrides.css`. However, this time, we can expect that as we are gradually removing legacy styles, we will also be able to gradually remove overrides that we’ve introduced to combat those unwanted side-effects.

The **downside of developing components in isolation** can be found in element styles that are shared between multiple components &mdash; style guide elements like buttons, inputs, headings, and so on. When developing these in isolation from the legacy codebase, we don’t have access to the legacy style guide. Additionally, we don’t want to create those dependencies between the legacy codebase and refactored codebase.

That is why it’s easier to remove the duplicated code blocks and move these styles into separate, more general style guide components and selectors later on. It allows us to address these changes right at the end and with the lower risk as we are working with a much healthier and consistent codebase, instead of the messy, inconsistent, and buggy legacy codebase. Of course, any unintended side-effects and bugs can still happen and these should be caught with the visual regression testing tools which we’ll cover in one of the following sections of the article.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e87fa4c-2750-49c8-94db-7fdf06298e1f/9-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e87fa4c-2750-49c8-94db-7fdf06298e1f/9-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="509" sizes="100vw" caption="Merging the refactored global CSS with the codebase and updating <code>overrides.css</code> to remove unwanted side-effects of the legacy codebase. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e87fa4c-2750-49c8-94db-7fdf06298e1f/9-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Merging the refactored global CSS with the codebase and updating overrides.css to remove unwanted side-effects of the legacy codebase." >}}

When the codebase has been completely refactored and we’ve removed all makeshift TODO items from the `overrides.css` file, we can safely remove it and we are left with the refactored and improved CSS codebase.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bed7a19f-1d3c-4f29-bfad-285eb3f42184/10-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bed7a19f-1d3c-4f29-bfad-285eb3f42184/10-refactoring-css-strategy-regression-testing-maintenance-part2.jpg" width="800" height="291" sizes="100vw" caption="Removing legacy global styles and <code>overrides.css</code> once the codebase has been completely refactored. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bed7a19f-1d3c-4f29-bfad-285eb3f42184/10-refactoring-css-strategy-regression-testing-maintenance-part2.jpg'>Large preview</a>)" alt="Removing legacy global styles and overrides.css once the codebase has been completely refactored." >}}

{{% ad-panel-leaderboard %}}

## Incremental CSS Refactoring Example

Let’s use the incremental refactoring strategy to refactor a simple page that consists of a title element and two card components in a grid component. Each card element consists of an image, title, subtitle, description, and a button and is placed in a 2-column grid with horizontal and vertical spacing.

{{< codepen height="480" theme_id="light" slug_hash="KKmRaQJ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 1](https://codepen.io/smashingmag/pen/KKmRaQJ) by <a href="hhttps://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

As you can see, we have a suboptimal CSS codebase with various specificity issues, overrides, duplicated code, and some cases of undoing styles.

<pre><code class="language-css">h1, h2 {
    margin-top: 0;
    margin-bottom: 0.75em;
    line-height: 1.3;
    font-size: 2.5em;
    font-family: serif;
}

/* ... */

.card h2 {
  font-family: Helvetica, Arial, sans-serif;
  margin-bottom: 0.5em;
  line-height: initial;
  font-size: 1.5em;
}</code></pre>

The `.card` component also uses high specificity selectors which enforces a specific HTML structure and allows styles to leak into other elements inside the card components.

<pre><code class="language-css">/* Element needs to follow this specific HTML structure to have these styles applied */
.card h2 &gt; small {
 /* ... */
}

/* These styles will leak into all div elements in a card component */
.card div {
  padding: 2em 1.5em 1em;
}

/* These styles will leak into all p elements in a card component */
.card p {
  font-size: 0.9em;
  margin-top: 0;
}</code></pre>

We’ll start with the lowest scoped and topmost children components, so let’s refactor the card component which is the topmost child of the page, i.e. the card component is a child of the grid component. We’ll develop the card component in isolation and use the agreed standards and best practices.

We’ll use BEM to replace the greedy wide-reaching selectors with simple class selectors and use CSS custom properties to replace the inconsistent, hard-coded inline color values. We’ll also add some CSS to help us develop the component, which we won’t copy to the existing codebase.

{{< codepen height="480" theme_id="light" slug_hash="JjNvELK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 2 (isolated card component)](https://codepen.io/smashingmag/pen/JjNvELK) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

We are using the `rf-` prefix for the new CSS classes so we can avoid class name conflicts and differentiate the refactored styles from legacy styles for better code organization and simpler debugging. This will also allow us to keep track of the refactoring progress.

<pre><code class="language-css">.rf-card {
  color: var(--color-text);
  background: var(--color-background);
}

.rf-card__figure {
  margin: 0;
}

.rf-card__title {
  line-height: 1.3;
  margin-top: 0;
  margin-bottom: 0.5em;
}</code></pre>

We are going to replace the legacy markup with the refactored markup, and add the refactored styles to the CSS codebase. We are not going to remove the legacy styles just yet. We need to check if any styles from other legacy selectors have leaked into the refactored component.

Due to the issues with global wide-ranging selectors, we have some unwanted style overrides leaking into the refactored component &mdash; title font properties have been reset and font size inside the card component has changed.

<pre><code class="language-css">.grid {
  /* ... */
  font-size: 24px;
}

h1, h2 {
    /* ... */
    font-size: 2.5em;
    font-family: Georgia, "Times New Roman", Times, serif;
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="NWjMdYO" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 3 (merge legacy and refactor)](https://codepen.io/smashingmag/pen/NWjMdYO) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

We need to add style overrides to overrides.css to remove the unwanted side-effects from other selectors. We’re also going to comment on each override so we know which selector has caused the issue. 

<pre><code class="language-css">/* Prevents .grid font-size override  */
.rf-card  {
  font-size: 16px;
}

/* Prevents h1, h2 font override  */
.rf-card__title {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 1.5em;
}</code></pre>

We now know that we are going to have to refactor the `.grid` component and global h1, h2 selector at some point. This is why we can treat it as a TODO list - these leaked styles can cause issues in other components, they are objectively faulty, and are applying styles that are being reset in the majority of use-cases.

{{< codepen height="480" theme_id="light" slug_hash="zYwjNjG" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 4 (adding overrides.css)](https://codepen.io/smashingmag/pen/zYwjNjG) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Let’s remove the legacy `.card` styles from the project and see if everything looks alright. We can check if we can remove any styles from `overrides.css`, however, we know right away that none of the overrides are related to legacy card component styles, but other components and element selectors.

{{< codepen height="480" theme_id="light" slug_hash="yLbjgjW" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 5 (Removing legacy component styles)](https://codepen.io/smashingmag/pen/yLbjgjW) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Now that the card component has been refactored, let’s check our makeshift TODO list and see what to tackle next. We have a choice between:

- Refactor the grid component &mdash; lower scope (short tunnel),
- Refactor global styles &mdash; higher scope (longer tunnel).

We’ll go with the lowest scope component, the grid component in this case, and apply the same approach. We’ll start by developing the grid component in isolation. We can use the card component markup for testing, card component styles won’t affect the grid and won’t help us develop the component, so we can leave them out of the isolated component for a simpler CSS markup.

{{< codepen height="480" theme_id="light" slug_hash="JjNvEZK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 6 (refactoring grid component)](https://codepen.io/smashingmag/pen/JjNvEZK) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Let’s replace the grid HTML markup with the refactored markup and add the refactored styles to the CSS codebase and check if we need to add any styles to `overrides.css` to mitigate any stylesheet conflicts or leaked styles.

{{< codepen height="480" theme_id="light" slug_hash="KKmRaeE" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 7 (merged grid component, updated overrides.css, removed styles)](https://codepen.io/smashingmag/pen/KKmRaeE) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

We can see that no new issues appeared, so we can proceed with removing the legacy `.grid` styles. Let’s also check if `overrides.css` contains any styles that are applied for the legacy `.grid` selector.

<pre><code class="language-css">/* Reset .grid font-size override */
.rf-card  {
  font-size: 16px;
}</code></pre>

This is why it’s useful to document the override rules. We can safely remove this selector and move it onto the last item in our makeshift TODO list &mdash; heading element selectors. We’re going to go through the same steps again &mdash; we’ll create a refactored markup in isolation, replace the HTML markup and add the refactored styles to the stylesheet. 

<pre><code class="language-html">&lt;h1 class="rf-title rf-title--size-regular rf-title--spacing-regular"&gt;Featured galleries&lt;/h1&gt;</code></pre>

<pre><code class="language-css">.rf-title {
   font-family: Georgia, "Times New Roman", Times, serif;
}

.rf-title--size-regular {
    line-height: 1.3;
    font-size: 2.5em;
}

.rf-title--spacing-regular {
    margin-top: 0;
    margin-bottom: 0.75em;
}</code></pre>

We’ll check if there are any issues and confirm that no new issues were introduced by the updated markup and stylesheet and we’ll remove the legacy `h1, h2` selector from the stylesheet. Finally, we’re going to check `overrides.css` and remove the styles related to the legacy element selector.

{{< codepen height="480" theme_id="light" slug_hash="VwbxPBW" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 8 (element selectors)](https://codepen.io/smashingmag/pen/VwbxPBW) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

The `overrides.css` is now empty and we’ve refactored the card, grid, and title components in our project. Our codebase is much more healthier and consistent compared to the starting point &mdash; we can add elements to the grid component and new title variations without having to undo the leaked styles.

However, **there are a few tweaks we can do to improve our codebase**. As we’ve developed the components in isolation, we’ve probably re-built the same style guide components multiple times and created some duplicated code. For example, a button is a style guide component and we’ve scoped these styles to a card component.

<pre><code class="language-css">/* Refactored button styles scoped to a component */
.rf-card__link {
  color: var(--color-text-negative);
  background-color: var(--color-cta);
  padding: 1em;
  display: flex;
  justify-content: center;
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: 600;
}</code></pre>

If any other component is using the same button styles, it means that we’re going to write the same styles each time we develop them in isolation. We can refactor these duplicates into a separate `.button` component and replace the duplicated scoped styles with general style guide styles.  However, we already have a legacy `.button` selector which needs to be refactored, so we’re also able to remove the legacy button selector.

Even though we’re moving onto refactoring higher scoped elements, the codebase is much healthier and consistent compared to the starting point, so the risk is lower and the task is much more doable. We also don’t have to worry that the changes in the topmost child components will override any changes to the general selector.

<pre><code class="language-css">/* Faulty legacy button styles */
.button {
  border: 0;
  display: block;
  max-width: 200px !important;
  text-align: center;
  margin: 1em auto;
  padding: 1em;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  cursor: pointer;
  font-weight: bold;
  text-decoration: none;
}

.cta {
  max-width: none !important;
  margin-bottom: 0;
  color: #fff;
  background-color: darkred;
  margin-top: 1em;
}</code></pre>

We can use the same incremental approach to the We’re going to rebuild the button component in isolation, update the markup, and add the refactored styles to the stylesheet. We’re going to do a quick check for stylesheet conflicts and bugs, notice that nothing has changed, and remove the legacy button markup and the component-scope button styles.

<pre><code class="language-css">.rf-button {
  display: flex;
  justify-content: center;
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: 600;
}

.rf-button--regular {
   padding: 1em;
}

.rf-button--cta {
  color: var(--color-text-negative);
  background-color: var(--color-cta);
}</code></pre>

<pre><code class="language-css">/* Before - button styles scoped to a card component */
&lt;a class="rf-card__link" href="#"&gt;View gallery&lt;/a&gt;

/* After - General styles from a button component */
&lt;a class="rf-button rf-button--regular rf-button--cta" href="#"&gt;View gallery&lt;/a&gt;</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="yLbjgqd" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Refactoring CSS — example 9 (final result)](https://codepen.io/smashingmag/pen/yLbjgqd) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Once the refactoring project has been completed, we can use search-and-replace to clean up the `rf-` prefixes in the codebase and treat the existing codebase as the new standard. That way, extending the codebase won’t introduce naming inconsistencies or force the `rf-` prefix naming that could cause issues for any future refactors.

{{% ad-panel-leaderboard %}}

## Testing And Avoiding Regressions

Regardless of the refactor tasks' scope size and how well the team follows the incremental refactoring strategy steps, bugs and regressions can happen. Ideally, We want to avoid introducing issues and regressions in the codebase &mdash; conflicting styles, missing styles, incorrect markup, leaked styles from other elements, etc. 

Using automated visual regression testing tools like [Percy](https://percy.io/) or [Chromatic](https://www.chromatic.com/) on a Pull Request level can speed up testing, allow developers to address regressions quickly and early, and **make sure that the bugs don’t end up on the live site**. These tools can take screenshots of individual pages and components and compare changes in style and layout and notify developers of any visual changes that can happen due to changes in the markup or CSS. 

Since the CSS refactor process shouldn’t result in any visual changes in usual cases and depending on the task and issues in the legacy codebase, the visual regression testing process can potentially be simple as checking if any visual changes happened at all and checking if these changes were intentional or unintentional.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3646bf6c-a2be-4be3-b7cc-335a27894924/11-refactoring-css-strategy-regression-testing-maintenance-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3646bf6c-a2be-4be3-b7cc-335a27894924/11-refactoring-css-strategy-regression-testing-maintenance-part2.png" width="800" height="419" sizes="100vw" caption="Visual regression test example in <a href='https://www.chromatic.com/'>Chromatic</a>. Dimensions for this specific button variation have been unintentionally changed when the button component has been refactored. This issue has been caught when Pull Request has been created, so developers were able to address this issue early. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3646bf6c-a2be-4be3-b7cc-335a27894924/11-refactoring-css-strategy-regression-testing-maintenance-part2.png'>Large preview</a>)" alt="Visual regression test example in Chromatic. Dimensions for this specific button variation have been unintentionally changed when the button component has been refactored. This issue has been caught when Pull Request has been created, so developers were able to address this issue early." >}}

Depending on the project, testing tools don’t need to be complex or sophisticated to be effective. While working on [refactoring the Sundance Institute’s](https://www.kirbyyardley.com/work/sundance-design-system) CSS codebase, the development team used a simple static style guide page generated by Jekyll to test the refactored components.

<blockquote>“One unintended consequence of executing the refactor in abstraction on a Jekyll instance was that we could now publish it to Github pages as a <a href="https://sundance-org.github.io/styles/cards/">living style guide</a>. This has become an invaluable resource for our dev team and for external vendors to reference.”</blockquote>

Once the CSS refactor tasks have been completed and the refactored code is ready for production, the team can also consider doing an **A/B test to check the effect of the refactored codebase on users**. For example, if the goal of the refactoring process was to reduce the overall CSS file size, the A/B test can potentially yield significant improvements for mobile users, and these results can also be beneficial to project stakeholders and management. That’s exactly how the [team at Trivago](https://tech.trivago.com/2016/02/02/large-scale-css-refactoring-at-trivago/) approached the deployment of their large-scale refactoring project.

<blockquote>“(…) we were able to release the technical migration as an A/B Test. We tested the migration for one week, with positive results on mobile devices where mobile-first paid out and accepted the migration after only four weeks.”</blockquote>

## Keeping Track Of Refactoring Progress

Kanban board, GitHub issues, GitHub project board, and standard project management tools can do a great job of keeping track of the refactoring progress. However, depending on the tools and how the project is organized, it may be difficult to estimate the progress on a per-page basis or do a quick check on which components need to be refactored.

This is where our `.rf`-prefixed CSS classes come in. Harry Roberts has talked about the [benefits of using the prefix](https://www.youtube.com/watch?v=fvTryZjGyg8) in detail. The bottom line is &mdash; not only do these classes allow developers to **clearly separate the refactored CSS codebase from the legacy codebase**, but also to quickly show the progress to the project managers and other project stakeholders on a per-page basis.

For example, management may decide to test the effects of the refactored codebase early by deploying only the refactored homepage code and they would want to know when the homepage components will be refactored and ready for A/B testing.

Instead of wasting some time comparing the homepage components with the available tasks on the Kanban board, developers can just temporarily add the following styles to highlight the refactored components which have the `rf-` prefix in their class names, and the components that need to be refactored. That way, they can reorganize the tasks and prioritize refactoring homepage components.

<pre><code class="language-css">/* Highlights all refactored components */
[class*="rf-"] {
  outline: 5px solid green;
}

/* Highlights all components that havent been refactored */
[class]:not([class*="rf-"]),
body *:not([class]) {
  outline: 5px solid red;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eb881b0-0e6c-4cda-8216-725e8948fb29/13-refactoring-css-strategy-regression-testing-maintenance-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eb881b0-0e6c-4cda-8216-725e8948fb29/13-refactoring-css-strategy-regression-testing-maintenance-part2.png" width="800" height="412" sizes="100vw" caption="Previous example of refactored card component with temporary highlight code added. Components that have been refactored are highlighted with the green outline, while components that may need to be refactored are highlighted with the red outline. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eb881b0-0e6c-4cda-8216-725e8948fb29/13-refactoring-css-strategy-regression-testing-maintenance-part2.png'>Large preview</a>)" alt="Previous example of refactored card component with temporary highlight code added. Components that have been refactored are highlighted with the green outline, while components that may need to be refactored are highlighted with the red outline." >}}

## Maintaining The Refactored Codebase

After the refactoring project has been completed, the team needs to make sure to maintain the codebase health for the foreseeable future &mdash; new features will be developed, some new features might even be rushed and produce technical debt, various bugfixes will also be developed, etc. All in all, the development team needs to make sure that the codebase health remains stable as long as they’re in charge of the codebase.

Technical debt which can result in potentially faulty CSS code should be isolated, documented, and implemented in a [separate CSS file](https://csswizardry.com/2013/04/shame-css/) which is often named as `shame.css`.

**It’s important to document the rules and best practices** that were established and applied during the refactoring projects. Having those rules in writing allows for standardized code reviews, faster project onboarding for new team members, easier project handoff, etc.

Some of the rules and best practices can also be enforced and documented with automated code-checking tools like [stylelint](https://stylelint.io/). Andrey Sitnik, the author of widely-used CSS development tools like PostCSS and Autoprefixer, has noted how automatic linting tools can make code reviews and onboarding [easier and less stressful](https://evilmartians.com/chronicles/five-years-of-postcss-state-of-the-union).

<blockquote>“However, automatic linting is not the only reason to adopt Stylelint in your project. It can be extremely helpful for onboarding new developers on the team: a lot of time (and nerves!) are wasted on code reviews until junior developers are fully aware of accepted code standards and best practices. Stylelint can make this process much less stressful for everyone.”</blockquote>

Additionally, the team can create a [Pull Request template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository) and include the checklist of standards and best practices and a link to the project code rules document so that the developers making the Pull Request can check the code themselves and make sure that it follows the agreed standards and best practices.

## Conclusion

Incremental refactoring strategy is one of the safest and most recommended approaches when it comes to refactoring CSS. The development team needs to refactor the codebase component by component to ensure that the tasks have a low scope and are manageable. Individual components need to be then developed in isolation &mdash; away from the faulty code &mdash; and then merged with the existing codebase. The issues that may come up from the conflicting codebases can be solved by adding a temporary CSS file that contains all the necessary overrides to **remove the conflicts in CSS styles**. After that, legacy code for the target component can be removed and the process continues until all components have been refactored and until the temporary CSS file which contains the overrides is empty.

Visual regression testing tools like Percy and Chromatic can be used for testing and to detect any regressions and unwanted changes on the Pull Request level, so developers can fix these issues before the refactored code is deployed to the live site.

Developers can use A/B testing and use monitoring tools to make sure that the refactoring doesn’t negatively affect performance and user experience before finally launching the refactored project on a live site. Developers will also need to ensure that the agreed standards and best practices are used on the project continues to maintain the codebase health and quality in the future.


<div class="c-felix-the-cat">
<h4 class="h3">Part Of: <a href="/category/refactoring/">CSS Refactoring</a></h4>
<ul>
<li>Part 1: <a href="/2021/07/refactoring-css-introduction-part1/">CSS Refactoring: Introduction</a></li>
<li>Part 2: <strong>CSS Strategy, Regression Testing And Maintenance</strong></li>
<li>Part 3: <a href="/2021/08/refactoring-css-optimizing-size-performance-part3/">Optimizing Size And Performance</a></li>
<li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next ones.</li>
</ul>
</div>

### References

- “[Refactoring CSS Without Losing Your Mind](https://www.youtube.com/watch?v=fvTryZjGyg8),” Harry Roberts (Video, WeAreDevelopers Conference, 2017)
- “[Large Scale CSS Refactoring At Trivago](https://tech.trivago.com/2016/02/02/large-scale-css-refactoring-at-trivago/),” Christoph Reinartz
- “[Refactoring Tunnels](https://csswizardry.com/2017/06/refactoring-tunnels/),” Harry Roberts
- “[Sundance.org Design System And CSS Refactor](https://www.kirbyyardley.com/work/sundance-design-system),” Kirby Yardley
- “[Five Years Of PostCSS: State Of The Union](https://evilmartians.com/chronicles/five-years-of-postcss-state-of-the-union),” Andrey Sitnik

{{< signature "vf, yk, il" >}}
